# Planets around white dwarfs: search status report, October 2026

As of 2026-10-21.

## Summary

No planet or debris transit has been found yet. The main result of October 2026 is a change of direction: the 2-minute TESS search we started had already been done by a professional team, and the open ground is the 20-second cadence data and the sectors observed in 2026, which no published search we found covers.

- The sample is 16,676 white dwarfs within 100 pc from Gaia EDR3, of which 3,339 are bright enough for TESS (G < 17).
- The pipeline recovers the only known transiting planet around a white dwarf, WD 1856+534 b, blind: period 1.407939 d, SDE 51 with six sectors at 20 s. It also recovers the 9.94 h debris transits of ZTF J0328-1219.
- 396 white dwarfs were searched at 2-min cadence. The 24 periodic signals found were all vetted: 17 are catalogued variables, 7 are instrument artefacts, 0 are transits.
- A census of TESS 20-s data shows 2,847 of the 3,339 targets (85 %) have 20-s light curves; 313 of them were observed in sectors 100 or later, which no published search covers.
- The 20-s search (version 2) started on 6 October, processed 10 stars and stopped when the host computer was off; it was restarted on 21 October.

## Sample and data

The sample is every high-confidence white dwarf within 100 pc in the Gaia EDR3 catalogue of Gentile Fusillo et al. 2021 (VizieR J/MNRAS/508/3877): parallax above 10 mas and white-dwarf probability above 0.75, which gives 16,676 stars. The nearest is Sirius B at 2.67 pc; the median temperature is 6,200 K.

| Cut | Stars | Note |
| --- | --- | --- |
| Within 100 pc, P_WD > 0.75 | 16,676 | Gaia EDR3 |
| G < 17 (search sample) | 3,339 | TESS noise swamps deeper transits beyond this |
| With any TESS 20-s light curve | 2,847 | 85 % of the search sample |
| With 20-s data in sectors 100 or later | 313 | not covered by the published searches we checked |
| First 20-s light curve after sector 65 | 898 | after the last published 20-s search |

Light curves are the SPOC products at MAST: 2-minute cadence (sectors 1 onward) and 20-second cadence (sectors 27 onward). Version 2 of the search takes the 20-s curve of a sector when it exists and the 2-min curve otherwise, newest sectors first, up to six sectors per star. The 20-s data are binned to 40 s, which still leaves three points inside a 2-minute transit.

Why cadence matters: a white dwarf is about the size of the Earth, so an Earth-sized planet crossing it blocks most of the light, but only for 2 to 8 minutes. At 2-min cadence that is one to four points; at 20 s it is 6 to 24 points.

## Method

The search is a box least squares (BLS) fit: for every trial period, the box-shaped dip that best explains the light curve. Because TESS sectors can be years apart, each sector is searched on one shared period grid and the log-likelihoods are added, then the best period is refined on all sectors together. The grid is uniform in log period, 176,000 trial periods from 0.15 to 13 days, with box durations of 1, 2, 4, 8, 16 and 30 minutes. Six sectors are searched in parallel processes; one star takes 130 to 220 s.

Every signal is vetted automatically (wdplanets/vetting.py): the longest transit physically possible at that period for an Earth-sized star; a sinusoid fit at P and P/2; odd versus even transit depths; signal present in each sector separately; the fraction of events next to data gaps; the share of pixel light from neighbours within the 21-arcsecond TESS pixel (CROWDSAP and Gaia DR3); SIMBAD and VSX lookups.

| Validation target | What it tests | Result |
| --- | --- | --- |
| WD 1856+534 b | blind recovery of an 8-min, 56 % transit every 1.408 d | recovered: P = 1.407939 d, SDE 51 (20 s, 6 sectors); SDE 53 (2 min) |
| ZTF J0328-1219 | hours-long, few-percent debris transits at 9.937 h | recovered: 9.942 h, depth 5.6 %, SDE 25 (one 2-min sector) |

The measured depth of WD 1856+534 b is not reliable (91 to 101 % in PDCSAP against 56 % published) because two neighbouring stars share the pixel and the crowding correction overshoots; on the raw SAP flux the dip is 4.8 % of the pixel light. Depths from TESS are treated as indicative only.

## Result 1: a census of TESS 20-second data for the 100 pc white dwarfs

2,847 of the 3,339 white dwarfs with G < 17 within 100 pc (85 %) have at least one TESS 20-second light curve, and 313 of them were observed in sectors 100 or later. We did not find a published list of which nearby white dwarfs have 20-s data (literature check of 6 October 2026).

Method: every SPOC 20-s observation in sectors 27 to 107 (156,696 observations) was pulled from MAST and matched to the sample by position, allowing for 16 years of proper motion. Median separation 1.7 arcseconds. A per-target check on 337 stars with lightkurve agrees for 97 % of them; the disagreements are bright binaries where the 20-s target is the companion.

| G | White dwarfs | With 20-s data | In sectors >= 100 | First 20-s curve after sector 65 |
| --- | --- | --- | --- | --- |
| < 13 | 38 | 37 (97 %) | 7 | 32 |
| 13-14 | 102 | 97 (95 %) | 16 | 89 |
| 14-15 | 336 | 318 (95 %) | 48 | 283 |
| 15-16 | 992 | 878 (89 %) | 100 | 724 |
| 16-17 | 1,871 | 1,517 (81 %) | 142 | 1,267 |
| All | 3,339 | 2,847 (85 %) | 313 | 2,395 |

The median star has two 20-s sectors; the most observed has 31. The latest public sector is 107 (released 1 October 2026); sector 108 should appear in early November. Each new sector adds roughly 40 to 170 white dwarfs with fresh 20-s data. Full table: [data/tess_20s_coverage.csv](../data/tess_20s_coverage.csv).

## Result 2: 24 periodic signals, zero transits

The 2-minute search of the 396 brightest targets (2 to 6 October) produced 24 signals above the thresholds (SDE >= 10, depth S/N >= 8, at least three events). All 24 were vetted; none is a transit.

| Verdict | Count | What they are |
| --- | --- | --- |
| Known variable | 17 | reflection-effect and eclipsing WD + M dwarf binaries (V0727 Car, WG 21, ...), pulsators (GD 358, G 29-38, EC 01585-1600, Feige 7, CL Oct), rotating magnetic white dwarfs (WD 2359-434, WD 2138-332, GD 323), a delta Scuti star next to GD 215 |
| Instrument artefact | 7 | four single-sector dips that are PDC ramps after scattered-light gaps on crowded pixels (CROWDSAP 0.04-0.24), two crowding-amplified sinusoids, one negative-flux artefact |
| Transit | 0 | |

Lessons built into the pipeline: a transit of a white dwarf lasts minutes, never half an hour; on pixels where less than 20 % of the light belongs to the target, the TESS systematics correction can turn an instrumental jump into a 50 % dip.

Side note: WG 26 (WDJ141039.06-474439.48, G = 14.35, 19,400 K, 56 pc) shows a 4.73-hour sinusoid with 29 % semi-amplitude in sectors 65, 101 and 102, absent from VSX. Not a transit; 77 % of the pixel light comes from neighbours. Either a reflection effect in an uncatalogued WD + M dwarf binary or a neighbour's variability. Candidate for a short note after a pixel-level check.

## Context: what has been searched before

| Search | Sample | Cadence and sectors | Outcome | Not covered |
| --- | --- | --- | --- | --- |
| Cavalier et al. 2026 (arXiv:2606.03850) | ~37,000 Gaia WDs with 2-min TESS targets | 2 min, sectors to at least 99 | 10 new eclipsing WD + M dwarf binaries; WD 1856+534 b recovered; no planet or debris candidate | 20-s data, FFIs, sectors after ~99, periods beyond a few days, single events; no completeness or candidate list |
| Robert et al. 2024 (arXiv:2407.21743) | 313 metal-polluted WDs | 20 s (214 stars) and 2 min, sectors 1-65 | ZTF J0328-1219 and WD 1054-226 recovered; no new detections; transit fraction 0.8 % | non-polluted WDs, sectors after 65 |
| van Roestel et al. 2026 (arXiv:2609.08923) | ZTF alerts, 8-year baseline | ground-based, nightly | six single deep obscuration events; 20 debris-transit WDs known | minute-scale events |
| IR-excess catalogues: Xu et al. 2020 (188), Madurga Favieres et al. 2024 (554), Murillo-Ojeda et al. 2026 (456 within 100 pc) | WDs with warm dust or companions | none | target lists | no TESS or ZTF transit search of these lists exists |

Our 100 pc, G < 17 sample sits inside the Cavalier et al. parent sample, so at 2 minutes our survey repeats their work. Gaia DR4 (2 December 2026) will reopen the whole question.

## Next steps and limitations

1. Reorder the survey by niche: first the 313 stars with 20-s data in sectors >= 100, then the 898 whose first 20-s curve came after sector 65.
2. Re-measure dips deeper than 100 % on the raw SAP flux; add WD 1054-226 as a second debris validation target.
3. Search the infrared-excess white dwarfs first, period grid to 27 days.
4. Single-event dip finder (depth > 10 %, 10 minutes to 1 day).
5. Injection and recovery test at G = 13, 15, 16, 17. Without it a null result has no sensitivity and cannot be published.
6. Pixel-level check of WG 26.
7. Gaia DR4 epoch-photometry script before 2 December 2026.

Limitations: no completeness yet (thresholds set by hand); at most six sectors per star; 21-arcsecond pixels make depths indicative; version 2 has processed 10 of 3,339 stars, so Result 2 is a 2-minute result only; the 20-s niche may close, since Cavalier et al. name it as their next step.

## References

- Cavalier et al. 2026, arXiv:2606.03850
- Gendreau-Distler et al. 2026, AJ 172, 141, arXiv:2511.21611
- Gentile Fusillo et al. 2021, MNRAS 508, 3877, arXiv:2106.07669
- Murillo-Ojeda et al. 2026, A&A 707, A268, arXiv:2602.10070
- Robert et al. 2024, MNRAS 533, 1756, arXiv:2407.21743
- Vanderbosch et al. 2021, arXiv:2106.02659
- Vanderburg et al. 2020, Nature 585, 363
- van Roestel et al. 2026, arXiv:2609.08923
- Xu et al. 2020, ApJ 902, 127, arXiv:2009.00193
- Project files: research/notes/literature_verification.md, research/notes/tess_20s_availability.md, research/notes/tess_20s_coverage.csv, research/notes/WDJ*.md, research/targets.csv
