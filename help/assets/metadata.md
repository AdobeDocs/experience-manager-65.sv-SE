---
title: Hantera metadata för digitala resurser i [!DNL Adobe Experience Manager].
description: Lär dig mer om metadatatyperna och hur [!DNL Adobe Experience Manager Assets] hjälper dig att hantera metadata för resurser så att det blir enklare att kategorisera och ordna resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# Hantera metadata för digitala resurser {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] sparar metadata för varje resurs. Detta gör det enklare att kategorisera och organisera mediefiler och det hjälper personer som letar efter en viss mediefil. Tack vare möjligheten att extrahera metadata från filer som överförts till [!DNL Experience Manager Assets]kan metadatahanteringen integreras med det kreativa arbetsflödet. Med möjligheten att behålla och hantera godtyckliga metadata med dina resurser, [!DNL Experience Manager Assets] blir det möjligt att automatiskt ordna och bearbeta resurser baserat på deras metadata.

* [XMP-metadata](xmp.md)
* [Redigera eller lägga till metadata](meta-edit.md)
* [Metadata Schema Reference](meta-ref.md)

## Därför behöver vi metadata {#why-we-need-metadata}

Metadata är data om data. I detta avseende avser data den tillgång du hanterar, till exempel en bild. Metadata är viktiga eftersom de gör det möjligt för användarna att hantera resurser mer effektivt.

Metadata är samlingen av alla data som är tillgängliga för den här bilden, men det behöver inte finnas i bilden, till exempel:

* namnet på tillgången
* tid och datum då den senast ändrades
* storleken på bilden som den sparades i databasen
* namnet på mappen som den finns i

Detta är de grundläggande metadataegenskaperna som [!DNL Experience Manager] kan hantera resurser, vilket gör att användare kan se alla resurser, till exempel ordnade efter det senaste ändringsdatumet - användbart när de försöker identifiera vilka resurser som nyligen har lagts till i databasen.

Du kan lägga till mer högnivådata till digitala resurser, till exempel:

* resurstypen (är det en bild, en video, ett ljudklipp eller ett dokument?)
* tillgångens ägare
* tillgångens namn
* beskrivningen av tillgången
* taggarna som har tilldelats en resurs

Fler metadata hjälper dig att kategorisera resurser ytterligare och är till hjälp när mängden digital information växer. Även om det är möjligt för en enskild person att hantera en lista med några hundra filer helt enkelt baserat på deras filnamn, är det här tillvägagångssättet inte tillräckligt när antalet inblandade personer och antalet mediefiler som hanteras ökar.

När metadata läggs till i resurser växer resursens värde, eftersom resursen blir

* mer åtkomligt - det blir mycket enklare för andra
* enklare att hantera - du kan hitta resurser med samma uppsättning egenskaper enklare och använda ändringar på dem
* mer komplex - ju mer metadata du har lagt till i en resurs, desto viktigare blir det att hantera metadata

Därför har du tillgång [!DNL Assets] till rätt sätt att skapa, hantera och utbyta metadata för dina digitala resurser.

## Grundläggande om metadata {#metadata-basics}

Metadata extraheras från resurser när de importeras (hämtas). Genom att lägga till metadata kan du kategorisera materialet ytterligare.

I det här avsnittet beskrivs olika typer av metadata och kodningsstandarder.

### Typer av metadata {#types-of-metadata}

Det finns två grundläggande typer av metadata:

* tekniska metadata
* beskrivande metadata

#### Tekniska metadata {#technical-metadata}

Tekniska metadata är användbara för program som hanterar digitala resurser och bör inte underhållas manuellt. Tekniska metadata kan fastställas automatiskt av [!DNL Experience Manager Assets] och andra program och kan ändras när resursen ändras. Vilka tekniska metadata som är tillgängliga för en mediefil beror till stor del på filtypen för resursen. Exempel på tekniska metadata är följande:

* en fils storlek
* bildens mått (höjd och bredd)
* bithastigheten för en ljud- eller videofil
* bildens upplösning (detaljnivå)

#### Beskrivande metadata {#descriptive-metadata}

Beskrivande metadata är metadata som rör programdomänen, till exempel det företag som en resurs kommer från. Beskrivande metadata kan inte bestämmas automatiskt. Den måste skapas manuellt eller halvautomatiskt. En GPS-aktiverad kamera kan till exempel automatiskt spåra latituden och longituden som en bild togs på och lägga till den här informationen i bildens metadata.

På grund av den höga kostnaden för manuell insats som krävs för att skapa beskrivande metadatainformation har standarder upprättats för att underlätta utbyte av metadata mellan olika programsystem och organisationer.

[!DNL Experience Manager Assets] stöder alla relevanta standarder för metadatahantering.

Eftersom metadata är så viktiga och det krävs mycket manuellt arbete för att skapa metadata har standarder fastställts som gör det enklare att utbyta.

### Kodningsstandarder {#encoding-standards}

Det finns flera olika sätt att bädda in metadata i filer. Ett urval kodningsstandarder stöds:

* XMP: används av [!DNL Assets] för att lagra extraherade metadata i databasen.
* ID3: för ljud- och videofiler.
* EXIF: för bildfiler.
* Annat/äldre: från Microsoft Word, PowerPoint, Excel och så vidare.

#### XMP {#xmp}

XMP betyder Extensible Metadata Platform och är den metadatastandard som används av [!DNL Experience Manager Assets] för all metadatahantering. XMP erbjuder universell metadatakodning som kan bäddas in i alla filformat, och erbjuder en innehållsmodell som stöds av Adobe och andra företag, så att användare av XMP i kombination med [!DNL Experience Manager Assets] en kraftfull plattform kan bygga vidare på.

#### ID3 {#id}

Data som lagras i dessa ID3-taggar visas när du spelar upp en digital ljudfil på datorn eller en bärbar MP3-spelare.

ID3-taggar är utformade för filformatet MP3. Mer information om format:

* ID3-taggar fungerar i MP3- och MP3pro-filer.
* WAV saknar taggar.
* WMA har egna taggar som inte tillåter implementering med öppen källkod.
* Ogg Vorbis använder Xiph-kommentarer som är inbäddade i Ogg-behållaren.
* AAC använder ett märkordsformat.

#### EXIF {#exif}

EXIF betyder Utbytbart bildfilformat och är det vanligaste metadataformatet som används för digitalfoto. Det är ett sätt att bädda in en fast ordlista med metadataegenskaper i ett antal filformat, till exempel JPEG, TIFF, RIFF och WAV.

En stor begränsning för EXIF är att det inte stöds av andra populära bildfilformat som BMP, GIF eller PNG.

EXIF lagrar metadata som par av ett metadatanamn och ett metadatavärde. Dessa metadata name-value-pars kallas också taggar, som inte ska blandas ihop med taggarna i [!DNL Experience Manager].

Eftersom EXIF automatiskt skapas av moderna digitalkameror och stöds av moderna grafikprogram, kan det ses som den lägsta gemensamma nämnaren för metadatahantering.

De flesta metadatafält som definieras av EXIF är av mycket teknisk karaktär och har begränsad användning för beskrivande metadatahantering. Därför erbjuder mappning av EXIF-egenskaper till [!DNL Assets] vanliga metadatamatchningar [och till](metadata-schemas.md) XMP [, det kraftfulla metadataformatet](xmp-writeback.md)[!DNL Assets] som används för metadatahantering.

#### Andra metadata {#other-metadata}

Andra metadata som kan bäddas in från filer är bland annat Microsoft Word, PowerPoint och Excel.

## Metadata-schema {#metadata-schemata}

Metadata-scheman är fördefinierade uppsättningar metadata-egenskapsdefinitioner som kan användas i en mängd olika program. Egenskaper är alltid kopplade till en resurs, vilket innebär att egenskaperna gäller resursen.

Du kan också utforma egna metadatamappningar om det inte finns några som passar dina behov (var försiktig, men inte med att duplicera något som redan finns). Inom en organisation blir det enklare att dela metadata mellan olika organisationer.

[!DNL Experience Manager] innehåller en färdig lista med de vanligaste metadatamappningarna, så att du snabbt kan komma igång med metadatastrategin och välja de metadataegenskaper du behöver från ett redan definierat schema.

De metadatamodeller som stöds visas i följande avsnitt.

### Standardmetadata {#standard-metadata}

* dc - Dublin Core - den viktigaste och mest använda uppsättningen metadata
* DICOM - Digital Imaging and Communications in Medicine
* Iptc4xmpCore &amp; iptc4xmpExt - International Press Communications Standard - massor av ämnesspecifika metadata
* rdf - Resource Description Framework - för generiska semantiska webbmetadata
* xmp - Extensible Metadata Platform
* xmpBJ - grundläggande jobbiljetter

### Programspecifika metadata {#application-specific-metadata}

>[!NOTE]
>
>Programspecifika metadata innehåller tekniska och beskrivande metadata. Om du använder dessa kanske andra program inte kan använda metadata. Om du till exempel har en resurs med Adobe Photoshop-metadata och ett annat bildåtergivningsprogram försöker få åtkomst till metadata kanske det inte går att få åtkomst till den.
>
>Om du har många programspecifika metadata i dina resurser kan du skapa ett arbetsflödessteg som ändrar den programspecifika egenskapen till ett standardsteg.

* cd-see - metadata hanteras av ACDSee-programmet [www.acdsee.com/](https://www.acdsee.com/)
* album - Adobe Photoshop Album
* cq - används av [!DNL Experience Manager Assets]
* dam - används av [!DNL Experience Manager Assets]
* dex - Optima SC Description Explorer
* crs - Adobe Photoshop Camera Raw
* lr - Adobe Lightroom
* mediapro - IView MediaPro
* Microsoft Photo och MP - Microsoft Photo
* pdf och pdfx
* photoshop &amp; psAux - Adobe Photoshop

### Metadata för hantering av digitala rättigheter {#digital-rights-management-metadata}

* cc - creative comms
* xmpRights
* plus - Picture Licensing Universal System - https://www.useplus.com/
* prisma - https://www.idealliance.org/prism-metadata Publiceringskrav för branschstandardmetadata
* prl - Prism Rights Language
* pur - Användarrättigheter för prismaanvändning
* xmpPlus - integrering av PLUS med XMP

### Fotografispecifika metadata {#photography-specific-metadata}

* exif - massor av teknisk information från kameran, inklusive GPS-position
* crs - photoshop camera raw
* Iptc4xmpCore och iptc4xmpExt
* TIFF - bildmetadata (inte bara för TIFF-bilder)

### Utskriftsspecifika metadata {#print-specific-metadata}

* pdf och pdfx - Adobe PDF och tredjepartsprogram
* prisma - [www.prismstandard.org](https://www.prismstandard.org) publiceringskrav för branschstandardmetadata
* xmp
* xmpPG - xmp för växlad text

### Multimediaspecifika metadata {#multimedia-specific-metadata}

* xmpDM - Dynamiska media
* xmpMM - Mediehantering

## Metadatastyrda arbetsflöden {#metadata-driven-workflows}

Genom att skapa metadatadrivna arbetsflöden kan du automatisera vissa processer, vilket ökar effektiviteten. I ett metadatadrivet arbetsflöde läser arbetsflödet och utför därför en fördefinierad åtgärd.

Du kan till exempel använda metadatadrivna arbetsflöden på olika sätt:

* Arbetsflödet kan kontrollera om en bild har en titel. Om så inte är fallet meddelas användaren om att lägga till en titel.
* Arbetsflödet kan kontrollera om ett copyrightmeddelande för en mediefil tillåter distribution. Om så är fallet skickas resursen till en server. Om så inte är fallet skickas resursen till en annan server.
