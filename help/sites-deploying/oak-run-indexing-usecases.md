---
title: Exempel på indexeringsanvändning för Oak-run.jar
seo-title: Exempel på indexeringsanvändning för Oak-run.jar
description: Lär dig mer om de olika användarexemplen för att utföra indexering med verktyget Oak-run.
seo-description: Lär dig mer om de olika användarexemplen för att utföra indexering med verktyget Oak-run.
uuid: 3c50080d-1e0d-4886-8d37-269f06881eb4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 084075b8-826d-4f27-9342-35f33368f24f
noindex: true
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Exempel på indexeringsanvändning för Oak-run.jar{#oak-run-jar-indexing-use-cases}

Oak-run har stöd för indexering av användningsfall på kommandoraden utan att man behöver samordna körningen av dessa användningsfall via AEM:s JMX-konsol.

De största fördelarna med att använda indexkommandot oak-run.jar för att hantera Oak-index är:

1. Kommandot för index vid körning ger en ny indexeringsverktygslåda för AEM 6.4.
1. Oak-run minskar tiden för omindexering vilket minskar omindexeringstiden för större databaser.
1. Oak-run minskar resursförbrukningen vid omindexering i AEM, vilket ger bättre systemprestanda.
1. Oak-run ger omindexering utan band, stöd för situationer där produktionen måste vara tillgänglig och klarar inte underhåll eller driftavbrott som annars krävs för omindexering.

I avsnitten nedan finns exempelkommandon. Oak-run index-kommandot stöder alla NodeStore- och BlobStore-inställningar. Exemplen nedan handlar om inställningar som har FileDataStore och SegmentNodeStore.

## Användningsfall 1 - Kontroll av indexöverensstämmelse {#usercase1indexconsistencycheck}

Det här är ett användningsexempel som rör skadade index. I vissa fall gick det inte att avgöra vilken av indexen som är skadad. Därför har Adobe tagit fram verktyg som:

1. Utför konsekvenskontroller av index för alla index och tillhandahåller en rapport om vilka index som är giltiga och vilka som inte är giltiga.
1. Verktygen är användbara även om AEM inte är tillgängligt.
1. Den är lätt att använda.

Kontroll av skadade index kan göras via `--index-consistency-check` åtgärden:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

Då skapas en rapport i `indexing-result/index-consistency-check-report.txt`. Nedan finns en exempelrapport:

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

För diagnostisering av vissa av fallen kring frågeprestanda behövde Adobe ofta en befintlig indexdefinition, indexrelaterad statistik från kundinställningarna. Hittills har denna information spridits över flera resurser. För att underlätta felsökningen har Adobe skapat verktyg som

1. Dumpa alla indexdefinitioner som finns i systemet i en enda JSON-fil.

1. Dumpa viktig statistik från befintliga index,

1. Dumpa indexinnehåll för offlineanalys.

1. Kan användas även om AEM inte är tillgängligt

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

Beroende på [scenarierna](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing)måste i vissa fall omindexering göras. Omindexeringen görs för närvarande genom att `reindex` flaggan ställs in `true` i indexdefinitionsnoden via CRXDE eller via användargränssnittet i Indexhanteraren. När flaggan har angetts utförs omindexering asynkront.

Några punkter att tänka på när det gäller omindexering:

* Omindexering är mycket långsammare på `DocumentNodeStore` uppsättningar jämfört med `SegmentNodeStore` uppsättningar där allt innehåll är lokalt.

* I den aktuella designen blockeras den asynkrona indexeraren medan omindexering sker och alla andra asynkrona index blir inaktuella och uppdateras inte under indexeringstiden. På grund av detta kanske användarna inte ser aktuella resultat om systemet används.
* Omindexering innebär att hela databasen gås igenom, vilket kan göra AEM-installationen mycket belastad och därmed påverka slutanvändarens upplevelse.
* För en `DocumentNodeStore` anläggning där omindexering kan ta lång tid, måste indexeringen startas om från början om anslutningen till Mongo-databasen misslyckas under operationen.

* I vissa fall kan omindexering ta lång tid på grund av textrahering. Detta gäller främst för inställningar med många PDF-filer, där den tid som går åt för textrahering kan påverka indexeringstiden.

För att uppnå dessa mål har indexverktygen för ekningskörning stöd för olika omindexeringslägen som kan användas efter behov. Indexkommandot för ekning ger följande fördelar:

* **omindexering** utanför band - omindexering vid ekning kan göras separat från en AEM-konfiguration som körs och minimerar därmed effekten på den AEM-instans som används.

* **omindexering** utanför intervall - Omindexeringen utförs utan att indexeringen påverkas. Detta innebär att den asynkrona indexeraren kan fortsätta att indexera andra index.

* **Förenklad omindexering för DocumentNodeStore-installationer** - För `DocumentNodeStore` installationer kan omindexering göras med ett enda kommando som ser till att omindexering görs på det optimala sättet.

* **Stöder uppdatering av indexdefinitioner och introduktion av nya indexdefinitioner**

### Indexera om - DocumentNodeStore {#reindexdocumentnodestore}

För `DocumentNodeStore` installationer kan omindexering göras via ett enda ekupkommando:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

Detta ger följande fördelar

* Minimal effekt på AEM-instanser som körs. De flesta läsningar kan göras från sekundära servrar, och körning av AEM-cacher påverkas inte negativt på grund av all den genomgång som krävs för omindexering.
* Användare kan även tillhandahålla en JSON-fil med ett nytt eller uppdaterat index via `--index-definitions-file` alternativet.

### Indexera om - SegmentNodeStore {#reindexsegmentnodestore}

För `SegmentNodeStore` installationer kan omindexering göras på något av följande sätt:

#### Online Reindex - SegmentNodeStore {#onlinereindexsegmentnodestore}

Följ det etablerade sättet där omindexering sker via `reindex` inställningsflaggan.

#### Online Reindex - SegmentNodeStore - AEM-instansen körs {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

För `SegmentNodeStore` installationer kan bara en process få åtkomst till segmentfiler i läs- och skrivläge. På grund av detta måste ytterligare manuella åtgärder vidtas för att vissa åtgärder i körning ska kunna utföras.

Detta skulle innebära följande:

1. Stega text
1. Anslut `oak-run` till samma databas som används av AEM i skrivskyddat läge och utför indexering. Ett exempel på hur du kan uppnå detta:

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. Importera slutligen de skapade indexfilerna via `IndexerMBean#importIndex` åtgärden från den sökväg där körningen sparade indexfilerna när ovanstående kommando kördes.

I det här fallet behöver du inte stoppa AEM-servern eller etablera en ny instans. När indexering innebär att hela databasen gås igenom, ökar dock I/O-belastningen i installationen, vilket påverkar körningens prestanda negativt.

#### Online Reindex - SegmentNodeStore - AEM-instansen är avstängd {#onlinereindexsegmentnodestoreaeminstanceisdown}

För `SegmentNodeStore` installationer kan omindexering göras via ett enda ekupkommando. AEM-instansen måste dock stängas av.

Du kan aktivera omindexering med följande kommando:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

Skillnaden mellan det här sättet och det som förklaras ovan är att skapande av kontrollpunkter och indeximport sker automatiskt. Nackdelen är att AEM måste vara nere under processen.

#### Out of Band Reindex - SegmentNodeStore {#outofbandreindexsegmentnodestore}

I det här fallet kan du indexera om en klonad installation för att minimera påverkan på den AEM-instans som körs:

1. Skapa en kontrollpunkt via en JMX-åtgärd. Du kan göra detta genom att gå till [JMX-konsolen](/help/sites-administering/jmx-console.md) och söka efter `CheckpointManager`. Klicka sedan på åtgärden **createCheckpoint(long p1)** med ett högt värde som anger att den upphör att gälla i sekunder (till exempel **2592000**).
1. Kopiera `crx-quickstart` mappen till en ny dator
1. Indexera om via indexkommandot för ekvering

1. Kopiera de genererade indexfilerna till AEM-servern

1. Importera indexfilerna via JMX.

I det här fallet antas det att datalagret är tillgängligt i en annan instans, vilket kanske inte är möjligt om det `FileDataStore` placeras i en molnbaserad lagringslösning som EBS. Detta utesluter scenariot där `FileDataStore` också klonas. Om indexdefinitionen inte utför fulltextindexering behövs ingen åtkomst till `DataStore` .

## Användningsfall 4 - Uppdaterar indexdefinitioner {#usecase4updatingindexdefinitions}

För närvarande kan du skicka indexdefinitionsändringar via [ACS-paketet Kontrollera index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) . Detta gör att indexdefinitionerna kan levereras via innehållspaket som senare kräver omindexering via att `reindex` flaggan ställs in på `true`.

Detta fungerar bra för mindre installationer där omindexering inte tar lång tid. För mycket stora databaser kommer dock omindexering att göras på betydligt längre tid. I sådana fall kan vi nu använda indexverktygen för ekakning.

Funktionen Oak-run har nu stöd för att tillhandahålla indexdefinitioner i JSON-format och att skapa index i out-of-band-läge där inga ändringar görs i en live-instans.

Den process du behöver tänka på för detta ändamål är:

1. En utvecklare uppdaterar indexdefinitionerna på en lokal instans och genererar sedan en JSON-fil för indexdefinitioner via `--index-definitions` alternativet

1. Den uppdaterade JSON-versionen ges sedan till systemadministratören
1. Systemadministratören följer out-of-band-metoden och förbereder indexet för en annan installation
1. När detta är klart importeras de genererade indexfilerna till en AEM-installation som körs.

