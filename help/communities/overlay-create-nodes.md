---
title: Skapa noder
description: Lär dig hur du övertäcker kommentarsystemet med en anpassad version genom att kopiera det minsta antalet filer som behövs från /libs och redigera dem i /apps.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3d72cbdf-5eb4-477d-aa61-035a846f7dcb
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Skapa noder {#create-nodes}

Täck över kommentarsystemet med en anpassad version genom att kopiera det minsta antalet filer som behövs från `/libs` till `/apps` och ändra dem i `/apps`.

>[!CAUTION]
>
>Innehållet i mappen /libs redigeras aldrig eftersom ominstallation eller uppgradering kan ta bort eller ersätta mappen /libs medan innehållet i mappen /apps lämnas orört.

Använd [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) på en författarinstans och börja med att skapa en sökväg i mappen /apps som är identisk med sökvägen till de överlagrade komponenterna i mappen /libs.

Sökvägen som dupliceras är:

* `/libs/social/commons/components/hbs/comments/comment`

Vissa noder i sökvägen är mappar och andra är komponenter.

1. Gå till [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. Skapa `/apps/social` (om den inte redan finns)
   * Välj `/apps`-nod
   * **[!UICONTROL Create > Folder]**
      * Ange namn: `social`
1. Välj `social`-nod
   * **[!UICONTROL Create]** > **[!UICONTROL Folder]**
      * Ange namn: `commons`
1. Välj `commons`-nod
   * **[!UICONTROL Create > Folder]**
      * Ange namn: `components`
1. Välj `components`-nod
   * **[!UICONTROL Create > Folder]**.
      * Ange namn: `hbs`
1. Välj `hbs`-nod
   * **[!UICONTROL Create]** > **[!UICONTROL Create Component]**
      * Ange etikett: `comments`
      * Ange titel: `Comments`
      * Ange beskrivning: `List of comments without showing avatars`
      * Supertyp: `social/commons/components/comments`
      * Ange grupp: `Communities`
      * Klicka på **[!UICONTROL Next]** till **[!UICONTROL OK]**
1. Välj `comments`-nod

   * **[!UICONTROL Create]** > **[!UICONTROL Create Component]**

      * Ange etikett: `comment`
      * Ange titel: `Comment`
      * Ange beskrivning: `A comment instance without avatars`
      * Supertyp: `social/commons/components/comments/comment`
      * Ange grupp: `.hidden`
      * Klicka på **[!UICONTROL Next]** till **[!UICONTROL OK]**
   * Välj **[!UICONTROL Save All]**
1. Ta bort standardvärdet `comments.jsp`
   * Välj nod `/apps/social/commons/components/hbs/comments/comments.jsp`
   * Välj **[!UICONTROL Delete]**
1. Ta bort standardkommentaren.jsp
   * välj nod `/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * Välj **[!UICONTROL Delete]**
   * Välj **[!UICONTROL Save All]**

>[!NOTE]
>
>För att bevara arvskedjan anges `Super Type` (egenskap `sling:resourceSuperType`) för överläggskomponenterna till samma värde som `Super Type` för de komponenter som ska överlappas, i det här fallet:
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
