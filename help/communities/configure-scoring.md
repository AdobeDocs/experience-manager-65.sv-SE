---
title: Grundläggande om poäng och emblem
seo-title: Grundläggande om poäng och emblem
description: Betygsättning och märkning - funktionsöversikt
seo-description: Betygsättning och märkning - funktionsöversikt
uuid: 6e3af071-04e8-4dc1-977a-0da711b72961
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 628b6dcd-8b1c-4166-8fc2-843baa86ac1c
docset: aem65
translation-type: tm+mt
source-git-commit: bc49aaad1f55b8c70228d3c800f1e5abf8a2519c
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 0%

---


# Grundläggande om poäng och emblem {#scoring-and-badges-essentials}

Funktionen AEM Communities-poäng och -badges gör det möjligt att identifiera och belöna communitymedlemmar.

Information om hur du konfigurerar funktionen finns i

* [Communities Scoring and Badges](/help/communities/implementing-scoring.md)

Den här sidan innehåller ytterligare teknisk information:

* Så här [visar du ett märke](#displaying-badges) som bild eller text
* Aktivera omfattande [felsökningsloggning](#debug-log-for-scoring-and-badging)
* Så här [får du åtkomst till UGC](#ugc-for-scoring-and-badging) för bedömning och märkning

>[!CAUTION]
>
>Implementeringsstrukturen som visas i CRXDE Lite kan komma att ändras.

## Visar emblem {#displaying-badges}

Om ett märke visas som text eller bild styrs på klientsidan i HBS-mallen.

Sök till exempel efter `this.isAssigned` i `/libs/social/forum/components/hbs/topic/list-item.hbs`:

```
{{#each author.badges}}

  {{#if this.isAssigned}}

    <div class="scf-badge-text">

      {{this.title}}

    </div>

  {{/if}}

{{/each}}

{{#each author.badges}}

  {{#unless this.isAssigned}}

    <img class="scf-badge-image" alt="{{this.title}}" title="{{this.title}}" src="{{this.imageUrl}}" />

  {{/unless}}

{{/each}}
```

Om värdet är true anger isAssigned att märket har tilldelats en roll och att märket ska visas som text.

Om värdet är false anges märket Tilldelad att märket tilldelats för ett upparbetat resultat och att märket ska visas som en bild.

Alla ändringar av detta beteende bör göras i ett anpassat skript (antingen åsidosätt eller övertäckning). Se Anpassa [på klientsidan](/help/communities/client-customize.md).

## Felsökningslogg för poängsättning och märkning {#debug-log-for-scoring-and-badging}

En anpassad loggfil kan konfigureras för felsökning av poängsättning och badging. Innehållet i loggfilen kan sedan tillhandahållas kundsupporten om problem uppstår med funktionen.

Detaljerade anvisningar finns i [Skapa en anpassad loggfil](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).

Så här konfigurerar du snabbt en slinglog-fil:

1. Få åtkomst till loggstödet **för** Adobe Experience Manager Web Console, till exempel

   * https://localhost:4502/system/console/slinglog

1. Välj **Lägg till ny loggare**

   1. Välj `DEBUG` för **loggnivå**

   1. Ange ett namn för **loggfilen**, till exempel

      * logs/scoring-debug.log
   1. Ange två **Logger** -poster (klass) (med `+` ikon)

      * `com.adobe.cq.social.scoring`
      * `com.adobe.cq.social.badging`
   1. Välj **Spara**



![chlimage_1-193](assets/chlimage_1-193.png)

Så här visar du loggposter:

* Från webbkonsolen

   * Under menyn **Status**
   * Välj **loggfiler**
   * Sök efter loggfilens namn, till exempel `scoring-debug`

* På serverns lokala disk

   * Loggfilen finns på &lt;*server-install-dir*>/crx-quickstart/logs/&lt;*log-file-name*>.log

   * Till exempel, `.../crx-quickstart/logs/scoring-debug.log`

![chlimage_1-194](assets/chlimage_1-194.png)

## UGC för poängsättning och märkning {#ugc-for-scoring-and-badging}

Det går att visa användargenererat innehåll som är relaterat till poängsättning och märkning när den valda SRP är antingen JSRP eller MSRP, men inte ASRP. (Om du inte känner till dessa termer läser du Översikt över [Community Content Storage](/help/communities/working-with-srp.md) and [Storage Resource Provider](/help/communities/srp.md).)

Beskrivningarna för att komma åt betygs- och badging-data använder JSRP, eftersom UGC är lätt att komma åt med [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

**JSRP on author**: när du experimenterar i redigeringsmiljön resulterar det i användargenererat innehåll som bara är synligt från författarmiljön.

**JSRP vid publicering**: På samma sätt måste du vid testning i publiceringsmiljön få tillgång till CRXDE Lite med administratörsbehörighet för en publiceringsinstans. Om publiceringsinstansen körs i [produktionsläge](/help/sites-administering/production-ready.md) (noSampleContent Runmode) måste du [aktivera CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

UGC:s basplats på JSRP är `/content/usergenerated/asi/jcr/`.

### API:er för klassificering och märkning {#scoring-and-badging-apis}

Följande API:er kan användas:

* [com.adobe.cq.social.scoring.api](https://docs.adobe.com/content/docs/en/aem/6-3/develop/ref/javadoc/com/adobe/cq/social/scoring/api/package-summary.html)
* [com.adobe.cq.social.badging.api](https://docs.adobe.com/content/docs/en/aem/6-3/develop/ref/javadoc/com/adobe/cq/social/badging/api/package-summary.html)

De senaste Javadocs-filerna för det installerade funktionspaketet är tillgängliga för utvecklare från Adobe-databasen. Se [Använda Maven for Communities: Javadocs](/help/communities/maven.md#javadocs).

**Platsen och formatet för användargenererat innehåll i databasen kan ändras utan förvarning**.

### Exempelinställningar {#example-setup}

Skärmbilderna av databasdata kommer från att konfigurera poängsättning och märkning för ett forum på två olika AEM-webbplatser:

1. En AEM-webbplats *med* ett unikt ID (communitywebbplats skapad med guide):

   * Använda självstudiekursen Komma igång (engagera) som skapades under självstudiekursen [Komma igång](/help/communities/getting-started.md)
   * Hitta forumsidnoden

      `/content/sites/engage/en/forum/jcr:content`

   * Lägga till egenskaper för poängsättning och märkning

   ```
   scoringRules = [/etc/community/scoring/rules/comments-scoring,
   /etc/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/etc/community/badging/rules/comments-scoring,
   /etc/community/badging/rules/forums-scoring]
   ```

   * Hitta forumkomponentnoden

      `/content/sites/engage/en/forum/jcr:content/content/primary/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * Lägg till egenskap för att visa emblem

      `allowBadges = true`

   * En användare loggar in, skapar ett forumämne och tilldelas ett bronze-märke


1. En AEM-webbplats *utan* unikt ID:

   * Använda guiden [Community Components](/help/communities/components-guide.md)
   * Hitta forumsidnoden

      `/content/community-components/en/forum/jcr:content`

   * Lägga till egenskaper för poängsättning och märkning

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /etc/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-badging,
   /libs/settings/community/badging/rules/forums-badging]
   ```

   * Hitta forumkomponentnoden

      `/content/community-components/en/forum/jcr:content/content/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * Lägg till egenskap för att visa emblem

      `allowBadges = true`

   * En användare loggar in, skapar ett forumämne och tilldelas ett bronze-märke


1. En användare tilldelas ett moderatormärke med cURL:

   ```shell
   curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/etc/community/badging/images/moderator/jcr:content/moderator.png" https://localhost:4503/home/users/community/w271OOup2Z4DjnOQrviv/profile.social.json
   ```

   När en användare har fått två bronze-märken och tilldelats ett moderatormärke, är det så här användaren visas med sitt foruminlägg.

![chlimage_1-195](assets/chlimage_1-195.png)

>[!NOTE]
>
>Det här exemplet följer inte följande metodtips:
>
>* Poängregelnamnen ska vara globalt unika. de ska inte sluta med samma namn.
   >  Ett exempel på vad som *inte* ska göras:
   >  /etc/community/scoring/rules/site1/forums-scoring
   >  /etc/community/scoring/rules/site2/forums-scoring
   >
   >
* Skapa unika märkesbilder för olika AEM-webbplatser
>



### UGC för åtkomstbedömning {#access-scoring-ugc}

Du bör använda [API:erna](#scoring-and-badging-apis) .

I undersökningssyfte, till exempel med JSRP, är baskamappen som innehåller poäng

* `/content/usergenerated/asi/jcr/scoring`

Den underordnade noden för `scoring` är resultatregelns namn. Det bästa sättet är alltså att betygsregelnamn på en server är globalt unika.

För Geometrixx Engage-webbplatsen finns användaren och poängen i en sökväg som är konstruerad med namnet på bedömningsregeln, communityplatsens webbplats-ID ( `engage-ba81p`), ett unikt ID och användarens ID:

* `.../scoring/forums-scoring/engage-ba81p/6d179715c0e93cb2b20886aa0434ca9b5a540401/riley`

För stödwebbplatsen för Community Components är användaren och poängen i en sökväg som konstruerats med resultatregelnamnet, ett standard-ID ( `default-site`), ett unikt ID och användarens ID:

* `.../scoring/forums-scoring/default-site/b27a17cb4910a9b69fe81fb1b492ba672d2c086e/riley`

Ljudspåret lagras i egenskapen `scoreValue_tl` som bara kan innehålla ett värde eller indirekt referera till en atomicCounter.

![chlimage_1-196](assets/chlimage_1-196.png)

### Access Badging UGC {#access-badging-ugc}

Du bör använda [API:erna](#scoring-and-badging-apis) .

I undersökningssyfte, till exempel med JSRP, är baskappen som innehåller information om tilldelade eller tilldelade märken

* `/content/usergenerated/asi/jcr`

Följs av sökvägen till användarens profil och avslutas i en badges-mapp, till exempel

* `/home/users/community/w271OOup2Z4DjnOQrviv/profile/badges`

#### Tilldelad bricka {#awarded-badge}

![chlimage_1-197](assets/chlimage_1-197.png)

#### Tilldelat märke {#assigned-badge}

![chlimage_1-198](assets/chlimage_1-198.png)

## Additional Information {#additional-information}

Så här visar du en sorterad lista med medlemmar baserat på punkter:

* [Ledarpanelsfunktion](/help/communities/functions.md#leaderboard-function) för att ingå i en communitywebbplats eller gruppmall.
* [Leaderboard-komponenten](/help/communities/enabling-leaderboard.md), den komponent som finns i Leaderboard-funktionen, för framtagning av sidor.

