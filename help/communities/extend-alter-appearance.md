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
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# Ändra utseendet (HBS) {#alter-the-appearance-hbs}

Nu när komponenterna för det anpassade kommentarsystemet i programkatalogen (/apps) finns på plats, med en resourceSuperType som refererar till standardkommentarsystemet och den anpassade modellen/vyn registrerad, är det möjligt att ändra implementeringen.

För en enkel demonstration, en visuell funktion, tas den avatar som visas för den inloggade användaren som skickar en kommentar bort.

>[!NOTE]
>
>Om du vill använda tillägget måste instansen av kommentarsystemet på en webbplats som ska påverkas (/content) ange att dess resourceType ska vara det anpassade kommentarsystemet.

## Ändra HBS-skript {#modify-the-hbs-scripts}

Använda [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Open [/apps/custom/components/comments/comment/**comment.hbs **](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * kommentera taggen som innehåller avataren för ett kommentarinlägg (~ line 21):

      ```
      <!--
       <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
       -->
      ```

* Open [/apps/custom/components/comments/**comments.hbs **](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * kommentera taggen som innehåller avataren för nästa kommentarspost (~ line 44):

      ```
      <!--
       <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
       -->
      ```

* Välj **Spara alla**

### Replikera anpassad app {#replicate-custom-app}

När programmet har ändrats måste den anpassade komponenten replikeras om.

Ett sätt att göra detta är att

* Från huvudmenyn

   * välj **Verktyg > Åtgärder > Replikering**
   * select `Activate Tree`
   * uppsättning `Start Path`: till `/apps/custom`
   * avmarkera `Only Modified`
   * välj `Activate`knapp

### Visa ändrad kommentar på publicerad exempelsida {#view-modified-comment-on-published-sample-page}

[Nu kan du uppdatera sidan i publiceringsmiljön och visa ändringen för att ta bort avataren genom att fortsätta med upplevelsen](/help/communities/extend-sample-page.md#publish-sample-page) på publiceringsinstansen, som fortfarande är inloggad som samma användare:

![chlimage_1-136](assets/chlimage_1-136.png)

### Exempel på kommentartillägg {#sample-comment-extension-package}

Bifogat är ett paket med det anpassade kommentarprogrammet som skapas i den här självstudiekursen.

[Hämta fil](assets/sample-comment-extension-6-1-fp3.zip)
