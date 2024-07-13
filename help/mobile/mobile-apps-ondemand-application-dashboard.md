---
title: AEM Mobile Application Dashboard
description: Du kan hantera program- och mobilappsinnehåll från AEM Mobile Application Dashboard eller Control Center. Följ den här sidan om du vill veta mer.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: daafc8b8-3c01-4c97-a14b-f1b706600249
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 2%

---

# AEM Mobile Application Dashboard {#aem-mobile-application-dashboard}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

Du kan hantera program- och mobilappsinnehåll från AEM Mobile Application Dashboard eller Control Center.

Du kan detaljgranska varje ruta i kontrollcentret för att visa eller redigera detaljer genom att klicka på.. i det nedre högra hörnet.

![chlimage_1-54](assets/chlimage_1-54.png)

>[!NOTE]
>
>Du kan ändra ordningen på rutorna genom att klicka på rutans gripikon (de 9 övre vänstra punkterna). Orderändringen är användarspecifik - skiljer sig åt för enskilda användare.

Att hantera appinnehåll kräver en gemensam insats från utvecklare, innehållsförfattare och administratörer. Författare hanterar sidor, som i sin tur är baserade på mallar och komponenter som genererats av apputvecklare.

Slutligen publicerar administratörer det uppdaterade programinnehållet strategiskt.

## Hantera programpanel {#the-manage-app-tile}

**Hantera app**-panelen visar tillgänglig programinformation:

* Titel
* Beskrivning
* Ikon
* Senast ändrad
* Senast ändrad av

![chlimage_1-55](assets/chlimage_1-55.png)

## Hantera anslutningspanel {#the-manage-connection-tile}

Under **Hantera anslutning** visas anslutningsinformationen för AEM Mobile On-demand Services:

* Namn på molnkonfiguration
* Projektnamn och ID
* Anslutningsstatus

>[!NOTE]
>
>Klicka på kugghjulet i det övre högra hörnet för att konfigurera en molnkonfiguration för mobil på begäran.
>
>Mer information finns i [Konfigurera Mobile On-Demand Services](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md).

![chlimage_1-56](assets/chlimage_1-56.png)

## Hantera entiteter {#managing-entities}

Dessa tre paneler ger en översikt över läget för en apps innehåll:

* **banners**
* **artiklar**
* **samlingar**

Du kan expandera varje ruta för att få en mer detaljerad listvy genom att klicka på ellipsen (..) i det nedre högra hörnet. De här listvyerna är ett alternativt sätt att komma åt vanliga åtgärder för Mobile On Demand som att ta bort, överföra och redigera egenskaper.

### Panelen Hantera banderoller {#the-manage-banners-tile}

Med rutan **Hantera banderoller** kan du hantera innehållet för en banderoll. Följande information visas för en banderoll:

* image
* **TITLE**: bannerns namn
* **ÄNDRAT**: senast ändrat i AEM
* **ÖVERFÖRT**: senast överfört från AEM
* **PUBLICERAD**: AEM för senaste publicerade begäran
* **SOURCE**: källa (AEM lokal eller fjärransluten från Mobile On Demand)

I följande bild visas panelen **Hantera banners** på AEM Mobile Application Dashboard:

![chlimage_1-57](assets/chlimage_1-57.png)

>[!NOTE]
>
>Se **[Hantera banners](/help/mobile/mobile-on-demand-managing-banners.md)** för att skapa, ta bort eller uppdatera banners.

### Panelen Hantera artiklar {#the-manage-articles-tile}

Med rutan **Hantera artiklar** kan du hantera innehållet för en artikel. Följande information visas för en artikel:

* image
* **TITLE**: artikelns namn
* **ÄNDRAT**: senast ändrat i AEM
* **ÖVERFÖRT**: senast överfört från AEM
* **PUBLICERAD**: AEM för senaste publicerade begäran
* **SOURCE**: källa (AEM lokal eller fjärransluten från Mobile On-Demand)

Följande bild visar panelen **Hantera artiklar** på AEM Mobile Application Dashboard:

![chlimage_1-58](assets/chlimage_1-58.png)

>[!NOTE]
>
>Se [**Hantera artiklar**](/help/mobile/mobile-on-demand-managing-articles.md) för att skapa, ta bort eller uppdatera artiklar.

### Panelen Hantera samlingar {#the-manage-collections-tile}

Med rutan **Hantera samlingar** kan du hantera innehåll för en samling. Följande information visas för en samling:

* image
* **TITLE**: samlingens namn
* **ÄNDRAT**: senast ändrat i AEM
* **ÖVERFÖRT**: senast överfört från AEM
* **PUBLICERAD**: AEM för senaste publicerade begäran
* **SOURCE**: källa (AEM lokal eller fjärransluten från Mobile On-Demand)

I följande bild visas panelen **Hantera samlingar** på AEM Mobile Application Dashboard:

![chlimage_1-59](assets/chlimage_1-59.png)

>[!NOTE]
>
>Se **[Hantera samlingar](/help/mobile/mobile-on-demand-managing-collections.md)** för att skapa, ta bort eller uppdatera samlingar.

### Nästa steg {#the-next-steps}

När du känner till kontrollpanelen för program kan du läsa följande resurser för att skapa en mobilapp:

* [Skapa och konfigurera program](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [Associera en app på begäran med en molnkonfiguration](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [Innehållshanteringsåtgärder](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)

### Ytterligare resurser {#additional-resources}

Mer information om roller och ansvar för en administratör och utvecklare finns i resurserna nedan:

* [Utveckla AEM för AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Administrera innehåll för användning av AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)
