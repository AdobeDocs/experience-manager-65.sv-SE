---
title: Migrering till tillägget AEM Commerce Integration Framework (CIF)
description: Så här migrerar du till CIF-tillägget (AEM Commerce Integration Framework) från en gammal version
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# Migreringshandbok för tillägget Experience Manager {#cif-migration}

Den här guiden hjälper dig att identifiera de områden du behöver uppdatera för migrering av tilläggsprogram för Experience Manager.

## CIF-tillägg

CIF-tillägg är tillgängligt för AEM 6.5 via [portalen för programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). Den är kompatibel och har samma funktioner som CIF-tillägget för Experience Manager som en Cloud Service.

Se [Komma igång med AEM innehåll och handel](getting-started.md).

För att stödja projekt som distribuerar CIF tillhandahåller Adobe [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components).

## Produktkatalog

Import av produktkatalogdata stöds inte av CIF-tillägget. Med hjälp av CIF-tilläggsobjekt kan produkt- och katalogförfrågningar efterfrågas på begäran via realtidsanrop till en extern handelslösning. Gå till kapitlet Integrating för att lära dig mer om att integrera en e-handelslösning.

>[!TIP]
>
>Om det inte finns några API:er i realtid bör en extern produktcache med API:er användas för integreringen. Exempel [Magento öppen källkod](https://magento.com/products/magento-open-source).

## Produktkatalogupplevelser med AEM rendering

Om du använder katalogutkast med klassisk CIF måste du uppdatera arbetsflödet för produktkatalogen. Tillägget CIF återger nu produktkatalogupplevelser direkt med hjälp AEM katalogmallar. Du behöver inte längre replikera produktdata eller produktsidor.

## Icke-cacheable Data and Shopping Interaction

Begäranden på klientsidan om icke-cachelagrade data och interaktioner (t.ex. tillägg till kundvagnen, sökning) ska gå direkt till slutpunkten för e-handeln (antingen e-handelslösningen eller integreringslagret) via CDN/Dispatcher. Ta bort alla samtal där AEM bara var en proxy.
