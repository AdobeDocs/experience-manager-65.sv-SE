---
title: Länka URL:er till ditt webbprogram
description: Länka URL:er till ditt webbprogram i Dynamic Media
uuid: cf599e66-b1f9-40c0-b572-cea19f2e6793
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: d12e6ea3-aaf4-4672-9679-3c16c76d7d5b
role: User, Admin
exl-id: d62275f0-02a4-48c9-bfb1-e23d63b618c9
feature: Configuration
source-git-commit: 78aa7aac838dabc1c4f0329520092e4755541322
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 4%

---

# Länka URL:er till ditt webbprogram {#linking-urls-to-your-web-application}

Dina webbplatser och tillämpningar har åtkomst till Dynamic Media tjänster via URL-samtal. När du har publicerat en resurs aktiverar Dynamic Media en URL-sträng som refererar till resursen. Du kan klistra in dessa URL:er i en webbläsare för testning.

Du länkar bara till URL-adresser om du är *not* med Experience Manager som WCM. Länkning - och inte inbäddning - används när du vill leverera en videospelare som ett popup-fönster eller modalt fönster. Om du använder Experience Manager som WCM, [du lägger till resurserna direkt på sidan](adding-dynamic-media-assets-to-pages.md).

Om du vill placera dessa URL-strängar på dina webbsidor och i dina program kopierar du dem från Dynamic Media.

>[!NOTE]
>
>URL-strängar är bara tillgängliga för dynamiska återgivningar av resurser. De är för närvarande inte tillgängliga för statiska resurser som finns i DAM och inte på Dynamic Media-servern. URL-knappen visas inte för återgivningar som är statiska.

Se även [Bädda in video- eller bildvisningsprogrammet på en webbsida](embed-code.md).

Se även [Länka YouTube URL:er till ditt webbprogram](video.md).

Se även [Leverera optimerade bilder för en responsiv webbplats](responsive-site.md).

Se även [Överför resurser](manage-assets.md#uploading-assets).

## Hämta en URL för en resurs {#obtaining-a-url-for-an-asset}

Du kan hämta en URL-sträng som genereras av en bildförinställning eller en visningsförinställning. När du har kopierat URL:en markeras den i Urklipp så att du kan klistra in den på sidorna på webbplatsen eller i programmet.

>[!NOTE]
>
>URL:en är inte tillgänglig för kopiering förrän du har publicerat den valda resursen. Dessutom måste du även publicera visningsförinställningen eller bildförinställningen.
>
>Se [Publicera resurser](publishing-dynamicmedia-assets.md).
>
>Se [Publicera förinställningar för visningsprogram](managing-viewer-presets.md#publishing-viewer-presets).
>
>Se [Publicera bildförinställningar](managing-image-presets.md#publishing-image-presets).

Du kan hämta en URL-sträng på flera olika sätt. Stegen nedan visar dock bara en metod som du kan använda.

**Så här hämtar du en URL för en resurs:**

1. Navigera till *publicerad* resurs vars förinställda URL eller URL för visningsförinställning som du vill kopiera, och markera resursen för att öppna den.

   Kom ihåg att URL:er endast går att kopiera *efter* att du har *publicerat* resurserna. Dessutom måste visningsförinställningen eller bildförinställningen också publiceras.

   Se [Publicera resurser](publishing-dynamicmedia-assets.md).

   Se [Publicera förinställningar för visningsprogram](managing-viewer-presets.md#publishing-viewer-presets).

   Se [Publicera bildförinställningar](managing-image-presets.md#publishing-image-presets).

1. Gör något av följande beroende på vilken resurs du valt:

   * Om du har markerat en bild väljer du **[!UICONTROL Renditions]**.

      Under **[!UICONTROL Dynamic]** väljer du ett förinställningsnamn för att visa återgivningen i den högra bildrutan. Om det behövs bläddrar du i listan Återgivningar för att se den dynamiska rubriken.

      Längst ned i den vänstra listen väljer du **[!UICONTROL URL]**.

      ![chlimage_1-270](assets/chlimage_1-270.png)

   * Om du valde en snurra, en bilduppsättning, en Carousel-uppsättning eller en video väljer du **[!UICONTROL Viewers]**.

      Välj ett namn på visningsförinställningen i den vänstra listen. En förhandsgranskning av uppsättningen eller videon öppnas på en separat sida.

      I den vänstra listen längst ned väljer du **[!UICONTROL URL]**.

      ![chlimage_1-271](assets/chlimage_1-271.png)

1. Markera och kopiera texten till webbläsaren så att du kan förhandsgranska resursen eller lägga till den på webbinnehållssidan.

   Om du vill avsluta URL-fönstret väljer du **[!UICONTROL X]** eller markera **[!UICONTROL Close]**.

## Hämta en URL för en statisk resurs {#obtaining-a-url-for-a-static-asset}

Dynamic Media stöder leverans av statiskt material, som är ytterligare material utöver bara bilder och video. Statiska medieformat som stöds för leverans är bland annat följande:

* 3D-filer
* Animerad GIF
* Ljudfiler
* CSS
* JavaScript (när ditt företag är konfigurerat med sin egen domän)
* PDF
* SVG
* XML
* ZIP

**Så här hämtar du en URL för en statisk resurs:**

1. Navigera till *publicerad* statisk resurs vars URL du vill kopiera och markera resursen för att öppna den.

   Kom ihåg att URL-adresser endast är tillgängliga för kopiering *efter* du har först *publicerad* den statiska resursen.

   Se [Publicera resurser](publishing-dynamicmedia-assets.md).

1. Använd någon av följande metoder för att hämta URL:en för den publicerade statiska resursen:

   * `The URL of the published static is the following:`

      * `https://*<server_name>*/is/content/*<company_name>*/*<static_asset_filename>*.*<extension>*`

         Till exempel, `https://aem.com/is/content/adobe/image.gif`.
   * Välj **[!UICONTROL Asset]** > **[!UICONTROL Dynamic Renditions]** väljer du sedan en dynamisk återgivning av den statiska resursen och kopierar URL:en.

      Ändra den kopierade URL-adressen som ska användas `is/content` i banan i stället för `is/image/`.


## Hämta en video-URL för en publicerad videoåtergivning {#obtaining-a-video-url-for-a-published-video-rendition}

1. I Experience Manager går du till **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Cloud]** > **[!UICONTROL Cloud Services]**.
1. På **[!UICONTROL Cloud Services]** sida, bläddra nedåt till **[!UICONTROL Dynamic Media Cloud Services]** rubrik, markera **[!UICONTROL Show Configurations]**.
1. Under **[!UICONTROL Available Configurations]** markerar du namnet på konfigurationen som du vill använda.

1. På **[!UICONTROL Dynamic Media Cloud Settings]** sida, under **[!UICONTROL Video Service URL]**, kopierar hela URL-sökvägen. Du måste gå till den kopierade URL-sökvägen senare i stegen.

   URL-sökvägen kan till exempel se ut ungefär så här:

   `https://s7athens.macromedia.com:9090/DMGateway/`

   (Sökvägen ovan är endast ett exempel; det är inte den faktiska sökvägen som du kopierar.)

1. Under **[!UICONTROL Registration ID]** kopierar du det kundnamn som finns i den sista delen av ID:t.

   Om registrerings-ID till exempel var `87654321|MyCompany`, blir kundens namn `MyCompany`.

1. I närheten av sidans övre vänstra hörn väljer du **[!UICONTROL Cloud Services]** väljer du Experience Manager logotyp och navigerar till **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. Kopiera ned hela videouppdateringssökvägen från JCR (Java™ Content Repository).

   Videons återgivningssökväg kan till exempel se ut ungefär så här:

   `/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112f/avs/Momentum_1080-0x720-2600k.mp4`

   (Sökvägen ovan är endast ett exempel; det är inte den faktiska sökvägen som du kopierar.)

1. Ordna den kopierade informationen i följande ordning så att den utgör en fullständig URL-sökväg:

   `<Video_Service_URL>/public/<Customer_name_from_Registration_ID>/<Video_rendition_path>`

   Om du till exempel använder exempelsökvägarna och exempelkundnamnet från stegen ovan, visas den fullständiga sökvägen enligt följande:

   `https://s7athens.macromedia.com:9090/DMGateway/public/MyCompany/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112ff/avs/Momentum_1080-0x720-2600k.mp4`

   Det här exemplet är den fullständiga video-URL:en för en publicerad videoåtergivning.

## Hämta en video-URL för strömning med adaptiv bithastighet (DASH eller HLS) {#obtaining-a-video-url-for-adaptive-streaming-hls}

1. I Experience Manager går du till **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Cloud]** > **[!UICONTROL Cloud Services]**.
1. På **[!UICONTROL Cloud Services]** sida, bläddra nedåt till **[!UICONTROL Dynamic Media Cloud Services]** rubrik, markera **[!UICONTROL Show Configurations]**.
1. Under **[!UICONTROL Available Configurations]** markerar du namnet på konfigurationen som du vill använda.
1. På **[!UICONTROL Dynamic Media Cloud Services Settings]** gör du följande på sidan:

   * Under **[!UICONTROL Video Service URL]**, kopierar hela URL-sökvägen. Du behöver den kopierade URL-sökvägen senare i dessa steg. URL-sökvägen kan till exempel se ut ungefär så här:

   `https://gateway-na.assetsadobe.com/DMGateway/`

   (Sökvägen ovan är endast ett exempel; det är inte den faktiska sökvägen som du kopierar.)

   * Under **[!UICONTROL Registration ID]** kopierar du det kundnamn som finns i den sista delen av ID:t. Du behöver det kopierade kundnamnet senare i dessa steg.

      Om registrerings-ID till exempel var `87654321|demoCo`, det kundnamn du kopierar är `demoCo`.


1. Kopiera respektive protokollväljare baserat på vilket videoleveransprotokoll du använder. Du behöver den kopierade protokollväljaren senare i dessa steg.

   | Videoleveransprotokoll som du använder | Protokollväljare som ska användas |
   |---|---|
   | HTTP <br> Om du använder HTTP (osäker videoleverans) måste du ändra https till http i URL-värdet för videotjänsten som du kopierade tidigare. | `public/` |
   | HTTPS | `public-ssl/` |

1. Kopiera den fullständiga sökvägen för videoresurser i Experience Manager, enligt Dynamic Media bearbetning. Du behöver den här kopierade videoresurssökvägen senare i dessa steg.

   Till exempel:

   `/content/dam/marketing/MyVideo.mp4`

1. Kombinera alla delar du kopierat tidigare och skapa en sträng i följande ordning:

   &lt; `video service URL`>&lt; `protocol selector`>&lt; `customer name`>&lt; `video asset path`>

   Om du till exempel använder den kopierade informationen från exemplen i de här stegen ser strängen ut så här:

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4`

1. Fyll i URL:en genom att lägga till `.m3u8` till strängens slut. Lägg till exempel `.m3u8` till strängen från det föregående steget visas den fullständiga URL-sökvägen enligt följande:

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4.m3u8`

## Använd HTTP/2 för att leverera dina Dynamic Media-resurser {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 är det nya, uppdaterade webbprotokollet som förbättrar kommunikationen mellan webbläsare och servrar. Det ger snabbare överföring av information och minskar mängden processorkraft som behövs. Dynamic Media-material kan nu levereras via HTTP/2 vilket ger bättre respons och laddningstider.

Se [HTTP2-leverans av innehåll](http2.md) om du vill ha fullständig information om hur du kommer igång med HTTP/2 med ditt Dynamic Media-konto.
