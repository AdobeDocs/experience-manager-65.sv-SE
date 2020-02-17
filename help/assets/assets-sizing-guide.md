---
title: Guide för resursstorlek
description: Bästa metoder för att fastställa effektiva mätvärden för att uppskatta den infrastruktur och de resurser som krävs för att driftsätta AEM Assets.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 70a88085a0fd6e949974aa7f1f92fdc3def3d98e

---


# Guide för resursstorlek {#assets-sizing-guide}

När du ändrar storlek på miljön för en implementering av Adobe Experience Manager-resurser (AEM) är det viktigt att se till att det finns tillräckligt med resurser tillgängliga när det gäller disk, processor, minne, IO och nätverksgenomströmning. Om du vill ändra storlek på många av dessa resurser måste du känna till hur många resurser som läses in i systemet. Om det inte finns något bättre mätvärde kan du dividera storleken på det befintliga biblioteket med bibliotekets ålder för att hitta frekvensen som resurserna skapas med.

## Skiva {#disk}

### DataStore {#datastore}

Ett vanligt misstag när storleken på det nödvändiga diskutrymmet för en resursimplementering väljs är att beräkningarna baseras på storleken på de råbilder som ska importeras till systemet. Som standard skapar AEM tre renderingar utöver den ursprungliga bilden som kan användas för att återge AEM UI-elementen. I tidigare implementeringar har dessa återgivningar observerats anta dubbelt så stora som storleken på de resurser som har importerats.

De flesta användare definierar anpassade återgivningar utöver de färdiga återgivningarna. Förutom återgivningarna kan du med AEM Resurser extrahera underresurser från vanliga filtyper, till exempel InDesign och Illustrator.

Versionshanteringsfunktionerna i AEM lagrar kopior av resurserna i versionshistoriken. Du kan konfigurera versionerna så att de rensas ofta. Många användare väljer dock att behålla versioner i systemet under lång tid, vilket kräver ytterligare lagringsutrymme.

Med tanke på dessa faktorer behöver du en metod för att beräkna ett tillräckligt exakt lagringsutrymme för lagring av användarresurser.

1. Fastställ storleken och antalet resurser som ska läsas in i systemet.
1. Hämta ett representativt urval av de resurser som ska överföras till AEM. Om du t.ex. tänker läsa in PSD-, JPG-, AI- och PDF-filer i systemet behöver du flera exempelbilder för varje filformat. Dessutom bör dessa prover representera de olika filstorlekarna och komplexiteterna i bilderna.
1. Definiera de återgivningar som ska användas.
1. Skapa renderingarna i AEM med ImageMagick eller Adobes Creative Cloud-program. Förutom de återgivningar som användarna anger skapar du färdiga återgivningar. För användare som implementerar Scene7 kan du använda IC-binärfilen för att generera PTIFF-återgivningar som ska lagras i AEM.
1. Om du tänker använda delresurser genererar du dem för rätt filtyper. Mer information finns i onlinedokumentationen om hur du genererar underresurssidor från InDesign-filer eller PNG-/PDF-filer från Illustrator-lager.
1. Jämför storleken på utdatabilder, återgivningar och delresurser med originalbilderna. Det gör att du kan generera en förväntad tillväxtfaktor när systemet har lästs in. Om du till exempel genererar återgivningar och delresurser med en kombinerad storlek på 3 GB efter att ha bearbetat 1 GB resurser, blir återgivningens tillväxtfaktor 3.
1. Fastställer den maximala tid som tillgångsversionerna ska underhållas i systemet.
1. Bestäm hur ofta befintliga resurser ändras i systemet. Om AEM används som samarbetsnav i kreativa arbetsflöden är antalet ändringar höga. Om endast färdiga resurser överförs till systemet är det här antalet mycket lägre.
1. Bestäm hur många resurser som ska läsas in i systemet varje månad. Om du är osäker kan du kontrollera antalet tillgängliga resurser och dividera antalet med åldern på den äldsta resursen för att beräkna ett ungefärligt antal.

Om du utför steg 1-9 kan du se följande:

* Råstorlek för resurser som ska läsas in
* Antal resurser som ska läsas in
* Renderingstillväxtfaktor
* Antal tillgångsändringar som gjorts per månad
* Antal månader att underhålla tillgångsversioner
* Antal nya resurser som läses in varje månad
* År av tillväxt att allokera utrymme för

Du kan ange dessa tal i kalkylbladet Nätverksstorlek för att fastställa det totala utrymmet som krävs för datalagret. Det är också ett användbart verktyg för att avgöra vilken inverkan som underhåll av resursversioner eller ändring av resurser i AEM har på disktillväxten.

De exempeldata som finns i verktyget visar hur viktigt det är att utföra de angivna stegen. Om du ändrar storlek på datalagret baserat enbart på de Raw-bilder som läses in (1 TB) kan du ha underskattat databasstorleken med faktorn 15.

[Hämta fil](assets/disk_sizing_tool.xlsx)

### Delade datalager {#shared-datastores}

För stora datalager kan du implementera ett delat datalager antingen via ett delat fildatalager på en nätverksansluten enhet eller via ett S3-datalager. I det här fallet behöver enskilda instanser inte ha en kopia av binärfilerna. Dessutom underlättar ett delat datalager binär replikering utan extra intervall och minskar bandbredden som används för att replikera resurser till publiceringsmiljöer.

#### Användningsexempel {#use-cases}

Datalagret kan delas mellan en primär författarinstans och en väntande författarinstans för att minimera den tid det tar att uppdatera standby-instansen med ändringar som görs i den primära instansen. Du kan också dela datalagret mellan författaren och publiceringsinstanserna för att minimera trafiken under replikeringen.

#### Nackdelar {#drawbacks}

På grund av vissa fallgropar rekommenderas inte delning av ett datalager i alla fall.

#### En felpunkt {#single-point-of-failure}

Med ett delat datalager introduceras en enda felpunkt i en infrastruktur. Tänk dig ett scenario där ditt system har en författare och två publiceringsinstanser, var och en med sitt eget datalager. Om någon av dem kraschar kan de andra fortfarande fortsätta att köras. Om datalagret delas kan dock ett diskfel ta bort hela infrastrukturen. Se därför till att du upprätthåller en säkerhetskopia av det delade datalagret där du snabbt kan återställa datalagret.

Att distribuera AWS S3-tjänsten för delade datalager är att föredra eftersom det minskar sannolikheten för fel avsevärt jämfört med normala diskarkitekturer.

#### Ökad komplexitet {#increased-complexity}

Delade datastores ökar även komplexiteten i åtgärder, till exempel skräpinsamling. Vanligtvis kan skräpinsamlingen för ett fristående datalager initieras med ett enda klick. Delade datalager kräver dock markeringssvepning för varje medlem som använder datalagret, förutom att den faktiska samlingen körs på en enskild nod.

För AWS-åtgärder kan en implementering av en central plats (via S3) i stället för att bygga en RAID-matris med EBS-volymer avsevärt kompensera för komplexiteten och driftriskerna i systemet.

#### Prestandafrågor {#performance-concerns}

Ett delat datalager kräver att binärfilerna lagras på en nätverksansluten enhet som delas mellan alla instanser. Eftersom dessa binärfiler nås via ett nätverk påverkas systemprestandan negativt. Du kan delvis minska effekten genom att använda en snabb nätverksanslutning till ett snabbt disksystem. Detta är dock ett dyrt förslag. När det gäller AWS-åtgärder är alla diskar fjärranslutna och kräver nätverksanslutning. Tidigare volymer förlorar data när instansen startas eller stoppas.

#### Latens {#latency}

Latens i S3-implementeringar introduceras av skrivtrådar i bakgrunden. Säkerhetskopieringsprocedurer måste ta hänsyn till denna fördröjning. Dessutom kan Lucene-index vara ofullständiga vid säkerhetskopiering. Det gäller för alla tidskänsliga filer som skrivs till S3-datalagret och som öppnas från en annan instans.

### Nodarkiv eller dokumentarkiv {#node-store-document-store}

Det är svårt att få fram exakta siffror för storleken för en NodeStore eller DocumentStore på grund av de resurser som används av följande:

* Resursmetadata
* Resursversioner
* Granskningsloggar
* Arkiverade och aktiva arbetsflöden

Eftersom binärfilerna lagras i datalagret tar varje binärfil upp lite utrymme. De flesta databaser är mindre än 100 GB. Det kan dock finnas större databaser som är upp till 1 TB stora. För att utföra offlinekomprimering behöver du dessutom tillräckligt med ledigt utrymme på volymen för att skriva om den komprimerade databasen tillsammans med den förkomprimerade versionen. En bra tumregel är att ändra storlek på disken till 1,5 gånger den storlek som förväntas för databasen.

Använd SSD-diskar eller diskar med en IOPS-nivå som är större än 3 kB för databasen. För att eliminera riskerna att IOPS inför flaskhalsar i prestandan bör du övervaka CPU-IO-väntenivåer för tidiga tecken på problem.

[Hämta fil](assets/aem_environment_sizingtool.xlsx)

## Nätverk {#network}

AEM Assets har ett antal användningsfall som gör nätverksprestanda viktigare än i många av våra AEM-projekt. En kund kan ha en snabb server, men om nätverksanslutningen inte är tillräckligt stor för att stödja belastningen på de användare som överför och hämtar resurser från systemet verkar den ändå vara långsam. Det finns en bra metod för att fastställa krympningspunkten i en användares nätverksanslutning till AEM vid [AEM Asset för användarupplevelser, till exempel storlek, utvärdering av arbetsflöde och nätverkstopologi](/help/assets/assets-network-considerations.md).

## Begränsningar {#limitations}

När du ändrar storlek på en implementering är det viktigt att tänka på systembegränsningar. Om den föreslagna implementeringen överskrider dessa begränsningar ska du använda kreativa strategier, som att dela resurser över flera resursimplementationer.

Filstorleken är inte den enda faktor som bidrar till problem med ostrukturerat minne. Det beror också på bildens dimensioner. Du kan undvika OOM-problem genom att ange en högre stackstorlek när du startar AEM.

Dessutom kan du redigera egenskapen för tröskelstorlek för komponenten i Configuration Manager så att den mellanliggande temporära filen som är större än noll används. `com.day.cq.dam.commons.handler.StandardImageHandler`

## Maximalt antal resurser {#maximum-number-of-assets}

Gränsen för antalet filer som kan finnas i ett datalager kan vara 2,1 miljarder på grund av begränsningar i filsystemet. Det är troligt att databasen stöter på problem på grund av ett stort antal noder långt innan datalagrets gräns har nåtts.

Om återgivningarna genereras på ett felaktigt sätt använder du Camera Raw-biblioteket. I det här fallet får dock den längsta sidan av bilden inte vara större än 65 000 pixlar. Dessutom får bilden inte innehålla fler än 512 MP (512 x 1 024 x 1 024 pixlar). Storleken på resursen spelar ingen roll.

Det är svårt att exakt uppskatta storleken på TIFF-filen som stöds från början med en särskild heap för AEM eftersom ytterligare faktorer, som pixelstorlek, påverkar bearbetningen. Det är möjligt att AEM kan bearbeta en fil som är 255 MB färdig, men inte kan bearbeta en filstorlek på 18 MB eftersom den senare innehåller ett ovanligt högre antal pixlar jämfört med den förra.

## Storlek på resurser {#size-of-assets}

Som standard kan du med AEM överföra resurser med en filstorlek på upp till 2 GB. Information om hur du överför mycket stora resurser i AEM finns i [Konfiguration för att överföra mycket stora resurser](managing-video-assets.md#configuration-to-upload-assets-that-are-larger-than-gb).
