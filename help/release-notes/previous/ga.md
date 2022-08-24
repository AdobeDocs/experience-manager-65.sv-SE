---
title: Allmän versionsinformation för [!DNL Adobe Experience Manager] 6.5
description: '"[!DNL Adobe Experience Manager] 6.5 som beskriver versionsinformation, nyheter, hur man installerar och detaljerade ändringslistor."'
exl-id: b3d4a527-44ca-4eb6-b393-f3e8117cf1a6
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '4696'
ht-degree: 1%

---

# Allmän versionsinformation för [!DNL Adobe Experience Manager] 6.5{#general-release-notes-for-adobe-experience-manager}

## Versionsinformation {#release-information}

| Produkt | [!DNL Adobe Experience Manager] |
|---|---|
| Version | 6.5 |
| Typ | Större release |
| Allmänt tillgänglighetsdatum | 8 april 2019 |
| Rekommenderade uppdateringar | Se [AEM senaste uppdateringarna](https://helpx.adobe.com/experience-manager/aem-releases-updates.html). |

### Trivia {#trivia}

Versionscykeln för den här versionen av [!DNL Adobe Experience Manager] började 4 april 2018, genomgick 23 versioner av kvalitetssäkring och felkorrigeringar och slutade 28 mars 2019. Det totala antalet kundrelaterade problem, inklusive förbättringar och nya funktioner som har korrigerats i den här versionen, är 1345.

[!DNL Adobe Experience Manager] 6.5 är allmänt tillgängligt sedan 8 april 2019.

![AEM 6.5 Inloggningsskärm](/help/assets/assets/aem65-login-v4.png)

## Nyheter {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 är en uppgraderingsversion till [!DNL Adobe Experience Manager] 6.4 code base. Den innehåller nya och förbättrade funktioner, viktiga kundkorrigeringar, högprioriterade kundförbättringar och allmänna felkorrigeringar som är inriktade på produktstabilisering. Den innehåller även [!DNL Adobe Experience Manager] 6.4 Service Pack-versioner upp till SP4.

Listan nedan innehåller en översikt, medan de efterföljande sidorna innehåller fullständig information.

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

Plattformen för [!DNL Adobe Experience Manager] 6.5 bygger vidare på uppdaterade versioner av det OSGi-baserade ramverket (Apache Sling och Apache Felix) och Java Content Repository: Apache Jackrabbit Oak 1.10.2.

Quickstart använder Eclipse Jetty 9.4.15 som servermotor.

#### Java-stöd  {#java-support}

* Nytt stöd för Java 11 och Java 8 som redan stöds.
* För optimala prestanda bör du åsidosätta GC-standardvärden med andra värden. Mer information finns i [installera och uppdatera](/help/sites-deploying/custom-standalone-install.md) -avsnitt.
* Underhållsuppdateringar för Java 11 och Java 8 distribueras av Adobe för kundanvändning i AEM projekt, när de inte är allmänt tillgängliga från Oraclet.

#### Java Development {#java-development}

* Det finns nu [två versioner av Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies), en rekommenderad version med publika gränssnitt som inte är markerade för borttagning, samt en version som innehåller gränssnitt som är markerade för borttagning.

#### Användargränssnitt {#user-interface}

Ett antal förbättringar har gjorts i användargränssnittet för att göra det mer produktivt och enklare att använda.

* Nytt användargränssnitt för behörighetshantering för användare och grupper.
* Kolumnvyer läser nu bara in poster som är synliga på skärmen och som bara läses in mer när användaren börjar rulla. List- och kortvyn gjorde redan det sedan 6.0 (förbättrat i 6.4).
* Kolumnvyer innehåller nu arbetsflödesstatus för sidor/resurser när det är tillämpligt.
* The [Markera alla](/help/sites-authoring/basic-handling.md#select-all) är ett snabbt sätt att utföra en åtgärd med alla sidor/resurser i samma mapp.
* The [Markera alla](/help/sites-authoring/basic-handling.md#select-all) -åtgärden försöker utföra åtgärden på alla sidor/resurser, inte bara det som har lästs in. En varningsdialogruta visas om åtgärden inte har uppgraderats för att hantera gruppåtgärder.

>[!CAUTION]
>
>Adobe planerar inte att göra fler förbättringar av det klassiska användargränssnittet. AEM 6.5 innehåller det klassiska användargränssnittet och kunder som uppgraderar från tidigare versioner kan fortsätta använda det som det är. Observera att Classic-användargränssnittet fortfarande stöds fullt ut när det är inaktuellt. [Läs mer](/help/sites-deploying/ui-recommendations.md).

#### Sökning och indexering {#indexing-and-search}

* Sök i Oak har nu stöd för dynamiska aspekter. Filterfältet i resurssökningen visar t.ex. den uppskattade mängden resultat.
* QueryBuilder utökades för att ge resultat med dynamiska aspekter.

#### Uppgradera {#upgrade}

* Direktuppgradering på plats till AEM 6.5 stöds av kunder som kör AEM 6.2, 6.3 och 6.4. Kunder som använder 5.x eller 6.0/6.1 och vill använda en uppgradering på plats måste först uppgradera till 6.4 och sedan uppgradera till 6.5, eller uppgradera via överföring av innehållet mellan förekomsterna direkt till AEM 6.5.
* Uppgraderingsförfarandet är i stort sett detsamma i 6.5.
* Vi fortsätter att stödja funktionerna Bakåtkompatibilitet, utvärdering av uppgraderingskomplexitet och hållbar uppgradering som introducerades i 6.4. Det har gjorts versionsspecifika uppdateringar av dessa områden där det behövs.
* Pattern Detector har förenklats och det kommer att finnas ett paket som utvärderar uppgraderingar till 6.5 för de tillgängliga källversionerna.
* Mer information om uppgraderingsproceduren finns i [uppgraderingsdokumentation](/help/sites-deploying/upgrade.md).

#### Projekt och arbetsflöden {#projects-and-workflows}

* Den nya redigeraren för arbetsflödesmodeller som introducerades i 6.4 har förbättrats och omfattar fler åtgärder som kopiera och publicera, variabelstöd i arbetsflödessteg och förbättrat `OR` och `AND` delar.

#### Databas {#repository}

* Grunden till Adobe Experience Manager 6.5 bygger på uppdaterade versioner av det OSGi-baserade ramverket (Apache Sling och Apache Felix) och Java Content Repository: Apache Jackrabbit Oak 1.10.2.
* En översikt över åtgärdade problem finns i [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) och [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt).

>[!CAUTION]
>
>Den nya versionen av Oak Segment-taggen som finns sedan AEM 6.3 kräver en databasmigrering. Det här steget är obligatoriskt om du uppgraderar från en äldre version av tarMK eller vill växla den nya segmenttaggen från en annan typ av beständighet. Mer information om fördelarna med den nya segmenttaggen finns i [Migrering till Oak Segment tar - frågor och svar](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).

#### OSGI {#osgi}

* Tillagda OSGi Promises- och Converter-verktygsbibliotek.

#### Dokumentskydd {#security}

* Lösenordet har lagts till för administratörsanvändaren.

#### Webbserver {#web-server}

* Vid QuickStart-distributionen används Eclipse Jetty 9.4.15 som serverkomponent (AEM 6.4 levererades med 9.3.22).

### [!DNL Experience Manager] Sites {#experience-manager-sites}

#### Hanterade single-page-appar {#managed-single-page-apps}

Med Page Editor kan du redigera innehåll i sitt sammanhang och skapa/layouta i klientsidans renderade upplevelser (även känt [som SPA](/help/sites-developing/spa-architecture.md)). Befintliga ensidiga appar som byggs med JavaScript-ramverket React eller Angular kan utökas med AEM SJ SDK för att göras redigerbara för användare.

Först levererad som en del av AEM 6.4 SP2, med AEM 6.5 får SPA support följande fördelar:

* Använd mallredigeraren för att redigera och konfigurera AEM redigerbara delar av SPA
* Använd hantering av flera webbplatser för att skapa SPA, franchise eller white-label

#### Headless Content Management {#headless-content-management}

AEM kan hantera innehållet i olika format och från olika nivåer i högen. Vissa har funnits sedan 2008 med [Sling GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) och [POST Servlet](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html). Innehållstjänster ([Export av försäljningsmodell](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/develop-sling-model-exporter.html)) introducerades i AEM 6.3 och är den metod som används av AEM SJ SDK för att hysa enkelsidiga appar. The [HTTP API for Assets](/help/assets/mac-api-assets.md) är ett CRUD-API, som utökades för AEM 6.5.

Nya HTTP API-funktioner:

* Tillagd [Stöd för innehållsfragment i HTTP API for Assets](/help/assets/assets-api-content-fragments.md) för att skapa, uppdatera, läsa och ta bort fragment.
* Visa listor med innehållsfragment via Content Services med [Huvudkomponent för innehållsfragmentlista](https://opensource.adobe.com/aem-core-wcm-components/library/content-fragment-list.html).
* [Core Component Library](https://opensource.adobe.com/aem-core-wcm-components/library.html) som visar standardutdata för Content Services JSON för varje komponent

#### Tillägget Skärmar {#screens-add-on}

Designa, leverera och optimera effektivt upplevelser på alla digitala skärmar, från interaktiva kioskdatorer till digitala skyltar.

* Sammanställ upplevelser och innehåll i alla digitala kanaler och butiker med förbättrad återanvändning av innehållet
* Effektivare arbetsflöden för redigering, godkännande och publicering med stöd för Launches
* Redigera och leverera interaktiva upplevelser med SPA Editor
* Använda Startar för att planera framtida innehållsändringar för signeringsinnehåll
* Uppspelning med datapriser i en sekvenskanal
* Skapa projektstruktur automatiskt med en källfil som ett Excel-blad
* Utökat stöd för mediespelare med robust online- och offlinefunktion (Smart Sync) som kan skalas till även de största signeringsnätverken.
* Anpassa efter plats eller konfiguration av data som triggat innehåll med hjälp av dynamiska platshållare.
* Enhetliga insikter som bygger på Adobe Analytics integration i AEM Screens Player

Mer information om ändringar i AEM Screens finns i versionsinformationen i [AEM Screens Användarhandbok](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html).

#### Utveckling av komponenter och mallar {#component-amp-template-development}

* Maven Project Archetype 18+ för nya projekt, se [Github for release notes](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/releases).
* Single-page App Maven Project Archetype 1.0.6+ för nya projekt, se [Github for release notes](https://github.com/adobe/aem-spa-project-archetype/releases).
* HTML version 1.4, se [Github for release notes](https://github.com/adobe/htl-spec/releases/tag/1.4).

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

* Core Components 2.3.2+, se [Github for release notes](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/releases).
* Stödrastersystem för layoutbehållare, se [Github](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid).
* Clientlib Manager: gjorde Google Closure Compiler till standard för minification of JavaScript clientlibs (gammalt standard var Yahoo YUI) och uppdaterade Google Closure Compiler till version v20190121
* Mallredigerare och profiler

   * Skapa och redigera mallar för single-page-appar som använder JS SDK (kallas även SPA Editor)

* Referenswebbplats - butik 4.0, se [Github for release notes](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases).
* Verktyg för att uppgradera befintliga webbplatser för att utnyttja de senaste redigeringsfunktionerna finns i [Github-databas](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM innehåller version 1.12.4 av jQuery-biblioteket för att ge maximal kompatibilitet med befintlig anpassad kod. Adobe har gjort ändringar för att åtgärda kända säkerhetsproblem.

#### Webbplatsadministration {#site-administration}

* The [Referens](/help/sites-authoring/author-environment-tools.md#references) har ett nytt avsnitt som visar interna länkar som pekar mot den markerade sidan. Det här är användbart när du planerar att ta en sida offline eller ta bort för att se vilka sidor som behöver justeras innan du tar dem offline.
* The [listvy](/help/sites-authoring/basic-handling.md#list-view) har en ny arbetsflödeskolumn som visar status när sidan är i ett arbetsflöde.
* I [sidegenskaper](/help/sites-authoring/editing-page-properties.md)kan du nu bläddra efter befintliga resurser när du tilldelar en miniatyrbild till sidan (fliken Miniatyrbilder).

#### Page Editor {#page-editor}

* Möjliggör kontextredigering och komposition av ensidiga appupplevelser med React- och Angular-komponenter på klientsidan som utnyttjar JS SDK (kallas även SPA Editor)
* Skolningsläge visas bara om sidan har en konfigurerad ställningar.

#### Content Fragments &amp; Editor {#content-fragments-amp-editor}

* Nytt [Anteckningar](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) i Content Fragment Editor för att göra allmänna kommentarer och se kommentarerna i texten (visas även i tidslinjen)
* Möjlighet att ange standardinnehållstypen för ett flerradigt textelement i en [Modell för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md) till enkel text, formaterad text eller markering
* Lägg till [kommentar/anteckningar](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment) genom att markera text i textredigeraren (helskärmsläge)
* [Jämför versioner](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) av ett innehållsfragment sida vid sida via referensspåret
* Resurserna i hämtningsrapporten visar nu innehållsfragment utifrån detta
* Lägg till [Stöd för innehållsfragment i Assets HTTP API](/help/assets/assets-api-content-fragments.md) via /api.json. Det finns API:er för att skapa, uppdatera, läsa och ta bort innehållsfragment.

#### Experience Fragments {#experience-fragments}

* Förbättrad indexering av [Upplevelsefragment](/help/sites-authoring/experience-fragments.md)så deras innehåll hittas i sökningen efter sidor där de används
* The [Exportera till mål](/help/sites-administering/experience-fragments-target.md) nu kan du skicka Experience Fragment som JSON (standard är HTML), eller båda

#### Översättning {#translation}

* Förenkla framtagningen av översättningsprojekt med Projektmallar
* Förenkla körningen av översättningsprojekt genom att ange att översättningsjobb ska ha statusen godkänd som standard
* Tillåt uppdatering av översatta sidor med ändringar i översättningsminne från tredje part
* Tillåt export av översättningsjobb i JSON-format
* Uppdatera integreringen med Microsoft Translation till att använda V3 API

#### Hantering av flera webbplatser (MSM) {#multi-site-management-msm}

* För rollout-konfigurationer som använder PushOnModify, bättre hantering av sidflyttningsåtgärd för att undvika inkonsekvent läge
* Om du skapar en ny sida i livecopy-strukturen skapas nu som standard en fristående sida
* Använd MSM-funktioner i enkelsidiga appar som använder JS SDK (kallas även SPA Editor)

#### Launches {#launches}

* Nytt arbetsflöde för granskning och godkännande för lanseringar och möjlighet att endast befordra godkända startsidor
* Tillagd [i användargränssnittet för att välja att ta bort Launch direkt efter erbjudandesteget](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

#### Målinriktning och simulering av innehåll {#content-targeting-simulation}

* ContextHub-datalagret och JavaScript på klientsidan har uppdaterats till att använda jQuery 3 som standard.

#### AEM och Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>För närvarande:
>
>* Endast `at.js 1.x` stöds om du använder Adobe Target som målmotor i AEM.
>
>* Båda `at.js. 1.x` och `at.js 2.x` stöds om du använder Experience Fragment-export till Target och kör aktiviteter i Target-konsolen.


* Adobe Target-integrering kan nu använda Target Standard API. I tidigare versioner av AEM används Target Classic HTTP API, som nu är föråldrat.
* Adobe Target `mbox.js` version 63 ingår. Adobe rekommenderar starkt att du byter implementering till `at.js` v1.x.
* `at.js` version 1.5.0 ingår nu. Adobe rekommenderar att du använder [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) att tillhandahålla `at.js` v1.x in på webbplatsen.

#### AEM och Adobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` H.27.5 ingår. Adobe rekommenderar att du byter implementering till `AppMeasurement.js`
* `AppMeasurement.js` v1.8.0 ingår. Adobe rekommenderar att du använder [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) för att etablera AppMeasurement.js på webbplatsen.

#### AEM och handel {#aem-commerce}

Förbättringar av Commerce Integration Framework pågår snabbare sedan AEM 6.4. [Läs mer här](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/docs.html).

#### Webbgrupper, tillägg {#communities-add-on}

Om du vill ha den senaste versionen går du till [Distribuera webbgrupper](/help/communities/deploy-communities.md) i dokumentationen.

##### Förbättringar av communityns engagemang {#enhancements-to-community-engagement}

**Stöd för @Mentions**
AEM Communities tillåter nu registrerade användare att tagga (nämna) andra registrerade medlemmar för att få sin uppmärksamhet i användargenererat innehåll. Taggade (nämnda) medlemmar meddelas sedan, med en djup länk till motsvarande användargenererat innehåll. Användarna kan dock välja att inaktivera/aktivera webb- och e-postmeddelanden.

![Stöd för omnämnanden](/help/release-notes/assets/at-mentions.png)

Community-användare behöver inte söka efter sina förnamn, efternamn eller användarnamn för att se om någon har kommit fram till dem eller behöver deras uppmärksamhet. Dessutom kan UGC-författare söka svar från specifika registrerade användare som bäst kan åtgärda problemet och lägga till indata.

Community-administratörer måste **Aktivera omnämnande** om communitykomponenter för att tillåta registrerade användare att använda funktionerna för dessa komponenter.

**Gruppmeddelanden**

Registrerade communitymedlemmar kan nu skicka direktmeddelanden i grupp till grupper via en enda e-postkomposition, i stället för att skicka samma meddelande till gruppmedlemmarna separat. Tillåt [gruppmeddelanden](/help/communities/configure-messaging.md), aktivera båda förekomsterna av [Tjänsten Meddelandeåtgärder](/help/communities/messaging.md#group-messaging).

![Gruppmeddelande](/help/release-notes/assets/group-messaging.png)

##### Förbättringar av massmoderering {#enhancements-to-bulk-moderation}

Egna filter i Massmoderering

[Egna filter](/help/communities/moderation.md#custom-filters) kan nu utvecklas och läggas till i gränssnittet för massmoderering.

A [exempelprojekt](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) visa filtrering via taggar i [Github](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter). Det här projektet kan användas som bas för att utveckla analoga anpassade filter.

![Egna filter](/help/release-notes/assets/custom-tag-filter.png)

**Listvy i Massmoderering**

Ny listvy med förbättrat användargränssnitt har tillhandahållits i bulkmoderering för att visa användargenererade innehållsposter.

![Massmoderering i listvyn](/help/release-notes/assets/list-view-moderation.png)

##### Förbättringar av plats- och grupphantering {#enhancements-to-site-and-group-management}

**Författare av webbplats- och gruppadministratörer**

Communities, AEM 6.5 och framåt, medger decentraliserad administration (och förvaltning) av olika communityplatser och grupper/ kapslade grupper. Organisationer som har flera communitysajter och kapslade grupper kan nu välja medlemmar för administratörsroller på författarsidan när webbplatsen (och gruppen) skapas.

![Webbplatsadministratör](/help/release-notes/assets/site-admin.png)

Webbplatsadministratörer kan skapa en grupp på vilken hierarkinivå som helst och bli standardadministratörer. Dessa administratörer kan senare tas bort av andra gruppadministratörer. Gruppadministratörer kan hantera sin grupp G1 och skapa en undergrupp som är kapslad under G1.

##### Förbättringar av aktivering {#enhancements-to-enablement}

**Stöd för SCORM 2017.1**

Aktiveringsfunktionen i AEM 6.5 Communities har stöd för Shareable Content Object Reference Model [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) motor.

* Stöd för tangentbordsnavigering i aktiveringskomponenter
* Aktivera komponenter (t.ex. Katalog- och kursuppspelning, Uppdrag, Filbibliotek) i AEM Communities med stöd för tangentbordsnavigering för förbättrad tillgänglighet.

##### Andra förbättringar {#other-enhancements}

* Stöd för Solr 7
* AEM 6.5 Communities stöder Apache Solr 7.0-versionen av sökplattformen när MSRP och DSRP konfigureras.

### [!DNL Experience Manager Assets] {#experience-manager-assets}

I AEM 6.5 introduceras följande funktioner och förbättringar som ökar produktiviteten hos AEM, DAM-roller och associerade kreativa roller och marknadsföringsroller.

#### Integration med [!DNL Adobe Creative Cloud] och kreativa arbetsflöden {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager] erbjuder olika sätt att integrera med [!DNL Adobe Creative Cloud] och dela resurser för användning i arbetsflöden där kreatörerna och marknadsförarna eller affärsteamen samarbetar nära. [!DNL Experience Manager] 6.5 fortsätter att förbättra integreringen och effektivisera den ytterligare för att ge fler möjligheter och effektivisera befintliga metoder.

Läs vidare för att lära dig mer om de specifika funktionerna och integreringarna i [!DNL Experience Manager] 6.5 som ni kan använda för att få bästa möjliga stöd för ert innehåll.

##### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] stärker samarbetet mellan kreatörer och marknadsförare när det gäller att skapa innehåll. Kreatörer har åtkomst till innehåll som lagras i [!DNL Experience Manager Assets]utan att lämna de program de är mest bekanta med. Med hjälp av panelen i appen i [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]och [!DNL Adobe InDesign] appar.

[!DNL Adobe Asset Link] är en del av [Creative Cloud för företag](https://www.adobe.com/creativecloud/business/enterprise.html) erbjuder. Mer information, inklusive nödvändig konfiguration av [!DNL Experience Manager] distribution, se [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html).

![Söka efter resurser i Adobe Photoshop](/help/release-notes/assets/asset_search_photoshop.png)

##### [!DNL Adobe Stock] integration {#stock}

Din organisation kan använda [!DNL Adobe Stock] företagsplan inom [!DNL Experience Manager Assets] för att se till att licensierat material finns tillgängligt för dina kreativa projekt och marknadsföringsprojekt. Du kan snabbt hitta, förhandsgranska och licensiera [!DNL Adobe Stock] resurser som har sparats i Experience Manager, med de kraftfulla DAM-funktionerna i [!DNL Experience Manager].

[!DNL Adobe Stock] ger designers och företag tillgång till miljontals utvalda och royaltyfria foton, vektorer, illustrationer, videor, mallar och 3D-resurser av hög kvalitet för alla kreativa projekt.

Mer information finns på [Använda Adobe Stock-resurser i Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md).

![Förhandsgranska Adobe Stock-bilder och licenser inifrån Experience Manager Assets](/help/release-notes/assets/stock_image_preview_license_options.png)

*Bild: Förhandsgranska [!DNL Adobe Stock] bild och licens inifrån [!DNL Experience Manager Assets].*

![Söka efter och filtrera licensierade Adobe Stock-bilder i Experience Manager](/help/release-notes/assets/aem-search-filters2.jpg)

*Bild: Sök efter och filtrera licensierade [!DNL Adobe Stock] bilder i [!DNL Experience Manager].*

##### Dynamiska referenser i [!DNL Adobe InDesign] {#dynamic-references-in-indesign}

[!DNL Experience Manager Assets] används i [!DNL Adobe InDesign] filer är dynamiska. Referenserna uppdateras automatiskt om de refererade resurserna flyttas i databasen. Mer information finns i [hantera sammansatta resurser](/help/assets/managing-linked-subassets.md).

#### Brand Portal-funktioner {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] hjälper er att enkelt skaffa, effektivt kontrollera och på ett säkert sätt distribuera godkända resurser till externa leverantörer/myndigheter och interna företagsanvändare på olika enheter. Det bidrar till att effektivisera tillgångsdelningen, snabbar upp time-to-market för tillgångar och eliminerar risken för otillåten användning och obehörig åtkomst.

Mer information finns i [Nyheter i Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=en).

#### Anslutna resurser {#connectedassets}

I stora företag kan den infrastruktur som krävs för att skapa webbplatser distribueras. Ibland finns funktionerna för att skapa webbplatser och de digitala resurser som behövs i olika vattentäta skott.

[!DNL Experience Manager Sites] erbjuder funktioner för att skapa webbsidor och är det DAM-system (Digital Asset Management) som tillhandahåller de resurser som krävs för webbplatserna. [!DNL Experience Manager Assets] [!DNL Experience Manager] har nu stöd för ovanstående användningsexempel genom att integrera [!DNL Sites] och [!DNL Assets]. Se [konfigurera och använda funktionen för anslutna resurser](/help/assets/use-assets-across-connected-assets-instances.md).

![Dra en resurs från en [!DNL Experience Manager] driftsättning på [!DNL Sites] sida med en annan [!DNL Experience Manager] distribution](/help/release-notes/assets/connected-assets-drag-and-drop-only.gif)

*Bild: Dra en resurs från en [!DNL Experience Manager] driftsättning på [!DNL Sites] sida på en annan [!DNL Experience Manager] distribution.*

#### Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] har förbättrat funktionerna för framtagning och distribution av multimedia i [!DNL Experience Manager Assets] för att skapa avancerade upplevelser som är engagerande och personaliserade. Genom att ladda upp en primär resurs av hög kvalitet och använda avancerad molnrendering och visningsprogram i Adobe kan ni leverera vilken kombination av renderingar som helst direkt som stöd för er organisations mediestrategi.

Mer information om nya [!DNL Dynamic Media] funktioner, se [Versionsinformation för Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html).

##### Stöd för 360-video {#video-support}

Hantera dina 360-videofiler direkt i [!DNL Experience Manager] med de allra senaste tittarna för att leverera VR-upplevelser till datorer, mobiler och VR-headset. Mer information finns i [Använda 360-video](/help/assets/360-video.md).

##### Egna videominiatyrer {#custom-video-thumbnails}

Nu kan du anpassa miniatyrbilderna för videomaterialet med hjälp av bildrutor från själva videon eller annat innehåll som lagras i DAM. Ytterligare instruktioner finns i [Om videominiatyrer](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

##### Förbättrad tillgänglighet {#accessibility-enhancements}

[!DNL Dynamic Media] visningsprogrammen har nu stöd för förbättrade hjälpmedelsfunktioner som Aria-support, skärmläsare och Alt-text. Mer information finns i [Referenshandbok för visningsprogram](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html).

#### Förbättrad sökupplevelse {#experience-enhancement-for-searching}

[!DNL Experience Manager] 6.5 Från och med sökresultatsidan kan marknadsförarna hitta de önskade resurserna snabbare. Sökmetoderna uppdateras med antalet resurser även innan sökfiltret används. Genom att se det förväntade antalet mot filtret kan användarna navigera effektivt genom sökresultaten. Mer information finns i [Söka efter resurser i Experience Manager](/help/assets/search-assets.md).

![Se antalet resurser utan att filtrera sökresultaten i sökfaktorer](/help/assets/assets/asset_search_results_in_facets_filters.png)

*Bild: Se antalet resurser utan att filtrera sökresultaten i sökfaktorer.*

#### Förbättrad användbarhet {#usability-enhancement}

Du kan nu välja alla inlästa resurser i en mapp eller från ett sökresultat på en gång. Det hjälper dig att hantera flera resurser snabbt. Kryssrutan markerar alla resurser som passar scenariot, till exempel ett sökresultat, och inte bara de resurser som är synliga i [!DNL Experience Manager] gränssnitt.

![Använd alternativet Markera alla för att markera alla inlästa resurser med ett klick.](/help/release-notes/assets/select-all-in-aem-assets.gif)

*Bild: Använd alternativet Markera alla för att markera alla inlästa resurser med ett klick.*

#### Förbättringar av metadata {#metadata-enhancements}

[!DNL Assets] gör att du kan skapa metadatamappar för resursmappar, som definierar layouten och metadata som visas på mappegenskapssidor. Du kan nu tilldela ett mappmetadatchema till en befintlig mapp eller när du skapar en mapp. Mer information finns i [Mappmetadatamatchschema](/help/assets/metadata-config.md#folder-metadata-schema).

När du anger överlappande metadata kan alternativen läsas in från en JSON-fil vid körningen, till exempel i stället för att du skriver manuellt i formuläret. Mer information finns i [överlappande metadata](/help/assets/metadata-schemas.md#cascading-metadata).

#### Rapportförbättringar {#reporting-enhancements}

Innehållsfragment och länkdelningar ingår nu i den hämtade rapporten. Mer information finns i [Resursrapporter](/help/assets/asset-reports.md).

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM 6.5 Forms har flera nya funktioner och förbättringar. Högdagrarna är följande:

* Transaktionsrapporter för att spåra antalet skickade formulär, bearbetade dokument och återgivna dokument
* Förbättrad användning av interaktiv kommunikation
* Molnbaserade digitala signaturer i anpassningsbara formulär
* Bädda in adaptiva formulär och interaktiv kommunikation i AEM Sites single page-applikationer (SPA).
* Stöd för variabler i AEM arbetsflöden
* Stöd för datavisningsmönster i interaktiv kommunikation
* Sortera adaptiva formulär och interaktiva kommunikationstabeller
* Automatisk validering av indata i formulärdatamodeller

Se [Sammanfattning av nya funktioner och förbättringar i AEM 6.5 Forms](/help/forms/using/whats-new.md) för information om nya och förbättrade funktioner och dokumentationsresurser.

### [!DNL Experience Manager Livefyre] {#experience-manager-livefyre}

Du kan integrera Livefyre med AEM 6.5-instansen. Se [hur man integrerar Livefyre med AEM](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/livefyre.html).

### Utnyttja kundfokuserad utveckling {#leverage-customer-focused-development}

Adobe använder en kundfokuserad utvecklingsmodell som gör det möjligt för kunderna att bidra till alla faser i utvecklingsprocessen, under specifikation, utveckling och testning. Vi tackar alla kunder och partners som deltar i den här processen.

Adobe har de rutiner och processer som behövs för att kunna samla in, prioritera och spåra kundfokuserade fellösningar och utveckla förbättringsförfrågningar. The [Experience Manager supportportal](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) är integrerat med Adobe Enhancement and Defect Tracking System. Kundfrågor identifieras och löses av kundsupportteamet där det är möjligt. När den eskaleras till FoU hämtas all kundinformation in och används för prioritering och rapportering. Vid utveckling av betald support, garantifrågor och kundbetalda förbättringar prioriteras.

Denna prioriteringsprocess har resulterat i över 750 kundfokuserade förändringar som fastslagits i AEM 6.5.

## Lista över filer som ingår i releasen {#list-of-files-that-are-part-of-the-release}

**Foundation**

* Fristående QuickStart: `cq-quickstart-6.5.0.jar`.
* Snabbstart för programserver: `cq-quickstart-6.5.0.war`.
* Skicka 4.3.2 eller senare för olika webbservrar och plattformar. Se [ladda ned länk](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html)
* Plug-in för Eclipse IDE ([läs mer och ladda ned](/help/sites-developing/aem-eclipse.md))

* Tillägg för Brackets Code Editor ([läs mer och ladda ned](/help/sites-developing/aem-brackets.md))
* Maven/Gradle-beroenden ([ladda ned länk](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/))

**Sites**

* Kärnkomponenter ([GitHub-projekt](https://github.com/adobe/aem-core-wcm-components))
* Implementering av referens för Vi.butik ([läs mer](/help/sites-developing/we-retail.md))
* Maven Project Archetypes:

   * för fullstacksplatser: [GitHub-projekt](https://github.com/adobe/aem-project-archetype)
   * för ensidiga appar med React/Angular: [GitHub-projekt](https://github.com/adobe/aem-spa-project-archetype)

* AEM Screens Players for various target platforms ([ladda ned](https://download.macromedia.com/screens/))

* Språkmodeller för smart innehåll. Engelska är förinstallerat - fler språk kan hämtas

   * [Tyska](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [Spanska](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [Italienska](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [Franska](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* AEM Modernize Tools Suite, t.ex. Dialog Conversion Tool. ([GitHub-projekt](https://github.com/adobe/aem-modernize-tools))

**Assets**

* Paket för att lägga till utökad PDF rastrerare ([läs mer](/help/assets/aem-pdf-rasterizer.md))
* Paket för att lägga till utökat stöd för RAW-bilder ([läs mer](/help/assets/camera-raw.md))

**Forms**

* [Paket för AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [AEM Forms OSGi Client SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)

## Språk {#languages}

Användargränssnittet finns på följande språk:

* Engelska
* Tyska
* Franska
* Spanska
* Italienska
* Brasiliansk portugisiska
* Japanska
* Förenklad kinesiska
* Traditionell kinesiska (begränsat stöd)
* Koreanska

[!DNL Experience Manager] 6.5 har certifierats för GB18030-2005 CITS för att använda den kinesiska kodningsstandarden.

## Installera och uppdatera {#install-update}

Information om installationskrav finns i [installationsanvisningar](/help/sites-deploying/custom-standalone-install.md).

Detaljerade anvisningar finns i [uppgraderingsdokumentation](/help/sites-deploying/upgrade.md).

## Plattformar som stöds {#supported-platforms}

Hitta en komplett matris med plattformar som stöds, inklusive supportnivå på [AEM 6.5 Tekniska krav](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>Oraclet har flyttat till en LTS-modell (Long Term Support) för Oracle Java SE-produkter. Java 9 och 10 är icke-LTS-versioner som Oracle. Se [Oracle Java SE - supportöversikt](https://www.oracle.com/technetwork/java/eol-135779.html). Adobe har stöd för LTS-versioner av Java som endast kan köras AEM i produktionen. Java 11 är den rekommenderade versionen som ska användas med AEM 6.5.

## Föråldrade och borttagna funktioner {#deprecated-and-removed-features}

Adobe utvärderar ständigt funktionerna i produkten och planerar att ersätta funktioner med kraftfullare versioner, eller bestämmer sig för att omimplementera utvalda delar så att de blir bättre förberedda för framtida förväntningar eller tillägg.

För [!DNL Adobe Experience Manager] 6.5, [läs listan över borttagna funktioner](/help/release-notes/deprecated-removed-features.md). Sidan innehåller även förhandsmeddelanden om förändringar inom den närmaste framtiden och viktiga meddelanden för kunder som uppdaterar från tidigare versioner.

## Kända fel {#known-issues}

### Plattform {#platform}

* Ett problem rapporteras där CRX-Quickstart och dess innehåll tas bort.

   Kontrollera att egenskapen `htmllibmanager.fileSystemOutputCacheLocation` är inte en tom sträng:

   1. Anropar `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. Uppgraderar till AEM 6.5.
   3. Kör migrering av&quot;lat innehåll&quot; på AEM 6.5.

   A [Knowledge Base](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) det finns mer information och en lösning på problemet i artikeln.

* Om du använder JDK 11 med AEM 6.5-instansen kan vissa sidor visas som tomma efter distributionen av vissa paket. Följande felmeddelande visas i loggfilen:

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

Så här löser du felet:

1. Stoppa AEM. Gå till `<aem_server_path_on_server>crx-quickstart\conf` och öppna `sling.properties` -fil. Adobe rekommenderar att du säkerhetskopierar den här filen.

1. Sök efter `org.osgi.framework.bootdelegation=`. Lägg till `jdk.internal.reflect,jdk.internal.reflect.*` egenskaper för att visa resultatet som.

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. Spara filen och starta om AEM.

### Sites {#sites}

* **Arbeta med sidversioner**: [Om en sida har flyttats kan du inte längre förhandsgranska versioner som gjorts före flyttningen](/help/sites-authoring/working-with-page-versions.md#previewing-a-version).

### Assets {#assets}

* **Sök:** Sökningen ger inga resultat om söksträngen innehåller inledande blanksteg ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **Metadataschema för mapp**: När du har lagt till en alternativknapp återges ID- och Value-fältet inte som förväntat och borttagningsfunktionen fungerar inte. (CQ-4261144)
* När du byter namn på en resurs går det inte att använda ett tomt utrymme i resursnamnet. (CQ-4266403)

### Forms {#forms}

* När AEM Forms är installerat i Linux fungerar inte den digitala signaturen med maskinvarusäkerhetsmodulen. (CQ-4266721)
* (Endast AEM Forms på WebSphere) **Forms Workflow** > **Uppgiftssökning** alternativet returnerar inget resultat om du söker efter **Administratör** med **Användarnamn** som sökvillkor. (CQ-4266457)

* AEM Forms kan inte konvertera TIF- och TIFF-filer med JPEG-komprimering till PDF-dokument. (CQ-4265972)
* The **AEM Forms Assets Scanner** och **Letter to Interactive Communication Migration** alternativ fungerar inte på **AEM Forms Migration** sida. (CQ-4266572)

* (Endast JBoss 7) När du uppgraderar från en tidigare version till AEM 6.5 Forms och den tidigare versionen hade processer (.lca) som skapade och använde en kopia av standardåtergivningsprocessen eller standardåtergivningsprocessen, kan HTML5 Forms som använder sådana processer (.lca) inte utföra de åtgärder som krävs. (CQ-4243928)
* När en formulärdatamodelltjänst anropas från regelredigeraren för att dynamiskt uppdatera värden för bildvalskomponenten, uppdateras inte värdena för bildvalskomponenten i en adaptiv varifrån. (CQ-4254754)
* AEM Forms Designer-installationsprogrammet kräver 32-bitarsversionen av [Visual C++ redistributable runtime package 2012](https://support.microsoft.com/en-in/help/2977003/the-latest-supported-visual-c-downloads) och [Omdistribuerbara Visual C++-körtidspaket 2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). Kontrollera att ovannämnda omdistribuerbara körtidspaket är installerade innan du startar installationen. (CQ-4265668)

* PDF Generator stöder inte autentisering med smartkort.  När en administratör aktiverar grupprincipen `Interactive Logon: Require Smart card` på en Windows-server blir alla användare av PDF Generator ogiltiga.

* När ett adaptivt formulär har konfigurerats för att dynamiskt uppdatera värden för en komponent och den publiceringsinstans som är värd för formuläret nås via dispatchern, slutar funktionen att dynamiskt uppdatera värden för ett fält att fungera. Du löser problemet genom att öppna CRXDE på publiceringsinstansen och navigera till `/libs/fd/af/runtime/clientlibs/guideChartReducer`och skapa den egenskap som anges nedan.

   * Namn: allowProxy
   * Typ: Boolean
   * Värde: true
   * Skyddad: Falskt
   * Obligatoriskt: Falskt
   * Flera: Falskt
   * Automatiskt skapad: Falskt

   Egenskapen gör att klientbiblioteken under körningsmappen kan komma åt proxies. (CQ-4268679)

* När AEM Forms startas `SAX Security Manager could not be setup` visas.
* När du öppnar ett PDF som är skyddat med AEM Forms Document Security på en Apple iOS eller iPadOS som kör Adobe Acrobat Reader version 20.10.00.
* När du skickar ett formulär som innehåller ett standardfält för överföring av HTML från en Apple iOS-enhet skickas ibland inte filens innehåll och en 0-byte-fil tas emot i den andra änden. Apple iOS 15.1 åtgärdar problemet.

## Nedladdning och support av produkter (begränsade platser) {#product-download-and-support-restricted-sites}

Följande webbplatser är bara tillgängliga för kunder. Om du är kund och behöver åtkomst kontaktar du din kontoansvarige på Adobe.

* [Produktnedladdning på licensing.adobe.com](https://licensing.adobe.com/).

* Produktuppdateringar, patchar och paket för ytterligare funktionalitet i [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).

* [Kundsupport via Admin Console](https://adminconsole.adobe.com/). Mer information finns i [Ny Adobe-upplevelse för kundsupport](https://docs.adobe.com/content/help/en/customer-one/using/home.html).
