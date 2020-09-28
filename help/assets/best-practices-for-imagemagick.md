---
title: Installera och konfigurera ImageMagick
description: Läs om programmet ImageMagick, hur du installerar det, konfigurerar kommandoradsprocessen och använder det för att redigera, skapa och generera miniatyrbilder från bilder.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---


# Installera och konfigurera ImageMagick så att det fungerar med [!DNL Experience Manager Assets] {#install-and-configure-imagemagick-to-work-with-aem-assets}

ImageMagick är en plugin för att skapa, redigera, komponera och konvertera bitmappsbilder. Det kan läsa och skriva bilder i olika format (över 200), bland annat PNG, JPEG, JPEG-2000, GIF, TIFF, DPX, EXR, WebP, Postscript, PDF och SVG. Använd ImageMagick för att ändra storlek, vända, spegla, rotera, förvränga, skeva och omforma bilder. Du kan också justera bildfärger, använda olika specialeffekter eller rita text, linjer, polygoner, ellipser och kurvor med ImageMagick.

Använd [!DNL Adobe Experience Manager] mediehanteraren från kommandoraden för att bearbeta bilder via ImageMagick. Mer information om hur du arbetar med olika filformat med ImageMagick finns i [Metodtips](/help/assets/assets-file-format-best-practices.md)för resursfilformat. Mer information om alla filformat som stöds finns i Format som stöds för [resurser](/help/assets/assets-formats.md).

Om du vill bearbeta stora filer med ImageMagick bör du tänka på högre minneskrav än vanligt, möjliga ändringar av IM-policyer och den övergripande inverkan på prestanda. Minneskraven beror på olika faktorer som upplösning, bitdjup, färgprofil och filformat. Om du tänker bearbeta mycket stora filer med ImageMagick bör du testa servern korrekt [!DNL Experience Manager] . Äntligen finns det resurser som kan vara till hjälp.

>[!NOTE]
>
>Om du använder [!DNL Experience Manager] på [!DNL Adobe Managed Services] (AMS) kontaktar du kundtjänst på Adobe om du tänker bearbeta många högupplösta PSD- eller PSB-filer. [!DNL Experience Manager] kan inte bearbeta PSB-filer med hög upplösning som är större än 30000 x 23000 pixlar.

## Installera ImageMagick {#installing-imagemagick}

Det finns flera versioner av installationsfilerna för ImageMagic för olika operativsystem. Använd rätt version för ditt operativsystem.

1. Hämta rätt [ImageMagick-installationsfiler](https://www.imagemagick.org/script/download.php) för ditt operativsystem.
1. Starta installationsfilen om du vill installera ImageMagick på den disk där [!DNL Experience Manager] servern finns.

1. Ange miljövariabeln path till installationskatalogen för ImageMagic.
1. Om du vill kontrollera om installationen lyckades kör du `identify -version` kommandot.

## Ställa in kommandoradens processsteg {#set-up-the-command-line-process-step}

Du kan ställa in kommandoradens processsteg för ditt särskilda användningsfall. Följ de här stegen för att generera en bild och miniatyrbilder (140x100, 48x48, 319x319 och 1280x1280) varje gång du lägger till en JPEG-bildfil `/content/dam` på [!DNL Experience Manager] servern:

1. Gå till arbetsflödeskonsolen ( [!DNL Experience Manager] ) på`https://[aem_server]:[port]/workflow`servern och öppna **[!UICONTROL DAM Update Asset]** arbetsflödesmodellen.
1. Öppna **[!UICONTROL DAM Update Asset]** steget från arbetsflödesmodellen **[!UICONTROL EPS thumbnails (powered by ImageMagick)]** .
1. Lägg **[!UICONTROL Arguments tab]** till i `image/jpeg` listan i **[!UICONTROL Mime Types]** .

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. Ange följande kommando i **[!UICONTROL Commands]** rutan:

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. Markera **[!UICONTROL Delete Generated Rendition]** - och **[!UICONTROL Generate Web Rendition]** -flaggorna.

   ![select_flags](assets/select_flags.png)

1. På **[!UICONTROL Web Enabled Image]** fliken anger du information om återgivningen med måtten 1 280 × 1 280 pixlar. Ange dessutom `image/jpeg` i **[!UICONTROL Mimetype]** rutan.

   ![web_enabled_image](assets/web_enabled_image.png)

1. Click **[!UICONTROL OK]** to save the changes.

   >[!NOTE]
   >
   >Kommandot kanske inte kan köras med vissa Windows-versioner (till exempel Windows SE) eftersom det står i konflikt med det inbyggda `convert` `convert` verktyget som ingår i Windows-installationen. I det här fallet anger du den fullständiga sökvägen för verktyget ImageMagick. Ange t.ex.
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. Öppna **[!UICONTROL Process Thumbnails]** steget och lägg till MIME-typen `image/jpeg` under **[!UICONTROL Skip Mime Types]**.

   ![skip_mime_types](assets/skip_mime_types.png)

1. Lägg till MIME-typen **[!UICONTROL Web Enabled Image]** under fliken `image/jpeg` **[!UICONTROL Skip List]**. Click **[!UICONTROL OK]** to save the changes.

   ![web_enabled](assets/web_enabled.png)

1. Spara arbetsflödet.

1. Om du vill verifiera att bearbetningen är korrekt överför du en JPG-bild till [!DNL Assets]. När bearbetningen är klar kontrollerar du om en bild som har vänts och återgivningarna har genererats eller inte.

## Minska säkerhetsluckor {#mitigating-security-vulnerabilities}

Det finns flera säkerhetsluckor i samband med användning av ImageMagick för att bearbeta bilder. Att bearbeta bilder som skickas in av användaren innebär till exempel en risk för fjärrexekvering av kod (RCE).

Dessutom är olika bildbehandlingspluginer beroende av ImageMagick-biblioteket, inklusive, men inte begränsat till, PHP:s bild, Rubys magick och paperclip samt nydatums imagemagick.

Om du använder ImageMagick eller ett drabbat bibliotek rekommenderar Adobe att du åtgärdar de kända säkerhetsluckorna genom att utföra minst en av följande åtgärder (men helst båda):

1. Kontrollera att alla bildfiler börjar med de förväntade [&quot;magiska byten&quot;](https://en.wikipedia.org/wiki/List_of_file_signatures) som motsvarar de bildfilstyper som du stöder innan du skickar dem till ImageMagick för bearbetning.
1. Använd en principfil för att inaktivera sårbara ImageMagick-kodare. Den globala profilen för ImageMagick finns på `/etc/ImageMagick`.
