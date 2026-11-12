# TESS 20-second data for the 100 pc white dwarf sample: availability census

Date: 2026-10-06. Author: Kister Space (Christian Jair). Follows `literature_verification.md`
(2026-10-05), which identified 20-s cadence and sectors >= 100 as the open niche.

Companion file: `research/notes/tess_20s_coverage.csv` (one row per WD of the
3,339-star sample: `n_20s`, `sectors_20s`, `tic_20s`, `n_20s_S100plus`,
`n_120s_S97plus`, `sectors_120s_S97plus`). Built from the MAST cross-match
described in section 2; it can drive the target ordering of the 20-s pipeline
without any further MAST metadata queries.

---

## 1. Latest public sector, and the Cycle 8 calendar

**Latest sector with public SPOC 2-min and 20-s light curves at MAST: Sector 107**
(observed 9 Aug - 7 Sep 2026; MAST `t_obs_release` = 2026-10-01). Sector 108
(7 Sep - 5 Oct 2026) has no SPOC timeseries products yet (query count 0 on
2026-10-06). Sector 107 holds 2,160 20-s and 13,000 2-min SPOC light curves.

Sources: MAST CAOM via `astroquery.mast.Observations.query_criteria(obs_collection="TESS",
dataproduct_type="timeseries", provenance_name="SPOC", sequence_number=S, t_exptime=[19,21] / [119,121])`;
sector dates from the per-sector pages at https://tess.mit.edu/observations/sector-NNN/ ;
MAST data release notes index https://archive.stsci.edu/tess/tess_drn.html (lists
DRN 142 = Sector 104 as of its last modification, 2026-09-04; the HEASARC condensed
DRN page lists up to Sector 101). The release notes lag the data: light curves
for 105-107 are at MAST although their DRNs are not yet indexed.

| Sector | Observed (tess.mit.edu) | Orbits | Released at MAST (t_obs_release) | 20-s LCs | 2-min LCs |
|---|---|---|---|---|---|
| 96 | 20 Aug - 14 Sep 2025 | 199-200 | 2025-10-03 | 3,000 | - |
| 97 | 15 Sep - 9 Nov 2025 (4 orbits) | 201-204 | 2025-12-08 | 2,261 | 13,000 |
| 98 | 9 Nov 2025 - 5 Jan 2026 (4 orbits) | 205-208 | 2026-02-06 | 2,438 | 13,000 |
| 99 | 5 Jan - 2 Feb 2026 | 209-210 | 2026-02-26 | 2,639 | 13,000 |
| 100 | 2 Feb - 2 Mar 2026 | 211-212 | 2026-03-27 | 2,576 | 13,000 |
| 101 | 2 - 27 Mar 2026 | 213-214 | 2026-04-20 | 2,724 | 13,000 |
| 102 | 27 Mar - 21 Apr 2026 | 215-216 | 2026-05-22 | 2,668 | 13,000 |
| 103 | 21 Apr - 17 May 2026 | 217-218 | 2026-06-25 | 2,566 | 13,000 |
| 104 | 17 May - 13 Jun 2026 | 219-220 | 2026-07-13 | 2,474 | 13,000 |
| 105 | 13 Jun - 11 Jul 2026 | 221-222 | 2026-08-17 | 2,256 | 13,000 |
| 106 | 11 Jul - 9 Aug 2026 | 223-224 | 2026-09-10 | 2,121 | 13,000 |
| 107 | 9 Aug - 7 Sep 2026 | 225-226 | **2026-10-01** | 2,160 | 13,000 |
| 108 | 7 Sep - 5 Oct 2026 | 227-228 | not yet | 0 | 0 |
| 109 | 5 - 31 Oct 2026 | 229-230 | in progress | - | - |

**Cycle 8 = Year 8 = Sectors 97-107**, 15 Sep 2025 - 7 Sep 2026 (tess.mit.edu
"Year 8 (S97-107)"; GI program pages G08082/G08108 list targets over "Sectors
97-107"). Sectors 97 and 98 are the two four-orbit (~55 d) sectors. Cycle 9 =
Year 9 = Sectors 108-121, started 7 Sep 2026; "Sector 110 begins on October 31,
2026" (https://tess.mit.edu/observations/). The 2-min allocation is a fixed
13,000 targets per sector in Cycle 8 (identical count in all eleven sectors, and
in a declination-banded re-query of Sector 97); the 20-s allocation is
2,100-2,700 per sector. Sector 100 is "one of sixteen consecutive rolled sectors
focusing on the southern ecliptic mid-latitude range".

Typical latency observed: 24-35 days from end of sector to light curves at MAST.
Sector 108 should therefore appear around 2026-10-30 to 11-10.

## 2. How many of our 3,339 WDs have 20-s SPOC light curves

### Method

Two independent routes, both on 2026-10-06.

(a) **Complete census by positional cross-match.** For every sector 1-109 I
pulled the full list of SPOC 20-s timeseries observations from MAST CAOM
(`query_criteria(..., sequence_number=S, t_exptime=[19,21])`, columns
`target_name, s_ra, s_dec, proposal_id, t_min, t_max, t_obs_release`): 156,696
observations in sectors 27-107 (20-s mode started in Sector 27; sectors 1-26
return 0). The same for 2-min in sectors 97-107 (143,000 rows). Each
observation was matched to the nearest star of `data/catalog/wd_100pc.csv`
(Gaia EDR3 epoch 2016 positions) within a radius of 10" + 16 yr x proper motion
(clipped to 10-90"), to absorb the J2000 TIC epoch. 9,621 20-s observations
matched 2,847 distinct WDs; median separation 1.7", 90 % < 5.4". Caveats: 63 WDs
matched more than one TIC id (a neighbour inside the radius is counted as the WD),
and at the bright end the 20-s target can be the primary of a WD binary (Sirius B,
40 Eri B, ...). Expect ~3 % false "has 20-s" at G < 13, negligible fainter.

(b) **Per-target lightkurve sample.** 337 stars queried one by one with
`lightkurve.search_lightcurve(target, mission="TESS")` (no exptime filter; the
SPOC rows were then split by exposure time): all 37 stars with G < 13 and TIC id
in `targets.csv`, 60 random of 102 at 13-14 and 80 random of 221 at 14-15 (by
TIC id), plus 80 random at 15-16 and 80 at 16-17 from the catalogue (by
coordinates, 40" cone, nearest TIC kept). 339 queries including WD 1856+534 and
ZTF J0328-1219, 0 failures, sequential with 0.5 s pauses. Routes (a) and (b)
agree on "has any 20-s" for 97 % of the common stars and on the exact sector
count for 96 %; the disagreements are the bright-binary and neighbour cases
above.

### Results (complete census, route a)

| G bin | N WDs | with any 20-s | with 20-s in S >= 100 | with 20-s after S65 (post Robert+24) | 20-s sectors per star (median / mean / max) |
|---|---|---|---|---|---|
| < 13 | 38 | 37 (97 %) | 7 (18 %) | 32 | 2 / 4.4 / 30 |
| 13-14 | 102 | 97 (95 %) | 16 (16 %) | 89 | 3 / 5.0 / 30 |
| 14-15 | 336 | 318 (95 %) | 48 (14 %) | 283 | 2 / 3.5 / 31 |
| 15-16 | 992 | 878 (89 %) | 100 (10 %) | 724 | 2 / 3.3 / 29 |
| 16-17 | 1,871 | 1,517 (81 %) | 142 (8 %) | 1,267 | 2 / 3.2 / 29 |
| **all** | **3,339** | **2,847 (85 %)** | **313 (9.4 %)** | **2,395 (72 %)** | **2 / 3.35 / 31** |

Sample route (b), for comparison (fractions with any 20-s / with 20-s in S >= 100):
G < 13: 81 % / 19 % (n = 37); 13-14: 92 % / 12 % (60); 14-15: 96 % / 11 % (80);
15-16: 85 % / 10 % (80); 16-17: 83 % / 4 % (80); all 88 % / 10 %. Median 2-3
20-s sectors per star in every bin. The 2-min fractions in the same sample are
81-98 % (any) and 11-19 % (S >= 100).

Other numbers from the census:

- 898 WDs got their *first* 20-s light curve after Sector 65 (385 after Sector
  83, 117 in Cycle 8). So the post-Robert+2024 20-s material is not just new
  epochs of old targets.
- Cycle 8 (S97-107): 474 WDs with 20-s data (231 in one sector, 118 in two, 60
  in three, 62 in four, 3 in five); 905 WDs with 2-min data. Every 20-s target
  also has a 2-min light curve; 431 WDs have 2-min only.
- Sectors >= 100 (not covered by Cavalier+ 2026): **313 WDs at 20 s, 599 at
  2 min** (286 2-min only). 2-min per bin for S >= 100: <13: 7, 13-14: 20,
  14-15: 66, 15-16: 184, 16-17: 322.
- WDs with 20-s light curves per sector: 25-60 in Cycle 3 (S27-39), ~100-170 in
  Cycles 4-6 (S40-83), 100-170 in Cycle 7 (S84-96), 36-107 in Cycle 8 (S97-107;
  the dip to 36-77 in S100-103 is the southern mid-latitude "rolled" pointings).
- Per cycle (distinct WDs / median G): C3 291 / 15.2; C4 997 / 16.1; C5 1,356 /
  16.1; C6 1,094 / 16.1; C7 1,168 / 16.1; C8 474 / 15.9. The G distribution of
  the 20-s WD targets is essentially our catalogue's (90th percentile G = 16.9).

Physics note for the notebook: a transit of an Earth-size body across a
0.013 R_sun WD lasts ~2-4 min; at 2 min that is 1-2 points, at 20 s it is 6-12
points, which is why the 20-s products are the ones worth stacking.

## 3. Which GI programs put white dwarfs on the 20-s list (Cycles 6-8)

Read from the `proposal_id` attached to each matched 20-s observation at MAST,
and the program abstracts at
https://heasarc.gsfc.nasa.gov/docs/tess/data/approved-programs/cycleN/GNNNNN.txt .
Counts are observations / distinct WDs of *our* sample.

| Cycle | Program | PI | Title (abridged) | Target selection | Our WDs at 20 s |
|---|---|---|---|---|---|
| 4 | G04137 | J. Hermes (Boston U.) | High-speed observations of WDs in Cycle 4 | ">5,200 known or candidate white dwarfs", mixed 20 s / 2 min | 2,115 / 983 |
| 4 | G04036, G04200 | (not read) | - | - | 876, 830 WDs |
| 5 | G05084 | A. Vanderburg (MIT) | Disintegrating rocky bodies transiting WDs | WD list for transiting debris | 1,913 / 1,196 |
| 5 | G05115 | R. Aloisi (UW-Madison) | Habitable-zone planets around WDs | "white dwarf stars from Gaia eDR3", 20 s | 1,899 / 1,185 |
| 6 | G06028 | R. Aloisi (UW-Madison) | Habitable-zone planets and precursors around WDs | Gaia eDR3 WDs, 20 s only (622 targets in S70) | 1,982 / 989 |
| 6 | G06049 | A. Vanderburg (MIT) | Disintegrating rocky bodies transiting WDs | 2,250 at 2 min + 635 at 20 s (S70) | 1,982 / 989 |
| 6 | G06161 | J. Hermes (Boston U.) | Ultra-high-speed observations of WDs in Cycle 6 | known + high-likelihood pulsators, known rapid variables, eclipsing binaries (~850 targets) | 880 / 481 |
| 6 | G06197 | N. Suzuki (LBNL) | Companion stars of close WD binaries | HR-diagram binary candidates (354 targets) | 240 / 117 |
| 6 | G06024 | D. Martin (OSU) | WDs in binaries | 6,454 wide binaries with a WD | 180 / 85 |
| 6 | G06075 | J. Provencal (Delaware) | WD rotation / angular momentum | pulsators and rotators (81 targets) | 107 / 49 |
| 6 | G06158 | M. Pichardo Marcano (AMNH) | Magnetic WDs in symbiotic binaries | all confirmed symbiotics (~40), 20 s | - |
| 7 | G07092 | J. Becker (UW-Madison) | Discovery and occurrence rates of disintegrating minor planets transiting WDs | "largest search to date for transiting debris" (~2,800 targets in S84-86) | 961 / 689 |
| 7 | G07084 | K. Bell (CUNY) | TESS legacy catalogue for WD asteroseismology | 158 known + 7 known + 77 likely pulsators | 153 / 99 |
| 7 | G07036 | T. Wainer (UW) | Stellar activity cycles with flares | 14,268 CVZ stars (WDs incidental) | 359 / 96 |
| 7 | G07009 | D. Martin (Tufts) | WDs in binaries | 7,886 wide binaries | 94 / 68 |
| 7 | G07146 | J. Hermes (Boston U.) | Ultrafast monitoring of WDs in Cycle 7 | "several hundred" known variable WDs | small |
| 7 | G07020 | J. Provencal (Delaware) | WD rotation | ~40 WDs | 57 / 26 |
| 7 | G07169 | I. Clark (Iowa State) | Outbursting WDs | 5 known outbursters | 9 / 2 |
| 8 | G08062 | M. Soares-Furtado (UW-Madison) | Discovery and occurrence rates of disintegrating minor planets transiting WDs | 3,842 targets: 3,764 at 2 min, 78 at 20 s | 175 / 100 (20 s); 772 obs at 2 min |
| 8 | G08002 | R. Aloisi (UW-Madison) | Habitable-zone planets and precursors around WDs | Gaia eDR3 WDs, 20 s (82 in S97) | 170 / 97 (20 s); 767 obs at 2 min |
| 8 | G08082 | D. Martin (Tufts) | WDs in binaries | 5,009 wide binaries, 447 targets in S97-107 | 37 / 23 |
| 8 | G08158 | D. Rapetti (USRA) | Star-planet interactions (flares) | exoplanet hosts and flare stars (WDs incidental) | 12 / 7 |
| 8 | G08105 | J. Merc (Charles U.) | Magnetic WD in AE Cir | 1 symbiotic, 20 s, S99-102 | - |
| 8 | G08108, G08110 | B. Barlow (UNC) | Pulsating / post-CE hot subdwarfs | sdB stars, not WDs | - |

Not read individually: G04036, G04200, G05081, G03124, G03207 (Cycles 3-5).

Important metadata gap: from Cycle 7 on, most 20-s observations at MAST carry
**no proposal id** (449 of 1,694 WD observations in Cycle 7; 714 of 917 in Cycle
8; 88.5 % of all 26,883 Cycle 8 20-s observations of any kind). 283 of the 392
Cycle 8 "no-id" WDs had already been 20-s targets in earlier cycles, and their
G distribution is the same as the labelled ones, so they look like mission-side
re-observations of earlier GI lists (Cycle 8 "pre-selected / guaranteed"
targets, https://heasarc.gsfc.nasa.gov/docs/tess/list-of-guaranteed-targets-for-2-min-observation-in-cycle-8.html,
which I could not read in full) rather than a new selection. The per-cycle
program pages (approved-programs-cycleN.html) return 404; the main
approved-programs page only rendered Cycles 1-2 through the fetch tool.

**Answer to the question "known interesting WDs or broad Gaia sample?": broad.**
The bulk of the 20-s WD light curves (Cycles 4-8) come from three transit-search
programs that select from Gaia EDR3 WD lists - Aloisi (G05115/G06028/G08002,
habitable-zone planets), Vanderburg/Becker/Soares-Furtado
(G05084/G06049/G07092/G08062, disintegrating debris) - and from Hermes' broad
"known or candidate WD" lists (G04137, G06161). The pulsator/polluted/known-variable
programs (Bell G07084, Provencal, Hermes G07146, Clark) contribute only ~100-500
of our WDs each. Consequence for us: 85 % of our sample has 20-s data, with the
same magnitude distribution as the catalogue. Second consequence, to be stated
plainly: **these 20-s light curves exist because other teams proposed them for
exactly the search we plan** (HZ planets, transiting debris, occurrence rates).
"Unsearched" in `literature_verification.md` means "no published blind search";
the proposing teams (UW-Madison, MIT) very probably have run their own BLS on
their targets. What has not appeared is a published candidate list or
completeness. Our edge is therefore speed on the newest sectors and a
different period/duration grid, not exclusive data.

## 4. WD 1856+534 and ZTF J0328-1219

lightkurve `search_lightcurve`, SPOC rows only, 2026-10-06.

- **WD 1856+534 (TIC 267574918)**: 20-s in 18 sectors: 40, 41, 49, 53, 54, 55,
  56, 59, 73, 74, 75, 76, 79, 80, 81, 82, 83, 86. 2-min in 23 sectors: 14, 15,
  19, 22, 26 plus the same 18. Last sector 86 (Cycle 7); nothing in Cycle 8 so
  far. Ample 20-s material (18 sectors x 1.408 d period, ~330 transits) for the
  validation of the 20-s pipeline.
- **ZTF J0328-1219 (TIC 93031595, RA 52.1397, Dec -12.3292)**: **no 20-s data.**
  2-min only in Sector 31 (SPOC; also TESS-SPOC 600 s FFI product in S31, and
  FFI-only products in Sector 4). So it cannot serve as the 20-s validation
  target. Robert+ 2024 recovered it in the 2-min data. A better 20-s debris
  validator is WD 1054-226 (TIC 415714190: 2 min in S9, 20 s in S36, 63 and 90
  per Korth+ 2026, arXiv:2603.07677); SBSS 1232+563 and ZTF J1944+4557 (both
  northern, 20-s in Hermes+ 2025 / Guidry+ 2025) are alternatives.

## 5. Literature check: any 2026 paper searching 20-s WD light curves for transits?

arXiv API queries on 2026-10-06 (`export.arxiv.org/api/query`, sorted by
submission date): (i) all:"white dwarf" AND TESS AND ("20-second" OR "20-s" OR
"20 second" OR "20 s cadence"), 50 results; (ii) all:"white dwarf" AND TESS AND
(transit*), 60 results, 2026 subset; (iii) abs:"white dwarf" AND TESS AND
(debris OR eclipse OR transit OR occultation OR planet), 80 results, Sep-Oct
2026 subset; plus a web search.

**None found.** The 2026 entries that touch 20-s WD data are:
- arXiv:2605.03323 (Huang+, 5 May 2026) "A Search for High Frequency Oscillations
  in TESS Cycle 7" - Lomb-Scargle on Cycle 7 20-s light curves, pulsations, no
  box search.
- arXiv:2605.22802 (Luna+, 21 May 2026) rapidly rotating WD in nova YZ Ret, 20-s
  timing; single object.
- arXiv:2603.07677 (Korth+, Mar 2026) WD 1054-226 revisited, uses its own 20-s
  sectors 36/63/90; single object, already in `literature.md`.
- arXiv:2606.03850 (Cavalier+, Jun 2026) remains 2-min only.
- Newest matching entry in query (iii) is arXiv:2609.06352 (eclipsing CV), not
  relevant.

Status unchanged since 2026-10-05: no published blind transit search of TESS
20-s WD light curves beyond Robert+ 2024 (214 polluted WDs, S1-65), and nothing
at all on sectors >= 100 at any cadence.

## 6. What this means for the pipeline switch to 20 s

1. Target list: 2,847 WDs with 20-s data (`tess_20s_coverage.csv`); order by
   `n_20s_S100plus` desc, then by newest `sectors_20s`, then by `n_20s`. The
   313 stars with 20-s data in S100-107 and the 286 with 2-min only in S100-107
   are the fully unsearched set; the 2,395 with 20-s data after S65 are
   unsearched at 20 s in published work.
2. Validation: WD 1856+534 b at 20 s (18 sectors) and WD 1054-226 (3 sectors),
   not ZTF J0328-1219.
3. Sector 108 should land at MAST in early November 2026; re-run the per-sector
   MAST list (sections 1-2 scripts) monthly rather than re-querying targets one
   by one.
4. Volume: ~9,600 20-s light-curve files for the whole sample; a 20-s SPOC
   file is ~6x a 2-min one (~10-15 MB), i.e. ~100-150 GB in total. Run in
   batches below the 20 GB job limit, newest sectors first.

### Query scripts (scratchpad, this session)

`mast_sector_lists.py` (per-sector CAOM lists), `crossmatch.py` (positional
match and tables), `tess20s_census.py` + `analyze_census.py` (per-target
lightkurve sample). Raw lists kept in the session scratchpad only; the derived
per-WD table is `research/notes/tess_20s_coverage.csv`.
