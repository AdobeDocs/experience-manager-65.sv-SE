---
title: Advanced Scoring and Badges
seo-title: Advanced Scoring and Badges
description: Konfigurera avancerad poängsättning
seo-description: Konfigurera avancerad poängsättning
uuid: 48caca57-43d3-4f2f-adf3-257428ba54d5
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: eb3d5c37-8097-46de-8c4f-804ea723f1c5
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Advanced Scoring and Badges{#advanced-scoring-and-badges}

## Översikt {#overview}

Med avancerad poängsättning kan man tilldela märken för att identifiera medlemmar som experter. Avancerad poängsättning tilldelar poäng baserat på mängden *och *kvalitet på innehåll som skapats av en medlem, medan grundläggande poängberäkning tilldelar poäng helt enkelt baserat på mängden innehåll som skapas.

Denna skillnad beror på poängsättningsmotorn som används för att beräkna poängen. Den grundläggande poängsättningsmotorn använder enkel matematik. Den avancerade bedömningsmotorn är en adaptiv algoritm som belönar aktiva medlemmar som bidrar med värdefullt och relevant innehåll, som dras av genom ämnesens naturliga språkbearbetning.

Förutom innehållets relevans tar bedömningsalgoritmerna hänsyn till medlemsaktiviteter, som röstning och procent av svaren. Även om grundläggande poängsättning innehåller dem kvantitativt, används de algoritmiskt i avancerad poängsättning.

Den avancerade bedömningsmotorn kräver därför tillräckligt med data för att göra analysen meningsfull. Tröskelvärdet för att bli expert omprövas ständigt när algoritmen kontinuerligt anpassas till volymen och kvaliteten på det innehåll som skapas. Det finns också ett koncept för *minskning *av en medlems tidigare tjänster. Om en expertmedlem slutar delta i det ämne där han/hon fick expertstatus, kan han/hon vid någon förutbestämd tidpunkt (se [poängsättningsmotorkonfigurationen](#configurable-scoring-engine)) förlora sin status som expert.

Att ställa in avancerad poängsättning är i stort sett detsamma som grundläggande poängsättning:

* grundläggande och avancerade regler för poängsättning och märkning [tillämpas på innehåll](/help/communities/implementing-scoring.md#apply-rules-to-content) på samma sätt

   * grundläggande och avancerade regler för poängsättning och märkning kan tillämpas på samma innehåll

* [aktivering av märken för komponenter](/help/communities/implementing-scoring.md#enable-badges-for-component) är generiskt

Skillnaderna i hur du ställer in poängsättnings- och badging-regler är:

* konfigurerbar, avancerad bedömningsmotor
* avancerade poängregler:

   * scoringType inställd på &#39;advanced&#39;
   * kräver stoppord

* avancerade regler för märkning:

   * badgingType inställd på &#39;advanced&#39;
   * badgingLevels set to number of expert levels to award
   * kräver badgingPaths-matris av badges i stället för att mappa punkter till badges för trösklar

>[!NOTE]
>
>Om du vill använda avancerade funktioner för bedömning och märkning installerar du [expertpaketet](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/social/cq-social-expert-identification-pkg).

## Konfigurerbar bedömningsmotor {#configurable-scoring-engine}

Den avancerade bedömningsmotorn tillhandahåller en OSGi-konfiguration med parametrar som påverkar den avancerade bedömningsalgoritmen.

![chlimage_1-139](assets/chlimage_1-139.png)

* **poängsättningsvikter** För ett ämne anger du det verb som ska ha högst prioritet när du beräknar poängen. Ett eller flera ämnen kan anges, men begränsas till **ett verb per ämne**. Se [Ämnen och Verb](/help/communities/implementing-scoring.md#topics-and-verbs).
Angicks som `topic,verb` med kommatecknet escape. Exempel:
   `/social/forum/hbs/social/forum\,ADD`
Standardvärdet är ADD-verbet för QnA- och forumkomponenter.

* **poängintervall**Intervallet för avancerade poäng definieras av det här värdet (maximal poäng) och 0 (lägsta möjliga poäng).
Standardvärdet är 100 så att poängintervallet är 0-100.

* **tidsintervall**för entitetsminskning Den här parametern representerar antalet timmar efter vilka alla entitetsmoment dekanteras. Detta krävs för att inte längre inkludera gammalt innehåll i poängen för en community-webbplats.
Standardvärdet är 216000 timmar (~24 år).

* **poängsättningstillväxthastighet**Detta anger poängen mellan 0 och poängintervallet, efter vilket tillväxten saktar ned för att begränsa antalet experter.
Standardvärdet är 50.

## Avancerade poängregler {#advanced-scoring-rules}

Vid grundläggande poängsättning är den kvantitet som behövs för att få ett märke känd.

Vid avancerad poängsättning justeras mängden som behövs hela tiden baserat på mängden kvalitetsdata i systemet. Poängen beräknas kontinuerligt på ungefär samma sätt som en klockkurva.

Om en medlem har fått ett expertmärke för ett ämne som inte längre är aktivt, finns det en risk att de förlorar sitt märke på grund av att de har gått ner över tiden.

### scoringType {#scoringtype}

En resultatregel är en uppsättning underregler, som alla deklarerar `scoringType`.

Om du vill anropa den avancerade bedömningsmotorn `scoringType`bör du ange den till `advanced`.

Se [Underregler](/help/communities/implementing-scoring.md#scoring-sub-rules)för poängsättning.

![chlimage_1-140](assets/chlimage_1-140.png)

### Stoppord {#stopwords}

Det avancerade poängsättningspaketet installerar en konfigurationsmapp som innehåller en stoppordsfil:

* /etc/community/scoring/configuration/stopwords

Den avancerade bedömningsalgoritmen använder listan med ord i stoppordsfilen för att identifiera vanliga engelska ord som ignoreras under innehållsbearbetningen.

Det finns ingen anledning att anta att den här filen kommer att ändras.

Om stoppordsfilen saknas genereras ett fel i den avancerade bedömningsmotorn.

## Avancerade märkningsregler {#advanced-badging-rules}

De avancerade egenskaperna för märkningsregeln skiljer sig från de [grundläggande märkningsregelegenskaperna](/help/communities/implementing-scoring.md#badging-rules).

I stället för att associera punkter med en badge-bild är det bara nödvändigt att identifiera det antal experter som tillåts och den badge-bild som ska tilldelas.

![chlimage_1-141](assets/chlimage_1-141.png)

<table>
 <tbody>
  <tr>
   <th>Egenskap</th>
   <th>Typ</th>
   <th>Värdebeskrivning</th>
  </tr>
  <tr>
   <td>badgingPath</td>
   <td>Sträng[]</td>
   <td><em>(obligatoriskt)</em> En sträng med flera värden av badge-bilder upp till antalet badgingLevels. Sökvägarna för taggbilder måste beställas så att den första tilldelas den högsta experten. Om det finns färre emblem än vad som anges av badgingLevels fyller det sista märket i arrayen ut resten av arrayen.  Exempelpost:<br /> <code>/etc/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>badgingLevels</td>
   <td>Lång</td>
   <td><em>(valfritt)</em> Anger vilka kunskapsnivåer som ska tilldelas. Om det till exempel ska finnas ett <code>expert </code>och ett <code>almost expert</code> (två emblem), ska värdet anges till 2. badgingLevel ska motsvara antalet expertrelaterade badge-bilder som anges för egenskapen badgingPath. Standardvärdet är 1.</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Sträng</td>
   <td><em>(obligatoriskt)</em> Identifierar bedömningsmotorn som antingen grundläggande eller avancerad. Ange som "avancerat", annars är standardvärdet "grundläggande".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>Sträng[]</td>
   <td><em>(valfritt)</em> En sträng med flera värden som begränsar badging-regeln till de poäng som identifieras av de poängsättningsregler som anges.<br /><br /> Exempelpost: <code>/etc/community/scoring/rules/adv-comments-scoring</code><br /> Standard är ingen begränsning.</td>
  </tr>
 </tbody>
</table>

## Inkluderade regler och emblem {#included-rules-and-badge}

### Inkluderat märke {#included-badge}

I den här betaversionen ingår ett belöningsbaserat expertmärke:

* expert/etc/community/badging/images/expert-badge/jcr:content/expert.png

![chlimage_1-142](assets/chlimage_1-142.png)

För att expertmärket ska visas som en belöning för aktiviteten måste du se till att:

* `badges` är aktiverade för funktionen, till exempel ett forum eller QnA-komponent
* avancerade regler för bedömning och märkning tillämpas på den sida (eller det överordnade objekt) som komponenten placeras på

Se den grundläggande informationen för:

* [aktivera emblem för en komponent](/help/communities/implementing-scoring.md#enableforcomponent)
* [tillämpa regler](/help/communities/implementing-scoring.md#applytopage)

### Inkluderade poängsättningsregler och underregler {#included-scoring-rules-and-sub-rules}

I betaversionen finns två avancerade poängregler för [forumfunktionen](/help/communities/functions.md#forum-function) (en för forumfunktionen och kommentarkomponenterna i forumfunktionen):

1. /etc/community/scoring/rules/adv-comments-scoring

   * subRules[] =/etc/community/scoring/rules/sub-rules/adv-comments-rule/etc/community/scoring/rules/sub-rules/adv-voice-rule-owner/etc/community/scoring/rules/sub-rules/adv-voice-rule

1. /etc/community/scoring/rules/adv-forums-scoring

   * subRules[] =/etc/community/scoring/rules/sub-rules/adv-forums-rule/etc/community/scoring/rules/sub-rules/adv-comments-rule/etc/community/scoring/rules/sub-rules/adv-voice-rule-owner

**Anteckningar:**

* både `rules`och `sub-rules` noder är av typen cq:Page

* `subRules`är ett attribut av typen String[] i regelns `jcr:content` nod

* `sub-rules` kan delas mellan olika poängregler
* `rules`ska finnas på en databasplats med läsbehörighet för alla

   * regelnamn måste vara unika oavsett plats

### Inkluderade märkningsregler {#included-badging-rules}

I releasen finns två avancerade regler för märkning som motsvarar de [avancerade forumen och kommentarsreglerna](#included-scoring-rules-and-sub-rules).

* /etc/community/badging/rules/adv-comments-badging
* /etc/community/badging/rules/adv-forums-badging

**Anteckningar:**

* `rules` noder är av typen cq:Page
* `rules`ska finnas på en databasplats med läsbehörighet för alla

   * regelnamn måste vara unika oavsett plats

