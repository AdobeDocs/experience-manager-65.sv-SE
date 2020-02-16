---
title: Moderating Community Content
seo-title: Moderating Community Content
description: Moderniseringskoncept och åtgärder
seo-description: Moderniseringskoncept och åtgärder
uuid: 5c991d3a-0037-4d78-8f91-bb62e44441fa
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6866d209-5789-4ef9-bc3c-d644d4fb4b1c
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Moderating Community Content{#moderating-community-content}

## Översikt {#overview}

Community-innehåll, som också kallas användargenererat innehåll (UGC), skapas när en medlem (inloggad besökare) publicerar innehåll från en publicerad community-webbplats genom interaktion med någon av följande communitykomponenter:

* [blog](/help/communities/blog-feature.md) : medlemmar publicerar en bloggartikel eller kommentar
* [kalender](/help/communities/calendar.md) : medlemmar publicerar en kalenderhändelse eller kommentar
* [kommentarer](/help/communities/comments.md) : medlemmar publicerar en kommentar eller svarar på en kommentar

* [forum](/help/communities/forum.md) : medlemmar publicerar ett nytt ämne eller svarar på ett ämne
* [ideation](/help/communities/ideation-feature.md) : medlemmar publicerar en idé eller kommentar
* [QnA](/help/communities/working-with-qna.md) : medlemmar skapar en fråga eller besvarar en fråga
* [recensioner](/help/communities/reviews.md) : medlemmar publicerar en kommentar när de klassificerar ett objekt

Moderering av användargenererat innehåll är användbart för erkännande av positiva bidrag samt för begränsning av negativa bidrag (t.ex. skräppost och missbruk). UGC kan modereras från flera miljöer: [](/help/communities/working-with-srp.md)

* [masmodereringskonsol](/help/communities/moderation.md)Moderationskonsolen är tillgänglig för administratörer och [community-moderatorer](/help/communities/users.md) i den offentliga miljön samt för administratörer i författarmiljön. Detta är möjligt när communityinnehåll lagras i en [gemensam butik](/help/communities/working-with-srp.md).

* [moderering](/help/communities/in-context.md)av kontext i publiceringsmiljön kan utföras av administratörer och community-moderatorer direkt på den sida där innehållet publicerades.

## Modereringsåtgärder {#moderation-actions}

Vilka åtgärder som kan utföras på det publicerade innehållet (UGC) varierar beroende på användaridentitet och miljö. I tabellen nedan används följande terminologi för att beskriva de olika rollerna utifrån användaridentitet:

* `Admin`
en användare som är medlem i en [community-administratörsgrupp](/help/communities/users.md)

* `Moderator`
en medlem i en [community-moderatorgrupp](/help/communities/users.md#publishenvironmentusersandgroups) (har [moderatorbehörighet](/help/communities/in-context.md#moderatorpermissions))

* `Creator`
användaren som publicerade innehållet

* `Member`
en inloggad användare utan särskild behörighet

* `Visitor`
en anonym användare

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Administratör</strong></td>
   <td><strong>Moderator</strong></td>
   <td><strong>Originalformat</strong></td>
   <td><strong>medlem</strong></td>
   <td><strong>Besökare</strong></td>
   <td><strong>Händelsen<br /> utlöses</strong></td>
   <td><strong>Förmodererad</strong></td>
  </tr>
  <tr>
   <td><strong>Redigera/<br /> ta bort</strong></td>
   <td>X</td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Klipp ut</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Neka</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Stäng/<br /> öppna igen</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X<br /> </td>
  </tr>
  <tr>
   <td><strong>Flagga/<br /> avflagga</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td>X</td>
   <td> </td>
   <td>X</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Tillåt</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X</td>
  </tr>
 </tbody>
</table>

### Redigera/ta bort {#edit-delete}

När ett inlägg har gjorts kan det redigeras eller tas bort av författaren, en administratör eller en community-moderator.

När UGC tas bort tas den bort från databasen och kanske inte återskapas.

### Klipp ut {#cut}

Administratörer och community-moderatorer kan flytta ett eller flera forumämnen eller QnA-frågor från en plats till en annan. Detta inkluderar från en community-webbplats till en annan community-webbplats, förutsatt att samma medlem har modereringsbehörighet på båda webbplatserna.

Genom att välja åtgärden Klipp ut kopieras innehållet till ett urklipp. Flera inlägg kan kopieras och flyttas som en grupp till den nya platsen.

![cutugc](assets/cutugc.png) ![putbackugc](assets/putbackugc.png)

På den andra platsen, när innehållet finns i Urklipp, visas knappen Klistra in bredvid Nytt inlägg med ett nummer som anger antalet inlägg som ska klistras in. Knappen Klistra in innehåller ett alternativ för att rensa Urklipp i stället för att klistra in.

![chlimage_1-28](assets/chlimage_1-28.png) ![chlimage_1-29](assets/chlimage_1-29.png)

### Neka {#deny}

En moderator kanske inte tillåter att UGC visas på den publicerade webbplatsen. För administratörer och community-moderatorer är inlägget fortfarande tillgängligt och kommenteras som skräppost.

### Stäng/öppna igen {#close-reopen}

Åtgärden Stäng utför hela konversationstråden (ett forumämne eller den inledande kommentaren) och omfattar alla efterföljande inlägg eller svar.

När det är stängt är det inte bara möjligt att svara vidare, inga modereringsåtgärder tillåts heller.

Ämnet eller kommentaren måste öppnas igen för att du ska kunna utföra några åtgärder.

Åtgärden Stäng/öppna igen kan utföras av administratörer eller community-moderatorer.

### Flagga/avflagga {#flag-unflag}

Flaggning är ett sätt för alla inloggade medlemmar, förutom den som skapat innehållet, att ange att det finns ett problem med innehållet i ett inlägg. När den är flaggad visas en avflaggikon som tillåter att samma medlem avflaggar innehållet.

Kontextmoderering kan konfigureras så att medlemmar kan välja en orsak när de flaggar ett inlägg. Listan med valbara flaggorsaker kan konfigureras, inklusive om en anpassad orsak kan anges eller inte. Flaggorsaken sparas med användargenererat innehåll, men orsaken utlöser inte någon särskild åtgärd. Endast antalet flaggor utlöser ett meddelande. Flaggat innehåll kommenteras som sådant, så att moderatorerna kan agera på det.

Systemet håller reda på alla flaggor, vem som har flaggats, och flaggorsaken och skickar en händelse när tröskelvärdet har uppnåtts. Om användargenererat innehåll tillåts av en community-moderator arkiveras dessa flaggor. Om det finns efterföljande flaggningar efter att de har godkänts och arkiverats, arkiveras de som om det inte hade funnits några tidigare flaggningar.

### Tillåt {#allow}

Åtgärden Tillåt är ett alternativ för UGC som har flaggats, nekats eller inte har godkänts i ett förmodererat system. Åtgärden Tillåt rensar flaggade eller nekade/spam-status och arkiverar alla flaggade data.

## Vanliga modereringsbegrepp {#common-moderation-concepts}

### Förmoderering {#premoderation}

När UGC är förmodererat visas inte inlägget på den publicerade webbplatsen förrän det har godkänts av en modereringsåtgärd. När du skapar en [communitywebbplats](/help/communities/sites-console.md)och markerar kryssrutan `[Content is Premoderated](/help/communities/sites-console.md#moderation)` aktiveras förmoderering för hela webbplatsen. När komponenter har placerats på en sida kan komponenter som stöder moderering konfigureras för förmoderering med en inställning i redigeringsdialogrutan:

* [kommentarer](/help/communities/comments.md) och [granskningar](/help/communities/reviews.md)på fliken **Användarmoderering** , kontrollera **Förhandsmoderering**
* [forum](/help/communities/forum.md), [ideation](/help/communities/ideation-feature.md), [QnA](/help/communities/working-with-qna.md)och [kalender](/help/communities/calendar.md)på fliken **Inställningar** , kontrollera **modererat**

### Skräppostidentifiering {#spam-detection}

Skräppostavkänning är en automatisk modereringsfunktion som filtrerar bort oönskade delar av skickat användargenererat innehåll genom att markera dem som skräppost. När det är aktiverat identifieras om ett användargenererat innehåll är skräppost eller inte baserat på en förkonfigurerad samling skräppost. Standardord för skräppost finns på

`/libs/settings/community/sites/moderation/spamdetector-conf/profiles/spam_words.txt`.

Men om du vill anpassa eller utöka standardskräppost skapar du en uppsättning ord i katalogen /apps efter strukturen för standardskräppostorden med hjälp av [övertäckning](/help/communities/overlay-comments.md).

Ett användargenererat inlägg (i alla innehållstyper, t.ex. bloggar, forum och kommentarer) som innehåller skräppostord markeras med texten&quot;Det här inlägget klassificerades som skräppost&quot; ovanför inlägget.

Moderatorn kan se ett sådant inlägg och markera detsamma för att tillåta eller neka att visas på webbplatsen. Modereringsåtgärder för dessa inlägg kan utföras antingen i sitt sammanhang eller genom användargränssnitt för gruppmoderering.

![skräppidentifiering](assets/spamdetection.png)

Så här aktiverar du skräppostavkänningsmotorn:

1. Öppna [webbkonsolen](https://localhost:4502/system/console/configMgr)genom att gå till /system/console/configMgr.

1. Leta reda på konfigurationen av automatisk moderering **av** AEM Communities och redigera den.
1. Lägg till posten&quot;SpamProcess&quot;.

![skräp](assets/spamprocess.png)

>[!NOTE]
>
>Spam detection is only implementation for English locale.

### Sentiment {#sentiment}

Sentiment beräknas baserat på antalet positiva och negativa nyckelord ([bevakningsord](#configuringwatchwords)) som finns i ett inlägg (UGC).

I ekvationsanalysen används en uppsättning förkonfigurerade regler och UGC-känslan beräknas. Standardreglerna finns på `/libs/cq/workflow/components/workflow/social/sentiments/rules.`

Värdet som reglerna genererar är från 1 (alla negativa, inga positiva ord) till 10 (alla positiva, inga negativa ord). Ett värde på 5 är en neutral uppfattning och är standardvärdet.

Reglerna som definieras i komponenten /libs är:

* Regel 1: ange värdet 1 om det inte finns några positiva ord och minst ett negativt ord
* Regel 2: ange värdet 10 om det inte finns några negativa ord och minst ett positivt ord
* Regel 3: ange värdet 3 om det finns fler negativa ord än positiva ord
* Regel 4: ange värdet 8 om det finns fler positiva ord än negativa ord

Om du vill skriva över eller lägga till regler skapar du en uppsättning regler i katalogen /apps efter strukturen för standardreglerna. Redigera känslningskonfigurationen för att identifiera var reglerna finns.

Efter analys lagras känslan med användargenererat innehåll.

Från [masmodereringskonsolen](/help/communities/moderation.md)går det att filtrera och visa UGC baserat på om känslan är negativ, neutral eller positiv.

#### Bevakningsord {#watchwords}

AEM Communities tillhandahåller en *bevakningsfunktion *som ett steg i processen för att utvärdera [känslan](#sentiment). Bidraget till det känslomässiga värde som tillhandahålls av bevakningsord beror på en jämförelse av negativa och positiva bevakningsord som används i det publicerade innehållet samt förbjudna ord.

#### Konfigurera känslolägesikoner och bevakningsord {#configure-sentiment-and-watchwords}

Listan med positiva och negativa bevakningsord kan anpassas på samma sätt som personlighetsreglerna.

Standardlistan med bevakade ord kan anges som egenskaper för en nod i databasen, ungefär som standardvärdet eller genom att åsidosätta standardinställningen genom att konfigurera OSGi-tjänsten `sentimentprocess.name`med listan över ord.

Sentimentprocess.name **** kan också ändras så att den refererar till platsen för en anpassad uppsättning med attitydregler.

Så här konfigurerar du uttryck och bevakningsord:

* på en författarinstans
* logga in som administratör
* öppna [webbkonsol](https://localhost:4502/system/console/configMgr)
* leta `sentimentprocess.name`
* välj den konfiguration som ska öppnas i redigeringsläge

![sentimentprocess](assets/sentimentprocess.png)

* **Positiva bevakningsord** En kommaseparerad lista med ord som bidrar till en positiv uppfattning som åsidosätter standardvärdena. Standard är en tom lista.

* **Negativa Watchwords** En kommaseparerad lista med ord som bidrar till en negativ uppfattning som åsidosätter standardvärdena. Standard är en tom lista.

* **Explicit sökväg till bevakningsordsnod** Databasplatsen för en nod som innehåller standard `positive` och `negative` egenskaper som anger standardbevakningsord. Standardvärdet är `/libs/settings/community/watchwords/default`.

* **Sentiment Rules** Databasplatsen för reglerna för beräkning av känslouttryck baserat på positiva och negativa bevakningsord. Standard är `/libs/cq/workflow/components/workflow/social/sentiments/rules` (men det finns inte längre något arbetsflöde).

Följande är ett exempel på en anpassad post för standardbevakningsorden, när `Explicit Path to Watchwords Node` är inställd på `/libs/settings/community/watchwords/default`.

![crxde](assets/crxde.png)

### Tillstånd för moderatorn {#moderator-permissions}

Följande behörigheter, som tilldelas till samma resurs, kallas tillsammans för **`moderator permissions`** :

* `Read`
* **`Modify`**
* `Create`
* `Delete`
* `Replicate`

