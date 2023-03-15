---
title: Felsöka ekindex
seo-title: Troubleshooting Oak Indexes
description: Hur man upptäcker och åtgärdar långsam omindexering.
seo-description: How to detect and fix slow re-indexing.
uuid: 6567ddae-128c-4302-b7e8-8befa66b1f43
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: ea70758f-6726-4634-bfb4-a957187baef0
exl-id: 85981463-189c-4f50-9d21-1d2f734b960a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 0%

---

# Felsöka ekindex{#troubleshooting-oak-indexes}

## Långsam omindexering  {#slow-re-indexing}

AEM interna omindexeringsprocess samlar in databasdata och lagrar dem i Oak-index för att ge stöd för prestandafrågor. I undantagsfall kan processen bli långsam eller till och med fastna. Den här sidan fungerar som en felsökningsguide som hjälper dig att identifiera om indexeringen är långsam, hitta orsaken och lösa problemet.

Det är viktigt att skilja mellan omindexering som tar en otillräckligt lång tid och omindexering som tar lång tid eftersom det indexerar enorma mängder innehåll. Den tid det tar att indexera innehåll skalas till exempel med mängden innehåll, så stora produktionsdatabaser tar längre tid att indexera om än små utvecklingsdatabaser.

Se [Metodtips för frågor och indexering](/help/sites-deploying/best-practices-for-queries-and-indexing.md) om du vill ha mer information om när och hur du indexerar om innehåll.

## Inledande identifiering {#initial-detection}

Inledande identifiering av långsam indexering kräver granskning av `IndexStats` JMX MBeans. Gör följande på den påverkade AEM:

1. Öppna webbkonsolen och klicka på fliken JMX eller gå till https://&lt;host>:&lt;port>/system/console/jmx (t.ex. [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)).
1. Navigera till `IndexStats` Mönster.
1. Öppna `IndexStats` MBeans for &quot; `async`&quot; och &quot; `fulltext-async`&quot;.

1. Kontrollera om **Klar** tidsstämpel och **LastIndexTime** tidsstämpeln är mindre än 45 minuter från den aktuella tiden.

1. För MBean, om tidsvärdet (**Klar** eller **LastIndexedTime**) är längre än 45 minuter från den aktuella tiden. Indexjobbet misslyckas eller tar för lång tid. Detta gör att asynkrona index blir inaktuella.

## Indexeringen pausas efter en tvingad avstängning {#indexing-is-paused-after-a-forced-shutdown}

En framtvingad avstängning medför AEM att asynkron indexering avbryts i upp till 30 minuter efter omstarten och kräver normalt ytterligare 15 minuter för att slutföra den första omindexeringsprocessen i totalt cirka 45 minuter (återkoppling till [Inledande identifiering](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) 45 minuter). Om du misstänker att indexering har pausats efter en tvingad avstängning:

1. För det första ska du avgöra om AEM stängdes av på ett tvingat sätt (den AEM processen tvångsdödades eller ett strömavbrott inträffade) och därefter starta om.

   * [AEM](/help/sites-deploying/configure-logging.md) kan granskas för detta ändamål.

1. Om den framtvingade avstängningen inträffar kommer AEM automatiskt att avbryta omindexering i upp till 30 minuter vid omstart.
1. Vänta ca 45 minuter tills AEM återupptar vanliga asynkrona indexeringsåtgärder.

## Trådpoolen har överlästs {#thread-pool-overloaded}

>[!NOTE]
>
>För AEM 6.1 ska du se till att [AEM 6.1 CFP 11](https://helpx.adobe.com/experience-manager/release-notes-aem-6-1-cumulative-fix-pack.html) är installerat.

I undantagsfall kan den trådpool som används för att hantera asynkron indexering bli överbelastad. För att isolera indexeringsprocessen kan en trådpool konfigureras för att förhindra att andra AEM stör Oaks förmåga att indexera innehåll i tid. För att göra detta bör du:

1. Definiera en ny isolerad trådpool för Apache Sling Scheduler som ska användas för asynkron indexering:

   * På den berörda AEM-instansen går du till AEM OSGi Web Console>OSGi>Configuration>Apache Sling Scheduler eller går till https://&lt;host>:&lt;port>/system/console/configMgr (t.ex. [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))
   * Lägg till en post i fältet Tillåtna trådpooler med värdet eke.
   * Klicka på Spara längst ned till höger för att spara ändringarna.

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. Kontrollera att den nya trådpoolen för Apache Sling Scheduler är registrerad och visas i webbkonsolen för Apache Sling Scheduler Status.

   * Gå till AEM OSGi Web console>Status>Sling Scheduler eller gå till https://&lt;host>:&lt;port>/system/console/status-slingscheduler (till exempel [http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler))
   * Kontrollera att följande poolposter finns:

      * ApacheSlingoak
      * ApacheSlingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## Observationskön är full {#observation-queue-is-full}

Om för många ändringar och implementeringar görs i databasen på kort tid kan indexeringen fördröjas på grund av en fullständig observationskö. Börja med att fastställa om observationskön är full:

1. Gå till webbkonsolen och klicka på fliken JMX eller gå till https://&lt;host>:&lt;port>/system/console/jmx (t.ex. [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
1. Öppna MBean för Oak Repository-statistik och kontrollera om det finns några `ObservationQueueMaxLength` värdet är större än 10 000.

   * Vid normal användning måste det här maxvärdet alltid minskas till noll (särskilt i `per second` -avsnittet) så verifiera att `ObservationQueueMaxLength`Sekundärstatistik är 0.
   * Om värdena är 10 000 eller fler och ökar stadigt innebär det att minst en (eventuellt fler) kö inte kan bearbetas så fort nya ändringar (implementeringar) inträffar.
   * Varje observationskö har en gräns (10 000 som standard) och om kön når den gränsen försämras hanteringen.
   * När du använder MongoMK försämras prestanda för intern ekacache när kölängden blir stor. Denna korrelation kan ses vid en ökad `missRate` för `DocChildren` i `Consolidated Cache` statistik MBean.

1. För att undvika att överskrida tillåtna gränser för observationsköer bör du:

   * Minska den konstanta frekvensen för implementeringar. Korta toppar i implementeringar är godtagbara, men den konstanta hastigheten bör minskas.
   * Öka storleken på `DiffCache` enligt beskrivning i [Prestandajusteringstips > Justering av monolagring > Dokumentcache-storlek](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html#main-pars_text_3).

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
   * Samla in data från asynkron `IndexStats` MBean:

      * Navigera till AEM OSGi Web Console>Main>JMX>IndexStat>async

         eller gå till [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)
   * Använd [oak-run.jar konsolläge](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) för att samla in uppgifter om vad som finns under * `/:async`* nod.
   * Samla in en lista med databaskontrollpunkter med `CheckpointManager` MBean:

      * AEM OSGi Web Console>Main>JMX>CheckpointManager>listCheckpoints()

         eller gå till [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)



1. När du har samlat in all information som beskrivs i steg 1 startar du om AEM.

   * Om du startar om AEM kan problemet åtgärdas vid hög samtidig belastning (spill i observationskön eller liknande).
   * Om en omstart inte löser problemet kan du öppna ett problem med [Adobe kundtjänst](https://helpx.adobe.com/marketing-cloud/contact-support.html) och tillhandahålla all information som samlats in i steg 1.

## Säkert avbryter asynkron omindexering {#safely-aborting-asynchronous-re-indexing}

Omindexering kan avbrytas (avbrytas innan den är klar) via `async, async-reindex`och f `ulltext-async` indexera köer ( `IndexStats` Mbean). Mer information finns också i dokumentationen för Apache Oak på [Så här avbryter du omindexering](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex). Ta dessutom hänsyn till att

* Omindexeringen av egenskapsindexen Lucene och Lucene kan avbrytas eftersom de är naturligt asynkrona.
* Omindexeringen av Oak-egenskapsindex kan endast avbrytas om omindexering initierades via `PropertyIndexAsyncReindexMBean`.

Så här avbryter du omindexering:

1. Identifiera det IndexStats MBean som styr det omindexeringsintervall som behöver stoppas.

   * Navigera till rätt IndexStats MBean via JMX-konsolen genom att antingen gå till AEM OSGi Web Console>Main>JMX eller https://&lt;host>:&lt;port>/system/console/jmx (t.ex. [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
   * Öppna IndexStats MBean baserat på det omindexeringsfält som du vill stoppa ( `async`, `async-reindex`, eller `fulltext-async`)

      * Titta på egenskapen async för att identifiera lämpligt intervall och därmed instansen IndexStats MBean. Egenskapen &quot;async&quot; kommer att innehålla körfältets namn: `async`, `async-reindex`, eller `fulltext-async`.
      * Fältet är också tillgängligt genom att du öppnar AEM Index Manager i kolumnen &quot;Async&quot;. Om du vill komma åt indexhanteraren går du till Åtgärder > Diagnostik > Indexhanteraren.

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. Anropa `abortAndPause()` kommando på lämplig `IndexStats` MBean.
1. Markera indexdefinitionen på ekv för att förhindra att indexeringen återupptas när indexeringsintervallet återupptas.

   * När en **befintlig** index, ange egenskapen reindex till false

      * `/oak:index/someExistingIndex@reindex=false`
   * Eller, för **new** index, antingen:

      * Ange att type-egenskapen ska vara inaktiverad

         * `/oak:index/someNewIndex@type=disabled`
      * eller ta bort indexdefinitionen helt

   Genomför ändringarna i databasen när de är klara.

1. Slutligen kan du återuppta asynkron indexering på det avbrutna indexeringsfältet.

   * I `IndexStats` MBean som utfärdade `abortAndPause()` i steg 2 anropar du `resume()`-kommando.

## Förhindra långsam omindexering {#preventing-slow-re-indexing}

Det är bäst att indexera om under tysta perioder (t.ex. inte under en stor innehållsimport) och helst under underhållsperioder när AEM är känd och kontrollerad. Se även till att omindexeringen inte sker under andra underhållsaktiviteter.
