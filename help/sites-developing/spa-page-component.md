---
title: SPA-sidkomponent
seo-title: SPA-sidkomponent
description: I en SPA tillhandahåller inte sidkomponenten HTML-elementen för dess underordnade komponenter, utan delegerar i stället detta till SPA-ramverket. I det här dokumentet förklaras hur det gör sidkomponenten i en SPA unik.
seo-description: I en SPA tillhandahåller inte sidkomponenten HTML-elementen för dess underordnade komponenter, utan delegerar i stället detta till SPA-ramverket. I det här dokumentet förklaras hur det gör sidkomponenten i en SPA unik.
uuid: d444527a-e883-4873-a55b-c2bc140d8d7f
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6329301c-1a26-4a46-99ae-1b7cc15b08be
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# SPA-sidkomponent{#spa-page-component}

I en SPA tillhandahåller inte sidkomponenten HTML-elementen för dess underordnade komponenter, utan delegerar i stället detta till SPA-ramverket. I det här dokumentet förklaras hur det gör sidkomponenten i en SPA unik.

>[!NOTE]
>
>SPA-redigeraren är den rekommenderade lösningen för projekt som kräver SPA-ramverksbaserad rendering på klientsidan (t.ex. React eller Angular).

## Introduktion {#introduction}

Sidkomponenten för en SPA tillhandahåller inte HTML-elementen för dess underordnade komponenter via en JSP- eller HTML-fil och resursobjekt. Den här åtgärden har delegerats till SPA-ramverket. Representationen av underordnade komponenter hämtas som en JSON-datastruktur (d.v.s. modellen). SPA-komponenterna läggs sedan till på sidan enligt den angivna JSON-modellen. Det innebär att sidkomponentens inledande innehållsdisposition skiljer sig från dess förrenderade HTML-motsvarigheter.

## Sidmodellshantering {#page-model-management}

Sidmodellens upplösning och hantering delegeras till en angiven [`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) modul. SPA måste interagera med `PageModelManager` modulen när den initieras för att hämta den första sidmodellen och registrera sig för modelluppdateringar - oftast när författaren redigerar sidan via sidredigeraren. SPA-projektet `PageModelManager` är tillgängligt som npm-paket. Som tolk mellan AEM och SPA ska `PageModelManager` avtalet medfölja SPA.

För att sidan ska kunna redigeras måste ett klientbibliotek med namnet `cq.authoring.pagemodel.messaging` läggas till för att ge en kommunikationskanal mellan SPA och sidredigeraren. Om SPA-sidkomponenten ärver från sidans wcm/core-komponent finns det följande alternativ för att göra `cq.authoring.pagemodel.messaging` klientbibliotekskategorin tillgänglig:

* Om mallen är redigerbar lägger du till klientbibliotekskategorin i sidprincipen.
* Lägg till klientbibliotekskategorin med hjälp `customfooterlibs.html` av sidkomponenten.

Glöm inte att begränsa inkludering av `cq.authoring.pagemodel.messaging` kategorin till sidredigerarens kontext.

## Kommunikationsdatatyp {#communication-data-type}

Kommunikationsdatatypen ställs in på ett HTML-element i AEM Page-komponenten med hjälp av `data-cq-datatype` -attributet. När kommunikationens datatyp är JSON, når GET-förfrågningarna en komponents Sling Model-slutpunkter. När en uppdatering har gjorts i sidredigeraren skickas JSON-representationen av den uppdaterade komponenten till sidmodellsbiblioteket. Sidmodellbiblioteket varnar sedan SPA för uppdateringar.

**SPA-sidkomponent -`body.html`**

```
<div id="page"></div>
```

Förutom att vara god praxis att inte fördröja DOM-genereringen kräver SPA-ramverket att skripten läggs till i slutet av brödtexten.

**SPA-sidkomponent -`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

Meta-resursegenskaperna som beskriver SPA-innehållet:

**SPA-sidkomponent -`customheaderlibs.html`**

```
<meta property="cq:datatype" data-sly-test="${wcmmode.edit || wcmmode.preview}" content="JSON"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.edit}" content="edit"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.preview}" content="preview"/>
<meta property="cq:pagemodel_root_url" data-sly-use.page="com.adobe.cq.sample.spa.journal.models.AppPage" content="${page.rootUrl}"/>
<sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
    <sly data-sly-call="${clientlib.css @ categories='we-retail-journal-react'}"/>
</sly>
```

>[!NOTE]
>
>Standardmodellväljaren anges statiskt när Sling Model-representationen av en komponent begärs.

## Metaegenskaper {#meta-properties}

* `cq:wcmmode`: Redigerarnas WCM-läge (t.ex. sida, mall)
* `cq:pagemodel_root_url`: URL för appens rotmodell. Viktigt vid direkt åtkomst till en underordnad sida eftersom den underordnade sidmodellen är ett fragment av appens rotmodell. Därefter komponeras den inledande programmodellen om systematiskt när programmet anges från rotstartpunkten. ` [PageModelManager](/help/sites-developing/spa-page-component.md)`

* `cq:pagemodel_router`: Aktivera eller inaktivera ` [ModelRouter](/help/sites-developing/spa-routing.md)` funktionen för `PageModelManager` biblioteket

* `cq:pagemodel_route_filters`: Kommaavgränsad lista eller reguljära uttryck som tillhandahåller vägar som måste ignoreras ` [ModelRouter](/help/sites-developing/spa-routing.md)` .

## Synkronisering av sidredigeringsövertäckning {#page-editor-overlay-synchronization}

Synkroniseringen av övertäckningarna garanteras av exakt samma Mutation-observatör som finns i `cq.authoring.page` kategorin.

## Sling Model JSON Exported Structure Configuration {#sling-model-json-exported-structure-configuration}

När routningsfunktionerna är aktiverade antas att JSON-exporten av SPA innehåller de olika vägarna i programmet tack vare JSON-exporten av AEM-navigeringskomponenten. JSON-utdata för AEM-navigeringskomponenten kan konfigureras i SPA:s innehållsprincip för rotsidor via följande två egenskaper:

* `structureDepth`: Nummer som motsvarar djupet i det exporterade trädet
* `structurePatterns`: Regex för en matris med regexter som motsvarar den sida som ska exporteras

Detta kan visas i SPA-exempelinnehållet i `/conf/we-retail-journal/react/settings/wcm/policies/we-retail-journal/react/components/structure/page/root`.
