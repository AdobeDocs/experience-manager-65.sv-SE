---
title: Konfigurera komponenten Video
description: Lär dig hur du använder videokomponenten i Adobe Experience Manager för att placera en fördefinierad, färdig videoresurs på sidan.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 9c97f99e-d6ef-4817-8b2a-201ab22f2b38
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# Konfigurera komponenten Video {#configure-the-video-component}

The [Videokomponent](/help/sites-authoring/default-components-foundation.md#video) Med kan du placera en fördefinierad, färdig videoresurs på sidan.

För att korrekt omkodning ska ske installerar administratören FFmpeg separat. Se [Installera och konfigurera AEM](#install-ffmpeg). Administratörer kan också [Konfigurera videoprofiler](#configure-video-profiles) för användning med HTML5-element.

>[!CAUTION]
>
>Den här Foundation-komponenten har tagits bort. Adobe rekommenderar att du använder [Bädda in komponent för kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/embed.html) i stället.

>[!CAUTION]
>
>Den här komponenten förväntas inte längre fungera utan omfattande anpassning på projektnivå.

## Konfigurera videoprofiler {#configure-video-profiles}

Definiera videoprofiler om du vill använda HTML5-element. De som väljs här används i ordning. Använd [Designläge](/help/sites-authoring/default-components-designmode.md) (Endast Classic UI) och välj **[!UICONTROL Profiles]** tab:

![chlimage_1-317](assets/chlimage_1-317.png)

I den här dialogrutan kan du även konfigurera designen för videokomponenten och parametrar för [!UICONTROL Playback], [!UICONTROL Flash]och [!UICONTROL Advanced].

## Installera och konfigurera AEM {#install-ffmpeg}

Videokomponenten använder öppen källkod-produkten från tredje part för omkodning av videoklipp. Hämtat från [https://ffmpeg.org/](https://ffmpeg.org/). När du har installerat mpeg konfigurerar du AEM att använda en viss ljudkodek och specifika körningsalternativ.

Så här installerar du FlashPeg på **Windows** gör du så här:

1. Hämta den kompilerade binärfilen som `ffmpeg.zip`.
1. Avarkivera till en mapp.
1. Ange systemmiljövariabeln `PATH` till &lt;*your-ffmpeg-location*>`\bin`.
1. Starta om AEM.

Så här installerar du FlashPeg på **MACOS X** gör du så här:

1. Install Xcode available at [developer.apple.com/xcode](https://developer.apple.com/xcode/).
1. Installationen finns på [XQuartz](https://www.xquartz.org) för att [X11](https://support.apple.com/en-us/100724).
1. Installera MacPorts som finns på [www.macports.org](https://www.macports.org/).
1. Kör i konsolen `sudo port install ffmpeg` och följ instruktionerna på skärmen. Se till att sökvägen till `FFmpeg` körbar fil läggs till i `PATH` systemvariabel.

Så här installerar du FlashPeg på **macOS X 10.6** gör du så här i den förkompilerade versionen:

1. Hämta den förkompilerade versionen.
1. Avarkivera det på `/usr/local` katalog.
1. Kör i konsolen `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`. Ändra sökvägen efter behov.

Till **konfigurera AEM** gör du så här:

>[!NOTE]
>
>Dessa steg är bara nödvändiga om du behöver anpassa kodekarna ytterligare.

1. Öppna [!UICONTROL CRXDE Lite] i webbläsaren. Åtkomst [http://localhost:4502/crx/de](http://localhost:4502/crx/de).
2. Välj `/libs/settings/dam/video/format_aac/jcr:content` nod och kontrollera att nodegenskaperna är följande:

   * `audioCodec` är `aac`.
   * `customArgs` är `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`.

3. Om du vill anpassa konfigurationen skapar du en övertäckning i `/apps/settings/` nod och flytta samma struktur under `/conf/global/settings/` nod. Det kan inte redigeras i `/libs` nod. Till exempel för att täcka över bana `/libs/settings/dam/video/fullhd-bp`, skapa på `/conf/global/settings/dam/video/fullhd-bp`.

   >[!NOTE]
   >
   >Täck över och redigera hela profilnoden och inte bara den egenskap som behöver ändras. Sådana resurser löses inte via SlingResourceMerger.

4. Om du har ändrat någon av egenskaperna klickar du på **[!UICONTROL Save All]**.

>[!NOTE]
>
>Ändringar i standardarbetsflödesmodellerna som är färdiga bevaras inte när du uppgraderar AEM. Adobe rekommenderar att du kopierar de ändrade arbetsflödesmodellerna innan du redigerar dem. Du kan till exempel kopiera den färdiga filen [!UICONTROL DAM Update Asset] modellen innan du redigerar steget för FFmpeg-omkodning i [!UICONTROL DAM Update Asset] modell för att välja videoprofilnamn som fanns före uppgraderingen. Sedan kan du täcka över `/apps` nod som AEM kan hämta anpassade ändringar i modellen som är klar att användas.
