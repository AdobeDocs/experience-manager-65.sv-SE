---
title: Autentisering för Adobe Experience Manager GraphQL-fjärrfrågor om innehållsfragment
description: Förstå den autentisering som krävs för fjärrfrågor till Adobe Experience Manager GraphQL för att säkra din headless-leverans av innehåll.
feature: Content Fragments,GraphQL API
exl-id: 167f3318-7bc7-48fc-aaa9-73da43433f2f
source-git-commit: e068cee192c0837f1473802143e0793674d400e8
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# Autentisering för Adobe Experience Manager GraphQL-fjärrfrågor om innehållsfragment {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Ett primärt användningsexempel för [Adobe Experience Manager (AEM) GraphQL API for Content Fragment Delivery](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) är att acceptera fjärrfrågor från program eller tjänster från tredje part. Dessa fjärrfrågor kan kräva autentiserad API-åtkomst för säker leverans av headless-innehåll.

>[!NOTE]
>
>För testning och utveckling kan du även komma åt AEM GraphQL API direkt via [GraphiQL-gränssnitt](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphiql-interface).

För autentisering måste tredjepartstjänsten autentiseras med hjälp av användarnamnet och lösenordet för AEM.

<!-- 6.5.10.0 - does this content/page need to be migrated? -->

<!--
For authentication the third party service needs to [retrieve an Access Token](#retrieving-access-token), that can then be [used in the GraphQL Request](#use-access-token-in-graphql-request).

## Retrieving an Access Token {#retrieving-access-token}

See [Generating Access Tokens for Server Side APIs](/help/sites-developing/generating-access-tokens-for-server-side-apis.md) for full details.

## Using the Access Token in a GraphQL Request {#use-access-token-in-graphql-request}

For a third party service to connect with an AEM instance it needs to have an *Access Token*. The service must then add this token to the `Authorization` header on the POST request. 

For example, a GraphQL Authorization Header:

```xml
Authorization: Bearer <access_token>
```

## Permission Requirements {#permission-requirements}

All requests made using the access token will actually be made *by the user account that generated the token*. 

This means that you need to check that the account has the permissions required to run GraphQL queries. 

You can check this by using GraphiQL on the local instance.
-->
