---
title: Skapa ett AEM Mobile-program med guiden Skapa
description: AEM Mobile-programmen bygger på en plan som definierar en sidstruktur och egenskaper. Följ den här sidan om du vill veta mer om hur du skapar ett program baserat på en appmall.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: be093025-b19f-4499-a7b5-aae5ab74f966
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---

# Skapa ett AEM Mobile-program med guiden Skapa{#creating-a-new-aem-mobile-app-using-create-wizard}

{{ue-over-mobile}}

AEM Mobile-programmen bygger på en plan som definierar en sidstruktur och egenskaper. Du kan konfigurera följande programegenskaper:

* **Titel:** Programnamnet.
* **Målsökväg:** Platsen i databasen där programmet lagras. Låt standardinställningen vara om du vill skapa en sökväg baserat på programnamnet.

* **Namn:** Standardvärdet är värdet på egenskapen Title där blankstegstecken tas bort. Namnet används i AEM för att referera till programmet, till exempel för databasnoden som representerar programmet.
* **Beskrivning:** En beskrivning av programmet.
* **Server-URL:** Den URL som tillhandahåller OTA-innehåll (Over-the-Air) uppdateras i programmet. Standardvärdet är publiceringsserverns URL-adress för instansen som används för att skapa ett program (hämtas från externaliseringstjänsten). Observera att detta måste vara en publiceringsserverinstans i stället för en författare, vilket kräver autentisering.

Du kan också tillhandahålla en bildfil som du kan använda som programminiatyrbild, välja vilken PhoneGap Build-konfiguration som ska användas och välja vilken mobilappsanalyskonfiguration som ska användas. Den här bilden används bara som miniatyrbild för att representera ditt mobilprogram i mobilappskonsolen i Experience Manager.

Det finns ytterligare flikar (och valfria) för att bygga molntjänster och integrera SDK-pluginmodulen för Adobe Mobile Services i appen.

* Bygg: Klicka på Hantera konfigurationer och konfigurera build.phonegap.com här. I listrutan kan du sedan välja den nya molntjänsten PhoneGap build.
* Analys: Klicka på Hantera konfigurationer och konfigurera molntjänsten [Adobe Mobile Services SDK](https://experienceleague.adobe.com/docs/mobile-services/using/home.html?lang=sv-SE). I listrutan kan du sedan välja den nya mobiltjänsten som ska integreras i din mobilapp.

## Använda appmallar {#using-app-templates}

Appmallar är ett enkelt sätt att använda befintliga designer som skapats av utvecklare och som används för att skapa nya appar i AEM.

Vad är en appmall? Se det som en samling sidmallar och komponenter som utgör en grund eller grund för ett program.
När du skapar ett program baserat på en mall för ett annat program får du ett program som har en startpunkt som representerar det program som det skapades från.

Du måste ha en befintlig mobilappsmall (eller en app som har en appmall) för att kunna använda den här funktionen.

Det senaste exempelpaketet AEM program innehåller en uppdaterad version av Geometrixx-appen med en appmall. Du kan också installera [StarterKit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) som även innehåller en mall.

Steg för att skapa ett program baserat på en appmall:

1. Gå till AEM Mobile programkatalog: &lt;*server-url*>aem/apps.html/content/mobileapps
1. Välj **Skapa** och välj sedan **App** enligt nedan

![chlimage_1-158](assets/chlimage_1-158.png)

Välj en appmall som har gjorts tillgänglig för dig av en AEM. Se [Struktur för en AEM Mobile-app](/help/mobile/phonegap-structure-an-app.md) för utvecklarhjälp.

![chlimage_1-159](assets/chlimage_1-159.png)

Fyll i information om det nya programmet efter behov, inklusive möjlighet att ändra dess miniatyrbild. Dessa värden kan redigeras senare från panelen **Hantera program**.

![chlimage_1-160](assets/chlimage_1-160.png)

## Nästa steg {#the-next-steps}

Läs mer om andra författarroller i följande resurser:

* [Hantera programpanel](/help/mobile/phonegap-app-details-tile.md)
* [Redigera appmetadata](/help/mobile/phonegap-editmetadata.md)
* [Programdefinitioner](/help/mobile/phonegap-app-definitions.md)
* [Importera en befintlig hybridapp](/help/mobile/phonegap-adding-content-to-imported-app.md)
* [Innehållstjänster](/help/mobile/develop-content-as-a-service.md)

## Ytterligare resurser {#additional-resources}

Mer information om roller och ansvar för en administratör och utvecklare finns i resurserna nedan:

* [Utveckla för Adobe PhoneGap Enterprise med AEM](/help/mobile/developing-in-phonegap.md)
* [Administrera innehåll för Adobe PhoneGap Enterprise med AEM](/help/mobile/administer-phonegap.md)
