# Roadmap (12 November 2026)

What we are doing now and what comes next, ranked by scientific value. Status: [run] in progress, [next] ready to
start, [idea] needs a resource or a decision.

## In progress

- [run] **Injection-recovery:** TESS completeness for planets around the 100 pc white dwarfs, with transit models
  injected into raw light curves and run through the full search. Without it a null result has no sensitivity.
- [run] **Pulsating white dwarfs in TESS 20-s data:** a search for ZZ Ceti (DAV) pulsators among the hydrogen white
  dwarfs inside the instability strip, starting with a literature check of the published TESS pulsator searches.
- [run] **Machine-learning repositories on NASA data:** an AstroNet/ExoMiner-style transit classifier on Kepler
  DR24 and a Mars terrain segmentation model on AI4Mars, to be published as separate repositories.

## Next, ranked

1. [next] **A short research note from the injection-recovery map:** "How small a planet can TESS find around a
   nearby white dwarf?" Our own survey plus its completeness is a citable, checkable product.
2. [next] **Gaia DR4 readiness (DR4 is expected on 2 December 2026).** DR4 publishes epoch astrometry. A giant planet
   a few au from a white dwarf at 20 pc moves the star by tens to hundreds of micro-arcseconds; the detectable scale
   has to be computed star by star before we promise anything. Plan: an astrometric-signal simulator for the 100 pc
   sample (wobble against planet mass and period, using our cooling ages and survival limits), a fitter for epoch
   data, and a test on the DR3 non-single-star solutions. Literature check first (Gaia exoplanet yield predictions,
   DR4 documentation).
3. [next] **The survey pipeline as a package:** stacked BLS for minute-long transits, 20-s data, validation on
   WD 1856+534 b, and the completeness map, packaged and tested. General transit tools (lightkurve, TLS, wotan) are
   not tuned for white dwarfs, where transits last minutes.
4. [next] **A vetting classifier for our own survey:** the transit-classifier architecture trained on our injections
   (positives) and our vetted false positives, so new survey signals get a score.
5. [idea] **When do the nearest dead stars come closest, and how long would it take to reach them:** Gaia positions,
   proper motions and radial velocities for the 100 pc white dwarfs; closest-approach epochs; travel times for
   chemical, nuclear-electric, solar-sail and laser-sail propulsion with the relativistic rocket equation.
6. [idea] **Telescope time beyond MicroObservatory** (limit G ≈ 16 in 60 s): Las Cumbres Observatory Global Sky
   Partners and AAVSOnet give time to education and citizen projects by application. Targets: our infrared-excess
   white dwarfs, any pulsator candidate (a time series confirms pulsation), and survey candidates that need a second
   instrument.
