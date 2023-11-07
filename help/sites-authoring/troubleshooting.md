---
title: Felsökning vid redigering i AEM
description: Vissa problem som kan uppstå när du använder AEM.
uuid: 99af51ea-8628-4811-83f2-ab3f88f0279e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: da0a5644-2e1d-4394-a6aa-11bb41406ba6
exl-id: 05586b17-35d4-496e-8f0e-293c755eb066
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 10%

---

# Felsöka AEM vid redigering{#troubleshooting-aem-when-authoring}

I följande avsnitt beskrivs några problem som du kan stöta på när du använder AEM, tillsammans med förslag på hur du felsöker dem.

>[!NOTE]
>
>När du får problem är det också värt att kontrollera listan med [Kända fel](/help/release-notes/release-notes.md) för din instans (release- och servicepaket).

>[!NOTE]
>
>Användare som har administratörsbehörighet och som vill felsöka problem med AEM kan använda felsökningsmetoderna som beskrivs i [AEM (för administratörer)](/help/sites-administering/troubleshoot.md). Om du inte har tillräcklig behörighet kan du kontakta systemadministratören om felsökning av AEM.

## Gammal sidversion på publicerad webbplats {#old-page-version-still-on-published-site}

* **Problem**:

   * Du har ändrat en sida och replikerat sidan till publiceringsplatsen, men *gammal* versionen av sidan visas fortfarande på publiceringswebbplatsen.

* **Orsak**:

   * Detta kan ha flera orsaker, oftast cachen (antingen din lokala webbläsare eller Dispatcher), men ibland kan det vara ett problem med replikeringskön.

* **Lösningar**:

   * Här finns olika möjligheter:
   * Bekräfta att sidan har replikerats korrekt. Kontrollera sidstatus och, om det behövs, status för replikeringskön.
   * Rensa cacheminnet i den lokala webbläsaren och få åtkomst till sidan igen.
   * Lägg till `?` till slutet av sidans URL. Till exempel:

      * `http://localhost:4502/sites.html/content?`
      * Detta begär sidan direkt från AEM och kringgår Dispatcher. Om du får den uppdaterade sidan är det en indikation på att du bör rensa Dispatcher-cachen.

   * Kontakta systemadministratören om det finns problem med replikeringsköerna.

## Komponentåtgärder visas inte i verktygsfältet {#component-actions-not-visible-on-toolbar}

* **Problem**:

   * Hela omfånget av tillämpliga komponentåtgärder visas inte när du redigerar en innehållssida i redigeringsmiljön.

* **Orsak**:

   * I sällsynta fall kan en tidigare åtgärd påverka verktygsfältet.

* **Lösning**:

   * Uppdatera sidan.
