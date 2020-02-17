---
title: Installera och konfigurera ImageMagick så att det fungerar med AEM Assets
description: Läs om programmet ImageMagick, hur du installerar det, konfigurerar kommandoradsprocessen och använder det för att redigera, skapa och generera miniatyrbilder från bilder.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 70a88085a0fd6e949974aa7f1f92fdc3def3d98e

---


# Installera och konfigurera ImageMagick så att det fungerar med AEM Assets{#install-and-configure-imagemagick-to-work-with-aem-assets}

ImageMagick är en plugin för att skapa, redigera, komponera och konvertera bitmappsbilder. Det kan läsa och skriva bilder i olika format (över 200), bland annat PNG, JPEG, JPEG-2000, GIF, TIFF, DPX, EXR, WebP, Postscript, PDF och SVG. Använd ImageMagick för att ändra storlek, vända, spegla, rotera, förvränga, skeva och omforma bilder. Du kan också justera bildfärger, använda olika specialeffekter eller rita text, linjer, polygoner, ellipser och kurvor med ImageMagick.

Använd Adobe Experience Manager-mediehanteraren (AEM) från kommandoraden för att bearbeta bilder via ImageMagick. Mer information om hur du arbetar med olika filformat med ImageMagick finns i [Metodtips](/help/assets/assets-file-format-best-practices.md)för resursfilformat. Mer information om alla filformat som stöds finns i Format som stöds för [resurser](/help/assets/assets-formats.md).

Om du vill bearbeta stora filer med ImageMagick bör du tänka på högre minneskrav än vanligt, möjliga ändringar av IM-policyer och den övergripande inverkan på prestanda. Minneskraven beror på olika faktorer som upplösning, bitdjup, färgprofil och filformat. Om du tänker bearbeta mycket stora filer med ImageMagick bör du testa AEM-servern ordentligt. Äntligen finns det resurser som kan vara till hjälp.

>[!NOTE]
>
>Om du använder AEM på Adobes hanterade tjänster (AMS) kan du kontakta Adobe Support om du tänker bearbeta många stora PSD- eller PSB-filer.

## Installera ImageMagick {#installing-imagemagick}

Det finns flera versioner av installationsfilerna för ImageMagic för olika operativsystem. Använd rätt version för ditt operativsystem.

1. Hämta rätt [ImageMagick-installationsfiler](https://www.imagemagick.org/script/download.php) för ditt operativsystem.
1. Starta installationsfilen om du vill installera ImageMagick på den skiva som är värd för AEM-servern.

1. Ange miljövariabeln path till installationskatalogen för ImageMagic.
1. Om du vill kontrollera om installationen lyckades kör du `identify -version` kommandot.

## Ställa in kommandoradens processsteg {#set-up-the-command-line-process-step}

Du kan ställa in kommandoradens processsteg för ditt särskilda användningsfall. Följ de här stegen för att generera en bild och miniatyrbilder (140x100, 48x48, 319x319 och 1280x1280) varje gång du lägger till en JPEG-bildfil `/content/dam` på AEM-servern:

1. Gå till arbetsflödeskonsolen ( `https://[*AEM server*]:[*Port*]/workflow`) på AEM-servern och öppna arbetsflödesmodellen för **[!UICONTROL DAM-uppdatering]** .
1. Öppna steget **[!UICONTROL EPS-miniatyrbilder (som drivs av ImageMagick)]** från arbetsflödesmodellen för **[!UICONTROL DAM-uppdatering av resurser]** .
1. På fliken **** Argument lägger du `image/jpeg` till i listan **[!UICONTROL Mime-typer]** .

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. Ange följande kommando i rutan **[!UICONTROL Kommandon]** :

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. Markera **[!UICONTROL Ta bort genererad återgivning]** och **[!UICONTROL Generera]** webbåtergivning.

   ![select_flags](assets/select_flags.png)

1. På fliken **[!UICONTROL Webbaktiverad bild]** anger du information om återgivningen med måtten 1 280 × 1 280 pixlar. Dessutom anger du *bild/jpeg* i rutan **[!UICONTROL Mimeter]** .

   ![web_enabled_image](assets/web_enabled_image.png)

1. Tryck/klicka på **[!UICONTROL OK]** för att spara ändringarna.

   >[!NOTE]
   >
   >Kommandot kanske inte kan köras med vissa Windows-versioner (till exempel Windows SE) eftersom det står i konflikt med det inbyggda `convert` `convert` verktyget som ingår i Windows-installationen. I det här fallet anger du den fullständiga sökvägen för verktyget ImageMagick. Ange t.ex.
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. Öppna steget **[!UICONTROL Bearbeta miniatyrer]** och lägg till MIME-typen `image/jpeg` under **[!UICONTROL Hoppa över Mime-typer]**.

   ![skip_mime_types](assets/skip_mime_types.png)

1. På fliken **[!UICONTROL Webbaktiverad bild]** lägger du till MIME-typen `image/jpeg` under **[!UICONTROL Hoppa över lista]**. Tryck/klicka på **[!UICONTROL OK]** för att spara ändringarna.

   ![web_enabled](assets/web_enabled.png)

1. Spara arbetsflödet.
1. Om du vill kontrollera om ImageMagic kan bearbeta bilder på rätt sätt överför du en JPG-bild till AEM Assets. Kontrollera om en bild som har vänts och återgivningarna genereras för den.

## Minska säkerhetsluckor {#mitigating-security-vulnerabilities}

Det finns flera säkerhetsluckor i samband med användning av ImageMagick för att bearbeta bilder. Att bearbeta bilder som skickas in av användaren innebär till exempel en risk för fjärrexekvering av kod (RCE).

Dessutom är olika bildbehandlingspluginer beroende av ImageMagick-biblioteket, inklusive, men inte begränsat till, PHP:s bild, Rubys magick och paperclip samt nydatums imagemagick.

Om du använder ImageMagick eller ett drabbat bibliotek rekommenderar Adobe att du åtgärdar de kända säkerhetsluckorna genom att utföra minst en av följande åtgärder (men helst båda):

1. Kontrollera att alla bildfiler börjar med de förväntade [&quot;magiska byten&quot;](https://en.wikipedia.org/wiki/List_of_file_signatures) som motsvarar de bildfilstyper som du stöder innan du skickar dem till ImageMagick för bearbetning.
1. Använd en principfil för att inaktivera sårbara ImageMagick-kodare. Den globala profilen för ImageMagick finns på `/etc/ImageMagick`.
