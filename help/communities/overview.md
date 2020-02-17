---
title: Översikt över AEM Communities
seo-title: Översikt över AEM Communities
description: En översikt över funktionerna och konfigurationen i AEM Communities
seo-description: En översikt över funktionerna och konfigurationen i AEM Communities
uuid: 14405847-36ae-4958-bdc6-d799ecd05f06
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 44374006-f711-4af8-a1fe-f89164f79581
docset: aem65
translation-type: tm+mt
source-git-commit: 70e6f2d8366456e5091b7b775dc40914948921ab

---


# Översikt över AEM Communities{#aem-communities-overview}

Med Adobe Experience Manager Communities (AEM) kan ni snabbt skapa en lokal communitysajt som har bättre prestanda, förbättrad webbplatshantering och uppmuntrar till konvertering av besökare till värdefulla communitymedlemmar.

Kontakta din kontorepresentant för att få information om licensiering av AEM Communities samt ytterligare licensiering för aktiveringsfunktioner och Adobe Analytics.

## Funktioner i Communities {#communities-features}

Med AEM Communities kan man utveckla en relation med webbplatsbesökare som

* **informerar** genom bloggar, frågor och svar och händelsekalendrar,
* while **getting insights **via forum, kommentarer och annat communityinnehåll, som ofta kallas användargenererat innehåll (UGC).
* Den tillåter** moderering **av betrodda medlemmar i publiceringsmiljön,
* **social inloggning **med Twitter och Facebook,
* **intern översättning** av communityinnehåll,
* **communitygrupper skapar **från publicerad communitywebbplats,
* **poäng **till utmärkelsebrickor,
* **fildelning**,
* **meddelanden **och **aktivitetsströmmar**,

* använder du för att **tagga** (@mention) andra registrerade medlemmar i användargenererat innehåll för att få dem att uppmärksammas.
* Stöder **tangentbordsnavigering** i aktiveringskomponenter (t.ex. Katalog- och kursuppspelning, Uppdrag, Filbibliotek).

Communities-funktioner kan demonstreras med [AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) som är allmänt tillgänglig på GitHub.com eller med den nya referensimplementeringen We.Retail.

## Community Sites {#community-sites}

En community-webbplats är en AEM-webbplats som skapas med en enkel guide som ger en webbplats med många vanliga funktioner som är förkopplade till webbplatsen.

Guiden [Skapa](/help/communities/sites-console.md)plats:

* sammanställer funktioner för webbplatsen, baserat på den valda mallen [för](/help/communities/sites.md) communitywebbplats som är:

   * bygger på [communityfunktioner](#community-functions)
   * valfri funktion för [communitygrupper](#communitygroups)

* använder inställningar för att konfigurera:

   * moderering
   * inloggning
   * översättning

* innehåller viktiga funktioner:

   * responsiv design:
använder [Twitter-startteman](https://getbootstrap.com)

   * inloggning:
självregistrering, [social inloggning](/help/communities/social-login.md), användarprofiler

   * meddelanden:
Medlemmar ser händelser som är relevanta för dem och användargenererat innehåll där de är [@nämnda](/help/communities/overview.md#mentionssupport).

   * meddelanden:
medlemmar kan skicka eller ta emot meddelanden på communitywebbplatsen
   * sökning:
möjlighet att söka på communitywebbplatsen
   * språkväxling:
möjlighet att välja språk för en [flerspråkig webbplats](/help/sites-administering/translation.md)

   * administration:
behörighet för behöriga medlemmar att moderera och hantera användare på communitywebbplatsen

* eliminerar många steg i utvecklingen på sidnivå:

   * branding:
valfri överföring av en banderollbild för visning på alla sidor i communitywebbplatsen
   * navigeringsmeny:
navigeringslänkar finns för de funktioner som ingår i communitywebbplatsmallen

Om du snabbt vill skapa en ny communitysajt går du till [Komma igång med AEM Communities](/help/communities/getting-started.md).

## Community Content Persistence {#community-content-persistence}

För att förbättra prestanda och synkronisering av communityinnehåll behöver AEM Communities en gemensam butik specifikt för användargenererat innehåll (UGC) som delas mellan alla AEM-instanser (författare och publicering).

Community-innehåll är enkelt att komma åt via lagringsresursens leverantör (SRP), som tillhandahåller ett lager som åtskiljer åtkomsten från den underliggande topologin och stöder en gemensam lagringsplats för UGC.

Mer information om publicering av communityinnehåll och rekommenderade distributioner finns i:

* [Community Content Storage](/help/communities/working-with-srp.md), som diskuterar de tillgängliga SRP-lagringsalternativen för UGC.
* [Rekommenderade topologier](/help/communities/topologies.md), som diskuterar topologier baserat på användningsfall och SRP-val.
* [Uppgradera till AEM 6.5 Communities](/help/communities/upgrade.md), som ger användbar information om UGC när man går över till AEM 6.5.

## Communities-konsoler {#communities-consoles}

I författarmiljön ger den globala navigeringskonsolen åtkomst till [webbgruppskonsolen](/help/communities/consoles.md), som innehåller:

* [Platskonsol](/help/communities/sites-console.md)

   * webbplatsskapande
   * webbplatsredigering
   * platshantering
   * [Community Groups](/help/communities/groups.md) console

* [Modereringskonsol](/help/communities/moderation.md)

   * allmänt modereringsgränssnitt för massredigering för skribent- och publiceringsmiljöer
   * nya filtervillkor

* [Konsoler för hantering av medlemmar och grupper](/help/communities/members.md)

   * ger möjlighet att skapa och hantera användare på publiceringssidan (medlemmar) från redigeringsmiljön
   * ger möjlighet att förbjuda medlemmar
   * ger möjlighet att skapa och hantera användargrupper på publiceringssidan (medlemsgrupper) från redigeringsmiljön

* [Rapportkonsol](/help/communities/reports.md)

   * ger möjlighet att generera rapporter om uppdrag, inlägg och vyer

* [Resurskonsol](/help/communities/resources.md)

   * ger möjlighet att skapa aktiveringsresurser och utbildningsvägar
   * ger tillgång till rapporter om aktiveringsresurser och utbildningsvägar

Den globala verktygskonsolen ger tillgång till följande webbgruppsverktyg:

* [Konsol för webbplatsmallar](/help/communities/tools.md#sitetemplatesconsole)

   * skapa och hantera communitymallar

* [Konsolen Gruppmallar](/help/communities/tools.md#grouptemplatesconsole)

   * skapa och hantera communitygruppsmallar

* [Konsol för communityfunktioner](/help/communities/tools.md#communityfunctionsconsole)

   * skapa och hantera communityfunktioner

* [Konsol för](/help/communities/tools.md#storageconfiguratonconsole) lagringskonfiguration

   * markera och konfigurera webbplatsens [gemensamma lagringsplats](/help/communities/working-with-srp.md)

* [Komponentguide](/help/communities/components-guide.md)

   * en exempelplats, [Community Components](https://localhost:4502/editor.html/content/community-components/en.html), som innehåller ett exempel på alla webbdelar med standardkonfiguration och möjlighet att experimentera med dem

## Mallar för communitywebbplatser {#community-site-templates}

Skapandet av communitysajter bygger på ett urval av mallar för communitysajter som snabbt skapar en community som är oberoende av valfri exempelwebbplats.

En mall för communitysajter, som består av communityfunktioner och mallar för communitygrupper, innehåller en struktur för en community-webbplats som inloggning, användarprofiler, meddelanden, webbplatsmeny, sökning, teman och varumärken.

Se konsolen [](/help/communities/sites.md)Platsmallar.

## Community-funktioner {#community-functions}

De funktioner som förväntas av en community-upplevelse är välkända. Med AEM Communities finns dessa funktioner som byggstenar, så kallade communityfunktioner.

Community-funktioner är vanliga AEM-sidor som innehåller komponenter som är kopplade till en funktion som enkelt kan införlivas i en community-mall.

Se [användarfunktionskonsolen](/help/communities/functions.md).

## Community-grupper och gruppmallar {#community-groups-and-group-templates}

Funktionen för communitygrupper är möjligheten för en undercommunity att skapas dynamiskt på en community-webbplats av behöriga användare och communitymedlemmar från både författarmiljön och publiceringsmiljön.

I författarmiljön kan communitygrupper (undergrupper) skapas inom en befintlig communitywebbplats eller kapslas inom en befintlig grupp när mallstrukturen innehåller [gruppfunktionen](/help/communities/functions.md#groups-function).

När du skapar en community-grupp måste du välja en community-gruppmall som innehåller designen för communitygruppssidorna. När en gruppfunktion läggs till i en mallstruktur konfigureras den att antingen ange en gruppmall eller välja mallar när en ny gruppgrupp skapas.

Se även:

* [Konsol](/help/communities/groups.md) för webbplatsgrupper för att skapa undergrupper i författarmiljön
* [Konsol](/help/communities/tools-groups.md) för gruppmallar för att skapa platsstruktur för grupper
* [Komma igång med AEM Communities](/help/communities/getting-started.md) för självstudiekurs för att snabbt skapa en community-webbplats med kapslade grupper

## Community-komponenter {#community-components}

De [communitykomponenter](/help/communities/author-communities.md) som en communitywebbplats byggs från kan användas för att lägga till communityfunktioner på en AEM-webbplats.

Komponentguiden [för](/help/communities/components-guide.md) communityn finns tillgänglig för interaktiv utforskning av komponenterna.

## Typ av Communities {#types-of-communities}

### Engagement Community {#engagement-community}

En engagemangscommunity är en communitywebbplats som fokuserar på att engagera kunder för att informera, begära feedback och låta kunderna interagera som communitymedlemmar.

En engagemangscommunity kan innehålla:

* inloggning
* meddelanden
* forum
* kommentarer
* recensioner
* omdömen
* röstning
* bloggar
* grupper
* kalendrar
* översättning
* moderering
* meddelanden
* poängsättning och märken
* analysrapportering

Om du snabbt vill skapa en ny engagemangscommunity kan du besöka [Getting Started with AEM Communities](/help/communities/getting-started.md).

### Aktivera community {#enablement-community}

En community för hjälpsystem är en communitywebbplats som innehåller funktioner för onlineutbildning.

En community för aktivering kan innehålla:

* alla funktioner i en [engagemangscommunity](#engagement-community)
* möjlighet att tilldela innehåll och utbildningsresurser till medlemmar och medlemsgrupper
* har stöd för SCORM-innehåll, t.ex. frågor och tester
* spårning av uppdragsslutförande
* tillgång till rapportering och analys
* möjlighet att diskutera en utbildningsresurs via forum, meddelanden, kommentarer och omdömen

En aktiveringscommunity kan skapas när [aktiveringstillägget har konfigurerats](/help/communities/enablement.md), vilket kräver ytterligare licensiering för användning i en produktionsmiljö. En community-webbplats för aktivering kommer att innehålla [tilldelningsfunktionen](#community-functions).

Om du enkelt vill skapa en ny aktiveringscommunity går du till [Komma igång med AEM Communities för aktivering](/help/communities/getting-started-enablement.md).

## AEM Demo Machine {#aem-demo-machine}

AEM [Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) hanterar och kör demonstrationer för AEM [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [Communities](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [Apps](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) [](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)ochForms¥, som ofta kräver mer konfiguration än att bara starta en QuickStart-instans. AEM Demo Machine kommer att konfigurera ytterligare [infrastrukturer](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) som MongoDB-, Solr-, MySQL-, FFmpeg- och e-postservrar.

AEM Demo Machine innehåller:

* ett [grafiskt användargränssnitt](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface)
* Apache ANT-skript med konfigurerbara [egenskaper](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) och [mål](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line)

* paket att installera

AEM Demo Machine har testats med CQ 5.5, CQ 5.6.1, AEM 6.0, AEM 6.1, AEM 6.2, AEM 6.3 och AEM 6.4 i Windows, MacOS och Linux.

AEM Demo Machine kräver en giltig AEM-licens.

>[!NOTE]
>
>Se en [videointroduktion](https://www.youtube.com/watch?v=zEE_zkR9fVQ&feature=youtu.be) till AEM Demo Machine (13:26).

## AEM Communities-dokumentation {#aem-communities-documentation}

* Besök [Distribuera communityn](/help/communities/deploy-communities.md) om du vill veta mer om rekommenderade distributioner.
* Besök [Administrera communitysajter](/help/communities/administer-landing.md) om du vill veta mer om hur du skapar en community-webbplats, lägger till communitygrupper, konfigurerar mallar för communitysajter, modererar communityinnehåll, hanterar medlemmar, taggar, meddelanden, poängsättning och märken.
* Besök [Utvecklingsgrupper](/help/communities/communities.md) om du vill veta mer om ramverket för sociala komponenter (SCF) och hur du anpassar komponenter och funktioner i Communities.
* Besök [Authoring Communities Components](/help/communities/author-communities.md) om du vill veta mer om hur du skapar med och konfigurerar Communities-komponenter.

