---
title: Versionsinformation för AEM Sites
description: Versionsinformation om webbplatser som tillhör Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: 23656e023a9a0bfc335655f9cfb0530aa917b3ef
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 0%

---


# Versionsinformation för AEM Sites {#aem-sites-release-notes}

Se följande för AEM Sites 6.5-förbättringar i detalj:

## Utveckling av komponenter och mallar {#component-amp-template-development}

* Maven Project Archetype 18+ för nya projekt, se [Github för versionsinformation](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/releases).
* Single-page App Maven Project Archetype 1.0.6+ för nya projekt, se [Github för versionsinformation](https://github.com/adobe/aem-spa-project-archetype/releases).
* HTML version 1.4, se [Github för versionsinformation](https://github.com/adobe/htl-spec/releases/tag/1.4).

   * operatorn &quot;in&quot; för strängar, arrayer och objekt:

      ```html
      ${'a' in 'abc’}
      ${100 in myArray}
      ${'a' in myObject}
      ```

   * Variabeldeklarationer med datavänligt angivna:
      `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * Lista och upprepa kontrollparametrar: begin, step, end:
      `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * Identifierare för automatisk uppbrytning av data:

      ```html
      <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
      text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
      </div>
      ```

   * Stöd för negativa tal

* Core Components 2.3.2+, se [Github för versionsinformation](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/releases).
* Stödrastersystem för layoutbehållare, se [Github](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid).
* Clientlib Manager: gjorde Google Closure Compiler till standard för minification of JavaScript clientlibs (gammalt standard var Yahoo YUI) och uppdaterade Google Closure Compiler till version v20190121
* Mallredigerare och profiler

   * Skapa och redigera mallar för single-page-appar som använder JS SDK (kallas även SPA Editor)

* Referenswebbplats We.Retail 4.0, se [Github för versionsinformation](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases).
* Verktyg för att uppgradera befintliga webbplatser och utnyttja de senaste redigeringsfunktionerna finns i [Github-databasen](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM innehåller version 1.12.4 av jQuery-biblioteket för att ge maximal kompatibilitet med befintlig anpassad kod. Adobe har gjort ändringar för att åtgärda kända säkerhetsproblem.

## Platsadministration {#site-administration}

* Ratten [Referens](/help/sites-authoring/author-environment-tools.md#references) har ett nytt avsnitt som visar interna länkar som pekar på den valda sidan. Det här är användbart när du planerar att ta en sida offline eller ta bort för att se vilka sidor som behöver justeras innan du tar dem offline.
* I [listvyn](/help/sites-authoring/basic-handling.md#list-view) finns en ny arbetsflödeskolumn som visar status när sidan befinner sig i ett arbetsflöde.
* I [sidegenskaperna](/help/sites-authoring/editing-page-properties.md) går det nu att bläddra efter befintliga resurser när du tilldelar en miniatyrbild till sidan (fliken Miniatyrbilder).

## Sidredigeraren {#page-editor}

* Möjliggör kontextredigering och komposition av ensidiga appupplevelser med React- och Angular-komponenter på klientsidan som utnyttjar JS SDK (kallas även SPA Editor)
* Skolningsläge visas bara om sidan har en konfigurerad ställningar.

## Innehållsfragment och redigerare {#content-fragments-amp-editor}

* Ny [Anteckningar](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) i Content Fragment Editor för att göra allmänna kommentarer och se kommentarer i texten (visas även i tidslinjen)
* Möjlighet att ange standardinnehållstypen för ett flerradigt textelement i en [Content Fragment-modell](/help/assets/content-fragments/content-fragments-models.md) till enkel text, formaterad text eller markering
* Lägg till [kommentar/anteckningar](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment) genom att markera text i textredigeraren (helskärmsläge)
* [Jämför ](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) versioner av ett innehållsfragment sida vid sida via referensspåret
* Resurserna i hämtningsrapporten visar nu innehållsfragment utifrån detta
* Lägg till [Stöd för innehållsfragment i Assets HTTP API](/help/assets/assets-api-content-fragments.md) via /api.json. Det finns API:er för att skapa, uppdatera, läsa och ta bort innehållsfragment.

## Experience Fragments {#experience-fragments}

* Förbättrade indexeringen av [Experience Fragments](/help/sites-authoring/experience-fragments.md), så deras innehåll hittas i sökningen efter sidor där de används
* Alternativet [Exportera till mål](/help/sites-administering/experience-fragments-target.md) tillåter nu att Experience Fragment skickas som JSON (standard är HTML), eller båda

## Översättning {#translation}

* Förenkla framtagningen av översättningsprojekt med Projektmallar
* Förenkla körningen av översättningsprojekt genom att ange att översättningsjobb ska ha statusen godkänd som standard
* Tillåt uppdatering av översatta sidor med ändringar i översättningsminne från tredje part
* Tillåt export av översättningsjobb i JSON-format
* Uppdatera Microsoft Translation-integrering så att V3 API används

## Hantering av flera platser (MSM) {#multi-site-management-msm}

* För rollout-konfigurationer som använder PushOnModify, bättre hantering av sidflyttningsåtgärd för att undvika inkonsekvent läge
* Om du skapar en ny sida i livecopy-strukturen skapas nu som standard en fristående sida
* Använd MSM-funktioner i enkelsidiga appar som använder JS SDK (kallas även SPA Editor)

## Launches {#launches}

* Nytt arbetsflöde för granskning och godkännande för lanseringar och möjlighet att endast befordra godkända startsidor
* [Alternativet i användargränssnittet har lagts till för att välja att ta bort starten direkt efter kampanjsteget](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

## Målinriktning och simulering av innehåll {#content-targeting-simulation}

* ContextHub-datalagret och JavaScript på klientsidan har uppdaterats till att använda jQuery 3 som standard.

## AEM och Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>För närvarande:
>
>* Endast `at.js 1.x` stöds om du använder Adobe Target som målmotor i AEM aktivitetskonsol.
   >
   >
* Både `at.js. 1.x` och `at.js 2.x` stöds om du använder Experience Fragment-export till Target och kör aktiviteter i Target-konsolen.


* Adobe Target-integrering kan nu använda Target Standard API. I tidigare versioner av AEM används Target Classic HTTP API, som nu är föråldrat.
* Adobe Target `mbox.js` version 63 ingår. Adobe rekommenderar starkt att implementeringen växlas till `at.js` v1.x.
* `at.js` version 1.5.0 ingår nu. Adobe rekommenderar att du använder [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) för att etablera `at.js` v1.x på platsen.

## AEM och Adobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` H.27.5 ingår. Adobe rekommenderar att du byter implementering till `AppMeasurement.js`
* `AppMeasurement.js` v1.8.0 ingår. Adobe rekommenderar att du använder [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) för att etablera AppMeasurement.js på webbplatsen.

## AEM och handel {#aem-commerce}

Förbättringar av Commerce Integration Framework pågår snabbare sedan AEM 6.4. [Läs mer här](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/docs.html).

## Webbgruppstillägg {#communities-add-on}

Se [Versionsinformation för Communities](../release-notes/communities-release-notes.md)

## Skärmtillägg {#screens-add-on}

* Använda Startar för att planera framtida innehållsändringar för signeringsinnehåll
* Uppspelning med datapriser i en sekvenskanal
* Skapa projektstruktur automatiskt med hjälp av en källfil, t.ex. Excel-blad

Mer information om ändringar i AEM Screens finns i versionsinformationen i [AEM Screens användarhandbok](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html).
