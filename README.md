*This project was fully AI-assisted (vibe-coded) and is subsequently reviewed and maintained by the author.*

You can also use InTyMaVi directly in your browser, **no download needed**!
→ https://pardosergi.github.io/InTyMaVi/

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
- [10. Acknowledgements](#10-acknowledgements)

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
| Latitude (optional, see §4) | `Latitud` / `Latitude` |
| Longitude (optional, see §4) | `Longitud` / `Longitude` |
| Family / classification | `Família` / `Family` |

Coordinates can be plain decimal numbers (`41.38`) or degrees/minutes/seconds
with a cardinal letter (`41°23'N`).

**Any other column is treated as a typological variable** — its header becomes
the variable's name in the app, and each cell is one language's value for that
variable (e.g. `SVO`, `yes`/`no`, `prenominal`…). You can have as many variable
columns as you like; you'll choose which one to visualise from a dropdown once
the file is loaded.

You may also use the **EXAMPLE SPREADSHEET** as a template.

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

The **"🌐 Grambank"** button lets you pull in grammatical data from the
[Grambank](https://grambank.clld.org) database (195 features, ~2,400
languages) to put your own sample in a broader typological context.

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
  instead.
- **Your data is never duplicated or overwritten.** Languages you already have
  (matched by name) are left exactly as they are; Grambank only *adds*
  languages you don't already have. Added points carry a **"Grambank"** badge
  in their popup and detail panel.

Note: if your own coding scheme uses different category labels than Grambank's, 
both will appear as separate categories in the legend for that variable.

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

## 10. Acknowledgements

The development and use of this tool have been made possible by the following open-source projects, datasets, and research infrastructures. We are grateful to their creators and maintainers for making their work freely available.

---

### Core Libraries

#### Leaflet
An open-source JavaScript library for interactive, mobile-friendly maps.  
© 2010–2024 Volodymyr Agafonkin and contributors.  
Licensed under the **BSD 2-Clause License**.  
https://leafletjs.com/

#### html2canvas
A JavaScript library for capturing screenshots of web pages.  
© 2012 Niklas von Hertzen.  
Licensed under the **MIT License**.  
https://html2canvas.hertzen.com/

#### SheetJS (Community Edition)
A JavaScript library for reading and writing spreadsheet files.  
© SheetJS Community Edition.  
Licensed under the **MIT License**.  
https://sheetjs.com/

---

### Cartographic Data

#### Natural Earth
Free, public-domain vector and raster map data. Natural Earth is used as the primary cartographic basemap in this tool, providing country boundaries, coastlines, and populated place data at 1:10m resolution.  
Public Domain.  
https://www.naturalearthdata.com/

---

### Linguistic Data

#### Glottolog
A comprehensive bibliographic database of the world's languages, providing language classification and geographic coordinates. Glottolog coordinates are used as a fallback for language locations when Excel coordinates are missing or invalid.  
Hammarström, Harald, Forkel, Robert, Haspelmath, Martin, & Bank, Sebastian. (2025). *Glottolog 5.1*. Max Planck Institute for Evolutionary Anthropology.  
https://glottolog.org/  
DOI: [10.5281/zenodo.13950591](https://doi.org/10.5281/zenodo.13950591)

#### Grambank
A global database of grammatical features, providing typological data for over 2,400 languages. Grambank data can be imported directly into the tool for comparative analysis and contextualisation of user-provided datasets.  
Skirgård, H., Haynie, H. J., Blasi, D. E., Hammarström, H., Collins, J., Latarche, J. J., … & Greenhill, S. J. (2023). *Grambank: A global database of grammatical features* (v1.0). Max Planck Institute for Evolutionary Anthropology.  
https://grambank.clld.org/  
DOI: [10.5281/zenodo.7740434](https://doi.org/10.5281/zenodo.7740434)  
Licensed under **CC BY 4.0**.

---

We also thank the broader open-source and open-science communities whose tools and data make reproducible, transparent research possible.
