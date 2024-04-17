---
title: Lösningsintegrering
description: Läs mer om hur du integrerar Adobe Experience Manager (AEM) med andra Adobe- eller tredjepartstjänster.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ee5e8ebb-773f-4aa6-9c3e-2cc3bf4a3bbd
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Lösningsintegrering{#solutions-integration}

* [Integrera med Adobe Experience Cloud](/help/sites-administering/marketing-cloud.md)
* [Integrera med tredjepartstjänster](/help/sites-administering/third-party-services.md)
* [Analyser med externa leverantörer](/help/sites-administering/external-providers.md)
* [Katalogproducent](/help/sites-administering/catalog-producer.md)
* [Förstå, använda och strukturera smarta taggar](/help/assets/enhanced-smart-tags.md)

Följande information finns om hur du integrerar AEM med andra Adobe- eller tredjepartstjänster:

>[!NOTE]
>
>Om du använder en anpassad proxykonfiguration tillsammans med integreringen måste du konfigurera båda HTTP-klientproxykonfigurationerna eftersom vissa funktioner i AEM använder 3.x-API:erna och andra 4.x-API:er:
>
>* 3.x har konfigurerats med [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x har konfigurerats med [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>
