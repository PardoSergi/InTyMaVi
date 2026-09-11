**54 prompts** ordered chronologically (oldest to newest).

This prompt list is currently still in progress and is therefore non-exhaustive. It does not constitute a guide on how to create a program like InTyMaVi, but rather a retrospective account of its development.

Prompts originally written in Catalan include an English translation below the original. Prompts originally written in English are shown as-is.

Unless specified otherwise, all prompts were given to Claude Sonnet in its most recent version available at the time of prompting.

---

## Phase 1: creating InTyMaBo, an Interactive Typological Map of Borneo

**Comment:** I originally created this program to assist me with my Bachelor's thesis on the typology of Bornean voice systems and needed to generate and download maps.
I wasn't very experienced with R and constantly had to ask AI before entering any new code into RStudio. Since I was using AI anyway, why not vibe-code a program that
would do what I needed in a more intuitive way?

### 1. 2026-04-06

**Original:**

> I want to create a program with an interactive typological map of the languages of Borneo using the data from an excel file

**Comment:** I attached the Excel file with my typological data together with this prompt. Although vague, this prompt proved extremely useful, as it created a fully
functional program that set the base for InTyMaVi.

---

### 2. 2026-04-07

**Original:**

> Make these changes to the original program: En l’apartat “llista de llengües”, en clicar una llengua, s’ha d’obrir un desplegable amb tota la llista de característiques de la llengua en qüestió.
> En clicar una llengua en el mapa, no han d’aparèixer totes les característiques de la llengua en qüestió, sinó només la corresponent a la variable visualitzada. En comptes de les coordenades, hi apareixerà la classificació filogenètica, que apareix a l’excel com a nota sobre la casella del nom de la llengua.
> Els noms de les variables no han d’incloure el seu codi/abreviatura (com ara “VOL”, “PROC”).
> El zoom del mapa ha de fer salts 4 vegades més curts.
> En l’apartat “llegenda”, en clicar la rodona de color d’una característica en concret, s’ha de poder accedir a una selecció de colors per canviar el color de la característica. Al costat de cada característica, hi ha d’aparèixer el nombre de llengües en què es troba
> Les llengües que continguin “Nuclear Malayic” en algun lloc de la seva classificació filogenètica han d’estar marcats en el mapa no amb una rodona, sinó amb un triangle amb el color de la característica corresponent. No totes les llengües tenen classificació filogenètica encara.
> Cal incloure un botó que, en clicar-hi, descarregui una imatge del mapa de Borneo amb la variable visualitzada i els colors seleccionats. El botó ha de contenir una icona de càmera. La imatge ha d’incloure un requadre amb la llegenda al cantó superior esquerre. La imatge ha de tenir una ràtio 4:3, ha d’englobar tota l’illa de Borneo amb un petit marge al voltant i l’illa ha d’estar centrada lleugerament a la dreta.
> La paleta de colors la interfície ha de tenir colors freds.

**English translation:**

> Make these changes to the original program: In the "language list" section, clicking on a language should open a dropdown with the full list of characteristics for that language.
> Clicking on a language on the map should not show all the characteristics of that language, only the one corresponding to the displayed variable. Instead of the coordinates, the phylogenetic classification should appear, which is included in the Excel file as a note on the language-name cell.
> Variable names should not include their code/abbreviation (such as "VOL", "PROC").
> The map zoom should move in steps 4 times shorter.
> In the "legend" section, clicking on the color circle of a specific characteristic should give access to a color picker to change that characteristic's color. Next to each characteristic, the number of languages it appears in should be shown.
> Languages that contain "Nuclear Malayic" anywhere in their phylogenetic classification should be marked on the map not with a circle, but with a triangle in the color of the corresponding characteristic. Not all languages have a phylogenetic classification yet.
> A button should be included that, when clicked, downloads an image of the Borneo map with the displayed variable and selected colors. The button should contain a camera icon. The image should include a box with the legend in the top-left corner. The image should have a 4:3 ratio, should encompass the entire island of Borneo with a small margin around it, and the island should be centered slightly to the right.
> The interface's color palette should use cool colors.

**Comment:** The "Nuclear Malayic" feature was specific to my research and was later reverted.

---

### 3. 2026-04-08

**Original:**

> Eliminar el text “42 varietats lingüístiques. Dades tipològiques comparades”. En comptes d’això, incloure el nombre de varietats lingüístiques dins un badge al costat del títol “Llista de llengües”.
> En l’apartat “llista de llengües”, el desplegable amb tota la llista de característiques de la llengua en qüestió no ha de contenir la filogènia. En clicar-hi una llengua, a part d’obrir el desplegable, ha de mostrar-se la llengua en el mapa.
> El zoom del mapa ha de fer salts el doble de llargs que en la darrera versió
> L’apartat “llegenda” ha d’ocupar més espai. Per fer espai, treure el títol “Tret tipològic” i el subtítol “Clica el cercle per canviar color · Clica l’etiqueta per filtrar”. La llista de llengües també pot ocupar una mica menys. La selecció de colors ha d’incloure tota mena de colors, no només freds. Eliminar el badge al costat del títol “Llegenda” que compta el nombre de característiques diferents.
> El triangle de les llengües “Nuclear Malayic” ha de tenir la mateixa vora blanca que les rodones de la resta de llengües.
> La imatge descarregada ha d’incloure la llegenda al cantó superior esquerre dins d’un requadre amb fons blanc. La imatge descarregada no ha d’incloure els botons de zoom.
> Cal canviar els colors de la interfície a uns altres de més neutres.
> Cal afegir-hi un mecanisme que em permeti actualitzar les dades del mapa pujant-hi un Excel com l’adjuntat en aquesta conversa.

**English translation:**

> Remove the text "42 linguistic varieties. Compared typological data". Instead, include the number of linguistic varieties in a badge next to the "Language list" title.
> In the "language list" section, the dropdown with the full list of characteristics for a given language should not contain the phylogeny. Clicking on a language should, besides opening the dropdown, also show the language on the map.
> The map zoom should move in steps twice as long as in the previous version.
> The "legend" section should take up more space. To make room, remove the title "Typological feature" and the subtitle "Click the circle to change color · Click the label to filter". The language list can also take up a bit less space. The color picker should include all kinds of colors, not just cool ones. Remove the badge next to the "Legend" title that counts the number of different characteristics.
> The triangle for "Nuclear Malayic" languages should have the same white border as the circles for the rest of the languages.
> The downloaded image should include the legend in the top-left corner inside a box with a white background. The downloaded image should not include the zoom buttons.
> Change the interface colors to more neutral ones.
> Add a mechanism that lets me update the map data by uploading an Excel file like the one attached in this conversation.

---

### 4. 2026-04-08

**Original:**

> En els desplegables de “llista de llengües”, el nom de la característica ha d’ocupar horitzontalment només una mica més de la meitat de la taula.
> En la llegenda, cal ordenar les característiques de més a menys freqüent.
> El programa actualment consta d’un botó de descàrrega que descarrega una captura del mapa, però això no és el que vull. Cal refer de zero la funció de descàrrega de mapa. Vull que el botó generi una imatge (no que faci una captura) amb un mapa de l’illa de Borneo amb la variable seleccionada i els colors seleccionats per a cada característica en cada llengua, amb una llegenda en el cantó superior esquerre. La llegenda ha de tenir com a títol el nom de la variable visualitzada. La llegenda ha de tenir un fons blanc quadrangular amb vores arrodonides i un lleuger ombrejat. En el mapa no hi han de sortir botons de zoom. Tampoc no ha de quedar cap marge blanc en el mapa descarregat.

**English translation:**

> In the "language list" dropdowns, the characteristic name should horizontally take up only a little more than half of the table.
> In the legend, the characteristics should be ordered from most to least frequent.
> The program currently has a download button that downloads a screenshot of the map, but that's not what I want. The map-download function needs to be rebuilt from scratch. I want the button to generate an image (not take a screenshot) with a map of the island of Borneo showing the selected variable and the selected colors for each characteristic in each language, with a legend in the top-left corner. The legend's title should be the name of the displayed variable. The legend should have a white, rectangular background with rounded corners and a slight shadow. The map should not show zoom buttons. The downloaded map should also have no white margin left.

---

### 5. 2026-04-08

**Original:**

> En la selecció de colors no hi ha d’haver colors massa similars. Conservar la funcionalitat de personalitzar el color.
> El menú de la llegenda ha de contenir un botó per desfer la selecció de característiques destacades en el mapa.
> El mapa generat en la descàrrega ha de tenir una ràtio de 4:3 (ampliar horitzontalment només cap a l’esquerra) i s’ha d’ampliar una mica més verticalment tant al nord com al sud perquè hi surti tota l’illa amb un petit marge. La llegenda del mapa generat ha de tenir un text bastant més gran en general, però sobretot pel que fa al títol. La llegenda no ha de contenir mai una icona triangular, tan sols cercles. Els cercles tant del mapa com de la llegenda han de ser un 50% més grans.
> La definició del mapa descarregat ha de ser més alta.
> El programa no ha de contenir dades lingüístiques per defecte sobre les llengües més enllà de les filogenètiques, sinó que cal pujar-hi abans un Excel perquè mostri les seves dades. L’actualització de dades ha de permetre l’addició de noves variables, així com l’eliminació d’altres en cas que ja no apareguin a l’excel.

**English translation:**

> In the color picker, there should be no colors that are too similar to each other. Keep the ability to customize the color.
> The legend menu should contain a button to undo the selection of highlighted characteristics on the map.
> The map generated for download should have a 4:3 ratio (expanding horizontally only to the left) and should be expanded a bit more vertically, both north and south, so that the whole island appears with a small margin. The legend of the generated map should have noticeably larger text overall, but especially the title. The legend should never contain a triangular icon, only circles. The circles, both on the map and in the legend, should be 50% larger.
> The resolution of the downloaded map should be higher.
> The program should not contain any default linguistic data about the languages beyond the phylogenetic ones; instead, an Excel file must be uploaded first for it to display its data. The data update should allow adding new variables as well as removing others if they no longer appear in the Excel file.

---

## Conversation: Especificacions de disseny per a interfície de mapa

### 6. 2026-04-08

**Original:**

> Els colors del menú de colors han d’estar ordenats horitzontalment segons l’escala cromàtica i verticalment segons la brillantor, i no pot haver-hi colors repetits.
> Quan dos o més punts se superposin, cal separar-los lleugerament i indicar amb una línia la seva ubicació real.
> La imatge descarregada no ha de tenir marges buits ni blancs, no es pot estendre més enllà de la part visible. El marge superior del mapa descarregat ha de reduir-se un 60% i l’inferior s’ha de reduir un 40%.

**English translation:**

> The colors in the color menu should be ordered horizontally according to the chromatic scale and vertically according to brightness, with no repeated colors.
> When two or more points overlap, they should be separated slightly and their real location indicated with a line.
> The downloaded image should have no empty or white margins, and should not extend beyond the visible area. The top margin of the downloaded map should be reduced by 60% and the bottom margin by 40%.

---

### 7. 2026-04-09

**Original:**

> El menú de colors ha d’incloure també una escala de grisos que inclogui blanc i negre.
> Quan dos o més punts se superposin, cal separar-los lleugerament i indicar amb una línia contínua la seva ubicació real. Si la nova ubicació del punt comporta la superposició amb un altre punt, cal desplaçar amb un angle diferent.
> Quant a les proporcions del mapa descarregat, aquest ha de tenir una ràtio 4:3. Per aconseguir-la, cal retallar el 25% de la imatge per la dreta i ampliar la resta cap al nord fins a aconseguir la ràtio desitjada.

**English translation:**

> The color menu should also include a grayscale column that includes white and black.
> When two or more points overlap, they should be separated slightly and their real location indicated with a solid line. If the point's new location causes it to overlap with another point, it should be shifted at a different angle.
> As for the downloaded map's proportions, it should have a 4:3 ratio. To achieve this, 25% of the image should be cropped from the right and the rest expanded northward until the desired ratio is reached.

---

### 8. 2026-04-09

**Original:**

> En el menú de colors, eliminar la fila inferior. Quant a la columna de l’escala de grisos, ha de contenir el color blanc, un gris clar, un gris fosc i el color negre.
> Quant a la superposició dels punts, cal reduir la sensibilitat per considerar que dos punts estan superposats. La distància a què es desplacen els punts superposats s’ha de reduir a la meitat.
> Quant al mapa descarregat, cal fer-hi una mica de zoom-in sense perdre la ràtio 4:3.

**English translation:**

> In the color menu, remove the bottom row. As for the grayscale column, it should contain white, a light gray, a dark gray, and black.
> As for point overlap, the sensitivity for considering two points overlapping should be reduced. The distance overlapping points are shifted by should be reduced by half.
> As for the downloaded map, zoom in on it slightly without losing the 4:3 ratio.

---

### 9. 2026-04-09

**Original:**

> En el menú de colors, cal moure les files perquè quedin en aquest ordre: 4a, 1a, 2a, 3a. Aquest canvi no s’ha d’aplicar a la darrera columna. D’aquesta forma, els colors queden ordenats verticalment de més clar a més fosc.
> Sense alterar el zoom, la imatge descarregada s’ha de moure un 3% cap al nord i un 5% cap a l’est. Els punts han de ser un 10% més grans. Les llengües “nuclear Malayic” també han de ser triangles en la imatge descarregada. El nom de la imatge descarregada ha de ser “Mapa_” +  el nom de la variable observada.

**English translation:**

> In the color menu, the rows need to be reordered as follows: 4th, 1st, 2nd, 3rd. This change should not apply to the last column. This way, the colors end up ordered vertically from lightest to darkest.
> Without changing the zoom, the downloaded image should be shifted 3% north and 5% east. The points should be 10% bigger. “Nuclear Malayic” languages should also be triangles in the downloaded image. The downloaded image's filename should be “Map_” + the name of the observed variable.

---

### 10. 2026-04-09

**Original:**

> Sense alterar el zoom, la imatge descarregada s’ha de moure un 1% cap al sud. Els punts han de ser un 10% més grans. El desplaçament dels punts superposats en la imatge descarregada s’ha de reduir un 50%.

**English translation:**

> Without changing the zoom, the downloaded image should be shifted 1% south. The points should be 10% bigger. The offset of overlapping points in the downloaded image should be reduced by 50%.

---

### 11. 2026-04-09

**Original:**

> En la descàrrega de fotos, fer que el títol de la llegenda sigui només lleugerament més gran que la resta del text

**English translation:**

> In the photo download, make the legend's title only slightly bigger than the rest of the text

---

### 12. 2026-04-12

**Original:**

> Fes que les llengües amb que pertanyin al grup "Malayic" (però no al Nuclear Malayic) estiguin marcades amb un triangle invertit tant en el mapa interactiu com en la imatge descarregada. Les llengües que pertanyin al grup "Greater Sulawesi" han d'estar marcades amb un quadrat tant en el mapa interactiu com en la imatge descarregada. En el mapa interactiu, tant els triangles invertits com els quadrats han de tenir la mateixa vora blanca i sombrejat que la resta d'icones

**English translation:**

> Make languages belonging to the "Malayic" group (but not Nuclear Malayic) marked with an inverted triangle, both on the interactive map and in the downloaded image. Languages belonging to the "Greater Sulawesi" group should be marked with a square, both on the interactive map and in the downloaded image. On the interactive map, both the inverted triangles and the squares should have the same white border and shading as the rest of the icons.

---

### 13. 2026-04-13

**Original:**

> Actualment, el mapa descarregat conté la mateixa regió geogràfica independentment de les coordenades de les dades. Cal canviar això. El mapa descarregat s’ha de centrar automàticament en base a les coordenades de les dades introduïdes de forma que englobi tots els punts amb el mateix marge en cada costat amb què ho fa ara, amb una diferència: el marge cap amunt ha de ser tan ample com l’actual marge cap avall. La ràtio del mapa descarregat sempre ha de ser de 4:3.

**English translation:**

> Currently, the downloaded map contains the same geographic region regardless of the data's coordinates. This needs to change. The downloaded map should automatically center itself based on the coordinates of the entered data, so that it encompasses all the points with the same margin on each side as it does now, with one difference: the top margin should be as wide as the current bottom margin. The downloaded map's ratio should always be 4:3.

**Comment:** My first attempt at making InTyMaBo less about Borneo. These changes (including the following two prompts) did not make it through, and I kept on elaborating on
the Borneo-specific program.

---

### 14. 2026-04-13

**Original:**

> La imatge descarregada no es pot estendre més enllà dels límits del mapa, fins i tot si això vol dir no respectar els marges. La llegenda ha de ser una mica més gran. Quant al mapa interactiu, aquest no s'ha d'obrir necessàriament a Borneo, sinó que a primera vista ha de permetre visualitzar totes les llengües de la mostra

**English translation:**

> The downloaded image must not extend beyond the map's limits, even if that means not respecting the margins. The legend should be a bit bigger. As for the interactive map, it doesn't necessarily have to open on Borneo — at first glance it should allow all the languages in the sample to be seen.

---

### 15. 2026-04-13

**Original:**

> La llegenda que cal fer més gran és la del mapa descarregat, la del sidebar deixa-la com estava

**English translation:**

> The legend that needs to be made bigger is the one on the downloaded map — leave the sidebar's legend as it was.

---

### 16. 2026-04-15

**Original:**

> El text de la llegenda del mapa descarregat ha de saltar de línia si s'allarga massa

**English translation:**

> The downloaded map's legend text should wrap to a new line if it gets too long

---

### 17. 2026-04-15

**Original:**

> Els triangles (tant els invertits com els no invertits) del mapa interactiu assenyalen amb la punta la ubicació, caldria centrar l’ubicació en el centre del triangle. Els triangles (tant els invertits com els no invertits) del mapa descarregat han de tenir una vora blanca i més prima, com les altres formes

**English translation:**

> The triangles (both inverted and non-inverted) on the interactive map point to the location with their tip — the location should instead be centered on the triangle's center. The triangles (both inverted and non-inverted) on the downloaded map should have a thinner white border, like the other shapes.

---

### 18. 2026-04-24

**Original:**

> Afegeix una funcionalitat que permeti combinar variables per observar correlacions, és a dir: a part de visualitzar variables individualment, hi ha d'haver la possibilitat de seleccionar-ne una segona i veure com s'interseccionen, per exemple, per veure quantes llengües amb Nombre de veus "3" tenen Veu Instrumental "sí" ("3" + "sí")

**English translation:**

> Add a feature that allows combining variables to observe correlations — that is, besides displaying variables individually, it should be possible to select a second one and see how they intersect, for example to see how many languages with Number of voices "3" have Instrumental voice "yes" ("3" + "yes")

---

### 19. 2026-05-09

**Original:**

> Fes que en les correlacions també ensenyi les combinacions que donin zero

**English translation:**

> Make it so the correlations also show the combinations that result in zero.

---

## Phase 2: Beyond Borneo — InTyMaBo becomes InTyMaVi

**Comment:** A couple of classmates asked if they could use my program for their poster on a typological feature. I then made a series of changes aimed at removing all 
Borneo-specific features, such as allowing to download a world-wide map.

### 20. 2026-06-15

**Original:**

> Fes que en el mode de descàrrega de mapa es vegi la totalitat del mapamundi, no només un zoom a Borneo. El títol del marge superior ha de ser "Mapa Tipològic Interactiu" sense referència a Borneo i també cal treure "▲ = Nuclear Malayic  ·  ▽ = Malayic  ·  ■ = Greater South Sulawesi"

**English translation:**

> Make the map-download mode show the entire world map, not just a zoomed-in view of Borneo. The title in the top margin should be "Interactive Typological Map" with no reference to Borneo, and "▲ = Nuclear Malayic  ·  ▽ = Malayic  ·  ■ = Greater South Sulawesi" also needs to be removed

---

### 21. 2026-06-15

**Original:**

> Fes que el programa extregui les dades filogenètiques de l'excel, concretament d'una columna anomenada "Família".

**English translation:**

> MMake the program extract the phylogenetic data from the Excel file, specifically from a column called "Família" (Family).

---

### 22. 2026-06-15

**Original:**

> Fes que també detecti i llegeixi coordenades no decimals amb punts cardinals.

**English translation:**

> Make it also detect and read non-decimal coordinates with cardinal points.

---

### 23. 2026-06-15

**Original:**

> Fes que el zoom inicial en obrir el programa no sigui a Borneo, sinó al mapa sencer.

**English translation:**

> Make the initial zoom when opening the program not be on Borneo, but on the whole map.

---

### 24. 2026-06-15

**Original:**

> Encara no incorpora la columna "Família" a la informació filogenètica

**English translation:**

> It still doesn't incorporate the "Família" column into the phylogenetic information

---

### 25. 2026-06-15

**Original:**

> No ho dic per les comprovacions de isNM etc. (elimina-les, per cert), sinó per la informació filogenètica que apareix al perfil de la llengua (on ara posa "Classificació filogenètica pendent")

**English translation:**

> I don't mean the isNM checks etc. (remove those, by the way), but the phylogenetic information that appears in the language's profile (where it currently says "Phylogenetic classification pending")

---

### 26. 2026-06-16

**Original:**

> Abans de descarregar el mapa, s'ha de seleccionar el lloc on apareixerà la llegenda

**English translation:**

> Before downloading the map, it should be possible to select where the legend will appear

**Comment:** I initially intended for the user to be able to drag the legend anywhere they wanted it to be on the map. Given my extreme vagueness, Claude provided me with the
four-corners system that InTyMaVi still uses as of v0.2.0, which I ended up liking more.

---

## Phase 3: NO mantinc el català — InTyMaVi learns English

**Comment:** At this point, I was planning to present InTyMaVi at the 18th Conference on Austronesian and Papuan Languages and Linguistics in Düsseldorf, so the interface had
to be translated to English. I also introduced some changes I reckoned would be useful beyond my own research and my classmates'.

### 27. 2026-07-08

**Original:**

> Traduir tota la interfície del programa a l’anglès.
> Quan el títol d’una llegenda és massa llarg, ha de continuar a la línia següent.
> En clicar descarregar el mapa, s’han de poder seleccionar el zoom i ràtio desitjats en el mapa, així com la posició de la llegenda (incloent-hi l’opció d’exportar el mapa sense llegenda + la llegenda per separat), aquestes opcions de zoom i llegenda s’han de poder guardar a fins de consistència entre els diferents mapes generats.
> Fes servir la font Arial en tota la interfície.

**English translation:**

> Translate the entire program interface into English.
> When a legend title is too long, it should continue on the next line.
> When clicking to download the map, it should be possible to select the desired zoom and ratio for the map, as well as the legend's position (including the option to export the map without the legend + the legend separately); these zoom and legend options should be saveable for consistency across the different generated maps.
> Use the Arial font throughout the interface.

---

### 28. 2026-07-09

**Original:**

> S’ha de poder triar la forma de les icones (cercle predeterminat, opcions extra: triangle, triangle invertit, quadrat i rombe), han d’aparèixer com s’hagin triat també al mapa descarregat.
> S’ha de poder triar la mida de les icones i la llegenda en el mapa descarregat. La mida actual hauria de ser la més petita, caldria afegir-hi mides mitjana i gran.

**English translation:**

> It should be possible to choose the shape of the icons (default circle, extra options: triangle, inverted triangle, square and diamond); they should appear as chosen on the downloaded map as well.
> It should be possible to choose the size of the icons and legend on the downloaded map. The current size should be the smallest; medium and large sizes need to be added.

---

### 29. 2026-07-09

**Original:**

> Els quadrats del mapa interactiu s’han de fer un 20% més petits. Els quadrats del mapa descarregat s’han de fer un 15% més grans, però.
> La llegenda dels mapes descarregats ha de ser en tots els casos un 20% més gran
> Actualment les mides mitjana i gran en les icones+llegenda del mapa descarregat són la mateixa mida. Conserva la mida gran tal com està, però fes que la mida mitjana sigui un terme intermedi entre la petita i la gran.
> Els diferents tipus de zoom per al mapa descarregat han de tenir noms més tècnics i neutres.
> El menú de selecció de paràmetres per al mapa descarregat ha d’incloure una previsualització del mapa.

**English translation:**

> The squares on the interactive map should be made 20% smaller. The squares on the downloaded map, however, should be made 15% larger.
> The legend on downloaded maps should in all cases be 20% larger.
> Currently the medium and large sizes for the icons+legend on the downloaded map are the same size. Keep the large size as it is, but make the medium size an intermediate step between small and large.
> The different zoom types for the downloaded map should have more technical and neutral names.
> The parameter-selection menu for the downloaded map should include a map preview.

---

### 30. 2026-07-09

**Original:**

> La ràtio 9:16 ha de portar el nom “phone screen”.
> Els zoom levels s’han de dividir en 10 nivells des del 0 (full-world) fins al 10, que ha de ser aproximadament tan petit com Catalunya. Addicionalment, hi haurà l’opció de modificar manualment el zoom del mapa descarregat, així com el focus (més centrat a la dreta/esquerra/amunt/avall).
> El mapa de la previsualització ha de ser un 50% més gran.
> Totes les formes del mapa interactiu excepte els cercles s’han de fer un 10% més grans.
> S’ha de treure el text “(default)” de la mida “small”.
> Esborra les dades filogenètiques preestablertes del programa, qualsevol dada filogenètica ha de venir de l’excel importat.
> El mapa ha de reconèixer també els noms de les columnes com “llengua”, “família”, etc. no només en català, sinó també en anglès “language”, “family”, etc.
> La varietat de la llengua no ha d’aparèixer entre parèntesis després del nom de la llengua, sinó tan sols a l’apartat “variety”. A la llista de llengües, la varietat ha d’aparèixer després del nom de la llengua separada d’alguna manera, amb la varietat en cursiva i/o un color més feble.

**English translation:**

> The 9:16 ratio should be named "phone screen".
> Zoom levels should be split into 10 levels, from 0 (full-world) to 10, which should be roughly as small as Catalonia. Additionally, there will be an option to manually adjust the downloaded map's zoom, as well as the focus (more centered to the right/left/up/down).
> The preview map should be 50% larger.
> All shapes on the interactive map except circles should be made 10% larger.
> The text "(default)" should be removed from the "small" size.
> Delete the program's preset phylogenetic data; any phylogenetic data should come from the imported Excel file.
> The map should also recognize column names like "llengua", "família", etc. not only in Catalan, but also in English: "language", "family", etc.
> The language variety should not appear in parentheses after the language name, but only in the "variety" field. In the language list, the variety should appear after the language name, set apart in some way, in italics and/or a lighter color.

---

### 31. 2026-07-09

**Original:**

> El menú d’opcions del mapa descarregat actualment és més gran que la pantalla al 100%, s’ha de fer més petit. No ha d’augmentar la seva llargada vertical per acomodar el mapa de previsualització, però sí l’horitzontal (és a dir, a l’inrevés que ara).
> Actualment hi ha un límit en la quantitat de vegades que pots desplaçar el focus en una mateixa direcció. S’hauria de poder fer indefinidament.
> El nom de la varietat a la llista de llengües ha d’estar escrit en una font de la mateixa mida que la del nom de la llengua.

**English translation:**

> The download-map options menu is currently larger than the screen at 100%; it needs to be made smaller. It should not increase its vertical length to accommodate the preview map, but it should increase horizontally (i.e., the opposite of how it works now).
> Currently there's a limit on how many times you can shift the focus in the same direction. It should be possible to do so indefinitely.
> The variety name in the language list should be written in a font the same size as the language name's font.

---

## Phase 4: InTyMaVi meets Glottolog and Grambank

**Comment:** After presenting InTyMaVi at APLL18, I got two very useful suggestions: using Glottolog coordinates instead of entering them manually into the spreadsheet and
importing Grambank data so that the user can view their own data in a wider typological context.

---

### 32. 2026-08-03

**Original:**

> Cal adaptar el programa perquè s'hi pugui importar un fitxer com aquest i extreure'n les coordenades. Quan l'excel importat amb les dades no contingui dades referents a les coordenades o aquestes no siguin vàlides, es recorrerà a les coordenades del fitxer .csv per ubicar el punt al mapa. Tot i així, si l'excel sí inclou llengües amb coordenades vàlides, es prendran sense atendre al fitxer .csv

**English translation:**

> The program needs to be adapted so that a file like this one can be imported and coordinates extracted from it. When the imported data Excel file doesn't contain coordinate data, or it's not valid, it will fall back on the coordinates from the .csv file to place the point on the map. Even so, if the Excel file does include languages with valid coordinates, those will be used without referring to the .csv file.

**Comment:** I attached the latest version of `languages_and_dialects_geo.csv`.

---

### 33. 2026-08-03

**Original:**

> Vull que l'usuari pugui descarregar qualsevol característica del grambank per contextualitzar-hi la seva mostra.

**English translation:**

> I want the user to be able to download any Grambank characteristic to put their sample in context.

---

### 34. 2026-08-03

**Original:**

> Les característiques del grambank s'han de poder solapar amb les de l'excel importat, sempre que les característiques d'aquest excel tinguin com a nom el mateix codi (p. ex. GB130)

**English translation:**

> The Grambank characteristics should be able to overlap with those in the imported Excel file, as long as the characteristics in that Excel file are named with the same code (e.g. GB130).

---


### 35. 2026-08-03

**Original:**

> S'ha de poder guardar (descarregar) un zoom concret per al mapa descarregable, de forma que aquest zoom es pugui tornar a carregar per a una major consistència entre els mapes descarregats

**English translation:**

> It should be possible to save (download) a specific zoom level for the downloadable map, so that this zoom can be reloaded later for greater consistency across downloaded maps.

---

### 36. 2026-08-06

**Original:**

> Canvis per al programa: Pel que fa al nom de la característica de Grambank, ha d’aparèixer el seu codi + nom tant a “Variable to display” com al títol de la llegenda del mapa descarregable, ja que actualment hi apareix només el codi i no s’entén què s’està visualitzant.
> La funció de guardar zoom i posició del mapa descarregat ha de ser completament precisa, actualment no ho és.
> La “language list” no s’ha d’encongir i, sobretot, no pot ser que, en fer scroll fins avall de tot, l’última llengua de la llista encara quedi fora del camp visual de la pantalla. Actualment passa.
> La preview de les ratio “portrait” i “phone screen” s’ha de eixamplar fins ocupar l’espai horitzontal dedicat a la preview.
> El programa ha de tenir un mode de pantalla completa.

**English translation:**

> Changes for the program: Regarding the name of the Grambank characteristic, its code + name should appear both in "Variable to display" and in the title of the downloadable map's legend, since currently only the code appears and it's unclear what's being displayed.
> The function to save the downloaded map's zoom and position needs to be completely accurate; currently it isn't.
> The "language list" should not shrink, and above all, it can't be that, when scrolling all the way down, the last language on the list still ends up outside the screen's visible area. This currently happens.
> The preview for the "portrait" and "phone screen" ratios should be widened until it fills the horizontal space dedicated to the preview.
> The program should have a full-screen mode.

---

### 37. 2026-08-10

**Original:**

> La “Language list” ha de tenir un 40% de l’extensió actual i ha de poder-se ampliar o encongir verticalment mantenint pulsat i arrossegant la línia divisòria amb l’apartat de la llegenda.

**English translation:**

> The "Language list" should be 40% of its current extent, and it should be possible to expand or shrink it vertically by pressing and dragging the dividing line with the legend section.

---

### 38. 2026-08-31

**Original:**

> Cal modificar InTyMaVi perquè en extreure les coordenades del document .csv funcioni també amb caràcters especials. Ara no detecta noms com Tupinambá o Önge, ja que al .csv hi apareixen com a TupinambÃ¡, Ã–nge

**English translation:**

> InTyMaVi needs to be modified so that, when extracting coordinates from the .csv file, it also works with special characters. Right now it doesn't detect names like Tupinambá or Önge, since in the .csv they appear as TupinambÃ¡, Ã–nge.

---

### 39. 2026-09-01

**Original:**

> El programa també t'ha de dir de quines llengües exactes no s'han pogut importar les coordenades

**English translation:**

> The program also needs to tell you exactly which languages' coordinates could not be imported.

---

### 40. 2026-09-01

**Original:**

> No, no cal. El mapa em carrega bastant lent. Com ho podríem arreglar? A part, els contorns dels països de color negre queden massa agressius, es podrien canviar per un color més clar?

**English translation:**

> No, that's not needed. The map loads quite slowly for me. How could we fix that? Also, the black country borders look too harsh; could they be changed to a lighter color?

---

### 41. 2026-09-01

**Original:**

> És molt important que la resolució sigui el millor possible, restableix-la a 10m

**English translation:**

> It's very important that the resolution be the best possible; reset it to 10m.

---

### 42. 2026-09-01

**Original:**

> Fes que la terra sigui de color blanc i l'aigua de color gris clar, tant al mapa interactiu com al descarregable

**English translation:**

> Make the land white and the water light gray, both on the interactive map and the downloadable one.

---

## Phase 5: InTyMaVi gets published

**Comment:** Every prompt from here onward was given originally in English. Uploading InTyMaVi to GitHub got me very useful feedback, which I used in order to further improve
the program. I am extremely thankful to everyone who emailed me or opened an issue suggesting changes.

### 43. 2026-09-05

**Original:**

> I need your help modifying InTyMaVi.
> The application uses a Natural Earth world map with Leaflet and GeoJSON. Currently, the map is Atlantic-centered, so the Pacific Ocean is split between the left and right edges.
> Some users would like to create and export Pacific-centered maps. My preferred solution would be to make the world map wrap or repeat horizontally, allowing users to pan freely and choose any longitude as the center.
> Implement it while preserving all existing functionality, including markers, labels, layers, zooming, panning, and map export.

**Comment:** wrapping the map horizontally worked, but made it too slow, so I came up with a different solution in the next prompt.

---

### 44. 2026-09-05

**Original:**

> Modify my program so users can choose between an Atlantic-centered (default) and Pacific-centered world map.
> The selected centering must apply to both the interactive map and exported maps.

---

### 45. 2026-09-05

**Original:**

> The Pacific-centered map is currently rendering incorrectly. As shown in the attached screenshot, several long horizontal lines are being drawn across the map, suggesting that some connectors or other overlays are not correctly handling the new central longitude and the map cut.
> Additionally, the Pacific-centered map should be cut at 30°W, meaning that 30°W should be used as the map's wrap/cut longitude.

---

### 46. 2026-09-06

**Original:**

> Although the problem with the Pacific-centered map has been fully solved, the Atlantic-centered map now shows two horizontal lines that weren't there before, as shown in the attached screenshot. Without changing anything about the Pacific-centered map, restore the Atlantic-centered map to its former appearance.

---

### 47. 2026-09-06

**Original:**

> Please modify the export functionality so that all downloaded images have a resolution of at least 300 × 300 DPI.

---

### 48. 2026-09-06

**Original:**

> When adding language names tags to the downloadable, uppercase M appears with two long "spikes" sticking out over it, as well as a small spike under it. Although less visibly, this also seems to be the case for V and W (both upper- and lowercase). Can you solve this issue?

---

### 49. 2026-09-06

**Original:**

> Add a "tiny" size option to the map download options.

---

### 50. 2026-09-06

**Original:**

> Every legend position option other than "top left" does not show any legend anywhere on the downloaded map.

**Comment:** Just a temporary bug that did not make it to any of the published versions.

---

### 51. 2026-09-07

**Original:**

> Could we use the Equal Earth map instead of the current Mercator?

---

### 52. 2026-09-07

**Original:**

> While this is not the case for the downloadable map, the interactive map is both mirrored and upside down. Additionally, the American continent in the Pacific-centred map is excessively deformed. Fix these issues.

---

### 53. 2026-09-08

**Original:**

> Add the world map options "Pacific-centered (Mercator)" and "Atlantic-centered (Mercator)", while keeping "Pacific-centered (Equal Earth)" as the default.

---

### 54. 2026-09-08

**Original:**

> Make "Atlantic-centered (Equal Earth)" the default, followed by "Pacific-centered (Equal Earth)", "Atlantic-centered (Mercator)" and "Pacific-centered (Mercator)"
