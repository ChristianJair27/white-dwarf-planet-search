# Infrared excess, first pass (2026-10-29)

Code: `python -m wdplanets.irx fetch` then `python -m wdplanets.irx excess` (wdplanets/irx.py).
Data: NOIRLab Astro Data Lab, `ls_dr11.tractor` joined to our Gaia DR3 IDs through
`ls_dr11.x1p5__tractor__gaia_dr3__gaia_source`; anonymous queries, 34 batches, 34 s.
Outputs: data/irx/ls_dr11_100pc.csv, data/irx/irx_first_pass.csv, ../figures/irx_first_pass.png.
Literature context: research/notes/ir-excess-literature.md.

## Numbers

- 12,477 of 16,676 WDs (74.8 %) have a DR11 Tractor source; every match is the
  Gaia-anchored source itself (ref_id == Gaia source_id for all 12,477).
- W1 S/N > 5: 11,569.
- "Clean" for this pass: brick_primary, wisemask_w1 = 0, fracflux_w1 < 1 (neighbours add
  less flux than the WD itself), rchisq_w1 < 5 or S/N > 100, S/N(W1) > 5, z and BP-RP present:
  6,451 WDs.
- Method: empirical locus. In 0.05-mag bins of Gaia BP-RP, the running median and MAD-sigma
  of z-W1 and z-W2 over the clean set (bins with >= 15 stars); chi = (colour - median) /
  sqrt(sigma_int^2 + errors^2). Candidate = clean and chi > 3 in both W1 and W2, S/N(W2) > 3.
- **128 candidates (1.98 % of the clean set)**; 51 have fracflux_w1 > 0.3 (blend risk),
  20 have BP-RP >= 0.86 (outside the colour range analysed by Murillo-Ojeda+ 2026), 50 have G > 18.
- Sanity checks: the known dusty WDs G 29-38 (WDJ232847.64+051454.24) and PG 1015+161
  (WDJ101803.83+155158.57) are both recovered. G 29-38 was first lost to the rchisq cut
  (rchisq_w1 = 2945 at S/N 884, a PSF-model mismatch at high S/N), hence the S/N > 100 exception.
  Other known disks I tried were outside the 100 pc sample or I had their coordinates wrong;
  a proper recovery test needs the published tables (Xu+ 2020, Lai+ 2021) from VizieR.

## Limitations (this is not a candidate list yet)

- The rate (1.98 %) matches the expected disk + companion occurrence, which is reassuring
  but says nothing about individual objects.
- Empirical locus, not model atmospheres: a WD whose colour bin is dominated by excess
  stars would bias the median; magnetic/DQ/He-atmosphere WDs can sit off the locus.
- No near-IR (J, H, K) yet, so disks and brown-dwarf companions are not separated.
- No image inspection yet; the WISE beam is ~6", and a third of literature excesses
  failed image vetting.
- Not yet cross-matched with published candidates: CDS/VizieR was unreachable on
  2026-10-29, so novelty is unknown.

## Next

1. When CDS is back: pull Xu+ 2020, Lai+ 2021, Madurga Favieres+ 2024, Murillo-Ojeda+ 2026
   tables; mark each of the 128 as known / new; measure our recovery of their confirmed disks.
2. Image vetting of every candidate (Legacy Survey viewer cutouts g/r/z + unWISE W1, Aladin Lite).
3. Near-IR from Data Lab (VHS, UKIDSS, 2MASS) to split disks from companions.
4. W1/W2 light curves (`ls_dr11.wise`, up to 25 epochs) for the survivors.
