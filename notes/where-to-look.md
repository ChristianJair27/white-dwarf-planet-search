# Where to look first: clock + fate, star by star (2026-11-10)

Code: `-m wdplanets.labs.where_to_look [--write-priority]`. Output: research/hz_priority.csv (3,329 white dwarfs with
G < 17 and a cooling age), figure ../figures/where_to_look.png. Inputs: data/catalog/wd_ages.csv (wdclock),
planetfate (inverse IFMR, a_crit), research/notes/tess_20s_coverage.csv, data/polluted_priority.csv, research/targets.csv.

## What it computes

- Progenitor mass by inverting the Cummings et al. (2018) IFMR: available for 2,697 of 3,329 stars (white-dwarf mass
  0.55-1.24 Msun). Gap edge (closest surviving Jupiter today): median 11.1 AU, 16-84 % 6.4-18.3 AU. So for every star in
  the sample a planet in the habitable zone (0.005-0.03 AU) is a migrant by three orders of magnitude in distance.
- Score = transit probability at the habitable-zone centre x transits per 27-day sector x brightness factor x
  habitable-stay factor x 2 if metal-polluted x 0.5 without 20-s data. A ranking device; all ingredients are in the CSV.

## Result

Top of the list: cool (4,000-6,700 K), nearby (4-20 pc), G = 12-16 white dwarfs whose habitable zone has periods of
5-40 hours and where a planet at the zone centre stays habitable 3-6 Gyr. First ten: WDJ225353.39-064654.49 (G 15.4,
8.5 pc, 4,190 K, polluted), WDJ055509.53-041007.07 (14.2, 6.4 pc, polluted), WDJ024836.43+542322.46, WDJ084248.46-134713.21,
WDJ174807.99+705235.92, WDJ082126.70-670320.02, WDJ004909.90+052318.99 (van Maanen 2: 12.3, 4.3 pc, polluted, not yet
searched), WDJ215140.11+591734.85, WDJ113430.48-325002.40, WDJ144725.34-174215.75.
In the top 200: 82 already searched, 184 with 20-s data, 36 polluted, median G 16.1, median habitable-zone period 20 h.
The 118 unsearched stars of the top 200 were appended to research/priority_targets.txt and the survey was restarted
(112 priority targets queued).

## Limits

- The transit probability per star is 0.5-1.3 %: even a complete search of the top 200 expects about one transiting
  habitable-zone Earth only if every star had one. The list orders the work; it does not promise a detection.
- Pure-H Gaia parameters; cool DZ/DC stars (many of the top ranks) have He-rich atmospheres and their Teff, mass and
  ages are biased. The simple common-name identifications above were not checked in SIMBAD (mirror down today).
- "Polluted" doubles the score by choice (pollution means bodies are being scattered inward now); change the weight in
  build() if it should not.
- Faint stars (G > 16) have 20-s photometric noise comparable to a shallow transit; the injection-recovery test
  (backlog 6) is what will turn this ranking into a real sensitivity map.
