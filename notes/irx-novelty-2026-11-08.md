# IR-excess novelty check against Wang+2026, Hogg+2020 and Girven+2011 (2026-11-08)

Read-only literature check. Downloads (arXiv source tarballs, PDFs, HTML, VizieR TSV)
are in `data/irx/lit/wang2026_src/` and were treated as untrusted data (parsed with
`python -I` from the scratchpad; nothing executed).

**Resumen (ES).** De nuestros cinco objetos, solo WDJ074231.99+285727.43
(Gaia DR3 878635723331279360) aparece en Wang+2026: esta en su Tabla 3 ("WD + BD or
dust disk candidates", los 24 ambiguos), marcado como ya reportado por Girven+2011.
No es nuevo. Los otros cuatro (WDJ0332-1743, WDJ0803+1633, WDJ1639+1036, WDJ1207-0754)
no estan en ninguna de las cuatro tablas de candidatos (139 filas; ni por Gaia ID ni
por posicion a 30"). Hogg+2020 tomo un espectro optico de J0742+2857 y concluye que la
compañera es una enana M5-M6, no una L6, y que la WD es mucho mas caliente (31 926 K)
que el ajuste fotometrico de Girven (9000 K). Girven+2011 lo lista en su tabla de
exceso IR (`ire`) como DA:ire con compañera fotometrica L6.

## 1. Wang, Liu, Xu, Rebassa-Mansergas 2026, ApJ 1001, 81 — arXiv:2603.10481

- arXiv id confirmed via API: https://export.arxiv.org/api/query?search_query=ti:%22White%20Dwarfs%20with%20Infrared%20Excess%20from%20LAMOST%22&max_results=5
  -> `http://arxiv.org/abs/2603.10481v1`, "White Dwarfs with Infrared Excess from LAMOST
  Data Release 11", authors Keyi Wang, Qiong Liu, Siyi Xu, Alberto Rebassa-Mansergas,
  comment "19 pages, 8 figures, 4 tables, accepted for publication in ApJ".
- Sources used: LaTeX source https://arxiv.org/src/2603.10481 (file `LAMOST_DR_11.tex`),
  HTML https://arxiv.org/html/2603.10481v1, PDF https://arxiv.org/pdf/2603.10481v1.
- The LaTeX source holds the four candidate tables inline (no separate machine-readable
  file). Parsed 139 rows: 30 "WD+M Dwarf Binary Candidates", 19 "WD + BD Binary
  Candidates", 24 "WD + BD or dust disk candidates", 66 "WD+Dust disk Candidates".
  Columns: obsid, R.A., Decl., Gaia ID, G, Type, Teff, logg, Mass, Age, D, + model fits.
  Identifiers are LAMOST obsid + Gaia DR3 source_id + decimal coordinates (no SDSS/WDJ
  names). The 23 sources excluded for contamination within 6" and the 5 excluded by
  WISE cc_flags are NOT listed individually anywhere in the paper.

### Match results (by Gaia DR3 id and by position, all 139 rows)

| Our object | Gaia DR3 | In Wang+2026? |
|---|---|---|
| 1. WDJ074231.99+285727.43 | 878635723331279360 | YES — Table 3 "WD + BD or dust disk candidates", 0.86" from our position, Gaia id identical |
| 2. WDJ033256.37-174323.78 | 5102511204522388736 | No (no Gaia id, nothing within 30") |
| 3. WDJ080323.85+163357.90 | 655245124121246720 | No |
| 4. WDJ163917.47+103604.84 | 4447039585308297088 | No |
| 5. WDJ120726.77-075444.26 | 3594474519618208256 | No |

Objects 2-5 also do not appear anywhere else in the full text (grep of tex and HTML for
their Gaia ids). Note the LAMOST footprint is Dec > about -10 deg, so objects 2 and 5
(Dec -17.7 and -7.9) are unlikely to be in the parent sample anyway; the paper does not
publish the 1818-object parent sample.

### Object 1 verbatim (LaTeX source, `LAMOST_DR_11.tex` line 447; HTML table cell ids S5.T3.5.23.*)

Table caption: `\caption{WD + BD or dust disk candidates}` (`\label{tab:WD+BD_or_dust}`).
Header: `obsid & R.A. & Decl. & Gaia ID & G & Type & $T_{\rm eff}$ & $\log g$ & Mass & Age & D & Blackbody Model (T_eff(BB), chi2_dust) & Companion Model (T_eff(BT), chi2_comp)`.

Row, verbatim:

```
811913219$^c$ & 115.6331 & 28.9577 & 878635723331279360 & 17.66 & DA & 7843 & 8.19 & 0.713 & 1.5582 & 97.75 & 2000 & 1.7 & 1500 & 1.8 \\
```

Footnotes of that table, verbatim:

```
$^a$ Reported by \citet{2023ApJ...944...23W}. \\
$^b$ Reported by \citet{2011ApJS..197...38D}.\\
$^c$ Reported by \citet{2011MNRAS.417.1210G}.\\
$^s$ indicates that the IR excess in the WISE bands may not be real.
```

So Wang+2026 flag it with `c` = already reported by Girven et al. 2011 (not one of their
19 "new" ambiguous systems), and it does NOT carry the `s` flag (they consider the WISE
excess real). Their fits: blackbody T_BB = 2000 K (chi2 1.7) vs BT-Settl companion
T = 1500 K (chi2 1.8) — degenerate, hence the "BD or dust" bin. Their WD parameters
(LAMOST): Teff 7843 K, logg 8.19, 0.713 Msun, cooling age 1.56 Gyr, d = 97.75 pc.

Text about this table (tex line ~460, verbatim): "We compiled a total of 24 WD+BD or
WD+dust disk candidates in Table ~\ref{tab:WD+BD_or_dust}, of which 19 are newly
discovered. These sources exhibit IR excess with blackbody temperatures between 1200 K
and 2100 K, and their SEDs are similarly well-fitted by both the companion and the
blackbody disk models."

The obsid 811913219 is not discussed individually anywhere else in the text (only the
table row). URL for the HTML row: https://arxiv.org/html/2603.10481v1 (Table 3, row
with Gaia ID 878635723331279360).

## 2. Hogg et al. 2020, MNRAS 498, 12 — arXiv:2007.15389

- arXiv id via API: https://export.arxiv.org/api/query?search_query=ti:%22Confirming%20new%20white%20dwarf%22%20AND%20ti:%22ultracool%22&max_results=5
  -> `http://arxiv.org/abs/2007.15389v1`, DOI 10.1093/mnras/staa2233.
- Source read: https://arxiv.org/src/2007.15389 (`main.tex`); PDF https://arxiv.org/pdf/2007.15389v1.
- The paper never uses the GALEX name or a Gaia id; the object appears as
  SDSS J074231.98+285727.3 (same SDSS source; our WDJ074231.99+285727.43 is 0.8" away).
  It IS one of their candidates: one of the Girven+2011 photometric WD+L candidates for
  which they obtained an optical (GTC/OSIRIS, 2015-03-17, 900 s) spectrum.

Verbatim quotes from `main.tex`:

Table 1 (literature values, ref 1 = Girven et al. 2011):
```
SDSS\,J074231.98$+$285727.3 & 07:42:31.98 & +28:57:27.3 & DA & 9\,000 & 7.25 & L6 & 1 \\
```

Results table (FITSB2 fit, "ten newly confirmed DA white dwarfs"):
```
SDSS\,J074231.98$+$285727.3 & 31\,926 $\pm$300 &7.21 $\pm$0.07 &0.403 $\pm$0.023&0.0187 $\pm$ $9\times10^{-4}$&18 $\pm$1&DA \\
```
(Teff 31 926 +/- 300 K, logg 7.21 +/- 0.07, 0.403 Msun, R 0.0187 Rsun, t_cool 18 +/- 1 Myr.)

Section "SDSS074231.98+285727.3", verbatim:

> "Our fit to the optical spectrum of this object gave a temperature of ~31 000 K,
> however, the photometric fit from Girven et al. (2011) predicted a 9 000 K temperature.
> The $i$ and $z$ bands are consistent with an M4 or M5 while the $YJHK$ bands are more
> indicative of the M5.5 or M6 template. A similar situation was highlighted by Tremblay
> & Bergeron (2011) where some objects in their survey had a mismatch between the
> photometric derived temperature and spectroscopically derived temperature, in some
> cases by as much as 70 per cent. They determined that if the white dwarf is magnetic
> or part of an unresolved double degenerate binary, it is possible to cause a systematic
> positive offset between the spectroscopic and photometric temperatures. It is also
> possible that a significant reflection effect may be present from the the M dwarf
> companion due to the high temperature white dwarf if it is part of a close binary,
> causing the discrepancy in spectral type."

Figure caption, verbatim: "OSIRIS spectrum of SDSS074231.98+285727.3 with the photometry
and the combined spectra of the white dwarf model and M5, M5.5 and M6 template spectra
for comparison. The data suggest that the companion is a mid-M dwarf with a spectral
type between M5-M6, although the photometry do not fit one specific spectral type."

Comparison table (Table "comparison"):
```
SDSS\,J074231.98$+$285727.3 & 31\,926 $\pm$300 & 9\,000 & M5$-$M6 & L6& Phot & 1\\
```
i.e. their companion type M5-M6 (from photometry, "Phot") vs literature L6.

Conclusion of Hogg+2020 for this object: WD confirmed as a hot DA (~32 kK, low mass
0.40 Msun), the near-IR excess is real and due to a mid-M dwarf (M5-M6) companion, not
an L dwarf. They do not establish whether it is a close binary ("Radial velocity follow
up is required").

## 3. Girven et al. 2011, MNRAS 417, 1210 — VizieR J/MNRAS/417/1210

Query: https://vizier.cfa.harvard.edu/viz-bin/asu-tsv?-source=J/MNRAS/417/1210&-c=115.633066+28.957464&-c.rs=5&-out.all
(saved as `data/irx/lit/wang2026_src/girven_vizier.tsv`). Two of the four sub-tables
return a row:

- `J/MNRAS/417/1210/spec` ("SDSS DR7 spectroscopic white dwarfs"), _r = 0.785":
  `J074231.98+285727.3`, RA 115.633258 Dec +28.957603, u=18.167 g=17.686 r=17.702
  i=17.766 z=17.877, UKIDSS Y=17.432 J=17.321 H=17.088 K=16.883, pmRA -40.68 pmDE -36.12,
  Teff 8500 +250/-130 K, logg 8.00 (fixed).
- `J/MNRAS/417/1210/ire` ("SDSS DR7 & UKIDSS DR8 IR excess candidates"), _r = 0.885":
  `J074231.98+285727.3`, Name `0742+2857`, photometric fit Teffp = 9000 +120/-50 K,
  loggp 7.25 +0.28/-0.12, Distp 86 +12/-0 pc, Sp.p (photometric companion type) = `L6`,
  Notes = `DA:ire`, Note.s/Note.p empty, clSDSS/clEIS/clSim empty, spectroscopic
  companion fit empty; WISE W1 16.52 +/- 0.12, W2 16.53 +/- 0.39, W3 12.58, W4 8.65
  (no errors on W3/W4 = non-detections/upper limits); SimbadName SDSS J074231.98+285727.3.
- Not in `phot` or `posqso` tables.

So YES: the object is in Girven+2011's IR-excess table, flagged `DA:ire` with a
photometric L6 companion.

## Bottom line

- WDJ074231.99+285727.43: NOT novel. IR excess known since Girven+2011 (L6 photometric
  companion), followed up spectroscopically by Hogg+2020 (hot DA + M5-M6 companion),
  and re-listed by Wang+2026 as a "BD or dust" candidate with flag c (previously
  reported). The three papers disagree on the WD Teff (8500-9000 K photometric vs
  31 926 K spectroscopic vs 7843 K LAMOST), which is itself a hint of a composite /
  reflection-affected SED. Treat as `known` in targets.csv.
- WDJ033256.37-174323.78, WDJ080323.85+163357.90, WDJ163917.47+103604.84,
  WDJ120726.77-075444.26: absent from all 139 Wang+2026 candidate rows (Gaia id and
  30" position). Wang+2026 does not constrain their novelty further (parent sample not
  published; two are outside the LAMOST footprint).

## Addendum (same night)

- Debes+ 2011 WIRED (VizieR J/ApJS/197/38, mirror): 9 of our 113 candidates are in the 1,527-object WIRED sample; of
  the unpublished ones only WDJ111424.68+334124.39 (the known DA+M LP 264-22) sits in an excess table (table 6).
  WDJ033256.37-174323.78, WDJ080323.85+163357.90, WDJ163917.47+103604.84 and WDJ120726.77-075444.26 are not in WIRED.
- Girven+ 2011 (`ire`, 153 rows) and Wang+ 2026 (123 of 139 rows parsed from the LaTeX; 16 rows in another format
  not parsed) and Debes+ 2011 (163 excess rows with coordinates) are now in `wdplanets.irx crossmatch`.
- Not available on the Harvard mirror (0 tables): Hoard+ 2013 (J/ApJ/770/21), Barber+ 2014 (J/ApJ/786/77),
  Rebassa-Mansergas+ 2019 (J/MNRAS/482/3656), Dennihy+ 2020 (J/ApJ/905/5), Steele+ 2011 (J/MNRAS/416/2768). Their
  samples are SDSS/Gaia-bright (G < 17) or Spitzer-targeted, so our G 18.5-19.9 candidates are unlikely to be in
  them, but this is an inference, not a check.
- Status of the three clean candidates after this night: no individual study found (SIMBAD bibliography titles read,
  arXiv API by Gaia id and J-names, eight excess lists). "Not previously reported as an infrared-excess candidate, to
  the extent of the lists above" is the honest wording.
