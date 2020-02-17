---
title: Skapa mobilprogram
seo-title: Skapa mobilprogram
description: Med AEM Mobile Dashboard kan du skapa, bygga och driftsätta mobilprogram, skapa, ta bort och redigera programmetadata. Följ den här sidan om du vill veta mer.
seo-description: Med AEM Mobile Dashboard kan du skapa, bygga och driftsätta mobilprogram, skapa, ta bort och redigera programmetadata. Följ den här sidan om du vill veta mer.
uuid: 293b5d29-df7e-42dd-ae64-8c677317e7a5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: abfeea65-102d-4800-abeb-304d61afcc13
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Skapa mobilprogram{#authoring-mobile-applications}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

Med AEM Mobile Dashboard kan du skapa, bygga och driftsätta mobilprogram, skapa, ta bort och redigera programmetadata. När applikationen är live kan ni analysera applikationsanalyser, inklusive livscykelvärden och användningsstatistik, för att förbättra kundkonverteringen och varumärkeslojaliteten.

Information om hur du skapar ditt AEM-mobilprogram finns på sidan [Skapa mobilprogram](/help/mobile/building-app-mobile-phonegap.md) .

Mer information om hur du konfigurerar miljön och kommer igång finns i [Administrera AEM för att använda AEM PhoneGap Enterprise](/help/mobile/administer-phonegap.md).

## AEM Mobile Apps Catalog {#the-aem-mobile-apps-catalog}

I [AEM Mobile Apps-katalogen](http://localhost:4502/aem/apps.html/content/phonegap) visas alla mobilappar som hanteras i AEM.

Se den här katalogen som&quot;landningssida&quot; för AEM Mobile, där administratörer kan starta en ny AEM Mobile-applikation genom att antingen skapa baserad på en mall eller överföra en befintlig app som redan startats av en mobilutvecklare.

Följ de här stegen för att komma till startsidan för programkatalogen:

1. Bläddra till **Navigering** och välj sedan **Mobil**.

1. Välj **Appar** för att öppna programkatalogen.

![AEM Mobile Apps Catalog](assets/chlimage_1-135.png)

## AEM Mobile App Dashboard {#the-aem-mobile-app-dashboard}

Om du väljer en AEM-mobilapp i katalogen visas dess instrumentpanel. Här kan du hantera ditt program, visa statistik, bygga, distribuera och hantera ditt innehåll för mobilappar.

Du kan expandera till varje ruta i AEM Mobile Dashboard för att visa eller redigera information genom att klicka på ... i det nedre högra hörnet.

![AEM Mobile Applications Command Center](assets/chlimage_1-136.png)

### Hantera programpanel {#the-manage-app-tile}

I Manage App Tile visas programikonen, namn, beskrivning, plattformar som stöds, hur du ringer hem för att få information om uppdaterings-URL:en och versionen. Du kan fördjupa dig i den här rutan om du vill redigera och underhålla PhoneGap Application Configuration (config.xml) och förbereda ditt program för att skickas till olika programbutiker för distribution.

Klicka [här](/help/mobile/phonegap-app-details-tile.md) för mer information.

![chlimage_1-137](assets/chlimage_1-137.png)

### Panelen Hantera sidinnehåll {#the-manage-page-content-tile}

Innehåll kan skapas, uppdateras och tas bort i AEM Mobile på ungefär samma sätt som i AEM Sites. På panelen **Hantera sidinnehåll** visas antalet sidor med hanterat innehåll och senast ändrade sidor. Du kan fördjupa innehållet för att skapa, kopiera, flytta, ta bort och uppdatera sidor genom att klicka på varje post i rutan. När innehållet har uppdaterats kan du skicka en innehållsuppdatering till dina kunder via **Hantera innehållspaket.**

![Innehållsruta](assets/chlimage_1-138.png)

### Panelen Hantera innehållspaket {#the-manage-content-packages-tile}

När du har lagt till eller ändrat innehåll via panelen Hantera sidinnehåll kan du skicka ut dessa ändringar till dina kunder med en uppdatering av innehållsreleasen.

Med innehållspaketet kan AEM App Author hantera sidinnehåll i AEM och låta utvecklingsteamet göra ändringar i ditt PhoneGap Shell-program (t.ex. appramverk eller infrastruktur) och sedan skicka ut ändringarna till dina kunder snabbt och utan att behöva registrera en utvecklare för att skicka vidare till olika butiker för distribution.

Innehållspaket skapar en ZIP-fil, som betraktas som ett innehållspaket, för varje uppdatering. Dessa paket innehåller HTML-resurser och HTML-sidor som genereras när programmet återges och är tillräckligt intelligenta för att bara paketera de filer som har ändrats sedan den senaste uppdateringen.

Kolumnen **Typ** för hanteringspaketet visar antingen App för att ange innehåll för programgränssnitt, till exempel ramverk eller infrastruktur för appen som hanteras av en utvecklare eller Content som representerar sidinnehåll som hanteras av innehållsförfattaren.

Innehåll kan representeras som ett språk eller som en viss del av programmet där flera innehållsversionspaket används av programmet. Alternativet att paketera innehållet är utformat för att vara flexibelt och helt i linje med hur du vill hantera innehållet för programmet.

Kolumnen **Ändrad** anger när sidor senast ändrades.

Kolumnen **Mellanlagrad** visas när den senaste innehållsuppdateringen skapades. Om du vill skapa en ny innehållsuppdatering och mellanlagra ändringarna öppnar du alla poster i rutan och skapar en ny uppdatering.

Kolumnen **Publicerad** visar när den senaste innehållsuppdateringen publicerades och gjordes tillgänglig för dina kunder. Om du vill publicera innehåll måste du först mellanlagra innehållet och sedan publicera uppdateringen genom att gå in i den här rutan och publicera från konsolen för information om innehållsrelease.

![Content Release Tile](assets/chlimage_1-139.png) ![ContentSync-paket för appskalet](do-not-localize/chlimage_1-5.png)

Den här ikonen representerar ett innehållsversionspaket för programskalet

![](do-not-localize/chlimage_1-6.png)

De här ikonerna representerar ett paket för innehållsrelease för appinnehåll

### PhoneGap Build Tile {#the-phonegap-build-tile}

PhoneGap **Build Tile** ansluts till [https://build.phonegap.com](https://build.phonegap.com) för att skapa och vara värd för fjärrbuider. När bygget har byggts blir det tillgängligt antingen som nedladdning eller direkt till enheten via en QR-kod.

Du kan också hämta enhetskällan för att bygga lokalt via [PhoneGap CLI](https://docs.phonegap.com/en/3.5.0/guide_cli_index.md.html).

![PhoneGap Build Tile](assets/chlimage_1-140.png)

### Mätplattan {#the-metrics-tile}

>[!CAUTION]
>
>Rutan Metrics visas först när du har konfigurerat molntjänsten.
>
>Mer information finns i [Konfigurera Adobe Mobile Services Cloud-tjänsten](/help/mobile/configure-adobe-mobile-cloud-service.md) .

AEM Mobile integreras med Adobe Analytics via [Adobe Mobile Services SDK](https://www.adobe.com/ca/solutions/digital-marketing/mobile-services/app-sdk.html) (AMS).

Kontrollcentrets **måttpanel** visar en sammanfattning av analyser som hämtats från AMS för ditt program. Du kan gå in på kontrollpanelen för analyser genom att klicka på ... längst ned till höger.

![Mätplatta](assets/chlimage_1-141.png)

### Panelen Hantera entitetsinnehåll {#the-manage-entity-content-tile}

Med panelen Hantera enhetsinnehåll kan du lägga till och hantera programdefinitioner. Appdefinitioner är ett sätt att identifiera vilka utrymmen (och andra konfigurationer) som är lämpliga för appen. På så sätt kan ett nytt utrymme läggas till utan att appen behöver kompileras om. Programdefinitionen uppdateras och innehåller information om nya mellanslag.

Klicka [här](/help/mobile/phonegap-app-definitions.md) för att skapa och hantera programdefinitioner.

Du kan gå närmare in på kontrollpanelen för enhetsinnehåll genom att klicka på ... längst ned till höger.

![chlimage_1-142](assets/chlimage_1-142.png)

#### Additional Resources {#additional-resources}

Mer information om roller och ansvar för en administratör och utvecklare finns i resurserna nedan:

* [Utveckla för Adobe PhoneGap Enterprise med AEM](/help/mobile/developing-in-phonegap.md)
* [Administrera innehåll för Adobe PhoneGap Enterprise med AEM](/help/mobile/administer-phonegap.md)

