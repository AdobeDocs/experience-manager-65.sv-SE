---
title: Format som stöds för resurser
description: Lista över filformat som stöds av AEM Resurser och funktioner som stöds för varje format.
contentOwner: AG
translation-type: tm+mt
source-git-commit: d7d25c75c1023383e07c36252ece2e85425a95be

---


# Format som stöds för resurser {#assets-supported-formats}

AEM Resurser har stöd för ett stort antal filformat och alla funktioner har olika stöd för olika MIME-typer.

Använd Adobes Extensible Metadata Platform (XMP) för att integrera AEM Assets med andra standardbaserade DAM-lösningar och datorprogramvara.

Använd teckenförklaringen för att förstå supportnivån.

| Supportnivå | Beskrivning |
|:---:|---|
| ✓ | Stöds |
| * | Stöds med tilläggsfunktioner |
| - | Ej relevant |

## Rasterbildformat som stöds {#supported-raster-image-formats}

Följande rasterbildformat stöds för filhanteringsfunktioner:

| Format | Lagring | Metadatahantering | Extrahering av metadata | Generering av miniatyrbilder | Interaktiv redigering | Återskrivning av metadata | Insikter |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| PNM | ✓ | ✓ |  |  |  |  | ✓ |
| PFM | ✓ | ✓ |  |  |  |  | ✓ |
| PBM | ✓ | ✓ |  |  |  |  | ✓ |
| PPM | ✓ | ✓ |  |  |  |  | ✓ |
| PSD **¹** | ✓ | ✓ | ✓ | ✓ |  |  | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ |  | ✓ |  |
| PICT |  |  |  |  |  |  | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ |  |  |  |

**¹** Den sammanfogade bilden extraheras från PSD-filen. Det är en bild som genereras av Adobe Photoshop och inkluderas i PSD-filen. Beroende på inställningarna kan den sammanfogade bilden vara den faktiska bilden eller inte.

Följande rasterbildformat stöds för Dynamic Media-funktioner:

| Format | Överför<br> (indataformat) | Skapa<br> bildförinställning<br><br> (utdataformat) | Förhandsgranska<br> dynamisk<br> återgivning | Leverera<br> dynamisk<br> återgivning | Hämta<br> dynamisk<br> återgivning |
|---|:---:|:---:|:---:|:---:|:---:|
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ |  |  |  |  |
| PSD **¹** | ✓ |  |  |  |  |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ |  |  |  |  |

**¹** Den sammanfogade bilden extraheras från PSD-filen. Det är en bild som genereras av Adobe Photoshop och inkluderas i PSD-filen. Beroende på inställningarna kan den sammanfogade bilden vara den faktiska bilden eller inte.

Utöver informationen ovan bör du tänka på följande:

* Stödet för EPS-filer gäller endast för rasterbilder. Generering av miniatyrbilder för EPS-vektorbilder stöds till exempel inte som standard. Om du vill lägga till stöd [konfigurerar du ImageMagick](best-practices-for-imagemagick.md). Information om hur du integrerar tredjepartsverktyg för att aktivera ytterligare funktioner finns i [Kommandoradsbaserad mediehanterare](media-handlers.md#command-line-based-media-handler).

* Metadatatillbakaskrivning fungerar för PSB-filformat när det läggs till i `NComm` hanteraren.

* Information om hur du använder Dynamic Media för att förhandsgranska och generera dynamiska renderingar för EPS-filer finns i [Adobe Illustrator (AI), PostScript (EPS) och PDF-filformat.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* För EPS-filer stöds tillbakaskrivning av metadata i PostScript Document Structuring Convention (PS-Adobe) version 3.0 eller senare.

## PDF Rasterizer-bibliotek som stöds {#supported-pdf-rasterizer-library}

Adobe PDF Rasterizer-biblioteket genererar högkvalitativa miniatyrbilder och förhandsgranskningar för stora och innehållsintensiva Adobe Illustrator- och PDF-filer. Adobe rekommenderar att du använder PDF-rastreringsbiblioteket för följande:

* Innehållsintensiva AI/PDF-filer som är resurskrävande att bearbeta.
* AI/PDF-filer, för vilka miniatyrer inte genereras som standard.
* AI-filer med Pantone Matching System-färger (PMS).

Se [Använda PDF-rastrering](aem-pdf-rasterizer.md).

## Bildkodningsbibliotek som stöds {#supported-image-transcoding-library}

Adobe Imaging Transcoding Library är en bildbehandlingslösning som utför viktiga bildhanteringsfunktioner som kodning, omkodning, omsampling och storleksändring.

Bildkonverteringsbiblioteket stöder JPG/JPEG, PNG (8-bitars och 16-bitars), GIF, BMP, TIFF/komprimerad TIFF (förutom 32-bitars TIFF-filer och PTIFF-filer), ICO- och ICN MIME-typer.

Se [Bildkonverteringsbibliotek](imaging-transcoding-library.md).

## Camera Raw som stöds {#supported-camera-raw}

Med Adobe Camera Raw-biblioteket kan AEM Resurser importera råbilder. Se [Stöd](camera-raw.md)för Camera Raw.

## Dokumentformat som stöds {#supported-document-formats}

Dokumentformat som stöds för filhanteringsfunktioner är följande:

| Format | Lagring | Metadatahantering<br> | Extrahering av metadata<br> | Generering av miniatyrbilder<br> | Interaktiv<br> redigering | Metadata<br> -tillbakaskrivning | [Insikter](touch-ui-asset-insights.md) | [Anslutna resurser](use-assets-across-connected-assets-instances.md) |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ |  |
| DOC | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| ODT | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| RTF | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| TXT | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| XLS | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| ODS | ✓ | ✓ | ✓ |  |  |  |  |  |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| ODP | ✓ | ✓ | ✓ |  |  |  |  |  |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ |  |
| PS | ✓ | ✓ |  |  |  |  |  |  |
| QXP | ✓ | ✓ |  |  |  |  |  |  |
| EPUB | ✓ | ✓ |  | ✓ | ✓ |  |  |  |

Dokumentformat som stöds för Dynamic Media-funktioner är följande:

| Format | Överför<br> (indataformat) | Skapa<br> bildförinställning<br><br> (utdataformat) | Förhandsgranska<br> dynamisk<br> återgivning | Leverera<br> dynamisk<br> återgivning | Hämta<br> dynamisk<br> återgivning |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ |  |  |  |  |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ |  |  |  |  |

Utöver ovanstående funktioner bör du tänka på följande:

* Information om hur du använder Dynamic Media för att generera dynamiska återgivningar för PDF-filer finns i [Adobe Illustrator (AI), Postscript (EPS) och PDF-filformat.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Information om hur du använder Dynamic Media för att förhandsgranska och generera dynamiska renderingar för AI-filer finns i [Adobe Illustrator (AI), PostScript (EPS) och PDF-filformat.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Information om hur du använder Dynamic Media för att generera dynamiska återgivningar för INDD-filer finns i [InDesign-filformat](../assets/managing-image-presets.md#indesign-indd-file-format)(INDD).

## Multimediaformat som stöds {#supported-multimedia-formats}

|  | Lagring | Metadatahantering | Extrahering av metadata | Generering av miniatyrbilder | FFMPEG-omkodning |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ |  | - | * |
| MIDI | ✓ | ✓ |  | - | * |
| 3GP | ✓ | ✓ |  | - | * |
| MP3 | ✓ | ✓ | ✓ | - | * |
| MPG | ✓ | ✓ |  | - | * |
| OGA | ✓ | ✓ |  | - | * |
| OGG | ✓ | ✓ |  | - | * |
| RA | ✓ | ✓ |  | - | * |
| WAV | ✓ | ✓ |  | - | * |
| WMA | ✓ | ✓ |  | - | * |
| DVI | ✓ | ✓ |  | * | * |
| FLV | ✓ | ✓ |  | * | * |
| M4V | ✓ | ✓ |  | * | * |
| MPEG | ✓ | ✓ |  | * | * |
| OGV | ✓ | ✓ |  | * | * |
| MOV | ✓ | ✓ |  | * | * |
| WMV | ✓ | ✓ |  | * | * |
| SWF | ✓ | ✓ |  |  |  |

## Videoformat som stöds för Dynamic Media Transcoding {#supported-input-video-formats-for-dynamic-media-transcoding}

| Videofiltillägg | Behållare | Rekommenderade videokodekar | Videokodekar som inte stöds |
|---|---|---|---|
| MP4 | MPEG-4 | H264/AVC (alla profiler) |  |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 &amp; HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, Apple Animation |
| FLV, F4V | Adobe Flash | H264/AVC, Flix VP6, H263, Sorenson | SWF (vektoranimeringsfiler) |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Microsoft-skärm (MSS2), Microsoft Photo Story (WVP2) |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 |  |
| M4V | Apple iTunes | H264/AVC |  |
| AVI | A/V-sammanflätning | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft Video 1 (MS-CRAM) |
| WebM | WebM | Google VP8 |  |
| OGV, OGG | Ogg | Theora, VP3, Dirac |  |
| MXF | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro |  |
| MTS | AVCHD | H264/AVC |  |
| MKV | Matroska | H264/AVC |  |
| R3D, RM | Red Raw-video | MJPEG 2000 |  |
| RAM, RM | RealVideo | Stöds inte | Real G2 (RV20), Real 8 (RV30), Real 10 (RV40) |
| FLAC | Inbyggd Flash | Kostnadsfri förlustfri ljudkodek |  |
| MJ2 | Motion JPEG 2000 | Motion JPEG 2000-kodek |  |

## Arkivformat som stöds {#supported-archive-formats}

De arkivformat som stöds och tillämpligheten för de vanliga DAM-arbetsflödena beskrivs i följande tabell.

| Format | Lagring | Versionshantering | Arbetsflöde | Publicering | Åtkomstkontroll | Dynamic Media Delivery |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## Andra format som stöds {#other-supported-formats}

Hur vanliga DAM-arbetsflöden kan användas för ett par andra filformat beskrivs i tabellen nedan. Den vanliga DAM-funktionen som lagring, versionshantering, ACL, arbetsflöde, publicering och metadatahantering, förutom Dynamic Media Delivery, stöds för alla filer.

| Format | Lagring | Versionshantering | Arbetsflöde | Publicering | Åtkomstkontroll | Dynamic Media Delivery |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript (när konfigureras med egen leveransdomän) |  |  |  |  |  | ✓ |

## MIME-typer som stöds {#supported-mime-types}

Som standard identifierar AEM filtypen med hjälp av filtillägget. AEM kan identifiera det från innehållet i filerna. För det senare alternativet [!UICONTROL Identifiera MIME från innehåll] i [!UICONTROL Day CQ DAM Mime Type Service] i AEM Web Console.

En lista över MIME-typer som stöds finns i CRXDE Lite på `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`.

Se [Konfigurera MIME-typbaserad för stöd](config-dynamic.md)för överföringsjobbparametrar.

Se även [Aktivera stöd](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support)för MIME-typbaserade resurser/Scene7-överföringsjobbparametrar.

| Filtillägg | MIME-typ/ Internetmedietyp | Standardvärde för jobParam | Tillåtet jobParam-värde |
|---|---|---|---|
| Bild | bild/s7resurs | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | Standardvärdet jobParam gäller för alla bildresurser av MIME-typ.<ul><li>[knockoutBackgroundOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_knockout_background_options.html)</li><li>manualCropOptions</li><li>[autoColorCropOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_auto_color_crop_options)</li><li>[autoTransparentCropOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_auto_transparent_crop_options)</li><li>[colorManagementOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_color_management_options.html)</li><li>[autoSetCreationOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_auto_set_creation_options.html)</li><li>[emailSetting](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/string_constants/index.html?f=r_email_settings)</li><li>[xmpKeywords](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_xmp_keywords)</li><li>[unsharpMaskOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_unsharp_mask_options.html)</li></ul> |
| 3G2 | video/3gpp2 |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| 3GP | video/3gpp |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_exclude_master_video_from_avs) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_post_script_options.html)</li><li> [illustratorOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_illustrator_options.html)</li></ul> |
| AIFF | audio/x-aiff |  |  |
| AVI | video/x-msvideo |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| BMP | image/bmp |  |  |
| CSS | text/css |  |  |
| DOC | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>program/steg</li><li>application/x-eps</li><li>bild/steg</li><li>image/x-eps</li></ul> |  |  |
| F4V | video/x-f4v |  | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | image/jpeg |  |  |
| M2V | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| M4V | video/x-m4v |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MOV | video/quicktime |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MPEG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MPG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_pdf_options) |
| PFB | application/x-font-type1 |  |  |
| PGM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | bild/png |  |  |
| PPT | application/vnd.ms |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_post_script_options)</li><li>[illustratorOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_illustrator_options)</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_photoshop_options)</li><li>[photoshopLayerOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_photoshop_layer_options.html)</li></ul> |
| RTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shockwave-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF/TIFF | bild/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | video/dvd |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| VTT | text/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| XLS | application/vnd.ms |  |  |
| ZIP | application/zip |  |  |

>[!MORELIKETHIS]
>
>* [Aktivera stöd](../sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support)för MIME-typbaserade resurser/Scene7-överföringsjobbparametrar.

