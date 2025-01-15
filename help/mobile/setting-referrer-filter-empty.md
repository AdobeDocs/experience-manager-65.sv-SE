---
title: Ange att referensfiltret ska vara tomt
description: Läs mer om referensfilter. Om du vill att Adobe Experience Manager (AEM) Mobile Application Viewer ska kunna visa program på din Author-instans måste du ställa in HTML-referensfiltret på"allow empty".
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Ange att referensfiltret ska vara tomt{#setting-your-referrer-filter-to-allow-empty}

{{ue-over-mobile}}

Om du vill att Adobe Experience Manager (AEM) Mobile Application Viewer ska kunna visa program på din Author-instans måste du ställa in HTML-referensfiltret på&quot;allow empty&quot;.

Om du inte tänker använda Application Viewer för att granska program i utvecklings- och mellanlagringslägen, behöver du inte ändra standardinställningen för referensfiltret.

Gå till [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) i den Author-instans av AEM som du kör och sök efter &#39;Apache Sling Referrer-filter&#39;. Klicka för att redigera referensfiltret och markera kryssrutan Tillåt tomt (se bilden nedan). Tryck sedan på knappen Spara och stäng webbläsarsidan.

![Inställningar för referensfilter](assets/chlimage_1-106.png)
