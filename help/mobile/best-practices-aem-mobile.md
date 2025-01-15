---
title: Best Practices for AEM Mobile On-demand Services
description: Lär dig mer om de effektivaste strategierna och riktlinjerna som hjälper behöriga Adobe Experience Manager-utvecklare (AEM) att skapa mallar och komponenter för mobilappar.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# Bästa praxis {#best-practices}

{{ue-over-mobile}}

Att skapa en AEM Mobile On-demand Services-app skiljer sig från att skapa en app som körs direkt i Cordova-skalet (eller PhoneGap-skalet). Utvecklarna bör känna till

* Plugin-program som kan användas direkt och Adobe Experience Manager (AEM) Mobile-specifika plugin-program.

>[!NOTE]
>
>Mer information om plugin-program finns i följande resurser:
>
>* [Använda Cordova-plugin-program i AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [Använda AEM Mobile-specifika Cordova-aktiverade plugin-program](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)
>

* Mallar som använder plugin-funktioner bör skrivas på ett sådant sätt att de fortfarande är redigerbara i webbläsaren, utan att plugin-bryggan finns.

   * Se till att du väntar på funktionen *device* innan du försöker komma åt ett plugin-programs API.

## Riktlinjer AEM utvecklare {#guidelines-for-aem-developers}

Följande riktlinjer hjälper AEM utvecklare av webbplatser som vill skapa mallar och komponenter för mobilappar:

**Strukturera AEM webbplatsmallar för att uppmuntra återanvändning och utbyggbarhet**

* Föredra flera komponentskriptfiler i stället för en enda

   * Det finns flera tomma tilläggspunkter, till exempel *customheaderlibs.html* och *customfooterlibs.html*, som utvecklaren kan använda för att ändra sidmallen och samtidigt duplicera så lite kärnkod som möjligt
   * Mallar kan sedan utökas och anpassas via Sling-funktionen *sling:resourceSuperType*

* Föredra Sightly/HTL framför JSP som mallspråk

   * Om du använder det här förhindrar du att koden separeras från markeringar, erbjuder inbyggt XSS-skydd och har en mer välbekant syntax

**Optimera för prestanda på enheten**

* Artikelspecifika skript och formatmallar ska inkluderas i artikelnyttolasten med hjälp av innehållsmallen dps-article contentSync
* Skript och formatmallar som delas av mer än en artikel bör inkluderas i delade resurser via innehållsmallen dps-HTMLResources contentsync
* Referera inte till externa skript som är renderingsblockerande

>[!NOTE]
>
>Du kan lära dig mer om återgivningsblockerande externa skript [här](https://developers.google.com/speed/docs/insights/BlockingJS).

**Föredra programspecifika JS- och CSS-bibliotek på klientsidan framför webbspecifika**

* För att undvika att dyka upp i bibliotek som jQuery Mobile för att hantera en enorm bredd av enheter och webbläsare
* När en mall körs i en apps webbvy har du kontroll över de plattformar och versioner som appen kommer att ha stöd för, och du vet att det finns stöd för JavaScript. Använd till exempel Ionic (bara CSS) framför jQuery Mobile och Onsen i stället för Bootstrap.

>[!NOTE]
>
>Klicka [här](https://jquerymobile.com/browser-support/1.4/) om du vill veta mer om jQuery Mobile.

**Föredra mikrobibliotek framför högar**

* Den tid det tar att lägga in materialet i enhetens glas saktas ned av alla bibliotek som artiklarna är beroende av. Den här nedgången förvärras när en ny webbvy används för att återge varje artikel, så varje bibliotek måste initieras igen från början
* Om artiklarna inte har skapats som SPA (appar med en sida) behöver du förmodligen inte inkludera ett bibliotek med en hel hög, som Angular
* Använd mindre bibliotek med ett enda syfte som hjälper dig att lägga till den interaktivitet som sidan kräver, till exempel [Fastclick](https://github.com/ftlabs/fastclick) eller [Velocity.js](https://velocityjs.org)

**Minimera artikelnyttolastens storlek**

* Använd minsta möjliga resurser som effektivt kan täcka den största visningsruta ni stöder, med en rimlig upplösning
* Använd ett verktyg som *ImageOptime* på dina bilder så att du kan ta bort överflödiga metadata

## Komma i förväg {#getting-ahead}

Mer information om de två andra rollerna och ansvarsområdena finns i resurserna nedan:

* [Administratör](/help/mobile/aem-mobile.md)
* [Författare](/help/mobile/aem-mobile-on-demand.md)
