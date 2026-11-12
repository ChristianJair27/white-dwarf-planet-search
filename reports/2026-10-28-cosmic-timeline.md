# A linear timeline of cosmic history: 13.787 billion years in 10 minutes

Date: 2026-10-28. Author: Kister Space (Christian Jair). Code: `wdplanets/labs/cosmic_timeline.py`.

## Summary

Our timelapse video maps the age of the universe linearly onto 600 s of screen time.
One second of video is 23.0 million years; one frame at 24 fps is
0.957 million years. The Solar System appears at 401.2 s, the
Cambrian at 576.6 s, the end of the dinosaurs at
597.13 s, and the whole Holocene (11,700 years) lasts
0.51 ms, about 1/1964
of a second: less than one frame.

## Data

- Planck Collaboration 2020, A&A 641, A6 (arXiv:1807.06209), Table 2, column TT,TE,EE+lowE+lensing+BAO:
  age 13.787 ± 0.020 Gyr, z* = 1089.80 ± 0.21, z_re = 7.82 ± 0.71.
- International Commission on Stratigraphy, International Chronostratigraphic Chart v2024/12.
- GPlates Web Service, coastline reconstructions with the plate model of Merdith et al. 2021
  (Earth-Science Reviews 214, 103477), 17 snapshots from 1000 Ma to today.

## Method

Universe ages at a redshift come from astropy's `Planck18` cosmology (flat ΛCDM with the
Planck 2018 parameters). Geological events are converted with age = 13.787 Gyr − (Ma / 1000).

## Results

| event | universe age (Gyr) | how long ago (Gyr) | video time (s) | source |
|---|---|---|---|---|
| Last Scattering · The Cosmic Microwave Background | 0.0004 | 13.7866 | 0.02 | Planck 2018 Table 2 (z*) |
| The Dark Ages | 0.0057 | 13.7813 | 0.25 | era label; time from Planck18 cosmology |
| Reionization (Mid-Point) | 0.6569 | 13.1301 | 28.59 | Planck 2018 Table 2 (z_re, tanh model) |
| Birth Of The Solar System | 9.2200 | 4.5670 | 401.25 | ICS chart v2024/12 (base of Hadean) |
| Archean Eon | 9.7560 | 4.0310 | 424.57 | ICS chart v2024/12 (4031 +/- 3 Ma) |
| Proterozoic Eon | 11.2870 | 2.5000 | 491.20 | ICS chart v2024/12 |
| Cryogenian Period | 13.0670 | 0.7200 | 568.67 | ICS chart v2024/12 (~720 Ma) |
| Ediacaran Period | 13.1520 | 0.6350 | 572.37 | ICS chart v2024/12 (~635 Ma) |
| Cambrian Period · Phanerozoic Eon | 13.2482 | 0.5388 | 576.55 | ICS chart v2024/12 (538.8 +/- 0.6 Ma) |
| End-Permian · Triassic Begins | 13.5351 | 0.2519 | 589.04 | ICS chart v2024/12 (251.902 +/- 0.024 Ma) |
| Jurassic Period | 13.5856 | 0.2014 | 591.24 | ICS chart v2024/12 (201.4 +/- 0.2 Ma) |
| Cretaceous Ends · Paleogene Begins | 13.7210 | 0.0660 | 597.13 | ICS chart v2024/12 (66.00 Ma) |
| Quaternary · Ice Ages | 13.7844 | 0.0026 | 599.89 | ICS chart v2024/12 |
| Holocene | 13.7870 | 0.0000 | 600.00 | ICS chart v2024/12 (11,700 yr) |

## Limitations

- Ages of the first stars and galaxies are model-dependent; the video labels the era (dark
  ages, cosmic dawn) and does not claim a date for them.
- Plate reconstructions before ~250 Ma rest on sparse palaeomagnetic data; they show where
  the continents were in the model, not surveyed coastlines.
- Visuals of the early universe and of early Earth are simulations and illustrations; the
  on-screen provenance line says which shots are data and which are renders.

## References

- Planck Collaboration 2020, A&A 641, A6.
- Cohen, K. M., Finney, S. C., Gibbard, P. L. & Fan, J.-X. 2013 (updated 2024/12), The ICS International
  Chronostratigraphic Chart, Episodes 36, 199–204.
- Merdith, A. S. et al. 2021, Earth-Science Reviews 214, 103477.
- Astropy Collaboration 2022, ApJ 935, 167.
