---
title: Bästa tillvägagångssätt för att bearbeta de olika filformat som stöds med hjälp av AEM Assets.
description: Bästa tillvägagångssätt för att bearbeta de olika filtyper som stöds med hjälp av AEM Resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 70a88085a0fd6e949974aa7f1f92fdc3def3d98e

---


# Bästa metoder för att använda filformat {#assets-file-format-best-practices}

AEM Assets stöder många egna och tredjepartsbibliotek för filformat för att tillgodose olika användarbehov. De Adobe-bibliotek som stöds är bland annat Adobe Camera Raw, Gibson, Adobe PDF Rasterizer och Adobe InDesign Server. Dessutom har AEM Assets stöd för tredjepartsbibliotek som ImageMagick, TwelveMonkeys och så vidare.

Information om vilka filformat som stöds finns i Format [som stöds för](/help/assets/assets-formats.md)resurser.

>[!TIP]
>
>Om du använder Experience Manager på Adobe Managed Services (AMS) kan du kontakta Adobe Support om du tänker bearbeta många stora PSD- eller PSB-filer. Samarbeta med Adobes kundtjänstrepresentant för att implementera de bästa metoderna för driftsättningen av AMS och för att välja de bästa möjliga verktygen och modellerna för Adobes egna format.

## Adobe Camera Raw-bibliotek {#adobe-camera-raw-library}

Adobe rekommenderar att du använder Adobe Camera Raw-biblioteket för RAW- och DNG-filer för optimala prestanda.

Adobe Camera Raw-biblioteket stöder CMYK-färgprofil som indata. Däremot genereras utdata i RGB-färgrymd och endast JPEG-format stöds. Färgrymden för källfilen (till exempel CMYK) behålls inte i miniatyrbilderna.

Mer information finns i Stöd för [](/help/assets/camera-raw.md)Camera Raw.

## Adobe PDF Rasterizer-bibliotek {#adobe-pdf-rasterizer-library}

För bästa resultat bör du använda Adobe PDF-rastreringsbiblioteket för följande filer:

* Tunga, innehållsintensiva PDF-filer
* AI-filer med miniatyrbilder som inte genererats direkt från paketet
* För AI-filer med SPOT-färger (PMS)

Miniatyrbilder och förhandsgranskningar som genererats med PDF Rasterizer har bättre kvalitet än färdiga rasterutdata. Adobe PDF Rasterizer-biblioteket har inte stöd för konvertering av färgrymd. Oberoende av färgrymden i PDF-källfilen genererar Adobe PDF Rasterizer bara RGB-utdata.

## Adobe InDesign Server {#adobe-indesign-server}

Adobe rekommenderar att du använder Adobe InDesign Server för att extrahera Adobe InDesign-specifika återgivningar som IDML och HTML. Mer information finns i [Lägga till AEM-resurser som referenser i Adobe InDesign](/help/assets/managing-linked-subassets.md#refai).

## Dynamiska medier {#dynamic-media}

Dynamic Media genererar och levererar flera varianter av multimedieinnehåll i realtid via sitt globala, skalbara och prestandaoptimerade nätverk. Det levererar interaktiva tittarupplevelser och effektiviserar den digitala kampanjhanteringsprocessen. Mer information om hur du aktiverar dynamiska media finns i [Konfigurera dynamiska media](/help/assets/config-dynamic.md).

För närvarande har Dynamic Media stöd för videor på upp till 20 GB innehåll per fil.

## ImageMagick Library {#imagemagick-library}

Adobe rekommenderar att du använder ImageMagick-biblioteket i följande scenarier:

* Generera miniatyrrenderingar för EPS-filer
* Bevara bildprofilsinformation
* Bevara genomskinlighet
* Bearbeta PSD- och PSB-filer

Mer information om hur du konfigurerar ImageMagic-biblioteket i AEM finns i [Använda ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick). Mer information finns i [Bästa metoder för att konfigurera ImageMagick](/help/assets/best-practices-for-imagemagick.md).

## Bildomkodningsbibliotek {#image-transcoding-library}

Adobe Imaging Transcoding Library är en bildbehandlingslösning som utför grundläggande bildhanteringsfunktioner, som bildkodning, omkodning, omsampling, storleksändring med mera.

Bildkodningsbiblioteket stöder följande MIME-typer:

* JPG/JPEG
* PNG (8 och 16 bitar)
* GIF
* BMP
* TIFF/Komprimerad TIFF (förutom 32-bitars tips och PTiff).
* ICO
* ICN

Mer information finns i [Bildkonverteringsbibliotek](/help/assets/imaging-transcoding-library.md).
