# Infrared excess, second pass (2026-11-07)

> **Correction 2026-11-08.** WDJ074231.99+285727.43, called below "the best unpublished candidate", is a published
> infrared-excess object: Girven+ 2011 (MNRAS 417, 1210, VizieR `ire` table, "0742+2857", photometric companion L6),
> Hogg+ 2020 (MNRAS 498, 12: GTC spectrum, M5-M6 companion suggested, "radial velocity follow up is required") and
> Wang+ 2026 (ApJ 1001, 81, table 3 "WD + BD or dust disk candidates", flagged as previously reported). Our cross-match
> had used only Xu+ 2020, Lai+ 2021, Madurga+ 2024 and Murillo-Ojeda+ 2026; the per-object SIMBAD bibliography
> (research/notes/irx-novelty-2026-11-08.md) caught it. Girven+ 2011 and Wang+ 2026 are now in the cross-match
> (`irx crossmatch`: with Debes+ 2011 WIRED too, 66 published, 47 new; recovery Girven 3/3, Wang 6/9, WIRED 4/20:
> WIRED's tables 6-8 are mostly WD+M candidates and are known to be contaminated, so the low number is expected).
> The objects with no individual study found in SIMBAD, arXiv or those lists are
> WDJ033256.37-174323.78, WDJ080323.85+163357.90, WDJ163917.47+103604.84 and WDJ120726.77-075444.26 (the last one
> marginal in the images): **three clean unpublished candidates plus one marginal**, with the caveats below. Our SED
> and light-curve analysis of WDJ074231 stays as a validation case: the method recovers a known excess at 19 sigma.

Code: `python -m wdplanets.irx excess` (adds the Gaia-G colour test and the saturation flag), `python -m wdplanets.irx crossmatch`
(published lists through the Harvard VizieR mirror; Lai+ 2021 from the arXiv source), `logs/p4.py` (tier-1 selection, SIMBAD,
cutouts, gallery), `logs/p7.py` (image verdicts, near-IR from Data Lab). Files: data/irx/irx_first_pass.csv (recomputed),
data/irx/irx_crossmatch.csv, data/irx/lit/*.csv, data/irx/tier1_new.csv, ../figures/irx_tier1_{1,2}.png.
First pass and its limitations: irx-first-pass.md. Literature: ir-excess-literature.md, irx-literature-2026-11-07.md.

## What changed since the first pass

1. **Saturation.** DECam saturates near 16th magnitude; the Tractor z flux of bright WDs is wrong and z-W1 comes out red.
   21 of the 128 first-pass candidates carried SATUR bits (among them LAWD 52, G = 12.8, and CPD-69 177, G = 11.4, 10 pc,
   which would have been "new" discoveries and are artefacts). Now `saturated` = maskbits & (SATUR_G|SATUR_R|SATUR_Z).
2. **Two colour systems.** The empirical locus (running median and MAD in 0.05-mag bins of BP-RP) is built for z-W1, z-W2
   and also for Gaia G-W1, G-W2 (G does not saturate here). A candidate must exceed 3 sigma in both systems; saturated stars
   are judged on G alone. Result: z-based 128, G-based 123, both: **113 candidates** (1.75 % of the 6,451 clean WDs), 16 of them
   saturated (kept only through G).
3. **Cross-match with the published lists** (positions within 5" + 10 yr of proper motion; Gaia id where available):

| List | their excess objects in our clean set | flagged by us | recovery |
|---|---|---|---|
| Xu, Lai & Dennihy 2020 (unWISE, G < 17; `Exs` not "...") | 41 | 25 | 61 % |
| Madurga Favieres+ 2024 table 1 (previously published excesses) | 39 | 29 | 74 % |
| Madurga Favieres+ 2024 table 3 (CatWISE, FinalExcess = Mag/Color) | 38 | 32 | 84 % |
| Murillo-Ojeda+ 2026 (456 objects, 292 reliable + 164 tentative) | 185 | 59 | 32 % |
| **Lai+ 2021, Spitzer-confirmed (52 disks + 10 companions)** | 12 | 11 | **92 %** |

   The one Lai+ 2021 miss and the low Murillo-Ojeda recovery (their list reaches J/H/K excesses and tentative objects that
   WISE alone cannot see; ExcessBeg is 2MASS/UKIDSS/VISTA for 67 of 456) are the expected behaviour of a W1+W2-only test.
   145 published excesses in our clean set are not flagged (median chi 0.6): mostly Murillo-Ojeda tentatives.

   Of the 113: **64 published, 49 not in any list.**

## Tier 1 (not published, not saturated, fracflux_w1 < 0.3, W2 S/N > 5, SIMBAD not a binary/galaxy): 20 objects

Image vetting (Legacy Survey DR10 g/r/z and unWISE NEO7 60" cutouts, 6" circle = WISE beam) and near-IR (Data Lab:
2MASS PSC, VHS DR5, UKIDSS LAS within 3"):

| WDJname | G | Teff (K) | d (pc) | chi1 / chi2 | ff_W1 | image | near-IR | status |
|---|---|---|---|---|---|---|---|---|
| WDJ074231.99+285727.43 | 17.66 | 8904 | 98 | 8.4 / 4.1 | 0.03 | clean, isolated | UKIDSS J 17.32 H 17.09 K 16.88: J photospheric, K red by ~0.3 | **best candidate** |
| WDJ123410.98+580815.53 | 16.60 | 13300 | 99 | 4.4 / 4.3 | 0.24 | clean, isolated | 2MASS J 16.78 H 16.58 K 16.55 (K near the 2MASS limit) | candidate |
| WDJ014710.96+301941.39 | 18.10 | 8877 | 97 | 3.8 / 5.4 | 0.19 | clean; W2 > W1 excess (red, disk-like) | none | candidate |
| WDJ033256.37-174323.78 | 19.42 | 5445 | 94 | 5.7 / 3.6 | 0.05 | clean | VHS J 18.42 only | candidate |
| WDJ080323.85+163357.90 | 18.65 | 5566 | 64 | 4.8 / 3.1 | 0.08 | clean | none | candidate |
| WDJ163917.47+103604.84 | 18.52 | 6386 | 74 | 5.2 / 3.7 | 0.28 | clean (DAH, magnetic) | none | candidate |
| WDJ120726.77-075444.26 | 19.86 | 5647 | 88 | 6.1 / 4.2 | 0.24 | marginal (faint in unWISE) | VHS J 18.75 H 18.77 Ks 18.15: J-Ks 0.6, red | candidate (near-IR supports) |
| WDJ134138.37-344730.85 | 19.98 | 4623 | 90 | 5.1 / 3.5 | 0.16 | clean, weak | VHS J 18.61 Ks 18.19 | weak |
| WDJ004949.18+290321.77 | 19.23 | 5583 | 90 | 4.8 / 3.0 | 0.16 | clean, weak | none | weak |
| WDJ162253.66+193143.73 | 18.23 | 7362 | 96 | 3.8 / 3.2 | 0.25 | clean, weak | none | weak |
| WDJ043729.37-594603.40 | 19.98 | - | 69 | 9.2 / 5.9 | 0.27 | nothing visible in unWISE; W2 S/N 5.6 | VHS J 19.48 | marginal |
| WDJ103546.96-003145.62 | 19.87 | 5194 | 99 | 4.4 / 3.5 | 0.15 | edge of DR10 coverage | UKIDSS J 18.74 H 18.26 K 18.54: photospheric | dropped |
| WDJ163708.43-325210.35 | 17.69 | 8917 | 93 | 22.7 / 10.5 | 0.24 | no DR10 optical; crowded unWISE (bulge direction) | 2MASS J 16.37 K 15.38; VHS J 17.92 Ks 17.28 (2MASS blended) | dropped (crowding) |
| WDJ174703.85+201120.03 | 18.52 | 6013 | 76 | 4.5 / 3.2 | 0.22 | crowded | none | dropped |
| WDJ142152.24+143646.09 | 18.94 | 5391 | 96 | 10.4 / 4.8 | 0.10 | second, redder source inside 6" | 2MASS J 16.51 K 15.45 (the neighbour) | blend |
| WDJ150549.34+330410.82 | 20.14 | 4285 | 100 | 10.4 / 6.1 | 0.15 | red neighbour at the circle edge | UKIDSS J 17.89 K 16.84 | blend |
| WDJ015614.22-102924.91 | 20.58 | 4986 | 99 | 8.8 / 3.7 | 0.28 | red companion inside the circle | none | blend |
| WDJ134215.39-320351.62 | 19.07 | 7410 | 95 | 8.5 / 5.2 | 0.15 | blue+red pair inside the circle | VHS J 18.61 | blend |
| WDJ235432.47+080404.64 | 20.74 | - | 96 | 10.6 / 5.7 | 0.02 | red point | UKIDSS J 16.98 H 16.36 K 15.85: G-J = 3.8, an M/L dwarf colour | not a WD (misclassified) |
| WDJ111424.68+334124.39 | 17.77 | 6883 | 98 | 16.0 / 7.4 | 0.03 | - | 2MASS J 16.27 K 15.21 | known DA+M (LP 264-22) |

**Outcome: 7 unpublished IR-excess candidates that survive images and near-IR (first seven rows), 3 weak, 1 marginal; 9 rejected.**
All seven are fainter than G = 16.6, i.e. outside Xu+ 2020 (G < 17 for all but one) and in the part of the 100 pc sample
that Murillo-Ojeda+ 2026 did not analyse with VOSA; that is where our strategy expected the remaining excesses to be.

## Caveats (not a discovery yet)

- Literature attrition: about one third of VOSA excesses died on image inspection (Murillo-Ojeda+ 2026) and Spitzer confirmed
  79 % of Xu's observed candidates but only about 25 % of the colour-only ones (Lai+ 2021). Our seven are 3-8 sigma objects
  at the WISE confusion limit; expect some to fail.
- Faint WDs (G 18-20) have W1 S/N 20-120 but W2 S/N 10-40; the chi2 values (3-5) are modest. Only WDJ074231 and WDJ120726
  have a near-IR K excess hint; the others have no J/H/K at all.
- The locus is empirical; cool WDs (< 5000 K, BP-RP > 1) with collision-induced absorption or He atmospheres sit off it.
  Three of the seven are 5,400-5,600 K; treat them with more suspicion than the 8,900-13,300 K ones.
- Gaia DR3 (ESA archive TAP, 2026-11-07) for the seven candidates, the three weak and the marginal one: RUWE 0.92-1.07,
  non_single_star = 0, ipd_frac_multi_peak = 0, astrometric_excess_noise_sig <= 1.3, parallax_over_error 17-229. No
  astrometric or resolved binary among them (a wide M-dwarf companion would show in RUWE or in the images).
- unWISE epoch light curves (Legacy Survey DR11 `ls_dr11.wise`, 22-25 coadd epochs 2010-2024, `logs/p9.py`,
  data/irx/wise_lightcurves.csv): the per-epoch forced fluxes are noisy at these magnitudes (W1 errors ~1.3-2.5 nmgy on
  8-23 nmgy, W2 errors ~4-7 nmgy), so only large effects show. WDJ074231.99+285727.43 is stable (W1 15-28 nmgy around
  23, reduced chi2 2.5 like the other faint stars; per-epoch fracflux <= 0.15). Two candidates are **not** stable:
  WDJ014710.96+301941.39 (W1 epochs -8 to +20, W2 -25 to +103 with per-epoch fracflux spikes to 5-7: a neighbour steals
  the fit in some epochs, so its W2-strong excess is unreliable) and WDJ123410.98+580815.53 (W1 epochs 3-37 nmgy, the
  lowest ones with fracflux 2.7-3.8: contamination by the brighter unWISE blob outside the circle). Both downgraded to
  "uncertain"; the candidate list is therefore **five** clean (WDJ074231, WDJ033256, WDJ080323, WDJ163917, WDJ120726)
  plus two uncertain, three weak and one marginal.
## VOSA SED fits (2026-11-08)

Files uploaded: data/irx/vosa_tier1.txt (positions only) and data/irx/vosa_tier1_phot.txt (same eleven objects plus our
unWISE DR11 W1/W2 forced fluxes in Jy; name map in data/irx/vosa_names.csv). VO photometry from 2MASS, UKIDSS, VHS,
Gaia DR3, SDSS DR12, Pan-STARRS DR2, DES, GALEX, APASS... with the AllWISE and NEOWISE services switched off: the
AllWISE catalogue gives only upper limits or blends for these G 17-20 stars (for WDJ033256 it returned a W2 flux 15x
the star's z flux, a neighbour), and the first run with AllWISE on showed W1 fluxes 3x our forced ones.

- VOSA's own excess detector (independent of our locus method) flags 7 of 11: WDJ074231 (excess **from W1**, the only
  one), WDJ033256, WDJ043729, WDJ014710, WDJ123410, WDJ134138, WDJ162253 (from W2). Not flagged: WDJ004949,
  WDJ080323, WDJ120726, WDJ163917 (all 5,500-6,400 K; VOSA's slope test is built for the Rayleigh-Jeans tail, which
  these cool stars only reach beyond 2 um).
- Chi-square fit, Koester DA models, Teff 5,000-30,000 K, log g 7.5-9.0, excess points excluded automatically:

| object | Teff VOSA | Teff GF21 | log g | chi2_red | Nfit/Ntot | W1 obs/phot | W2 obs/phot |
|---|---|---|---|---|---|---|---|
| WDJ074231.99+285727.43 | 8,500 | 8,904 | 7.5 | 15 | 17/20 (K fitted, W1 W2 excess) | 1.9 (22 sigma) | 2.2 (8 sigma); K 1.2 |
| WDJ033256.37-174323.78 | 5,500 | 5,445 | 7.5 | 39 | 14/15 | 2.2 | 3.0 |
| WDJ080323.85+163357.90 | 5,500 | 5,566 | 9.0 | 30 | 15/15 | 1.7 | 1.9 |
| WDJ163917.47+103604.84 | 6,250 | 6,386 | 7.5 | 22 | 16/16 | 1.5 | 1.9 |
| WDJ120726.77-075444.26 | 5,500 | 5,647 | 8.0 | 35 | 10/10 | 2.1 | 2.9 |
| WDJ004949.18+290321.77 | 5,500 | 5,583 | 7.5 | 36 | 15/15 | 2.0 | 2.5 |
| WDJ134138.37-344730.85 | 5,000 | 4,623 | 7.5 | 45 | 5/6 | 1.9 | 2.9 |
| WDJ162253.66+193143.73 | 7,250 | 7,362 | 7.5 | 13 | 14/15 | 1.2 | 1.8 |
| WDJ043729.37-594603.40 | 7,750 | - | 7.5 | 298 (bad fit) | 9/10 | 1.7 | 3.7 |
| WDJ014710.96+301941.39 | 9,000 | 8,877 | 8.0 | 7.5 | 15/16 | 1.3 | 3.4 |
| WDJ123410.98+580815.53 | 12,250 | 13,300 | 7.75 | 163 (bad fit) | 24/25 | 1.1 | 1.5 |

  "obs/phot" is the observed flux over the photosphere, with the photosphere approximated by a blackbody at the VOSA
  Teff scaled by the fitted dilution factor Md = (R/d)^2 (`logs/p11.py`, data/irx/vosa_fit_summary.csv); the Koester
  synthetic fluxes per filter are in VOSA's downloadable results (not downloaded yet: our call). The fitted
  Teff agree with Gentile Fusillo+ 2021 to within 300 K for all but the two bad fits, which is a check on the photometry.
- Reading: WDJ074231 has about twice the photospheric flux at 3.4 and 4.6 um and a ~20 % K-band bump: the shape of a
  warm dust disk or a late-type brown dwarf companion (a stellar M dwarf would dominate J and H, which are
  photospheric). The cool 5,500 K objects show W1/W2 ratios of 2-3 as well, but with chi2_red 30-45 and VOSA's own
  detector silent, so their photosphere is less certain; the 7,250-13,300 K ones have the smallest excesses.
- VOSA results archive downloaded (our decision, 2026-11-08): data/irx/vosa/vosa_results_136_full.tgz,
  extracted to data/irx/vosa/extracted/ (402 files: per-object SED, Koester fit, excess regression, plots, refs.bibtex).
  The Koester spectra in VOSA end near 2.6 um, so VOSA gives no model flux at W1/W2 either; the blackbody-scaled
  photosphere above is the right extrapolation for a pure-H atmosphere in the Rayleigh-Jeans tail. VOSA's excess
  regression (`<obj>.reg.dat`, column nsig = sigma above the Rayleigh-Jeans line fitted to the bluer points):
  WDJ074231 W1 19.3, W2 6.8 (line anchored on K); for the others the line is anchored on W1 and only W2 is tested:
  014710 12.3 (unreliable epochs), 123410 4.4, 043729 4.0, 134138 3.9, 162253 3.7, 033256 3.2, 163917 2.5, 004949 2.2,
  120726 2.2, 080323 1.4. So for the cool objects VOSA measures a W1-W2 colour excess (small), while our locus test
  measures a flux excess in both bands relative to the optical (large, 2-3x): both can be true at once, and the
  blackbody-scaled photosphere in the figures shows W1 and W2 equally high.
- Independent WISE pipelines (IRSA Gator, `logs/p14.py`, data/irx/tier1_wise_catalogs.csv; Vega magnitudes, ours =
  22.5 - 2.5 log10(flux) - AB offsets 2.699/3.339): CatWISE2020 and AllWISE agree with our forced W1 to 0.0-0.35 mag
  and with W2 to 0.1-0.4 mag (ours slightly brighter in W2, the deeper coadd). WDJ074231: ours W1 16.35, W2 16.18;
  CatWISE 16.48±0.04, 16.36±0.09; AllWISE 16.44±0.08, 16.73±0.34 (ph_qual AB). WDJ080323: ours 16.51/16.29, CatWISE
  16.51/16.47, AllWISE 16.50/16.67. WDJ163917: 16.80/16.48, CatWISE 16.72/16.67, AllWISE 16.75/16.63. WDJ033256:
  16.93/16.53, CatWISE 16.92/16.79, AllWISE 16.97/16.93. WDJ120726: 17.45/17.00, CatWISE 17.33/16.59. The excesses
  (0.7-1.2 mag over the photosphere) are far larger than these pipeline differences, so they are not a forced-
  photometry artefact. (The Harvard VizieR mirror does not serve II/328, II/363 or II/365: use IRSA for WISE catalogues.)
- Blackbody fit to the excess (`logs/p15.py`, data/irx/excess_bb_fits.csv; excess = observed minus the scaled
  blackbody photosphere in K, W1, W2; two or three points, so T is indicative only): WDJ033256 1,375 K, WDJ080323
  1,850 K, WDJ163917 1,225 K, WDJ120726 1,200 K, WDJ074231 1,450 K (K+W1+W2, chi2 4). The excess-to-star luminosity
  ratios are large, L_IR/L_WD = 0.02-0.09, because these are faint 5,500-6,400 K white dwarfs (L ~ 1e-4 Lsun):
  known dust disks sit at 1e-3 to 1e-2, so for the cool candidates a substellar or late-M companion is the more
  natural reading of a 2-3x excess, if it is real; WDJ074231's 0.02 at 1,450 K is in the range Hogg+ 2020 debated
  (their spectrum says hot DA + M5-M6, Girven's photometry said 9,000 K + L6). None of this is settled by photometry.
- Injection-recovery test (`-m wdplanets.irx_inject`, data/irx/injection.csv, ../figures/irx_injection.png;
  3,000 clean non-candidate WDs, blackbody excesses at 600-2,500 K added to W1/W2 with the real noise, chi recomputed
  against the real locus): the rule (3 sigma in z-W1, z-W2, G-W1, G-W2; W2 S/N > 3) recovers 50 % of excesses
  that double the W1 flux of a 1,000 K source at G 17-18.5 (72 % at 1.0x, 44 % at G >= 18.5, 91 % at G < 17);
  at 0.5x the W1 flux it recovers 20 % overall (48 % bright, 10 % faint); hotter excesses (2,500 K) are recovered
  less because they add less to W2. False-positive floor with zero injected excess: 0.1 %, against the 1.75 %
  candidate rate: the candidates are not noise, even if some are blends. Our survey is therefore sensitive to
  bright, companion-like excesses (1-3x) and nearly blind to the 10-30 % excesses of faint dust disks at G > 18.
- The 47 unpublished candidates outside tier 1 (`logs/p17.py`, data/irx/new47.csv): 29 excluded, all by the blend
  cut (fracflux_w1 >= 0.3; 2 also saturated, 2 also W2 S/N <= 5). Eleven with moderate contamination (0.3-0.6) and
  W2 S/N > 5 are shown in ../figures/irx_rescue_1.png for inspection. Image verdicts (data/irx/new47.csv): 5 blends,
  1 not a WD (red point), 1 weak, 1 marginal, 3 "rescued" (isolated). Epoch light curves of the three (`logs/p19.py`):
  **WDJ031123.36-291247.25** (G 18.4, 8,274 K, 88 pc, chi 13.9/5.9, fracflux 0.36) is stable (W1 reduced chi2 3.3,
  0.71-1.28) and has only catalogue papers in SIMBAD: it joins the clean unpublished list as a fourth object;
  WDJ205526.59+102536.62 (G 16.3, 13,000 K) is variable or contaminated by epoch (W1 chi2 20, 0.59-1.43) and was in
  Xu+ 2020's analysed sample without an excess flag: uncertain; WDJ001945.91-291227.33 has fracflux spikes to 25 in
  W1 epochs: contaminated, dropped.
- Gaia XP classes (Vincent+ 2024, J/A+A/682/A5, mirror) for the clean candidates: WDJ033256 "DA:" (P_DA 0.54,
  P_DC 0.16), WDJ080323 DA (0.78), WDJ163917 DA (0.98), WDJ031123 DA (1.0), WDJ074231 DA (1.0); WDJ120726 not in
  the catalogue; P_DZ = 0 for all. No metal signature at XP resolution (which cannot see the Ca lines of a cool DA),
  so pollution is neither supported nor excluded; a spectrum would settle it.
- Figures: ../figures/irx_vosa_seds.png (eleven panels) and ../figures/sed_WDJ074231.99+285727.43.png
  (`-m wdplanets.irx_sed`).

## Next

1. SED fit of the seven with model atmospheres (Koester DA / Bergeron cooling models) to measure the excess in flux units and a
   blackbody disk temperature; VOSA is the standard tool (needs an account).
2. unWISE/NEOWISE W1-W2 light curves from Data Lab `ls_dr11.wise` for the seven.
3. Gaia DR3 RUWE / non_single_star for the seven (the ESA archive TAP answers in a second).
