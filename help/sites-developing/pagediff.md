---
title: Developing and Page Diff
seo-title: Developing and Page Diff
description: 'null'
seo-description: 'null'
uuid: 06f27bc2-f42a-4176-ab94-255e721c6933
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6612f89d-c518-4e5a-8df1-6487cc330a9a
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# Developing and Page Diff{#developing-and-page-diff}

## Funktionsöversikt {#feature-overview}

Att skapa innehåll är en repetitiv process. Effektiv redigering kräver att man kan se vad som har ändrats från en iteration till en annan. Om du visar den ena sidversionen och den andra är ineffektiv och felbenägen kan uppstå. En författare vill kunna jämföra den aktuella sidan med en tidigare version sida vid sida med skillnaderna markerade.

Med sidskillnader kan en användare jämföra den aktuella sidan med startsidor, tidigare versioner osv. Mer information om den här användarfunktionen finns i [Sidskillnad](/help/sites-authoring/page-diff.md).

## Operationsinformation {#operation-details}

När man jämför versioner av en sida skapas den tidigare versionen som användaren vill jämföra av AEM i bakgrunden för att underlätta skillnaderna. Detta behövs för att kunna återge innehållet [för jämförelse](/help/sites-developing/pagediff.md#operation-details)sida vid sida.

Denna rekreationsåtgärd utförs internt av AEM och är transparent för användaren och kräver ingen åtgärd. En administratör som visar databasen, till exempel i CRX DE Lite, skulle dock se dessa återskapade versioner i innehållsstrukturen.

När innehållet jämförs återskapas hela trädet fram till sidan som ska jämföras på följande plats:

`/tmp/versionhistory/`

En rensningsåtgärd körs automatiskt för att rensa upp det tillfälliga innehållet.

## Permissions {#permissions}

I det klassiska användargränssnittet behövde man tidigare tänka på hur man skulle kunna underlätta AEM-differentiering (t.ex. genom att använda `cq:text` tag lib eller integrera `DiffService` OSGi-tjänsten i komponenter). Det här behövs inte längre för den nya diff-funktionen, eftersom skillnaden inträffar på klientsidan via DOM-jämförelse.

Det finns dock ett antal begränsningar som måste beaktas av utvecklaren.

* Den här funktionen använder CSS-klasser som inte har namnmellanrum med AEM-produkten. Om andra anpassade CSS-klasser eller CSS-klasser från tredje part med samma namn inkluderas på sidan kan visningen av skillnaderna påverkas.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Eftersom differensen är klientsidan och körs vid sidinläsning, kommer eventuella justeringar av DOM efter att klientsidans diff-tjänst har körts inte att beaktas. Detta kan påverka

   * Komponenter som använder AJAX för att inkludera innehåll
   * Enkelsidiga program
   * Javascript-baserade komponenter som manipulerar DOM när användaren interagerar.
