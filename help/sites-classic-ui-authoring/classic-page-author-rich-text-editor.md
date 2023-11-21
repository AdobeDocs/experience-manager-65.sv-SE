---
title: RTF-redigerare
description: RTF-redigeraren är en grundläggande byggsten för att infoga textinnehåll i AEM.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
docset: aem65
exl-id: 5623dcf4-bda9-4dee-ace3-5a1f6057e96c
source-git-commit: 7d46ba0eaa73d9f7a67034ba81d7fa379aa0112c
workflow-type: tm+mt
source-wordcount: '1823'
ht-degree: 0%

---

# RTF-redigerare {#rich-text-editor}

RTF-redigeraren är en grundläggande byggsten för att infoga textinnehåll i AEM. Den utgör grunden för olika komponenter, bland annat följande:

* Text
* Textbild
* Tabell

## RTF-redigerare {#rich-text-editor-1}

Dialogrutan för WYSIWYG-redigering innehåller många olika funktioner:

![cq55_rte_basicchars](assets/cq55_rte_basicchars.png)

>[!NOTE]
>
>De tillgängliga funktionerna kan konfigureras för enskilda projekt, så de kan variera för din installation.

## Direktredigering {#in-place-editing}

Förutom det dialogbaserade läget för textredigering i Rich Text, innehåller AEM även redigeringsläget på plats, som tillåter direkt redigering av texten så som den visas i sidlayouten.

Klicka två gånger på ett stycke (ett långsamt dubbelklick) för att gå in i redigeringsläget (komponentens kantlinje är nu orange).

Du kan redigera texten direkt på sidan i stället för i ett dialogrutefönster. Gör bara dina ändringar så sparas de automatiskt.

![cq55_rte_inlineediting](assets/cq55_rte_inlineediting.png)

>[!NOTE]
>
>Om du har innehållshanteraren öppen visas ett verktygsfält med formateringsalternativen för textredigering överst på fliken (enligt ovan).
>
>Om innehållssökaren inte är öppen visas inte verktygsfältet.

För närvarande är läget Redigering på plats aktiverat för sidelement som genereras av **Text** och **Titel** -komponenter.

>[!NOTE]
>
>The [!UICONTROL Title] -komponenten är utformad för att innehålla en kort text utan radbrytningar. När du redigerar en titel i läget för infogad redigering öppnas en ny radbrytning **Text** -komponenten under rubriken.

## Funktioner i RTF-redigeraren {#features-of-the-rich-text-editor}

RTF-redigeraren har en rad funktioner, som [beroende på konfigurationen](/help/sites-administering/rich-text-editor.md) för den enskilda komponenten. Funktionerna är tillgängliga för både pekoptimerade och klassiska användargränssnitt.

### Grundläggande teckenformat {#basic-character-formats}

![Verktygsfältet Teckenformat](do-not-localize/cq55_rte_basicchars.png)

Här kan du formatera tecken som du har markerat (markerat). Vissa alternativ har även kortkommandon:

* Fet (Ctrl-B)
* Kursiv (Ctrl-I)
* Understruken (Ctrl-U)
* Nedsänkt
* Upphöjd

![cq55_rate_basicchars_use](assets/cq55_rte_basicchars_use.png)

Alla fungerar som en växlingsknapp, så om du väljer det tas formatet bort.

### Fördefinierade format och format {#predefined-styles-and-formats}

![cq55_rte_stylesparagraph](assets/cq55_rte_stylesparagraph.png)

Installationen kan innehålla fördefinierade format och format. Dessa finns i **[!UICONTROL Style]** och **[!UICONTROL Format]** nedrullningsbara listor och kan användas på text som du har valt.

Ett format kan användas på en viss sträng (ett format korrelerar till CSS):

![cq55_rate_styles_use](assets/cq55_rte_styles_use.png)

Ett format tillämpas på hela textstycket (ett format är HTML-baserat):

![cq55_rte_paragraph_use](assets/cq55_rte_paragraph_use.png)

Ett specifikt format kan bara ändras (standardvärdet är **[!UICONTROL Paragraph]**).

Ett format kan tas bort. Placera markören i texten som formatet har tillämpats på och klicka på ikonen Ta bort:

>[!CAUTION]
>
>Markera inte om någon text som formatet har tillämpats på eller så inaktiveras ikonen.

### Klipp ut, Kopiera, Klistra in {#cut-copy-paste}

![Verktygsfältet Klipp ut, Kopiera, Klistra in](do-not-localize/cq55_rte_cutcopypaste.png)

Standardfunktionerna i **[!UICONTROL Cut]** och **[!UICONTROL Copy]** är tillgängliga. Flera smaker av **[!UICONTROL Paste]** finns för olika format.

* Klipp ut (Ctrl-X)
* Kopiera (Ctrl-C)
* Klistra in Det här är standardmekanismen för inklistring (Ctrl-V) av komponenten. När den är installerad utanför rutan är den konfigurerad att [!UICONTROL Paste from Word].

* Klistra in som text: Tar bort alla format och formatering så att endast den oformaterade texten klistras in.

* Klistra in från Word: Innehållet klistras in som HTML (med viss nödvändig formatering).

### Ångra, Gör om {#undo-redo}

![Verktygsfältet Ångra, Gör om](do-not-localize/cq55_rte_undoredo.png)

AEM sparar information om dina senaste 50 åtgärder i den aktuella komponenten, som hålls i kronologisk ordning. Dessa åtgärder kan ångras (och sedan göras om) i strikt ordning om det behövs.

>[!CAUTION]
>
>Historiken sparas bara för den aktuella redigeringssessionen. Den startas om varje gång du öppnar komponenten för redigering.

>[!NOTE]
>
>Femtio är standardantalet uppgifter. Detta kan vara annorlunda för din installation.

### Justering {#alignment}

![Justering (verktygsfält)](do-not-localize/cq55_rte_alignment.png)

Texten kan antingen vara vänsterjusterad, centrerad eller högerjusterad.

![cq55_rate_alignment_use](assets/cq55_rte_alignment_use.png)

### Indrag {#indentation}

![Verktygsfältet Indrag](do-not-localize/cq55_rte_indent.png)

Indraget för ett stycke kan ökas eller minskas. Det markerade stycket dras in och ny text som matas in behåller den aktuella indragsnivån.

![cq55_te_indent_use](assets/cq55_rte_indent_use.png)

### Listor {#lists}

![Visar verktygsfältet](do-not-localize/cq55_rte_lists.png)

Du kan skapa både punktlistor och numrerade listor i texten. Välj listtyp och börja skriva eller markera texten som ska konverteras. I båda fallen startar en radmatning ett nytt listobjekt.

Du kan skapa kapslade listor genom att dra in ett eller flera listobjekt.

Du kan ändra formatet på en lista genom att placera markören i listan och sedan välja det andra formatet. En underlista kan också ha ett annat format än innehållslistan. Detta kan användas när underlistan har skapats (med indrag).

![cq55_rte_lists_use](assets/cq55_rte_lists_use.png)

### Länkar {#links}

![Verktygsfältet Länkar](do-not-localize/cq55_rte_links.png)

En länk till en URL-adress (antingen på din webbplats eller på en extern plats) skapas genom att markera texten och sedan klicka på hyperlänkikonen:

![Ikon för hyperlänk](do-not-localize/chlimage_1-9.png)

I en dialogruta kan du ange mål-URL:en och även ange om den ska öppnas i ett nytt fönster.

![cq55_rte_link_use](assets/cq55_rte_link_use.png)

Du kan:

* Skriv in en URI direkt
* Använd webbplatskartan för att välja en sida på webbplatsen
* Ange URI:n och lägg sedan till målankarpunkten, till exempel `www.TargetUri.org#AnchorName`
* Ange endast en ankarpunkt (för att referera till&quot;den aktuella sidan&quot;), till exempel `#anchor`
* Söka efter en sida i innehållssökaren och dra och släpp sidikonen i hyperlänksdialogrutan

>[!NOTE]
>
>URI:n kan prepended med vilket som helst av de protokoll som är konfigurerade för din installation. I en standardinstallation finns följande `https://`, `ftp://`och `mailto:`. Protokoll som inte har konfigurerats för din installation kommer att avvisas och markeras som ogiltiga.

Om du vill bryta länken placerar du markören någonstans i länktexten och klickar på knappen [!UICONTROL Unlink] ikon:

![Ikonen Bryt länk](do-not-localize/chlimage_1-10.png)

### Fästpunkter {#anchors}

![Verktygsfältet Ankarpunkter](do-not-localize/cq55_rte_anchor.png)

Du kan skapa en ankarpunkt var som helst i texten genom att antingen placera markören eller markera text. Klicka sedan på **Ankarpunkt** för att öppna dialogrutan.

Ange namnet på ankarpunkten och klicka sedan **OK** att spara.

![cq55_rte_anchor_use](assets/cq55_rte_anchor_use.png)

Fästpunkten visas när komponenten redigeras och kan nu användas inom ett länkmål.

![chlimage_1-104](assets/chlimage_1-104.png)

### Sök och ersätt {#find-and-replace}

![Verktygsfältet Sök och ersätt](do-not-localize/cq55_rte_findreplace.png)

AEM tillhandahåller båda **Sök** och **Ersätt** funktionen (sök och ersätt).

Båda har en **Sök nästa** om du vill söka efter den angivna textens öppna komponent. Du kan också ange om du vill att skiftläget (övre/nedre) ska matchas.

Sökningen startar alltid från den aktuella markörpositionen i texten. När komponentens slut nås visas ett meddelande om att nästa sökåtgärd kommer att starta uppifrån.

![cq55_rte_find_use](assets/cq55_rte_find_use.png)

The **Ersätt** kan du **Sök** sedan **Ersätt** en enskild instans med den angivna texten, eller till **Ersätt alla** -instanser i den aktuella komponenten.

![cq55_rte_findreplace_use](assets/cq55_rte_findreplace_use.png)

### Bilder {#images}

Du kan dra bilder från innehållssökaren för att lägga till dem i texten.

![cq55_rate_image_use](assets/cq55_rte_image_use.png)

>[!NOTE]
>
>AEM erbjuder också specialkomponenter för mer detaljerad bildkonfiguration. Till exempel **Bild** och **Textbild** finns tillgängliga.

### Stavningskontroll {#spelling-checker}

![Stavningskontroll](do-not-localize/cq55_rte_spellchecker.png)

Stavningskontrollen kontrollerar all text i den aktuella komponenten.

Felaktiga stavningar kommer att markeras:

![cq55_rte_spellchecker_use](assets/cq55_rte_spellchecker_use.png)

>[!NOTE]
>
>Stavningskontrollen fungerar på webbplatsens språk antingen genom att använda underträdets language-egenskap eller genom att extrahera språket från URL:en. Till exempel `en` kommer att kontrolleras för engelska och `de` för tyska.

### Tabeller {#tables}

Tabeller är tillgängliga båda:

* Som **Tabell** komponent

  ![Tabellkomponent](assets/chlimage_1-105.png)

* Från **Text** komponent

  ![Verktygsfältet Text](do-not-localize/chlimage_1-11.png)

  >[!NOTE]
  >
  >Även om tabeller är tillgängliga i RTE bör du använda **Tabell** -komponenten när du skapar tabeller.

I båda **Text** och **Tabell** funktionaliteten i komponenttabellen är tillgänglig via snabbmenyn (oftast högermusknappen) som klickas i tabellen, till exempel:

![cq55_rte_tablemenu](assets/cq55_rte_tablemenu.png)

>[!NOTE]
>
>I **Tabell** finns det också ett specialverktygsfält, som innehåller olika RTF-redigeringsfunktioner och en delmängd av de tabellspecifika funktionerna.

Tabellspecifika funktioner är:

* [Tabellegenskaper](#table-properties)
* [Cellegenskaper](#cell-properties)
* [Lägg till eller ta bort rader](#add-or-delete-rows)
* [Lägg till eller ta bort kolumner](#add-or-delete-columns)
* [Markera hela rader eller kolumner](#selecting-entire-rows-or-columns)
* [Sammanfoga celler](#merge-cells)
* [Dela celler](#split-cells)
* [Kapslade tabeller](#creating-nested-tables)
* [Ta bort tabell](#remove-table)

#### Tabellegenskaper {#table-properties}

![cq55_rte_tableproperties_icon](assets/cq55_rte_tableproperties_icon.png)

Tabellens grundläggande egenskaper kan konfigureras innan du klickar på **OK** att spara:

![cq55_rte_tableproperties_dialog](assets/cq55_rte_tableproperties_dialog.png)

* **Bredd**: Tabellens totala bredd.

* **Höjd**: Tabellens totala höjd.

* **Kant**: Tabellkantens storlek.

* **Cellutfyllnad**: Detta definierar det tomma utrymmet mellan cellinnehållet och dess kanter.

* **Cellmellanrum**: Detta definierar avståndet mellan cellerna.

>[!NOTE]
>
>Vissa cellegenskaper, som Bredd och Höjd, kan definieras som pixlar eller som procentvärden.

>[!CAUTION]
>
>Adobe rekommenderar att du anger en bredd för tabellen.

#### Cellegenskaper {#cell-properties}

![cq55_rte_cellproperties_icon](assets/cq55_rte_cellproperties_icon.png)

Egenskaperna för en viss cell, eller serie med celler, kan konfigureras:

![cq55_rte_cellproperties_dialog](assets/cq55_rte_cellproperties_dialog.png)

* **Bredd**
* **Höjd**
* **Vågrät justering** - Vänster, Centrera eller Höger
* **Lodrät justering** - Överkant, Mitten, Nederkant eller Baslinje
* **Celltyp**- Data eller rubrik
* **Använd för:** En cell, Hela raden, Hela kolumnen

#### Lägg till eller ta bort rader {#add-or-delete-rows}

![cq55_rte_rows](assets/cq55_rte_rows.png)

Rader kan läggas till antingen ovanför eller under den aktuella raden.

Den aktuella raden kan också tas bort.

#### Lägg till eller ta bort kolumner {#add-or-delete-columns}

![cq55_rte_columns](assets/cq55_rte_columns.png)

Du kan lägga till kolumner till vänster eller höger om den aktuella kolumnen.

Den aktuella kolumnen kan också tas bort.

#### Markera hela rader eller kolumner {#selecting-entire-rows-or-columns}

![chlimage_1-106](assets/chlimage_1-106.png)

Markerar hela den aktuella raden eller kolumnen. Specifika åtgärder (till exempel sammanfogning) är sedan tillgängliga.

#### Sammanfoga celler {#merge-cells}

![cq55_rte_cellmerge](assets/cq55_rte_cellmerge.png) ![cq55_rte_cellmerge-1](assets/cq55_rte_cellmerge-1.png)

* Om du har markerat en grupp celler kan du sammanfoga dessa till en.
* Om du bara har markerat en cell kan du sammanfoga den med cellen till höger eller nedanför.

#### Dela celler {#split-cells}

![cq55_rte_cellsplit](assets/cq55_rte_cellsplit.png)

Markera en enskild cell för att dela den:

* Om du delar en cell vågrätt skapas en ny cell till höger om den aktuella cellen, i den aktuella kolumnen.
* När du delar en cell lodrätt genereras en ny cell under den aktuella cellen, men inom den aktuella raden.

#### Skapa kapslade tabeller {#creating-nested-tables}

![chlimage_1-107](assets/chlimage_1-107.png)

När du skapar en kapslad tabell skapas en tabell i den aktuella cellen som innehåller en egen tabell.

>[!NOTE]
>
>Viss ytterligare beteende är webbläsarberoende:
>
>* Windows IE: Använd Ctrl+primär musknapp-klicka (vanligtvis vänster) för att markera flera celler.
>* Firefox: Dra pekaren för att markera ett cellområde.

#### Ta bort tabell {#remove-table}

![cq55_rte_removetable](assets/cq55_rte_removetable.png)

Använd alternativet för att ta bort tabellen från **[!UICONTROL Text]** -komponenten.

### Specialtecken {#special-characters}

![Verktygsfältet Specialtecken](do-not-localize/cq55_rte_specialchars.png)

Specialtecken kan göras tillgängliga för textredigeraren. De kan variera beroende på installationen.

![cq55_rte_specialchars_use](assets/cq55_rte_specialchars_use.png)

Använd muspekaren för att se en förstorad version av tecknet och klicka sedan för att det ska tas med på den aktuella platsen i texten.

### Källredigeringsläge {#source-editing-mode}

![Verktygsfältet för källredigeringsläge](do-not-localize/cq55_rte_sourceedit.png)

I källredigeringsläget kan du visa och redigera komponentens underliggande HTML.

Så texten:

![cq55_te_sourcemode_1](assets/cq55_rte_sourcemode_1.png)

Ser ut så här i källäge (källan är ofta mycket längre, så du måste rulla):

![cq55_te_sourcemode_2](assets/cq55_rte_sourcemode_2.png)

>[!CAUTION]
>
>När du lämnar källäget utför AEM vissa valideringskontroller (t.ex. ser du till att texten är korrekt innesluten/kapslad i block). Detta kan leda till ändringar i dina redigeringar.
