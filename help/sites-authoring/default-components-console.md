---
title: Komponentkonsol
seo-title: Components Console
description: Komponentkonsol
seo-description: null
uuid: a4e34d81-7875-4e26-8b48-4473e2905c37
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: b657f95d-7be3-4409-a31b-d47fb2bfa550
docset: aem65
exl-id: d79107b9-dfa4-4e80-870e-0b7ea72f0bc7
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 22%

---

# Komponentkonsol{#components-console}

Med komponentkonsolen kan du bläddra igenom alla komponenter som definierats för instansen och visa nyckelinformation för varje komponent.

Den finns under **Verktyg ->** **Allmänt ->** **Komponenter**. I konsolen finns kortvyn och listvyn. Eftersom det inte finns någon trädstruktur för komponenter är kolumnvyn inte tillgänglig.

![screen-shot_2019-03-05at113145](assets/screen-shot_2019-03-05at113145.png)

>[!NOTE]
>
>Komponentkonsolen visar alla komponenter i systemet. The [Komponentbläddraren](/help/sites-authoring/author-environment-tools.md#components-browser) visar komponenter som är tillgängliga för författare och döljer komponentgrupper som börjar med en punkt ( `.`).

## Sökning {#searching}

Med ikonen **Endast innehåll** (överst till vänster) kan du öppna **sökpanelen** och söka efter och/eller filtrera komponenterna:

![screen-shot_2019-03-05at113251](assets/screen-shot_2019-03-05at113251.png)

### Komponentinformation {#component-details}

Om du vill visa information om en viss komponent trycker/klickar du på den nödvändiga resursen. Tre flikar innehåller:

* **Egenskaper**

  ![screen_shot_2018-03-27at165847](assets/screen_shot_2018-03-27at165847.png)

  På fliken Egenskaper kan du:

   * Visa komponentens allmänna egenskaper.
   * Visa hur [ikon eller förkortning har definierats](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) för komponenten.

      * Om du klickar på ikonens källa kommer du till den komponenten.

   * Visa **Resurstyp** och **Resurssupertyp** (om det är definierat) för komponenten.

      * Om du klickar på Resurssupertypen kommer du till den komponenten.

  >[!NOTE]
  >
  >För `/apps` går inte att redigera vid körning, komponentkonsolen är skrivskyddad.

* **Profiler**

  ![Profiler](assets/chlimage_1-169.png)

* **Live-användning**

  ![Live-användning](assets/chlimage_1-170.png)

  >[!CAUTION]
  >
  >På grund av den typ av information som samlas in för den här vyn kan det ta en stund att sortera/visa informationen.

* **Dokumentation**

  Om utvecklaren har tillhandahållit [dokumentation för komponenten](/help/sites-developing/developing-components.md#documenting-your-component)visas den på **Dokumentation** -fliken. Om det inte finns någon tillgänglig dokumentation **Dokumentation** kommer inte att visas.

  ![Dokumentation](assets/chlimage_1-171.png)
