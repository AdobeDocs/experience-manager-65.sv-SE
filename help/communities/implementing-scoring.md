---
title: Communities Scoring and Badges
seo-title: Communities Scoring and Badges
description: Med AEM Communities-poäng och -märken kan ni identifiera och belöna communitymedlemmar
seo-description: Med AEM Communities-poäng och -märken kan ni identifiera och belöna communitymedlemmar
uuid: d73683df-a413-4b3c-869c-67568bfdfcf6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ea033bb9-cb92-4c93-855f-8c902999378c
docset: aem65
tagskeywords: scoring, badging, badges, gamification
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Communities Scoring and Badges{#communities-scoring-and-badges}

## Översikt {#overview}

Funktionen AEM Communities-poäng och -badges gör det möjligt att identifiera och belöna communitymedlemmar.

De viktigaste aspekterna på poängsättning och märkning är:

* [tilldela märken](#assign-and-revoke-badges) för att identifiera en medlems roll i communityn

* [grundläggande tilldelning av märken](#enable-scoring) till medlemmar för att uppmuntra dem att delta (mängden innehåll som skapas)
* [Avancerad tilldelning av märken](/help/communities/advanced.md) för att identifiera medlemmar som experter (kvaliteten på det material som skapas)

**Observera** att tilldelning av märken [inte är aktiverat som standard](/help/communities/implementing-scoring.md#main-pars-text-237875536).

>[!CAUTION]
>
>Implementeringsstrukturen som visas i CRXDE Lite kan ändras när användargränssnittet blir tillgängligt.

## Badges {#badges}

Beteckningar placeras under en medlems namn för att ange antingen deras roll eller deras ställning i communityn. Badges kan antingen visas som en bild eller som ett namn. När namnet visas som en bild inkluderas det som alternativ text för tillgänglighet.

Som standard finns emblem i databasen på

* /etc/community/badging/images

Om de lagras på en annan plats bör de vara tillgängliga för alla.

UGC har olika märken för att avgöra om de har tilldelats eller förvärvats enligt reglerna. För närvarande visas tilldelade märken som text och färdiga märken som en bild.

### Användargränssnitt för hantering av emblem {#badge-management-ui}

Konsolen Communities [Badges](/help/communities/badges.md) ger möjlighet att lägga till egna emblem som kan visas för en medlem när de har förtjänats (tilldelats) eller när de har en specifik roll i communityn (tilldelade).

### Tilldelade märken {#assigned-badges}

Rollbaserade märken tilldelas av en administratör till communitymedlemmar baserat på deras roll i communityn.

Tilldelade (och tilldelade) märken lagras i den valda [SRP](/help/communities/srp.md) och är inte direkt tillgängliga. Det enda sättet att tilldela rollbaserade emblem är att göra det med kod eller cURL tills ett GUI är tillgängligt. Instruktioner för cURL finns i avsnittet [Tilldela och återkalla märken](#assign-and-revoke-badges).

I releasen ingår tre rollbaserade märken:

* moderator
   `/etc/community/badging/images/moderator/jcr:content/moderator.png`

* gruppansvarig
   `/etc/community/badging/images/group-manager/jcr:content/group-manager.png`

* behörig medlem
   `/etc/community/badging/images/privileged-member/jcr:content/privileged-member.png`

![chlimage_1-98](assets/chlimage_1-98.png)

### Tilldelade märken {#awarded-badges}

Belöningsbaserade märken delas ut av betygstjänsten till communitymedlemmar baserat på regler som tillämpas på deras verksamhet i communityn.

För att emblem ska visas som en belöning för aktivitet måste två saker hända:

* emblem måste vara [aktiverat](#enableforcomponent) för funktionskomponenten
* regler för klassificering och märkning måste [tillämpas](#applytopage) på den sida (eller det överordnade objekt) som komponenten placeras på

I releasen ingår tre belöningsbaserade märken:

* guld
   `/etc/community/badging/images/gold-badge/jcr:content/gold.png`

* silver
   `/etc/community/badging/images/silver-badge/jcr:content/silver.png`

* brons
   `/etc/community/badging/images/bronze-badge/jcr:content/bronze.png`

![chlimage_1-99](assets/chlimage_1-99.png)

>[!NOTE]
>
>Poängregler kan konfigureras för att tilldela negativa punkter för inlägg som markerats som olämpliga och därmed påverka poängvärdet. När ett märke har skapats tas det dock inte bort automatiskt på grund av ändringar i poängsättningsregeln eller poängsättningsregeln.
>
>Tilldelade märken kan återkallas på samma sätt som tilldelade märken. Se avsnittet [Tilldela och återkalla märken](#assign-and-revoke-badges) . Framtida förbättringar kommer att omfatta ett användargränssnitt för att hantera medlemmarnas märken.

### Egna märken {#custom-badges}

Anpassade emblem kan installeras med [Badges-konsolen](/help/communities/badges.md) och antingen tilldelas eller anges i badging-regler.

Anpassade märken replikeras automatiskt till publiceringsmiljön när de installeras från badges-konsolen.

## Aktivera poängsättning {#enable-scoring}

Poängen är inte aktiverad som standard. De grundläggande stegen för att skapa och aktivera poängsättning och tilldelning av märken är:

* identifiera regler för intjäningspunkter ([poängregler](#scoring-rules))
* för poäng som ackumuleras per poängregler, tilldela [märken](#badges) ([badging-regler](#badging-rules))

* [tillämpa regler för poäng och märkning på en communitywebbplats](#apply-rules-to-content)
* [aktivera märkning för communityfunktioner](#enable-badges-for-component)

Se avsnittet [Snabbtest](#quick-test) för att aktivera poängsättning för en community-webbplats med standardreglerna för poäng och taggning för forum och kommentarer.

### Använd regler för innehåll {#apply-rules-to-content}

Om du vill aktivera poängsättning och märken lägger du till egenskaperna `scoringRules` och `badgingRules`till en nod i platsens innehållsträd.

Om webbplatsen redan är publicerad, efter att ha tillämpat alla regler och aktiverat komponenter, publicerar du om den.

Reglerna som gäller för en komponent som har aktiverats för badging är reglerna för den aktuella noden eller dess överordnade nod.

Om noden är av typen `cq:Page` (rekommenderas) lägger du sedan till egenskaperna med CRXDE|Lite i `jcr:content`noden.

| **Egenskap** | **Typ** | **Beskrivning** |
|---|---|---|
| badgingRules | Sträng[] | en matrislista med [märkningsregler](#badging-rules) |
| scoringRules | Sträng[] | en matrislista med [poängregler](#scoring-rules) |

>[!NOTE]
>
>Om en bedömningsregel inte verkar ha någon effekt på att dela ut märken kontrollerar du att resultatregeln inte har blockerats av märkningsregelns egenskap scoringRules. Se avsnittet [Badging Rules](#badging-rules).

### Aktivera emblem för komponent {#enable-badges-for-component}

Poängreglerna och reglerna för radavstånd gäller endast för instanser av komponenter som har aktiverat badging genom att redigera komponentkonfigurationen i [redigeringsläget](/help/communities/author-communities.md).

En boolesk egenskap, `allowBadges`, aktiverar/inaktiverar visning av emblem för en komponentinstans. Den kan konfigureras i dialogrutan [för](/help/communities/author-communities.md) komponentredigering för forum-, QnA- och kommentarkomponenter via en kryssruta med etiketten **Display Badges**.

#### Exempel: allowBadges för instans av forumkomponent {#example-allowbadges-for-forum-component-instance}

![chlimage_1-100](assets/chlimage_1-100.png)

>[!NOTE]
>
>Alla komponenter kan överlappas för att visa emblem med HBS-koden som finns i forumen, QnA och kommentarer som exempel.

## Poängregler {#scoring-rules}

Poängregler är grunden för poängsättning för att tilldela märken.

Enkelt uttryckt är varje resultatregel en lista med en eller flera underregler. Poängregler tillämpas på communitywebbplatsinnehållet för att identifiera reglerna som ska gälla när emblem är aktiverade.

Poängregler ärvs men är inte additiva. Exempel:

* om page2 innehåller resultatregel2 och dess överordnade sida1 innehåller poängregel1
* en åtgärd på en sidkomponent aktiverar både regel1 och regel2
* om båda reglerna innehåller tillämpliga delregler för samma `topic/verb` :

   * bara underregeln från regel 2 påverkar poängen
   * poängen från båda delreglerna inte läggs samman

Om det finns mer än en resultatregel bevaras poängen separat för varje regel.

Poängregler är noder av typen `cq:Page` med egenskaper på `jcr:content`noden som anger listan med underregler som definierar den.

Bakgrundsmusik lagras i SRP.

>[!NOTE]
>
>God praxis: unikt namn för varje poängregel.
>
>Poängregelnamnen ska vara globalt unika. de ska inte sluta med samma namn.
>
>Ett exempel på vad *inte ska göra:
>/etc/community/scoring/rules/site1/forums-scoring
>/etc/community/scoring/rules/site2/forums-scoring

### Underregler för poängsättning {#scoring-sub-rules}

Delreglerna för poängsättning innehåller egenskaper som detaljerar värdena för att delta i communityn.

Varje poängsättningsunderregel identifierar

* vilka aktiviteter som spåras
* vilken specifik communityfunktion som berörs
* hur många poäng som tilldelas

Som standard tilldelas poäng till den medlem som utför en åtgärd, såvida inte underregeln anger att ägaren av innehållet tar emot poängen ( `forOwner`).

Varje underregel kan ingå i en eller flera poängregler.

Underregelns namn följer vanligtvis mönstret för att använda ett *ämne, objekt *och *verb.* Exempel:

* medlem-comment-create
* medlem-receive-voice

Underregler är noder av typen `cq:Page` med egenskaper på dess `jcr:content`nod som anger [verb och ämnen](#topics-and-verbs) .

<table>
 <tbody>
  <tr>
   <th>Egenskap</th>
   <th>Typ</th>
   <th> Värdebeskrivning</th>
  </tr>
  <tr>
   <td><i><code>VERB</code></i></td>
   <td>Lång</td>
   <td>
    <ul>
     <li>krävs, verbet motsvarar en händelseåtgärd</li>
     <li>det måste finnas minst en verb-egenskap</li>
     <li>verbet måste anges i VERb</li>
     <li>det kan finnas flera verb-egenskaper, men inga dubbletter</li>
     <li>värdet är poängvärdet som ska användas för den här händelsen</li>
     <li>värdet kan vara positivt eller negativt</li>
     <li>en lista över verb som stöds i den här versionen finns i avsnittet <a href="#topics-and-verbs">Ämnen och verb</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>Sträng[]</td>
   <td>
    <ul>
     <li>frivilligt, begränsar underregeln till communitykomponenter som identifieras av händelseämnen</li>
     <li>om angivet: värdet är en sträng med flera värden för händelseämnen</li>
     <li>en lista med ämnen i releasen finns i avsnitten <a href="#topics-and-verbs">Ämnen och Verb</a></li>
     <li>standard ska gälla för alla ämnen som är associerade med verbet/verbet/verbet</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>forOwner</code></td>
   <td>Boolesk</td>
   <td>
    <ul>
     <li>frivilligt, inte är relevant när en medlem agerar på innehåll som han/hon äger</li>
     <li>om true, använd poäng på ägaren av det innehåll som ska hanteras</li>
     <li>om falskt, lägg till poäng för en medlem som utför åtgärden</li>
     <li>default is false</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>scoringType</code></td>
   <td>Sträng</td>
   <td>
    <ul>
     <li>frivilligt, identifierar bedömningsmotorn</li>
     <li>om "grundläggande", anger poängsättningsmotorn baserat på kvantitet
      <ul>
       <li>ingår i releasen</li>
      </ul> </li>
     <li>om "avancerat", anger poängsättningsmotorn baserat på kvalitet och kvantitet
      <ul>
       <li>kräver ett <a href="/help/communities/advanced.md">extra paket</a></li>
      </ul> </li>
     <li>default is "basic"</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Inkluderade poängsättningsregler och underregler {#included-scoring-rules-and-sub-rules}

I releasen finns två poängregler för [forumfunktionen](/help/communities/functions.md#forum-function) (en för respektive forum och kommentarkomponenter för forumfunktionen):

1. /etc/community/scoring/rules/comments-scoring

   * subRules[] =/etc/community/scoring/rules/sub-rules/member-comment-create/etc/community/scoring/rules/sub-rules/member-receive-voice/etc/community/scoring/rules/sub-rules/Member-give-voice/etc/community/scoring/rules/sub-rules/member-is-moderated

1. /etc/community/scoring/rules/forums-scoring

   * subRules[] =/etc/community/scoring/rules/sub-rules/Member-forum-create/etc/community/scoring/rules/sub-rules/Member-receive-voice/etc/community/scoring/rules/sub-rules/Member-give-voice/etc/community/scoring/rules/sub-rules/member-is-moderated

**Anteckningar:**

* både `rules`och `sub-rules` noder är av typen cq:Page

* `subRules`är ett attribut av typen String[] i regelns `jcr:content` nod

* `sub-rules` kan delas mellan olika poängregler
* `rules`ska finnas på en databasplats med läsbehörighet för alla

   * regelnamn måste vara unika oavsett plats

### Aktivera anpassade poängsättningsregler {#activating-custom-scoring-rules}

Alla ändringar eller tillägg som görs i resultatregler eller underregler i redigeringsmiljön måste installeras vid publicering.

## Badningsregler {#badging-rules}

Märkordsregler länkar poängregler till märken genom att ange :

* vilken resultatregel
* poängen som krävs för att tilldelas ett visst märke

Badging-regler är noder av typen `cq:Page` med egenskaper på dess `jcr:content`nod som korrelerar poängregler till poäng och emblem.

Reglerna för märkning består av en obligatorisk `thresholds`egenskap som är en ordnad lista med bakgrundsmusik som är mappade till emblem. Poängen måste ordnas i högre värde. Exempel :

* `1|/etc/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * ett bronze-märke tilldelas för 1 poäng

* `60|/etc/community/badging/images/silver-badge/jcr:content/silver.png`

   * ett silvermärke tilldelas när 60 poäng har samlats in

* `80|/etc/community/badging/images/gold-badge/jcr:content/gold.png`

   * ett guldmärke delas ut när 80 poäng har samlats in

Betygsregler kombineras med poängregler, som bestämmer hur poäng ackumuleras. Se avsnittet [Använd regler på innehåll](#apply-rules-to-content).

Egenskapen `scoringRules`för en badging-regel begränsar helt enkelt vilka poängregler som kan kombineras med den speciella badging-regeln.

>[!NOTE]
>
>God praxis: skapa unika märkesbilder för varje AEM-webbplats.

![chlimage_1-101](assets/chlimage_1-101.png)

<table>
 <tbody>
  <tr>
   <th>Egenskap</th>
   <th>Typ</th>
   <th>Värdebeskrivning</th>
  </tr>
  <tr>
   <td>tröskelvärden</td>
   <td>Sträng[]</td>
   <td><em>(obligatoriskt)</em> En sträng med flera värden i formatet 'number|path'
    <ul>
     <li>number = score</li>
     <li>| = den lodräta linjen char (U+007C)</li>
     <li>sökväg = fullständig sökväg till badge-bildresurs</li>
    </ul> Strängarna måste ordnas så att siffrorna ökar i värde och inget mellanrum ska visas mellan talet och sökvägen.<br /><br /> Exempelpost: <code>80|/etc/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Sträng</td>
   <td><em>(valfritt)</em> Identifierar bedömningsmotorn som antingen grundläggande eller avancerad. Om du vill använda den avancerade poängsättningsmotorn läser du i <a href="/help/communities/advanced.md">Avancerade poäng och märken</a>. Standardvärdet är "basic".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>Sträng[]</td>
   <td>(<em>valfritt</em>) En sträng med flera värden som begränsar badging-regeln till bedömningshändelser som identifieras av poängreglerna</td>
  </tr>
 </tbody>
</table>

### Inkluderade märkningsregler {#included-badging-rules}

I den här versionen finns två regler för taggning som motsvarar [reglerna](#includedscoringrules)för forum och kommentarer.

* /etc/community/badging/rules/comments-badging
* /etc/community/badging/rules/forums-badging

**Anteckningar:**

* `rules` noder är av typen cq:Page
* `rules`ska finnas på en databasplats med läsbehörighet för alla

   * regelnamn måste vara unika oavsett plats

### Aktivera anpassade märkningsregler {#activating-custom-badging-rules}

Alla ändringar eller tillägg som görs i märkningsregler eller bilder i redigeringsmiljön måste installeras vid publicering.

## Tilldela och återkalla märken {#assign-and-revoke-badges}

Medlemmar kan tilldelas märken antingen med hjälp av [medlemskonsolen](/help/communities/members.md#badges-tab) eller via programmering med hjälp av cURL-kommandon.

Följande cURL-kommandon visar vad som krävs för en HTTP-begäran om att tilldela och återkalla emblem. Grundformatet är:

cURL -i -X POST -H *header* -u *signin * -F *operation * -F *badge * *member-profile-url*

*header* = &quot;Accept:application/json&quot;anpassad rubrik som ska skickas till servern (obligatoriskt)

*signin* = administrator-id:passwordTill exempel : admin:admin

*operation* = &quot;:operation=social:assignBadge&quot; OR &quot;:operation=social:deleteBadge&quot;

*badge* = &quot;badgeContentPath=*badge-image-file*&quot;

*badge-image-file* = platsen för badge-bildfilen i databasen, till exempel: /etc/community/badging/images/moderator/jcr:content/moderator.png

*member-profile-url* = slutpunkten för medlemmens profil vid publicering, till exempel: https://&lt;server>:&lt;port>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>The *member-profile-url*
>
>* kan referera till en författarinstans om [tunneltjänsten](/help/communities/users.md#tunnel-service) är aktiverad
>* kan vara ett otydligt, slumpmässigt namn - se [Säkerhetschecklista](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path) för auktoriserat ID
>



### Exempel: {#examples}

#### Tilldela ett moderatormärke {#assign-a-moderator-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/etc/community/badging/images/moderator/jcr:content/moderator.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

#### Återkalla ett tilldelat silvermärke {#revoke-an-assigned-silver-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:deleteBadge" -F "badgeContentPath=/etc/community/badging/images/silver/jcr:content/silver.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

>[!NOTE]
>
>Om du använder cURL för att tilldela och återkalla emblem fungerar det för alla badge-bilder, men när de tilldelas i stället för EV markeras de som tilldelade märken och hanteras därefter.

## Betyg och märken för anpassade komponenter {#scoring-and-badges-for-custom-components}

Du kan skapa regler för klassificering och märkning för anpassade komponenter genom att koppla händelseavsnitten som skapats för komponenten till verb.

## Ämnen och verb {#topics-and-verbs}

När medlemmar interagerar med communityfunktioner skickas händelser som kan utlösa asynkrona avlyssnare, som meddelanden och poängsättning.

En komponents SocialEvent-instans registrerar händelserna som `actions`de inträffar för en `topic`. SocialEvent innehåller en metod för att returnera en `verb`associerad åtgärd. Det finns en *n-1* -relation mellan `actions`och `verbs`.

För de communitykomponenter som levereras beskrivs `verbs`definitionen för varje `topic`tillgänglig för användning i [poängdelregler](#scoring-sub-rules)i följande tabeller.

>[!NOTE]
>
>En ny boolesk egenskap, `allowBadges`, aktiverar/inaktiverar visning av emblem för en komponentförekomst. Den kan konfigureras i uppdaterade dialogrutor [för](/help/communities/author-communities.md) komponentredigering via en kryssruta med etiketten **Display Badges**.

**[Calendar Component](/help/communities/calendar.md)**SocialEvent`topic`= com/adobe/cq/social/calendar

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar en kalenderhändelse |
| LÄGG TILL | kommentarer från medlemmar i en kalenderhändelse |
| UPPDATERA | medlemmens kalenderhändelse eller -kommentar har redigerats |
| TA BORT | medlemmens kalenderhändelse eller -kommentar tas bort |

**[Comments Component](/help/communities/comments.md)**SocialEvent`topic`= com/adobe/cq/social/comment

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar en kommentar |
| LÄGG TILL | medlemssvar på kommentarer |
| UPPDATERA | Medlemmens kommentar har redigerats |
| TA BORT | medlemmens kommentar har tagits bort |

**[File Library Component](/help/communities/file-library.md)**SocialEvent`topic`= com/adobe/cq/social/fileLibrary

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar en mapp |
| BIFOGA | medlem överför en fil |
| UPPDATERA | medlemmen uppdaterar en mapp eller fil |
| TA BORT | medlem tar bort en mapp eller fil |

**[Forum Component](/help/communities/forum.md)**SocialEvent`topic`= com/adobe/cq/social/forum

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar forumämne |
| LÄGG TILL | medlemssvar på forumämnet |
| UPPDATERA | Medlemmens forumämne eller svar har redigerats |
| TA BORT | forumämnet eller svaret för en medlem tas bort |

**[Journal Component](/help/communities/blog-feature.md)**SocialEvent`topic`= com/adobe/cq/social/journal

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar en bloggartikel |
| LÄGG TILL | kommentarerna på en bloggartikel |
| UPPDATERA | Medlemmens bloggartikel eller kommentar redigeras |
| TA BORT | Medlemmens bloggartikel eller kommentar tas bort |

**[QnA Component](/help/communities/working-with-qna.md)**SocialEvent`topic`= com/adobe/cq/social/qna

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar en QnA-fråga |
| LÄGG TILL | medlem skapar ett QnA-svar |
| UPPDATERA | -medlemmens fråga eller svar har redigerats |
| MARKERA | Medlemmens svar har valts |
| AVMARKERA | Medlemmens svar är avmarkerat |
| TA BORT | en medlems fråga eller svar tas bort |

**[Review Component](/help/communities/reviews.md)**SocialEvent`topic`= com/adobe/cq/social/review

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar granskning |
| UPPDATERA | Medlemmens granskning har redigerats |
| TA BORT | Medlemmens granskning har tagits bort |

**[Värderingskomponent](/help/communities/rating.md)**SocialEvent`topic`= com/adobe/cq/social/tally/rating

| **Verb** | **Beskrivning** |
|---|---|
| LÄGG TILL KLASSIFICERING | Medlemmens innehåll har fått en högre gradering |
| TA BORT KLASSIFICERING | medlemmens innehåll har nedgraderats |

**[Röstkomponent](/help/communities/voting.md)**SocialEvent`topic`= com/adobe/cq/social/tally/voting

| **Verb** | **Beskrivning** |
|---|---|
| LÄGG TILL RÖST | Medlemmens innehåll har röstats upp |
| TA BORT RÖSTNING | Medlemmens innehåll har inte röstats ned |

**Moderation-enabled Components** SocialEvent `topic`= com/adobe/cq/social/moderation

| **Verb** | **Beskrivning** |
|---|---|
| NEKA | medlemmens innehåll nekas |
| FLAGGA-SOM-OLÄMPLIGT | medlemmens innehåll är flaggat |
| OLÄMPLIG FLAGNING SOM | medlemmens innehåll är oflaggat |
| ACCEPTERA | Medlemmens innehåll godkänns av moderatorn |
| STÄNG | medlem stänger kommentarer till redigeringar och svar |
| ÖPPNA | medlem öppnar kommentaren igen |

### Anpassade komponenthändelser {#custom-component-events}

För en anpassad komponent instansieras en SocialEvent-instans för att spela in komponentens händelser som `actions`de inträffar för en `topic`.

För att det ska gå att använda poängsättning måste SocialEvent åsidosätta metoden `getVerb()` så att en lämplig metod `verb`returneras för varje `action`. Den `verb` som returneras för en åtgärd kan vara en vanlig (t.ex. `POST`) eller en speciell komponent (t.ex. `ADD RATING`). Det finns en *n-1* -relation mellan `actions`och `verbs`.

## Felsökning {#troubleshooting}

### Inga märken visas {#badges-are-not-appearing}

Om regler för klassificering och märkning har tillämpats på webbplatsens innehåll, men emblem inte tilldelas för någon aktivitet, kontrollerar du att emblem har aktiverats för komponentens instans.

Se [Aktivera märken för komponent](#enable-badges-for-component).

### Poängregeln har ingen effekt {#scoring-rule-has-no-effect}

Om regler för poängsättning och märkning har tillämpats på webbplatsens innehåll, och emblem tilldelas för vissa åtgärder, men inte andra, kontrollerar du att badging-regeln inte har begränsat de poängregler som den gäller för.

Se `scoringRules`egenskapen [Badging Rules](#badging-rules).

### Skiftlägeskänslig typo {#case-sensitive-typo}

De flesta egenskaper och värden, särskilt verbet, är skiftlägeskänsliga. Verb måste vara VERSALER när de används i en underregel för poängsättning.

Om funktionen inte fungerar som väntat kontrollerar du att data har angetts korrekt.

## Snabbtest {#quick-test}

Det går snabbt att testa poängsättning och märkning med hjälp av [Komma igång-självstudiekursen](/help/communities/getting-started.md) (engagera):

* få åtkomst till CRXDE Lite på författaren
* bläddra till bassidan:

   * /content/sites/engage/en/jcr:content

* lägg till egenskapen badgingRules:

   * **Namn**: `badgingRules`
   * **Typ**: `String`
   * välj **flera**
   * välj **Lägg till**
   * enter `/etc/community/badging/rules/forums-badging`
   * select **+**
   * enter `/etc/community/badging/rules/comments-badging`
   * välj **OK**

* lägg till egenskapen scoringRules:

   * **Namn**: `scoringRules`
   * **Typ**: `String`
   * välj **flera**
   * välj **Lägg till**
   * enter `/etc/community/scoring/rules/forums-scoring`
   * select **+**
   * enter `/etc/community/scoring/rules/comments-scoring`
   * välj **OK**

* välj **Spara alla**

![chlimage_1-102](assets/chlimage_1-102.png)

Kontrollera sedan att forumkomponenterna och kommentarkomponenterna tillåter att märken visas:

* igen med CRXDE Lite
* bläddra till forumkomponenten

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`

* lägg till den booleska egenskapen allowBadges, om det behövs, och kontrollera att den är true

   * **Namn**: `allowBadges`
   * **Typ**: `Boolean`
   * **Värde**: `true`

![chlimage_1-103](assets/chlimage_1-103.png)

Publicera sedan [communitywebbplatsen igen](/help/communities/sites-console.md#publishing-the-site) .

Äntligen

* bläddra till komponenten i publiceringsinstansen
* logga in som community-medlem (till exempel: weston.mccall@dodgit.com / lösenord)
* publicera ett nytt forumämne
* sidan måste uppdateras för att märket ska kunna visas

   * logga ut och logga in som en annan community-medlem (till exempel: aaron.mcdonald@mailinator.com/lösenord)

* välj forum

Detta bör göra att communitymedlemmen får ett bronze-märke synligt med sitt foruminlägg eftersom den första tröskeln för forumbadging är ett poäng på 1.

![bronzebadge](assets/bronzebadge.png)

## Additional Information {#additional-information}

Mer information finns på sidan [Scoring and Badges Essentials](/help/communities/configure-scoring.md) för utvecklare.

Mer information om den avancerade bedömningsmotorn finns i [Advanced Scoring and Badges](/help/communities/advanced.md).

Den konfigurerbara [komponenten](/help/communities/enabling-leaderboard.md) och [funktionen](/help/communities/functions.md#leaderboard-function) för ledningsgruppen förenklar visningen av medlemmar och deras poäng på en communitywebbplats.
