---
title: Lösningsintegrering
seo-title: Solutions Integration
description: Läs mer om integrering av lösningar i AEM.
seo-description: Learn more about Solutions Integration in AEM.
uuid: 3bf56b1b-284d-4f14-8974-0a595ece5028
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b5ff918d-08ab-4307-a807-693468fc083b
exl-id: ee5e8ebb-773f-4aa6-9c3e-2cc3bf4a3bbd
source-git-commit: d19b203ffe75a5628f350113d4d74a2916beffc8
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---

# Lösningsintegrering{#solutions-integration}

* [Integrera med Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md)
* [Integrera med tredjepartstjänster](/help/sites-administering/third-party-services.md)
* [Analyser med externa leverantörer](/help/sites-administering/external-providers.md)
* [Katalogproducent](/help/sites-administering/catalog-producer.md)
* [SharePoint Connector](/help/sites-administering/sharepoint-connector.md)

Följande information finns om hur du integrerar AEM med andra Adobe- eller tredjepartstjänster:

>[!NOTE]
>
>Om du använder en anpassad proxykonfiguration tillsammans med integreringen måste du konfigurera båda HTTP-klientproxykonfigurationerna eftersom vissa funktioner i AEM använder 3.x-API:erna och andra 4.x-API:er:
>
>* 3.x har konfigurerats med [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x har konfigurerats med [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>

