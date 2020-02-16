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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Communities-meddelanden{#communities-notifications}

## Översikt {#overview}

AEM Communities tillhandahåller ett meddelandeavsnitt som visar händelser av intresse för den signerade communitymedlemmen.

Meddelanden liknar [aktiviteter](/help/communities/essentials-activities.md) och [prenumerationer](/help/communities/subscriptions.md) eftersom de kan vara ett resultat av

* Medlemmen publicerar innehåll
* medlemmen väljer att följa en annan medlem
* medlemmen väljer att följa specifika ämnen, artiklar och andra trådar med innehåll
* medlemstaggning (@mention) en annan community-medlem i ett användargenererat innehåll

Det som skiljer meddelanden från aktiviteter och prenumerationer är

* en länk till meddelandeavsnittet alltid finns i en communitysajts rubrik

   * aktiviteter kräver att [aktivitetsströmfunktionen](/help/communities/functions.md#activity-stream-function) inkluderas i communityplatsens struktur
   * prenumerationer kräver [konfigurering av e-post](/help/communities/email.md)

* implementeringen av meddelanden sker via skalbara och anslutningsbara kanaler

   * aktiviteter är bara tillgängliga på webben
   * prenumerationer är bara tillgängliga via e-post

Från och med Communities [FP1](/help/communities/deploy-communities.md#latestfeaturepack)är de tillgängliga meddelandekanalerna

* webbkanalen, som du kommer åt via `Notifications` länken
* e-postkanalen, tillgänglig när e-post har konfigurerats korrekt

Framtida kanaler är mobila och stationära.

### Krav {#requirements}

**Konfigurera e-post**

E-post måste konfigureras för att e-postkanalen ska fungera.

Instruktioner om hur du konfigurerar e-post finns i [Konfigurera e-post](/help/communities/analytics.md).

**Aktivera Följ**

Komponenter måste konfigureras för att aktivera följande. Funktioner som tillåter följande är [blogg](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [kalender](/help/communities/calendar.md), [filbibliotek](/help/communities/file-library.md)[](/help/communities/comments.md)och¥comments.

Observera att

* komponenter som används i [communitymallar](/help/communities/sites.md) och [gruppmallar](/help/communities/tools-groups.md) kan redan vara konfigurerade för att tillåta följande

* medlemsprofiler är redan konfigurerade så att andra medlemmar kan följa

## Meddelanden från följande {#notifications-from-following}

![chlimage_1-243](assets/chlimage_1-243.png)

Med knappen **Följ **gör du det möjligt att följa inmatningar som aktiviteter, prenumerationer och/eller meddelanden. Varje gång **Följ **knappen är markerad går det att aktivera eller inaktivera en markering. Markeringen visas bara när den är konfigurerad. `Email Subscriptions`

Om någon av följande metoder är markerad ändras texten för knappen till **Följ**. Du kan välja `Unfollow All` att inaktivera alla metoder.

Knappen **Följ **visas

* när du visar en annan medlems profil
* på en huvudfunktionssida, t.ex. forum, QnA och bloggar

   * följer all aktivitet för den allmänna funktionen

* för ett visst inlägg, t.ex. ett forumämne, en QnA-fråga eller en bloggartikel

   * följer all aktivitet för den specifika posten

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

Om du till exempel vill ändra omnämnanden i e-postmeddelanden (för en communitykomponent) lägger du till ett** if **condition for verb **mention** i mallarna för de komponenter som du aktiverade stödet för **@mentions** .

Om du vill ändra e-postmeddelandemallen för @mention i bloggkommentarer placerar du ut mallen utanför rutan på: **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

