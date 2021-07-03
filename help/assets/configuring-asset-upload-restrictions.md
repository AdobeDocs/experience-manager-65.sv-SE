---
title: Konfigurera överföringsbegränsningar för resurser
description: 'Begränsa den typ av resurser (filer) som användare kan överföra '
contentOwner: AG
role: Developer, Admin, Architect
feature: Resurshantering,Överför
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 31%

---

# Konfigurera överföringsbegränsningar för resurser {#configuring-asset-upload-restrictions}

Du kan konfigurera [!DNL Adobe Experience Manager Assets] för att begränsa vilken typ av resurser som användare kan överföra. Det förhindrar oavsiktliga överföringar av oönskade format och skadliga filer. Med tjänsten `Day CQ DAM Asset Upload Restriction` kan du styra vilken typ av filer som användare kan överföra. Som standard tillåter [!DNL Assets] användare att överföra resurser av alla MIME-typer. Du kan dock konfigurera tjänsten så att den begränsar användare till att överföra filer av specifika MIME-typer.

1. Öppna Configuration Manager-webbkonsolen. Öppna `https://[aem_server]:[port]/system/console/configMgr`.
1. Öppna tjänsten **[!UICONTROL Day CQ DAM Asset Upload Restriction]** i redigeringsläge. Som standard är alternativet **Tillåt alla MIME** markerat, vilket gör att användare kan överföra filer av alla MIME-typer.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. Om du vill att användarna bara ska kunna överföra filer av vissa MIME-typer avmarkerar du alternativet **[!UICONTROL Allow all MIME]** och anger tillåtna MIME-typer i fälten **[!UICONTROL Allowed Asset MIMEs (regex)]** med reguljära uttryck.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Klicka på **[!UICONTROL Save]** för att spara ändringarna. Om du anger MIME-strängar för tillåtna MIME-typer misslyckas överföringen för alla resurser med en MIME-typ som inte matchar de konfigurerade MIME-strängarna i dessa fält.
