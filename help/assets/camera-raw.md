---
title: "[!DNL Adobe Camera Raw] stöd för bearbetning av digitala resurser"
description: Lär dig hur du aktiverar [!DNL Adobe Camera Raw] stöd i [!DNL Adobe Experience Manager Assets]
contentOwner: AG
role: Admin
feature: Developer Tools
exl-id: 7159a908-4c36-42b4-bbb4-d7fb1be4ee1b
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 3%

---

# Bearbeta bilder med [!DNL Adobe Camera Raw] {#camera-raw-support}

Du kan aktivera [!DNL Adobe Camera Raw] har stöd för att bearbeta råfilsformat, t.ex. CR2, NEF och RAF, och återge bilderna i JPEG-format. Funktionen stöds i [!DNL Adobe Experience Manager Assets] med [Camera Raw paket](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) som kan köpas från Software Distribution.

>[!NOTE]
>
>Funktionen har bara stöd för JPEG-renderingar. Det stöds i Windows 64-bitars, Mac OS och RHEL 7.x.

Aktivera [!DNL Camera Raw] stöd i [!DNL Experience Manager Assets]gör du så här:

1. Ladda ned [[!DNL Camera Raw] package](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-cameraraw-pkg-1.4.8.zip) från [!DNL Software Distribution].
1. Åtkomst `https://[aem_server]:[port]/workflow`. Öppna **[!UICONTROL DAM Update Asset]** arbetsflöde.
1. Redigera **[!UICONTROL Process Thumbnails]** steg.
1. Ange följande konfiguration i **[!UICONTROL Thumbnails]** tab:

   * **[!UICONTROL Thumbnails]**: `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL Skip Mime Types]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. I **[!UICONTROL Web Enabled Image]** -fliken, i **[!UICONTROL Skip List]** fält, ange `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. Lägg till **[!UICONTROL Camera Raw/DNG Handler]** steg nedanför **[!UICONTROL Process Thumbnails]** steg.
1. I **[!UICONTROL Camera Raw/DNG Handler]** lägger du till följande konfiguration i **[!UICONTROL Arguments]** tab:

   * **[!UICONTROL Mime Types]**: `image/dng` och `image/x-raw-(.*)`
   * **[!UICONTROL Command]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. Klicka på **[!UICONTROL Save]**.

>[!NOTE]
>
>Kontrollera att ovanstående konfiguration är samma som **[!UICONTROL Sample DAM Update Asset With Camera RAW and DNG Handling Step]** konfiguration.

Nu kan du importera Camera Raw-filer till Assets. När du har installerat det Camera Raw paketet och konfigurerat arbetsflödet, **[!UICONTROL Image Adjust]** visas i listan med sidorutor.

![chlimage_1-131](assets/chlimage_1-337.png)

*Bild: Alternativ på sidopanelen.*

![chlimage_1-132](assets/chlimage_1-338.png)

*Bild: Använd alternativet om du vill göra små ändringar i dina bilder.*

När du har sparat redigeringarna i en [!DNL Camera Raw] bild, en ny rendering `AdjustedPreview.jpg` genereras för bilden. För andra bildtyper förutom [!DNL Camera Raw]återspeglas ändringarna i alla återgivningar.

## God praxis, kända problem och begränsningar {#best-practices}

Funktionen har följande begränsningar:

* Funktionen har bara stöd för JPEG-renderingar. Det stöds på 64-bitars Windows, Mac OS och RHEL 7.x.
* Metadatatillbakaskrivning stöds inte för RAW- och DNG-format.
* The [!DNL Camera Raw] biblioteket har begränsningar för det totala antalet pixlar som kan bearbetas samtidigt. För närvarande kan programmet bearbeta maximalt 65 000 pixlar på den långa sidan av en fil eller 512 MP, oavsett vilket villkor som påträffas först.
