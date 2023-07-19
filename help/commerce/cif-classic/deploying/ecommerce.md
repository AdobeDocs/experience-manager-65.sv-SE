---
title: e-handel - översikt
seo-title: eCommerce Overview
description: AEM generiska e-handelslösningen finns som en del av standardinstallationen och ger dig full funktionalitet i e-handelsramverket.
seo-description: AEM generic eCommerce is available as part of the standard installation and provides you with the full functionality of the eCommerce framework.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# e-handel - översikt{#ecommerce-overview}

AEM allmänna e-handelslösningen är tillgänglig som en del av en standardinstallation och ger dig full funktionalitet i e-handelsramverket.

Adobe tillhandahåller två versioner av Commerce Integration Framework:

|                         | CIF lokal | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| AEM | AEM på plats eller AMS 6.x | AEM AMS 6.4 och 6.5 |
| Back-end | - AEM, Java <br> - Monolitisk integrering, mappning före bygge (mall)<br> - JCR-databas | - Adobe Commerce <br>- Java och JavaScript <br>- Inga handelsdata lagras i JCR-databasen |
| Front-end | AEM återgivna sidor på serversidan | Blandat sidprogram (hybridåtergivning) |
| Produktkatalog | - Produktimport, redigerare, cachelagring i AEM <br>- Vanliga kataloger med AEM- eller proxysidor | - Ingen produktimport <br>- Allmänna mallar <br>- On demand-data via anslutning |
| Skalbarhet | - Kan stödja upp till ett fåtal miljoner produkter (beroende på användningsfall) <br> - Cachelagring av Dispatcher | - Ingen volymbegränsning <br>- Cachelagring på Dispatcher eller CDN |
| Standardiserad datamodell | Nej | Ja, Adobe Commerce GraphQL-schema |
| Tillgänglighet | Ja:<br> - SAP Commerce Cloud (tillägget har uppdaterats för att stödja AEM 6.4 och Hybris 5 (standard) och bibehåller kompatibiliteten med Hybris 4 <br>- Salesforce Commerce Cloud (Connector open-sourced to support AEM 6.4) | Ja via öppen källkod via GitHub. <br> Adobe Commerce (Stöder 2.3.2 (standard) och är kompatibelt med 2.3.1). |
| När ska användas | Begränsad användning: För scenarier där små, statiska kataloger kan behöva importeras | Rekommenderad lösning i de flesta fall |


## Distribuera andra implementeringar {#deploying-other-implementations}

För AEM och Adobe Commerce, se [Integrering med AEM och Adobe Commerce](/help/commerce/cif/integrating/magento.md) med [Commerce Integration Framework](/help/commerce/cif/introduction.md).

>[!NOTE]
>
>Mer information om koncept och administration av e-handelsimplementeringar finns i [Administrera e-handel](/help/commerce/cif-classic/administering/ecommerce.md).
>
>Mer information om hur du utökar e-handelsfunktionerna finns i [Utveckla e-handeln](/help/commerce/cif-classic/developing/ecommerce.md).
