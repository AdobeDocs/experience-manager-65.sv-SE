---
title: Bästa tillvägagångssätt för att bearbeta de olika filformat som stöds med [!DNL Adobe Experience Manager Assets].
description: Bästa tillvägagångssätt för att bearbeta de olika filtyper som stöds med hjälp av [!DNL Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# Bästa metoder för att använda filformat {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] har stöd för många egna och tredjepartsbibliotek för filformat för att tillgodose användarnas olika krav på filstöd. De Adobe-bibliotek som stöds är bland annat [!DNL Adobe Camera Raw], Gibson, Adobe PDF Rasterizer [!DNL Adobe InDesign Server]. Dessutom har stöd [!DNL Experience Manager Assets] för bibliotek från tredje part, inklusive [!DNL ImageMagick], [!DNL TwelveMonkeys]och så vidare.

Information om vilka filformat som stöds finns i Format [som stöds för](/help/assets/assets-formats.md)resurser.

>[!TIP]
>
>Om du använder Adobe Managed Services (AMS) kan du kontakta Adobes kundtjänst om du tänker bearbeta många stora PSD- eller PSB-filer. [!DNL Experience Manager] Samarbeta med Adobes kundtjänstrepresentant för att implementera de bästa metoderna för driftsättningen av AMS och för att välja de bästa möjliga verktygen och modellerna för Adobes egna format. [!DNL Experience Manager] kan inte bearbeta PSB-filer med hög upplösning som är större än 30000 x 23000 pixlar.

## [!DNL Adobe Camera Raw] bibliotek {#adobe-camera-raw-library}

Adobe rekommenderar att du använder [!DNL Adobe Camera Raw] biblioteket för RAW- och DNG-filer för optimala prestanda.

[!DNL Adobe Camera Raw] biblioteket stöder CMYK-färgprofil som indata. Däremot genereras utdata i RGB-färgrymd och endast JPEG-format stöds. Källfilens färgrymd (till exempel CMYK) behålls inte i miniatyrbilderna.

Mer information finns i Stöd för [](/help/assets/camera-raw.md)Camera Raw.

## Adobe PDF Rasterizer-bibliotek {#adobe-pdf-rasterizer-library}

För bästa resultat bör du använda Adobe PDF-rastreringsbiblioteket för följande filer:

* Tunga, innehållsintensiva PDF-filer
* AI-filer med miniatyrbilder som inte genererats direkt från paketet
* För AI-filer med SPOT-färger (PMS)

Miniatyrbilder och förhandsgranskningar som genererats med PDF Rasterizer har bättre kvalitet än färdiga rasterutdata. Adobe PDF Rasterizer-biblioteket har inte stöd för konvertering av färgrymd. Oberoende av färgrymden i PDF-källfilen genererar Adobe PDF Rasterizer bara RGB-utdata.

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe rekommenderar att du använder [!DNL Adobe InDesign Server] för att extrahera [!DNL Adobe InDesign]specifika renderingar, som IDML och HTML. Mer information finns i [Lägga till Experience Manager-resurser som referenser i Adobe InDesign](/help/assets/managing-linked-subassets.md#refai).

## [!DNL Dynamic Media]  {#dynamic-media}

[!DNL Dynamic Media] genererar och levererar flera varianter av avancerat innehåll i realtid via sitt globala, skalbara och prestandaoptimerade nätverk. Det levererar interaktiva tittarupplevelser och effektiviserar den digitala kampanjhanteringsprocessen. Mer information om aktivering [!DNL Dynamic Media]finns i [Konfigurera dynamiska media](/help/assets/config-dynamic.md).

För närvarande [!DNL Dynamic Media] kan hantera videoklipp med upp till 20 GB innehåll per fil.

## ImageMagick Library {#imagemagick-library}

Adobe rekommenderar att du använder ImageMagick-biblioteket i följande scenarier:

* Om du vill generera miniatyrbildsrenderingar för EPS-filer.
* Bevara bildprofilsinformation.
* För att bevara genomskinlighet.
* Så här bearbetar du PSD- och PSB-filer.

Mer information om hur du konfigurerar [!DNL ImageMagick] biblioteket i [!DNL Experience Manager]finns i [Använda ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick). Mer information finns i [Bästa metoder för att konfigurera ImageMagick](/help/assets/best-practices-for-imagemagick.md).

## Bildomkodningsbibliotek {#image-transcoding-library}

Adobe Imaging Transcoding Library är en bildbehandlingslösning som utför grundläggande bildhanteringsfunktioner, som bildkodning, omkodning, omsampling, storleksändring med mera.

Bildbiblioteket Transcoding Library har stöd för följande MIME-typer:

* JPG/JPEG
* PNG (8 och 16 bitar)
* GIF
* BMP
* TIFF/Komprimerad TIFF (förutom 32-bitars tips och PTiff).
* ICO
* ICN

Mer information finns i [Bildkonverteringsbibliotek](/help/assets/imaging-transcoding-library.md).
