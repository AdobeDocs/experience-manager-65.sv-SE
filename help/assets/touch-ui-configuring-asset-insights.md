---
title: Konfigurera tillgångsinsikter
description: Konfigurera tillgångsinsikter i AEM Resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 6d4f79c126a3c44666e2a42b2246c964813d24ab

---


# Konfigurera tillgångsinsikter {#configure-asset-insights}

Adobe Experience Manager (AEM) Assets hämtar användningsdata om AEM-resurser som används av tredjepartswebbplatser från Adobe Analytics. Om du vill att tillgångsinsikter ska kunna hämta data och generera insikter måste du först konfigurera funktionen så att den integreras med Adobe Analytics.

>[!NOTE]
>
>Insikter stöds endast och tillhandahålls för bilder.

1. I AEM klickar du på **[!UICONTROL Verktyg]** > **[!UICONTROL Resurser]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Klicka på **[!UICONTROL Insights Configuration]** -kortet.
1. Välj ett datacenter i guiden och ange dina autentiseringsuppgifter, inklusive namnet på din organisation, användarnamn och delad hemlighet.

   ![Konfigurera Adobe Analytics för Assets Insights i AEM](assets/insights_config2.png)


   *Bild:Konfigurera Adobe Analytics för Assets Insights i AEM*

1. Klicka/tryck på **[!UICONTROL Autentisera]**.
1. När AEM har autentiserat dina inloggningsuppgifter väljer du en Adobe Analytics-rapportssvit från **[!UICONTROL Report Suite]** -listan, där du vill att resursinsikter ska hämta data. Click **[!UICONTROL Add]**.
1. När AEM har konfigurerat rapportsviten klickar/trycker du på **[!UICONTROL Klar]**.

## Sidspårare {#page-tracker}

När du har konfigurerat ditt Adobe Analytics-konto genereras sidspårningskoden åt dig. Om du vill göra det möjligt för Assets Insights att spåra AEM-resurser som används på tredjepartswebbplatser, inkluderar du sidspårningskoden i webbplatskoden. Använd sidspårningsverktyget i AEM Resurser för att generera sidspårningskod. Mer information om hur du inkluderar Page Tracker-kod i tredjepartswebbsidor finns i [Använda sidspåraren och bädda in kod på webbsidor](/help/assets/touch-ui-using-page-tracker.md).

1. I AEM klickar du på **[!UICONTROL Verktyg]** > **[!UICONTROL Resurser]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. På **[!UICONTROL navigeringssidan]** klickar du på **[!UICONTROL Insights Page Tracker]** -kortet.
1. Klicka på **[!UICONTROL Hämta]** för att hämta sidspårningskoden.
