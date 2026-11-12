# Three-dimensional correlation function of the Gaia 100 pc white dwarfs

Date: 2026-11-08. Code: `wdplanets/labs/wd_clustering.py` (Landy-Szalay from `labs/clustering.py`).
Data: data/catalog/wd_100pc.csv (16,676 high-confidence white dwarfs within 100 pc, Gentile Fusillo et al.
2021 selection, Galactic x, y, z in pc). Results: data/catalog/xi_wd_all.csv; figure ../figures/wd_xi.png.

## Why

After the SDSS replication (notes/sdss-clustering.md) the plan was to point the same estimator at a sample
nobody has clustered. A web search (2026-11-08) found stellar two-point correlation functions for the solar
neighbourhood (Kamdar et al., arXiv:2007.10990, 1.7 million Gaia DR2 stars within 1 kpc, power law of slope
about -1 between 1 and 100 pc; Hinkel, Gardner & Yanny, arXiv:2210.13450, Gaia DR3 stars within a few kpc)
and wide-binary separation studies of white dwarfs (El-Badry & Rix 2018, arXiv:1807.06011, within 200 pc;
Torres et al. 2022, arXiv:2202.04199, comoving pairs within 100 pc), but no correlation function computed for
white dwarfs alone. ADS was not queried (it blocks scripts), so "not published" is still UNVERIFIED in the
sense of research rule 3.

## Random catalogue (the whole measurement)

n(r, b) = S(r) * exp(-|z| / h), with S(r) the data's own distance distribution (carries the completeness
loss of cool, faint white dwarfs with distance) and h fitted by a KS comparison of the |z| distributions:

| h (pc) | KS |
|---|---|
| 150 | 0.060 |
| 300 | 0.028 |
| 700 | 0.0099 |
| 3000 | 0.0067 |
| isotropic | 0.0124 |

Best: h = 3000 pc, i.e. the sample shows almost no vertical gradient inside 100 pc. A thin-disc scale height
of ~300 pc would thin the sample by 28 % at |z| = 100 pc; it does not, which suggests that completeness
losses near the Galactic plane (crowding) roughly cancel the disc gradient in this sample. Not pursued.
20 randoms per white dwarf (333,520), 18 logarithmic bins from 0.001 to 60 pc, jackknife over 8 Galactic
longitude wedges. Runtime 11.6 min.

## Result

| r (pc) | xi | jackknife error | DD pairs |
|---|---|---|---|
| 0.18 | 10.0 | 3.3 | 38 |
| 0.33 | 3.04 | 0.35 | 90 |
| 0.61 | 0.75 | 0.16 | 234 |
| 1.13 | 0.094 | 0.076 | 906 |
| 2.08 | 0.035 | 0.024 | 5,362 |
| 3.83 | 0.022 | 0.012 | 32,430 |
| 7.06 | 0.0056 | 0.0056 | 195,410 |
| 13.0 | 0.0030 | 0.0025 | 1.16 M |
| 24.0 | 0.0013 | 0.0019 | 6.5 M |
| 44.2 | 0.0013 | 0.0009 | 32.6 M |

Bins below 0.1 pc have fewer than 100 random pairs and are not usable (the binary regime below ~20,000 au
is already measured by the wide-binary papers above; it needs an analytic RR, not more randoms).

- 0.1-1 pc: xi ∝ r^-2.1, the tail of the wide-binary population out to ~1 pc (200,000 au), as in El-Badry &
  Rix 2018 and Torres et al. 2022.
- 1-5 pc: xi = 0.02-0.09, each bin 1.2-1.8 sigma above zero, all positive. A weak excess at this scale would
  be comoving groups or the remains of birth clusters; for a population with a median age of gigayears it
  should be small. Not significant on its own; the combined excess of the three bins is about 2.5 sigma if
  the bins were independent (they are not, the jackknife covariance was not propagated).
- 7-60 pc: consistent with zero (0.0013 +/- 0.0009 at 44 pc).

Verdict: beyond the wide-binary regime the 100 pc white dwarfs are unclustered at the per-cent level; the
hint at 1-5 pc is a target for a follow-up, not a result.

## Follow-ups (ordered)

1. Cross-correlate the polluted subsample (data/polluted_priority.csv, 798 objects) with the full sample at
   0.001-1 pc to test whether polluted white dwarfs have more wide companions (the binary-driven pollution
   channel of Bonsor & Veras 2015); the auto-correlation of 798 objects is too sparse.
2. Compare the 1-5 pc values with the all-star correlation function of Kamdar et al. (read the paper; the
   number quoted above is from an abstract).
3. Jackknife covariance and a proper significance of the 1-5 pc excess; test the selection model by
   replacing S(r) with a volume-limited cut (d < 50 pc, where the sample is complete for most of the
   cooling sequence).
4. Once ADS is reachable, search "white dwarf" + "two-point correlation" before any claim of novelty.

## Follow-up 1 done: wide WD companions of the polluted white dwarfs (2026-11-08)

`wdplanets/labs/wd_pairs.py`, data/catalog/wd_pairs.csv. Direct neighbour counts in the 100 pc sample (no
random catalogue): companions per star in 3-D separation bins, polluted (798) against the other 15,878 white
dwarfs re-weighted to the same joint (distance, G) distribution (effective control size 11,461). The polluted
list is not brighter than the sample (median G 18.61 vs 18.41) because most of it comes from the Gaia XP
classes of Vincent et al. 2024.

| separation (pc) | polluted pairs | per polluted star | per matched control star |
|---|---|---|---|
| 0.003-0.01 | 0 | 0 | 0.0007 |
| 0.01-0.03 | 0 | 0 | 0.0007 |
| 0.03-0.1 | 1 | 0.0013 | 0.0029 |
| 0.1-0.3 | 1 | 0.0013 | 0.0038 |
| 0.3-1 | 16 | 0.0201 +/- 0.0050 | 0.0246 |

Within 1 pc: 0.0226 +/- 0.0052 companions per polluted star against 0.0327 for the matched control (ratio
0.69). In the binary-dominated range 0.003-0.3 pc the polluted stars show 2 pairs where the control predicts
6.5 (Poisson probability of 2 or fewer: 0.04). Verdict: no excess of resolved white-dwarf companions among
polluted white dwarfs; if anything a 2-sigma deficit. This only tests WD+WD pairs: the binary-driven pollution
channel (Bonsor & Veras 2015) mostly involves main-sequence companions, which need the El-Badry et al. 2021
wide-binary catalogue (VizieR J/MNRAS/506/2269) cross-matched with data/polluted_priority.csv. That is the
next step, and it is cheap.

## Follow-up 2 done: companions of any type from El-Badry, Rix & Heintz 2021 (2026-11-08)

`python -m wdplanets.labs.wd_pairs --elbadry`; data/catalog/elbadry2021_100pc.csv (25,099 pairs with Plx1 > 9.5 mas
from VizieR J/MNRAS/506/2269 via the Harvard mirror), data/catalog/xp_classes.csv (Vincent et al. 2024 XP classes
for the control), results in data/catalog/wd_pairs_elbadry.csv. Pairs with chance-alignment probability R < 0.1:
2,035 of our 16,676 white dwarfs have a companion in that catalogue (496 of them another white dwarf of our sample).
Control = non-polluted white dwarfs with a Vincent+24 XP class (14,008), re-weighted to the polluted (distance, G)
distribution.

| separation (au) | polluted with companion (of 798) | expected from matched control | ratio |
|---|---|---|---|
| < 100 | 1 | 1.9 | 0.5 |
| 100-1000 | 27 | 51.2 | 0.53 |
| 1,000-10,000 | 23 | 38.7 | 0.59 |
| > 10,000 | 1 | 4.1 | 0.24 |
| all | 52 | 96.0 | 0.54 +/- 0.08 |
| all, MS companions | 43 | 70.9 | 0.61 |
| all, WD companions | 9 | 25.0 | 0.36 |
| all, H-atmosphere polluted (DA*, 176) | 11 | 20.8 | 0.53 |
| all, other polluted (622) | 41 | 75.2 | 0.55 |

The companion fraction of polluted white dwarfs is 6.5 +/- 0.9 % against 12.0 % for the matched control: a
deficit of 44 companions where 96 were expected (4.5 sigma if Poisson), the same whether the control is all
non-polluted stars or only the XP-classified ones, for main-sequence and white-dwarf companions alike, and
at 100-1,000 au as much as at 1,000-10,000 au.

Literature (abstracts read 2026-11-08, full papers not yet): Noor, Farihi, Hollands & Toonen 2024
(arXiv:2403.08870, MNRAS accepted) find a wide-binary fraction of 10.6 (+3.9/-3.2) % for 71 DAZ stars, within
1 sigma of the field, but below 1.8 % for two DZ catalogues (116 and 101 stars), each more than 3 sigma below
the field. Xu et al. 2026 (arXiv:2609.11798, ApJ in press, DESI DR1) find cool metal-enriched white dwarfs in
9.8 +/- 2.1 % of wide binaries against 20.5 +/- 0.9 % of single stars (4.7 sigma), with the enrichment
decreasing at smaller separations and lower temperatures. Bonsor & Veras 2015 (arXiv:1508.05715) proposed wide
companions as a pollution trigger (Kozai-Lidov); O'Brien et al. 2024 (40 pc sample, arXiv:2312.02735) report
few polluted stars in wide binaries.

What ours adds: an independent, Gaia-selected (mostly XP-classified) sample of 798 polluted white dwarfs within
100 pc gives the same suppression factor as the DESI result (0.54 +/- 0.08 here, 0.48 +/- 0.10 from the DESI
fractions, the two conditional fractions being equivalent at these small values), and in our sample the deficit
is present for the H-atmosphere polluted stars too (11 vs 20.8, 2 sigma), unlike Noor et al.'s DAZ result.
Not new as a phenomenon (rule 2 satisfied: it is published twice); possibly new in extent (DA* deficit, same
suppression at 1,000-10,000 au). Caveats before any write-up: (1) the XP "Z" flags (PDZ > 0.5) are noisy, which
dilutes but cannot create a deficit; (2) could a companion hide pollution from the XP classifier? Blending only
matters below ~3.5 arcsec (280 au at 80 pc), while the deficit is as strong at 1,000-10,000 au; (3) the
El-Badry catalogue's astrometric quality cuts apply equally to both groups; (4) the "DA*" split uses whichever
spectral type string any source catalogue gave. Report: research/reports/2026-11-08-polluted-wd-wide-binaries.md.
