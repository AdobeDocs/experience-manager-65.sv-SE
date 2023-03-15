---
title: Indexering via Oak-run Jar
seo-title: Indexing via the Oak-run Jar
description: Lär dig hur du utför indexering via Oak-run Jar.
seo-description: Learn how to perform indexing via the Oak-run Jar.
uuid: 09a83ab9-92ec-4b55-8d24-2302f28fc2e4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: c8a505ab-a075-47da-8007-43645a8c3ce5
exl-id: dcec8c1b-13cc-486c-b1a4-62e6eb3184ad
source-git-commit: c61bf629e35db848c3f2f88c6c7e1dd3b7074b1c
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---

# Indexering via Oak-run Jar {#indexing-via-the-oak-run-jar}

Oak-run har stöd för alla indexeringsanvändningsfall på kommandoraden utan att du behöver använda JMX-nivån. Fördelarna med att använda ekon är:

1. Det är en ny indexverktygslåda för AEM 6.4
1. Det minskar time-to-re-index-värdet, vilket påverkar omindexeringstiderna positivt för större databaser
1. Det minskar resursförbrukningen vid omindexering av AEM vilket ger bättre systemprestanda för andra AEM aktiviteter
1. Oak-run ger out-of-band-stöd: Om produktionsvillkoren inte tillåter omindexering på produktionsinstanser, kan en klonad miljö användas för omindexering för att undvika kritiska prestandapåverkan.

Nedan finns en lista över användningsfall som kan utnyttjas när du utför indexeringsåtgärder via `oak-run` verktyg.

## Konsekvenskontroller för index {#indexconsistencychecks}

>[!NOTE]
>
>Mer detaljerad information om detta scenario finns i [Användningsfall 1 - Kontroll av indexöverensstämmelse](/help/sites-deploying/oak-run-indexing-usecases.md#usercase1indexconsistencycheck).

* `oak-run.jar`Kontrollera snabbt om Lucene-ekindex är skadade.
* Det är säkert att köra på en AEM som används för konsekvenskontrollnivå 1 och 2.

![Konsekvenskontroller för index](assets/screen_shot_2017-12-14at135758.png)

## Indexstatistik {#indexstatistics}

>[!NOTE]
>
>Mer detaljerad information om detta scenario finns i [Användningsfall 2 - Indexstatistik](/help/sites-deploying/oak-run-indexing-usecases.md#usecase2indexstatistics)

* `oak-run.jar` alla indexdefinitioner, viktiga indexvärden och indexinnehåll tas bort för offlineanalys.
* Kan köras på en AEM som används.

![image2017-12-19_9-47-40](assets/image2017-12-19_9-47-40.png)

## Beslutsträd för omindexering av metod {#reindexingapproachdecisiontree}

Bilden är ett beslutsträd för när olika omindexeringsmetoder ska användas.

![oak_-_reindexingwithoak-run](assets/oak_-_reindexingwithoak-run.png)

## Indexerar om MongoMK/RDMBMK {#reindexingmongomk}

>[!NOTE]
>
>Mer detaljerad information om detta scenario finns i [Användningsfall 3 - omindexering](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing).

### Textförextrahering för SegmentNodeStore och DocumentNodeStore {#textpre-extraction}

[Textförextrahering](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-perform-text-pre-extraction) (en funktion som finns i AEM 6.3) kan användas för att minska tiden för indexering. Textförextrahering kan användas tillsammans med alla omindexeringsmetoder.

Beroende på `oak-run.jar` indexeringsmetoden kommer att utföras i olika steg på båda sidor av steget Utför omindexering i diagrammet nedan.

![Textförextrahering för SegmentNodeStore och DocumentNodeStore](assets/4.png)

>[!NOTE]
>
>Orange betecknar aktiviteter där AEM måste finnas i en underhållsperiod.

### Omindexering online för MongoMK eller RDBMK med oak-run.jar {#onlinere-indexingformongomk}

>[!NOTE]
>
>Mer detaljerad information om detta scenario finns i [Indexera om - DocumentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexdocumentnodestore).

Detta är den rekommenderade metoden för omindexering av AEM MongoMK (och RDBMK). Ingen annan metod bör användas.

Den här processen behöver bara köras mot en enda AEM i klustret.

![Omindexering online för MongoMK eller RDBMK med oak-run.jar](assets/5.png)

## Omindexering av tarMK {#re-indexingtarmk}

>[!NOTE]
>
>Mer detaljerad information om detta scenario finns i [Indexera om - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexsegmentnodestore).

* **Väntetiderna i kallt läge (tarMK)**

   * Det finns ingen särskild hänsyn till vänteläge i guld. kan du synkronisera ändringar som vanligt med väntelägesinstanserna.

* **AEM Publish Farms (AE Publish Farms ska alltid vara tarMK)**

   * För publiceringsgrupper måste det göras för alla ELLER, och sedan klona konfigurationen för andra (med alla vanliga prestationer när AEM klonas). sling.id - ska länka till något här)

### Omindexering online för tarMK {#onlinere-indexingfortarmk}

>[!NOTE]
>
>Mer detaljerad information om detta scenario finns i [Online Reindex - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestore).

Detta är den metod som användes innan de nya indexeringsfunktionerna i oak-run.jar introducerades. Du kan göra det genom att ställa in `reindex=true` på Oak-indexet.

Den här metoden kan användas om tids- och prestandaeffekterna som ska indexeras är godtagbara för kunden. Detta gäller ofta små till medelstora AEM installationer.

![Omindexering online för tarMK](assets/6.png)

### Omindexering online av tarMK med oak-run.jar {#onlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Mer detaljerad information om detta scenario finns i [Online Reindex - SegmentNodeStore - Den AEM instansen körs](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoretheaeminstanceisrunning).

Omindexering online av tarMK med funktionen oak-run.jar är snabbare än med [Omindexering online för tarMK](#onlinere-indexingfortarmk) som beskrivs ovan. Den kräver dock även exekvering under en underhållsperiod. med en hänvisning till att fönstret kommer att bli kortare och att fler steg krävs för att utföra omindexeringen.

>[!NOTE]
>
>Orange betecknar verksamhet där AEM måste utföras under en underhållsperiod.

![Omindexering online av tarMK med oak-run.jar](assets/7.png)

### Offline omindexing tarMK med oak-run.jar {#offlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Mer detaljerad information om detta scenario finns i [Online Reindex - SegmentNodeStore - Den AEM instansen är avstängd](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoreaeminstanceisdown).

Omindexering offline av tarMK är den enklaste `oak-run.jar` baserad omindexeringsmetod för tarMK eftersom den kräver en enda `oak-run.jar` -kommentar. AEM måste dock stängas.

>[!NOTE]
>
>Rött anger åtgärder där AEM måste stängas av.

![Offline omindexing tarMK med oak-run.jar](assets/8.png)

### Omindexerings-TarMK utanför band med oak-run.jar  {#out-of-bandre-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Mer detaljerad information om detta scenario finns i [Out of Band Reindex - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#outofbandreindexsegmentnodestore).

Omindexering utan band minimerar effekten av omindexering på AEM som används.

>[!NOTE]
>
>Rött anger åtgärder där AEM kan avslutas.

![Omindexerings-TarMK utanför band med oak-run.jar](assets/9.png)

## Uppdaterar indexeringsdefinitioner {#updatingindexingdefinitions}

>[!NOTE]
>
>Mer information om det här scenariot finns i [Användningsfall 4 - Uppdaterar indexdefinitioner](/help/sites-deploying/oak-run-indexing-usecases.md#usecase4updatingindexdefinitions).

### Skapa och uppdatera indexdefinitioner på tarMK med ACS Kontrollera index {#creatingandupdatingindexdefinitionsontarmkusingacsensureindex}

>[!NOTE]
>
>ACS Kontrollera att Index är ett projekt som stöds av communityn och inte stöds av Adobe Support.

Detta gör att indexdefinitioner kan skickas via innehållspaket, vilket senare resulterar i omindexering genom att flaggan för omindexering anges till `true`. Detta fungerar för mindre uppsättningar där omindexering inte tar lång tid.

Mer information finns i [ACS Kontrollera indexdokumentation](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) för mer information.

### Skapa och uppdatera indexdefinitioner på tarMK med oak-run.jar {#creatingandupdatingindexdefinitionsontarmkusingoak-run-jar}

Om tiden eller prestandaeffekten av omindexering med icke `oak-run.jar` metoderna är för höga, följande `oak-run.jar` baserat tillvägagångssätt kan användas för att importera och indexera om Lucene-indexdefinitioner i en TarmMK-baserad AEM.

![Skapa och uppdatera indexdefinitioner på tarMK med oak-run.jar](assets/10.png)

### Skapa och uppdatera indexdefinitioner på MonogMK med oak-run.jar {#creatingandupdatingindexdefinitionsonmonogmkusingoak-run-jar}

Om tiden eller prestandaeffekten av omindexering med icke `oak-run.jar` metoderna är för höga, följande `oak-run.jar` Den baserade metoden kan användas för att importera och indexera om Lucene-indexdefinitioner i MongoMK-baserade AEM.

![Skapa och uppdatera indexdefinitioner på MonogMK med oak-run.jar](assets/11.png)
