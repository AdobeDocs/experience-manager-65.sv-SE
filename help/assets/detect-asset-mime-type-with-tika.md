---
title: Identifiera MIME-typ av resurser med Apache Tika
description: Aktivera Apache Tika för att hjälpa AEM Assets att identifiera MIME-typen för resurser från innehållsströmmen under överföringen i stället för filtillägget.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# Identifiera MIME-typ av resurser med Apache Tika {#detecting-mime-type-of-assets-using-apache-tika}

I vanliga fall identifierar Adobe Experience Manager (AEM) Assets den MIME-typ av resurser som du överför från filtillägget.

Om du använder Apache Tika för att överföra resurser, identifierar AEM Resurser deras MIME-typ från innehållsströmmen under överföringen i stället för filtillägget.

Den här funktionen är inaktiverad som standard. Om du vill aktivera funktionen konfigurerar du **[!UICONTROL Day CQ DAM Mime Type]** tjänsten från [!UICONTROL Configuration Manager].

>[!NOTE]
>
>MIME-typidentifiering med Apache Tika-biblioteket är en resurskrävande åtgärd.

1. Om du vill öppna webbkonsolen för Configuration Manager går du till `https://[aem_server]:[port]/system/console/configMgr`.

1. Leta upp **[!UICONTROL Day CQ DAM Mime Type Service]** och klicka på **[!UICONTROL Edit]** i listan över tjänster.

1. Välj **[!UICONTROL Detect MIME from content]** alternativet för att aktivera parsning av överförda resurser för att bestämma deras MIME-typ samtidigt som filtillägg ignoreras. Som standard är det här alternativet avmarkerat.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Click **[!UICONTROL Save]** to save the changes.
