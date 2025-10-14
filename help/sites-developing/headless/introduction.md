---
title: Headless Development for AEM 6.5 Sites
description: Läs om hur AEM 6.5 kraftfulla headless-funktioner som Content Models, Content Fragments och GraphQL API fungerar tillsammans så att ni kan hantera era upplevelser centralt och leverera dem i alla kanaler.
exl-id: b6598bcf-b2ce-403a-87cf-6895fec8a91b
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Architect,Data Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Headless Development for AEM 6.5 Sites {#headless-development}

Läs om hur AEM 6.5 kraftfulla headless-funktioner som Content Models, Content Fragments och GraphQL API fungerar tillsammans så att ni kan hantera era upplevelser centralt och leverera dem i alla kanaler.

## Ökning {#overview}

Headless-implementering blir allt viktigare för att ni ska kunna leverera upplevelser till er målgrupp, oavsett var de finns och kanal.

Den Headless-implementeringen förskjuter hantering av sidor och komponenter på samma sätt som traditionella lösningar med kompletta stackar och hybridlösningar och fokuserar på att skapa kanalneutrala, återanvändbara fragment av innehåll och deras flerkanalsleverans. Det är ett modernt och dynamiskt utvecklingsmönster för implementering av webbupplevelser.

![AEM implementeringsmodeller](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

## Jämför Headful och Headless {#headful-headless}

Det här dokumentet fokuserar på den fullständiga headless-implementeringsmodellen för AEM. Däremot behöver headful kontra headless inte vara ett binärt val i AEM. Headless-funktioner kan användas för att hantera och leverera innehåll till olika slutpunkter och samtidigt göra det möjligt för innehållsförfattare att redigera single page-applikationer. Allt i AEM.

>[!TIP]
>
>Mer information finns i dokumentet [Headful and Headless in AEM](/help/sites-developing/headful-headless.md).

## AEM 6.5 och Headless {#aem-headless}

AEM 6.5 är ett flexibelt verktyg för den headless-implementeringsmodellen med tre kraftfulla tjänster:

1. Innehållsmodeller
   * Innehållsmodeller är strukturerade representationer av innehåll.
   * Dessa definieras av informationsarkitekter i AEM Content Fragment Model Editor.
   * Innehållsmodeller fungerar som bas för innehållsfragment.
1. Innehållsfragment
   * Innehållsfragment är instansieringar av innehållsmodeller.
   * Dessa skapas av innehållsförfattare med AEM Content Fragment Editor.
   * De lagras i AEM Assets och hanteras i användargränssnittet för Assets Admin.
1. Innehålls-API för leverans
   * AEM GraphQL API stöder leverans av innehållsfragment.
   * AEM Assets REST API stöder CRUD-åtgärder för innehållsfragment.
   * Direktinnehållsleverans är också möjligt med [Content Fragment Core Component&#39;s JSON export.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=sv-SE)

## Dina första steg med AEM headless {#first-steps}

Det finns flera resurser som du kan använda för att komma igång med AEM headless-funktioner. De är avsedda för olika användningsområden, men ger alla en bra översikt över AEM rubrikfria funktioner.

| Resurs | Beskrivning | Typ | Målgrupp | Beräkna. Tid |
|---|---|---|---|---|
| [Headless Developer Journey](/help/journey-headless/developer/overview.md) | **För användare som inte har AEM eller använder headless** kan du börja här för att få en omfattande introduktion till AEM och dess headless-funktioner, från teorin om headless till att börja med ditt första headless-projekt. | Guide | Utvecklare **nya för AEM och utan huvud** | 1 timme |
| [Starthandbok för Headless](/help/sites-developing/headless/getting-started/introduction.md) | **För erfarna AEM**-användare som behöver en kort sammanfattning av AEM headless-funktioner kan du ta en titt på den här snabbstartsöversikten. | Snabbstart | Utvecklare, administratörer **med AEM** | 20 minuter |
| [Komma igång med självstudiekurs AEM Headless Handless &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=sv-SE) | **Om du föredrar en praktisk metod och är bekant med AEM**, kommer den här självstudiekursen att dyka direkt i ett enkelt headless-projekt. | Självstudiekurs | Utvecklare | 2 timmar |
| [AEM Developer Portal](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=sv-SE) | Den här resurssamlingen tillhandahålls för både **nya**- och **erfarna**-utvecklare. | Resurser | Utvecklare | |
