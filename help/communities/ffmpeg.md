---
title: FFmpeg for Communities
description: Installera och konfigurera MPEG för Communities
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# FFmpeg for Communities {#ffmpeg-for-communities}

## Ökning {#overview}

FFmpeg är en lösning för konvertering och direktuppspelning av ljud och video. När den är installerad används den för korrekt omkodning av [videomaterial](../../help/sites-authoring/default-components-foundation.md#video).

## Installerar FFmpeg {#installing-ffmpeg}

FFmpeg ska vara installerat på servern/servrarna som är värd för AEM *author* instans(er).

1. Gå till [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. Hämta den senaste versionen av MPEG för just din miljö (Macintosh, Windows eller Linux).

   * Det är viktigt att hålla MPEG uppdaterad på grund av säkerhetsluckor i äldre versioner.

1. Installera MPEG enligt instruktionerna för operativsystemet.

1. Kontrollera att den körbara filen för FFmpeg har angetts i systemsökvägen.

   Du bör kunna köra MPEG från vilken katalog som helst i systemet.

   * Exempel: `ffmpeg -version`.

## Konfigurera MPEG-omkodningstjänsten {#configure-ffmpeg-transcoding-service}

När FFmpeg är installerat konfigureras som standard flera renderingar (transkoding) enligt arbetsflödesdefinitionen [!UICONTROL DAM Update Asset].

Eftersom omkodningarna är processorintensiva bör du ändra listan över målåtergivningar. I de flesta fall behövs inte omkodning.

Så här ändrar du arbetsflödet [!UICONTROL DAM Update Asset] och i det här exemplet stänger du av omkodning:

* Logga in på författarinstansen med administratörsbehörighet.
* Navigera från global navigering till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
* Sök efter **[!UICONTROL DAM Update Asset]**.
* Dubbelklicka för att öppna arbetsflödet för redigering i det klassiska användargränssnittet.

  Resultatplats: [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* Dubbelklicka på steget **[!UICONTROL FFmpeg transcoding]** för att öppna dialogrutan Stegegenskaper.
* Under fliken **[!UICONTROL Process]**:

   * **[!UICONTROL Arugments]**: Rensa alla poster om du vill inaktivera standardvärden för omkodning: `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

  ![configure-ffmpeg](assets/configure-ffmpeg.png)

* Välj **[!UICONTROL OK]** för att stänga dialogrutan `Step Properties`.

* Välj **[!UICONTROL Save]** om du vill spara arbetsflödet för `DAM Update Asset`.
