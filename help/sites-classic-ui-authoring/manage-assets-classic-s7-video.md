---
title: Video i Sites Classic Authoring
description: Med resurser får du centraliserad hantering av videoresurser där du kan överföra videor direkt till Assets för automatisk kodning till Dynamic Media Classic och få tillgång till Dy-videor direkt från Assets för sidredigering.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: c540aa49-9981-4e8c-97df-972085b26490
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1613'
ht-degree: 0%

---

# Video{#video}

Med resurser får du centraliserad hantering av videoresurser där du kan överföra videor direkt till Assets för automatisk kodning till Dynamic Media Classic och få tillgång till Dynamic Media Classic videor direkt från Assets för sidredigering.

Tack vare Dynamic Media Classic videointegration kan optimerad video även användas på alla skärmar (automatisk enhets- och bandbreddsidentifiering).

* Dynamic Media Classic videokomponent utför automatiskt enhets- och bandbreddsidentifiering för att spela upp video i rätt format och med rätt kvalitet på datorer, surfplattor och mobiler.
* Resurser - Du kan inkludera adaptiva videouppsättningar i stället för bara enskilda videoresurser. En adaptiv videouppsättning är en behållare för alla videoåtergivningar som krävs för att spela upp video sömlöst på flera skärmar. En adaptiv videouppsättning grupperar versioner av samma video som är kodade med olika bithastigheter och format som 400 kbit/s, 800 kbit/s och 1 000 kbit/s. Du använder en adaptiv videouppsättning, tillsammans med S7-videokomponenten, för adaptiv videoströmning på flera skärmar, inklusive datorer, iOS, Android™, BlackBerry® och Windows mobila enheter. Se [Dynamic Media Classic dokumentation om adaptiva videouppsättningar för mer information](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/video/quick-start-video.html#video).

## Om FFMPEG och Dynamic Media Classic {#about-ffmpeg-and-scene}

Standardprocessen för videokodning bygger på den FFMPEG-baserade integrationen med videoprofiler. Därför är det en färdig lösning [!UICONTROL DAM Update Asset] arbetsflödet innehåller följande två ffmpeg-baserade arbetsflödessteg:

* FFMPEG-miniatyrbilder
* FFMPEG-kodning

Om du aktiverar och konfigurerar Dynamic Media Classic-integreringen tas inte dessa två arbetsflödessteg bort automatiskt från körklart [!UICONTROL DAM Update Asset] arbetsflöde för förtäring. Om du redan använder FFMPEG-baserad videokodning i Adobe Experience Manager är det troligt att du har FFMPEG installerat i dina redigeringsmiljöer. I det här fallet kodas en ny videofil som har importerats med Experience Manager Assets två gånger: en gång från FFMPEG-kodaren och en gång från Dynamic Media Classic-integreringen.

Om du har konfigurerat och installerat den FFMPEG-baserade videokodningen i Experience Manager rekommenderar Adobe att du tar bort de två FFMPEG-arbetsflödena från [!UICONTROL DAM Update Asset] arbetsflöden.

### Format som stöds {#supported-formats}

Följande format stöds för komponenten Dynamic Media Classic Video:

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
1. I Experience Manager får du tillgång till videomaterial i WCM i **[!UICONTROL Movies]** -fliken i Content Finder.
1. Skapa med Dynamic Media Classic video- eller grundvideokomponent.

#### Om du överför din video till Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

Om du inte behöver ett arbetsflöde eller en versionshantering för dina resurser bör du överföra dina resurser till Dynamic Media Classic. Här följer det rekommenderade arbetsflödet:

1. I Dynamic Media Classic-datorprogrammet [konfigurera en schemalagd FTP-överföring och -kodning till Dynamic Media Classic (automatisk systeminstallation)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#upload-options).
1. I Experience Manager får du tillgång till videomaterial i WCM i **[!UICONTROL Dynamic Media Classic]** -fliken i Content Finder.
1. Skapa med Dynamic Media Classic videokomponent.

### Konfigurera integrering med Dynamic Media Classic Video {#configuring-integration-with-scene-video}

1. I **[!UICONTROL Cloud Services]** navigera till **[!UICONTROL Dynamic Media Classic]** konfigurera och välja **[!UICONTROL Edit]**.
1. Välj **[!UICONTROL Video]** -fliken.

   >[!NOTE]
   >
   >The **[!UICONTROL Video]** visas inte om sidan inte har någon molnkonfiguration. Se [Aktivera Dynamic Media Classic för WCM](#enablingscene7forwcm).

1. Välj den adaptiva videokodningsprofilen, en färdig videokodningsprofil eller en anpassad videokodningsprofil.

   >[!NOTE]
   >
   >Mer information om vad videoförinställningarna betyder finns i [Videoförinställningar för kodning av videofiler](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files).
   >
   >Adobe rekommenderar att du antingen väljer båda adaptiva videouppsättningar när du konfigurerar de universella förinställningarna eller väljer **[!UICONTROL Adaptive Video Encoding]** alternativ.

1. De valda kodningsprofilerna tillämpas automatiskt på alla videoklipp som överförs till CQ DAM-målmappen som du konfigurerar för den här Dynamic Media Classic-molnkonfigurationen. Du kan konfigurera flera Dynamic Media Classic molnkonfigurationer med olika målmappar för att tillämpa olika kodningsprofiler efter behov.

### Uppdatera visningsprogram och kodningsförinställningar {#updating-viewer-and-encoding-presets}

Uppdatera visnings- och kodningsförinställningarna för video i Experience Manager om förinställningarna uppdaterades i Dynamic Media Classic. I så fall går du till Dynamic Media Classic-konfigurationen i molnkonfigurationen och väljer **Uppdatera visningsprogrammet och kodningsförinställningarna**.

![chlimage_1-131](assets/chlimage_1-131.png)

### Överför din primära källvideo {#uploading-your-master-video}

Så här överför du din primära källvideo till Dynamic Media Classic från Adobe DAM:

1. Navigera till målmappen för CQ DAM där du har konfigurerat molnkonfigurationen med Dynamic Media Classic-kodningsprofiler.
1. Välj **[!UICONTROL Upload]** för att överföra primärt källvideoklipp. Videoöverföring och -kodning är klar efter [!UICONTROL DAM Update Asset] arbetsflödet är klart och **[!UICONTROL Publish to Dynamic Media Classic]** har en bock.

   >[!NOTE]
   >
   >Det kan ta en stund innan videominiatyrbilderna genereras.

   När du drar den primära källvideon för DAM till videokomponenten får den åtkomst *alla* Dynamic Media Classic-kodade proxyrenderingar för leverans.

### Foundation Video-komponent jämfört med Dynamic Media Classic Video-komponent {#foundation-video-component-versus-scene-video-component}

När du använder Experience Manager har du tillgång till både videokomponenten som finns på Sites och videokomponenten i Dynamic Media Classic. Dessa komponenter är inte utbytbara.

Dynamic Media Classic videokomponent fungerar bara för Dynamic Media Classic-videofilmer. Grundkomponenten fungerar med videofilmer som lagras från Experience Manager (med ffmpeg) och Dynamic Media Classic-videofilmer.

I följande matris förklaras när du bör använda vilken komponent:

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>Dynamic Media Classic videokomponent har en universell videoprofil. Du kan dock hämta den HTML5-baserade videospelaren som kan användas av Experience Manager. I Dynamic Media Classic kopierar du inbäddningskoden för den färdiga HTML5-videospelaren och placerar den på Experience Manager-sidan.
>

## Videokomponent för Experience Manager {#aem-video-component}

Även om du bör använda komponenten Dynamic Media Classic Video för att visa Dynamic Media Classic-videofilmer beskrivs hur du använder Dynamic Media Classic-videofilmer med [!UICONTROL Foundation Video Component] i Experience Manager för fullständighetens skull.

### Experience Manager Video and Dynamic Media Classic Video comparison {#aem-video-and-scene-video-comparison}

Följande tabell innehåller en högnivåjämförelse mellan videokomponenten i Experience Manager Foundation och Dynamic Media Classic Video-komponenten som stöds:

|   | Experience Manager Foundation Video | Dynamic Media Classic Video |
|---|---|---|
| Metod | HTML5:a första metoden. Flash används bara för reservlösningar som inte är HTML5. | Flash på de flesta datorer. HTML5 används för mobiler och surfplattor. |
| Leverans | Progressiv | Adaptiv strömning |
| Spårning | Ja | Ja |
| Utbyggbarhet | Ja | Nej |
| Mobilvideo | Ja | Ja |

### Konfigurera {#setting-up}

#### Skapa videoprofiler {#creating-video-profiles}

De olika videokodningarna skapas enligt de kodningsförinställningar för Dynamic Media Classic som valts i Dynamic Media Classic Cloud-konfigurationen. För att den grundläggande videokomponenten ska kunna använda dem måste du skapa en videoprofil för varje vald kodningsförinställning för Dynamic Media Classic. Det gör att videokomponenten kan välja DAM-återgivningar utifrån detta.

>[!NOTE]
>
>Nya videoprofiler och ändringar av dem måste aktiveras för publicering.

1. I Experience Manager, gå till **[!UICONTROL Tools]** väljer **[!UICONTROL Configuration Console]**.
1. Gå till Konfiguration **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Video Profiles]** i navigeringsträdet.
1. Skapa en Dynamic Media Classic Video-profil. I **[!UICONTROL New]** meny, välja **[!UICONTROL Create Page]**.
1. Markera Dynamic Media Classic videoprofilmall. Ge den nya videoprofilsidan ett namn och välj **[!UICONTROL Create]**.

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. Redigera den nya videoprofilen. Välj molnkonfigurationen först. Välj sedan samma kodningsförinställning som du valde i molnkonfigurationen.

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | Egenskap | Beskrivning |
   |---|---|
   | Dynamic Media Classic Cloud-konfiguration | Den molnkonfiguration som ska användas för kodningsförinställningarna. |
   | Dynamic Media Classic Encoding Preset | Den kodningsförinställning som den här videoprofilen ska kopplas till. |
   | HTML5-videotyp | Med den här egenskapen kan du ange värdet för type-egenskapen i HTML5-videokällelementet. Den här informationen finns inte i Dynamic Media Classic-kodningsförinställningar, men krävs för att återge videoklippen med videoelementet HTML5 på rätt sätt. En lista över vanliga format tillhandahålls, men kan skrivas över för andra format. |

   Upprepa det här steget för alla kodningsförinställningar som är markerade i molnkonfigurationen och som du vill använda i videokomponenten.

#### Konfigurera design {#configuring-design}

Grundvideokomponenten måste känna till vilka videoprofiler som ska användas för att skapa listan över videokällor. Öppna dialogrutan för design av videokomponenter och konfigurera komponentdesignen för de nya videoprofilerna.

>[!NOTE]
>
>Om du använder grundläggande videokomponent på en mobilsida upprepar du de här stegen i designen av mobilsidan.

>[!NOTE]
>
>Ändringar som görs i designen kräver att designen aktiveras för publicering.

1. Öppna den grundläggande videokomponentens designdialog och ändra till **[!UICONTROL Profiles]** -fliken. Ta sedan bort färdiga profiler och lägg till de nya videoprofilerna för Dynamic Media Classic. Ordningen på profillistan i designdialogrutan definierar också ordningen på videokällelementet vid återgivning.
1. För webbläsare som inte stöder HTML5 kan du konfigurera ett flash-fall med videokomponenten. Öppna dialogrutan för design av videokomponenter och ändra till **[!UICONTROL Flash]** -fliken. Konfigurera Flash Player-inställningarna och tilldela en reservprofil för Flash Player.

#### Checklista {#checklist}

1. Skapa en Dynamic Media Classic-molnkonfiguration. Kontrollera att förinställningarna för videokodning är angivna och att importeraren körs.
1. Skapa en Dynamic Media Classic-videoprofil för varje videokodningsförinställning som valts i molnkonfigurationen.
1. Videoprofilerna måste aktiveras.
1. Konfigurera utformningen av den grundläggande videokomponenten på sidan.
1. Aktivera designen när du är klar med designändringarna.
