---
title: Identifiera MIME-typ av resurser med Apache Tika
description: Aktivera Apache Tika som hjälp [!DNL Experience Manager Assets] identifiera MIME-typen för resurser från innehållsströmmen under överföringen i stället för filtillägget.
contentOwner: AG
role: Admin, Architect
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 1%

---

# Identifiera MIME-typ av resurser med [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

Normalt [!DNL Adobe Experience Manager Assets] identifierar MIME-typen för resurser som du överför från filtillägget.

Om du [!DNL Apache Tika] för att överföra resurser, [!DNL Assets] identifierar sin MIME-typ från innehållsströmmen under överföringen i stället för filtillägget.

Den här funktionen är inaktiverad som standard. Om du vill aktivera funktionen konfigurerar du **[!UICONTROL Day CQ DAM Mime Type]** tjänst från [!UICONTROL Configuration Manager].

>[!NOTE]
>
>MIME-typidentifiering med [!DNL Apache Tika] biblioteket är en resurskrävande åtgärd.

1. Om du vill öppna webbkonsolen för Configuration Manager går du till `https://[aem_server]:[port]/system/console/configMgr`.

1. I listan över tjänster letar du upp **[!UICONTROL Day CQ DAM Mime Type Service]** och klicka **[!UICONTROL Edit]**.

1. Välj **[!UICONTROL Detect MIME from content]** om du vill aktivera parsning av överförda resurser för att bestämma deras MIME-typ samtidigt som filtillägg ignoreras. Som standard är det här alternativet avmarkerat.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Klicka **[!UICONTROL Save]** för att spara ändringarna.
