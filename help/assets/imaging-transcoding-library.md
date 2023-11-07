---
title: Konverteringsbibliotek för bildbehandling
description: Lär dig hur du konfigurerar och använder Adobe Imaging Transcoding Library, en bildbehandlingslösning som kan utföra grundläggande bildhanteringsfunktioner, inklusive kodning, omkodning, bildomsampling och storleksändring.
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools,Asset Processing
exl-id: b67465f9-177c-49c4-b4eb-a1d6e09ac9a2
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 0%

---

# Konverteringsbibliotek för bildbehandling {#imaging-transcoding-library}

Adobe Imaging Transcoding Library är en tillverkarspecifik bildbehandlingslösning som kan utföra grundläggande bildhanteringsfunktioner, som:

* Kodning
* Omkodning (konverterar format som stöds)
* Bildomsampling, använda PS- och Intel IPP-algoritmer
* Bevara bitdjup och färgprofil
* JPEG-komprimering
* Storleksändring av bild

Bildkonverteringsbiblioteket har stöd för CMYK och fullt stöd för alfa, utom CMYK -Alpha.

Förutom stöd för ett stort antal filformat och profiler har Imaging Transcoding Library betydande fördelar jämfört med andra tredjepartslösningar när det gäller prestanda, skalbarhet och kvalitet. Här är några av fördelarna med att använda Imaging Transcoding Library:

* **Skalförändra med ökad filstorlek eller upplösning**: Skalning uppnås huvudsakligen genom den patenterade möjligheten i Imaging Transcoding Library att ändra storlek samtidigt som filer avkodas. Detta gör att minnesanvändningen vid körning alltid är optimal och inte är en kvadratisk funktion som ökar filstorleken eller upplösningsmegapixlar. Konverteringsbiblioteket för bildbehandling kan bearbeta större och högupplösta filer (som innehåller högre megapixlar). Tredjepartsverktyg som ImageMagick kan inte hantera stora filer och krascher när sådana filer bearbetas.
* **Komprimerings- och storleksändringsalgoritmer för Photoshop**: Överensstämmelse med branschstandard när det gäller kvalitet på nedsampling (jämn, skarp och automatisk bikubisk) och komprimeringskvalitet. Imaging Transcoding Library utvärderar dessutom kvalitetsfaktorn för indatabilden och använder intelligent optimala tabeller och kvalitetsinställningar för utdatabilden. Detta ger filer av optimal storlek utan att den visuella kvaliteten äventyras.
* **Hög genomströmning:** Svarstiden är kortare och genomströmningen är genomgående högre än ImageMagick. Därför bör Imaging Transcoding Library minska väntetiden för användare och kostnaden för värdtjänster.
* **Skala bättre med samtidig inläsning:** Omkodningsbiblioteket för bilder fungerar optimalt under samtidiga inläsningsförhållanden. Den ger hög genomströmning med optimala processorprestanda, minnesanvändning och låg svarstid, vilket minskar kostnaderna för värdtjänster.

## Plattformar som stöds {#supported-platforms}

Imaging Transcoding Library är bara tillgängligt för distributioner av RHEL 7 och CentOS 7.

>[!NOTE]
>
>Mac OS och andra *nix-distributioner (till exempel Debian och Ubuntu) stöds inte.

## Användning {#usage}

Kommandoradsargumenten för Imaging Transcoding Library kan innehålla följande:

```shell
 -destMime PNG/JPEG: Mime type of output rendition
 -BitDepth 8/16: Preserves Bit Depth. Bitdepth '4' is automatically converted to '8'
 -preserveBitDepth: Downscales Bit Depth (No upscaling)
 -preserveCMYK: Preserves CMYK color space
 -jpegQuality: Provides jpeg quality parameter (0-12 , corresponding to Photoshop qualities)
 -ResamplingMethod BiCubic/Lanczos/PSBicubic: Provides resampling methods. PSBicubic is a Photoshop quality resampling method.
 -resize
```

Du kan konfigurera följande alternativ för `-resize` parameter:

* `X`: Fungerar ungefär som [!DNL Experience Manager]. Till exempel -resize 319.
* `WxH`: Proportionerna behålls inte, till exempel `-resize 319x319`.
* `Wx`: Fastställer bredden och beräknar höjden med bibehållna proportioner. Till exempel, `-resize 319x`.
* `xH`: Korrigerar höjden och beräknar bredden med bibehållna proportioner. Till exempel, `-resize x319`.

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## Konfigurera bildkonverteringsbibliotek {#configuring-imaging-transcoding-library}

Om du vill konfigurera ITL-bearbetning skapar du en konfigurationsfil och uppdaterar arbetsflödet för att köra det.

### Skapa konfigurationsfil för extraherat paket {#create-conf-file}

Om du vill konfigurera biblioteket skapar du en CONF-fil som anger biblioteken med följande steg. Du behöver administratörs- eller rotbehörigheter.

1. Ladda ned [Paket för avkodningsbibliotek från programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) och installera det med pakethanteraren. Paketet är kompatibelt med [!DNL Experience Manager] 6.5.

1. Att känna till ett paket-ID för `com.day.cq.dam.cq-dam-switchengine`loggar du in på webbkonsolen och klickar på **[!UICONTROL OSGi]** > **[!UICONTROL Bundles]**. Du kan även öppna paketkonsolen genom att gå till `https://[aem_server:[port]/system/console/bundles/` URL. Sök `com.day.cq.dam.cq-dam-switchengine` och dess ID.

1. Kontrollera att alla nödvändiga bibliotek har extraherats genom att kontrollera mappen med kommandot `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`, där mappnamnet skapas med paket-ID:t. Kommandot är till exempel `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` om paket-ID är `588`.

1. Skapa `SWitchEngineLibs.conf` fil som ska länkas till biblioteket.

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. Lägg till `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` sökväg till conf-filen med `cat SWitchEngineLibs.conf` -kommando.

1. Kör `ldconfig` för att skapa nödvändiga länkar och cacheminne.

1. I kontot som används för att starta [!DNL Experience Manager], redigera `.bash_profile` -fil. Lägg till `LD_LIBRARY_PATH` genom att lägga till följande:

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. För att säkerställa att värdet för banan är inställt på `.`, använda `echo $LD_LIBRARY_PATH` -kommando. Utdata ska bara `.`. Om värdet inte är inställt på `.`startar du om sessionen.

### Konfigurera [!UICONTROL DAM Update Asset] arbetsflöde {#configure-dam-asset-update-workflow}

Uppdatera [!UICONTROL DAM Update Asset] arbetsflöde för att använda biblioteket för bearbetning av bilder.

1. I [!DNL Experience Manager] användargränssnitt, välja **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.

1. Från **[!UICONTROL Workflow Models]** sida, öppna **[!UICONTROL DAM Update Asset]** arbetsflödesmodell i redigeringsläge.

1. Öppna **[!UICONTROL Process Thumbnails]** steg i arbetsflödesprocessen. I **[!UICONTROL Thumbnails]** lägger du till de MIME-typer som du vill hoppa över standardprocessen för generering av miniatyrbilder för i **[!UICONTROL Skip Mime Types]** lista.
Om du till exempel vill skapa miniatyrbilder för en TIFF-bild med hjälp av Imaging Transcoding Library, anger du `image/tiff` i **[!UICONTROL Skip Mime Types]** fält.

1. I **[!UICONTROL Web Enabled Image]** lägger du till de MIME-typer för vilka du vill hoppa över standardprocessen för generering av webbåtergivning i **[!UICONTROL Skip List]**. Om du till exempel hoppade över MIME-typen `image/tiff` i steget ovan lägger du till `image/tiff` till överhoppningslistan.

1. Öppna **[!UICONTROL EPS thumbnails (powered by ImageMagick)]** går du till **[!UICONTROL Arguments]** -fliken. I **[!UICONTROL Mime Types]** lägger du till de MIME-typer som du vill att Imaging Transcoding Library ska bearbeta. Om du t.ex. hoppade över MIME-typen `image/tiff` i steget ovan lägger du till `image/jpeg` till **[!UICONTROL Mime Types]** lista.

1. Ta bort eventuella standardkommandon.

1. Växla sidopanel och lägg till i listan med steg **[!UICONTROL SWitchEngine Handler]**.

1. Lägg till kommandon i [!UICONTROL SwitchEngine Handler] baserat på era egna krav. Finjustera parametrarna för de kommandon som du anger så att de uppfyller dina krav. Om du till exempel vill bevara färgprofilen för JPEG-bilden lägger du till följande kommandon i **[!UICONTROL Commands]** lista:

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`

   ![klibbig](assets/chlimage_1-199.png)

1. (Valfritt) Generera miniatyrbilder från en mellanrendering med ett enda kommando. Den mellanliggande återgivningen fungerar som källa för att generera statiska återgivningar och webbåtergivningar. Den här metoden är snabbare än den tidigare metoden. Du kan emellertid inte använda anpassade parametrar för miniatyrbilder med den här metoden.

   ![klibbig](assets/chlimage_1-200.png)

1. Om du vill generera webbåtergivningar konfigurerar du parametrarna i **[!UICONTROL Web-Enabled Image]** -fliken.

1. Synkronisera den uppdaterade [!UICONTROL DAM Update Asset] arbetsflödesmodell. Spara arbetsflödet.

Du kontrollerar konfigurationen genom att överföra en TIFF-avbildning och övervaka filen error.log. Du kommer att märka `INFO` meddelanden med omnämnanden av `SwitchEngineHandlingProcess execute: executing command line`. Loggarna anger de återgivningar som genereras. När arbetsflödet är klart kan du visa de nya återgivningarna i [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [MIME-typer som stöds, artikel](assets-formats.md#supported-image-transcoding-library)
