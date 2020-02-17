---
title: Anteckningar vid redigering av en sida
seo-title: Anteckningar vid redigering av en sida
description: Många komponenter som är direkt relaterade till innehåll gör att du kan lägga till en anteckning
seo-description: Många komponenter som är direkt relaterade till innehåll gör att du kan lägga till en anteckning
uuid: 157be55c-8ab8-472e-be32-0dcc02bfa41d
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: aa89326a-ad33-4b0b-8d09-c68c5a5c790a
translation-type: tm+mt
source-git-commit: 55a4c7eee6f1305fe84a22bc9b23cd77d73d414a

---


# Anteckningar vid redigering av en sida{#annotations-when-editing-a-page}

Om du lägger till innehåll på webbplatsens sidor kan det ofta bli aktuellt med diskussioner innan det faktiskt publiceras. För att underlätta detta kan du lägga till en anteckning i många komponenter som är direkt relaterade till innehåll (till skillnad från till exempel layout).

En anteckning placerar en färgmarkör/anteckning på sidan. Med anteckningen kan du (eller andra användare) lämna kommentarer och/eller frågor till andra författare/granskare.

>[!NOTE]
>
>Definitionen av en enskild komponenttyp avgör om det är möjligt att lägga till en anteckning (eller inte) i instanser av den komponenten.

>[!NOTE]
>
>Anteckningar som skapas i det klassiska användargränssnittet visas i det pekaktiverade användargränssnittet. Skisser är dock gränssnittsspecifika och visas bara i det användargränssnitt där de skapades.

>[!CAUTION]
>
>Om du tar bort en resurs (t.ex. ett stycke) tas alla anteckningar och skisser som är kopplade till den resursen bort, oavsett deras position på sidan som helhet.

>[!NOTE]
>
>Beroende på dina behov kan du även utveckla ett arbetsflöde för att skicka meddelanden när anteckningar läggs till, uppdateras eller tas bort.

## Anteckningar {#annotations}

Ett särskilt [läge](/help/sites-authoring/author-environment-tools.md#page-modes) används för att skapa och visa anteckningar.

>[!NOTE]
>
>Glöm inte att det också finns [kommentarer](/help/sites-authoring/basic-handling.md#timeline) för att ge feedback på en sida.

>[!NOTE]
>
>Du kan anteckna en mängd olika resurser:
>
>* [Anteckna resurser](/help/assets/managing-assets-touch-ui.md#annotating)
>* [Kommentera videomaterial](/help/assets/managing-video-assets.md#annotate-video-assets)
>



### Kommentera en komponent {#annotating-a-component}

I anteckningsläget kan du skapa, redigera, flytta eller ta bort anteckningar i ditt innehåll:

1. Du kan öppna anteckningsläget med ikonen i verktygsfältet (längst upp till höger) när du redigerar en sida:

   ![](do-not-localize/screen_shot_2018-03-22at110414.png)

   Nu kan du visa alla befintliga anteckningar.

   >[!NOTE]
   >
   >Om du vill avsluta anteckningsläget trycker/klickar du på ikonen Anteckning (x-symbolen) till höger om det övre verktygsfältet.

1. Klicka/tryck på ikonen Lägg till anteckning (plus symbol till vänster i verktygsfältet) för att börja lägga till anteckningar.

   >[!NOTE]
   >
   >Om du vill sluta lägga till anteckningar (och återgå till att visa) trycker/klickar du på ikonen Avbryt (x-symbolen i en vit cirkel) till vänster om det övre verktygsfältet.

1. Klicka/tryck på den nödvändiga komponenten (komponenter som kan kommenteras markeras med en blå ram) för att lägga till anteckningen och öppna dialogrutan:

   ![screen_shot_2018-03-22at110606](assets/screen_shot_2018-03-22at110606.png)

   Här kan du använda rätt fält och/eller ikon för att:

   * Ange anteckningstexten.
   * Skapa en skiss (linjer och former) för att markera ett område i komponenten.

      Markören ändras till en korstråd när du skapar en skiss. Du kan rita flera distinkta linjer. Skisslinjen återspeglar anteckningsfärgen och kan vara en pil, cirkel eller oval.
   ![](do-not-localize/screen_shot_2018-03-22at110640.png)

   * Välj/ändra färg:
   ![](do-not-localize/chlimage_1-19.png)

   * Ta bort anteckningen.
   ![](do-not-localize/screen_shot_2018-03-22at110647.png)

1. Du kan stänga anteckningsdialogrutan genom att klicka/trycka utanför dialogrutan. En trunkerad vy (det första ordet) av anteckningen, tillsammans med eventuella skisser, visas:

   ![screen_shot_2018-03-22at110850](assets/screen_shot_2018-03-22at110850.png)

1. När du är klar med redigeringen av en viss anteckning kan du:

   * Klicka/tryck på textmarkören för att öppna anteckningen. När du har öppnat hela texten kan du göra ändringar eller ta bort anteckningen.

      * Skisser kan inte tas bort oberoende av anteckningen.
   * Flytta textmarkören.
   * Klicka/tryck på en skisslinje för att markera skissen och dra den till önskad plats.
   * Flytta, eller kopiera, en komponent

      * Alla relaterade anteckningar och skisser av dem flyttas eller kopieras också, och deras placering i förhållande till stycket förblir densamma.


1. Om du vill avsluta anteckningsläget och återgå till det tidigare använda läget trycker/klickar du på ikonen Anteckning (x-symbol) till höger i det övre verktygsfältet.

>[!NOTE]
>
>Anteckningar kan inte läggas till på en sida som har låsts av en annan användare.

### Anteckningsindikator {#annotation-indicator}

Anteckningar visas inte i redigeringsläge, men märket längst upp till höger i verktygsfältet visar hur många anteckningar som finns för den aktuella sidan. Märket ersätter standardikonen för anteckningar, men fungerar fortfarande som en snabblänk som växlar till/från anteckningsläget:

![chlimage_1-242](assets/chlimage_1-242.png)

