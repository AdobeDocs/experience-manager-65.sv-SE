---
title: Arbeta med dynamiska media
description: Lär dig hur du använder Dynamic Media för att leverera material för webben, mobiler och sociala medier.
uuid: 4dc0f436-d20e-4e8b-aeff-5515380fa44d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
discoiquuid: a8063d43-923a-42ac-9a16-0c7fadd8f73f
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Arbeta med dynamiska media {#working-with-dynamic-media}

[Dynamic Media](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html) hjälper er att leverera visuella marknadsförings- och marknadsföringsresurser on demand, som automatiskt skalas för konsumtion på webben, mobilsajter och sociala medier. Med hjälp av en uppsättning masterresurser genererar och levererar Dynamic Media flera varianter av multimediematerial i realtid via sitt globala, skalbara, prestandaoptimerade nätverk.

Dynamiska medier ger interaktiva tittarupplevelser som zoomning, 360-graders rotation och video. Dynamiska medier införlivar arbetsflödena i Adobe Experience Managers lösning för digital resurshantering (Assets) för att förenkla och effektivisera hanteringen av digitala kampanjer.

>[!NOTE]
>
>Det finns en communityartikel om [att arbeta med Adobe Experience Manager och Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html).

## Vad du kan göra med Dynamic Media {#what-you-can-do-with-dynamic-media}

Med Dynamic Media kan du hantera dina resurser innan du publicerar dem. Hur du arbetar med resurser i allmänhet beskrivs i detalj i [Arbeta med digitala resurser](managing-assets-touch-ui.md). Allmänna ämnen är bland annat att ladda upp, ladda ned, redigera och publicera material. visa och redigera egenskaper och söka efter resurser.

Funktioner som bara är dynamiska media inkluderar följande:

* [Carousel Banners](carousel-banners.md)
* [Bilduppsättningar](image-sets.md)
* [Interaktiva bilder](interactive-images.md)
* [Interaktiva videoklipp](interactive-videos.md)
* [Blandade medieuppsättningar](mixed-media-sets.md)
* [Panoramabilder](panoramic-images.md)

* [Snurra uppsättningar](spin-sets.md)
* [Video](video.md)
* [Leverera dynamiska medieresurser](delivering-dynamic-media-assets.md)
* [Hantera resurser](managing-assets.md)
* [Använda snabbvyer för att skapa anpassade popup-fönster](custom-pop-ups.md)

Se även [Konfigurera Dynamic Media](administering-dynamic-media.md).

>[!NOTE]
>
>Mer information om skillnaderna mellan att använda Dynamic Media och integrera Dynamic Media Classic med AEM finns i [Dynamic Media Classic-integrering jämfört med Dynamic Media](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media).

## Dynamiska media aktiverat jämfört med Dynamic Media inaktiverat {#dynamic-media-on-versus-dynamic-media-off}

Du kan se om Dynamic Media är aktiverat (aktiverat) av följande egenskaper:

* Dynamiska återgivningar är tillgängliga när du hämtar eller förhandsgranskar resurser.
* Bilduppsättningar, snurruppsättningar, blandade medieuppsättningar är tillgängliga.
* PTIFF-återgivningar skapas.

När du klickar på en bildresurs ser resursen annorlunda ut med Dynamic Media [aktiverat](config-dynamic.md#enabling-dynamic-media). Dynamic Media använder on-demand-visningsprogram för HTML5.

### Dynamiska renderingar {#dynamic-renditions}

Dynamiska renderingar som bild- och visningsförinställningar (under **[!UICONTROL Dynamisk]**) är tillgängliga när Dynamic Media är aktiverat.

![chlimage_1-358](assets/chlimage_1-358.png)

### Bilduppsättningar, snurruppsättningar, blandade medieuppsättningar {#image-sets-spins-sets-mixed-media-sets}

Bilduppsättningar, snurruppsättningar och blandade medieuppsättningar är tillgängliga om Dynamic Media är aktiverat.

![chlimage_1-359](assets/chlimage_1-359.png)

### PTIFF-återgivningar {#ptiff-renditions}

Dynamiska medieaktiverade resurser omfattar `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### Ändra resursvyer {#asset-views-change}

När Dynamic Media är aktiverat kan du zooma in och ut genom att klicka på `+` - och `-` -knapparna. Du kan också klicka/trycka för att zooma in i ett visst område. Med Återställ återgår du till den ursprungliga versionen och du kan göra bilden i helskärmsläge genom att klicka på de diagonala pilarna. Dynamic Media-aktiverade ser ut så här:

![chlimage_1-361](assets/chlimage_1-361.png)

När Dynamic Media är inaktiverat kan du zooma in och ut och återgå till den ursprungliga storleken:

![chlimage_1-362](assets/chlimage_1-362.png)
