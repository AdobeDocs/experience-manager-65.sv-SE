---
title: Redigeringsövningar
seo-title: Redigeringsövningar
description: 'När du har skapat en startsida för sidan (eller en uppsättning sidor) kan du redigera innehållet i startkopian av sidorna. '
seo-description: 'När du har skapat en startsida för sidan (eller en uppsättning sidor) kan du redigera innehållet i startkopian av sidorna. '
uuid: 1f2c2e53-73a3-4bd7-b2c7-425491bc0118
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 30aa3177-bcf4-4260-8f64-e73bc907942a
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
translation-type: tm+mt
source-git-commit: 2d7492cdee9f7f730dfa6ad2ffae396b3a737b15

---


# Redigeringsövningar{#editing-launches}

## Redigera startsidor {#editing-launch-pages}

När en startsida har skapats för en sida (eller en uppsättning sidor) kan du redigera innehållet i startkopian av sidorna.

1. Öppna [Starta från referenser (Sites-konsolen)](/help/sites-authoring/launches.md#launches-in-references-sites-console) för att visa tillgängliga åtgärder.
1. Välj **Gå till sidan** för att öppna sidan för redigering.

### Redigera startsidor som är beroende av en Live-kopia {#editing-launch-pages-subject-to-a-live-copy}

Om lanseringen baseras på en [live-kopia](/help/sites-administering/msm.md) kommer du att:

* se låssymboler (små hänglås) när du redigerar en komponent (innehåll och/eller egenskaper).
* se fliken **Live-kopia** i **Sidegenskaper**

En livecopy används för att synkronisera innehåll *från* källgrenen *till* startgrenen (för att hålla igång programmet uppdaterat med ändringarna i källan).

Du kan göra ändringar på samma sätt som du kan redigera en vanlig Live-kopia; till exempel:

* Om du klickar på ett stängt hänglås bryts synkroniseringen och du kan göra nya uppdateringar av innehållet när du startar programmet. När du har låst upp (öppet hänglås) skrivs inte ändringarna över av ändringar som gjorts på samma plats i källgrenen.
* **Skjut upp** (och **återuppta**) arv för en viss sida.

Mer information finns i [Ändra Live Copy-innehåll](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) .

## Jämföra en startsida med dess källsida {#comparing-a-launch-page-to-its-source-page}

Om du vill spåra de ändringar du har gjort kan du visa startsidan i **Referenser** och jämföra startsidan med dess källsida:

1. Gå **till startsidan i konsolen** Platser [och markera den](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources).
1. Öppna panelen **[Referenser](/help/sites-authoring/basic-handling.md#references)**och välj **Starta**.
1. Välj en specifik start och sedan **Jämför med källa**:

   ![screen-shot_2019-03-05at121952](assets/screen-shot_2019-03-05at121952.png)

1. De två sidorna (start och källa) öppnas sida vid sida.

   Mer information om hur du använder den här funktionen finns i [Sidskillnad](/help/sites-authoring/page-diff.md).

## Ändra använda källsidor {#changing-the-source-pages-used}

Du kan när som helst lägga till eller ta bort sidor till/från intervallet med källsidor för en start:

1. Öppna och välj programstart från:

   * konsolen [](/help/sites-authoring/launches.md#the-launches-console)Launches:

      * Välj **Redigera**.
   * [Referenser (platskonsolen)](/help/sites-authoring/launches.md#launches-in-references-sites-console) för att visa tillgängliga åtgärder:

      * Välj **Redigera start**.
   Källsidorna visas.

1. Gör önskade ändringar och bekräfta sedan med **Spara**.

   >[!NOTE]
   >
   >Om du vill lägga till sidor i en programstart måste de ligga under en gemensam språkrot. dvs. inom en enda plats.

## Redigera en startkonfiguration {#editing-a-launch-configuration}

Du kan när som helst redigera egenskaperna för en start:

1. Öppna och välj programstart från:

   * konsolen [](/help/sites-authoring/launches.md#the-launches-console)Launches:

      * Välj **Egenskaper**.
   * [Referenser (platskonsolen)](/help/sites-authoring/launches.md#launches-in-references-sites-console) för att visa tillgängliga åtgärder:

      * Välj **Redigera egenskaper**.
   Detaljerna visas.

1. Gör önskade ändringar och bekräfta sedan med **Spara**.

   Se [Startprogram - Evenemangsordningen](/help/sites-authoring/launches.md#launches-the-order-of-events) för information om syftet med och interaktionen mellan fälten **Startdatum** och **Produktionsklar** .

## Identifiera startstatus för en sida {#discovering-the-launch-status-of-a-page}

Statusen visas när du väljer en viss start på fliken Inställningar (se [Starta i Referenser (platskonsolen)](/help/sites-authoring/launches.md#launches-in-references-sites-console)).

![screen-shot_2019-03-05at121901](assets/screen-shot_2019-03-05at121901.png)
