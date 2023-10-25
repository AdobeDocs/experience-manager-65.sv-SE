---
title: Developing and Page Diff
description: Lär dig hur du utvecklar och använder sidskillnader i Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: b07134b2-074a-4d52-8d0c-7e7abe51fc3a
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Developing and Page Diff{#developing-and-page-diff}

## Översikt över funktioner {#feature-overview}

Att skapa innehåll är en repetitiv process. Effektiv redigering kräver att man kan se vad som har ändrats från en iteration till en annan. Om du visar den ena sidversionen och den andra är ineffektiv och felbenägen kan uppstå. En författare vill kunna jämföra den aktuella sidan med en tidigare version sida vid sida med skillnaderna markerade.

Med sidskillnaden kan användaren jämföra den aktuella sidan med startsidor, tidigare versioner osv. Mer information om den här användarfunktionen finns i [Sidskillnader](/help/sites-authoring/page-diff.md).

## Operationsinformation {#operation-details}

När du jämför versioner av en sida återskapas den tidigare versionen som användaren vill jämföra av AEM i bakgrunden för att underlätta skillnaderna. Detta krävs för att innehållet ska kunna återges [för jämförelse sida vid sida](/help/sites-developing/pagediff.md#operation-details).

Denna rekreationsåtgärd görs internt av AEM och är transparent för användaren och kräver ingen åtgärd. En administratör som till exempel visar databasen i CRXDE Lite kan se dessa återskapade versioner i innehållsstrukturen.

När innehållet jämförs återskapas hela trädet fram till sidan som ska jämföras på följande plats:

`/tmp/versionhistory/`

En rensningsåtgärd körs automatiskt för att rensa upp det tillfälliga innehållet.

## Behörigheter {#permissions}

I det klassiska användargränssnittet behövde man tidigare tänka på hur man skulle underlätta AEM (t.ex. använda `cq:text` tagg lib, eller anpassad integrering av `DiffService` OSGi-tjänst in i komponenter). Det här behövs inte längre för den nya diff-funktionen, eftersom skillnaden inträffar på klientsidan via DOM-jämförelse.

Det finns dock vissa begränsningar som måste beaktas av utvecklaren.

* Den här funktionen använder CSS-klasser som inte har något namn som AEM Produkten. Om andra anpassade CSS-klasser eller CSS-klasser från tredje part med samma namn inkluderas på sidan kan visningen av skillnaderna påverkas.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Eftersom differensen är klientsidan och körs vid sidinläsning, kommer eventuella justeringar av DOM efter att klientsidans diff-tjänst har körts inte att beaktas. Detta kan påverka

   * Komponenter som använder AJAX för att inkludera innehåll
   * Enkelsidiga program
   * JavaScript-baserade komponenter som ändrar DOM när användaren interagerar.

>[!NOTE]
>
>Det går bara att jämföra sidskillnader för komponenter som har giltiga cq:editConfig-noder.
