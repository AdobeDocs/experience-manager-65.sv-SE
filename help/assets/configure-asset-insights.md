---
title: Konfigurera Assets Insights för att få analyser.
description: Konfigurera resursinsikter i [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Admin
feature: Resursinsikter,Resursrapporter
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 1%

---

# Konfigurera resursinsikter {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] hämtar användningsdata om digitala resurser som används av tredjepartswebbplatser från  [!DNL Adobe Analytics]. Om du vill att Assets Insights ska kunna hämta data och generera insikter måste du först konfigurera funktionen så att den integreras med [!DNL Adobe Analytics]. Om du vill använda den här funktionen i en lokal installation måste du köpa [!DNL Adobe Analytics]-licensen separat. Kunder på [!DNL Managed Services] får [!DNL Analytics] licens som paketerats med [!DNL Experience Manager]. Se [Managed Services produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>Insikter stöds endast och tillhandahålls för bilder.

1. I [!DNL Experience Manager] klickar du på **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Klicka på **[!UICONTROL Insights Configuration]**-kortet.
1. Välj ett datacenter i guiden och ange dina autentiseringsuppgifter, inklusive namnet på din organisation, användarnamn och delad hemlighet.

   ![Konfigurera Adobe Analytics för Assets Insights i Experience Manager](assets/insights_config2.png)

   *Bild: Konfigurera  [!DNL Adobe Analytics] för Assets Insights i  [!DNL Experience Manager].*

1. Klicka på **[!UICONTROL Authenticate]**.
1. När [!DNL Experience Manager] har autentiserat dina autentiseringsuppgifter väljer du en [!DNL Adobe Analytics]-rapportsvit från **[!UICONTROL Report Suite]**-listan där du vill att resursinsikter ska hämta data. Klicka på **[!UICONTROL Add]**.
1. När [!DNL Experience Manager] har konfigurerat rapportsviten klickar du på **[!UICONTROL Done]**.

## Sidspårare {#page-tracker}

När du har konfigurerat ditt [!DNL Adobe Analytics]-konto genereras sidspårningskoden åt dig. Om du vill att Assets Insights ska kunna spåra [!DNL Experience Manager]-resurser som används på tredjepartswebbplatser, inkluderar du sidspårningskoden i webbplatskoden. Använd verktyget [!UICONTROL Page Tracker] i [!DNL Experience Manager Assets] för att generera sidspårningskod. Mer information om hur du inkluderar Page Tracker-koden i tredjepartswebbsidor finns i [Använda sidspåraren och bädda in kod i webbsidor](/help/assets/use-page-tracker.md).

1. I [!DNL Experience Manager] klickar du på **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. Klicka på **[!UICONTROL Insights Page Tracker]**-kortet på sidan **[!UICONTROL Navigation]**.
1. Klicka på **[!UICONTROL Download]** om du vill hämta sidspårningskoden.
