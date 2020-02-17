---
title: Felsöka AEM vid redigering
seo-title: Felsöka AEM vid redigering
description: Problem som kan uppstå när du använder AEM
seo-description: Problem som kan uppstå när du använder AEM
uuid: 99af51ea-8628-4811-83f2-ab3f88f0279e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: da0a5644-2e1d-4394-a6aa-11bb41406ba6
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

