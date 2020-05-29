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
source-git-commit: 071f4a292343f0ad52ca3700c95bf60f03c307cc
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---


# Konfigurera komponenten Video {#configure-the-video-component}

Med [videokomponenten](/help/sites-authoring/default-components-foundation.md#video) kan du placera en fördefinierad, färdig videoresurs (OTB) på sidan.

För att korrekt omkodning ska ske installerar administratören FFmpeg separat. Se [Installera MPEG och konfigurera AEM](#install-ffmpeg). Administratörer [konfigurerar också videoprofiler](#configure-video-profiles) för HTML5-element.

## Konfigurera videoprofiler {#configure-video-profiles}

Definiera videoprofiler om du vill använda HTML5-element. De som väljs här används i ordning. Använd [designläget](/help/sites-authoring/default-components-designmode.md) (endast Classic UI) och välj **[!UICONTROL Profiles]** fliken:

![chlimage_1-317](assets/chlimage_1-317.png)

I den här dialogrutan kan du även konfigurera designen för videokomponenten och parametrar för [!UICONTROL Playback], [!UICONTROL Flash]och [!UICONTROL Advanced].

## Installera MPEG och konfigurera AEM {#install-ffmpeg}

Videokomponenten använder öppen källkod-produkten från tredje part för omkodning av videoklipp. Hämtat från [https://ffmpeg.org/](https://ffmpeg.org/). När du har installerat MPEG konfigurerar du AEM så att en viss ljudkodek och specifika körningsalternativ används.

Följ de här stegen för att installera **MPEG i Windows**:

1. Hämta den kompilerade binärfilen som `ffmpeg.zip`.
1. Avarkivera till en mapp.
1. Ställ in systemmiljövariabeln `PATH` på &lt;*your-ffmpeg-location*>`\bin`.
1. Starta om AEM.

Så här installerar du mpeg i **Mac OS X**:

1. Installera Xcode som finns på [developer.apple.com/xcode](hhttps://developer.apple.com/xcode/).
1. Installera på [XQuartz](https://www.xquartz.org) för att hämta [X11](https://support.apple.com/en-us/HT201341).
1. Installera MacPorts som finns på [www.macports.org](https://www.macports.org/).
1. Kör `sudo port install ffmpeg` kommandot på konsolen och följ instruktionerna på skärmen. Kontrollera att sökvägen till den `FFmpeg` körbara filen läggs till i `PATH` systemvariabeln.

Så här installerar du FFmpeg i **Mac OS X 10.6** med den förkompilerade versionen:

1. Ladda ned den förkompilerade versionen.
1. Avarkivera det i `/usr/local` katalogen.
1. Kör i konsolen `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`. Ändra banorna efter behov.

Så här **konfigurerar du AEM**:

>[!NOTE]
>
>Dessa steg är bara nödvändiga om du behöver anpassa kodekarna ytterligare.

1. Öppna [!UICONTROL CRXDE Lite] i webbläsaren. Gå till [http://localhost:4502/crx/de](http://localhost:4502/crx/de).
2. Markera `/libs/settings/dam/video/format_aac/jcr:content` noden och kontrollera att nodegenskaperna är följande:

   * `audioCodec` är `aac`.
   * `customArgs` är `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`.

3. Om du vill anpassa konfigurationen skapar du en övertäckning i `/apps/settings/` noden och flyttar samma struktur under `/conf/global/settings/` noden. Den kan inte redigeras i `/libs` noden. Om du till exempel vill täcka över en bana `/libs/settings/dam/video/fullhd-bp`skapar du den på `/conf/global/settings/dam/video/fullhd-bp`.

   >[!NOTE]
   >
   >Lägg över och redigera hela profilnoden och inte bara den egenskap som behöver ändras. Sådana resurser löses inte via SlingResourceMerger.

4. Om du har ändrat någon av egenskaperna klickar du på **[!UICONTROL Save All]**.

>[!NOTE]
>
>Ändringar av standardarbetsflödesmodellerna som är färdiga att användas (OTB) bevaras inte när du uppgraderar din AEM-instans. Adobe rekommenderar att du kopierar de ändrade arbetsflödesmodellerna innan du redigerar dem. Du kan till exempel kopiera OTB- [!UICONTROL DAM Update Asset] modellen innan du redigerar steget Fmpeg-omkodning i [!UICONTROL DAM Update Asset] modellen för att välja videoprofilnamn som fanns före uppgraderingen. Sedan kan du täcka över noden så att AEM kan hämta de anpassade ändringarna i OOTB-modellen `/apps` .
