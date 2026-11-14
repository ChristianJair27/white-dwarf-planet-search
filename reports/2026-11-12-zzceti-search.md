# Pulsating white dwarfs in TESS 20-s and 120-s data of the Gaia 100 pc sample

Backlog item 28, run 2026-11-12. Code: `wdplanets/labs/zzceti.py`. Data products: `data/labs/zzceti/`
(`targets.csv`, `plan.csv`, `sectors.csv`, `peaks.csv`, `detections.csv`, `checked.csv`, `fullfap.csv`,
`deep.json`, `final.csv`). Literature note: `research/notes/zzceti-literature.md`.

## Summary

We searched 4,258 TESS SPOC light curves (one per star and sector, 20-s cadence where available) of 1,421 white
dwarfs within 100 pc whose photometric temperature puts them in or near the ZZ Ceti (DAV) or DBV instability
strips, concentrating on data taken after the published TESS-wide ZZ Ceti searches (Sector ≥ 70). Ninety stars
show pulsation-band signals above a 0.1 % false-alarm threshold under our detection rule. After literature and
neighbour checks, 84 are known variables (including 33 of the 49 TESS ZZ Cetis of Romero et al. 2022/2024 that
fall in our searched set), **3 are candidate new pulsators**, 2 are unconfirmed and 1 is a false positive.

The strongest candidate is **WDJ203728.70+145353.15** (SDSS J2037+1453), a DB white dwarf at 88 pc with
Teff = 23,225 K (Kilic et al. 2020), inside the DBV strip. It shows two modes, 334.85 s and 283.55 s, at the same
frequencies in Sectors 55, 81 and 82, plus their sum frequency, and Gaia DR3 flags it as variable. **ZTF independently detects both modes** at the
TESS frequencies in g and r over 2018–2025 and shows nothing on the 4" neighbour, so the white dwarf is the pulsator.
An ADS search found no report of its pulsations; Jestin et al. 2026 list it as not variable in their ZTF vetting. The two other candidates are DA white dwarfs observed in a single sector
(WDJ210219.83−123412.11, 454.6 s; WDJ142213.99−332351.75, 256.7 s or 225 s). None of them is a confirmed discovery.

## Data

- Sample: `data/catalog/wd_100pc.csv` (Gentile Fusillo et al. 2021 catalogue, our 100 pc extract), Pwd > 0.75.
  DAV box: TeffH 9,800–13,800 K (1,546 stars); DBV box: TeffH 20,000–35,000 K (264 stars). TeffH is the
  hydrogen-atmosphere photometric fit; the catalogue extract has no spectral types, so the DAV box also holds
  non-DA stars and the DBV box is only a proxy for helium atmospheres.
- TIC ids: from the survey's `research/targets.csv` when present, otherwise a TIC cone search matched on the
  Gaia DR2 id (1,809 of 1,810 resolved).
- TESS: 12,694 SPOC timeseries products at MAST for 1,655 stars. Per star and sector one light curve was kept
  (20 s preferred). Analysed: everything already cached by the transit survey, plus new downloads of every sector
  ≥ 70 and every sector of stars fainter than G = 17.5 (≈ 19 GB, 2,448 files; 2,332 on the first pass, the rest on
  retry; multi-sector SPOC products were excluded). Result: 4,258 light curves, 1,421 stars (1,185 DAV box, 236
  DBV box), 1,302 of them with at least one sector ≥ 70. One light curve was unusable.

## Method

1. Light curve: SPOC PDCSAP flux, QUALITY = 0, (flux/median − 1) in ppt, 0.25-day running median subtracted,
   5σ two-sided clipping (as Romero et al. 2022, 2024). SPOC already corrects PDCSAP for crowding (CROWDSAP), so
   amplitudes refer to the white dwarf's flux and are inflated by noise when CROWDSAP is small.
2. Amplitude spectrum: Lomb–Scargle (astropy, fast method), A = √(4 P_psd / N), oversampling 5, from 0.2 µHz to the
   Nyquist frequency. Pulsation band: periods 100–1,500 s (667–10,000 µHz), capped at the Nyquist frequency
   (4,167 µHz) for 120-s data. Tested on a synthetic 5-ppt sinusoid: recovered 5.00 ppt.
3. Threshold: Romero et al. use the 0.1 % false-alarm amplitude from 1,000 shuffled light curves (highest peak per
   shuffle). Doing that for 4,258 light curves was too slow, so we calibrated it as a multiple k of the mean band
   amplitude ⟨A⟩: 200 shuffles of 8 random 20-s and 5 random 120-s light curves, a Gumbel fit to the per-shuffle
   maxima extrapolated to 0.999, giving k = 5.02 (20 s) and 4.89 (120 s). The white-noise expectation
   k = √((4/π) ln(1000 M)), with M independent frequencies in the band, gives 4.62 and 4.49; we adopted the larger
   (shuffle) values. A peak must also exceed k times the local ⟨A⟩ in a 400-µHz window (red noise).
4. Detection rule per star: peaks above threshold in ≥ 2 sectors, or in the only sector available, or one sector at
   ≥ 7⟨A⟩. Peaks shared by ≥ 3 stars within 1 µHz in the same sector would be instrumental: none were found.
5. Checks for detected stars: SIMBAD (Harvard mirror) within 20" with all object types (a ZZ Ceti usually has main
   type WD* and Pu*/V* among its other types) and reference counts; the TIC ids listed in the Romero et al. tables;
   Gaia DR3 neighbours within 42" (ESA archive, Harvard VizieR fallback); only neighbours bluer than BP−RP = 0.6 were
   treated as possible sources (a red main-sequence star does not pulsate at 100–1,500 s).
6. For every star not explained by those checks: full 1,000-shuffle 0.1 % FAP in its strongest sector, amplitude of
   the main frequency in each half of every sector, first harmonic, all sectors downloaded, per-object literature
   (SIMBAD bibliography titles, arXiv papers listed below, web search).

## Results

**Detections.** 1,240 peaks above threshold in 98 stars; 90 stars pass the detection rule (82 DAV box, 8 DBV box).

**Completeness against published TESS pulsators.** Romero et al. 2022 and 2024 list 110 TIC ids; 55 are in our
target boxes and 49 were searched. We recover 33 (67 %). The 16 misses reach 0.73–1.36 times our threshold in their
best sector: our per-sector search with a ≥ 2-sector rule is less sensitive than their concatenated multi-sector
spectra, and for most of them we analysed only Sectors ≥ 70, not their discovery sectors.

**Verdicts** (`data/labs/zzceti/final.csv`):

| Verdict | Stars | Notes |
|---|---|---|
| known | 84 | 33 in the Romero tables, 49 with a variable/pulsator type in SIMBAD, plus WD 1310+583 (ZZ Ceti; Bognár et al. 2018, 2026) and J0006+3104 (23.15-min rotation of a massive DC, Jewett et al. 2024 — we recover 1,389 s in Sectors 17, 57 and 84) |
| candidate | 3 | below |
| unconfirmed | 2 | WDJ194549.13−153135.63 (195.7 s, 1.08× the 1,000-shuffle FAP amplitude, below the 1.1× Romero et al. 2024 require for a single period); WDJ062054.41+070050.21 (878 s in Sector 87, absent in Sector 33, CROWDSAP 0.08) |
| false positive | 1 | WDJ184030.54−111422.90: CROWDSAP 0.0085 in a Galactic-plane field |

**Candidates**

| Star | Type | Sectors with signal | Period(s) | Amplitude | vs 0.1 % FAP (1,000 shuffles) | Notes |
|---|---|---|---|---|---|---|
| WDJ203728.70+145353.15 (TIC 456645161) | DB, 23,225 ± 1,087 K, log g 7.96 (Kilic+2020) | 55, 81, 82 (all available) | 334.85 s, 283.55 s; sum frequency 153.54 s | 11.7–14.4 and 9.5–10.4 ppt | 3.5× (S81) | Gaia DR3 VARIABLE; background G/K star (G 14.85, 850 pc) at 4.1" |
| WDJ210219.83−123412.11 (TIC 442532281) | DA (Gaia XP, P 0.92), 11,444 K, log g 8.06 | 92 (only sector) | 454.62 s | 14.4 ppt | 1.34× | both halves of the sector |
| WDJ142213.99−332351.75 (TIC 270350156) | DA (Gaia XP, P 0.94), 11,324 K, log g 7.95 | 102 (only sector, 120 s) | 256.65 s or 225 s (Nyquist) | 7.9 ppt | 1.36× | two stars as bright as the WD at 12" |

Per-object notes: `research/notes/<WDJname>.md`. Figures: [zzceti_strip.png](../figures/zzceti_strip.png) and
[zzceti_<WDJname>.png](../figures/zzceti_<WDJname>.png).

Why J2037+1453 is the interesting one: it is spectroscopically a DB in the DBV strip, so pulsations are expected
physics rather than a coincidence; its two periods are stable over two years; the sum frequency appears in all three
sectors, which points to one non-linearly pulsating star rather than a blend of two variables; Gaia DR3, which
resolves the 4" neighbour, flags the white dwarf itself as variable. It is not among the 28 DBVs known before 2022
nor the 19 new ones of Vanderbosch et al. 2022, nor the two new DBVs of Córsico et al. 2022 (A&A 668, A161), and the Romero
ZZ Ceti searches were restricted to DAs.

### Follow-up of J2037+1453 (same day)

- **Pixel-level centroid** (`wdplanets/labs/dbv_centroid.py`; figure [dbv_centroid_TIC456645161.png](../figures/dbv_centroid_TIC456645161.png)):
  per-pixel amplitudes at both mode frequencies in the three 20-s target pixel files, fitted with a Gaussian PSF
  registered on the Gaia DR3 field. In all six measurements (2 modes x 3 sectors) the centroid is 1.3–9.4" from the white
  dwarf or its 4" neighbour and 16–22" from the next star, so the two other neighbours are excluded. The 4" pair is not
  resolved: Sector 81 puts the centroid 1.3" and 3.1" from the white dwarf (5.7" and 7.3" from the neighbour); Sectors 55
  and 82 sit ~8" from both, a PSF-model systematic (noise scatter 1.4–2.6").
- **Gaia DR3 resolves the pair.** The white dwarf alone shows a G-band scatter of 15.7 mmag over 37 epochs (4.6 times
  its errors) and the variability classifier assigns it the class "WD" (variable white dwarf, score 0.84); the G = 14.85
  neighbour was not analysed. The TESS amplitudes (14 and 10 ppt, rms ~13 mmag) match the scatter Gaia measures on the white
  dwarf, so we attribute the pulsations to it.
- **Prior catalogues.** Not in Guidry et al. 2021 (ApJ 912, 125; VizieR J/ApJ/912/125). Jestin et al. 2026 (A&A 712,
  A243; VizieR J/A+A/712/A243/tablea1, 864 Gaia-variable WDs vetted with ZTF DR23) **list it with Variable = False,
  Periodic = False**. Their search reached 320 c/d, but every high-frequency pulsator they detected has a ZTF g amplitude
  of 0.07–0.11 mag; ours is ~0.01 mag, below what a blind search over all frequencies can pick out.
- **ADS** (browser, 2026-11-12): `simbid:15865513` returns the same 8 catalogue papers as SIMBAD; full-text searches for
  "J203728", "J2037+1453", the TIC and the Gaia DR3 ids find nothing about its variability (one unrelated Cygnus X
  paper; Kilic et al. 2020). Recent DBV/pulsating-WD abstracts (2023–2026, 65 records) contain no list that includes it;
  Huang et al. 2026 (ApJS 284, 72, 24 new TESS WD pulsators) used Sectors 84–96 only. ADS does not index
  machine-readable tables (the Jestin table had to be read on VizieR).
- **ZTF targeted test** (`wdplanets/labs/dbv_ztf.py`; `data/labs/dbv_ztf/ztf_result*.json`; figure
  [dbv_ztf_TIC456645161.png](../figures/dbv_ztf_TIC456645161.png)). IRSA ZTF light curves, catflags = 0, 30–60-s exposures only (300-s exposures
  average a 335-s pulsation away), 1,097 g and 1,790 r epochs, 2018 April – 2025 October. A least-squares amplitude spectrum within
  ±1 µHz of each TESS frequency, compared with the same window maximum at 300 control frequencies:

  | Band | 334.85 s | 283.55 s | control window max: median / 99.9 % |
  |---|---|---|---|
  | g | 9.95 ppt at 2,986.417 µHz | 8.86 ppt at 3,526.662 µHz | 3.2 / 4.5 ppt |
  | r | 8.02 ppt at 2,986.416 µHz | 5.81 ppt at 3,526.661 µHz | 2.1 / 3.4 ppt |

  All four peaks exceed all 300 control windows (empirical false-alarm probability < 0.3 % each) and fall within
  0.02–0.04 µHz of the TESS frequencies; g and r agree to 0.002 µHz. The seven-year baseline refines the periods to
  **334.8494 s and 283.5543 s**. Per season, the 334.85-s mode exceeds the 99 % control level in every season in both
  bands; the 283.55-s mode in 14 of 16 band-seasons. Amplitudes are larger in g than in r, as expected for g-mode
  pulsations. The full-baseline amplitudes (8–10 ppt) are lower than single seasons (11–18 ppt): partly the upward
  bias of a window maximum on fewer points, possibly slow phase or amplitude changes over the years.
- **The neighbour does not pulsate.** ZTF resolves the G = 14.85 star 3.9" away as a separate source. The same test on
  it gives 1.3–2.1 ppt, at the noise level (false-alarm probability 36–80 %).
- Verdict: **a pulsating DB white dwarf (DBV) detected by two instruments, TESS and ZTF**, with the pulsator
  identified by ZTF's resolved photometry. Gaia DR3 had flagged it as a variable-WD candidate without a period, and a
  ZTF-based vetting listed it as not variable; we found no publication of its pulsations.

## Limitations

- Single-sector candidates are not confirmations. TESS cannot separate the 4" pair of J2037+1453; the attribution
  rests on ZTF and Gaia DR3 resolved photometry (above).
- Our threshold is calibrated on 13 light curves, and computed over the pulsation band only; Romero et al. used
  the whole spectrum, which gives a slightly higher threshold.
- The search is per sector; concatenating sectors (as Romero et al. do) would find weaker pulsators.
- "Known" via SIMBAD uses a 20" region, so a variable neighbour can mark a target as known (for example the
  HS 0507+0434 A/B pair); counts of known stars are approximate.
- Sectors before 70 were analysed only where the survey had already cached them; stars fainter than G = 17.5 were
  fully downloaded but few have SPOC data.
- Novelty for J2037+1453 rests on SIMBAD, ADS (including full text), VizieR catalogues and the papers below, as of
  2026-11-12; a paper in preparation by others cannot be excluded.
- An earlier draft of this report said ZTF could not test 5-min periods. That was wrong: with 30–60-s exposures and
  a frequency known from TESS, ZTF's sparse sampling detects them (above). The other two candidates (single-sector
  DAs) have not been tested with ZTF.
- No ground-based fast photometry, which would resolve more modes and allow asteroseismology.

## References (read)

- Romero, A. D. et al. 2022, MNRAS 511, 1574, arXiv:2201.04158 — 74 new ZZ Cetis, Sectors 1–39.
- Romero, A. D. et al. 2025, ApJ 984, 112 (arXiv:2407.07260; cited as "2024" in earlier drafts) — 32 new ZZ Cetis, Sectors 40–69; 1.1× FAP rule for single periods.
- Bognár, Zs. et al. 2023, A&A, arXiv:2305.05246 — known southern ZZ Cetis re-observed by TESS.
- Córsico, A. H. et al. 2022, A&A 668, A161, arXiv:2210.05486 (misattributed to Romero et al. in an earlier draft) — two new DBVs (WD J152738.4−450207.4, WD 1708−871);
  DBV strip ∼ 21,000–30,000 K.
- Vanderbosch, Z. et al. 2022, ApJ 927, 158, arXiv:2201.09893 — 19 new DBVs, list of 28 known DBVs.
- Jestin, T. et al. 2026, A&A 712, A243 (arXiv:2509.15133) — Gaia DR3 variable WDs vetted by ZTF; table A1 read on VizieR.
- Huang, G. et al. 2026, ApJS 284, 72 (arXiv:2605.03323) — high-frequency oscillators in TESS Cycle 7 (abstract read).
- Masci, F. J. et al. 2019, PASP 131, 018003 — standard ZTF data citation (not read; no facts taken from it).
- Jewett, G. et al. 2024, ApJ 974, 12, arXiv:2407.04827 — J0006+3104 23.15-min period (Table 4).
- Guidry, J. A. et al. 2021, ApJ 912, 125 (VizieR J/ApJ/912/125) — Gaia+ZTF variable white dwarfs; catalogue queried.
- Jestin, T. et al. 2025, arXiv:2509.15133 — Gaia DR3 variable white dwarfs vetted by ZTF; text read.
- Antunes Amaral, L. et al. 2025, A&A, arXiv:2501.09003; PLATO white-dwarf paper arXiv:2511.19196 — context only.
- Catalogue values: Kilic, M. et al. 2020, ApJ 898, 84 (VizieR J/ApJ/898/84); Jiménez-Esteban, F. M. et al. 2023,
  MNRAS 518, 5106 (J/MNRAS/518/5106); O'Brien, M. W. et al. 2023, MNRAS 518, 3055 (J/MNRAS/518/3055); Gaia DR3
  (I/355/gaiadr3); Bognár, Zs. et al. 2018, MNRAS 478, 2676 and 2026, A&A 707, A47 (titles via SIMBAD only).
