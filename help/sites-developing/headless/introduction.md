---
title: 'Headless Development for AEM 6.5 Sites '
description: Läs om hur AEM 6.5 kraftfulla headless-funktioner som Content Models, Content Fragments och GraphQL API samverkar så att ni kan hantera era upplevelser centralt och leverera dem i alla kanaler.
source-git-commit: 8c7acd06f3909897e5756170c606e00aead098b8
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 1%

---


# Headless Development for AEM 6.5 Sites {#headless-development}

Läs om hur AEM 6.5 kraftfulla headless-funktioner som Content Models, Content Fragments och GraphQL API samverkar så att ni kan hantera era upplevelser centralt och leverera dem i alla kanaler.

## Översikt {#overview}

Headless-implementering blir allt viktigare för att ni ska kunna leverera upplevelser till er målgrupp, oavsett var de finns och kanal.

Den Headless-implementeringen förskjuter hantering av sidor och komponenter på samma sätt som traditionella lösningar med kompletta stackar och hybridlösningar och fokuserar på att skapa kanalneutrala, återanvändbara fragment av innehåll och deras flerkanalsleverans. Det är ett modernt och dynamiskt utvecklingsmönster för implementering av webbupplevelser.

![AEM implementeringsmodeller](assets/aem-implementation-models.png)

## Jämför Headful och Headless {#headful-headless}

Det här dokumentet fokuserar på den fullständiga headless-implementeringsmodellen för AEM. Men headful kontra headless behöver inte vara ett binärt val i AEM. Headless-funktioner kan användas för att hantera och leverera innehåll till olika slutpunkter och samtidigt göra det möjligt för innehållsförfattare att redigera single page-applikationer. Allt i AEM.

<!--
>[!TIP]
>
>See the document [Headful and Headless in AEM](/help/implementing/developing/headful-headless.md) for more information.
-->

## AEM 6.5 och Headless {#aem-headless}

AEM 6.5 är ett flexibelt verktyg för den headless-implementeringsmodellen med tre kraftfulla tjänster:

1. Innehållsmodeller
   * Innehållsmodeller är strukturerade representationer av innehåll.
   * Dessa definieras av informationsarkitekter i AEM Content Fragment Model Editor.
   * Innehållsmodeller fungerar som bas för innehållsfragment.
1. Innehållsfragment
   * Innehållsfragment är instansieringar av innehållsmodeller.
   * Dessa skapas av innehållsförfattare med AEM Content Fragment Editor.
   * De lagras i AEM Assets och hanteras i gränssnittet Resurser Admin.
1. Innehålls-API för leverans
   * AEM GraphQL API har stöd för leverans av innehållsfragment.
   * AEM Assets REST API stöder CRUD-åtgärder för innehållsfragment.
   * Direktleverans av innehåll är också möjligt med [Content Fragment Core Component&#39;s JSON export.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)

## Dina första steg med AEM headless {#first-steps}

Det finns ett antal resurser som du kan använda för att komma igång med AEM headless-funktioner. De är avsedda för olika användningsområden, men ger alla en bra översikt över AEM rubrikfria funktioner.

| Resurs | Beskrivning | Typ | Målgrupp | Beräkna. Time |
|---|---|---|---|---|
| [Komma igång med AEM självstudiekurs utan hörn](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **Om du föredrar en praktisk lösning och är bekant med AEM** går den här självstudiekursen direkt in i att skapa ett enkelt headless-projekt. | Självstudiekurs | Utvecklare | 2 timmar |

<!--
|Resource|Description|Type|Audience|Est. Time|
|---|---|---|---|---|
|[Headless Developer Journey](/help/journey-headless/developer/overview.md)|**For users new to AEM and headless** technologies, start here for a comprehensive introduction to AEM and its headless features from the theory of headless through going live with your first headless project.|Guide|Developers **new to AEM and headless**|1 hour|
|[Headless Getting Started Guide](/help/implementing/developing/headless/getting-started/introduction.md)|**For experienced AEM users** who need a short summary of the key AEM headless features, check out this quick start overview.|Quick Start|Developers, Administrators **with AEM experience**|20 minutes|
|[Getting Started with AEM Headless hands-on tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html)|**If you prefer a hands-on approach and are familiar with AEM**, this tutorial dives directly into creating a simple headless project.|Tutorial|Developers|2 hours|
-->
