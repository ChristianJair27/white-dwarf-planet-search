# Roadmap (28 November 2026)

What we are doing now and what comes next, ranked by scientific value. Status: [run] in progress, [next] ready to
start, [idea] needs a resource or a decision.

## In progress

- [done 2026-11-20] **Injection-recovery:** 304 transit models injected into raw TESS 20-s light curves of 16 white
  dwarfs and run through the full search; 50 % recovery at 0.26–1.08 Earth radii from G 13.5 to 16.5
  ([report](reports/2026-11-20-injection-recovery.md)). Next: more test stars, and noisy, single-sector and
  120-s-only targets.
- [run] **The transit survey of the TESS-bright sample (G < 17) is in its last few hundred stars.** When it ends,
  the final counts and the completeness map go into the injection-recovery note.
- [done 2026-11-24] **Vetting fixes:** per-star physical duration limit with a 4-min to 4-h box scan, a shared-period
  veto and verdicts written back automatically ([report](reports/2026-11-24-pipeline-fixes.md)).
- [done 2026-11-28] **Survey robustness:** a watchdog restarts the survey if an archive read hangs, and a sector
  with no usable cadences no longer costs the whole star.
- [run] **Infrared-excess candidates, expert checks:** CatWISE proper motions against Gaia, background galaxies in
  the WISE beam, and ~1″ near-infrared imaging, as recommended by a specialist in dusty white dwarfs.
- [done 2026-11-12] **Pulsating white dwarfs in TESS 20-s data** ([report](reports/2026-11-12-zzceti-search.md)).
- [done] **Machine-learning repositories on NASA data:**
  [exoplanet-cnn](https://github.com/ChristianJair27/exoplanet-cnn) and
  [mars-terrain-seg](https://github.com/ChristianJair27/mars-terrain-seg).

## Next, ranked

1. [draft 2026-11-20] **A short research note from the injection-recovery map:** "How small a planet can TESS find
   around a nearby white dwarf?" Draft in [papers/2026-injection-recovery](papers/2026-injection-recovery/).
2. [ready 2026-11-24] **Gaia DR4 (expected 2 December 2026).** Code for epoch photometry, epoch astrometry and
   variability is written and self-tested; it waits for the data
   ([report](reports/2026-11-24-pipeline-fixes.md), section 6). Epoch astrometry: a Jupiter on a 3-yr orbit would
   displace 379 of the 16,676 white dwarfs by more than 100 micro-arcseconds; whether that is detectable depends on
   the DR4 per-epoch errors, which we will measure before promising anything. Epoch photometry: eclipses and debris
   dips need at least three in-transit epochs from different visits.
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
