---
title: Communities-prenumerationer
description: Medlemmar i communityn interagerar med andra medlemmar via e-post
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 338be220-659a-459c-8e90-55e3a11ddeb0
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Communities-prenumerationer {#communities-subscriptions}

## Ökning {#overview}

Från och med Communities [FP1](deploy-communities.md#latestfeaturepack) kan communitymedlemmar interagera med communityn via e-post med en funktion som kallas prenumerationer.

Prenumerationer liknar [meddelanden](notifications.md) eftersom medlemmar kan prenumerera när de följer bloggartiklar, forumämnen eller frågor om Frågor och svar.

Det som skiljer prenumerationer från meddelanden är:

* Medlemmar får inte prenumerera när de följer efter andra medlemmar.
* Den enda åtgärd som medlemmar kan utföra är att välja `Email Subscriptions` när de följer.
* När e-postsvar har konfigurerats kan medlemmar effektivt publicera innehåll genom att helt enkelt svara på det mottagna e-postmeddelandet.

### Krav {#requirements}

**Konfigurera e-post**

E-post måste konfigureras för att prenumerationerna ska fungera och för att medlemmarna ska kunna svara via e-post.

Instruktioner om hur du konfigurerar e-post finns i [Konfigurera e-post](email.md).

**Aktivera prenumerationer och följ**

Komponenter måste konfigureras för att aktivera prenumerationer *och* efter. Funktioner som tillåter prenumerationer är [blogg](blog-feature.md), [forum](forum.md) och [QnA](working-with-qna.md).

## Prenumerationer från följande {#subscriptions-from-following}

![prenumerationsföljande](assets/subscription-following.png)

Med knappen **Följ** kan du följa upp aktiviteter, prenumerationer och/eller meddelanden. Varje gång knappen **Följ** är markerad går det att aktivera eller inaktivera en markering.

Om någon av följande metoder är markerad ändras texten för knappen till **Efter**. Det går att välja `Unfollow All` för att inaktivera alla metoder.

Knappen **Följ** kommer endast att innehålla alternativet `Email Subscriptions` när ett forum, QnA eller blogg har konfigurerats för att aktivera e-postprenumerationer. Den här knappen visas:

* På huvudfunktionssidan för det aktiverade forumet, QnA eller bloggen Kommer att skicka ett e-postmeddelande för all aktivitet under den funktionen.

* För ett visst inlägg, t.ex. ett forumämne, QnA-fråga eller bloggartikel Skickar ett e-postmeddelande när det finns aktivitet för det aktuella inlägget.

## Svara via e-post {#reply-by-email}

När e-postmeddelandet är [konfigurerat för att svara via e-post](email.md#configure-polling-importer) får den medlem som prenumererade ett e-postmeddelande med det publicerade innehållet och en länk till onlineinnehållet.

Om de svarar på e-postmeddelandet visas det innehåll de anger i svaret som innehåll online.

![email-reply](assets/email-reply.png)

Hur lång tid det tar för ett svar att bokföras styrs av [avsökningimporterarens uppdateringsintervall](email.md#configure-polling-importer).

![QA](assets/qa.png)
