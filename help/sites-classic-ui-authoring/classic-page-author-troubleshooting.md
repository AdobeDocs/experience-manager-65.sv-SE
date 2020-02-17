---
title: Felsöka AEM vid redigering
seo-title: Felsöka AEM vid redigering
description: I följande avsnitt beskrivs några problem som du kan stöta på när du använder AEM, tillsammans med förslag på hur du felsöker dem.
seo-description: I följande avsnitt beskrivs några problem som du kan stöta på när du använder AEM, tillsammans med förslag på hur du felsöker dem.
uuid: eb95e5ba-1eed-4ffb-80c1-9b8468820c22
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9b492b17-9029-46ae-9dc0-bb21e6b484df
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Felsöka AEM vid redigering{#troubleshooting-aem-when-authoring}

I följande avsnitt beskrivs några problem som du kan stöta på när du använder AEM, tillsammans med förslag på hur du felsöker dem.

>[!NOTE]
>
>När du får problem är det också värt att kontrollera listan med [kända fel](/help/release-notes/known-issues.md) för din instans (release- och servicepaket).

>[!NOTE]
>
>Användare som har administratörsbehörighet och som vill felsöka problem med AEM kan använda de felsökningsmetoder som beskrivs i [Felsökning för AEM (för administratörer)](/help/sites-administering/troubleshoot.md). Om du inte har tillräcklig behörighet kontaktar du systemadministratören för felsökning av AEM.

## Gammal sidversion finns fortfarande på publicerad webbplats {#old-page-version-still-on-published-site}

* **Problem**:

   * Du har ändrat en sida och replikerat sidan till publiceringsplatsen, men den *gamla* versionen av sidan visas fortfarande på publiceringsplatsen.

* **Orsak**:

   * Detta kan ha flera orsaker, oftast cachen (antingen din lokala webbläsare eller Dispatcher), men ibland kan det vara ett problem med replikeringskön.

* **Lösningar**:

   * Här finns olika möjligheter:
   * Bekräfta att sidan har replikerats korrekt. Kontrollera sidstatus och, om det behövs, status för replikeringskön.
   * Rensa cacheminnet i den lokala webbläsaren och öppna sidan igen.
   * Lägg till `?` i slutet av sid-URL:en. Exempel:

      `http://localhost:4502/sites.html/content?`

      Detta begär sidan direkt från AEM och kringgår Dispatcher. Om du får den uppdaterade sidan är det en indikation på att du bör rensa Dispatcher-cachen.

   * Kontakta systemadministratören om det finns problem med replikeringsköerna.

## Sidekick inte synlig {#sidekick-not-visible}

* **Problem**:

   * Sidsparken syns inte när du redigerar en innehållssida i författarmiljön.

* **Orsak**:

   * I sällsynta fall kan du ha placerat sidhuvudet utanför det aktuella fönstret. Det innebär att du inte kan flytta den igen.

* **Lösning**:

   * Logga ut från den aktuella sessionen och logga in igen. Sparken återgår till standardpositionen.

## Sök och ersätt - alla förekomster ersätts inte {#find-replace-not-all-instances-are-replaced}

* **Problem:**

   * När du använder alternativet **Sök och ersätt** kan det hända att inte alla förekomster av `find` termen ersätts på en sida.

* **Orsak**:

   * Funktionen **Sök och ersätt** beror på hur innehållet sparas och om det går att söka efter det. En bloggtext sparas till exempel i en `jcr:text` egenskap som inte är konfigurerad att genomsökas. Standardomfånget för sök- och ersättningsservern omfattar följande egenskaper:

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **Lösning**:

   * Dessa definitioner kan ändras med konfigurationen för WCM Find Replace Server för **Dag CQ** med hjälp av **webbkonsolen**. till exempel

      `http://localhost:4502/system/console/configMgr`

