---
title: e-handel - översikt
description: AEM generiska e-handelslösningen finns som en del av standardinstallationen och ger dig full funktionalitet i e-handelsramverket.
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
solution: Experience Manager,Commerce
source-git-commit: 1751bfb32386685e3a159939113b9667b5e17f0e
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# e-handel - översikt{#ecommerce-overview}

AEM allmänna e-handelslösningen är tillgänglig som en del av en standardinstallation och ger dig full funktionalitet i e-handelsramverket.

Adobe tillhandahåller två versioner av Commerce integrationa frameworken:

|                         | CIF på plats | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| AEM som stöds | AEM på plats eller AMS 6.x | AEM AMS 6.4 och 6.5 |
| Back-end | - AEM, Java™ <br> - Monolitisk integrering, mappning före bygge (mall)<br> - JCR-databas | - ADOBE COMMERCE <br>- Java och JavaScript <br>- Inga handelsdata lagras i JCR-databasen |
| Front-end | AEM återgivna sidor på serversidan | Blandat sidprogram (hybridåtergivning) |
| Produktkatalog | - Produktimport, redigerare, cachelagring i AEM <br>- Vanliga kataloger med AEM- eller proxysidor | - Ingen produktimport <br>- Allmänna mallar <br>- On demand-data via anslutning |
| Skalbarhet | - Kan stödja upp till ett fåtal miljoner produkter (beroende på användningsfall) <br> - Cachelagring av Dispatcher | - Ingen volymbegränsning <br>- Cachelagring på Dispatcher eller CDN |
| Standardiserad datamodell | Nej | Ja, Adobe Commerce GraphQL-schema |
| Tillgänglighet | Ja:<br> - SAP Commerce Cloud (tillägget har uppdaterats för att stödja AEM 6.4 och Hybris 5 (standard) och bibehåller kompatibiliteten med Hybris 4 <br>- Salesforce Commerce Cloud (Connector open-sourced to support AEM 6.4) | Ja via öppen källkod via GitHub. <br> Adobe Commerce (Stöder 2.3.2 (standard) och är kompatibelt med 2.3.1). |
| När ska du använda | Begränsad användning: För scenarier där små, importera statiska kataloger efter behov | Rekommenderad lösning i de flesta fall |


## Distribuera andra implementeringar {#deploying-other-implementations}

För AEM och Adobe Commerce, se [Integrering med AEM och Adobe Commerce](/help/commerce/cif/integrating/magento.md) med [Commerce integration framework](/help/commerce/cif/introduction.md).

>[!NOTE]
>
>Mer information om koncept och administration av e-handelsimplementeringar finns i [Administrera e-handel](/help/commerce/cif-classic/administering/ecommerce.md).
>
>Mer information om hur du utökar e-handelsfunktionerna finns i [Utveckla e-handeln](/help/commerce/cif-classic/developing/ecommerce.md).
