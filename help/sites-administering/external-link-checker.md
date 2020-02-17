---
title: Kontrollen Extern länk
seo-title: Kontrollen Extern länk
description: Läs mer om Extern länkkontroll i AEM.
seo-description: Läs mer om Extern länkkontroll i AEM.
uuid: 09160594-e45f-4604-8b36-f14b148b9f63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d1ccd194-8549-4188-8932-7136be1e88a2
docset: aem65
translation-type: tm+mt
source-git-commit: 0a94bf49a7136c5831c42eb274d07517c12014ec

---


# Kontrollen Extern länk{#the-external-link-checker}

En extern länkkontroll tillhandahålls i AEM. Länkkontrollen:

* söker igenom alla innehållssidor
* genererar en lista med alla giltiga och ogiltiga länkar
* markerar ogiltiga länkar som brutna på plats på de enskilda innehållssidorna

## Validera externa länkar {#how-to-validate-external-links}

Så här använder du den externa länkkontrollen:

1. Välj **Navigering**, **Verktyg** och sedan **Platser**.
1. Välj **Extern länkkontroll**. En lista över alla externa länkar genereras.
1. Validera en specifik länk genom att markera den i listan och sedan klicka på **Kontrollera**:

   ![](assets/telc-01.png)

   Information visas:

   * **Status** för länken
   * **Webbadress**
   * **Referent**
   * tid sedan länken **senast kontrollerades** (validerad)
   * den **senaste statusen** returnerades

   * tid sedan länken var **senast tillgänglig**
   * tid sedan länken **senast användes**

1. På de enskilda innehållssidorna visas ogiltiga länkar som brutna:

   ![](assets/chlimage_1-143.png)