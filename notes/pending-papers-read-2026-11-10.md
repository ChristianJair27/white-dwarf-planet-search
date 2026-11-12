# Pending papers read in full, 2026-11-10

Five PDFs in `kindle/articulos/` (files 20-24) were read in full with the Read tool, including tables,
figure captions and appendices. Page numbers below are PDF page numbers (they equal the printed page
numbers in all five files). Every number is taken from the PDF; where I computed something from their
numbers, or interpret, it is marked **[my inference]** or **[my calculation]**. "not found" means I looked
and the paper does not state it.

Internal result being checked: `research/reports/2026-11-08-polluted-wd-wide-binaries.md`
(798 polluted WDs in the 100 pc sample, 6.5 ± 0.9 % with an El-Badry+2021 companion vs 12.0 % for a
distance- and G-matched control, suppression 0.54 ± 0.08; companion pairs with R < 0.1).

---

## 1. Noor et al. 2024 — arXiv:2403.08870

- **Title:** "White Dwarf Pollution: One Star or Two?" (p1).
- **Authors:** H. T. Noor, J. Farihi, M. Hollands, S. Toonen (p1).
- **Status in the PDF:** MNRAS preprint, "Accepted XXX", arXiv v2 19 Mar 2024 (p1). The published
  reference, as cited by Xu+2026 (p13) and Norambuena+2026 I (p15), is MNRAS 529, 2910.
- **Samples (p2):**
  - W19: 71 DAZ stars with Si II detected in the **ultraviolet with HST** (from Wilson+2019),
    14,000 < Teff < 31,000 K, cooling ages 9-300 Myr. Also used: 82 W19 DA stars without metals.
  - D07: 116 warm DZ (6,000 < Teff < 12,000 K) from Dufour+2007, SDSS spectroscopy.
  - H18: 101 cool DZ (4,500 < Teff < 9,000 K) from Hollands+2018a (MNRAS 477, 93), SDSS spectroscopy.
  - Cuts: Gaia DR3 5-parameter solution, proper motion > 5 mas/yr, parallax/error > 10 for both members.
  - **No distance limit.** Distances reach ~0.5 kpc (Fig. 2, p4); median field distances 0.29, 0.20 and
    0.14 kpc (p5).
  - Control ("fields"): Gaia DR3 white dwarfs in parallelograms around each sample on the colour-magnitude
    diagram, cleaned with the Gentile Fusillo+2021 catalogue: 15,218 / 15,917 / 15,779 stars (p2).
- **Wide-binary catalogue:** **not** El-Badry+2021. They run their own search: companion within projected
  1 pc, parallax and proper-motion criteria of El-Badry & Rix 2018, chance-alignment statistic R built
  following El-Badry+2021, high-confidence pairs R < 0.01 (p3-5).
- **Results (Table 1, p5).** Wide-binary fractions (per cent):
  - W19 DAZ: 7/71 = 10.6 (-3.2, +3.9). W19 DA (not polluted): 5/82 = 6.8 (-2.4, +3.1).
    Field 1: 7.08 (-0.20, +0.21); distance-adjusted 9.10.
  - D07 DZ: 0/116, < 1.6. Field 2: 7.54 (-0.20, +0.21); distance-adjusted 8.06.
  - H18 DZ: 0/101, < 1.8. Field 3: 8.38 (-0.21, +0.22).
  - Each DZ sample is "inconsistent with those of their corresponding fields by at least 3σ" (p5).
    With relaxed proper-motion criteria, one H18 star has a high-confidence companion that is itself an
    unresolved binary (hierarchical triple); counting it gives 1.64 (+1.50, -0.94) % for H18 (p6).
  - No suppression factor is quoted. **[my calculation]** As ratios: D07 < 1.6/8.06 ≈ < 0.20,
    H18 < 1.8/8.38 ≈ < 0.21; W19 DAZ 10.6/9.10 ≈ 1.2 (no deficit).
  - **No separation bins** (Fig. 3, p4, shows separations only for Field 1, to illustrate chance
    alignments). **No main-sequence vs white-dwarf companion split** (not found).
- **DA (hydrogen) polluted stars:** treated separately, and the result is the **opposite of a deficit**:
  the DAZ wide-binary fraction is within 1σ of the field and of non-polluted DAs (p5). They argue the
  DAZ-DZ difference cannot come from spectral evolution and that these DAZ stars will not turn into DZ
  stars (p6-7).
- **Explanation (p5, p7):** wide companions do not drive pollution, "even weakly"; delivery is
  "almost certainly driven by (as yet unseen) major planets". DZ stars look like a population of
  stars that evolved as singletons, like dusty WDs with IR excess. Proposed: two sub-populations, a
  strongly polluted one dominated by single stars (optical DZ, dusty WDs) and a weakly polluted one
  (UV-only DAZ) with field-like binarity (p7). Mergers mentioned "only for completeness" and called
  "severely problematic" (p7). No stripping / Kozai mechanism is proposed.
- **Future work (p7):** "insufficient unbiased samples of metal-enriched white dwarfs to test this
  possibility"; may become feasible with large spectroscopic surveys, to constrain the efficiency of
  metal enrichment among single WDs vs WDs in wide binaries.

## 2. Xu et al. 2026 — arXiv:2609.11798

- **Title:** "Planetary Accretion Is Less Frequent in Wide Binaries: Evidence from Metal-Enriched White
  Dwarfs in DESI DR1" (p1).
- **Authors:** Siyi Xu, L. K. Rogers, J. Najita, B. T. Gänsicke, P. Izquierdo, S. E. Koposov,
  C. J. Manser, A. Swan, ... and the DESI collaboration (p1).
- **Status in the PDF:** "Draft version September 11, 2026", AASTeX 7, arXiv v1 10 Sep 2026 (p1). Thanks
  an anonymous referee (p10). **Journal / "ApJ in press": not found in the PDF.**
- **Sample (p3):** DESI DR1 white-dwarf catalogue (Swan+2026, 44,409 WDs) → 32,456 after five quality
  cuts (P_WD ≥ 0.5, spectral-type confidence ≥ 0.8, fibre contamination ≤ 0.001, blue S/N ≥ 4,
  primary = True) → **2,805 cool helium-dominated WDs**, 5,000 ≲ Teff ≲ 11,500 K, cooling ages
  ~460 Myr - 6.4 Gyr, 0 < BP-RP < 1. Types DC, DQ (non-polluted) and DZ, DQZ, DZQ (polluted).
  Hydrogen-dominated DCs are explicitly excluded by the colour cut. **Distance limit: not found**
  (WDs reach G ≈ 20, Figs. 2-3, p7-8).
- **Wide-binary catalogue (p4):** **El-Badry, Rix & Heintz 2021**, R_chance_align < 0.01, WD RUWE < 1.25
  → 215 wide binaries: 183 WD+MS, 30 WD+WD, 2 unknown companion type. Separations 160-33,640 AU (p6).
  RV test on 482 systems: Pearson r = 0.677 vs 0.195 for random pairs (p4).
- **Control (p4):** 2,578 "single" cool He-dominated WDs (the 2,805 minus the 215 binaries and 12 with
  RUWE > 1.25).
- **Measured quantity:** the **enrichment fraction** f = (polluted)/(all) in binaries vs singles — the
  reverse conditional of ours (we measure companion fraction among polluted vs non-polluted).
- **Results:**
  - f(wide binaries) = 9.8 ± 2.1 %, f(single) = 20.5 ± 0.9 %, difference 4.7σ (abstract p2; text p4).
    Table 1 (p4) prints 20.6 ± 0.9 % for the singles (internal inconsistency; 530/2,578 = 20.56 %
    **[my calculation]**). With R < 0.1: 10.0 ± 2.1 %, 4.6σ (p4).
  - Counts (Table 1, p4): binaries DC 139, DQ 55, DZ 21; singles DC 1,661, DQ 387, DZ 528, DQZ 1, DZQ 1.
  - SDSS check: singles 839/3,665 = 22.9 ± 0.8 %; binaries 13/143 = 9.1 ± 2.5 % (p5).
  - **WD+WD vs WD+MS:** 2/30 = 6.6 ± 4.7 % vs 19/185 = 10.3 ± 2.4 %; "A larger sample is needed" (p5).
    Companion BP-RP distributions of enriched vs non-enriched systems are similar; "metal enrichment
    does not strongly depend on the physical properties of the companion star" (p6, Fig. 2 p7).
  - **Separation bins (p6, Fig. 4 p9):** 4/81 = 4.9 ± 2.5 % at < 1,000 AU (caption: 100-1,000 AU; the
    figure label reads 4/79) vs 15/121 = 12.4 ± 3.2 % at 1,000-10,000 AU (difference 1.8σ), and 2/15 at
    > 10,000 AU. "Tentative"; enrichment "further suppressed" below ≈ 1,000 AU (p10).
  - Tentative dependence on WD Teff (abstract p2); KS tests show no significant differences (p5-8).
  - **No suppression factor "0.48 ± 0.10" appears anywhere in the paper.** **[my calculation]**
    9.8/20.5 = 0.478, propagated error ±0.105. Converting their Table 1 counts to *our* metric
    (companion fraction among polluted / among non-polluted): 21/551 = 3.8 % vs 194/2,242 = 8.7 %,
    ratio ≈ 0.44 (± ~0.10 from Poisson on 21).
- **DA (hydrogen) polluted stars:** not analysed (He-dominated only). They cite Lizana-Vidal+2026
  (arXiv:2607.22911): homogeneous SDSS hydrogen-dominated sample, enrichment fraction "below ~1 % for
  both single systems and wide binaries" (p5). They also cite Noor+2024's field-like warm DAZ result and
  Wilson+2019's 8/12 = 67 (+10, -15) % enrichment for hot wide-binary WDs (p6), and summarise: warm
  (Teff ≳ 14,000 K) WDs show no binary effect, cool ones (≲ 11,500 K) do (p9).
- **Explanation (p2, p9):** binaries either start with a smaller planetary reservoir (planetesimal
  formation suppressed, especially < 200 AU) or deplete it faster during the early WD phase (more tidal
  disruption events early, so fewer left for cool WDs); possibly both.
- **Future work:** model each system's accretion level and its age dependence in singles vs binaries
  (p9-10); enrichment vs separation on the main sequence "beyond the scope" (p6); dependence on WD
  parameters deferred (p6); larger sample for WD+WD vs WD+MS (p5); unbiased survey of warm WDs in wide
  binaries (p10); companion chemistry vs accreted chemistry using the Table 2 sample (p9).
- Table 2 (p11) lists the 21 polluted WDs in binaries with Gaia DR3 IDs of both members (G = 17.5-19.9).

## 3. Norambuena, Charalambous & Aguilera-Gómez 2026 (I) — arXiv:2610.28896

- **Title:** "White dwarf pollution in wide binaries I: the effects of stellar evolution" (p1).
- **Authors:** C. Norambuena, C. Charalambous, C. Aguilera-Gómez (PUC Chile) (p1).
- **Status:** A&A manuscript, received 12 Aug 2026, "A&A proofs" running header (p2), thanks a reviewer
  (p14); arXiv v1 20 Oct 2026.
- **Type:** theory only (N-body, REBOUND + REBOUNDx tides + MESA tracks). No observational sample, no
  measured companion fractions.
- **Setup (p3-5, Table 1 p4):** 2 M☉ host → 0.6 M☉ WD; two mass-loss histories (fast: η_RGB = 0.35,
  η_AGB = 1.0; slow: 0.2, 0.5) (p3, p10); 1 M_Jup planet at 2, 3 or 5 au; 25 planetesimals of 4 lunar
  masses (≈ 1.2 M⊕ total) inside or outside the planet; **1 M☉ companion (fixed)** at a_B = 250, 500,
  1,000 au (pre-AGB), e_B = 0.01-0.9, i_B = 0-90°. 1,344 simulations, 5 realisations per fiducial cell
  (p5). Galactic tides and GR not included (p4, p9). Binary orbit expands by ≈ 2-3 (p6).
- **Results:** "pollution" = planetesimal reaching the Roche limit during the cool-WD phase
  (Teff < 25,000 K down to 5,000 K) (p5-6). The incidence of such late accretion **increases from
  a_B = 250 to 500 and 1,000 au** (p7, p9, Figs. 4, 6, 7); strongly suppressed for e_B = 0.9 at any
  separation (p9); inner discs pollute more than outer discs (p7). Mechanism: wider companions delay
  the onset of von Zeipel-Kozai-Lidov (ZKL) cycles on the planet (pre-WD at 250 au, hot WD at 500 au,
  cool WD at 1,000 au; Fig. 5, p9), so the reservoir survives into the WD phase; close companions
  "destabilize planetary systems too early, depleting the reservoir of small bodies before the host
  star reaches the WD phase" (p10). Stellar mass-loss history is a secondary effect (p14).
- **DA / atmosphere type:** not treated (theory). Introduction states "fractions of about 2 %" for the
  most strongly enriched populations citing Wilson+2019, Noor+2024 and Xu+2026 (p2) — the 2 % applies to
  Noor's DZ upper limits, not to Xu's 9.8 % **[my reading]**.
- **Explicitly NOT done:** no quantitative pollution frequencies or accretion rates ("we do not aim to
  derive accretion rates ... or make quantitative predictions of the frequency of WD pollution", p14);
  no comparison of binary vs single-star pollution rates yet ("As a next step", p14); a_B > 1,000 au and
  Galactic tides left for future work (p4, p14); GR omitted (p9); only one host mass and one companion
  mass. They caution that observed "binary fraction of polluted WDs" and "pollution fraction of WDs in
  binaries" are different quantities from differently selected samples (p13).

## 4. Norambuena, Charalambous & Aguilera-Gómez 2026 (II) — arXiv:2611.03291

- **Title:** "White dwarf pollution in wide binaries: the role of planetary mass" (p1).
- **Authors:** same three authors (p1). **Status:** Proceedings IAU Symposium 408 (p1); arXiv v1
  2 Nov 2026. 8 pages.
- **Setup (p2-3):** as paper I, fast mass-loss model only, **companion fixed at a_B = 250 au and 1 M☉**,
  planet of **10 M⊕ or 1 M_Jup** at 3 or 5 au, i_B 0-90°, e_B 0-0.9.
- **Results (p5-6, Fig. 2):** lower-mass planets let more planetesimals survive, so delivery persists
  into the cool-WD phase; Jupiter-mass planets deplete the reservoir earlier. Planet location (3 vs 5 au)
  has minor impact. At 250 au, ZKL is triggered pre-WD for all planet masses (planet engulfed); pollution
  is more frequent at low inclination and eccentricity (abstract p1, p5).
- "Planetary mass" here is the **planet's** mass, not the companion's. No observational numbers; no
  companion fractions; DA not treated. Points to paper I for the separation dependence (p6).
- **Future work:** not stated beyond the need to "jointly consider planetary architecture and binary
  dynamics" (p6).

## 5. Gentile Fusillo et al. 2026 — arXiv:2610.37773

- **Title:** "A double debris disc around a white dwarf sculpted by two planetary bodies" (p1).
- **Authors:** N. P. Gentile Fusillo, F. Lagos-Vilches, B. T. Gänsicke, C. J. Manser, D. Koester (p1).
- **Status:** arXiv v2 2 Nov 2026, Nature-style layout (Main / Methods / Extended Data); thanks
  "anonymous referees" (p25). Journal: not found.
- **Object:** WD J132800.85−145019.95, a helium-atmosphere WD (He lines, abundances as log Z/He; p12,
  p21). Teff = 17,424 ± 567 K, log g = 7.76 ± 0.19, M = 0.47 ± 0.09 M☉, cooling age 73 (+49, -26) Myr
  (p13, p21). Gaia parallax 2.014 ± 0.292 mas (p36), distance ≃ 500 pc (p32).
- **Discovery path (p2, p12):** flagged as a debris-disc host from an **infrared excess in VHS and WISE
  photometry**, then VLT/X-shooter spectra (2021-2023) showed Ca, Mg, Si absorption (accretion) and
  Ca II, O I, Mg I, Fe II emission (gas disc).
- **Result:** Ca II and O I emission lines are **quadruple-peaked** (first among 22 known gas-disc WDs),
  modelled as two coplanar gas rings at 0.14 (+0.01, -0.02) - 0.34 (+0.02, -0.05) R☉ and
  0.54 (+0.44, -0.16) - 1.93 (+0.10, -0.30) R☉, inclination 77 (+9, -13)° (p5). Mg I emission only from
  the inner ring; Mg would be detected at > 6σ in the outer ring if Ca/Mg were equal (p5, p18) →
  compositionally distinct rings. Fractional IR luminosity τ = 2.7 %, "one of the brightest" WD dust
  discs (p7, p20). Accretion rates are unremarkable; Ca in convection zone 1.53 × 10^20 g (p3).
- **Interpretation (p9-10):** each ring is generated by a planetesimal embedded in the dust (as in
  SDSS J1228+1040); inner body ≲ 45-172 km, outer up to ~350-3,500 km depending on density and strength.
  Alternatives considered: unresolved double WD (Gaia resolves ~0.3", i.e. ~150 au at 500 pc; judged
  very unlikely, p32-33), a single body opening a gap (p33), disc self-shadowing (possible but no
  evidence, p33-35).
- **Caveats they state:** IR SED modelling is degenerate; a flat-disc fit gives i = 0°, incompatible with
  the gas lines (p18); MCFOST fit not unique (p20); abundances have hard-to-quantify systematics (p14).

---

## Implications for the 2026-11-08 report

### Q1. Are our two "published" statements correct as written?

- **"Noor et al. 2024 for DZ stars": correct in substance, incomplete.** Noor+2024 find 0/116 and 0/101
  companions for two SDSS DZ samples (< 1.6 % and < 1.8 %) against field fractions of 7.54 % (8.06 %
  distance-adjusted) and 8.38 %, each > 3σ below the field (Table 1 and text, p5). What the report
  omits and must add: (a) in the same paper the **DAZ sample shows no deficit** (10.6 (-3.2, +3.9) % vs
  field 7.08 % / 9.10 %, p5), which directly bears on our H-atmosphere claim; (b) their deficit is much
  stronger than ours (**[my calculation]** ratio < 0.2 vs our 0.54); (c) the citation is now
  MNRAS 529, 2910 (as cited in Xu+2026 p13), not "MNRAS accepted".
- **"Xu et al. 2026 ... suppression 0.48 ± 0.10": the number is not in the paper.** Xu+2026 quote
  enrichment fractions 9.8 ± 2.1 % (wide binaries) vs 20.5 ± 0.9 % (singles), 4.7σ (p2, p4). 0.48 ± 0.10
  is our own ratio of those two numbers (**[my calculation]** 0.478 ± 0.105), and it is a ratio of
  *pollution fractions*, not of *companion fractions* like our 0.54. Recomputed in our metric from their
  Table 1 counts it is ≈ 0.44 (**[my calculation]**). "ApJ in press" is also not found in the PDF.
  Suggested wording: "Xu et al. (2026; DESI DR1, cool He-atmosphere WDs) find 9.8 ± 2.1 % of WDs in wide
  binaries are polluted vs 20.5 ± 0.9 % of single WDs (4.7σ); the ratio is 0.48 ± 0.10 (our
  calculation)."

### Q2. Is our sample "differently selected"?

Yes for the pollution flags and the volume, partly no for the binary catalogue.
- Neither Noor nor Xu uses Vincent+2024 Gaia XP classes (Vincent is not in either reference list,
  p8 and p12-13), and neither uses a 100 pc volume limit (Noor: no limit, out to ~0.5 kpc, p4-5;
  Xu: none stated, WDs to G ≈ 20). Pollution comes from HST UV and SDSS spectra (Noor, p2) and DESI
  spectra (Xu, p3).
- **Shared ingredients:** Xu uses the **same El-Badry+2021 catalogue** (they adopt R < 0.01 as baseline,
  R < 0.1 as a check, p4; we use R < 0.1). Noor's fields are drawn from the same Gentile Fusillo+2021
  WD catalogue (p2). Some of our 203 spectroscopically flagged stars (Coutu+2019 DZ, Hollands+2017 cool
  DZ) may overlap Noor's D07/H18 samples and Xu's DESI DZs within 100 pc **[my inference — not checked]**;
  Xu's Table 2 (p11) gives Gaia IDs of their 21 polluted binary WDs, so the overlap with our 52 can be
  checked directly.
- So: "independent confirmation with a differently selected sample" is fair for the 595 XP-only stars;
  for the other 203 it should say "partly overlapping".

### Q3. Do any of the five already report our three "indications"?

- **Main-sequence vs white-dwarf companions — already reported (replication).** Xu+2026: enrichment
  2/30 = 6.6 ± 4.7 % with WD companions vs 19/185 = 10.3 ± 2.4 % with MS companions, "slightly lower",
  not significant (p5); companion colour does not matter (p6). **[my calculation]** relative to their
  singles that is ≈ 0.32 and ≈ 0.50, the same ordering as our 0.36 (WD) and 0.61 (MS). Our split is a
  replication of a tentative trend, not new.
- **Two separation bins — already reported, and ours disagrees mildly.** Xu+2026: 4/81 = 4.9 ± 2.5 %
  (100-1,000 AU) vs 15/121 = 12.4 ± 3.2 % (1,000-10,000 AU), 1.8σ, "tentative" (p6, Fig. 4 p9).
  **[my calculation]** relative to singles: ≈ 0.24 ± 0.12 and ≈ 0.60 ± 0.16. Our ratios are 0.53 and
  0.59. Our 1,000-10,000 au value replicates theirs; our 100-1,000 au value does **not** show their extra
  suppression (difference ≈ 1.8σ using Poisson errors, **[my calculation]**). Neither is significant. Noor has no bins.
- **DA (hydrogen) polluted stars — reported, with the opposite result for a different kind of DAZ.**
  Noor+2024: hot (14,000-31,000 K), HST-UV-detected DAZ have a field-like companion fraction (p5).
  Xu+2026 excludes H-atmosphere stars and cites Lizana-Vidal+2026 (arXiv:2607.22911) for SDSS
  H-dominated WDs: enrichment < ~1 % in both singles and binaries (p5). So our DA hint is **not** a
  replication; it is either new or in tension, depending on what our 176 "H-atmosphere polluted" stars
  are. **[my inference]** If they are mostly cool DAZ found optically or by XP (strong Ca lines), Noor's
  own two-population hypothesis (strongly polluted → single; UV-only weakly polluted → field-like, p7)
  *predicts* a deficit for them, so our hint would be a test of Noor's hypothesis rather than a
  contradiction. Lizana-Vidal+2026 must be read before saying anything about DA.

### Q4. What remains genuinely new, and the single most useful check

**[my inference throughout]**
- Possibly new: (i) the first use, among these papers, of Gaia XP pollution classes for this test
  (595 of 798 stars); (ii) a 100 pc volume-limited sample with a distance- and G-matched control,
  measured as a companion fraction (the same quantity as Noor) for a mix of H- and He-atmosphere
  polluted WDs; (iii) the 2σ H-atmosphere signal, which no one has published for optically/XP-detected
  cool DAZ (pending Lizana-Vidal+2026 and an ADS search on that exact question).
- Not new: the existence of the deficit (Noor 2024 for DZ, Xu 2026 for cool He-atmosphere WDs), its
  presence for both MS and WD companions (Xu), its presence at 1,000-10,000 au (Xu).
- **Single most decisive check:** recompute the suppression separately for the 595 XP-only stars and
  the 203 spectroscopically flagged stars, and for the XP-only subset also as a function of *angular*
  separation (e.g. companions closer vs farther than ~10 arcsec). If the XP-only subset shows the same
  ≈ 0.5 deficit at large angular separations (where BP/RP blending cannot hide Ca), the XP-based result
  is real and the method is new; if the XP-only deficit is absent, or appears only at small angular
  separation, the XP part of the result dies and what remains is a replication of Noor/Xu with the
  spectroscopic stars. A cheap companion check: cross-match our 52 polluted+companion stars with Xu's
  Table 2 and Noor's D07/H18 lists to count truly independent systems.

### Q5. Testable predictions in Norambuena I/II

- **Norambuena I** makes a **qualitative** prediction only: the incidence of late (cool-WD) accretion
  **increases with binary separation** over initial a_B = 250 → 500 → 1,000 au (p7, p9, Figs. 4, 6, 7;
  conclusion 1, p14), and is strongly suppressed for e_B = 0.9 at any separation (p9). Orbits widen by
  ≈ 2-3 during mass loss (p6), so **[my inference]** this maps to present-day separations of roughly
  500-3,000 au. They explicitly decline to predict pollution frequencies (p14) and have not compared
  binaries with single stars (p14), so there is no predicted suppression factor. Our data can test the
  *sign* of the trend within binaries: our ratios 0.53 (100-1,000 au) and 0.59 (1,000-10,000 au) are flat
  within errors; finer bins across 250-3,000 au would be the direct test, but with 52 systems the
  power is low **[my inference]**. Galactic tides (> 1,000 au) are not modelled (p4, p14).
- **Norambuena II** varies the **planet** mass (10 M⊕ vs 1 M_Jup), not the companion mass, at a single
  separation (250 au) (p2-3). No companion-mass prediction exists in either paper (companion fixed at
  1 M☉, paper I p4 and p16; paper II p2). Planet mass is not observable in our data, so nothing to test.
  Their low-inclination / low-eccentricity preference (II, p1) is not testable with projected
  separations alone.

### Q6. Gentile Fusillo et al. 2026 and our IR-excess candidates

WD J1328−1450 is a ~73 Myr-old, 17,400 K helium-atmosphere white dwarf at ≃ 500 pc whose infrared excess
(VHS + WISE) led to X-shooter spectra showing metal absorption and, uniquely, quadruple-peaked Ca II and
O I emission from two gas rings (0.14-0.34 and 0.54-1.93 R☉), with Mg missing in the outer ring; the
authors attribute each ring to a surviving planetesimal and quote a fractional IR luminosity of 2.7 %
(p2, p5, p7, p13). Its parallax (2.014 mas, p36) is far below our 10 mas cut, so it cannot be one of our
100 pc candidates (fact). Its relevance is methodological **[my inference]**: (1) it is a published
example of the exact route our candidates would need — photometric IR excess from VHS/WISE, then
spectroscopy for metals and gas — so an IR excess alone is a candidate, not a disc; (2) the authors show
SED fits are degenerate (a flat-disc fit gives a face-on disc that contradicts the gas lines, p18;
MCFOST solution "not unique", p20), so we should not over-interpret disc parameters fitted to our
WISE/VHS points; (3) τ = 2.7 % is quoted as among the largest known (p7, p20), a useful benchmark: a
candidate of ours with a much larger fractional excess deserves extra suspicion of contamination or an
unresolved companion before being called a disc; (4) they explicitly rule out an unresolved double WD
using Gaia's ~0.3" resolution (p32) — the same blending argument applies, more favourably, at < 100 pc.
It says nothing about our wide-binary result.

---

## Action items for the report

1. Rewrite the two "published" sentences as in Q1; add Noor's DAZ result and Xu's separation and
   WD/MS results to the Summary and Limitations.
2. Change the MS/WD and separation statements from "indication" to "consistent with Xu+2026" (and note the
   mild disagreement at 100-1,000 au).
3. Read Lizana-Vidal+2026 (arXiv:2607.22911) before keeping any H-atmosphere claim.
4. Run the XP-only vs spectroscopic split with angular-separation bins (Q4).
5. Update references: Noor MNRAS 529, 2910; Xu "arXiv preprint (draft 11 Sep 2026)".
