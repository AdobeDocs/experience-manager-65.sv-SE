---
title: Konfigurera komponenten Video
seo-title: Konfigurera komponenten Video
description: Lär dig hur du konfigurerar videokomponenten.
seo-description: Lär dig hur du konfigurerar videokomponenten.
uuid: f4755a13-08ea-4096-a951-46a590f8d766
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: a1efef3c-0e4b-4a17-bcad-e3cc17adbbf7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konfigurera komponenten Video {#configure-the-video-component}

Med [videokomponenten](/help/sites-authoring/default-components-foundation.md#video) kan du placera ett fördefinierat OTB-videoelement (körklar) på sidan.

För att korrekt omkodning ska fungera måste administratören [installera MPEG och konfigurera AEM](#install-ffmpeg) separat. De kan också [konfigurera videoprofilerna](#configure-video-profiles) för användning med HTML5-element.

## Konfigurera videoprofiler {#configure-video-profiles}

Du kanske vill definiera videoprofiler som ska användas för HTML5-element. De som väljs här används i ordning. Använd [designläget](/help/sites-authoring/default-components-designmode.md) (endast Classic UI) och välj fliken **[!UICONTROL Profiler]** :

![chlimage_1-317](assets/chlimage_1-317.png)

Du kan också konfigurera designen för videokomponenter och parametrar för [!UICONTROL Uppspelning], [!UICONTROL Flash]och [!UICONTROL Avancerat].

## Installera MPEG och konfigurera AEM {#install-ffmpeg}

Video Component (videokomponenten) använder öppen källkod-produkten från tredje part för korrekt omkodning av videofilmer som kan hämtas från [https://ffmpeg.org/](https://ffmpeg.org/). När du har installerat MPEG måste du konfigurera AEM så att en viss ljudkodek och specifika körningsalternativ används.

**Så här installerar du FFmpeg för din plattform**:

* **I Windows:**

   1. Hämta den kompilerade binärfilen som `ffmpeg.zip`
   1. Zippa upp i en mapp.
   1. Ställ in systemmiljövariabeln `PATH` på `<*your-ffmpeg-locatio*n>\bin`
   1. Starta om AEM.

* **I Mac OS X:**

   1. Installera Xcode ([https://developer.apple.com/technologies/tools/xcode.html](https://developer.apple.com/technologies/tools/xcode.html))
   1. Installera XQuartz/X11.
   1. Installera MacPorts ([https://www.macports.org/](https://www.macports.org/))
   1. Kör följande kommando i konsolen och följ instruktionerna:

      `sudo port install ffmpeg`

      `FFmpeg` måste vara i `PATH` så att AEM kan hämta det via kommandoraden.

* **Använda den förkompilerade versionen för OS X 10.6:**

   1. Ladda ned den förkompilerade versionen.
   1. Extrahera den till `/usr/local` katalogen.
   1. Kör från terminal:

      `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`

**Så här konfigurerar du AEM**:

1. Öppna [!UICONTROL CRXDE Lite] i webbläsaren. ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))
1. Markera `/libs/settings/dam/video/format_aac/jcr:content` noden och kontrollera att nodegenskaperna är följande:

   * audioCodec:

      ```
       aac
      ```

   * customArgs:

      ```
       -flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8
      ```

1. Om du vill anpassa konfigurationen skapar du en övertäckning i `/apps/settings/` noden och flyttar samma struktur under `/conf/global/settings/` noden. Den kan inte redigeras i `/libs` noden. Om du till exempel vill täcka över en bana `/libs/settings/dam/video/fullhd-bp`skapar du den på `/conf/global/settings/dam/video/fullhd-bp`.

   >[!NOTE]
   >
   >Lägg över och redigera hela profilnoden och inte bara den egenskap som behöver ändras. Sådana resurser löses inte via SlingResourceMerger.

1. Om du har ändrat någon av egenskaperna klickar du på **[!UICONTROL Spara alla]**.

>[!NOTE]
>
>Arbetsflödesmodeller från OTB bevaras inte när du uppgraderar din AEM-instans. Adobe rekommenderar att du kopierar OOTB-arbetsflödesmodeller innan du redigerar dem. Kopiera till exempel OTB DAM Update Asset-modellen innan du redigerar omkodningssteget för MPEG i DAM Update Asset-modellen för att välja videoprofilnamn som fanns före uppgraderingen. Sedan kan du täcka över noden så att AEM kan hämta de anpassade ändringarna i OOTB-modellen `/apps` .

