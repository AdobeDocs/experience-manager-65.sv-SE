---
title: Integrera med Adobe Analytics
seo-title: Integrera med Adobe Analytics
description: Lär dig integrera AEM med Adobe Analytics.
seo-description: Lär dig integrera AEM med Adobe Analytics.
uuid: d8548263-6ac5-45fb-8c70-52ecd4161bbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 444c522e-2f33-4f41-846c-8d317e799659
docset: aem65
translation-type: tm+mt
source-git-commit: ca25e66b280db479f69c487753a557b0240233da
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 20%

---


# Integrera med Adobe Analytics{#integrating-with-adobe-analytics}

Genom att integrera Adobe Analytics och AEM kan du spåra webbsidans aktivitet:

* Med en Adobe Analytics-konfiguration kan AEM autentisera med Adobe Analytics.
* Ett ramverk identifierar de data som skickas till din Adobe Analytics-rapportsserie.

Informationen innehåller sid- och användardata. till exempel:

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

Du kan också använda [Opt-in-guiden](/help/sites-administering/opt-in.md) för att enkelt utföra integreringen.

>[!NOTE]
>
>Se även artikeln med instruktioner: [Integrera AEM med Adobe Target och Adobe Analytics med DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

## Ytterligare information {#further-information}

Se:

* [Utvidga Adobe Analytics ](/help/sites-developing/extending-analytics.md) Integrationför information om utveckling av komponenter som samlar in användardata och anpassar Adobe Analytics ramverk.
* Kunskapsbasartikeln [Adobe Analytics-integration - felsökning av problem](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html) innehåller information om hur du felsöker din Adobe Analytics-integrering.

>[!NOTE]
>
>Om du använder Adobe Analytics med en anpassad proxykonfiguration måste du [konfigurera två OSGi-paket](/help/sites-deploying/configuring-osgi.md) (till exempel med webbkonsolen) som krävs för proxykonfigurationerna i **Apaches HTTP-klient**. Båda är obligatoriska eftersom vissa funktioner i AEM använder 3.x-API:erna, medan andra använder 4.x-API:erna. Konfigurera:
>
>* **Day Commons HTTP Client 3.1** för att konfigurera 3.x API;
   >  till exempel [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **Proxykonfiguration** för Apache HTTP Components för att konfigurera 4.x API;
   >  till exempel [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



