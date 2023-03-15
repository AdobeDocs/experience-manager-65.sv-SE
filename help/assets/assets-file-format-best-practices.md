---
title: Bästa tillvägagångssätt för att bearbeta de filformat som stöds
description: Bästa tillvägagångssätt för att bearbeta de olika filtyper som stöds med [!DNL Experience Manager Assets].
contentOwner: AG
role: Admin
feature: Asset Management,Developer Tools
exl-id: da080f12-4cf7-4c26-901b-cd40d9c00bcb
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# Bästa metoder för att använda filformat {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] har stöd för många egna och tredjepartsbibliotek för filformat för att tillgodose användarnas olika krav på filstöd. De Adobe-bibliotek som stöds omfattar [!DNL Adobe Camera Raw], Gibson, Adobe PDF Rasterizer och [!DNL Adobe InDesign Server]. Dessutom [!DNL Experience Manager Assets] stöder bibliotek från tredje part, inklusive [!DNL ImageMagick], [!DNL TwelveMonkeys]och så vidare.

Information om vilka filformat som stöds finns i [Format som stöds för resurser](/help/assets/assets-formats.md).

>[!TIP]
>
>Om du använder [!DNL Experience Manager] om du planerar att bearbeta stora PSD- eller PSB-filer på Adobe Managed Services (AMS) kan du kontakta Adobe kundsupport. Samarbeta med Adobe kundsupportrepresentant för att implementera de bästa metoderna för driftsättningen av AMS och för att välja de bästa möjliga verktygen och modellerna för Adobe egna format. [!DNL Experience Manager] kan inte bearbeta PSB-filer med hög upplösning som är större än 30000 x 23000 pixlar.

## [!DNL Adobe Camera Raw] bibliotek {#adobe-camera-raw-library}

Adobe rekommenderar att du använder [!DNL Adobe Camera Raw] bibliotek för RAW- och DNG-filer.

[!DNL Adobe Camera Raw] biblioteket stöder CMYK-färgprofil som indata. Däremot genereras utdata i färgrymden RGB och endast utdata i JPEG-format stöds. Källfilens färgrymd (till exempel CMYK) behålls inte i miniatyrbilderna.

Mer information finns i [Camera Raw stöd](/help/assets/camera-raw.md).

## Adobe PDF Rasterizer-bibliotek {#adobe-pdf-rasterizer-library}

För att få bästa möjliga resultat rekommenderar Adobe att du använder Adobe PDF rastreringsbibliotek för följande filer:

* Tunga, innehållsintensiva PDF-filer
* AI-filer med miniatyrbilder som inte genererats direkt från paketet
* För AI-filer med SPOT-färger (PMS)

Miniatyrbilder och förhandsgranskningar som genererats med PDF Rasterizer har bättre kvalitet jämfört med färdiga rasterutdata. Adobe PDF Rasterizer-biblioteket stöder inte någon färgutrymmeskonvertering. Oavsett färgrymden i källfilen genereras endast utdata från RGB i Adobe PDF Rasterizer.

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe rekommenderar att du använder [!DNL Adobe InDesign Server] extrahera [!DNL Adobe InDesign]-specifika renderingar, som IDML och HTML. Mer information finns i [Lägga till Experience Manager-resurser som referenser i Adobe InDesign](/help/assets/managing-linked-subassets.md#refai).

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] genererar och levererar flera varianter av avancerat innehåll i realtid via sitt globala, skalbara och prestandaoptimerade nätverk. Det levererar interaktiva tittarupplevelser och effektiviserar den digitala kampanjhanteringsprocessen. Mer information om aktivering [!DNL Dynamic Media], se [Konfigurera Dynamic Media](/help/assets/config-dynamic.md).

För närvarande [!DNL Dynamic Media] kan hantera videoklipp med upp till 15 GB innehåll per fil.

## ImageMagick Library {#imagemagick-library}

Adobe rekommenderar att du använder ImageMagick-biblioteket i följande scenarier:

* Generera miniatyrbildsrenderingar för EPS-filer.
* Bevara bildprofilsinformation.
* För att bevara genomskinlighet.
* Om du vill bearbeta PSD- och PSB-filer.

Så här konfigurerar du [!DNL ImageMagick] bibliotek i [!DNL Experience Manager], se [Använda ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick). Optimal användning finns i [Bästa metoder för att konfigurera ImageMagick](/help/assets/best-practices-for-imagemagick.md).

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

Mer information finns i [Konverteringsbibliotek för bildbehandling](/help/assets/imaging-transcoding-library.md).
