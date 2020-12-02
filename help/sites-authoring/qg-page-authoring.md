---
title: Snabbguide till framtagning av sidor
seo-title: Snabbguide till framtagning av sidor
description: En snabb guide på hög nivå till de viktigaste funktionerna vid framtagning av sidinnehåll
seo-description: En snabb guide på hög nivå till de viktigaste funktionerna vid framtagning av sidinnehåll
uuid: ef7ab691-f80d-4eeb-9f4a-afbf1bc83669
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 2d35a2a4-0c8c-4b16-99a6-c6e6d66446dc
docset: aem65
translation-type: tm+mt
source-git-commit: e3683f6254295e606e9d85e88979feaaea76c42e
workflow-type: tm+mt
source-wordcount: '1590'
ht-degree: 4%

---


# Snabbguide till redigering av sidor{#quick-guide-to-authoring-pages}

De här procedurerna är avsedda som en snabbguide (på hög nivå) till de viktigaste åtgärderna för att skapa sidinnehåll i AEM.

De ska:

* Är inte avsedda som omfattande täckning.
* Ange länkar till den detaljerade dokumentationen.

Mer information om redigering med AEM finns i:

* [Steg 1 för författare](/help/sites-authoring/first-steps.md)
* [Redigeringssidor](/help/sites-authoring/page-authoring.md)

## Några snabba tips {#a-few-quick-hints}

Innan du ger en översikt över specifika detaljer finns det en liten samling allmänna tips och tips som du bör tänka på.

### Platskonsol {#sites-console}

* **Skapa**

   * Den här knappen är tillgänglig i många konsoler - de alternativ som visas är sammanhangsberoende så att de kan variera beroende på scenario.

* Ändra ordning på sidor i en mapp

   * Detta kan du göra i [listvyn](/help/sites-authoring/basic-handling.md#list-view). Ändringarna används och visas i andra vyer.

#### Sidredigering {#page-authoring}

* Navigera i länkar

   * ***Länkar är inte tillgängliga för*** navigering när du är i  **** redigeringsläge. Om du vill navigera med länkar måste du [förhandsgranska sidan](/help/sites-authoring/editing-content.md#previewing-pages) genom att antingen:

      * [Förhandsgranskningsläge](/help/sites-authoring/editing-content.md#preview-mode)
      * [Visa som publicerad](/help/sites-authoring/editing-content.md#view-as-published)

* Versioner startas/skapas inte från sidredigeraren; detta görs nu från webbplatskonsolen (via antingen **Skapa** eller [Tidslinje](/help/sites-authoring/basic-handling.md#timeline) för en vald resurs).

>[!NOTE]
>
>Det finns ett antal kortkommandon som kan underlätta redigeringen.
>
>* [Kortkommandon vid sidredigering](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
>* [Kortkommandon för konsoler](/help/sites-authoring/keyboard-shortcuts.md)

>



### Söker efter sidan {#finding-your-page}

Det finns olika aspekter av att hitta en sida. kan du navigera och/eller söka:

1. Öppna konsolen **Platser** (med alternativet **Platser** i [Global navigering](/help/sites-authoring/basic-handling.md#global-navigation) - detta aktiveras (listruta) när du väljer länken Adobe Experience Manager (överst till vänster).

1. Navigera nedåt i trädet genom att trycka/klicka på lämplig sida. Hur sidresurserna visas beror på vilken vy du använder - [Kort, Lista eller Kolumn](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources):

   ![screen_shot_2018-03-21at160214](assets/screen_shot_2018-03-21at160214.png)

1. Navigera uppåt i trädet med [det synliga spåret i huvudet](/help/sites-authoring/basic-handling.md#theheaderwithbreadcrumbs), som gör att du kan gå tillbaka till den valda platsen:

   ![qgtap-01](assets/qgtap-01.png)

1. Du kan även [söka](/help/sites-authoring/search.md) efter en sida. Du kan välja din sida bland de resultat som visas.

   ![qgtap-03](assets/qgtap-03.png)

### Skapar en ny sida {#creating-a-new-page}

Om du vill [skapa en ny sida](/help/sites-authoring/managing-pages.md#creating-a-new-page):

1. [Navigera till den ](#finding-your-page) plats där du vill skapa den nya sidan.
1. Använd ikonen **Skapa** och välj sedan **Sida** i listan:

   ![qgtap-02](assets/qgtap-02.png)

1. Guiden som vägleder dig genom att samla in den information som behövs när du skapar den nya sidan[. ](/help/sites-authoring/managing-pages.md#creating-a-new-page) Följ instruktionerna på skärmen.

### Välja sida för ytterligare åtgärd {#selecting-your-page-for-further-action}

Du kan markera en sida så att du kan utföra en åtgärd på den. När du väljer en sida uppdateras verktygsfältet automatiskt så att de åtgärder som är relevanta för resursen visas.

Hur du väljer en sida beror på vilken vy du använder i konsolen:

1. Kolumnvy:

   * Tryck/klicka på miniatyrbilden för resursen - miniatyrbilden kommer att överlappas med en bock för att visa att den har markerats.

1. Listvy:

   * Tryck/klicka på miniatyrbilden för resursen - miniatyrbilden kommer att överlappas med en bock för att visa att den har markerats.

1. Kortvy:

   * Ange markeringsläge genom att [välja önskad resurs](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources) med:

      * Mobil enhet: tryck och håll
      * Skrivbord: [snabbåtgärden](/help/sites-authoring/basic-handling.md#quick-actions) - tick-ikon:

   ![screen_shot_2018-03-21at160503](assets/screen_shot_2018-03-21at160503.png)

   * Kortet kommer att förses med en bock som visar att sidan har valts.
   >[!NOTE]
   >
   >I markeringsläge ändras ikonen **Markera** (en bock) till ikonen **Avmarkera** (ett kryss).

### Snabbåtgärder (endast kortvyn/skrivbordet) {#quick-actions-card-view-desktop-only}

[Det finns ](/help/sites-authoring/basic-handling.md#quick-actions) snabbåtgärder:

1. [Navigera till den ](#finding-your-page) sida som du vill utföra åtgärden på.
1. Håll muspekaren över kortet som representerar den resurs du behöver. snabbåtgärderna visas:

   ![screen_shot_2018-03-21at160503-1](assets/screen_shot_2018-03-21at160503-1.png)

### Redigera sidinnehållet {#editing-your-page-content}

Så här redigerar du sidan:

1. [Navigera till den ](#finding-your-page) sida som du vill redigera.
1. [Öppna sidan för ](/help/sites-authoring/managing-pages.md#opening-a-page-for-editing) redigering med ikonen Redigera (penna):

   ![screen_shot_2018-03-21at160607](assets/screen_shot_2018-03-21at160607.png)

   Du kommer åt detta från antingen:

   * [Snabbåtgärder (endast kortvyn/skrivbordet) ](#quick-actions-card-view-desktop-only) för lämplig resurs.
   * Verktygsfältet när din [sida har valts](#selectiingyourpageforfurtheraction).

1. När redigeraren öppnas kan du:

   * [Lägg till en ny komponent på din ](/help/sites-authoring/editing-content.md#inserting-a-component) sida genom att:

      * öppna sidopanelen
      * välja fliken Komponenter ([komponentwebbläsaren](/help/sites-authoring/author-environment-tools.md#components-browser))
      * dra den nödvändiga komponenten till sidan.

      Sidpanelen kan öppnas (och stängas) med:
   ![](do-not-localize/screen_shot_2018-03-21at160738.png)

   * [Redigera innehållet i en befintlig ](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) komponent på sidan:

      * Öppna komponentens verktygsfält genom att trycka eller klicka. Använd ikonen **Redigera** (penna) för att öppna dialogrutan.
      * Öppna komponentens direktredigerare genom att trycka och hålla ned eller dubbelklicka. De tillgängliga åtgärderna visas (för vissa komponenter är detta ett begränsat urval).
      * Om du vill visa alla tillgängliga åtgärder går du till helskärmsläge med:

   ![](do-not-localize/screen_shot_2018-03-21at160706.png)

   * [Konfigurera egenskaperna för en befintlig komponent](/help/sites-authoring/editing-content.md#component-edit-dialog)

      * Öppna komponentens verktygsfält genom att trycka eller klicka. Använd ikonen **Konfigurera** (skiftnyckel) för att öppna dialogrutan.
   * [Flytta en ](/help/sites-authoring/editing-content.md#moving-a-component) komponent:

      * Dra den önskade komponenten till dess nya plats.
      * Öppna komponentens verktygsfält genom att trycka eller klicka. Använd ikonerna **Klipp ut** och **Klistra in** där det behövs.
   * [Kopiera (och klistra in)](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) en komponent:

      * Öppna komponentens verktygsfält genom att trycka eller klicka. Använd ikonerna **Kopiera** och **Klistra in** efter behov.
   >[!NOTE]
   >
   >Du kan **Klistra in**-komponenter på samma sida eller på en annan sida. Om du klistrar in på en annan sida som redan var öppen före klipp ut/kopiera-åtgärden, måste sidan uppdateras.

   * [Deletea-](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) komponent:

      * Öppna komponentens verktygsfält med tryck eller klicka och använd sedan ikonen **Ta bort**.
   * [Lägg till ](/help/sites-authoring/annotations.md#annotations) anteckningar på sidan:

      * Välj läget **Anteckna** (ikonen för pratbubbla). Lägg till anteckningar med ikonen **Lägg till anteckning** (plus). Avsluta anteckningsläget med X överst till höger.

   ![](do-not-localize/screen_shot_2018-03-21at160813.png)

   * [Förhandsgranska en sida](/help/sites-authoring/editing-content.md#preview-mode)  (för att se hur den kommer att se ut i publiceringsmiljön)

      * Välj **Förhandsgranska** i verktygsfältet.
   * Återgå till redigeringsläget (eller välj ett annat läge) med listrutan **Redigera**.

   >[!NOTE]
   >
   >Om du vill navigera med hjälp av länkar i innehållet måste du använda [förhandsgranskningsläget](/help/sites-authoring/editing-content.md#preview-mode).

### Redigera sidegenskaperna {#editing-the-page-properties}

Det finns två (huvudsakliga) metoder för att [redigera sidegenskaper](/help/sites-authoring/editing-page-properties.md):

* Från konsolen **Platser**:

   1. [Navigera till den ](#finding-your-page) sida som du vill publicera.
   1. Välj ikonen **Egenskaper** från antingen:

      * [Snabbåtgärder (endast kortvyn/skrivbordet) ](#quick-actions-card-view-desktop-only) för lämplig resurs.
      * Verktygsfältet när din [sida har valts](#selectiingyourpageforfurtheraction).

   ![screen_shot_2018-03-21at160850](assets/screen_shot_2018-03-21at160850.png)

   1. Sidegenskaperna visas. Du kan göra nödvändiga uppdateringar och sedan använda Spara för att behålla dessa


* När [du redigerar sidan](#editing-your-page-content):

   1. Öppna menyn **Sidinformation**.
   1. Välj **Öppna Egenskaper** för att öppna dialogrutan för redigering av egenskaperna.

   ![screen_shot_2018-03-21at160920](assets/screen_shot_2018-03-21at160920.png)

### Publicera din sida (eller avpublicera) {#publishing-your-page-or-unpublishing}

Det finns två huvudmetoder för att [publicera sidan](/help/sites-authoring/publishing-pages.md) (och även för att avpublicera):

* Från konsolen **Platser**:

   1. [Navigera till den ](#finding-your-page) sida som du vill publicera.
   1. Välj ikonen **Snabbpublicering** från antingen:

      * [Snabbåtgärder (endast kortvyn/skrivbordet) ](#quick-actions-card-view-desktop-only) för lämplig resurs.
      * Verktygsfältet när [sidan har valts](#selectiingyourpageforfurtheraction) (ger även åtkomst till [Publicera senare](/help/sites-authoring/publishing-pages.md#main-pars-title-12)).

   ![screen_shot_2018-03-21at160957](assets/screen_shot_2018-03-21at160957.png)

* När [du redigerar sidan](#editing-your-page-content):

   1. Öppna menyn **Sidinformation**.
   1. Välj **Publicera sida**.

   ![screen_shot_2018-03-21at161026](assets/screen_shot_2018-03-21at161026.png)

* Du kan bara avpublicera en sida från konsolen via alternativet **Hantera publikation**, som bara är tillgängligt i verktygsfältet (inte via snabbåtgärderna).

   Alternativet **Avpublicera sida** är fortfarande tillgängligt via menyn **Sidinformation** i redigeraren.

   ![screen_shot_2018-03-21at161059](assets/screen_shot_2018-03-21at161059.png)

   Mer information finns i [Publicera sidor](/help/sites-authoring/publishing-pages.md#unpublishing-pages).

### Flytta, kopiera och klistra in eller ta bort sidan {#move-copy-and-paste-or-delete-your-page}

Alla dessa åtgärder kan utlösas av:

1. [Navigera till den ](#finding-your-page) sida som du vill flytta, kopiera och klistra in eller ta bort.
1. Välj ikonen för kopiera (och sedan klistra in), flytta eller ta bort efter behov på något av följande sätt:

   * [Snabbåtgärder (endast kortvyn/skrivbordet) ](#quick-actions-card-view-desktop-only) för den begärda resursen.
   * Verktygsfältet när din [sida har valts](#selecting-your-page-for-further-action).

   Sedan, beroende på vad du gör:

   * Kopiera:

      * Du måste sedan navigera till den nya platsen och klistra in.
   * Flytta:

      * Guiden öppnas och samlar in den information som behövs för att flytta sidan. Följ instruktionerna på skärmen.
   * Ta bort:

      * Du ombeds bekräfta åtgärden.
   >[!NOTE]
   >
   >Borttagning är inte tillgängligt som snabbåtgärd.

### Låser sidan (låser upp) {#locking-your-page-then-unlocking}

[När du låser en sida](/help/sites-authoring/editing-content.md#locking-a-page) kan andra författare inte arbeta med den. Ikonen/knappen Lås (och Lås upp) finns:

* Verktygsfältet när din [sida har valts](#selecting-your-page-for-further-action).
* Listrutan [Sidinformation](#editing-the-page-properties) när du redigerar en sida.
* Sidans verktygsfält när du redigerar en sida (när sidan är låst)

Låsikonen ser till exempel ut så här:

![screen_shot_2018-03-21at161124](assets/screen_shot_2018-03-21at161124.png)

### Åtkomst till sidreferenser {#accessing-page-references}

[Snabb åtkomst till ](/help/sites-authoring/author-environment-tools.md#references) referenser till/från en sida finns i Reference Rail.

1. Välj **Referenser** med verktygsfältsikonen (antingen före eller efter [att välja sida](#selecting-your-page-for-further-action)):

   ![screen_shot_2018-03-21at161210](assets/screen_shot_2018-03-21at161210.png)

   En lista över referenstyper visas:

   ![screen-shot_2019-03-05at114412](assets/screen-shot_2019-03-05at114412.png)

1. Tryck/klicka på den typ av referens som krävs för att visa mer information och (vid behov) vidta ytterligare åtgärder.

### Skapa en version av din sida {#creating-a-version-of-your-page}

Så här skapar du en [version](/help/sites-authoring/working-with-page-versions.md) av sidan:

1. Om du vill öppna tidslinjen väljer du **[Tidslinje](/help/sites-authoring/basic-handling.md#timeline)** med verktygsfältsikonen (antingen före eller efter [att markera sidan](#selecting-your-page-for-further-action)):

   ![screen_shot_2018-03-21at161355](assets/screen_shot_2018-03-21at161355.png)

1. Tryck/klicka på uppilen längst ned till höger i kolumnen Tidslinje för att visa extra knappar, inklusive **Spara som version**.

   ![screen-shot_2019-03-05at114600](assets/screen-shot_2019-03-05at114600.png)

1. Välj **Spara som version** och **Skapa**.

### Återställa/jämföra en version av sidan {#restoring-comparing-a-version-of-your-page}

Samma grundläggande funktion används när du återställer och/eller jämför versioner av sidan:

1. Välj **[Tidslinje](/help/sites-authoring/basic-handling.md#timeline)** med verktygsfältsikonen (antingen före eller efter [markering av sidan](#selecting-your-page-for-further-action)):

   ![screen_shot_2018-03-21at161355-1](assets/screen_shot_2018-03-21at161355-1.png)

   Om en version av sidan redan har sparats visas den i tidslinjen.

1. Tryck/klicka på den version som du vill återställa - då visas ytterligare åtgärdsknappar:

   * **Återgå till den här versionen**

      * Versionen återställs.
   * **Visa skillnader**

      * Sidan öppnas med skillnader (mellan de två versionerna) markerade.
