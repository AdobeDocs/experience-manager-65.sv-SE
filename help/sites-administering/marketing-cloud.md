---
title: Integrera med Adobe Marketing Cloud
description: Lär dig hur du integrerar Adobe Experience Manager med Adobe Marketing Cloud.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ba518290-dd82-44dc-ae7c-c8152df89179
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 1%

---

# Integrera med Adobe Marketing Cloud{#integrating-with-the-adobe-marketing-cloud}

The [Adobe Marketing Cloud](https://www.adobe.com/solutions/digital-marketing.html), innehåller kraftfulla produkter för webbanalys och webbplatsoptimering som levererar användbara data och insikter i realtid för att driva framgångsrika onlineinitiativ. Det erbjuder en integrerad och öppen plattform för optimering av onlineverksamhet. Molnet består av integrerade program för att samla in och släppa loss kraften i kundinsikterna för att optimera kundvärvning, konvertering och lojalitet samt för att skapa och distribuera innehåll.

Med Adobe Experience Manager (AEM) kan du smidigt integrera med följande Adobe Marketing Cloud-produkter:

* Adobe Analytics förser marknadsförarna med användbar realtidsinformation om onlinestrategier och marknadsföringsinitiativ.
* Adobe Target ger marknadsförarna möjlighet att kontinuerligt göra sitt webbinnehåll mer relevant för sina kunder, vilket ger större konverteringsgrad.
* Adobe Dynamic Media Classic automatiserar mediehanteringen, effektiviserar webbpubliceringen och förbättrar webbupplevelserna - allt i en hostingmiljö.
* Adobe Dynamic Tag Management ger marknadsförarna intuitiva verktyg för att snabbt och enkelt hantera ett obegränsat antal taggar från Adobe och externa leverantörer.
<!-- Search&Promote is end of life as of September 1, 2022 * Adobe Search&Promote gives marketers the ability to control and optimize the search results on their sites. -->
* Med Adobe Campaign kan ni hantera e-postleveransen direkt i Adobe Experience Manager.

Dessutom kan du [integrera AEM med Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) och med [tredjepartstjänster](/help/sites-administering/third-party-services.md).

## Integrera med Adobe Analytics {#integrating-with-adobe-analytics}

[Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) är den branschledande lösningen som ger digitala marknadsförare en plats där de kan mäta, analysera och optimera integrerade data från alla onlineinitiativ över flera marknadsföringskanaler. Det ger marknadsförarna användbar webbanalysinformation i realtid om digitala strategier och marknadsföringsinitiativ. Adobe Analytics hjälper marknadsförarna att snabbt identifiera de mest lönsamma vägarna via en webbplats, segmentera trafiken för att hitta värdefulla webbbesökare, avgöra var besökarna navigerar bort från webbplatsen och identifiera viktiga framgångsmått för onlinemarknadsföringskampanjer.

Du kan använda Adobe Analytics för att analysera data från dina webbplatser.

Genom att integrera med Adobe Analytics kan du göra följande:

* Aktivera användarspårning i Analytics.
* Mappa körningslägena (till exempel författare, publicera) till olika rapportsviter.
* Skicka klientkontextvariabler som konverteringsvariabler eller trafikegenskaper.
* Använd fördefinierade variabelmappningar.
* Konfigurera hela webbplatsavsnitt samtidigt.
* Spåra anpassade händelser.

Mer information om hur du integrerar AEM med Analytics finns i [Integrera med Adobe Analytics](/help/sites-administering/adobeanalytics.md).

Du kan också använda [Guiden Anmäl dig](/help/sites-administering/opt-in.md) för att enkelt kunna genomföra integreringen.

## Integrera med Adobe Target {#integrating-with-adobe-target}

[Adobe Target](https://www.omniture.com/en/products/conversion/test-and-target) används av marknadsförare för att utforma och genomföra onlinetester, skapa direktsända målgruppssegment (baserat på beteende) och automatisera målgruppsanpassningen för innehåll och onlineupplevelser.

Dagens onlinekonsumenter har ständigt nya behov och förväntar sig relevant, till och med personaliserat innehåll från en mängd olika webbplatser och innehållskällor som de kan välja bland. För att engagera en webbpublik är det viktigt att onlinemarknadsförarna snabbt kan identifiera vilka erbjudanden och vilket innehåll som är relevant och engagerande för deras målgrupper. Med denna kunskap i ryggen behöver marknadsförarna möjlighet att kontinuerligt utveckla sina webbplatser och rikta lämpligt innehåll till olika målgrupper.

[Integrera med Adobe Target](/help/sites-administering/target.md) förklarar hur du kan integrera din webbplats med Target.

Du kan också använda [Guiden Anmäl dig](/help/sites-administering/opt-in.md) för att enkelt kunna genomföra integreringen.

## Anmäl dig till Analytics och Target {#opting-in-to-analytics-and-target}

AEM erbjuder en enkel anmälningsprocedur för integrering med Adobe Analytics och Adobe Target. När du loggar in som administratör och går till projektkonsolen visas en anmälningsguide.

![chlimage_1-107](assets/chlimage_1-107a.png)

Anmäl dig till integreringen med Analytics och/eller Target för att göra det möjligt att använda deras funktioner för sidspårning och sidanalys samt personaliseringsfunktioner. När du väljer att vara med måste du ange din användarkontoinformation och ange vilka sidor som ska spåras.

Mer information finns i [Till Adobe Analytics och Adobe Target.](/help/sites-administering/opt-in.md)

## Integrera med Adobe Dynamic Media Classic {#integrating-with-scene}

Adobe Dynamic Media Classic är en värdbaserad lösning för publicering, hantering, förbättring och leverans av dynamiskt marknadsföringsmaterial och visuell marknadsföring på webben, mobiler, e-post, sociala medier, internetanslutna skärmar och tryck.

I Adobe Experience Manager kan du publicera digitala resurser direkt från Adobe Experience Manager till Dynamic Media Classic och du kan publicera digitala resurser från Dynamic Media Classic till Adobe Experience Manager.

Dessutom kan du visa Adobe Experience Manager-resurser som publicerats i Dynamic Media Classic i olika visningsprogram, till exempel Grundläggande zoom och Video.

Mer information om hur Adobe Experience Manager integreras med Dynamic Media Classic finns i [Integrera med Dynamic Media Classic](/help/sites-administering/scene7.md) dokumentation.

## Integrera med Adobe Dynamic Tag Management {#integrating-with-adobe-dynamic-tag-management}

[Adobe Dynamic Tag Management](https://www.adobe.com/solutions/digital-marketing/dynamic-tag-management.html) ger marknadsförarna intuitiva verktyg för att snabbt och enkelt hantera ett obegränsat antal taggar från Adobe och tredje part. Du får större kontroll och flexibilitet att optimera praktiskt taget allt online, samtidigt som du minskar beroendet av IT-resurser.

[Integrera Adobe Dynamic Tag Management](/help/sites-administering/dtm.md) med AEM så att du kan använda dina dynamiska Tag Management-webbegenskaper för att spåra AEM webbplatser.

## Integrera med Adobe Audience Manager {#integrating-with-adobe-audience-manager}

Integreringen av Audience Manager har tagits bort i AEM 6.3.

<!-- Search&Promote is end of life as of September 1, 2022 ## Integrating with Search&Promote {#integrating-with-search-promote} -->

<!-- Search&Promote is end of life as of September 1, 2022 Adobe Search&Promote enables marketers to optimizehow visitors browse, find, compare, and select relevant products and content on web and mobile sites. Businesses can easily promote priority items based on business objectives and visitor intent, as well as automate merchandising and promotions activity via KPI-based triggers or metrics. -->

<!-- Search&Promote is end of life as of September 1, 2022 Adobe Search&Promote is a reliable and scalable hosted site search application, capable of scaling to millions of pages or products, for heavily visited online businesses ranging from retail to news sites. It offers unprecedented levels of marketer control and metrics-based relevance. -->

<!-- Search&Promote is end of life as of September 1, 2022 For information about integrating AEM and Search&Promote, see [Integrating with Adobe Search&Promote](/help/sites-administering/search-and-promote.md). -->

## Integrera med Adobe Campaign {#integrating-with-adobe-campaign}

[Adobe Campaign](https://www.adobe.com/solutions/campaign-management.html) Med kan du hantera e-postinnehåll direkt i Adobe Experience Manager.

Mer information om hur AEM integreras med Adobe Campaign finns i [Integrera med Adobe Campaign](/help/sites-administering/campaignstandard.md).

## Integrera med Livefyre {#integrating-with-livefyre}

Läs om AEM och Livefyre:

* [Komma igång med Livefyre](https://answers.livefyre.com/developers/getting-started)

* [Livefyre och AEM](https://answers.livefyre.com/product/livefyre-for-adobe-experience-manager-aem/livefyre-for-adobe-experience-manager/)
