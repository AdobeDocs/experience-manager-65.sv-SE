---
title: Introduktion till anpassning av arbetsytan i AEM-formulär
seo-title: Introduktion till anpassning av arbetsytan i AEM-formulär
description: En snabb introduktion med konceptuell och teknisk information för att anpassa arbetsytan i LiveCycle AEM Forms för processhantering.
seo-description: En snabb introduktion med konceptuell och teknisk information för att anpassa arbetsytan i LiveCycle AEM Forms för processhantering.
uuid: 38759071-e6b8-4976-8b06-909ad7a786cd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 021c6606-8cd3-472c-a80b-b1bcace7e87f
docset: aem65
translation-type: tm+mt
source-git-commit: 21623c615ebe69226cfaf84baf4cfb1717b449f4

---


# Introduktion till anpassning av arbetsytan i AEM-formulär{#introduction-to-customizing-aem-form-workspace}

AEM-formulärarbetsytan har funktioner för att ändra presentationssemantik och funktioner i gränssnittet. Typerna av anpassningar för att ändra format, layout, formatering, varumärke och grundfunktioner beskrivs nedan.

![cu_customized_workspace_example](assets/cu_customized_workspace_example.png)

Ett exempel på en anpassad arbetsyta

## Typer av anpassningar {#types-of-customizations}

Arbetsytan i AEM Forms har stöd för en mängd anpassningar för att uppdatera användargränssnittets layout, utseende, funktioner och mycket annat. Anpassningarna innefattar att uppdatera ett eller flera av följande:

* Användargränssnittets utseende
* Funktioner som använder semantiska anpassningar
* Återanvända HTML-komponenter i andra program

### Ändringar i användargränssnittet {#user-interface-changes}

Du kan ändra utseende, layout och andra presentationssemantik för arbetsytan i AEM Forms. Ändra arbetsyta genom att anpassa CSS-, HTML-mallar och JavaScript™-filer. Alla standardfiler finns i standardinstallationen.

De vanligaste stegen beskrivs i [Allmänna steg för anpassning](../../forms/using/generic-steps-html-workspace-customization.md)av arbetsytan i AEM Forms. Specifika exempel på sådana anpassningar, inklusive detaljerade steg, finns i de relaterade artiklarna i slutet av den här artikeln.

#### Förstå formatmallen {#understanding-the-style-sheet}

Innan du anpassar arbetsytan bör du bekanta dig med den standardformatmall som finns i AEM Forms på /libs/ws/css/style.css.

Om du vill anpassa arbetsytan bör du bekanta dig med den befintliga formatmallen, style.css, som finns i mappen /libs/ws/css. Nedan beskrivs några viktiga komponenter.

<table>
 <tbody>
  <tr>
   <th><p>CSS-element</p> </th>
   <th><p>Användargränssnittskomponenten har ändrats</p> </th>
  </tr>
  <tr>
   <td><p>#header</p> </td>
   <td><p>Sidhuvud på arbetsytan för AEM-formulär</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList</p> </td>
   <td><p>Kategorilista</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList.header</p> </td>
   <td><p>Rubrik för kategorilista</p> </td>
  </tr>
  <tr>
   <td><p>.categories, .filters</p> </td>
   <td><p>Avstånd nedanför kategorilistan</p> </td>
  </tr>
  <tr>
   <td><p>.category, .filter</p> </td>
   <td><p>Kategori</p> </td>
  </tr>
  <tr>
   <td><p>.category:hover, .category.selected, .filter:hover, .filter.selected</p> </td>
   <td><p>Markerad kategori och typ av hovring över-kategori</p> </td>
  </tr>
  <tr>
   <td><p>categoryListBar.tool, categoryListBar.content</p> </td>
   <td><p>Startprocesssida (stängd kategorilista)</p> </td>
  </tr>
  <tr>
   <td><p>filterListBar.tool, filterListBar.content</p> </td>
   <td><p>Att göra-sida (sluten filterlista)</p> </td>
  </tr>
  <tr>
   <td><p>processNameListBar.tool, processNameListBar.content</p> </td>
   <td><p>Spårningssida (namnlista för stängd process)</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList, .tasklist</p> </td>
   <td><p>Startpunktslistan eller uppgiftslistan</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList.header, .tasklist.header</p> </td>
   <td><p>Huvudet för en startpunktslista eller en uppgiftslista</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected, .task.selected</p> </td>
   <td><p>Den valda startpunkten eller uppgiften</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected.description, .task.selected.description</p> </td>
   <td><p>Beskrivning av den valda startpunkten eller uppgiften</p> </td>
  </tr>
  <tr>
   <td><p>#taskarea</p> </td>
   <td><p>Åtgärdsområdet</p> </td>
  </tr>
  <tr>
   <td><p>#header.dropdown</p> </td>
   <td><p>Listrutan Användare i rubriken</p> </td>
  </tr>
  <tr>
   <td><p>.sortDrop dd ul</p> </td>
   <td><p>Sorteringsaktivitetslistruta</p> </td>
  </tr>
 </tbody>
</table>

#### CSS {#css}

Utseendet på arbetsytan i AEM Forms lånar utseendet från en CSS. Genom att anpassa CSS kan du ändra presentationssemantik för arbetsytan, som teckensnitt, färger, varumärke och layout.

De översta stegen för CSS-anpassning är:

* Skapa en CSS-fil.
* Lägg till formatobjekt i denna CSS. Mer information finns i Förstå CSS-format.
* Uppdatera referenserna i `html.jsp`.

Exakt hur du gör dessa anpassningar finns i [Allmänna steg för anpassning](../../forms/using/generic-steps-html-workspace-customization.md)av arbetsytan i AEM Forms. CSS-filen som levereras med arbetsytan AEM Forms finns på /libs/ws/css/. Använd [leveranspaketet](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)för CSS-relaterade anpassningar. Specifika exempel på CSS-relaterade anpassningar finns i de relaterade hjälpavsnitten i slutet av den här artikeln.

#### Bild {#image}

Du kan anpassa arbetsytan i AEM Forms för att lägga till olika användare eller för att lägga till organisationens logotyp. Använd [Ship Package](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)för dessa anpassningar.

De översta stegen för anpassning av bilderna är:

* Installera och konfigurera WebDAV.
* Lägg till nya bilder.
* Lägg till nya format som motsvarar de tillagda bilderna.
* Länka till den nya CSS-filen i `html.jsp` filen.

Om du vill komma igång med att anpassa bilderna på arbetsytan i AEM Forms följer du de [allmänna stegen för anpassning](../../forms/using/generic-steps-html-workspace-customization.md)av arbetsytan i AEM Forms. Specifika exempel på bildrelaterade anpassningar finns i de relaterade hjälpavsnitten i slutet av den här artikeln.

#### HTML-mall {#html-template}

HTML-mallar hjälper till att definiera utseendet och layouten för arbetsytans användargränssnitt. Genom att uppdatera HTML-standardmallarna kan du anpassa standardgränssnittet för layouten.

De översta stegen för anpassning av HTML-mallen är:

* Skapa kopior av de standardfiler som behövs i en mapp som skapats av användaren.
* Lägg till nya mallar i en användardefinierad mapp.
* Gör relevanta uppdateringar av de kopierade filerna, som sökvägen till den nya mallen.

Specifika exempel på sådana anpassningar finns i hjälpavsnitten i slutet av den här artikeln. Välj mellan [Ship Package](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p) eller [Dev Package](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p), beroende på vilken mall som ska anpassas.

### Semantiska ändringar {#semantic-changes}

Ändra JavaScript-källkoden om du vill ändra AEM Forms-arbetsytans funktioner. Ändringarna i kärnfunktionen kallas Semantiska ändringar. Du kan ändra modeller, vyer och mallar som ingår i källkoden för arbetsytan i AEM Forms.

De översta stegen för att göra semantiska ändringar för att ändra funktionaliteten i AEM Forms-arbetsytan är:

* Skapa kopior av standardfilerna i en mapp som skapas av användaren.
* Lägg till nya modeller och vyer i den användardefinierade mappen.
* Gör relevanta uppdateringar, som att uppdatera sökvägar för nytillagda modeller och vyer i JavaScript-standardfilerna.
* Minimera paketet för att optimera prestanda.

Mer konceptuell information om komponenterna som är en del av källkoden finns i [Beskrivningen av återanvändbara komponenter](/help/forms/using/description-reusable-components.md). Använd Dev Package för dessa anpassningar.

### Återanvändbara komponenter {#reusable-components}

Eftersom AEM Forms-arbetsytan är ett komponentbaserat program kan den enkelt anpassas och återanvändas. Du kan enkelt integrera arbetsytekomponenterna med dina webbprogram.

Mer konceptuell information finns i [Beskrivning av återanvändbara komponenter](/help/forms/using/description-reusable-components.md) och instruktioner om hur du använder komponenterna finns i [Integrera AEM Forms-arbetsytekomponenter i webbprogram](/help/forms/using/description-reusable-components.md).

## Skapar kod för arbetsytan i AEM Forms {#building-html-workspace-code}

### SDK-paket {#sdk-package}

Paketet innehåller källkoden för AEM Forms-arbetsytan. Paketet finns på `[LC root]\sdk\html-workspace\adobe-lc-workspace-src.zip`.

Det är främst avsett för anpassningar, eftersom det ger möjlighet att generera:

* CRX-paket för Ship-, Debug- och Dev-profiler (anges nedan i [CRX-paket](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)).
* Minimerad version av anpassad kod (för semantiska ändringar).

#### WS-innehåll {#ws-content}

* client-pkg:

   * src - Innehåller artefakter som behövs för att skapa CRX-noder.
   * pom.xml - Skript för att skapa distributionspaket för olika profiler WS-Deploy Package

* client-html:

   * assembly - Innehåller zip.xml som används av skript för att skapa SDK för arbetsytan AEM Forms.
   * src/main/webapp -

      * css - Innehåller formatmallar för AEM Forms-arbetsytan.
      * bilder - Innehåller bilder som används på arbetsytan i AEM Forms.
      * js:

         * libs - Innehåller alla tredjepartsbibliotek som används i AEM Forms-arbetsytan.
         * licenser - Innehåller licenser för HTML- och JS-filer samt kod som prefix till dessa licenser för respektive källfil.
         * minifier - Används för kombination, minifiering och uppgradering av anpassad javascript-kod.
         * resourcejs_optimizer - Används för kombination, minimering och uglifiering av javascript-källa.
         * resource_generator - Används för att generera register.js och modelcontroller.path.js.
         * runtime:

            * initierare - Innehåller initierare.js som används för att initiera stambentytor och modeller som används på arbetsytan i AEM Forms.
            * modeller - Innehåller stammodeller av alla komponenter som finns på arbetsytan i AEM Forms.
            * vägar - Innehåller javascript-filer och HTML-filer som läser in startprocess, att göra, spåra och inställningar på arbetsytan i AEM Forms.
            * services - Innehåller service.js som används på arbetsytan i AEM Forms. Alla serveranrop görs via service.js.
            * mallar - Innehåller alla mallar, det vill säga HTML-filer av alla vyer på arbetsytan i AEM Forms.
            * util - Innehåller alla verktygsfiler (javascript) som används i AEM Forms-arbetsytan.
            * vyer - Innehåller ryggradsvyer av alla komponenter på arbetsytan i AEM Forms.
         * main.js
         * router.js
      * libs/ws: pdf.html och pluginPing.pdf används för att läsa in PDF-formulär i AEM Forms-arbetsytan, och WSNextAdapter.swf används för att läsa in SWF-formulär och stödlinjer i AEM Forms-arbetsytan.
      * nationella inställningar:

         * de-DE - Innehåller translation.json för tyska.
         * en-US - Innehåller translation.json för engelska.
         * fr-FR - Innehåller translation.json för franska.
         * ja-JP - Innehåller translation.json för japanska.
         * html.jsp - Innehåller kod för att ta reda på webbläsarens aktuella språkområde.
      * html.jsp
      * GET.jsp




### CRX-paket {#crx-package}

CRX-paketet kan distribueras i CRX™-databasen. Den finns på `[LC root]\crx-repository\install\adobe-lc-workspace-pkg.zip`.

Paketet kan byggas med de tre profiler som beskrivs nedan.

| **Profil** | **Beskrivning** | **Användning** |
|---|---|---|
| Leveransprofil | Den här profilen skapar ett CRX-paket med minsta möjliga storlek med hjälp av miniatyrbilder. Det här paketet är mest effektivt. Alla JavaScript™-filer kombineras och minieras till en enda JS-fil. | Använd den här profilen när inga ytterligare semantiska ändringar krävs i JS-filer. |
| Felsökningsprofil | Den här profilen skapar ett måttligt effektivt CRX-paket. Paketets storlek är något större än det paket som skapats med Ship-profilen. Det här paketet innehåller de flesta JavaScript-filer som kombineras till en enda JS-fil. | Använd den här profilen för felsökning. |
| Dev-profil | Den här profilen skapar ett CRX-paket med största möjliga storlek. Alla JavaScript-filer är tillgängliga separat, som de är i SDK-paketet. | Använd den här profilen när du inkluderar semantiska ändringar. |

#### Leveransprofil {#ship-profile}

#### Command {#command}

* mvn clean -P Ship install on client-pkg folder of Source package shipping to client.
* Kommandokörning av Ship-profil fungerar bara på en 64-bitars JVM.

#### WS-innehåll {#ws-content-1}

* css - Innehåller style.css, ie.css och jquery-ui.css.
* bilder - Innehåller alla bilder.
* js:

   * libs:

      * require - Contains require.js.
      * jqueryui - Innehåller jquery.ui.datepicker.ja.js.
   * runtime:

      * mallar - Innehåller alla mallar, det vill säga HTML-filer för alla komponenter i AEM Forms-arbetsytan.
   * main.js (kombinerat, minifierat och uglifierat).
   * register.js



* libs:

   * ws - Innehåller pluginPing.pdf, pdf.html och WSNextAdapter.swf.

* Språk - innehåller .content.xml.
* nationella inställningar:

   * de-DE - Innehåller translation.json för tyska.
   * en-US - Innehåller translation.json för engelska.
   * fr-FR - Innehåller translation.json för franska.
   * ja-JP - Innehåller translation.json för japanska.
   * html.jsp - Innehåller kod för att ta reda på webbläsarens aktuella språkområde.

* Index - innehåller .content.xml
* profile - Innehåller offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Felsökningsprofil {#debug-profile}

#### Command {#command-1}

* mvn ren -P Felsökningsinstallation på klient-pkg
* Kommandokörning av felsökningsprofiler fungerar bara på 64-bitars JVM.

#### WS-innehåll {#ws-content-2}

* css - Innehåller style.css, ie.css och jqueri-ui.css.
* bilder - Innehåller alla bilder.
* js:

   * libs:

      * require - Contains require.js.
      * jqueryui - Innehåller jquery.ui.datepicker.ja.js.
   * runtime:

      * mallar - Innehåller alla mallar, det vill säga HTML-filer för alla komponenter i AEM Forms-arbetsytan.
   * main.js (kombinerat).
   * register.js



* libs:

   * ws - Innehåller pluginPing.pdf, pdf.html och WSNextAdapter.swf.

* Språk - innehåller .content.xml.
* nationella inställningar:

   * de-DE - Innehåller translation.json för tyska.
   * en-US - Innehåller translation.json för engelska.
   * fr-FR - Innehåller translation.json för franska.
   * ja-JP - Innehåller translation.json för japanska.
   * html.jsp - Innehåller kod för att ta reda på webbläsarens aktuella språkområde.

* Index - innehåller .content.xml
* profile - Innehåller offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Dev-profil {#dev-profile}

#### Command {#command-2}

mvn clean -P Dev install on client-pkg

#### WS-innehåll {#ws-content-3}

* css - Innehåller style.css, ie.css och jqueri-ui.css.
* bilder - Innehåller alla bilder.
* js:

   * libs - Innehåller alla bibliotek som används i AEM Forms-arbetsytan.
   * require - Contains require.js
   * jqueryui - innehåller jquery.ui.datepicker.ja.js
   * runtime:

      * initierare - Innehåller initializer.js och modelcontroller.path.js.
      * modeller - Innehåller modeller av alla komponenter på arbetsytan i AEM Forms.
      * vägar - Innehåller javascript-filer och HTML-filer som läser in startprocess, att göra, spåra och inställningar på arbetsytan i AEM Forms.
      * services - Innehåller service.js som används på arbetsytan i AEM Forms.
      * mallar - Innehåller alla mallar, det vill säga HTML-filer för alla komponenter i AEM Forms-arbetsytan.
      * util - Innehåller alla verktygsfiler (JavaScript) som används i AEM Forms-arbetsytan.
      * vyer - Innehåller vyer över alla komponenter på arbetsytan i AEM Forms.
   * main.js
   * register.js
   * router.js


* libs:

   * ws - Innehåller pluginPing.pdf, pdf.html och WSNextAdapter.swf.

* Språk - innehåller .content.xml.
* nationella inställningar:

   * de-DE - Innehåller translation.json för tyska.
   * en-US - Innehåller translation.json för engelska.
   * fr-FR - Innehåller translation.json för franska.
   * ja-JP - Innehåller translation.json för japanska.
   * html.jsp - Innehåller kod för att ta reda på webbläsarens aktuella språkområde.

* Index - innehåller .content.xml
* profile - Innehåller offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
