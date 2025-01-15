---
title: Adobe Experience Manager Mobile On-Demand
description: För att starta en ny upplevelse av Adobe Experience Manager (AEM)-mobilappen krävs det att rollerna är enhetliga innan det är klart för innehållsredigering. Följ den här sidan för att komma igång med AEM on-demand-tjänster för mobiler.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
exl-id: 4be199d8-963d-4807-b9bb-e23fa577c5f2
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%

---

# AEM Mobile On-Demand{#aem-mobile-on-demand}

{{ue-over-mobile}}

>[!NOTE]
>
>Om du inte använder Adobe Experience Manager (AEM) som innehållshanteringskälla kan du läsa [AEM Mobile On-demand Services-hjälpen](https://helpx.adobe.com/digital-publishing-solution/topics.html).

AEM innehåller flera verktyg som gör att du kan integrera ditt innehåll i mobilprogram.

Följande diagram visar hur de olika komponenterna i AEM Mobile och On-Demand Services passar ihop för att leverera innehåll till mobilappar.

AEM kan betraktas som en testmiljö för att förhandsgranska appen och innehållet före publicering, medan AEM Mobile App är den sista app som har skapats för distribution.

>[!NOTE]
>
>Mer information om preflight-appen finns i [Använda AEM Preflight-appen](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) i AEM Mobile On-demand Services-hjälpen.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>I diagrammet ovan krävs inte den AEM Publish-instansen för ett typiskt distributionsscenario för AEM Mobile On-demand Services.

## Starta en ny mobilapp {#starting-a-new-mobile-app}

AEM Mobile är bara en av de två pelarna som utgör den kompletta AEM.

För att starta en ny AEM Mobile-appupplevelse krävs det att rollerna är enhetliga innan man kan redigera innehåll. Följande roller utgör en startpunkt när du skapar ett AEM Mobile-program:

* **Administratör**
* **Utvecklare**
* **Författare**

>[!NOTE]
>
>Innan du börjar arbeta med AEM Mobile och följer stegen i den här guiden bör du känna till AEM. Lär dig grunderna i AEM [här](/help/sites-deploying/deploy.md).

### Om AEM Mobile Application Dashboard {#understanding-the-aem-mobile-application-dashboard}

Innan användaren förstår roller och ansvarsområden bör han/hon ha ingående kunskaper om **AEM Mobile Control Center** eller **Application Dashboard**. Klicka [här](/help/mobile/mobile-apps-ondemand-application-dashboard.md) om du vill ha mer information.

### AEM-administratör {#aem-administrator}

En ***AEM-administratör*** ansvarar för att lägga till ett program i AEM Mobile-katalogen, antingen genom att skapa ett program med hjälp av guiden Skapa eller genom att importera ett befintligt program. AEM administratörer som skapar en app med hjälp av AEM Mobile *skapandeguide* väljer vanligtvis en av de önskade appmallarna antingen från Adobe körklara referensexempel eller (vanligtvis) en anpassad appmall som skapats av *AEM utvecklare.*

En AEM är ansvarig för följande när du skapar ett program med AEM Mobile On-demand Services:

* [Konfigurera AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [Konfigurera användar- och användargrupper](/help/mobile/aem-mobile-configure-users.md)
* [Förhandsgranska med Preflight](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [Administrera innehållstjänster](/help/mobile/developing-content-services.md)

Information om hur du kommer igång med en administratörs roller och ansvar finns i [Administrera innehåll för att använda AEM Mobile On-demand Services](/help/mobile/aem-mobile.md).

## AEM Developer {#aem-developer}

En **AEM utvecklare** utökar och skapar anpassade webbmallar och komponenter som gör att *AEM författare *kan skapa tilltalande och engagerande mobilupplevelser. Dessa mallar och komponenter är inte bara optimerade för mobilappsvärlden utan kommunicerar både med enheten och med AEM server (valfri fjärrserver) till slutpunkter för flerkanalstjänster. AEM inbyggda innehållsredigerare används av *AEM Authors* för att skapa innehållsrika och relevanta upplevelser i appen, inklusive integrering med resten av Adobe Experience Cloud.

En AEM utvecklare ansvarar för följande när de skapar ett program med AEM Mobile On-demand Services:

* [Appmallar och komponenter](/help/mobile/app-templates-and-components1.md)
* [Mobil med innehållssynkronisering](/help/mobile/mobile-ondemand-contentsync.md)
* [Innehållsegenskaper och export av innehåll](/help/mobile/on-demand-content-properties-exporting.md)
* [Utveckla AEM Mobile Content Services](/help/mobile/developing-content-services.md)

Om du vill komma igång med Developers roller och ansvar kan du läsa [Utveckla AEM innehåll för AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>En *AEM-utvecklares*-roll börjar och slutar inte med utvecklingen av mallar och komponenter. En *AEM-utvecklare* kan skapa ett helt nytt program i stället för att bara utöka det körklara referensimplementeringsexemplet.

## AEM {#aem-author}

En ***AEM författare* (eller *Marketer*)**använder de anpassade utvecklade mallarna eller komponenterna som är klara för att lägga till och redigera sidor, dra och släppa komponenter och lägga till media av alla typer från DAM, inklusive bilder, videor och textfragment (innehållsfragment). AEM inbyggda innehållsredigeraren används sedan av *AEM Authors* för att skapa innehållsrika och relevanta upplevelser i appen, inklusive integrering med resten av Adobe Experience Cloud.

AEM måste förstå följande när de skapar ett program med AEM Mobile On-demand Services:

* [AEM Mobile Application Dashboard](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [Skapa och konfigurera program](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [Molnkonfiguration](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [Hantera innehåll](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [Content Services - översikt](/help/mobile/develop-content-as-a-service.md)

Om du vill komma igång med en författares roller och ansvarsområden, se [Skapa AEM innehåll för AEM Mobile On-demand Services App](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>En AEM författare ansvarar också för att ställa in tillstånd, skapa kort och layouter samt skicka push-meddelanden. Mer information om metoder för att skapa innehåll, hantera artiklar och samlingar, skapa banners, kort och layouter i AEM Mobile finns i [AEM Mobile On-Demand Portal](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).
