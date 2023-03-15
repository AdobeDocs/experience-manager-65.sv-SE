---
title: Ange att referensfiltret ska vara tomt
seo-title: Setting Your Referrer Filter to Allow Empty
description: Följ den här sidan om du vill veta mer om referensfiltret. Om du vill att AEM Mobile Application Viewer ska kunna visa program på din Author-instans måste du ange HTML-referensfiltret till"allow empty".
seo-description: Follow this page to learn about Referrer Filter. In order to allow the AEM Mobile Application Viewer to view apps on your Author instance, you'll need to set your HTML referrer filter to 'allow empty'.
uuid: 4fb0f95c-ac8f-4a14-8c46-6616d9d4f380
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 8fb7d088-94bf-4799-98b3-8fa58eef83df
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# Ange att referensfiltret ska vara tomt{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

Om du vill att AEM Mobile Application Viewer ska kunna visa program på din Author-instans måste du ange HTML-referensfiltret till&quot;allow empty&quot;.

Om du inte tänker använda programvisningsprogrammet för att granska program i utvecklings- och mellanlagringslägen, behöver du inte ändra standardinställningen för referensfiltret.

Navigera till följande i den Author-instans av AEM som du kör: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) och sök efter &#39;Apache Sling Referrer Filter&#39;. Klicka för att redigera referensfiltret och markera kryssrutan Tillåt tomt (se bilden nedan). Tryck sedan på knappen Spara och stäng webbläsarsidan.

![Inställningar för referensfilter](assets/chlimage_1-106.png)
