---
title: Ändra utseende (HBS)
description: Lär dig hur du ändrar utseendet (HBS) genom att redigera HBS-skripten.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 27e1bff3-385e-4ced-87af-54044b7e8812
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Ändra utseende (HBS) {#alter-the-appearance-hbs}

Nu när komponenterna för det anpassade kommentarsystemet i programkatalogen (/apps) finns på plats, med en resourceSuperType som refererar till standardkommentarsystemet och den anpassade modellen/vyn registrerad, kan du redigera implementeringen.

För en enkel demonstration, en visuell funktion, tas den avatar som visas för den inloggade användaren som skickar en kommentar bort.

>[!NOTE]
>
>Om du vill använda tillägget måste instansen av kommentarsystemet på en webbplats som ska påverkas (/content) ange att dess resourceType ska vara det anpassade kommentarsystemet.

## Ändra HBS-skript {#modify-the-hbs-scripts}

Använda [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Öppna [/apps/custom/components/comments/comment/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * Kommentera taggen som innehåller avataren för ett kommentarinlägg (~ line 21):

     ```
       <!--
        <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
        -->
     ```

* Öppna [/apps/custom/components/comments/**kommentarer.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * Kommentera taggen som innehåller avataren för nästa kommentarspost (~ line 44):

     ```
       <!--
        <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
        -->
     ```

* Välj **Spara alla**

### Replikera anpassad app {#replicate-custom-app}

När programmet har ändrats måste den anpassade komponenten replikeras om.

Ett sätt är att

* Från huvudmenyn

   * Välj **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Replication]**.
   * Välj **[!UICONTROL Activate Tree]**.
   * Ange `Start Path` till `/apps/custom`.
   * Avmarkera **[!UICONTROL Only Modified]**.
   * Välj **[!UICONTROL Activate]** -knappen.

### Visa ändrad kommentar på publicerad exempelsida {#view-modified-comment-on-published-sample-page}

[Fortsätta upplevelsen](/help/communities/extend-sample-page.md#publish-sample-page) i publiceringsinstansen, som fortfarande är inloggad som samma användare, är det nu möjligt att uppdatera sidan i publiceringsmiljön för att visa ändringen för att ta bort avataren:

![view-modified-content](assets/view-modified-content.png)

### Exempel på kommentartillägg {#sample-comment-extension-package}

Bifogat är ett paket med det anpassade kommentarprogrammet som skapas i den här självstudiekursen.

[Hämta fil](assets/sample-comment-extension-6-1-fp3.zip)
