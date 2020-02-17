---
title: Communities-prenumerationer
seo-title: Communities-prenumerationer
description: Medlemmar i communityn interagerar med andra medlemmar via e-post
seo-description: Medlemmar i communityn interagerar med andra medlemmar via e-post
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Communities-prenumerationer {#communities-subscriptions}

## Översikt {#overview}

Från och med Communities [FP1](deploy-communities.md#latestfeaturepack)kan communitymedlemmar interagera med communityn via e-post med en funktion som kallas prenumerationer.

Prenumerationer liknar [meddelanden](notifications.md) , eftersom medlemmar kan prenumerera när de följer bloggartiklar, forumämnen eller frågor om Frågor och svar.

Det som skiljer prenumerationer från meddelanden är:

* Medlemmar får inte prenumerera efter andra medlemmar
* Den enda åtgärd som medlemmar kan utföra är att välja `Email Subscriptions` när de följer
* När e-postsvar har konfigurerats kan medlemmar effektivt publicera innehållet genom att helt enkelt svara på det mottagna e-postmeddelandet

### Krav {#requirements}

**Konfigurera e-post**

E-post måste konfigureras för att prenumerationerna ska fungera och för att medlemmarna ska kunna svara via e-post.

Instruktioner om hur du konfigurerar e-post finns i [Konfigurera e-post](email.md).

**Aktivera prenumerationer och följ**

Komponenter måste konfigureras för att aktivera prenumerationer *och* följande. Funktioner som tillåter prenumerationer är [blogg](blog-feature.md), [forum](forum.md) och [QnA](working-with-qna.md).

## Prenumerationer från följande {#subscriptions-from-following}

![chlimage_1-5](assets/chlimage_1-5.png)

Med knappen **Följ** kan du följa inmatningar som aktiviteter, prenumerationer och/eller meddelanden. Varje gång knappen **Följ** är markerad går det att aktivera eller inaktivera en markering.

Om någon av följande metoder är markerad ändras texten för knappen till **Följ**. Du kan välja `Unfollow All` att inaktivera alla metoder.

Knappen **Följ** kommer endast att innehålla `Email Subscriptions` alternativet när ett forum, QnA eller blogg har konfigurerats för att aktivera e-postprenumerationer. Den här knappen visas

* På huvudfunktionssidan för det aktiverade forumet, QnA eller bloggen

   * Skickar ett e-postmeddelande för all aktivitet under den funktionen

* För ett visst inlägg, t.ex. ett forumämne, en QnA-fråga eller en bloggartikel

   * Skickar ett e-postmeddelande när det finns aktivitet för det specifika inlägget

## Svara via e-post {#reply-by-email}

När e-post är [konfigurerad för att svara via e-post](email.md#configure-polling-importer)får den medlem som prenumererar ett e-postmeddelande med det publicerade innehållet och en länk till onlineinnehållet.

Om de svarar på e-postmeddelandet visas det innehåll de anger i svaret som innehåll online.

![chlimage_1-6](assets/chlimage_1-6.png)

Hur lång tid det tar för ett svar att bokföras styrs av [avsökningimporterarens uppdateringsintervall](email.md#configure-polling-importer).

![chlimage_1-7](assets/chlimage_1-7.png)

