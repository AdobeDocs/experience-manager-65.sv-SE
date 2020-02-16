---
title: Konverteringsbibliotek för bildbehandling
description: Lär dig hur du konfigurerar och använder Adobes Imaging Transcoding Library, en bildbehandlingslösning som kan utföra grundläggande bildhanteringsfunktioner, inklusive kodning, omkodning, bildomsampling och storleksändring.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

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

* **Skalförändra med ökad filstorlek eller upplösning**: Skalning uppnås främst genom den patenterade möjligheten hos Imaging Transcoding Library att ändra storlek samtidigt som filer avkodas. Detta gör att minnesanvändningen vid körning alltid är optimal och inte är en kvadratisk funktion som ökar filstorleken eller upplösningsmegapixlar. Konverteringsbiblioteket för bilder kan bearbeta större och högupplösta filer (som innehåller högre megapixlar). Tredjepartsverktyg som ImageMagick kan inte hantera stora filer och krascher när sådana filer bearbetas.
* **Kvalitetskomprimerings- och storleksändringsalgoritmer** i Photoshop: Överensstämmelse med branschstandard när det gäller kvalitet på nedsampling (mjuk, skarp och automatisk bikubisk) och komprimeringskvalitet. Imaging Transcoding Library utvärderar dessutom kvalitetsfaktorn för indatabilden och använder intelligent optimala tabeller och kvalitetsinställningar för utdatabilden. Detta ger filer av optimal storlek utan att den visuella kvaliteten äventyras.
* **** Hög genomströmning: Svarstiden är kortare och genomströmningen är genomgående högre än ImageMagick. Därför bör Imaging Transcoding Library minska väntetiden för användare och kostnaden för värdtjänster.
* **** Skala bättre med samtidig inläsning: Omkodningsbiblioteket för bilder fungerar optimalt under samtidiga inläsningsförhållanden. Den ger hög genomströmning med optimala processorprestanda, minnesanvändning och låg svarstid, vilket minskar kostnaderna för värdtjänster.

## Plattformar som stöds {#supported-platforms}

Imaging Transcoding Library är bara tillgängligt för distributioner av RHEL 7 och CentOS 7.

>[!NOTE]
>
>Mac OS och andra *nix-distributioner (till exempel Debian och Ubuntu) stöds inte.

## Usage {#usage}

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

* `X`: `Works similar to AEM. For example -resize 319.`
* `WxH`: `Aspect Ratio will not be maintained, For example -resize 319X319.`
* `Wx`: `Fixes the width and calculates the height maintaining the aspect ratio. For example -resize 319x.`
* `xH`: `Fixes the height and calculates the width maintaining the aspect ratio. For example -resize x319.`

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## Konfigurera bildkonverteringsbibliotek {#configuring-imaging-transcoding-library}

Om du vill konfigurera ITL-bearbetning skapar du en konfigurationsfil och uppdaterar arbetsflödet för att köra det.

### Skapa konfigurationsfil för extraherat paket {#create-conf-file}

Om du vill konfigurera biblioteket skapar du en .conf-fil som anger biblioteken med följande steg. Du behöver administratörs- eller rotbehörigheter.

1. Ladda ned paketet [](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) Imaging Transcoding Library och installera det med Package Manager. Paketet är kompatibelt med AEM 6.5.

1. Om du vill veta ett paket-ID för `com.day.cq.dam.cq-dam-switchengine`loggar du in på webbkonsolen och trycker på **[!UICONTROL OSGi > Bundles]**. Du kan även öppna paketkonsolen genom att gå till `https://[aem_server:[port]/system/console/bundles/` URL. Hitta paketet och dess ID `com.day.cq.dam.cq-dam-switchengine` .

1. Kontrollera att alla nödvändiga bibliotek extraheras genom att kontrollera mappen med kommandot `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`där mappnamnet skapas med paket-ID:t. Kommandot är till exempel `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` om paket-ID är `588`.

1. Skapa `SWitchEngineLibs.conf` fil som ska länkas till biblioteket.

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. Lägg till `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` sökvägen till conf-filen med `cat SWitchEngineLibs.conf` kommandot .

1. Kör `ldconfig` kommando för att skapa nödvändiga länkar och cacheminne.

1. Redigera `.bash_profile` filen på kontot som används för att starta AEM. Lägg till `LD_LIBRARY_PATH` följande:

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. Om du vill vara säker på att värdet för banan är inställt på `.`använder du `echo $LD_LIBRARY_PATH` kommandot. Utdata ska bara vara `.`. Starta om sessionen om värdet inte är `.`angivet.

### Konfigurera arbetsflöde för DAM-uppdatering av resurser {#configure-dam-asset-update-workflow}

Uppdatera arbetsflödet för [!UICONTROL DAM-uppdatering av resurser] om du vill använda biblioteket för bearbetning av bilder.

1. Tryck/klicka på AEM-logotypen och gå till **[!UICONTROL Verktyg > Arbetsflöde > Modeller]**.

1. Öppna arbetsflödesmodellen **[!UICONTROL DAM Update Asset]** på sidan **[!UICONTROL Arbetsflödesmodeller]** i redigeringsläge.

1. Öppna steget **[!UICONTROL Bearbeta miniatyrbilder]** i arbetsflödet. På fliken **[!UICONTROL Miniatyrbilder]** lägger du till de MIME-typer för vilka du vill hoppa över standardprocessen för generering av miniatyrbilder i listan **[!UICONTROL Hoppa över Mime-typer]** .
Om du till exempel vill skapa miniatyrer för en TIFF-bild med hjälp av Imaging Transcoding Library, anger du `image/tiff` i fältet **[!UICONTROL Hoppa över Mime Types]** .

1. På fliken **[!UICONTROL Webbaktiverad bild]** lägger du till de MIME-typer som du vill hoppa över standardprocessen för generering av webbåtergivning i **[!UICONTROL Hoppa över lista]**. Om du t.ex. hoppade över MIME-typen `image/tiff` i ovanstående steg lägger du till `image/tiff` i hopplistan.

1. Öppna steget **[!UICONTROL EPS-miniatyrbilder (med ImageMagick)]** och gå till fliken **[!UICONTROL Argument]** . I listan **[!UICONTROL Mime-typer]** lägger du till de MIME-typer som du vill att Imaging Transcoding Library ska bearbeta. Om du t.ex. hoppade över MIME-typen `image/tiff` i ovanstående steg lägger du `image/jpeg` till i listan **[!UICONTROL Mime-typer]** .

1. Ta bort eventuella standardkommandon.

1. Växla sidopanelen och lägg till **[!UICONTROL SWitchEngine-hanterare]** från listan med steg.

1. Lägg till kommandon i [!UICONTROL SwitchEngine-hanteraren] baserat på dina egna krav. Finjustera parametrarna för de kommandon som du anger så att de uppfyller dina krav. Om du till exempel vill bevara färgprofilen i JPEG-bilden lägger du till följande kommandon i **[!UICONTROL kommandolistan]** :

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`
   ![klibbig](assets/chlimage_1-199.png)

1. (Valfritt) Generera miniatyrbilder från en mellanrendering med ett enda kommando. Den mellanliggande återgivningen fungerar som källa för att generera statiska återgivningar och webbåtergivningar. Den här metoden är snabbare än den tidigare metoden. Du kan emellertid inte använda anpassade parametrar för miniatyrbilder med den här metoden.

   ![klibbig](assets/chlimage_1-200.png)

1. Om du vill generera webbåtergivningar konfigurerar du parametrar på fliken **[!UICONTROL Webbaktiverad bild]** .

1. Synkronisera den uppdaterade [!UICONTROL arbetsflödesmodellen för DAM-uppdatering av resurser] . Spara arbetsflödet.

Verifiera konfigurationen, ladda upp en TIFF-bild och övervaka filen error.log. Du kommer att lägga märke till `INFO` meddelanden med omnämnanden av `SwitchEngineHandlingProcess execute: executing command line`. Loggarna anger de återgivningar som genereras. När arbetsflödet är klart kan du visa de nya återgivningarna i AEM.

>[!MORELIKETHIS]
>
>* [MIME-typer som stöds, artikel](assets-formats.md#supported-image-transcoding-library)