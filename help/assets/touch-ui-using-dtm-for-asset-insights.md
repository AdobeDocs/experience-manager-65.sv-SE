---
title: Aktivera tillgångsinsikter via DTM
description: Lär dig hur du använder Adobe Dynamic Tag Management (DTM) för att aktivera tillgångsinsikter.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Aktivera tillgångsinsikter via DTM {#enable-asset-insights-through-dtm}

Adobe Dynamic Tag Management är ett verktyg som aktiverar era digitala marknadsföringsverktyg. Den tillhandahålls kostnadsfritt till Adobe Analytics-kunder.

Även om du kan anpassa din spårningskod så att CMS-lösningar från tredje part kan använda resursinsikter, rekommenderar Adobe att du använder DTM för att infoga resursinsikter-taggar.

>[!NOTE]
>
>Insikter stöds endast och tillhandahålls för bilder.

Utför dessa steg för att aktivera tillgångsinsikter via DTM.

1. Tryck/klicka på AEM-logotypen och gå till **[!UICONTROL Verktyg]** > **[!UICONTROL Resurser]** > **[!UICONTROL Insights Configuration]**.
1. [Konfigurera AEM-instans med DTM Cloud-tjänsten](/help/sites-administering/dtm.md)

   API-token bör vara tillgänglig när du loggar in på [https://dtm.adobe.com](https://dtm.adobe.com/) och går till **[!UICONTROL Kontoinställningar]** från profilikonen. Detta steg är inte nödvändigt från tillgångsinsikter eftersom integrationen av AEM Sites med tillgångsinsikter fortfarande pågår.

1. Logga in på [https://dtm.adobe.com](https://dtm.adobe.com/)och välj ett företag.
1. Skapa/öppna en befintlig webbegenskap

   * Välj fliken **[!UICONTROL Webbegenskaper]** och tryck/klicka sedan på **[!UICONTROL Lägg till egenskap]**.

   * Uppdatera fälten efter behov och tryck/klicka på **[!UICONTROL Skapa egenskap]**. Se [dokumentationen](https://helpx.adobe.com/experience-manager/using/dtm.html).
   ![Skapa redigera webbegenskap](assets/Create-edit-web-property.png)

1. På fliken **[!UICONTROL Regler]** väljer du **[!UICONTROL Sidinläsningsregler]** i navigeringsrutan och trycker/klickar på **[!UICONTROL Skapa ny regel]**.

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. Expandera **[!UICONTROL JavaScript/tredjepartstaggar]**. Tryck/klicka sedan på **[!UICONTROL Lägg till nytt skript]** på fliken **[!UICONTROL Sekventiell HTML]** för att öppna skriptdialogrutan.

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. Tryck/klicka på AEM-logotypen och gå till **[!UICONTROL Verktyg > Resurser]**.
1. Tryck/klicka på **[!UICONTROL Insights Page Tracker]**, kopiera spårningskoden och klistra sedan in den i skriptdialogrutan som du öppnade i steg 6. Spara ändringarna.

   >[!NOTE]
   >
   > * `AppMeasurement.js` tas bort. Den förväntas bli tillgänglig via DTM:s Adobe Analytics-verktyg.
   > * Anropet till `assetAnalytics.dispatcher.init`() har tagits bort. Funktionen förväntas anropas när inläsningen av DTM:s Adobe Analytics-verktyg är klar.
   > * Beroende på var sidspåraren för tillgångsinsikter finns (till exempel AEM, CDN och så vidare) kan skriptkällans ursprung kräva ändringar.
   > * För AEM-värdbaserad sidspårare ska källan peka på en publiceringsinstans med värdnamnet för dispatcher-instansen.


1. Åtkomst `https://dtm.adobe.com`. Klicka på **[!UICONTROL Översikt]** i webbegenskapen och klicka på **[!UICONTROL Lägg till verktyg]** eller öppna ett befintligt Adobe Analytics-verktyg. När du skapar verktyget kan du ange **[!UICONTROL Konfigurationsmetod]** som **[!UICONTROL Automatisk]**.

   ![Lägg till Adobe Analytics-verktyget](assets/Add-Adobe-Analytics-Tool.png)

   Välj rapportsviter för mellanlagring/produktion efter behov.

1. Utöka **[!UICONTROL bibliotekshanteringen]** och se till att **[!UICONTROL Läs in bibliotek vid]** är inställt på **[!UICONTROL Sidbörjan]**.

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. Expandera **[!UICONTROL Anpassa sidkod]** och klicka eller tryck på **[!UICONTROL Öppna redigerare]**.

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
             "",  /** listVar to put comma-separated-list of Asset IDs for Asset Impression Events in tracking-call, e.g. 'listVar1' */
             "",  /** eVar to put Asset ID for Asset Click Events in, e.g. 'eVar3' */
             "",  /** event to include in tracking-calls for Asset Impression Events, e.g. 'event8' */
             "",  /** event to include in tracking-calls for Asset Click Events, e.g. 'event7' */
             sObj  /** [OPTIONAL] if the webpage already has an AppMeasurement object, please include the object here. If unspecified, Pagetracker Core shall create its own AppMeasurement object */
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

   * Sidinläsningsregeln i DTM inkluderar bara koden pagetracker.js. Alla `assetAnalytics` fält betraktas som åsidosättningar för standardvärden. De är inte obligatoriska som standard.
   * Koden anropar `assetAnalytics.dispatcher.init`() efter att ha kontrollerat att `_satellite.getToolsByType('sc')[0].getS`() har initierats och `assetAnalytics,dispatcher.init` är tillgänglig. Du kan därför hoppa över att lägga till den i steg 11.
   * Som framgår av kommentarerna i Insights Page Tracker-koden (**[!UICONTROL Verktyg > Resurser > Insights Page Tracker]**) är de tre första argumenten (RSID, Tracking Server och Visitor Namespace) irrelevanta när sidspåraren inte skapar ett `AppMeasurement` objekt. Tomma strängar skickas i stället för att markera detta.\
      De återstående argumenten motsvarar konfigurationen på sidan Insights Configuration (**[!UICONTROL Verktyg > Assets > Insights Configuration]**).
   * AppMeasurement-objektet hämtas genom att en fråga skickas `satelliteLib` till alla tillgängliga SiteCatalyst-motorer. Om flera taggar har konfigurerats ändrar du indexvärdet för arrayväljaren på rätt sätt. Posterna i arrayen ordnas enligt de SiteCatalyst-verktyg som finns i DTM-gränssnittet.

1. Spara och stäng fönstret Kodredigeraren och spara sedan ändringarna i verktygskonfigurationen.
1. Godkänn båda väntande godkännanden på fliken **[!UICONTROL Godkännanden]** . DTM-taggen kan infogas på webbsidan. Mer information om hur du infogar DTM-taggar på webbsidor finns i [Integrera DTM i anpassade sidmallar](https://blogs.adobe.com/experiencedelivers/experience-management/integrating-dtm-custom-aem6-page-template/).
