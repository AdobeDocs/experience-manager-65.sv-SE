---
title: AEM Mobile On-Demand
seo-title: AEM Mobile On-Demand
description: För att starta en ny AEM Mobile-appupplevelse krävs det att rollerna är enhetliga innan man kan redigera innehåll. Följ den här sidan för att komma igång med AEM on-demand-tjänster för mobiler.
seo-description: För att starta en ny AEM Mobile-appupplevelse krävs det att rollerna är enhetliga innan man kan redigera innehåll. Följ den här sidan för att komma igång med AEM on-demand-tjänster för mobiler.
uuid: 175c609d-3cb8-4a1b-bfea-278df272e500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: dc6891cd-19cc-4dff-8bda-a41ed8af8bfb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 0%

---


# AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Om du inte använder AEM som innehållshanteringskälla kan du läsa [AEM Mobile On-demand Services Hjälp](https://helpx.adobe.com/digital-publishing-solution/topics.html).

AEM innehåller flera verktyg som gör att du kan integrera ditt innehåll i mobilprogram.

Följande diagram visar hur de olika komponenterna i AEM Mobile och On-Demand Services passar ihop för att leverera innehåll till mobilappar.

AEM kan betraktas som en testmiljö för att förhandsgranska appen och innehållet före publiceringen. medan AEM Mobile App är den slutliga app som har byggts för distribution.

>[!NOTE]
>
>Mer information om preflight-appen finns i [Använda AEM Preflight-appen](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) i AEM Mobile On-demand Services-hjälpen.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>I bilden ovan krävs inte AEM Publish-instansen för ett typiskt distributionsscenario för AEM Mobile On-demand Services.

## Starta en ny mobilapp {#starting-a-new-mobile-app}

AEM Mobile är bara en av de två pelarna som utgör den kompletta AEM.

För att starta en ny AEM Mobile-appupplevelse krävs det att rollerna är enhetliga innan man kan redigera innehåll. Följande roller är en startpunkt när du skapar ett nytt AEM Mobile-program:

* **Administratör**
* **Developer**
* **Författare**

>[!NOTE]
>
>Innan du börjar arbeta med AEM Mobile och följer stegen i den här guiden bör du känna till AEM. Lär dig grunderna i [AEM](/help/sites-deploying/deploy.md).

### Om AEM Mobile Application Dashboard {#understanding-the-aem-mobile-application-dashboard}

Innan användaren förstår vilka roller och ansvarsområden som finns bör han/hon ha kunskap om **AEM Mobile Control Center** eller **Application Dashboard**. Klicka [här](/help/mobile/mobile-apps-ondemand-application-dashboard.md) för en ingående förståelse.

### AEM-administratör {#aem-administrator}

En ***AEM administratör*** ansvarar för att lägga till ett nytt program i AEM Mobile-katalogen, antingen genom att skapa ett nytt program med hjälp av guiden Skapa eller genom att importera ett befintligt program. AEM administratörer som skapar en ny app med AEM Mobile *guide* väljer vanligtvis en av de önskade programmallarna antingen från våra färdiga referensexempel eller (i de flesta fall) en anpassad programmall som skapats av *AEM utvecklare.*

En AEM är ansvarig för följande när du skapar ett program med AEM Mobile On-demand Services:

* [Konfigurera AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [Konfigurera användar- och användargrupper](/help/mobile/aem-mobile-configure-users.md)
* [Förhandsgranska med Preflight](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [Administrera innehållstjänster](/help/mobile/developing-content-services.md)

Information om hur du kommer igång med en administratörs roller och ansvar finns i [Administrera innehåll för att använda AEM Mobile On-demand Services](/help/mobile/aem-mobile.md).

## AEM Developer {#aem-developer}

En **AEM utvecklare** utökar och skapar anpassade webbmallar och komponenter som gör att *AEM Author *kan skapa vackra och engagerande mobilupplevelser. Dessa mallar och komponenter är inte bara optimerade för mobilappsvärlden. men kommunicera både till enheten och till AEM server (valfri fjärrserver) till slutpunkter för flerkanalstjänster. Den AEM inbyggda innehållsredigeraren används av *AEM Authors* för att skapa engagerande och relevanta upplevelser i appen, inklusive integrering med resten av Adobe Marketing Cloud.

En AEM ansvarar för följande när du skapar ett program med AEM Mobile On-demand Services:

* [Appmallar och komponenter](/help/mobile/app-templates-and-components1.md)
* [Mobil med innehållssynkronisering](/help/mobile/mobile-ondemand-contentsync.md)
* [Innehållsegenskaper och export av innehåll](/help/mobile/on-demand-content-properties-exporting.md)
* [Utveckla AEM Mobile Content Services](//help/mobile/developing-content-services.md)

Information om hur du kommer igång med Developer&#39;s roles and responsibility finns i [Utveckla AEM för AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>En *AEM utvecklarroll* börjar och slutar inte med utvecklingen av mallar och komponenter. En *AEM utvecklare* kan skapa ett helt nytt program i stället för att bara utöka det färdiga referensimplementeringsexemplet.

## AEM Author {#aem-author}

En ***AEM Author* (eller *Marketer*)**använder de anpassade utvecklade eller färdiga mallarna och komponenterna för att lägga till och redigera sidor, dra och släppa komponenter och lägga till media av alla typer från DAM, inklusive bilder, videor och textfragment (innehållsfragment). AEM inbyggda innehållsredigeraren används sedan av *AEM Authors* för att skapa engagerande och relevanta upplevelser i appen, inklusive integrering med resten av Adobe Marketing Cloud.

AEM måste förstå följande när de skapar ett program med AEM Mobile On-demand Services:

* [AEM Mobile Application Dashboard](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [Skapa och konfigurera program](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [Molnkonfiguration](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [Hantera innehåll](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [Content Services - översikt](/help/mobile/develop-content-as-a-service.md)

Om du vill komma igång med en författares roller och ansvar kan du läsa [AEM innehåll för AEM Mobile On-demand Services App](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>En AEM-författare ansvarar också för att ställa in tillstånd, skapa kort och layouter samt skicka push-meddelanden. Mer information om metoder för att skapa innehåll. hantera artiklar och samlingar, om du vill skapa banners, kort och layouter i AEM Mobile går du till [AEM Mobile On-Demand Portal](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).

