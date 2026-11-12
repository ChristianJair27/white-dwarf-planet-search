# The death of the Sun and the fate of its planets

Date: 2026-10-26. Author: Kister Space (Christian Jair). Lab code: `wdplanets/labs/sun_death.py`.

## Summary

We combined the solar-evolution numbers of Schröder & Connon Smith (2008) with our own
N-body runs to tell, with numbers, what happens to the eight planets when the Sun dies.
Mass loss alone (1.000 → 0.668 → 0.5405 M☉) widens every orbit by the adiabatic factor
a ∝ 1/M; our REBOUND integration reproduces this to 1.56 %.
Mercury and Venus still end inside the red giant (radius 256 R☉ = 1.19 AU). Earth would
reach 1.50 AU and survive if mass loss were the only effect; the paper's tidal and drag
calculation shows it is engulfed 0.5 Myr before the RGB tip, 7.59 Gyr from now. A planet
needs a present orbit of at least 1.15 AU to survive, so Mars (1.52 AU) is the innermost
survivor and ends at 2.82 AU around the 0.54 M☉ white dwarf.
The habitable zone moves from 1 AU today to 49–71 AU at the RGB tip, the Kuiper Belt.

## Data

- Schröder, K.-P. & Connon Smith, R. 2008, MNRAS 386, 155 (arXiv:0801.4031): Table 1
  (phases, L, Teff, R, M), Section 4 (orbit of Earth, engulfment, 1.15 AU threshold),
  Section 6 (final white-dwarf mass 0.5405 M☉). Local copy `data/schroeder_smith_2008.pdf`.
- Present-day planetary semi-major axes, eccentricities and masses: nominal mean values
  (NASA planetary fact sheet). Inclinations and phases randomised (seed 7).

## Method

REBOUND 5.2.2, IAS15 integrator, units AU/yr/M☉. The Sun's mass is
updated every 5 yr along two linear ramps: 1.000 → 0.668 M☉ over
2e+05 yr (RGB), a coast of 2e+04 yr, 0.668 → 0.5405 M☉
over 1e+05 yr (AGB) and a final coast. Both ramps are long compared with
Neptune's 165-yr period, so the expansion is adiabatic, as the real one is (the paper's RGB
mass-loss rate peaks at ~10⁻⁷ M☉/yr over the last Myr). Tides and chromospheric drag are not
simulated; we quote the paper. Habitable-zone limits are 0.95–1.37 AU scaled by √L, as the
paper adopts; Earth's equilibrium temperature uses T(1 AU) = 255 K (A = 0.3) scaled by L^¼.
Wall time 757 s.

## Results

| planet | a now (AU) | a at RGB tip (AU) | a final (AU) | a·M₀/M_f (AU) | fate |
|---|---|---|---|---|---|
| Mercury | 0.387 | 0.580 | 0.717 | 0.716 | engulfed by the red giant (even with mass loss alone) |
| Venus | 0.723 | 1.083 | 1.338 | 1.338 | engulfed by the red giant (even with mass loss alone) |
| Earth | 1.000 | 1.497 | 1.850 | 1.850 | engulfed 0.5 Myr before the tip (tides + drag; Schröder & Smith 2008) |
| Mars | 1.524 | 2.282 | 2.819 | 2.819 | survives |
| Jupiter | 5.203 | 7.782 | 9.621 | 9.626 | survives |
| Saturn | 9.555 | 14.304 | 17.554 | 17.678 | survives |
| Uranus | 19.218 | 28.964 | 35.428 | 35.556 | survives |
| Neptune | 30.110 | 44.826 | 56.116 | 55.708 | survives |

Largest deviation from the adiabatic prediction: 1.56 %. Eccentricities
stay within 0.0737 of their initial values: slow mass loss does not pump them.

| phase | age (Gyr) | L (L☉) | R (AU) | habitable zone (AU) | Earth T_eq (K) |
|---|---|---|---|---|---|
| ZAMS | 0.00 | 0.7 | 0.004 | 0.80–1.15 | 233 |
| present | 4.58 | 1 | 0.005 | 0.95–1.37 | 255 |
| MS: hottest | 7.13 | 1.26 | 0.005 | 1.07–1.54 | 270 |
| MS: final | 10.00 | 1.84 | 0.006 | 1.29–1.86 | 297 |
| RGB: tip | 12.17 | 2730 | 1.191 | 49.64–71.58 | 1843 |
| ZA-He | 12.17 | 53.7 | 0.052 | 6.96–10.04 | 690 |
| AGB: tip | 12.30 | 2090 | 0.693 | 43.43–62.63 | 1724 |
| AGB: tip-TP | 12.30 | 4170 | 0.833 | 61.35–88.47 | 2049 |

Timeline quoted from the paper: Earth is engulfed 7.59 ± 0.05 Gyr from now, 0.5 Myr before
the RGB tip, when the Sun still has 0.25 AU to grow; Venus 1.0 Myr and Mercury 3.8 Myr
earlier. After the AGB the Sun loses only ~0.01 M☉ in its last 30,000 yr and forms at most a
faint, short-lived shell rather than a classical planetary nebula.

## Limitations

- No tides, no drag, no planetary engulfment physics: our runs show mass loss alone. The
  engulfment statements are the paper's, which depend on the mass-loss parameter η
  (7–9 × 10⁻¹⁴ M☉/yr) and on the tidal-friction coefficient.
- Mass-loss ramps are shortened by a factor ~10 relative to reality to keep the run minutes
  long; the result does not depend on this as long as the ramp is adiabatic (it is).
- Giant-planet mutual perturbations over Gyr (secular chaos, Mercury's eccentricity
  excursions) are outside the scope of this short run.

## References

- Schröder, K.-P. & Connon Smith, R. 2008, MNRAS 386, 155, "Distant future of the Sun and
  Earth revisited", arXiv:0801.4031.
- Rein, H. & Liu, S.-F. 2012, A&A 537, A128 (REBOUND); Rein, H. & Spiegel, D. S. 2015,
  MNRAS 446, 1424 (IAS15).
