---
title: Headless Development for AEM 6.5 Sites
description: Läs om hur AEM 6.5 kraftfulla headless-funktioner som Content Models, Content Fragments och GraphQL API fungerar tillsammans så att ni kan hantera era upplevelser centralt och leverera dem i alla kanaler.
exl-id: b6598bcf-b2ce-403a-87cf-6895fec8a91b
source-git-commit: ac70fb534a95c9eee6f8340d9b8720a607b9f79f
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---

# Headless Development for AEM 6.5 Sites {#headless-development}

Läs om hur AEM 6.5 kraftfulla headless-funktioner som Content Models, Content Fragments och GraphQL API fungerar tillsammans så att ni kan hantera era upplevelser centralt och leverera dem i alla kanaler.

## Översikt {#overview}

Headless-implementering blir allt viktigare för att ni ska kunna leverera upplevelser till er målgrupp, oavsett var de finns och kanal.

Den Headless-implementeringen förskjuter hantering av sidor och komponenter på samma sätt som traditionella lösningar med kompletta stackar och hybridlösningar och fokuserar på att skapa kanalneutrala, återanvändbara fragment av innehåll och deras flerkanalsleverans. Det är ett modernt och dynamiskt utvecklingsmönster för implementering av webbupplevelser.

![AEM implementeringsmodeller](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

## Jämför Headful och Headless {#headful-headless}

Det här dokumentet fokuserar på den fullständiga headless-implementeringsmodellen för AEM. Men headful kontra headless behöver inte vara ett binärt val i AEM. Headless-funktioner kan användas för att hantera och leverera innehåll till olika slutpunkter och samtidigt göra det möjligt för innehållsförfattare att redigera single page-applikationer. Allt i AEM.

>[!TIP]
>
>Se dokumentet [Headless and Headless in AEM](/help/sites-developing/headful-headless.md) för mer information.

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
   * AEM GraphQL API stöder leverans av innehållsfragment.
   * AEM Assets REST API stöder CRUD-åtgärder för innehållsfragment.
   * Direktleverans av innehåll är också möjligt med [Content Fragment Core Component&#39;s JSON export.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)

## Dina första steg med AEM headless {#first-steps}

Det finns ett antal resurser som du kan använda för att komma igång med AEM headless-funktioner. De är avsedda för olika användningsområden, men ger alla en bra översikt över AEM rubrikfria funktioner.

| Resurs | Beskrivning | Typ | Målgrupp | Beräkna. Tid |
|---|---|---|---|---|
| [Headless Developer Journey](/help/journey-headless/developer/overview.md) | **För användare som inte är AEM och utan headless** börjar du här för att få en omfattande introduktion till AEM och dess headless-funktioner från teorin om headless genom att publicera ditt första headless-projekt. | Användarhandbok | Utvecklare **nya i AEM och utan huvud** | 1 timme |
| [Starthandbok för Headless](/help/sites-developing/headless/getting-started/introduction.md) | **För erfarna AEM** som behöver en kort sammanfattning av de viktigaste AEM rubrikfria funktionerna, se den här snabbstartsöversikten. | Snabbstart | Utvecklare, administratörer **med AEM** | 20 minuter |
| [Komma igång med AEM självstudiekurs utan hörn](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **Om du föredrar en praktisk lösning och är bekant med AEM** går den här självstudiekursen direkt in i att skapa ett enkelt headless-projekt. | Självstudiekurs | Utvecklare | 2 timmar |
