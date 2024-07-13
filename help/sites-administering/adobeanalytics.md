---
title: Integrera med Adobe Analytics
description: Lär dig hur du integrerar Adobe Experience Manager (AEM) med Adobe Analytics.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 0a87ece4-57ed-4022-a78a-264c1edf4b4e
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 19%

---

# Integrera med Adobe Analytics{#integrating-with-adobe-analytics}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/integrations/integrating-adobe-analytics.html) |
| AEM 6.5 | Den här artikeln |


Genom att integrera Adobe Analytics och AEM kan du spåra webbsidans aktivitet:

* Med en Adobe Analytics-konfiguration kan AEM autentisera med Adobe Analytics.
* Ett ramverk identifierar de data som skickas till din Adobe Analytics-rapportsserie.

Data innehåller sid- och användardata, till exempel:

* data som AEM komponenter samla in
* länkklick
* videoanvändningsinformation
* antalet sidbesök från Adobe Analytics

Följande sidor hjälper dig att konfigurera integreringen:

* [Ansluta till Adobe Analytics och skapa ramverk](/help/sites-administering/adobeanalytics-connect.md)
* [Konfigurera länkspårning för Adobe Analytics](/help/sites-administering/adobeanalytics-link.md)
* [Mappa komponentdata med Adobe Analytics-egenskaper](/help/sites-administering/adobeanalytics-mapping.md)
* [Konfigurera videospårning för Adobe Analytics](/help/sites-administering/adobeanalytics-video.md)
* [Adobe-klassificeringar](/help/sites-administering/adobeanalytics-classifications.md)

Du kan också använda guiden [Anmäl dig](/help/sites-administering/opt-in.md) för att enkelt utföra integreringen.

>[!NOTE]
>
>Se även artikeln [Integrera AEM med Adobe Target och Adobe Analytics med DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

## Ytterligare information {#further-information}

Se:

* [Utöka Adobe Analytics-integrationen](/help/sites-developing/extending-analytics.md) om du vill ha information om hur du utvecklar komponenter som samlar in användardata och anpassar Adobe Analytics-ramverket.
* Kunskapsbasartikeln [Integrering med Adobe Analytics - felsökning](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), innehåller information om hur du felsöker integreringen med Adobe Analytics.

>[!NOTE]
>
>Om du använder Adobe Analytics med en anpassad proxykonfiguration måste du [konfigurera två OSGi-paket](/help/sites-deploying/configuring-osgi.md) (till exempel med webbkonsolen) som krävs för proxykonfigurationerna i **Apaches HTTP-klient**. Båda är obligatoriska eftersom vissa funktioner i AEM använder 3.x-API:erna, medan andra använder 4.x-API:erna. Konfigurera:
>
>* **Day Commons HTTP Client 3.1** för att konfigurera 3.x API;
>  till exempel [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Proxykonfiguration för Apache HTTP Components** för att konfigurera 4.x API;
>  till exempel [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>
