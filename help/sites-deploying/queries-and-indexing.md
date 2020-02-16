---
title: Fråga och indexering
seo-title: Fråga och indexering
description: Lär dig hur du konfigurerar index i AEM.
seo-description: Lär dig hur du konfigurerar index i AEM.
uuid: a1233d2e-1320-43e0-9b18-cd6d1eeaad59
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 492741d5-8d2b-4a81-8f21-e621ef3ee685
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
translation-type: tm+mt
source-git-commit: 1f7a45adc73b407c402a51b061632e72d97ca306

---


# Fråga och indexering{#oak-queries-and-indexing}

>[!NOTE]
>
>Den här artikeln handlar om att konfigurera index i AEM 6. De bästa sätten att optimera fråga- och indexeringsprestanda finns i [Bästa metoder för frågor och indexering](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

## Introduktion {#introduction}

Till skillnad från Jackrabbit 2 indexerar inte Oak innehållet som standard. Anpassade index måste skapas när det behövs, ungefär som med traditionella relationsdatabaser. Om det inte finns något index för en viss fråga, kommer kanske många noder att gå igenom. Frågan kanske fortfarande fungerar, men den är antagligen väldigt långsam.

Om Oak stöter på en fråga utan index skrivs ett loggmeddelande på WARN-nivå ut:

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## Frågespråk som stöds {#supported-query-languages}

Oak-frågemotorn stöder följande språk:

* XPath (rekommenderas)
* SQL-2
* SQL (utgått)
* JQOM

## Indexerartyper och kostnadsberäkning {#indexer-types-and-cost-calculation}

Med den Apache Oak-baserade serverdelen kan olika indexerare kopplas in i databasen.

En indexerare är **egenskapsindexet**, som indexdefinitionen lagras i själva databasen.

Implementeringar för **Apache Lucene** och **Solr** är också tillgängliga som standard, som båda stöder fulltextindexering.

Om det inte finns någon annan indexerare används **Traversal Index** . Det innebär att innehållet inte är indexerat och att innehållsnoderna gås igenom för att hitta matchningar med frågan.

Om det finns flera tillgängliga indexerare för en fråga beräknar varje tillgänglig indexerare kostnaden för att köra frågan. Därefter väljer Oak indexeraren med den lägsta uppskattade kostnaden.

![chlimage_1-148](assets/chlimage_1-148.png)

Diagrammet ovan är en högnivårepresentation av frågekörningsmekanismen i Apache Oak.

Först tolkas frågan i ett abstrakt syntaxträd. Sedan kontrolleras frågan och omvandlas till SQL-2, som är det ursprungliga språket för Oak-frågor.

Därefter används varje index för att beräkna kostnaden för frågan. När det är klart hämtas resultaten från det lägsta indexvärdet. Slutligen filtreras resultaten, både för att säkerställa att den aktuella användaren har läsåtkomst till resultatet och att resultatet matchar hela frågan.

## Konfigurera index {#configuring-the-indexes}

>[!NOTE]
>
>För stora databaser är det tidskrävande att skapa ett index. Detta gäller både när ett index skapas första gången och när ett index indexeras om (när definitionen har ändrats). Se även [Felsöka ekindex](/help/sites-deploying/troubleshooting-oak-indexes.md) och [förhindra långsam omindexering](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing).

Om omindexering behövs i mycket stora databaser, särskilt när du använder MongoDB och fulltextindex, bör du överväga att extrahera text och använda eko-run för att skapa det ursprungliga indexet och indexera om.

Index konfigureras som noder i databasen under noden **oak:index** .

Indexnodens typ måste vara **oak:QueryIndexDefinition.** Det finns flera konfigurationsalternativ tillgängliga för varje indexerare som nodegenskaper. Mer information finns i konfigurationsinformationen för varje indexerartyp nedan.

### Egenskapsindexet {#the-property-index}

Egenskapsindexet är vanligtvis användbart för frågor som har egenskapsbegränsningar men som inte är fulltext. Den kan konfigureras genom att följa proceduren nedan:

1. Öppna CRXDE genom att gå till `http://localhost:4502/crx/de/index.jsp`
1. Skapa en ny nod under **ekning:index**
1. Namnge noden **PropertyIndex** och ange nodtypen till **oak:QueryIndexDefinition**
1. Ange följande egenskaper för den nya noden:

   * **** typ:  `property` (av typen String)
   * **** propertyNames:  `jcr:uuid` (av typen Namn)
   I det här exemplet indexeras `jcr:uuid` egenskapen, vars jobb är att visa den universellt unika identifieraren (UUID) för noden som den är kopplad till.

1. Spara ändringarna.

Egenskapsindexet har följande konfigurationsalternativ:

* Egenskapen **type** anger typen av index, och i det här fallet måste den anges till **egenskap**

* Egenskapen **propertyNames** anger listan med egenskaper som ska lagras i indexet. Om det saknas används nodnamnet som referensvärde för egenskapsnamnet. I det här exemplet läggs egenskapen **jcr:uid** , vars jobb är att visa den unika identifieraren (UUID) för dess nod, till i indexet.

* Den **unika** flaggan som, om den anges till **true** , lägger till en unik begränsning i egenskapsindexet.

* Med egenskapen **declareNodeTypes** kan du ange en viss nodtyp som indexet bara gäller för.
* The **reindex** flag that if set to **true**, will trigger a full content reindex.

### Orderat index {#the-ordered-index}

Det sorterade indexet är ett tillägg till egenskapsindexet. Den har dock tagits bort. Index av den här typen måste ersättas med [Lucene-egenskapsindexet](#the-lucene-property-index).

### Fullständigt Lucene-textindex {#the-lucene-full-text-index}

En fulltextindexerare baserad på Apache Lucene finns i AEM 6.

Om ett fulltextindex är konfigurerat används heltextindexet för alla frågor som har ett fulltextvillkor, oavsett om det finns andra villkor som är indexerade eller oavsett om det finns en sökvägsbegränsning.

Om inget fulltextindex är konfigurerat kommer frågor med fulltextvillkor inte att fungera som förväntat.

Eftersom indexet uppdateras via en asynkron bakgrundstråd kommer vissa textsökningar att vara otillgängliga under ett litet tidsfönster tills bakgrundsprocesserna är klara.

Du kan konfigurera ett fulltextindex för Lucene enligt följande procedur:

1. Öppna CRXDE och skapa en ny nod under **ek:index**.
1. Namnge noden **LuceneIndex** och ange nodtypen **oak:QueryIndexDefinition**
1. Lägg till följande egenskaper i noden:

   * **** typ:  `lucene` (av typen String)
   * **** asynk:  `async` (av typen String)

1. Spara ändringarna.

Lucene-indexet har följande konfigurationsalternativ:

* Den **type** -egenskap som anger indextypen måste anges till **lucene**
* Den **asynkrona** egenskapen som måste anges som **asynkron**. Detta skickar indexuppdateringsprocessen till en bakgrundstråd.
* Egenskapen **includePropertyTypes** , som definierar vilken delmängd av egenskapstyper som ska inkluderas i indexet.
* Egenskapen **excludePropertyNames** som definierar en svart lista med egenskapsnamn - egenskaper som ska exkluderas från indexet.
* Flaggan **reindex** som, när den anges till **true**, aktiverar ett fullständigt innehållsindexvärde.

### Egenskapsindexet Lucene {#the-lucene-property-index}

Sedan **Oak 1.0.8** kan Lucene användas för att skapa index som innehåller egenskapsbegränsningar som inte är fulltext.

För att uppnå ett Lucene-egenskapsindex måste egenskapen **fulltextEnabled** alltid anges till false.

Ta följande exempelfråga:

```xml
select * from [nt:base] where [alias] = '/admin'
```

Om du vill definiera ett Lucene-egenskapsindex för frågan ovan kan du lägga till följande definition genom att skapa en ny nod under **oak:index:**

* **** Namn: `LucenePropertyIndex`
* **** Typ: `oak:QueryIndexDefinition`

När noden har skapats lägger du till följande egenskaper:

* **type:**

   ```
   lucene (of type String)
   ```

* **asynk:**

   ```
   async (of type String)
   ```

* **fulltextEnabled:**

   ```
   false (of type Boolean)
   ```

* **** includePropertyNames: `["alias"] (of type String)`

>[!NOTE]
>
>Jämfört med det vanliga egenskapsindexet är Lucene-egenskapsindexet alltid konfigurerat i asynkront läge. Resultatet som returneras av indexet kanske inte alltid återspeglar det mest aktuella läget i databasen.

>[!NOTE]
>
>Mer information om Lucene-egenskapsindexet finns på dokumentationssidan [för](https://jackrabbit.apache.org/oak/docs/query/lucene.html)Apache Jackrabbit Oak Lucene.

### Lucene Analyzers {#lucene-analyzers}

Sedan version 1.2.0 stöder Oak Lucene-analysatorer.

Analysatorer används både när ett dokument indexeras och vid frågetillfället. En analyserare undersöker texten i fälten och genererar en tokenström. Lucene-analysatorerna består av en serie tokeniserings- och filterklasser.

Analysatorerna kan konfigureras via `analyzers` noden (av typen `nt:unstructured`) inuti `oak:index` definitionen.

Standardanalysatorn för ett index är konfigurerad i noden analysatorns underordnade `default` nod.

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>En lista över tillgängliga analysatorer finns i API-dokumentationen för Lucene-versionen som du använder.

#### Ange klassen Analyzer direkt {#specifying-the-analyzer-class-directly}

Om du vill använda någon av de färdiga analysverktygen kan du konfigurera den enligt följande procedur:

1. Leta reda på det index som du vill använda analyseraren med under `oak:index` -noden.

1. Skapa en underordnad nod under indexet med namnet `default` type `nt:unstructured`.

1. Lägg till en egenskap i standardnoden med följande egenskaper:

   * **** Namn: `class`
   * **** Typ: `String`
   * **** Värde: `org.apache.lucene.analysis.standard.StandardAnalyzer`
   Värdet är namnet på den analyserarklass som du vill använda.

   Du kan också ange att analyseraren ska användas med en specifik lucene-version genom att använda den valfria `luceneMatchVersion` strängegenskapen. Ett giltigt syntaxvärde för användning med Lucene 4.7 är:

   * **** Namn: `luceneMatchVersion`
   * **** Typ: `String`
   * **** Värde: `LUCENE_47`
   Om `luceneMatchVersion` inte anges kommer Oak att använda den version av Lucene som levereras med.

1. Om du vill lägga till en stoppordsfil i analyskonfigurationerna kan du skapa en ny nod under den med följande egenskaper: `default`

   * **** Namn: `stopwords`
   * **** Typ: `nt:file`

#### Skapa analytiker via Composition {#creating-analyzers-via-composition}

Analysatorer kan också sättas samman baserat på `Tokenizers`, `TokenFilters` och `CharFilters`. Du kan göra detta genom att ange en analysator och skapa underordnade noder till dess tillvalstokensorer och filter som ska användas i listordning. Se även [https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema](https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)

Se den här nodstrukturen som ett exempel:

* **** Namn: `analyzers`

   * **** Namn: `default`

      * **** Namn: `charFilters`
      * **** Typ: `nt:unstructured`

         * **** Namn: `HTMLStrip`
         * **** Namn: `Mapping`
      * **** Namn: `tokenizer`

         * **** Egenskapsnamn: `name`

            * **** Typ: `String`
            * **** Värde: `Standard`
      * **** Namn: `filters`
      * **** Typ: `nt:unstructured`

         * **** Namn: `LowerCase`
         * **** Namn: `Stop`

            * **** Egenskapsnamn: `words`

               * **** Typ: `String`
               * **** Värde: `stop1.txt, stop2.txt`
            * **** Namn: `stop1.txt`

               * **** Typ: `nt:file`
            * **** Namn: `stop2.txt`

               * **** Typ: `nt:file`





Namnet på filtren, charFilters och tokenizers formas genom att fabrikssuffixen tas bort. Således:

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` blir `standard`

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` blir `Mapping`

* `org.apache.lucene.analysis.core.StopFilterFactory` blir `Stop`

Alla konfigurationsparametrar som krävs för fabriken anges som egenskaper för den aktuella koden.

För exempelvis inläsning av stoppord där innehåll från externa filer måste läsas in, kan innehållet anges genom att en underordnad nod av `nt:file` typen för filen skapas.

### Solr-index {#the-solr-index}

Syftet med Solr-indexet är i huvudsak fulltextsökning, men det kan också användas för att indexera sökningar efter sökväg, egenskapsbegränsningar och primära typbegränsningar. Det innebär att Solr-indexet i Oak kan användas för alla typer av JCR-frågor.

Integrationen i AEM sker på databasnivå så att Solr är ett av de möjliga index som kan användas i Oak, den nya databasimplementeringen som levererades med AEM.

Den kan konfigureras för att fungera som en inbäddad server med AEM-instansen eller som en fjärrserver.

### Konfigurera AEM med en inbäddad Solr-server {#configuring-aem-with-an-embedded-solr-server}

>[!CAUTION]
>
>Använd inte en inbäddad Solr-server i en produktionsmiljö. Det ska endast användas i utvecklingsmiljö.

AEM kan användas med en inbäddad Solr-server som kan konfigureras via webbkonsolen. I det här fallet körs Solr-servern i samma JVM som den AEM-instans som den är inbäddad i.

Du kan konfigurera den inbäddade Solr-servern genom att:

1. Gå till webbkonsolen på `https://serveraddress:4502/system/console/configMgr`
1. Sök efter &quot;**Oak Solr server provider**&quot;.
1. Tryck på redigeringsknappen och i följande fönster anger du servertypen till **Inbäddad solr** i listrutan.

1. Redigera sedan &quot;**Oak Solr embedded server configuration**&quot; och skapa en konfiguration. Mer information om konfigurationsalternativen finns på [Apache Solr-webbplatsen](https://lucene.apache.org/solr/documentation.html).

   >[!NOTE]
   >
   >Konfigurationen av Solr-arbetskatalogen (solr.home.path) söker efter en mapp med samma namn i AEM-installationsmappen.

1. Öppna CRXDE och logga in som administratör.
1. Lägg till en nod med namnet **solnodex** av typen **oak:QueryIndexDefinition** under **oak:index** med följande egenskaper:

   * **** typ: `solr`(av typen String)
   * **** asynk: `async`(av typen String)
   * **** omindexera: `true`(av typen Boolean)

1. Spara ändringarna.

### Konfigurera AEM med en enda fjärrserver för Solr {#configuring-aem-with-a-single-remote-solr-server}

AEM kan även konfigureras för att fungera med en Solr-fjärrserverinstans:

1. Hämta och extrahera den senaste versionen av Solr. Mer information om hur du gör detta finns i dokumentationen [för installation av](https://cwiki.apache.org/confluence/display/solr/Installing+Solr)Apache Solr.
1. Skapa nu två Solr-kort. Du kan göra detta genom att skapa mappar för varje delning i mappen där Solr har uppgraderats:

   * Skapa mappen för det första delfönstret:
   `<solrunpackdirectory>\aemsolr1\node1`

   * Skapa mappen för den andra delningen:
   `<solrunpackdirectory>\aemsolr2\node2`

1. Leta reda på exempelinstansen i Solr-paketet. Den finns vanligtvis i en mapp som heter &quot; `example`&quot; i paketets rot.
1. Kopiera följande mappar från exempelinstansen till de två delade mapparna ( `aemsolr1\node1` och `aemsolr2\node2`):

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. Skapa en ny mapp med namnet &quot; `cfg`&quot; i var och en av de två delade mapparna.
1. Placera dina Solr- och Zookeeper-konfigurationsfiler i de nya `cfg` mapparna.

   >[!NOTE]
   >
   >Mer information om Solr- och ZooKeeper-konfigurationen finns i dokumentationen [för](https://wiki.apache.org/solr/ConfiguringSolr) Solr-konfiguration och i [guiden](https://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html)ZooKeeper Getting Started.

1. Starta den första delningen med stöd för ZooKeeper genom att gå till `aemsolr1\node1` och köra följande kommando:

   ```xml
   java -Xmx2g -Dbootstrap_confdir=./cfg/oak/conf -Dcollection.configName=myconf -DzkRun -DnumShards=2 -jar start.jar
   ```

1. Starta den andra delningen genom att gå till `aemsolr2\node2` och köra följande kommando:

   ```xml
   java -Xmx2g -Djetty.port=7574 -DzkHost=localhost:9983 -jar start.jar
   ```

1. När båda delarna har startats testar du att allt är igång genom att ansluta till Solr-gränssnittet på `http://localhost:8983/solr/#/`
1. Starta AEM och gå till webbkonsolen på `http://localhost:4502/system/console/configMgr`
1. Ange följande konfiguration under **fjärrserverkonfigurationen** för Oak Solr:

   * HTTP-URL för Solr: `http://localhost:8983/solr/`

1. Välj **Fjärrserver** i listrutan under **Oak Solr** -serverprovider.

1. Gå till CRXDE och logga in som administratör.
1. Skapa en ny nod med namnet **solrIndex** under **oak:index** och ange följande egenskaper:

   * **** typ: solr (av typen String)
   * **** asynk: async (av typen String)
   * **** omindexera: true (av typen Boolean)

1. Spara ändringarna.

#### Rekommenderad konfiguration för Solr {#recommended-configuration-for-solr}

Nedan visas ett exempel på en baskonfiguration som kan användas med alla tre Solr-distributioner som beskrivs i den här artikeln. Den passar de dedikerade egenskapsindexen som redan finns i AEM och bör inte användas med andra program.

För att kunna använda det på rätt sätt måste du placera innehållet i arkivet direkt i Solr Home Directory. Vid distributioner med flera noder bör den placeras direkt under rotmappen för varje nod.

Rekommenderade Solr-konfigurationsfiler

[Hämta fil](assets/recommended-conf.zip)

### AEM Indexing Tools {#aem-indexing-tools}

AEM 6.1 integrerar även två indexeringsverktyg som finns i AEM 6.0 som en del av Adobe Consulting Services Commons-verktygen:

1. **Förklara frågan**, ett verktyg som hjälper administratörer att förstå hur frågor utförs.
1. **Oak Index Manager**, ett webbanvändargränssnitt för att underhålla befintliga index.

Nu kan du nå dem genom att gå till **Verktyg - Åtgärder - Kontrollpanel - Diagnos** på AEM-välkomstskärmen.

Mer information om hur du använder dem finns i dokumentationen [till](/help/sites-administering/operations-dashboard.md)kontrollpanelen för åtgärder.

#### Skapa egenskapsindex via OSGi {#creating-property-indexes-via-osgi}

ACS Commons-paketet visar även OSGi-konfigurationer som kan användas för att skapa egenskapsindex.

Du kan komma åt den från webbkonsolen genom att söka efter &quot;**Se till att egenskapsindex** för eko&quot;.

![chlimage_1-150](assets/chlimage_1-150.png)

### Felsöka indexeringsproblem {#troubleshooting-indexing-issues}

Det kan uppstå situationer när frågor tar lång tid att köra och den allmänna svarstiden för systemet är långsam.

I det här avsnittet presenteras en uppsättning rekommendationer om vad som behöver göras för att spåra orsaken till sådana problem och råd om hur man löser dem.

#### Förbereder felsökningsinformation för analys {#preparing-debugging-info-for-analysis}

Det enklaste sättet att få den information som krävs för den fråga som körs är via verktyget [](/help/sites-administering/operations-dashboard.md#explain-query)Förklara fråga. På så sätt kan du samla in exakt den information som behövs för att felsöka en långsam fråga utan att behöva läsa loggnivåinformationen. Detta är önskvärt om du känner till frågan som felsöks.

Om detta inte är möjligt av någon anledning, kan du samla indexeringsloggarna i en enda fil och använda den för att felsöka just det problemet.

#### Aktivera loggning {#enable-logging}

Om du vill aktivera loggning måste du aktivera loggar på **DEBUG** -nivå för de kategorier som gäller Oak-indexering och frågor. Dessa kategorier är:

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

Kategorin **com.day.cq.search** gäller bara om du använder verktyget AEM provided Query Builder.

>[!NOTE]
>
>Det är viktigt att loggarna bara är inställda på DEBUG så länge frågan som du vill felsöka körs, annars genereras ett stort antal händelser i loggarna över tid. På grund av detta växlar du tillbaka till INFO-nivåloggning för de kategorier som nämns ovan när de obligatoriska loggarna har samlats in.

Du kan aktivera loggning genom att följa den här proceduren:

1. Peka webbläsaren till `https://serveraddress:port/system/console/slinglog`
1. Klicka på knappen **Lägg till ny loggare** i den nedre delen av konsolen.
1. Lägg till de kategorier som nämns ovan på den nyligen skapade raden. Du kan använda **+** -tecknet om du vill lägga till mer än en kategori i en enskild loggare.
1. Välj **DEBUG** i listrutan **Loggnivå** .
1. Ställ in utdatafilen på `logs/queryDebug.log`. Detta korrelerar alla DEBUG-händelser till en enda loggfil.
1. Kör frågan eller återge sidan som använder frågan som du vill felsöka.
1. När du har kört frågan går du tillbaka till loggningskonsolen och ändrar loggnivån för den nyligen skapade loggboken till **INFO**.

#### Indexkonfiguration {#index-configuration}

Hur frågan utvärderas påverkas i hög grad av indexkonfigurationen. Det är viktigt att få indexkonfigurationen för att kunna analyseras eller skickas till support. Du kan antingen hämta konfigurationen som ett innehållspaket eller hämta en JSON-återgivning.

Eftersom indexeringskonfigurationen i de flesta fall lagras under noden `/oak:index` i CRXDE kan du hämta JSON-versionen på:

`https://serveraddress:port/oak:index.tidy.-1.json`

Om indexet är konfigurerat på en annan plats ändrar du sökvägen i enlighet med detta.

#### MBean-utdata {#mbean-output}

I vissa fall kan det vara bra att ange utdata för indexrelaterade MBeans för felsökning. Du kan göra detta genom att:

1. Gå till JMX-konsolen på:
   `https://serveraddress:port/system/console/jmx`

1. Sök efter följande MBeans:

   * Lucene-indexstatistik
   * CopyOnRead - supportstatistik
   * Oak Query Statistik
   * IndexStats

1. Klicka på var och en av MBeans för att få prestandastatistik. Skapa en skärmbild eller anteckna dem om du behöver ge support.

Du kan också hämta JSON-varianten av statistiken på följande URL:er:

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

Du kan också tillhandahålla konsoliderade JMX-utdata via `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`. Detta inkluderar all Oak-relaterad MBean-information i JSON-format.

#### Annan information {#other-details}

Du kan samla in ytterligare information för att hjälpa till att felsöka problemet, till exempel:

1. Den Oak-version som instansen körs på. Du kan se detta genom att öppna CRXDE och titta på versionen i det nedre högra hörnet av välkomstsidan, eller genom att kontrollera versionen av `org.apache.jackrabbit.oak-core` paketet.
1. Felsökningsutdata för QueryBuilder-felsökningsfrågan. Felsökaren finns på: `https://serveraddress:port/libs/cq/search/content/querydebug.html`

