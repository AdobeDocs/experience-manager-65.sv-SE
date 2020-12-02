---
title: Skapa Launches
seo-title: Skapa Launches
description: Skapa en startsida för att möjliggöra uppdatering av en ny version av befintliga webbsidor för framtida aktivering. När du skapar en Launch anger du en titel och källsidan.
seo-description: Skapa en startsida för att möjliggöra uppdatering av en ny version av befintliga webbsidor för framtida aktivering. När du skapar en Launch anger du en titel och källsidan.
uuid: e67608a9-e6c9-42f3-bd1d-63a5fa87ae18
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 48826f03-6731-49c5-a6c5-6e2fb718f912
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 14%

---


# Skapa Launches{#creating-launches}

Skapa en startsida för att möjliggöra uppdatering av en ny version av befintliga webbsidor för framtida aktivering. När du skapar en Launch anger du en titel och källsidan:

* Titeln visas i **Sidekick**, där författare kan komma åt dem för att arbeta med dem.
* Källsidans underordnade sidor inkluderas som standard i starten. Du kan bara använda källsidan om du vill.
* Som standard uppdaterar [Live Copy](/help/sites-administering/msm.md) startsidorna automatiskt när källsidorna ändras. Du kan ange att en statisk kopia ska skapas för att förhindra automatiska ändringar.

Du kan också ange **startdatum** (och starttid) för att definiera när startsidorna ska befordras och aktiveras. **Startdatumet** fungerar dock endast i kombination med flaggan **Produktionsklar** (se [Redigera en startkonfiguration](/help/sites-classic-ui-authoring/classic-launches-editing.md#editing-a-launch-configuration)). För att åtgärderna ska köras automatiskt måste båda anges.

## Skapa en startsida {#creating-a-launch}

Följande procedur skapar en start.

1. Öppna sidan Webbplatsadministration ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin)).
1. Klicka på **Nytt...** och sedan **Ny start..**.
1. I dialogrutan **Create Launch** anger du värden för följande egenskaper:

   * **Starttitel**: Namnet på Launch. Namnet ska vara meningsfullt för författare.
   * **Källsida**: Sökvägen till sidan som starten ska skapas för. Som standard inkluderas alla underordnade sidor.
   * **Exkludera undersidor**: Välj det här alternativet om du bara vill skapa startsidan för källsidan och inte för de underordnade sidorna. Som standard är det här alternativet inte markerat.
   * **Synkronisera**: Välj det här alternativet om du automatiskt vill uppdatera innehållet på startsidor när källsidorna ändras. Detta uppnås genom att starta en [live-kopia](/help/sites-administering/msm.md).
   * **Startdatum**: Datum och tid då startkopian ska aktiveras (beroende på flaggan  **Production** Readyflag). se  [Startar - Händelsens](/help/sites-authoring/launches.md#launches-the-order-of-events) ordning).

   ![chlimage_1-99](assets/chlimage_1-99a.png)

1. Klicka på **Skapa**.

## Ta bort en start {#deleting-a-launch}

Du kan även ta bort en programstart.

1. Välj önskad start i [startkonsolen](/help/sites-classic-ui-authoring/classic-launches.md).
1. Klicka på **Ta bort** - bekräftelse krävs:

   ![chlimage_1-100](assets/chlimage_1-100a.png)

   >[!CAUTION]
   >
   >När du tar bort kapslade starter bör du ta bort de lägre nivåerna först.

