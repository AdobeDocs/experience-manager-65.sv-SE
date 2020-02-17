---
title: AEM Mobile On-Demand
seo-title: AEM Mobile On-Demand
description: Att starta en ny upplevelse av AEM-mobilappen kräver att rollerna är enhetliga innan det är klart för innehållsredigering. Följ den här sidan för att komma igång med AEM Mobile On-Demand-tjänster.
seo-description: Att starta en ny upplevelse av AEM-mobilappen kräver att rollerna är enhetliga innan det är klart för innehållsredigering. Följ den här sidan för att komma igång med AEM Mobile On-Demand-tjänster.
uuid: 175c609d-3cb8-4a1b-bfea-278df272e500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: dc6891cd-19cc-4dff-8bda-a41ed8af8bfb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Om du inte använder AEM som innehållshanteringskälla kan du läsa [AEM Mobile On-Demand Services Help](https://helpx.adobe.com/digital-publishing-solution/topics.html).

AEM har flera verktyg som gör att du kan integrera ditt innehåll i mobilprogram.

Följande diagram visar hur de olika komponenterna i AEM Mobile och On-Demand Services passar ihop för att leverera innehåll till mobilappar.

AEM Preflight-appen kan betraktas som en testmiljö för att förhandsgranska appen och innehållet före publiceringen. AEM Mobile App är den slutliga app som har byggts för distribution.

>[!NOTE]
>
>Mer information om preflight-appen finns i [Använda AEM Preflight-appen](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) i hjälpen för AEM Mobile On-Demand Services.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>I diagrammet ovan krävs inte AEM Publish-instansen för ett typiskt distributionsscenario för AEM Mobile On-Demand Services.

## Starta en ny mobilapp {#starting-a-new-mobile-app}

AEM Mobile är bara en av grundarna i den kompletta AEM-plattformen.

Att starta en ny upplevelse av AEM-mobilappen kräver att rollerna är enhetliga innan det är klart för innehållsredigering. Följande roller är en utgångspunkt när du skapar ett nytt AEM Mobile-program:

* **Administratör**
* **Utvecklare**
* **Författare**

>[!NOTE]
>
>Innan du börjar arbeta med AEM Mobile och följer stegen i den här guiden bör du känna till AEM. Lär dig grunderna i AEM [här](/help/sites-deploying/deploy.md).

### Förstå AEM Mobile Application Dashboard {#understanding-the-aem-mobile-application-dashboard}

Innan användaren förstår roller och ansvarsområden bör han/hon ha djupgående kunskaper om **AEM Mobile Control Center** eller **Application Dashboard**. Klicka [här](/help/mobile/mobile-apps-ondemand-application-dashboard.md) om du vill veta mer.

### AEM Administrator {#aem-administrator}

En ***AEM-administratör*** ansvarar för att lägga till ett nytt program i AEM Mobile-katalogen, antingen genom att skapa ett nytt program med hjälp av guiden Skapa eller genom att importera ett befintligt program. AEM-administratörer som skapar en ny app med hjälp av AEM Mobiles *skapandeguide* väljer vanligtvis en av de önskade appmallarna antingen från våra färdiga referensexempel eller (i de flesta fall) en anpassad appmall som skapats av *AEM-utvecklare.*

En AEM-administratör ansvarar för följande uppgifter när en app skapas med AEM Mobile On Demand Services:

* [Konfigurera AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [Konfigurera användar- och användargrupper](/help/mobile/aem-mobile-configure-users.md)
* [Förhandsgranska med Preflight](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [Administrera innehållstjänster](/help/mobile/developing-content-services.md)

Om du vill komma igång med en administratörs roller och ansvarsområden, se [Administrera innehåll för att använda AEM Mobile On-Demand Services](/help/mobile/aem-mobile.md).

## AEM Developer {#aem-developer}

En **AEM-utvecklare** utökar och skapar anpassade webbmallar och komponenter som gör att *AEM Author *kan skapa vackra och engagerande mobilupplevelser. Dessa mallar och komponenter är inte bara optimerade för mobilappsvärlden. men kommunicera både till enheten och till AEM-servern (valfri fjärrserver) till slutpunkterna för flerkanalstjänster. AEM:s inbyggda innehållsredigerare används av *AEM-författare* för att skapa innehållsrika och relevanta upplevelser i appen, inklusive integrering med resten av Adobe Marketing Cloud.

En AEM-utvecklare ansvarar för följande uppgifter när en app skapas med AEM Mobile On Demand Services:

* [Appmallar och komponenter](/help/mobile/app-templates-and-components1.md)
* [Mobil med innehållssynkronisering](/help/mobile/mobile-ondemand-contentsync.md)
* [Innehållsegenskaper och export av innehåll](/help/mobile/on-demand-content-properties-exporting.md)
* [Utveckla AEM Mobile Content Services](//help/mobile/developing-content-services.md)

Om du vill komma igång med Developers roller och ansvar kan du läsa [Utveckla AEM-innehåll för AEM Mobile On-Demand Services](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>En *AEM-utvecklares* roll börjar och slutar inte med att man utvecklar mallar och komponenter. En *AEM-utvecklare* kan skapa ett helt nytt program i stället för att bara utöka det färdiga referensimplementeringsexemplet.

## AEM Author {#aem-author}

En ***AEM-författare *(eller*Marketer *)**använder de anpassade, utvecklade eller färdiga mallarna och komponenterna för att lägga till och redigera sidor, dra och släppa komponenter och lägga till media av alla typer från DAM, inklusive bilder, videor och textfragment (innehållsfragment). AEM:s inbyggda innehållsredigerare används sedan av*AEM Authors *för att skapa innehållsrika och relevanta upplevelser i appen, inklusive integrering med resten av Adobe Marketing Cloud.

En AEM-författare måste förstå följande när de skapar en app med AEM Mobile On Demand Services:

* [AEM Mobile Application Dashboard](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [Skapa och konfigurera program](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [Molnkonfiguration](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [Hantera innehåll](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [Content Services - översikt](/help/mobile/develop-content-as-a-service.md)

Om du vill komma igång med en författares roller och ansvar kan du läsa [Skapa AEM-innehåll för AEM Mobile On-Demand Services-appen](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>En AEM-författare ansvarar också för att ställa in tillstånd, skapa kort och layouter samt skicka push-meddelanden. Mer information om metoder för att skapa innehåll. hantera artiklar och samlingar, skapa banners, kort och layouter i AEM Mobile, se [AEM Mobile On-Demand Portal](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).

