---
title: e-handel - översikt
seo-title: e-handel - översikt
description: AEM Generic eCommerce är tillgängligt som en del av standardinstallationen och ger dig full funktionalitet i eCommerce-ramverket.
seo-description: AEM Generic eCommerce är tillgängligt som en del av standardinstallationen och ger dig full funktionalitet i eCommerce-ramverket.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: 5d46836a8b7b66daa8f27bc6fad14319ab1f58a7

---


# e-handel - översikt{#ecommerce-overview}

AEM Generic eCommerce är tillgängligt som en del av en standardinstallation och ger dig full funktionalitet i eCommerce-ramverket.

Adobe tillhandahåller två versioner av Commerce Integration Framework:

|  | CIF lokal | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| AEM-versioner som stöds | AEM on-prem eller AMS 6.x | AEM AMS 6.4 och 6.5 |
| Back-end | - AEM, Java <br> - Monolitisk integrering, mappning före bygge (mall)<br> - JCR-databas | - Magento <br>- Java och Javascript <br>- Inga Commerce-data lagras i JCR-databasen |
| Front-end | Återgivna sidor på AEM-serversidan | Blandat sidprogram (hybridåtergivning) |
| Produktkatalog | - Produktimport, redigerare, cachelagring i AEM <br>- Vanliga kataloger med AEM- eller proxysidor | - Ingen produktimport <br>- generiska mallar <br>- on demand-data via anslutning |
| Skalbarhet | - Kan hantera upp till ett fåtal miljoner produkter (beroende på användningsfall) <br> - Cachelagring av Dispatcher | - Ingen volymbegränsning <br>- Cachelagring av Dispatcher eller CDN |
| Standardiserad datamodell | Nej | Ja, Magento GraphQL schema |
| Tillgänglighet | <br> Ja: - SAP Commerce Cloud (tillägget har uppdaterats med stöd för AEM 6.4 och Hybris 5 (standard) och bibehåller kompatibiliteten med Hybris 4 <br>- Salesforce Commerce Cloud (Connector har öppen källkod som stöd för AEM 6.4) | Ja via öppen källkod via GitHub. <br> Magento Commerce (stöder Magento 2.3.2 (standard) och är kompatibel med Magento 2.3.1). |
| När ska användas | Begränsad användning: För scenarier där små, statiska kataloger kan behöva importeras | Rekommenderad lösning i de flesta fall |


## Distribuera andra implementeringar {#deploying-other-implementations}

För AEM och Magento, se [AEM- och Magento-integration](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md) med [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html).

>[!NOTE]
>
>Mer information om koncept och hur du administrerar e-handelsimplementeringar finns i [Administrera e-handel](/help/sites-administering/ecommerce.md).
>
>Mer information om hur du utökar e-handelsfunktionerna finns i [Utveckla e-handel](/help/sites-developing/ecommerce.md).

