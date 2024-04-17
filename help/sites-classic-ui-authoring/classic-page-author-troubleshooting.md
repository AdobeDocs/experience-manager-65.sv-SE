---
title: Felsöka AEM vid redigering
description: I följande avsnitt beskrivs några problem som du kan stöta på när du använder AEM, tillsammans med förslag på hur du felsöker dem.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: 27a6b012-576e-40bc-9b50-c310b3c56c9e
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

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

     `http://localhost:4502/sites.html/content?`

     Detta begär sidan direkt från AEM och kringgår Dispatcher. Om du får den uppdaterade sidan är det en indikation på att du bör rensa Dispatcher-cachen.

   * Kontakta systemadministratören om det finns problem med replikeringsköerna.

## Sidekick är inte synlig {#sidekick-not-visible}

* **Problem**:

   * Sidekick är inte synligt när du redigerar en innehållssida i redigeringsmiljön.

* **Orsak**:

   * I sällsynta fall kan du ha placerat sidhuvudet utanför det aktuella fönstret. Det innebär att du inte kan flytta den igen.

* **Lösning**:

   * Logga ut från den aktuella sessionen och logga in igen. Sidekick återgår till standardpositionen.

## Sök och ersätt - alla förekomster ersätts inte {#find-replace-not-all-instances-are-replaced}

* **Problem:**

   * När du använder **Sök och ersätt** kan det hända att inte alla instanser av `find` ersätts på en sida.

* **Orsak**:

   * Möjligheten att **Sök och ersätt** beror på hur innehållet sparas och om det går att söka efter det. En bloggtext sparas till exempel i `jcr:text` som inte är konfigurerad att genomsökas. Standardomfånget för sök- och ersättningsservern omfattar följande egenskaper:

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **Lösning**:

   * Dessa definitioner kan ändras med konfigurationen för **Dag CQ WCM Sök Ersätt server** med **Webbkonsol**; till exempel vid

     `http://localhost:4502/system/console/configMgr`
