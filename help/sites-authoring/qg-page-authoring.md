---
title: Snabbguide till framtagning av sidor
description: En snabb guide på hög nivå till de viktigaste funktionerna vid framtagning av sidinnehåll
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: a7e16555-9bbe-4da2-817c-4495a0193f3f
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 4%

---

# Snabbguide till framtagning av sidor{#quick-guide-to-authoring-pages}

De här procedurerna är avsedda som en snabbguide (på hög nivå) till de viktigaste åtgärderna för att skapa sidinnehåll i AEM.

De ska:

* Är inte avsedda som omfattande täckning.
* Ange länkar till den detaljerade dokumentationen.

Mer information om redigering med AEM finns i:

* [Steg 1 för författare](/help/sites-authoring/first-steps.md)
* [Redigeringssidor](/help/sites-authoring/page-authoring.md)

## Några snabba tips {#a-few-quick-hints}

Innan du ger en översikt över specifika detaljer finns det en liten samling allmänna tips och tips som du bör tänka på.

### Webbplatskonsol {#sites-console}

* **Skapa**

   * Den här knappen är tillgänglig i många konsoler - de alternativ som visas är sammanhangsberoende så att de kan variera beroende på scenario.

* Ändra ordning på sidor i en mapp

   * Detta kan göras i [Listvy](/help/sites-authoring/basic-handling.md#list-view). Ändringarna används och visas i andra vyer.

#### Sidredigering {#page-authoring}

* Navigera i länkar

   * ***Länkar är inte tillgängliga för navigering*** när du är **Redigera** läge. Om du vill navigera med länkar måste du [förhandsgranska sidan](/help/sites-authoring/editing-content.md#previewing-pages) med antingen

      * [Förhandsgranskningsläge](/help/sites-authoring/editing-content.md#preview-mode)
      * [Visa som publicerad](/help/sites-authoring/editing-content.md#view-as-published)

* Versioner startas/skapas inte från sidredigeraren. Detta görs nu från webbplatskonsolen (via **Skapa** eller [Tidslinje](/help/sites-authoring/basic-handling.md#timeline) för en vald resurs).

>[!NOTE]
>
>Det finns flera kortkommandon som kan underlätta redigeringen.
>
>* [Kortkommandon vid sidredigering](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
>* [Kortkommandon för konsoler](/help/sites-authoring/keyboard-shortcuts.md)
>

### Hitta din sida {#finding-your-page}

Det finns olika aspekter av att hitta en sida. Du kan navigera och/eller söka efter:

1. Öppna **Webbplatser** konsol (med **Webbplatser** i [Global navigering](/help/sites-authoring/basic-handling.md#global-navigation)) - den här utlöses (nedrullningsbar) när du väljer länken Adobe Experience Manager (överst till vänster).

1. Navigera nedåt i trädet genom att trycka/klicka på lämplig sida. Hur sidresurserna visas beror på vilken vy du använder - [Kort, lista eller kolumn](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources):

   ![screen_shot_2018-03-21at160214](assets/screen_shot_2018-03-21at160214.png)

1. Navigera uppåt i trädet med [sidhuvudet på väggen](/help/sites-authoring/basic-handling.md#theheaderwithbreadcrumbs)som gör att du kan gå tillbaka till den valda platsen:

   ![qgtap-01](assets/qgtap-01.png)

1. Du kan också [Sök](/help/sites-authoring/search.md) för en sida. Du kan välja din sida bland de resultat som visas.

   ![qgtap-03](assets/qgtap-03.png)

### Skapa en ny sida {#creating-a-new-page}

Till [skapa en sida](/help/sites-authoring/managing-pages.md#creating-a-new-page):

1. [Navigera till platsen](#finding-your-page) där du vill skapa sidan.
1. Använd **Skapa** ikon och sedan markera **Sida** från listan:

   ![qgtap-02](assets/qgtap-02.png)

1. Då öppnas guiden som vägleder dig genom att samla in den information som behövs när [skapa en ny sida](/help/sites-authoring/managing-pages.md#creating-a-new-page). Följ instruktionerna på skärmen.

### Välja sida för ytterligare åtgärd {#selecting-your-page-for-further-action}

Du kan markera en sida så att du kan utföra en åtgärd på den. När du väljer en sida uppdateras verktygsfältet automatiskt så att de åtgärder som är relevanta för resursen visas.

Hur du väljer en sida beror på vilken vy du använder i konsolen:

1. Kolumnvy:

   * Klicka på miniatyrbilden för resursen - miniatyrbilden visas med en bock som visar att den har markerats.

1. Listvy:

   * Klicka på miniatyrbilden för resursen - miniatyrbilden visas med en bock som visar att den har markerats.

1. Kortvy:

   * Ange markeringsläge med [välja den resurs som krävs](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources) med:

      * Mobil enhet: markera och hålla kvar
      * Skrivbord: [snabbåtgärd](/help/sites-authoring/basic-handling.md#quick-actions) - ikon:

   ![screen_shot_2018-03-21at160503](assets/screen_shot_2018-03-21at160503.png)

   * Kortet kommer att förses med en bock som visar att sidan har valts.

   >[!NOTE]
   >
   >När du är i markeringsläge **Välj** ikonen (en bock) ändras till **Avmarkera** ikon (ett kors).

### Snabbåtgärder (endast kortvyn/skrivbordet) {#quick-actions-card-view-desktop-only}

[Snabbåtgärder](/help/sites-authoring/basic-handling.md#quick-actions) är tillgängliga:

1. [Navigera till sidan](#finding-your-page) du vill vidta åtgärder för.
1. Håll muspekaren över kortet som representerar den resurs du behöver. Snabbåtgärderna visas:

   ![screen_shot_2018-03-21at160503-1](assets/screen_shot_2018-03-21at160503-1.png)

### Redigera sidinnehåll {#editing-your-page-content}

1. [Navigera till sidan](#finding-your-page) du vill redigera.
1. [Öppna sidan för redigering](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing) med ikonen Redigera (penna):

   ![screen_shot_2018-03-21at160607](assets/screen_shot_2018-03-21at160607.png)

   Du kan komma åt detta från antingen:

   * [Snabbåtgärder (endast kortvyn/skrivbordet)](#quick-actions-card-view-desktop-only) för lämplig resurs.
   * Verktygsfältet när [sidan har valts](#selectiingyourpageforfurtheraction).

1. När redigeraren öppnas kan du:

   * [Lägga till en ny komponent på sidan](/help/sites-authoring/editing-content.md#inserting-a-component) av:

      * öppna sidopanelen
      * välja fliken Komponenter (på [komponentwebbläsare](/help/sites-authoring/author-environment-tools.md#components-browser))
      * dra den nödvändiga komponenten till sidan.

     Sidpanelen kan öppnas (och stängas) med:

     ![Öppna sidopanelen](do-not-localize/screen_shot_2018-03-21at160738.png)

   * [Redigera innehållet i en befintlig komponent](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) på sidan:

      * Öppna komponentens verktygsfält med ett klick. Använd **Redigera** (penna) för att öppna dialogrutan.
      * Öppna komponentens in-place-redigerare genom att markera och hålla ned eller dubbelklicka. De tillgängliga åtgärderna visas (för vissa komponenter är det ett begränsat urval).
      * Om du vill visa alla tillgängliga åtgärder går du till helskärmsläge med:

     ![Helskärmsläge](do-not-localize/screen_shot_2018-03-21at160706.png)

   * [Konfigurera egenskaperna för en befintlig komponent](/help/sites-authoring/editing-content.md#component-edit-dialog)

      * Öppna komponentens verktygsfält med ett klick. Använd **Konfigurera** (skiftnyckel) för att öppna dialogrutan.

   * [Flytta en komponent](/help/sites-authoring/editing-content.md#moving-a-component) antingen:

      * Dra den önskade komponenten till dess nya plats.
      * Öppna komponentens verktygsfält med ett klick. Använd **Klipp ut** sedan **Klistra in** ikoner där det behövs.

   * [Kopiera (och klistra in)](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) en komponent:

      * Öppna komponentens verktygsfält med ett klick. Använd **Kopiera** sedan **Klistra in** vid behov.

   >[!NOTE]
   >
   >Du kan **Klistra in** till antingen samma sida eller en annan sida. Om du klistrar in på en annan sida som redan var öppen före klipp ut/kopiera-åtgärden, måste sidan uppdateras.

   * [Ta bort](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) en komponent:

      * Öppna komponentverktygsfältet med ett klick och använd sedan kommandot **Ta bort** -ikon.

   * [Lägg till anteckningar](/help/sites-authoring/annotations.md#annotations) till sidan:

      * Välj **Anteckna** läge (pratbubblarikon). Lägg till anteckningar med **Lägg till anteckning** (plus). Avsluta anteckningsläget med X överst till höger.

     ![Anteckna](do-not-localize/screen_shot_2018-03-21at160813.png)

   * [Förhandsgranska en sida](/help/sites-authoring/editing-content.md#preview-mode) (för att se hur det kommer att se ut i publiceringsmiljön)

      * Välj **Förhandsgranska** i verktygsfältet.

   * Återgå till redigeringsläget (eller välj ett annat läge) med **Redigera** väljare.

   >[!NOTE]
   >
   >Om du vill navigera med länkar i innehållet måste du använda [Förhandsgranskningsläge](/help/sites-authoring/editing-content.md#preview-mode).

### Redigera sidegenskaperna {#editing-the-page-properties}

Det finns två (huvudsakliga) metoder för [redigera sidegenskaper](/help/sites-authoring/editing-page-properties.md):

* Från **Webbplatser** konsol:

   1. [Navigera till sidan](#finding-your-page) du vill publicera.
   1. Välj **Egenskaper** ikon från antingen

      * [Snabbåtgärder (endast kortvyn/skrivbordet)](#quick-actions-card-view-desktop-only) för lämplig resurs.
      * Verktygsfältet när [sidan har valts](#selectiingyourpageforfurtheraction).

  ![screen_shot_2018-03-2160850](assets/screen_shot_2018-03-21at160850.png)

   1. Sidegenskaperna visas. Du kan göra nödvändiga uppdateringar och sedan använda Spara för att behålla dessa

* När [redigera sidan](#editing-your-page-content):

   1. Öppna **Sidinformation** -menyn.
   1. Välj **Öppna egenskaper** för att öppna dialogrutan för redigering av egenskaperna.

  ![screen_shot_2018-03-2160920](assets/screen_shot_2018-03-21at160920.png)

### Publicera din sida (eller avpublicera) {#publishing-your-page-or-unpublishing}

Det finns två metoder [publicera din sida](/help/sites-authoring/publishing-pages.md) (och även för avpublicering):

* Från **Webbplatser** konsol:

   1. [Navigera till sidan](#finding-your-page) du vill publicera.
   1. Välj **Snabbpublicering** ikon från antingen

      * [Snabbåtgärder (endast kortvyn/skrivbordet)](#quick-actions-card-view-desktop-only) för lämplig resurs.
      * Verktygsfältet när [sidan har valts](#selectiingyourpageforfurtheraction) (ger även tillgång till [Publicera senare](/help/sites-authoring/publishing-pages.md#main-pars-title-12)).

  ![screen_shot_2018-03-2160957](assets/screen_shot_2018-03-21at160957.png)

* När [redigera sidan](#editing-your-page-content):

   1. Öppna **Sidinformation** -menyn.
   1. Välj **Publicera sida**.

  ![screen_shot_2018-03-21at161026](assets/screen_shot_2018-03-21at161026.png)

* Du kan bara avpublicera en sida från konsolen via alternativet **Hantera publikation**, som bara är tillgängligt i verktygsfältet (inte via snabbåtgärderna).

  The **Avpublicera sida** är fortfarande tillgängligt via **Sidinformation** i redigeraren.

  ![screen_shot_2018-03-2161059](assets/screen_shot_2018-03-21at161059.png)

  Se [Publicera sidor](/help/sites-authoring/publishing-pages.md#unpublishing-pages) för mer information.

### Flytta, kopiera och klistra in eller ta bort sidan {#move-copy-and-paste-or-delete-your-page}

Alla dessa åtgärder kan utlösas av:

1. [Navigera till sidan](#finding-your-page) du vill flytta, kopiera och klistra in eller ta bort.
1. Välj ikonen för kopiera (och sedan klistra in), flytta eller ta bort efter behov på något av följande sätt:

   * [Snabbåtgärder (endast kortvyn/skrivbordet)](#quick-actions-card-view-desktop-only) för den resurs som krävs.
   * Verktygsfältet när [sidan har valts](#selecting-your-page-for-further-action).

   Sedan, beroende på vad du gör:

   * Copy:

      * Navigera till den nya platsen och klistra in.

   * Flytta:

      * Guiden öppnas och samlar in den information som behövs för att flytta sidan. Följ instruktionerna på skärmen.

   * Ta bort:

      * Du ombeds bekräfta åtgärden.

   >[!NOTE]
   >
   >Borttagning är inte tillgängligt som snabbåtgärd.

### Låser sidan (låser upp) {#locking-your-page-then-unlocking}

[När du låser en sida](/help/sites-authoring/editing-content.md#locking-a-page) kan andra författare inte arbeta med den. Ikonen/knappen Lås (och Lås upp) finns:

* Verktygsfältet när [sidan har valts](#selecting-your-page-for-further-action).
* The [Listrutan Sidinformation](#editing-the-page-properties) när du redigerar en sida.
* Sidans verktygsfält när du redigerar en sida (när sidan är låst)

Låsikonen ser till exempel ut så här:

![screen_shot_2018-03-2161124](assets/screen_shot_2018-03-21at161124.png)

### Åtkomst till sidreferenser {#accessing-page-references}

[Snabb åtkomst till referenser](/help/sites-authoring/author-environment-tools.md#references) till en sida eller från en sida är tillgängliga i Reference Rail.

1. Välj **Referenser** med verktygsfältsikonen (antingen före eller efter [markera sidan](#selecting-your-page-for-further-action)):

   ![screen_shot_2018-03-2161210](assets/screen_shot_2018-03-21at161210.png)

   En lista över referenstyper visas:

   ![screen-shot_2019-03-05at114412](assets/screen-shot_2019-03-05at114412.png)

1. Klicka på önskad referenstyp för att visa mer information och (vid behov) vidta ytterligare åtgärder.

### Skapa en version av din sida {#creating-a-version-of-your-page}

Skapa en [version](/help/sites-authoring/working-with-page-versions.md) på sidan:

1. Om du vill öppna tidslinjen markerar du **[Tidslinje](/help/sites-authoring/basic-handling.md#timeline)** med verktygsfältsikonen (antingen före eller efter [markera sidan](#selecting-your-page-for-further-action)):

   ![screen_shot_2018-03-21at16135](assets/screen_shot_2018-03-21at161355.png)

1. Klicka på uppilen längst ned till höger i tidslinjen för att visa extra knappar, inklusive **Spara som version**.

   ![screen-shot_2019-03-05at114600](assets/screen-shot_2019-03-05at114600.png)

1. Välj **Spara som version** sedan **Skapa**.

### Återställa/jämföra en version av sidan {#restoring-comparing-a-version-of-your-page}

Samma grundläggande funktion används när du återställer och/eller jämför versioner av sidan:

1. Välj **[Tidslinje](/help/sites-authoring/basic-handling.md#timeline)** med verktygsfältsikonen (antingen före eller efter [markera sidan](#selecting-your-page-for-further-action)):

   ![screen_shot_2018-03-21at161355-1](assets/screen_shot_2018-03-21at161355-1.png)

   Om en version av sidan redan har sparats visas den på tidslinjen.

1. Klicka på den version som du vill återställa. Då visas ytterligare åtgärdsknappar:

   * **Återgå till den här versionen**

      * Versionen har återställts.

   * **Visa skillnader**

      * Sidan öppnas med skillnader (mellan de två versionerna) markerade.
