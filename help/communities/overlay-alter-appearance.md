---
title: Ändra utseendet
description: Lär dig hur du redigerar skriptet comment.hbs som ansvarar för att skapa det övergripande HTML för varje kommentar i Adobe Experience Manager Communities.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: cb8f6967-216c-46d3-a7ba-068b0f5e3b94
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Ändra utseendet {#alter-the-appearance}

## Ändra skriptet {#modify-the-script}

Skriptet `comment.hbs` ansvarar för att skapa det övergripande HTML för varje kommentar.

Så här visar du inte avataren bredvid varje publicerad kommentar:

1. Kopiera `comment.hbs` från `libs` till `apps`

   1. Välj `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. Välj **[!UICONTROL Copy]**
   1. Välj `/apps/social/commons/components/hbs/comments/comment`
   1. Välj **[!UICONTROL Paste]**

1. Öppna det dolda `comment.hbs`

   * Dubbelklicka på noden `comment.hbs` i `/apps/social/commons/components/hbs/comments/comment folder`

1. Hitta följande rader och ta bort eller kommentera dem:

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

Ta bort raderna eller omge dem med `<!--` och `-->` så att du kommenterar dem. Dessutom läggs tecknen &#39;xxx&#39; till som en visuell indikator på var avataren skulle ha varit.

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
>En robustare form av replikering skulle vara att skapa ett paket i Package Manager och [aktivera](/help/sites-administering/package-manager.md#replicating-packages) det. Ett paket kan exporteras och arkiveras.

I den globala navigeringen väljer du **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** och klickar på **[!UICONTROL Activate Tree]**.

Ange `/apps/social/commons` som startsökväg och välj **[!UICONTROL Activate]**.

![verify-content-template](assets/verify-content-template.png)

### Visa resultat {#view-results}

Om du loggar in på publiceringsinstansen som administratör, till exempel https://localhost:4503/crx/de som administratör/administratör, kan du kontrollera att de överliggande komponenterna finns där.

Om du loggar ut och sedan loggar in som `aaron.mcdonald@mailinator.com/password` och uppdaterar sidan, observerar du att en avatar inte visas med den publicerade kommentaren. Istället visas en enkel &#39;xxx&#39;.

![create-template-component](assets/create-template-component.png)
