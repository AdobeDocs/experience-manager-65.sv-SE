---
title: Använd PDF-rastrering för att generera återgivningar av PDF-filer.
description: Generera högkvalitativa miniatyrbilder och renderingar med Adobe PDF Rasterizer-biblioteket i [!DNL Adobe Experience Manager].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5f3af7041029a1b4dd1cbb4c65bd488b62c7e10c
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---


# Använd PDF-rastrering {#using-pdf-rasterizer}

När du överför stora, innehållsintensiva PDF- eller AI-filer till [!DNL Adobe Experience Manager Assets]kanske standardkonverteringen inte genererar korrekta utdata. Adobes PDF Rasterizer-bibliotek kan generera tillförlitligare och exaktare utdata jämfört med utdata från ett standardbibliotek. Adobe rekommenderar att du använder PDF-rastreringsbiblioteket för följande scenarier:

* Tunga, innehållsintensiva AI-filer eller PDF-filer.
* AI-filer och PDF-filer med miniatyrer som inte genereras som standard.
* AI-filer med Pantone Matching System-färger (PMS).

Miniatyrbilder och förhandsgranskningar som genererats med PDF Rasterizer har bättre kvalitet jämfört med färdiga utdata och ger därför en konsekvent visningsupplevelse på olika enheter. Adobe PDF Rasterizer-biblioteket har inte stöd för konvertering av färgrymd. Det skrivs alltid ut på RGB, oavsett källfilens färgrymd.

1. Installera PDF-rastreringspaketet på din [!DNL Experience Manager] distribution från [paketresursen](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/product/assets/aem-assets-pdf-rasterizer-pkg).

   >[!NOTE]
   >
   >PDF Rasterizer-biblioteket är endast tillgängligt för Windows och Linux.

1. Gå till [!DNL Assets] arbetsflödeskonsolen på `https://[aem_server]:[port]/workflow`. Öppna [!UICONTROL DAM Update Asset] arbetsflöde.

1. Följ de här stegen för att förhindra att miniatyrbilder och webbåtergivning genereras för PDF-filer och AI-filer med standardmetoderna:

   * Öppna **[!UICONTROL Process Thumbnails]** steget och lägg till `application/pdf` eller lägg till `application/postscript` i **[!UICONTROL Skip Mime Types]** fältet under **[!UICONTROL Thumbnails]** fliken efter behov.
   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * Lägg till **[!UICONTROL Web Enabled Image]** eller `application/pdf` under på `application/postscript` fliken **[!UICONTROL Skip List]** beroende på dina behov.
   ![Konfiguration för att hoppa över bearbetning av miniatyrbilder för ett bildformat](assets/web_enabled_imageskiplist.png)

1. Öppna **[!UICONTROL Rasterize PDF/AI Image Preview Rendition]** steget och ta bort MIME-typen som du vill hoppa över standardgenereringen av förhandsvisningsbildåtergivningar för. Ta till exempel bort MIME-typen `application/pdf`, `application/postscript`eller `application/illustrator` från **[!UICONTROL MIME Types]** listan.

   ![process_arguments](assets/process_arguments.png)

1. Dra **[!UICONTROL PDF Rasterizer Handler]** steget från sidopanelen till nedanför **[!UICONTROL Process Thumbnails]** steget.
1. Konfigurera följande argument för **[!UICONTROL PDF Rasterizer Handler]** steget:

   * MIME-typer: `application/pdf` eller `application/postscript`
   * Kommandon: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * Lägg till miniatyrstorlekar: 319:319, 140:100, 48:48. Lägg till anpassad miniatyrkonfiguration, om det behövs.
   Kommandoradsargumenten för `PDFRasterizer` kommandot kan innehålla följande:

   * `-d`: Flagga för smidig återgivning av text, vektorgrafik och bilder. Skapar bilder med bättre kvalitet. Om du tar med den här parametern körs kommandot långsamt och bildstorleken ökar.

   * `-p`: Sidnummer. Standardvärdet är alla sidor. Om du vill ange alla sidor använder du `*`.

   * `-s`: Största bilddimension (höjd eller bredd). Detta konverteras till DPI för varje sida. Om sidorna har olika storlek kan varje sida eventuellt skalas med olika mängd. Standardvärdet är faktisk sidstorlek.

   * `-t`: Typ av utdatabild. Giltiga typer är JPEG, PNG, GIF och BMP. Standardvärdet är JPEG.

   * `-i`: Sökväg för PDF-indata. Det är en obligatorisk parameter.

   * `-h`: Hjälp


1. Om du vill ta bort mellanliggande återgivningar markerar du **[!UICONTROL Delete Generated Rendition]**.
1. Om du vill att PDF-rastreraren ska kunna generera webbåtergivningar väljer du **[!UICONTROL Generate Web Rendition]**.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. Ange inställningarna på **[!UICONTROL Web Enabled Image]** fliken.

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. Spara arbetsflödet.
1. Om du vill att PDF-rastreraren ska kunna bearbeta PDF-sidor med PDF-bibliotek öppnar du **[!UICONTROL DAM Process Subasset]** modellen från arbetsflödeskonsolen.
1. Dra steget PDF-rastreringshanteraren från sidopanelen under **[!UICONTROL Create Web-Enabled Image Rendition]** steget.
1. Konfigurera följande argument för **[!UICONTROL PDF Rasterizer Handler]** steget:

   * MIME-typer: `application/pdf` eller `application/postscript`

   * Kommandon: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * Lägg till miniatyrstorlekar: `319:319`, `140:100`, `48:48`. Lägg till en anpassad miniatyrkonfiguration efter behov.
   Kommandoradsargumenten för `PDFRasterizer` kommandot kan innehålla följande:

   * `-d`: Flagga för smidig återgivning av text, vektorgrafik och bilder. Skapar bilder med bättre kvalitet. Om du tar med den här parametern körs kommandot långsamt och bildstorleken ökar.

   * `-p`: Sidnummer. Standardvärdet är alla sidor. `*` anger alla sidor.

   * `-s`: Största bilddimension (höjd eller bredd). Detta konverteras till DPI för varje sida. Om sidorna har olika storlek kan varje sida eventuellt skalas med olika mängd. Standardvärdet är faktisk sidstorlek.

   * `-t`: Typ av utdatabild. Giltiga typer är JPEG, PNG, GIF och BMP. Standardvärdet är JPEG.

   * `-i`: Sökväg för PDF-indata. Det är en obligatorisk parameter.

   * `-h`: Hjälp


1. Om du vill ta bort mellanliggande återgivningar markerar du **[!UICONTROL Delete Generated Rendition]**.
1. Om du vill att PDF-rastreraren ska kunna generera webbåtergivningar väljer du **[!UICONTROL Generate Web Rendition]**.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. Ange inställningarna på **[!UICONTROL Web Enabled Image]** fliken.

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. Spara arbetsflödet.
1. Överför en PDF eller en AI-fil till [!DNL Experience Manager Assets]. I PDF-rastreraren genereras miniatyrbilder och webbåtergivningar för filen.
