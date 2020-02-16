---
title: Skapa en ny AEM Mobile-app med guiden Skapa
seo-title: Skapa en ny AEM Mobile-app med guiden Skapa
description: AEM Mobile-appar bygger på en plan som definierar en sidstruktur och egenskaper. Följ den här sidan om du vill veta mer om hur du skapar ett nytt program baserat på en appmall.
seo-description: AEM Mobile-appar bygger på en plan som definierar en sidstruktur och egenskaper. Följ den här sidan om du vill veta mer om hur du skapar ett nytt program baserat på en appmall.
uuid: c2bd63a5-3dff-4a72-b1fb-0c776e0afa33
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 27605eb7-59b2-42d4-8cc5-02cfa52b4491
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Skapa en ny AEM Mobile-app med guiden Skapa{#creating-a-new-aem-mobile-app-using-create-wizard}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

AEM Mobile-appar bygger på en plan som definierar en sidstruktur och egenskaper. Du kan konfigurera följande programegenskaper:

* **** Titel: Programtitel.
* **** Målsökväg: Platsen i databasen där programmet lagras. Låt standardinställningen vara om du vill skapa en sökväg baserat på programnamnet.

* **** Namn: Standardvärdet är värdet för egenskapen Title med blankstegstecken borttagna. Namnet används i AEM för att referera till programmet, till exempel för databasnoden som representerar programmet.
* **** Beskrivning: En beskrivning av programmet.
* **** Server-URL: Den URL som innehåller OTA-innehåll (Over-the-Air) uppdateras i programmet. Standardvärdet är publiceringsserverns URL-adress för instansen som används för att skapa ett program (hämtas från externaliseringstjänsten). Observera att detta måste vara en publiceringsserverinstans i stället för en författare, vilket kräver autentisering.

Du kan också tillhandahålla en bildfil som du kan använda som programminiatyr, välja den PhoneGap Build-konfiguration som du vill använda och välja den mobilappsanalyskonfiguration som ska användas. Den här bilden används bara som miniatyrbild för att representera ditt mobilprogram i konsolen för mobilappar i Experience Manager.

Det finns ytterligare flikar (och valfria) för att bygga molntjänster och integrera Adobe Mobile Services SDK-pluginen i appen.

* Bygg: Klicka på Hantera konfigurationer och konfigurera bygg.phonegap.com här. I listrutan kan du sedan välja den nya molntjänsten PhoneGap build.
* Analyser: Klicka på Hantera konfigurationer och konfigurera molntjänsten [Adobe Mobile Services SDK](https://marketing.adobe.com/developer/en_US/get-started/mobile/c-measuring-mobile-applications) . I listrutan kan du sedan välja den nya mobiltjänsten som ska integreras i din mobilapp.

## Använda appmallar {#using-app-templates}

Appmallar är ett enkelt sätt att utnyttja befintliga designer som skapats av utvecklare och som används för att skapa nya appar i AEM.

Vad är en appmall? Se det som en samling sidmallar och komponenter som utgör en grund eller grund för ett program.
När du skapar ett nytt program baserat på en mall för ett annat program får du ett program som har en startpunkt som representerar det program som det skapades från.

Du måste ha en befintlig mobilappsmall (eller en app som har en appmall) för att kunna använda den här funktionen.

Det senaste exempelpaketet för AEM-appar innehåller en uppdaterad version av Geometrixx-appen med en appmall. Du kan också installera [StarterKit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) som också innehåller en mall.

Steg för att skapa ett nytt program baserat på en appmall:

1. Gå till AEM Mobile-appkatalogen: &lt;*server-url*>aem/apps.html/content/mobileapps
1. Välj **Skapa** och välj sedan **App** enligt nedan

![chlimage_1-158](assets/chlimage_1-158.png)

Välj en appmall som är tillgänglig för dig av en AEM-utvecklare. Se Struktur [för en AEM-mobilapp](/help/mobile/phonegap-structure-an-app.md) för utvecklarhjälp.

![chlimage_1-159](assets/chlimage_1-159.png)

Fyll i information om det nya programmet efter behov, inklusive möjlighet att ändra dess miniatyrbild. Dessa värden kan redigeras senare på panelen **Hantera program** .

![chlimage_1-160](assets/chlimage_1-160.png)

## Nästa steg {#the-next-steps}

Läs mer om andra författarroller i följande resurser:

* [Hantera programpanel](/help/mobile/phonegap-app-details-tile.md)
* [Redigera appmetadata](/help/mobile/phonegap-editmetadata.md)
* [Programdefinitioner](/help/mobile/phonegap-app-definitions.md)
* [Importera en befintlig hybridapp](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Innehållstjänster](/help/mobile/develop-content-as-a-service.md)

## Additional Resources {#additional-resources}

Mer information om roller och ansvar för en administratör och utvecklare finns i resurserna nedan:

* [Utveckla för Adobe PhoneGap Enterprise med AEM](/help/mobile/developing-in-phonegap.md)
* [Administrera innehåll för Adobe PhoneGap Enterprise med AEM](/help/mobile/administer-phonegap.md)
