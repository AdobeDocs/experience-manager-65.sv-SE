---
title: FFmpeg for Communities
seo-title: FFmpeg for Communities
description: Installera och konfigurera MPEG för Communities
seo-description: Installera och konfigurera MPEG för Communities
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
translation-type: tm+mt
source-git-commit: 299c4cb377c65e49b94383704a906fdd0bb38d06
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 1%

---


# FFmpeg för Communities {#ffmpeg-for-communities}

## Översikt {#overview}

FFmpeg är en lösning för konvertering och direktuppspelning av ljud och video och används, när den är installerad, för korrekt omkodning av [videomaterial](../../help/sites-authoring/default-components-foundation.md#video) samt för AEM Communities aktiveringsfunktion.

FFmpeg används i redigeringsmiljön för att hämta metadata för överförda aktiveringsresurser och generera en miniatyrbild som visas när aktiveringsresursen listas.

## Installerar FFmpeg {#installing-ffmpeg}

FFmpeg ska vara installerat på de servrar som är värd för AEM *författare* instans(er).

1. Gå till [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. Ladda ned den senaste versionen av MPEG för just din miljö (Macintosh, Windows eller Linux).

   * Det är viktigt att hålla MPEG uppdaterad på grund av säkerhetsluckor i äldre versioner.

1. Installera MPEG enligt instruktionerna för operativsystemet.

1. Kontrollera att den körbara filen för FFmpeg har angetts i systemsökvägen.

   Du bör kunna köra MPEG från vilken katalog som helst i systemet.

   * Till exempel, `ffmpeg -version`.

## Konfigurera MPEG-omkodningstjänsten {#configure-ffmpeg-transcoding-service}

När FFmpeg är installerat konfigureras som standard flera renderingar (transkoding) enligt arbetsflödesdefinitionen [!UICONTROL DAM Update Asset].

Eftersom omkodningarna är processorintensiva bör du ändra listan över målåtergivningar. I de flesta fall behövs inte omkodning.

Så här ändrar du arbetsflödet för [!UICONTROL DAM Update Asset] och i det här exemplet stänger du av omkodning:

* Logga in på författarinstansen med administratörsbehörighet.
* Navigera från global navigering till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
* Leta reda på **[!UICONTROL DAM Update Asset]**.
* Dubbelklicka för att öppna arbetsflödet för redigering i det klassiska användargränssnittet.

   Resultatplats: [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* Dubbelklicka på **[!UICONTROL FFmpeg transcoding]**-steget för att öppna dialogrutan Stegegenskaper.
* Under fliken **[!UICONTROL Process]**:

   * **[!UICONTROL Arugments]**: Rensa alla poster för att inaktivera omkodning Standardvärden:  `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

   ![chlimage_1-372](assets/chlimage_1-372.png)

* Välj **[!UICONTROL OK]** för att stänga dialogrutan `Step Properties`.

* Välj **[!UICONTROL Save]** om du vill spara arbetsflödet för `DAM Update Asset`.



