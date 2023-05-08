---
title: Skapa mobilprogram
seo-title: Authoring Mobile Applications
description: Med AEM Mobile Dashboard kan du skapa, bygga och driftsätta mobilprogram, skapa, ta bort och redigera programmetadata. Följ den här sidan om du vill veta mer.
seo-description: he AEM Mobile Dashboard allows you to create, build and deploy your mobile application, create, delete and edit application metadata. Follow this page to learn more.
uuid: 293b5d29-df7e-42dd-ae64-8c677317e7a5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: abfeea65-102d-4800-abeb-304d61afcc13
exl-id: 073daff7-0c1d-4715-bfd4-3e2336e4cb88
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 0%

---

# Skapa mobilprogram{#authoring-mobile-applications}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

Med AEM Mobile Dashboard kan du skapa, bygga och driftsätta mobilprogram, skapa, ta bort och redigera programmetadata. När applikationen är live kan ni analysera applikationsanalyser, inklusive livscykelvärden och användningsstatistik, för att förbättra kundkonverteringen och varumärkeslojaliteten.

Information om hur du skapar ditt AEM Mobile-program finns i [Bygger mobilprogram](/help/mobile/building-app-mobile-phonegap.md) sida.

Information om hur du konfigurerar miljön och kommer igång finns i [Administrera AEM för att använda AEM PhoneGap Enterprise](/help/mobile/administer-phonegap.md).

## The AEM Mobile Apps Catalog {#the-aem-mobile-apps-catalog}

The [AEM Mobile Apps Catalog](http://localhost:4502/aem/apps.html/content/phonegap) visar alla mobilappar som hanteras i AEM.

Se den här katalogen som&quot;landningssida&quot; för AEM Mobile, där administratörer kan starta ett nytt AEM Mobile-program genom att antingen skapa baserat på en mall eller överföra en befintlig app som redan startats av en mobilutvecklare.

Följ de här stegen för att komma till startsidan för programkatalogen:

1. Bläddra till **Navigering** och sedan välja **Mobil**.

1. Välj **Appar** för att öppna programkatalogen.

![AEM Mobile Apps Catalog](assets/chlimage_1-135.png)

## AEM Mobile App Dashboard {#the-aem-mobile-app-dashboard}

Om du väljer ett AEM Mobile-program i katalogen visas dess kontrollpanel. Här kan du hantera ditt program, visa statistik, bygga, distribuera och hantera ditt mobilappsinnehåll.

Du kan expandera till varje platta i AEM Mobile Dashboard om du vill visa eller redigera information genom att klicka på.. i det nedre högra hörnet.

![AEM Mobile Applications Command Center](assets/chlimage_1-136.png)

### Hantera programpanel {#the-manage-app-tile}

I Manage App Tile visas programikonen, namn, beskrivning, plattformar som stöds, hur du ringer hem för att få information om uppdaterings-URL:en och versionen. Du kan fördjupa dig i den här rutan om du vill redigera och underhålla PhoneGap Application Configuration (config.xml) och förbereda ditt program för att skickas till de olika programbutikerna för distribution.

Klicka [här](/help/mobile/phonegap-app-details-tile.md) för mer information.

![chlimage_1-137](assets/chlimage_1-137.png)

### Panelen Hantera sidinnehåll {#the-manage-page-content-tile}

Innehåll kan skapas, uppdateras och tas bort i AEM Mobile på ungefär samma sätt som i AEM Sites. The **Hantera sidinnehållspanel** visar antalet sidor med hanterat innehåll och senast ändrade sidor. Du kan fördjupa innehållet för att skapa, kopiera, flytta, ta bort och uppdatera sidor genom att klicka på varje post i rutan. När innehållet har uppdaterats kan ni göra en innehållsuppdatering för era kunder via **Hantera innehållspaket sida vid sida.**

![Innehållsruta](assets/chlimage_1-138.png)

### Panelen Hantera innehållspaket {#the-manage-content-packages-tile}

När du har lagt till eller ändrat innehåll via panelen Hantera sidinnehåll kan du skicka ut dessa ändringar till dina kunder med en uppdatering av innehållsreleasen.

Med innehållspaketet kan AEM App Author hantera sidinnehåll i AEM och låta utvecklingsteamet göra ändringar i ditt PhoneGap Shell-program (d.v.s. appramverk eller infrastruktur) och sedan skicka ut ändringarna till dina kunder snabbt och utan att behöva registrera en utvecklare som kan skicka in ändringarna till olika butiker för distribution.

Innehållspaket skapar en ZIP-fil, som betraktas som ett innehållspaket, för varje uppdatering. Dessa paket innehåller HTML-resurser och HTML-sidor som genereras när programmet återges och är tillräckligt intelligenta för att bara paketera de filer som har ändrats sedan den senaste uppdateringen.

Panelerna Hantera innehållspaket **Typ** kolumnen visar antingen App (App) för att beteckna Application Shell-innehåll, till exempel ramverk eller infrastruktur för appen som hanteras av en utvecklare eller Content (Content) som representerar sidinnehåll som hanteras av innehållsförfattaren.

Innehåll kan representeras som ett språk eller som en viss del av programmet där flera innehållsversionspaket används av programmet. Valet av hur ni paketerar ert innehåll är flexibelt och helt i linje med hur ni vill hantera innehåll för er applikation.

The **Ändrad** -kolumnen anger när sidor senast ändrades.

The **Mellanlagrad** visas när den senaste innehållsuppdateringen skapades. Om du vill skapa en innehållsuppdatering och mellanlagra dina ändringar öppnar du en valfri post i rutan och skapar en uppdatering.

The **Publicerad** visas när den senaste innehållsuppdateringen publicerades och gjordes tillgänglig för dina kunder. Om du vill publicera innehåll måste du först mellanlagra innehållet och sedan publicera uppdateringen genom att gå in i den här rutan och publicera från konsolen för information om innehållsrelease.

![Sida för innehållsrelease](assets/chlimage_1-139.png) ![ContentSync-paket för appskalet](do-not-localize/chlimage_1-5.png)

Den här ikonen representerar ett innehålls-releasepaket för programskalet

![](do-not-localize/chlimage_1-6.png)

De här ikonerna representerar ett innehålls-releasepaket för appinnehåll

### The PhoneGap Build Tile {#the-phonegap-build-tile}

The **PhoneGap Build** ansluter med [https://build.phonegap.com](https://build.phonegap.com) för att bygga och vara värd för fjärrbyggen. När bygget har byggts blir det tillgängligt antingen som nedladdning eller direkt till enheten via en QR-kod.

Du kan även hämta enhetskällan för att bygga lokalt via [PhoneGap CLI](https://docs.phonegap.com/en/3.5.0/guide_cli_index.md.html).

![PhoneGap Build](assets/chlimage_1-140.png)

### Mätplattan {#the-metrics-tile}

>[!CAUTION]
>
>Rutan Metrics visas först när du har konfigurerat molntjänsten.
>
>Se [Konfigurera Cloud Servicen för Adobe Mobile Services](/help/mobile/configure-adobe-mobile-cloud-service.md) för mer information.

AEM Mobile kan integreras med Adobe Analytics via [Adobe Mobile Services SDK](https://experienceleague.adobe.com/docs/mobile.html?lang=en) (AMS).

Kontrollcentret **Mätplatta** visar sammanfattningsanalyser som hämtats från AMS för ditt program. Du kan gå in på kontrollpanelen för analyser genom att klicka på ... längst ned till höger.

![Mätplatta](assets/chlimage_1-141.png)

### Panelen Hantera entitetsinnehåll {#the-manage-entity-content-tile}

Med panelen Hantera enhetsinnehåll kan du lägga till och hantera programdefinitioner. Appdefinitioner är ett sätt att identifiera vilka utrymmen (och andra konfigurationer) som är lämpliga för appen. På så sätt kan ett nytt utrymme läggas till utan att appen behöver kompileras om. Programdefinitionen uppdateras och innehåller information om nya mellanslag.

Klicka [här](/help/mobile/phonegap-app-definitions.md) för att skapa och hantera appdefinitioner.

Du kan gå närmare in på kontrollpanelen för enhetsinnehåll genom att klicka på ... längst ned till höger.

![chlimage_1-142](assets/chlimage_1-142.png)

#### Ytterligare resurser {#additional-resources}

Mer information om roller och ansvar för en administratör och utvecklare finns i resurserna nedan:

* [Utveckla för Adobe PhoneGap Enterprise med AEM](/help/mobile/developing-in-phonegap.md)
* [Administrera innehåll för Adobe PhoneGap Enterprise med AEM](/help/mobile/administer-phonegap.md)
