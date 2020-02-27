---
title: AEM med MongoDB
seo-title: AEM med MongoDB
description: Lär dig mer om de uppgifter och överväganden som krävs för en lyckad AEM med MongoDB-distribution.
seo-description: Lär dig mer om de uppgifter och överväganden som krävs för en lyckad AEM med MongoDB-distribution.
uuid: 8028832d-10de-4811-a769-fab699c162ec
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cd3b979f-53d4-4274-b4eb-a9533329192a
docset: aem65
translation-type: tm+mt
source-git-commit: 56006a1f49e4d357cd7ee44a4a1dd1af7189e70a

---


# AEM med MongoDB{#aem-with-mongodb}

Den här artikeln syftar till att förbättra kunskapen om de uppgifter och överväganden som krävs för att distribuera Adobe Experience Manager med MongoDB.

Mer distributionsrelaterad information finns i avsnittet [Distribuera och underhålla](/help/sites-deploying/deploy.md) i dokumentationen.

## När MongoDB ska användas med AEM {#when-to-use-mongodb-with-aem}

MongoDB används vanligtvis för att stödja AEM-utvecklardistributioner där något av följande villkor uppfylls:

* Mer än 1000 unika användare per dag.
* Mer än 100 samtidiga användare.
* stora volymer sidredigeringar,
* Stora rollouter eller aktiveringar.

Kriterierna ovan gäller bara för författarinstanserna och inte för några publiceringsinstanser som ska vara TjärMK-baserade. Antalet användare refererar till autentiserade användare, eftersom författarinstanser inte tillåter oautentiserad åtkomst.

Om villkoren inte uppfylls rekommenderar vi en aktiverings-/standby-distribution för att åtgärda tillgängligheten. Vanligtvis bör MongoDB övervägas i situationer där skalningskraven är mer än vad som kan uppnås med en enda maskinvaruartikel.

>[!NOTE]
>
>Mer information om storleken på författarinstanser och definitionen av samtidiga användare finns i riktlinjerna [för](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel)maskinvarans storlek.

### Minimal MongoDB-distribution för AEM {#minimal-mongodb-deployment-for-aem}

Nedan visas en minimal driftsättning för AEM på MongoDB. För enkelhetens skull har SSL-terminering och HTTP-proxykomponenter generaliserats. Den består av en enda MongoDB-replikuppsättning, med en primär och två sekundära.

![chlimage_1-4](assets/chlimage_1-4.png)

En minimal distribution kräver 3 `mongod` instanser konfigurerade som en replikuppsättning. En instans väljs som primär och de andra instanserna är sekundära, med valet hanterat av `mongod`. Kopplade till varje instans är en lokal disk. För att klustret ska stödja inläsningen rekommenderas en genomströmning på minst 12 MB/s med mer än 3 000 I/O-åtgärder per sekund (IOPS).

AEM-författarna är anslutna till `mongod` instanserna, där varje AEM-författare ansluter till alla tre `mongod` instanserna. Skrivningar skickas till det primära och läsningar kan läsas från någon av instanserna. Trafiken distribueras baserat på inläsning av en dispatcher till någon av de aktiva AEM-författarinstanserna. OAK-datalagret är ett `FileDataStore`och MongoDB-övervakning tillhandahålls av MMS eller MongoDB Ops Manager beroende på platsen för distributionen. Operativsystemnivå och loggövervakning tillhandahålls av tredjepartslösningar som Splunk eller Ganglia.

I den här distributionen krävs alla komponenter för en lyckad implementering. Komponenter som saknas kommer att lämna implementeringen som icke-fungerande.

### Operativsystem {#operating-systems}

En lista över vilka operativsystem som stöds för AEM 6 finns på sidan [](/help/sites-deploying/technical-requirements.md)Tekniska krav.

### Miljöer {#environments}

Virtualiserade miljöer stöds förutsatt att det finns god kommunikation mellan de olika tekniska team som kör projektet. Detta omfattar teamet som kör AEM, teamet som äger operativsystemet och teamet som hanterar den virtualiserade infrastrukturen.

Det finns specifika krav för I/O-kapaciteten för MongoDB-instanserna som måste hanteras av det team som hanterar den virtualiserade miljön. Om projektet använder en molndistribution, som Amazon Web Services, måste instanser etableras med tillräcklig I/O-kapacitet och konsekvens för att stödja MongoDB-instanserna. Annars kommer MongoDB-processerna och Oak-databasen att fungera otillförlitligt och felaktigt.

I virtualiserade miljöer kommer MongoDB att kräva specifika I/O- och VM-konfigurationer för att se till att lagringsmotorn i MongoDB inte har någon VMWare-resursallokeringsprinciper. En framgångsrik implementering säkerställer att det inte finns några hinder mellan de olika teamen och att alla är registrerade för att leverera de prestanda som krävs.

## Maskinvarufrågor {#hardware-considerations}

### Lagring {#storage}

För att uppnå läs- och skrivgenomströmningen för bästa prestanda utan behov av för tidig horisontell skalning, kräver MongoDB vanligtvis SSD-lagring eller lagring med prestanda som motsvarar SSD.

### RAM {#ram}

MongoDB version 2.6 och 3.0 som använder MMAP-lagringsmotorn kräver att databasens arbetsuppsättning och dess index passar i RAM-minnet.

Otillräckligt RAM-minne ger en avsevärd prestandaförsämring. Storleken på arbetsuppsättningen och databasen är mycket programberoende. Även om det går att göra vissa uppskattningar är det mest tillförlitliga sättet att fastställa mängden RAM-minne som krävs att bygga AEM-programmet och testa det.

För att underlätta inläsningstestningsprocessen kan följande förhållande mellan arbetsuppsättningens och databasens totala storlek förutsättas:

* 1:10 för SSD-lagring
* 1:3 för hårddisklagring

Detta innebär att 200 GB RAM krävs för en databas på 2 TB vid SSD-driftsättning.

Även om samma begränsningar gäller för lagringsmotorn WiredTiger i MongoDB 3.0 är korrelationen mellan arbetsmängden, RAM och sidfel inte så starka eftersom WiredTiger inte använder minnesmappning på samma sätt som MMAP-lagringsmotorn.

>[!NOTE]
>
>Adobe rekommenderar att du använder lagringsmotorn WiredTiger för AEM 6.1-distributioner som använder MongoDB 3.0.

### Datalager {#data-store}

På grund av begränsningar i MongoDB-arbetsflödet rekommenderas starkt att datalagret upprätthålls oberoende av MongoDB. I de flesta miljöer bör man använda en NAS `FileDataStore` som är tillgänglig för alla AEM-instanser. I situationer där Amazon Web Services används finns det också en `S3 DataStore`. Om datalagret av någon anledning bevaras i MongoDB, bör datalagrets storlek läggas till i den totala databasstorleken och arbetsmängdsberäkningarna justeras på lämpligt sätt. Det kan innebära att du måste tilldela betydligt mer RAM-minne för att kunna upprätthålla prestanda utan sidfel.

## Övervakning {#monitoring}

Övervakning är en nödvändig förutsättning för ett framgångsrikt genomförande av projektet. Även om det med tillräcklig kunskap är möjligt att köra AEM på MongoDB utan övervakning, finns denna kunskap vanligtvis hos ingenjörer som är specialiserade för varje avsnitt i distributionen.

Detta innebär vanligtvis att en FoU-tekniker arbetar på Apache Oak Core och en MongoDB-specialist.

Utan övervakning på alla nivåer krävs detaljerade kunskaper om kodbasen för att kunna diagnostisera problem. Tack vare övervakning och lämplig vägledning om större statistik kommer genomförandegrupperna att kunna reagera på avvikelser på lämpligt sätt.

Det går att använda kommandoradsverktyg för att få en snabb ögonblicksbild av driften av ett kluster, men det är nästan omöjligt att göra det i realtid över många värdar. Kommandoradsverktyg ger sällan historisk information längre än några minuter och tillåter aldrig korrelation mellan olika typer av mätvärden. En kort period av långsam `mongod` bakgrundssynkronisering kräver en stor manuell insats för att korrelera mot I/O Wait eller överdrivet skrivande till en delad lagringsresurs från en till synes oansluten virtuell dator.

### MongoDB Cloud Manager {#mongodb-cloud-manager}

MongoDB Cloud Manager är en kostnadsfri tjänst som erbjuds av MongoDB som tillåter övervakning och hantering av MongoDB-instanser. Den ger en översikt över prestanda och hälsa för MongoDB-klustret i realtid. Den hanterar både molninstanser och privata värdinstanser förutsatt att instansen kan nå Cloud Manager-övervakningsservern.

Det kräver en agent som är installerad på MongoDB-instansen som ansluter till övervakningsservern. Agenten består av tre nivåer:

* En automatiseringsagent som helt kan automatisera allt på MongoDB-servern,
* En övervakningsagent som kan övervaka `mongod` instansen,
* En säkerhetskopieringsagent som kan utföra schemalagda säkerhetskopieringar av data.

Även om det är enklare att använda Cloud Manager för underhållsautomatisering av ett MongoDB-kluster är många av rutinuppgifterna inte nödvändiga, och varken använder dem för säkerhetskopiering eller säkerhetskopiering. Övervakning krävs dock när du väljer Cloud Manager för övervakning.

Mer information om MongoDB Cloud Manager finns i [MongoDB-dokumentationen](https://docs.cloud.mongodb.com/).

### Ops-hanteraren för MongoDB {#mongodb-ops-manager}

MongoDB Ops Manager är samma programvara som MongoDB Cloud Manager. När Ops Manager har registrerats kan det laddas ned och installeras lokalt i ett privat datacenter eller på en annan bärbar eller stationär dator. Den använder en lokal MongoDB-databas för att lagra data och kommunicera på exakt samma sätt som Cloud Manager med de hanterade servrarna. Om du har säkerhetsprofiler som förbjuder en övervakningsagent bör MongoDB Ops Manager användas.

### Övervakning av operativsystem {#operating-system-monitoring}

Övervakning på operativsystemnivå krävs för att köra ett AEM MongoDB-kluster.

Ganglia är ett bra exempel på ett sådant system och ger en bild av omfattningen och detaljerna av den information som krävs, utöver grundläggande hälsomått som CPU, genomsnittlig belastning och ledigt diskutrymme. För att kunna diagnostisera problem krävs information på lägre nivå, t.ex. entropingpoolnivåer, CPU I/O Wait, socketar i FIN_WAIT2-läge.

### Loggaggregering {#log-aggregation}

Med ett kluster av flera servrar är central loggaggregering ett krav för ett produktionssystem. Programvara som Splunk stöder loggaggregering och gör det möjligt för team att analysera mönster för programmets beteende utan att behöva samla in loggarna manuellt.

## Checklistor {#checklists}

I det här avsnittet beskrivs olika åtgärder som du bör vidta för att se till att dina AEM- och MongoDB-distributioner är korrekt konfigurerade innan du implementerar ditt projekt.

### Nätverk {#network}

1. Kontrollera först att alla värdar har en DNS-post
1. Alla värdar ska kunna matchas genom sin DNS-post från alla andra routningsbara värdar
1. Alla MongoDB-värdar kan dirigeras från alla andra MongoDB-värdar i samma kluster
1. MongoDB-värdar kan dirigera paket till MongoDB Cloud Manager och de andra övervakningsservrarna
1. AEM-servrar kan dirigera paket till alla MongoDB-servrar
1. Fördröjning för paket mellan en AEM-server och en MongoDB-server är mindre än två millisekunder utan paketförlust och standarddistribution på en millisekund eller mindre.
1. Kontrollera att det inte finns mer än två hopp mellan en AEM- och en MongoDB-server
1. Det finns inte mer än två hopp mellan två MongoDB-servrar
1. Det finns inga routrar som är högre än OSI Level 3 mellan några huvudservrar (MongoDB eller AEM eller någon kombination).
1. Om VLAN-trunkering eller någon form av nätverkstunnling används måste den uppfylla paketets latenskontroller.

### AEM-konfiguration {#aem-configuration}

#### Konfiguration av nodarkiv {#node-store-configuration}

AEM-instanserna måste konfigureras att använda AEM med MongoMK. Basen på mongoMK-implementeringen i AEM är Document Node Store.

Mer information om hur du konfigurerar nodarkiv finns i [Konfigurera nodarkiv och datalager i AEM](/help/sites-deploying/data-store-config.md).

Nedan visas ett exempel på Document Node Store-konfiguration för en minimal MongoDB-distribution:

```xml
# org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config
#MongoDB server details
mongodburi=mongodb://aem:aempassword@mongodbserver1.customer.com:27000,mongodbserver2.customer.com:27000

#Name of MongoDB database to use
db=aem

#Store binaries in custom BlobStore e.g. FileDataStore
customBlobStore=true

cache=2048
blobCacheSize=1024
```


Var:

* `mongodburi`
Det här är MongoDB-servern som AEM behöver ansluta till. Anslutningar görs till alla kända medlemmar i standardreplikuppsättningen. Om MongoDB Cloud Manager används aktiveras serversäkerhet. Därför måste anslutningssträngen innehålla ett lämpligt användarnamn och lösenord. Icke-företagsversioner av MongoDB stöder endast autentisering av användarnamn och lösenord. Mer information om syntaxen för anslutningssträngar finns i [dokumentationen](https://docs.mongodb.org/manual/reference/connection-string/).

* `db`
Namnet på databasen. Standardvärdet för AEM är `aem-author`.

* `customBlobStore`
Om distributionen lagrar binärfiler i databasen utgör de en del av arbetsuppsättningen. Därför bör du inte lagra binärfiler i MongoDB, vilket kan innebära att du kan använda ett alternativt datalager som ett `FileSystem` datalager på en NAS.

* `cache`
Cachestorleken i megabyte. Detta fördelas mellan olika cacheminnen som används i `DocumentNodeStore`. Standardvärdet är 256 MB. Oak-läsningsprestanda kan dock utnyttja ett större cacheminne.

* `blobCacheSize`
Ofta använda bloggar kan cachas av AEM för att undvika att de hämtas från datalagret. Detta påverkar prestandan mer, särskilt när du lagrar blobbar i MongoDB-databasen. Alla filsystembaserade datalager kan utnyttja diskcachen på operativsystemnivå.

#### Konfiguration av datalager {#data-store-configuration}

Datalagret används för att lagra filer som är större än ett tröskelvärde. Under det tröskelvärdet lagras filer som egenskaper i Document Node Store. Om `MongoBlobStore` används skapas en dedikerad samling i MongoDB för att lagra blobben. Den här samlingen bidrar till `mongod` instansens arbetsuppsättning och kräver att `mongod` det finns mer RAM-minne för att undvika prestandaproblem. Av den anledningen bör du konfigurera så att du undviker problemet `MongoBlobStore` för produktionsdistributioner och användning `FileDataStore` som stöds av en NAS som delas av alla AEM-instanser. Eftersom cacheminnet på operativsystemnivå är effektivt vid filhantering bör den minsta storleken på en fil på disken ställas in på nära blockstorleken på disken så att filsystemet används effektivt och många små dokument inte bidrar mycket till `mongod` instansens arbetssätt.

Här är en typisk datalagerkonfiguration för en minimal AEM-distribution med MongoDB:

```xml
# org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
# The minimum size of an object that should be stored in this data store.
minRecordLength=4096
path=/datastore
maxCachedBinarySize=4096
cacheSizeInMB=128
```


Var:

* `minRecordLength`
Storlek i byte. Binärfiler som är mindre än eller lika med den här storleken lagras med Document Node Store. I stället för att lagra blobbens ID lagras innehållet i binärfilen. För binära filer som är större än den här storleken lagras binärfilens ID som en egenskap för dokumentet i nodsamlingen, och binärfilens brödtext lagras på `FileDataStore` disken. 4 096 byte är en typisk blockstorlek i filsystemet.

* `path`
Sökvägen till datalagrets rot. För en MongoMK-distribution måste det här vara ett delat filsystem som är tillgängligt för alla AEM-instanser. Vanligtvis används en NAS-server (Network Attached Storage). För molnbaserade distributioner som Amazon Web Services finns också `S3DataFileStore` lösningen.

* `cacheSizeInMB`
Den totala storleken på binärt cacheminne i megabyte. Den används för att cachelagra binärfiler som är mindre än `maxCacheBinarySize` inställningen.

* `maxCachedBinarySize`
Maximal storlek i byte för en binär cache-lagring i den binära cachen. Om ett filsystembaserat datalager används bör du inte använda höga värden för datalagrets cache eftersom binärfilerna redan cachas av operativsystemet.

#### Inaktivera frågetipset {#disabling-the-query-hint}

Du bör inaktivera frågetipset som skickas med alla frågor genom att lägga till egenskapen

`-Doak.mongo.disableIndexHint=true`

när du startar AEM. På så sätt beräknas MongoDB utifrån det lämpligaste indexvärdet som ska användas baserat på intern statistik.

Om frågetipset inte är inaktiverat kommer prestandajustering av index inte att påverka AEM-prestanda.

#### Aktivera beständig cache för MongoMK {#enable-persistent-cache-for-mongomk}

Vi rekommenderar att en beständig cachekonfiguration aktiveras för MongoDB-distributioner för att maximera hastigheten för miljöer med höga I/O-läsprestanda. Mer information finns i dokumentationen [till](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html)Jackrabbit Oak.

## Optimering av operativsystemet MongoDB {#mongodb-operating-system-optimizations}

### Stöd för operativsystem {#operating-system-support}

MongoDB 2.6 använder en minnesmappad lagringsmotor som är känslig för vissa aspekter av operativsystemets nivåhantering mellan RAM och disk. Fråge- och läsprestanda för MongoDB-instansen använder sig av att undvika eller eliminera långsamma I/O-åtgärder som ofta kallas sidfel. Det här är fel på sidor som gäller i synnerhet `mongod` processen. De ska inte blandas ihop med sidfel på operativsystemnivå.

För snabb drift bör MongoDB-databasen bara komma åt data som redan finns i RAM-minnet. De data som behövs för åtkomst består av index och data. Den här samlingen med index och data kallas för arbetsuppsättningen. Om arbetsuppsättningen är större än den tillgängliga RAM MongoDB måste skicka in data från disken till en I/O-kostnad, och andra data som redan finns i minnet raderas. Om avlägsnandet gör att data läses in på nytt från disksidans fel blir det vanligaste och prestandan försämras. Om arbetsuppsättningen är dynamisk och variabel uppstår fler sidfel som stöd för åtgärder.

MongoDB kan köras i ett antal operativsystem, bland annat en mängd olika Linux-versioner, Windows och Mac OS. Mer information finns på [https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms) . Beroende på vilket operativsystem du väljer har MongoDB olika rekommendationer på operativsystemnivå. Dokumentationen finns på [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) och sammanfattas här.

#### Linux {#linux}

* Inaktivera genomskinliga övertoningar och överstrålning. Mer information finns i Inställningar för [genomskinliga stora sidor](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/) .
* [Justera readahead-inställningarna](https://docs.mongodb.com/manual/administration/production-notes/#readahead) på enheterna som lagrar databasfilerna så att de passar ditt sätt att arbeta.

   * Om din arbetsuppsättning är större än det tillgängliga RAM-minnet och dokumentets åtkomstmönster är slumpmässigt bör du, för MMAPv1-lagringsmotorn, överväga att sänka läsbarheten till 32 eller 16. Utvärdera olika inställningar för att hitta ett optimalt värde som maximerar det inneboende minnet och minskar antalet sidfel.
   * För lagringsmotorn WiredTiger ska du ställa in readahead på 0 oavsett lagringsmedietyp (snurrning, SSD osv.). I allmänhet bör du använda den rekommenderade inställningen för framåtriktad avläsning, såvida inte testningen visar en mätbar, upprepningsbar och tillförlitlig fördel i ett högre avläsningsvärde. [Support](https://docs.mongodb.com/manual/administration/production-notes/#readahead) för MongoDB Professional ger råd och vägledning om andra konfigurationer än noll.

* Inaktivera det justerade verktyget om du kör RHEL 7/CentOS 7 i en virtuell miljö.
* När RHEL 7/CentOS 7 körs i en virtuell miljö anropar det justerade verktyget automatiskt en prestandaprofil som härleds från prestandagenomströmning, vilket automatiskt ställer in readahead-inställningarna till 4 MB. Detta kan påverka prestandan negativt.
* Använd diskschemaläggaren för noop eller deadline för SSD-enheter.
* Använd diskschemaläggaren på toppen för virtualiserade enheter på virtuella gästdatorer.
* Inaktivera NUMA eller ställ in vm.zone_reclaim_mode på 0 och kör [mongod](https://docs.mongodb.com/manual/administration/production-notes/#readahead) instans med nodinterfoliering. Se: [MongoDB och NUMA Hardware](https://docs.mongodb.com/manual/administration/production-notes/#readahead) för mer information.

* Justera de högsta tillåtna värdena för maskinvaran så att de passar ditt sätt att arbeta. Om flera instanser av [monguefeber](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) eller [mongos](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) körs under samma användare, skalar du gränsvärdena i enlighet med detta. Se: [UNIX Ulimit Settings](https://docs.mongodb.com/manual/reference/ulimit/) för mer information.

* Använd noatime för monteringspunkten [dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath) .
* Konfigurera tillräckliga filreferenser (fs.file-max), kernelns pidgräns (kernel.pid_max) och maximala trådar per process (kernel.threads-max) för distributionen. För stora system ger följande värden en bra utgångspunkt:

   * fs.file-max värde 98000,
   * kernel.pid_max värde på 64000,
   * andkernel.threads-max value of 64000

* Kontrollera att utbytesutrymmet är konfigurerat på datorn. Mer information om lämplig storlek finns i dokumentationen för ditt operativsystem.
* Kontrollera att systemets standardinställning för TCP Keepalive är korrekt. Värdet 300 ger ofta bättre prestanda för replikuppsättningar och delade kluster. Se: Påverkar [TCP-livstid MongoDB-distributioner?](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) i Vanliga frågor för mer information.

#### Windows {#windows}

* Överväg att inaktivera uppdateringarna för senaste åtkomsttid för NTFS. Motsvarar inaktivering av tid på Unix-liknande system.

### WiredTiger {#wiredtiger}

Från och med MongoDB 3.2 är standardlagringsmotorn för MongoDB lagringsmotorn WiredTiger. Den här motorn har ett antal robusta och skalbara funktioner som gör den mycket bättre lämpad för allmänna databasarbetsbelastningar. I följande avsnitt beskrivs dessa funktioner.

#### Samtidighet på dokumentnivå {#document-level-concurrency}

WiredTiger använder samtidighetskontroll på dokumentnivå för skrivåtgärder. Det innebär att flera klienter kan ändra olika dokument i en samling samtidigt.

För de flesta läs- och skrivåtgärder använder WiredTiger en optimistisk samtidighetskontroll. WiredTiger använder endast intent-lås på global nivå, databas- och samlingsnivå. När lagringsmotorn upptäcker konflikter mellan två åtgärder uppstår en skrivkonflikt som gör att MongoDB försöker utföra åtgärden på ett genomskinligt sätt. Vissa globala åtgärder, vanligtvis kortlivade åtgärder med flera databaser, kräver fortfarande ett globalt instansövergripande lås.

Vissa andra åtgärder, till exempel att släppa en samling, kräver fortfarande ett exklusivt databaslås.

#### Fixeringar och kontrollpunkter {#snapshots-and-checkpoints}

WiredTiger använder MultiVersion Concurrency Control (MVCC). I början av en åtgärd ger WiredTiger en ögonblicksbild av data till transaktionen. En ögonblicksbild ger en enhetlig vy över data i minnet.

När WiredTiger skriver till disk, skrivs alla data i en ögonblicksbild på ett konsekvent sätt över alla datafiler. De nu [varaktiga](https://docs.mongodb.com/manual/reference/glossary/#term-durable) data fungerar som en kontrollpunkt i datafilerna. Kontrollpunkten ser till att datafilerna är konsekventa fram till och med den sista kontrollpunkten. Kontrollpunkter fungerar alltså som återställningspunkter.

MongoDB konfigurerar WiredTiger för att skapa kontrollpunkter (d.v.s. skriva ögonblicksbildsdata till disk) med 60 sekunders intervall eller 2 GB journaldata.

När en ny kontrollpunkt skrivs är den föregående kontrollpunkten fortfarande giltig. Även om MongoDB avbryter eller stöter på ett fel när en ny kontrollpunkt skrivs kan MongoDB återställas från den senaste giltiga kontrollpunkten när den startas om.

Den nya kontrollpunkten blir tillgänglig och permanent när metadatatabellen i WiredTiger uppdateras automatiskt för att referera till den nya kontrollpunkten. När den nya kontrollpunkten är tillgänglig frigör WiredTiger sidor från de gamla kontrollpunkterna.

Med WiredTiger kan MongoDB återställas från den senaste kontrollpunkten, även utan [journalföring](https://docs.mongodb.com/manual/reference/glossary/#term-durable). Om du vill återställa ändringar som gjorts efter den sista kontrollpunkten kör du med [journalföring](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Journal {#journal}

WiredTiger använder en transaktionslogg som skriver framför i kombination med [kontrollpunkter](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints) för att säkerställa datalagring.

WiredTiger-journalen består av alla dataändringar mellan kontrollpunkterna. Om MongoDB avslutas mellan kontrollpunkter används journalen för att spela upp alla data som ändrats sedan den senaste kontrollpunkten. Information om hur ofta MongoDB skriver journaldata till disken finns i [Journalföringsprocess](https://docs.mongodb.com/manual/core/journaling/#journal-process).

WiredTiger-journalen komprimeras med hjälp av [komprimeringsbiblioteket](https://docs.mongodb.com/manual/core/journaling/#journal-process) Snappy. Om du vill ange en alternativ komprimeringsalgoritm eller ingen komprimering använder du inställningen [storage.wiredTiger.engineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor) .

Mer information finns i: [Journalföring med WiredTiger](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger).

>[!NOTE]
>
>Minsta loggpoststorlek för WiredTiger är 128 byte. Om en loggpost är 128 byte eller mindre komprimeras inte posten av WiredTiger.
>
>Du kan inaktivera journalföring genom att ställa in [storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) på false, vilket kan minska overheadkostnaden för att underhålla journalen.
>
>Om du inte använder journalen för [fristående](https://docs.mongodb.com/manual/reference/glossary/#term-standalone) instanser innebär det att du förlorar vissa dataändringar när MongoDB avslutas oväntat mellan kontrollpunkterna. För medlemmar i [replikuppsättningar](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set)kan replikeringsprocessen ge tillräckliga hållbarhetsgarantier.

#### Komprimering {#compression}

Med WiredTiger stöder MongoDB komprimering för alla samlingar och index. Komprimering minimerar användningen av lagringsutrymme på bekostnad av ytterligare CPU.

Som standard använder WiredTiger blockkomprimering med [komprimeringsbiblioteket Snappy](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) för alla samlingar och [prefixkomprimering](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression) för alla index.

För samlingar finns även blockkomprimering med [zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) . Om du vill ange en alternativ komprimeringsalgoritm eller ingen komprimering använder du inställningen [storage.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) .

Om du vill inaktivera [prefixkomprimering](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)för index använder du inställningen [storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression) .

Komprimeringsinställningarna kan även konfigureras per samling och per index när du skapar samlingar och index. Se [Ange lagringsmotoralternativ](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) och alternativet [db.collection.createIndex() storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options) .

För de flesta arbetsbelastningar balanserar standardkomprimeringsinställningarna lagringseffektivitet och bearbetningskrav.

Journalen WiredTiger komprimeras också som standard. Mer information om journalkomprimering finns i [Journal](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Minnesanvändning {#memory-use}

Med WiredTiger använder MongoDB både det interna WiredTiger-cacheminnet och filsystemets cache.

Från och med 3.4 kommer det interna cache-minnet för WiredTiger som standard att använda det större av antingen:

* 50 % RAM minus 1 GB, eller
* 256 MB

Som standard använder WiredTiger blockkomprimering för Snappy för alla samlingar och prefixkomprimering för alla index. Komprimeringsstandardinställningarna kan konfigureras på global nivå och kan även ställas in per samling och per index när du skapar samlingar och index.

Olika representationer används för data i det interna WiredTiger-cacheminnet jämfört med formatet på disken:

* Data i filsystemets cache är samma som på disken-formatet, inklusive fördelarna med komprimering för datafiler. Filsystemets cache används av operativsystemet för att minska I/O-diskens storlek.

Index som läses in i det interna WiredTiger-cacheminnet har en annan datarepresentation än formatet på disken, men kan ändå utnyttja indexprefixkomprimering för att minska RAM-användningen.

Vid komprimering av indexprefix dupliceras vanliga prefix från indexerade fält.

Samlingsdata i det interna WiredTiger-cacheminnet är okomprimerade och använder en annan representation än i formatet på disken. Blockkomprimering kan ge avsevärda besparingar på disken, men data måste vara okomprimerade för att kunna hanteras av servern.

Via filsystemets cache använder MongoDB automatiskt allt ledigt minne som inte används av WiredTiger-cachen eller av andra processer.

Information om hur du justerar storleken på det interna WiredTiger-cacheminnet finns i [storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) och [—wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb). Undvik att öka den interna cachestorleken för WiredTiger över standardvärdet.

### NUMA {#numa}

Med åtkomst till icke-enhetligt minne (NUMA) kan en kärna hantera hur minne mappas till processorkärnorna. Även om detta försöker göra minnesåtkomsten snabbare för kärnor som ser till att de kan komma åt de data som krävs, stör NUMA MMAP och lägger till ytterligare fördröjning eftersom läsningar inte kan förutsägas. Därför måste NUMA inaktiveras för processen på alla operativsystem som har den `mongod` funktionen.

I ett NUMA-arkitekturminne är alltså anslutet till CPU:er och CPU:er är anslutna till en buss. I en SMP- eller UMA-arkitektur är minnet anslutet till bussen och delas av CPU:er. När en tråd allokerar minne på en NUMA-processor tilldelas den enligt en princip. Standardinställningen är att tilldela minne som är kopplat till trådens lokala CPU, såvida det inte finns något ledigt utrymme, och då används minne från en ledig CPU till en högre kostnad. När minnet har tilldelats flyttas det inte mellan processorer. Allokeringen utförs av en princip som ärvs från den överordnade tråden, vilket i slutändan är den tråd som startade processen.

I många databaser som ser datorn som en enhetlig minnesarkitektur med flera kärnor leder detta till att den ursprungliga CPU:n blir full först och den sekundära CPU-fyllningen senare, särskilt om en central tråd är ansvarig för allokering av minnesbuffertar. Lösningen är att ändra NUMA-principen för huvudtråden som används för att starta `mongod` processen.

Detta kan du göra genom att köra följande kommando:

```shell
numactl --interleaved=all <mongod> -f config
```

Den här principen tilldelar minne i en runda robat över alla processornoder, vilket ger en jämn fördelning över alla noder. Den ger inte tillgång till minne med högsta prestanda, som i system med flera CPU-maskinvara. Ungefär hälften av minnesåtgärderna kommer att gå långsammare och över bussen, men `mongod` har inte skrivits för att nå NUMA på ett optimalt sätt, så det är en rimlig kompromiss.

### NUMA-problem {#numa-issues}

Om `mongod` processen startas från en annan plats än `/etc/init.d` mappen är det troligt att den inte kommer att startas med rätt NUMA-princip. Beroende på vilken standardprincip som används kan problem uppstå. Detta beror på att de olika installationsprogrammen för Linux-pakethanteraren för MongoDB även installerar en tjänst med konfigurationsfiler `/etc/init.d` som utför det steg som beskrivs ovan. Om du installerar och kör MongoDB direkt från ett arkiv ( `.tar.gz`) måste du manuellt köra pengar under `numactl` processen.

>[!NOTE]
>
>Mer information om tillgängliga NUMA-principer finns i den [numeriska dokumentationen](https://linux.die.net/man/8/numactl).

MongoDB-processen fungerar på olika sätt med olika allokeringsprinciper:

```

```

* `-membind=<nodes>`
Allokera bara på noderna i listan. Mongod allokerar inte minne på noder som visas och kanske inte använder allt tillgängligt minne.

* `-cpunodebind=<nodes>`
Kör bara på noderna. Mongud körs bara på de angivna noderna och använder bara minne som är tillgängligt på dessa noder.

* `-physcpubind=<nodes>`
Kör bara på de angivna CPU:erna (kärnor). Mongod kan bara köras på de angivna CPU:erna och bara använda minne som finns på dessa processorer.

* `--localalloc`
Alltid allokera minne på den aktuella noden, men använd alla noder som tråden körs på. Om en tråd utför allokering kommer endast det minne som är tillgängligt för den processorn att användas.

* `--preferred=<node>`
Prioriterar allokering till en nod, men återgår till andra om den önskade noden är full. Relativ notation för att definiera en nod kan användas. Dessutom körs trådarna på alla noder.

Vissa av profilerna kan resultera i mindre än allt tillgängligt RAM-minne för `mongod` processen. Till skillnad från MySQL undviker MongoDB aktivt sidindelning på operativsystemnivå, och därför kan `mongod` processen få mindre minne som verkar tillgängligt.

#### Byter {#swapping}

På grund av databasernas minneskrävande natur måste byte på operativsystemnivå inaktiveras. MongoDB-processen undviker designbyte.

#### Fjärrfilsystem {#remote-filesystems}

Fjärrfilsystem som NFS rekommenderas inte för MongoDB:s interna datafiler (enkelprocessdatabasfiler) eftersom de orsakar för mycket latens. Detta ska inte blandas ihop med det delade filsystem som krävs för lagring av Oak Blob-filer (FileDataStore), där NFS rekommenderas.

#### Läs framåt {#read-ahead}

Framåtläsning måste justeras så att onödiga block inte läses från disken vilket resulterar i onödig användning av I/O-bandbredd när en sida sidas i en slumpmässig läsning.

### Linux-krav {#linux-requirements}

#### Lägsta kernel-versioner {#minimum-kernel-versions}

* **2.6.23** för `ext4` filsystem

* **2.6.25** för `xfs` filsystem

#### Rekommenderade inställningar för databasdiskar {#recommended-settings-for-database-disks}

**Stäng av tid**

Vi rekommenderar att du `atime` stänger av för de diskar som ska innehålla databaserna.

**Ange NOOP-diskschemaläggaren**

Du kan göra detta genom att:

Kontrollera först i/O-schemaläggaren som är inställd. Detta kan du göra genom att köra följande kommando:

```shell
cat /sys/block/sdg/queue/scheduler
```

Om svaret är `noop` något behöver du inte göra mer.

Om NOOP inte är den inställda I/O-schemaläggaren kan du ändra den genom att köra:

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**Justera värdet för read ahead**

Vi rekommenderar att du använder värdet 32 för diskarna där MongoDB-databaser körs från. Detta uppgår till 16 kilobyte. Du kan ställa in den genom att köra:

```shell
sudo blockdev --setra <value> <device>
```

#### Aktivera NTP {#enable-ntp}

Kontrollera att NTP är installerat och igång på datorn som är värd för MongoDB-databaserna. Du kan till exempel installera det med pakethanteraren yum på en CentOS-dator:

```shell
sudo yum install ntp
```

När NTP-daemon har installerats och startats kan du kontrollera om körningsfilen innehåller serverns tidsförskjutning.

#### Inaktivera genomskinliga stora sidor {#disable-transparent-huge-pages}

Red Hat Linux använder en minneshanteringsalgoritm som kallas för Transparent Huge Pages (THP). Vi rekommenderar att du inaktiverar det om du använder operativsystemet för databasarbetsbelastningar.

Du kan inaktivera det genom att följa nedanstående procedur:

1. Öppna `/etc/grub.conf` filen i valfritt textredigeringsprogram.
1. Lägg till följande rad i filen grob.conf:

   ```xml
   transparent_hugepage=never
   ```

1. Kontrollera slutligen om inställningen har börjat gälla genom att köra:

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   Om THP är inaktiverat bör utdata för ovanstående kommando vara:

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>Mer information om genomskinliga stora sidor finns i den här [artikeln](https://access.redhat.com/solutions/46111).

#### Inaktivera NUMA {#disable-numa}

I de flesta installationer där NUMA är aktiverat inaktiveras MongoDB-daemon automatiskt om det körs som en tjänst från `/etc/init.d` mappen.

Om så inte är fallet kan du inaktivera NUMA per processnivå. Kör följande kommandon om du vill inaktivera den:

```shell
numactl --interleave=all <path_to_process>
```

Var `<path_to_process>` är vägen till monguefeden.

Inaktivera sedan zonåteranvändning genom att köra:

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### Justera de högsta tillåtna inställningarna för monteringsprocessen {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux ger konfigurerbar kontroll över resurstilldelningen via `ulimit` kommandot. Detta kan göras per användare eller process.

Vi rekommenderar att du konfigurerar ulimit för monguidade processer i enlighet med [MongoDB Recommended Ulimit Settings](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings).

#### Testa MongoDB I/O-prestanda {#test-mongodb-i-o-performance}

MongoDB har ett verktyg som heter `mongoperf` som är utformat för att testa I/O-prestanda. Vi rekommenderar att du använder den för att testa prestanda för alla dina MongoDB-instanser som utgör din infrastruktur.

Mer information om hur du använder `mongoperf`finns i [MongoDB-dokumentationen](https://docs.mongodb.org/manual/reference/program/mongoperf/).

>[!NOTE]
>
>Observera att det `mongoperf` är utformat för att vara en indikator på MongoDB-prestanda på den plattform det körs på. På grund av detta bör resultaten inte betraktas som slutgiltiga för ett produktionssystems prestanda.
>
>Du kan köra kompletterande tester med `fio` Linux-verktyget för att få exaktare prestanda.

**Testa läsprestanda på virtuella datorer som ingår i distributionen**

När du har installerat verktyget växlar du till MongoDB-databaskatalogen för att köra testerna. Starta sedan det första testet genom att köra `mongoperf`med den här konfigurationen:

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

De önskade utdata bör vara upp till två gigabyte per sekund (2 GB/s) och 500 000 IOPS med 32 trådar för alla MongoDB-instanser.

Kör ett andra test, den här gången med minnesmappade filer, genom att ange `mmf:true` parametern:

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

Utdata från det andra testet bör vara betydligt högre än det första, vilket indikerar minnesöverföringsprestanda.

>[!NOTE]
>
>När du utför testerna ska du kontrollera I/O-användningsstatistik för de virtuella datorerna i operativsystemets övervakningssystem. Om de anger värden som är lägre än 100 procent för I/O-läsningar kan det vara problem med din virtuella dator.

**Testa skrivprestanda för den primära MongoDB-instansen**

Kontrollera sedan I/O-skrivprestanda för den primära MongoDB-instansen genom att köra `mongoperf` från databaskatalogen MongoDB med samma inställningar:

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

Önskat utvärde bör vara 12 megabyte per sekund och nå cirka 3 000 IOPS, med liten variation mellan antalet trådar.

## Steg för virtualiserade miljöer {#steps-for-virtualised-environments}

### VMWare {#vmware}

Om du använder WMWare ESX för att hantera och driftsätta dina virtualiserade miljöer måste du utföra följande inställningar från ESX-konsolen för att kunna hantera MongoDB-åtgärden:

1. Stäng av minnesballongfunktion
1. Förallokera och reservera minne för de virtuella datorer som ska vara värd för MongoDB-databaserna
1. Använd I/O-kontroll för lagring för att tilldela tillräcklig I/O till `mongod` processen.
1. Garantera processorresurser för de datorer som är värdar för MongoDB genom att ställa in [CPU-reservation](https://pubs.vmware.com/vsphere-4-esx-vcenter/index.jsp?topic=/com.vmware.vsphere.vmadmin.doc_41/vsp_vm_guide/configuring_virtual_machines/t_allocate_cpu_resources.html)

1. Överväg att använda ParaVirtual I/O-drivrutiner. Mer information finns i den här [kunskapsbasartikeln](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1010398).

### Amazon Web Services {#amazon-web-services}

Mer information om hur du konfigurerar MongoDB med Amazon Web Services finns i artikeln [Konfigurera AWS-integrering](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/) på MongoDB-webbplatsen.

## Säkra MongoDB före distribution {#securing-mongodb-before-deployment}

Se det här inlägget om [säker driftsättning av MongoDB](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html) för råd om hur du skyddar konfigurationen av dina databaser före driftsättning.

## Dispatcher {#dispatcher}

### Välja operativsystem för Dispatcher {#choosing-the-operating-system-for-the-dispatcher}

För att din MongoDB-distribution ska fungera på rätt sätt måste det operativsystem som ska vara värd för dispatchern köra **Apache httpd** **version 2.4 eller senare.**

Se även till att alla bibliotek som används i ditt bygge är uppdaterade för att minimera säkerhetsriskerna.

### Dispatcher-konfiguration {#dispatcher-configuration}

En typisk Dispatcher-konfiguration fungerar mellan tio och tjugo gånger så mycket som dataflödet för en enda AEM-instans.

Eftersom Dispatcher i huvudsak är tillståndslös kan den enkelt skalas vågrätt. I vissa distributioner måste författare hindras från att komma åt vissa resurser. Därför rekommenderar vi att du använder en dispatcher med författarinstanserna.

För att köra AEM utan en dispatcher krävs att SSL-terminering och belastningsutjämning utförs av ett annat program. Detta är nödvändigt eftersom sessioner måste ha tillhörighet till den AEM-instans som de skapade, ett koncept som kallas klibbiga anslutningar. Syftet med detta är att säkerställa att uppdateringar av innehållet uppvisar minimal fördröjning.

Mer information om hur du konfigurerar [Dispatcher-dokumentationen](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) finns i Dispatcher-dokumentationen.

### Ytterligare konfiguration {#additional-configuration}

#### Fästiga anslutningar {#sticky-connections}

Antikiga anslutningar säkerställer att alla personaliserade sidor och sessionsdata för en användare är sammansatta på samma instans av AEM. Dessa data lagras på instansen, så efterföljande begäranden från samma användare kommer att återgå till samma instans.

Vi rekommenderar att klisterlappande anslutningar aktiveras för alla inre lagerroutningsbegäranden till AEM-instanserna, vilket uppmuntrar efterföljande begäranden att nå samma AEM-instans. Detta bidrar till att minimera fördröjning som annars syns när innehållet uppdateras mellan olika instanser.

#### Långt förfallodatum {#long-expires}

Som standard har innehåll som skickas ut från en AEM-dispatcher rubriker med senaste ändring och Etag-rubriker, utan någon indikation på innehållets förfallodatum. Detta garanterar att användargränssnittet alltid får den senaste versionen av resursen, men det innebär också att webbläsaren utför en GET-åtgärd för att kontrollera om resursen har ändrats. Detta kan resultera i flera begäranden till vilka HTTP-svaret är 304 (inte ändrat), beroende på sidinläsningen. Om du anger en förfallotid för resurser som inte går ut och tar bort rubrikerna Senaste ändring och ETag, kommer innehållet att cachelagras och inga ytterligare uppdateringsbegäranden kommer att göras förrän datumet i rubriken Förfaller är uppfyllt.

Men om du använder den här metoden finns det inget rimligt sätt att låta resursen förfalla i webbläsaren innan rubriken Förfaller förfaller. För att minska detta kan HtmlClientLibraryManager konfigureras att använda oföränderliga URL:er för klientbibliotek.

Dessa URL:er ändras garanterat inte. När innehållet i resursen som finns i URL-adressen ändras, återspeglas ändringarna automatiskt i URL-adressen så att webbläsaren begär rätt version av resursen.

Standardkonfigurationen lägger till en väljare i HtmlClientLibraryManager. Eftersom resursen är en väljare cachelagras den i dispatchern med väljaren intakt. Den här väljaren kan också användas för att säkerställa korrekt förfallobeteende. Standardväljaren följer `lc-.*?-lc` mönstret. Följande httpd-konfigurationsdirektiv för Apache säkerställer att alla begäranden som matchar mönstret hanteras med lämplig förfallotid.

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### Ingen sniff {#no-sniff}

Om innehåll skickas ut utan innehållstyp försöker många webbläsare gissa vilken typ av innehåll det är genom att läsa de första byten i innehållet. Det här kallas &quot;sniffing&quot;. Sniffing öppnar en säkerhetsrisk eftersom användare som kan skriva till databasen kan överföra skadligt innehåll utan innehållstyp.

Därför är det lämpligt att lägga till en rubrik till resurser som hanteras av dispatchern. `no-sniff` Dispatcharen cache-lagrar emellertid inte rubriker. Det innebär att innehåll som hanteras från det lokala filsystemet kommer att ha innehållstypen som bestäms av dess tillägg, i stället för att den ursprungliga innehållstyprubriken från den ursprungliga AEM-servern används.

Inga kodavsnitt kan aktiveras på ett säkert sätt om webbprogrammet är känt för att aldrig hantera cachelagrade resurser utan filtyp.

Du kan aktivera Ingen signatur:

```xml
Header set X-Content-Type-Options "nosniff"
```

Den kan också aktiveras selektivt:

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### Skyddsprofil för innehåll {#content-security-policy}

Standardinställningarna för avsändare tillåter en öppen säkerhetsprincip för innehåll, som också kallas CSP. Detta gör att en sida kan läsa in resurser från alla domäner som omfattas av standardreglerna i webbläsarsandlådan.

Det är önskvärt att begränsa varifrån resurser kan läsas in för att undvika att läsa in kod i javascript-motorn från otillförlitliga eller overifierade externa servrar.

Med CSP kan du finjustera principer. I ett komplext program måste emellertid CSP-huvuden utvecklas med försiktighet eftersom principer som är för restriktiva kan bryta delar av användargränssnittet.

>[!NOTE]
>
>Mer information om hur detta fungerar finns på [OWASP-sidan om skyddsprofiler](https://www.owasp.org/index.php/Content_Security_Policy)för innehåll.

### Storlek {#sizing}

Mer information om storleksändring finns i riktlinjerna [för](/help/managing/hardware-sizing-guidelines.md)maskinvarustorlek.

### Prestandaoptimering för MongoDB {#mongodb-performance-optimization}

Mer allmän information om MongoDB-prestanda finns i [Analysera MongoDB-prestanda](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/).

## Kända begränsningar {#known-limitations}

### Samtidiga installationer {#concurrent-installations}

MongoMK stöder samtidig användning av flera AEM-instanser med en databas, men inte samtidiga installationer.

För att undvika detta måste du först köra installationen med en enda medlem och lägga till de andra efter att den första installationen är klar.

### Sidnamnslängd {#page-name-length}

Om AEM körs på en distribution av en beständig MongoMK-hanterare, är [sidnamnen begränsade till 150 tecken.](/help/sites-authoring/managing-pages.md)

>[!NOTE]
>
>[Se även MongoDB-dokumentationen](https://docs.mongodb.com/manual/reference/limits/) för att lära dig mer om de kända begränsningarna och tröskelvärdena i MongoDB.

