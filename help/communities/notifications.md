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
source-git-commit: 22e853ecaf2696c7329a81bb9d375b1dbc74452c

---


# Communities-meddelanden {#communities-notifications}

## Översikt {#overview}

AEM Communities tillhandahåller ett meddelandeavsnitt som visar händelser av intresse för den signerade communitymedlemmen.

Meddelanden liknar [aktiviteter](/help/communities/essentials-activities.md) och [prenumerationer](/help/communities/subscriptions.md) eftersom de kan härröra från:

* Medlemmens bokföringsinnehåll.
* Medlemmen väljer att följa en annan medlem.
* Medlemmen väljer att följa specifika ämnen, artiklar och andra innehållstrådar.
* Medlemstaggningen (@mention) för en annan community-medlem i ett innehåll som skapats av en användare.

Det som skiljer meddelanden från aktiviteter och prenumerationer är:

* En länk till meddelandeavsnittet finns alltid i en communitysajts rubrik:

   * Aktiviteter kräver att [aktivitetsströmsfunktionen](/help/communities/functions.md#activity-stream-function) inkluderas i communityplatsens struktur.
   * Prenumerationer kräver [konfigurering av e-post](/help/communities/email.md).

* Implementeringen av meddelanden sker via skalbara och anslutningsbara kanaler:

   * Aktiviteter är bara tillgängliga på webben.
   * Prenumerationer är bara tillgängliga via e-post.

Från och med Communities [FP1](/help/communities/deploy-communities.md#latestfeaturepack)är de tillgängliga meddelandekanalerna:

* Webbkanalen som du kommer åt via `Notifications` länken.
* E-postkanalen, som är tillgänglig när e-post har konfigurerats korrekt.

Framtida kanaler är mobila och stationära.

### Krav {#requirements}

**Konfigurera e-post**

E-post måste konfigureras för att e-postkanalen ska fungera.

Instruktioner om hur du konfigurerar e-post finns i [Konfigurera e-post](/help/communities/analytics.md).

**Aktivera Följ**

Komponenter måste konfigureras för att aktivera följande. Funktioner som tillåter följande är [blogg](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [kalender](/help/communities/calendar.md), [filbibliotek](/help/communities/file-library.md)[](/help/communities/comments.md)och¥comments.

**Obs**:

* Komponenter som används i [communitymallar](/help/communities/sites.md) och [gruppmallar](/help/communities/tools-groups.md) kanske redan är konfigurerade att följa efter.

* Medlemsprofiler är redan konfigurerade så att andra medlemmar kan följa efter.

## Meddelanden från följande {#notifications-from-following}

![chlimage_1-243](assets/chlimage_1-243.png)

Med knappen **[!UICONTROL Följ]** kan du följa inmatningar som aktiviteter, prenumerationer och/eller meddelanden. Varje gång knappen **[!UICONTROL Följ]** är markerad går det att aktivera eller inaktivera en markering. Markeringen visas bara när den är konfigurerad. `Email Subscriptions`

Om någon av följande metoder är markerad ändras texten för knappen till **[!UICONTROL Följ]**. Du kan välja `Unfollow All` att inaktivera alla metoder.

Knappen **[!UICONTROL Följ]** visas:

* När en annan medlems profil visas.
* På en huvudfunktionssida, till exempel forum, QnA och bloggar:

   * Följer alla aktiviteter för den allmänna funktionen.

* För ett visst inlägg, t.ex. ett forumämne, en QnA-fråga eller en bloggartikel:

   * Följer all aktivitet för den specifika posten.

## Hantera meddelandeinställningar {#managing-notification-settings}

Genom att välja länken Meddelandeinställningar på meddelandesidan kan varje medlem hantera hur meddelanden tas emot.

Webbkanalen är alltid aktiverad.

![chlimage_1-244](assets/chlimage_1-244.png)

E-postkanalen, som bygger på rätt [konfiguration av e-post](/help/communities/email.md), ger samma inställningar som för webbkanalen.

E-postkanalen är inaktiverad som standard.

![chlimage_1-245](assets/chlimage_1-245.png)

Den kan vara aktiverad av en medlem, men är ändå beroende av att e-post konfigureras.

![chlimage_1-246](assets/chlimage_1-246.png)

## Visa meddelanden {#viewing-notifications}

### Webbmeddelanden {#web-notifications}

En [guide skapade en communitywebbplats](/help/communities/sites-console.md) innehåller nu en länk till `Notifications` funktionen i webbplatsens sidhuvud ovanför banderollen. Till skillnad från meddelanden skapas meddelanden för alla communitysajter, medan meddelanden måste aktiveras när webbplatsen skapas.

När du besöker den publicerade webbplatsen visas alla meddelanden för medlemmen om du väljer `Notifications` länken.

![chlimage_1-247](assets/chlimage_1-247.png)

### E-postmeddelanden {#email-notifications}

När e-postkanalen är aktiverad får medlemmen ett e-postmeddelande som innehåller en länk till innehållet på webben.

![chlimage_1-248](assets/chlimage_1-248.png)

## Anpassa e-postmeddelanden {#customize-email-notifications}

Organisationer kan anpassa e-postmeddelandena genom att [täcka över](/help/communities/client-customize.md#overlays) mallarna på **/libs/settings/community/templates/email/html**.

Om du till exempel vill ändra omnämns e-postmeddelanden (för en community-komponent) lägger du till ett **if** -villkor för verb- **omnämnande** i mallarna för de komponenter som du aktiverade stödet för **@omnämns** .

Om du vill ändra e-postmeddelandemallen för @mention i bloggkommentarer placerar du ut mallen utanför rutan på: **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

