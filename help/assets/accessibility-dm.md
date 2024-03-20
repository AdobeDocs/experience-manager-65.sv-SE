---
title: Tillgänglighet i Dynamic Media
description: Läs mer om tillgänglighetsstöd i Dynamic Media och Dynamic Media Viewer.
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: User, Admin
exl-id: bbdb800c-b6f8-4506-b8ac-daf64edcd6c0
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---

# Tillgänglighet i [!DNL Dynamic Media] {#working-with-three-d-assets-dm}

[!DNL Dynamic Media] har stöd för tangentbordskontroll och hjälpmedelstekniker, som JAWS och NVDA-skärmläsare, i hela användargränssnittet.

## Stöd för tangentbordstillgänglighet i [!DNL Dynamic Media]

För [!DNL Dynamic Media] är ett plugin-program till [!DNL Adobe Experience Manager Assets], är det mesta av tangentbordskontrollen densamma som i [!DNL Experience Manager Assets]. Till exempel `Cancel` knapp in [!DNL Dynamic Media] har samma fokus som i [!DNL Experience Manager Assets]och reagerar på `Spacebar` tangent as in [!DNL Experience Manager Assets]. Se [Kortkommandon i resurser](/help/assets/accessibility.md#keyboard-shortcuts).

Tangentbord som stöds av enskilda element i användargränssnittet i [!DNL Dynamic Media] är tydliga och lätta att upptäcka. Tangentbordskontroll i [!DNL Dynamic Media] handlar om följande:

* Möjlighet att använda `Tab` och `Shift+Tab` tangenttryckningar för att navigera mellan interaktiva element på sidan.
Använda `Tab` flyttar indatafokus till nästa element i användargränssnittet i tabbordningen, med `Shift+Tab` återför indatafokus till det föregående elementet i användargränssnittet.
Fokusförflyttningen följer det naturliga elementet i användargränssnittet på skärmen och flyttas från vänster till höger och sedan uppifrån och ned. Om ett fält innehåller ett fel kan du dessutom trycka på `Tab` för att flytta fokus till den.
* Möjlighet att använda `Spacebar` och `Enter` om du vill aktivera standardelement i användargränssnittet, till exempel knappar och nedrullningsbara listor.
* Möjlighet att se fokus på tangentbordet på det aktiva elementet. Det element i användargränssnittet som har indatafokus får en visuell fokusindikation som en kantlinje som återges runt elementet i användargränssnittet.
* I Hotspot-redigeraren kan du använda vissa anpassade tangenttryckningar, till exempel piltangenter, för att interagera med komplexa element i användargränssnittet för att flytta hotspot-områden.
* I den interaktiva videoredigeraren kan du använda `Spacebar` om du vill markera en bild och lägga till den i ett segment. Dessutom kan du använda `Backspace` om du vill ta bort det markerade objektet från **[!UICONTROL Content]** -fliken. Tryck även på `Tab` används för att navigera mellan interaktiva element på sidan.
* I redigeraren för bildbeskärning/smart beskärning kan du göra följande:
   * Använd piltangenterna för att beskära bildrutestorleken, flytta bilden eller båda.
   * Den första `Tab` högdagrar hela bildramen. Du kan sedan använda piltangenterna på tangentbordet för att flytta ramen.
   * De kommande fyra `Tab` stopp är ramens fyra hörn. När fokus placeras på ett ramhörn markeras hörnet. Återigen kan du använda piltangenterna på tangentbordet för att flytta det fokuserade hörnet.
Se [Redigera smart beskärning eller smarta färgrutor för en enskild bild](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Teknikstöd för assistans inom [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] Element i användargränssnittet fungerar med hjälpmedelstekniker som skärmläsare. Den känner till exempel igen landmärken på en sida när du navigerar mellan landmärken med kortkommandon `D` eller områden som använder kortkommando `R`. Rubriken visas också med en berättarröst när du navigerar med rubrikens kortkommando `H`.

## Stöd för tangentbordstillgänglighet i [!DNL Dynamic Media] tittare {#keyboard-accessibility-for-dm-viewers}

Allt som finns på plats [!DNL Dynamic Media] visningsprogramkomponenterna har stöd för tangentbordstillgänglighet för dina kunder.

Se [Tangentbordstillgänglighet och -navigering](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) i referenshandboken för Dynamic Media Viewer.

## Teknikstöd för assistans inom [!DNL Dynamic Media] tittare {#assistive-technology-support-for-dm-viewers}

Alla [!DNL Dynamic Media] visningsprogramkomponenterna har stöd för ARIA-roller (Accessible Rich Internet Applications) och -attribut för att förbättra integrationen med hjälpmedelstekniker som skärmläsare.
Se **Stöd för hjälpmedel** Hjälpavsnitt om hur du anpassar visningsprogramavsnitt i referenshandboken för Dynamic Media Viewer. Se till exempel [Stöd för hjälpmedel](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) för Video Viewer, eller [Stöd för hjälpmedel](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) för interaktiv bildvisning.

## Stöd för undertexter i Dynamic Media {#closed-caption-support}

Dynamic Media stöder leverans av videor och adaptiva videouppsättningar med undertexter. Bildtexterna måste visas ovanpå videoinnehållet.

Se [Video i Dynamic Media - Lägg in undertexter i videon](/help/assets/video.md#adding-captions-to-video).

>[!MORELIKETHIS]
>
>* [Tillgänglighet för Adobe-lösningar](https://www.adobe.com/accessibility.html)
>* [Tillgänglighet i [!DNL Experience Manager Assets]](/help/assets/accessibility.md)
