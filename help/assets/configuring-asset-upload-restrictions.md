---
title: Konfigurera överföringsbegränsningar för resurser
description: 'Begränsa den typ av resurser (filer) som användare kan överföra '
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 30%

---


# Konfigurera överföringsbegränsningar för resurser {#configuring-asset-upload-restrictions}

Du kan konfigurera [!DNL Adobe Experience Manager Assets] för att begränsa vilken typ av resurser som användare kan överföra. Det förhindrar oavsiktliga överföringar av oönskade format och skadliga filer. Med `Day CQ DAM Asset Upload Restriction` tjänsten kan du styra vilken typ av filer som användare kan överföra. Som standard [!DNL Assets] tillåter användare att överföra resurser av alla MIME-typer. Du kan dock konfigurera tjänsten så att den begränsar användare till att överföra filer av specifika MIME-typer.

1. Öppna Configuration Manager-webbkonsolen. Öppna `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Day CQ DAM Asset Upload Restriction]** service in Edit mode. Som standard är alternativet **Tillåt alla MIME** markerat, vilket gör att användare kan överföra filer av alla MIME-typer.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. Om du vill att användarna bara ska kunna överföra filer av vissa MIME-typer avmarkerar du alternativet **[!UICONTROL Allow all MIME]** och anger tillåtna MIME-typer i fälten **[!UICONTROL Allowed Asset MIMEs (regex)]** med reguljära uttryck.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Click **[!UICONTROL Save]** to save the changes. Om du anger MIME-strängar för tillåtna MIME-typer misslyckas överföringen för alla resurser med en MIME-typ som inte matchar de konfigurerade MIME-strängarna i dessa fält.
