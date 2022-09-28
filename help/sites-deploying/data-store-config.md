---
title: Konfigurera nodarkiv och datalager i AEM 6
description: Lär dig hur du konfigurerar nodarkiv och datalager och hur du utför skräpinsamling i datalager.
content-type: reference
topic-tags: deploying
docset: aem65
feature: Configuring
exl-id: c1c90d6a-ee5a-487d-9a8a-741b407c8c06
source-git-commit: 1a741ff01fcf17dfdcc8c1cebcd858052d07361c
workflow-type: tm+mt
source-wordcount: '3583'
ht-degree: 1%

---

# Konfigurera nodarkiv och datalager i AEM 6{#configuring-node-stores-and-data-stores-in-aem}

## Introduktion {#introduction}

I Adobe Experience Manager (AEM) kan binära data lagras oberoende av innehållsnoderna. Binära data lagras i ett datalager, medan innehållsnoder lagras i ett nodarkiv.

Både datalager och nodarkiv kan konfigureras med OSGi-konfiguration. Varje OSGi-konfiguration refereras med en beständig identifierare (PID).

## Konfigurationssteg {#configuration-steps}

Så här konfigurerar du både nodarkivet och datalagret:

1. Kopiera den AEM snabbstartsfilen till installationskatalogen.
1. Skapa en mapp `crx-quickstart/install` i installationskatalogen.
1. Konfigurera först nodarkivet genom att skapa en konfigurationsfil med namnet på nodarkivalternativet som du vill använda i `crx-quickstart/install` katalog.

   Dokumentnodarkivet (som är grunden för AEM MongoMK-implementering) använder filen `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`.

1. Redigera filen och ange konfigurationsalternativ.
1. Skapa en konfigurationsfil med PID:t för det datalager som du vill använda. Redigera filen för att ange konfigurationsalternativ.

   >[!NOTE]
   >
   >Se [Konfigurationer för nodarkivet](#node-store-configurations) och [Konfigurationer för datalager](#data-store-configurations) för konfigurationsalternativ.

1. Börja AEM.

## Konfigurationer för nodarkivet {#node-store-configurations}

>[!CAUTION]
>
>Nyare versioner av Oak använder ett nytt namnschema och format för OSGi-konfigurationsfiler. Det nya namnschemat kräver att konfigurationsfilen namnges **.config** och det nya formatet kräver att värden skrivs och [dokumenteras här](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>
>Om du uppgraderar från en äldre version av Oak måste du göra en säkerhetskopia av `crx-quickstart/install`mapp först. Efter uppgraderingen återställer du innehållet i mappen till den uppgraderade installationen och ändrar tillägget för konfigurationsfilerna från **.cfg** till **.config**.
>
>Om du läser den här artikeln som förberedelse för en uppgradering från en **AEM 5.x** installerar du [uppgradera](https://docs.adobe.com/content/docs/en/aem/6-0/deploy/upgrade.html) dokumentation först.

### Segmentnodarkiv {#segment-node-store}

Segmentnodarkivet är grunden för AdobeMK-implementeringen i AEM6. Den använder `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` PID för konfiguration.

>[!CAUTION]
>
>PID för segmentnodarkivet har ändrats från `org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions` av AEM 6 till `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` AEM 6.3. Se till att du gör de nödvändiga konfigurationsjusteringarna för att återspegla den här ändringen.

Du kan konfigurera följande alternativ:

* `repository.home`: Sökväg till databasstartplats där databasrelaterade data lagras. Segmentfiler lagras som standard under `crx-quickstart/segmentstore` katalog.

* `tarmk.size`: Maximal storlek för ett segment i MB. Standardmaxstorleken är 256 MB.
* `customBlobStore`: Booleskt värde som anger att ett anpassat datalager används. Standardvärdet är true för AEM 6.3 och senare versioner. Före AEM 6.3 var standardvärdet false.

Följande är ett exempel `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` fil:

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### Dokumentnodarkiv {#document-node-store}

Dokumentnodarkivet är grunden för AEM MongoMK-implementering. Den använder `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`* *PID. Följande konfigurationsalternativ är tillgängliga:

* `mongouri`: The [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) krävs för att ansluta till Mongo-databasen. Standardvärdet är `mongodb://localhost:27017`

* `db`: Namn på Mongo-databasen. Standardvärdet är **Oak** ``. However, new AEM 6 installations use **aem-author** ``som standarddatabasnamn.

* `cache`: Cachestorleken i MB. Detta fördelas mellan olika cacheminnen som används i DocumentNodeStore. Standardvärdet är `256`

* `changesSize`: Storlek i MB på den mappade samling som används i Mongo för cache-lagring av diff-utdata. Standardvärdet är `256`

* `customBlobStore`: Booleskt värde som anger att ett anpassat datalager kommer att användas. Standardvärdet är `false`.

Följande är ett exempel `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config` fil:

```shell
#Mongo server details
mongouri="mongodb://localhost:27017"

#Name of Mongo database to use
db="aem-author"

#Store binaries in custom BlobStore
customBlobStore=B"false"
```

## Konfigurationer för datalager {#data-store-configurations}

När du hanterar ett stort antal binära filer bör du använda ett externt datalager i stället för standardnodarkiven för att maximera prestandan.

Om ditt projekt till exempel kräver ett stort antal medieresurser kan du lagra dem i File- eller S3-datalagret så att du kommer åt dem snabbare än att lagra dem direkt i en MongoDB.

Fildatalagret ger bättre prestanda än MongoDB, och säkerhetskopierings- och återställningsåtgärderna i Mongo är också långsammare med ett stort antal resurser.

Information om olika datalager och konfigurationer beskrivs nedan.

>[!NOTE]
>
>Om du vill aktivera anpassade datalager måste du se till att `customBlobStore` är inställd på `true` i respektive Node Store-konfigurationsfil ([segmentnodbutik](/help/sites-deploying/data-store-config.md#segment-node-store) eller [dokumentnodarkiv](/help/sites-deploying/data-store-config.md#document-node-store)).

### Fildatalager {#file-data-store}

Detta är genomförandet av [FileDataStore](https://jackrabbit.apache.org/api/2.8/org/apache/jackrabbit/core/data/FileDataStore.html) finns i Jackrabbit 2. Det är ett sätt att lagra binära data som normala filer i filsystemet. Den använder `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore` PID.

Dessa konfigurationsalternativ är tillgängliga:

* `repository.home`: Sökväg till databasstartplats där olika databasrelaterade data lagras. Som standard lagras binära filer under `crx-quickstart/repository/datastore` katalog

* `path`: Sökväg till den katalog som filerna ska lagras i. Om det anges har det företräde framför `repository.home` value

* `minRecordLength`: Den minsta storleken i byte för en fil som lagras i datalagret. Binärt innehåll som är mindre än det här värdet infogas.

>[!NOTE]
>
>När du använder en NAS för att lagra delade fildatalager bör du endast använda högpresterande enheter för att undvika prestandaproblem.

## Amazon S3 - datalager {#amazon-s-data-store}

AEM kan konfigureras för att lagra data i Amazon Simple Storage Service (S3). Den använder `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` PID för konfiguration.

För att aktivera S3-datalagrets funktioner måste ett funktionspaket som innehåller S3 Datastore Connector hämtas och installeras. Gå till [Adobe-databas](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/) och ladda ned den senaste versionen från 1.10.x-versionerna av funktionspaketet (till exempel com.adobe.granite.oak.s3connector-1.10.0.zip). Dessutom måste du ladda ned och installera det senaste AEM Service Pack som finns på [Versionsinformation för AEM 6.5](/help/release-notes/release-notes.md) sida.

>[!NOTE]
>
>När du använder AEM med tarMK lagras binärfiler som standard i `FileDataStore`. Om du vill använda tarMK med S3-datastore måste du börja AEM med `crx3tar-nofds` runmode, till exempel:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

När du har laddat ned den kan du installera och konfigurera S3 Connector på följande sätt:

1. Extrahera innehållet i ZIP-filen för funktionspaketet till en tillfällig mapp.

1. Gå till den tillfälliga mappen och navigera till följande plats:

   ```xml
   jcr_root/libs/system/install
   ```

   Kopiera allt innehåll från ovanstående plats till `<aem-install>/crx-quickstart/install.`

1. Om AEM redan har konfigurerats för att fungera med lagringen tar du bort alla befintliga konfigurationsfiler från ***&lt;aem-install>***/*crx-quickstart*/*installera* innan du fortsätter. De filer som behöver tas bort är:

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Återgå till den tillfälliga platsen där funktionspaketet har extraherats och kopiera innehållet i följande mapp:

   * `jcr_root/libs/system/config`

   till

   * `<aem-install>/crx-quickstart/install`

   Kontrollera att du bara kopierar de konfigurationsfiler som behövs för den aktuella konfigurationen. Kopiera `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` -fil.

   >[!NOTE]
   >
   >Utför ovanstående steg på alla noder i klustret en i taget i en klusterkonfiguration. Se även till att använda samma S3-inställningar för alla noder.

1. Redigera filen och lägg till de konfigurationsalternativ som krävs för installationen.
1. Börja AEM.

## Uppgradera till en ny version av 1.10.x S3 Connector {#upgrading-to-a-new-version-of-the-s-connector}

Om du behöver uppgradera till en ny version av 1.10.x S3-kontakten (till exempel från 1.10.0 till 1.10.4) följer du dessa steg:

1. Stoppa AEM.

1. Navigera till `<aem-install>/crx-quickstart/install/15` i AEM installationsmapp och gör en säkerhetskopia av innehållet.
1. Efter säkerhetskopieringen tar du bort den gamla versionen av S3 Connector och dess beroenden genom att ta bort alla jar-filer i `<aem-install>/crx-quickstart/install/15` mapp, till exempel:

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >Filnamnen ovan används endast som illustrationer.

1. Ladda ned den senaste versionen av funktionspaketet 1.10.x från [Adobe-databas](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/).
1. Zippa upp innehållet i en separat mapp och navigera sedan till `jcr_root/libs/system/install/15`.
1. Kopiera jar-filerna till **&lt;aem-install>**/crx-quickstart/install/15 i AEM installationsmapp.
1. Starta AEM och kontrollera anslutningsfunktionen.

Du kan använda konfigurationsfilen med alternativen nedan.

<!--
* accessKey: The AWS access key.
* secretKey: The AWS secret access key. **Note:** When the `accessKey` or `secretKey` is not specified then the [IAM role](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) is used for authentication.
* s3Bucket: The bucket name.
* s3Region: The bucket region.
* path: The path of the data store. The default is **&lt;AEM install folder&gt;/repository/datastore**
* minRecordLength: The minimum size of an object that should be stored in the data store. The minimum/default is **16KB.**
* maxCachedBinarySize: Binaries with size less than or equal to this size will be stored in memory cache. The size is in bytes. The default is **17408 **(17 KB).
* cacheSize: The size of the cache. The value is specified in bytes. The default is **64GB**.
* secret: Only to be used if using binaryless replication for shared datastore setup.
* stagingSplitPercentage: The percentage of cache size configured to be used for staging asynchronous uploads. The default value is **10**.
* uploadThreads: The number of uploads threads that are used for asynchronous uploads. The default value is **10**.
* stagingPurgeInterval: The interval in seconds for purging finished uploads from the staging cache. The default value is **300** seconds (5 minutes).
* stagingRetryInterval: The retry interval in seconds for failed uploads. The default value is **600** seconds (10 minutes).
-->

### Alternativ för konfigurationsfil för S3 Connector {#s3-connector-configuration-file-options}

>[!NOTE]
>
>S3-anslutningen stöder både IAM-användarautentisering och IAM-rollautentisering. Om du vill använda IAM-rollautentisering utelämnar du `accessKey` och `secretKey` värden från konfigurationsfilen. S3-kopplingen får då standardvärdet [IAM-roll](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) som tilldelats instansen.

| Nyckel | Beskrivning | Standard | Krävs |
| --- | --- | --- | --- |
| accessKey | Åtkomstnyckel-ID för IAM-användaren med åtkomst till bucket. |  | Ja, när IAM-roller inte används. |
| secretsKey | Hemlig åtkomstnyckel för IAM-användaren med åtkomst till bucket. |  | Ja, när IAM-roller inte används. |
| cacheSize | Storleken (i byte) på det lokala cacheminnet. | 64 GB | Nej. |
| connectionTimeout | Ange väntetiden (i millisekunder) före timeout när anslutningen upprättas första gången. | 10000 | Nej. |
| maxCachedBinarySize | Binärfiler som är mindre än eller lika med det här värdet (i byte) lagras i minnescachen. | 17408 (17 kB) | Nej. |
| maxConnections | Ange maximalt antal tillåtna öppna HTTP-anslutningar. | 50 | Nej. |
| maxErrorRetry | Ange det maximala antalet försök för misslyckade (hämtningsbara) begäranden. | 3 | Nej. |
| minRecordLength | Den minsta storleken för ett objekt (i byte) som ska lagras i datalagret. | 16384 | Nej. |
| path | Den lokala sökvägen för AEM. | `crx-quickstart/repository/datastore` | Nej. |
| proxyHost | Ange den valfria proxyvärd som klienten ansluter via. |  | Nej. |
| proxyPort | Ange den valfria proxyport som klienten ansluter via. |  | Nej. |
| s3Bucket | Namn på S3-bucket. |  | Ja |
| s3EndPoint | S3 REST API-slutpunkt. |  | Nej. |
| s3Region | Region där bucket finns. Se det här [page](https://docs.aws.amazon.com/general/latest/gr/s3.html) för mer information. | Region där AWS-instansen körs. | Nej. |
| socketTimeout | Ställ in väntetiden (i millisekunder) för data som ska överföras via en etablerad, öppen anslutning innan anslutningens timeout inträffar och stängs. | 50000 | Nej. |
| stagingPurgeInterval | Intervallet (i sekunder) för tömning av slutförda överföringar från mellanlagringscachen. | 300 | Nej. |
| stagingRetryInterval | Intervallet (i sekunder) för återförsök av misslyckade överföringar. | 600 | Nej. |
| stagingSplitPercentage | Procentandel av `cacheSize` som används för att mellanlagra asynkrona överföringar. | 10 | Nej. |
| uploadThreads | Antalet överföringstrådar som används för asynkrona överföringar. | 10 | Nej. |
| writeThreads | Antalet samtidiga trådar som används för att skriva via S3 Transfer Manager. | 10 | Nej. |

<!---
### Bucket region options {#bucket-region-options}

<table>
 <tbody>
  <tr>
   <td>US Standard</td>
   <td><code>us-standard</code></td>
  </tr>
  <tr>
   <td>US West</td>
   <td><code>us-west-2</code></td>
  </tr>
  <tr>
   <td>US West (Northern California)</td>
   <td><code>us-west-1</code></td>
  </tr>
  <tr>
   <td>EU (Ireland)<br /> </td>
   <td><code>EU</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Singapore)<br /> </td>
   <td><code>ap-southeast-1</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Sydney)<br /> </td>
   <td><code>ap-southeast-2</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Tokyo)</td>
   <td><code>ap-northeast-1</code></td>
  </tr>
  <tr>
   <td>South America (Sao Paolo)<br /> </td>
   <td><code>sa-east-1</code></td>
  </tr>
 </tbody>
</table>
-->

### DataStore-cachelagring {#data-store-caching}

>[!NOTE]
>
>DataStore-implementeringar av `S3DataStore`, `CachingFileDataStore` och `AzureDataStore` har stöd för cachelagring av lokala filsystem. The `CachingFileDataStore` implementeringen är användbar när DataStore är på NFS (Network File System).

När du uppgraderar från en äldre cacheimplementering (före 1.6) är det en skillnad i strukturen för det lokala filsystemets cachekatalog. I den gamla cachestrukturen placerades både de hämtade och de överförda filerna direkt under cachesökvägen. Den nya strukturen delar upp hämtningarna och överföringarna och lagrar dem i två kataloger med namnet `upload` och `download` under cachesökväg. Uppgraderingsprocessen bör vara smidig och alla väntande överföringar bör schemaläggas för överföring och alla tidigare hämtade filer i cachen läggs i cachen vid initieringen.

Du kan även uppgradera cacheminnet offline med `datastorecacheupgrade` kommandot för ekkörning. Mer information om hur du kör kommandot finns i [readme](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md) för ekkörningsmodulen.

Cachen har en storleksgräns och kan konfigureras med parametern cacheSize.

#### Nedladdningar {#downloads}

Den lokala cachen kontrolleras för posten för den begärda filen/blobben innan den hämtas från DataStore. När cacheminnet överskrider den konfigurerade gränsen (se `cacheSize` parameter) när du lägger till en fil i cacheminnet kommer vissa filer att tas bort för att frigöra utrymme.

#### Asynkron överföring {#async-upload}

Cachen stöder asynkrona överföringar till DataStore. Filerna mellanlagras lokalt i cachen (i filsystemet) och ett asynkront jobb börjar överföra filen. Antalet asynkrona överföringar begränsas av mellanlagringscachens storlek. Mellanlagringscachens storlek konfigureras med `stagingSplitPercentage` parameter. Den här parametern definierar den procentandel av cachestorleken som ska användas för mellanlagringscachen. Dessutom beräknas procentandelen cacheminne som är tillgängligt för nedladdningar som **(100 - `stagingSplitPercentage`) &#42;`cacheSize`**.

De asynkrona överföringarna är flertrådiga och antalet trådar konfigureras med `uploadThreads` parameter.

Filerna flyttas till huvudcachen för hämtning när överföringen är klar. När storleken på mellanlagringscachen överskrider gränsen överförs filerna synkront till DataStore tills föregående asynkrona överföringar är slutförda och utrymme är igen tillgängligt i mellanlagringscachen. De överförda filerna tas bort från mellanlagringsområdet av ett periodiskt jobb vars intervall har konfigurerats av `stagingPurgeInterval` parameter.

Misslyckade överföringar (till exempel på grund av nätverksavbrott) placeras i en återförsökskö och försök med jämna mellanrum. Återförsöksintervallet konfigureras med `stagingRetryInterval parameter`.

#### Konfigurera icke-binära replikeringar med Amazon S3 {#configuring-binaryless-replication-with-amazon-s}

Följande steg krävs för att konfigurera binär replikering med S3:

1. Installera författaren och publicera instanser och se till att de har startats korrekt.
1. Gå till inställningarna för replikeringsagenten genom att öppna en sida till *https://localhost:4502/etc/replication/agents.author/publish.html*.
1. Tryck på **Redigera** i **Inställningar** -avsnitt.
1. Ändra **Serialisering** textalternativ till **Binärt mindre**.

1. Lägg till parametern &quot; `binaryless`= `true`&quot; i transport-URI:n. Efter ändringen bör URI:n se ut ungefär så här:

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. Starta om alla författare- och publiceringsinstanser så att ändringarna börjar gälla.

#### Skapa ett kluster med S3 och MongoDB {#creating-a-cluster-using-s-and-mongodb}

1. Packa upp CQ-snabbstart med följande kommando:

   `java -jar cq-quickstart.jar -unpack`

1. Skapa en mapp i installationskatalogen när AEM har packats upp *crx-quickstart*/*installera*.

1. Skapa dessa två filer i `crx-quickstart` mapp:

   * *org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService*.*config*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*.*config*

   När filerna har skapats lägger du till konfigurationsalternativen efter behov.

1. Installera de två paket som krävs för S3-datalagret enligt beskrivningen ovan.
1. Kontrollera att MongoDB är installerat och att en instans av `mongod` är igång.
1. AEM med följande kommando:

   `java -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart.jar -r crx3,crx3mongo`

1. Upprepa steg 1 till 4 för den andra AEM instansen.
1. Starta den andra AEM.

#### Konfigurera ett delat datalager {#configuring-a-shared-data-store}

1. Skapa först konfigurationsfilen för datalagret för varje instans som krävs för att dela datalagret:

   * Om du använder en `FileDataStore`, skapa en fil med namnet `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` och placera den i `<aem-install>/crx-quickstart/install` mapp.

   * Skapa en fil med namnet o `rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` i `<aem-install>/crx-quickstart/install` enligt ovan.

1. Ändra konfigurationsfilerna för datalagret på varje instans så att de pekar på samma datalager. Mer information finns i [den här artikeln](/help/sites-deploying/data-store-config.md#data-store-configurations).
1. Om instansen har klonats från en befintlig server måste du ta bort `clusterId` den nya instansen genom att använda det senaste ekkörningsverktyget när databasen är offline. Det kommando du behöver köra är:

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >Om en segmentnodbutik har konfigurerats måste databassökvägen anges. Som standard är banan `<aem-install-folder>/crx-quickstart/repository/segmentstore.` Om en dokumentnodbutik har konfigurerats kan du använda en [URI för Mongo-anslutningssträng](https://docs.mongodb.org/manual/reference/connection-string/).

   >[!NOTE]
   >
   >Du kan hämta verktyget för körning från följande plats:
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >Observera att olika versioner av verktyget måste användas beroende på vilken Oak-version du använder i AEM. Kontrollera listan över versionskrav innan du använder verktyget:
   >
   >
   >
   >    * För ekversioner **1.2.x** använd Oak-run **1.2.12 eller senare**
   >    * För ekversioner **nyare än ovan** använder du den version av Oak-run som matchar Oak Core i AEM.


1. Validera konfigurationen. För att göra detta måste du söka efter en unik fil som har lagts till i datalagret av varje databas som delar den. Filformatet är `repository-[UUID]`, där UUID är en unik identifierare för varje enskild databas.

   Därför bör en korrekt konfiguration ha så många unika filer som det finns databaser som delar datalagret.

   Filerna lagras på olika sätt beroende på datalagret:

   * För `FileDataStore` filerna skapas under rotsökvägen för datalagringsmappen.
   * För `S3DataStore` filerna skapas i den konfigurerade S3-bucket under `META` mapp.

## Azure Data Store {#azure-data-store}

AEM kan konfigureras för att lagra data i Microsoft Azure-lagringstjänst. Den använder `org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` PID för konfiguration.

Om du vill aktivera Azure-datalagrets funktioner måste ett funktionspaket som innehåller Azure Connector hämtas och installeras. Gå till [Adobe-databas](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/) och ladda ned den senaste versionen från 1.6.x-versionerna av funktionspaketet (till exempel com.adobe.granite.oak.azureblobconnector-1.6.3.zip).

>[!NOTE]
>
>När du använder AEM med tarMK lagras binärfiler som standard i FileDataStore. Om du vill använda tarMK med Azure DataStore måste du börja AEM med `crx3tar-nofds` runmode, till exempel:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

När du har hämtat den kan du installera och konfigurera Azure-anslutningen på följande sätt:

1. Extrahera innehållet i ZIP-filen för funktionspaketet till en tillfällig mapp.

1. Gå till den tillfälliga mappen och kopiera innehållet i `jcr_root/libs/system/install` till `<aem-install>crx-quickstart/install` mapp.
1. Om AEM redan har konfigurerats för att fungera med lagringen tar du bort alla befintliga konfigurationsfiler från `/crx-quickstart/install` innan du fortsätter. De filer som behöver tas bort är:

   ForMongoMK:

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   För tarMK:

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Återgå till den tillfälliga platsen där funktionspaketet har extraherats och kopiera innehållet i `jcr_root/libs/system/config` till `<aem-install>/crx-quickstart/install` mapp.
1. Redigera konfigurationsfilen och lägg till de konfigurationsalternativ som krävs för installationen.
1. Börja AEM.

Du kan använda konfigurationsfilen med följande alternativ:

* azureSas=&quot;&quot;: I version 1.6.3 av kopplingen lades stöd för Azure Shared Access Signature (SAS) till. **Om det finns både SAS- och lagringsuppgifter i konfigurationsfilen har SAS prioritet.** Mer information om SAS finns i [officiell dokumentation](https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1). Se till att tecknet &#39;=&#39; föregås av &#39;\=&#39;.

* azureBlobEndpoint=&quot;&quot;: Azure-blobslutpunkten. Till exempel https://&lt;storage-account>.blob.core.windows.net.
* accessKey=&quot;&quot;: Lagringskontots namn. Mer information om autentiseringsuppgifter för Microsoft Azure finns i [officiell dokumentation](https://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account).

* secretsKey=&quot;&quot;: Lagringsåtkomstnyckeln. Se till att tecknet &#39;=&#39; föregås av &#39;\=&#39;.
* container=&quot;&quot;: Microsoft Azure-lagringsbehållarens namn. Behållaren är en gruppering av en uppsättning blober. Mer information finns i [officiell dokumentation](https://msdn.microsoft.com/en-us/library/dd135715.aspx).
* maxConnections=&quot;&quot;: Antal samtidiga begäranden per åtgärd. Standardvärdet är 1.
* maxErrorRetry=&quot;&quot;: Antal återförsök per begäran. Standardvärdet är 3.
* socketTimeout=&quot;&quot;: Tidsgränsen i millisekunder som används för begäran. Standardvärdet är 5 minuter.

Förutom inställningarna ovan kan följande inställningar också konfigureras:

* sökväg: Datalagrets sökväg. Standardvärdet är `<aem-install>/repository/datastore.`
* RecordLength: Den minsta storleken för ett objekt som ska lagras i datalagret. Standardvärdet är 16 kB.
* maxCachedBinarySize: Binärfiler som är mindre än eller lika stora som den här storleken lagras i minnescachen. Storleken anges i byte. Standardvärdet är 17 408 (17 kB).
* cacheSize: Cachens storlek. Värdet anges i byte. Standardvärdet är 64 GB.
* hemlighet: Ska endast användas om binär replikering används för konfiguration av delade datalager.
* stagingSplitPercentage: Procentandel av cachestorleken som är konfigurerad att användas för att mellanlagra asynkrona överföringar. Standardvärdet är 10.
* uploadThreads: Antalet överförda trådar som används för asynkrona överföringar. Standardvärdet är 10.
* stagingPurgeInterval: Intervallet i sekunder för tömning av slutförda överföringar från mellanlagringscachen. Standardvärdet är 300 sekunder (5 minuter).
* stagingRetryInterval: Återförsöksintervallet i sekunder för misslyckade överföringar. Standardvärdet är 600 sekunder (10 minuter).

>[!NOTE]
>
>Alla inställningar ska anges mellan citattecken, till exempel:

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## Skräpinsamling för datalager {#data-store-garbage-collection}

Datalagrets skräpinsamlingsprocess används för att ta bort oanvända filer i datalagret, vilket frigör värdefullt diskutrymme.

Du kan köra skräpinsamling för datalager genom att:

1. Gå till JMX-konsolen på *https://&lt;serveraddress:port>/system/console/jmx*
1. Söker efter **RepositoryManagement.** När du har hittat Repository Manager MBean klickar du på det för att visa tillgängliga alternativ.
1. Bläddra till slutet av sidan och klicka på **startDataStoreGC(boolesk markOnly)** länk.
1. I följande dialogruta anger du `false` för `markOnly` parameter, klicka sedan på **Anropa**:

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >The `markOnly` parameter anger om svepfasen för skräpinsamlingen ska köras eller inte.

## Skräpinsamling för datalager för ett delat datalager {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>När du utför skräpinsamling i ett klustrat eller delat datalager (med mongo- eller segmentmål) kan loggen visa varningar om att vissa blob-ID inte kan tas bort. Detta beror på att blob-ID:n som tagits bort i en tidigare skräpinsamling felaktigt refereras igen av andra kluster eller delade noder som inte har information om ID-borttagningar. När skräpinsamlingen utförs loggas därför en varning när den försöker ta bort ett ID som redan har tagits bort i den senaste körningen. Det här beteendet påverkar inte prestanda eller funktioner.

>[!NOTE]
> Om du använder en delad datalagerinställning och datalagrets skräpinsamling är inaktiverad kan rensningen av Lucene-binärfilen plötsligt öka diskutrymmet som används. För att undvika detta måste du inaktivera BlobTracker på alla författare- och publiceringsinstanser enligt följande:
>
> 1. Stoppa AEM.
> 2. Lägg till `blobTrackSnapshotIntervalInSecs=L"0"` -parametern i `crx-quickstart/install/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` -fil. Den här parametern kräver Oak 1.12.0, 1.10.2 eller senare.
> 3. Starta om AEM.


Med senare versioner av AEM kan skräpinsamlingen i datalagret även köras på datalager som delas av mer än en databas. Gör så här för att kunna köra skräpinsamling i datalager på ett delat datalager:

1. Se till att alla underhållsuppgifter som konfigurerats för datalagrets skräpinsamling är inaktiverade för alla databasinstanser som delar datalagret.
1. Kör stegen som anges i [Binär skräpinsamling](/help/sites-deploying/data-store-config.md#data-store-garbage-collection) separat den **alla** databasinstanser som delar datalagret. Tänk dock på att `true` för `markOnly` innan du klickar på knappen Anropa:

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. När du har slutfört ovanstående procedur på alla instanser kör du skräpinsamlingen för datalagret igen från **alla** av förekomsterna:

   1. Gå till JMX-konsolen och välj Repository Manager Mbean.
   1. Klicka på **Klicka på startDataStoreGC (boolesk markOnly)** länk.
   1. I följande dialogruta anger du `false` för `markOnly` parametern igen.
   Då sorteras alla filer som hittas med markeringsfasen som använts tidigare och resten som inte används tas bort från datalagret.
