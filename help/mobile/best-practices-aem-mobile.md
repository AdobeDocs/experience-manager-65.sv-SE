---
title: Bästa praxis
seo-title: Bästa praxis
description: Följ den här sidan om du vill lära dig bästa praxis och riktlinjer som hjälper erfarna utvecklare AEM webbplatser som vill skapa mallar och komponenter för mobilappar.
seo-description: Följ den här sidan om du vill lära dig bästa praxis och riktlinjer som hjälper erfarna utvecklare AEM webbplatser som vill skapa mallar och komponenter för mobilappar.
uuid: 7733c8b1-a88c-455c-8080-f7add4205b92
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a0647696-72c3-409b-85ba-9275d8f99cff
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 1%

---


# Bästa praxis {#best-practices}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

Att skapa en AEM Mobile On-demand Services-app skiljer sig från att skapa en app som körs direkt i Cordova-skalet (eller PhoneGap-skalet). Utvecklarna bör känna till

* Plugin-program som kan användas direkt, liksom AEM Mobile-specifika plugin-program.

>[!NOTE]
>
>Mer information om plugin-program finns i följande resurser:
>
>* [Använda Cordova-plugin-program i AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [Använda AEM Mobile-specifika Cordova-aktiverade plugin-program](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)

>



* Mallar som använder plugin-funktioner bör skrivas på ett sådant sätt att de fortfarande är redigerbara i webbläsaren, utan att plugin-bron finns.

   * Se till att du väntar på funktionen *device* innan du försöker komma åt ett plugin-programs API.

## Riktlinjer för AEM utvecklare {#guidelines-for-aem-developers}

Följande riktlinjer är till hjälp för erfarna utvecklare AEM webbplatser som vill skapa mallar och komponenter för mobilappar:

**Strukturera AEM webbplatsmallar för att uppmuntra återanvändning och utbyggbarhet**

* Föredra flera komponentskriptfiler framför en enda monolitisk fil

   * Det finns ett antal tomma tilläggspunkter, t.ex. *customheaderlibs.html* och *customfooterlibs.html*, som gör att utvecklaren kan ändra sidmallen och duplicera så lite kärnkod som möjligt
   * Mallar kan sedan utökas och anpassas via Sling-funktionen *sling:resourceSuperType*

* Föredra Sightly/HTL framför JSP som mallspråk

   * Om du använder det här förhindrar du att koden separeras från markeringar, erbjuder inbyggt XSS-skydd och har en mer välbekant syntax

**Optimera för prestanda på enheter**

* Artikelspecifika skript och formatmallar ska inkluderas i artikelns nyttolast med hjälp av innehållsmallen dps-article contentsync
* Skript och formatmallar som delas av mer än en artikel ska inkluderas i delade resurser via innehållsmallen dps-HTMLResources contentsync
* Referera inte till externa skript som är renderingsblockerande

>[!NOTE]
>
>Mer information om återgivningsblockerande externa skript [finns här](https://developers.google.com/speed/docs/insights/BlockingJS).

**Föredra programspecifika JS- och CSS-bibliotek i klientsidan framför webbspecifika**

* För att undvika att dyka upp i bibliotek som jQuery Mobile för att hantera en enorm bredd av enheter och webbläsare
* När en mall körs i en apps webbvy har du kontroll över de plattformar och versioner som appen kommer att ha stöd för, samt kunskapen om att det finns stöd för JavaScript. Använd till exempel Ionic (kanske bara CSS) framför jQuery Mobile och Onsen i stället för Bootstrap.

>[!NOTE]
>
>Om du vill veta mer om jQuery Mobile klickar du [här](https://jquerymobile.com/browser-support/1.4/).

**Föredra mikrobibliotek framför högar**

* Den tid det tar att lägga in materialet i enhetens glas kommer att sänkas för varje bibliotek som artikeln/artiklarna är beroende av. Den här nedgången förvärras när en ny webbvy används för att återge varje artikel, så varje bibliotek måste initieras igen från början
* Om artiklarna inte har skapats som SPA (appar med en sida) behöver du förmodligen inte inkludera ett fullständigt stackbibliotek som vinkelrät
* Använd mindre bibliotek med ett enda syfte för att lägga till den interaktivitet som sidan kräver, till exempel [Fastclick](https://github.com/ftlabs/fastclick) eller [Velocity.js](https://velocityjs.org)

**Minimera artikelnyttolastens storlek**

* Använd minsta möjliga resurser som effektivt kan täcka den största visningsruta ni stöder, med en rimlig upplösning
* Använd ett verktyg som *ImageOptime* på dina bilder för att ta bort överflödiga metadata

## Komma framåt {#getting-ahead}

Mer information om de två andra rollerna och ansvarsområdena finns i resurserna nedan:

* [Administratör](/help/mobile/aem-mobile.md)
* [Författare](/help/mobile/aem-mobile-on-demand.md)
