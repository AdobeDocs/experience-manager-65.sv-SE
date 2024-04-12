---
title: Headless Content Delivery using Content Fragments with GraphQL
description: Lär dig hur du använder AEM innehållsfragment med GraphQL för leverans av headless-innehåll.
feature: Content Fragments,Headless,GraphQL
role: User,Developer
exl-id: 2debd678-2d73-41f2-b33c-c29d661f6a6b
solution: Experience Manager, Experience Manager Assets
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# Headless Content Delivery using Content Fragments with GraphQL {#headless-content-delivery-using-content-fragments-with-graphQL}

Med Adobe Experience Manager (AEM) kan du använda innehållsfragment tillsammans med det AEM GraphQL-API:t (en anpassad implementering som bygger på GraphQL-standard) för att leverera strukturerat innehåll som ska användas i dina program. Möjligheten att anpassa en enda API-fråga gör att du kan hämta och leverera det specifika innehåll som du vill ha/behöver återge (som svar på en enskild API-fråga).

<!--
>[!NOTE]
>
>See [Headless and AEM](/help/implementing/developing/headless/introduction.md) for an introduction to Headless Development for AEM Sites.
-->

>[!NOTE]
>
>GraphQL används för närvarande i två (separata) scenarier i Adobe Experience Manager (AEM):
>
>* [AEM Commerce använder data från en e-handelsplattform via GraphQL](/help/commerce/cif/integrating/magento.md).
>* [AEM Content Fragments fungerar tillsammans med det AEM GraphQL-API:t (en anpassad implementering som baseras på GraphQL) för att leverera strukturerat innehåll som kan användas i dina program](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md).

## Headless CMS {#headless-cms}

Ett CMS-system (Headless Content Management System) är:

* &quot;*Ett headless innehållshanteringssystem, eller headless CMS, är ett CMS-system (back-end only content management system) som byggs från grunden som ett innehållsarkiv som gör innehållet tillgängligt via ett API för visning på vilken enhet som helst.*

  Se [Wikipedia](https://en.wikipedia.org/wiki/Headless_content_management_system).

När det gäller utveckling av innehållsfragment i AEM innebär detta att:

* Du kan använda Innehållsfragment för att skapa innehåll som inte primärt är avsett att publiceras direkt (1:1) på formaterade sidor.

* Innehållet i dina innehållsfragment kommer att struktureras på ett förutbestämt sätt, enligt modellerna för innehållsfragment. Detta förenklar åtkomsten för dina program, som kommer att bearbeta innehållet ytterligare.

## GraphQL - en översikt {#graphql-overview}

GraphQL är:

* &quot;*...ett frågespråk för API:er och en körningsmiljö för att utföra dessa frågor med dina befintliga data.*&quot;.

  Se [GraphQL.org](https://graphql.org)

The [AEM GRAPHQL API](#aem-graphql-api) gör att du kan utföra (komplexa) frågor på [Innehållsfragment](/help/assets/content-fragments/content-fragments.md); där varje fråga följer en viss modelltyp. Det returnerade innehållet kan sedan användas av dina program.

## AEM GRAPHQL API {#aem-graphql-api}

För Adobe Experience har en anpassad implementering av GraphQL standard-API utvecklats. Se [AEM GraphQL API för användning med innehållsfragment](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) för mer information.

Den AEM API-implementeringen i GraphQL baseras på [GraphQL Java-bibliotek](https://graphql.org/code/#java).

## Innehållsfragment för användning med AEM GraphQL API {#content-fragments-use-with-aem-graphql-api}

[Innehållsfragment](#content-fragments) kan användas som bas för GraphQL AEM frågor som:

* Med dem kan du utforma, skapa, strukturera och publicera sidoberoende innehåll.
* The [Modeller för innehållsfragment](#content-fragments-models) tillhandahålla den struktur som krävs med hjälp av definierade datatyper.
* The [Fragmentreferens](#fragment-references), som är tillgängligt när du definierar en modell, kan användas för att definiera ytterligare lager av strukturen.

![Content Fragments for use with GraphQL](assets/cfm-nested-01.png "Content Fragments for use with GraphQL")

### Innehållsfragment {#content-fragments}

Innehållsfragment:

* Innehåller strukturerat innehåll.

* De är baserade på en [Content Fragment Model](#content-fragments-models), som fördefinierar strukturen för det resulterande fragmentet.

### Modeller för innehållsfragment {#content-fragments-models}

Dessa [Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md):

* Används för att generera [Scheman](https://graphql.org/learn/schema/), en gång **Aktiverad**.

* Ange de datatyper och fält som krävs för GraphQL. De ser till att programmet bara begär det som är möjligt och får det som förväntas.

* Datatypen **[Fragmentreferenser](#fragment-references)** kan användas i din modell för att referera till ett annat innehållsfragment, och därför införs ytterligare strukturnivåer.

### Fragmentreferenser {#fragment-references}

The **[Fragmentreferens](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**:

* Är av särskilt intresse tillsammans med GraphQL.

* Är en specifik datatyp som kan användas när en innehållsfragmentmodell definieras.

* Refererar till ett annat fragment, beroende på en viss innehållsfragmentmodell.

* Gör att du kan hämta strukturerade data.

   * Vid definition som **multifeed**, kan flera delfragment refereras (hämtas) av det primära fragmentet.

### JSON Preview {#json-preview}

Om du vill ha hjälp med att utforma och utveckla dina modeller för innehållsfragment kan du förhandsgranska [JSON-utdata](/help/assets/content-fragments/content-fragments-json-preview.md).

## Lära sig använda GraphQL med AEM - exempelinnehåll och frågor {#learn-graphql-with-aem-sample-content-queries}

Se [Lära sig använda GraphQL med AEM - exempelinnehåll och frågor](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md) om du vill få en introduktion till hur du använder AEM GraphQL API.

## Självstudiekurs - Komma igång med AEM Headless och GraphQL

Söker du en praktisk självstudiekurs? Checka ut [Komma igång med AEM Headless och GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) en komplett självstudiekurs som visar hur man bygger upp och exponerar innehåll med AEM GraphQL API:er och som används av en extern app, i ett headless CMS-scenario.
