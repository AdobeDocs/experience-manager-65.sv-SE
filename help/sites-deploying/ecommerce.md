---
title: e-handel - översikt
seo-title: e-handel - översikt
description: AEM generiska e-handelslösningen finns som en del av standardinstallationen och ger dig full funktionalitet i e-handelsramverket.
seo-description: AEM generiska e-handelslösningen finns som en del av standardinstallationen och ger dig full funktionalitet i e-handelsramverket.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
docset: aem65
feature: Commerce Integration Framework
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---


# eCommerce Overview{#ecommerce-overview}

AEM allmänna e-handelslösningen är tillgänglig som en del av en standardinstallation och ger dig full funktionalitet i e-handelsramverket.

Adobe tillhandahåller två versioner av Commerce Integration Framework:

|  | CIF lokal | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| AEM | AEM på plats eller AMS 6.x | AEM AMS 6.4 och 6.5 |
| Back-end | - AEM, Java <br> - Monolitisk integration, mappning före bygge (mall)<br> - JCR-databas | - Magento <br>- Java och Javascript <br>- Inga handelsdata har lagrats i JCR-databasen |
| Front-end | AEM återgivna sidor på serversidan | Blandat sidprogram (hybridåtergivning) |
| Produktkatalog | - Produktimport, redigerare, cachelagring i AEM <br>- Vanliga kataloger med AEM- eller proxysidor | - Ingen produktimport <br>- generiska mallar <br>- on demand-data via anslutning |
| Skalbarhet | - Kan hantera upp till ett fåtal miljoner produkter (beroende på användningsfall) <br> - Cachelagring på Dispatcher | - Ingen volymbegränsning <br>- Cachelagring av Dispatcher eller CDN |
| Standardiserad datamodell | Nej | Ja, Magento GraphQL-schema |
| Tillgänglighet | Ja:<br> - SAP Commerce Cloud (tillägget har uppdaterats till stöd för AEM 6.4 och Hybris 5 (standard) och bibehåller kompatibiliteten med Hybris 4 <br>- Salesforce Commerce Cloud (anslutningen har öppen källkod som stöd AEM 6.4) | Ja via öppen källkod via GitHub. <br> Magento Commerce (Stöder Magento 2.3.2 (standard) och är kompatibelt med Magento 2.3.1). |
| När ska användas | Begränsad användning: För scenarier där små, statiska kataloger kan behöva importeras | Rekommenderad lösning i de flesta fall |


## Distribuerar andra implementeringar {#deploying-other-implementations}

För AEM och Magento, se [Integrering av AEM och Magento](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md) med [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html).

>[!NOTE]
>
>Mer information om koncept och administration av e-handelsimplementeringar finns i [Administrera e-handel](/help/sites-administering/ecommerce.md).
>
>Mer information om hur du utökar e-handelsfunktionerna finns i [Utveckla e-handel](/help/sites-developing/ecommerce.md).

