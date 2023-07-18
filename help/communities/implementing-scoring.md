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
source-git-commit: d3c40d1452217983b01245ec1c81111a3c4e7295
workflow-type: tm+mt
source-wordcount: '2853'
ht-degree: 0%

---

# Communities Scoring and Badges {#communities-scoring-and-badges}

## Översikt {#overview}

AEM Communities poäng och badges ger möjlighet att identifiera och belöna communitymedlemmar.

De viktigaste aspekterna på poängsättning och märkning är:

* [Tilldela märken](#assign-and-revoke-badges) identifiera en medlems roll i communityn.

* [Grundläggande tilldelning av märken](#enable-scoring) till medlemmarna för att uppmuntra dem att delta (mängden innehåll som skapas).

* [Avancerad tilldelning av märken](/help/communities/advanced.md) för att identifiera medlemmar som experter (kvaliteten på det innehåll som skapas).

**Anteckning** att det är [inte aktiverat som standard](/help/communities/implementing-scoring.md#main-pars-text-237875536).

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

Communities [Badges Console](/help/communities/badges.md) Med kan du lägga till egna emblem som kan visas för en medlem när den har förtjänats (tilldelats) eller när de får en viss roll i communityn (tilldelade).

### Tilldelade märken {#assigned-badges}

Rollbaserade märken tilldelas av en administratör till communitymedlemmar baserat på deras roll i communityn.

Tilldelade (och tilldelade) märken lagras i det valda [SRP](/help/communities/srp.md) och är inte direkt tillgängliga. Det enda sättet att tilldela rollbaserade emblem är att göra det med kod eller cURL tills ett GUI är tillgängligt. Instruktioner för cURL finns i avsnittet med rubriken [Tilldela och återkalla märken](#assign-and-revoke-badges).

I releasen finns tre rollbaserade märken:

* **moderator**
  `/libs/settings/community/badging/images/moderator/jcr:content/moderator.png`

* **gruppansvarig**
  `/libs/settings/community/badging/images/group-manager/jcr:content/group-manager.png`

* **behörig medlem**
  `/libs/settings/community/badging/images/privileged-member/jcr:content/privileged-member.png`

  ![tilldelad-badges](assets/assigned-badges.png)

### Tilldelade märken {#awarded-badges}

Belöningsbaserade märken delas ut av betygstjänsten till communitymedlemmar baserat på regler som tillämpas på deras verksamhet i communityn.

För att emblem ska visas som en belöning för aktivitet måste två saker hända:

* Badging måste vara [aktiverad](#enableforcomponent) för funktionskomponenten.
* Regler för poängsättning och märkning måste vara [använd](#applytopage) till den sida (eller det överordnade objekt) som komponenten är placerad på.

I releasen ingår tre belöningsbaserade märken:

* **guld**
  `/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

* **silver**
  `/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

* **brons**
  `/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

  ![tilldelade-emblem](assets/awarded-badges.png)

>[!NOTE]
>
>Poängregler kan konfigureras för att tilldela negativa punkter för inlägg som markerats som olämpliga och därmed påverka poängvärdet. När ett märke har skapats tas det dock inte bort automatiskt på grund av ändringar i poängsättningsregeln eller poängsättningsregeln.
>
>Tilldelade märken kan återkallas på samma sätt som tilldelade märken. Se [Tilldela och återkalla märken](#assign-and-revoke-badges) -avsnitt. Framtida förbättringar kommer att omfatta ett användargränssnitt för att hantera medlemmarnas märken.

### Egna märken {#custom-badges}

Anpassade märken kan installeras med [Badges Console](/help/communities/badges.md) och antingen har tilldelats eller angetts i märkningsreglerna.

Anpassade märken replikeras automatiskt till publiceringsmiljön när de installeras från badges-konsolen.

## Aktivera poängsättning {#enable-scoring}

Poängen är inte aktiverad som standard. De grundläggande stegen för att sätta upp och aktivera poängsättning och tilldelning av märken är:

* Identifiera regler för intäktspunkter ([poängregler](#scoring-rules)).
* För poäng som ackumuleras per poängregler tilldelar du [emblem](#badges) ([regler för emblem](#badging-rules)).

* [Använd regler för poäng och utmärkelser på en communitywebbplats](#apply-rules-to-content).
* [Aktivera märkning för communityfunktioner](#enable-badges-for-component).

Se [Snabbtest](#quick-test) om du vill aktivera poängsättning för en communitywebbplats med standardreglerna för poäng och märkning för forum och kommentarer.

### Använd regler för innehåll {#apply-rules-to-content}

Om du vill aktivera poängsättning och märken lägger du till egenskaperna `scoringRules` och `badgingRules` till valfri nod i platsens innehållsträd.

Om webbplatsen redan är publicerad, efter att du har tillämpat alla regler och aktiverat komponenter, publicerar du om den.

Reglerna som gäller för en komponent som har aktiverats för badging är reglerna för den aktuella noden eller dess överordnade nod.

Om noden är av typen `cq:Page` (rekommenderas) och sedan använda CRXDE|Lite för att lägga till egenskaperna i `jcr:content` nod.

| **Egenskap** | **Typ** | **Beskrivning** |
|---|---|---|
| badgingRules | Sträng | en matrislista med [regler för emblem](#badging-rules) |
| scoringRules | Sträng | en matrislista med [poängregler](#scoring-rules) |

>[!NOTE]
>
>Om en bedömningsregel inte verkar ha någon effekt på att dela ut taggar kontrollerar du att resultatregeln inte har blockerats av spårningsregelns egenskap scoringRules. Se avsnittet [Märkningsregler](#badging-rules).

### Aktivera emblem för komponent {#enable-badges-for-component}

Poäng- och streckreglerna gäller endast för instanser av komponenter som har aktiverat badging genom att redigera komponentkonfigurationen i [redigeringsläge](/help/communities/author-communities.md).

En boolesk egenskap, `allowBadges`, aktiverar/inaktiverar visning av emblem för en komponentinstans. Den kan konfigureras i [redigeringsdialogruta för komponent](/help/communities/author-communities.md) för forum, QnA och kommentarkomponenter via en kryssruta med etiketten **Visa emblem**.

#### Exempel: allowBadges för instans av forumkomponent {#example-allowbadges-for-forum-component-instance}

![enable-badges-component](assets/enable-badges-component.png)

>[!NOTE]
>
>Alla komponenter kan överlappas för att visa emblem med HBS-koden som finns i forumen, QnA och kommentarer som exempel.

## Poängregler {#scoring-rules}

Poängregler är grunden för poängsättning för att dela ut märken.

Varje resultatregel är en lista med en eller flera underlinjer. Poängregler tillämpas på communitywebbplatsinnehållet för att identifiera de regler som ska gälla när emblem är aktiverade.

Poängregler ärvs men är inte additiva. Till exempel:

* Om sidan 2 innehåller resultatregel 2 och dess överordnade sida 1 innehåller resultatregel 1.
* En åtgärd på en sidkomponent2 anropar både regel1 och regel2.
* Om båda reglerna innehåller tillämpliga delregler för samma `topic/verb`:

   * Bara delpennan från regel2 påverkar poängen.
   * Poängen från båda undergrupperna läggs inte till.

Om det finns mer än en resultatregel bevaras poängen separat för varje regel.

Poängregler är noder av typen `cq:Page` med egenskaper på `jcr:content` nod som anger listan med underlinjer som definierar den.

Bakgrundsmusik lagras i SRP.

>[!NOTE]
>
>God praxis: unikt namn för varje poängregel.
>
>Poängregelnamnen ska vara globalt unika. de ska inte sluta med samma namn.
>
>Ett exempel på vad *not* att göra:
>
>/libs/settings/community/scoring/rules/site1/forums-scoring
>/libs/settings/community/scoring/rules/site2/forums-scoring

### Underregler för poängsättning {#scoring-sub-rules}

Värdena för att delta i communityt är de egenskaper som innehåller poängsättningsundergrupperna.

Varje bedömningsdelpensel identifierar:

* Vilka aktiviteter spåras?
* Vilken specifik communityfunktion är inblandad?
* Hur många poäng tilldelas?

Som standard tilldelas poäng till den medlem som utför åtgärden, såvida inte underrubriken anger att ägaren av innehållet tar emot poängen ( `forOwner`).

Varje subrul kan ingå i en eller flera poängregler.

Namnet på subruLen följer vanligtvis mönstret för att använda en *ämne*, *object* och *verb*. Till exempel:

* medlem-comment-create
* medlem-receive-voice

Underlinjer är noder av typen `cq:Page` med egenskaper på `jcr:content`nod som anger [verb och ämnen](#topics-and-verbs) .

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
     <li>en lista över verb som stöds i den här versionen finns i <a href="#topics-and-verbs">Ämnen och verb</a> section</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>Sträng</td>
   <td>
    <ul>
     <li>frivilligt, begränsar delpensel till communitykomponenter som identifieras av händelseämnen</li>
     <li>om angivet: värdet är en sträng med flera värden för händelseämnen</li>
     <li>en lista med ämnen i releasen finns i <a href="#topics-and-verbs">Ämnen och verb</a> section</li>
     <li>standard ska gälla för alla ämnen som är kopplade till verbet</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>forOwner</code></td>
   <td>Boolean</td>
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
       <li>kräver <a href="/help/communities/advanced.md">extra paket</a></li>
      </ul> </li>
     <li>default is "basic"</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Inkluderade poängsättningsregler och underregler {#included-scoring-rules-and-sub-rules}

I releasen finns två poängregler för [Forum](/help/communities/functions.md#forum-function) (en för var och en för forumfunktionen och kommentarskomponenterna för forumfunktionen):

1. /libs/settings/community/scoring/rules/comments-scoring

   * subRules[] = /libs/settings/community/scoring/rules/sub-rules/member-comment-create /libs/settings/community/scoring/rules/sub-rules/member-receive-voice /libs/settings/community/scoring/rules/sub-rules/member-give-voice /libs/settings/community/scoring/rules/sub-rules/member-is-moderated

1. /libs/settings/community/scoring/rules/forums-scoring

   * subRules[] = /libs/settings/community/scoring/rules/sub-rules/member-forum-create /libs/settings/community/scoring/rules/sub-rules/member-receive-voice /libs/settings/community/scoring/rules/sub-rules/member-give-voice /libs/settings/community/scoring/rules/sub-rules/member-is-moderated

**Anteckningar:**

* Båda `rules` och `sub-rules` noder är av typen cq:Page.

* `subRules` är ett attribut av typen String[] på regelns `jcr:content` nod.

* `sub-rules` kan delas mellan olika poängregler.
* `rules` ska finnas på en databasplats med läsbehörighet för alla.

   * Regelnamn måste vara unika oavsett plats.

### Aktivera anpassade poängsättningsregler {#activating-custom-scoring-rules}

Alla ändringar eller tillägg som görs i resultatregler eller underlinjer som görs i redigeringsmiljön måste installeras vid publiceringen.

## Märkningsregler {#badging-rules}

Regler för märkning länkar till poängregler genom att ange:

* Poängregel
* Poäng som krävs för att tilldelas ett specifikt märke

Märkningsregler är noder av typen `cq:Page` med egenskaper på `jcr:content` nod som korrelerar poängregler till poäng och emblem.

Reglerna för märkning består av ett obligatoriskt `thresholds` egenskap som är en ordnad lista över bakgrundsmusik mappad till emblem. Poängen måste ordnas i högre värde. Till exempel:

* `1|/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * Ett bronze-märke tilldelas för att man tjänar en poäng.

* `60|/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

   * En silverbricka tilldelas när 60 poäng har samlats.

* `80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

   * En guldbricka utdelas när 80 poäng har samlats.

Betygsregler kombineras med poängregler, som bestämmer hur poäng ackumuleras. Se avsnittet [Använd regler för innehåll](#apply-rules-to-content).

The `scoringRules` egenskapen för en badging-regel begränsar helt enkelt vilka poängregler som kan kombineras med den speciella badging-regeln.

>[!NOTE]
>
>God praxis: skapa unika emblem-bilder för varje AEM.

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
   <td><em>(obligatoriskt)</em> En sträng med flera värden i formatet 'number|path'
    <ul>
     <li>number = score</li>
     <li>| = den lodräta linjen char (U+007C)</li>
     <li>sökväg = fullständig sökväg till badge-bildresurs</li>
    </ul> Strängarna måste ordnas så att siffrorna ökar i värde och inget tomt utrymme ska visas mellan talet och banan.<br /> Exempelpost:<br /> <code>80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Sträng</td>
   <td><em>(valfritt)</em> Identifierar bedömningsmotorn som antingen "grundläggande" eller "avancerad". Om du vill använda den avancerade bedömningsmotorn läser du <a href="/help/communities/advanced.md">Advanced Scoring and Badges</a>. Standardvärdet är "basic".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>Sträng</td>
   <td>(<em>valfri</em>) En sträng med flera värden som begränsar badging-regeln till bedömningshändelser som identifieras av poängsättningsreglerna</td>
  </tr>
 </tbody>
</table>

### Inkluderade märkningsregler {#included-badging-rules}

I releasen finns två badging-regler som motsvarar [Ordningsregler för forum och kommentarer](#includedscoringrules).

* `/libs/settings/community/badging/rules/comments-badging`

* `/libs/settings/community/badging/rules/forums-badging`

**Anteckningar:**

* `rules` noder är av typen cq:Page.
* `rules` ska finnas på en databasplats med läsbehörighet för alla.

   * Regelnamn måste vara unika oavsett plats.

### Aktivera anpassade märkningsregler {#activating-custom-badging-rules}

Alla ändringar eller tillägg som görs i märkningsregler eller bilder som gjorts i redigeringsmiljön måste installeras vid publicering.

## Tilldela och återkalla märken {#assign-and-revoke-badges}

Medlemmar kan tilldelas märken antingen med [medlemskonsol](/help/communities/members.md#badges-tab) eller programmatiskt med cURL-kommandon.

Följande cURL-kommandon visar vad som krävs för en HTTP-begäran om att tilldela och återkalla emblem. Grundformatet är:

cURL -i -X POST -H *header* -u *signera* -F *operation* -F *bricka* *member-profile-url*

*header* = &quot;Acceptera:program/json&quot;, anpassad rubrik som ska skickas till servern (obligatoriskt)

*signera* = administrator-id:password till exempel : admin:admin

*operation* = &quot;:operation=social:assignBadge&quot; OR &quot;:operation=social:deleteBadge&quot;

*bricka* = &quot;badgeContentPath=*badge-image-file*&quot;

*badge-image-file* = platsen för badge-bildfilen i databasen, till exempel: /libs/settings/community/badging/images/moderator/jcr:content/moderator.png

*member-profile-url* = slutpunkten för medlemmens profil vid publicering, till exempel: https://&lt;server>:&lt;port>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>The *member-profile-url*:
>
>* Kan referera till en författarinstans om [Tunneltjänst](/help/communities/users.md#tunnel-service) är aktiverat.
>* Kan vara ett otydligt, slumpmässigt namn - se [Säkerhetschecklista](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path) om auktoriseringsbart ID.

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

En komponents SocialEvent-instans registrerar händelserna som `actions` som inträffar för en `topic`. SocialEvent innehåller en metod för att returnera en `verb` som är associerad med åtgärden. Det finns en *n-1* relation mellan `actions` och `verbs`.

För de communitykomponenter som levereras beskrivs följande tabeller `verbs` definierad för varje `topic` finns att använda i [betygsdelkurvor](#scoring-sub-rules).

>[!NOTE]
>
>En ny boolesk egenskap, `allowBadges`, aktiverar/inaktiverar visning av emblem för en komponentinstans. Den kan konfigureras i uppdaterad [dialogrutor för komponentredigering](/help/communities/author-communities.md) genom en kryssruta med etiketten **Visa emblem**.

**[Kalenderkomponent](/help/communities/calendar.md)**
SocialEvent `topic`= com/adobe/cq/social/calendar

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar en kalenderhändelse |
| LÄGG TILL | kommentarer från medlemmar i en kalenderhändelse |
| UPPDATERA | medlemmens kalenderhändelse eller -kommentar har redigerats |
| DELETE | medlemmens kalenderhändelse eller -kommentar tas bort |

**[Komponenten Kommentarer](/help/communities/comments.md)**
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

**[Forum-komponent](/help/communities/forum.md)**
SocialEvent `topic`= com/adobe/cq/social/forum

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar forumämne |
| LÄGG TILL | medlemssvar på forumämnet |
| UPPDATERA | Medlemmens forumämne eller svar har redigerats |
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
| MARKERA | Medlemmens svar har valts |
| AVMARKERA | Medlemmens svar är avmarkerat |
| DELETE | en medlems fråga eller svar tas bort |

**[Granskningskomponent](/help/communities/reviews.md)**
SocialEvent `topic`= com/adobe/cq/social/review

| **Verb** | **Beskrivning** |
|---|---|
| POST | medlem skapar granskning |
| UPPDATERA | Medlemmens granskning har redigerats |
| DELETE | Medlemmens granskning har tagits bort |

**[Klassificeringskomponent](/help/communities/rating.md)**
SocialEvent `topic`= com/adobe/cq/social/tally/rating

| **Verb** | **Beskrivning** |
|---|---|
| LÄGG TILL KLASSIFICERING | Medlemmens innehåll har fått en högre gradering |
| TA BORT KLASSIFICERING | medlemmens innehåll har nedgraderats |

**[Röstkomponent](/help/communities/voting.md)**
SocialEvent `topic`= com/adobe/cq/social/tally/röstande

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
| ACCEPTERA | Medlemmens innehåll godkänns av moderatorn |
| STÄNG | medlem stänger kommentarer till redigeringar och svar |
| ÖPPNA | medlem återöppnar kommentar |

### Anpassade komponenthändelser {#custom-component-events}

För en anpassad komponent instansieras en SocialEvent för att spela in komponentens händelser som `actions` som inträffar för en `topic`.

SocialEvent måste åsidosätta metoden för att stödja poängsättningen `getVerb()` så att `verb` returneras för varje `action`. The `verb` som returneras för en åtgärd kan vara en vanlig åtgärd (t.ex. `POST`) eller en som är specialiserad på komponenten (till exempel `ADD RATING`). Det finns en *n-1* relation mellan `actions` och `verbs`.

## Felsökning {#troubleshooting}

### Inga märken visas {#badges-are-not-appearing}

Om regler för klassificering och märkning har tillämpats på webbplatsens innehåll, men emblem inte tilldelas för någon aktivitet, kontrollerar du att emblem har aktiverats för komponentens förekomst.

Se [Aktivera emblem för komponent](#enable-badges-for-component).

### Poängregeln har ingen effekt {#scoring-rule-has-no-effect}

Om regler för poängsättning och märkning har tillämpats på webbplatsens innehåll, och emblem tilldelas för vissa åtgärder, men inte andra, kontrollerar du att badging-regeln inte har begränsat de poängregler som den gäller för.

Se `scoringRules` egenskap för [Märkningsregler](#badging-rules).

### Skiftlägeskänslig typo {#case-sensitive-typo}

De flesta egenskaper och värden, särskilt verbet, är skiftlägeskänsliga. Verb måste vara VERSALER när de används i en subpensel.

Om funktionen inte fungerar som väntat kontrollerar du att data har angetts korrekt.

## Snabbtest {#quick-test}

Det går snabbt att testa poängsättning och märkning med [Komma igång, självstudiekurs](/help/communities/getting-started.md) (engagera) webbplats:

* Öppna CRXDE Lite på författaren.
* Bläddra till bassidan:

   * /content/sites/engage/en/jcr:content

* Lägg till egenskapen badgingRules:

   * **Namn**: `badgingRules`
   * **Typ**: `String`
   * Välj **Flera**
   * Välj **Lägg till**
   * Retur `/libs/settings/community/badging/rules/forums-badging`
   * Välj **+**
   * Retur `/libs/settings/community/badging/rules/comments-badging`
   * Välj **OK**

* Lägg till egenskapen scoringRules:

   * **Namn**: `scoringRules`
   * **Typ**: `String`
   * Välj **Flera**
   * Välj **Lägg till**
   * Retur `/libs/settings/community/scoring/rules/forums-scoring`
   * Välj **+**
   * Retur `/libs/settings/community/scoring/rules/comments-scoring`
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

Nästa, [publicera igen](/help/communities/sites-console.md#publishing-the-site) communitywebbplatsen.

Äntligen

* Bläddra till komponenten i publiceringsinstansen.
* Logga in som community-medlem (till exempel: weston.mccall@dodgit.com / lösenord).
* Lägg upp ett nytt forumämne.
* Sidan måste uppdateras för att märket ska kunna visas.

   * Logga ut och logga in som en annan community-medlem (till exempel: aaron.mcdonald@mailinator.com/lösenord).

* Välj forum.

Detta bör göra att communitymedlemmen får ett bronze-märke synligt med sitt foruminlägg eftersom den första tröskeln för forumbadging är ett poäng på 1.

![bronzebadge](assets/bronzebadge.png)

## Ytterligare information {#additional-information}

Mer information finns på [Grundläggande om poäng och emblem](/help/communities/configure-scoring.md) för utvecklare.

Mer information om den avancerade bedömningsmotorn finns i [Advanced Scoring and Badges](/help/communities/advanced.md).

Konfigurerbar huvudpanel [komponent](/help/communities/enabling-leaderboard.md) och [function](/help/communities/functions.md#leaderboard-function) gör det enklare att visa medlemmar och deras poäng på en communitywebbplats.
