---
title: Skapa noder
seo-title: Skapa noder
description: Täck över kommentarsystemet
seo-description: Täck över kommentarsystemet
uuid: 802ae28b-9989-4c2c-b466-ab76a724efd3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cd4f53ee-537b-4f10-a64f-474ba2c44576
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 4%

---


# Skapa noder {#create-nodes}

Täck över kommentarsystemet med en anpassad version genom att kopiera det minsta antalet filer som behövs från `/libs` till `/apps` och ändra dem i `/apps`.

>[!CAUTION]
>
>Innehållet i mappen /libs redigeras aldrig eftersom ominstallation eller uppgradering kan ta bort eller ersätta mappen /libs medan innehållet i mappen /apps lämnas orört.

Om du använder [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) på en författarinstans börjar du med att skapa en sökväg i mappen /apps som är identisk med sökvägen till de överordnade komponenterna i mappen /libs.

Sökvägen som dupliceras är:

* `/libs/social/commons/components/hbs/comments/comment`

Vissa noder i sökvägen är mappar och andra är komponenter.

1. Bläddra till [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. Skapa `/apps/social` (om den inte redan finns)
   * Välj `/apps`-nod
   * **[!UICONTROL Create > Folder ...]**
      * Ange namn: `social`
1. Välj `social`-nod
   * **[!UICONTROL Create]** > **[!UICONTROL Folder...]**
      * Ange namn: `commons`
1. Välj `commons`-nod
   * **[!UICONTROL Create > Folder...]**
      * Ange namn: `components`
1. Välj `components`-nod
   * **[!UICONTROL Create > Folder..]**.
      * Ange namn: `hbs`
1. Välj `hbs`-nod
   * **[!UICONTROL Create]** >  **[!UICONTROL Create Component...]**
      * Ange etikett: `comments`
      * Ange titel: `Comments`
      * Ange beskrivning: `List of comments without showing avatars`
      * Supertyp: `social/commons/components/comments`
      * Ange grupp: `Communities`
      * Klicka på **[!UICONTROL Next]** tills **[!UICONTROL OK]**
1. Välj `comments`-nod

   * **[!UICONTROL Create]** >  **[!UICONTROL Create Component...]**

      * Ange etikett: `comment`
      * Ange titel: `Comment`
      * Ange beskrivning: `A comment instance without avatars`
      * Supertyp: `social/commons/components/comments/comment`
      * Ange grupp: `.hidden`
      * Klicka på **[!UICONTROL Next]** tills **[!UICONTROL OK]**
   * Välj **[!UICONTROL Save All]**
1. Ta bort standard `comments.jsp`
   * Välj nod `/apps/social/commons/components/hbs/comments/comments.jsp`
   * Välj **[!UICONTROL Delete]**
1. Ta bort standardkommentaren.jsp
   * välj nod `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * Välj **[!UICONTROL Delete]**
   * Välj **[!UICONTROL Save All]**

>[!NOTE]
>
>För att bevara arvskedjan anges `Super Type` (egenskapen `sling:resourceSuperType`) för överläggskomponenterna till samma värde som `Super Type` för de komponenter som ska överlappas, i det här fallet:
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`


Övertäckningens egna `Type`(egenskap `sling:resourceType`) måste vara en relativ självreferens så att innehåll som inte hittas i /apps sedan söks efter i /libs.
* Namn: `sling:resourceType`
* Typ: `String`
* Värde: `social/commons/components/hbs/comments`

1. Markera den gröna `[+] Add`
   * Namn: `sling:resourceType`
   * Typ: `String`
   * Värde: `social/commons/components/hbs/comments/comment`
1. Markera den gröna `[+] Add`
   * Välj **[!UICONTROL Save All]**

![create-nodes](assets/create-nodes.png)

