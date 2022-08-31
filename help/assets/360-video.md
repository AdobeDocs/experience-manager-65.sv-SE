---
title: 360/VR-video
description: Lär dig hur du arbetar med 360- och VR-video (Virtual Reality) i Dynamic Media.
uuid: c21bf2c0-7acc-401f-857e-0186de86e7a1
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: aac3c850-ae84-4bff-80de-d370e150f675
docset: aem65
feature: 360 VR Video
role: User, Admin
exl-id: 0c2077a7-bd16-484b-980f-4d4a1a681491
source-git-commit: c0a60ec39e35fa8113ce9e1795561709b9c7e289
workflow-type: tm+mt
source-wordcount: '1101'
ht-degree: 0%

---

# 360/VR-video {#vr-video}

360-gradersvyer spelar in en vy i alla riktningar samtidigt. De filmas med en omdirigerad kamera eller en samling kameror. Vid uppspelning på en platt skärm har användaren kontroll över betraktningsvinkeln. uppspelningar på mobila enheter använder vanligtvis de inbyggda gyroskopiska kontrollerna.

Dynamic Media - Scene7-läget har inbyggt stöd för leverans av 360 videomaterial. Som standard krävs ingen ytterligare konfiguration för visning eller uppspelning. Du levererar 360-video med standardvideotillägg som .mp4, .mkv och .mov. Den vanligaste kodeken är H.264.

I det här avsnittet beskrivs hur du arbetar med 360/VR Video Viewer för att återge ekvirektangulär video för en engagerande tittarupplevelse av ett rum, en egenskap, plats, landskap, medicinska procedurer och så vidare.

Spatial audio stöds för närvarande inte. om ljudet blandas i stereo ändras inte balansen (L/R) när kunden ändrar kamerans visningsvinkel.

Se även [Hantera visningsförinställningar](/help/assets/managing-viewer-presets.md).

## 360 Video in action {#video-in-action}

Välj [Space Station 360](https://s7d1.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS) för att öppna ett webbläsarfönster och titta på en 360-gradersvideo. Under videouppspelningen drar du muspekaren till en ny plats för att ändra visningsvinkeln.

![360-videoexempel med en internationell rymdstation som flyter i yttre rymden och jorden och solen bakom den.](assets/6_5_360videoiss_simplified.png)
*Videobildruta från Space Station 360*

## 360/VR Video och Adobe Premiere Pro {#vr-video-and-adobe-premiere-pro}

Du kan använda Adobe Premier Pro för att visa och redigera 360/VR-filmer. Du kan till exempel placera logotyper och text på rätt sätt i en scen och använda effekter och övergångar som är särskilt utformade för ekvirektangulära medier.

Se [Redigera 360/VR-video](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html).

## Ladda upp material som ska användas med 360-videovisningsprogrammet {#uploading-assets-for-use-with-the-video-viewer}

360 videomaterial som överförs till Adobe Experience Manager namnges som **Multimedia** på en Assets-sida, ungefär som i en vanlig videoresurs.

![6_5_360video-select-opreview](assets/6_5_360video-selecttopreview.png)
*En överförd 360-videoresurs som visas i kortvyn. Resursen är märkt som Multimedia.*

**Ladda upp material som ska användas med 360-videovisningsprogrammet:**

1. Skapade en mapp som är dedikerad till ditt 360-videomaterial.
1. [Använd en adaptiv videoprofil på mappen](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).

   Om du återger 360-videoinnehåll ställs högre krav på källvideoupplösning och för kodad återgivningsupplösning än standardvideoinnehåll som inte är 360.

   Du kan använda den färdiga adaptiva videoprofilen som redan finns i Dynamic Media. Det ger dock betydligt lägre 360-videokvalitet än vad du skulle få för icke-360-video som är kodad med samma inställningar som återges med ett icke-360-videovisningsprogram. Om 360-video med hög kvalitet krävs gör du därför följande:

   * Det bästa är att ditt ursprungliga 360-videomaterial har någon av följande upplösningar:

      * 1080p - 1920 x 1080, känd som Full HD eller FHD upplösning eller
      * 2160p - 3840 x 2160, känd som 4k, UHD eller Ultra HD-upplösning. Den här stora skärmupplösningen finns oftast på tv-apparater och datorskärmar. Upplösningen 2160p kallas ofta för&quot;4k&quot; eftersom bredden är nästan 4 000 pixlar. Med andra ord har den fyra gånger så många pixlar som 1080p.
   * [Skapa en anpassad adaptiv videoprofil](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) med renderingar av högre kvalitet. Skapa till exempel en adaptiv videoprofil som innehåller följande tre inställningar:

      * width=auto; height=720; bithastighet=2 500 kbit/s
      * width=auto; height=1080; bithastighet=5000 kbit/s
      * width=auto; height=1440; bithastighet=6600 kbit/s
   * Bearbeta 360-videomaterial i en mapp som är exklusivt dedikerad till 360-videomaterial.

   Detta tillvägagångssätt ställer större krav på slutanvändarens nätverk och processor.

1. [Överför videon till mappen](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).

## Åsidosätt standardproportionerna för 360-videofilmer  {#overriding-the-default-aspect-ratio-of-videos}

För att en överförd resurs ska kvalificera sig som en 360-video som du tänker använda med 360-videovisningsprogrammet måste resursen ha proportionerna 2.

Som standard identifierar Experience Manager video som&quot;360&quot; om proportionerna (bredd/höjd) är 2.0. Om du är administratör kan du åsidosätta standardinställningen för proportioner på 2 genom att ange den valfria inställningen `s7video360AR` i CRXDE Lite vid följande:

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

   * **Egenskapstyp** - Dubbel
   * **Värde** - flyttalsproportioner, standard 2.0.

När du har angett den här egenskapen börjar den gälla omedelbart för både befintliga videoklipp och nyligen överförda videoklipp.

Proportionerna gäller för 360 videoresurser för sidan med resursinformation och [Video 360 Media WCM-komponent](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components).

Börja med att ladda upp 360 videor.

## Förhandsgranska 360-video {#previewing-video}

Du kan använda Förhandsgranska för att se hur 360-videon ser ut för kunderna och kontrollera att den beter sig som förväntat.

Se även [Redigera förinställningar för visningsprogram](/help/assets/managing-viewer-presets.md#editing-viewer-presets).

När du är nöjd med 360-videon kan du publicera den.

Se [Bädda in video- eller bildvisningsprogrammet på en webbsida](/help/assets/embed-code.md).
Se [Länka URL:er till ditt webbprogram](/help/assets/linking-urls-to-yourwebapplication.md). Den URL-baserade länkningsmetoden är inte möjlig om det interaktiva innehållet har länkar till relativa URL-adresser, särskilt länkar till Experience Manager Sites-sidor.
Se [Lägga till Dynamic Media Assets på sidor](/help/assets/adding-dynamic-media-assets-to-pages.md).

**Så här förhandsgranskar du 360-video:**

1. I **[!UICONTROL Assets]** navigera till en befintlig 360-video som du har skapat. Välj 360-videomaterialet så att du kan öppna det i förhandsgranskningsläge.

   ![6_5_360video-selecttopreview-1](assets/6_5_360video-selecttopreview-1.png)

   Välj en 360-videoresurs så att du kan förhandsgranska videon.

1. Markera listrutan på förhandsvisningssidan, i det övre vänstra hörnet på sidan, och välj sedan **[!UICONTROL Viewers]**.

   ![6_5_360video-preview-viewers](assets/6_5_360video-preview-viewers.png)

   I visningslistan väljer du **[!UICONTROL Video360_social]** gör du något av följande:

   * Dra muspekaren över videon om du vill ändra visningsvinkeln för den statiska scenen.
   * Välj videons **[!UICONTROL Play]** om du vill påbörja uppspelningen. När videon spelas upp drar du muspekaren över videon för att ändra visningsvinkeln.

   ![En skärmbild av den internationella rymdstationen som flyter i yttre rymden med jorden och solen i bakgrunden ](assets/6_5_360video-preview-video360-social.png)*En 360-videobildbild.*

   * I visningslistan väljer du **[!UICONTROL Video360VR]**.

      VR-video (Virtual Reality) är engagerande videomaterial som nås via virtuella verklighetshuvuden. Precis som med vanliga videor skapar du VR-videor i början när en video spelas in eller spelas in med 360-graderskameror.
   ![En skärmbild av en närbild av den internationella rymdstationen som flyter i yttre rymden med jorden och solen delvis synlig i bakgrunden](assets/6_5_360video-preview-video360vr.png)
   *En 360 VR-videobildskärm.*

1. Välj i det övre högra hörnet på förhandsvisningssidan **[!UICONTROL Close]**.

## Publicera 360-video {#publishing-video}

Publicera 360-videon så att du kan använda den. När du publicerar en 360-video aktiveras URL:en och Bädda in kod. Dessutom publiceras 360-videon i Dynamic Media-molnet, som är integrerat med ett CDN för skalbar leverans och leverans med höga prestanda.

Se [Publicera Dynamic Media-resurser](/help/assets/publishing-dynamicmedia-assets.md) om du vill ha information om hur du publicerar 360-video.
Se även [Bädda in video- eller bildvisningsprogrammet på en webbsida](/help/assets/embed-code.md).
Se även [Länka URL:er till ditt webbprogram](/help/assets/linking-urls-to-yourwebapplication.md). Den URL-baserade länkningsmetoden är inte möjlig om det interaktiva innehållet har länkar till relativa URL-adresser, särskilt länkar till Experience Manager Sites-sidor.
Se även [Lägga till Dynamic Media-resurser på sidor](/help/assets/adding-dynamic-media-assets-to-pages.md).
