---
title: Skapa komponenterna
seo-title: Skapa komponenterna
description: Skapa komponenten Kommentarer
seo-description: Skapa komponenten Kommentarer
uuid: ea6e00d4-1db7-40ef-ae49-9ec55df58adf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 83c4f18a-d7d6-4090-88c7-41a9075153b5
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# Skapa komponenterna {#create-the-components}

Exemplet med utökade komponenter använder kommentarsystemet, som i själva verket består av två komponenter

* Kommentarer - det övergripande kommentarsystemet, som är den komponent som placeras på en sida
* Kommentar - Komponenten som hämtar en instans av en publicerad kommentar

Båda komponenterna måste installeras, särskilt om du anpassar utseendet på en publicerad kommentar.

>[!NOTE]
>
>Endast ett kommentarssystem per webbplatssida tillåts.
>
>Många webbgruppsfunktioner innehåller redan ett kommentarssystem vars resourceType kan ändras för att referera till det utökade kommentarsystemet.

## Skapa komponenten Kommentarer {#create-the-comments-component}

I de här riktningarna anges ett annat **gruppvärde** än `.hidden` så komponenten kan göras tillgänglig från komponentwebbläsaren (sidespark).

Borttagningen av den automatiskt skapade JSP-filen beror på att HBS-standardfilen används i stället.

1. Bläddra till **CRXDE|Lite** ([http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp))

1. Skapa en plats för anpassade program:

   * Markera `/apps` noden

      * **Skapa mapp** med namnet **[!UICONTROL custom]**
   * Markera `/apps/custom` noden

      * **Skapa mapp** med namngivna **[!UICONTROL komponenter]**


1. Markera `/apps/custom/components` noden

   * **[!UICONTROL Skapa > Komponent...]**

      * **Etikett**: *kommentarer*
      * **Titel**: *Alt-kommentarer*
      * **Beskrivning**: Format *för alternativa kommentarer*
      * **Supertyp**: social/ *gemensam/komponent/hbs/comments*
      * **Grupp**: *Anpassad*
   * Markera **[!UICONTROL nästa]**
   * Markera **[!UICONTROL nästa]**
   * Markera **[!UICONTROL nästa]**
   * Välj **[!UICONTROL OK]**


1. Expandera noden som nyss skapades: `/apps/custom/components/comments`
1. Välj **[!UICONTROL Spara alla]**
1. Högerklicka `comments.jsp`
1. Markera **[!UICONTROL Ta bort]**
1. Välj **[!UICONTROL Spara alla]**

![chlimage_1-70](assets/chlimage_1-70.png)

### Skapa den underordnade kommentarskomponenten {#create-the-child-comment-component}

I de här instruktionerna anges **Gruppera** som `.hidden` att bara den överordnade komponenten ska inkluderas på en sida.

Borttagningen av den automatiskt skapade JSP-filen beror på att HBS-standardfilen används i stället.

1. Navigate to the `/apps/custom/components/comments` node
1. Högerklicka på noden

   * Välj **[!UICONTROL Skapa > Komponent..]**

      * **Etikett**: *kommentar*
      * **Titel**: *Alt-kommentar*
      * **Beskrivning**: Format *för alternativa kommentarer*
      * **Supertyp**: social/ *gemensam/komponent/hbs/comments/comment*
      * **Grupp**: `*.hidden*`
   * Markera **[!UICONTROL nästa]**
   * Markera **[!UICONTROL nästa]**
   * Markera **[!UICONTROL nästa]**
   * Välj **[!UICONTROL OK]**


1. Expandera noden som nyss skapades: `/apps/custom/components/comments/comment`
1. Välj **[!UICONTROL Spara alla]**
1. Högerklicka `comment.jsp`
1. Markera **[!UICONTROL Ta bort]**
1. Välj **[!UICONTROL Spara alla]**

![chlimage_1-71](assets/chlimage_1-71.png) ![chlimage_1-72](assets/chlimage_1-72.png)

### Kopiera och ändra standard-HBS-skript {#copy-and-modify-the-default-hbs-scripts}

Använda [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Kopiera `comments.hbs`

   * Från [/libs/social/Commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * To [/apps/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* Redigera `comments.hbs` till:

   * Ändra värdet för `data-scf-component` attributet (~line 20):

      * From `social/commons/components/hbs/comments`
      * Till `/apps/custom/components/comments`
   * Ändra om du vill ta med den anpassade kommentarkomponenten (~line 75):

      * Replace `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * Med `{{include this resourceType='/apps/custom/components/comments/comment'}}`


* Kopiera `comment.hbs`

   * Från [/libs/social/Commons/components/hbs/comments/comment](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * To [/apps/custom/components/comments/comment](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* Redigera `comment.hbs` till:

   * Ändra värdet på data-scf-component-attributet (~ line 19)

      * From `social/commons/components/hbs/comments/comment`
      * Till `/apps/custom/components/comments/comment`

* Markera `/apps/custom` nod
* Välj **[!UICONTROL Spara alla]**

## Skapa en biblioteksmapp för klient {#create-a-client-library-folder}

För att undvika att uttryckligen ta med det här klientbiblioteket kan kategorivärdet för standardkommentarsystemets clientlib användas ( `cq.social.author.hbs.comments`), men sedan inkluderas klientlib även för alla instanser av standardkomponenten.

Använda [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Markera `/apps/custom/components/comments` nod
* Välj **[!UICONTROL Skapa nod]**

   * **Namn**: `clientlibs`
   * **Typ**: `cq:ClientLibraryFolder`
   * Lägg till på fliken **[!UICONTROL Egenskaper]** :

      * **Namnge** `categories` typ ****`String` värde **** `cq.social.author.hbs.comments``Multi`
      * **Namnge** `dependencies` typ ****`String` värde **** `cq.social.scf``Multi`

* Välj **[!UICONTROL Spara alla]**
* Med `/apps/custom/components/comments/clientlib`noden markerad skapar du tre filer:

   * **Namn**: `css.txt`
   * **Namn**: `js.txt`
   * **Namn**: customcommentsystem.js

* Ange &#39;customcommentsystem.js&#39; som innehåll i `js.txt`
* Välj **[!UICONTROL Spara alla]**

![chlimage_1-73](assets/chlimage_1-73.png)

## Registrera SCF-modellen och vyn {#register-the-scf-model-view}

När du utökar (åsidosätter) en SCF-komponent är resourceType annorlunda (overlay använder den relativa sökmekanismen som genomsöks `/apps` före `/libs` så att resourceType förblir densamma). Därför måste du skriva JavaScript (i klientbiblioteket) för att registrera SCF JS-modellen och visa för den anpassade resourceType.

Ange följande text som innehåll i `customcommentsystem.js`:

### customcommentsystem.js {#customcommentsystem-js}

```xml
(function($CQ, _, Backbone, SCF) {
    "use strict";

    var CustomComment = SCF.Components["social/commons/components/hbs/comments/comment"].Model;
    var CustomCommentView = SCF.Components["social/commons/components/hbs/comments/comment"].View;

    var CustomCommentSystem = SCF.Components["social/commons/components/hbs/comments"].Model;
    var CustomCommentSystemView = SCF.Components["social/commons/components/hbs/comments"].View;

    SCF.registerComponent('/apps/custom/components/comments/comment', CustomComment, CustomCommentView);
    SCF.registerComponent('/apps/custom/components/comments', CustomCommentSystem, CustomCommentSystemView);

})($CQ, _, Backbone, SCF);
```

* Välj **[!UICONTROL Spara alla]**

## Publicera appen {#publish-the-app}

För att den utökade komponenten ska fungera i publiceringsmiljön måste den anpassade komponenten replikeras.

Ett sätt att göra detta är att

* Från global navigering

   * Välj **[!UICONTROL Verktyg > Distribution > Replikering]**
   * Välj `Activate Tree`
   * Uppsättning `Start Path`: till `/apps/custom`
   * Avmarkera `Only Modified`
   * Markera `Activate`knapp

