---
title: Skapa komponenterna
description: Lär dig hur du utökar komponenter med kommentarsystemet som består av kommentarkomponenter och kommentarkomponenter.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 2e02db9f-294d-4d4a-92da-3ab1d38416ab
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 3%

---

# Skapa komponenterna  {#create-the-components}

Exemplet med utökade komponenter använder kommentarsystemet, som består av två komponenter.

* Kommentarer - Det övergripande kommentarsystemet, som är den komponent som placeras på en sida.
* Kommentar - Komponenten som hämtar en instans av en publicerad kommentar.

Båda komponenterna måste installeras, särskilt om du anpassar utseendet på en publicerad kommentar.

>[!NOTE]
>
>Endast ett kommentarssystem per webbplatssida tillåts.
>
>Många webbgruppsfunktioner innehåller redan ett kommentarssystem vars resourceType kan ändras för att referera till det utökade kommentarsystemet.

## Skapa kommentarskomponenten {#create-the-comments-component}

I dessa anvisningar anges **Grupp** annat värde än `.hidden` så att komponenten kan göras tillgänglig från komponentens webbläsare (sidospark).

Borttagningen av den automatiskt skapade JSP-filen beror på att HBS-standardfilen används i stället.

1. Bläddra till **CRXDE|Lite** ([http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp))

1. Skapa en plats för anpassade program:

   * Välj `/apps` nod

      * **Skapa mapp** namngiven **[!UICONTROL custom]**

   * Välj `/apps/custom` nod

      * **Skapa mapp** namngiven **[!UICONTROL components]**

1. Välj `/apps/custom/components` nod

   * **[!UICONTROL Create > Component...]**

      * **Etikett**: *kommentarer*
      * **Titel**: *Alt-kommentarer*
      * **Beskrivning**: *Format för alternativa kommentarer*
      * **Supertyp**: *social/gemensam/komponent/hbs/comments*
      * **Grupp**: *Egen*

   * Välj **[!UICONTROL Next]**
   * Välj **[!UICONTROL Next]**
   * Välj **[!UICONTROL Next]**
   * Välj **[!UICONTROL OK]**

1. Expandera noden som skapades: `/apps/custom/components/comments`
1. Välj **[!UICONTROL Save All]**
1. Högerklicka `comments.jsp`
1. Välj **[!UICONTROL Delete]**
1. Välj **[!UICONTROL Save All]**

![create-component](assets/create-component.png)

### Skapa den underordnade kommentarskomponenten {#create-the-child-comment-component}

De här riktningarna har angetts **Grupp** till `.hidden` eftersom endast den överordnade komponenten ska inkluderas på en sida.

Borttagningen av den automatiskt skapade JSP-filen beror på att HBS-standardfilen används i stället.

1. Navigera till `/apps/custom/components/comments` nod
1. Högerklicka på noden

   * Välj **[!UICONTROL Create]** > **[!UICONTROL Component...]**

      * **Etikett**: *kommentar*
      * **Titel**: *Alt-kommentar*
      * **Beskrivning**: *Alternativ kommentarsstil*
      * **Supertyp**: *social/gemensam/komponent/hbs/comments/comment*
      * **Grupp**: `*.hidden*`

   * Välj **[!UICONTROL Next]**
   * Välj **[!UICONTROL Next]**
   * Välj **[!UICONTROL Next]**
   * Välj **[!UICONTROL OK]**

1. Expandera noden som skapades: `/apps/custom/components/comments/comment`
1. Välj **[!UICONTROL Save All]**
1. Högerklicka `comment.jsp`
1. Välj **[!UICONTROL Delete]**
1. Välj **[!UICONTROL Save All]**

![create-child-component](assets/create-child-component.png)

![create-component-crxde](assets/create-component-crxde.png)

### Kopiera och ändra standard-HBS-skript {#copy-and-modify-the-default-hbs-scripts}

Använda [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Kopiera `comments.hbs`

   * Från [/libs/social/Commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * Till [/apps/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* Redigera `comments.hbs` till:

   * Ändra värdet för `data-scf-component` attribute (~line 20):

      * Från `social/commons/components/hbs/comments`
      * Till `/apps/custom/components/comments`

   * Ändra om du vill ta med den anpassade kommentarkomponenten (~line 75):

      * Ersätt `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * Med `{{include this resourceType='/apps/custom/components/comments/comment'}}`

* Kopiera `comment.hbs`

   * Från [/libs/social/commons/components/hbs/comments/comment](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * Till [/apps/custom/components/comments/comment](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* Redigera `comment.hbs` till:

   * Ändra värdet på data-scf-component-attributet (~ line 19)

      * Från `social/commons/components/hbs/comments/comment`
      * Till `/apps/custom/components/comments/comment`

* Välj `/apps/custom` nod
* Välj **[!UICONTROL Save All]**

## Skapa en biblioteksmapp för klient {#create-a-client-library-folder}

För att undvika att ta med det här klientbiblioteket kan kategorivärdet för standardkommentarsystemets klientlib användas ( `cq.social.author.hbs.comments`). Klientlib måste då också inkluderas för alla instanser av standardkomponenten.

Använda [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Välj `/apps/custom/components/comments` nod
* Välj **[!UICONTROL Create Node]**

   * **Namn**: `clientlibs`
   * **Typ**: `cq:ClientLibraryFolder`
   * Lägg till i **[!UICONTROL Properties]** tab:

      * **Namn** `categories` **Typ** `String` **Värde** `cq.social.author.hbs.comments` `Multi`
      * **Namn** `dependencies` **Typ** `String` **Värde** `cq.social.scf` `Multi`

* Välj **[!UICONTROL Save All]**
* Med `/apps/custom/components/comments/clientlib`När noden är markerad skapar du tre filer:

   * **Namn**: `css.txt`
   * **Namn**: `js.txt`
   * **Namn**: customcommentsystem.js

* Ange &#39;customcommentsystem.js&#39; som innehåll i `js.txt`
* Välj **[!UICONTROL Save All]**

![comments-clientlibs](assets/comments-clientlibs.png)

## Registrera SCF-modellen och vyn {#register-the-scf-model-view}

När du utökar (åsidosätter) en SCF-komponent är resourceType annorlunda (overlay använder den relativa sökmekanism som genomsöker `/apps` före `/libs` så att resourceType förblir densamma). Därför måste du skriva JavaScript (i klientbiblioteket) för att registrera SCF JS-modellen och visa för den anpassade resourceType.

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

* Välj **[!UICONTROL Save All]**

## Publicera appen {#publish-the-app}

Om du vill använda den utökade komponenten i publiceringsmiljön måste du replikera den anpassade komponenten.

Ett sätt är att

* Från global navigering

   * Välj **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]**
   * Välj **[!UICONTROL Activate Tree]**
   * Ange `Start Path` till `/apps/custom`
   * Avmarkera **[!UICONTROL Only Modified]**
   * Välj **[!UICONTROL Activate]** knapp
