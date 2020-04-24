---
title: Ändra utseendet
seo-title: Ändra utseendet
description: Ändra skriptet
seo-description: Ändra skriptet
uuid: 30555b9f-da29-4115-9ed5-25f80a247bd6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: c9d31ed8-c105-453b-bd3c-4660dfd81272
docset: aem65
translation-type: tm+mt
source-git-commit: 48afa2146d0dcbab4beaa1044645c269b49fd7ff

---


# Ändra utseendet {#alter-the-appearance}

## Ändra skriptet {#modify-the-script}

Skriptet comment.hbs ansvarar för att skapa den övergripande HTML-koden för varje kommentar.

Så här visar du inte avataren bredvid varje publicerad kommentar:

1. Kopiera `comment.hbs`från `libs`till `apps`

   1. Välj `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. Markera **kopia**
   1. Välj `/apps/social/commons/components/hbs/comments/comment`
   1. Markera **Klistra in**

1. Öppna överlägg `comment.hbs`

   * Dubbelklicka på noden `comment.hbs` i `/apps/social/commons/components/hbs/comments/comment folder`

1. Hitta följande rader och ta bort eller kommentera dem:

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

Radera raderna eller omge dem med `<!--` och kommentera `-->` ut dem. Dessutom läggs tecknen &#39;xxx&#39; till som en visuell indikator på var avataren skulle ha varit.

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


I den globala navigeringen väljer du **[!UICONTROL Verktyg]** > **[!UICONTROL Distribution]** > **[!UICONTROL Replikering]** och klickar på **[!UICONTROL Aktivera träd]**.

Ange `/apps/social/commons` och välj **[!UICONTROL Aktivera]** som startsökväg.

![chlimage_1-77](assets/chlimage_1-77.png)

### Visa resultat {#view-results}

Om du loggar in på publiceringsinstansen som administratör, t.ex. https://localhost:4503/crx/de som administratör/administratör, kan du verifiera att de överliggande komponenterna finns där.

Om du loggar ut och loggar in igen som `aaron.mcdonald@mailinator.com/password` och uppdaterar sidan, kommer du att märka att den publicerade kommentaren inte längre visas med en avatar, i stället visas en enkel &#39;xxx&#39;.

![chlimage_1-78](assets/chlimage_1-78.png)

