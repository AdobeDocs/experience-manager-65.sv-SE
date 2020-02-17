---
title: Indexering via Oak-run Jar
seo-title: Indexering via Oak-run Jar
description: Lär dig hur du utför indexering via Oak-run Jar.
seo-description: Lär dig hur du utför indexering via Oak-run Jar.
uuid: 09a83ab9-92ec-4b55-8d24-2302f28fc2e4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: c8a505ab-a075-47da-8007-43645a8c3ce5
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1

---


# Indexering via Oak-run Jar {#indexing-via-the-oak-run-jar}

Oak-run har stöd för alla indexeringsanvändningsfall på kommandoraden utan att du behöver använda JMX-nivån. Fördelarna med att använda ekon är:

1. Det är en ny indexeringsverktygslåda för AEM 6.4
1. Det minskar time-to-reindex-tiden vilket påverkar omindexeringstiderna positivt för större databaser
1. Det minskar resursförbrukningen vid omindexering i AEM, vilket ger bättre systemprestanda för andra AEM-aktiviteter
1. Oak-run ger out-of-band-stöd: Om produktionsvillkoren inte tillåter omindexering på produktionsinstanser, kan en klonad miljö användas för omindexering för att undvika kritiska prestandapåverkan.

Nedan finns en lista med användningsfall som kan användas när du utför indexeringsåtgärder via `oak-run` verktyget.

## Konsekvenskontroller för index {#indexconsistencychecks}

>[!NOTE]
>
>Mer detaljerad information om detta scenario finns i [Använd fall 1 - Kontroll](/help/sites-deploying/oak-run-indexing-usecases.md#usercase1indexconsistencycheck)av indexkonsekvens.

* `oak-run.jar`avgör snabbt om index för lucene-ekning är skadade.
* Det är säkert att köra på en AEM-instans som används för konsekvenskontrollnivå 1 och 2.

![screen_shot_2017-12-14at135758](assets/screen_shot_2017-12-14at135758.png)

## Indexstatistik {#indexstatistics}

>[!NOTE]
>
>Mer information om detta scenario finns i [Använd fall 2 - Indexstatistik](/help/sites-deploying/oak-run-indexing-usecases.md#usecase2indexstatistics)

* `oak-run.jar` alla indexdefinitioner, viktiga indexvärden och indexinnehåll tas bort för offlineanalys.
* Kan köras på en AEM-instans som används.

![image2017-12-19_9-47-40](assets/image2017-12-19_9-47-40.png)

## Beslutsträd för omindexering av metod {#reindexingapproachdecisiontree}

Bilden är ett beslutsträd för när olika omindexeringsmetoder ska användas.

![oak_-_reindexingwithoak-run](assets/oak_-_reindexingwithoak-run.png)

## Indexerar om MongoMK/RDMBMK {#reindexingmongomk}

>[!NOTE]
>
>Mer detaljerad information om detta scenario finns i [Använd fall 3 - Omindexering](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing).

### Textförextrahering för SegmentNodeStore och DocumentNodeStore {#textpre-extraction}

[Textförextrahering](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-perform-text-pre-extraction) (en funktion som fanns i AEM 6.3) kan användas för att minska tiden det tar att indexera om. Textförextrahering kan användas tillsammans med alla omindexeringsmetoder.

Beroende på hur `oak-run.jar` du indexerar kommer olika steg att utföras på båda sidor av steget Utför omindexering i diagrammet nedan.

![4](assets/4.png)

>[!NOTE]
>
>Orange betecknar aktiviteter där AEM måste finnas i en underhållsperiod.

### Omindexering online för MongoMK eller RDBMK med oak-run.jar {#onlinere-indexingformongomk}

>[!NOTE]
>
>Mer detaljerad information om det här scenariot finns i [Indexera om - DocumentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexdocumentnodestore).

Detta är den rekommenderade metoden för omindexering av AEM-installationer av MongoMK (och RDBMK). Ingen annan metod bör användas.

Den här processen behöver bara köras mot en enda AEM-instans i klustret.

![5](assets/5.png)

## Omindexering av tarMK {#re-indexingtarmk}

>[!NOTE]
>
>Mer detaljerad information om det här scenariot finns i [Reindex - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexsegmentnodestore).

* **Väntetiderna i kallt läge (tarMK)**

   * Det finns ingen särskild hänsyn till vänteläge i guld. kan du synkronisera ändringar som vanligt med väntelägesinstanserna.

* **AEM Publish Farms (AE Publish Farms ska alltid vara tarMK)**

   * För publiceringsgrupper måste det göras för alla ELLER utföra stegen för en enda publicering och sedan klona konfigurationen för andra (med alla vanliga prestationer när AEM-instanser klonas). sling.id - ska länka till något här)

### Omindexering online för tarMK {#onlinere-indexingfortarmk}

>[!NOTE]
>
>Mer detaljerad information om det här scenariot finns i [Online Reindex - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestore).

Detta är den metod som användes innan de nya indexeringsfunktionerna i oak-run.jar introducerades. Det kan du göra genom att ställa in egenskapen `reindex=true` på ekindexet.

Den här metoden kan användas om tids- och prestandaeffekterna som ska indexeras är godtagbara för kunden. Detta gäller ofta för små till medelstora AEM-installationer.

![6](assets/6.png)

### Omindexering online av tarMK med oak-run.jar {#onlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Mer detaljerad information om det här scenariot finns i [Online Reindex - SegmentNodeStore - AEM-instansen körs](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoretheaeminstanceisrunning).

Omindexering online av tarMK är snabbare än omindexeringen av TarkMK online som beskrivs ovan. Det kräver dock även körning under ett underhållsfönster, med metoden att fönstret blir kortare och fler steg krävs för att utföra omindexeringen.

>[!NOTE]
>
>Orange betecknar åtgärder där AEM måste utföras under en underhållsperiod.

![7](assets/7.png)

### Offline omindexing tarMK med oak-run.jar {#offlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Mer detaljerad information om det här scenariot finns i [Online Reindex - SegmentNodeStore - AEM-instansen är avstängd](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoreaeminstanceisdown).

Omindexering offline av tarMK är den enklaste `oak-run.jar` baserade omindexeringsmetoden för tarMK eftersom den kräver en enda `oak-run.jar` kommentar. AEM-instansen måste dock stängas av.

>[!NOTE]
>
>Rött anger åtgärder där AEM måste stängas av.

![8](assets/8.png)

### Omindexerings-TarMK utanför band med oak-run.jar {#out-of-bandre-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Mer detaljerad information om det här scenariot finns i [Omindexering utanför intervall - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#outofbandreindexsegmentnodestore).

Omindexering utan band minimerar effekten av omindexering på AEM-instanser som används.

>[!NOTE]
>
>Rött betecknar åtgärder där AEM kan vara avstängt.

![9](assets/9.png)

## Uppdaterar indexeringsdefinitioner {#updatingindexingdefinitions}

>[!NOTE]
>
>Mer information om detta scenario finns i [Använd fall 4 - Uppdatera indexdefinitioner](/help/sites-deploying/oak-run-indexing-usecases.md#usecase4updatingindexdefinitions).

### Skapa och uppdatera indexdefinitioner på tarMK med ACS Kontrollera index {#creatingandupdatingindexdefinitionsontarmkusingacsensureindex}

>[!NOTE]
>
>ACS Kontrollera att Index är ett projekt som stöds av communityn och inte stöds av Adobe Support.

Detta gör att indexdefinitioner för leverans kan definieras via innehållspaket, vilket senare resulterar i omindexering genom att flaggan reindex anges till `true`. Detta fungerar för mindre uppsättningar där omindexering inte tar lång tid.

Mer information finns i dokumentationen [till att kontrollera](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) ACS-index.

### Skapa och uppdatera indexdefinitioner på tarMK med oak-run.jar {#creatingandupdatingindexdefinitionsontarmkusingoak-run-jar}

Om tiden eller prestandaeffekten av omindexering med icke- `oak-run.jar` metoder är för hög kan följande `oak-run.jar` baserade metod användas för att importera och indexera om Lucene-indexdefinitioner i en TarmMK-baserad AEM-installation.

![10](assets/10.png)

### Skapa och uppdatera indexdefinitioner på MonogMK med oak-run.jar {#creatingandupdatingindexdefinitionsonmonogmkusingoak-run-jar}

Om tiden eller prestandaeffekten av omindexering med icke- `oak-run.jar` metoder är för hög kan följande `oak-run.jar` baserade metod användas för att importera och indexera om Lucene-indexdefinitioner i MongoMK-baserade AEM-installationer.

![11](assets/11.png)

