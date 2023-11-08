---
title: SPA sidkomponent
description: I en SPA tillhandahåller inte sidkomponenten elementen HTML i de underordnade komponenterna, utan delegerar i stället detta till det SPA ramverket. Det här dokumentet förklarar hur det gör sidkomponenten i ett SPA unik.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: 0e9e2350-67ef-45c3-991f-6c1cd98fe93d
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 0%

---

# SPA sidkomponent{#spa-page-component}

I en SPA tillhandahåller inte sidkomponenten elementen HTML i de underordnade komponenterna, utan delegerar i stället detta till det SPA ramverket. Det här dokumentet förklarar hur det gör sidkomponenten i ett SPA unik.

>[!NOTE]
>
>SPA Editor är den rekommenderade lösningen för projekt som kräver SPA ramverksbaserad rendering på klientsidan (till exempel React eller Angular).

## Introduktion {#introduction}

Sidkomponenten för en SPA tillhandahåller inte HTML-elementen för dess underordnade komponenter via en JSP- eller HTL-fil och resursobjekt. Den här åtgärden har delegerats till SPA ramverk. Representationen av underordnade komponenter hämtas som en JSON-datastruktur (d.v.s. modellen). De SPA komponenterna läggs sedan till på sidan enligt den angivna JSON-modellen. Det innebär att sidkomponentens ursprungliga brödkomposition skiljer sig från de förrenderade motsvarigheterna i HTML.

## Sidmodellshantering {#page-model-management}

Lösning och hantering av sidmodellen delegeras till en angiven [`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) -modul. SPA måste interagera med `PageModelManager` när det initieras för att hämta den första sidmodellen och registrera sig för modelluppdateringar - oftast när författaren redigerar sidan via sidredigeraren. The `PageModelManager` kan nås av SPA som ett npm-paket. Som tolk mellan AEM och SPA, `PageModelManager` är avsedd att medfölja SPA.

Om du vill tillåta att sidan kan redigeras, ett klientbibliotek med namnet `cq.authoring.pagemodel.messaging` måste läggas till för att en kommunikationskanal ska kunna skapas mellan SPA och sidredigeraren. Om den SPA sidkomponenten ärver från sidans wcm/core-komponent finns det följande alternativ för att skapa `cq.authoring.pagemodel.messaging` tillgänglig klientbibliotekskategori:

* Om mallen är redigerbar lägger du till klientbibliotekskategorin i sidprincipen.
* Lägg till klientbibliotekskategorin med `customfooterlibs.html` för sidkomponenten.

Glöm inte att begränsa möjligheten att inkludera `cq.authoring.pagemodel.messaging` till sidredigerarens kontext.

## Kommunikationsdatatyp {#communication-data-type}

Kommunikationsdatatypen ställs in på ett HTML-element i AEM Page-komponenten med hjälp av `data-cq-datatype` -attribut. När kommunikationsdatatypen är JSON, når GET-förfrågningarna en komponents Sling Model-slutpunkter. När en uppdatering har gjorts i sidredigeraren skickas JSON-representationen av den uppdaterade komponenten till sidmodellsbiblioteket. Sidmodellbiblioteket varnar sedan SPA om uppdateringar.

**SPA -`body.html`**

```
<div id="page"></div>
```

Förutom att vara god praxis att inte fördröja DOM-genereringen kräver SPA att skripten läggs till i slutet av brödtexten.

**SPA -`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

Meta-resursegenskaperna som beskriver SPA innehåll:

**SPA -`customheaderlibs.html`**

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

* `cq:wcmmode`: WCM-läge för redigerare (till exempel sida, mall)
* `cq:pagemodel_root_url`: URL för appens rotmodell. Viktigt vid direkt åtkomst till en underordnad sida eftersom den underordnade sidmodellen är ett fragment av appens rotmodell. The ` [PageModelManager](/help/sites-developing/spa-page-component.md)` disponerar sedan systematiskt om den inledande programmodellen när den anger programmet från dess rotstartpunkt.

* `cq:pagemodel_router`: Aktivera eller inaktivera ` [ModelRouter](/help/sites-developing/spa-routing.md)` i `PageModelManager` bibliotek

* `cq:pagemodel_route_filters`: Kommaseparerad lista eller reguljära uttryck som tillhandahåller vägar för ` [ModelRouter](/help/sites-developing/spa-routing.md)` måste ignorera.

>[!CAUTION]
>
>Det här dokumentet använder appen We.Retail Journal endast i demonstrationssyfte. Använd inte för projektarbete.
>
>Alla AEM ska använda [AEM Project Archettype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html), som stöder SPA projekt med React eller Angular och använder SPA SDK. Alla SPA projekt på AEM ska baseras på Maven Archetype för SPA Starter Kit.

## Synkronisering av sidredigeringsövertäckning {#page-editor-overlay-synchronization}

Synkroniseringen av övertäckningarna garanteras av samma Mutation-server som tillhandahålls av `cq.authoring.page` kategori.

## Sling Model JSON Exported Structure Configuration {#sling-model-json-exported-structure-configuration}

När routningsfunktionerna är aktiverade antas att JSON-exporten av SPA innehåller olika vägar för programmet tack vare JSON-exporten av den AEM navigeringskomponenten. JSON-utdata för den AEM navigeringskomponenten kan konfigureras i innehållsprincipen för SPA genom följande två egenskaper:

* `structureDepth`: Nummer som motsvarar djupet i det exporterade trädet
* `structurePatterns`: Regex för en matris av regexter som motsvarar den sida som ska exporteras

Detta kan visas i SPA exempelinnehåll i `/conf/we-retail-journal/react/settings/wcm/policies/we-retail-journal/react/components/structure/page/root`.
