---
title: Ändra utseendet (HBS)
seo-title: Ändra utseendet
description: Ändra HBS-skript
seo-description: Ändra HBS-skript
uuid: cff24505-dbb3-4312-9b1b-c1693b8d1c98
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e0da09b3-725d-4ed1-9273-2532132f6918
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# Ändra utseende (HBS) {#alter-the-appearance-hbs}

Nu när komponenterna för det anpassade kommentarsystemet i programkatalogen (/apps) finns på plats, med en resourceSuperType som refererar till standardkommentarsystemet och den anpassade modellen/vyn registrerad, är det möjligt att ändra implementeringen.

För en enkel demonstration, en visuell funktion, tas den avatar som visas för den inloggade användaren som skickar en kommentar bort.

>[!NOTE]
>
>Om du vill använda tillägget måste instansen av kommentarsystemet på en webbplats som ska påverkas (/content) ange att dess resourceType ska vara det anpassade kommentarsystemet.

## Ändra HBS-skripten {#modify-the-hbs-scripts}

Använda [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Öppna [/apps/custom/components/comments/comment/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * Kommentera taggen som innehåller avataren för ett kommentarinlägg (~ line 21):

      ```
        <!--
         <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
         -->
      ```

* Öppna [/apps/custom/components/comments/**comments.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

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
   * Välj **[!UICONTROL Activate]**-knappen.

### Visa ändrad kommentar på publicerad exempelsida {#view-modified-comment-on-published-sample-page}

[När ](/help/communities/extend-sample-page.md#publish-sample-page) upplevelsen av publiceringsinstansen fortsätter, som fortfarande är inloggad som samma användare, går det nu att uppdatera sidan i publiceringsmiljön för att visa ändringen för att ta bort avataren:

![view-modified-content](assets/view-modified-content.png)

### Exempel på kommentartillägg {#sample-comment-extension-package}

Bifogat är ett paket med det anpassade kommentarprogrammet som skapas i den här självstudiekursen.

[Hämta fil](assets/sample-comment-extension-6-1-fp3.zip)
