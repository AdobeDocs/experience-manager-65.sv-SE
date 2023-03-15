---
title: FFmpeg for Communities
seo-title: FFmpeg for Communities
description: Installera och konfigurera MPEG för Communities
seo-description: How to install and configure FFmpeg for Communities
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
role: Admin
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 1%

---

# FFmpeg for Communities {#ffmpeg-for-communities}

## Översikt {#overview}

FFmpeg är en lösning för konvertering och direktuppspelning av ljud och video och används, när den är installerad, för korrekt transkodning av [videomaterial](../../help/sites-authoring/default-components-foundation.md#video) samt för AEM Communities aktiveringsfunktion.

FFmpeg används i redigeringsmiljön för att hämta metadata för överförda aktiveringsresurser och generera en miniatyrbild som visas när aktiveringsresursen listas.

## Installerar FFmpeg {#installing-ffmpeg}

FFmpeg ska vara installerat på de servrar där AEM finns *författare* instans(er).

1. Gå till [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. Ladda ned den senaste versionen av MPEG för just din miljö (Macintosh, Windows eller Linux).

   * Det är viktigt att hålla MPEG uppdaterad på grund av säkerhetsluckor i äldre versioner.

1. Installera MPEG enligt instruktionerna för operativsystemet.

1. Kontrollera att den körbara filen för FFmpeg har angetts i systemsökvägen.

   Du bör kunna köra MPEG från vilken katalog som helst i systemet.

   * Till exempel, `ffmpeg -version`.

## Konfigurera MPEG-omkodningstjänsten {#configure-ffmpeg-transcoding-service}

När FFmpeg är installerat konfigureras som standard flera återgivningar (omkodningar) enligt [!UICONTROL DAM Update Asset] arbetsflödesdefinition.

Eftersom omkodningarna är processorintensiva bör du ändra listan över målåtergivningar. I de flesta fall behövs inte omkodning.

Ändra [!UICONTROL DAM Update Asset] arbetsflöde och i det här exemplet för att inaktivera omkodning:

* Logga in på författarinstansen med administratörsbehörighet.
* Navigera från global navigering till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
* Sök **[!UICONTROL DAM Update Asset]**.
* Dubbelklicka för att öppna arbetsflödet för redigering i det klassiska användargränssnittet.

   Resultatplats: [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* Dubbelklicka på **[!UICONTROL FFmpeg transcoding]** för att öppna dialogrutan Stegegenskaper.
* Under **[!UICONTROL Process]** tab:

   * **[!UICONTROL Arugments]**: Rensa alla poster för att inaktivera omkodning Standardvärden: `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

   ![configure-ffmpeg](assets/configure-ffmpeg.png)

* Välj **[!UICONTROL OK]** för att stänga `Step Properties` -dialogrutan.

* Välj **[!UICONTROL Save]** för att spara `DAM Update Asset` arbetsflöde.
