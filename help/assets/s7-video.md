---
title: Video
description: Läs om den centraliserade hanteringen av videoresurser i Adobe Experience Manager Assets där du kan överföra videor för automatisk kodning till Dynamic Media Classic och få tillgång till Dynamic Media Classic-videor direkt från Experience Manager Assets. Integrering med Dynamic Media Classic-video ger optimerad video även på alla skärmar.
uuid: 8b3423f1-d96b-44d9-bdb7-e3b77875b25d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
discoiquuid: 2685f9f3-0973-40a9-89b8-e7db0a6a75f2
role: User, Admin
exl-id: 56009925-1a36-48b5-b96c-ec2e468da106
feature: Video
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1513'
ht-degree: 1%

---

# Video {#video}

Adobe Experience Manager Assets har en centraliserad hantering av videor där du kan överföra videor direkt till Assets för automatisk kodning till Dynamic Media Classic och få tillgång till Dynamic Media Classic-videor direkt från Assets för sidredigering.

Integrering med Dynamic Media Classic för video ger optimerad video även på alla skärmar (automatisk enhets- och bandbreddsidentifiering).

* Komponenten **[!UICONTROL Scene7 Video]** utför automatiskt enhets- och bandbreddsidentifiering för att spela upp video i rätt format och med rätt kvalitet på datorer, surfplattor och mobiler.
* Resurser - Du kan inkludera adaptiva videouppsättningar i stället för bara enskilda videoresurser. En adaptiv videouppsättning innehåller alla videoåtergivningar som krävs för att spela upp video sömlöst på flera skärmar. En adaptiv videouppsättning grupperar versioner av samma video som är kodade med olika bithastigheter och format som 400 kbit/s, 800 kbit/s och 1 000 kbit/s. Du använder en adaptiv videouppsättning, tillsammans med S7-videokomponenten, för adaptiv videoströmning på flera skärmar, inklusive stationära datorer, iOS, Android™, BlackBerry® och Windows mobila enheter.
<!-- See [Scene7 documentation about adaptive video sets for more information](https://help.adobe.com/en_US/scene7/using/WS53492AE1-6029-45d8-BF80-F4B5CF33EB08.html). -->

## Om FFMPEG och Dynamic Media Classic {#about-ffmpeg-and-scene}

Standardprocessen för videokodning bygger på den FFMPEG-baserade integrationen med videoprofiler. Därför innehåller det körklara arbetsflödet för DAM-inmatning följande två åtgärder:

* FFMPEG-miniatyrbilder
* FFMPEG-kodning

Om du aktiverar och konfigurerar integreringen med Dynamic Media Classic tas inte dessa två arbetsflödessteg bort automatiskt från det körklara arbetsflödet för DAM-hämtning. Om du redan använder den FFMPEG-baserade videokodningen i Adobe Experience Manager är det troligt att du har FFMPEG installerat i dina redigeringsmiljöer. I det här fallet kodas en ny video som hämtas med DAM två gånger: en gång från FFMPEG-kodaren och en gång från Dynamic Media Classic-integreringen.

Om du har konfigurerat och installerat den FFMPEG-baserade videokodningen i Experience Manager rekommenderar Adobe att du tar bort de två FFMPEG-arbetsflödena från arbetsflödena för DAM-inhämtning.

## Format som stöds {#supported-formats}

Följande format stöds för komponenten Scene7 Video:

* F4V H.264
* MP4 H.264

## Bestäm var videon ska överföras {#deciding-where-to-upload-your-video}

Hur du avgör var du ska överföra dina videoresurser beror på följande:

* Behöver du ett arbetsflöde för videoresursen?
* Behöver du versionskontroll för videoresursen?

Om svaret är ja på någon av eller båda dessa frågor överför du videon direkt till Adobe DAM. Om svaret är nej på båda frågorna överför du videon direkt till Dynamic Media Classic. Arbetsflödet för varje scenario beskrivs i följande avsnitt.

### Om du överför videon direkt till Adobe DAM {#if-you-are-uploading-your-video-directly-to-adobe-dam}

Om du behöver ett arbetsflöde eller en versionshantering för dina resurser ska du först överföra till Adobe DAM. Här följer det rekommenderade arbetsflödet:

1. Ladda upp videomaterialet till Adobe DAM och koda och publicera automatiskt till Dynamic Media Classic.
1. I Experience Manager får du åtkomst till videomaterial i WCM på fliken **[!UICONTROL Movies]** i Content Finder.
1. Skapa med en **[!UICONTROL Scene7 Video]**- eller **[!UICONTROL Foundation Video]**-komponent.

### Om du överför videon till Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

Om du inte behöver ett arbetsflöde eller en versionshantering för dina resurser överför du dina resurser till Scene7. Här följer det rekommenderade arbetsflödet:

1. I Dynamic Media Classic [konfigurerar du en schemalagd FTP-överföring och -kodning till Scene7 (automatiskt system)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#upload-files-using-via-ftp).
1. I Experience Manager får du åtkomst till videomaterial i WCM på fliken **[!UICONTROL Scene7]** i Content Finder.
1. Skapa med komponenten **[!UICONTROL Scene7 Video]**.

## Konfigurera integrering med Scene7 Video {#configuring-integration-with-scene-video}

Så här konfigurerar du universella förinställningar:

1. I **[!UICONTROL Cloud Services]** navigerar du till din **[!UICONTROL Scene7]**-konfiguration och klickar på **[!UICONTROL Edit]**.
1. Välj fliken **[!UICONTROL Video]**.

   ![chlimage_1-363](assets/chlimage_1-363.png)

   >[!NOTE]
   >
   >Fliken **[!UICONTROL Video]** visas inte om sidan inte har någon molnkonfiguration.

1. Välj den adaptiva videokodningsprofilen, en färdig videokodningsprofil eller en anpassad videokodningsprofil.

   >[!NOTE]
   >
   >Mer information om vad videoförinställningarna betyder finns i [Dynamic Media Classic-dokumentationen](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files).
   >
   >Adobe rekommenderar att du antingen markerar båda adaptiva videouppsättningar när du konfigurerar de universella förinställningarna eller väljer alternativet **[!UICONTROL Adaptive Video Encoding]**.

1. De valda kodningsprofilerna tillämpas automatiskt på alla videoklipp som överförs till CQ DAM-målmappen som du konfigurerar för den här Scene7-molnkonfigurationen. Du kan konfigurera flera Scene7 molnkonfigurationer med olika målmappar för att tillämpa olika kodningsprofiler efter behov.

## Uppdatera visningsprogram och kodningsförinställningar {#updating-viewer-and-encoding-presets}

Om du vill uppdatera visnings- och kodningsförinställningarna för video eftersom förinställningarna har uppdaterats i Scene7 går du till Scene7-konfigurationen i molnkonfigurationen och trycker på **[!UICONTROL Update the viewer and encoding presets]**.

![chlimage_1-364](assets/chlimage_1-364.png)

## Överför din primära källvideo till Scene7 från Adobe DAM {#uploading-your-master-video}

1. Navigera till målmappen för CQ DAM där du har konfigurerat molnkonfigurationen med Scene7-kodningsprofiler.
1. Klicka på **[!UICONTROL Upload]** för att överföra primärt källvideoklipp. Överföringen och kodningen av videon är klar när arbetsflödet [!UICONTROL DAM Update Asset] är klart och **[!UICONTROL Publish to Scene7]** är markerat.

   >[!NOTE]
   >
   >Det tar tid innan videominiatyrbilderna genereras.

   Genom att dra den primära källvideon för DAM till videokomponenten kommer du åt *alla* Scene7-kodade proxyåtergivningar för leverans.

## Foundation Video Component jämfört med Scene7 Video Component {#foundation-video-component-versus-scene-video-component}

När du använder Experience Manager har du tillgång till både videokomponenten som finns på Sites och videokomponenten i Scene7. Dessa komponenter är inte utbytbara.

Scene7 videokomponent fungerar bara för Scene7-videofilmer. Grundkomponenten fungerar med videofilmer som lagras från Experience Manager (med ffmpeg) och Scene7-videofilmer.

I följande matris förklaras när du ska använda vilken komponent:

![chlimage_1-365](assets/chlimage_1-365.png)

>[!NOTE]
>
>Som standard använder S7-videokomponenten den universella videoprofilen. Du kan dock hämta den HTML5-baserade videospelaren som ska användas av Experience Manager. I Scene7 kopierar du inbäddningskoden för den färdiga HTML5-videospelaren och placerar den på Experience Manager-sidan.

## Videokomponent för Experience Manager {#aem-video-component}

Även om du bör använda videokomponenten för Scene7 för att visa Scene7-videofilmer beskrivs det här avsnittet hur du använder Scene7-videofiler med Foundation Video Component i Experience Manager för att få en fullständig beskrivning.

### Experience Manager Video and Scene7 Video comparison {#aem-video-and-scene-video-comparison}

Följande tabell innehåller en högnivåjämförelse mellan videokomponenten i Experience Manager Foundation och Scene7 Video-komponenten som stöds:

|  | Experience Manager Foundation Video | Scene7 Video |
|---|---|---|
| Metod | HTML5 first approach. Flash används endast för icke-HTML5-reservlösningar. | Flash på de flesta stationära datorer. HTML5 används för mobiler och surfplattor. |
| Leverans | Progressiv | Adaptiv strömning |
| Spårning | Ja | Ja |
| Utbyggbarhet | Ja | Nej |
| Mobilvideo | Ja | Ja |

### Konfigurera {#setting-up}

#### Skapa videoprofiler {#creating-video-profiles}

De olika videokodningarna skapas enligt de kodningsförinställningar för S7 som valts i molnkonfigurationen för S7. För att den grundläggande videokomponenten ska kunna använda dem måste en videoprofil skapas för varje vald S7-kodningsförinställning. Med den här metoden kan videokomponenten välja DAM-återgivningar utifrån detta.

>[!NOTE]
>
>Nya videoprofiler och ändringar av dem måste aktiveras för publicering.

1. I Experience Manager trycker du på **[!UICONTROL Tools]** > **[!UICONTROL Configuration Console]**.
1. I **[!UICONTROL Configuration Console]** navigerar du till **[!UICONTROL Tools]** > **[!UICONTROL DAM]** > **[!UICONTROL Video Profiles]** i navigeringsträdet.
1. Skapa en S7-videoprofil. I **[!UICONTROL New]**. väljer du **[!UICONTROL Create Page]** och sedan Scene7 videoprofilmall. Ge den nya videoprofilsidan ett namn och klicka på **[!UICONTROL Create]**.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. Redigera den nya videoprofilen. Välj molnkonfigurationen först. Välj sedan samma kodningsförinställning som du valde i molnkonfigurationen.

   ![chlimage_1-367](assets/chlimage_1-367.png)

   | Egenskap | Beskrivning |
   |---|---|
   | Scene7 Cloud-konfiguration | Den molnkonfiguration som ska användas för kodningsförinställningarna. |
   | Scene7 Encoding Preset | Den kodningsförinställning som den här videoprofilen ska kopplas till. |
   | HTML5-videotyp | Med den här egenskapen kan du ange värdet för type-egenskapen i HTML5-videokällelementet. Den här informationen finns inte i S7-kodningsförinställningarna, men krävs för att videorna ska kunna återges korrekt med HTML5-videoelementet. En lista över vanliga format tillhandahålls, men kan skrivas över för andra format. |

   Upprepa det här steget för alla kodningsförinställningar som är markerade i molnkonfigurationen och som du vill använda i videokomponenten.

#### Konfigurera design {#configuring-design}

Komponenten **[!UICONTROL Foundation Video]** måste känna till vilka videoprofiler som ska användas för att skapa listan över videokällor. Öppna dialogrutan för videokomponentdesign och konfigurera komponentdesignen för användning av de nya videoprofilerna.

>[!NOTE]
>
>Om du använder komponenten **[!UICONTROL Foundation Video]** på en mobilsida upprepar du de här stegen i designen av mobilsidan.

>[!NOTE]
>
>Ändringar i designen kräver att designen aktiveras för att börja gälla vid publiceringen.

1. Öppna **[!UICONTROL Foundation Video]**-komponentens designdialogruta och ändra till fliken **[!UICONTROL Profiles]**. Ta sedan bort färdiga profiler och lägg till de nya videoprofilerna för S7. Ordningen på profillistan i designdialogrutan definierar ordningen på videokällelementet vid återgivning.
1. För webbläsare som inte stöder HTML5 kan du konfigurera ett Flash-reserv med videokomponenten. Öppna dialogrutan för design av videokomponenter och ändra till fliken **[!UICONTROL Flash]**. Konfigurera inställningarna för Flash-spelaren och tilldela en reservprofil för Flash Player.

#### Checklista {#checklist}

1. Skapa en S7-molnkonfiguration. Kontrollera att förinställningarna för videokodning är angivna och att importeraren körs.
1. Skapa en S7-videoprofil för varje videokodningsförinställning som har valts i molnkonfigurationen.
1. Videoprofilerna måste aktiveras.
1. Konfigurera designen för **[!UICONTROL Foundation Video]**-komponenten på sidan.
1. Aktivera designen när du är klar med designändringarna.
