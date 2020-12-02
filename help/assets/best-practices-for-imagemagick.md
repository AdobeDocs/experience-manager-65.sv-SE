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

Använd mediehanteraren [!DNL Adobe Experience Manager] från kommandoraden för att bearbeta bilder via ImageMagick. Information om hur du arbetar med olika filformat med ImageMagick finns i [Metodtips för resursfilformat](/help/assets/assets-file-format-best-practices.md). Mer information om alla filformat som stöds finns i [Format som stöds för resurser](/help/assets/assets-formats.md).

Om du vill bearbeta stora filer med ImageMagick bör du tänka på högre minneskrav än vanligt, möjliga ändringar av IM-policyer och den övergripande inverkan på prestanda. Minneskraven beror på olika faktorer som upplösning, bitdjup, färgprofil och filformat. Om du tänker bearbeta mycket stora filer med ImageMagick bör du testa [!DNL Experience Manager]-servern ordentligt. Äntligen finns det resurser som kan vara till hjälp.

>[!NOTE]
>
>Om du använder [!DNL Experience Manager] på [!DNL Adobe Managed Services] (AMS) kontaktar du kundtjänst på Adobe om du tänker bearbeta många högupplösta PSD- eller PSB-filer. [!DNL Experience Manager] kan inte bearbeta PSB-filer med hög upplösning som är större än 30000 x 23000 pixlar.

## Installera ImageMagick {#installing-imagemagick}

Det finns flera versioner av installationsfilerna för ImageMagic för olika operativsystem. Använd rätt version för ditt operativsystem.

1. Hämta rätt [ImageMagick-installationsfiler](https://www.imagemagick.org/script/download.php) för ditt operativsystem.
1. Om du vill installera ImageMagick på den disk där [!DNL Experience Manager]-servern finns startar du installationsfilen.

1. Ange miljövariabeln path till installationskatalogen för ImageMagic.
1. Om du vill kontrollera om installationen lyckades kör du kommandot `identify -version`.

## Ställa in kommandoradsprocessteget {#set-up-the-command-line-process-step}

Du kan ställa in kommandoradens processsteg för ditt särskilda användningsfall. Följ de här stegen för att skapa en vänd bild och miniatyrbilder (140x100, 48x48, 319x319 och 1280x1280) varje gång du lägger till en JPEG-bildfil i `/content/dam` på [!DNL Experience Manager]-servern:

1. Gå till arbetsflödeskonsolen (`https://[aem_server]:[port]/workflow`) på [!DNL Experience Manager]-servern och öppna arbetsflödesmodellen för **[!UICONTROL DAM Update Asset]**.
1. Öppna steget **[!UICONTROL EPS thumbnails (powered by ImageMagick)]** i arbetsflödesmodellen **[!UICONTROL DAM Update Asset]**.
1. I **[!UICONTROL Arguments tab]** lägger du till `image/jpeg` i listan **[!UICONTROL Mime Types]**.

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. Ange följande kommando i rutan **[!UICONTROL Commands]**:

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. Markera flaggorna **[!UICONTROL Delete Generated Rendition]** och **[!UICONTROL Generate Web Rendition]**.

   ![select_flags](assets/select_flags.png)

1. På fliken **[!UICONTROL Web Enabled Image]** anger du information för återgivningen med måtten 1 280 × 1 280 pixlar. Ange dessutom `image/jpeg` i rutan **[!UICONTROL Mimetype]**.

   ![web_enabled_image](assets/web_enabled_image.png)

1. Klicka på **[!UICONTROL OK]** för att spara ändringarna.

   >[!NOTE]
   >
   >Kommandot `convert` kanske inte körs med vissa Windows-versioner (till exempel Windows SE) eftersom det står i konflikt med det ursprungliga `convert`-verktyget som är en del av Windows-installationen. I det här fallet anger du den fullständiga sökvägen för verktyget ImageMagick. Ange t.ex.
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. Öppna steget **[!UICONTROL Process Thumbnails]** och lägg till MIME-typen `image/jpeg` under **[!UICONTROL Skip Mime Types]**.

   ![skip_mime_types](assets/skip_mime_types.png)

1. Lägg till MIME-typen `image/jpeg` under **[!UICONTROL Skip List]** på fliken **[!UICONTROL Web Enabled Image]**. Klicka på **[!UICONTROL OK]** för att spara ändringarna.

   ![web_enabled](assets/web_enabled.png)

1. Spara arbetsflödet.

1. Om du vill verifiera att bearbetningen är korrekt överför du en JPG-bild till [!DNL Assets]. När bearbetningen är klar kontrollerar du om en bild som har vänts och återgivningarna har genererats eller inte.

## Minskar säkerhetsbrister {#mitigating-security-vulnerabilities}

Det finns flera säkerhetsluckor i samband med användning av ImageMagick för att bearbeta bilder. Att bearbeta bilder som skickas in av användaren innebär till exempel en risk för fjärrexekvering av kod (RCE).

Dessutom är olika bildbehandlingspluginer beroende av ImageMagick-biblioteket, inklusive, men inte begränsat till, PHP:s bild, Rubys magick och paperclip samt nydatums imagemagick.

Om du använder ImageMagick eller ett drabbat bibliotek rekommenderar Adobe att du åtgärdar de kända säkerhetsluckorna genom att utföra minst en av följande åtgärder (men helst båda):

1. Kontrollera att alla bildfiler börjar med de förväntade [&quot;magiska byten&quot;](https://en.wikipedia.org/wiki/List_of_file_signatures) som motsvarar de bildfilstyper som du stöder innan du skickar dem till ImageMagick för bearbetning.
1. Använd en principfil för att inaktivera sårbara ImageMagick-kodare. Den globala principen för ImageMagick finns på `/etc/ImageMagick`.
