---
title: Prestandajustering [!DNL Assets].
description: Förslag och vägledning om [!DNL Experience Manager] konfiguration, ändringar av maskinvara, programvara och nätverkskomponenter för att ta bort flaskhalsar och optimera prestanda för [!DNL Experience Manager Assets].
contentOwner: AG
mini-toc-levels: 1
role: Architect, Admin
feature: Asset Management
exl-id: 1d9388de-f601-42bf-885b-6a7c3236b97e
source-git-commit: e3caa3e3067cf5e29cfcdf4286047eb346aefa23
workflow-type: tm+mt
source-wordcount: '2687'
ht-degree: 0%

---

<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] guide för prestandajustering {#assets-performance-tuning-guide}

An [!DNL Experience Manager Assets] installationen innehåller ett antal maskinvaru-, programvaru- och nätverkskomponenter. Beroende på ditt driftsättningsscenario kan du behöva specifika konfigurationsändringar för maskinvara, programvara och nätverkskomponenter för att ta bort flaskhalsar i prestandan.

Genom att identifiera och följa vissa riktlinjer för optimering av maskinvara och programvara kan du dessutom skapa en stabil grund som gör att [!DNL Experience Manager Assets] driftsättning för att uppfylla förväntningarna om prestanda, skalbarhet och tillförlitlighet.

Dåliga prestanda i [!DNL Experience Manager Assets] kan påverka användarupplevelsen kring interaktiva prestanda, bearbetning av resurser, nedladdningshastighet och andra områden.

Prestandaoptimering är en grundläggande uppgift som du utför innan du fastställer målvärden för ett projekt.

Här är några viktiga fokusområden där du kan identifiera och åtgärda prestandaproblem innan de påverkar användarna.

## Plattform {#platform}

Experience Manager stöds på ett antal plattformar, men Adobe har funnit det bästa stödet för inbyggda verktyg i Linux och Windows, vilket ger optimala prestanda och förenklad implementering. Bäst är att du driftsätter ett 64-bitars operativsystem för att uppfylla de höga minneskraven i en [!DNL Experience Manager Assets] distribution. Precis som med andra Experience Manager-distributioner bör du implementera tarMK där det är möjligt. Även om TonaMK inte kan skalas bortom en enda författarinstans, fungerar det bättre än MongoMK. Du kan lägga till instanser för TjärtMK-avlastning för att öka arbetsflödets bearbetningskraft [!DNL Experience Manager Assets] distribution.

### Tillfällig mapp {#temp-folder}

Om du vill förbättra överföringstiderna använder du högpresterande lagringsutrymme för den tillfälliga Java-katalogen. I Linux och Windows kan en RAM-enhet eller SSD användas. I molnbaserade miljöer kan en motsvarande typ av höghastighetslagring användas. I Amazon EC2 kan du till exempel [kortdisk](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) kan användas för den tillfälliga mappen.

Om servern har tillräckligt med minne konfigurerar du en RAM-enhet. Kör följande kommandon i Linux för att skapa en 8 GB RAM-enhet:

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

I Windows använder du en drivrutin från tredje part för att skapa en RAM-enhet eller bara använda lagring med höga prestanda, till exempel SSD.

När den tillfälliga volymen med höga prestanda är klar anger du JVM-parametern `-Djava.io.tmpdir`. Du kan till exempel lägga till JVM-parametern nedan i `CQ_JVM_OPTS` variabeln i `bin/start` skript för [!DNL Experience Manager]:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java-konfiguration {#java-configuration}

### Java-version {#java-version}

Adobe rekommenderar driftsättning [!DNL Experience Manager Assets] på Java 8 för optimala prestanda.

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

Du bör separera datalagret från segmentlagret för alla [!DNL Experience Manager Assets] -användare. Dessutom konfigurerar `maxCachedBinarySize` och `cacheSizeInMB` parametrar kan maximera prestanda. Ange `maxCachedBinarySize` till den minsta filstorlek som kan sparas i cachen. Ange storleken på den minnescache som ska användas för datalagret i `cacheSizeInMB`. Adobe rekommenderar att du anger det här värdet mellan 2 och 10 procent av den totala stackstorleken. Inläsnings-/prestandatestning kan dock hjälpa till att fastställa den idealiska inställningen.

### Konfigurera maximal storlek för buffrad bildcache {#configure-the-maximum-size-of-the-buffered-image-cache}

Vid överföring av stora mängder resurser till [!DNL Adobe Experience Manager], för att tillåta oväntade toppar i minnesanvändningen och för att förhindra att JVM misslyckas med OutOfMemoryErrors, ska du minska den konfigurerade maxstorleken för buffrat bildcache. Tänk dig ett exempel på att du har ett system med en maximal heap (- `Xmx`param) på 5 GB, en Oak BlobCache inställd på 1 GB och dokumentcache inställd på 2 GB. I det här fallet tar den buffrade cachen upp till 1,25 GB och minne, vilket innebär att endast 0,75 GB minne återstår för oväntade toppar.

Konfigurera den buffrade cachestorleken i OSGi-webbkonsolen. At `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`, ange egenskapen `cq.dam.image.cache.max.memory` i byte. 1073741824 är till exempel 1 GB (1 024 x 1 024 x 1 024 = 1 GB).

Från Experience Manager 6.1 SP1, om du använder en `sling:osgiConfig` nod för att konfigurera den här egenskapen måste du ange datatypen Long. Mer information finns i [CQBufferedImageCache förbrukar heap under överföring av tillgångar](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html).

### Gemensamma datalager {#shared-data-stores}

Implementering av ett S3- eller delat fildatalager kan bidra till att spara diskutrymme och öka nätverkets genomströmning i storskaliga implementeringar. Mer information om för- och nackdelar med att använda ett delat datalager finns i [Guide för resursstorlek](/help/assets/assets-sizing-guide.md).

### S3-datalager {#s-data-store}

Följande konfiguration för S3-datalagret ( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`) hjälpte Adobe att extrahera 12,8 TB binära stora objekt (BLOB) från en befintlig fillagring till ett S3-datalager på en kunds webbplats:

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

Adobe rekommenderar att du aktiverar HTTPS eftersom många företag har brandväggar som fångar upp HTTP-trafik, vilket påverkar överföringar negativt och skadar filer. För stora filöverföringar måste användarna ha kabelanslutna anslutningar till nätverket eftersom ett WiFi-nätverk snabbt blir mättat. Riktlinjer för att identifiera flaskhalsar i nätverket finns i [Guide för resursstorlek](/help/assets/assets-sizing-guide.md). Information om hur du utvärderar nätverksprestanda genom att analysera nätverkstopologi finns i [Resurser för nätverksaspekter](/help/assets/assets-network-considerations.md).

Din nätverksoptimeringsstrategi är i första hand beroende av hur mycket bandbredd som är tillgänglig och belastningen på din [!DNL Experience Manager] -instans. Gemensamma konfigurationsalternativ, inklusive brandväggar och proxies, kan förbättra nätverkets prestanda. Här följer några viktiga punkter att tänka på:

* Beroende på vilken instanstyp du har (liten, måttlig, stor) kontrollerar du att du har tillräcklig nätverksbandbredd för instansen Experience Manager. Lämplig bandbreddsallokering är särskilt viktig om [!DNL Experience Manager] ligger hos AWS.
* Om [!DNL Experience Manager] som finns på AWS kan du dra nytta av en mångsidig skalningspolicy. Överför instansen om användarna förväntar sig hög belastning. Minska storleken för måttlig/låg belastning.
* HTTPS: De flesta användare har brandväggar som tolkar HTTP-trafik, vilket kan påverka överföringen av filer negativt eller till och med skada filer under överföringen.
* Stora filöverföringar: Kontrollera att användarna har kabelanslutna anslutningar till nätverket (WiFi-anslutningar blir snabbt mättade).

## Arbetsflöden {#workflows}

### Övergående arbetsflöden {#transient-workflows}

Ange [!UICONTROL DAM Update Asset] till Transient. Inställningen minskar avsevärt de allmänna kostnader som krävs för att bearbeta arbetsflöden, eftersom arbetsflöden i det här fallet inte behöver passera genom de normala spårnings- och arkiveringsprocesserna.

1. Navigera till `/miscadmin` i [!DNL Experience Manager] distribution på `https://[aem_server]:[port]/miscadmin`.

1. Expandera **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]** > **[!UICONTROL dam]**.

1. Öppna **[!UICONTROL DAM Update Asset]**. Växla från den flytande verktygspanelen till **[!UICONTROL Page]** och sedan klicka på **[!UICONTROL Page Properties]**.

1. Välj **[!UICONTROL Transient Workflow]** och klicka **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Vissa funktioner har inte stöd för tillfälliga arbetsflöden. Om [!DNL Assets] för distribution krävs dessa funktioner, konfigurera inte tillfälliga arbetsflöden.

Om tillfälliga arbetsflöden inte kan användas kör du regelbundet arbetsflödesrensning för att ta bort arkiverade [!UICONTROL DAM Update Asset] arbetsflöden för att säkerställa att systemprestanda inte försämras.

Vanligtvis kör du rensningsarbetsflödena varje vecka. I resurskrävande scenarier, till exempel vid omfattande tillgångsinmatning, kan du dock köra det oftare.

Om du vill konfigurera rensning av arbetsflöden lägger du till en ny Adobe Granite Workflow Renge-konfiguration via OSGi-konsolen. Konfigurera och schemalägg arbetsflödet som en del av veckounderhållsperioden.

Om tömningen är för lång så tar det för lång tid. Därför bör du se till att rensningsjobben är fullständiga för att undvika situationer där rensningsarbetsflödena misslyckas på grund av det stora antalet arbetsflöden.

När du har utfört flera icke-tillfälliga arbetsflöden (som skapar arbetsflödesinstansnoder) kan du till exempel köra [ACS AEM Commands Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) på ad hoc-basis. Det tar bort överflödiga, slutförda arbetsflödesinstanser direkt i stället för att vänta på att schemaläggaren för rensning av arbetsflöde i Adobe ska köras.

### Maximalt antal parallella jobb {#maximum-parallel-jobs}

Som standard [!DNL Experience Manager] kör ett maximalt antal parallella jobb som är lika med antalet processorer på servern. Problemet med den här inställningen är att under perioder med hög belastning används alla processorer av [!UICONTROL DAM Update Asset] arbetsflöden, minska svarstiderna i användargränssnittet och förhindra [!DNL Experience Manager] från att köra andra processer som skyddar serverns prestanda och stabilitet. Det är en god vana att ange det här värdet till hälften av de processorer som är tillgängliga på servern genom att utföra följande steg:

1. På [!DNL Experience Manager] Författare, åtkomst `https://[aem_server]:[port]/system/console/slingevent`.

1. Klicka **[!UICONTROL Edit]** på varje arbetsflödeskö som är relevant för implementeringen, till exempel **[!UICONTROL Granite Transient Workflow Queue]**.

1. Uppdatera värdet för **[!UICONTROL Maximum Parallel Jobs]** och klicka **[!UICONTROL Save]**.

Att ställa in en kö på hälften av de tillgängliga processorerna är en användbar lösning att börja med. Du kan dock behöva öka eller minska det här antalet för att få maximal genomströmning och justera det efter miljö. Det finns separata köer för tillfälliga och icke-tillfälliga arbetsflöden samt andra processer, till exempel externa arbetsflöden. Om flera köer är inställda på 50 % av processorerna aktiva samtidigt kan systemet snabbt bli överbelastat. De köer som används ofta varierar mycket mellan olika implementeringar. Därför kan du behöva konfigurera dem noggrant för maximal effektivitet utan att ge avkall på serverstabiliteten.

### DAM-uppdateringskonfiguration {#dam-update-asset-configuration}

The [!UICONTROL DAM Update Asset] arbetsflödet innehåller en komplett serie steg som är konfigurerade för uppgifter, t.ex. generering av Dynamic Media PTIFF och [!DNL Adobe InDesign Server] integrering. De flesta användare behöver dock inte utföra flera av dessa steg. Adobe rekommenderar att du skapar en anpassad kopia av [!UICONTROL DAM Update Asset] arbetsflödesmodell och ta bort onödiga steg. I det här fallet uppdaterar du startprogrammet för [!UICONTROL DAM Update Asset] för att peka på den nya modellen.

Kör [!UICONTROL DAM Update Asset] arbetsflödet kan kraftigt öka storleken på filens datalager. Resultaten från ett experiment som utfördes av Adobe har visat att datastorleken kan öka med ungefär 400 GB om cirka 500 arbetsflöden utförs inom 8 timmar.

Det är en tillfällig ökning och datalagret återställs till den ursprungliga storleken när du har kört skräpinsamlingsaktiviteten för datalagret.

Vanligtvis körs skräpinsamlingsaktiviteten för datalager varje vecka tillsammans med andra schemalagda underhållsaktiviteter.

Om du har begränsat diskutrymme och kör [!UICONTROL DAM Update Asset] arbetsflöden intensivt bör du överväga att schemalägga skräpinsamlingen oftare.

#### Generering av rendering vid körning {#runtime-rendition-generation}

Kunderna använder bilder av olika storlek och format på sin webbplats eller för att distribuera dem till affärspartners. Eftersom varje återgivning ökar utrymmet i databasen rekommenderar Adobe att du använder den här funktionen med gott omdöme. Om du vill minska mängden resurser som behövs för att bearbeta och lagra bilder kan du generera dessa bilder vid körning i stället för som återgivningar vid importen.

Många webbplatskunder implementerar en bildservett som ändrar storlek på och beskär bilder när de begärs, vilket medför ytterligare belastning på publiceringsinstansen. Så länge dessa bilder kan cachas kan utmaningen dock mildras.

Ett annat sätt är att använda Dynamic Media-teknik för att helt och hållet överlåta bildbearbetning. Dessutom kan du driftsätta Brand Portal som inte bara tar över ansvaret för återgivningsgenerering från [!DNL Experience Manager] infrastruktur, men också hela publiceringsnivån.

#### ImageMagick {#imagemagick}

Om du anpassar [!UICONTROL DAM Update Asset] arbetsflöde för att generera återgivningar med ImageMagick, Adobe rekommenderar att du ändrar `policy.xml` fil på `/etc/ImageMagick/`. Som standard använder ImageMagick hela det tillgängliga diskutrymmet på operativsystemsvolymen och det tillgängliga minnet. Gör följande konfigurationsändringar i `policymap` avsnitt i `policy.xml` för att begränsa dessa resurser.

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

Dessutom anger du sökvägen till den tillfälliga mappen för ImageMagick i `configure.xml` fil (eller genom att ställa in miljövariabeln `MAGICK_TEMPORARY_PATH`) till en diskpartition som har tillräckligt med utrymme och IOPS.

>[!CAUTION]
>
>En felaktig konfiguration kan göra servern instabil om ImageMagick använder allt tillgängligt diskutrymme. De principändringar som krävs för att bearbeta stora filer med ImageMagick kan påverka [!DNL Experience Manager] prestanda. Mer information finns i [installera och konfigurera ImageMagick](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>ImageMagick `policy.xml` och `configure.xml` filer finns på `/usr/lib64/ImageMagick-&#42;/config/` i stället för `/etc/ImageMagick/`.Se [ImageMagick-dokumentation](https://www.imagemagick.org/script/resources.php) för platsen för konfigurationsfilerna.

Om du använder [!DNL Experience Manager] om du planerar att bearbeta stora PSD- eller PSB-filer på Adobe Managed Services (AMS) kan du kontakta Adobe kundsupport. Samarbeta med Adobe kundsupportrepresentant för att implementera de bästa metoderna för driftsättningen av AMS och för att välja de bästa möjliga verktygen och modellerna för Adobe egna format. [!DNL Experience Manager] kan inte bearbeta PSB-filer med hög upplösning som är större än 30000 x 23000 pixlar.

### XMP {#xmp-writeback}

XMP återföring uppdaterar originalresursen när metadata ändras i [!DNL Experience Manager], vilket ger följande resultat:

* Själva tillgången ändras
* En version av resursen skapas
* [!UICONTROL DAM Update Asset] körs mot resursen

De listade resultaten kräver stora resurser. Adobe rekommenderar därför att XMP avaktiveras om det inte behövs. Mer information finns i [XMP](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/xmp-writeback.html).

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

Installera [senaste Service Pack](/help/release-notes/release-notes.md) och prestandarelaterade snabbkorrigeringar, eftersom de ofta innehåller uppdateringar av systemindex. Se [tips för prestandajustering](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/performance-tuning-guidelines.html?lang=en) för vissa indexoptimeringar.

Skapa anpassade index för frågor som du kör ofta. Mer information finns i [metod för att analysera långsamma frågor](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) och [skapa egna index](/help/sites-deploying/queries-and-indexing.md). Mer information om metodtips för frågor och index finns i [Metodtips för frågor och indexering](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Lucene-indexkonfigurationer {#lucene-index-configurations}

Vissa optimeringar kan göras för Oak-indexkonfigurationer som kan förbättra [!DNL Experience Manager Assets] prestanda. Uppdatera indexkonfigurationerna för att förbättra omindexeringstiden:

1. Öppna CRXDe `/crx/de/index.jsp` och logga in som administrativ användare.
1. Bläddra till `/oak:index/lucene`.
1. Lägg till en `String[]` property `excludedPaths` med värden `/var`, `/etc/workflow/instances`och `/etc/replication`.
1. Bläddra till `/oak:index/damAssetLucene`. Lägg till en `String[]` property `includedPaths` med värde `/content/dam`. Spara ändringar.

Om dina användare inte behöver göra fulltextsökning av resurser, till exempel söka igenom text i PDF-dokument, kan du inaktivera det. Du förbättrar indexets prestanda genom att inaktivera fulltextindexering. Inaktivera [!DNL Apache Lucene] textrahering, följ dessa steg:

1. I [!DNL Experience Manager] gränssnitt, åtkomst [!UICONTROL Package Manager].
1. Överför och installera det paket som finns på [disable_indexingbinarytextextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### Gissa totalt {#guess-total}

När du skapar frågor som genererar stora resultatuppsättningar använder du `guessTotal` så att du slipper använda mycket minne när du kör dem.

## Kända fel {#known-issues}

### Stora filer {#large-files}

Det finns två viktiga kända problem med stora filer i [!DNL Experience Manager]. När filer når större storlekar än 2 GB kan synkronisering med vänteläge i kallt läge hamna i en situation där minnet är slut. I vissa fall förhindras att standby-synkronisering körs. I andra fall kraschar den primära instansen. Detta scenario gäller alla filer i [!DNL Experience Manager] som är större än 2 GB, inklusive innehållspaket.

På samma sätt kan det ta lite tid innan filen är helt beständig från cachen till filsystemet om filen är 2 GB stor när ett delat S3-datalager används. Detta innebär att om du använder en binär replikering utan binärfiler kan det hända att binära data inte har befunnits beständiga innan replikeringen slutförs. Denna situation kan leda till problem, särskilt om datatillgängligheten är viktig.

## Prestandatestning {#performance-testing}

För varje [!DNL Experience Manager] driftsättning, upprätta ett system för prestandatestning som snabbt kan identifiera och lösa flaskhalsar. Här är några nyckelområden att fokusera på.

### Nätverkstestning {#network-testing}

Utför följande uppgifter för alla problem med nätverkets prestanda från kunden:

* Testa nätverksprestanda inifrån kundens nätverk
* Testa nätverksprestanda inifrån Adobe-nätverket. För AMS-kunder kan du arbeta med din CSE för att testa inifrån Adobe-nätverket.
* Testa nätverksprestanda från en annan åtkomstpunkt
* Genom att använda ett prestandatest för nätverk
* Testa mot dispatchern

### [!DNL Experience Manager] driftsättningstest {#aem-deployment-testing}

För att minimera latens och uppnå hög genomströmning genom effektiv processoranvändning och lastdelning bör du övervaka prestandan hos [!DNL Experience Manager] regelbundet. Särskilt gäller följande:

* Kör belastningstester mot [!DNL Experience Manager] distribution.
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
* Ta bort onödiga steg från [!UICONTROL DAM Update Asset] arbetsflöde.
* Konfigurera arbetsflöde och versionsrensning.
* Optimera index med de senaste Service Pack-uppdateringarna och snabbkorrigeringarna. Kontakta Adobe kundsupport för eventuella ytterligare indexoptimeringar.
* Använd gissningTotal för att optimera frågeprestanda.
* Om du konfigurerar [!DNL Experience Manager] för att identifiera filtyper från filinnehållet (genom att aktivera **[!UICONTROL Day CQ DAM Mime Type Service]** i **[!UICONTROL AEM Web Console]**) kan du överföra många filer samtidigt under icke-toppvärdesdagar eftersom det är resurskrävande.
