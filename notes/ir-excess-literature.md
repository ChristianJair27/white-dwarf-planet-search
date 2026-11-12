# Infrared excess around 100 pc white dwarfs: literature check (2026-10-29)

Purpose: decide whether an infrared-excess (IR-excess) search of our Gaia 100 pc sample
(16,676 WDs: Gentile Fusillo+ 2021, Plx > 10 mas, Pwd > 0.75; `wdplanets/catalog.py`) using
NOIRLab Astro Data Lab tables (Legacy Surveys Tractor forced unWISE photometry, plus
CatWISE/AllWISE/unWISE/VHS/UKIDSS/2MASS) is worth weeks of work, and which angle is defensible.

Method: papers were opened through arXiv (abstract pages, HTML, or PDF converted to text with
`pdftotext`), journal/repository pages and Legacy Surveys documentation. CDS (VizieR, SIMBAD) and
the SVO archive (svocats.cab.inta-csic.es, ECONNREFUSED) were unreachable on 2026-10-29, so no
published candidate table was downloaded. The Data Lab schema was queried directly. Anything seen
only in a search-engine snippet is marked **UNVERIFIED**. The References section says how deeply
each item was read.

---

## 1. Published IR-excess searches that overlap a Gaia 100 pc sample

| Study | Sample | IR data | Excess / vetting | Result | Table public? |
|---|---|---|---|---|---|
| **Rebassa-Mansergas+ 2019** (RM19) | Gaia DR2 100 pc, 8,555 WDs; BP-RP < 0.8 and >= 3 IR points: 3,733 | VO: 2MASS, UKIDSS, VISTA, WISE (AllWISE per Murillo-Ojeda+), Spitzer SEIP | VOSA SED fit; slope test from 2.15 um; > 3 sigma points; Aladin inspection removed 221 of 377 | 77 candidates (52 new) + 33 mid-IR-only; disk fraction 1.6 +/- 0.2 % (2.6 +/- 0.3 % after completeness), BD companions 0.1-0.2 % | Tables in paper |
| **Xu, Lai & Dennihy 2020** (Paper I) | Gaia DR2, all-sky, **G < 17.0**, Pwd > 0.75: 6,002 -> 3,065 with unWISE W1+W2 -> 2,847 with no background object within 3" | **unWISE catalogue** (Schlafly+ 2019), not forced at optical positions | W1/W2 magnitude excess and W1-W2 colour excess (Wilson+ 2019 method) | 188 candidates, 147 new | VizieR J/ApJ/902/127 + arXiv ancillary CSVs |
| **Lai+ 2021** (Paper II) | Follow-up of Paper I | Spitzer IRAC 3.6/4.5 um for 174 WDs; Gemini JHK for 235 | Confirm/refute unWISE excess; J-band excess (chi_J >= 3) flags companions | 62 confirmed (10 likely companions, 52 possible disks). Spitzer confirmation 95 % for colour+flux candidates, 79 % for all observed Paper I candidates, about 25 % for colour-only | Tables in paper |
| **Dennihy+ 2020** | 22 AllWISE-selected candidates near the WISE faint limit (not a Gaia volume sample) | Spitzer follow-up of **AllWISE**; no Legacy Survey data | Ground-based NIR imaging and astrometric filtering tested | 8/22 (36 %) were source confusion even after vetting | Table in paper |
| **Madurga Favieres+ 2024** | Gentile Fusillo EDR3 WDs, **G < 18.5**: 41,020 (64 of the candidates are within 100 pc) | **CatWISE2020** | Magnitude + colour excess; strict thresholds (chi > 8 or 30 depending on G, as described by Murillo-Ojeda+) | 554 candidates, 446 new; IR-excess fraction about 6 % | VizieR J/A+A/688/A168 |
| **Bravo+ 2025** (AJ 169, 100) | Gentile Fusillo 2021, parallax >= 10 mas: **16,959 WDs** (essentially our sample) | **CatWISE2020** W1/W2 (W2 S/N > 10), UHS/UKIDSS/VHS/VVV/VIKING; Pan-STARRS/DES/NSC/SkyMapper; DECam cutouts via Data Lab | Colour cut BP-RP < 0.417(G-W2) - 0.10; Gaia neighbour within 3" rejected; visual inspection | Ultracool companions: 54 resolved (31 new) + 74 unresolved IR excess (17 new in the body text; the abstract says 20) | Tables in paper |
| **Murillo-Ojeda+ 2026** (A&A 707, A268; "Paper I") | Jimenez-Esteban+ 2023 100 pc sample (12,718 WDs after RUWE/flux cuts); **only the 8,150 with BP-RP < 0.86** (Teff >~ 5,500 K) that have Gaia XP; 5,084 with >= 3 good IR points | 2MASS, UKIDSS, VISTA (VHS, VIKING, VVV, VMC), **CatWISE2020** (W1/W2 only), Spitzer GLIMPSE/SEIP; proper-motion-corrected 3" match | VOSA; >= 2 points > 20 % and > 3 sigma above the model; Aladin inspection (DESI Legacy, PS1, SDSS, DSS2, 2MASS, UKIDSS, VISTA, WISE images) rejected 218 of 674 | **456 IR-excess WDs (292 reliable, 164 tentative), 75 % new**; fraction 5.9 +/- 0.3 % (reliable) to 9.2 +/- 0.4 %; contamination <= 15 % (their estimate) | VizieR + SVO archive of WDs from Gaia (both down today) |
| **Guidry+ 2024** (ApJ, arXiv:2406.18646) | Gaia eDR3 **100 pc**, Pwd > 0.75, **G_RP < 17**, catWISE W2 S/N > 5: 3,215 WDs | Own aperture photometry (5.5") on **unWISE epochal coadds** from the 2023 NEOWISE release, about every 6 months 2013-2023 | Reduced chi^2 of the W1 light curve; scan-angle and crowding cuts | 163 variables (chi^2 > 2), **104 high-confidence (84 new)**; 6/11 Ca II gas-disk WDs and 9/17 other dusty WDs are high-amplitude variables | Table 2 (appendix) |
| Wang & Liu 2026 (RAA, arXiv:2604.11175) | DESI EDR spectroscopic WDs: 2,670 parent, 316 with full coverage | SDSS, PS1, UKIDSS, 2MASS; **CatWISE2020 W1/W2, AllWISE W3/W4** | VOSA; Pan-STARRS/SDSS/2MASS/UKIDSS images within 6" | 62 reliable (38 disk candidates, 5 WD+BD, 3 WD+M, 16 ambiguous); disk candidate rate 38/316 = 12 %, which they call a selection-dependent candidate fraction | VizieR (link in PDF) |
| Wang+ 2026 (ApJ, arXiv:2603.10481) | LAMOST DR11: 3,092 WDs, 1,818 SED-fitted | WISE + 2MASS + UKIDSS. CatWISE2020 first with AllWISE fallback: **UNVERIFIED** (snippet) | VOSA | 139 candidates (66 disks, 19 WD+BD, 30 WD+M, 24 ambiguous) | Not checked |

Not found, or not relevant to a 100 pc IR search:
- No **Estrada-Dorado 2023** WD IR-excess paper could be located.
- **Rogers+ 2020** is UKIRT JHK monitoring of 34 known dusty WDs, not a search.
- No "Rogers+ 2024" IR-excess search was found.
- **O'Brien+ 2024** (40 pc sample): the abstract seen in a snippet mentions no IR-excess analysis (**UNVERIFIED**).
- **Kilic+ 2025** (100 pc SDSS footprint II) is about spectral evolution.
- **Manser+ 2024** (DESI EDR WD catalogue) did not do an IR-excess search; Wang & Liu 2026 did, using its sample.
- **Wilson+ 2019** (Spitzer + HST, 195 single WDs): 3 dusty disks, 1.5 (+1.5/-0.5) %; only 1 of 30 polluted WDs has an excess (**UNVERIFIED**: search excerpts only).

**Did anyone use Legacy Surveys Tractor forced unWISE photometry for WD IR excess?** Not that
I could find. Several targeted searches (2026-10-29) returned nothing. In the papers read, the
Legacy Surveys appear only as:
- optical images for visual inspection (Murillo-Ojeda+ 2026);
- an optical-photometry reference and DECam cutouts (Bravo+ 2025).

Every catalogue search used AllWISE, the unWISE catalogue or CatWISE2020. This is absence of
evidence, not proof. DESI-internal WD work or brown-dwarf searches may use LS WISE fluxes without
saying so in the abstract.

**What Data Lab actually offers (queried 2026-10-29):**
- `ls_dr9`, `ls_dr10` and **`ls_dr11`** (3.93e9 sources). DR11 is north (DR9 reductions) plus the
  extended DECam south, with 22,731 deg^2 in all bands at >= 1 pass.
- Per the DR11 description, DR11 WISE fluxes come from "all imaging through year 11 of
  NEOWISE-Reactivation", force-photometered in the unWISE maps at the positions of the Legacy
  Surveys optical sources.
- The table `ls_dr11.wise` holds **time-resolved forced W1/W2 photometry, "up to twenty five
  unWISE coadd epochs"** (`lc_flux_w*`, `lc_mjd_w*`, etc.). DR10 has 17 epochs.
- Precomputed cross-matches: `ls_dr11.x1p5__tractor__gaia_dr3__gaia_source`, plus allwise and
  unwise_dr1.
- Also on Data Lab: `catwise2020`, `allwise`, `unwise_dr1`, `vhs_dr5`, `ukidss_dr11plus`,
  `twomass`, `des_dr2`, `delve_dr3`.
- Footprint caveat: DR9 targets |b| > 18 deg. A Legacy Surveys forum post says DR11 reaches
  roughly Dec < +30 at |b| > 10 deg. So **only part of our all-sky sample (my rough estimate:
  about 55-65 %) will have LS photometry**. This needs to be measured.

## 2. What is plausibly not done yet (with explicit uncertainty)

1. **Legacy Surveys DR11 forced W1/W2 (deblended against a deep optical model) for the whole
   100 pc sample inside the footprint.**
   - Not found in the literature (see above).
   - Forced photometry gives a flux, with an error, even where CatWISE has no detection or
     W2 S/N < 10. That was Bravo's cut, and Murillo-Ojeda needed >= 3 good IR points.
   - It also gives `fracflux_w1/w2`, the fraction of the modelled flux in the aperture that comes
     from neighbours: a quantitative blending metric that catalogue searches lacked.
   - The deep optical model (r ~ 23-24) should catch some of the faint neighbours that
     Dennihy+ 2020 found invisible in J/Ks. This is **my expectation, not a published result**.
   - Risk: modest. The Murillo-Ojeda+ team (a "Paper II" is announced), the Xu/Lai group and the
     DESI WD group could do the same.
2. **The WDs that Murillo-Ojeda+ 2026 did not analyse.** About 11,700 of our 16,676 were not
   SED-searched there:
   - BP-RP > 0.86 (cool WDs, Teff < ~5,500 K);
   - fewer than 3 good IR points;
   - not in the Jimenez-Esteban+ 2023 sample (RUWE >= 1.4, flux-excess cuts).

   Bravo+ 2025 covered this full volume with CatWISE, but only for red G-W2 colours, W2 S/N > 10,
   and with a companion focus. Warm-dust disks around cool WDs are rare (known dusty WDs span
   about 34,000-8,000 K according to Madurga Favieres+ / Lai+), so the expected yield here is
   mostly brown-dwarf companions and systematics.
3. **Independent re-vetting of published candidates with deblended photometry.** Murillo-Ojeda's
   164 "tentative" objects, plus Madurga's 64 and Bravo's unresolved excesses within 100 pc, can
   each be checked against LS forced fluxes, `fracflux` and the LS optical model. This has not
   been published as far as I can tell. It is low-risk and useful, but less exciting.
4. **Time-domain IR.**
   - Guidry+ 2024 already searched W1 variability for the 100 pc WDs with G_RP < 17 (3,215 objects,
     data to 2023). They did **not** analyse W2, PSF/forced photometry or fainter WDs, and they
     defer the pipeline to "K. De et al. in prep".
   - Swan+ 2019 (more than half of known dusty WDs vary at 3.4 um) and Noor+ 2025 (Spitzer:
     variability in 85 % of disks) cover known disks.
   - Still open: forced, deblended W1+W2 light curves to the end of NEOWISE (DR11, up to 25
     epochs) for (a) all IR-excess candidates fainter than G_RP = 17, and (b) W2 and W1-W2 colour
     changes. Noor+ found disks redder when dimmer, so colour behaviour in WISE could be tested.
   - Risk: the Guidry/De team is the obvious competitor. NEOWISE ended in 2024, so the dataset is
     final and anyone can do this.
5. **Cross-link to our transit work** (literature.md gap 2): run TESS/ZTF on the new or confirmed
   IR-excess list. As far as checked on 2026-10-05, this is still unpublished.

Not novel / not worth it: a CatWISE or AllWISE-based 100 pc search (done three times); W3/W4
disk searches (WD disks are "typically only detected in W1 and W2", Dennihy+ 2020); any claim of
a confirmed disk or brown dwarf from photometry alone.

## 3. False positives and standard vetting (key numbers)

- **Beam and confusion.**
  - WISE PSF FWHM is 6.1" (W1) and 6.4" (W2) (Wang & Liu 2026).
  - Dennihy+ 2020 adopt 1.3 x FWHM = 7.8" as the confusion radius.
  - Contaminants are often invisible in NIR images. "Background galaxies can rise in flux as a
    power law at the WISE wavelengths, escaping detection at optical and even near-infrared
    wavelengths" (Dennihy+ 2020).
  - Their verdict: WISE excesses are "guilty until proven innocent".
- **Measured false-positive rates.**
  - 36 % (8/22) for faint AllWISE candidates after vetting (Dennihy+ 2020).
  - unWISE Paper I candidates: 79 % confirmed overall, 95 % for colour+flux, about 25 % for
    colour-only (Lai+ 2021).
  - Visual inspection removed about one third of the VOSA excesses (218/674; Murillo-Ojeda+ 2026)
    and 221/377 in RM19.
  - Residual contamination <= 15 % for CatWISE + NIR (Murillo-Ojeda's estimate).
  - Colour-only excesses are mostly contamination, because contaminants are redder than WDs.
- **Standard checks.**
  1. Propagate Gaia proper motion to the IR epoch and match within about 3".
  2. Reject Gaia/LS neighbours within about 6-8"; inspect deep optical and NIR images.
  3. Require excess in >= 2 bands (W1 and W2) and both a flux and a colour excess.
  4. Compare Gaia vs CatWISE proper motions: a discrepancy flags confusion (Dennihy+).
  5. Check the Gaia-AllWISE figure of merit.
  6. Use DA vs non-DA models. Using DA-only models misses more than half of the non-DA excesses
     (Murillo-Ojeda+: 79 of 180), and cool He-atmosphere models are unreliable in the IR.
  7. Search SIMBAD for known binaries, CVs and subdwarfs (Xu+ removed 39 of 1,688 SIMBAD-typed objects).
  8. Final confirmation needs Spitzer-quality data (no longer available) or JWST, plus optical
     spectroscopy for metals or Ca II gas.
- **Disk vs brown dwarf vs M dwarf.**
  - Dust disks rarely show excess below about 2 um, because dust sublimates at the inner edge at
    about 1,600-2,000 K. A significant J-band excess (chi_J >= 3) points to a companion; known
    disks have mean chi_J = -0.03 +/- 0.89 (Lai+ 2021).
  - Low-mass stars also show y/J excess. A WD+M pair usually stands out already in Gaia/optical
    colours.
  - Brown dwarfs and disks look alike in W1/W2. NIR spectroscopy separates them (Owens+ 2023, seen
    only as a search result: **UNVERIFIED**).
  - All confirmed dusty WDs are metal-polluted (Farihi 2016, quoted by Dennihy+), so the absence of
    pollution argues against a disk.
- **Occurrence rates.**
  - Dusty disks around about 1-4 % of WDs (Murillo-Ojeda+ intro) or 2-4 % (Lai+ intro).
  - Spitzer, unbiased: 1.5 (+1.5/-0.5) % (Wilson+ 2019, **UNVERIFIED**) and 3.7 % for 134 DAs at
    17,000-25,000 K (Rocchetto+ 2015). Rocchetto+ conclude that about 90 % of disks implied by
    pollution are too faint to detect in the IR.
  - Gaia 100 pc: 1.6-2.6 % (RM19).
  - All IR excess (any cause): 5.9-9.2 % (Murillo-Ojeda+), about 6 % (Madurga+).
  - Unresolved brown-dwarf companions: 0.5-2 % (Lai+ intro, citing Girven/Steele/Casewell);
    0.1-0.2 % (RM19); "<~0.5 % of WDs with IR excess" (Murillo-Ojeda+ footnote).
  - **So for our sample we should expect a few hundred real excesses at most, and several
    times more spurious flags before vetting.**
- **Fractional luminosity.**
  - tau = L_IR/L_* for the 35 known Spitzer disks lies between 0 and about 3 % (Rocchetto+ 2015,
    Fig. 4 histogram range).
  - The observed tau is below the maximum for a flat, opaque disk with inner temperature
    1,500-1,800 K.
  - Physical meaning: a disk inside the Roche radius (about 1 R_sun) reprocesses at most a few
    per cent of the starlight. That is why the excess shows up only at >= 2-3 um, where the WD
    photosphere has faded, and why a cool or faint WD gives little contrast.
  - I did not find a single adopted tau threshold in what I read. Treat "tau > 1e-3" as a working
    rule, not a cited standard.
- **Legacy Surveys specifics to test before trusting them (my concerns, not from papers):**
  - How the forced WISE fit treats Gaia sources with high proper motion. unWISE coadds span
    2010-2024, so a 0.5"/yr WD moves several arcsec.
  - Whether Gaia-retained sources without optical model fits still get WISE fluxes.
  - The flux calibration of forced W1/W2 against CatWISE for isolated bright WDs.

## 4. Recommendation

This is worthwhile as a **careful, modest project, not a likely discovery engine**. The
bright-WD, 100 pc, catalogue-photometry version has been done three times in 2019-2026:
- RM19;
- Bravo+ 2025 on exactly our Gentile Fusillo 100 pc list;
- Murillo-Ojeda+ 2026, with 456 objects and a characterisation paper announced.

So "we found IR excess around 100 pc WDs" would mostly rediscover their lists.

The most defensible new angle is **deblended photometry**: run Legacy Surveys DR11 Tractor forced
W1/W2 (through NEOWISE year 11, with `fracflux` blending metrics and the up-to-25-epoch light
curves) over the whole 100 pc sample inside the LS footprint. Use it to:
1. **re-vet** the published 100 pc candidates (Murillo-Ojeda reliable + tentative, Madurga,
   Bravo, Xu/Lai) and say which survive deblending;
2. **extend** to the roughly 11,700 WDs that Murillo-Ojeda did not analyse (cool, faint, or
   lacking catalogue IR photometry);
3. add a **W1+W2 variability screen** of every candidate below Guidry+ 2024's G_RP = 17 limit.

The output would be a cleaned, flagged candidate list plus a measured false-positive rate for
catalogue-based searches. That is a citable data product even if no single object is new, and it
feeds our TESS/ZTF transit pipeline directly. Before any novelty claim:
- re-check arXiv for a Murillo-Ojeda "Paper II" and a "De et al." unWISE light-curve paper;
- download the Murillo-Ojeda and Madurga tables when CDS is back.

## References (what was actually read)

Full text read (PDF converted to text, relevant sections read):
- Murillo-Ojeda R., Jimenez-Esteban F. M., Rebassa-Mansergas A., Torres S. 2026, A&A 707, A268, arXiv:2602.10070 (sections 1-6 and data availability).
- Dennihy E., Farihi J., Gentile Fusillo N. P., Debes J. H. 2020, ApJ 891, 97, "A Word to the WISE" (UCL Discovery PDF).
- Xu S., Lai S., Dennihy E. 2020, ApJ 902, 127, arXiv:2009.00193 (abstract, sections 1-3).
- Lai S. et al. 2021, ApJ 920, 156, arXiv:2107.01221 (abstract, sections 1, 4, 5).
- Madurga Favieres C., Kissler-Patig M., Xu S., Bonsor A. 2024, A&A 688, A168 (abstract, sections 1-3.3; author PDF).
- Wang K.-Y., Liu Q. 2026, RAA (accepted), arXiv:2604.11175 (sections 2, 4.1, occurrence rates).
- Swan A., Farihi J., Wilson T. G. 2019, MNRAS 484, L109, arXiv:1901.09468 (abstract and introduction).
- Rocchetto M. et al. 2015, MNRAS 449, 574, arXiv:1410.6527 (abstract; text searched for fractional luminosity / Fig. 4).
- Farihi J. 2016, New Astron. Rev. 71, 9, arXiv:1604.03092 (text searched only; Fig. 12 description).

Abstract or HTML read (partly):
- Rebassa-Mansergas A. et al. 2019, MNRAS, arXiv:1908.11176 (ar5iv HTML, summarised; volume not checked).
- Bravo A. et al. 2025, AJ 169, 100, arXiv:2412.04597 (HTML, first ~70 % of the text).
- Guidry J. A. et al. 2024, ApJ, arXiv:2406.18646 (HTML, first ~70 % of the text).
- Rogers L. K. et al. 2020, MNRAS, arXiv:2003.13711 (abstract).
- Noor H. T. et al. 2025, MNRAS (accepted), arXiv:2508.13119 (abstract).
- Wang K. et al. 2026, ApJ (accepted), arXiv:2603.10481, LAMOST DR11 (abstract).
- Morales R. A. et al. 2025, arXiv:2509.12116, HETDEX (abstract).
- Legacy Surveys DR9, DR10 and DR11 "Description" pages and the DR10 "Catalogs" page (legacysurvey.org); Legacy Surveys forum thread "Legacy Surveys Early DR11".
- NOIRLab Astro Data Lab schema for `ls_dr11`, `ls_dr11.tractor` and `ls_dr11.wise` (queried 2026-10-29 with astro-datalab 2.22.1).

Seen only in search-engine snippets (**UNVERIFIED**):
- Wilson T. G. et al. 2019, MNRAS 487, 133, arXiv:1904.05891 (1.5 % disk frequency).
- O'Brien M. W. et al. 2024, MNRAS 527, 8687 (40 pc sample; IR excess not checked).
- Steele P. R. et al. 2011, arXiv:1102.0505 (unresolved BD companion fraction 0.3-1.3 %).
- Owens et al. 2023, AJ (NIR spectroscopy of 7 IR-excess WDs).
- Wang et al. 2023, ApJ, LAMOST DR5 (50 candidates, disk fraction about 1.4 %).
- Kilic M. et al. 2025, ApJ 979, 157 (100 pc SDSS II).
- Manser C. J. et al. 2024, MNRAS 535, 254 (DESI EDR WD catalogue).
- Marocco F. et al. 2021 (CatWISE2020; only quoted via Madurga+ and Murillo-Ojeda+).
