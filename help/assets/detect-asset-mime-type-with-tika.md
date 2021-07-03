---
title: Identifiera MIME-typ av resurser med Apache Tika
description: Aktivera Apache Tika för att hjälpa [!DNL Experience Manager Assets] identifiera MIME-typen för resurser från innehållsströmmen under överföringen i stället för filtillägget.
contentOwner: AG
role: Admin, Architect
feature: Metadata,Utvecklarverktyg,Resurshantering
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# Identifiera MIME-typ av resurser med [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

Vanligtvis identifierar [!DNL Adobe Experience Manager Assets] MIME-typen för resurser som du överför från filtillägget.

Om du använder [!DNL Apache Tika] för att överföra resurser identifierar [!DNL Assets] deras MIME-typ från innehållsströmmen under överföringen i stället för filtillägget.

Den här funktionen är inaktiverad som standard. Om du vill aktivera funktionen konfigurerar du tjänsten **[!UICONTROL Day CQ DAM Mime Type]** från [!UICONTROL Configuration Manager].

>[!NOTE]
>
>MIME-typidentifiering med biblioteket [!DNL Apache Tika] är en resurskrävande åtgärd.

1. Öppna Configuration Manager-webbkonsolen genom att gå till `https://[aem_server]:[port]/system/console/configMgr`.

1. Leta reda på **[!UICONTROL Day CQ DAM Mime Type Service]** i listan över tjänster och klicka på **[!UICONTROL Edit]**.

1. Välj alternativet **[!UICONTROL Detect MIME from content]** om du vill aktivera parsning av överförda resurser för att bestämma deras MIME-typ samtidigt som filtillägg ignoreras. Som standard är det här alternativet avmarkerat.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Klicka på **[!UICONTROL Save]** för att spara ändringarna.
