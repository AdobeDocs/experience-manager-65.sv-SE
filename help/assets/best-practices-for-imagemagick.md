---
title: Installera och konfigurera ImageMagick
description: Läs om programmet ImageMagick, hur du installerar det, konfigurerar kommandoradsprocessen och använder det för att redigera, skapa och generera miniatyrbilder från bilder.
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools
exl-id: 6c149d31-1e64-4d29-a32a-58bd69e9fa98
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---

# Installera och konfigurera ImageMagick så att det fungerar med [!DNL Experience Manager Assets] {#install-and-configure-imagemagick-to-work-with-aem-assets}

ImageMagick är ett plugin-program för att skapa, redigera, komponera och konvertera bitmappsbilder. Det kan läsa och skriva bilder i olika format (över 200), bland annat PNG, JPEG, JPEG-2000, GIF, TIFF, DPX, EXR, WebP, Postscript, PDF och SVG. Använd ImageMagick för att ändra storlek, vända, spegla, rotera, förvränga, skeva och omforma bilder. Du kan också justera bildfärger, använda olika specialeffekter eller rita text, linjer, polygoner, ellipser och kurvor med ImageMagick.

Använd [!DNL Adobe Experience Manager] mediehanterare från kommandoraden för att bearbeta bilder via ImageMagick. Information om hur du arbetar med olika filformat med ImageMagick finns i [Metodtips för att skapa filformat](/help/assets/assets-file-format-best-practices.md). Mer information om alla filformat som stöds finns i [Format som stöds för resurser](/help/assets/assets-formats.md).

Om du vill bearbeta stora filer med ImageMagick bör du tänka på högre minneskrav än vanligt, möjliga ändringar av IM-policyer och den övergripande inverkan på prestanda. Minneskraven beror på olika faktorer som upplösning, bitdjup, färgprofil och filformat. Om du tänker bearbeta mycket stora filer med ImageMagick bör du testa [!DNL Experience Manager] server. Äntligen finns det resurser som kan vara till hjälp.

>[!NOTE]
>
>Om du använder [!DNL Experience Manager] på [!DNL Adobe Managed Services] (AMS), kontakta Adobe kundsupport om du tänker bearbeta många högupplösta PSD- eller PSB-filer. [!DNL Experience Manager] kan inte bearbeta PSB-filer med hög upplösning som är större än 30000 x 23000 pixlar.

## Installera ImageMagick {#installing-imagemagick}

Det finns flera versioner av installationsfilerna för ImageMagic för olika operativsystem. Använd rätt version för ditt operativsystem.

1. Ladda ned [ImageMagick-installationsfiler](https://www.imagemagick.org/script/download.php) för ditt operativsystem.
1. Installera ImageMagick på disken som är värd för [!DNL Experience Manager] startar du installationsfilen.

1. Ange miljövariabeln path till installationskatalogen för ImageMagic.
1. Kontrollera om installationen lyckades genom att köra `identify -version` -kommando.

## Ställa in kommandoradens processsteg {#set-up-the-command-line-process-step}

Du kan ställa in kommandoradens processsteg för ditt särskilda användningsfall. Följ de här stegen för att generera en bild och miniatyrbilder som har vänts (140x100, 48x48, 319x319 och 1280x1280) varje gång du lägger till en JPEG-bildfil i `/content/dam` på [!DNL Experience Manager] server:

1. På [!DNL Experience Manager] server, gå till Workflow Console (`https://[aem_server]:[port]/workflow`) och öppna **[!UICONTROL DAM Update Asset]** arbetsflödesmodell.
1. Från **[!UICONTROL DAM Update Asset]** arbetsflödesmodell, öppna **[!UICONTROL EPS thumbnails (powered by ImageMagick)]** steg.
1. I **[!UICONTROL Arguments tab]**, lägga till `image/jpeg` till **[!UICONTROL Mime Types]** lista.

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. I **[!UICONTROL Commands]** anger du följande kommando:

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. Välj **[!UICONTROL Delete Generated Rendition]** och **[!UICONTROL Generate Web Rendition]** flaggor.

   ![select_flags](assets/select_flags.png)

1. I **[!UICONTROL Web Enabled Image]** anger du information för återgivningen med måtten 1 280 × 1 280 pixlar. Dessutom anger du `image/jpeg` i **[!UICONTROL Mimetype]** box.

   ![web_enabled_image](assets/web_enabled_image.png)

1. Klicka **[!UICONTROL OK]** för att spara ändringarna.

   >[!NOTE]
   >
   >The `convert` -kommandot kanske inte kan köras med vissa Windows-versioner (till exempel Windows SE) eftersom det är i konflikt med de ursprungliga `convert` som ingår i Windows-installationen. I det här fallet anger du den fullständiga sökvägen för verktyget ImageMagick. Ange till exempel
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. Öppna **[!UICONTROL Process Thumbnails]** och lägga till MIME-typen `image/jpeg` under **[!UICONTROL Skip Mime Types]**.

   ![skip_mime_types](assets/skip_mime_types.png)

1. I **[!UICONTROL Web Enabled Image]** lägger du till MIME-typen `image/jpeg` under **[!UICONTROL Skip List]**. Klicka **[!UICONTROL OK]** för att spara ändringarna.

   ![web_enabled](assets/web_enabled.png)

1. Spara arbetsflödet.

1. Om du vill verifiera korrekt bearbetning överför du en JPG-bild till [!DNL Assets]. När bearbetningen är klar kontrollerar du om en bild som har vänts och återgivningarna har genererats eller inte.

## Minska säkerhetsbrister {#mitigating-security-vulnerabilities}

Det finns flera säkerhetsluckor i samband med användning av ImageMagick för att bearbeta bilder. Att bearbeta bilder som skickas in av användaren innebär till exempel en risk för fjärrexekvering av kod (RCE).

Dessutom är olika bildbehandlingspluginer beroende av ImageMagick-biblioteket, inklusive, men inte begränsat till, PHP:s bild, Rubys magick och paperclip samt nydatums imagemagick.

Om du använder ImageMagick eller ett drabbat bibliotek rekommenderar Adobe att du åtgärdar de kända säkerhetsluckorna genom att utföra minst en av följande åtgärder (men helst båda):

1. Verifiera att alla bildfiler börjar med det förväntade [&quot;magiska byte&quot;](https://en.wikipedia.org/wiki/List_of_file_signatures) motsvarar de bildfiltyper som du stöder innan du skickar dem till ImageMagick för bearbetning.
1. Använd en principfil för att inaktivera sårbara ImageMagick-kodare. Den globala principen för ImageMagick finns på `/etc/ImageMagick`.
