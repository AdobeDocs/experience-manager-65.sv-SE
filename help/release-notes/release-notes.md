---
title: Allmän versionsinformation om Adobe Experience Manager 6.5
description: Adobe Experience Manager 6.5 innehåller en beskrivning av versionsinformation, nyheter, hur man installerar och detaljerade ändringslistor.
uuid: b916624e-9486-4391-8c6f-cb4045e78490
contentOwner: chuesler
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 7d3ceccb-4f00-4e11-9c9f-6de46a455e02
docset: aem65
translation-type: tm+mt
source-git-commit: 57bad4e74b2dfd9e389643bfe58ef25564c5c545

---


# Allmän versionsinformation om Adobe Experience Manager 6.5{#general-release-notes-for-adobe-experience-manager}

## Versionsinformation {#release-information}

<table>
 <tbody>
  <tr>
   <th>Produkt</th>
   <td>Adobe Experience Manager<br /> </td>
  </tr>
  <tr>
   <th>Version</th>
   <td>6.5</td>
  </tr>
  <tr>
   <th>Typ</th>
   <td>Större release</td>
  </tr>
  <tr>
   <th>Allmänt tillgänglighetsdatum</th>
   <td>8 april 2019<br /> </td>
  </tr>
  <tr>
   <th>Rekommenderade uppdateringar</th>
   <td>Se <a href="https://helpx.adobe.com/experience-manager/aem-releases-updates.html">AEM Releases and Updates</a></td>
  </tr>
 </tbody>
</table>

### Trivia {#trivia}

Versionscykeln för den här versionen av Adobe Experience Manager inleddes den 4 april 2018, genomgick 23 versioner av kvalitetssäkring och felkorrigering och avslutades den 28 mars 2019. Det totala antalet kundrelaterade problem, inklusive förbättringar och nya funktioner som har korrigerats i den här versionen, är 1345.

Adobe Experience Manager 6.5 är generellt tillgängligt sedan 8 april 2019.

![AEM 6.5 Inloggningsskärm](/help/assets/assets/aem65-login-v4.png)

## Nyheter {#what-s-new}

Adobe Experience Manager 6.5 är en uppgraderingsversion till kodbasen Adobe Experience Manager 6.4. Den innehåller nya och förbättrade funktioner, viktiga kundkorrigeringar, högprioriterade kundförbättringar och allmänna felkorrigeringar som är inriktade på produktstabilisering. Den innehåller även Adobe Experience Manager 6.4 Service Pack-versioner upp till SP4.

Listan nedan innehåller en översikt, medan de efterföljande sidorna innehåller fullständig information.

### Experience Manager Foundation {#experience-manager-foundation}

Fullständig lista över ändringar i [AEM Foundation](/help/release-notes/wcm-platform.md).

Plattformen för Adobe Experience Manager 6.5 bygger på uppdaterade versioner av det OSGi-baserade ramverket (Apache Sling och Apache Felix) och Java Content Repository: Apache Jackrabbit Oak 1.10.2.

Quickstart använder Eclipse Jetty 9.4.15 som servermotor.

#### Java-stöd {#java-support}

* Nytt stöd för Java 11 samt Java 8 som redan stöds
* För optimala prestanda bör du åsidosätta GC-standardvärden med andra värden. Mer information finns i avsnittet [Installera och uppdatera](/help/sites-deploying/custom-standalone-install.md) .
* Underhållsuppdateringar för Java 11 och Java 8 kommer att distribueras av Adobe för kundanvändning i AEM-relaterade projekt, om de inte är allmänt tillgängliga från Oracle

#### Java Development {#java-development}

* Det finns nu [två versioner av Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies), en rekommenderad version med publika gränssnitt som inte är markerade för borttagning, samt en version som innehåller gränssnitt som är markerade för borttagning.

#### Användargränssnitt {#user-interface}

Ett antal förbättringar har gjorts i användargränssnittet för att göra det mer produktivt och enklare att använda.

* Nytt användargränssnitt för behörighetshantering för användare och grupper
* Kolumnvyer läser nu bara in poster som är synliga på skärmen och som bara läses in mer när användaren börjar rulla. List- och kortvyn gjorde redan det sedan 6.0 (förbättrat i 6.4)
* Kolumnvyer innehåller nu arbetsflödesstatus för sidor/resurser när det är tillämpligt
* Åtgärden [Markera allt](/help/sites-authoring/basic-handling.md#select-all) är ett snabbt sätt att köra en åtgärd med alla sidor/resurser i samma mapp
* Åtgärden [Markera alla](/help/sites-authoring/basic-handling.md#select-all) försöker utföra åtgärden på alla sidor/resurser, inte bara det som har lästs in. En varningsdialogruta visas om åtgärden inte har uppgraderats för att hantera gruppåtgärder

>[!CAUTION]
>
>Adobe planerar inte att göra fler förbättringar av det klassiska användargränssnittet. AEM 6.5 innehåller det klassiska användargränssnittet, och kunder som uppgraderar från tidigare versioner kan fortsätta använda det som det är. Observera att Classic-användargränssnittet fortfarande stöds fullt ut när det är inaktuellt. [Läs mer](/help/sites-deploying/ui-recommendations.md).

#### Sökning och indexering {#search-indexing}

* Sök i Oak har nu stöd för dynamiska aspekter. Filterfältet i resurssökningen visar t.ex. den uppskattade mängden resultat.
* QueryBuilder utökades för att ge resultat med dynamiska aspekter

#### Uppgradera {#upgrade}

* Direktuppgradering på plats till AEM 6.5 stöds av kunder som kör AEM 6.2, 6.3 och 6.4. Kunder som använder 5.x eller 6.0/6.1 och vill använda en uppgradering på plats måste först uppgradera till 6.4 och sedan uppgradera till 6.5, eller uppgradera via överföring av innehållet mellan instanserna direkt till AEM 6.5.

#### Projekt och arbetsflöden {#projects-and-workflows}

* Den nya redigeraren för arbetsflödesmodeller som introducerades i 6.4 har förbättrats så att den omfattar fler åtgärder som Kopiera och Publicera, Variabelstöd i arbetsflödessteg samt förbättrade OR- och AND-delningar.

### Experience Manager Sites {#experience-manager-sites}

Fullständig lista över ändringar i [AEM Sites och Add-ons](/help/release-notes/sites.md).

#### Hanterade single-page-appar {#managed-single-page-apps}

Med Page Editor kan du redigera innehåll i sitt sammanhang och skapa/layouta i klientsidans renderade upplevelser (kallas även [SPA Editor](/help/sites-developing/spa-architecture.md)). Befintliga enkelsidiga appar som byggs med JavaScript-ramverket React eller Angular kan utökas med AEM SJ SDK för att göras redigerbara för användare.

Först levererad som en del av AEM 6.4 SP2, med AEM 6.5, får SPA-supporten följande funktioner:

* Använd mallredigeraren för att redigera och konfigurera AEM-redigerbara delar i SPA
* Använd hantering av flera webbplatser för att skapa SPA-upplevelser med länder, franchise eller vit etiketter

#### Headless Content Management {#headless-content-management}

AEM kan hantera innehållet i olika format och från olika nivåer i stacken. Vissa har funnits sedan 2008 med [Sling GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) och [POST Servlet](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html). Content Services ([Sling Model Exporter](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/sling-model-exporter-tutorial-develop.html)) introducerades i AEM 6.3 och är den metod som används av AEM SJ SDK för att hysa enkelsidiga appar. API:t för [HTTP för Assets](/help/assets/mac-api-assets.md) är ett CRUD-API, som utökades för AEM 6.5.

Nya HTTP API-funktioner:

* Stöd för [innehållsfragment har lagts till i HTTP API för resurser](/help/assets/assets-api-content-fragments.md) för att skapa, uppdatera, läsa och ta bort fragment.
* Visa listor med innehållsfragment via Content Services med kärnkomponenten [Content Fragment List](https://opensource.adobe.com/aem-core-wcm-components/library/content-fragment-list.html).
* [Core Component Library](https://opensource.adobe.com/aem-core-wcm-components/library.html) som visar standardutdata för Content Services JSON för varje komponent

#### Tillägget Skärmar {#screens-add-on}

Designa, leverera och optimera effektivt upplevelser på alla digitala skärmar, från interaktiva kioskdatorer till digitala skyltar.

**Design**

* Sammanställ upplevelser och innehåll i alla digitala kanaler och butiker med förbättrad återanvändning av innehållet
* Effektivare arbetsflöden för redigering, godkännande och publicering med stöd för Launches
* Redigera och leverera interaktiva upplevelser med SPA Editor

**Leverera**

* Utökat stöd för mediespelare med robust online- och offlinefunktion (Smart Sync) som kan skalas till även de största signeringsnätverken.

**Optimera**

* Anpassa efter plats eller konfiguration av data som triggat innehåll med hjälp av dynamiska platshållare.
* Enhetliga insikter som bygger på Adobe Analytics-integrering i AEM Screens Player

Mer information om ändringar av AEM-skärmar finns i versionsinformationen i användarhandboken för [AEM-skärmar](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html).

### Experience Manager Assets {#experience-manager-assets}

Fullständig lista över ändringar i versionsinformationen [för](/help/release-notes/assets.md)AEM 6.5 Assets.

AEM 6.5 innehåller följande funktioner och förbättringar som ökar produktiviteten för AEM-användare, DAM-roller och associerade kreativa roller och marknadsföringsroller.

#### Integrering med Adobe Creative Cloud {#integration-with-adobe-creative-cloud}

Introduktionen av [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html), en upplevelse i appen för kreativa användare som arbetar i Adobe Creative Cloud-program, inklusive Photoshop, Illustrator och InDesign, effektiviserar samarbetet mellan kreatörer och marknadsförare när det gäller att skapa innehåll. AEM-skrivbordsappen fortsätter att stödja behoven hos användare som arbetar med resurser från AEM på datorn, oavsett filtyp och datorprogram.

Dessutom kan AEM integreras med Adobe Stock för att hjälpa till att hitta, förhandsgranska, licensiera och spara Adobe Stock-mediefiler direkt från AEM Web UI.

![Panelen Resurslänk i Photoshop](/help/assets/assets/aem65-assetlink-photoshop.png)

#### Anslutna resurser {#connected-assets}

Funktionen för sammankopplade resurser är avsedd för större driftsättningar med ett antal AEM Sites-driftsättningar som behöver utnyttja resurser från en central AEM Assets DAM-driftsättning. Det gör det möjligt att förbättra styrningen av resurser som hanteras centralt samtidigt som det blir mycket effektivt att leverera resurser till de olika platsernas driftsättningar.

### Dynamiska medier {#dynamic-media}

Med Dynamic Media får du förbättrade funktioner för framtagning och leverans av multimedia i AEM Assets för att skapa avancerade upplevelser som är både engagerande och personaliserade. Med ett och samma högklassiga mastermaterial kan ni utnyttja vår avancerade molnrendering, Smart Crop och förstklassiga visningsprogram för att leverera de mest engagerande upplevelserna med branschledande prestanda.

Nya funktioner:

* Stöd för 360-video- och VR-headset
* Egna videominiatyrer
* Bättre stöd för tillgänglighet
* Hot-linking protection

#### Användarupplevelse och sökning {#user-experience-and-search}

Viktiga förbättringar hjälper till att hitta rätt resurser snabbare genom att tillhandahålla dynamiska sökfunktioner och hantera flera resurser effektivare genom att ge möjlighet att välja alla resurser från valfri mapp eller sökresultat.

### Adobe Experience Manager Forms {#experience-manager-forms}

AEM 6.5 Forms innehåller flera nya funktioner och förbättringar. Högdagrarna är följande:

* Transaktionsrapporter för att spåra antalet skickade formulär, bearbetade dokument och återgivna dokument
* Förbättrad användning av interaktiv kommunikation
* Molnbaserade digitala signaturer i anpassningsbara formulär
* Bädda in adaptiva formulär och interaktiv kommunikation i en AEM Sites Single-page application (SPA).
* Stöd för variabler i AEM-arbetsflöden
* Stöd för datavisningsmönster i interaktiv kommunikation
* Sortera adaptiva formulär och interaktiva kommunikationstabeller
* Automatisk validering av indata i formulärdatamodeller

Se [Sammanfattning av nya funktioner och förbättringar i AEM 6.5-formulär](/help/forms/using/whats-new.md) för information om nya och förbättrade funktioner och dokumentationsresurser.

### Experience Manager Communities {#communitiesreleasenotes}

AEM 6.5 innehåller nya funktioner och förbättringar för Communities. Den här versionen innehåller följande:

* Registrerad medlemstaggning (@mention) stöds vid redigering av användargenererat innehåll.
* Direkt massutskick till en grupp medlemmar stöds nu.
* Anpassade filter har utvecklats och lagts till i användargränssnittet för massmoderering. Ett [exempelprojekt](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) som visar filtrering med taggar kan användas som bas för att utveckla analoga anpassade filter.
* Ny listvy med förbättrat användargränssnitt vid gruppmoderering.
* Separata administratörer för olika communitysajter och kapslade grupper kan tilldelas i stället för en enda community-administratör.
* Aktiveringsfunktionen i AEM 6.5 Communities har stöd [(SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) .
* Stöd för tangentbordsnavigering i aktiveringskomponenter för förbättrad tillgänglighet.
* Stöd för Apache Solr 7.0 vid konfiguration av MSRP och DSRP.

En detaljerad lista över ändringar finns i Versionsinformation [för](/help/release-notes/communities-release-notes.md)AEM 6.5 Communities.

### Experience Manager Livefyre {#experience-manager-livefyre}

Du kan integrera Livefyre med din AEM 6.5-instans. Information om hur du integrerar Livefyre med AEM finns här:

* [Integrera Livefyre](https://helpx.adobe.com/experience-manager/6-4/help/sites-administering/livefyre.html)

### Utnyttja kundfokuserad utveckling {#leverage-customer-focused-development}

Adobe använder en kundfokuserad utvecklingsmodell som gör det möjligt för kunderna att bidra till alla faser i utvecklingsprocessen, under specifikation, utveckling och testning. Vi tackar alla kunder och partners som deltar i den här processen.

Adobe har de rutiner och processer som krävs för att möjliggöra insamling, prioritering och spårning av kundfokuserad fellösning och utveckling av förbättringsförfrågningar. Supportportalen [för](https://helpx.adobe.com/marketing-cloud/contact-support.html) Adobe Marketing Cloud är integrerad med Adobe Enhancement &amp; Defect Tracking System. Kundfrågor identifieras och löses med kundtjänst där det är möjligt. När den eskaleras till FoU hämtas all kundinformation in och används för prioritering och rapportering. Vid utveckling ges prioritet åt betald support och garantifrågor samt betalda kundförbättringar.

Denna prioriteringsprocess har resulterat i över 750 kundfokuserade förändringar som korrigerats i AEM 6.5.

## Lista över filer som ingår i releasen {#list-of-files-that-are-part-of-the-release}

**Foundation**

* Fristående QuickStart: cq-quickstart-6.5.0.jar
* Snabbstart för programserver: cq-quickstart-6.5.0.war
* Dispatcher 4.3.2 eller senare för olika webbservrar och plattformar ([nedladdningslänk](https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html))
* Plugin för Eclipse IDE ([läs mer och ladda ned](/help/sites-developing/aem-eclipse.md))

* Tillägg för Brackets Code Editor ([läs mer och ladda ned](/help/sites-developing/aem-brackets.md))
* Maven/Gradle-beroenden ([nedladdningslänk](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/aem/uber-jar/6.5.0/))

**Webbplatser**

* Kärnkomponenter ([GitHub-projekt](https://github.com/adobe/aem-core-wcm-components))
* Implementering av referens för butik ([läs mer](/help/sites-developing/we-retail.md))
* Maven Project Archetypes:

   * för fullstacksplatser: [GitHub-projekt](https://github.com/adobe/aem-project-archetype)
   * för ensidiga appar med React/Angular: [GitHub-projekt](https://github.com/adobe/aem-spa-project-archetype)

* AEM Screens Players för olika målplattformar ([ladda ned](https://download.macromedia.com/screens/))

* Språkmodeller för smart innehåll. Engelska är förinstallerat - fler språk kan hämtas

   * [Tyska](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [Spanska](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [Italienska](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [Franska](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-fr)

* AEM Modernize Tools Suite, t.ex. Dialog Conversion Tool. ([GitHub-projekt](https://github.com/adobe/aem-modernize-tools))

**Resurser**

* Paket för att lägga till förbättrad PDF-rastrerare ([läs mer](/help/assets/aem-pdf-rasterizer.md))
* Paket för att lägga till stöd för utökad RAW-bild ([läs mer](/help/assets/camera-raw.md))

**Formulär**

* [Paket för AEM Forms-funktioner](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)
* [AEM Forms OSGi Client SDK](https://repo.adobe.com/nexus/content/repositories/public/com/adobe/aemfd/aemfd-client-sdk/6.0.80/)

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

Experience Manager 6.5 har certifierats för GB18030-2005 CITS för att använda den kinesiska kodningsstandarden.

## Installera och uppdatera {#install-update}

Se [installationsanvisningarna](/help/sites-deploying/custom-standalone-install.md) för installationskrav.

Mer information finns i [uppgraderingsdokumentationen](/help/sites-deploying/upgrade.md) .

## Plattformar som stöds {#supported-platforms}

Den fullständiga matrisen med plattformar som stöds finns här. Supportnivå för [AEM 6.5 - tekniska krav](/help/sites-deploying/technical-requirements.md)

Oak MicroKernel forOak MicroKernel for

>[!NOTE]
>
>Oracle har flyttat till en LTS-modell (Long Term Support) för Oracle Java SE-produkter. Java 9 och 10 är icke-LTS-versioner från Oracle (se [Oracle Java SE support roadmap](https://www.oracle.com/technetwork/java/eol-135779.html)). Adobe ger endast stöd för LTS-versioner av Java för att köra AEM i produktionen. Därför rekommenderas Java 11 för AEM 6.5.

## Föråldrade och borttagna funktioner {#deprecated-and-removed-features}

Adobe utvärderar ständigt funktionerna i produkten och planerar att ersätta funktioner med kraftfullare versioner, eller bestämmer sig för att omimplementera utvalda delar så att de blir bättre förberedda för framtida förväntningar eller tillägg.

För Adobe Experience Manager 6.5, [läs listan över borttagna funktioner](/help/release-notes/deprecated-removed-features.md). Sidan innehåller även förhandsmeddelanden om förändringar inom en nära framtid och viktiga meddelanden för kunder som uppdaterar från tidigare versioner.

## Kända fel {#known-issues}

[Lista över kända fel](/help/release-notes/known-issues.md)

### Nedladdning och support av produkter (begränsade platser) {#product-download-and-support-restricted-sites}

Dessa webbplatser är bara tillgängliga för kunder. Om du är kund och behöver åtkomst kontaktar du din kontoansvarige på Adobe.

* [](https://daycare.day.com) Hämta [produkt på licensing.adobe.com](https://licensing.adobe.com/)

* [Kundsupport på day.day.com](https://daycare.day.com)

