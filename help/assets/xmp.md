---
title: Stöd för XMP-metadata i AEM Assets
description: Läs om metadatastandarden XMP (Extensible Metadata Platform) som används av AEM Assets för metadatahantering. XMP har ett standardformat för att skapa, bearbeta och utbyta metadata för ett stort antal program.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# XMP-metadata {#xmp-metadata}

XMP (Extensible Metadata Platform) är den metadatastandard som används av AEM Assets för all metadatahantering. XMP har ett standardformat för att skapa, bearbeta och utbyta metadata för ett stort antal program.

Förutom universell metadatakodning som kan bäddas in i alla filformat, erbjuder XMP en innehållsmodell [som](xmp.md#xmp-core-concepts) stöds av Adobe [](xmp.md#advantages-of-xmp) och andra företag, så att användare av XMP i kombination med AEM Assets har en kraftfull plattform att bygga vidare på.

XMP- [specifikationen](https://www.adobe.com/devnet/xmp.html) finns hos Adobe.

## Vad är XMP? {#what-is-xmp}

AEM Assets stöder XMP - Extensible Metadata Platform som leds av Adobe. XMP är en standard för bearbetning och lagring av standardiserade och egna metadata i digitala resurser. XMP är en standard som gör att flera program kan arbeta effektivt med metadata.

Produktionspersonal kan till exempel använda det inbyggda XMP-stödet i Adobes program för att skicka information till olika filformat. AEM Assets-databasen extraherar XMP-metadata och använder dem för att hantera innehållets livscykel och ger möjlighet att skapa automatiserade arbetsflöden.

XMP standardiserar hur metadata definieras, skapas och bearbetas genom att tillhandahålla en datamodell, en lagringsmodell och scheman. Alla dessa begrepp beskrivs i detta avsnitt.

Alla äldre metadata från EXIF, ID3 eller Microsoft Office översätts automatiskt till XMP, som kan utökas för att stödja kundspecifika metadatamatchningar, som produktkataloger.

Metadata i XMP består av en uppsättning egenskaper. Dessa egenskaper är alltid kopplade till en särskild enhet som kallas resurs. Egenskaperna är alltså&quot;om&quot; resursen. För XMP är resursen alltid resursen.

### Adobe {#adobe}

Adobe introducerade först XMP-standarden som en del av Adobe Acrobat-produkten. Sedan dess har XMP-standarden blivit allmänt förekommande.

### XMP-ekosystem {#xmp-ecosystem}

XMP definierar en [metadatamodell](https://en.wikipedia.org/wiki/Metadata) som kan användas med alla definierade metadataobjekt. XMP definierar också särskilda [scheman](https://en.wikipedia.org/wiki/XML_schema) för grundläggande egenskaper som är användbara för att spela in en resurshistorik när den går igenom flera bearbetningssteg, från att fotograferas, [skannas](https://en.wikipedia.org/wiki/Image_scanner)eller redigeras som text, genom fotoredigeringssteg (som [beskärning](https://en.wikipedia.org/wiki/Cropping_%28image%29) eller färgjustering), till att sammanfoga en slutbild. Med XMP kan varje program eller enhet läggas in i en digital resurs, som sedan kan sparas i den slutliga digitala filen.

XMP är oftast serialiserat och lagras med en delmängd av [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF), som i sin tur uttrycks i [XML](https://en.wikipedia.org/wiki/XML).

## Fördelar med XMP {#advantages-of-xmp}

XMP har följande fördelar jämfört med andra kodningsstandarder och -scheman:

* XMP-baserade metadata är mycket kraftfulla och detaljerade.
* Med XMP kan du ha flera värden för en egenskap.
* XMP har standardiserad kodning, vilket gör att du enkelt kan utbyta metadata.
* XMP är utökningsbart. Du kan lägga till ytterligare information i dina resurser.

### Utbyggbart {#extensible}

XMP-standarden är utformad för att vara utökningsbar så att du kan lägga till anpassade typer av metadata i XMP-data. EXIF har däremot inte det, utan en fast lista över egenskaper som inte kan utökas.

>[!NOTE]
>
>XMP tillåter vanligtvis inte att binära datatyper bäddas in. Om du vill ha binära data i XMP-filer, till exempel miniatyrbilder, måste de kodas i ett XML-anpassat format, till exempel `Base64`.

## XMP Core Concepts {#xmp-core-concepts}

I följande avsnitt beskrivs de centrala begreppen för XMP, inklusive namnutrymmen och scheman, egenskaper och värden samt språkalternativ.

### Namnutrymmen och scheman {#namespaces-and-schemata}

Ett XMP-schema är en uppsättning egenskapsnamn i ett vanligt XML-namnutrymme som innehåller datatypen och beskrivande information. Ett XMP-schema identifieras av dess XML-namnområdes-URI. Om du använder namnutrymmen förhindras konflikter mellan egenskaper i olika scheman som har samma namn men en annan betydelse.

Egenskapen i två oberoende designade scheman kan till exempel avse den person som skapade resursen eller det program som resursen skapades i (till exempel Adobe Photoshop). `Creator`

### Egenskaper och värden {#properties-and-values}

XMP kan innehålla egenskaper från ett eller flera av scheman.

En vanlig delmängd som används av många Adobe-program kan till exempel vara följande:

* Dublin Core-schema: dc:title, dc:creator, dc:subject, dc:format, dc:rights
* XMP grundläggande schema: xmp:CreateDate, xmp:CreatorTool, xmp:ModifyDate, xmp:metadataDate
* XMP-schema för rättighetshantering: xmpRights:WebStatement, xmpRights:Marked
* XMP-schema för mediehantering: xmpMM:DocumentID

### Språkalternativ {#language-alternatives}

Med XMP kan du lägga till en egenskap i textegenskaper för att ange textens språk. `xml:lang`
