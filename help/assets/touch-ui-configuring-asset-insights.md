---
title: Konfigurera tillgångsinsikter för att få analyser.
description: Konfigurera tillgångsinsikter i [!DNL Adobe Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 1%

---


# Konfigurera tillgångsinsikter {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] hämtar användningsdata om digitala resurser som används av tredjepartswebbplatser från [!DNL Adobe Analytics]. Om du vill att tillgångsinsikter ska kunna hämta dessa data och generera insikter måste du först konfigurera funktionen så att den integreras med Adobe Analytics.

>[!NOTE]
>
>Insikter stöds endast och tillhandahålls för bilder.

1. Klicka [!DNL Experience Manager]på **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Klicka på **[!UICONTROL Insights Configuration]** kortet.
1. Välj ett datacenter i guiden och ange dina autentiseringsuppgifter, inklusive namnet på din organisation, användarnamn och delad hemlighet.

   ![Konfigurera Adobe Analytics för Assets Insights i Experience Manager](assets/insights_config2.png)

   *Bild: Konfigurera[!DNL Adobe Analytics]för Assets Insights i[!DNL Experience Manager].*

1. Klicka på **[!UICONTROL Authenticate]**.
1. När du har [!DNL Experience Manager] autentiserat dina inloggningsuppgifter väljer du i **[!UICONTROL Report Suite]** listan en [!DNL Adobe Analytics] rapportsserie där du vill att tillgångsinsikter ska hämta data. Klicka på **[!UICONTROL Add]**.
1. När du har [!DNL Experience Manager] konfigurerat rapportsviten klickar du på **[!UICONTROL Done]**.

## Sidspårare {#page-tracker}

När du har konfigurerat ditt [!DNL Adobe Analytics] konto genereras sidspårningskoden åt dig. Om du vill att Assets Insights ska kunna spåra [!DNL Experience Manager] resurser som används på tredjepartswebbplatser, inkluderar du sidspårningskoden i webbplatskoden. Använd [!UICONTROL Page Tracker] verktyget i [!DNL Experience Manager Assets] för att generera sidspårningskod. Mer information om hur du inkluderar Page Tracker-kod i tredjepartswebbsidor finns i [Använda sidspåraren och bädda in kod på webbsidor](/help/assets/touch-ui-using-page-tracker.md).

1. Klicka [!DNL Experience Manager]på **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. På **[!UICONTROL Navigation]** sidan klickar du på **[!UICONTROL Insights Page Tracker]** kortet.
1. Klicka **[!UICONTROL Download]** för att hämta sidspårningskoden.
