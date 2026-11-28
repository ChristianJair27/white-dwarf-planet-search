# Have we found anything new? Survey, vetting and lab status on 2026-11-24

Written by the verificador agent, 2026-11-24, to answer Christian's question "with our tools and research, have we
found anything new?". Code added today: `wdplanets/labs/vet_extra.py` (extra candidate tests) and
`wdplanets/labs/j1422_ffi.py` (FFI test of the pulsator candidate). Data products: `data/labs/vet_2026-11-24/`
(one JSON per vetted star plus the ZTF light curves) and `data/labs/j1422_ffi/` (TESScut cutout).

## Summary

**No new discovery survives.** The transit survey has now searched 2,144 white dwarfs with TESS data (1,941 of them
at 20-s cadence) out of 2,263 processed; 132 signals have crossed the detection thresholds since October and all
132 are explained: 91 false positives and 41 known variables or binaries. Today we vetted the 22 rows still marked
`candidate` in `research/targets.csv`: 12 had already been rejected by the automatic vetting on 2026-11-07/11 but
their status had never been written; the other 10 (6 new since 2026-11-15) were tested here and all 10 are blends
or instrumental: 9 false positives and 1 known neighbouring eclipsing binary. No row is left as `candidate`.

Outside the transit survey, the open leads are unchanged and none is a confirmed result of ours:

- the pulsating DB white dwarf WD J203728.70+145353.15 is real (TESS + ZTF) but another group (Wenenn and von Hippel)
  found it first, so it is not ours to announce;
- the other two 2026-11-12 pulsator "candidates" ended differently: WDJ210219.83-123412.11 is a confirmed pulsator
  but was already published by Huang et al. 2026, and WDJ142213.99-332351.75 is **still an unconfirmed, unpublished
  candidate** (one TESS sector; today's SIMBAD bibliography and an FFI test did not change that);
- three clean infrared-excess candidates (WDJ033256.37-174323.78, WDJ080323.85+163357.90, WDJ163917.47+103604.84)
  are still unreported in every list we have checked, but their W2 excesses are only 3.1-3.7 sigma (chi(z-W2)).

Two findings about our own pipeline are new and useful: the survey's 30-min box cap lets 1.5-3-h eclipses of
neighbouring stars pass the automatic physical-duration test (five of the six signals the automatic vetting had
passed were such blends; the sixth was a crowding artefact), and a 10.96-d "period" shared by 18 unrelated stars is a TESS Sector 72 systematic.

## Data

- Survey state: `research/targets.csv` (2,263 rows at the time of writing, 2026-11-24 ~06:20 local),
  `research/journal.jsonl`, `research/survey_heartbeat.json` (age < 3 min during this work; the survey was not
  touched), per-star notes `research/notes/<WDJname>.md`.
- TESS SPOC 20-s and 120-s PDCSAP and SAP light curves (MAST, through the survey cache `data/tess/`, up to six newest
  sectors per star); TESScut Sector 102 full-frame-image cutout for J1422-3323.
- Gaia DR3 `gaia_source`, `vari_eclipsing_binary`, `vari_classifier_result` (ESA Gaia archive TAP; note: the archive
  goes offline on 2026-11-25 for the DR4 release on 2026-12-02).
- AAVSO VSX (`B/vsx/vsx`) and Xu et al. 2020 tables (`J/ApJ/902/127`) through the Harvard VizieR mirror; SIMBAD
  through the Harvard mirror (basic, otypes, ident, has_ref, ref).
- ZTF public light curves (IRSA light-curve service), 2.5" around the white dwarf moved to epoch 2021.5,
  catflags = 0.
- arXiv API (metadata) for object identifiers; most queries were rate-limited (HTTP 429/503) today.
- Earlier results quoted from our own reports: `research/reports/2026-11-12-zzceti-search.md`,
  `2026-11-07-ir-excess-second-pass.md`, `2026-11-20-injection-recovery.md`,
  `2026-11-08-polluted-wd-wide-binaries.md`, and `research/notes/irx-novelty-2026-11-08.md`.

## Method

1. **Survey progress.** Counted `targets.csv` rows by status and by `updated` date; looked for gaps longer than
   6 h in the update times.
2. **Automatic vetting** (`python -m wdplanets.vetting <names>`) for the four candidates that had no note (the
   survey's own vetting call had failed for them).
3. **Extra tests** (`python -m wdplanets.labs.vet_extra <names>`) on the ten candidates that had no rejecting
   verdict, in order of SDE:
   - refined period (BLS, +-0.2 % around the survey period) and a **duration scan from 4 min to 4 h** at that period.
     The survey's longest box is 30 min, so an eclipse lasting hours shows up there as a "30-min transit"; the longest
     possible transit of a 0.6 Msun, 0.013 Rsun white dwarf by a Jupiter-size body is computed as in
     `vetting.max_transit_minutes`;
   - the **raw SAP dip** in each sector at the refined ephemeris (12-h running median removed): PDCSAP divides by
     CROWDSAP, the fraction of aperture light that the TIC assigns to the target, so a 2 % dip of the aperture light
     becomes a 30 % "transit" when CROWDSAP = 0.07;
   - **Gaia DR3 field** within 60" (ESA TAP), fraction of the light inside 21", 42" and 60" not coming from the
     white dwarf; Gaia DR3 eclipsing binaries and variability classes and VSX entries within 3' (periods compared with
     P, P/2, 2P);
   - **ZTF fold of the white dwarf itself**: ZTF's ~2" resolution separates the white dwarf from the stars that share
     its 21" TESS pixel; flux per ZTF field/CCD normalised, points inside the transit window compared with the rest;
   - number of 20-s SPOC light curves (lightkurve search).
4. Verdicts written to each note (section "2026-11-24 - agent vetting (verificador)") and to `targets.csv`.
5. **Other labs**: read `wdplanets/labs/`, `research/BACKLOG.md`, the pulsator and infrared-excess reports and notes.
6. **Novelty check** for every object still open: SIMBAD bibliography with titles (Harvard TAP), arXiv API by Gaia
   id and J-name, VizieR tables where relevant (Xu et al. 2020 for J1422-3323), plus the per-object lists already
   checked earlier (Girven 2011, Hogg 2020, Wang 2026, Debes 2011 for the infrared candidates; Huang 2026, Jestin
   2026, Romero 2022/2025 for the pulsators). ADS full text was not reachable by script and was not repeated today.
7. **J1422-3323 FFI test** (`python -m wdplanets.labs.j1422_ffi`): the 200-s FFI cadence aliases the two possible
   true frequencies of the 120-s signal to different places (1,103.5 and 562.8 uHz), so a detection would break the
   Nyquist ambiguity. Aperture photometry (1, 4 and 9 pixels), Lomb-Scargle amplitude spectrum, 200 shuffles and 300
   random 4-uHz control windows.

## Results

### 1. Survey progress since 2026-11-15

| | rows | with TESS data | status now |
|---|---|---|---|
| all time | 2,263 | 2,144 (1,941 at 20 s) | 2,012 searched, 114 no data, 91 false_positive, 41 known, 3 no TIC, 2 error, 0 candidate |
| processed since 2026-11-15 | 710 | 661 | 626 searched, 47 no data, 31 false_positive, 4 known, 2 error |

- Since 2026-11-15 the survey moved from G = 15.57 to G = 16.44 (it goes brightest first after the priority list).
  The G < 17 sample has 3,339 white dwarfs, so 68 % have been processed.
- 34 signals crossed the thresholds since 2026-11-15: the survey's automatic vetting rejected 28 (25 false_positive,
  3 known); 6 were left as `candidate` and are vetted below (5 false_positive, 1 known).
- **The survey was not running 24/7.** No rows were written from 2026-11-13 19:13 to 2026-11-20 04:47 (6.4 days),
  from 2026-11-20 12:37 to 2026-11-21 16:35 (28 h) and from 2026-11-21 18:35 to 2026-11-23 18:25 (48 h). The current
  process started 2026-11-23 18:24 and its heartbeat was fresh throughout today's work.

### 2. The 22 open candidates

Stale rows (automatic verdict of 2026-11-07 to 11-11 confirmed by reading each note; `python -m wdplanets.vetting`
writes the note but never calls `update_status`, which is why they stayed `candidate`):

| Star | P (d) | SDE | Verdict | Reason |
|---|---|---|---|---|
| WDJ192034.41-471529.44 | 0.284 | 208 | false_positive | box 2.7x the physical limit, sinusoidal, CROWDSAP 0.06 |
| WDJ200736.50+174214.73 | 0.170 | 149 | known | WZ Sge (cataclysmic variable) |
| WDJ163421.55+571008.87 | 0.634 | 132 | known | CM Dra in the aperture (VSX EA, P = 1.26839 d = 2 x our P) |
| WDJ150742.03-592754.43 | 0.232 | 65 | false_positive | box 2.8x limit, sinusoidal, one sector |
| WDJ034329.03-454904.23 | 0.150 | 34 | known | VY Hor, ZZ Ceti |
| WDJ204745.04+323922.58 | 12.2 | 31 | false_positive | one sector carries the signal, odd/even 4.7 sigma, CROWDSAP 0.01 |
| WDJ042415.74+521010.64 | 0.774 | 26 | false_positive | box 1.9x limit |
| WDJ164057.15+534109.32 | 0.161 | 24 | false_positive | GD 356; box 3.2x limit, sinusoid as large as the box |
| WDJ042211.36-474142.02 | 0.150 | 16 | known | EC 04207-4748, pulsator |
| WDJ041856.64+271748.31 | 0.263 | 15 | known | HL Tau 76, ZZ Ceti |
| WDJ182503.04-293145.02 | 0.454 | 13 | false_positive | box 2.3x limit, sinusoidal |
| WDJ211146.39+012054.26 | 6.995 | 10 | false_positive (was `known`) | P within 2.1 % of the TESS orbit alias 13.7/2 d, 4 events, depth > 100 % |

Rows vetted today (extra tests; all numbers in `data/labs/vet_2026-11-24/<name>.json`):

| Star | Refined P (d) | Best box / physical limit (min) | Raw SAP dip (aperture) | ZTF on the WD (in-window points) | Verdict |
|---|---|---|---|---|---|
| WDJ071546.90-385201.36 | 2.457742 | 120 / 23 | 1.9-2.3 %, 5 of 5 sectors, CROWDSAP 0.06-0.08 | south of ZTF | false_positive: eclipsing neighbour (79 % of the 21" light is neighbours, G 13.3 and 14.2 at ~20") |
| WDJ075356.62-252401.48 | 1.688890 | 90 / 20 | 0.9-1.5 %, 4 of 4, CROWDSAP 0.06-0.10 | r: 0.67 +- 0.15 % (140) vs 11-12 % PDC | false_positive: eclipsing neighbour (91 % of the 21" light) |
| WDJ200114.63+202757.15 | 0.229810 | 180 / 10.5 | (SAP fit failed) | g: -0.04 +- 0.07 % (311), r: -0.02 +- 0.06 % (936) vs 4.7 % | known: W UMa ZTF J200114.57+202741.1 at 16.4" (VSX, P = 0.4593342 d; P/2 fits as well, S/N 40.0 vs 39.6) |
| WDJ022111.49+533330.39 | 11.94 | 45 / 39 | 0.40 +- 0.08 % in S85 only; CROWDSAP 0.003 (G 9.8 star at 11.6") | 1 point | false_positive: crowding artefact, not periodic |
| WDJ000855.80+364559.19 | 2.504874 | 120 / 23 | 5-10 %, odd/even 6.2 sigma | g: 0.14 +- 0.27 % (17), r: 0.05 +- 0.26 % (27) vs 6-21 % | false_positive: eclipsing binary at ~5.01 d in the aperture (G 14.7 star at 36" a plausible host, untested) |
| WDJ100623.08+071212.70 | 7.21 | 4 min, S/N 7 | no dip (< 2.4 sigma) | 0 points | false_positive: one sector (S72), depth > 100 %, orbit-alias window |
| WDJ033320.37+000720.65 | 9.1179 | 180 / 36 | 1.4 % and 3.5 % (2 sectors) | g: -0.9 +- 0.7 % (5), r: -1.0 +- 0.6 % (6) vs 7.5 % | false_positive: 5x too long, 5 events, inconsistent |
| WDJ220602.42-004632.71 | 0.58334 | 120 / 14 | absent in S42, 1.6-3.6 % in S55/S82 | g: 0.1 +- 0.5 % (10), r: 0.2 +- 0.6 % (7) vs 2.4 % | false_positive |
| WDJ191850.20+333602.29 | 7.569195 | 120 / 34 | 5.6-8.4 %, 5 of 5, CROWDSAP 0.013-0.033 | g: -0.03 +- 0.34 % (9), r: -0.03 +- 0.25 % (17) | false_positive: eclipsing neighbour (would need 170-630 % of the WD's light) |
| WDJ090331.29+140049.17 | 10.9617 | 4 min | S72 artefact only | 0 points | false_positive: one sector, shared 10.96-d systematic |

The ZTF tests with fewer than ~10 in-window points (WDJ033320, WDJ220602) are weak on their own; for those stars the
duration and per-sector tests carry the verdict.

### 3. What the vetting taught us about the pipeline

- **The 30-min box cap hides long eclipses.** Five of the six signals that the automatic vetting had passed (verdict
  `vetted`) had their best box at 90-180 min once longer boxes were allowed, 4-5 times the longest possible
  white-dwarf transit, and wherever ZTF had enough points the white dwarf itself showed at most a small fraction of the
  PDC depth. The automatic duration test (ratio > 1.5) cannot see this because the measured duration is capped at 30 min.
  The sixth (WDJ022111) is a CROWDSAP = 0.003 artefact that only the SAP test catches (backlog 2c). Adding the duration
  scan, the ZTF fold and the SAP comparison to `wdplanets/vetting.py` would have rejected all six automatically.
- **A Sector 72 systematic at 10.9615 d.** 18 stars in `targets.csv` have periods within 0.01 d of 10.961 d; 7 of
  them have Sector 72 as their newest sector, and those 7 all lie at RA 8h16m-10h46m. It is not one of the 13.7/n-d orbit
  aliases the vetting already vetoes; a "shared period across unrelated stars" veto would catch it.
- **Two bookkeeping bugs.** (a) `python -m wdplanets.vetting` never writes the status to `targets.csv` (12 stale
  candidates). (b) In notes written 2026-11-09/10 the Gaia neighbour table from the Harvard VizieR mirror came back
  with Source = 0 and G = 999999999, so the automatic contamination read 0 %; the ESA TAP query gives 79 % and 91 %
  for those two stars.

### 4. Other labs

**Pulsating white dwarfs (`wdplanets/labs/zzceti.py`, report 2026-11-12).** Of the three 2026-11-12 candidates and
two "unconfirmed" stars:

| Star | Status today | Evidence |
|---|---|---|
| WDJ203728.70+145353.15 (DBV) | real, **priority belongs to Wenenn and von Hippel** (found 2026-10-27, per JJ Hermes, 2026-11-21) | TESS S55/S81/S82 + ZTF g and r at the same two frequencies; not treated as ours |
| WDJ210219.83-123412.11 | confirmed pulsator, **already published** (Huang et al. 2026, Appendix A) | ZTF recovers 454.6 s and finds 262.1 s |
| WDJ142213.99-332351.75 | **still a candidate**, apparently unpublished | one sector (S102, 120 s), 256.65 s or 225.4 s, 7.9 ppt, 1.36x the 0.1 % FAP; Gaia DR3 classifier "WD" variable (0.86); no ZTF (dec -33) |
| WDJ062054.41+070050.21 | variable, **already published** (Huang et al. 2026) | 878 s in S87 |
| WDJ194549.13-153135.63 | unconfirmed (195.7 s, 1.08x FAP) | ZTF not detected, excludes a stable mode > ~4 ppt only |

New today for J1422-3323: MAST still has only the Sector 102 120-s light curve. The Sector 102 FFI (200 s) does not
show either alias (amplitudes 0.74-1.11 ppt at the alias positions against a 99 % shuffle maximum of 2.0-2.5 ppt),
but the expected FFI amplitude is only ~0.5-0.9 ppt after 200-s smearing and without crowding correction, so the test
is inconclusive, not negative.

**Infrared excess (`wdplanets/irx.py`, report 2026-11-07).** Three clean candidates remain (cool, G = 18.5-19.4,
64-94 pc, chi(z-W1) / chi(z-W2) = 4.8-5.7 / 3.1-3.7) plus one marginal (WDJ120726.77-075444.26). Today's SIMBAD
bibliographies list only catalogue and classification papers (J1639+1036 is a catalogued magnetic DAH; J0803+1633 and
J1639+1036 appear in a 2025 SDSS 100 pc magnetic-WD paper, title only). arXiv returned no hit for their Gaia ids or
for J0803/J1639 J-names. Not yet checked: Wang & Liu 2026 (DESI), Hoard 2013, Barber 2014, Rebassa-Mansergas 2019.

**Polluted white dwarfs and wide companions (`wdplanets/labs/wd_pairs.py`, report 2026-11-08).** The deficit of wide
companions (0.54 +- 0.08 of the control) reproduces published results (Noor et al. 2024; Xu et al. 2026); what is
ours is an XP-selected sample and a ~2-sigma DA(Z) deficit, too weak to claim.

**Injection-recovery (report 2026-11-20).** Our own completeness limits (every non-grazing body >= 1 Earth radius
recovered; R50 = 0.26-1.08 Earth radii from G 13.5 to 16.5). With today's result that none of the survey candidates
is real, the null result is now final for the stars searched so far.

### 5. Novelty check summary

| Object | SIMBAD bibliography (today) | Other lists | Novel? |
|---|---|---|---|
| J2037+1453 | (2026-11-12: 8 catalogue papers) | Jestin 2026 lists it as not variable | detection independent, **priority not ours** |
| J1422-3323 | 9 papers, all catalogues/classifications; otypes *, PM*, UV, WD*, WD? | not in Romero 2022/2025, Huang 2026, Steen 2024 (checked 2026-11-20); not in Xu 2020 VizieR tables; arXiv rate-limited today | no publication found; **unconfirmed** |
| J0332-1743, J0803+1633, J1639+1036 | catalogue/magnetic-WD papers only | not in Girven 2011, Debes 2011, Wang 2026, Xu 2020, Lai 2021, Madurga 2024, Murillo-Ojeda 2026 (2026-11-08) | no publication found; modest significance |

### Answer to the question

Nothing we have found is both confirmed and new. The only confirmed new object from our tools (the DBV J2037+1453)
was found first by another group. What is left that could still be new: one single-sector pulsator candidate
(J1422-3323) and three modest infrared-excess candidates, none confirmed. The transit survey has produced a clean
null result with measured completeness, which is itself a reportable result but not a discovery.

## Limitations

- Pixel-level (centroid) tests were not run for the transit blends; the identification of the eclipsing star is
  left open except for WDJ200114 (VSX match) and WDJ163421 (CM Dra).
- The ZTF windows assume the refined TESS ephemeris holds over 2018-2025; period errors smear the window for the
  long-period, few-event signals.
- The SAP dip computation failed for WDJ200114 (a NaN in the running median); its verdict rests on the VSX match,
  the BLS at the VSX period and ZTF.
- SIMBAD (Harvard) timed out for several stars during the extra tests; the identifiers in the table come from the
  automatic notes.
- arXiv was rate-limited for J1422-3323 and the J0332-1743 J-name; ADS full text was not repeated.
- The answer covers what is in our files and the catalogues listed; papers in preparation (like Wenenn's) cannot be
  excluded.

## References

Read in earlier sessions (details and links in the reports cited):
- Huang, G. et al. 2026, ApJS 284, 72 (arXiv:2605.03323) - Appendix A white-dwarf table.
- Jestin, T. et al. 2026, A&A 712, A243 - VizieR J/A+A/712/A243/tablea1.
- Romero, A. D. et al. 2022, MNRAS 511, 1574; Romero, A. D. et al. 2025, ApJ 984, 112.
- Girven, J. et al. 2011, MNRAS 417, 1210; Hogg, M. A. et al. 2020, MNRAS 498, 12; Wang, K. et al. 2026, ApJ 1001, 81;
  Debes, J. H. et al. 2011, ApJS 197, 38 (see `research/notes/irx-novelty-2026-11-08.md`).
- Noor et al. 2024 and Xu et al. 2026 (see `research/reports/2026-11-08-polluted-wd-wide-binaries.md`).

Catalogues queried today: Gaia DR3 (Gaia Collaboration 2023; `gaia_source`, `vari_eclipsing_binary`,
`vari_classifier_result`), AAVSO VSX (`B/vsx/vsx`), SIMBAD, Xu, S. et al. 2020, ApJ 902, 127 (VizieR
J/ApJ/902/127, tables 3-4; title read via SIMBAD), ZTF public data (IRSA), TESS SPOC and TESScut (MAST).

SIMBAD titles read today (titles only): 2018MNRAS.480.4505J, 2019MNRAS.482.4570G, 2019MNRAS.485.5573T,
2020ApJ...898...84K, 2020ApJ...902..127X, 2021A&A...649A...6G, 2021MNRAS.508.3877G, 2023A&A...679A.127G,
2023ApJ...944...56A, 2023MNRAS.518.5106J, 2023MNRAS.520.6111H, 2024A&A...682A...5V, 2025ApJ...990...25M,
2015MNRAS.446.4078K, 2015MNRAS.448.2260G, 2019MNRAS.486.2169K.

## Next step

The single best research step toward something genuinely new is to **confirm or kill WDJ142213.99-332351.75**: it
is the only signal left that is both unconfirmed and, as far as we can find, unpublished, and the group that found
J2037+1453 first is assembling new TESS pulsators. It needs either a TESS 20-s sector or ground photometry with
<= 30-s exposures from a southern telescope (Christian decides whether to request time). In parallel, the cheapest
improvement to the transit survey is to add the 4-h duration scan, the ZTF fold and a shared-period veto to
`wdplanets/vetting.py`, and to make `python -m wdplanets.vetting` write the status.
