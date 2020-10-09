---
title: Hantera metadata för era digitala resurser i [!DNL Adobe Experience Manager].
description: Lär dig mer om metadatatyperna och [!DNL Adobe Experience Manager Assets] helps manage metadata for assets to allow easier categorization and organization of assets. [!DNL Experience Manager] hur du automatiskt kan ordna och bearbeta resurser baserat på deras metadata.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 117208c634613559bb13556e12f094add70006e2
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---


# Hantera metadata för dina digitala resurser {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] sparar metadata för varje resurs. Det gör det enklare att kategorisera och ordna resurser och det hjälper personer som letar efter en viss resurs. Tack vare möjligheten att extrahera metadata från filer som överförts till [!DNL Experience Manager Assets]kan metadatahanteringen integreras med det kreativa arbetsflödet. Med möjligheten att behålla och hantera metadata med dina resurser kan du automatiskt ordna och bearbeta resurser baserat på deras metadata.

* [XMP-metadata](xmp.md).
* [Redigera eller lägga till metadata](meta-edit.md).
* [Referens](meta-ref.md)för metadatamappningar.

<!--  TBD: Complete this section. Take help from Metadata IRD for DDAM. Also, look at metadata features in Forrester analysis.

## Understand metadata handling in Experience Manager {#metadata-possibilities-with-aem}

Describe the journey of an assets' metadata. What all happens to metadata when an asset is added to Experience Manager.

## Add metadata to your digital assets {#add-metadata}

Typically, the applications that create digital assets add some metadata to the assets created. Before uploading an asset to Experience Manager, you can edit and modify metadata using either the native application used to create an asset or using some metadata editors. When you upload an asset to Experience Manager, the metadata is processed.

## Metadata of assets, folders, and collections {#metadata-of-assets-folders-collections}

## Modify metadata of an asset, folder, or collection {#modify-metadata}

## Modify metadata in bulk {#modify-metadata-in-bulk}

[!DNL Adobe Enterprise Manager Assets] lets you edit the metadata of multiple assets simultaneously so you can quickly propagate common metadata changes to assets in bulk. You can also edit the metadata for multiple collections in bulk.

Use the properties page to perform metadata changes on multiple assets or collections:

* Change metadata properties to a common value
* Add or modify tags

To customize the metadata properties page, including adding, modifying, deleting metadata properties, use the schema editor.

>[!NOTE]
>
>The bulk editing methods work for assets available in a folder or a collection. For the assets that are available across folders or match a common criteria, it is possible to [bulk update the metadata after searching](search-assets.md#metadataupdates).

1. In the [!DNL Assets] user interface, navigate to the location of the assets you want to edit.
1. Select the assets for which you want to edit common properties.
1. From the toolbar, click **[!UICONTROL Properties]** to open the properties page for the selected assets.

   >[!NOTE]
   >
   >When you select multiple assets, the lowest common parent form is selected for the assets. In other words, the properties page only displays metadata fields that are common across the properties pages of all the individual assets.

1. Modify the metadata properties for selected assets under the various tabs.
1. To view the metadata editor for a specific asset, deselect the remaining assets in the list. The metadata editor fields are populated with the metadata for the particular asset.

   >[!NOTE]
   >
   >* In the properties page, you can remove assets from the asset list by deselecting them. The asset list has all the assets selected by default. The metadata for assets that you remove from the list is not updated.
   >* At the top of assets list, select the check box near **[!UICONTROL Title]** to toggle between selecting the assets and clearing the list.

1. To select a different metadata schema for the assets, click **[!UICONTROL Settings]** from the toolbar, and select the desired schema.
1. Save the changes.
1. To append the new metadata with the existing metadata in fields that contain multiple values, select **[!UICONTROL Append mode]**. If you do not select this option, the new metadata replaces the existing metadata in the fields. click **[!UICONTROL Submit]**.

   >[!CAUTION]
   >
   >For single-value fields, the new metadata is not appended to the existing value in the field even if you select **[!UICONTROL Append mode]**.

## Configure limit for bulk metadata update {#limit-bulk-metadata-updates}

To prevent DOS like situation, Enterprise Manager limits the number of parameters supported in a Sling request. When updating metadata of many assets in one go, you may reach the limit and the metadata does not get updated for more assets. Enterprise Manager generates the following warning in the logs:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** and change the value of **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi configuration.

-->

## Därför behöver vi metadata {#why-we-need-metadata}

Metadata är data om data. I det här avseendet avser data era digitala resurser, till exempel en bild. Metadata är avgörande för effektiv resurshantering.

Metadata är en samling med alla data som är tillgängliga för en resurs, men som inte nödvändigtvis finns i bilden. Några exempel på metadata är:

* Namnet på resursen.
* Tid och datum för senaste ändring.
* Storlek på resursen när den sparades i databasen.
* Namnet på mappen som den finns i.
* Relaterade resurser eller tillämpade taggar.

Ovanstående är de grundläggande metadataegenskaper som [!DNL Experience Manager] kan hantera resurser, vilket gör att användare kan se alla resurser. Det kan till exempel vara bra att beställa resurser efter det senaste ändringsdatumet när du försöker identifiera nyligen tillagda resurser.

Du kan lägga till mer högnivådata till digitala resurser, till exempel:

* Typ av resurs (är det en bild, en video, ett ljudklipp eller ett dokument?).
* Tillgångens ägare.
* Tillgångens namn.
* Beskrivning av tillgången.
* Taggar som tilldelats en resurs.

Fler metadata hjälper dig att kategorisera resurser ytterligare och är till hjälp när mängden digital information växer. Det går att hantera några hundra filer baserat på bara filnamnen. Den här metoden är dock inte skalbar. Den blir kort när antalet inblandade och antalet förvaltade tillgångar ökar.

Med hjälp av metadata ökar värdet på en digital resurs eftersom resursen blir

* Mer åtkomligt - system och användare hittar det enkelt.
* Enklare att hantera - du kan hitta resurser med samma uppsättning egenskaper enklare och använda ändringarna på dem.
* Fullständigt - materialet innehåller mer information och sammanhang med fler metadata.

Därför har du tillgång [!DNL Assets] till rätt sätt att skapa, hantera och utbyta metadata för dina digitala resurser.

## Typer av metadata {#types-of-metadata}

De två grundläggande metadatatyperna är tekniska metadata och beskrivande metadata.

Tekniska metadata är användbara för program som hanterar digitala resurser och bör inte underhållas manuellt. [!DNL Experience Manager Assets] och andra program bestämmer automatiskt tekniska metadata och metadata kan ändras när resursen ändras. Vilka tekniska metadata som är tillgängliga för en mediefil beror till stor del på filtypen för resursen. Några exempel på tekniska metadata är:

* Storlek på en fil.
* Dimensioner (höjd och bredd) för en bild.
* Bithastighet för en ljud- eller videofil.
* Upplösning (detaljnivå) för en bild.

Beskrivande metadata är metadata som rör programdomänen, till exempel det företag som en resurs kommer från. Beskrivande metadata kan inte bestämmas automatiskt. Den skapas manuellt eller halvautomatiskt. En GPS-aktiverad kamera kan till exempel automatiskt spåra latitud och longitud och lägga till geotagga bilden.

Kostnaden för att manuellt skapa beskrivande metadatainformation är hög. Därför har standarder upprättats för att underlätta utbyte av metadata mellan olika programsystem och organisationer. [!DNL Experience Manager Assets] stöder alla relevanta standarder för metadatahantering.

## Kodningsstandarder {#encoding-standards}

Det finns olika sätt att bädda in metadata i filer. Ett urval kodningsstandarder stöds:

* XMP: används av [!DNL Assets] för att lagra extraherade metadata i databasen.
* ID3: för ljud- och videofiler.
* Exif: för bildfiler.
* Annat/äldre: från [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel]och så vidare.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP) är en öppen standard som används av [!DNL Experience Manager Assets] för all metadatahantering. Standarden erbjuder universell metadatakodning som kan bäddas in i alla filformat. Adobe och andra företag stöder XMP standard eftersom de erbjuder en innehållsmodell med mycket innehåll. Användare av XMP som är standard och av [!DNL Experience Manager Assets] har en kraftfull plattform att bygga vidare på. For more information, see [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

Data som lagras i dessa ID3-taggar visas när du spelar upp en digital ljudfil på datorn eller en bärbar MP3-spelare.

ID3-taggar är utformade för filformatet MP3. Mer information om format:

* ID3-taggar fungerar i MP3- och mp3PRO-filer.
* WAV saknar taggar.
* WMA har egna taggar som inte tillåter implementering med öppen källkod.
* Ogg Vorbis använder Xiph-kommentarer som är inbäddade i Ogg-behållaren.
* AAC använder ett märkordsformat.

### Exif {#exif}

Exchangeable image file format (Exif) är det vanligaste metadataformatet som används för digitalfoto. Det är ett sätt att bädda in en fast ordlista med metadataegenskaper i många filformat, till exempel JPEG, TIFF, RIFF och WAV. Exif lagrar metadata som par av ett metadatanamn och ett metadatavärde. Dessa metadata name-value-pars kallas också taggar, som inte ska blandas ihop med taggarna i [!DNL Experience Manager]. Moderna digitalkameror skapar Exif-metadata och moderna grafikprogram stöder det. Exif-formatet är den minsta gemensamma nämnaren för metadatahantering, särskilt för bilder.

En stor begränsning för Exif är att ett fåtal populära bildfilsformat som BMP, GIF och PNG inte har stöd för det.

Metadatafält som definieras av Exif är vanligtvis av teknisk natur och har begränsad användning för beskrivande metadatahantering. Av den anledningen erbjuder [!DNL Experience Manager Assets] mappning av Exif-egenskaper till [vanliga metadatamatchningar](metadata-schemas.md) och till [XMP](xmp-writeback.md).

### Andra metadata {#other-metadata}

Andra metadata som kan bäddas in från filer är bland annat [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel]osv.

## Metadata-scheman {#metadata-schemata}

Metadata-scheman är fördefinierade uppsättningar metadataegenskapsdefinitioner som kan användas i olika program. Egenskaper är alltid kopplade till en resurs, vilket innebär att egenskaperna är&quot;about&quot; för resursen.

Du kan också utforma egna metadatamatchningar om det inte finns några som passar dina behov. Duplicera inte befintlig information. Inom en organisation gör separerade scheman det enklare att dela metadata. [!DNL Experience Manager] innehåller en standardlista med de vanligaste metadataschemana. Listan hjälper dig att snabbt komma igång med metadatastrategin och snabbt välja de metadataegenskaper du behöver.

De metadatamappningar som stöds listas nedan.

### Standardmetadata {#standard-metadata}

* DC - [!DNL Dublin Core] är en viktig och allmänt använd uppsättning metadata.
* DICOM - Digital Imaging and Communications in Medicine.
* `Iptc4xmpCore` och `iptc4xmpExt` - International Press Communications Standard innehåller många ämnesspecifika metadata.
* RDF - Resource Description Framework - för generiska semantiska webbmetadata.
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ` - Grundläggande jobbiljetter.

### Programspecifika metadata {#application-specific-metadata}

Programspecifika metadata innehåller tekniska och beskrivande metadata. Om du använder sådana metadata kanske andra program inte kan använda dessa metadata. Ett annat bildåtergivningsprogram kanske inte kan komma åt [!DNL Adobe Photoshop] metadata. Du kan skapa ett arbetsflödessteg som ändrar en programspecifik egenskap till en standardegenskap.

* ACDSee - metadata som hanteras av [!DNL ACDSee] programmet. Se [www.acdsee.com/](https://www.acdsee.com/).
* Album - [!DNL Adobe Photoshop Album].
* CQ - Används av [!DNL Experience Manager Assets].
* DAM - Används av [!DNL Experience Manager Assets].
* DEX - [Optima SC Description Explorer](http://www.optimasc.com/products/dex/index.html) är en samling verktyg för metadata och filhantering i Windows.
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* Microsoft Photo och MP - Microsoft Photo.
* PDF och PDF/X.
* Photoshop och psAux - [!DNL Adobe Photoshop].

### Digital Rights Management metadata {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights].
* PLUS - [Picture Licensing Universal System](https://www.useplus.com).
* PRISM - [publiceringskrav för branschstandardmetadata](https://www.idealliance.org/prism-metadata).
* PRL - PRISM Rights Language.
* PUR - PRISM-användningsrättigheter.
* `xmpPlus` - Integration av PLUS med XMP.

### Fotografispecifika metadata {#photography-specific-metadata}

* Exif - Teknisk information från kameran, inklusive GPS-position.
* CRS - [!DNL Camera Raw] schema.
* `iptc4xmpCore` and `iptc4xmpExt`.
* TIFF - bildmetadata (inte bara för TIFF-bilder).

### Utskriftsspecifika metadata {#print-specific-metadata}

* PDF och PDF/X - Adobe PDF och tredjepartsprogram.
* PRISM - [publiceringskrav för branschstandardmetadata](https://www.idealliance.org/prism-metadata/).
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG` - XMP metadata för sidindelad text.

### Multimediaspecifika metadata {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` - Mediehantering.

## Metadatastyrda arbetsflöden {#metadata-driven-workflows}

Genom att skapa metadatadrivna arbetsflöden kan du automatisera vissa processer, vilket ökar effektiviteten. I ett metadatadrivet arbetsflöde läser arbetsflödet och utför därför en fördefinierad åtgärd. Du kan till exempel använda metadatadrivna arbetsflöden på olika sätt:

* Arbetsflödet kan kontrollera om en bild har en titel eller inte. Om så inte är fallet meddelas systemet om att en titel ska läggas till.
* Arbetsflödet kan kontrollera om ett copyrightmeddelande för en mediefil tillåter distribution eller inte. Systemet skickar alltså resursen till den ena servern eller den andra.
* Ett arbetsflöde kan söka efter resurser utan fördefinierade, obligatoriska metadata eller resurser med *ogiltiga* metadata.

>[!MORELIKETHIS]
>
>* [Redigera metadataegenskaper för flera samlingar](managing-collections-touch-ui.md#editing-collection-metadata-in-bulk)
>* [XMP-metadata](xmp.md).
>* [Redigera eller lägga till metadata](meta-edit.md).
>* [Referens](meta-ref.md)för metadatamappningar.

