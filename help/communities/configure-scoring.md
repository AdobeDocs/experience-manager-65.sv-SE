---
title: Grundläggande om poäng och emblem
description: Läs om hur Adobe Experience Manager Communities-funktionen poäng och badges identifierar och belönar communitymedlemmar.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 470a382a-2aa7-449e-bf48-b5a804c5b114
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# Grundläggande om poäng och emblem {#scoring-and-badges-essentials}

AEM Communities poäng och brickor identifierar och belönar communitymedlemmar.

Information om hur du konfigurerar funktionen finns i

* [Communities Scoring and Badges](/help/communities/implementing-scoring.md)

Den här sidan innehåller ytterligare teknisk information:

* [Visa ett märke](#displaying-badges) som bild eller text
* Så här aktiverar du omfattande [felsökningsloggning](#debug-log-for-scoring-and-badging)
* Så här [får du åtkomst till UGC](#ugc-for-scoring-and-badging) för poäng och badging

>[!CAUTION]
>
>Den implementeringsstruktur som visas i CRXDE Lite kan komma att ändras.

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

Om värdet är true anger `isAssigned` att märket har tilldelats en roll och att märket ska visas som text.

Om värdet är false anger `isAssigned` att märket har tilldelats för ett upparbetat poäng och att märket ska visas som en bild.

Alla ändringar av detta beteende bör göras i ett anpassat skript (antingen åsidosätt eller övertäckning). Se [Anpassning på klientsidan](/help/communities/client-customize.md).

## Felsökningslogg för poängsättning och märkning {#debug-log-for-scoring-and-badging}

En anpassad loggfil kan konfigureras för felsökning av poängsättning och badging. Innehållet i loggfilen kan sedan tillhandahållas kundsupporten om problem uppstår med funktionen.

Detaljerade instruktioner finns på [Skapa en anpassad loggfil](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).

Så här konfigurerar du snabbt en slinglog-fil:

1. Få åtkomst till loggstödet för **Adobe Experience Manager Web Console**, till exempel

   * https://localhost:4502/system/console/slinglog

1. Välj **Lägg till ny loggare**

   1. Välj `DEBUG` för **Loggnivå**

   1. Ange ett namn för **loggfilen**, till exempel

      * logs/scoring-debug.log

   1. Ange två **Logger**-poster (klass) (med ikonen `+` )

      * `com.adobe.cq.social.scoring`
      * `com.adobe.cq.social.badging`

   1. Välj **Spara**

![debug-scoring-log](assets/debug-scoring-log.png)

Så här visar du loggposter:

* Från webbkonsolen

   * Under menyn **Status**
   * Välj **Loggfiler**
   * Sök efter loggfilens namn, till exempel `scoring-debug`

* På serverns lokala disk

   * Loggfilen finns på &lt;*server-install-dir*>/crx-quickstart/logs/&lt;*log-file-name*>.log

   * Exempel: `.../crx-quickstart/logs/scoring-debug.log`

![poänglogg](assets/scoring-log.png)

## UGC för poängsättning och märkning {#ugc-for-scoring-and-badging}

Det går att visa användargenererat innehåll som är relaterat till poängsättning och märkning när den valda SRP är antingen JSRP eller MSRP, men inte ASRP. (Om du inte känner till dessa termer läser du [Community Content Storage](/help/communities/working-with-srp.md) och [Storage Resource Provider Overview](/help/communities/srp.md).)

Beskrivningarna för att komma åt betygs- och badging-data använder JSRP, eftersom UGC är lätt att komma åt med [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

**JSRP på författare**: Om du experimenterar i författarmiljön resulterar det i UGC som bara är synligt från författarmiljön.

**JSRP vid publicering**: Om du testar i publiceringsmiljön måste du även ha administratörsbehörighet för en publiceringsinstans i CRXDE Lite. Om publiceringsinstansen körs i [produktionsläge](/help/sites-administering/production-ready.md) (noSampleContent Run Mode) måste du [aktivera CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

Basplatsen för UGC på JSRP är `/content/usergenerated/asi/jcr/`.

### API:er för klassificering och märkning {#scoring-and-badging-apis}

Följande API:er kan användas:

* [com.adobe.cq.social.scoring.api in 6.3](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=sv-SE)
* [com.adobe.cq.social.badging.api in 6.3](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=sv-SE)

De senaste Javadocs-filerna för det installerade funktionspaketet är tillgängliga för utvecklare från Adobe-databasen. Se [Använda Maven för Communities: Javadocs](/help/communities/maven.md#javadocs).

**Platsen och formatet för användargenererat innehåll i databasen kan ändras utan varning**.

### Exempelinställningar {#example-setup}

Skärmbilder av databasdata kommer från konfiguration av poängsättning och märkning för ett forum på två olika AEM:

1. En AEM *med* ett unikt ID (communitywebbplatsen har skapats med guiden):

   * Använda självstudiekursen Komma igång (engagerande) som skapades under självstudiekursen [Komma igång](/help/communities/getting-started.md)
   * Hitta forumsidnoden

     `/content/sites/engage/en/forum/jcr:content`

   * Lägga till egenskaper för poängsättning och märkning

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-scoring,
   /libs/settings/community/badging/rules/forums-scoring]
   ```

   * Leta reda på forumkomponentnoden

     `/content/sites/engage/en/forum/jcr:content/content/primary/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * Lägg till egenskap för att visa emblem

     `allowBadges = true`

   * En användare loggar in, skapar ett forumämne och tilldelas ett bronze-märke

1. En AEM *utan* ett unikt ID:

   * Använda guiden [Community Components](/help/communities/components-guide.md)
   * Hitta forumsidnoden

     `/content/community-components/en/forum/jcr:content`

   * Lägga till egenskaper för poängsättning och märkning

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-badging,
   /libs/settings/community/badging/rules/forums-badging]
   ```

   * Leta reda på forumkomponentnoden

     `/content/community-components/en/forum/jcr:content/content/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * Lägg till egenskap för att visa emblem

     `allowBadges = true`

   * En användare loggar in, skapar ett forumämne och tilldelas ett bronze-märke

1. En användare tilldelas ett moderatormärke med cURL:

   ```shell
   curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" https://localhost:4503/home/users/community/w271OOup2Z4DjnOQrviv/profile.social.json
   ```

   När en användare har fått två bronze-märken och tilldelats ett moderatormärke visas användaren med sitt foruminlägg på följande sätt:

   ![moderator](assets/moderator.png)

>[!NOTE]
>
>Det här exemplet följer inte följande metodtips:
>
>* Poängregelnamn ska vara globalt unika. De får inte sluta med samma namn.
>
>  Ett exempel på vad *inte* ska göra:
>
>  /libs/settings/community/scoring/rules/site1/forums-scoring
>  /libs/settings/community/scoring/rules/site2/forums-scoring
>
>* Skapa unika märkesbilder för olika AEM

### UGC för åtkomstbedömning {#access-scoring-ugc}

Du bör använda [API:erna](#scoring-and-badging-apis).

I undersökningssyfte, till exempel med JSRP, är baskamappen som innehåller poäng

* `/content/usergenerated/asi/jcr/scoring`

Den underordnade noden för `scoring` är resultatregelns namn. Det bästa sättet är alltså att betygsregelnamn på en server är globalt unika.

För Geometrixx Engage-webbplatsen är användaren, och poängen för den, i en sökväg som konstruerats med resultatregelnamnet, webbplatsens webbplats-ID ( `engage-ba81p`), ett unikt ID och användarens ID:

* `.../scoring/forums-scoring/engage-ba81p/6d179715c0e93cb2b20886aa0434ca9b5a540401/riley`

För stödwebbplatsen för Community Components finns användaren, och poängen för den, i en sökväg som konstruerats med bedömningsregelnamnet, ett standard-ID ( `default-site`), ett unikt ID och användarens ID:

* `.../scoring/forums-scoring/default-site/b27a17cb4910a9b69fe81fb1b492ba672d2c086e/riley`

Poängen lagras i egenskapen `scoreValue_tl` som bara kan innehålla ett värde eller indirekt referera till en atomicCounter.

![access-scoring-ugc](assets/access-scoring-ugc.png)

### Access Badging UGC {#access-badging-ugc}

Du bör använda [API:erna](#scoring-and-badging-apis).

I undersökningssyfte, till exempel med JSRP, är baskappen som innehåller information om tilldelade eller tilldelade märken

* `/content/usergenerated/asi/jcr`

Följs av sökvägen till användarens profil och avslutas i en badges-mapp, till exempel:

* `/home/users/community/w271OOup2Z4DjnOQrviv/profile/badges`

#### Tilldelad bricka {#awarded-badge}

![tilldelad-badging-ugc](assets/access-badging-ugc.png)

#### Tilldelat märke {#assigned-badge}

![tilldelad-badge](assets/assigned-badge.png)

## Ytterligare information {#additional-information}

Så här visar du en sorterad lista med medlemmar baserat på punkter:

* [Ledarpanelsfunktion](/help/communities/functions.md#leaderboard-function) för inkludering i en community-webbplats eller gruppmall.
* [Ledarpanelskomponent](/help/communities/enabling-leaderboard.md), den aktuella komponenten i Leaderboard-funktionen, för sidredigering.
