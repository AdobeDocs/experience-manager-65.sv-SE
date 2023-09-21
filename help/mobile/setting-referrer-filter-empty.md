---
title: Ange att referensfiltret ska vara tomt
description: Läs mer om referensfilter. Om du vill att Adobe Experience Manager (AEM) Mobile Application Viewer ska kunna visa program på din Author-instans måste du ställa in HTML-referensfiltret på"allow empty".
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
source-git-commit: 6799f1d371734b69c547f3c0c68e1e633aa63229
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Ange att referensfiltret ska vara tomt{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

Om du vill att Adobe Experience Manager (AEM) Mobile Application Viewer ska kunna visa program på din Author-instans måste du ställa in HTML-referensfiltret på&quot;allow empty&quot;.

Om du inte tänker använda Application Viewer för att granska program i utvecklings- och mellanlagringslägen, behöver du inte ändra standardinställningen för referensfiltret.

Navigera till följande i den Author-instans av AEM som du kör: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) och sök efter &#39;Apache Sling Referrer Filter&#39;. Klicka för att redigera referensfiltret och markera kryssrutan Tillåt tomt (se bilden nedan). Tryck sedan på knappen Spara och stäng webbläsarsidan.

![Inställningar för referensfilter](assets/chlimage_1-106.png)
