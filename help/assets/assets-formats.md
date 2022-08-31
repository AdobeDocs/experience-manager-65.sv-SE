---
title: Filformat och MIME-typer som stöds
description: Filformat och MIME-typer som stöds av [!DNL Assets] och [!DNL Dynamic Media] och de funktioner som stöds för varje format.
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Asset Management,Renditions
exl-id: a4bcf67b-54f4-4681-9e42-fd4753acde1a
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1741'
ht-degree: 2%

---

# Format som stöds i [!DNL Adobe Experience Manager Assets] {#assets-supported-formats}

[!DNL Experience Manager Assets] har stöd för ett stort antal filformat och alla funktioner har olika stöd för olika MIME-typer. Integrera [!DNL Assets] använder Adobe [!DNL Extensible Metadata Platform] (XMP).

Använd teckenförklaringen för att förstå supportnivån.

| Supportnivå | Beskrivning |
| :-----------: | ------------------------------ |
| ✓ | Stöds |
| &#42; | Stöds med tilläggsfunktioner |
| - | Ej relevant |

## Rasterbildformat som stöds i [!DNL Experience Manager] {#supported-raster-image-formats}

De rasterbildformat som stöds i [!DNL Assets] är:

| Format | Lagring | Metadatahantering | Extrahering av metadata | Generering av miniatyrbilder | Redigering | Återskrivning av metadata | Insikter |
| ------------ | :------: | :-----------------: | :-----------------: | :------------------: | :------: | :----------------: | :------: |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| PNM | ✓ | ✓ | - | - | - | - | ✓ |
| PGM | ✓ | ✓ | - | - | - | - | ✓ |
| PBM | ✓ | ✓ | - | - | - | - | ✓ |
| PPM | ✓ | ✓ | - | - | - | - | ✓ |
| PSD ‡ | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | - | ✓ | - |
| PICT | - | - | - | - | - | - | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ | - | - | - |

‡ Den sammanfogade bilden extraheras från filen PSD. Det är en bild som genereras av Adobe Photoshop och inkluderas i filen PSD. Beroende på inställningarna kan den sammanfogade bilden vara den faktiska bilden eller inte.

Utöver informationen ovan bör du tänka på följande:

* Stödet för EPS-filer gäller endast för rasterbilder. Generering av miniatyrbilder för EPS-vektorbilder stöds till exempel inte som standard. Om du vill lägga till stöd [konfigurera ImageMagick](best-practices-for-imagemagick.md). Information om hur du integrerar tredjepartsverktyg för att aktivera ytterligare funktioner finns i [Kommandoradsbaserad mediehanterare](media-handlers.md#command-line-based-media-handler).

* Metadatatillbakaskrivning fungerar för PSB-filformatet när det läggs till i `NComm` hanterare.

* För EPS-filer stöds tillbakaskrivning av metadata i PostScript Document Structuring Convention (PS-Adobe) version 3.0 eller senare.

## 3D-format som stöds {#support-3d-formats}

Följande lista över 3D-format stöds.

Se även [Arbeta med 3D-resurser i Dynamic Media.](/help/assets/assets-3d.md)

| Format | Lagring | Versionshantering | Arbetsflöde | Publicering | Åtkomstkontroll | Förhandsvisning av miniatyrbilder | Förhandsgranska 3D | Leverans till Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ |  | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ |  | ✓ | - | ✓ | - |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |

## Biblioteket PDF Rasterizer stöds {#supported-pdf-rasterizer-library}

Adobe PDF Rasterizer-biblioteket genererar högkvalitativa miniatyrbilder och förhandsgranskningar för stora och innehållsintensiva [!DNL Adobe Illustrator] och PDF-filer. Adobe rekommenderar att du använder PDF rastrerarbiblioteket för följande:

* Innehållsintensiva AI/PDF-filer som är resurskrävande att bearbeta.
* AI/PDF-filer, för vilka miniatyrbilder inte genereras som standard.
* AI-filer med Pantone Matching System-färger (PMS).

Se [Använda PDF Rasterizer](aem-pdf-rasterizer.md).

## Bildkodningsbibliotek som stöds {#supported-image-transcoding-library}

Biblioteket Adobe Imaging Transcoding är en bildbehandlingslösning som utför viktiga bildhanteringsfunktioner, som kodning, omkodning, omsampling och storleksändring.

Biblioteket för bildkonvertering har stöd för JPG/JPEG, PNG (8-bitars och 16-bitars), GIF, BMP, TIFF/komprimerad TIFF (förutom 32-bitars TIFF och PTIFF-filer), ICO och ICN MIME.

Se [Konverteringsbibliotek för bildbehandling](imaging-transcoding-library.md).

## Camera Raw som stöds {#supported-camera-raw}

The [!DNL Adobe Camera Raw] bibliotek aktiverar [!DNL Assets] för att importera råbilder. Se [Camera Raw stöd](camera-raw.md).

## Stöds [!DNL Assets] dokumentformat {#supported-document-formats}

Dokumentformat som stöds för filhanteringsfunktioner är följande:

| Format | Lagring | [Metadatahantering](metadata.md) | Fulltext<br> extrahering | [Extrahering av metadata](metadata.md) | Miniatyrbild<br> generering | [Extrahering av deltillgångar](managing-linked-subassets.md) | [Återskrivning av metadata](xmp-writeback.md) | [Anslutna resurser](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|---|---|---|---|---|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ | - |
| DOC | ✓ | ✓ | ✓ | ✓ | - | - | - | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | - | - | - | ✓ |
| ODT | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| RTF | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| TXT | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| XLS | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | - | - | - | ✓ |
| ODS | ✓ | ✓ | ✓ | - | - | - | - | - |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| ODP | ✓ | ✓ | ✓ | - | - | - | - | - |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ | - |
| PS | ✓ | ✓ | - | - | - | - | - | - |
| QXP | ✓ | ✓ | - | - | - | - | - | - |
| ePub | ✓ | ✓ | - | ✓ | ✓ | - | - | - |

## Multimediaformat som stöds {#supported-multimedia-formats}

|  | Lagring | Metadatahantering | Extrahering av metadata | Generering av miniatyrbilder | FFmpeg-omkodning |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ | - | - | &#42; |
| MIDI | ✓ | ✓ | - | - | &#42; |
| 3GP | ✓ | ✓ | - | - | &#42; |
| MP3 | ✓ | ✓ | ✓ | - | &#42; |
| MPG | ✓ | ✓ | - | - | &#42; |
| OGA | ✓ | ✓ | - | - | &#42; |
| OGG | ✓ | ✓ | - | - | &#42; |
| RA | ✓ | ✓ | - | - | &#42; |
| WAV | ✓ | ✓ | - | - | &#42; |
| WMA | ✓ | ✓ | - | - | &#42; |
| DVI | ✓ | ✓ | - | &#42; | &#42; |
| FLV | ✓ | ✓ | - | &#42; | &#42; |
| M4V | ✓ | ✓ | - | &#42; | &#42; |
| MPEG | ✓ | ✓ | - | &#42; | &#42; |
| OGV | ✓ | ✓ | - | &#42; | &#42; |
| MOV | ✓ | ✓ | - | &#42; | &#42; |
| WMV | ✓ | ✓ | - | &#42; | &#42; |
| SWF | ✓ | ✓ | - | - | - |

## Arkivformat som stöds {#supported-archive-formats}

De arkivformat som stöds och tillämpligheten för de vanliga DAM-arbetsflödena beskrivs i följande tabell.

| Format | Lagring | Versionshantering | Arbetsflöde | Publicering | Åtkomstkontroll | Dynamic Media Delivery |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## Andra format som stöds {#other-supported-formats}

Hur de vanliga DAM-funktionerna kan användas för ett fåtal specifika filformat beskrivs nedan.

| Format | Lagring | Versionshantering | Arbetsflöde | Publicering | Åtkomstkontroll | Dynamic Media Delivery |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript (när konfigureras med egen leveransdomän) | - | - | - | - | - | ✓ |

>[!NOTE]
>
>Att överföra och distribuera JavaScript-filer kan vara säkert eller inte. Om det behövs kan du använda övertäckningar för att hindra användare från att överföra JS-filer.

## MIME-typer som stöds {#supported-mime-types}

Som standard [!DNL Experience Manager] identifierar filtypen med hjälp av filtillägget. [!DNL Experience Manager] kan identifiera det från innehållet i filerna. För den senare väljer du [!UICONTROL Detect MIME from content] alternativ i [!UICONTROL Day CQ DAM Mime Type Service] i [!DNL Experience Manager] Webbkonsol.

En lista över MIME-typer som stöds finns i CRXDE Lite på `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`.

| Filtillägg | MIME-typ/ Internetmedietyp | Standardvärde för jobParam | Tillåtet jobParam-värde |
|---|---|---|---|
| Bild | bild/s7resurs | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | Standardvärdet jobParam gäller för alla MIME-bildresurser.<ul><li>[knockoutBackgroundOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-knockout-background-options.html)</li><li>[manualCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-manual-crop-options.html)</li><li>[autoColorCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-color-crop-options.html)</li><li>[autoTransparentCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-transparent-crop-options.html)</li><li>[colorManagementOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-color-management-options.html)</li><li>[autoSetCreationOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-set-creation-options.html)</li><li>[emailSetting](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/sting-constants/r-email-settings.html)</li><li>[xmpKeywords](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-xmp-keywords.html)</li><li>[unsharpMaskOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-unsharp-mask-options.html)</li></ul> |
| 3G2 | video/3gpp2 |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| 3GP | video/3gpp |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li> [illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html)</li></ul> |
| AIFF | audio/x-aiff |  |  |
| AVI | video/x-msvideo |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| BMP | image/bmp |  |  |
| CSS | text/css |  |  |
| DOC | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>program/steg</li><li>application/x-eps</li><li>bild/steg</li><li>image/x-eps</li></ul> |  |  |
| F4V | video/x-f4v |  | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | image/jpeg |  |  |
| M2V | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| M4V | video/x-m4v |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MOV | video/quicktime |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPEG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-pdf-options.html) |
| PFB | application/x-font-type1 |  |  |
| PFM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | bild/png |  |  |
| PPT | application/vnd.ms |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li>[illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-options.html)</li><li>[photoshopLayerOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-layer-options.html)</li></ul> |
| RTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shockwave-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF/TIFF | bild/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | video/dvd |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| VTT | text/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| XLS | application/vnd.ms |  |  |
| ZIP | application/zip |  |  |

## Dynamic Media - Videoformat som stöds för transkodning {#supported-input-video-formats-for-dynamic-media-transcoding}

| Videofiltillägg | Behållare | Rekommenderade videokodekar | Videokodekar som inte stöds |
|---|---|---|---|
| AVI | A/V-sammanflätning | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft® Video 1 (MS-CRAM) |
| FLV, F4V | Adobe Flash | H264/AVC, Flix VP6, H263, Sorenson | SWF (vektoranimeringsfiler) |
| M4V | Apple iTunes | H264/AVC | - |
| MKV | Matroska | H264/AVC | - |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 &amp; HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, Apple Animation |
| MP4 | MPEG-4 | H264/AVC (alla profiler) | - |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 | - |
| MXF ‡ | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro | - |
| OGV, OGG | Ogg | Theora, VP3, Dirac | - |
| WebM | WebM | Google VP8 | - |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Microsoft® Screen (MSS2), Microsoft® Photo Story (WVP2) |

‡ Det här videoformatet stöds ännu inte för interaktiva videoklipp i Dynamic Media eller för användning med anteckningar i Experience Manager Assets.

## Dynamic Media - dokumentformat som stöds {#supported-document-formats-dynamic-media}

| Format | Överför<br> (Indataformat) | Skapa<br> image<br> förinställning<br> (Utdataformat) | Förhandsgranska<br> dynamisk<br> rendering | Leverera<br> dynamisk<br> rendering | Hämta<br> dynamisk<br> rendering |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | - | - | - | - |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | - | - | - | - |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) (Se anmärkningen nedan) | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>För säker PDF stöds bara överföring.

Utöver ovanstående funktioner bör du tänka på följande:

* Information om hur du använder Dynamic Media för att generera dynamiska renderingar för PDF-filer finns i [Filformaten Adobe Illustrator (AI), Postscript (EPS) och PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Information om hur du använder Dynamic Media för att förhandsgranska och generera dynamiska återgivningar för AI-filer finns i [Filformaten Adobe Illustrator (AI), Postscript (EPS) och PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Information om hur du använder Dynamic Media för att generera dynamiska renderingar för INDD-filer finns i [InDesign (INDD), filformat](../assets/managing-image-presets.md#indesign-indd-file-format).

## Dynamic Media - Rasterbildformat som stöds {#supported-raster-image-formats-dynamic-media}

| Format | Överför<br> (Indataformat) | Skapa<br> image<br> förinställning<br> (Utdataformat) | Förhandsgranska<br> dynamisk<br> rendering | Leverera<br> dynamisk<br> rendering | Hämta<br> dynamisk<br> rendering | Ange typer som stöder det här formatet |
|---|:---:|:---:|:---:|:---:|:---:| --- |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [Bild](/help/assets/image-sets.md), [Blandade media](/help/assets/mixed-media-sets.md)och [Snurra](/help/assets/spin-sets.md) |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [Bild](/help/assets/image-sets.md), [Blandade media](/help/assets/mixed-media-sets.md)och [Snurra](/help/assets/spin-sets.md) |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [Bild](/help/assets/image-sets.md), [Blandade media](/help/assets/mixed-media-sets.md)och [Snurra](/help/assets/spin-sets.md) |
| BMP | ✓ | - | - | - | - | [Bild](/help/assets/image-sets.md), [Blandade media](/help/assets/mixed-media-sets.md)och [Snurra](/help/assets/spin-sets.md) |
| PSD ‡ | ✓ | - | - | - | - | - |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| PICT | ✓ | - | - | - | - | - |

‡ Den sammanfogade bilden extraheras från filen PSD. Det är en bild som genereras av Adobe Photoshop och inkluderas i filen PSD. Beroende på inställningarna kan den sammanfogade bilden vara den faktiska bilden eller inte.

* Stödet för EPS-filer gäller endast för rasterbilder. Generering av miniatyrbilder för EPS-vektorbilder stöds till exempel inte som standard. Om du vill lägga till stöd [konfigurera ImageMagick](best-practices-for-imagemagick.md). Information om hur du integrerar tredjepartsverktyg för att aktivera ytterligare funktioner finns i [Kommandoradsbaserad mediehanterare](media-handlers.md#command-line-based-media-handler).

* Används [!DNL Dynamic Media] om du vill förhandsgranska och generera dynamiska återgivningar för EPS-filer, se [Filformaten Adobe Illustrator (AI), Postscript (EPS) och PDF.](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* För EPS-filer stöds tillbakaskrivning av metadata i PostScript Document Structuring Convention (PS-Adobe) version 3.0 eller senare.

## Dynamic Media - Rasterbildformat som inte stöds {#unsupported-image-formats-dynamic-media}

I följande lista beskrivs de undertyper av rasterbildfilformat som *not* stöds i Dynamic Media.

Se även [Identifiera filformat som inte stöds för Dynamic Media](https://helpx.adobe.com/experience-manager/kb/detect-unsupported-assets-for-dynamic-media.html) Kunskapsbasartikeln.

* PNG-filer som har en IDAT-segmentstorlek som är större än 100 MB.
* PSB-filer.
* PSD-filer med en annan färgmodell än CMYK, RGB, Gråskala eller Bitmapp stöds inte. Färgrymderna DuoTone, Lab och Indexed stöds inte.
* PSD-filer med ett bitdjup som är större än 16.
* TIFF-filer med flyttalsdata.
* TIFF-filer med Lab-färgrymd.

<!-- Topic commented out for now as of March 31, 2020. The topic may still need adjustment so it can be published live, or it may be moved into a KB article instead. Just waiting on feedback in CQDOC-15657. - Rick
## Unsupported raster image formats in Dynamic Media (#unsupported-image-formats-dynamic-media)

The following table describes the sub-types of raster image formats that are *not* supported in Dynamic Media. The table also describes suggested methods you can use to detect such files.

| Format | What is unsupported? | Suggested detection method |
|---|---|---|
| JPEG  | Files where the initial three bytes is incorrect. | To identify a JPEG file, its initial three bytes must be `ff d8 ff`. If they are anything else, then it is not classified as a JPEG.<br>&bull; There is no software tool that can help with this issue.<br>&bull; A small C++/java program which reads the initial three bytes of a file should be able to detect these types of files.<br>&bull; It may be better to track the source of such files and look at the tool generating the file. |
| PNG |  Files that have an IDAT chunk size greater than 100 MB. | You can detect this issue using [libpng](https://www.libpng.org/pub/png/libpng.html) in C++. |
| PSB |  | Use exiftool if the file type is PSB.<br>Example in an ExifTool log:<br>1. File type: `PSB` |
| PSD | Files with a color space other than CMYK, RGB, Grayscale, or Bitmap are not supported.<br>DuoTone, Lab, and Indexed color spaces are not supported. | Use ExifTool if Color mode is Duotone.<br>Example in an ExifTool log:<br>1. Color mode: `Duotone` |
|  | Files with abrupt endings. | Adobe is unable to detect this condition. Also, such files cannot be opened with Adobe PhotoShop. Adobe suggests you examine the tool that was used to create such a file and troubleshoot at the source. |
|  | Files that have a bit depth greater than 16. | Use ExifTool if the bit depth is greater than 16.<br>Example in an ExifTool log:<br>1. Bit depth: `32` |
|  | File that have Lab color space. | Use exiftool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
| TIFF | Files that have floating point data. That is, a TIFF file with 32-bit depth is not supported. | Use ExifTool if the MIME type is `image/tiff` and the SampleFormat has `Float` in its value. Example in an ExifTool log:<br>1. MIME type: `image/tiff`<br>Sample format: `Float #`<br>2. MIME type: `image/tiff`<br>Sample format: `Float; Float; Float; Float` |
|  | Files that have Lab color space. | Use ExifTool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
-->

## Dynamic Media - 3D-format som stöds {#supported-three-d-file-formats-in-dm}

Dynamic Media stöder följande 3D-format.

Se även [Arbeta med 3D-resurser i Dynamic Media](/help/assets/assets-3d.md).

| 3D-filtillägg | Filformat | MIME-typ | Anteckningar |
|---|---|---|---|
| GLB | Binär GL-överföring | model/gltf-binary | Materialen och texturerna inkluderas som en enda resurs. |
| OBJ | WaveFront 3D-objektfil | application/x-tgif |  |
| STL | Stereolitografi | application/vnd.ms-pki.stl |  |
| USDZ | Zip-arkiv för universell scenbeskrivning | model/vnd.usdz+zip | *Stöd endast för förtäring. ingen visning eller interaktion är tillgänglig.* USDZ är ett tillverkarspecifikt 3D-format som kan visas direkt på enheter med Safari och iOS. |

>[!MORELIKETHIS]
>
>* [Aktivera stöd för MIME-typbaserade resurser och Dynamic Media Classic överföringsjobbparametrar](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).
>* [Konfigurera MIME-typbaserad för stöd av överföringsjobbparametrar](config-dynamic.md).

