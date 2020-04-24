---
title: Aktivera tillgångsinsikter via DTM
description: Learn how to use Adobe Dynamic Tag Management (DTM) to enable Asset Insights.
contentOwner: AG
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# Enable Asset Insights through DTM {#enable-asset-insights-through-dtm}

Adobe Dynamic Tag Management is a tool that activates your digital marketing tools. It is provided for free to Adobe Analytics customers.

Although you can customize your tracking code to enable third-party CMS solutions to use Asset Insights, Adobe recommends that you use DTM to insert Asset Insights tags.

>[!NOTE]
>
>Insights are only supported and provided for images.

Perform these steps to enable Asset Insights through DTM.

1. Tap/click the AEM logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Insights Configuration]**.
1. [Configure AEM instance with DTM Cloud Service](/help/sites-administering/dtm.md)

   API-token bör vara tillgänglig när du loggar in på [https://dtm.adobe.com](https://dtm.adobe.com/) och går till **[!UICONTROL Kontoinställningar]** från profilikonen. This step is not required from the Asset Insights standpoint, because the integration of AEM Sites with Asset Insights is still in the works.

1. Log on to [https://dtm.adobe.com](https://dtm.adobe.com/), and select a Company, as appropriate.
1. Create/Open an the existing Web Property

   * Välj fliken **[!UICONTROL Webbegenskaper]** och tryck/klicka sedan på **[!UICONTROL Lägg till egenskap]**.

   * Uppdatera fälten efter behov och tryck/klicka på **[!UICONTROL Skapa egenskap]**. Se [dokumentationen](https://helpx.adobe.com/experience-manager/using/dtm.html).
   ![Skapa redigera webbegenskap](assets/Create-edit-web-property.png)

1. På fliken **[!UICONTROL Regler]** väljer du **[!UICONTROL Sidinläsningsregler]** i navigeringsrutan och trycker/klickar på **[!UICONTROL Skapa ny regel]**.

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. Expandera **[!UICONTROL JavaScript/tredjepartstaggar]**. Tryck/klicka sedan på **[!UICONTROL Lägg till nytt skript]** på fliken **[!UICONTROL Sekventiell HTML]** för att öppna skriptdialogrutan.

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. Tap/click the AEM logo, and go to **[!UICONTROL Tools > Assets]**.
1. Tryck/klicka på **[!UICONTROL Insights Page Tracker]**, kopiera spårningskoden och klistra sedan in den i skriptdialogrutan som du öppnade i steg 6. Spara ändringarna.

   >[!NOTE]
   >
   > * `AppMeasurement.js` tas bort. Den förväntas bli tillgänglig via DTM:s Adobe Analytics-verktyg.
   > * Anropet till `assetAnalytics.dispatcher.init`() har tagits bort. Funktionen förväntas anropas när inläsningen av DTM:s Adobe Analytics-verktyg är klar.
   > * Beroende på var sidspåraren för tillgångsinsikter finns (till exempel AEM, CDN och så vidare) kan skriptkällans ursprung kräva ändringar.
   > * För AEM-värdbaserad sidspårare ska källan peka på en publiceringsinstans med värdnamnet för dispatcher-instansen.


1. Öppna `https://dtm.adobe.com`. Klicka på **[!UICONTROL Översikt]** i webbegenskapen och klicka på **[!UICONTROL Lägg till verktyg]** eller öppna ett befintligt Adobe Analytics-verktyg. While creating the tool, you can set **[!UICONTROL Configuration Method]** to **[!UICONTROL Automatic]**.

   ![Lägg till Adobe Analytics-verktyget](assets/Add-Adobe-Analytics-Tool.png)

   Select Staging/Production report suites, as appropriate.

1. Expand **[!UICONTROL Library Management]**, and ensure that **[!UICONTROL Load Library at]** is set to **[!UICONTROL Page Top]**.

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. Expand **[!UICONTROL Customize Page Code]**, and click or tap **[!UICONTROL Open Editor]**.

   ![chlimage_1-62](assets/chlimage_1-198.png)

1. Paste the following code in the window:

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

   * Regeln för sidinläsning i DTM innehåller bara `pagetracker.js` koden. Any `assetAnalytics` fields are considered as overrides for default values. De är inte obligatoriska som standard.
   * The code calls `assetAnalytics.dispatcher.init()` after making sure that `_satellite.getToolsByType('sc')[0].getS()` is initialized and `assetAnalytics,dispatcher.init` is available. Du kan därför hoppa över att lägga till den i steg 11.
   * Som framgår av kommentarerna i Insights Page Tracker-koden (**[!UICONTROL Verktyg > Resurser > Insights Page Tracker]**) är de tre första argumenten (RSID, Tracking Server och Visitor Namespace) irrelevanta när sidspåraren inte skapar ett `AppMeasurement` objekt. Empty strings are passed instead to highlight this.\
      The remaining arguments correspond to what is configured in the Insights Configuration page (**[!UICONTROL Tools > Assets > Insights Configuration]**).
   * The AppMeasurement object is retrieved by querying `satelliteLib` for all available SiteCatalyst engines. Om flera taggar har konfigurerats ändrar du indexvärdet för arrayväljaren på rätt sätt. Posterna i arrayen ordnas enligt de SiteCatalyst-verktyg som finns i DTM-gränssnittet.

1. Spara och stäng fönstret Kodredigeraren och spara sedan ändringarna i verktygskonfigurationen.
1. In the **[!UICONTROL Approvals]** tab, approve both the pending approvals. The DTM tag is ready for insertion in your web page. For details on how to insert DTM tags in web pages, see [Integrate DTM in custom page templates](https://blogs.adobe.com/experiencedelivers/experience-management/integrating-dtm-custom-aem6-page-template/).
