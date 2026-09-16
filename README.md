*This project was fully AI-assisted (vibe-coded) and is subsequently reviewed and maintained by the author.*

You can also use InTyMaVi directly in your browser, **no download needed**!
→ https://pardosergi.github.io/InTyMaVi/

# InTyMaVi — Interactive Typological Map Visualiser

InTyMaVi is a single, self-contained HTML file for exploring linguistic-typological
data on an interactive map. Open the `.html` file in any modern browser — no
installation, server, or internet account is required. An internet connection is needed
for the base map and for the Glottolog/Grambank features described below; both are
cached locally afterwards.

## Contents

- [1. Getting started](#1-getting-started)
- [2. Two ways to bring in data](#2-two-ways-to-bring-in-data)
- [3. Preparing an Excel/CSV file](#3-preparing-an-excelcsv-file)
- [4. Using a CLDF dataset](#4-using-a-cldf-dataset)
- [5. Glottocodes and Glottolog enrichment](#5-glottocodes-and-glottolog-enrichment)
- [6. Choosing a Glottolog/Grambank release and managing the cache](#6-choosing-a-glottologgrambank-release-and-managing-the-cache)
- [7. Adding context with Grambank](#7-adding-context-with-grambank)
- [8. Exploring the map](#8-exploring-the-map)
- [9. Downloading a map image](#9-downloading-a-map-image)
- [10. Saving and reusing a specific zoom/view](#10-saving-and-reusing-a-specific-zoomview)
- [11. Troubleshooting](#11-troubleshooting)
- [12. Acknowledgements](#12-acknowledgements)

---

## 1. Getting started

Double-click the `.html` file (or open it from your browser).
The map loads empty, with a **"📂 Load data"** prompt in the middle — click it,
or use the **"Update data"** button in the header, to import your first dataset.

## 2. Two ways to bring in data

InTyMaVi accepts two kinds of dataset, and **detects automatically** which one
you're giving it:

- an **Excel or CSV file** (§3) — the simplest option for most users;
- a **CLDF dataset** (§4) — for interoperating with the wider CLDF/typology
  ecosystem (Grambank, WALS-style resources, your own CLDF-formatted data, etc.).

Either way, dropping a new dataset into **"Update data"** *replaces* the map's
current data. A short status message confirms how many varieties and
variables were loaded, or explains what went wrong.

Across both formats, **Glottocode is the primary language identifier**
(see §5): give one, and everything else about that language — name,
coordinates, phylogenetic classification — becomes optional, since it can be
retrieved from Glottolog. Anything you *do* supply yourself always takes
precedence over Glottolog.

## 3. Preparing an Excel/CSV file

InTyMaVi reads a single sheet (`.xlsx`/`.xls`/`.csv`/`.tsv`) with one row per
language/variety. Column headers are matched flexibly — in **Catalan or
English**, accents and capitalisation are ignored:

| Purpose | Accepted header names |
|---|---|
| Glottocode (conditionally optional, see §5) | `Glottocode` |
| Language name (conditionally optional, see §5) | `Llengua` / `Language` / `Nom` / `Name` |
| Variety / dialect (optional) | `Varietat` / `Variety` |
| Latitude (conditionally optional, see §5) | `Latitud` / `Latitude` |
| Longitude (conditionally optional, see §5) | `Longitud` / `Longitude` |
| Family / classification (optional, see §5) | `Família` / `Family` / `Phylogeny` / `Classification` |

A row needs **either** a Glottocode **or** a language name — coordinates too
can come from either your own columns or from Glottolog, as long as a
Glottocode is given. A row with neither a Glottocode nor its own name and
coordinates can't be placed on the map.

Coordinates can be plain decimal numbers (`41.38`) or degrees/minutes/seconds
with a cardinal letter (`41°23'N`).

**Any other column is treated as a typological variable** — its header becomes
the variable's name in the app, and each cell is one language's value for that
variable (e.g. `SVO`, `yes`/`no`, `prenominal`…). You can have as many variable
columns as you like; you'll choose which one to visualise from a dropdown once
the file is loaded.

**Columns whose header starts with `#` are ignored completely** (whatever
they contain) — handy for notes, comments, or working columns you don't want
treated as a variable.

You may also use the `EXAMPLE.xlsx` spreadsheet as a template.

> 💡 If you want a variable column to later merge automatically with Grambank
> data (see §7), name it **exactly like the Grambank code**, e.g. `GB130`.
> If you're using a CLDF dataset instead, see §7 for the equivalent rule.

## 4. Using a CLDF dataset

InTyMaVi can also read a [CLDF](https://cldf.clld.org/) dataset directly —
the same format used by Glottolog, Grambank, and most large typological
databases. Rather than assuming any fixed file or column names, InTyMaVi
reads the dataset's own `*-metadata.json` to work out which files hold
languages, features (parameters), codes, and values.

To import one, drop into **"Update data"**:
- a single **`.zip`** file containing the whole dataset, or
- the metadata JSON file **together with** its table files (select them all
  at once — multiple files in one go are treated as a CLDF dataset).

What's read from it:
- **Languages** (`LanguageTable`) — Glottocode, name, coordinates and, if
  present, a classification/family column. As with Excel/CSV, a Glottocode is
  enough on its own; anything else missing is filled in from Glottolog.
- **Features and values** (`ParameterTable` + `ValueTable`, optionally
  `CodeTable` for coded values) — each parameter becomes one variable column
  in InTyMaVi, named after the parameter's `Name` (falling back to its ID).

A CLDF dataset needs a `LanguageTable` plus a `ParameterTable`/`ValueTable`
pair to be usable — a dataset with only languages, or only values, isn't
enough on its own.

## 5. Glottocodes and Glottolog enrichment

Whenever a language has a **Glottocode**, InTyMaVi treats it as that
language's primary identifier and can look it up in
[Glottolog](https://glottolog.org/) for anything you didn't supply yourself:
name, coordinates, and phylogenetic classification. Matching is **always by
Glottocode**.

Rules:
- Anything your own dataset provides — Excel/CSV or CLDF — is **always used
  as-is**; Glottolog only fills in what's missing.
- A language with **no Glottocode** still works exactly like before: it just
  needs its own name and coordinates (phylogeny is optional either way).
- Glottolog is downloaded automatically, once, the first time a dataset with
  Glottocodes is imported (see §6 for choosing *which* release and for local
  caching).

**Seeing what came from where:** click a language on the map, or select it in
the language list, to see its Glottocode, name, coordinates and phylogenetic
classification. A small **"Glottolog"** badge appears next to each of these
individually whenever *that particular piece* was retrieved from Glottolog
rather than supplied in your own dataset — so a language can have, say, its
name from your file and its coordinates from Glottolog, and you'll see
exactly which is which.

## 6. Choosing a Glottolog/Grambank release and managing the cache

The **"🗂️ Data sources"** button opens a panel where you can:
- see which Glottolog and/or Grambank release is currently loaded;
- pick a **different release** from a dropdown (populated from each project's
  published releases; the most recent is selected by default) and load it;
- **clear the local cache** if you want to force a fresh download.

Neither dataset is ever bundled into the InTyMaVi file itself — both are
downloaded on demand, in [CLDF](https://cldf.clld.org/) form, directly from
their official repositories, and then **cached locally in your browser** so
reopening InTyMaVi later, or reloading the same release, doesn't need to
re-download anything.

Switching to a different Glottolog release re-resolves your currently loaded
data against it immediately (any coordinates/names/classifications that came
from Glottolog are recomputed; anything you supplied yourself is untouched).

## 7. Adding context with Grambank

The **"🌐 Grambank"** button lets you pull in grammatical data from
[Grambank](https://grambank.clld.org) (195 features, ~2,400 languages) to put
your own sample in a broader typological context. It uses whichever Grambank
release is currently selected in **"🗂️ Data sources"** (§6).

1. Click **"🌐 Grambank"**. The app fetches Grambank's feature list, codes and
   language table once per selected release (cached afterwards).
2. **Search** for a feature by keyword or code (`word order`, `article`,
   `GB130`…) and **check** any number of features you want.
3. Optionally **restrict by family** (comma-separated, e.g. `Indo-European`,
   `Austronesian`) to avoid cluttering the map with unrelated languages.
4. Click **"Download & import"**. The first time, this downloads Grambank's
   full value table for the selected release (a progress bar is shown);
   afterwards it's cached locally.

**How it combines with your own data:**
- If a selected Grambank code matches an **existing column** in your loaded
  data — either an Excel/CSV column literally named like the code (e.g.
  `GB130`), *or*, for a CLDF dataset, a parameter whose **CLDF Parameter ID**
  matches the code (its display name doesn't need to match anything) — the
  checklist shows a **"↔ merges into…"** tag, and the imported values are
  merged into that same column. No extra Grambank-specific setup is needed on
  your end either way.
- If there's no matching column, the feature is added as a **new column**
  instead.
- **Languages are matched and de-duplicated by Glottocode only, never by
  name.** Languages you already have are left exactly as they are; Grambank
  only *adds* languages you don't already have (and only those with a
  Glottocode).
- **Grambank-added languages only appear on the map while you're actually
  visualising a feature that came from Grambank** — switch back to one of
  your own features and they're hidden again automatically, so they never
  clutter an unrelated view. If they're not visible right after importing,
  the status message will tell you to switch the visualised feature to see
  them.

Note: if your own coding scheme uses different category labels than
Grambank's, both will appear as separate categories in the legend for that
variable.

## 8. Exploring the map

- **Variable to display** — the dropdown selects which imported column colours
  the markers, with a matching legend.
- **"+ Correlation" / Cross with** — colour markers by the *combination* of two
  variables at once, to explore co-occurrence patterns.
- Click a legend entry to **filter** the map to only that value (click again,
  or **"✕ Clear selection"**, to reset); you can also change each value's
  marker **colour** and **shape** from the legend.
- The **search box** filters the language list by name.
- Click any marker, or any row in the language list, to see its full detail
  panel: Glottocode, name, coordinates, phylogenetic classification (each
  badged when it came from Glottolog — see §5), and every variable's value.

## 9. Downloading a map image

The **download button** in the header opens **"Map download options"**, where
you choose:
- Zoom level (coarse selector + a fine adjustment slider) and pan/focus,
- Aspect ratio,
- Icon and legend size,
- Whether and where you want to show language names,
- Legend position (four corners, or none — for adding one manually elsewhere),
- Whether to also export the legend as a separate image.

A live preview updates as you change these. Click **"Download"** to generate
and save the PNG. Your choices are remembered automatically for next time.

## 10. Saving and reusing a specific zoom/view

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

## 11. Troubleshooting

- **"No valid rows found"** on import — each row needs either a Glottocode
  that Glottolog can resolve, or its own name and readable coordinates.
- **"Could not find a CLDF metadata file"** — make sure you selected the
  `*-metadata.json` file together with all of the table files it references
  (or a single `.zip` containing the whole dataset).
- **A family/classification looks wrong or missing** — InTyMaVi never shows a
  bare Glottocode in place of a family name; if a dataset only provides a
  coded family reference and Glottolog hasn't resolved it yet, the field is
  left blank rather than showing the code.
- **Grambank download feels slow the first time** — the full value table for
  a release is tens of MB and is only fetched once per release; it's cached
  locally afterwards, including across sessions.
- **Two categories that should be the same appear separately in the legend**
  after a Grambank merge — your dataset's own value labels for that column
  don't match Grambank's wording exactly (e.g. `SOV` vs `SV`); you'll need to
  align your category labels manually if you want a single merged legend.
- **I picked a different Glottolog/Grambank release and nothing changed** —
  switching releases re-resolves your current data immediately for Glottolog;
  for Grambank, re-import the features you want from the newly selected
  release via the "🌐 Grambank" button.
- InTyMaVi needs an internet connection for the base map tiles and for the
  first download of any given Glottolog/Grambank release (or CLDF file
  fetched from a URL) — everything else, including previously downloaded
  releases, works fully offline.

## 12. Acknowledgements

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
A JavaScript library for reading and writing spreadsheet files, also used
here to parse CSV/TSV tables from CLDF datasets.  
© SheetJS Community Edition.  
Licensed under the **MIT License**.  
https://sheetjs.com/

#### JSZip
A JavaScript library for reading `.zip` archives in the browser, used to
unpack CLDF datasets provided as a single `.zip` file.  
© Stuart Knightley and contributors.  
Licensed under the **MIT License** (dual MIT/GPLv3).  
https://stuk.github.io/jszip/

---

### Cartographic Data

#### Natural Earth
Free, public-domain vector and raster map data. Natural Earth is used as the primary cartographic basemap in this tool, providing country boundaries, coastlines, and populated place data at 1:10m resolution.  
Public Domain.  
https://www.naturalearthdata.com/

---

### Linguistic Data

#### Glottolog
A comprehensive bibliographic database of the world's languages, providing
language classification and geographic coordinates. InTyMaVi downloads
Glottolog as a CLDF dataset and uses Glottocodes as the primary identifier
for every language, retrieving name, coordinates, and classification for
anything not supplied directly in the user's own dataset.  
Hammarström, Harald, Forkel, Robert, Haspelmath, Martin, & Bank, Sebastian. (2025). *Glottolog 5.1*. Max Planck Institute for Evolutionary Anthropology.  
https://glottolog.org/  
DOI: [10.5281/zenodo.13950591](https://doi.org/10.5281/zenodo.13950591)

(InTyMaVi lets you choose which published Glottolog release to use; the
citation above refers to the release current at the time of writing.)

#### Grambank
A global database of grammatical features, providing typological data for
over 2,400 languages. InTyMaVi downloads Grambank as a CLDF dataset and lets
users import any subset of its features directly, for comparative analysis
and contextualisation of their own data.

Skirgård, Hedvig, Hannah J. Haynie, Damián E. Blasi, Harald Hammarström, Jeremy Collins, Jay J. Latarche, Jakob Lesage, Tobias Weber, Alena Witzlack-Makarevich, Sam Passmore, Angela Chira, Luke Maurits, Russell Dinnage, Michael Dunn, Ger Reesink, Ruth Singer, Claire Bowern, Patience Epps, Jane Hill, Outi Vesakoski, Martine Robbeets, Noor Karolin Abbas, Daniel Auer, Nancy A. Bakker, Giulia Barbos, Robert D. Borges, Swintha Danielsen, Luise Dorenbusch, Ella Dorn, John Elliott, Giada Falcone, Jana Fischer, Yustinus Ghanggo Ate, Hannah Gibson, Hans-Philipp Göbel, Jemima A. Goodall, Victoria Gruner, Andrew Harvey, Rebekah Hayes, Leonard Heer, Roberto E. Herrera Miranda, Nataliia Hübler, Biu Huntington-Rainey, Jessica K. Ivani, Marilen Johns, Erika Just, Eri Kashima, Carolina Kipf, Janina V. Klingenberg, Nikita König, Aikaterina Koti, Richard G. A. Kowalik, Olga Krasnoukhova, Nora L.M. Lindvall, Mandy Lorenzen, Hannah Lutzenberger, Tônia R.A. Martins, Celia Mata German, Suzanne van der Meer, Jaime Montoya Samamé, Michael Müller, Saliha Muradoglu, Kelsey Neely, Johanna Nickel, Miina Norvik, Cheryl Akinyi Oluoch, Jesse Peacock, India O.C. Pearey, Naomi Peck, Stephanie Petit, Sören Pieper, Mariana Poblete, Daniel Prestipino, Linda Raabe, Amna Raja, Janis Reimringer, Sydney C. Rey, Julia Rizaew, Eloisa Ruppert, Kim K. Salmon, Jill Sammet, Rhiannon Schembri, Lars Schlabbach, Frederick W.P. Schmidt, Amalia Skilton, Wikaliler Daniel Smith, Hilário de Sousa, Kristin Sverredal, Daniel Valle, Javier Vera, Judith Voß, Tim Witte, Henry Wu, Stephanie Yam, Jingting Ye 葉婧婷, Maisie Yong, Tessa Yuditha, Roberto Zariquiey, Robert Forkel, Nicholas Evans, Stephen C. Levinson, Martin Haspelmath, Simon J. Greenhill, Quentin D. Atkinson & Russell D. Gray (2023). *Grambank reveals the importance of genealogical constraints on linguistic diversity and highlights the impact of language loss.* Science Advances, 9(16), eadg6175. https://doi.org/10.1126/sciadv.adg6175

Skirgård, Hedvig, Hannah J. Haynie, Harald Hammarström, Damián E. Blasi, Jeremy Collins, Jay Latarche, Jakob Lesage, Tobias Weber, Alena Witzlack-Makarevich, Michael Dunn, Ger Reesink, Ruth Singer, Claire Bowern, Patience Epps, Jane Hill, Outi Vesakoski, Noor Karolin Abbas, Sunny Ananth, Daniel Auer, Nancy A. Bakker, Giulia Barbos, Anina Bolls, Robert D. Borges, Mitchell Browen, Lennart Chevallier, Swintha Danielsen, Sinoël Dohlen, Luise Dorenbusch, Ella Dorn, Marie Duhamel, Farah El Haj Ali, John Elliott, Giada Falcone, Anna-Maria Fehn, Jana Fischer, Yustinus Ghanggo Ate, Hannah Gibson, Hans-Philipp Göbel, Jemima A. Goodall, Victoria Gruner, Andrew Harvey, Rebekah Hayes, Leonard Heer, Roberto E. Herrera Miranda, Nataliia Hübler, Biu H. Huntington-Rainey, Guglielmo Inglese, Jessica K. Ivani, Marilen Johns, Erika Just, Ivan Kapitonov, Eri Kashima, Carolina Kipf, Janina V. Klingenberg, Nikita König, Aikaterina Koti, Richard G. A. Kowalik, Olga Krasnoukhova, Kate Lynn Lindsey, Nora L. M. Lindvall, Mandy Lorenzen, Hannah Lutzenberger, Alexandra Marley, Tânia R. A. Martins, Celia Mata German, Suzanne van der Meer, Jaime Montoya, Michael Müller, Saliha Muradoglu, HunterGatherer, David Nash, Kelsey Neely, Johanna Nickel, Miina Norvik, Bruno Olsson, Cheryl Akinyi Oluoch, David Osgarby, Jesse Peacock, India O.C. Pearey, Naomi Peck, Jana Peter, Stephanie Petit, Sören Pieper, Mariana Poblete, Daniel Prestipino, Linda Raabe, Amna Raja, Janis Reimringer, Sydney C. Rey, Julia Rizaew, Eloisa Ruppert, Kim K. Salmon, Jill Sammet, Rhiannon Schembri, Lars Schlabbach, Frederick W. P. Schmidt, Dineke Schokkin, Jeff Siegel, Amalia Skilton, Hilário de Sousa, Kristin Sverredal, Daniel Valle, Javier Vera, Judith Voß, Daniel Wikalier Smith, Tim Witte, Henry Wu, Stephanie Yam, Jingting Ye 葉婧婷, Maisie Yong, Tessa Yuditha, Roberto Zariquiey, Robert Forkel, Nicholas Evans, Stephen C. Levinson, Martin Haspelmath, Simon J. Greenhill, Quentin D. Atkinson & Russell D. Gray (2023). Grambank v1.0 (v1.0) [Data set]. Zenodo. https://doi.org/10.5281/zenodo.7740140

https://grambank.clld.org/   
Licensed under **CC BY 4.0**.

(InTyMaVi lets you choose which published Grambank release to use; the
citation above refers to v1.0.)

#### CLDF (Cross-Linguistic Data Formats)
An open specification for interoperable, machine-readable cross-linguistic
data. InTyMaVi reads Glottolog, Grambank, and user-supplied datasets alike as
CLDF, resolving tables and columns from each dataset's own metadata rather
than assuming fixed file or column names.  
Forkel, R., List, J. M., Greenhill, S. J., Rzymski, C., Bank, S., Cysouw, M., Hammarström, H., Haspelmath, M., Kaiping, G. A., & Gray, R. D. (2018). *Cross-Linguistic Data Formats, advancing data sharing and re-use in comparative linguistics*. Scientific Data, 5, 180205.  
https://cldf.clld.org/

---

We also thank the broader open-source and open-science communities whose tools and data make reproducible, transparent research possible.
