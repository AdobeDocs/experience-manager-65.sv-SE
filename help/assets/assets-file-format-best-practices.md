---
title: Bästa tillvägagångssätt för att bearbeta de filformat som stöds
description: Bästa tillvägagångssätt för att bearbeta de olika filtyper som stöds med [!DNL Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---


# Metodtips för resursfilformat {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] har stöd för många egna och tredjepartsbibliotek för filformat för att tillgodose användarnas olika krav på filstöd. De Adobe-bibliotek som stöds är [!DNL Adobe Camera Raw], Gibson, Adobe PDF Rasterizer och [!DNL Adobe InDesign Server]. Dessutom har [!DNL Experience Manager Assets] stöd för tredjepartsbibliotek som [!DNL ImageMagick], [!DNL TwelveMonkeys] och så vidare.

Information om vilka filformat som stöds finns i [Format för resurser som stöds](/help/assets/assets-formats.md).

>[!TIP]
>
>Om du använder [!DNL Experience Manager] på Adobe Managed Services (AMS) kan du kontakta Adobe kundtjänst om du tänker bearbeta många stora PSD- eller PSB-filer. Samarbeta med Adobe kundtjänstrepresentant för att implementera de bästa metoderna för driftsättningen av AMS och för att välja bästa möjliga verktyg och modeller för Adobe egna format. [!DNL Experience Manager] kan inte bearbeta PSB-filer med hög upplösning som är större än 30000 x 23000 pixlar.

## [!DNL Adobe Camera Raw] bibliotek  {#adobe-camera-raw-library}

Adobe rekommenderar att du använder biblioteket [!DNL Adobe Camera Raw] för RAW- och DNG-filer för optimala prestanda.

[!DNL Adobe Camera Raw] biblioteket stöder CMYK-färgprofil som indata. Däremot genereras utdata i RGB-färgrymd och endast JPEG-format stöds. Källfilens färgrymd (till exempel CMYK) behålls inte i miniatyrbilderna.

Mer information finns i [Camera Raw stöd](/help/assets/camera-raw.md).

## Adobe PDF Rasterizer-bibliotek {#adobe-pdf-rasterizer-library}

För att få bästa möjliga resultat rekommenderar Adobe att du använder Adobe PDF rastreringsbibliotek för följande filer:

* Tunga, innehållsintensiva PDF-filer
* AI-filer med miniatyrbilder som inte genererats direkt från paketet
* För AI-filer med SPOT-färger (PMS)

Miniatyrbilder och förhandsgranskningar som genererats med PDF Rasterizer har bättre kvalitet än färdiga rasterutdata. Adobe PDF Rasterizer-biblioteket stöder inte någon färgutrymmeskonvertering. Oavsett färgrymden i PDF-källfilen genererar Adobe PDF Rasterizer endast RGB-utdata.

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe rekommenderar att du använder [!DNL Adobe InDesign Server] för att extrahera [!DNL Adobe InDesign]-specifika renderingar, som IDML och HTML. Mer information finns i [Lägga till resurser i Experience Manager som referenser i Adobe InDesign](/help/assets/managing-linked-subassets.md#refai).

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] genererar och levererar flera varianter av avancerat innehåll i realtid via sitt globala, skalbara och prestandaoptimerade nätverk. Det levererar interaktiva tittarupplevelser och effektiviserar den digitala kampanjhanteringsprocessen. Mer information om hur du aktiverar [!DNL Dynamic Media] finns i [Konfigurera dynamiska media](/help/assets/config-dynamic.md).

För närvarande kan [!DNL Dynamic Media] ha stöd för videoklipp med upp till 15 GB innehåll per fil.

## ImageMagick library {#imagemagick-library}

Adobe rekommenderar att du använder ImageMagick-biblioteket i följande scenarier:

* Om du vill generera miniatyrbildsrenderingar för EPS-filer.
* Bevara bildprofilsinformation.
* För att bevara genomskinlighet.
* Så här bearbetar du PSD- och PSB-filer.

Mer information om hur du konfigurerar [!DNL ImageMagick]-biblioteket i [!DNL Experience Manager] finns i [Använda ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick). Mer information finns i [Bästa metoder för att konfigurera ImageMagick](/help/assets/best-practices-for-imagemagick.md).

## Bildomkodningsbibliotek {#image-transcoding-library}

Adobe Imaging Transcoding Library är en bildbehandlingslösning som utför viktiga bildhanteringsfunktioner, till exempel bildkodning, omkodning, omsampling, storleksändring osv.

Bildbiblioteket Transcoding Library har stöd för följande MIME-typer:

* JPG/JPEG
* PNG (8 och 16 bitar)
* GIF
* BMP
* TIFF/Komprimerad TIFF (förutom 32-bitars tips och PTiff).
* ICO
* ICN

Mer information finns i [Bildkonverteringsbibliotek](/help/assets/imaging-transcoding-library.md).
