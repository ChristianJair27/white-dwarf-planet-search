# WISE-excess candidates: confusion checks (2026-11-28)

*investigador, 2026-11-28. Code: `logs/p45_irx_debes_checks.py` (downloads), `logs/p46_irx_debes_analysis.py`
(analysis; `extra` argument for the tail probabilities and the K prediction), `logs/p47_irx_debes_figure.py` (figure).
Data: `data/irx/debes/` (summary.json, catwise.csv, catwise_gaia_field_calibration.csv, ls_dr10_tractor.csv,
ls_dr10_field3arcmin.csv, nir_wfau.csv, nir_forced_phot.csv, extended_neighbours.csv, img/, img_wide/).
Figure: not included in this public copy.*

## Why

Our three unpublished W1/W2-excess white dwarfs (WDJ033256.37-174323.78, WDJ080323.85+163357.90,
WDJ163917.47+103604.84; plus the marginal WDJ120726.77-075444.26) have excesses of only 3-4 sigma at W1 = 16.5-17.5
(Vega), where confusion with background galaxies is significant (Dennihy et al. 2020, ApJ 891, 97). Following the
advice of a specialist in dusty white dwarfs we checked (a) public ~1" near-IR imaging, (b) known background
sources, (c) whether the unWISE/CatWISE sources move with the white dwarf.

What Dennihy et al. (2020) found (full text read, arXiv:2002.01021): of 22 WISE-selected white-dwarf excess
candidates near the faint WISE limit, already vetted with ground-based near-IR images and astrometry, Spitzer showed
**8 to be confused (36 %)**; in all eight the contaminants were invisible in the J/Ks images. Near-IR imaging and
astrometry "cannot be used to confirm WISE-selected infrared excess candidates, but only to rule them out". Their
practical criteria: sources within 7.8" (1.3 x W1 FWHM) are potential contaminants; W1 S/N > 10 with a Gaia-AllWISE
figure of merit < 4 suggests confusion; and a CatWISE proper motion different from Gaia's (CatWISE accuracy then
~30 mas/yr at W1 = 15.5, ~100 mas/yr at W1 = 17) flags it, but only for bright or fast-moving objects. **Everything
below can therefore only reject a candidate, never confirm one.**

## Data (all official archives; total download ~25 MB)

- Gaia DR3 astrometry and neighbours (15"): ARI Heidelberg TAP (the ESA archive TAP returned an HTML page today).
  No other Gaia source within 15" of any of the four.
- Gaia EDR3 x AllWISE neighbourhood (figure of merit "score"), ARI TAP (`gaiaedr3.allwise_neighbourhood`; the DR2
  table Dennihy used answered empty there, so the scale may differ somewhat from theirs).
- IRSA TAP: CatWISE2020 (`catwise_2020`, positions at MJD 57170 / mean epoch, motions in arcsec/yr), AllWISE,
  unWISE catalogue (Schlafly+ 2019, `unwise_2019`), CatWISE counts within 5'.
- Legacy Surveys DR10 Tractor catalogue (viewer `cat.json`, 30" box and 3' box) and cutouts (image, Tractor model,
  residual, unWISE NEO7). NOIRLab Data Lab returned 502 all session, so the DR10 viewer was used instead.
- Near-IR: VHS DR5 (VizieR II/367, Harvard mirror) and VHS DR6 (VSA free SQL); UHS DR3 and UKIDSS LAS DR11+ (WSA free
  SQL); VHS DR6 / UHS DR3 image stacks (WFAU GetImage, 1' and 4' cutouts); 2MASS PSC stars in the 4' cutouts
  (VizieR II/246) to calibrate our own aperture photometry.
- Known sources: SIMBAD (Harvard TAP, 30"), Milliquas v8 (VII/294), NVSS, FIRST, Gaia DR3 QSO and galaxy candidates
  (I/356), SDSS DR16 (V/154), Pan-STARRS DR1 (II/349).
- Photosphere: Montreal pure-H DA synthetic photometry (`data/models/montreal/Table_DA`, Bergeron group, 2021 grid),
  colours (band - G) interpolated at the Gentile Fusillo+ 2021 TeffH and log gH and anchored on the observed Gaia G;
  uncertainty = +-150 K in Teff plus 0.03 mag.

## Method

1. **Moves with the white dwarf?** CatWISE2020 position vs Gaia DR3 propagated to the CatWISE mean epoch, and CatWISE
   vs Gaia proper motion. Both were calibrated on 600 field stars (Gaia stars with significant parallax or motion,
   no Gaia neighbour within 8", CatWISE W1 15.5-18.0, within 8' of the targets): the CatWISE position errors are
   **underestimated by a factor 1.5-1.7** at these magnitudes, with per-field offsets of up to 0.14"; the motion
   errors are realistic (scale 1.04-1.07) with field biases up to 20 mas/yr. Targets are compared after removing the
   field bias and scaling the errors, and against the empirical distribution of field stars of the same W1 (+-0.75).
   Two hypotheses for the motion: (a) the whole W1 source co-moves; (b) the W1 excess is a stationary background
   source unresolved from the WD, so the blend moves at (1 - f) times the Gaia motion, f = excess fraction of W1.
2. **Extended sources in the beam:** DR10 Tractor sources within 8" with type != PSF; their Tractor forced W1, and the
   W1 that galaxies of the same z magnitude have in the surrounding 3' field (median, 90th percentile, fraction
   reaching the excess flux). Chance alignment: CatWISE density of sources at least as bright as the excess.
3. **Near-IR:** catalogue photometry and morphology (VHS/UHS class, pStar/pGalaxy), and our own 1"-radius aperture
   photometry on the stacks with the zero point from 2MASS stars in the same 4' cutout (checks against the catalogue
   J/H: our values are 0.0-0.16 mag brighter, so ~0.1 mag systematic). K expected if the W1/W2 excess were a
   blackbody at the temperature fitted earlier (`data/irx/excess_bb_fits.csv`, two-point fits, indicative only).

## Results

Photosphere (Montreal DA, Vega) vs observed W1/W2 (DR11 forced unWISE; CatWISE in brackets):

| WD | G | Teff (K) | pm (mas/yr) | W1 phot / obs | W2 phot / obs | excess fraction of W1 |
|---|---|---|---|---|---|---|
| WDJ033256.37-174323.78 | 19.42 | 5,445 | 47 | 17.83 / 16.93 (16.91) | 17.78 / 16.53 (16.68) | 0.56 |
| WDJ080323.85+163357.90 | 18.65 | 5,566 | 223 | 17.13 / 16.51 (16.54) | 17.09 / 16.29 (16.50) | 0.43 |
| WDJ163917.47+103604.84 | 18.52 | 6,386 | 47 | 17.40 / 16.80 (16.75) | 17.38 / 16.48 (16.61) | 0.42 |
| WDJ120726.77-075444.26 | 19.86 | 5,647 | 31 | 18.39 / 17.45 (17.36) | 18.35 / 17.00 (16.61) | 0.58 |

(The Montreal photosphere gives a slightly larger excess than the earlier blackbody estimate; it does not change any
conclusion.)

### 1. CatWISE2020 vs Gaia DR3

| WD | CatWISE source | offset E, N (") | offset, calibrated | field stars with larger offset | CatWISE pm (mas/yr, bias-corrected) | Gaia pm | difference | field stars with larger difference |
|---|---|---|---|---|---|---|---|---|
| 033256 | J033256.37-174325.0 | -0.28, -0.62 | 2.4 sigma | 18 % | (+76 +- 56, -52 +- 57) | (+19.2, -43.0) | 1.0 sigma | 55 % |
| 080323 | J080323.83+163354.5 | +0.66, +0.06 | 2.5 sigma | 18 % | (-45 +- 48, -70 +- 52) | (-50.9, -217.3) | **2.8 sigma (in Dec)** | **3.0 %** (of 428) |
| 163917 | J163917.43+103605.2 | +0.05, -0.03 | 0.2 sigma | 97 % | (-21 +- 43, -19 +- 53) | (-38.8, +26.6) | 1.0 sigma | 60 % |
| 120726 | J120726.69-075444.4 | -0.75, +0.15 | 2.5 sigma | 18 % | (-3 +- 86, -133 +- 102) | (-23.5, -19.8) | 1.1 sigma | 51 % |

- **Positions:** none of the offsets is significant once the CatWISE errors are calibrated: 18 % of field stars of
  the same W1 show offsets as large. AllWISE (2010.6) and unWISE agree in direction for 033256 (0.53" and 0.79", to
  the SSW) and 080323 (0.32", 0.40", to the E), but those catalogues share data with CatWISE.
- **Motions:** only WDJ080323 moves fast enough for the test to have power. Its W1 source moves at -70 +- 52 mas/yr
  in Dec, while the white dwarf moves at -217 mas/yr: 2.8 sigma, matched or exceeded by 3 % of field stars (12 %
  chance that one of four targets does so). A blend with a stationary source carrying the 43 % excess predicts
  (-29, -123) mas/yr, which fits (chi2 1.1 against 7.9 for full co-motion; likelihood ratio ~30 for Gaussian
  errors). For the other three the CatWISE error (43-102 mas/yr) is larger than the motion (31-47 mas/yr), so the
  test cannot distinguish (likelihood ratios 0.7-1.3).
- **Gaia-AllWISE figure of merit:** 080323 FoM 6.9 (AllWISE W1 S/N 13.2), 163917 FoM 5.4 (S/N 12.1), 033256 FoM 5.7
  (S/N 12.3): none meets Dennihy's "S/N > 10 and FoM < 4" confusion flag. WDJ120726 has no AllWISE counterpart at
  all (the nearest AllWISE source is 8" to the S).
- **unWISE morphology:** spread_model_1 = 0.008 +- 0.003 for WDJ120726 (2.8 sigma extended; centroid 1.45" from the
  WD); 0.000-0.002 (consistent with a point source) for the other three.

### 2. Extended sources in the beam (Legacy Surveys DR10)

| WD | source | sep. | type, r, z (AB) | Tractor W1 (nmgy) | same-z field galaxies: median / 90th pct W1 | fraction reaching the excess | z - W1 needed to make all the excess |
|---|---|---|---|---|---|---|---|
| 033256 | galaxy WNW | **2.6"** | REX, 23.5, 22.6, r_e 0.2" | 0.02 +- 0.49 | 1.3 / 5.2 (66 galaxies) | 0 % (excess 7.9 nmgy) | 2.35 |
| 033256 | galaxy N | 7.4" | REX, 23.5, 22.5 | 0.49 +- 0.59 | 1.3 / 5.3 | 2 % | 2.2 |
| 163917 | point source NW | 7.1" | PSF, 21.7, 20.5 | 3.3 +- 0.5 (modelled) | 2.9 / 5.3 (stars) | 4 % | 0.1 |
| 120726 | galaxy SSW | **7.7"** | REX, 23.9, 22.1 (very red) | **8.8 +- 0.6** | 2.4 / 10.8 (43 galaxies) | 33 % (excess 5.0 nmgy) | 1.4 |
| 080323 | nothing within 9" | | | | | | |

- WDJ080323: no DR10 source within 9" (z 5-sigma depth ~23.4), and SDSS DR16 (2004-05, when the WD was 2.5" further
  north) shows nothing within 12" except the WD itself. A stationary contaminant would have to be optically very faint
  and IR-bright (z - W1 > ~3 AB).
- WDJ033256: the 2.6" galaxy sits well inside the beam. Tractor gives it no W1 flux, but the split between two sources
  2.6" apart in a 6" PSF is fragile; typical galaxies of its z magnitude have 1-5 nmgy in W1, i.e. 15-65 % of the
  excess. Its direction (WNW) does not match the CatWISE offset (SSW).
- WDJ120726: a red galaxy at 7.7" (inside Dennihy's 7.8" radius) is as bright in W1 as the white dwarf itself.
- Chance of an unrelated CatWISE source as bright as the excess (W1 17.4-18.0) within 1" / 2" / 3" of a given WD:
  0.3-0.6 % / 1.4-2.5 % / 3.1-5.5 %.
- Known background sources: none. Within 30" SIMBAD lists only the white dwarfs; no Milliquas, NVSS, FIRST or Gaia
  DR3 QSO/galaxy candidate. WDJ163917 has an SDSS BOSS spectrum (plate 4075, MJD 55352) classified STAR, z ~ 0
  (DR16Q superset): the white dwarf itself.

### 3. Near-IR imaging and K band

| WD | survey | catalogue (Vega) | class | our aperture phot. | photosphere | K if the excess were real |
|---|---|---|---|---|---|---|
| 033256 | VHS DR6, 2016 | J 18.42 +- 0.04; no Ks in catalogue | **J extended (classStat 2.6, pGal 0.90)** | J 18.39 +- 0.05, Ks 17.96 +- 0.22 | J 18.30, Ks 17.95 | Ks 17.52 (1,375 K) |
| 080323 | UHS DR3, 2013-2021 | J 17.53 +- 0.04, H 17.25 +- 0.05, K 17.35 +- 0.15 | point (pStar 0.94) | J 17.43, H 17.13, K 17.01 +- 0.27 | J 17.58, H 17.31, K 17.22 | K 16.86 (1,850 K) |
| 163917 | UHS DR3, 2012-2024 | J 17.68 +- 0.04, H 17.43 +- 0.07; no K | point (pStar 0.99) | J 17.63, H 17.27, K 17.18 +- 0.22 | J 17.71, H 17.48, K 17.44 | K 17.24 (1,225 K) |
| 120726 | VHS DR5, 2010 | J 18.75 +- 0.11, Ks 18.15 +- 0.22 (J - Ks 0.61 +- 0.25) | **galaxy (pGal 0.997; classStat 1.0-1.7)** | J 18.64, Ks 17.94 +- 0.16 | J 18.82, Ks 18.51 | Ks 18.13 (1,200 K) |

- No near-IR image (seeing 0.8-1.0") resolves a second source within 5" of any of the four; the WD is the only
  detection inside the WISE beam in VHS/UHS (the 7.1" point source near 163917 is detected by UHS in J/H).
- J and H are photospheric for all four, as expected for an excess that only appears beyond 3 um.
- K: WDJ080323's UHS K (17.35 +- 0.15) is photospheric and 3.2 sigma fainter than a 1,850 K source making the W1/W2
  excess would give (our own K, 17.01 +- 0.27, cannot decide). WDJ033256's Ks (our measurement, no catalogue value)
  is photospheric, 2.0 sigma below a 1,375 K source. WDJ163917's K (ours only) lies between the two models. WDJ120726
  is red in Ks (0.36 +- 0.23 mag catalogue, 0.57 +- 0.17 ours), but VHS calls it extended. The excess temperatures
  are two-point fits; cooler dust would add less K, so K excludes a hot companion only, not a cool disk.
- UKIDSS LAS has no coverage/detections for the two northern stars (WSA query empty); UHS DR3 provides the imaging.

## Verdicts

| WD | verdict | why |
|---|---|---|
| WDJ033256.37-174323.78 | **inconclusive, at risk** | A galaxy (z = 22.6) 2.6" from the WD inside the W1 beam; galaxies of that magnitude typically carry 15-65 % of the excess flux, and Tractor's zero W1 for it is not a robust split. VHS J classifies the WD's J detection as extended (2.6 sigma). The motion test has no power (1.0 sigma, 47 mas/yr against 56 mas/yr errors). Ks is photospheric. |
| WDJ080323.85+163357.90 | **weakened: inconclusive, leaning confused** | The best test case (223 mas/yr): the CatWISE W1 source moves slower than the white dwarf by 2.8 sigma (3 % of field stars; 12 % for one of four), as expected if ~40 % of W1 came from a stationary source; UHS K is photospheric and disfavours a >= 1,800 K companion at 3 sigma. Against confusion: nothing in DR10 or SDSS images within 9-12" at any epoch, point-like in UHS, FoM 6.9 passes Dennihy's flag. |
| WDJ163917.47+103604.84 | **survives, but weakly tested** | CatWISE position agrees with Gaia to 0.06" (0.2 sigma), so a stationary contaminant carrying the 42 % excess would have to lie within ~1" of the WD (chance for a CatWISE-level source 0.6 %); no galaxy within 11"; point-like in UHS J/H; FoM 5.4. But the motion test has no power (47 mas/yr vs 43-53 mas/yr errors), a 7.1" point source (modelled by Tractor; 26 % of the W1 PSF flux belongs to neighbours) lies inside Dennihy's 7.8" radius, and there is no catalogue K. Dennihy+ 2020 lost 36 % of candidates that had passed exactly these ground-based checks. |
| WDJ120726.77-075444.26 | **likely confused** | VHS classifies the near-IR counterpart as a galaxy (pGal 0.997, though at low classStat); unWISE shows an extended source (2.8 sigma) whose centroid is 1.45" from the WD; CatWISE is offset 0.75" W; no AllWISE detection; a very red galaxy 7.7" away is as bright in W1 as the WD; CatWISE W1 - W2 = 0.75. |

Overall: **one of four survives these checks, and that one only because the strongest test (proper
motion) has no power for it.** None of the four can be claimed as a dusty white dwarf from WISE data; confirming
WDJ163917 (and settling WDJ080323) needs resolved 3-5 um imaging (JWST/NIRCam or a ground-based L/M' image on a
large telescope) or, for a companion, a near-IR spectrum. These results do not support writing the excesses up as
discoveries; they belong in the paper plan as "candidates that fail / survive confusion tests".

## Limitations

- The calibrated CatWISE position errors still have heavy tails (18 % of field stars beyond 2.4-2.5 sigma), so
  position offsets are weak evidence either way. Field stars may themselves include blends, which makes the empirical
  tail probabilities conservative.
- Our aperture photometry on the WFAU stacks is ~0.1 mag brighter than the catalogue in J/H; the K values without a
  catalogue counterpart (033256 Ks, 163917 K) carry that systematic. No 2MASS-to-MKO/VISTA colour terms applied.
- The "K if real" predictions depend on two-point blackbody fits (W1, W2) whose temperature is poorly constrained.
- The EDR3 cross-match figure of merit may not be on exactly the DR2 scale Dennihy used.
- The galaxy-W1 estimates use Tractor forced W1 for field galaxies, which is itself noisy at these fluxes.
- Not done: per-epoch unWISE astrometry (would need the time-resolved coadds), Spitzer archive (no Spitzer
  observations of these four were searched for in this pass).

## References (read)

- Dennihy E., Farihi J., Gentile Fusillo N. P., Debes J. H. 2020, ApJ 891, 97, "A Word to the WISE: Confusion is
  Unavoidable for WISE-selected Infrared Excesses" (arXiv:2002.01021, full text read 2026-11-28).
- Our earlier notes: research/notes/irx-second-pass.md, research/reports/2026-11-07-ir-excess-second-pass.md.

Catalogues used as data (papers not re-read here): Gaia DR3; CatWISE2020 (Marocco et al. 2021; column definitions
read from the IRSA TAP schema); AllWISE; unWISE catalogue (Schlafly et al. 2019); Legacy Surveys DR10 (Dey et al.
2019); VHS (McMahon et al. 2013); UHS (WFAU); 2MASS; SDSS DR16 and DR16Q superset; Pan-STARRS DR1; Montreal
white-dwarf photometry tables (Bergeron group).
