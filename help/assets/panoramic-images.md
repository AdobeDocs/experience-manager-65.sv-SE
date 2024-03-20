---
title: Panorambilder
description: Lär dig arbeta med panoramabilder i Dynamic Media.
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
docset: aem65
feature: Panoramic Images,Asset Management
role: User, Admin
exl-id: 4d6fbeb1-94db-4154-9e41-b76033fb4398
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 3%

---

# Panorambilder{#panoramic-images}

I det här avsnittet beskrivs hur du arbetar med visningsprogrammet för panoramabilder för att återge sfäriska panoramabilder så att du får en totalupplevelse på 360 grader av ett rum, en egenskap, en plats eller ett landskap.

Se även [Hantera visningsförinställningar](/help/assets/managing-viewer-presets.md).

![panoramabild2](assets/panoramic-image2.png)

## Överför resurser som ska användas med panoramabildsvisningsprogrammet {#uploading-assets-for-use-with-the-panoramic-image-viewer}

För att en överförd resurs ska kvalificeras som en sfärisk panoramabild som du tänker använda med panoramabildsvisningsprogrammet måste resursen ha antingen ett eller båda av följande:

* Proportionerna 2.
Du kan åsidosätta standardinställningen för proportioner på 2 i CRXDE Lite enligt följande:
  `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* Taggad med nyckelorden `equirectangular`, eller `spherical`och `panorama`, eller `spherical` och `panoramic`. Se [Använda taggar](/help/sites-authoring/tags.md).

Kriterierna för proportioner och nyckelord gäller även för panoramaresurser på sidan med resursinformation och för komponenten `Panoramic Media` i innehållshanteringssystemet.

Information om hur du överför resurser som ska användas med visningsprogrammet för panoramabilder finns i [Överför resurser](/help/assets/manage-assets.md#uploading-assets).

## Konfigurera Dynamic Media Classic {#configuring-dynamic-media-classic-scene}

För att visningsprogrammet för panoramabilder ska fungera på rätt sätt i Adobe Experience Manager synkroniserar du förinställningarna för visningsprogrammet för panoramabilder med Dynamic Media Classic och Dynamic Media Classic-specifika metadata så att visningsprogrammets förinställningar uppdateras i JCR-filen. Konfigurera Dynamic Media Classic enligt följande:

1. Öppna [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)och logga sedan in på ditt konto.

1. I sidans övre högra hörn väljer du **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Publish Setup]** > **[!UICONTROL Image Server]**.
1. På sidan Image Server Publish (Image Server Publish) går du till **[!UICONTROL Publish Context]** nedrullningsbar meny nära överkanten väljer **[!UICONTROL Image Serving]**.

1. På samma Image Server Publish-sida hittar du rubriken **[!UICONTROL Request Attributes]**.
1. Under rubriken Begärandeattribut går du till **[!UICONTROL Reply Image Size Limit]**. I de associerade fälten Bredd och Höjd ökar du den största tillåtna bildstorleken för panoramabilder.

   Dynamic Media Classic har en begränsning på 25 000 000 pixlar. Den största tillåtna storleken för bilder med 2:1-proportioner är 7 000 x 3 500. För vanliga skärmar räcker det dock med 4 096 x 2 048 pixlar.

   >[!NOTE]
   >
   >Endast bilder som ligger inom den största tillåtna bildstorleken stöds. Begäran om bilder som är större än storleksgränsen resulterar i ett 403-svar.

1. Gör följande under rubriken Begärandeattribut:

   * Ställ in begärandefelsökningsläget på **[!UICONTROL Disabled]**.
   * Ange låsläge för begäran till **[!UICONTROL Disabled]**.

   Dessa inställningar är nödvändiga för att du ska kunna använda `Panoramic Media` WCM-komponent i Experience Manager.

1. Längst ned på sidan Image Server Publish (Publicera på vänster sida) väljer du **[!UICONTROL Save]**.

1. Välj i det nedre högra hörnet **[!UICONTROL Close]**.

### Felsöka komponenten Panoramic Media WCM {#troubleshooting-the-panoramic-media-wcm-component}

Om du har släppt en bild i panoramamediakomponenten i WCM-filen och platshållaren för komponenten är komprimerad felsöker du följande:

* Om du får ett otillåtet 403-fel kan det bero på att den begärda bildstorleken är för stor. Granska **[!UICONTROL Reply Image Size Limit]** inställningar i [Konfigurera Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

* Om objektet har ett ogiltigt lås eller om ett parsningsfel visas på sidan, kontrollerar du Begär felsökningsläge och Begär låsläge för att vara säker på att de är inaktiverade.
* Om det är ett fel på arbetsytan för målning anger du en sökväg till definitionsfilen för regeluppsättningen och en ogiltig CTN för de tidigare förfrågningarna om bildresursen.
* Om bildkvaliteten blir låg efter en bildbegäran med en storlek över den gräns som stöds, kontrollerar du att **[!UICONTROL JPEG Encoding Attributes > Quality]** inställningen är inte tom. En typisk inställning för **[!UICONTROL Quality]** fältet är `95`. Inställningen finns på sidan Image Server Publish (Bildserverpublicering). Information om hur du kommer åt sidan finns i [Konfigurera Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

## Förhandsgranska panoramabilder {#previewing-panoramic-images}

Se [Förhandsgranska resurser](/help/assets/previewing-assets.md).

## Publicera panorambilder {#publishing-panoramic-images}

Se [Publicera resurser](/help/assets/publishing-dynamicmedia-assets.md).
