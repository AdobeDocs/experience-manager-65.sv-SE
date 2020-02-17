---
title: Förhandsgranska sidor med ContextHub-data
seo-title: Förhandsgranska sidor med ContextHub-data
description: Verktygsfältet ContextHub visar data från ContextHub-butiker och gör att du kan ändra lagringsdata. Det är användbart för förhandsgranskning av innehåll
seo-description: Verktygsfältet ContextHub visar data från ContextHub-butiker och gör att du kan ändra lagringsdata. Det är användbart för förhandsgranskning av innehåll
uuid: 0150555a-0a92-4692-a706-bbe59fd34d6a
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: f281ef8c-0831-470c-acb7-189f20452a50
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Förhandsgranska sidor med ContextHub-data{#previewing-pages-using-contexthub-data}

Verktygsfältet [ContextHub](/help/sites-developing/contexthub.md) visar data från ContextHub-arkiv och gör att du kan ändra lagringsdata. Verktygsfältet ContextHub är användbart när du vill förhandsgranska innehåll som bestäms av data i ett ContextHub-lager.

Verktygsfältet består av en serie användargränssnittslägen som innehåller en eller flera användargränssnittsmoduler.

* Gränssnittslägen är ikoner som visas till vänster i verktygsfältet. När du klickar på eller trycker på en ikon visas de gränssnittsmoduler som finns i verktygsfältet.
* Gränssnittsmoduler visar data från en eller flera ContextHub-butiker. Vissa gränssnittsmoduler gör det även möjligt för dig att ändra lagrade data.

ContextHub installerar flera gränssnittslägen och gränssnittsmoduler. Din administratör kan ha [konfigurerat ContextHub](/help/sites-administering/contexthub-config.md) för att visa olika.

![screen_shot_2018-03-23at093446](assets/screen_shot_2018-03-23at093446.png)

## Visa verktygsfältet ContextHub {#revealing-the-contexthub-toolbar}

Verktygsfältet ContextHub är tillgängligt i förhandsgranskningsläget. Verktygsfältet är bara tillgängligt på författarinstanser och endast när administratören har aktiverat det.

![screen_shot_2018-03-23at093730](assets/screen_shot_2018-03-23at093730.png)

1. Öppna sidan för redigering, klicka eller tryck på Förhandsgranska i verktygsfältet.

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Visa verktygsfältet genom att klicka på eller trycka på ikonen ContextHub.

   ![](do-not-localize/screen_shot_2018-03-23at093621.png)

## Funktioner i gränssnittsmodul {#ui-module-features}

Varje gränssnittsmodul innehåller olika uppsättningar funktioner, men följande typer av funktioner är vanliga. Eftersom gränssnittsmodulerna kan utökas kan utvecklaren implementera andra funktioner efter behov.

### Innehåll i verktygsfält {#toolbar-content}

Gränssnittsmoduler kan visa data från en eller flera ContextHub-butiker i verktygsfältet. I gränssnittsmoduler används en ikon och en titel för att identifiera sig själva.

![screen_shot_2018-03-23at093936](assets/screen_shot_2018-03-23at093936.png)

### Popup-innehåll {#popup-content}

I vissa gränssnittsmoduler visas ett popup-fönster som är övertryckt när användaren klickar eller trycker på. Vanligtvis innehåller popup-fönstret mer information än vad som visas i verktygsfältet.

![screen_shot_2018-03-23at094003](assets/screen_shot_2018-03-23at094003.png)

### Popup-formulär {#popup-forms}

Popup-överlägget för en modul kan innehålla formulärelement som gör att du kan ändra data i ContextHub-arkivet. Om sidinnehållet avgörs av lagringsdata kan du använda formuläret och observera ändringar i sidinnehållet.

### Helskärmsläge {#fullscreen-mode}

Popup-övertäckningar kan innehålla en ikon som du klickar på eller trycker på för att expandera popup-innehållet så att det täcker hela webbläsarfönstret eller skärmen.

![](do-not-localize/chlimage_1-18.png)

