---
title: Konverteringsbibliotek för bildbehandling
description: Lär dig hur du konfigurerar och använder Adobes Imaging Transcoding Library, en bildbehandlingslösning som kan utföra grundläggande bildhanteringsfunktioner, inklusive kodning, omkodning, bildomsampling och storleksändring.
contentOwner: AG
translation-type: tm+mt
source-git-commit: bccc937c1e1a349ab292a748c3c7b9d0c68b6199
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 0%

---


# Konverteringsbibliotek för bildbehandling {#imaging-transcoding-library}

Adobes Imaging Transcoding Library är en tillverkarspecifik bildbehandlingslösning som kan utföra grundläggande bildhanteringsfunktioner, som:

* Kodning
* Omkodning (konverterar format som stöds)
* Bildomsampling, använda PS- och Intel IPP-algoritmer
* Bevara bitdjup och färgprofil
* Komprimering av JPEG-kvalitet
* Storleksändring av bild

Bildkonverteringsbiblioteket har stöd för CMYK och fullt stöd för alfa, förutom CMYK-Alpha.

Förutom stöd för ett stort antal filformat och profiler har Imaging Transcoding Library betydande fördelar jämfört med andra tredjepartslösningar när det gäller prestanda, skalbarhet och kvalitet. Här är några av fördelarna med att använda Imaging Transcoding Library:

* **Skalförändra med ökad filstorlek eller upplösning**: Skalning uppnås främst genom den patenterade möjligheten hos Imaging Transcoding Library att ändra storlek samtidigt som filer avkodas. Detta gör att minnesanvändningen vid körning alltid är optimal och inte är en kvadratisk funktion som ökar filstorleken eller upplösningsmegapixlar. Konverteringsbiblioteket för bildbehandling kan bearbeta större och högupplösta filer (som innehåller högre megapixlar). Tredjepartsverktyg som ImageMagick kan inte hantera stora filer och krascher när sådana filer bearbetas.
* **Kvalitetskomprimerings- och storleksändringsalgoritmer** i Photoshop: Överensstämmelse med branschstandard när det gäller kvalitet på nedsampling (mjuk, skarp och automatisk bikubisk) och komprimeringskvalitet. Imaging Transcoding Library utvärderar dessutom kvalitetsfaktorn för indatabilden och använder intelligent optimala tabeller och kvalitetsinställningar för utdatabilden. Detta ger filer av optimal storlek utan att den visuella kvaliteten äventyras.
* **Hög genomströmning:** Svarstiden är kortare och genomströmningen är konsekvent högre än ImageMagick. Därför bör Imaging Transcoding Library minska väntetiden för användare och kostnaden för värdtjänster.
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
 -BitDepth 8/16: Preserves Bit Depth. Bitdepth ‘4’ is automatically converted to ‘8’
 -preserveBitDepth: Downscales Bit Depth (No upscaling)
 -preserveCMYK: Preserves CMYK color space
 -jpegQuality: Provides jpeg quality parameter (0-12 , corresponding to Photoshop qualities)
 -ResamplingMethod BiCubic/Lanczos/PSBicubic: Provides resampling methods. PSBicubic is a Photoshop quality resampling method.
 -resize
```

Du kan konfigurera följande alternativ för `-resize` parametern:

* `X`: Fungerar ungefär som Experience Manager. Till exempel -resize 319.
* `WxH`: Proportionerna behålls inte, till exempel `-resize 319x319`.
* `Wx`: Fastställer bredden och beräknar höjden med bibehållna proportioner. Till exempel `-resize 319x`.
* `xH`: Korrigerar höjden och beräknar bredden med bibehållna proportioner. Till exempel `-resize x319`.

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## Konfigurera bildkonverteringsbibliotek {#configuring-imaging-transcoding-library}

Om du vill konfigurera ITL-bearbetning skapar du en konfigurationsfil och uppdaterar arbetsflödet för att köra det.

### Skapa konfigurationsfil för extraherat paket {#create-conf-file}

Om du vill konfigurera biblioteket skapar du en .conf-fil som anger biblioteken med följande steg. Du behöver administratörs- eller rotbehörigheter.

1. Hämta paketet [Imaging Transcoding Library från Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) och installera det med Package Manager. Paketet är kompatibelt med Experience Manager 6.5.

1. Om du vill veta ett paket-ID för `com.day.cq.dam.cq-dam-switchengine`loggar du in på webbkonsolen och klickar på **[!UICONTROL OSGi > Bundles]**. Du kan även öppna paketkonsolen genom att gå till `https://[aem_server:[port]/system/console/bundles/` URL. Hitta paketet och dess ID `com.day.cq.dam.cq-dam-switchengine` .

1. Kontrollera att alla nödvändiga bibliotek extraheras genom att kontrollera mappen med kommandot `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`där mappnamnet skapas med paket-ID:t. Kommandot är till exempel `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` om paket-ID är `588`.

1. Skapa `SWitchEngineLibs.conf` fil som ska länkas till biblioteket.

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. Lägg till `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` sökvägen till conf-filen med `cat SWitchEngineLibs.conf` kommandot .

1. Kör `ldconfig` kommando för att skapa nödvändiga länkar och cacheminne.

1. Redigera `.bash_profile` filen i det konto som används för att starta Experience Manager. Lägg till `LD_LIBRARY_PATH` följande:

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. Om du vill vara säker på att värdet för banan är inställt på `.`använder du `echo $LD_LIBRARY_PATH` kommandot. Utdata ska bara vara `.`. Starta om sessionen om värdet inte är `.`angivet.

### Konfigurera [!UICONTROL DAM Update Asset] arbetsflöde {#configure-dam-asset-update-workflow}

Uppdatera arbetsflödet så att det använder biblioteket för bearbetning av bilder. [!UICONTROL DAM Update Asset]

1. I användargränssnittet för Experience Manager väljer du **[!UICONTROL Tools > Workflow > Models]**.

1. Öppna arbetsflödesmodellen från **[!UICONTROL Workflow Models]** sidan i redigeringsläge **[!UICONTROL DAM Update Asset]** .

1. Öppna arbetsflödets **[!UICONTROL Process Thumbnails]** processsteg. Lägg till de MIME-typer som du vill hoppa över standardprocessen för generering av miniatyrbilder för i **[!UICONTROL Thumbnails]** **[!UICONTROL Skip Mime Types]** listan på fliken.
Om du till exempel vill skapa miniatyrbilder för en TIFF-bild med hjälp av Imaging Transcoding Library, anger du `image/tiff` i **[!UICONTROL Skip Mime Types]** fältet.

1. Lägg till de MIME-typer som du vill hoppa över standardprocessen för generering av webbåtergivning i på **[!UICONTROL Web Enabled Image]** fliken **[!UICONTROL Skip List]**. Om du t.ex. hoppade över MIME-typen `image/tiff` i ovanstående steg lägger du till `image/tiff` i hopplistan.

1. Öppna **[!UICONTROL EPS thumbnails (powered by ImageMagick)]** steget och gå till **[!UICONTROL Arguments]** fliken. I **[!UICONTROL Mime Types]** listan lägger du till de MIME-typer som du vill att Imaging Transcoding Library ska bearbeta. Om du t.ex. hoppade över MIME-typen `image/tiff` i ovanstående steg lägger du till `image/jpeg` i **[!UICONTROL Mime Types]** listan.

1. Ta bort eventuella standardkommandon.

1. Växla sidopanelen och lägg till i listan med steg **[!UICONTROL SWitchEngine Handler]**.

1. Lägg till kommandon i [!UICONTROL SwitchEngine Handler] baserat på dina egna krav. Finjustera parametrarna för de kommandon som du anger så att de uppfyller dina krav. Om du till exempel vill bevara färgprofilen för JPEG-bilden lägger du till följande kommandon i **[!UICONTROL Commands]** listan:

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`
   ![klibbig](assets/chlimage_1-199.png)

1. (Valfritt) Generera miniatyrbilder från en mellanrendering med ett enda kommando. Den mellanliggande återgivningen fungerar som källa för att generera statiska återgivningar och webbåtergivningar. Den här metoden är snabbare än den tidigare metoden. Du kan emellertid inte använda anpassade parametrar för miniatyrbilder med den här metoden.

   ![klibbig](assets/chlimage_1-200.png)

1. Konfigurera parametrar på **[!UICONTROL Web-Enabled Image]** fliken för att generera webbåtergivningar.

1. Synkronisera den uppdaterade [!UICONTROL DAM Update Asset] arbetsflödesmodellen. Spara arbetsflödet.

Verifiera konfigurationen, ladda upp en TIFF-bild och övervaka filen error.log. Du kommer att lägga märke till `INFO` meddelanden med omnämnanden av `SwitchEngineHandlingProcess execute: executing command line`. Loggarna anger de återgivningar som genereras. När arbetsflödet är klart kan du visa de nya återgivningarna i Experience Manager.

>[!MORELIKETHIS]
>
>* [MIME-typer som stöds, artikel](assets-formats.md#supported-image-transcoding-library)

