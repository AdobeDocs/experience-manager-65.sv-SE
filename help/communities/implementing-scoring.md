---
title: Communities Scoring and Badges
description: Med AEM Communities poäng och emblem kan ni identifiera och belöna communitymedlemmar
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
tagskeywords: scoring, badging, badges, gamification
role: Admin
exl-id: 4aa857f7-d111-4548-8f03-f6d6c27acf51
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2856'
ht-degree: 0%

---

# Communities Scoring and Badges {#communities-scoring-and-badges}

## Ökning {#overview}

AEM Communities poäng och badges ger möjlighet att identifiera och belöna communitymedlemmar.

De viktigaste aspekterna på poängsättning och märkning är:

* [Tilldela emblem](#assign-and-revoke-badges) för att identifiera en medlems roll i communityn.

* [Grundläggande tilldelning av emblem](#enable-scoring) till medlemmar för att uppmuntra dem att delta (antal skapade innehåll).

* [Avancerad tilldelning av märken](/help/communities/advanced.md) för att identifiera medlemmar som experter (kvaliteten på det innehåll som skapas).

**Obs!** Att tilldela emblem är [inte aktiverat som standard](/help/communities/implementing-scoring.md#main-pars-text-237875536).

>[!CAUTION]
>
>Den implementeringsstruktur som visas i CRXDE Lite kan ändras när användargränssnittet blir tillgängligt.

## Badges {#badges}

Beteckningar placeras under en medlems namn för att ange antingen deras roll eller deras ställning i communityn. Badges kan antingen visas som en bild eller som ett namn. När namnet visas som en bild inkluderas det som alternativ text för tillgänglighet.

Som standard finns emblem i databasen på följande plats:

* `/libs/settings/community/badging/images`

Om de lagras på en annan plats bör de vara tillgängliga för alla.

UGC har olika märken oavsett om de har tilldelats eller förvärvats enligt reglerna. För närvarande visas tilldelade märken som text och färdiga märken som en bild.

### Användargränssnitt för hantering av emblem {#badge-management-ui}

Med konsolen [emblem](/help/communities/badges.md) kan du lägga till egna emblem som kan visas för en medlem när den har tjänats in (tilldelats) eller när de har en specifik roll i communityn (tilldelats).

### Tilldelade märken {#assigned-badges}

Rollbaserade märken tilldelas av en administratör till communitymedlemmar baserat på deras roll i communityn.

Tilldelade (och tilldelade) märken lagras i den valda [SRP](/help/communities/srp.md) och är inte direkt tillgängliga. Det enda sättet att tilldela rollbaserade emblem är att göra det med kod eller cURL tills ett GUI är tillgängligt. Instruktioner för cURL finns i avsnittet [Tilldela och återkalla emblem](#assign-and-revoke-badges).

I releasen finns tre rollbaserade märken:

* **moderator**
  `/libs/settings/community/badging/images/moderator/jcr:content/moderator.png`

* **grupphanterare**
  `/libs/settings/community/badging/images/group-manager/jcr:content/group-manager.png`

* **privilegierad medlem**
  `/libs/settings/community/badging/images/privileged-member/jcr:content/privileged-member.png`

  ![tilldelade-emblem](assets/assigned-badges.png)

### Tilldelade märken {#awarded-badges}

Belöningsbaserade märken delas ut av betygstjänsten till communitymedlemmar baserat på regler som tillämpas på deras verksamhet i communityn.

För att emblem ska visas som en belöning för aktivitet måste två saker hända:

* Badging måste vara [enabled](#enableforcomponent) för funktionskomponenten.
* Regler för klassificering och märkning måste [tillämpas](#applytopage) på sidan (eller det överordnade objektet) som komponenten placeras på.

I releasen ingår tre belöningsbaserade märken:

* **guld**
  `/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

* **silver**
  `/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

* **brons**
  `/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

  ![tilldelad-badges](assets/awarded-badges.png)

>[!NOTE]
>
>Poängregler kan konfigureras för att tilldela negativa punkter för inlägg som markerats som olämpliga och därmed påverka poängvärdet. När ett märke har skapats tas det dock inte bort automatiskt på grund av ändringar i poängsättningsregeln eller poängsättningsregeln.
>
>Tilldelade märken kan återkallas på samma sätt som tilldelade märken. Se avsnittet [Tilldela och återkalla märken](#assign-and-revoke-badges). Framtida förbättringar kommer att omfatta ett användargränssnitt för att hantera medlemmarnas märken.

### Egna märken {#custom-badges}

Anpassade emblem kan installeras med [Badges-konsolen](/help/communities/badges.md) och antingen tilldelas eller anges i badging-regler.

Anpassade märken replikeras automatiskt till publiceringsmiljön när de installeras från badges-konsolen.

## Aktivera poängsättning {#enable-scoring}

Poängen är inte aktiverad som standard. De grundläggande stegen för att sätta upp och aktivera poängsättning och tilldelning av märken är:

* Identifiera regler för inkomstpunkter ([poängregler](#scoring-rules)).
* Tilldela [emblem](#badges) ([badging-regler](#badging-rules)) för poäng som samlas per poängregler.

* [Använd reglerna för poäng och badging på en communitywebbplats](#apply-rules-to-content).
* [Aktivera märkning för communityfunktioner](#enable-badges-for-component).

Gå till avsnittet [Snabbtest](#quick-test) om du vill aktivera poängsättning för en community-webbplats med standardreglerna för bedömning och märkning av forum och kommentarer.

### Använd regler för innehåll {#apply-rules-to-content}

Lägg till egenskaperna `scoringRules` och `badgingRules` till en nod i platsens innehållsträd om du vill aktivera poängsättning och emblem.

Om webbplatsen redan är publicerad, efter att du har tillämpat alla regler och aktiverat komponenter, publicerar du om den.

Reglerna som gäller för en komponent som har aktiverats för badging är de som gäller för den aktuella noden eller dess överordnade nod.

Om noden är av typen `cq:Page` (rekommenderas) lägger du sedan till egenskaperna i noden `jcr:content` med CRXDE|Lite.

| **Egenskap** | **Typ** | **Beskrivning** |
|---|---|---|
| badgingRules | Sträng | en matrislista med [märkningsregler](#badging-rules) |
| scoringRules | Sträng | en matrislista med [poängregler](#scoring-rules) |

>[!NOTE]
>
>Om en bedömningsregel inte verkar ha någon effekt på att dela ut taggar kontrollerar du att resultatregeln inte har blockerats av spårningsregelns egenskap scoringRules. Se avsnittet [Badging Rules](#badging-rules).

### Aktivera emblem för komponent {#enable-badges-for-component}

Poängreglerna och reglerna för radavstånd gäller endast för instanser av komponenter som har aktiverat badging genom att redigera komponentkonfigurationen i [redigeringsläget](/help/communities/author-communities.md).

En boolesk egenskap, `allowBadges`, aktiverar/inaktiverar visning av emblem för en komponentinstans. Den kan konfigureras i [komponentredigeringsdialogrutan](/help/communities/author-communities.md) för forum-, QnA- och kommentarskomponenter via en kryssruta med namnet **Display Badges**.

#### Exempel: allowBadges för instans av forumkomponent {#example-allowbadges-for-forum-component-instance}

![enable-badges-component](assets/enable-badges-component.png)

>[!NOTE]
>
>Alla komponenter kan överlappas för att visa emblem med HBS-koden som finns i forumen, QnA och kommentarer som exempel.

## Poängregler {#scoring-rules}

Poängregler är grunden för poängsättning för att dela ut märken.

Varje resultatregel är en lista med en eller flera underlinjer. Poängregler tillämpas på communitywebbplatsinnehållet för att identifiera reglerna som ska gälla när emblem är aktiverade.

Poängregler ärvs men är inte additiva. Till exempel:

* Om sidan 2 innehåller resultatregel 2 och dess överordnade sida 1 innehåller resultatregel 1.
* En åtgärd på en sidkomponent2 anropar både regel1 och regel2.
* Om båda reglerna innehåller tillämpliga underlinjer för samma `topic/verb`:

   * Bara delpennan från regel2 påverkar poängen.
   * Poängen från båda undergrupperna läggs inte till.

Om det finns mer än en resultatregel bevaras poängen separat för varje regel.

Poängregler är noder av typen `cq:Page` med egenskaper på noden `jcr:content` som anger listan med underlinjer som definierar den.

Bakgrundsmusik lagras i SRP.

>[!NOTE]
>
>God praxis: ge varje resultatregel ett unikt namn.
>
>Poängregelnamn ska vara globalt unika. De får inte sluta med samma namn.
>
>Ett exempel på vad *inte* ska göra:
>
>/libs/settings/community/scoring/rules/site1/forums-scoring
>/libs/settings/community/scoring/rules/site2/forums-scoring

### Underregler för poängsättning {#scoring-sub-rules}

Värdena för att delta i communityt är de egenskaper som innehåller poängsättningsundergrupperna.

Varje bedömningsdelpensel identifierar:

* Vilka aktiviteter spåras?
* Vilken specifik communityfunktion är inblandad?
* Hur många poäng tilldelas?

Som standard tilldelas poäng till den medlem som utför en åtgärd, såvida inte delpennan anger att ägaren av innehållet tar emot punkterna ( `forOwner`).

Varje subrul kan ingå i en eller flera poängregler.

Namnet på underpennan följer vanligtvis mönstret för att använda ett *ämne*, *objekt* och *verb*. Till exempel:

* medlem-comment-create
* medlem-receive-voice

Underlinjer är noder av typen `cq:Page` med egenskaper på noden `jcr:content` som anger [verbs and topics](#topics-and-verbs) .

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
     <li>krävs; verbet motsvarar en händelseåtgärd</li>
     <li>det måste finnas minst en verb-egenskap</li>
     <li>verbet måste anges i VERSALER</li>
     <li>det kan finnas flera verb-egenskaper, men inga dubbletter</li>
     <li>värdet är poängvärdet som ska användas för den här händelsen</li>
     <li>värdet kan vara positivt eller negativt</li>
     <li>en lista över verb som stöds i den här versionen finns i avsnittet <a href="#topics-and-verbs">Ämnen och verb</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>Sträng</td>
   <td>
    <ul>
     <li>frivilligt; begränsar delpensel till communitykomponenter som identifieras av händelseämnen</li>
     <li>if specified : value is multi-value string of event topics</li>
     <li>en lista med ämnen i releasen finns i avsnittet <a href="#topics-and-verbs">Ämnen och verb</a></li>
     <li>standard ska gälla för alla ämnen som är kopplade till verberna</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>forOwner</code></td>
   <td>Boolean</td>
   <td>
    <ul>
     <li>valfritt, inte relevant när en medlem agerar på innehåll som han/hon äger</li>
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
     <li>valfritt, identifierar poängmotorn</li>
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

1. /libs/settings/community/scoring/rules/comments-scoring

   * subRules[] =
/libs/settings/community/scoring/rules/sub-rules/member-comment-create
/libs/settings/community/scoring/rules/sub-rules/member-receive-voice
/libs/settings/community/scoring/rules/sub-rules/member-give-voice
/libs/settings/community/scoring/rules/sub-rules/member-is-moderated

1. /libs/settings/community/scoring/rules/forums-scoring

   * subRules[] =
/libs/settings/community/scoring/rules/sub-rules/member-forum-create
/libs/settings/community/scoring/rules/sub-rules/member-receive-voice
/libs/settings/community/scoring/rules/sub-rules/member-give-voice
/libs/settings/community/scoring/rules/sub-rules/member-is-moderated

**Anteckningar:**

* Både `rules`- och `sub-rules`-noder är av typen cq:Page.

* `subRules` är ett attribut av typen String [] i regelnoden `jcr:content`.

* `sub-rules` kan delas mellan olika poängregler.
* `rules` ska finnas på en databasplats med läsbehörighet för alla.

   * Regelnamn måste vara unika oavsett plats.

### Aktivera anpassade poängsättningsregler {#activating-custom-scoring-rules}

Alla ändringar eller tillägg som görs i resultatregler eller underlinjer som görs i redigeringsmiljön måste installeras vid publiceringen.

## Märkningsregler {#badging-rules}

Regler för märkning länkar till poängregler genom att ange:

* Poängregel
* Poäng som krävs för att tilldelas ett specifikt märke

Badging-regler är noder av typen `cq:Page` med egenskaper på dess `jcr:content`-nod som korrelerar poängregler till poäng och emblem.

Reglerna för märkning består av en obligatorisk `thresholds`-egenskap som är en ordnad lista med poäng mappade till emblem. Poängen måste ordnas i högre värde. Till exempel:

* `1|/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * Ett bronze-märke tilldelas för att man tjänar en poäng.

* `60|/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

   * En silverbricka tilldelas när 60 poäng har samlats.

* `80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

   * En guldbricka utdelas när 80 poäng har samlats.

Betygsregler kombineras med poängregler, som bestämmer hur poäng ackumuleras. Se avsnittet [Använd regler för innehåll](#apply-rules-to-content).

Egenskapen `scoringRules` i en badging-regel begränsar helt enkelt vilka poängregler som kan paras med den speciella badging-regeln.

>[!NOTE]
>
>Bästa tillvägagångssätt: skapa unika emblem-bilder för varje AEM.

![badging-rule-configuration](assets/badging-rule-configuration.png)

<table>
 <tbody>
  <tr>
   <th>Egenskap</th>
   <th>Typ</th>
   <th>Värdebeskrivning</th>
  </tr>
  <tr>
   <td>tröskelvärden</td>
   <td>Sträng</td>
   <td><em>(obligatoriskt)</em> En sträng med flera värden i formatet number|path
    <ul>
     <li>number = score</li>
     <li>| = den lodräta linjen char (U+007C)</li>
     <li>sökväg = fullständig sökväg till badge-bildresurs</li>
    </ul> Strängarna måste ordnas så att siffrorna ökar i värde och inget tomt utrymme ska visas mellan talet och banan.<br /> Exempelpost:<br /> <code>80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Sträng</td>
   <td><em>(valfritt)</em> Identifierar bedömningsmotorn som antingen grundläggande eller avancerad. Om du vill använda den avancerade bedömningsmotorn läser du <a href="/help/communities/advanced.md">Avancerade poäng och märken</a>. Standardvärdet är "basic".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>Sträng</td>
   <td>(<em>valfri</em>) En sträng med flera värden som begränsar badging-regeln till bedömningshändelser som identifieras av poängreglerna</td>
  </tr>
 </tbody>
</table>

### Inkluderade märkningsregler {#included-badging-rules}

I utgåvan finns två märkningsregler som motsvarar [Forums- och kommentarsbedömningsreglerna](#includedscoringrules).

* `/libs/settings/community/badging/rules/comments-badging`

* `/libs/settings/community/badging/rules/forums-badging`

**Anteckningar:**

* `rules` noder är av typen cq:Page.
* `rules` ska finnas på en databasplats med läsbehörighet för alla.

   * Regelnamn måste vara unika oavsett plats.

### Aktivera anpassade märkningsregler {#activating-custom-badging-rules}

Alla ändringar eller tillägg som görs i märkningsregler eller bilder som gjorts i redigeringsmiljön måste installeras vid publicering.

## Tilldela och återkalla märken {#assign-and-revoke-badges}

Märkningar kan tilldelas medlemmar antingen med [medlemskonsolen](/help/communities/members.md#badges-tab) eller via programmering med cURL-kommandon.

Följande cURL-kommandon visar vad som krävs för en HTTP-begäran om att tilldela och återkalla emblem. Grundformatet är:

cURL -i -X POST -H *header* -u *signin* -F *operation* -F *badge* *member-profile-url*

*header* = &quot;Accept:application/json&quot;
anpassad rubrik som ska skickas till servern (obligatoriskt)

*inloggning* = administrator-id:password
till exempel admin:admin

*operation* = &quot;:operation=social:assignBadge&quot; OR &quot;:operation=social:deleteBadge&quot;

*badge* = &quot;badgeContentPath=*badge-image-file*&quot;

*badge-image-file* = platsen för badge-bildfilen i databasen
till exempel /libs/settings/community/badging/images/moderator/jcr:content/moderator.png

*member-profile-url* = slutpunkten för medlemmens profil vid publicering
till exempel https://&lt;server>:&lt;port>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>*Member-profile-url*:
>
>* Kan referera till en författarinstans om [tunneltjänsten](/help/communities/users.md#tunnel-service) är aktiverad.
>* Kan vara ett otydligt, slumpmässigt namn - se [Checklista för säkerhet](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path) angående auktoriseringsbart ID.

### Exempel: {#examples}

#### Tilldela ett moderatormärke {#assign-a-moderator-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

#### Återkalla ett tilldelat silvermärke {#revoke-an-assigned-silver-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:deleteBadge" -F "badgeContentPath=/libs/settings/community/badging/images/silver/jcr:content/silver.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

>[!NOTE]
>
>Om du använder cURL för att tilldela och återkalla emblem fungerar det för alla badge-bilder, men när de tilldelas i stället för EV markeras de som tilldelade märken och hanteras därefter.

## Betyg och märken för anpassade komponenter {#scoring-and-badges-for-custom-components}

Du kan skapa regler för klassificering och märkning för anpassade komponenter genom att koppla händelseavsnitten som skapats för komponenten till verb.

## Ämnen och verb {#topics-and-verbs}

När medlemmar interagerar med communityfunktioner skickas händelser som kan utlösa asynkrona avlyssnare, som meddelanden och poängsättning.

En komponents SocialEvent-instans registrerar händelserna som `actions` som inträffar för en `topic`. SocialEvent innehåller en metod för att returnera en `verb` som är associerad med åtgärden. Det finns en *n-1*-relation mellan `actions` och `verbs`.

För de communitykomponenter som levereras beskrivs `verbs` som definierats för varje `topic` som är tillgänglig för användning i [poängdelsregler](#scoring-sub-rules) i följande tabeller.

>[!NOTE]
>
>En ny boolesk egenskap, `allowBadges`, aktiverar/inaktiverar visning av emblem för en komponentinstans. Den kan konfigureras i uppdaterade [komponentredigeringsdialogrutor](/help/communities/author-communities.md) via en kryssruta med namnet **Visa emblem**.

**[Kalenderkomponent](/help/communities/calendar.md)**
SocialEvent `topic`= com/adobe/cq/social/calendar

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar en kalenderhändelse |
| LÄGG TILL | kommentarer från medlemmar i en kalenderhändelse |
| UPPDATERA | medlemmens kalenderhändelse eller -kommentar har redigerats |
| DELETE | medlemmens kalenderhändelse eller -kommentar tas bort |

**[Kommentarskomponent](/help/communities/comments.md)**
SocialEvent `topic`= com/adobe/cq/social/comment

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar en kommentar |
| LÄGG TILL | medlemssvar på kommentarer |
| UPPDATERA | Medlemmens kommentar har redigerats |
| DELETE | medlemmens kommentar har tagits bort |

**[Filbibliotekskomponent](/help/communities/file-library.md)**
SocialEvent `topic`= com/adobe/cq/social/fileLibrary

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar en mapp |
| BIFOGA | medlem överför en fil |
| UPPDATERA | medlemmen uppdaterar en mapp eller fil |
| DELETE | medlem tar bort en mapp eller fil |

**[Forumkomponent](/help/communities/forum.md)**
SocialEvent `topic`= com/adobe/cq/social/forum

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar forumämne |
| LÄGG TILL | medlemssvar på forumämnet |
| UPPDATERA | Medlemmens forum eller svar har redigerats |
| DELETE | forumämnet eller svaret för en medlem tas bort |

**[Journalkomponent](/help/communities/blog-feature.md)**
SocialEvent `topic`= com/adobe/cq/social/journal

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar en bloggartikel |
| LÄGG TILL | kommentarerna på en bloggartikel |
| UPPDATERA | Medlemmens bloggartikel eller kommentar redigeras |
| DELETE | Medlemmens bloggartikel eller kommentar tas bort |

**[QnA-komponent](/help/communities/working-with-qna.md)**
SocialEvent `topic` = com/adobe/cq/social/qna

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar en QnA-fråga |
| LÄGG TILL | medlem skapar ett QnA-svar |
| UPPDATERA | -medlemmens fråga eller svar har redigerats |
| MARKERA | Medlemmens svar är markerat |
| AVMARKERA | Medlemmens svar är avmarkerat |
| DELETE | en medlems fråga eller svar tas bort |

**[Granskningskomponent](/help/communities/reviews.md)**
SocialEvent `topic`= com/adobe/cq/social/review

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar granskning |
| UPPDATERA | Medlemmens granskning har redigerats |
| DELETE | Medlemmens granskning har tagits bort |

**[Värderingskomponent](/help/communities/rating.md)**
SocialEvent `topic`= com/adobe/cq/social/tally/rating

| **Verb** | **Beskrivning** |
|---|---|
| LÄGG TILL KLASSIFICERING | Medlemmens innehåll har fått en högre gradering |
| TA BORT KLASSIFICERING | medlemmens innehåll har nedgraderats |

**[Röstkomponent](/help/communities/voting.md)**
SocialEvent `topic`= com/adobe/cq/social/tally/voice

| **Verb** | **Beskrivning** |
|---|---|
| LÄGG TILL RÖST | Medlemmens innehåll har röstats upp |
| TA BORT RÖSTNING | Medlemmens innehåll har inte röstats ned |

**Modereringsaktiverade komponenter**
SocialEvent `topic`= com/adobe/cq/social/moderation

| **Verb** | **Beskrivning** |
|---|---|
| NEKA | Medlemmens innehåll nekas |
| FLAGGA-SOM-OLÄMPLIGT | medlemmens innehåll är flaggat |
| OLÄMPLIG FLAGNING SOM | medlemmens innehåll är oflaggat |
| GODKÄNN | Medlemmens innehåll godkänns av moderatorn |
| STÄNG | medlem stänger kommentarer till redigeringar och svar |
| ÖPPNA | medlem återöppnar kommentar |

### Anpassade komponenthändelser {#custom-component-events}

För en anpassad komponent instansieras en SocialEvent för att spela in komponentens händelser som `actions` som inträffar för en `topic`.

SocialEvent måste åsidosätta metoden `getVerb()` så att en lämplig `verb` returneras för varje `action` för att stödja poängsättningen. `verb` som returneras för en åtgärd kan vara en vanlig (t.ex. `POST`) eller en speciell för komponenten (t.ex. `ADD RATING`). Det finns en *n-1*-relation mellan `actions` och `verbs`.

## Felsökning {#troubleshooting}

### Inga märken visas {#badges-are-not-appearing}

Om regler för klassificering och märkning har tillämpats på webbplatsens innehåll, men emblem inte tilldelas för någon aktivitet, kontrollerar du att emblem har aktiverats för komponentens förekomst.

Se [Aktivera emblem för komponent](#enable-badges-for-component).

### Poängregeln har ingen effekt {#scoring-rule-has-no-effect}

Om regler för poängsättning och märkning har tillämpats på webbplatsens innehåll, och emblem tilldelas för vissa åtgärder, men inte andra, kontrollerar du att badging-regeln inte har begränsat de poängregler som den gäller för.

Se egenskapen `scoringRules` i [Badging Rules](#badging-rules).

### Skiftlägeskänslig typo {#case-sensitive-typo}

De flesta egenskaper och värden, särskilt verbet, är skiftlägeskänsliga. Verb måste vara VERSALER när de används i en subpensel.

Om funktionen inte fungerar som förväntat kontrollerar du att data har angetts korrekt.

## Snabbtest {#quick-test}

Det går snabbt att testa poängsättning och märkning med hjälp av webbplatsen [Komma igång med självstudiekursen](/help/communities/getting-started.md) (engagera):

* Öppna CRXDE Lite på författaren.
* Bläddra till bassidan:

   * /content/sites/engage/en/jcr:content

* Lägg till egenskapen badgingRules:

   * **Namn**: `badgingRules`
   * **Typ**: `String`
   * Välj **Multi**
   * Välj **Lägg till**
   * Ange `/libs/settings/community/badging/rules/forums-badging`
   * Markera **+**
   * Ange `/libs/settings/community/badging/rules/comments-badging`
   * Välj **OK**

* Lägg till egenskapen scoringRules:

   * **Namn**: `scoringRules`
   * **Typ**: `String`
   * Välj **Multi**
   * Välj **Lägg till**
   * Ange `/libs/settings/community/scoring/rules/forums-scoring`
   * Markera **+**
   * Ange `/libs/settings/community/scoring/rules/comments-scoring`
   * Välj **OK**

* Välj **Spara alla**.

![test-scoring-badging](assets/test-scoring-badging.png)

Kontrollera sedan att forumkomponenterna och kommentarkomponenterna tillåter att märken visas:

* Återigen med CRXDE Lite.
* Bläddra till forumkomponenten

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`

* Lägg till den booleska egenskapen allowBadges, om det behövs, och kontrollera att den är true.

   * **Namn**: `allowBadges`
   * **Typ**: `Boolean`
   * **Värde**: `true`

![test-forum-component](assets/test-forum-component.png)

[Publicera](/help/communities/sites-console.md#publishing-the-site) igen på communitywebbplatsen.

Äntligen

* Bläddra till komponenten i publiceringsinstansen.
* Logga in som community-medlem (till exempel weston.mccall@dodgit.com/lösenord).
* Post är ett nytt forum.
* Sidan måste uppdateras för att emblemet ska kunna visas.

   * Logga ut och logga in som en annan community-medlem (till exempel: aaron.mcdonald@mailinator.com/password).

* Välj forum.

Detta bör göra att communitymedlemmen får ett bronze-märke synligt med sitt foruminlägg eftersom den första tröskeln för forumbadging är ett poäng på 1.

![bronzebadge](assets/bronzebadge.png)

## Ytterligare information {#additional-information}

Mer information finns på sidan [Värderingsläge och emblem Essentials](/help/communities/configure-scoring.md) för utvecklare.

Mer information om den avancerade bedömningsmotorn finns i [Avancerade poäng och märken](/help/communities/advanced.md).

Den konfigurerbara huvudpanelen [component](/help/communities/enabling-leaderboard.md) och [function](/help/communities/functions.md#leaderboard-function) förenklar visningen av medlemmar och deras poäng på en communitywebbplats.
