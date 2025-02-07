---
title: Moderating Community Content
description: Lär dig att moderera användargenererat innehåll så att du kan identifiera positiva bidrag och begränsa negativa, som skräppost och stötande språk.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 22276580-e6bc-41c5-9ac3-e8f291f676b7
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1513'
ht-degree: 0%

---

# Moderating Community Content {#moderating-community-content}

## Ökning {#overview}

Community-innehåll, som också kallas användargenererat innehåll (UGC), skapas när en medlem (inloggad besökare) publicerar innehåll från en publicerad communitywebbplats genom interaktion med någon av följande communitykomponenter:

* [Blogg](/help/communities/blog-feature.md): medlemmar skickar en bloggartikel eller kommentar.
* [Kalender](/help/communities/calendar.md): medlemmar bokför en kalenderhändelse eller kommentar.
* [Kommentarer](/help/communities/comments.md): medlemmar skickar en kommentar eller svarar på en kommentar.

* [Forum](/help/communities/forum.md): medlemmar skriver ett nytt ämne eller svarar på ett ämne.
* [Identifiering](/help/communities/ideation-feature.md): medlemmar publicerar en idé eller kommentar.
* [QnA](/help/communities/working-with-qna.md): medlemmar skapar en fråga eller besvarar en fråga.
* [Recensioner](/help/communities/reviews.md): medlemmar skickar en kommentar när de klassificerar ett objekt.

Moderering av användargenererat innehåll är användbart för erkännande av positiva bidrag och begränsning av negativa bidrag (t.ex. skräppost och missbruk). UGC kan modereras från flera miljöer:

* [Community-innehållslagring](working-with-srp.md)

* [Konsol för massmoderering](moderation.md)

  Moderationskonsolen är tillgänglig för administratörer och [community-moderatorer](/help/communities/users.md) i den offentliga miljön och för administratörer i författarmiljön. Detta är möjligt när communityinnehåll lagras i en [gemensam butik](/help/communities/working-with-srp.md).

* [Kontextanpassad moderering](in-context.md)

  Administratörer och moderatorer i communityn kan moderera i Publish-miljön direkt på den sida där innehållet publicerades.

## Modereringsåtgärder {#moderation-actions}

Vilka åtgärder som kan utföras på det publicerade innehållet (UGC) varierar beroende på användaridentitet och miljö. I tabellen nedan används följande terminologi för att beskriva de olika rollerna utifrån användaridentitet:

* `Admin`

  En användare som är medlem i gruppen [community-administratörer](users.md).

* `Moderator`

  En medlem i en [community-moderatorgrupp](users.md#publishenvironmentusersandgroups) (har [moderatorbehörigheter](in-context.md#moderatorpermissions)).

* `Creator`

  Användaren som publicerade innehållet.

* `Member`

  En inloggad användare utan särskild behörighet.

* `Visitor`

  En anonym användare.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Administratör</strong></td>
   <td><strong>Moderator</strong></td>
   <td><strong>Skapare</strong></td>
   <td><strong>medlem</strong></td>
   <td><strong>Besökare</strong></td>
   <td><strong>Händelsen <br /> utlöstes</strong></td>
   <td><strong>Förmodererad</strong></td>
  </tr>
  <tr>
   <td><strong>Redigera/<br /> Ta bort</strong></td>
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
   <td><strong>Stäng/<br /> Öppna igen</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X<br /> </td>
  </tr>
  <tr>
   <td><strong>Flagga/<br /> - unflagga</strong></td>
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

![cutugc](assets/cutugc.png)

![putbackugc](assets/putbackugc.png)

När det finns innehåll i Urklipp på den andra platsen visas knappen Klistra in bredvid Ny Post med ett nummer som anger antalet inlägg som ska klistras in. Knappen Klistra in innehåller ett alternativ för att rensa Urklipp i stället för att klistra in.

![pasteugc](assets/pasteugc.png)

![pasteugc1](assets/pasteugc1.png)

### Neka {#deny}

En moderator kanske inte tillåter att UGC visas på den publicerade webbplatsen. För administratörer och community-moderatorer är inlägget fortfarande tillgängligt och kommenteras som skräppost.

### Stäng/öppna igen {#close-reopen}

Åtgärden Stäng utför hela konversationstråden (ett forumämne eller den inledande kommentaren) och omfattar alla efterföljande inlägg eller svar.

När det är stängt är det inte bara möjligt att svara vidare, inga modereringsåtgärder tillåts heller.

Ämnet eller kommentaren måste öppnas igen för att du ska kunna utföra några åtgärder.

Åtgärden Stäng/öppna igen kan utföras av administratörer eller community-moderatorer.

### Flagga/avflagga {#flag-unflag}

Flaggning är ett sätt för alla inloggade medlemmar, förutom den som skapat innehållet, att ange att det finns ett problem med innehållet i ett inlägg. När innehållet har flaggats visas en avflaggikon som gör att samma medlem kan avflagga innehållet.

Kontextmoderering kan konfigureras så att medlemmar kan välja en orsak när de flaggar ett inlägg. Listan med valbara flaggorsaker kan konfigureras, inklusive om en anpassad orsak kan anges. Flaggorsaken sparas med användargenererat innehåll, men orsaken utlöser inte någon särskild åtgärd. Endast antalet flaggor utlöser ett meddelande. Flaggat innehåll kommenteras som sådant, så att moderatorerna kan agera på det.

Systemet spårar alla flaggor, vem som har flaggats, och flaggorsaken och skickar en händelse när tröskelvärdet har uppnåtts. Om användargenererat innehåll tillåts av en community-moderator arkiveras dessa flaggor. Om det finns efterföljande flaggningar efter att de har godkänts och arkiverats, arkiveras de som om det inte hade funnits några tidigare flaggningar.

### Tillåt {#allow}

Åtgärden Tillåt är ett alternativ för UGC som har flaggats, nekats eller inte har godkänts i ett förmodererat system. Åtgärden Tillåt rensar flaggade eller nekade/spam-status och arkiverar alla flaggade data.

## Vanliga modereringsbegrepp {#common-moderation-concepts}

### Förmoderering {#premoderation}

När UGC är förmodererat visas inte inlägget på den publicerade webbplatsen förrän det har godkänts av en modereringsåtgärd. När du skapar en [community-webbplats](/help/communities/sites-console.md) och markerar kryssrutan [Innehållet är förmodererat](sites-console.md#moderation) aktiveras förmoderering för hela webbplatsen. När komponenter placeras på en sida kan komponenter som stöder moderering konfigureras för förmoderering med en inställning i redigeringsdialogrutan:

* [Kommentarer](comments.md) och [granskningar](reviews.md)
in **[!UICONTROL User Moderation]** > **[!UICONTROL Pre-Moderation]**.

* [Forum](/help/communities/forum.md), [ideation](/help/communities/ideation-feature.md), [QnA](/help/communities/working-with-qna.md) och [calendar](/help/communities/calendar.md)
in **[!UICONTROL Settings]** > **[!UICONTROL Moderated]**.

### Skräppostidentifiering {#spam-detection}

Skräppostavkänning är en automatisk modereringsfunktion som filtrerar bort oönskade delar av skickat användargenererat innehåll genom att markera dem som skräppost. När det är aktiverat identifieras om ett användargenererat innehåll är skräppost eller inte baserat på en förkonfigurerad samling skräppostord. Standardord för skräppost finns på

`/libs/settings/community/sites/moderation/spamdetector-conf/profiles/spam_words.txt`.

Om du vill anpassa eller utöka skräppostens standardord skapar du en uppsättning ord i katalogen /apps efter strukturen för standardskräppostorden med [overlay](/help/communities/overlay-comments.md).

Ett användargenererat inlägg (i alla innehållstyper, t.ex. bloggar, forum och kommentarer) som innehåller skräppostord markeras med texten&quot;Det här inlägget klassificerades som skräppost&quot; ovanför inlägget.

Moderatorn kan se ett sådant inlägg och markera detsamma för att tillåta eller neka att visas på webbplatsen. Modereringsåtgärder för dessa inlägg kan utföras antingen i sitt sammanhang eller genom användargränssnitt för gruppmoderering.

![skräpavkänning](assets/spamdetection.png)

Följ de här stegen för att aktivera skräppostavkänningsmotorn:

1. Öppna [webbkonsolen](https://localhost:4502/system/console/configMgr) genom att gå till `/system/console/configMgr`.

1. Leta reda på konfigurationen för **Automatisk moderering** för AEM Communities och redigera den.
1. Lägg till posten **[!UICONTROL SpamProcess]**.

![spamprocess](assets/spamprocess.png)

>[!NOTE]
>
>Spamidentifiering implementeras endast för engelska språk.

### Sentiment {#sentiment}

Sentiment beräknas baserat på antalet positiva och negativa nyckelord ([bevakningsord](#configuringwatchwords)) som finns i ett inlägg (UGC).

I ekvationsanalysen används en uppsättning förkonfigurerade regler och UGC-känslan beräknas. Standardreglerna är `/libs/cq/workflow/components/workflow/social/sentiments/rules`.

Värdet som reglerna genererar är från 1 (alla negativa, inga positiva ord) till 10 (alla positiva, inga negativa ord). Ett värde på 5 är en neutral uppfattning och är standardvärdet.

Reglerna som definieras i komponenten /libs är:

* Regel 1: ange värdet 1 om det inte finns några positiva ord och minst ett negativt ord.
* Regel 2: ange värdet 10 om det inte finns några negativa ord och minst ett positivt ord.
* Regel 3: ange värdet 3 om det finns fler negativa ord än positiva ord.
* Regel 4: ange värdet 8 om det finns fler positiva ord än negativa ord.

Om du vill skriva över eller lägga till regler skapar du en uppsättning regler i katalogen /apps efter strukturen för standardreglerna. Redigera känslningskonfigurationen så att du kan identifiera var reglerna finns.

Efter analys lagras känslan med användargenererat innehåll.

Från [masmoderationskonsolen](/help/communities/moderation.md) går det att filtrera och visa UGC utifrån om känslan är negativ, neutral eller positiv.

#### Watchwords {#watchwords}

AEM Communities tillhandahåller en *bevakningsordsanalys* som ett steg i processen för att utvärdera [känslouttryck](#sentiment). Bidraget till det känslomässiga värde som tillhandahålls av bevakningsord beror på en jämförelse av negativa och positiva bevakningsord som används i det publicerade innehållet och förbjudna ord.

#### Konfigurera känslolägesikoner och bevakningsord {#configure-sentiment-and-watchwords}

Listan med positiva och negativa bevakningsord kan anpassas på samma sätt som personlighetsreglerna.

Standardlistan med bevakade ord kan anges som egenskaper för en nod i databasen, ungefär som standardvärdet eller genom att åsidosätta standardvärdet genom att konfigurera OSGi-tjänsten `sentimentprocess.name` med listan över ord.

**sentimentprocess.name** kan också ändras så att den refererar till platsen för en anpassad uppsättning med sentimentsregler.

Så här konfigurerar du uttryck och bevakningsord:

* Logga in på författarinstansen som administratör.
* Öppna [webbkonsolen](https://localhost:4502/system/console/configMgr).
* Sök efter `sentimentprocess.name`.
* Markera konfigurationen så att du kan öppna den i redigeringsläge.

![sentimentprocess](assets/sentimentprocess.png)

* **Positiva bevakningsord**

  En kommaavgränsad lista med ord som bidrar till en positiv uppfattning som åsidosätter standardvärdena. Standard är en tom lista.

* **Negativa bevakningsord**

  En kommaavgränsad lista med ord som bidrar till en negativ uppfattning som åsidosätter standardvärdena. Standard är en tom lista.

* **Explicit sökväg till bevakningsordsnod**

  Databasplatsen för en nod som innehåller standardegenskaperna `positive` och `negative` som anger standardbevakningsord. Standardvärdet är `/libs/settings/community/watchwords/default`.

* **Känslighetsregler**

  Databasplatsen för reglerna för att beräkna en uppfattning baserat på positiva och negativa bevakningsord. Standardvärdet är `/libs/cq/workflow/components/workflow/social/sentiments/rules` (men det finns inte längre något arbetsflöde).

Följande är ett exempel på en anpassad post för standardbevakningsorden när `Explicit Path to Watchwords Node` är inställd på `/libs/settings/community/watchwords/default`.

![crxde](assets/crxde.png)

### Tillstånd för moderatorn {#moderator-permissions}

Följande behörigheter, när de tilldelas till samma resurs, kallas gemensamt `moderator permissions`:

* `Read`
* `Modify`
* `Create`
* `Delete`
* `Replicate`
