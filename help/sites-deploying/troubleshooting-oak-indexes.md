---
title: Felsöka ekindex
seo-title: Felsöka ekindex
description: Hur man upptäcker och åtgärdar långsam omindexering.
seo-description: Hur man upptäcker och åtgärdar långsam omindexering.
uuid: 6567ddae-128c-4302-b7e8-8befa66b1f43
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: ea70758f-6726-4634-bfb4-a957187baef0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1486'
ht-degree: 0%

---


# Felsökning av aktivitetsindex{#troubleshooting-oak-indexes}

## Långsam omindexering {#slow-re-indexing}

AEM interna omindexeringsprocess samlar in databasdata och lagrar dem i Oak-index för att ge stöd för prestandafrågor. I undantagsfall kan processen bli långsam eller till och med fastna. Den här sidan fungerar som en felsökningsguide som hjälper dig att identifiera om indexeringen är långsam, hitta orsaken och lösa problemet.

Det är viktigt att skilja mellan omindexering som tar en otillräckligt lång tid och omindexering som tar lång tid eftersom det indexerar enorma mängder innehåll. Den tid det tar att indexera innehåll skalas till exempel med mängden innehåll, så stora produktionsdatabaser tar längre tid att indexera om än små utvecklingsdatabaser.

Mer information om när och hur du indexerar om innehåll finns i [Bästa praxis för frågor och indexering](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

## Inledande identifiering {#initial-detection}

Inledande identifiering av långsam indexering kräver granskning av JMX MBeans för `IndexStats`. Gör följande på den påverkade AEM:

1. Öppna webbkonsolen och klicka på fliken JMX eller gå till https://&lt;värd>:&lt;port>/system/console/jmx (t.ex. [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)).
1. Navigera till menyerna `IndexStats`.
1. Öppna `IndexStats` MBeans för `async` och `fulltext-async`.

1. För båda MBeans ska du kontrollera om tidsstämpeln **Done** och **LastIndexTime** är mindre än 45 minuter från den aktuella tiden.

1. Om tidsvärdet (**Done** eller **LastIndexedTime**) är större än 45 minuter från den aktuella tiden i MBean misslyckas indexjobbet eller tar för lång tid. Detta gör att asynkrona index blir inaktuella.

## Indexeringen pausas efter en tvingad avstängning {#indexing-is-paused-after-a-forced-shutdown}

En framtvingad avstängning resulterar i AEM att asynkron indexering avbryts i upp till 30 minuter efter omstarten och kräver normalt ytterligare 15 minuter för att slutföra den första omindexeringsprocessen, i totalt cirka 45 minuter (återkoppling till tidsramen [Inledande detektion](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) på 45 minuter). Om du misstänker att indexering har pausats efter en tvingad avstängning:

1. För det första ska du avgöra om AEM stängdes av på ett tvingat sätt (den AEM processen tvångsdödades eller ett strömavbrott inträffade) och därefter starta om.

   * [AEM ](/help/sites-deploying/configure-logging.md) loggning kan granskas för detta ändamål.

1. Om den framtvingade avstängningen inträffar kommer AEM automatiskt att avbryta omindexering i upp till 30 minuter vid omstart.
1. Vänta ca 45 minuter tills AEM återupptar vanliga asynkrona indexeringsåtgärder.

## Trådpoolen överlästes {#thread-pool-overloaded}

>[!NOTE]
>
>För AEM 6.1 kontrollerar du att [AEM 6.1 CFP 11](https://helpx.adobe.com/experience-manager/release-notes-aem-6-1-cumulative-fix-pack.html) är installerat.

I undantagsfall kan den trådpool som används för att hantera asynkron indexering bli överbelastad. För att isolera indexeringsprocessen kan en trådpool konfigureras för att förhindra att andra AEM stör Oaks förmåga att indexera innehåll i tid. För att göra detta bör du:

1. Definiera en ny isolerad trådpool för Apache Sling Scheduler som ska användas för asynkron indexering:

   * På den berörda AEM-instansen går du till AEM OSGi Web Console>OSGi>Configuration>Apache Sling Scheduler eller till https://&lt;host>:&lt;port>/system/console/configMgr (t.ex. [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))
   * Lägg till en post i fältet Tillåtna trådpooler med värdet eke.
   * Klicka på Spara längst ned till höger för att spara ändringarna.

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. Kontrollera att den nya trådpoolen för Apache Sling Scheduler är registrerad och visas i webbkonsolen för Apache Sling Scheduler Status.

   * Gå till AEM OSGi Web console>Status>Sling Scheduler eller gå till https://&lt;port>/system/console/status-slingscheduler (t.ex. [http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler))
   * Kontrollera att följande poolposter finns:

      * ApacheSlingoak
      * ApacheSlingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## Observationskön är full {#observation-queue-is-full}

Om för många ändringar och implementeringar görs i databasen på kort tid kan indexeringen fördröjas på grund av en fullständig observationskö. Börja med att fastställa om observationskön är full:

1. Gå till webbkonsolen och klicka på fliken JMX eller gå till https://&lt;värd>:&lt;port>/system/console/jmx (t.ex. [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
1. Öppna MBean för Oak-databasstatistik och kontrollera om något `ObservationQueueMaxLength`-värde är större än 10 000.

   * Vid normal användning måste det här maxvärdet alltid minskas till noll (särskilt i avsnittet `per second`) så verifiera att sekundmåtten för `ObservationQueueMaxLength` är 0.
   * Om värdena är 10 000 eller fler och ökar stadigt innebär det att minst en (eventuellt fler) kö inte kan bearbetas så fort nya ändringar (implementeringar) inträffar.
   * Varje observationskö har en gräns (10 000 som standard) och om kön når den gränsen försämras hanteringen.
   * När du använder MongoMK försämras prestanda för intern ekacache när kölängden blir stor. Den här korrelationen kan ses i ett ökat `missRate` för cachen `DocChildren` i MBean för `Consolidated Cache`-statistik.

1. För att undvika att överskrida tillåtna gränser för observationsköer bör du:

   * Minska den konstanta frekvensen för implementeringar. Korta toppar i implementeringar är godtagbara, men den konstanta hastigheten bör minskas.
   * Öka storleken på `DiffCache` enligt beskrivningen i [Prestandajusteringstips > Justering av monolagring > Dokumentcache-storlek](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html#main-pars_text_3).

## Identifiera och åtgärda en fast omindexeringsprocess {#identifying-and-remediating-a-stuck-re-indexing-process}

Omindexering kan betraktas som&quot;helt fast&quot; under två förhållanden:

* Omindexeringen är mycket långsam, till den punkt där inga större framsteg rapporteras i loggfiler om antalet noder som har gått igenom.

   * Om det t.ex. inte finns några meddelanden under en timme, eller om förloppet är så långsamt att det tar en vecka eller mer att slutföra.

* Omindexering fastnar i en oändlig slinga om upprepade undantag förekommer i loggfilerna (till exempel `OutOfMemoryException`) i indexeringstråden. Upprepningen av samma undantag i loggen anger att Oak försöker indexera samma sak flera gånger, men misslyckas i samma problem.

Så här identifierar och korrigerar du en fast omindexeringsprocess:

1. För att identifiera orsaken till den fastande indexeringen måste följande information samlas in:

   * Samla 5 minuters tråddump, en tråddump varannan sekund.
   * [Ange DEBUG-nivå och loggar för tilläggen](/help/sites-deploying/configure-logging.md).

      * *org.apache.jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*
   * Samla in data från asynkrona `IndexStats` MBean:

      * Navigera till AEM OSGi Web Console>Main>JMX>IndexStat>async

         eller gå till [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)
   * Använd [oak-run.jar konsolläge](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) för att samla in information om vad som finns under noden * `/:async`*.
   * Samla in en lista med databaskontrollpunkter med hjälp av `CheckpointManager` MBean:

      * AEM OSGi Web Console>Main>JMX>CheckpointManager>listCheckpoints()

         eller gå till [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)



1. När du har samlat in all information som beskrivs i steg 1 startar du om AEM.

   * Om du startar om AEM kan problemet åtgärdas vid hög samtidig belastning (spill i observationskön eller liknande).
   * Om en omstart inte löser problemet kan du öppna ett problem med [Adobe kundtjänst](https://helpx.adobe.com/marketing-cloud/contact-support.html) och ange all information som samlats in i steg 1.

## Säkert avbryter asynkron omindexering {#safely-aborting-asynchronous-re-indexing}

Omindexering kan avbrytas (stoppas innan den är klar) via indexeringsfälten `async, async-reindex`och f `ulltext-async` ( `IndexStats` Mbean). Mer information finns också i dokumentationen för Apache Oak om [Så här avbryter du omindexering](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex). Ta dessutom hänsyn till att

* Omindexeringen av egenskapsindexen Lucene och Lucene kan avbrytas eftersom de är naturligt asynkrona.
* Omindexeringen av Oak-egenskapsindex kan bara avbrytas om omindexering initierades via `PropertyIndexAsyncReindexMBean`.

Så här avbryter du omindexering:

1. Identifiera det IndexStats MBean som styr det omindexeringsintervall som behöver stoppas.

   * Navigera till rätt IndexStats MBean via JMX-konsolen genom att antingen gå till AEM OSGi Web Console>Main>JMX eller https://&lt;host>:&lt;port>/system/console/jmx (t.ex. [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
   * Öppna IndexStats MBean baserat på det omindexeringsfält som du vill stoppa ( `async`, `async-reindex` eller `fulltext-async`)

      * Titta på egenskapen async för att identifiera lämpligt intervall och därmed instansen IndexStats MBean. Egenskapen &quot;async&quot; kommer att innehålla körfältets namn: `async`, `async-reindex` eller `fulltext-async`.
      * Fältet är också tillgängligt genom att du öppnar AEM Index Manager i kolumnen &quot;Async&quot;. Om du vill komma åt indexhanteraren går du till Åtgärder > Diagnostik > Indexhanteraren.

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. Anropa kommandot `abortAndPause()` på lämpligt `IndexStats` MBean.
1. Markera indexdefinitionen på ekv för att förhindra att indexeringen återupptas när indexeringsintervallet återupptas.

   * När du indexerar om ett **befintligt**-index ska du ange egenskapen reindex till false

      * `/oak:index/someExistingIndex@reindex=false`
   * Eller, för ett **nytt**-index, antingen:

      * Ange att type-egenskapen ska vara inaktiverad

         * `/oak:index/someNewIndex@type=disabled`
      * eller ta bort indexdefinitionen helt

   Genomför ändringarna i databasen när de är klara.

1. Slutligen kan du återuppta asynkron indexering på det avbrutna indexeringsfältet.

   * Anropa kommandot `resume()`i det `IndexStats` MBean som utfärdade kommandot `abortAndPause()` i steg 2.

## Förhindrar långsam omindexering {#preventing-slow-re-indexing}

Det är bäst att indexera om under tysta perioder (t.ex. inte under en stor innehållsimport) och helst under underhållsperioder när AEM är känd och kontrollerad. Se även till att omindexeringen inte sker under andra underhållsaktiviteter.
