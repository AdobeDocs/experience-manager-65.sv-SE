---
title: Exempel på indexeringsanvändning för Oak-run.jar
seo-title: Oak-run.jar Indexing Use Cases
description: Lär dig mer om de olika användarexemplen för att utföra indexering med verktyget Oak-run.
seo-description: Learn about the various user cases for performing indexing with the Oak-run tool.
uuid: 3c50080d-1e0d-4886-8d37-269f06881eb4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 084075b8-826d-4f27-9342-35f33368f24f
noindex: true
exl-id: d25e3070-080a-4594-8fdb-9f09164135fc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 0%

---

# Exempel på indexeringsanvändning för Oak-run.jar{#oak-run-jar-indexing-use-cases}

Oak-run har stöd för indexering av användningsfall på kommandoraden utan att du behöver utföra dessa användningsfall via AEM JMX-konsol.

De största fördelarna med att använda indexkommandot oak-run.jar för att hantera Oak-index är:

1. Kommandot för index som körs på baksidan innehåller en ny indexverktygsuppsättning för AEM 6.4.
1. Oak-run minskar tiden för omindexering vilket minskar omindexeringstiden för större databaser.
1. Oak-run minskar resursförbrukningen vid omindexering av AEM, vilket ger bättre systemprestanda.
1. Oak-run ger omindexering utan band, stöd för situationer där produktionen måste vara tillgänglig och klarar inte underhåll eller driftavbrott som annars krävs för omindexering.

I avsnitten nedan finns exempelkommandon. Oak-run index-kommandot stöder alla NodeStore- och BlobStore-inställningar. Exemplen nedan handlar om inställningar som har FileDataStore och SegmentNodeStore.

## Användningsfall 1 - Kontroll av indexöverensstämmelse {#usercase1indexconsistencycheck}

Det här är ett användningsexempel som rör skadade index. I vissa fall gick det inte att avgöra vilken av indexen som är skadad. Adobe har därför tillhandahållit verktyg som

1. Utför konsekvenskontroller av index för alla index och tillhandahåller en rapport om vilka index som är giltiga och vilka som inte är giltiga.
1. Verktygen är användbara även om AEM inte är åtkomliga.
1. Den är lätt att använda.

Kontroll av skadade index kan göras via `--index-consistency-check` operation:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

Detta genererar en rapport i `indexing-result/index-consistency-check-report.txt`. Nedan finns en exempelrapport:

```
Valid indexes :
        - /content/oak:index/enablementResourceName
        - /oak:index/cqProjectLucene
        - /oak:index/cqTagLucene
        - /oak:index/lucene
        - /oak:index/ntBaseLucene
        - /oak:index/socialLucene
    Invalid indexes :
        - /oak:index/atDamIndex
        - /oak:index/atIndex
        - /oak:index/cqPageLucene
        - /oak:index/damAssetLucene
        - /oak:index/groups
        - /oak:index/slingeventJob
        - /oak:index/users
        - /oak:index/workflowDataLucene
    Ignored indexes as these are not of type lucene:
        - /oak:index/acPrincipalName
        - /oak:index/active
```

### Fördelar {#uc1benefits}

Den här verktygen kan nu användas av supporten och systemadministratören för att snabbt avgöra vilka index som är skadade och sedan indexera om dem.

## Användningsfall 2 - Indexstatistik {#usecase2indexstatistics}

För diagnostisering av vissa fall kring frågeprestanda behövde Adobe ofta en befintlig indexdefinition, indexrelaterad statistik från kundinställningarna. Hittills har denna information spridits över flera resurser. För att underlätta felsökningen har Adobe skapat verktyg som gör att:

1. Dumpa alla indexdefinitioner som finns i systemet i en enda JSON-fil.

1. Dumpa viktig statistik från befintliga index,

1. Dumpa indexinnehåll för offlineanalys.

1. Kan användas även om AEM inte är tillgänglig

Ovanstående åtgärder kan nu utföras med följande kommandon för åtgärdsindex:

* `--index-info` - Samlar in och dumpar diverse statistik som hör till index

* `--index-definitions` - Samlar in och dumpar indexdefinitioner

* `--index-dump` - Dumpar indexinnehåll

Nedan visas ett exempel på hur kommandona fungerar i praktiken:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

Rapporterna genereras i `indexing-result/index-info.txt` och `indexing-result/index-definitions.json`

Dessutom tillhandahålls samma information via webbkonsolen och ingår i konfigurationsdumpens zip. De kan nås på följande plats:

`https://serverhost:serverport/system/console/status-oak-index-defn`

### Fördelar {#uc2benefits}

Med det här verktyget kan du snabbt samla in all information som behövs för indexering eller frågeproblem och minska tiden för extrahering av informationen.

## Användningsfall 3 - omindexering {#usecase3reindexing}

Beroende på [scenarier](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing)I vissa fall måste omindexering göras. Omindexeringen görs för närvarande genom att inställningen `reindex` flagga till `true` i indexdefinitionsnoden via CRXDE eller via användargränssnittet i Indexhanteraren. När flaggan har angetts utförs omindexering asynkront.

Några punkter att tänka på när det gäller omindexering:

* Omindexering går långsammare `DocumentNodeStore` uppsättningar jämfört med `SegmentNodeStore` uppsättningar där allt innehåll är lokalt,

* I den aktuella designen blockeras den asynkrona indexeraren medan omindexering sker och alla andra asynkrona index blir inaktuella och uppdateras inte under indexeringstiden. På grund av detta kanske användarna inte ser aktuella resultat om systemet används.
* Omindexering innebär att hela databasen gås igenom, vilket kan göra AEM mycket belastad och därmed påverka slutanvändarens upplevelse.
* För `DocumentNodeStore` installation där omindexering kan ta lång tid, och om anslutningen till Mongo-databasen misslyckas under operationen, måste indexeringen startas om från början.

* I vissa fall kan omindexering ta lång tid på grund av textrahering. Detta gäller främst för uppsättningar med många PDF-filer, där den tid som går åt för textrahering kan påverka indexeringstiden.

För att uppnå dessa mål har indexverktygen för ekningskörning stöd för olika omindexeringslägen som kan användas efter behov. Indexkommandot för ekning ger följande fördelar:

* **omindexering utanför band** - Omindexering av ekar kan göras separat från en AEM som körs och minimerar därmed påverkan på den AEM instansen som används.

* **omindexering utanför intervall** - Omindexeringen sker utan att indexeringen påverkas. Detta innebär att den asynkrona indexeraren kan fortsätta att indexera andra index.

* **Förenklad omindexering för installationer av DocumentNodeStore** - för `DocumentNodeStore` installationer, omindexering kan göras med ett enda kommando som säkerställer att omindexering görs på bästa möjliga sätt,

* **Stöder uppdatering av indexdefinitioner och introduktion av nya indexdefinitioner**

### Indexera om - DocumentNodeStore {#reindexdocumentnodestore}

För `DocumentNodeStore` omindexering av installationer kan göras med ett enda ekupkommando:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

Detta ger följande fördelar

* Minimal påverkan på pågående AEM. De flesta läsningar kan göras från sekundära servrar och AEM som körs påverkas inte negativt på grund av all den genomgång som krävs för omindexering.
* Användarna kan också tillhandahålla en JSON av ett nytt eller uppdaterat index via `--index-definitions-file` alternativ.

### Indexera om - SegmentNodeStore {#reindexsegmentnodestore}

För `SegmentNodeStore` omindexering av installationer kan göras på något av följande sätt:

#### Online Reindex - SegmentNodeStore {#onlinereindexsegmentnodestore}

Följ det etablerade sättet där omindexering sker via inställning `reindex` flagga.

#### Online Reindex - SegmentNodeStore - Den AEM instansen körs {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

För `SegmentNodeStore` installerar bara en process för åtkomst av segmentfiler i läs- och skrivläge. På grund av detta måste ytterligare manuella åtgärder vidtas för att vissa åtgärder i körning ska kunna utföras.

Detta skulle innebära följande:

1. Stega text
1. Anslut `oak-run` till samma databas som används av AEM i skrivskyddat läge och utför indexering. Ett exempel på hur du kan uppnå detta:

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. Importera slutligen de skapade indexfilerna via `IndexerMBean#importIndex` från den sökväg där körningen sparade indexeringsfilerna efter att ovanstående kommando kördes.

I det här fallet behöver du inte stoppa AEM eller etablera någon ny instans. När indexering innefattar genomgång av hela databasen skulle dock I/O-belastningen på installationen öka, vilket påverkar körningens prestanda negativt.

#### Online Reindex - SegmentNodeStore - Den AEM instansen är avstängd {#onlinereindexsegmentnodestoreaeminstanceisdown}

För `SegmentNodeStore` omindexering av installationer kan göras med ett enda ekupkommando. AEM måste dock stängas av.

Du kan aktivera omindexering med följande kommando:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

Skillnaden mellan det här sättet och det som förklaras ovan är att skapande av kontrollpunkter och indeximport sker automatiskt. Nackdelen är att AEM måste vara nere under processen.

#### Out of Band Reindex - SegmentNodeStore {#outofbandreindexsegmentnodestore}

I det här fallet kan du indexera om en klonad installation för att minimera påverkan på den AEM som körs:

1. Skapa kontrollpunkt med en JMX-åtgärd. Du kan göra detta genom att gå till [JMX Console](/help/sites-administering/jmx-console.md) och söka efter `CheckpointManager`. Klicka sedan på **createCheckpoint(long p1)** operation med ett högt värde för förfallotid i sekunder (till exempel **2592000**).
1. Kopiera `crx-quickstart` mapp till en ny dator
1. Indexera om via indexkommandot för ekvering

1. Kopiera de genererade indexfilerna till AEM server

1. Importera indexfilerna via JMX.

I det här fallet antas det att datalagret är tillgängligt i en annan instans som kanske inte är möjlig om `FileDataStore` placeras i en molnbaserad lagringslösning som EBS. Detta utesluter scenariot där `FileDataStore` är också klonad. Om indexdefinitionen inte utför fulltextindexering får du tillgång till `DataStore` är inte obligatoriskt.

## Användningsfall 4 - Uppdaterar indexdefinitioner {#usecase4updatingindexdefinitions}

För närvarande kan du skicka ändringar av indexdefinitioner via [ACS - säkerställ index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) paket. På så sätt kan indexdefinitioner levereras via innehållspaket som senare kräver omindexering via inställningen `reindex` flagga till `true`.

Detta fungerar bra för mindre installationer där omindexering inte tar lång tid. För mycket stora databaser kommer dock omindexering att göras på betydligt längre tid. I sådana fall kan vi nu använda indexverktygen för ekakning.

Funktionen Oak-run har nu stöd för att tillhandahålla indexdefinitioner i JSON-format och att skapa index i out-of-band-läge där inga ändringar görs i en live-instans.

Den process du behöver tänka på för detta ändamål är:

1. En utvecklare uppdaterar indexdefinitionerna på en lokal instans och genererar sedan en JSON-fil för indexdefinitioner via `--index-definitions` option

1. Den uppdaterade JSON-versionen ges sedan till systemadministratören
1. Systemadministratören följer out-of-band-metoden och förbereder indexet för en annan installation
1. När detta är klart importeras de genererade indexfilerna till en AEM som körs.
