---
title: Autentisering för AEM GraphQL-frågor om innehållsfragment
description: Förstå den autentisering som krävs för GraphQL-frågor AEM fjärranslutet för att skydda din headless-innehållsleverans.
feature: Content Fragments,GraphQL API
source-git-commit: 2f647fc640d3809dc684bce397831ab37fb94b07
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Autentisering för AEM GraphQL-frågor om innehållsfragment {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Ett primärt användningsexempel för Adobe Experience Manager GraphQL API för Content Fragment Delivery](/help/assets/content-fragments/graphql-api-content-fragments.md) är att ta emot fjärrfrågor från tredjepartsprogram eller -tjänster. [ Dessa fjärrfrågor kan kräva autentiserad API-åtkomst för att säkra headless-innehållsleverans.

>[!NOTE]
>
>För testning och utveckling kan du även komma åt AEM GraphQL API direkt via gränssnittet [GraphiQL](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface).

För autentisering måste tredjepartstjänsten [hämta en åtkomsttoken](#retrieving-access-token) som sedan kan användas i GraphQL-begäran](#use-access-token-in-graphql-request).[

## Hämtar en åtkomsttoken {#retrieving-access-token}

<!-- 6.5.10.0 - does this page need to be migrated? -->

<!--
See [Generating Access Tokens for Server Side APIs](/help/sites-developing/generating-access-tokens-for-server-side-apis.md) for full details.
-->

## Använda åtkomsttoken i en GraphQL-begäran {#use-access-token-in-graphql-request}

För att en tredjepartstjänst ska kunna ansluta till en AEM måste den ha en *åtkomsttoken*. Tjänsten måste sedan lägga till denna token i rubriken `Authorization` på begäran om POST.

Ett GraphQL Authorization Header:

```xml
Authorization: Bearer <access_token>
```

## Behörighetskrav {#permission-requirements}

Alla förfrågningar som görs med åtkomsttoken kommer faktiskt att göras *av användarkontot som genererade token*.

Det innebär att du måste kontrollera att kontot har de behörigheter som krävs för att köra GraphQL-frågor.

Du kan kontrollera detta med GraphiQL på den lokala instansen.
