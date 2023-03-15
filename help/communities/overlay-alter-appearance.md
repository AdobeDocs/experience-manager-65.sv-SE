---
title: Ändra utseendet
seo-title: Alter the Appearance
description: Ändra skriptet
seo-description: Modify the script
uuid: 30555b9f-da29-4115-9ed5-25f80a247bd6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: c9d31ed8-c105-453b-bd3c-4660dfd81272
docset: aem65
exl-id: cb8f6967-216c-46d3-a7ba-068b0f5e3b94
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 1%

---

# Ändra utseendet {#alter-the-appearance}

## Ändra skriptet {#modify-the-script}

Skriptet comment.hbs ansvarar för att skapa det övergripande HTML för varje kommentar.

Så här visar du inte avataren bredvid varje publicerad kommentar:

1. Kopiera `comment.hbs`från `libs`till `apps`

   1. Välj `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. Välj **[!UICONTROL Copy]**
   1. Välj `/apps/social/commons/components/hbs/comments/comment`
   1. Välj **[!UICONTROL Paste]**

1. Öppna överlägg `comment.hbs`

   * Dubbelklicka på noden `comment.hbs` in `/apps/social/commons/components/hbs/comments/comment folder`

1. Hitta följande rader och ta bort eller kommentera dem:

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

Radera linjerna eller omge dem med `<!--` och `-->` för att kommentera ut dem. Dessutom läggs tecknen &#39;xxx&#39; till som en visuell indikator på var avataren skulle ha varit.

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### Replikera övertäckningen {#replicate-the-overlay}

Överlagrade kommentarer skickas till publiceringsinstansen med replikeringsverktyget.

>[!NOTE]
>
>En robustare form av replikering skulle vara att skapa ett paket i Package Manager och [activate](/help/sites-administering/package-manager.md#replicating-packages) den. Ett paket kan exporteras och arkiveras.

Välj **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** och klicka **[!UICONTROL Activate Tree]**.

Ange startsökvägen `/apps/social/commons` och markera **[!UICONTROL Activate]**.

![verify-content-template](assets/verify-content-template.png)

### Visa resultat {#view-results}

Om du loggar in på publiceringsinstansen som administratör, t.ex. https://localhost:4503/crx/de som administratör/administratör, kan du verifiera att de överliggande komponenterna finns där.

Om du loggar ut och loggar in igen som `aaron.mcdonald@mailinator.com/password` och uppdatera sidan, observera att den publicerade kommentaren inte längre visas med en avatar, i stället visas en enkel &#39;xxx&#39;.

![create-template-component](assets/create-template-component.png)
