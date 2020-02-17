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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# FFmpeg for Communities {#ffmpeg-for-communities}

## Översikt {#overview}

FFmpeg är en lösning för konvertering och direktuppspelning av ljud och video. När den är installerad används den för korrekt transkodning av [videomaterial](../../help/sites-authoring/default-components-foundation.md#video) samt för AEM Communities-aktiveringsfunktion.

FFmpeg används i redigeringsmiljön för att hämta metadata för överförda aktiveringsresurser och generera en miniatyrbild som visas när aktiveringsresursen listas.

## Installerar FFmpeg {#installing-ffmpeg}

FFmpeg ska vara installerat på de servrar där AEM- *författarinstansen* finns.

1. Gå till [https://www.ffmpeg.org](https://www.ffmpeg.org/)
1. Ladda ned den senaste versionen av MPEG för just din miljö (Macintosh, Windows eller Linux)

   * det är viktigt att hålla MPEG uppdaterad på grund av säkerhetsluckor i äldre versioner

1. Installera MPEG enligt instruktionerna för operativsystemet.

1. Kontrollera att den körbara filen för FFmpeg har angetts i systemsökvägen.

   Du bör kunna köra MPEG från vilken katalog som helst i systemet.

   * for example, `ffmpeg -version`

## Konfigurera MPEG-omkodningstjänsten {#configure-ffmpeg-transcoding-service}

När FFmpeg är installerat konfigureras som standard flera återgivningar (transkoding) enligt arbetsflödesdefinitionen för DAM-uppdatering.

Eftersom omkodningarna är processorintensiva bör du ändra listan över målåtergivningar. I de flesta fall behövs inte omkodning.

Så här ändrar du arbetsflödet för DAM Update Asset, och i det här exemplet, för att inaktivera omkodning:

* Logga in på författarinstansen med administratörsbehörighet
* Från global navigering: **[!UICONTROL Verktyg > Arbetsflöde > Modeller]**
* Hitta **[!UICONTROL DAM-uppdateringsresurs]**
* Dubbelklicka för att öppna arbetsflödet för redigering i det klassiska användargränssnittet

   Resultatplats: [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* Dubbelklicka på **[!UICONTROL omkodningssteget]** för att öppna dialogrutan Stegegenskaper
* Under fliken **[!UICONTROL Process]** :

   * **[!UICONTROL Åklaganden]**: Rensa alla poster för att inaktivera omkodning Standardvärden: `profile:firefoxhq,profile:hq,profile:flv,profile:iehq`

![chlimage_1-372](assets/chlimage_1-372.png)

* Stäng **[!UICONTROL dialogrutan genom att klicka på]** OK `Step Properties`

* Välj **[!UICONTROL Spara]** för att spara `DAM Update Asset` arbetsflödet

   (övre vänstra hörnet)

