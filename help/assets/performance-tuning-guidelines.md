---
title: Prestandajustering för [!DNL Adobe Experience Manager Assets].
description: Förslag och vägledning [!DNL Experience Manager] om konfiguration, ändringar av maskinvara, programvara och nätverkskomponenter för att ta bort flaskhalsar och optimera prestanda för [!DNL Experience Manager Assets].
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 9a4ae73c08657195da2741cccdb196bd7f7142c9
workflow-type: tm+mt
source-wordcount: '2680'
ht-degree: 0%

---


<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] guide för prestandajustering {#assets-performance-tuning-guide}

En [!DNL Experience Manager Assets] konfiguration innehåller ett antal maskinvaru-, programvaru- och nätverkskomponenter. Beroende på ditt driftsättningsscenario kan du behöva specifika konfigurationsändringar för maskinvara, programvara och nätverkskomponenter för att ta bort flaskhalsar i prestandan.

Genom att identifiera och följa vissa riktlinjer för optimering av maskinvara och programvara kan ni dessutom skapa en stabil grund som gör att driftsättningen kan uppfylla förväntningarna på prestanda, skalbarhet och tillförlitlighet. [!DNL Experience Manager Assets]

Dåliga prestanda i [!DNL Experience Manager Assets] kan påverka användarupplevelsen kring interaktiva prestanda, bearbetning av resurser, nedladdningshastighet och andra områden.

Prestandaoptimering är en grundläggande uppgift som du utför innan du fastställer målvärden för ett projekt.

Här är några viktiga fokusområden där du kan identifiera och åtgärda prestandaproblem innan de påverkar användarna.

## Platform {#platform}

Experience Manager stöds på ett antal plattformar, men Adobe har funnit det bästa stödet för inbyggda verktyg i Linux och Windows, vilket ger optimala prestanda och förenklad implementering. Bäst är att du driftsätter ett 64-bitars operativsystem för att uppfylla de höga minneskraven för en [!DNL Experience Manager Assets] driftsättning. Precis som med andra Experience Manager-distributioner bör du implementera tarMK där det är möjligt. Även om TonaMK inte kan skalas bortom en enda författarinstans, fungerar det bättre än MongoMK. Du kan lägga till instanser för TjärMK-avlastning för att öka arbetsflödets bearbetningskraft i din [!DNL Experience Manager Assets] distribution.

### Tillfällig mapp {#temp-folder}

Om du vill förbättra överföringstiderna använder du högpresterande lagringsutrymme för den tillfälliga Java-katalogen. I Linux och Windows kan en RAM-enhet eller SSD användas. I molnbaserade miljöer kan en motsvarande typ av höghastighetslagring användas. I Amazon EC2 kan till exempel en [kortdisk](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) användas för den tillfälliga mappen.

Om servern har tillräckligt med minne konfigurerar du en RAM-enhet. Kör följande kommandon i Linux för att skapa en 8 GB RAM-enhet:

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

I Windows använder du en drivrutin från tredje part för att skapa en RAM-enhet eller bara använda lagring med höga prestanda, till exempel SSD.

När den tillfälliga volymen med höga prestanda är klar anger du JVM-parametern `-Djava.io.tmpdir`. Du kan till exempel lägga till JVM-parametern nedan till `CQ_JVM_OPTS` variabeln i `bin/start` skriptet för [!DNL Experience Manager]:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java-konfiguration {#java-configuration}

### Java-version {#java-version}

Adobe rekommenderar att man driftsätter [!DNL Experience Manager Assets] Java 8 för optimala prestanda.

<!-- TBD: Link to the latest official word around Java.
-->

### JVM-parametrar {#jvm-parameters}

Ange följande JVM-parametrar:

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## Datalagring och minneskonfiguration {#data-store-and-memory-configuration}

### Konfiguration av fillagring {#file-data-store-configuration}

Du bör separera datalagret från segmentlagret för alla [!DNL Experience Manager Assets] användare. Dessutom kan konfigurering av parametrarna `maxCachedBinarySize` och `cacheSizeInMB` hjälpa till att maximera prestandan. Ange `maxCachedBinarySize` den minsta filstorlek som kan sparas i cachen. Ange storleken på den minnescache som ska användas för datalagret i `cacheSizeInMB`. Adobe rekommenderar att du anger det här värdet mellan 2 och 10 procent av den totala stackstorleken. Inläsnings-/prestandatestning kan dock hjälpa till att fastställa den idealiska inställningen.

### Konfigurera maximal storlek för buffrad bildcache {#configure-the-maximum-size-of-the-buffered-image-cache}

När du överför stora mängder resurser till [!DNL Adobe Experience Manager], för att undvika oväntade förändringar i minnesanvändningen och för att förhindra att JVM misslyckas med OutOfMemoryErrors, ska du minska den konfigurerade maxstorleken för buffrat bildcache. Tänk dig ett exempel på att du har ett system med en högsta heap (- `Xmx`param) på 5 GB, en Oak BlobCache inställd på 1 GB och dokumentcache inställd på 2 GB. I det här fallet tar den buffrade cachen upp till 1,25 GB och minne, vilket innebär att endast 0,75 GB minne återstår för oväntade toppar.

Konfigurera den buffrade cachestorleken i OSGi-webbkonsolen. Vid `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`anger du egenskapen `cq.dam.image.cache.max.memory` i byte. 1073741824 är till exempel 1 GB (1 024 x 1 024 x 1 024 = 1 GB).

Om du använder en nod för att konfigurera den här egenskapen från Experience Manager 6.1 SP1 måste du ange datatypen till Long, om du använder en `sling:osgiConfig` nod. Mer information finns i [CQBufferedImageCache förbrukar heap under överföring](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html)av resurser.

### Gemensamma datalager {#shared-data-stores}

Implementering av ett S3- eller delat fildatalager kan bidra till att spara diskutrymme och öka nätverkets genomströmning i storskaliga implementeringar. Mer information om för- och nackdelar med att använda ett delat datalager finns i [Handboken](/help/assets/assets-sizing-guide.md)för resursstorlek.

### S3-datalager {#s-data-store}

Följande konfiguration ( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`) för S3-datalagret hjälpte Adobe att extrahera 12,8 TB binära stora objekt (BLOB) från ett befintligt arkiv av fildata till ett S3-datalager på en kundplats:

```conf
accessKey=<snip>
 secretKey=<snip>
 s3Bucket=<snip>
 s3Region=us-standard
 s3EndPoint=<a href="https://s3.amazonaws.com/">s3.amazonaws.com</a>
 connectionTimeout=120000
 socketTimeout=120000
 maxConnections=80
 writeThreads=60
 concurrentUploadsThreads=30
 asyncUploadLimit=30
 maxErrorRetry=1000
 path=/opt/author/crx-quickstart/repository/datastore
 s3RenameKeys=false
 s3Encryption=SSE_S3
 proactiveCaching=true
 uploadRetries=1000
 migrateFailuresCount=400
```

## Nätverksoptimering {#network-optimization}

Adobe rekommenderar att du aktiverar HTTPS eftersom många företag har brandväggar som fångar upp HTTP-trafik, vilket påverkar överföringar negativt och skadar filer. För stora filöverföringar måste användarna ha kabelanslutna anslutningar till nätverket eftersom ett WiFi-nätverk snabbt blir mättat. Riktlinjer för identifiering av flaskhalsar i nätverk finns i [Handboken](/help/assets/assets-sizing-guide.md)för resursstorlek. Information om hur du utvärderar nätverksprestanda genom att analysera nätverkstopologi finns i [Resurser för nätverksaspekter](/help/assets/assets-network-considerations.md).

Din nätverksoptimeringsstrategi är i första hand beroende av hur mycket bandbredd som är tillgänglig och hur stor belastning din [!DNL Experience Manager] instans har. Gemensamma konfigurationsalternativ, inklusive brandväggar och proxies, kan förbättra nätverkets prestanda. Här följer några viktiga saker att tänka på:

* Beroende på vilken instanstyp du har (liten, måttlig, stor) kontrollerar du att du har tillräcklig nätverksbandbredd för instansen Experience Manager. Lämplig bandbreddsallokering är särskilt viktig om AWS är värd [!DNL Experience Manager] .
* Om din [!DNL Experience Manager] instans finns på AWS kan du dra nytta av en mångsidig skalningspolicy. Överför instansen om användarna förväntar sig hög belastning. Minska storleken för måttlig/låg belastning.
* HTTPS: De flesta användare har brandväggar som tolkar HTTP-trafik, vilket kan påverka överföringen av filer negativt eller till och med skada filer under överföringen.
* Stora filöverföringar: Se till att användarna har kabelanslutna anslutningar till nätverket (WiFi-anslutningar blir snabbt mättade).

## Arbetsflöden {#workflows}

### Övergående arbetsflöden {#transient-workflows}

Ställ in arbetsflödet på Övergående när det är möjligt [!UICONTROL DAM Update Asset] . Inställningen minskar avsevärt de allmänna kostnader som krävs för att bearbeta arbetsflöden, eftersom arbetsflöden i det här fallet inte behöver passera genom de normala spårnings- och arkiveringsprocesserna.

1. Navigera till `/miscadmin` i [!DNL Experience Manager] distributionen på `https://[aem_server]:[port]/miscadmin`.

1. Expandera **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]** > **[!UICONTROL dam]**.

1. Öppna **[!UICONTROL DAM Update Asset]**. I den flytande verktygspanelen växlar du till **[!UICONTROL Page]** fliken och klickar sedan på **[!UICONTROL Page Properties]**.

1. Select **[!UICONTROL Transient Workflow]** and click **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Vissa funktioner har inte stöd för tillfälliga arbetsflöden. Om din [!DNL Assets] distribution kräver dessa funktioner ska du inte konfigurera tillfälliga arbetsflöden.

Om det inte går att använda tillfälliga arbetsflöden kör du regelbundet arbetsflödesrensning för att ta bort arkiverade [!UICONTROL DAM Update Asset] arbetsflöden så att systemprestanda inte försämras.

Vanligtvis kör du rensningsarbetsflödena varje vecka. I resurskrävande scenarier, till exempel vid omfattande tillgångsinmatning, kan du dock köra det oftare.

Om du vill konfigurera rensning av arbetsflöden lägger du till en ny Adobe Granite Workflow Renge-konfiguration via OSGi-konsolen. Konfigurera och schemalägg arbetsflödet som en del av veckounderhållsperioden.

Om tömningen är för lång så tar det för lång tid. Därför bör du se till att rensningsjobben är fullständiga för att undvika situationer där rensningsarbetsflödena misslyckas på grund av det stora antalet arbetsflöden.

Om du till exempel har kört flera icke-tillfälliga arbetsflöden (som skapar arbetsflödesinstansnoder) kan du köra [ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) på ad hoc-basis. Det tar bort överflödiga, slutförda arbetsflödesinstanser direkt i stället för att vänta på att schemaläggaren för rensning av arbetsflöde i Adobe ska köras.

### Maximalt antal parallella jobb {#maximum-parallel-jobs}

Som standard [!DNL Experience Manager] körs ett maximalt antal parallella jobb som är lika med antalet processorer på servern. Problemet med den här inställningen är att under perioder med hög belastning så hanteras alla processorer av [!UICONTROL DAM Update Asset] arbetsflöden, vilket gör att användargränssnittet tar längre tid och förhindrar [!DNL Experience Manager] att andra processer som skyddar serverns prestanda och stabilitet körs. Det är en god vana att ange det här värdet till hälften av de processorer som är tillgängliga på servern genom att utföra följande steg:

1. Gå till [!DNL Experience Manager] Author `https://[aem_server]:[port]/system/console/slingevent`.

1. Klicka **[!UICONTROL Edit]** på varje arbetsflödeskö som är relevant för implementeringen, till exempel **[!UICONTROL Granite Transient Workflow Queue]**.

1. Uppdatera värdet för **[!UICONTROL Maximum Parallel Jobs]** och klicka **[!UICONTROL Save]**.

Att ställa in en kö på hälften av de tillgängliga processorerna är en användbar lösning att börja med. Du kan dock behöva öka eller minska det här antalet för att få maximal genomströmning och justera det efter miljö. Det finns separata köer för tillfälliga och icke-tillfälliga arbetsflöden samt andra processer, till exempel externa arbetsflöden. Om flera köer är inställda på 50 % av processorerna aktiva samtidigt kan systemet snabbt bli överbelastat. De köer som används ofta varierar mycket mellan olika implementeringar. Därför kan du behöva konfigurera dem noggrant för maximal effektivitet utan att ge avkall på serverstabiliteten.

### DAM-uppdateringskonfiguration {#dam-update-asset-configuration}

Arbetsflödet innehåller en komplett serie steg som är konfigurerade för uppgifter, till exempel generering och [!UICONTROL DAM Update Asset] [!DNL Adobe InDesign Server] integrering av Scene7 PTIFF. De flesta användare behöver dock inte utföra flera av dessa steg. Adobe rekommenderar att du skapar en anpassad kopia av arbetsflödesmodellen och tar bort alla onödiga steg. [!UICONTROL DAM Update Asset] I det här fallet uppdaterar du startarna [!UICONTROL DAM Update Asset] så att de pekar på den nya modellen.

Om du kör arbetsflödet intensivt kan du öka storleken på fildatalagret avsevärt. [!UICONTROL DAM Update Asset] Resultaten från ett experiment som utfördes av Adobe har visat att datastorleken kan öka med ungefär 400 GB om cirka 500 arbetsflöden utförs inom 8 timmar.

Det är en tillfällig ökning och datalagret återställs till den ursprungliga storleken när du har kört skräpinsamlingsaktiviteten för datalagret.

Vanligtvis körs skräpinsamlingsaktiviteten för datalager varje vecka tillsammans med andra schemalagda underhållsaktiviteter.

Om du har begränsat diskutrymme och kör [!UICONTROL DAM Update Asset] arbetsflöden intensivt bör du överväga att schemalägga skräpinsamlingen oftare.

#### Generering av rendering vid körning {#runtime-rendition-generation}

Kunderna använder bilder av olika storlek och format på sin webbplats eller för att distribuera dem till affärspartners. Eftersom varje återgivning ökar utrymmet i databasen rekommenderar Adobe att du använder den här funktionen med gott omdöme. Om du vill minska mängden resurser som behövs för att bearbeta och lagra bilder kan du generera dessa bilder vid körning i stället för som återgivningar vid importen.

Många webbplatskunder implementerar en bildservett som ändrar storlek på och beskär bilder när de begärs, vilket medför ytterligare belastning på publiceringsinstansen. Så länge dessa bilder kan cachas kan utmaningen dock mildras.

Ett annat sätt är att använda Scene7-teknik för att helt och hållet överge bildbearbetning. Dessutom kan ni distribuera varumärkesportalen som inte bara tar över ansvaret för att skapa renderingar från [!DNL Experience Manager] infrastrukturen, utan även hela publiceringsnivån.

#### ImageMagick {#imagemagick}

Om du anpassar arbetsflödet för att generera återgivningar med ImageMagick rekommenderar Adobe att du ändrar [!UICONTROL DAM Update Asset] filen i `policy.xml` `/etc/ImageMagick/`. Som standard använder ImageMagick hela det tillgängliga diskutrymmet på operativsystemsvolymen och det tillgängliga minnet. Gör följande konfigurationsändringar i `policymap` avsnittet av för `policy.xml` att begränsa resurserna.

```xml
<policymap>
  <!-- <policy domain="system" name="precision" value="6"/> -->
  <policy domain="resource" name="temporary-path" value="/ephemeral0/imagemagick_tmp"/>
  <policy domain="resource" name="memory" value="1000MiB"/>
  <policy domain="resource" name="map" value="1000MiB"/>
  <!-- <policy domain="resource" name="area" value="1gb"/> -->
  <policy domain="resource" name="disk" value="10000MiB"/>
  <!-- <policy domain="resource" name="file" value="768"/> -->
  <policy domain="resource" name="thread" value="1"/>
  <policy domain="resource" name="throttle" value="50"/>
  <!-- <policy domain="resource" name="time" value="3600"/> -->
</policymap>
```

Dessutom anger du sökvägen till ImageMagick:s tillfälliga mapp i `configure.xml` filen (eller genom att ange miljövariabeln `MAGIC_TEMPORARY_PATH`) till en diskpartition som har tillräckligt med utrymme och IOPS.

>[!CAUTION]
>
>En felaktig konfiguration kan göra servern instabil om ImageMagick använder allt tillgängligt diskutrymme. De principändringar som krävs för att bearbeta stora filer med ImageMagick kan påverka prestandan i [!DNLEExperience Manager] . Mer information finns i [Installera och konfigurera ImageMagick](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>ImageMagick `policy.xml` - och `configure.xml` -filerna är tillgängliga `/usr/lib64/ImageMagick-&#42;/config/` i stället för `/etc/ImageMagick/`.Mer information om var konfigurationsfilerna finns i [dokumentationen](https://www.imagemagick.org/script/resources.php) till ImageMagick.

Om du använder Adobe Managed Services (AMS) kan du kontakta Adobe kundtjänst om du tänker bearbeta många stora PSD- eller PSB-filer. [!DNL Experience Manager] Samarbeta med Adobe kundtjänstrepresentant för att implementera de bästa metoderna för driftsättningen av AMS och för att välja bästa möjliga verktyg och modeller för Adobe egna format. [!DNL Experience Manager] kan inte bearbeta PSB-filer med hög upplösning som är större än 30000 x 23000 pixlar.

### XMP {#xmp-writeback}

XMP återföring uppdaterar originalresursen när metadata ändras i [!DNL Experience Manager], vilket ger följande resultat:

* Själva tillgången ändras
* En version av resursen skapas
* [!UICONTROL DAM Update Asset] körs mot resursen

De listade resultaten kräver stora resurser. Adobe rekommenderar därför att du [inaktiverar XMP](https://helpx.adobe.com/experience-manager/kb/disable-xmp-writeback.html)återskrivning, om det inte behövs.

Om du importerar en stor mängd metadata kan det leda till resurskrävande XMP återskrivningsaktivitet om körningsarbetsflödesflaggan är markerad. Planera en sådan import under begränsad serveranvändning så att prestanda för andra användare inte påverkas.

## Replikering {#replication}

När du replikerar resurser till ett stort antal publiceringsinstanser, till exempel i en webbplatsimplementering, rekommenderar Adobe att du använder kedjereplikering. I det här fallet replikeras författarinstansen till en enda publiceringsinstans som i sin tur replikeras till de andra publiceringsinstanserna och frigör författarinstansen.

### Konfigurera kedjereplikering {#configure-chain-replication}

1. Välj vilken publiceringsinstans du vill använda för att länka replikeringarna till
1. På den publiceringsinstansen lägger du till replikeringsagenter som pekar på andra publiceringsinstanser
1. På var och en av dessa replikeringsagenter aktiverar du&quot;Vid mottagning&quot; på fliken&quot;Utlösare&quot;

>[!NOTE]
>
>Adobe rekommenderar inte att resurser aktiveras automatiskt. Om det behövs rekommenderar Adobe att du gör detta som det sista steget i ett arbetsflöde, vanligtvis DAM-uppdateringsresurs.

## Sökindex {#search-indexes}

Se till att du implementerar de senaste Service Pack-uppdateringarna och prestandarelaterade snabbkorrigeringar eftersom de ofta innehåller uppdateringar av systemindex. Se [Prestandajusteringstips](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) för vissa indexoptimeringar.

Skapa anpassade index för frågor som du kör ofta. Mer information finns i [metod för att analysera långsamma frågor](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) och [skapa anpassade index](/help/sites-deploying/queries-and-indexing.md). Mer information om de effektivaste strategierna för frågor och index finns i [Bästa metoder för frågor och indexering](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Lucene-indexkonfigurationer {#lucene-index-configurations}

Vissa optimeringar kan göras för Oak-indexkonfigurationer som kan förbättra [!DNL Experience Manager Assets] prestandan. Uppdatera indexkonfigurationerna för att förbättra omindexeringstiden:

1. Öppna CRXDe `/crx/de/index.jsp` och logga in som administrativ användare.
1. Bläddra till `/oak:index/lucene`.
1. Lägg till en `String[]` egenskap `excludedPaths` med värdena `/var`, `/etc/workflow/instances`och `/etc/replication`.
1. Bläddra till `/oak:index/damAssetLucene`. Lägg till en `String[]` egenskap `includedPaths` med ett värde `/content/dam`. Spara ändringar.

Om dina användare inte behöver göra fulltextsökning av resurser, till exempel söka igenom text i PDF-dokument, kan du inaktivera det. Du förbättrar indexets prestanda genom att inaktivera fulltextindexering. Så här inaktiverar du [!DNL Apache Lucene] textrahering:

1. I [!DNL Experience Manager] gränssnittet, åtkomst [!UICONTROL Package Manager].
1. Överför och installera det paket som finns på [disable_indexingbinarytextextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### Gissa totalt {#guess-total}

När du skapar frågor som genererar stora resultatuppsättningar bör du använda parametern för att undvika att använda mycket minne när du kör dem. `guessTotal`

## Known issues {#known-issues}

### Stora filer {#large-files}

Det finns två stora kända fel som rör stora filer i [!DNL Experience Manager]. När filer når större storlekar än 2 GB kan synkronisering med kalla väntelägen hamna i en situation där minnet är slut. I vissa fall förhindras att standby-synkronisering körs. I andra fall kraschar den primära instansen. Detta scenario gäller för alla filer i [!DNL Experience Manager] som är större än 2 GB, inklusive innehållspaket.

På samma sätt kan det ta lite tid innan filen är helt beständig från cachen till filsystemet om filen är 2 GB stor när ett delat S3-datalager används. Detta innebär att om du använder en binär replikering utan binärfiler kan det hända att binära data inte har befunnits beständiga innan replikeringen slutförs. Denna situation kan leda till problem, särskilt om datatillgängligheten är viktig.

## Prestandatestning {#performance-testing}

För varje [!DNL Experience Manager] driftsättning måste ni skapa ett system för prestandatestning som snabbt kan identifiera och lösa flaskhalsar. Här är några nyckelområden att fokusera på.

### Nätverkstestning {#network-testing}

Utför följande uppgifter för alla problem med nätverkets prestanda från kunden:

* Testa nätverksprestanda inifrån kundens nätverk
* Testa nätverksprestanda inifrån Adobe-nätverket. För AMS-kunder kan du arbeta med din CSE för att testa inifrån Adobe-nätverket.
* Testa nätverksprestanda från en annan åtkomstpunkt
* Genom att använda ett prestandatest för nätverk
* Testa mot dispatchern

### [!DNL Experience Manager] driftsättningstest {#aem-deployment-testing}

För att minimera latens och uppnå hög genomströmning genom effektiv processoranvändning och lastdelning ska du regelbundet övervaka prestanda för din [!DNL Experience Manager] driftsättning. Särskilt gäller följande:

* Kör lasttester mot [!DNL Experience Manager] distributionen.
* Övervaka uppladdningsprestanda och användargränssnittets svarstider.

## [!DNL Experience Manager Assets] resultatchecklista och påverkan av tillgångshanteringsåtgärder {#checklist}

* Gör det möjligt för HTTPS att kringgå alla HTTP-trafiksniffare på företag.
* Använd en kabelanslutning för överföring av stora resurser.
* Driftsätt med Java 8.
* Ange optimala JVM-parametrar.
* Konfigurera ett datalager i filsystemet eller ett S3-datalager.
* Inaktivera generering av underresurser. Om det är aktiverat skapar AEM en separat resurs för varje sida i en flersidig resurs. Var och en av dessa sidor är en enskild resurs som förbrukar mer diskutrymme, kräver versionshantering och ytterligare arbetsflödesbearbetning. Om du inte behöver separata sidor inaktiverar du generering av delresurser och sidextrahering.
* Möjliggör tillfälliga arbetsflöden.
* Justera Granite-arbetsflödesköerna för att begränsa antalet samtidiga jobb.
* Konfigurera [!DNL ImageMagick] för att begränsa resursförbrukning.
* Ta bort onödiga steg från [!UICONTROL DAM Update Asset] arbetsflödet.
* Konfigurera arbetsflöde och versionsrensning.
* Optimera index med de senaste servicepaketen och snabbkorrigeringarna. Kontakta Adobe kundtjänst om du har ytterligare indexoptimeringar som kan vara tillgängliga.
* Använd gissningTotal för att optimera frågeprestanda.
* If you configure [!DNL Experience Manager] to detect file types from the content of the files (by enabling **[!UICONTROL Day CQ DAM Mime Type Service]** in the **[!UICONTROL AEM Web Console]**), upload many files in bulk during non-peak hours as it is resource-intensive.
