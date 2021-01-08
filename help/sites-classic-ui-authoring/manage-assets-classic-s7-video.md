---
title: Video
seo-title: Video
description: Med Assets får du centraliserad hantering av videoresurser där du kan överföra videor direkt till Assets för automatisk kodning till Dynamic Media Classic och få tillgång till Dy-videor direkt från Assets för sidredigering.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dfaa4b3f-f65a-4fe3-87a7-f3bc71015e56
translation-type: tm+mt
source-git-commit: 801d57bbe8a1bede6dcb4bf7884e5f71ddea1e83
workflow-type: tm+mt
source-wordcount: '1649'
ht-degree: 0%

---


# Video{#video}

Med resurser kan du centralisera hanteringen av videoresurser så att du kan överföra videor direkt till Assets för automatisk kodning till Dynamic Media Classic och få tillgång till Dynamic Media Classic-videor direkt från Assets för sidredigering.

Integrering med Dynamic Media Classic för video ger optimerad video även på alla skärmar (automatisk enhets- och bandbreddsidentifiering).

* Dynamic Media Classic-videokomponenten utför automatiskt enhets- och bandbreddsidentifiering för att spela upp video i rätt format och med rätt kvalitet på datorer, surfplattor och mobila enheter.
* Resurser - Du kan inkludera adaptiva videouppsättningar i stället för bara enskilda videoresurser. En adaptiv videouppsättning är en behållare för alla videoåtergivningar som krävs för att spela upp video sömlöst på flera skärmar. En adaptiv videouppsättning grupperar versioner av samma video som är kodade med olika bithastigheter och format som 400 kbit/s, 800 kbit/s och 1 000 kbit/s. Du använder en adaptiv videouppsättning, tillsammans med S7-videokomponenten, för adaptiv videoströmning på flera skärmar, inklusive stationära datorer, iOS, Android, Blackberry och Windows mobila enheter. Mer information finns i [Dynamic Media Classic-dokumentationen om adaptiva videouppsättningar](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/video/quick-start-video.html#video).

## Om FFMPEG och Dynamic Media Classic {#about-ffmpeg-and-scene}

Standardprocessen för videokodning bygger på den FFMPEG-baserade integrationen med videoprofiler. Därför innehåller det färdiga [!UICONTROL DAM Update Asset]-arbetsflödet följande två ffmpeg-baserade arbetsflödessteg:

* FFMPEG-miniatyrbilder
* FFMPEG-kodning

Tänk på att aktivering och konfigurering av integreringen med Dynamic Media Classic inte automatiskt tar bort eller inaktiverar dessa två arbetsflödessteg från det färdiga arbetsflödet för [!UICONTROL DAM Update Asset]-import. Om du redan använder den FFMPEG-baserade videokodningen i AEM är det troligt att du har FFMPEG installerat i dina redigeringsmiljöer. I det här fallet kodas en ny video som hämtas med Assets två gånger: en gång från FFMPEG-kodaren och en gång från Dynamic Media Classic-integreringen.

Om du har konfigurerat och installerat den FFMPEG-baserade videokodningen i AEM rekommenderar Adobe att du tar bort de två FFMPEG-arbetsflödena från dina [!UICONTROL DAM Update Asset]-arbetsflöden.

### Format som stöds {#supported-formats}

Följande format stöds för videokomponenten i Dynamic Media Classic:

* F4V H.264
* MP4 H.264

### Bestäm var videon ska överföras {#deciding-where-to-upload-your-video}

Hur du avgör var du ska överföra dina videoresurser beror på följande:

* Behöver du ett arbetsflöde för videoresursen?
* Behöver du versionskontroll för videoresursen?

Om svaret är ja på någon av eller båda dessa frågor överför du videon direkt till Adobe DAM. Om svaret är nej på båda frågorna överför du videon direkt till Dynamic Media Classic. Arbetsflödet för varje scenario beskrivs i följande avsnitt.

#### Om du överför videon direkt till Adobe Assets {#if-you-are-uploading-your-video-directly-to-adobe-assets}

Om du behöver ett arbetsflöde eller en versionshantering för dina resurser bör du överföra dem till Adobe Assets först. Här följer det rekommenderade arbetsflödet:

1. Ladda upp videomaterialet till Adobe Assets och koda och publicera automatiskt till Dynamic Media Classic.
1. I AEM kommer du åt videomaterial i WCM på fliken **[!UICONTROL Movies]** i Content Finder.
1. Skapa med videokomponenten i Dynamic Media Classic.

#### Om du överför din video till Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

Om du inte behöver ett arbetsflöde eller en versionshantering för dina resurser bör du överföra dina resurser till Dynamic Media Classic. Här följer det rekommenderade arbetsflödet:

1. [Konfigurera en schemalagd FTP-överföring och -kodning till Dynamic Media Classic (automatiskt system)](https://help.adobe.com/en_US/scene7/using/WS70B173EC-4CAD-4b4c-BF9C-43A11F3A5950.html) i Dynamic Media Classic-datorprogrammet.
1. I AEM kommer du åt videomaterial i WCM på fliken **[!UICONTROL Dynamic Media Classic]** i Content Finder.
1. Skapa med videokomponenten i Dynamic Media Classic.

### Konfigurera integrering med Dynamic Media Classic Video {#configuring-integration-with-scene-video}

**Så här konfigurerar du universella förinställningar**:

1. I **[!UICONTROL Cloud Services]** navigerar du till din **[!UICONTROL Dynamic Media Classic]**-konfiguration och klickar på **[!UICONTROL Edit.]**
1. Välj fliken **[!UICONTROL Video]**.

   >[!NOTE]
   >
   >Fliken **[!UICONTROL Video]** visas inte om sidan inte har någon molnkonfiguration. Se [Aktivera Dynamic Media Classic för WCM](#enablingscene7forwcm).

1. Välj den adaptiva videokodningsprofilen, en färdig videokodningsprofil eller en anpassad videokodningsprofil.

   >[!NOTE]
   >
   >Mer information om vad videoförinställningarna betyder finns i [Videoförinställningar för kodning av videofiler](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html?lang=en#video-presets-for-encoding-video-files).
   >
   >Adobe rekommenderar att du antingen markerar båda adaptiva videouppsättningar när du konfigurerar de universella förinställningarna eller väljer alternativet **[!UICONTROL Adaptive Video Encoding]**.

1. De valda kodningsprofilerna tillämpas automatiskt på alla videoklipp som överförs till CQ DAM-målmappen som du konfigurerar för den här Dynamic Media Classic-molnkonfigurationen. Du kan konfigurera flera Dynamic Media Classic-molnkonfigurationer med olika målmappar för att tillämpa olika kodningsprofiler efter behov.

### Uppdaterar förinställningar för visningsprogram och kodning {#updating-viewer-and-encoding-presets}

Om du behöver uppdatera visningsprogrammet och kodningsförinställningarna för video i AEM eftersom förinställningarna har uppdaterats i Dynamic Media Classic går du till Dynamic Media Classic-konfigurationen i molnkonfigurationen och klickar på **Uppdatera visningsprogrammet och kodningsförinställningarna**.

![chlimage_1-131](assets/chlimage_1-131.png)

### Överför din primära källvideo {#uploading-your-master-video}

Så här överför du din primära källvideo till Dynamic Media Classic från Adobe DAM:

1. Navigera till målmappen för CQ DAM där du har konfigurerat molnkonfigurationen med kodningsprofiler för Dynamic Media Classic.
1. Klicka på **[!UICONTROL Upload]** för att överföra primärt källvideoklipp. Överföringen och kodningen av videon är klar när arbetsflödet [!UICONTROL DAM Update Asset] är klart och **[!UICONTROL Publish to Dynamic Media Classic]** är markerat.

   >[!NOTE]
   >
   >Det kan ta en stund innan videominiatyrbilderna genereras.

   Om du drar den primära källvideon för DAM till videokomponenten kommer du åt *alla* av de Dynamic Media Classic-kodade proxyåtergivningarna för leverans.

### Foundation Video Component jämfört med Dynamic Media Classic Video Component {#foundation-video-component-versus-scene-video-component}

När du använder AEM har du tillgång till både videokomponenten som är tillgänglig i Sites och videokomponenten i Dynamic Media Classic. Dessa komponenter är inte utbytbara.

Videokomponenten Dynamic Media Classic fungerar bara för Dynamic Media Classic-videofilmer. Grundkomponenten fungerar med videor som lagras från AEM (med ffmpeg) och Dynamic Media Classic-videor.

I följande matris förklaras när du bör använda vilken komponent:

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>Dynamic Media Classic-videokomponenten använder den universella videoprofilen. Du kan dock hämta den HTML5-baserade videospelaren som kan användas av AEM. I Dynamic Media Classic kopierar du inbäddningskoden för den färdiga HTML5-videospelaren och placerar den på AEM.


## AEM videokomponent {#aem-video-component}

Även om du bör använda videokomponenten för Dynamic Media Classic för att visa Dynamic Media Classic-videofilmer beskrivs det här avsnittet hur du använder Dynamic Media Classic-videofilmer med [!UICONTROL Foundation Video Component] i AEM, för fullständighetens skull.

### AEM Video och Dynamic Media Classic Video-jämförelse {#aem-video-and-scene-video-comparison}

I följande tabell visas en högnivåjämförelse av funktioner som stöds mellan AEM Foundation Video-komponenten och Dynamic Media Classic Video-komponenten:

|  | AEM Foundation Video | Dynamic Media Classic-video |
|---|---|---|
| Metod | HTML5 first approach. Flash används endast för icke-HTML5-reservlösningar. | Flash på de flesta stationära datorer. HTML5 används för mobiler och surfplattor. |
| Leverans | Progressiv | Adaptiv strömning |
| Spårning | Ja | Ja |
| Utbyggbarhet | Ja | Nej |
| Mobilvideo | Ja | Ja |

### Konfigurera {#setting-up}

#### Skapar videoprofiler {#creating-video-profiles}

De olika videokodningarna skapas enligt de kodningsförinställningar för Dynamic Media Classic som valts i molnkonfigurationen för Dynamic Media Classic. För att den grundläggande videokomponenten ska kunna använda dem måste en videoprofil skapas för varje vald kodningsförinställning för Dynamic Media Classic. Detta gör att videokomponenten kan välja DAM-återgivningar utifrån detta.

>[!NOTE]
>
>Nya videoprofiler och ändringar av dem måste aktiveras för publicering.

1. I AEM går du till **[!UICONTROL Tools]** och väljer **[!UICONTROL Configuration Console.]** Gå till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Video Profiles]** i navigeringsträdet i Configuration Console.
1. Skapa en ny Dynamic Media Classic-videoprofil. På menyn **[!UICONTROL New...]** väljer du **[!UICONTROL Create Page]** och sedan Dynamic Media Classic Video Profile-mallen. Ge den nya videoprofilsidan ett namn och klicka på **[!UICONTROL Create.]**

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. Redigera den nya videoprofilen. Välj molnkonfigurationen först. Välj sedan samma kodningsförinställning som du valde i molnkonfigurationen.

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | Egenskap | Beskrivning |
   |---|---|
   | Dynamic Media Classic Cloud-konfiguration | Den molnkonfiguration som ska användas för kodningsförinställningarna. |
   | Dynamic Media Classic-kodningsförinställning | Den kodningsförinställning som den här videoprofilen ska kopplas till. |
   | HTML5-videotyp | Med den här egenskapen kan du ange värdet för type-egenskapen i HTML5-videokällelementet. Den här informationen finns inte i kodningsförinställningarna för Dynamic Media Classic, men krävs för att återge videoklippen med HTML5-videoelementet. En lista över vanliga format tillhandahålls, men kan skrivas över för andra format. |

   Upprepa det här steget för alla kodningsförinställningar som är markerade i molnkonfigurationen och som du vill använda i videokomponenten.

#### Konfigurerar design {#configuring-design}

Grundvideokomponenten måste känna till vilka videoprofiler som ska användas för att skapa listan över videokällor. Du måste öppna dialogrutan för videokomponentdesign och konfigurera komponentdesignen för de nya videoprofilerna.

>[!NOTE]
>
>Om du använder den grundläggande videokomponenten på en mobilsida kan du behöva upprepa de här stegen när du designar mobilsidan.

>[!NOTE]
>
>Ändringar i designen kräver att designen aktiveras för att börja gälla vid publiceringen.

1. Öppna bildvideokomponentens designdialogruta och växla till fliken **[!UICONTROL Profiles]**. Ta sedan bort färdiga profiler och lägg till de nya videoprofilerna i Dynamic Media Classic. Ordningen på profillistan i designdialogrutan definierar också ordningen på videokällelementet vid återgivning.
1. För webbläsare som inte stöder HTML5 kan videokomponenten konfigurera ett flash-reserv. Öppna dialogrutan för design av videokomponenter och ändra till fliken **[!UICONTROL Flash]**. Konfigurera Flash Player-inställningarna och tilldela en reservprofil för Flash Player.

#### Checklista {#checklist}

1. Skapa en Dynamic Media Classic-molnkonfiguration. Kontrollera att förinställningarna för videokodning är angivna och att importeraren körs.
1. Skapa en Dynamic Media Classic-videoprofil för varje videokodningsförinställning som har valts i molnkonfigurationen.
1. Videoprofilerna måste aktiveras.
1. Konfigurera utformningen av den grundläggande videokomponenten på sidan.
1. Aktivera designen när du är klar med designändringarna.

