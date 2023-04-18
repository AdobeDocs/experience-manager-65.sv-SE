---
title: Felsöka AEM vid redigering
description: I följande avsnitt beskrivs några problem som du kan stöta på när du använder AEM, tillsammans med förslag på hur du felsöker dem.
uuid: eb95e5ba-1eed-4ffb-80c1-9b8468820c22
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9b492b17-9029-46ae-9dc0-bb21e6b484df
exl-id: 27a6b012-576e-40bc-9b50-c310b3c56c9e
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 7%

---

# Felsöka AEM vid redigering{#troubleshooting-aem-when-authoring}

I följande avsnitt beskrivs några problem som du kan stöta på när du använder AEM, tillsammans med förslag på hur du felsöker dem.

>[!NOTE]
>
>När du får problem är det också värt att kontrollera listan med [Kända fel](/help/release-notes/release-notes.md) för din instans (release- och servicepaket).

>[!NOTE]
>
>Användare som har administratörsbehörighet och som vill felsöka problem med AEM kan använda felsökningsmetoderna som beskrivs i [AEM (för administratörer)](/help/sites-administering/troubleshoot.md). Om du inte har tillräcklig behörighet kontaktar du systemadministratören om felsökning AEM.

## Gammal sidversion finns fortfarande på publicerad webbplats {#old-page-version-still-on-published-site}

* **Problem**:

   * Du har gjort ändringar på en sida och replikerat sidan till publiceringsplatsen, men *gammal* versionen av sidan visas fortfarande på publiceringswebbplatsen.

* **Orsak**:

   * Detta kan ha flera orsaker, oftast cachen (antingen din lokala webbläsare eller Dispatcher), men ibland kan det vara ett problem med replikeringskön.

* **Lösningar**:

   * Här finns olika möjligheter:
   * Bekräfta att sidan har replikerats korrekt. Kontrollera sidstatus och, om det behövs, status för replikeringskön.
   * Rensa cacheminnet i den lokala webbläsaren och öppna sidan igen.
   * Lägg till `?` till slutet av sid-URL:en. Till exempel:

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

   * När du använder **Sök och ersätt** kan det hända att inte alla instanser av `find` termen ersätts på en sida.

* **Orsak**:

   * Möjligheten att **Sök och ersätt** beror på hur innehållet sparas och om det går att söka efter det. En bloggtext sparas till exempel i `jcr:text` som inte är konfigurerad att genomsökas. Standardomfånget för sök- och ersättningsservern omfattar följande egenskaper:

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **Lösning**:

   * Dessa definitioner kan ändras med konfigurationen för **Dag CQ WCM Sök Ersätt server** med **Webbkonsol**; till exempel

      `http://localhost:4502/system/console/configMgr`
