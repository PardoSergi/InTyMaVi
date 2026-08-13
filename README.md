*This project was developed with the assistance of Anthropic's Claude AI and subsequently reviewed and maintained by the author.*

# InTyMaVi — Interactive Typological Map Visualiser

InTyMaVi is a single, self-contained HTML file for exploring linguistic-typological
data on an interactive map. Open the `.html` file in any modern browser — no
installation, server, or internet account is required. An internet connection is
only needed for the base map tiles and for the optional Glottolog/Grambank
features described below.

## Contents

- [1. Getting started](#1-getting-started)
- [2. Preparing your Excel file](#2-preparing-your-excel-file)
- [3. Importing your data](#3-importing-your-data)
- [4. Filling in missing coordinates from Glottolog](#4-filling-in-missing-coordinates-from-glottolog)
- [5. Adding context with Grambank](#5-adding-context-with-grambank)
- [6. Exploring the map](#6-exploring-the-map)
- [7. Downloading a map image](#7-downloading-a-map-image)
- [8. Saving and reusing a specific zoom/view](#8-saving-and-reusing-a-specific-zoomview)
- [9. Troubleshooting](#9-troubleshooting)
- [10. Data sources & attribution](#10-data-sources--attribution)

---

## 1. Getting started

Double-click the `.html` file (or open it from your browser with *File → Open*).
The map loads empty, with a **"📂 Load Excel"** prompt in the middle — click it,
or use the **"Update data"** button in the header, to import your first dataset.

## 2. Preparing your Excel file

InTyMaVi reads a single sheet (`.xlsx`/`.xls`) with one row per language/variety.
Column headers are matched flexibly — in **Catalan or English**, accents and
capitalisation are ignored:

| Purpose | Accepted header names |
|---|---|
| Language name (required) | `Llengua` / `Language` |
| Variety / dialect (optional) | `Varietat` / `Variety` |
| Latitude (decimal or DMS) | `Latitud` / `Latitude` |
| Longitude (decimal or DMS) | `Longitud` / `Longitude` |
| Family / classification | `Familia` / `Family` |

Coordinates can be plain decimal numbers (`41.38`) or degrees/minutes/seconds
with a cardinal letter (`41°23'N`).

**Any other column is treated as a typological variable** — its header becomes
the variable's name in the app, and each cell is one language's value for that
variable (e.g. `SVO`, `yes`/`no`, `prenominal`…). You can have as many variable
columns as you like; you'll choose which one to visualise from a dropdown once
the file is loaded.

> 💡 If you want a variable column to later merge automatically with Grambank
> data (see §5), name it **exactly like the Grambank code**, e.g. `GB130`.

## 3. Importing your data

Click **"Update data"** in the header (or the "📂 Load Excel" prompt on an empty
map) and drag your file into the drop zone, or click it to browse. Importing a
new file **replaces** the map's current data. A short status message confirms
how many varieties and variables were loaded, or explains what went wrong
(missing language column, no variable columns found, etc.).

## 4. Filling in missing coordinates from Glottolog

Not every dataset comes with coordinates for every language. In the same
"Update data" window there's an optional second drop zone, **"Coordinates
fallback"**, where you can load a Glottolog geographic file — typically
[`languages_and_dialects_geo.csv`](https://glottolog.org/meta/downloads),
which lists `name`, `latitude`, `longitude` for every Glottolog languoid.

Rules:
- If a row in your Excel file **already has valid coordinates**, they are
  always used — Glottolog is never consulted for that row.
- If coordinates are **missing or unreadable**, InTyMaVi looks up the language
  by name (accents/case ignored) in the Glottolog file and uses its
  coordinates instead. Language-level entries are preferred over dialects
  when a name is ambiguous.
- You can load the Excel file and the Glottolog file **in either order** — the
  app re-resolves coordinates automatically each time either one changes.
- Languages located this way show a small **"Glottolog"** badge in their map
  popup and in the language-list detail panel, so you always know which
  points are your own data and which were filled in.
- Use **"Remove Glottolog file"** to drop the fallback file and recompute with
  only your Excel's own coordinates.

## 5. Adding context with Grambank

The **"🌐 Grambank"** button lets you pull in real grammatical data from the
[Grambank](https://grambank.clld.org) database (195 features, ~2,400
languages) to put your own sample in a broader typological context — no
manual download needed.

1. Click **"🌐 Grambank"**. The app fetches Grambank's feature list once per
   session (small files, a few seconds).
2. **Search** for a feature by keyword or code (`word order`, `article`,
   `GB130`…) and **check** any number of features you want.
3. Optionally **restrict by family** (comma-separated, e.g. `Indo-European,
   Austronesian`) to avoid cluttering the map with unrelated languages.
4. Click **"Download & import"**. The first time, this downloads Grambank's
   full value table (~50 MB — a progress bar is shown); afterwards it's cached
   in memory for the rest of the session.

**How it combines with your own data:**
- If a selected Grambank code matches an **existing column name** in your
  loaded Excel exactly (e.g. your column is called `GB130`), the Grambank
  checklist shows a **"↔ merges into…"** tag, and the imported values are
  merged into that **same column** — your own languages and Grambank's
  worldwide sample appear together, colour-coded under the same variable.
- If there's no matching column, the feature is added as a **new column**
  instead (still useful for context, just not merged into an existing one).
- **Your data is never duplicated or overwritten.** Languages you already have
  (matched by name) are left exactly as they are; Grambank only *adds*
  languages you don't already have. Added points carry a **"Grambank"** badge
  in their popup and detail panel.
- If no data is loaded yet, Grambank becomes the map's dataset directly —
  handy for exploring Grambank on its own.

Note: matching is based on the **column name being exactly a Grambank code**
(e.g. `GB130`), not on the values themselves — if your own coding scheme uses
different category labels than Grambank's, both will appear as separate
categories in the legend for that variable.

## 6. Exploring the map

- **Variable to display** — the dropdown selects which imported column colours
  the markers, with a matching legend.
- **"+ Correlation" / Cross with** — colour markers by the *combination* of two
  variables at once, to explore co-occurrence patterns.
- Click a legend entry to **filter** the map to only that value (click again,
  or **"✕ Clear selection"**, to reset); you can also change each value's
  marker **shape** from the legend.
- The **search box** filters the language list by name.
- Click any marker, or any row in the language list, to see its full detail
  panel (all variables, family classification, and coordinate/data-source
  notes).

## 7. Downloading a map image

The **download button** in the header opens **"Map download options"**, where
you choose:
- Zoom level (coarse selector + a fine adjustment slider) and pan/focus,
- Aspect ratio,
- Icon and legend size,
- Legend position (four corners, or none — for adding one manually elsewhere).

A live preview updates as you change these. Click **"Download"** to generate
and save the PNG. Your choices are remembered automatically for next time.

## 8. Saving and reusing a specific zoom/view

If you're exporting several maps (e.g. one per variable, for a paper or
presentation) and want them all at **exactly the same zoom, framing, and
legend layout**, use:

- **💾 "Save view settings…"** — downloads a small `.json` file capturing the
  current zoom, pan, aspect ratio, icon size, and legend position.
- **📂 "Load view settings…"** — loads that file back and immediately applies
  it to the modal and preview.

This file is portable — you can reuse it later, on a different computer or
browser, so that unrelated map exports stay visually consistent. Loading a
file also becomes the new "remembered" default for subsequent downloads in
that browser.

## 9. Troubleshooting

- **"No valid rows found"** on import — check that your language-name column
  is present and that at least one row has readable coordinates (or a
  Glottolog fallback file that covers it).
- **Grambank download feels slow** — the full value table is ~50 MB and is
  only fetched once per browser session; after that, selecting more features
  is instant.
- **Two categories that should be the same appear separately in the legend**
  after a Grambank merge — your Excel's own value labels for that column
  don't match Grambank's wording exactly (e.g. `SOV` vs `SV`); you'll need to
  align your category labels manually if you want a single merged legend.
- InTyMaVi needs an internet connection for the base map tiles, the Glottolog
  file (if you choose to fetch one online rather than loading a local file),
  and the Grambank features — everything else works fully offline.

## 10. Data sources & attribution

InTyMaVi itself doesn't ship with any linguistic data — you bring your own —
but two optional, built-in features fetch and display data from external
databases: the **Glottolog coordinate fallback** (§4) and the **Grambank
import** (§5). Both are distributed under the **Creative Commons Attribution
4.0 International licence (CC BY 4.0)**, which requires attribution whenever
their data is used or redistributed — including here. If you publish, share,
or redistribute InTyMaVi (e.g. on GitHub) with these features enabled, please
keep this section intact, or otherwise credit both projects visibly in your
own copy.

### Grambank

Grambank's own citation guidance asks that **both** the release paper **and**
the dataset release (for the specific version used) be cited:

>Skirgård, Hedvig, Hannah J. Haynie, Damián E. Blasi, Harald Hammarström, Jeremy Collins, Jay J. Latarche, Jakob Lesage, Tobias Weber, Alena Witzlack-Makarevich, Sam Passmore, Angela Chira, Luke Maurits, Russell Dinnage, Michael Dunn, Ger Reesink, Ruth Singer, Claire Bowern, Patience Epps, Jane Hill, Outi Vesakoski, Martine Robbeets, Noor Karolin Abbas, Daniel Auer, Nancy A. Bakker, Giulia Barbos, Robert D. Borges, Swintha Danielsen, Luise Dorenbusch, Ella Dorn, John Elliott, Giada Falcone, Jana Fischer, Yustinus Ghanggo Ate, Hannah Gibson, Hans-Philipp Göbel, Jemima A. Goodall, Victoria Gruner, Andrew Harvey, Rebekah Hayes, Leonard Heer, Roberto E. Herrera Miranda, Nataliia Hübler, Biu Huntington-Rainey, Jessica K. Ivani, Marilen Johns, Erika Just, Eri Kashima, Carolina Kipf, Janina V. Klingenberg, Nikita König, Aikaterina Koti, Richard G. A. Kowalik, Olga Krasnoukhova, Nora L.M. Lindvall, Mandy Lorenzen, Hannah Lutzenberger, Tônia R.A. Martins, Celia Mata German, Suzanne van der Meer, Jaime Montoya Samamé, Michael Müller, Saliha Muradoglu, Kelsey Neely, Johanna Nickel, Miina Norvik, Cheryl Akinyi Oluoch, Jesse Peacock, India O.C. Pearey, Naomi Peck, Stephanie Petit, Sören Pieper, Mariana Poblete, Daniel Prestipino, Linda Raabe, Amna Raja, Janis Reimringer, Sydney C. Rey, Julia Rizaew, Eloisa Ruppert, Kim K. Salmon, Jill Sammet, Rhiannon Schembri, Lars Schlabbach, Frederick W.P. Schmidt, Amalia Skilton, Wikaliler Daniel Smith, Hilário de Sousa, Kristin Sverredal, Daniel Valle, Javier Vera, Judith Voß, Tim Witte, Henry Wu, Stephanie Yam, Jingting Ye 葉婧婷, Maisie Yong, Tessa Yuditha, Roberto Zariquiey, Robert Forkel, Nicholas Evans, Stephen C. Levinson, Martin Haspelmath, Simon J. Greenhill, Quentin D. Atkinson & Russell D. Gray (2023).
> *Grambank reveals the importance of genealogical constraints on linguistic
> diversity and highlights the impact of language loss.* Science Advances,
> 9(16), eadg6175. https://doi.org/10.1126/sciadv.adg6175
>
> Skirgård, Hedvig, Hannah J. Haynie, Harald Hammarström, Damián E. Blasi, Jeremy Collins, Jay Latarche, Jakob Lesage, Tobias Weber, Alena Witzlack-Makarevich, Michael Dunn, Ger Reesink, Ruth Singer, Claire Bowern, Patience Epps, Jane Hill, Outi Vesakoski, Noor Karolin Abbas, Sunny Ananth, Daniel Auer, Nancy A. Bakker, Giulia Barbos, Anina Bolls, Robert D. Borges, Mitchell Browen, Lennart Chevallier, Swintha Danielsen, Sinoël Dohlen, Luise Dorenbusch, Ella Dorn, Marie Duhamel, Farah El Haj Ali, John Elliott, Giada Falcone, Anna-Maria Fehn, Jana Fischer, Yustinus Ghanggo Ate, Hannah Gibson, Hans-Philipp Göbel, Jemima A. Goodall, Victoria Gruner, Andrew Harvey, Rebekah Hayes, Leonard Heer, Roberto E. Herrera Miranda, Nataliia Hübler, Biu H. Huntington-Rainey, Guglielmo Inglese, Jessica K. Ivani, Marilen Johns, Erika Just, Ivan Kapitonov, Eri Kashima, Carolina Kipf, Janina V. Klingenberg, Nikita König, Aikaterina Koti, Richard G. A. Kowalik, Olga Krasnoukhova, Kate Lynn Lindsey, Nora L. M. Lindvall, Mandy Lorenzen, Hannah Lutzenberger, Alexandra Marley, Tânia R. A. Martins, Celia Mata German, Suzanne van der Meer, Jaime Montoya, Michael Müller, Saliha Muradoglu, HunterGatherer, David Nash, Kelsey Neely, Johanna Nickel, Miina Norvik, Bruno Olsson, Cheryl Akinyi Oluoch, David Osgarby, Jesse Peacock, India O.C. Pearey, Naomi Peck, Jana Peter, Stephanie Petit, Sören Pieper, Mariana Poblete, Daniel Prestipino, Linda Raabe, Amna Raja, Janis Reimringer, Sydney C. Rey, Julia Rizaew, Eloisa Ruppert, Kim K. Salmon, Jill Sammet, Rhiannon Schembri, Lars Schlabbach, Frederick W. P. Schmidt, Dineke Schokkin, Jeff Siegel, Amalia Skilton, Hilário de Sousa, Kristin Sverredal, Daniel Valle, Javier Vera, Judith Voß, Daniel Wikalier Smith, Tim Witte, Henry Wu, Stephanie Yam, Jingting Ye 葉婧婷, Maisie Yong, Tessa Yuditha, Roberto Zariquiey, Robert Forkel, Nicholas Evans, Stephen C. Levinson, Martin Haspelmath, Simon J. Greenhill, Quentin D. Atkinson & Russell D. Gray (2023). Grambank v1.0 (v1.0) [Data set]. Zenodo. https://doi.org/10.5281/zenodo.7740140

- Website: <https://grambank.clld.org>
- Full citation instructions: <https://github.com/grambank/grambank/wiki/Citing-grambank>
- Licence: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)
- The Zenodo DOI above is the **concept DOI**, which always resolves to the
  latest release; since InTyMaVi fetches directly from the `grambank/grambank`
  GitHub repository's `master` branch, the exact version can change over
  time. If you're citing a specific analysis made with InTyMaVi, check the
  version-specific DOI shown on the Zenodo page at the time you used the app.
- Grambank is part of [Glottobank](https://glottobank.org), a joint
  initiative of the Max Planck Institute for Evolutionary Anthropology, the
  Australian National University, Yale University, and many collaborating
  institutions worldwide.

### Glottolog

> Hammarström, Harald & Forkel, Robert & Haspelmath, Martin & Bank,
> Sebastian. 2026. *Glottolog 5.3*. Leipzig: Max Planck Institute for Evolutionary
> Anthropology. https://doi.org/10.5281/zenodo.18840935
(Available online at http://glottolog.org)

- Licence: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)
- Glottolog is versioned; if you cite a specific analysis made with InTyMaVi,
  note the version/date of the `languages_and_dialects_geo.csv` file you
  loaded (shown on the [Glottolog downloads page](https://glottolog.org/meta/downloads)).
