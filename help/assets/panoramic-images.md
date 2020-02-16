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
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Panoramabilder{#panoramic-images}

I det här avsnittet beskrivs hur du arbetar med visningsprogrammet för panoramabilder för att återge sfäriska panoramabilder så att du får en totalupplevelse på 360° i ett rum, en egenskap, en plats eller ett landskap.

Se även [Hantera visningsförinställningar](/help/assets/managing-viewer-presets.md).

![panoramic-image2](assets/panoramic-image2.png)

## Överföra resurser som ska användas med panoramabildsvisningsprogrammet {#uploading-assets-for-use-with-the-panoramic-image-viewer}

För att en överförd resurs ska kvalificeras som en sfärisk panoramabild som du tänker använda med panoramabildsvisningsprogrammet måste resursen ha antingen ett eller båda av följande:

* Proportionerna 2.
Du kan åsidosätta standardinställningen för proportioner på 2 i CRXDE Lite på följande sätt:
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* Taggad med nyckelorden `equirectangular`, eller `spherical`och `panorama`, eller `spherical` och `panoramic`. Se [Använda taggar](/help/sites-authoring/tags.md).

Både proportionerna och nyckelordskriterierna gäller för panoramaresurser för sidan med resursinformation och för `Panoramic Media` WCM-komponenten.

Information om hur du överför resurser som ska användas med panoramabildsvisningsprogrammet finns i [Överföra resurser](/help/assets/managing-assets-touch-ui.md#uploading-assets).

## Konfigurera Dynamic Media Classic (Scene7) {#configuring-dynamic-media-classic-scene}

För att visningsprogrammet för panoramabilder ska fungera på rätt sätt i AEM måste du synkronisera förinställningarna för visningsprogrammet för panoramabilder med hjälp av metadata som är specifika för Dynamic Media Classic (Scene7) och Dynamic Media Classic (Scene7) så att visningsförinställningarna uppdateras i JCR. Konfigurera Dynamic Media Classic (Scene7) på följande sätt:

1. [Logga in på din instans av Dynamic Media Classic (Scene7)](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) för varje företagskonto.

1. I det övre högra hörnet av sidan klickar du på **[!UICONTROL Konfigurera > Programinställningar > Publiceringsinställningar > Bildserver]**.
1. På sidan Image Server Publish (Publicera) väljer du **[!UICONTROL Image Serving (Bildserver]** ) i listrutan **[!UICONTROL Publish Context (Publiceringskontext]**) längst upp.

1. På samma Image Server Publish-sida hittar du rubriken **[!UICONTROL Request Attributes]**.
1. Under rubriken Begärandeattribut går du till **[!UICONTROL Svarsbildens storleksgräns]**. I de associerade fälten Bredd och Höjd ökar du den största tillåtna bildstorleken för panoramabilder.

   Dynamic Media Classic (Scene7) har en gräns på 25 000 000 pixlar. Den största tillåtna storleken för bilder med 2:1-proportioner är 7 000 x 3 500. För vanliga skärmar räcker det dock med 4 096 x 2 048 pixlar.

   >[!NOTE]
   >
   >Endast bilder som ligger inom den största tillåtna bildstorleken stöds. Begäran om bilder som är större än storleksgränsen resulterar i ett 403-svar.

1. Gör följande under rubriken Begärandeattribut:

   * Ställ in läget för begärandeautentisering på **[!UICONTROL Inaktiverad]**.
   * Ange att låsläget för begäran ska vara **[!UICONTROL inaktiverat]**.
   Dessa inställningar är nödvändiga för att du ska kunna använda `Panoramic Media` WCM-komponenten i AEM.

1. Klicka på **[!UICONTROL Spara]** längst ned på sidan Image Server Publish (Publicera på vänster sida).

1. Klicka på **[!UICONTROL Stäng]** i det nedre högra hörnet.

### Felsöka komponenten Panoramic Media WCM {#troubleshooting-the-panoramic-media-wcm-component}

Om du har släppt en bild i panoramamediakomponenten i WCM-filen och platshållaren för komponenten är komprimerad kanske du vill felsöka följande:

* Om du får ett otillåtet fel 403 kan det bero på att den begärda bildstorleken är för stor. Granska inställningarna för **[!UICONTROL Reply Image Size]** (Gräns för svarsbildstorlek) i [Configuring Dynamic Media Classic (Scene7)](/help/assets/panoramic-images.md#configuring%20dynamic%20media%20classic%20(scene7)).

* Om objektet har ett ogiltigt lås eller om ett parsningsfel visas på sidan, kontrollerar du Begär felsökningsläge och Begär låsläge för att se om de är inaktiverade.
* Om det uppstår ett fel på arbetsytan för en målad arbetsyta skapar du en sökväg till definitionsfilen för regeluppsättningen och kontrollerar CTN för de tidigare förfrågningarna om bildresursen.
* Om bildkvaliteten blir mycket låg efter en bildbegäran med en storlek över den gräns som stöds, kontrollerar du att **[!UICONTROL JPEG-kodningsattribut > Kvalitet]** inte är tom. En typisk inställning för fältet **[!UICONTROL Kvalitet]** är `95`. Inställningen finns på sidan Image Server Publish (Bildserverpublicering). Mer information om hur du kommer åt sidan finns i [Konfigurera Dynamic Media Classic (Scene7)](/help/assets/panoramic-images.md#configuring%20dynamic%20media%20classic%20(scene7)).

## Förhandsgranska panoramabilder {#previewing-panoramic-images}

Se [Förhandsgranska resurser](/help/assets/previewing-assets.md).

## Publicera panoramabilder {#publishing-panoramic-images}

Se [Publicera resurser](/help/assets/publishing-dynamicmedia-assets.md).
