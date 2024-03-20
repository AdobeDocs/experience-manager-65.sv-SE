---
title: Komma åt och leverera innehållsfragment Headless Quick Start Guide
description: Lär dig använda AEM Assets REST API för att hantera innehållsfragment och GraphQL API för headless-leverans av Content Fragment-innehåll.
exl-id: 4664b3a4-4873-4f42-b59d-aadbfaa6072f
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---

# Komma åt och leverera innehållsfragment Headless Quick Start Guide {#accessing-delivering-content-fragments}

Lär dig använda AEM Assets REST API för att hantera innehållsfragment och GraphQL API för headless-leverans av Content Fragment-innehåll.

## Vad är GraphQL och Assets REST API:er? {#what-are-the-apis}

[Nu när du har skapat några innehållsfragment,](create-content-fragment.md) kan du använda AEM-API:er för att leverera dem utan problem.

* [GRAPHQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) Med kan du skapa förfrågningar om åtkomst och leverans av innehållsfragment.
   * Om du vill använda det här [slutpunkter måste definieras och aktiveras i AEM](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint)och, om det behövs, [GraphiQL-gränssnittet är installerat](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#installing-graphiql-interface).
* [Resursens REST API](/help/assets/assets-api-content-fragments.md) I kan du skapa och ändra innehållsfragment (och andra resurser).

Resten av guiden fokuserar på GraphQL åtkomst och leverans av innehållsfragment.

## Leverera ett innehållsfragment med GraphQL {#how-to-deliver-a-content-fragment}

Informationsarkitekterna måste utforma frågor så att deras kanalslutpunkter kan leverera innehåll. Dessa frågor får endast övervägas en gång per slutpunkt och modell. I den här guiden för att komma igång får du bara skapa en.

1. Logga in AEM och få åtkomst till [GraphiQL-gränssnitt](/help/sites-developing/headless/graphql-api/graphiql-ide.md):
   * Till exempel: `http://<host>:<port>/aem/graphiql.html`.

1. GraphiQL är en frågeredigerare i webbläsaren för GraphQL. Du kan använda den för att skapa frågor för att hämta innehållsfragment och leverera dem helhjärtat som JSON.
   * På den vänstra panelen kan du skapa din fråga.
   * Resultatet visas på den högra panelen.
   * Frågeredigeraren har funktioner för kodkomplettering och snabbtangenter för att enkelt köra frågan.
     ![GraphiQL editor](assets/graphiql.png)

1. Anta att modellen du skapade anropades `person` med fält `firstName`, `lastName`och `position`kan du skapa en enkel fråga som hämtar innehållet i innehållsfragmentet.

   ```text
   query 
   {
     personList {
       items {
         _path
         firstName
         lastName
         position
       }
     }
   }
   ```

1. Skriv frågan i den vänstra panelen.
<!--
   ![GraphiQL query](assets/graphiql-query.png)
-->

1. Klicka på **Kör fråga** (högerpil) eller använd `Ctrl-Enter` snabbtangenten och resultatet visas som JSON i den högra panelen.
   ![GraphiQL-resultat](assets/graphiql-results.png)

1. Klicka:
   * **Dokument** längst upp till höger på sidan om du vill visa sammanhangsberoende dokumentation som hjälper dig att skapa frågor som anpassar sig till dina egna modeller.
   * **Historik** i det övre verktygsfältet om du vill visa tidigare frågor.
   * **Spara som** och **Spara** för att spara dina frågor, därefter kan du visa och hämta dem från **Beständiga frågor** panel och **Publicera**.
     ![GraphiQL-dokumentation](assets/graphiql-documentation.png)

GraphQL möjliggör strukturerade frågor som inte bara kan rikta sig till specifika datauppsättningar eller enskilda dataobjekt, utan även kan leverera specifika element i objekten, kapslade resultat, har stöd för frågevariabler och mycket annat.

GraphQL kan undvika iterativa API-begäranden och överleverans. I stället kan man få exakt det som behövs för återgivningen som svar på en enda API-fråga. Den resulterande JSON kan användas för att leverera data till andra webbplatser eller appar.

## Nästa steg {#next-steps}

Så ja! Ni har nu en grundläggande förståelse för innehållshantering utan problem i AEM. Det finns många fler resurser där du kan fördjupa dig för att få en heltäckande bild av de funktioner som finns.

* **[Konfigurationsläsaren](create-configuration.md)** - Mer information om AEM Configuration Browser
* **[Innehållsfragment](/help/assets/content-fragments/content-fragments.md)** - Mer information om hur du skapar och hanterar innehållsfragment
* **[GraphiQL IDE](/help/sites-developing/headless/graphql-api/graphiql-ide.md)** för mer information om hur du använder GraphiQL IDE
* **[Beständiga frågor](/help/sites-developing/headless/graphql-api/persisted-queries.md)** för mer information om beständiga frågor
* **[Stöd för innehållsfragment i AEM Assets HTTP API](/help/assets/assets-api-content-fragments.md)** - Mer information om hur du får åtkomst till AEM direkt via HTTP API, via CRUD-åtgärder (Create, Read, Update, Delete)
* **[GRAPHQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)** - Mer information om hur du levererar innehållsfragment utan problem
