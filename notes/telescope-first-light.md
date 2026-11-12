# First light: our own telescope images of two dying stars (2026-11-10)

Requests made 2026-11-08 to MicroObservatory (Harvard-Smithsonian CfA, "Observing With NASA"); the e-mail with the
links arrived 2026-11-09 12:30. The same frames are public in the image
directory (https://waps.cfa.harvard.edu/microobservatory/MOImageDirectory/ImageDirectory.php), so they were fetched
from there: 16 FITS files in data/telescope/microobservatory/ (two nights, two telescopes). Reduction:
`-m skyimages.telescope` (skyimages/telescope.py). Results: research/telescope_results.json. Pictures:
../figures/telescope_{m27,m57}_{field,crop,annot}.png.

## Data

| target | frames used (UT 2026-11-09) | telescope | filters | exposure | altitude |
|---|---|---|---|---|---|
| M27 Dumbbell | DumbbellNebu261109025221 / 025656 / 025853 / 030315 | "Ben", Whipple Observatory, Amado AZ (6-inch) | R, G, B, clear | 60 s each | 53° |
| M57 Ring | RingNebulaM5261109023628 / 023927 / 024230 / 024532 | same | R, G, B, clear | 60 s each | 46° |

A second set from "Ed" (Cambridge MA, UT 2026-11-09 23:46 to 2026-11-10 00:11) has a sky 2-10 times brighter (city)
and was not used. The e-mail calls the fourth frame a dark calibration; the FITS header and the pixel statistics say
it is a clear-filter exposure, and we use it as luminance. The Moon request has not been taken (new Moon on
2026-11-09; the directory has no Moon frame after 2026-10-31... to re-check when the Moon is back in the evening sky).

## Reduction (what a professional pipeline does, in small)

1. Background: mesh model per frame (sep, 64-px boxes). No darks or flats exist, so hot pixels are found as pixels
   more than 6 sigma bright at the same detector position in the frames of both fields (1,160 pixels) and replaced by
   the local median.
2. Registration: each filter is shifted onto the clear frame by voting over star-centroid differences (shifts up to
   9 px between filters: the mount drifts). Phase correlation was tried first and failed on M27 (colour fringes).
3. Astrometry: Gaia DR3 stars from the ESA archive (TAP; the Harvard VizieR mirror timed out); vote over parity,
   rotation and scale, then an affine fit grown from bright to faint stars, then a TAN WCS with second-order
   distortion.
4. Photometry: 2.5-px apertures on the clear frame against Gaia G; forced aperture with a local annulus at the Gaia
   position of each central star.
5. Colour: filters scaled so the median star is white (gains R 0.5-0.7, B 3.5-4.1), clear frame as luminance,
   asinh stretch; shown north up (the detector is rotated 180°).

## Results

| quantity | M27 | M57 |
|---|---|---|
| stars detected / identified with Gaia DR3 | 1,604 / 1,493 | 1,244 / 1,162 |
| astrometric residual (median) | 0.9" | 0.6" |
| pixel scale measured (header says 5.00") | 5.19" | 5.19" |
| zero point (G = zp − 2.5 log counts), scatter, stars | 20.21, 0.10 mag, 458 | 20.21, 0.05 mag, 274 |
| 5-sigma limit | G ≈ 16.0 | G ≈ 16.4 |
| nebula: integrated magnitude (clear, on the G scale) | 7.3 (catalogue V 7.4-7.5) | 8.9 (catalogue V 8.8) |
| nebula: size at 20 % of peak | 5.9' × 6.0' (catalogue 8.0' × 5.6') | 1.5' × 1.3' (catalogue 1.4' × 1.0') |
| central star, Gaia DR3: G, BP−RP | 14.04, −0.54 | 15.65, −0.54 |
| central star distance (Gaia parallax) | 389 ± 6 pc = 1,269 ly | 788 ± 27 pc = 2,569 ly |
| central star absolute G | 6.09 | 6.16 |
| central star in our image | **detected, S/N 42, G ≈ 14.16** (0.12 mag from Gaia) | not detected (inside the ring's glow; 0.8 mag above our limit in clean sky) |
| filter fluxes of the nebula after white balance, R : G : B | 0.54 : 1 : 0.88 | 0.70 : 1 : 0.99 |

What the numbers say:
- We photographed a newborn white dwarf: the central star of M27 is in our 60-s clear frame at S/N 42, and our
  magnitude agrees with Gaia to 0.12 mag. Both central stars have the same absolute magnitude (G ≈ 6.1) and the same
  very blue colour: they sit above the top of the cooling sequence of our wdclock diagram (which starts near absolute
  G ≈ 8-10): the clock at zero.
- Distances from our own Gaia query agree with the published ones: 1,269 ly for M27 (NASA: "more than 1,200";
  SIMBAD 389 pc) and 2,569 ly for M57 (Gaia DR3 value quoted as 2,570 ± 90 ly; ESA/Webb: "roughly 2,500").
- The nebulae are green-teal with red edges in a white-balanced image: the green and blue filters catch the [O III]
  495.9/500.7 nm lines of doubly ionised oxygen from the hot interior, and the red rim is H-alpha and [N II] from
  the cooler outer gas (line identifications as given on the Ring Nebula Wikipedia page; NASA's Hubble captions use a
  different false-colour mapping). In M57 the ring is 17 pixels across and still shows the teal inside / red outside.
- The header pixel scale is wrong by 3.8 % (5.19", not 5.00"): a number we could only get by solving the astrometry.
- Integrated magnitudes within 0.1-0.2 mag of the catalogue values, from a single 60-s frame calibrated on Gaia stars.

## Limitations

- No dark, bias or flat frames: the background model absorbs gradients, vignetting is not corrected (zero-point
  scatter 0.05-0.10 mag is the price). 12-bit data, bright stars saturate (peak 4095) and bleed.
- Clear-filter magnitudes are tied to Gaia G without a colour term; emission-line objects (the nebulae) are not
  stars, so their "G-like" magnitudes are indicative.
- The M57 central star is undetected; the forced aperture is dominated by ring light.
- Single epoch: nothing here measures variability.

## What next with the telescope

1. Requests are free and take a day: build a list of targets where a 6-inch telescope and 60 s reach something
   relevant to us. With a limit of G ≈ 16 in clean sky: the brightest white dwarfs (Sirius B is too close to
   Sirius A; 40 Eri B at G 9.5 and van Maanen 2 at G 12.3 are easy if they are on the menu: the OWN menu is a fixed
   list, so only objects on it can be asked for), more planetary nebulae (Helix, Cat's Eye if offered), M4/NGC 6397
   (globular clusters with white-dwarf sequences far below our limit, as context).
2. Repeat M27 on several nights and stack: 10 frames gain 1.25 mag; a light curve of the central star at the
   0.03-mag level would be a real measurement (it is a known binary candidate in the literature: to check before
   saying anything).
3. Use the clear frames as a photometry exercise: 1,493 stars with Gaia matches per frame is a ready-made
   variable-star search field (compare two nights: we already have a second night from "Ed").
4. The Moon when it returns (first quarter around 2026-11-17).

Credit line for every use: "Image taken with the MicroObservatory robotic telescopes, Harvard-Smithsonian Center for
Astrophysics, Observing With NASA". Sources read 2026-11-10 (our reading): NASA Messier 27 and 57 pages,
ESA/Webb weic2320, Benedict et al. 2003 abstract (M27 central star: R = 0.055 ± 0.02 Rsun, "may be descending to the
white dwarf cooling track"), Wikipedia Dumbbell and Ring Nebula pages, MicroObservatory about page.
