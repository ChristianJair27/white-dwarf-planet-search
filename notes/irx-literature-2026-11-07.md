# IR-excess literature check, 2026-11-07

Two read-only tasks: (1) obtain the Lai et al. 2021 Spitzer/Gemini tables for cross-matching
with our 100 pc IR-excess candidates; (2) check arXiv for the two papers announced in
`research/notes/ir-excess-literature.md` (a Murillo-Ojeda "Paper II" and a "K. De et al."
unWISE light-curve paper).

## 1. Lai et al. 2021, ApJ 920, 156 (arXiv:2107.01221) — tables obtained

Source: the arXiv LaTeX source tarball, https://arxiv.org/src/2107.01221 (4.48 MB, v2 of
27 Oct 2021), downloaded to `data/irx/lit/lai2021_src/` and unpacked there (treated as
untrusted data; nothing executed). The abstract page https://arxiv.org/abs/2107.01221 says
"Three of the tables are available digitally", and the tarball indeed contains the three
machine-readable tables that the paper footnotes as "Temporarily available at
https://www.mso.anu.edu.au/~samlai/...":

| File | Paper table | Rows | Content |
|---|---|---|---|
| `Table_2_MR.csv` | Table 2 | 320 | All photometry: Gemini NIRI/F2 JHK (235 targets) and Spitzer IRAC ch1/ch2 (183 targets, 98 in both) |
| `Table_A2_MR.csv` | Table A2 (`tab:excess_all`) | 62 | Spitzer-confirmed IR excess: chi_J/H/K, chi_ch1/ch2, colour excess, flags, excess type, Sample, Teff, log g |
| `Table_A3_MR.csv` | Table A3 (`tab:no-excess_all`) | 121 | Spitzer-observed without confirmed excess (incl. 9 with flag `s`, unreliable PRF photometry) |

Positions are Gaia RA/Dec in decimal degrees in all three files; nothing had to be derived
from names. Nine further "best remaining targets" (Table 5, `tab:remaining_targets`, not
observed with Spitzer) were copied by hand from `sample63.tex` lines 276-284.

### Output: `data/irx/lit/lai2021.csv`

Columns `name, ra_deg, dec_deg, verdict, spitzer, notes`. 328 rows (320 from Table 2 + 8
Table 5 targets not in Table 2). Numbers are copied as strings from the MR files.

Verdict mapping (paper's own rules, Section 4: "white dwarfs are considered to have an IR
excess when either flux excess or color excess metric exceed the threshold"; Section 5:
"we use this metric to identify Spitzer-confirmed infrared excess candidates with
chi_J >= 3.0 as likely to be hosting a companion rather than a dust disk"):

| verdict | n | meaning |
|---|---|---|
| `companion` | 10 | Table A2 with `J` flag (chi_J >= 3): GaiaJ0007+1951, 0433+2827, 0507+4541, 0751+1059, 0841-6511, 1100-1350, 1131-1438, 1731-1002, 2026+5925, 2048+1333 |
| `disk_candidate` | 52 | Table A2 without `J` flag. Whole A2: 26 Colour+Flux, 34 FluxOnly, 2 ColourOnly; the 52 non-companions split 25 / 25 / 2 because one companion (GaiaJ0507+4541, flags `Jg`, Gemini photometry flagged) is Colour+Flux. The paper's conclusion says "The remaining 52 ... 26 of which exhibit both flux and color excess", a one-object difference I cannot resolve from the files. The paper does not confirm disks; it says these "have the potential to double the known sample" |
| `no_excess` | 112 | Table A3, Spitzer photometry reliable, unWISE excess refuted |
| `unreliable` | 9 | Table A3 with `s` flag; authors exclude them from statistics |
| `unknown` | 136 | Table 2 only: Gemini JHK, never observed by Spitzer; no verdict published |
| `unobserved_best_candidate` | 9 | Table 5: unWISE Colour+Mag candidates from Paper I not observed by Spitzer, recommended for follow-up (one, GaiaJ0508+0535, has Gemini photometry in Table 2) |

`spitzer` = yes for 183 rows, no for 145. The `notes` column carries excess type, Sample,
flags, all chi values, Teff/log g (from Gentile Fusillo+ 2019, as the MR files give them) and
the raw Gemini/Spitzer photometry. Not derivable and left out: a per-object disk vs
brown-dwarf distinction ("we do not distinguish between stellar or brown dwarf companions"),
and any verdict for the 136 Gemini-only targets. The Spitzer flux columns of `Table_2_MR.csv`
are in an unstated unit (the printed Table 2 gives magnitudes); they are copied verbatim.

Totals: 62 Spitzer-confirmed excesses = 52 disk candidates + 10 likely companions, and the
CSV reproduces exactly these counts. Verbatim from the paper (`sample63.tex`):

- Abstract: "In total, we confirm the infrared excess around 62 white dwarfs, 10 of which are
  likely to be stellar companions."
- Section 4.3: "Our Spitzer observations confirm a total of 62 white dwarfs with flux or color
  infrared excess, ten of which have excess likely to be attributed to low-mass companions
  rather than debris disks based on the observed J-band excess."
- Section 3: "In this study, we have identified a total of 62 systems with Spitzer-confirmed
  infrared excess across all Samples ABCDE, 44 of which are from the unWISE-selected
  candidates in Sample E originally from Paper I."
- Table 2 caption: "The total number of targets observed is 320, with near-infrared photometry
  reported for 180 targets for the first time and new Spitzer photometry for 174 targets."
  (174 = 183 observed minus the 9 `s`-flagged.)

Parser: scratch script `parse_lai2021.py` (run with `python -I`, paths as arguments); the
rules above are its docstring.

## 2. arXiv check for the two announced papers

All queries via https://export.arxiv.org/api/query, `max_results=50`, sorted by submission
date descending, run 2026-11-07. Lesson: the `au:Last_F` underscore convention fails for
hyphenated surnames; `au:"Murillo-Ojeda"` (quoted, hyphen) works.

### (a) Murillo-Ojeda, Jiménez-Esteban, Rebassa-Mansergas & Torres, "Paper II" — NOT FOUND

Not found with these queries:

- `au:Murillo_Ojeda` -> 0; `au:Murillo AND all:"white dwarf"` -> 0; `au:Ojeda AND all:"white dwarf"` -> 0
- `au:Rebassa_Mansergas AND all:infrared` -> 0; `au:Jimenez_Esteban AND all:"white dwarf"` -> 0
- `au:"Murillo-Ojeda"` -> 9 papers (2022-2026); newest 2604.09845 (2026-04-10, Jałowiczor+,
  WD J0008-3504 with two companions). The only IR-excess paper is Paper I, 2602.10070.
- `au:"Rebassa-Mansergas" AND all:infrared` -> 17; 2025-26: 2604.09845, 2603.10481
  (Wang, Liu, Xu, Rebassa-Mansergas, "White Dwarfs with Infrared Excess from LAMOST DR11"),
  2602.10070, 2512.14774 (Raddi+, "The Future of Evolved Planetary Systems", white paper).
- `au:"Jimenez-Esteban" AND all:infrared` -> 17; 2025-26: 2603.17083 (J-PLUS stellar
  parameters), 2602.10070.
- `all:"infrared excess" AND all:"white dwarf" AND all:"100 pc"` -> 4; only 2602.10070 in 2025-26.
- `ti:"infrared excess" AND ti:"white dwarf"` -> 18; 2025-26: 2604.11175 (Wang & Liu, DESI
  EDR), 2603.10481 (LAMOST DR11), 2602.10070, 2509.12116 (Morales+, HETDEX, 30 WDs),
  2507.20594 (Bhattacharjee, thick disks).
- `ti:"Gaia white dwarfs with infrared excess"` -> 1 (Paper I only).
- Author page https://arxiv.org/a/murilloojeda_r_1.html -> HTTP 404.
- Web search `"Gaia white dwarfs with infrared excess II" Murillo-Ojeda` -> only Paper I
  (arXiv HTML/PDF, A&A page https://www.aanda.org/articles/aa/pdf/2026/03/aa57709-25.pdf).

Paper I confirmed: arXiv:2602.10070, "Gaia white dwarfs with infrared excess I. The 100 pc
catalogue", submitted 2026-02-10, A&A 707, A268 (2026), Comments "Accepted in A&A"
(https://arxiv.org/abs/2602.10070). Abstract: "We built a catalogue of 456 infrared excess
WDs, of which 292 are robust identifications, and 164 are candidates." and "351 (~75%) are
new identifications." and "This implies a fraction of infrared excess WDs between 5.9+/-0.3%
and 9.2+/-0.4%". The abstract page does not itself announce a Paper II; the "I." in the title
is the only indication of a series. Our note's "Paper II is announced" comes from the full
text read on 2026-10-05 (literature_verification.md line 138); as of today no Paper II is on
arXiv.

### (b) K. De et al., unWISE/NEOWISE light curves of dusty white dwarfs — NOT FOUND

Context: Guidry+ 2024 (arXiv:2406.18646, "Using 3.4-um Variability towards White Dwarfs as a
Signpost of Remnant Planetary Systems", K. De third author) defers the light-curve pipeline
to "K. De et al. in prep". Not found with these queries:

- `au:De_K AND all:"white dwarf" AND (all:unWISE OR all:NEOWISE OR all:WISE)` -> 2:
  2609.08923 (van Roestel+ 2026, De is 12th author; ZTF obscuration events, not WISE light
  curves) and 1507.04175 (unrelated, "De Smedt").
- `au:De_Kishalay AND all:"white dwarf"` -> 17; none from 2025-26 on WD dust (2606.12532 is a
  nova; 2505.06228 is cecilia, He-atmosphere WD compositions, De coauthor).
- `au:De_K AND all:dust AND all:"white dwarf"` -> 1 in 2025-26: 2609.08923.
- `au:De_K AND cat:astro-ph.SR` -> 44; 2025-26 entries: 2609.08923, 2601.00386 (TRAPPIST-1
  flares), 2511.12362 (Type Ibn SNe). Nothing on WD dust.
- `ti:"white dwarf" AND (ti:unWISE OR ti:NEOWISE)` -> 2 (Lai+ 2021, Xu+ 2020).
- `all:unWISE AND all:"white dwarf"` -> 3 (2406.18646, 2107.01221, 2009.00193); none 2025-26.
- `all:"white dwarf" AND all:NEOWISE` -> 2; 2025-26: 2609.08923 only.
- `all:"white dwarf" AND all:NEOWISE AND (all:dust OR all:disk) AND all:"light curve"` -> 1 (2410.14644, SNe Ia).
- `au:Guidry_J AND all:"white dwarf"` -> 2025-26: 2609.08923 only.
- `all:"white dwarf" AND all:"debris disk" AND all:WISE AND (variability OR variable OR "light curves")`
  -> 1 in 2025-26: **2609.34868**, Noor, Farihi & Kenyon, "Activity in White Dwarf Debris
  Disks II: WISE Mission Traces a Decade of Disk Evolution and Persistence", submitted
  2026-09-28, "Submitted to MNRAS (in revision)" (https://arxiv.org/abs/2609.34868). No author
  named De. Abstract: "multi-epoch photometry from the Wide-field Infrared Survey Explorer",
  "utilizing the full 14.5 yr mission datasets pre- and post-cryogen", "Unambiguous variations
  are detected across the bulk of the 52 confirmed dusty white dwarfs". This is the closest
  2026 paper to the announced topic, but it covers the 52 known disks, not a blind unWISE
  survey of IR-excess candidates.
- Web search (Kishalay De, white dwarf, NEOWISE/unWISE, 2025-2026) -> only Guidry+ 2024 and a
  Feb 2025 Caltech colloquium abstract on De's "WISE Transients Project" (NEOWISE archival
  variability); no 2025-26 preprint.

### Consequence for our plan

Both competitor papers remain unpublished as of 2026-11-07. The gaps listed in
`ir-excess-literature.md` (items 1, 3 and 4: deblended forced photometry of the 456 / 164
tentative objects, and W1+W2 light curves below G_RP = 17) are still open. New since the
last check and worth reading before the cross-match: Noor+ 2026 (2609.34868, WISE variability
of the 52 known disks), Wang+ 2026 (2603.10481, LAMOST DR11 IR excess), Wang & Liu 2026
(2604.11175, DESI EDR IR excess), Morales+ 2025 (2509.12116, HETDEX, 30 WDs).
