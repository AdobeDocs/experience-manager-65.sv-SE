---
title: Arbeta med Dynamic Media
description: Lär dig hur du använder Dynamic Media för att leverera mediefiler för webben, mobiler och sociala medier.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
role: User, Admin
exl-id: f8a80b22-b1a6-475f-b3f1-b2f47822f21d
feature: Collaboration,Asset Management
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 2%

---

# Arbeta med Dynamic Media {#working-with-dynamic-media}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) hjälper till att leverera visuella marknadsförings- och marknadsföringsresurser on demand, som automatiskt skalas för konsumtion på webben, mobiler och sociala medier. Med en uppsättning primära källresurser genererar och levererar Dynamic Media flera varianter av multimedieinnehåll i realtid via sitt globala, skalbara, prestandaoptimerade nätverk.

Dynamic Media visar interaktivt material, som zoomning, 360-graders rotation och video. Dynamic Media införlivar smidigt arbetsflödena i Adobe Experience Manager Digital Asset Management (Assets) för att förenkla och effektivisera hanteringen av digitala kampanjer.

<!-- >ARTICLE IS MISSING. GIVES 404 [!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## Vad du kan göra med Dynamic Media {#what-you-can-do-with-dynamic-media}

Med Dynamic Media kan du hantera dina resurser innan du publicerar dem. Hur du arbetar med resurser i allmänhet beskrivs i detalj i [Arbeta med digitala resurser](manage-assets.md). Allmänna ämnen är bland annat att ladda upp, ladda ned, redigera och publicera resurser, visa och redigera egenskaper och söka efter resurser.

Dynamic Media har följande funktioner:

* [Carousel Banners](carousel-banners.md)
* [Bilduppsättningar](image-sets.md)
* [Interaktiva bilder](interactive-images.md)
* [Interaktiva videoklipp](interactive-videos.md)
* [Blandade medieuppsättningar](mixed-media-sets.md)
* [Panorambilder](panoramic-images.md)

* [Snurra uppsättningar](spin-sets.md)
* [Video](video.md)
* [Leverera Dynamic Media-material](delivering-dynamic-media-assets.md)
* [Hantera resurser](managing-assets.md)
* [Skapa anpassade popup-fönster med snabbvyn](custom-pop-ups.md)

Se även [Konfigurera Dynamic Media](administering-dynamic-media.md).

>[!NOTE]
>
>Mer information om skillnaderna mellan att använda Dynamic Media och integrera Dynamic Media Classic med Adobe Experience Manager finns i [Dynamic Media Classic-integrering jämfört med Dynamic Media](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media).

## Dynamic Media-aktiverat jämfört med Dynamic Media inaktiverat {#dynamic-media-on-versus-dynamic-media-off}

Du kan se om Dynamic Media är aktiverat (aktiverat) enligt följande:

* Dynamiska återgivningar är tillgängliga när du hämtar eller förhandsgranskar resurser.
* Bilduppsättningar, snurruppsättningar, blandade medieuppsättningar är tillgängliga.
* PTIFF-återgivningar skapas.

När du väljer en bildresurs ser resursen annorlunda ut än Dynamic Media [enabled](config-dynamic.md#enabling-dynamic-media). Dynamic Media använder on-demand-visningsprogrammen för HTML 5.

### Dynamiska renderingar {#dynamic-renditions}

Dynamiska återgivningar som bild- och visningsförinställningar (under **[!UICONTROL Dynamic]**) är tillgängliga när Dynamic Media är aktiverat.

![chlimage_1-358](assets/chlimage_1-358.png)

### Bilduppsättningar, snurruppsättningar, blandade medieuppsättningar {#image-sets-spins-sets-mixed-media-sets}

Uppsättningar med bilder, snurra och blandade medieuppsättningar är tillgängliga om Dynamic Media är aktiverat.

![chlimage_1-359](assets/chlimage_1-359.png)

### PTIFF-återgivningar {#ptiff-renditions}

Dynamic Media-aktiverade resurser innehåller `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### Ändra resursvyer {#asset-views-change}

När Dynamic Media är aktiverat kan du zooma in och ut genom att klicka på knapparna `+` och `-`. Du kan också klicka för att zooma in i ett visst område. Med Återställ återgår du till den ursprungliga versionen och du kan göra bilden i helskärmsläge genom att klicka på de diagonala pilarna. Dynamic Media-aktiverad ser ut så här:

![chlimage_1-361](assets/chlimage_1-361.png)

Med Dynamic Media inaktiverat kan du zooma in och ut och återställa till den ursprungliga storleken:

![chlimage_1-362](assets/chlimage_1-362.png)
