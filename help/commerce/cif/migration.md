---
title: Migrering till tillägget AEM Commerce Integration Framework (CIF)
description: Så här migrerar du till CIF-tillägget (AEM Commerce Integration Framework) från en gammal version
translation-type: tm+mt
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Migreringsguide för tillägget Experience Manager {#cif-migration}

Den här guiden hjälper dig att identifiera de områden du behöver uppdatera för migrering av tilläggsprogram för Experience Manager.

## CIF-tillägg

CIF-tillägg är tillgängligt för AEM 6.5 via [portalen för programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). Den är kompatibel och har samma funktioner som CIF-tillägget för Experience Manager som en Cloud Service.

Se [Komma igång med AEM innehåll och handel](getting-started.md).

För att stödja projekt som distribuerar CIF Adobe ska du tillhandahålla [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components).

## Produktkatalog

Import av produktkatalogdata stöds inte av CIF-tillägget. Med hjälp av CIF-tilläggsobjekt kan produkt- och katalogförfrågningar efterfrågas på begäran via realtidsanrop till en extern handelslösning. Gå till kapitlet Integrating för att lära dig mer om att integrera en e-handelslösning.

>[!TIP]
>
>Om det inte finns några API:er i realtid bör en extern produktcache med API:er användas för integreringen. Exempel [Magento öppen källkod](https://magento.com/products/magento-open-source).

## Produktkatalogupplevelser med AEM rendering

Om du använder katalogutkast med klassisk CIF måste du uppdatera arbetsflödet för produktkatalogen. Tillägget CIF återger nu produktkatalogupplevelser direkt med hjälp AEM katalogmallar. Du behöver inte längre replikera produktdata eller produktsidor.

## Data och shoppinginteraktion som inte är tillgängliga

Klientförfrågningar om icke-cachelagrade data och interaktioner (t.ex. tillägg i kundvagnen, sökning) ska gå direkt till slutpunkten för e-handeln (antingen e-handelslösningen eller integreringslagret) via CDN/Dispatcher. Ta bort alla samtal där AEM bara var en proxy.
