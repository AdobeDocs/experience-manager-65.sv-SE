---
title: Konfigurera Assets Insights för att få analyser.
description: Konfigurera resursinsikter i [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Admin
feature: Asset Insights,Asset Reports
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 1%

---

# Konfigurera resursinsikter {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] hämtar användningsdata om digitala resurser som används av tredjepartswebbplatser från [!DNL Adobe Analytics]. Om du vill att Assets Insights ska kunna hämta data och generera insikter måste du först konfigurera funktionen så att den integreras med [!DNL Adobe Analytics]. Om du vill använda den här funktionen i en lokal installation ska du köpa [!DNL Adobe Analytics] separat. Kunder på [!DNL Managed Services] ta [!DNL Analytics] licens som medföljer [!DNL Experience Manager]. Se [Managed Services produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>Insikter stöds endast och tillhandahålls för bilder.

1. I [!DNL Experience Manager], klicka **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Klicka på **[!UICONTROL Insights Configuration]** kort.
1. Välj ett datacenter i guiden och ange dina autentiseringsuppgifter, inklusive namnet på din organisation, användarnamn och delad hemlighet.

   ![Konfigurera Adobe Analytics för Assets Insights i Experience Manager](assets/insights_config2.png)

   *Bild: Konfigurera [!DNL Adobe Analytics] för Assets Insights i [!DNL Experience Manager].*

1. Klicka på **[!UICONTROL Authenticate]**.
1. Efter [!DNL Experience Manager] autentiserar dina inloggningsuppgifter från **[!UICONTROL Report Suite]** välj en [!DNL Adobe Analytics] Rapportera paket där du vill att Assets Insights ska hämta data. Klicka på **[!UICONTROL Add]**.
1. Efter [!DNL Experience Manager] ställer in din rapportsvit, klicka på **[!UICONTROL Done]**.

## Sidspårare {#page-tracker}

När du har konfigurerat [!DNL Adobe Analytics] så genereras sidspårningskoden åt dig. Aktivera resursinsikter för att spåra [!DNL Experience Manager] resurser som används på tredjepartswebbplatser, inkluderar sidspårningskoden i webbplatskoden. Använd [!UICONTROL Page Tracker] utility in [!DNL Experience Manager Assets] för att generera sidspårningskod. Mer information om hur du inkluderar Page Tracker-koden på webbsidor från tredje part finns i [Använda sidspårning och bädda in kod på webbsidor](/help/assets/use-page-tracker.md).

1. I [!DNL Experience Manager], klicka **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. Från **[!UICONTROL Navigation]** klickar du på **[!UICONTROL Insights Page Tracker]** kort.
1. Klicka **[!UICONTROL Download]** för att hämta sidspårningskod.
