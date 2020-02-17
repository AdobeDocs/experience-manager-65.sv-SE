---
title: Identifiera MIME-typ av resurser med Apache Tika
description: Aktivera Apache Tika för att hjälpa AEM Assets att identifiera MIME-typen för resurser från innehållsströmmen under överföringen i stället för filtillägget.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Identifiera MIME-typ av resurser med Apache Tika {#detecting-mime-type-of-assets-using-apache-tika}

I vanliga fall identifierar Adobe Experience Manager (AEM) Assets den MIME-typ av resurser som du överför från filtillägget.

Om du använder Apache Tika för att överföra resurser, identifierar AEM Resurser deras MIME-typ från innehållsströmmen under överföringen i stället för filtillägget.

Den här funktionen är inaktiverad som standard. Om du vill aktivera funktionen konfigurerar du tjänsten Dag CQ DAM Mime Type **[!UICONTROL från]** Configuration Manager .

>[!NOTE]
>
>MIME-typidentifiering med Apache Tika-biblioteket är en resurskrävande åtgärd.

1. Om du vill öppna webbkonsolen för Configuration Manager går du till `https://[aem_server]:[port]/system/console/configMgr`.
1. I listan över tjänster går du till **[!UICONTROL Day CQ DAM Mime Type Service]** och trycker på **[!UICONTROL Edit]** Bside it för att öppna den i Edit-läget.

1. Välj alternativet **[!UICONTROL Identifiera MIME från innehåll]** om du vill aktivera parsning av överförda resurser för att bestämma MIME-typen samtidigt som filtillägg ignoreras. Som standard är det här alternativet avmarkerat.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Klicka/tryck på **[!UICONTROL Spara]** för att spara ändringarna.
