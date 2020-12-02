---
title: Communities-meddelanden
seo-title: Communities-meddelanden
description: AEM Communities har meddelanden som visar händelser av intresse för den inloggade communitymedlemmen
seo-description: AEM Communities har meddelanden som visar händelser av intresse för den inloggade communitymedlemmen
uuid: 2f5ea4b5-7308-414e-a3f8-2e8aa76b1ef4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ab9088b7-a691-4153-ac82-1e8c0a19ed5d
docset: aem65
translation-type: tm+mt
source-git-commit: 5d196d1f6d5f94f2d3ef0d4461cfe38562f8ba8c
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 0%

---


# Communities Notifications {#communities-notifications}

## Översikt {#overview}

AEM Communities tillhandahåller ett meddelandeavsnitt som visar händelser av intresse för den signerade communitymedlemmen.

Meddelanden liknar [aktiviteter](/help/communities/essentials-activities.md) och [prenumerationer](/help/communities/subscriptions.md) eftersom de kan vara ett resultat av:

* Medlemmens bokföringsinnehåll.
* Medlemmen väljer att följa en annan medlem.
* Medlemmen väljer att följa specifika ämnen, artiklar och andra innehållstrådar.
* Medlemstaggningen (@mention) för en annan community-medlem i ett innehåll som skapats av en användare.

Det som skiljer meddelanden från aktiviteter och prenumerationer är:

* En länk till meddelandeavsnittet finns alltid i en communitysajts rubrik:

   * Aktiviteter kräver att funktionen [aktivitetsström](/help/communities/functions.md#activity-stream-function) inkluderas i communityplatsens struktur.
   * Prenumerationer kräver [konfigurering av e-post](/help/communities/email.md).

* Implementeringen av meddelanden sker via skalbara och anslutningsbara kanaler:

   * Aktiviteter är bara tillgängliga på webben.
   * Prenumerationer är bara tillgängliga via e-post.

Från och med Communities [FP1](/help/communities/deploy-communities.md#latestfeaturepack) är de tillgängliga meddelandekanalerna:

* Webbkanalen som nås via länken `Notifications`.
* E-postkanalen, som är tillgänglig när e-post har konfigurerats korrekt.

Framtida kanaler är mobila och stationära.

### Krav {#requirements}

**Konfigurera e-post**

E-post måste konfigureras för att e-postkanalen ska fungera.

Instruktioner om hur du konfigurerar e-post finns i [Konfigurera e-post](/help/communities/analytics.md).

**Aktivera Följ**

Komponenter måste konfigureras för att aktivera följande. Följande funktioner tillåter [blogg](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [kalender](/help/communities/calendar.md), [filelibrary](/help/communities/file-library.md) och [kommentarer](/help/communities/comments.md).

**Obs**:

* Komponenter som används i community [webbplatsmallar](/help/communities/sites.md) och [gruppmallar](/help/communities/tools-groups.md) kan redan vara konfigurerade att följa efter.

* Medlemsprofiler är redan konfigurerade så att andra medlemmar kan följa efter.

## Meddelanden från följande {#notifications-from-following}

![meddelanden](assets/notifications.png)

Med knappen **[!UICONTROL Follow]** kan du följa upp aktiviteter, prenumerationer och/eller meddelanden. Varje gång knappen **[!UICONTROL Follow]** är markerad går det att aktivera eller inaktivera en markering. Markeringen `Email Subscriptions` finns bara när den är konfigurerad.

Om någon av följande metoder är markerad ändras knappens text till **[!UICONTROL Following]**. Du kan av praktiska skäl välja `Unfollow All` för att inaktivera alla metoder.

Knappen **[!UICONTROL Follow]** visas:

* När en annan medlems profil visas.
* På en huvudfunktionssida, till exempel forum, QnA och bloggar:

   * Följer alla aktiviteter för den allmänna funktionen.

* För ett visst inlägg, t.ex. ett forumämne, en QnA-fråga eller en bloggartikel:

   * Följer all aktivitet för den specifika posten.

## Hantera meddelandeinställningar {#managing-notification-settings}

Genom att välja länken Meddelandeinställningar på meddelandesidan kan varje medlem hantera hur meddelanden tas emot.

Webbkanalen är alltid aktiverad.

![meddelanden14](assets/notifications1.png)

E-postkanalen, som är beroende av rätt [konfiguration av e-post](/help/communities/email.md), innehåller samma inställningar som för webbkanalen.

E-postkanalen är inaktiverad som standard.

![meddelanden2](assets/notifications2.png)

Den kan vara aktiverad av en medlem, men är ändå beroende av att e-post konfigureras.

![meddelanden3](assets/notifications3.png)

## Visa meddelanden {#viewing-notifications}

### Webbmeddelanden {#web-notifications}

En [guide skapade en communityplats](/help/communities/sites-console.md) innehåller nu en länk till funktionen `Notifications` i webbplatsens rubrikfält ovanför banderollen. Till skillnad från meddelanden skapas meddelanden för alla communitysajter, medan meddelanden måste aktiveras när webbplatsen skapas.

När du går till den publicerade webbplatsen och väljer länken `Notifications` visas alla meddelanden för medlemmen.

![meddelanden4](assets/notifications4.png)

### E-postmeddelanden {#email-notifications}

När e-postkanalen är aktiverad får medlemmen ett e-postmeddelande som innehåller en länk till innehållet på webben.

![meddelanden5](assets/notifications5.png)

## Anpassa e-postmeddelanden {#customize-email-notifications}

Organisationer kan anpassa e-postmeddelanden genom att [lägga över](/help/communities/client-customize.md#overlays) mallarna på **/libs/settings/community/templates/email/html**.

Om du till exempel vill ändra e-postmeddelandena om omnämnanden (för en community-komponent) lägger du till ett **if**-villkor för verb **mention** i mallarna för de komponenter som du aktiverade stödet för **@omnämns**.

Om du vill ändra e-postmeddelandemallen för @mention i bloggkommentarer placerar du ut mallen utanför rutan på: **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

