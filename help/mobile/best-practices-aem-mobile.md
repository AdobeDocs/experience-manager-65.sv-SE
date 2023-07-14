---
title: Best Practices for AEM Mobile On-demand Services
description: Lär dig mer om bästa praxis och riktlinjer som hjälper erfarna utvecklare av webbplatser som vill skapa mallar och komponenter för mobilappar.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---

# Bästa praxis {#best-practices}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

Att skapa en AEM Mobile On-demand Services-app skiljer sig från att skapa en app som körs direkt i Cordova-skalet (eller PhoneGap-skalet). Utvecklarna bör känna till

* Plugin-program som kan användas direkt och AEM Mobile-specifika plugin-program.

>[!NOTE]
>
>Mer information om plugin-program finns i följande resurser:
>
>* [Använda Cordova-plugin-program i AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [Använda AEM Mobile-specifika Cordova-aktiverade plugin-program](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)
>

* Mallar som använder plugin-funktioner bör skrivas på ett sådant sätt att de fortfarande är redigerbara i webbläsaren, utan att plugin-bron finns.

   * Se till att vänta på *avskild* innan du försöker komma åt ett plugin-programs API.

## Riktlinjer för AEM utvecklare {#guidelines-for-aem-developers}

Följande riktlinjer hjälper erfarna utvecklare AEM webbplatser som vill skapa mallar och komponenter för mobilappar:

**Strukturera AEM webbplatsmallar för att uppmuntra återanvändning och utbyggbarhet**

* Föredra flera komponentskriptfiler framför en enda monolitisk fil

   * Flera tomma tilläggspunkter anges, till exempel *customheaderlibs.html* och *customfooterlibs.html* som gör att utvecklaren kan ändra sidmallen samtidigt som så lite kärnkod som möjligt dupliceras
   * Mallar kan sedan utökas och anpassas via Sling *sling:resourceSuperType* mekanism

* Föredra Sightly/HTL framför JSP som mallspråk

   * Om du använder det här förhindrar du att koden separeras från markeringar, erbjuder inbyggt XSS-skydd och har en mer välbekant syntax

**Optimera för prestanda på enheter**

* Artikelspecifika skript och formatmallar ska inkluderas i artikelnyttolasten med hjälp av innehållsmallen dps-article contentSync
* Skript och formatmallar som delas av mer än en artikel bör inkluderas i delade resurser via innehållsmallen dps-HTMLResources contentsync
* Referera inte till externa skript som är renderingsblockerande

>[!NOTE]
>
>Du kan läsa mer i detalj om återgivningsblockerande externa skript [här](https://developers.google.com/speed/docs/insights/BlockingJS).

**Föredra programspecifika JS- och CSS-bibliotek i klientsidan framför webbspecifika**

* För att undvika att dyka upp i bibliotek som jQuery Mobile för att hantera en enorm bredd av enheter och webbläsare
* När en mall körs i en apps webbvy har du kontroll över de plattformar och versioner som appen kommer att ha stöd för, och du vet att det finns stöd för JavaScript. Använd till exempel Ionic (kanske bara CSS) framför jQuery Mobile och Onsen i stället för Bootstrap.

>[!NOTE]
>
>Om du vill veta mer om jQuery Mobile klickar du på [här](https://jquerymobile.com/browser-support/1.4/).

**Föredra mikrobibliotek framför högar**

* Den tid det tar att få in materialet på enhetens glas kommer att bromsas av alla bibliotek som era artiklar är beroende av. Den här nedgången förvärras när en ny webbvy används för att återge varje artikel, så varje bibliotek måste initieras igen från början
* Om artiklarna inte har skapats som SPA (appar för en sida) behöver du förmodligen inte inkludera ett fullständigt stackbibliotek som Angular
* Använd mindre bibliotek med ett enda syfte för att lägga till den interaktivitet sidan kräver, till exempel [Snabbklickning](https://github.com/ftlabs/fastclick) eller [Velocity.js](https://velocityjs.org)

**Minimera artikelnyttolastens storlek**

* Använd minsta möjliga resurser som effektivt kan täcka den största visningsruta ni stöder, med en rimlig upplösning
* Använd ett verktyg som *ImageOptime* på bilderna för att ta bort överflödiga metadata

## Komma framåt {#getting-ahead}

Mer information om de två andra rollerna och ansvarsområdena finns i resurserna nedan:

* [Administratör](/help/mobile/aem-mobile.md)
* [Författare](/help/mobile/aem-mobile-on-demand.md)
