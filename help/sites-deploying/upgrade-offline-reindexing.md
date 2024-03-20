---
title: Använda omindexering offline för att minska driftstoppen under en uppgradering
description: Lär dig hur du använder omindexeringsmetoder offline för att minska systemets driftstopp när du utför en AEM uppgradering.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: 85bc041e-0ab1-42de-8bcc-c98a175d7494
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 0%

---

# Använda omindexering offline för att minska driftstoppen under en uppgradering {#offline-reindexing-to-reduce-downtime-during-upgrades}

## Introduktion {#introduction}

En av de största utmaningarna när det gäller att uppgradera Adobe Experience Manager är att det inte tar längre tid att uppgradera när en uppgradering på plats utförs. Innehållsförfattare kan inte komma åt miljön under en uppgradering. Därför är det önskvärt att minimera tiden det tar att genomföra uppgraderingen. För stora databaser, särskilt AEM Assets-projekt, som vanligtvis har stora datalager och stora uppladdningar av resurser per timme, tar omindexering av Oak-index en betydande del av uppgraderingstiden.

I det här avsnittet beskrivs hur du använder Oak-run-verktyget för att indexera om databasen **före** som utför uppgraderingen, vilket minskar tiden för driftavbrott under den faktiska uppgraderingen. Stegen som presenteras kan användas på [Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html) index för version AEM 6.4 och senare.

## Ökning {#overview}

I nya versioner av AEM införs ändringar i Oak-indexdefinitioner när funktionsuppsättningen utökas. Ändringar av Oak-index tvingar omindexering när AEM uppgraderas. Omindexering är dyrt för resursinstallationer eftersom text i resurser (till exempel text i pdf-fil) extraheras och indexeras. Med MongoMK-databaser bevaras data över nätverket vilket ytterligare ökar tiden för omindexering.

Det problem som de flesta kunder står inför under en uppgradering är att tiden för driftstopp minskar. Lösningen är att **hoppa över** omindexeringsaktiviteten under uppgraderingen. Detta kan du uppnå genom att skapa nya index **föregående** när du ska uppgradera och sedan importera dem under uppgraderingen.

## Metod {#approach}

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-process.png)

Tanken är att skapa indexet före uppgraderingen, mot indexdefinitionerna för AEM målversionen med [Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md) verktyg. I bilden ovan visas omindexeringsmetoden offline.

Detta är dessutom ordningen för stegen som beskrivs i metoden:

1. Text från binärfiler extraheras först
2. Målindexdefinitioner skapas
3. Offlineindex skapas
4. Index importeras sedan under uppgraderingsprocessen

### Textextrahering {#text-extraction}

Om du vill aktivera fullständig indexering i AEM extraheras och läggs text från binärfiler som PDF till i indexet. Detta är vanligtvis ett dyrt steg i indexeringsprocessen. Textrahering är ett optimeringssteg som rekommenderas särskilt för omindexering av resursdatabaser när de lagrar ett stort antal binära filer.

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-text-extraction.png)

Text från binärfiler som lagras i systemet kan extraheras med hjälp av ekkörningsverktyget och kodbiblioteket. En klon av produktionssystemen kan tas före uppgraderingen och kan användas för textraheringsprocessen. Den här processen skapar sedan textarkivet genom att gå igenom följande steg:

**1. Bläddra i databasen och samla in information om binärfiler**

I det här steget skapas en CSV-fil som innehåller en tuppel med binärfiler som innehåller en sökväg och ett blob-id.

Kör kommandot nedan från den katalog där du vill skapa indexet. I exemplet nedan används databasens hemkatalog.

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

Plats `nodestore path` är `mongo_ur` eller `crx-quickstart/repository/segmentstore/`

Använd `--fake-ds-path=temp` parameter i stället för `–fds-path` för att snabba upp processen.

**2. Återanvänd det binära textarkivet som finns i det befintliga indexet**

Dumpa indexdata från det befintliga systemet och extrahera textarkivet.

Du kan dumpa befintliga indexdata med följande kommando:

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

Plats `nodestore path` är `mongo_ur` eller `crx-quickstart/repository/segmentstore/`

Använd sedan indexdumpen ovan för att fylla i butiken:

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

Plats `oak-index-name` är namnet på det fullständiga textindexet, till exempel &quot;lucene&quot;.

**3. Kör textextraheringsprocessen med kodbiblioteket för binärfilerna som hoppats ut i ovanstående steg**

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

Plats `datastore path` är sökvägen till det binära datalagret.

Det skapade textarkivet kan uppdateras och återanvändas för omindexering i framtiden.

Mer information om textraheringsprocessen finns i [Körningsdokumentation](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html).

### Omindexering offline {#offline-reindexing}

![offline-reindexing-upgrade-offline-reindexing](assets/offline-reindexing-upgrade-offline-reindexing.png)

Skapa Lucene-indexet offline före uppgraderingen. Om du använder MongoMK bör du köra det direkt på en av MongoMk-noderna, eftersom det undviker nätverkskostnader.

Så här skapar du indexet offline:

**1. Generera indexdefinitioner för Oak Lucene för målversionen AEM**

Dumpa de befintliga indexdefinitionerna. Indexdefinitioner som ändrades genererades med databaskaketet Adobe Granite för AEM och ekkörning.

Så här dumpar du indexdefinitionen från **källa** AEM förekomst, run this command:

>[!NOTE]
>
>Mer information om dumpningsindexdefinitioner finns i [Oak-dokumentation](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data).

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

Plats `datastore path` och `nodestore path` är från **källa** AEM.

Generera sedan indexdefinitioner från **target** AEM version med målversionens Granite-databaspaket.

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
>Processen för att skapa indexdefinitioner ovan stöds endast från `oak-run-1.12.0` från och med version. Målsättningen görs med Granites databaskaket `com.adobe.granite.repository-x.x.xx.jar`.

Ovanstående steg skapar en JSON-fil med namnet `merge-index-definitions_target.json` som är indexdefinitionen.

**2. Skapa en kontrollpunkt i databasen**

Skapa en kontrollpunkt i produktionen **källa** AEM med lång livstid. Detta bör göras innan databasen klonas.

Via JMX-konsolen på `http://serveraddress:serverport/system/console/jmx`, gå till `CheckpointMBean` och skapa en kontrollpunkt med lång livslängd (till exempel 200 dagar). Anropa `CheckpointMBean#createCheckpoint` med `17280000000` som argument för livstid i millisekunder.

När du är klar kopierar du det nya kontrollpunkts-ID:t och validerar livstiden med JMX `CheckpointMBean#listCheckpoints`.

>[!NOTE]
>
>Den här kontrollpunkten tas bort när indexet importeras senare.

Mer information finns i [skapa kontrollpunkter](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint) i dokumentationen för eken.

**Indexera offline för de genererade indexdefinitionerna**

Omindexering av Lucene kan göras offline med ekkörning. Den här processen skapar indexdata på disken under `indexing-result/indexes`. Det gör det **not** skriver till databasen och behöver därför inte stoppa den AEM som körs. Det skapade textarkivet matas in i den här processen:

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

Användning av `--doc-traversal-mode` parametern är användbar med MongoMK-installationer eftersom den förbättrar omindexeringstiden avsevärt genom att mellanlagra databasinnehåll i en lokal platt fil. Det kräver dock ytterligare diskutrymme som är dubbelt så stort som databasens storlek.

Om det finns MongoMK kan den här processen accelereras om det här steget körs i en instans som är närmare MongoDB-instansen. Om den körs på samma dator kan nätverksladdning undvikas.

Ytterligare teknisk information finns i [körningsdokumentation för indexering](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html).

### Importera index {#importing-indexes}

Med AEM 6.4 och senare versioner har AEM den inbyggda möjligheten att importera index från disk i startsekvenser. Mappen `<repository>/indexing-result/indexes` bevakas för att se om det finns indexdata under start. Du kan kopiera det förskapade indexet till ovanstående plats under [uppgraderingsprocess](in-place-upgrade.md#performing-the-upgrade) innan den nya versionen av **target** AEM burk. AEM importerar den till databasen och tar bort motsvarande kontrollpunkt från systemet. Därför undviks helt omindexering.

## Fler tips och felsökning {#troubleshooting}

Här nedan hittar du användbara tips och felsökningsanvisningar.

### Minska påverkan på Live Production System {#reduce-the-impact-on-the-live-production-system}

Vi rekommenderar att du klonar produktionssystemet och skapar offlineindexet med klonen. Detta eliminerar eventuella effekter på produktionssystemet. Kontrollpunkten som krävs för import av index måste dock finnas i produktionssystemet. Därför är det viktigt att du skapar en kontrollpunkt innan du tar klonen.

### Förbered en körning av en Runbook och en testversion {#prepare-a-runbook-and-trial-run}

Vi rekommenderar att du förbereder en [Runbook](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook) och utför några försök innan uppgraderingen körs.

### Dokumentspårningsläge med offlineindexering {#doc-traversal-mode-with-offline-indexing}

Offlineindexering kräver flera genomgångar av hela databasen. Med MongoMK-installationer är databasen åtkomlig via nätverket, vilket påverkar indexeringsprocessens prestanda. Ett alternativ är att köra offlineindexeringsprocessen på själva MongoDB-repliken, vilket eliminerar nätverksbelastningen. Ett annat alternativ är att använda dokumentgenomströmningsläget.

Dokumentövergångens läge kan användas genom att lägga till kommandoradsparametern `—doc-traversal` till kommandot för ekvering för offlineindexering. I det här läget mellanlagras en kopia av hela databasen på den lokala disken som en platt fil och används för att köra indexeringen.
