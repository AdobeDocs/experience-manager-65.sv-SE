---
title: Skapa starter
description: Du kan skapa en startsida som gör det möjligt att uppdatera en ny version av befintliga webbsidor för framtida aktivering.
uuid: c1a32710-8189-4a2e-bf2f-428ab30d48c8
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 4ec6b408-a165-4617-8d90-e89d8a415bb3
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: bc7897da-15f6-4de4-a9fd-9dd84e6c7eed
source-git-commit: 7f595bec8ea138d5a73a17d0548320a31544dcd1
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 14%

---

# Skapa starter{#creating-launches}

Skapa en startsida för att möjliggöra uppdatering av en ny version av befintliga webbsidor för framtida aktivering. När du skapar en Launch anger du en titel och källsidan:

* Titeln visas i [Referenser](/help/sites-authoring/author-environment-tools.md#references) på webben, där författarna kan arbeta med dem.
* Källsidans underordnade sidor inkluderas som standard i starten. Du kan bara använda källsidan om du vill.
* Som standard [Live Copy](/help/sites-administering/msm.md) uppdaterar startsidorna automatiskt när källsidorna ändras. Du kan ange att en statisk kopia ska skapas för att förhindra automatiska ändringar.

Du kan också ange **startdatum** (och starttid) för att definiera när startsidorna ska befordras och aktiveras. **Startdatumet** fungerar dock endast i kombination med flaggan **Produktionsklar** (se [Redigera en startkonfiguration](/help/sites-authoring/launches-editing.md#editing-a-launch-configuration)). För att åtgärderna ska köras automatiskt måste båda anges.

## Skapa en Launch {#creating-a-launch}

Du kan skapa en start från Sites- eller Launches-konsolen:

1. Öppna **Webbplatser** eller **Startar** konsol.

   >[!NOTE]
   >
   >När du använder **Webbplatser** konsol är det vanligt att navigera till källsidans plats, men det är inte obligatoriskt eftersom du kan navigera när du väljer **Startkälla** i guiden.

1. Beroende på vilken konsol du använder:

   * **Launches**:

      1. Välj **Skapa start** i verktygsfältet för att öppna guiden.
   * **Sites**:

      1. Välj **Skapa** i verktygsfältet för att öppna markeringsrutan.
      1. Välj **Skapa start** för att öppna guiden.

   >[!NOTE]
   >
   >I **Sites**-konsolen kan du även använda [markeringsläget](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources) för att välja en sida innan du väljer **Skapa**.
   >
   >Då används den valda sidan som den ursprungliga källsidan.

1. I **Välj källa** steg du behöver **Lägg till sidor**. Du kan markera flera sidor och ange sökvägen för varje sida:

   * Navigera till önskad plats.
   * Markera källsidorna och bekräfta.

   Upprepa efter behov.

   ![chlimage_1-225](assets/chlimage_1-225.png)

   >[!NOTE]
   >
   >Om du vill lägga till sidor och/eller grenar i en lansering måste de finnas på en webbplats. dvs. under en gemensam toppnivårot.
   >
   >Om en webbplats innehåller språkrötter under den översta nivån måste sidorna och grenarna för en start ligga under en gemensam språkrot.
   >
   >Om du försöker skapa en start med en överordnad eller underordnad sida i källsökvägen misslyckas den och returnerar felet&quot;Målet finns redan vid :path till sidan&quot;.

1. För varje tävlingsbidrag kan du ange om du vill:

   * **Inkludera undersidor**:

      * Ange om du vill skapa starten med eller utan de underordnade sidorna.  Som standard inkluderas de här undersidorna.

   Fortsätt med **Nästa**.

   ![chlimage_1-226](assets/chlimage_1-226.png)

1. I **Egenskaper** steg i guiden som du kan ange:

   * **Starta titel**: Namnet på Launch. Namnet ska vara meningsfullt för författare.
   * **med befintligt innehåll**: det ursprungliga innehållet kommer att användas för att skapa starten.
   * **använda en ny mall för att ersätta sidan**: Se [Skapa start med ny mall](#create-launch-with-new-template) för mer information.
   * **Ärv källsidans livedata**: Välj det här alternativet om du automatiskt vill uppdatera innehållet på startsidor när källsidorna ändras. Det här alternativet uppnår du genom att göra starten till [live copy](/help/sites-administering/msm.md).

      Som standard är det här alternativet markerat.

   * **Startdatum**: Datum och tid då startkopian ska aktiveras (beroende på **Produktionsklar** Flagga. se [Startar - ordningen för händelser](/help/sites-authoring/launches.md#launches-the-order-of-events)).

   ![chlimage_1-227](assets/chlimage_1-227.png)

1. Använd **Skapa** för att slutföra processen och skapa en ny start. I bekräftelsedialogrutan får du frågan om du vill öppna starten direkt.

   Om du returnerar konsolen (med **Klar**) kan du se (och få tillgång till) din programstart från:

   * den [**Startar** konsol](/help/sites-authoring/launches.md#the-launches-console)
   * den [**Referenser** i **Webbplatser** konsol](/help/sites-authoring/launches.md#launches-in-references-sites-console)

### Skapa start med ny mall {#create-launch-with-new-template}

När [skapa en start](/help/sites-authoring/launches-creating.md#create-launch-with-new-template) du kan välja om du vill använda en ny mall:

**använda en ny mall för att ersätta sidan**

>[!CAUTION]
>
>Det här alternativet är endast tillgängligt när du skapar en start från **Webbplatser** konsol. Det är inte tillgängligt när du skapar en start från **Startar** konsol.

![chlimage_1-228](assets/chlimage_1-228.png)

Om du väljer det här alternativet kommer det att:

* uppdatera övriga tillgängliga alternativ,
* innehåller ett nytt steg där du kan välja önskad mall.

![chlimage_1-229](assets/chlimage_1-229.png)

>[!CAUTION]
>
>Om du använder en annan mall kommer den nya sidan att vara tom. På grund av den annorlunda sidstrukturen kommer inget innehåll att kopieras över.
>
>Den här funktionen kan användas för att ändra mallen för en [befintlig sida](/help/sites-authoring/managing-pages.md#creating-a-new-page) - även om innehållsförlusten måste beaktas.

### Skapa en kapslad start {#creating-a-nested-launch}

Genom att skapa en kapslad programstart (starta vid en programstart) kan du skapa en programstart från en befintlig programstart så att författarna kan utnyttja redan gjorda ändringar i stället för att behöva göra samma ändringar flera gånger för varje programstart.

>[!NOTE]
>
>Se även [Befordra en kapslad start](/help/sites-authoring/launches-promoting.md#promoting-a-nested-launch).

#### Skapa en kapslad start - Startar konsolen {#creating-a-nested-launch-launches-console}

Skapa en kapslad start från **Startar** konsolen är i stort sett densamma som att skapa andra former av programstart, med undantag för att du måste navigera till startgrenen `/content/launches`:

1. I **Startar** välj konsol **Skapa**.
1. Välj **Lägg till sidor** och navigera sedan till startgrenen genom att ange `/content/launches` i filtret. Välj önskad start och bekräfta med **Välj**:

   ![chlimage_1-230](assets/chlimage_1-230.png)

1. Fortsätt med **Nästa** och fylla i **Egenskaper** som vid andra starter.

   ![chlimage_1-231](assets/chlimage_1-231.png)

#### Skapa en kapslad start - platskonsol {#creating-a-nested-launch-sites-console}

Skapa en kapslad programstart från **Webbplatser** konsol - baserat på en befintlig start:

1. Öppna [Starta från referenser (platskonsolen)](/help/sites-authoring/launches.md#launches-in-references-sites-console) för att visa tillgängliga åtgärder.
1. Välj **Skapa start** för att öppna guiden (eftersom källan redan har valts hoppas steget **Välj källa** över).

1. Ange **Starta titel** och annan nödvändig information (som vid normal start).

1. Använd **Skapa** för att slutföra processen och skapa en ny start. I bekräftelsedialogrutan får du frågan om du vill öppna starten direkt.

   Om du väljer **Klar** återgår du till rutan **Referenser** i **Sites**-konsolen och om du väljer rätt sida visas den nya startsidan.

### Ta bort en start {#deleting-a-launch}

Du kan ta bort en programstart från [startar konsolen](/help/sites-authoring/launches.md#the-launches-console):

* Välj start genom att trycka på/klicka på miniatyrbilden.
* Verktygsfältet visas. Välj Ta bort.
* Bekräfta åtgärden.

>[!CAUTION]
>
>Om du tar bort en programstart tas själva programstarten och alla underordnade kapslade programstarter bort.
