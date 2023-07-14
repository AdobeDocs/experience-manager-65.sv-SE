---
title: AEM Communities - översikt
description: En översikt över AEM Communities funktioner och inställningar
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
exl-id: d6243dff-a067-455c-a326-5f451f225efd
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# AEM Communities - översikt {#aem-communities-overview}

Adobe Experience Manager (AEM) Communities ger möjlighet att snabbt skapa en lokal communitysajt som har förbättrade prestanda, förbättrad webbplatshantering och uppmuntrar till konvertering av besökare till värdefulla communitymedlemmar.

## Funktioner i Communities {#communities-features}

Med AEM Communities kan man utveckla en relation med besökare på en webbplats som:

* **Information** via bloggar, frågor och svar och händelsekalendrar,
* while **få insikter** via forum, kommentarer och annat communityinnehåll, som ofta kallas användargenererat innehåll (UGC).
* Den tillåter **moderering** av betrodda medlemmar i publiceringsmiljön,
* **Social inloggning** med Twitter och Facebook,
* **Textbunden översättning** av communityinnehåll,
* **Skapande av communitygrupper** från den publicerade communitywebbplatsen,
* **Poäng** till utmärkelsebrickor,
* **Fildelning**,
* **Meddelanden** och **aktivitetsströmmar**,
* Tillåter **taggning** (@mention) andra registrerade medlemmar i användargenererat innehåll för att få uppmärksamhet.

Funktioner i Communities kan visas med [AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) som är tillgängliga offentligt på GitHub.com eller med den nya implementeringen av referensen We.Retail.

## Community Sites {#community-sites}

En communitywebbplats är en AEM webbplats som skapats med en enkel guide som ger en webbplats med många vanliga funktioner som är förkopplade till webbplatsen.

The [guide för att skapa webbplatser](/help/communities/sites-console.md):

* Sammanställer funktioner för webbplatsen, baserat på det valda [mall för communitywebbplats](/help/communities/sites.md) som är:

   * skapat från [communityfunktioner](#community-functions)
   * valfri [communitygrupper](#communitygroups) funktion

* Använder inställningar för att konfigurera:

   * moderering
   * inloggning
   * översättning

* Innehåller viktiga funktioner:

   * Responsiv design: använder [Twitter Bootstrap-teman](https://getbootstrap.com)

   * Logga in: självregistrering, [social inloggning](/help/communities/social-login.md), användarprofiler

      * Meddelanden: medlemmar ser händelser som är relevanta för dem och användargenererat innehåll där de är [@nämnda](/help/communities/overview.md#mentionssupport).

      * Meddelanden: Medlemmar kan skicka eller ta emot meddelanden på communitywebbplatsen.
      * Sök: möjlighet att söka på communitywebbplatsen.
      * Språkväxling: möjlighet att välja språk för [flerspråkig webbplats](/help/sites-administering/translation.md).

      * Administration: åtkomst för behöriga medlemmar att moderera och hantera användare på communitywebbplatsen.

* Eliminerar många steg i utvecklingen på sidnivå:

   * Varumärke: valfri överföring av en banderollbild för visning på alla sidor i communitywebbplatsen
   * Navigeringsmeny: navigeringslänkar finns för de funktioner som ingår i communitywebbplatsmallen.

Om du snabbt vill skapa en communitysajt kan du besöka [Komma igång med AEM Communities](/help/communities/getting-started.md).

## Community Content Persistence {#community-content-persistence}

För att förbättra prestanda och synkronisering av communityinnehåll behöver AEM Communities en gemensam lagringsplats för användargenererat innehåll (UGC) som delas mellan alla AEM (författare och publicering) instanser.

Community-innehåll är enkelt att komma åt via lagringsresursens leverantör (SRP), som tillhandahåller ett lager som åtskiljer åtkomsten från den underliggande topologin och stöder en gemensam lagringsplats för UGC.

Mer information om publicering av communityinnehåll och rekommenderade distributioner finns i:

* [Community-innehåll](/help/communities/working-with-srp.md)- diskuterar de tillgängliga SRP-lagringsalternativen för UGC.
* [Rekommenderade topologier](/help/communities/topologies.md)- diskuterar topologier baserat på användningsfall och SRP-val.
* [Uppgradera till AEM 6.5 Communities](/help/communities/upgrade.md)- ger användbar information om UGC vid övergång till AEM 6.5.

## Communities-konsoler {#communities-consoles}

I författarmiljön ger den globala navigeringskonsolen åtkomst till [Communities-konsol](/help/communities/consoles.md), som innehåller:

* [Webbplatser](/help/communities/sites-console.md) konsol

   * Skapa webbplats
   * Webbplatsredigering
   * Platshantering
   * [Community-grupper](/help/communities/groups.md) konsol

* [Moderering](/help/communities/moderation.md) konsol

   * Vanligt gränssnitt för massmoderering för skribent- och publiceringsmiljöer.
   * Nya filtervillkor.

* [Medlemmar och grupper](/help/communities/members.md) hanteringskonsoler

   * Ger möjlighet att skapa och hantera användare på publiceringssidan (medlemmar) från redigeringsmiljön.
   * Möjlighet att förbjuda medlemmar.
   * Ger möjlighet att skapa och hantera användargrupper (medlemsgrupper) på publiceringssidan från redigeringsmiljön.

* [Rapporter](/help/communities/reports.md) konsol

   * Ger möjlighet att generera rapporter om uppdrag, inlägg och vyer.

Den globala verktygskonsolen ger tillgång till följande verktyg för communities:

* [Webbplatsmallar](/help/communities/tools.md#sitetemplatesconsole) konsol

   * Skapa och hantera mallar för communitysajter.

* [Gruppmallar](/help/communities/tools.md#grouptemplatesconsole) konsol

   * Skapa och hantera communitygruppsmallar.

* [Community-funktioner](/help/communities/tools.md#communityfunctionsconsole) konsol

   * Skapa och hantera communityfunktioner.

* [Lagringskonfiguration](/help/communities/tools.md#storageconfiguratonconsole) konsol

   * Välj och konfigurera [gemensam lagringsplats](/help/communities/working-with-srp.md) för webbplatsen.

* [Komponentguide](/help/communities/components-guide.md)

   * En exempelplats, [Community-komponenter](https://localhost:4502/editor.html/content/community-components/en.html) innehåller ett exempel på alla communitykomponenter med deras standardkonfiguration och möjlighet att experimentera med dem.

## Mallar för communitywebbplatser {#community-site-templates}

Skapandet av communitysajter baseras på ett urval av en mall för communitysajter som snabbt skapar en community som är oberoende av valfri exempelwebbplats.

En mall för communitysajter, som består av communityfunktioner och mallar för communitygrupper, innehåller en struktur för en community-webbplats som inloggning, användarprofiler, meddelanden, webbplatsmeny, sökning, teman och varumärken.

Se [Konsol för webbplatsmallar](/help/communities/sites.md).

## Community-funktioner {#community-functions}

De funktioner som förväntas av en community-upplevelse är välkända. Med AEM Communities finns dessa funktioner som byggstenar, så kallade communityfunktioner.

Community-funktioner är vanliga AEM sidor innehåller komponenter som är sammankopplade i en funktion som enkelt kan integreras i en community-mall.

Se [Konsol för communityfunktioner](/help/communities/functions.md).

## Community-grupper och gruppmallar {#community-groups-and-group-templates}

Funktionen för communitygrupper är möjligheten för en undercommunity att skapas dynamiskt på en community-webbplats av behöriga användare och community-medlemmar från både författarmiljön och publiceringsmiljön.

I författarmiljön kan communitygrupper (undergrupper) skapas inom en befintlig communitywebbplats eller kapslas inom en befintlig grupp när mallstrukturen innehåller [Funktionen Grupper](/help/communities/functions.md#groups-function).

När du skapar en community-grupp måste du välja en community-gruppmall som innehåller designen för communitygruppssidorna. När en gruppfunktion läggs till i en mallstruktur konfigureras den att antingen ange en gruppmall eller välja mallar när en ny gruppgrupp skapas.

Se även:

* [Konsol för webbplatsgrupper](/help/communities/groups.md) för att skapa undergrupper i författarmiljön.
* [Konsolen Gruppmallar](/help/communities/tools-groups.md) för att skapa platsstruktur för grupper.
* [Komma igång med AEM Communities](/help/communities/getting-started.md) för självstudiekurs för att snabbt skapa en community-webbplats med kapslade grupper.

## Community-komponenter {#community-components}

The [communitykomponenter](/help/communities/author-communities.md) från vilken en communitywebbplats byggs kan användas för att lägga till communityfunktioner till valfri AEM.

The [communitykomponentguide](/help/communities/components-guide.md) finns för interaktiv utforskning av komponenterna.

## Engagement Community {#engagement-community}

En engagemangscommunity är en communitywebbplats som fokuserar på att engagera kunder för att informera, begära feedback och låta kunderna interagera som communitymedlemmar.

En engagemangscommunity kan innehålla:

* Inloggning
* Meddelanden
* Forum
* Kommentarer
* Recensioner
* Klassificeringar
* Omröstning
* Bloggar
* Grupper
* Kalendrar
* Översättning
* Moderering
* Meddelanden
* Betyg och emblem
* Analysrapporter

Om du snabbt vill skapa en engagemangscommunity kan du besöka [Komma igång med AEM Communities](/help/communities/getting-started.md).

## AEM Demo Machine {#aem-demo-machine}

The [AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) hanterar och kör demonstrationer för AEM [Webbplatser](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [Resurser](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [Communities](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [Appar](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) och [Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms), som ofta kräver mer konfiguration än att bara starta en QuickStart-instans. AEM Demo Machine konfigurerar ytterligare [infrastruktur](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) som MongoDB-, Solr-, MySQL-, FFmpeg- och e-postservrar.

Den AEM demomaskinen innehåller:

* A [grafiskt användargränssnitt](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface).
* Apache ANT-skript med konfigurerbara [egenskaper](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) och [mål](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line).

* Paket som ska installeras.

AEM Demo Machine har testats med CQ 5.5, CQ 5.6.1, AEM 6.0, AEM 6.1, AEM 6.2, AEM 6.3 och AEM 6.4 i Windows, MacOS och Linux®.

AEM Demo Machine kräver en giltig AEM.

>[!NOTE]
>
>Visa en [videointroduktion](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) till AEM Demo Machine (13:26).

## AEM Communities Documentation {#aem-communities-documentation}

* Besök [Distribuera webbgrupper](deploy-communities.md) om du vill veta mer om rekommenderade distributioner.
* Besök [Administrera webbgruppsplatser](administer-landing.md) om du vill veta mer om hur du skapar en community-webbplats, lägger till communitygrupper, konfigurerar mallar för communitywebbplatser, modererar communityinnehåll, hanterar medlemmar, taggning, meddelanden, poängsättning och emblem.
* Besök [Utveckla webbgrupper](communities.md) om du vill veta mer om ramverket för sociala komponenter (SCF) och hur du anpassar komponenter och funktioner i Communities.
* Besök [Komponenter i redigeringsgrupper](author-communities.md) om du vill lära dig hur du redigerar med och konfigurerar Communities-komponenter.
