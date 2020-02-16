---
title: Integrera med Adobe Analytics
seo-title: Integrera med Adobe Analytics
description: Lär dig hur du integrerar AEM med Adobe Analytics.
seo-description: Lär dig hur du integrerar AEM med Adobe Analytics.
uuid: d8548263-6ac5-45fb-8c70-52ecd4161bbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 444c522e-2f33-4f41-846c-8d317e799659
docset: aem65
translation-type: tm+mt
source-git-commit: ca25e66b280db479f69c487753a557b0240233da

---


# Integrera med Adobe Analytics{#integrating-with-adobe-analytics}

Genom att integrera Adobe Analytics och AEM kan ni följa webbsidans aktivitet:

* Med en Adobe Analytics-konfiguration kan AEM autentisera med Adobe Analytics.
* Ett ramverk identifierar de data som skickas till rapportsviten för Adobe Analytics.

Informationen innehåller sid- och användardata. till exempel:

* data som AEM-komponenter samlar in
* länkklick
* videoanvändningsinformation
* antalet sidbesök från Adobe Analytics

Följande sidor hjälper dig att konfigurera integreringen:

* [Ansluta till Adobe Analytics och skapa ramverk](/help/sites-administering/adobeanalytics-connect.md)
* [Konfigurera länkspårning för Adobe Analytics](/help/sites-administering/adobeanalytics-link.md)
* [Mappa komponentdata med Adobe Analytics-egenskaper](/help/sites-administering/adobeanalytics-mapping.md)
* [Konfigurera videospårning för Adobe Analytics](/help/sites-administering/adobeanalytics-video.md)
* [Adobe-klassificeringar](/help/sites-administering/adobeanalytics-classifications.md)

Du kan också använda guiden [](/help/sites-administering/opt-in.md) Anmäl dig för att enkelt utföra integreringen.

>[!NOTE]
>
>Se även artikeln med instruktioner: Integrera AEM [med Adobe Target och Adobe Analytics med DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

## Ytterligare information {#further-information}

Se:

* [Utöka Adobe Analytics-integreringen](/help/sites-developing/extending-analytics.md) för information om hur du utvecklar komponenter som samlar in användardata och anpassar Adobe Analytics-ramverket.
* Kunskapsbasartikeln, [Adobe Analytics-integrering - felsökningsproblem](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), innehåller information om hur du felsöker Adobe Analytics-integreringen.

>[!NOTE]
>
>Om du använder Adobe Analytics med en anpassad proxykonfiguration måste du [konfigurera två OSGi-paket](/help/sites-deploying/configuring-osgi.md) (till exempel med webbkonsolen) som krävs för **Apache HTTP Client** -proxykonfigurationerna. Båda är obligatoriska eftersom vissa funktioner i AEM använder 3.x-API:erna, medan andra använder 4.x-API:erna. Konfigurera:
>
>* **Day Commons HTTP Client 3.1** för att konfigurera 3.x API;
   >  till exempel [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **Proxykonfiguration** för Apache HTTP Components för att konfigurera 4.x API;
   >  till exempel [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>



