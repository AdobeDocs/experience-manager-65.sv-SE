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
source-git-commit: 48afa2146d0dcbab4beaa1044645c269b49fd7ff

---


# Översikt över AEM Communities {#aem-communities-overview}

Med Adobe Experience Manager Communities (AEM) kan ni snabbt skapa en lokal communitywebbplats som har bättre prestanda, förbättrad webbplatshantering och uppmuntrar till konvertering av besökare till värdefulla communitymedlemmar.

Kontakta din kontorepresentant för att få information om licensiering av AEM Communities samt ytterligare licensiering för aktiveringsfunktioner och Adobe Analytics.

## Funktioner i Communities {#communities-features}

Med AEM Communities kan man utveckla en relation med webbplatsbesökare som

* **Information** via bloggar, frågor och svar och händelsekalendrar,
* Samtidigt som ni **får insikter** via forum, kommentarer och annat communityinnehåll, som ofta kallas användargenererat innehåll (UGC).
* Den tillåter **moderering** av betrodda medlemmar i publiceringsmiljön,
* **Social inloggning** med Twitter och Facebook,
* **Inline translation** of community content,
* **Skapande** av communitygrupper från den publicerade communitywebbplatsen,
* **Betygsätta** för utmärkelsebrickor,
* **Fildelning**,
* **Meddelanden** och **aktivitetsströmmar**,
* Gör att andra registrerade medlemmar i användargenererat innehåll kan uppmärksammas genom att **tagga** (@mention).
* Stöder **tangentbordsnavigering** i aktiveringskomponenter (t.ex. Katalog- och kursuppspelning, Uppdrag, Filbibliotek).

Communities-funktioner kan demonstreras med [AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) som är allmänt tillgänglig på GitHub.com eller med den nya referensimplementeringen We.Retail.

## Community Sites {#community-sites}

En community-webbplats är en AEM-webbplats som skapas med en enkel guide som ger en webbplats med många vanliga funktioner som är förkopplade till webbplatsen.

Guiden [Skapa](/help/communities/sites-console.md)plats:

* Sammanställer funktioner för webbplatsen, baserat på den valda [communitywebbplatsmallen](/help/communities/sites.md) som är:

   * bygger på [communityfunktioner](#community-functions)
   * valfri funktion för [communitygrupper](#communitygroups)

* Använder inställningar för att konfigurera:

   * moderering
   * inloggning
   * översättning

* Innehåller viktiga funktioner:

   * Responsiv design: använder [Twitter-startteman](https://getbootstrap.com)

   * Inloggning: självregistrering, [social inloggning](/help/communities/social-login.md), användarprofiler

      * Meddelanden:
Medlemmar ser händelser som är relevanta för dem och användargenererat innehåll där de är [@nämnda](/help/communities/overview.md#mentionssupport).

      * Meddelanden: Medlemmar kan skicka eller ta emot meddelanden på communitywebbplatsen.
      * Sök: möjlighet att söka på communitywebbplatsen.
      * Språkväxling: möjlighet att välja språk för en [flerspråkig webbplats](/help/sites-administering/translation.md).

      * Administration: åtkomst för behöriga medlemmar att moderera och hantera användare på communitywebbplatsen.

* Eliminerar många steg i utvecklingen på sidnivå:

   * Varumärke: valfri överföring av en banderollbild för visning på alla sidor i communitywebbplatsen
      * Navigeringsmeny: navigeringslänkar finns för de funktioner som ingår i communitywebbplatsmallen.

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

   * Skapa webbplats
   * Webbplatsredigering
   * Platshantering
   * [Community Groups](/help/communities/groups.md) console

* [Modereringskonsol](/help/communities/moderation.md)

   * Vanligt gränssnitt för massmoderering för skribent- och publiceringsmiljöer.
   * Nya filtervillkor.

* [Konsoler för hantering av medlemmar och grupper](/help/communities/members.md)

   * Ger möjlighet att skapa och hantera användare på publiceringssidan (medlemmar) från redigeringsmiljön.
   * Möjlighet att förbjuda medlemmar.
   * Ger möjlighet att skapa och hantera användargrupper (medlemsgrupper) på publiceringssidan från redigeringsmiljön.

* [Rapportkonsol](/help/communities/reports.md)

   * Ger möjlighet att generera rapporter om uppdrag, inlägg och vyer.

* [Resurskonsol](/help/communities/resources.md)

   * Ger möjlighet att skapa aktiveringsresurser och utbildningsvägar.
   * Ger tillgång till rapporter om aktiveringsresurser och utbildningsvägar.

Den globala verktygskonsolen ger tillgång till följande verktyg för communities:

* [Konsol för webbplatsmallar](/help/communities/tools.md#sitetemplatesconsole)

   * Skapa och hantera mallar för communitysajter.

* [Konsolen Gruppmallar](/help/communities/tools.md#grouptemplatesconsole)

   * Skapa och hantera communitygruppsmallar.

* [Konsol för communityfunktioner](/help/communities/tools.md#communityfunctionsconsole)

   * Skapa och hantera communityfunktioner.

* [Konsol för](/help/communities/tools.md#storageconfiguratonconsole) lagringskonfiguration

   * Välj och konfigurera platsens [gemensamma lagringsplats](/help/communities/working-with-srp.md) .

* [Komponentguide](/help/communities/components-guide.md)

   * En exempelplats, [Community Components](https://localhost:4502/editor.html/content/community-components/en.html), som innehåller ett exempel på alla Communities-komponenter med deras standardkonfiguration och möjlighet att experimentera med dem.

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

* [Webbplatsgruppskonsol](/help/communities/groups.md) för att skapa undergrupper i författarmiljön.
* [Konsolen](/help/communities/tools-groups.md) Gruppmallar för att skapa platsstruktur för grupper.
* [Komma igång med AEM Communities](/help/communities/getting-started.md) för självstudiekurs för att snabbt skapa en communitysajt med kapslade grupper.

## Community-komponenter {#community-components}

De [communitykomponenter](/help/communities/author-communities.md) som en communitywebbplats byggs från kan användas för att lägga till communityfunktioner på en AEM-webbplats.

Komponentguiden [för](/help/communities/components-guide.md) communityn finns tillgänglig för interaktiv utforskning av komponenterna.

## Typ av Communities {#types-of-communities}

### Engagement Community {#engagement-community}

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

Om du snabbt vill skapa en ny engagemangscommunity kan du besöka [Getting Started with AEM Communities](/help/communities/getting-started.md).

### Aktivera community {#enablement-community}

En community för hjälpsystem är en communitywebbplats som innehåller funktioner för onlineutbildning.

En community för aktivering kan innehålla:

* Alla funktioner i en [engagemangscommunity](#engagement-community).
* möjlighet att tilldela innehåll och inlärning. till medlemmar och medlemsgrupper.
* Stöder SCORM-innehåll, t.ex. frågor och tester.
* Spårning av slutförda tilldelningar.
* Tillgång till rapporter och analyser.
* Möjlighet att diskutera en utbildningsresurs via forum, meddelanden, kommentarer och omdömen.

En aktiveringscommunity kan skapas när [aktiveringstillägget har konfigurerats](/help/communities/enablement.md), vilket kräver ytterligare licensiering för användning i en produktionsmiljö. En community-webbplats för aktivering kommer att innehålla [tilldelningsfunktionen](#community-functions).

Om du enkelt vill skapa en ny aktiveringscommunity går du till [Komma igång med AEM Communities för aktivering](/help/communities/getting-started-enablement.md).

## AEM Demo Machine {#aem-demo-machine}

AEM [Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) hanterar och kör demonstrationer för AEM [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [Communities](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [Apps](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) [](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)ochForms¥, som ofta kräver mer konfiguration än att bara starta en QuickStart-instans. AEM Demo Machine kommer att konfigurera ytterligare [infrastrukturer](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) som MongoDB-, Solr-, MySQL-, FFmpeg- och e-postservrar.

AEM Demo Machine innehåller:

* Ett [grafiskt användargränssnitt](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface).
* Apache ANT-skript med konfigurerbara [egenskaper](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) och [mål](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line).

* Paket som ska installeras.

AEM Demo Machine har testats med CQ 5.5, CQ 5.6.1, AEM 6.0, AEM 6.1, AEM 6.2, AEM 6.3 och AEM 6.4 i Windows, MacOS och Linux.

AEM Demo Machine kräver en giltig AEM-licens.

>[!NOTE]
>
>Se en [videointroduktion](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) till AEM Demo Machine (13:26).


## AEM Communities-dokumentation {#aem-communities-documentation}

* Besök [Distribuera communityn](deploy-communities.md) om du vill veta mer om rekommenderade distributioner.
* Besök [Administrera communitysajter](administer-landing.md) om du vill veta mer om hur du skapar en community-webbplats, lägger till communitygrupper, konfigurerar mallar för communitysajter, modererar communityinnehåll, hanterar medlemmar, taggar, meddelanden, poängsättning och märken.
* Besök [Utvecklingsgrupper](communities.md) om du vill veta mer om ramverket för sociala komponenter (SCF) och hur du anpassar komponenter och funktioner i Communities.
* Besök [Authoring Communities Components](author-communities.md) om du vill veta mer om hur du skapar med och konfigurerar Communities-komponenter.

