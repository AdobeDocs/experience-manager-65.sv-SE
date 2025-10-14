---
title: Komma åt och leverera innehållsfragment Headless Quick Start Guide
description: Lär dig hur du använder AEM Assets REST API för att hantera innehållsfragment och GraphQL API för headless-leverans av Content Fragment-innehåll.
exl-id: 4664b3a4-4873-4f42-b59d-aadbfaa6072f
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Architect,Data Architect,Developer
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# Komma åt och leverera innehållsfragment Headless Quick Start Guide {#accessing-delivering-content-fragments}

Lär dig hur du använder AEM Assets REST API för att hantera innehållsfragment och GraphQL API för headless-leverans av Content Fragment-innehåll.

## Vad är GraphQL och Assets REST API:er? {#what-are-the-apis}

[Nu när du har skapat några innehållsfragment &#x200B;](create-content-fragment.md) kan du använda AEM API:er för att leverera dem utan problem.

* [Med GraphQL-API:t](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) kan du skapa begäranden om åtkomst till och leverans av innehållsfragment.
   * Om du vill använda detta måste [slutpunkter definieras och aktiveras i AEM](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint), och om det behövs måste [GraphiQL-gränssnittet vara installerat](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#installing-graphiql-interface).
* [Med Assets REST API](/help/assets/assets-api-content-fragments.md) kan du skapa och ändra innehållsfragment (och andra resurser).

Resten av guiden fokuserar på GraphQL åtkomst och leverans av innehållsfragment.

## Leverera ett innehållsfragment med GraphQL {#how-to-deliver-a-content-fragment}

Informationsarkitekterna måste utforma frågor så att deras kanalslutpunkter kan leverera innehåll. Ta endast hänsyn till dessa frågor en gång per slutpunkt, per modell. Skapa bara en startguide för den här guiden.

1. Logga in AEM och öppna [GraphiQL-gränssnittet](/help/sites-developing/headless/graphql-api/graphiql-ide.md):
   * Till exempel: `http://<host>:<port>/aem/graphiql.html`.

1. GraphiQL är en frågeredigerare i webbläsaren för GraphQL. Du kan använda den för att skapa frågor för att hämta innehållsfragment och leverera dem helhjärtat som JSON.
   * På den vänstra panelen kan du skapa din fråga.
   * Resultatet visas på den högra panelen.
   * Frågeredigeraren har funktioner för kodkomplettering och snabbtangenter för att enkelt köra frågan.

     ![GraphiQL-redigerare](assets/graphiql.png)

1. Om du utgår ifrån att den modell du skapade anropades med fälten `firstName`, `lastName` och `position` kan du skapa en enkel fråga för att hämta innehållet i innehållsfragmentet.`person`

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

1. Klicka på ikonen **Kör fråga** (högerpil) eller använd snabbtangenten `Ctrl-Enter` så visas resultatet som JSON i den högra panelen.
   ![GraphiQL-resultat](assets/graphiql-results.png)

1. Klicka:
   * **Dokument** längst upp till höger på sidan om du vill visa sammanhangsberoende dokumentation som hjälper dig att skapa frågor som anpassar sig efter dina egna modeller.
   * **Historik** i det övre verktygsfältet om du vill visa tidigare frågor.
   * **Spara som** och **Spara** om du vill spara dina frågor. Därefter kan du visa och hämta dem från panelen **Beständiga frågor** och **Publish**.

     ![GraphiQL-dokumentation](assets/graphiql-documentation.png)

GraphQL möjliggör strukturerade frågor som inte bara kan rikta sig till specifika datauppsättningar eller enskilda dataobjekt, utan även kan leverera specifika element i objekten, kapslade resultat, har stöd för frågevariabler och mycket annat.

GraphQL kan undvika iterativa API-begäranden och överleverans. I stället kan man få exakt det som behövs för återgivningen som svar på en enda API-fråga. Den resulterande JSON kan användas för att leverera data till andra webbplatser eller appar.

## Nästa steg {#next-steps}

Så ja! Ni har nu en grundläggande förståelse för innehållshantering utan problem i AEM. Det finns många fler resurser där du kan fördjupa dig för att få en heltäckande bild av de funktioner som finns.

* **[Konfigurationsläsaren](create-configuration.md)** - Mer information om AEM konfigurationsläsare
* **[Innehållsfragment](/help/assets/content-fragments/content-fragments.md)** - Mer information om hur du skapar och hanterar innehållsfragment
* **[GraphiQL IDE](/help/sites-developing/headless/graphql-api/graphiql-ide.md)** om du vill ha mer information om hur du använder GraphiQL IDE
* **[Beständiga frågor](/help/sites-developing/headless/graphql-api/persisted-queries.md)** för mer information om beständiga frågor
* **[Stöd för innehållsfragment i AEM Assets HTTP API](/help/assets/assets-api-content-fragments.md)** - Mer information om hur du får åtkomst till AEM direkt via HTTP API, via CRUD-åtgärder (Create, Read, Update, Delete)
* **[GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)** - Mer information om hur du skickar innehållsfragment utan problem
