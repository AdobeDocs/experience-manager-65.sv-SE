---
title: AEM och Adobe Commerce Integration med Commerce integration framework
description: AEM och Adobe Commerce är helintegrerade med Commerce integrationa frameworken (CIF). Med CIF kan AEM få åtkomst till en Adobe Commerce-instans och kommunicera med Adobe Commerce via GraphQL. AEM kan också använda produkt- och kategoriväljare och produktkonsolen för att bläddra bland produkt- och kategoridata som hämtas on demand från Adobe Commerce. Dessutom har CIF en färdig butik som kan snabba upp affärsprojekt.
thumbnail: aem-magento-architecture.jpg
exl-id: f843784c-5ff7-41d1-97c5-13facb8459b2
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# Integrering med AEM och Adobe Commerce (Magento) med Commerce integration framework {#aem-commerce-framework}

Experience Manager och Adobe Commerce är helintegrerade med Commerce integrationa frameworken (CIF). CIF gör att AEM kan komma åt och kommunicera direkt med e-handelsinstansen med Adobe Commerce [GraphQL API:er](https://devdocs.magento.com/guides/v2.4/graphql/).

>[!NOTE]
>
>Den lägsta GraphQL API-version som stöds är 2.3.5. Vissa funktioner stöds endast i nyare versioner eller bara i Adobe Commerce.

## Arkitektur - översikt {#overview}

Den övergripande arkitekturen är följande:

![CIF Översikt över arkitekturen](../assets/AEM_Magento_Architecture.png)

Inom CIF finns stöd för kommunikationsmönster på serversidan och klientsidan.
API-anrop på serversidan implementeras med hjälp av den generiska [GraphQL-klienten](https://github.com/adobe/commerce-cif-graphql-client) i kombination med en [uppsättning genererade datamodeller](https://github.com/adobe/commerce-cif-magento-graphql) för Commerce GraphQL-schemat. Dessutom kan valfri GraphQL-fråga eller mutation i GQL-format användas.

För klientkomponenterna, som byggs med [React](https://reactjs.org/), används [Apollo-klienten](https://www.apollographql.com/docs/react/).

## AEM CIF Core Component Architecture {#cif-core-components}

![AEM CIF Core Component Architecture](../assets/cif-component-architecture.jpg)

[AEM CIF kärnkomponenter](https://github.com/adobe/aem-core-cif-components) följer mycket liknande designmönster och metodtips som [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components).

Affärslogik och serverdelskommunikation med Adobe Commerce för de AEM kärnkomponenterna implementeras i Sling Models. Om det är nödvändigt att anpassa den här logiken för att uppfylla projektspecifika krav kan delegeringsmönstret för segmenteringsmodeller användas.

>[!TIP]
>
>Sidan [Anpassa AEM &#x200B;](../customizing/customize-cif-components.md) CIF kärnkomponenter innehåller ett detaljerat exempel och bästa praxis för hur du anpassar CIF kärnkomponenter.

I projekt kan AEM kärnkomponenter och anpassade projektkomponenter enkelt hämta den konfigurerade klienten för en Adobe Commerce-butik som är kopplad till en AEM sida via Sling Context-Aware-konfiguration.
