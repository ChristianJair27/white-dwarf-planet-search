# Vetting fixes after the 2026-11-24 review, and a Gaia DR4 plan

Written by the programador agent, 2026-11-24. Follows `research/reports/2026-11-24-what-is-new.md` (section 3,
"What the vetting taught us about the pipeline") and backlog item 2c. Code: `wdplanets/vetting.py` (changed),
`tests/test_vetting.py` (new), `logs/fix_neighbour_notes_2026-11-24.py`, `logs/revet_summary_2026-11-24.py`,
`wdplanets/labs/dr4_common.py`, `dr4_photometry.py`, `dr4_astrometry.py`, `dr4_variability.py` (new).
Plan: `research/notes/gaia-dr4-plan.md`.

## Summary

The four pipeline problems found this morning are fixed in `wdplanets/vetting.py` and covered by 14 offline
tests (all pass):

1. `python -m wdplanets.vetting` now writes the verdict into `research/targets.csv` (re-read just before the
   write, integer columns kept, atomic replace).
2. The physical duration limit now uses each star's Gaia mass and radius, and a box scan from 4 min to 4 h at the
   survey period measures how long the dip really lasts; a dip longer than 2x the longest possible transit, on a
   crowded pixel, is a blend (`false_positive`). On a clean pixel (CROWDSAP >= 0.8 and <= 10 % neighbour light) it
   is left to an agent, because debris clouds also make hour-long dips.
3. A shared-period veto: `research/period_table.csv` (7,945 rows: the survey's best period for 2,153 stars per
   TESS sector; 8,053 rows / 2,182 stars after the final rebuild) and a Poisson test against the local density of periods. Over all 2,153 stars it flags exactly
   the 9 stars of the 10.961-d Sector 72 cluster and nothing else.
4. The Gaia neighbour query checks its answer (the white dwarf itself must be in it, no Source = 0, no
   G = 999999999) and falls back to the ESA Gaia TAP and then ARI Heidelberg; if every service fails the
   contamination is "unknown", never 0 %. 76 vetting notes (2026-10-22 to 2026-11-24, not only 11-09/10) had a
   failed query; all 76 are corrected: 31 of them actually have > 50 % of the pixel light from neighbours.

Re-vetting all 133 past signals (dry run, nothing overwritten): the new tests alone decide 6 verdicts, all
stars that agents had already rejected by hand as blends; nothing real is vetoed: WD 1856+534 b stays `vetted`
and is still recovered by `python -m wdplanets.validate`. One honest cost: on the real debris white dwarf
ZTF J0328-1219 the blend test fires at its 11.2-h period (not at 9.937 h), see Limitations.

The running survey process imported the old `vetting.py` when it started (2026-11-23 18:24); **the new vetting
applies to the survey only after its next restart**, which was not done here.

Gaia DR4 (2026-12-02): the plan and four code stubs are ready; the whole white-dwarf programme needs about 2 GB.

## Data

- `research/targets.csv` (2,263-2,300 rows during the work; the survey kept appending), `research/notes/*.md`,
  `research/survey_heartbeat.json` (fresh throughout, < 5 min; the survey was not touched).
- TESS SPOC light curves from the survey cache `data/tess/` (10,780 files; the sector list per TIC is read from
  the cache directory names).
- Gaia DR3 `gaia_source` cones of 21" through the Harvard VizieR mirror (`I/355/gaiadr3`), the ESA Gaia TAP
  (`https://gea.esac.esa.int/tap-server/tap`) and ARI Heidelberg (`https://gaia.ari.uni-heidelberg.de/tap`);
  SIMBAD and VSX (Harvard mirrors), TIC (MAST), as in the existing vetting.
- Gentile Fusillo et al. (2021) masses and log g of the 100 pc sample (`wdplanets.catalog`).
- Gaia DR4 documentation: ESA pages listed in the plan note and the draft DR4 data model of 2026-06-26
  (`data/dr4_prerelease/`, downloaded from the ESA public FTP).

## Method

**1. Status.** `main()` calls `update_status(name, verdict)` after `write_note`. `--all` re-vets every row with a
signal (candidate, vetted, known, false_positive) as a dry run: evidence to `data/labs/revet_<date>/<name>.json`,
no note or status written. `--no-catalogs` skips the network look-ups; `--periods` rebuilds the period table.

**2. Duration and blends.** R_wd = sqrt(G M / g) from the Gaia MassH and loggH (0.6 Msun / 0.013 Rsun if
missing), as in `wdplanets/inject.py`. The longest transit is P/pi x arcsin((R_wd + R_body)/a), R_body = 1.2
Jupiter radii (the existing convention), circular orbit. The duration scan runs `BoxLeastSquares` at the fixed
survey period with free epoch for boxes of 4, 8, 15, 30, 45, 60, 90, 120, 180, 240 min (shorter than half the
period and not shorter than the cadence), on the same detrended flux the survey searched, as in
`wdplanets/labs/vet_extra.py`. Blend: best box > 2 x the longest transit (BLEND_RATIO, allows e ~ 0.5 and the
coarse grid), S/N >= 5, and S/N > 1.1 x the best box within the limit. Verdict `false_positive` unless the pixel
is clean (above).

**3. Shared periods.** For the candidate's sectors, the pool is every other star in the table with a sector in
common and more than 120" away (pairs inside one TESS pixel can share a real signal). n = stars with
|P_i/P - 1| < 0.1 %; the expected number is the count in the 0.1-5 % window scaled by width; flag if n >= 3 and
the Poisson probability < 1e-4 (2,153 stars tested, so this is ~0.2 false flags expected at most).

**4. Neighbours.** `gaia_field()` tries VizieR -> ESA -> ARI and accepts an answer only if `neighbours_check`
passes; the white dwarf is identified by its Gaia DR3 source id, so a real companion within 1.5" now counts as
contamination (e.g. WDJ011044.68+275815.74: 47 %, a G = 16.41 source at 1.4"). TAP answers are read as CSV
(binary VOTable int64 source ids overflow astropy's C long on Windows - found while testing). Affected notes =
neighbour table with G = 999999999 (corrupt) or with zero sources (the white dwarf itself missing); each was
re-queried and its neighbour line and table rewritten, with a dated "Correction 2026-11-24 (neighbour table)"
section (`logs/fix_neighbour_notes_all.json`).

**5. Tests and checks.** `tests/test_vetting.py` (pytest, offline, synthetic light curves built with the survey's
own transit model from `inject.py`): star-specific limit; a 2-h, 1 % eclipse at 2.46 d is flagged; four
physical transits (WD 1856 b-like 10 R_earth at 1.41 d, 1 R_earth at 0.3 d, 3 R_earth at 5 d with b = 0.8,
10 R_earth at 9 d) are not; shared-period flags a synthetic 10.96-d cluster but not another sector, an ordinary
period or a close pair; neighbour fallback order, NaN (never 0) when all fail, the 1.4" companion; `main()`
writes the status and keeps integer columns; `vet()` end to end: blend veto on a crowded pixel, agent note on a
clean one. Then `python -m wdplanets.validate` and the dry-run re-vet of all 133 rows with a signal (4 parallel
shards; one hung for an hour on a MAST read without timeout and was restarted; `vetting` now sets a 300-s socket
timeout when run from the command line).

## Results

### 1. Unit tests

`python -m pytest tests -q`: **14 passed** (157 s on the loaded machine).

### 2. Validation

`python -m wdplanets.validate` (transits.py was not changed; run as a check): **WD 1856+534 b recovered**
in both runs (07:31 and 08:28): P = 1.407939 d (published 1.4079405 d), SDE 51.0, depth S/N 46.2, 87 transits in
Sectors 79-86 (all six at 20 s); with 2-min data only P = 1.407935 d, SDE 55.1. Both runs then stopped in the
second, reported-only check (ZTF J0328-1219) on a MAST read timeout (`validate.py` had no socket timeout; a 300-s one is now set); the
same TESS data were read later by `logs/ztf0328_blend_check.py` (Limitations).

With the new vetting, WD 1856+534 b (WDJ185739.34+533033.30) stays `vetted` by the automatic tests: best box 4 min
(S/N 45.8), the longest possible transit for this star is 20.5 min, no blend flag, 0 of 411 stars share its
period, 3 % neighbour light. (Its `targets.csv` status is `known`, set by an agent, and is not changed.)

### 3. Shared-period table

Of 2,153 stars, 9 are flagged, all at P = 10.9611-10.9619 d with Sector 72 in common (8-10 matches each, 0.3-0.6
expected, p = 2e-10 to 5e-8): 5 already `false_positive`, 2 `known` (the catalogued variable is real but the
10.96-d period is the artefact), 2 `searched` (below the candidate thresholds). No other period is flagged.

### 4. Re-vetting every past signal (dry run)

All 133 rows of `targets.csv` that ever had a signal (92 `false_positive`, 41 `known` at the start; evidence in
`data/labs/revet_2026-11-24/`, summary in `logs/revet_summary_2026-11-24.json`):

| | false_positive | known | vetted |
|---|---|---|---|
| old automatic tests only (same run) | 98 | 26 | 9 |
| with the new tests | 104 | 26 | **3** |

- **The new tests decide 6 verdicts**, all `vetted` -> `false_positive` by the blend test, and all six had
  already been rejected by agents: WDJ071546.90-385201.36, WDJ075356.62-252401.48, WDJ000855.80+364559.19,
  WDJ033320.37+000720.65, WDJ191850.20+333602.29 (the five named this morning) and WDJ034511.83+194026.08
  (2026-10-05). Best boxes 90-240 min against limits of 22-36 min.
- **Nothing real is vetoed.** The 3 rows left `vetted` are WD 1856+534 b (the real planet; best box 4 min),
  WDJ022111.49+533330.39 (the CROWDSAP 0.003 artefact that only the SAP test catches, still not in
  `vetting.py`) and WDJ061000.36+281428.37 (rejected by an agent on 2026-10-05; 68 % neighbour light).
- The blend flag fires on 85 rows: 62 already `false_positive` and 23 `known` (catalogued variables: real signals,
  but not transits; the catalogue match keeps them `known`). 6 of the 85 are on clean pixels and were left to
  agents by the new rule; all 6 are already rejected or known.
- The shared-period flag fires on 7 of the 133 (the 10.96-d stars), all already `false_positive` or `known` for
  other reasons.
- 27 re-vet verdicts differ from the stored status, none because of the new tests: 19 `known` rows came out
  `false_positive` and 5 the other way because the SIMBAD/VSX cone answers differ from the day they were vetted
  (agents' `known` verdicts also rest on literature, not only on the automatic look-up), and 2 + 1 are the
  `vetted` rows above. Stored statuses were not changed (dry run).

### 5. Corrected neighbour notes

76 notes had a failed neighbour query: 28 corrupt answers (Source 0, G 999999999) and 48 empty ones. 16 of them
were written on 2026-11-09/10 (the dates named this morning); the others span 2026-11-07 to 11-24. Corrected
values (56 from the Harvard mirror on retry, 20 from the ESA TAP): 16 stars really have 0 %, 49 have > 10 % and
31 have > 50 % of the pixel's G light from neighbours (largest: WDJ104539.04-190645.03 99 %, WDJ035015.22+455843.17
99 %, WDJ162626.33+193839.32 98 %, WDJ080420.96+225017.36 95 %, WDJ142428.39-510233.63 95 %). For the two stars
quoted this morning, WDJ071546.90-385201.36 and WDJ075356.62-252401.48, the corrected values are 79 % and 91 %,
the same as the ESA values found by hand. Contamination does not enter the automatic verdict, so no status
changes; the notes now say plainly where a blend is the default explanation.

### 6. Gaia DR4 readiness

Verified (ESA pages and the draft data model; details and URLs in `research/notes/gaia-dr4-plan.md`): release
2026-12-02 ~12:00 CET, archive offline from 2026-11-25 12:00 CET; 66 months of data (2014-07-25 to 2020-01-20);
epoch photometry for all sources (121.8 billion FoV-transit rows, 7.2 TB), epoch astrometry (129.6 billion rows,
62 TB), both through DataLink only (50 sources per request anonymous, 5,000 logged in);
`vari_planetary_transit` (1,007 rows), `vari_compact_companion` (6,224), `vari_classifier_result` (315 million,
with `prob_wd` and `prob_ep`), `nss_two_body_orbit` (5.9 million), `gaia_exoplanet_candidates` (size not given);
DR3->DR4 ids through `dr3_neighbourhood`.

Stubs and their offline self-tests:
- `dr4_common.py`: `check` (DR4 not available today: HTTP 400 on `gaiadr4.gaia_source`, as expected), `volume`,
  `xmatch`, DataLink batches with a byte budget (5 GB default, 20 GB hard cap).
- (a) `dr4_photometry.py` `selftest` (60 Gaia-like epochs over 2,000 d, 1 % noise): quiet star, no low point; a
  single 30 % dip: 1 low point, confirmed in BP and RP; a 40 %, 1-h eclipse at 0.19 d: period recovered exactly,
  18 in-eclipse epochs, BLS S/N 143; a 20 %, 1-h debris dip at 4.5 h: period recovered exactly, 12 epochs, S/N 61.
  The single dip also produces a spurious BLS "period" (S/N 30 from 5 points): hence the rule >= 3 in-transit
  epochs from different visits.
- (b) `dr4_astrometry.py`: of 16,676 white dwarfs, a Jupiter on a 3-yr orbit would displace 379 by > 100 micro-
  arcsec and 3,138 by > 50; a 13-Jupiter-mass companion at 3 yr, 6,213 by > 500. Self-test (70 epochs, 0.3 mas,
  99 % false-alarm level from 50 noise-only copies, dchi2 = 32): 5 M_J at 2 yr and 20 pc (530 micro-arcsec)
  detected at P = 1.84 yr with alpha = 490 micro-arcsec; 1 M_J at 3 yr (140) and 13 M_J at 0.5 yr and 50 pc
  with 1 mas errors (217) not detected; no false detection without a planet.
- (c) `dr4_variability.py`: TAP cross-match of nine DR4 tables with the sample, joined with our TESS statuses.
- (d) volume for 16,676 white dwarfs: epoch photometry 0.04 GB, per-CCD photometry 0.14 GB, epoch astrometry
  0.37 GB, all TAP tables < 0.01 GB (x3 for serialisation: ~1.6 GB in total).

## Limitations

- The blend test cannot tell an eclipsing neighbour from a debris cloud: both make hour-long dips. On crowded
  pixels (most of our faint white dwarfs: CROWDSAP < 0.8) a real debris system like ZTF J0328-1219 would be
  labelled `false_positive` with a reason that says debris is possible; only the ZTF fold of the white dwarf or
  the SAP comparison can rescue it, and those are still only in `labs/vet_extra.py`, not in `vetting.py`.
  Checked directly on the real debris white dwarf ZTF J0328-1219 (TIC from `validate.py`, TESS S31 and S108,
  CROWDSAP 0.54-0.59; `logs/ztf0328_blend_check.log`): at the 9.937-h period the best box is 30 min (S/N 7.9) vs
  15 min (S/N 7.6) within the 25.6-min limit, so no blend flag; at the 11.2-h period the best box is 90 min
  (S/N 5.3 vs 4.8) and the blend flag fires. Had the survey found it at 11.2 h, the new vetting would have
  called this real system a blend. This is the main cost of the new test and the reason the ZTF fold should be
  moved into `vetting.py` next.
- The clean-pixel thresholds (CROWDSAP 0.8, 10 % neighbour light) and BLEND_RATIO = 2 are judgement calls, not
  calibrated on injected debris.
- The shared-period table uses the survey's single best period per star, not per-sector detections, and the
  sector list is reconstructed from the download cache (newest 6 sectors up to `max_sector`); a systematic that
  shows up only as a second-best peak is missed.
- The dry-run re-vet ran with the code of 06:50-07:20 (before the CSV/ARI fix and the clean-pixel exemption;
  both applied afterwards in `logs/revet_summary_2026-11-24.py` where possible): 18 rows got "contamination
  unknown" because the old ESA parser failed while VizieR was failing. SIMBAD/VSX answers also vary from day to
  day, which explains most of the differences between the re-vet verdicts and the stored statuses (Results 4).
- The DR4 stubs use table and column names from a draft data model; `to_al_series` (turning
  `centroid_pos_al` into an along-scan residual) is deliberately unimplemented until the DR4 documentation exists.
  No per-epoch Gaia precision for white dwarfs is assumed anywhere.
- ESA Gaia TAP will be offline from 2026-11-25 12:00 CET to 2026-12-02; the neighbour fallback then relies on
  VizieR and ARI only.

## References

- Gentile Fusillo, N. P. et al. 2021, MNRAS 508, 3877 (Gaia EDR3 white-dwarf catalogue; masses, log g).
- Gaia Collaboration 2023, A&A 674, A1 (Gaia DR3), queried as `gaiadr3.gaia_source`.
- Vanderburg, A. et al. 2020, Nature 585, 363 (WD 1856+534 b; validation target, values from `validate.py`).
- Vanderbosch, Z. et al. 2021, ApJ 917, 41 (ZTF J0328-1219 debris, as cited in `validate.py`).
- Lindegren, L. et al. 2012, A&A 538, A78 (along-scan astrometric model; used for the AL formula of the stub).
- ESA Gaia DR4 pages read 2026-11-24: https://www.cosmos.esa.int/web/gaia/dr4 (content table, last updated
  2026-09-14), https://www.cosmos.esa.int/web/gaia/news (dates), https://www.cosmos.esa.int/web/gaia/iow_20260703,
  https://www.cosmos.esa.int/web/gaia/iow_20261014, https://www.cosmos.esa.int/web/gaia/dr4-papers,
  https://www.cosmos.esa.int/web/gaia-users/archive/collaborate; Gaia DR4 draft data model (2026-06-26), sections
  1.1, 2.2, 3.1, 7.3, 11.1, 18.4, 18.5, 18.12.
- Our own: `research/reports/2026-11-24-what-is-new.md`, `research/reports/2026-11-20-injection-recovery.md`.
