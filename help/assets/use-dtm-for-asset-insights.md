---
title: Aktivera resursinsikter via DTM
description: Lär dig hur du använder Adobe Dynamic Tag Management (DTM) för att aktivera Assets Insights.
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 80e8f84e-3235-4212-9dcd-6acdb9067893
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 1%

---

# Aktivera resursinsikter via DTM {#enable-asset-insights-through-dtm}

Adobe Dynamic Tag Management är ett verktyg som aktiverar era verktyg för digital marknadsföring. Det tillhandahålls kostnadsfritt till Adobe Analytics-kunder. Du kan antingen anpassa din spårningskod för att aktivera CMS-lösningar från tredje part för att använda Assets Insights eller använda DTM för att infoga Assets Insights-taggar. Insikter stöds endast och tillhandahålls för bilder.

>[!CAUTION]
>
>Adobe DTM är ersatt med [!DNL Adobe Experience Platform] och kommer snart [livstid](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f). Adobe rekommenderar att du [use [!DNL Adobe Experience Platform] för resursinsikter](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html).

Utför dessa steg för att aktivera Assets Insights via DTM.

1. Klicka på Experience Manager-logotypen och gå till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Insights Configuration]**.
1. [Konfigurera driftsättning av Experience Manager med DTM-Cloud Service](/help/sites-administering/dtm.md)

   API-token bör vara tillgänglig när du loggar in på [https://dtm.adobe.com](https://dtm.adobe.com/) och besök **[!UICONTROL Account Settings]** i användarprofilen. Detta steg är inte nödvändigt från Assets Insights-synpunkt eftersom integrationen av Experience Manager Sites med Assets Insights fortfarande pågår.

1. Logga in på [https://dtm.adobe.com](https://dtm.adobe.com/)och välja ett företag.
1. Skapa eller öppna en befintlig webbegenskap

   * Välj **[!UICONTROL Web Properties]** och sedan klicka på **[!UICONTROL Add Property]**.

   * Uppdatera fälten efter behov och klicka **[!UICONTROL Create Property]**. Se [dokumentation](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html).

   ![Skapa redigera webbegenskap](assets/Create-edit-web-property.png)

1. I **[!UICONTROL Rules]** flik, välja **[!UICONTROL Page Load Rules]** i navigeringsrutan och klicka på **[!UICONTROL Create New Rule]**.

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. Expandera **[!UICONTROL JavaScript /Third Party Tags]**. Klicka sedan på **[!UICONTROL Add New Script]** i **[!UICONTROL Sequential HTML]** för att öppna skriptdialogrutan.

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. Klicka på Experience Manager-logotypen och gå till **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.
1. Klicka **[!UICONTROL Insights Page Tracker]** kopierar du spårningskoden och klistrar sedan in den i skriptdialogrutan som du öppnade i steg 6. Spara ändringarna.

   >[!NOTE]
   >
   >* `AppMeasurement.js` tas bort. Den förväntas bli tillgänglig via DTM:s Adobe Analytics-verktyg.
   >* Samtalet till `assetAnalytics.dispatcher.init()` tas bort. Funktionen förväntas anropas när inläsningen av DTM:s Adobe Analytics-verktyg är klar.
   >* Beroende på var Assets Insights Page Tracker finns (till exempel Experience Manager, CDN och så vidare) kan skriptkällans ursprung kräva ändringar.
   >* För sidspåraren som är värd för Experience Manager ska källan peka på en publiceringsinstans med hjälp av värdnamnet för dispatcher-instansen.

1. Åtkomst `https://dtm.adobe.com`. Klicka **[!UICONTROL Overview]** i webbegenskapen och klicka **[!UICONTROL Add Tool]** eller öppna ett befintligt Adobe Analytics-verktyg. När du skapar verktyget kan du ange **[!UICONTROL Configuration Method]** till **[!UICONTROL Automatic]**.

   ![Verktyget Lägg till Adobe Analytics](assets/Add-Adobe-Analytics-Tool.png)

   Välj rapportsviter för mellanlagring/produktion efter behov.

1. Expandera **[!UICONTROL Library Management]** och se till att **[!UICONTROL Load Library at]** är inställd på **[!UICONTROL Page Top]**.

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. Expandera **[!UICONTROL Customize Page Code]** och klicka **[!UICONTROL Open Editor]**.

   ![chlimage_1-62](assets/chlimage_1-198.png)

1. Klistra in följande kod i fönstret:

   ```Java
   var sObj;
   
   if (arguments.length > 0) {
     sObj = arguments[0];
   } else {
     sObj = _satellite.getToolsByType('sc')[0].getS();
   }
   _satellite.notify('in assetAnalytics customInit');
   (function initializeAssetAnalytics() {
     if ((!!window.assetAnalytics) && (!!assetAnalytics.dispatcher)) {
       _satellite.notify('assetAnalytics ready');
       /** NOTE:
           Copy over the call to 'assetAnalytics.dispatcher.init()' from Assets Pagetracker
           Be mindful about changing the AppMeasurement object as retrieved above.
       */
       assetAnalytics.dispatcher.init(
             "",  /** RSID to send tracking-call to */
             "",  /** Tracking Server to send tracking-call to */
             "",  /** Visitor Namespace to send tracking-call to */
             "",  /** listVar to put comma-separated-list of Asset IDs for Asset Impression Events in tracking-call, for example, 'listVar1' */
             "",  /** eVar to put Asset ID for Asset Click Events in, for example, 'eVar3' */
             "",  /** event to include in tracking-calls for Asset Impression Events, for example, 'event8' */
             "",  /** event to include in tracking-calls for Asset Click Events, for example, 'event7' */
             sObj  /** [OPTIONAL] if the webpage already has an AppMeasurement object, include the object here. If unspecified, Pagetracker Core shall create its own AppMeasurement object */
             );
       sObj.usePlugins = true;
       sObj.doPlugins = assetAnalytics.core.updateContextData;
       assetAnalytics.core.optimizedAssetInsights();
     }
     else {
       _satellite.notify('assetAnalytics not available. Consider updating the Custom Page Code', 4);
     }
   })();
   ```

   * Sidinläsningsregeln i DTM innehåller endast `pagetracker.js` kod. Alla `assetAnalytics` -fält betraktas som åsidosättningar för standardvärden. De är inte obligatoriska som standard.
   * Kodanrop `assetAnalytics.dispatcher.init()` efter att ha kontrollerat att `_satellite.getToolsByType('sc')[0].getS()` initieras och `assetAnalytics,dispatcher.init` är tillgängligt. Du kan därför hoppa över att lägga till den i steg 11.
   * Enligt kommentarerna i Insights Page Tracker-koden (**[!UICONTROL Tools > Assets > Insights Page Tracker]**), när sidspåraren inte skapar en `AppMeasurement` är de tre första argumenten (RSID, Tracking Server och Visitor Namespace) irrelevanta. Tomma strängar skickas i stället för att markera detta.\
     De återstående argumenten motsvarar konfigurationen på sidan Insights Configuration (**[!UICONTROL Tools > Assets > Insights Configuration]**).
   * AppMeasurementet hämtas genom att en fråga skickas `satelliteLib` för alla tillgängliga SiteCatalyster. Om flera taggar har konfigurerats ändrar du indexvärdet för arrayväljaren på rätt sätt. Posterna i arrayen ordnas enligt de verktyg för SiteCatalyst som finns i DTM-gränssnittet.

1. Spara och stäng fönstret Kodredigeraren och spara sedan ändringarna i verktygskonfigurationen.
1. I **[!UICONTROL Approvals]** godkänner du båda väntande godkännanden. DTM-taggen är klar att infogas på webbsidan.
