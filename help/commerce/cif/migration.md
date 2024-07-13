---
title: Migrering till AEM Commerce integration framework (CIF)
description: Så här migrerar du till tillägget AEM Commerce integration framework (CIF) från en gammal version.
exl-id: c6c0c2fc-6cfa-4c64-b3d8-7e428b2a4b2e
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Migreringshandbok för tillägget Experience Manager {#cif-migration}

Den här guiden hjälper dig att identifiera de områden du behöver uppdatera för migrering av tilläggsprogram för Experience Manager.

## CIF

CIF är tillgängligt för AEM 6.5 via [Programdistributionsportalen](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). Den är kompatibel och innehåller samma funktioner som CIF för Experience Manager as a Cloud Service.

Se [Komma igång med AEM och Commerce](getting-started.md).

För att ge stöd åt projekt som distribuerar CIF tillhandahåller Adobe [AEM CIF kärnkomponenter](https://github.com/adobe/aem-core-cif-components).

## Produktkatalog

Import av produktkatalogdata stöds inte av CIF. Med hjälp av CIF tilläggsobjekt kan produkt- och katalogförfrågningar efterfrågas vid behov via realtidsanrop till en extern e-handelslösning. Gå till kapitlet Integrating för att lära dig mer om att integrera en e-handelslösning.

>[!TIP]
>
>Om det inte finns några API:er i realtid bör en extern produktcache med API:er användas för integreringen. Exempel: [Magento öppen källkod](https://business.adobe.com/products/magento/open-source.html).

## Produktkatalogupplevelser med AEM rendering

Om du använder katalogutkast med klassiska CIF måste du uppdatera produktkatalogarbetsflödet. Tillägget CIF renderar nu produktkataloger direkt med hjälp AEM katalogmallar. Du behöver inte längre replikera produktdata eller produktsidor.

## Icke-cacheable Data and Shopping Interaction

Begäranden på klientsidan om icke-cachelagrade data och interaktioner (t.ex. tillägg i kundvagnen, sökning) ska gå direkt till slutpunkten för e-handeln (antingen e-handelslösningen eller integreringslagret) via CDN/Dispatcher. Ta bort alla samtal där AEM bara var en proxy.
