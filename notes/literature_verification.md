# Verification of research/literature.md against the primary papers

Date: 2026-10-05. Author: Kister Space (Christian Jair).

Method: every arXiv identifier in literature.md was resolved through the arXiv API
(`export.arxiv.org/api/query?id_list=...`, 34 ids, all resolved to the expected
paper; list at the end). The three papers that steer our strategy (Cavalier+ 2026,
Robert+ 2024, Murillo-Ojeda+ 2026) were read in full text (PDF/HTML), the rest
from abstracts. Verdicts: VERIFIED / CORRECTED / COULD NOT VERIFY.

Our survey for reference: Gaia EDR3 100 pc WDs (Gentile Fusillo+ 2021), G < 17,
3,339 stars, SPOC 2-min PDCSAP, up to 6 sectors stacked, BLS with box durations
4-30 min and periods 0.15-13 d (`wdplanets/transits.py`, `load_sectors(exptime=120)`).

---

## 1. Cavalier+ 2026 - broad TESS 2-min search of Gaia WDs

Read: https://arxiv.org/abs/2606.03850 and the full PDF (https://arxiv.org/pdf/2606.03850).
Title: "A Previously Underexplored Regime in TESS: Minute-Scale Eclipses Reveal Ten
White Dwarf-Cool M-Dwarf Binaries". Cavalier, de Wit, Timmermans, Rackham, ... (SPECULOOS
team). Submitted 2 June 2026. **Identifier VERIFIED.**

What the paper actually says (Section 2):

- Parent sample: Gaia EDR3 WD-candidate catalogue (Gentile Fusillo+ 2021) with an
  "intentionally inclusive threshold of P_WD > 0.10", ~9 x 10^5 objects. **No magnitude
  or distance cut is stated.** The search sample is the cross-match with the TESS
  short-cadence target lists (Stassun+ 2019): "~3.7 x 10^4 potential WDs monitored at
  2-min cadence". So the magnitude limit is implicitly whatever got 2-min targets
  (GI programs; in practice mostly G < 17-18).
- Cadence: **2-min SPOC PDCSAP only.** 20-s data and FFIs are not used. They write
  "The TESS extended mission, including 20-second cadence observations, will further
  improve sensitivity to ultra-short-duration eclipses" (future work).
- Sectors: **not stated as a range.** Light curves are "all available TESS sectors"
  per target; the pixel-level vetting example uses Sector 99 (approx. Nov 2025), so
  the data extend at least to Sector 99. Follow-up epochs (T0 in Table 2) run
  BTJD 3970-4160, i.e. Oct 2025 - Apr 2026. Sectors from ~100 onward (2026) are
  probably not included, but this is my inference, not a statement in the paper.
- Method: BLS on PDCSAP, "optimized for short and frequent eclipses, with periods
  spanning 0.1 hr to a few days". **No duration grid, no SDE/SNR threshold, no
  injection-recovery and no completeness or occurrence-rate limits are published.**
- Funnel: ~6,000 candidate signals -> ~180 "high-SNR" candidates after automated and
  visual vetting -> literature search removes known systems -> 40 new candidates ->
  TPF pixel-level vetting rejects ~19 (4 background EBs, 15 weak/spatially
  inconsistent) -> 21 ambiguous go to SPECULOOS -> 11 on-target (10 WD+M dwarf
  eclipsing binaries, Table 2, plus the WD+BD WD J0404+1112, de Wit+ 2025) and 10
  background EBs. So all 40 new candidates are accounted for; **no planet or debris
  candidate is reported and the words "debris" or "planet candidate" appear only
  for the WD 1856+534 b recovery.** The candidate list (~180 or ~6,000) is not
  published.
- Validation: "the pipeline recovers known WD companions such as the WD planet
  candidate WD 1856+534 b (Vanderburg et al. 2020) and the WD brown dwarf
  WD 0038+2030 B". **VERIFIED.**
- Ten new WD+M: periods 0.094-0.291 d (2.25-7.0 h), companion T_eff 2700-3400 K;
  three (TIC 600854869, 2041210548, 1883504789) were already WDMS candidates in
  Kosakowski+ 2022 (ZTF).
- Future: extend to the full 1.3 M catalogue; "ongoing analyses of the full TESS
  dataset".

Does it cover our sample? **Yes at 2-min cadence.** Every 100 pc, G < 17 WD with
P_WD > 0.1 that has SPOC 2-min light curves is inside their ~37,000, and their
period range (0.1 h to "a few days") overlaps ours (3.6 h-13 d) except at the
long end. What they did NOT do: 20-s cadence, FFIs, sectors after ~99, periods
beyond a few days, a single-event search, any published completeness, any target
prioritisation by pollution or IR excess, and they did not release candidates.

Verdict on literature.md line: **CORRECTED** (details added; the "no planets or
debris" phrasing is right but it was never a stated null result with sensitivity -
the paper simply reports no such candidates).

## 2. Robert+ 2024 - 313 polluted WDs in TESS

Read: https://arxiv.org/abs/2407.21743 and https://arxiv.org/html/2407.21743.
MNRAS 533, 1756 (2024). **Identifier VERIFIED.**

- Sample: literature metal-polluted WDs cross-matched with TIC v8.2; 313 with TESS
  light curves, "around 20 per cent of all known polluted white dwarfs". **VERIFIED.**
- Cadence: 214 with 20-s light curves, the remaining 99 at 120 s only. Mean baselines
  2.34 sectors (120 s) and 1.72 sectors (20 s). **VERIFIED.**
- Sectors: "All available light curves from Sectors 1-65". **VERIFIED.**
- Search: BLS + Lomb-Scargle; periods 1 h to 27 d, grid step 60 s, for both cadences;
  threshold = 99.9th percentile of bootstrap-randomised power; median SDE 10.8 +/- 2.9.
  Transit candidates required >= 4 (120 s) or >= 12 (20 s) consecutive in-event points.
- Injection-recovery: 8 log-spaced radii 0.0625-8.00 R_earth (literature.md said
  "0.06-8", fine), 37,800 injections per 120-s light curve set, 20,400 for the 20-s
  subset. The 20-s data have higher sensitivity than 120 s.
- Results: ZTF J0328-1219 and WD 1054-226 recovered blindly; WD 1145+017 NOT recovered
  (its transits were much shallower and rarer in 2022-2023); no new detections;
  transit fraction 0.8 (+0.6/-0.4) %; single transits also excluded in all data.
  **VERIFIED.**
- Ground-based part: 33 polluted WDs with ULTRACAM (19) / ULTRASPEC (14), periods
  15 min-7 h, median 4.1 h per light curve; only weak limits beyond ~2 h.
- Not covered: non-polluted WDs, IR-excess-selected WDs, FFIs, sectors > 65, periods
  < 1 h in TESS. The literature.md claim "G fainter than ~18" is not in the paper;
  the magnitude distribution is set by which polluted WDs got 2-min/20-s targets.
  **CORRECTED** (removed the magnitude claim).

## 3. Are TESS 20-s WD data unsearched for transits?

Searched (web + arXiv) for any blind BLS transit search on 20-s WD light curves.
Found:

- Robert+ 2024: 214 polluted WDs at 20 s, Sectors 1-65 - the only blind BLS search
  on 20-s WD data I can find.
- Romero+ 2024 (arXiv:2407.07260, "Thirty Two New Bright ZZ Ceti Stars from TESS:
  Adding Cycles 4 and 5", submitted 9 Jul 2024; literature.md said 2025 - **CORRECTED**
  to 2024): 120 s and 20 s data to Sector 69, G < 17.5, Fourier-transform pulsation
  search. **Pulsations only; no transit/BLS search.** https://arxiv.org/abs/2407.07260
- Oliveira da Rosa+ 2024 (arXiv:2407.05214, ApJ 974, 314): 9,285 WDs to Sector 69,
  Fourier transforms + TESS_localize, 318 periodic (rotation). Not a box search.
  https://arxiv.org/abs/2407.05214 **VERIFIED.**
- Aungwerojwit+ 2024 (arXiv:2404.04422) and Hermes+ 2025 (arXiv:2501.02050) use 20-s
  TESS data on *known* debris-transit WDs (DFT), not blind searches.
- Cavalier+ 2026: 2-min only; lists 20 s as future work.

Conclusion: **VERIFIED** - apart from the 214 polluted WDs through Sector 65, no
published blind transit search of TESS 20-s WD light curves exists, and nothing
covers 20-s data after Sector 65 (Cycles 6-8, mid-2023 onward) for any WD class.
Caveat: Cavalier+ say "ongoing analyses of the full TESS dataset", so this niche
may close within a year.

## 4. IR-excess samples vs TESS/ZTF transit searches

- Xu+ 2020, arXiv:2009.00193 (ApJ 902, 127): "2847 bright Gaia white dwarf
  candidates (G < 17.0 mag)" cross-matched with unWISE, 188 IR-excess candidates
  (147 new). Read from the PDF. **VERIFIED.**
- Lai+ 2021, arXiv:2107.01221 (ApJ 920, 156): Spitzer (174 WDs) + Gemini (235)
  follow-up, 62 confirmed excesses, 52 likely dust disks. **VERIFIED.**
- Madurga Favieres+ 2024, A&A 688, A168 (DOI 10.1051/0004-6361/202347368): 41,020
  Gaia EDR3 WD candidates with G < 18.5 x CatWISE, 554 candidates, 446 new; VizieR
  J/A+A/688/A168. **VERIFIED** (A&A page + VizieR listing; no arXiv id was given).
- Murillo-Ojeda+ 2026, arXiv:2602.10070 = A&A 707, A268 (2026): 8,150
  spectroscopically classified WDs within 100 pc (Gaia DR3, Jimenez-Esteban+ 2023)
  with Gaia XP synthetic photometry + IR; 456 IR-excess WDs (292 robust, 164
  candidates), ~75 % new; catalogue at CDS and the SVO WD archive. **The paper does
  not mention TESS, ZTF, light curves or variability of its sample at all.**
  Paper II (parameters, disk vs companion) is announced. **VERIFIED.**
- Search for "IR-excess WD catalogue + TESS transit search": nothing found. The
  closest are Robert+ 2024 (polluted WDs, which overlap but are a different
  selection) and the ZTF variability searches (Guidry+ 2021, Bhattacharjee+ 2025,
  van Roestel+ 2026) which select on variability, not on IR excess. Note from
  Bhattacharjee+ 2025: known transiting-debris WDs "generally do not have infrared
  excesses", i.e. an IR-excess sample is not guaranteed to be transit-rich; it is
  still the natural place to look for recurring Roche-limit debris.

Conclusion: gap 1 of literature.md ("photometry of the IR-excess candidates has
not been done") stands. **VERIFIED as far as the literature shows**; tag changed from
UNCONFIRMED to "no such search found (2026-10-05)".

## 5. Other identifiers / claims

All 34 arXiv ids resolve (arXiv API, 2026-10-05). Specific fixes:

- WD 0806-661 b: primary paper is Luhman, Burgasser & Bochanski 2011, ApJ 730, L9,
  arXiv:1102.5411 ("Discovery of a Candidate for the Coolest Known Brown Dwarf").
  **CORRECTED** (id added).
- WD 1202-232 / WD 2105-82: primary is Mullally S.+ 2024, ApJL 962, L32,
  arXiv:2401.13153 (arXiv:2505.20520 is the Espinoza+ 2025 JWST highlights review).
  Follow-up: Mullally F.+ 2025, arXiv:2512.08191 (accepted AAS Journals): second
  MIRI epoch shows **both resolved sources have no proper motion and are likely
  background galaxies**; WD 2105-82 keeps an unresolved IR excess that shares the
  star's proper motion, consistent with a ~1.4 MJup companion at < 4 au. The
  Wikipedia-based statement was essentially right. **CORRECTED** with primary source.
- WD 1856+534 b ephemeris: Gendreau-Distler+ 2026 (AJ 172, 141, arXiv:2511.21611)
  constant-period fit: T0 = 2458779.375083 +/- 0.000001 BJD_TDB,
  P = 1.407939211 +/- 0.000000005 d, 1,498 epochs, Pdot = 0.04 +/- 0.43 ms/yr.
  literature.md had P = 1.40793923, T0 = 2458779.375079 (differences 2e-8 d and
  0.3 s; harmless, but now sourced). **CORRECTED.**
- van Roestel+ 2026 (arXiv:2609.08923): ZTF negative alerts, 8-yr ZTF baseline, six
  single deep events (25-100 %), 20 confirmed debris-transit WDs, ZTF J0436+5728
  with 5.910 h. Number of WDs searched not in abstract. **VERIFIED** (data span).
- Gaia DR4: ESA release page states "Gaia DR4 (based on 66 months of data)
  2 December 2026" (https://www.cosmos.esa.int/web/gaia/release). **VERIFIED.**
- Romero+ year: 2024, not 2025 (arXiv July 2024). **CORRECTED.**
- Murillo-Ojeda+ 2026 journal ref added (A&A 707, A268).
- Not checked (low value): Aloisi 2021 Zenodo poster, CHEOPS A&A 651 L12, AAS Nova
  JWST piece, JWST program numbers 3964/4403/9067. Left as is.

---

## What our survey can add that those did not cover

Plain statement first: **at 2-min cadence, with data through ~Sector 99, Cavalier+
2026 has already run a BLS over a superset of our 3,339 targets, covering periods
from 0.1 h to a few days, and recovered WD 1856 b.** Any strong, periodic,
few-minute dip in that data has very likely been seen by them and vetted as a
binary or rejected. Our current 2-min run will mostly re-find their eclipsing
binaries (good as validation, not as discovery). Two things soften this: they
publish no completeness or candidate list, and their vetting was tuned to
eclipsing binaries, so weaker or irregular signals were not necessarily followed
up. Robert+ 2024 covers only polluted WDs and only to Sector 65.

Niches that remain, ranked by feasibility for a lightkurve-based hobby pipeline
(1 = easiest):

1. **20-s cadence, all sectors, our whole sample.** Unsearched for non-polluted WDs,
   and unsearched for everyone after Sector 65. An Earth-size body transits a WD in
   ~2-4 min: one or two points at 2 min, 6-12 points at 20 s. Implementation is
   one argument (`exptime=20`) plus durations down to ~1 min and periods down to
   ~0.1 h; validate on WD 1856 b and ZTF J0328-1219. Risk: Cavalier+ announce 20 s
   as their next step.
2. **Newest sectors (>= ~100, 2026 onward) at 2 min and 20 s.** Nobody has searched
   them; each new sector adds targets (Cycle 8 GI lists) and new epochs for old
   targets. Cheap to run as a "fresh sectors first" ordering in the survey loop.
   This niche renews itself every ~27 days.
3. **IR-excess-selected targets** (Xu+ 2020: 188; Madurga Favieres+ 2024: 554;
   Murillo-Ojeda+ 2026: 456 within 100 pc, so largely inside our sample). No TESS
   or ZTF transit search of these lists exists. Run them first, with the period
   grid extended to 27 d, 20-s data where available, and a single-event scan.
   Expected yield is low (transiting-debris WDs are usually not IR-bright), but a
   positive would be publishable, and a null is a clean, reportable limit.
4. **Longer periods (3-13 d, and up to ~27 d) and single-event dips** for the
   non-polluted sample. Cavalier+ stopped at "a few days"; Robert+ went to 27 d but
   only for polluted WDs; van Roestel+ 2026 show one-off deep events are a real
   population. A single-transit / dip finder on stacked 2-min + 20-s data is simple
   to add to the pipeline (depth > 10 %, duration 10 min-days).
5. **Re-monitoring known systems** (WD 1054-226, ZTF J0328-1219, SBSS 1232+563,
   ZTF J1944+4557, WD 1145+017) in every new sector: low novelty, but Korth+ 2026
   got a paper out of it, and activity changes are frequent.
6. **FFIs (200 s since Cycle 5) for 100 pc WDs without 2-min/20-s data** (G 17-18.5,
   and the ~20 % of our list flagged `no_data`). Only a 2021 poster and a 30-min
   Lomb-Scargle study exist. Hard: 21" pixels, dilution, scattered light; needs
   TESScut + custom apertures. Highest novelty of the TESS options, lowest
   feasibility.
7. **ZTF DR > 10 periodic box search** of IR-excess / 100 pc WDs: feasible via IRSA,
   but the ZTF team is active here (van Roestel+ 2026); treat as opportunistic.
8. **Gaia DR4 (2 Dec 2026)**: prepare an epoch-photometry dip/periodogram script now;
   professional teams will be fast, but the 100 pc WD subset is small enough to
   process on day one.

Recommended immediate change to the pipeline: make 20-s the preferred cadence
(fall back to 2 min), order targets by (IR-excess or polluted) first and then by
newest sector, extend durations to 1-30 min and periods to 0.1 h-27 d, and add a
single-event scan. Keep the 2-min run as the validation layer, not the discovery
layer.

---

### arXiv ids resolved on 2026-10-05 (first author, title truncated)

2606.03850 Cavalier - Minute-Scale Eclipses ... Ten WD-Cool M-Dwarf Binaries;
2407.21743 Robert - frequency of transiting planetary systems around polluted WDs;
2407.07260 Romero - Thirty Two New Bright ZZ Ceti Stars (2024);
2407.05214 Oliveira da Rosa - Photometric WD Rotation (ApJ 974, 314);
2602.10070 Murillo-Ojeda - Gaia WDs with IR excess I (A&A 707, A268);
2009.00193 Xu - IR Excesses around Bright WDs I; 2107.01221 Lai - ... II;
2505.20520 Espinoza - JWST exoplanet highlights (review); 2401.13153 Mullally - JWST
images giant planet candidates; 2512.08191 Mullally - follow-up with MIRI;
2408.16813 Limbach - MEOW; 2601.18965 Poulsen - MEAD II; 2410.03288 Iskandarli - Helix;
2310.05778 Rogers - WD0141-675; 1804.01997 Vanderburg - WD 1145+017 review;
1908.09839 Vanderbosch - ZTF J0139+5245; 2106.02659 Vanderbosch - ZTF J0328-1219;
2109.06183 Farihi - WD 1054-226; 2603.07677 Korth - WD 1054-226 revisited;
2012.00035 Guidry - I Spy Transits and Pulsations; 2404.04422 Aungwerojwit;
2501.02050 Hermes - SBSS 1232+563; 2502.05502 Bhattacharjee - ZTF six candidates;
2508.18348 Guidry - 4.97 h debris; 2609.08923 van Roestel - deep obscuration events;
2202.03895 Priyatikanto - WD variables in TESS; 1711.09691 van Sluijs - K2;
1902.04075 Dame - DECam; 2404.02201 Steen - Gaia DR3 variability (ApJ 967, 166);
2206.02505 Sanderson - Can Gaia find planets around WDs; 2303.06157 Kubiak - TTV;
2511.21611 Gendreau-Distler - transit timing (AJ 172, 141); 2106.07669 Gentile
Fusillo - Gaia EDR3 WD catalogue; 1911.07889 Bell - ZTF forecast; 1102.5411 Luhman -
WD 0806-661 B.
