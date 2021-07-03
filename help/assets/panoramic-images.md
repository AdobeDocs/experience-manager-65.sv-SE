---
title: Panoramabilder
description: Lär dig hur du arbetar med panoramabilder i Dynamic Media.
uuid: ced3e5bd-93c8-4d5f-a397-1380d4d0a5e7
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 632a9074-b747-49a1-a57d-1f42bba1f4e9
docset: aem65
feature: Panoramabilder,Resurshantering
role: User, Admin
exl-id: 4d6fbeb1-94db-4154-9e41-b76033fb4398
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 4%

---

# Panoramabilder{#panoramic-images}

I det här avsnittet beskrivs hur du arbetar med visningsprogrammet för panoramabilder för att återge sfäriska panoramabilder så att du får en totalupplevelse på 360° i ett rum, en egenskap, en plats eller ett landskap.

Se även [Hantera visningsförinställningar](/help/assets/managing-viewer-presets.md).

![panoramabild2](assets/panoramic-image2.png)

## Överföra resurser som ska användas med panoramabildsvisningsprogrammet {#uploading-assets-for-use-with-the-panoramic-image-viewer}

För att en överförd resurs ska kvalificeras som en sfärisk panoramabild som du tänker använda med panoramabildsvisningsprogrammet måste resursen ha antingen ett eller båda av följande:

* Proportionerna 2.
Du kan åsidosätta standardinställningen för proportioner på 2 i CRXDE Lite enligt följande:
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* Taggad med nyckelorden `equirectangular`, `spherical`och `panorama`, eller `spherical` och `panoramic`. Se [Använda taggar](/help/sites-authoring/tags.md).

Kriterierna för proportioner och nyckelord gäller även för panoramaresurser på sidan med resursinformation och för komponenten `Panoramic Media` i innehållshanteringssystemet.

Information om hur du överför resurser som ska användas med visningsprogrammet för panoramabilder finns i [Överföra resurser](/help/assets/manage-assets.md#uploading-assets).

## Konfigurera Dynamic Media Classic {#configuring-dynamic-media-classic-scene}

För att visningsprogrammet för panoramabilder ska fungera på rätt sätt i Adobe Experience Manager synkroniserar du förinställningarna för visningsprogrammet för panoramabilder med Dynamic Media Classic och Dynamic Media Classic-specifika metadata så att visningsförinställningarna uppdateras i JCR-filen. Konfigurera Dynamic Media Classic enligt följande:

1. Öppna [Dynamic Media Classic-datorprogrammet](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) och logga sedan in på ditt konto.

1. Klicka på **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Publish Setup]** > **[!UICONTROL Image Server]** i sidans övre högra hörn.
1. Välj **[!UICONTROL Image Serving]** i listrutan **[!UICONTROL Publish Context]** på sidan Image Server Publish.

1. Gå till rubriken **[!UICONTROL Request Attributes]** på samma Image Server Publish-sida.
1. Gå till **[!UICONTROL Reply Image Size Limit]** under rubriken Begärandeattribut. I de associerade fälten Bredd och Höjd ökar du den största tillåtna bildstorleken för panoramabilder.

   Dynamic Media Classic har en begränsning på 25 000 000 pixlar. Den största tillåtna storleken för bilder med 2:1-proportioner är 7 000 x 3 500. För vanliga skärmar räcker det dock med 4 096 x 2 048 pixlar.

   >[!NOTE]
   >
   >Endast bilder som ligger inom den största tillåtna bildstorleken stöds. Begäran om bilder som är större än storleksgränsen resulterar i ett 403-svar.

1. Gör följande under rubriken Begärandeattribut:

   * Ställ in begäranobfuktningsläget på **[!UICONTROL Disabled]**.
   * Ange läget för låsning av begäran till **[!UICONTROL Disabled]**.

   Dessa inställningar är nödvändiga för att du ska kunna använda WCM-komponenten `Panoramic Media` i Experience Manager.

1. Klicka på **[!UICONTROL Save]** längst ned på sidan Image Server Publish (Publicera på vänster sida).

1. Klicka på **[!UICONTROL Close]** i det nedre högra hörnet.

### Felsöka komponenten Panoramic Media WCM {#troubleshooting-the-panoramic-media-wcm-component}

Om du har släppt en bild i panoramamediakomponenten i WCM-filen och platshållaren för komponenten är komprimerad felsöker du följande:

* Om du får ett otillåtet 403-fel kan det bero på att den begärda bildstorleken är för stor. Granska **[!UICONTROL Reply Image Size Limit]**-inställningarna i [Konfigurera Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

* Om objektet har ett ogiltigt lås eller om ett parsningsfel visas på sidan, kontrollerar du Begär felsökningsläge och Begär låsläge för att se om de är inaktiverade.
* Om det är ett fel på arbetsytan för målning anger du en sökväg till definitionsfilen för regeluppsättningen och en ogiltig CTN för de tidigare förfrågningarna om bildresursen.
* Om bildkvaliteten blir låg efter en bildbegäran med en storlek över den gräns som stöds, kontrollerar du att inställningen **[!UICONTROL JPEG Encoding Attributes > Quality]** inte är tom. En typisk inställning för fältet **[!UICONTROL Quality]** är `95`. Inställningen finns på sidan Image Server Publish (Bildserverpublicering). Mer information finns i [Konfigurera Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

## Förhandsgranska panoramabilder {#previewing-panoramic-images}

Se [Förhandsgranska resurser](/help/assets/previewing-assets.md).

## Publicera panoramabilder {#publishing-panoramic-images}

Se [Publicera resurser](/help/assets/publishing-dynamicmedia-assets.md).
