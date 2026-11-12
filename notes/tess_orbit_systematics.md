# Period clustering of survey signals at the TESS orbital period (2026-10-25)

Source: `research/targets.csv` (35 rows with status known / false_positive / candidate, search v2, 20-s cadence where available).

Periods of the 35 periodic signals split into three groups:

| Group | Periods | Count | Status in targets.csv |
| --- | --- | --- | --- |
| Short | 0.151 to 1.17 d (3.6 h to 28 h) | 24 | 19 known (SIMBAD/VSX eclipsing or variable), 5 false_positive, 1 candidate (0.1745 d) |
| Mid | 6.98 d (twice, two different stars), 7.27 d | 3 | 2 candidate, 1 known |
| Long | 10.96 d (twice, identical to 4 decimals in two stars), 11.9 to 13.0 d (six) | 8 | 7 false_positive, 1 known |

TESS orbits the Earth every 13.7 days; each sector is two orbits with a data gap at perigee, and scattered light / momentum dumps repeat with that cadence. A box search over several sectors therefore finds spurious periods near 13.7 d and its half, 6.85 d. The two 6.98-d candidates (WDJ204906.70+372814.05 and WDJ194213.00+373156.60, both with 1-min "transits" of 6.6 % and 33 %) and the two 10.96-d false positives (WDJ085047.51+172602.06, WDJ084253.03+230025.47) sit on this pattern: the same period in two unrelated stars is the instrument, not the sky.

Example: PG 1601+581 = WDJ160241.98+575815.32, P = 12.946 d. Odd-transit depth 1.3 %, even 0.05 % (2-min SPOC, sectors 15, 16, 22, 23, 24, 25). Of five predicted events with data, only the sector-25 event shows a dip (14.1 %); the others are 0.2 %, 1.1 %, -0.05 %, -0.05 %.

Action for the pipeline (backlog): add a period veto window around 13.7/n days (n = 1, 2) and around twice the sector length, and require detection in at least two sectors before a signal becomes `candidate`. Both 6.98-d candidates should be re-vetted with that rule; they are the only open items besides WDJ131257.90+580511.29 (0.1745 d, 4-min duration, 670 events, which is probably a short-period binary and needs SIMBAD/ZTF).
