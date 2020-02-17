---
title: Komponentkonsol
seo-title: Komponentkonsol
description: 'null'
seo-description: 'null'
uuid: a4e34d81-7875-4e26-8b48-4473e2905c37
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: b657f95d-7be3-4409-a31b-d47fb2bfa550
docset: aem65
translation-type: tm+mt
source-git-commit: 4dc4a518c212555b7833ac27de02087a403d3517

---


# Komponentkonsol{#components-console}

Med komponentkonsolen kan du bläddra igenom alla komponenter som definierats för instansen och visa nyckelinformation för varje komponent.

Den finns under **Verktyg ->** Allmänt -> **** Komponenter ****. I konsolen är kort- och listvyn tillgängliga. Eftersom det inte finns någon trädstruktur för komponenter är kolumnvyn inte tillgänglig.

![screen-shot_2019-03-05at113145](assets/screen-shot_2019-03-05at113145.png)

>[!NOTE]
>
>Komponentkonsolen visar alla komponenter i systemet. I [komponentwebbläsaren](/help/sites-authoring/author-environment-tools.md#components-browser) visas komponenter som är tillgängliga för författare och alla komponentgrupper som börjar med en punkt ( `.`) döljs.

## Sök {#searching}

Med ikonen Endast **** innehåll (överst till vänster) kan du öppna **sökpanelen** och söka efter och/eller filtrera komponenterna:

![screen-shot_2019-03-05at113251](assets/screen-shot_2019-03-05at113251.png)

### Komponentinformation {#component-details}

Om du vill visa information om en viss komponent trycker/klickar du på den nödvändiga resursen. Tre flikar innehåller:

* **Egenskaper**

   ![screen_shot_2018-03-27at165847](assets/screen_shot_2018-03-27at165847.png)

   På fliken Egenskaper kan du:

   * Visa komponentens allmänna egenskaper.
   * Visa hur [ikonen eller förkortningen har definierats](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) för komponenten.

      * Om du klickar på ikonens källa kommer du till den komponenten.
   * Visa komponentens **resurstyp** och **resurssupertyp** (om den är definierad).

      * Om du klickar på Resurssupertypen kommer du till den komponenten.
   >[!NOTE]
   >
   >Eftersom `/apps` inte kan redigeras under körning är komponentkonsolen skrivskyddad.

* **Profiler**

   ![chlimage_1-169](assets/chlimage_1-169.png)

* **Live-användning**

   ![chlimage_1-170](assets/chlimage_1-170.png)

   >[!CAUTION]
   >
   >På grund av den typ av information som samlas in för den här vyn kan det ta en stund att sortera/visa informationen.

* **Dokumentation**

   Om utvecklaren har tillhandahållit [dokumentation för komponenten](/help/sites-developing/developing-components.md#documenting-your-component)visas den på fliken **Dokumentation** . Om det inte finns någon tillgänglig dokumentation visas inte fliken **Dokumentation** .

   ![chlimage_1-171](assets/chlimage_1-171.png)

