---
title: Modereringskonsol
description: Lär dig hur administratörer och moderatorer kan använda modereringskonsolen för att få åtkomst till all UGC som de har behörighet att moderera.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 829da16a-4083-43c1-857d-f2666b363bfc
source-git-commit: 00b6f2f03470aca7f87717818d0dfcd17ac16bed
workflow-type: tm+mt
source-wordcount: '2036'
ht-degree: 0%

---

# Modereringskonsol {#moderation-console}

I AEM Communities: bulk [moderering av communityinnehåll](/help/communities/moderate-ugc.md) kan användas både i författar- och publiceringsmiljöer av administratörer och community-moderatorer (betrodda communitymedlemmar tilldelade som moderatorer).

Administratörer och community-moderatorer kan även utföra [sammanhangsbaserad moderering](/help/communities/in-context.md) i publiceringsmiljön.

En funktion i alla [communitysajter](/help/communities/sites-console.md) är en `Administration` menyalternativ som är tillgängliga för användare som loggar in med administratörsbehörighet. The `Administration` -länken ger åtkomst till modereringskonsolen.

Från modereringskonsolen har administratörer och moderatorer tillgång till allt användargenererat innehåll (UGC) som de har behörighet att moderera. Om du tillåter att flera webbplatser modereras kan du visa inlägg på alla webbplatser eller filtrera efter utvalda communityplatser.

Mer detaljerad information finns på [Hantera användare och användargrupper](/help/communities/users.md).

Moderationskonsolen stöder:

* Utföra flera modereringsåtgärder samtidigt.
* Söker i UGC.
* Visa UGC-information.
* Visa information om UGC-författare.

Endast när du är inloggad som administratör eller som medlem med ` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`kan modereringsuppgifter utföras.

## Publiceringsmiljöåtkomst {#publish-environment-access}

Åtkomst till moderationskonsolen från en publicerad communitywebbplats sker via en administrationslänk som visas när en community-moderator är inloggad.

![publicweretail](assets/publishweretail.png)

Genom att välja administrationslänken visas modereringskonsolen:

![moderation-console-publish](assets/moderation-console-publish.png)

## Åtkomst till författarmiljö {#author-environment-access}

För att nå Kontrollpanelen i författarmiljön

* Välj **[!UICONTROL Communities]** > **[!UICONTROL Moderation]**.

Endast när du är inloggad som administratör eller som medlem med [moderatorbehörigheter](/help/communities/in-context.md#identifyingtrustedmembers)kan modereringsuppgifter utföras. Det enda communityinnehåll som visas är det som den inloggade medlemmen får moderera.

>[!NOTE]
>
>UGC från publiceringsmiljön visas bara på författare om den valda SRP implementerar en gemensam butik. Som standard är exempelvis lagringen JSRP, som inte är en gemensam butik för Författare och Publicera. Se [Community-innehåll](/help/communities/working-with-srp.md).

![moderationkonsoleförfattare](assets/moderationconsoleauthor.png)

## Användargränssnitt för modereringskonsol {#moderation-console-ui}

Bortsett från den vänstra navigeringslisten (som visas på författaren men inte på Publicera) har modereringsgränssnittet följande huvudområden:

* **[Övre navigeringsfältet](#top-navigation-bar)**
* **[Verktygsfält](#toolbar)**
* **[Innehållsområde](#content-area)**

### Övre navigeringsfält {#top-navigation-bar}

Det övre navigeringsfältet är konstant för alla konsoler. Mer information finns i [Grundläggande hantering](/help/sites-authoring/basic-handling.md).

### Verktygsfält {#toolbar}

Verktygsfältet, som finns under det övre navigeringsfältet, har följande växlingsknapp till vänster:

* [Filterspår](/help/communities/moderation.md#filterrail)
öppnar en räl som gör det möjligt att välja vilka egenskaper som innehållet ska filtreras efter.

Verktygsfältet, som finns under det övre navigeringsfältet, har följande växlingsknapp till vänster:

![växlarSwitch](assets/toggleswitch.png)

[Filterspår](/help/communities/moderation.md#filterrail)
öppnar en räl när du väljer Sök, vilket gör att du kan välja vilka egenskaper som innehållet ska filtreras efter.

![filterrail](assets/filterrail.png)

### Innehållsområde {#content-area}

Innehållsområdet innehåller information för publicerad UGC:

* UGC har bokförts
* Medlemsnamn
* Medlem avatar
* Postens plats
* När den bokförs
* Antal svar till inlägget
* [Sentiment](/help/communities/moderate-ugc.md#sentiment) associerat med inlägget
* Om det godkänns visas en bock
* Om det finns en bifogad fil visas ett gem

>[!NOTE]
> 
>Innehållsområdet har en *oändlig rullning*, vilket innebär att du kan fortsätta rulla tills du har nått slutet av innehållet. Verktygsfältet ligger kvar på en fast, synlig plats ovanför innehållsområdet även när du bläddrar.

### Filterspår {#ootbfilters}

![open-filterrail](assets/open-filterrail.png)

Ikonen för sidopanelen öppnar filterlisten. Filtercirkeln, som visas till vänster om innehållsområdet, innehåller olika filter, som båda har en omedelbar effekt på den refererade UGC:n som visas i innehållsområdet.

Filtren inom varje kategori är **ELLER**&quot;d tillsammans och filtren i olika kategorier är **OCH** tillsammans.

Om du till exempel markerar båda **Fråga** och **Svar** ser du innehåll som antingen **Fråga** *eller* en **Svar**.

Om du däremot markerar **Fråga** och **Väntande** ser du bara innehåll som **Fråga** och är **Väntande**.

>[!NOTE]
>
>Moderatorer för communityn kan skapa bokmärken för fördefinierade filter i modereringskonsolens användargränssnitt. När dessa filter läggs till i slutet av URL:en (som frågesträngsparametrar) kan moderatorerna senare gå tillbaka till bokmärkesfiltren och även dela dessa länkar.

![sökningsikon](assets/searchicon.png)

När filterlisten är öppen växlar ikonen Sök och sidopanelen stängs. Om du vill stänga filterfältet och bara visa det användargenererade innehållet klickar du på ikonen Sök och väljer alternativet Endast innehåll.

#### Innehållsbana {#content-path}

Innehållssökväg begränsar den UGC-referens som visas för inlägg i den angivna innehållsdatabasen.

![content-path](assets/content-path.png)

#### Textsökning {#text-search}

Textsökning begränsar den refererade UGC som visas till inlägg som innehåller den angivna texten.

![textsökning](assets/text-search.png)

#### Plats {#site}

Webbplatsen begränsar den refererade UGC som visas till inlägg på valda communitywebbplatser. Om inga platser är markerade visas alla referenser till UGC.

![platspanel](assets/site-panel.png)

>[!NOTE]
>
>När en administratör öppnar konsolen för gruppmoderering visas alla referenser till UGC, även webbplatser som inte skapats med [guide för att skapa webbplatser](/help/communities/sites-console.md), t.ex. Geometrixx.
>
>När en betrodd community-medlem öppnar konsolen för gruppmoderering visas endast referenser till UGC som skapats för communitywebbplatser som medlemmen har behörighet att moderera. Den kan också filtreras med platsfiltret.

#### Innehållstyp {#content-type}

Innehållstyp begränsar den refererade UGC-enheten som visas till inlägg av den valda resurstypen. Du kan välja en eller flera av följande typer. Alla typer visas om inget är markerat.

* **Kommentar**
* **Forum**
* **Forum Reply**
* **Fråga**
* **Svar på fråga**
* **Bloggartikel**
* **Bloggkommentar**
* **Kalenderhändelse**
* **Kalenderkommentar**
* **Filbiblioteksmapp**
* **Filbiblioteksdokument**
* **Idea**
* **Idékommentar**

![innehållstyper](assets/content-types.png)

#### Ytterligare innehållstyper {#additional-content-types}

Så här lägger du till ytterligare resurser att filtrera:

* Logga in på författarinstansen som administratör.
* Öppna [Webbkonsol](https://localhost:4502/system/console/configMgr).
* Sök `AEM Communities Moderation Dashboard Filters`.
* Markera konfigurationen så att du kan öppna den i redigeringsläge.
* Ange den ResourceType för en komponent som du vill filtrera:

   * Om du till exempel vill filtrera på de medföljande röstkomponenterna anger du:

     `Voting=social/tally/components/hbs/voting`

  ![additional-contenttype](assets/additional-contenttype.png)

* Välj Spara.
* Uppdatera webbcommunityn - modereringskonsolen.

Resultatet är ett nytt valbart filter för `Voting` under `Content Type` filtergrupp.

När det filtret är markerat visar kontrollpanelens innehåll UGC som matchar någon av de ResourceTypes som har angetts.

#### Status {#status}

Statusen begränsar den refererade UGC:n som visas till inlägg med den valda statusen, som kan vara en eller flera av Väntande, Godkänd, Nekad eller Stängd samt Utkast eller Schemalagt för bloggartiklar samt Svarat eller Inte besvarat för QnA-frågor. Om ingen är markerad visas alla.

>[!NOTE]
>
>Om du bara väljer statusen Inte besvarat visas allt innehåll (för alla innehållstyper) utom de besvarade frågorna. Det beror på att egenskapen som är ansvarig för den besvarade frågan inte finns om det inte finns några besvarade frågor och annat innehåll, som forumämne, bloggartikel eller kommentarer.

![status](assets/statuses.png)

#### Flaggning {#flagging}

Flaggning begränsar det refererade användargenererat innehåll som visas till inlägg som är flaggade eller dolda.

När ett innehåll har flaggats förblir det flaggat tills du bryter flaggan för det enskilda innehållet genom att markera **Flagga** igen. Det finns inga flaggningsnivåer, som är viktiga eller som uppföljning.

![flaggning](assets/flagging.png)

#### Medlemmar {#members}

Medlemmar begränsar den refererade UGC som visas för UGC som har bokförts av det angivna medlemsnamnet.

![medlemmar](assets/members.png)

#### Anslaget senast {#posted-in-the-last}

Bokförd i sista begränsa hur den refererade UGC:n visas för inlägg gjorda i sista timmen, dagen, veckan, månaden eller året.

![postad-sista](assets/posted-last.png)

#### Sentiment {#sentiment}

[Sentiment](/help/communities/moderate-ugc.md#sentiment) begränsar den refererade UGC-enheten som visas till inlägg med ett känslomässigt värde som är antingen positivt, negativt eller neutralt.

![känslouttryck](assets/sentiment.png)

## Egna filter {#custom-filters}

Förutom själva förpackningen filtreras [Filterspår](/help/communities/moderation.md#ootbfilters)kan ytterligare anpassade metadatafilter läggas till i modereringsgränssnittet. Utvecklare kan använda exempelkoden i GitHub för att utöka de befintliga gränssnittsfiltren för moderering.

![custom-tag-filter](assets/custom-tag-filter.png)

The [exempelprojekt](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/main/aem-communities-moderation-filter) på GitHub implementerar taggfiltret för att filtrera UGC-listan baserat på om de specifika taggarna tillämpas på användargenererat innehåll. Du kan följa exempelkoden och skapa analoga filter för andra liknande UGC-metadatafält.

Så här installerar du exemplet för taggfiltret:

1. Öppna Package Manager på AEM Author (`https://[aem-author]:4502/crx/packmgr/index.jsp`) och AEM publicera (`https://[aem-publish]:4503/crx/packmgr/index.jsp`).
1. Bygg paketet `com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip` från GitHub-koden och installera och aktivera samma.
1. Öppna paketkonsolen på AEM författare ( `https://[aem-author]:4502/system/console/bundles`) och AEM publicera ( `https://[aem-publish]:4503/system/console/bundles`).
1. Bygg paketet (`[com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar`) från GitHub, och installera och aktivera samma.
1. Gå till **/apps/social/moderation/facets** nod på AEM författare (`https://[aem-author]:4502/crx/de/index.jsp#/apps/social/moderation/facets`) och AEM Publish (`https://[aem-publish]:4502/crx/de/index.jsp#/apps/social/moderation/facets`).
1. Lägg till en teknisk användare **communities-utility-reader** med `jcr:read` behörigheter.

Så här visar du anpassade filter på befintliga communityplatser:

1. Redigera `Clientlibs` befintlig modereringssida `/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`

   * Lägg till ny kategori `cq.social.hbs.moderation.v2.`

1. Gå till `/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.`

   * Ange som ny komponent `sling:resourceType = social/moderation/v2/filters.`

1. Gå till `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer`.

   * Ange som ny komponent `sling:resourceType = social/moderation/v2/modcontainer`.

## Modereringsåtgärder {#moderation-actions}

[Modereringsåtgärder](/help/communities/moderate-ugc.md#moderation-actions) kan utföras på en eller flera markeringar som gjorts i innehållsområdet eller när du visar innehållsdetaljer.

Om du vill moderera inläggen i stor skala klickar du på Välj (![selecticon](assets/selecticon.png)) på ett inlägg, som visas när du hovrar över det med musen (skrivbordet) eller trycker och håller ett finger på inlägget (mobilen). Genom att göra detta aktiverar du flervalsläget och kan nu välja de efterföljande inlägg som ska gruppmodereras genom att klicka på dem. Använd knapparna som visas i verktygsfältet så att du kan utföra modereringsåtgärder för de valda inläggen. Alla funktionsmakron uppmanas att bekräfta.

Om du vill ändra ett inlägg i innehållsområdet till en viss nivå håller du pekaren över det med musen (skrivbordet) eller trycker och håller ned ett finger på posten (mobilen) så att knapparna visas på posten. När du arbetar med en enskild innehållsdetalj uppmanas du bara att bekräfta en borttagningsåtgärd.

### Moderering av flera inlägg {#moderating-multiple-posts}

Ange gruppmarkeringsläget genom att klicka på `Select` ikon i ett inlägg:

![select-icon](assets/select-icon.png)

Om du vill avsluta gruppmarkeringsläget väljer du ikonen Avbryt (x) i verktygsfältet:

Modereringsåtgärderna som kan utföras på flera inlägg är:

* Neka
* Ta bort
* Stäng/öppna inlägg igen

Ikonerna som tillåter dessa åtgärder visas bara i verktygsfältet när flera inlägg är markerade.

![bulkmoderat](assets/bulkmoderate.png)

### Moderera ett enstaka inlägg {#moderating-a-single-post}

I läget för en markering är det möjligt att

* Visa användarinformation genom att välja användarens namn.
* Visa inlägget i sitt sammanhang genom att markera länken till inlägget.
* [Svara](#reply)
* [Tillåt](#allow)
* [Neka](#deny)
* [Ta bort](#delete)
* [Stäng](#close)
* Visa [Modereringshistorik](#moderation-history)
* [Visa detaljer](#viewdetails)

I kortvyn ovanför ikonerna för modereringsåtgärder finns texten i posten och nedan finns data som indikerar:

* Om den har svar, och om så är fallet, föregås av antalet svar
* Om den har flaggats
* Om det har godkänts
* När användargenererat innehåll bokfördes

![singleselectmode](assets/singleselectmode.png)

#### Svara {#reply}

![svara](assets/reply.png)

När du arbetar med ett enstaka inlägg visas en svarsikon om UGC-typen stöder svar och är konfigurerad för att tillåta svar.

#### Tillåt {#allow}

![tillåt](assets/allow.png)

När du arbetar med ett enstaka inlägg visas ikonen Tillåt när inlägget antingen har flaggats eller nekats. Om du markerar Tillåt tas alla flaggor bort.

#### Neka {#deny}

![neka](assets/deny.png)

The **Neka** modereringsåtgärden är bara tillgänglig för innehåll som är modererat och inte visas på omodererat innehåll förutom i flervalsläge.

Innehåll som inte är modererat godkänns alltid.

Innehåll som modereras från början försätts i ett väntande läge och kan ändras senare för godkännande eller avslag.

Innehåll som lämnar det väntande läget kan aldrig återgå till ett väntande läge. Innehåll som markerats som godkänt eller nekat kan när som helst ändras till ett annat läge.

#### Ta bort {#delete}

![delete](assets/delete.png)

I envalsläge eller gruppläge kan du markera objekt och ta bort dem. Borttagningsåtgärden resulterar i en bekräftelsedialogruta. När de har tagits bort försvinner dessa objekt omedelbart från innehållsområdet. **När UGC har tagits bort tas det bort permanent från databasen och kan inte hämtas senare**.

#### Stäng {#close}

![stäng](assets/close.png)

När du arbetar med ett enstaka inlägg visas en stängningsikon om UGC-typen stöder möjligheten att förhindra fler inlägg för den resursen.

#### Modereringshistorik {#moderation-history}

![moderering](assets/moderation.png)

När du arbetar med ett enstaka inlägg visas en ikon för modereringshistorik när du hovrar över det. Om du väljer ikonen visas en ruta med en historik över åtgärder som har vidtagits för UGC-inlägget.

Om du vill återgå till visning av flera UGC-inlägg i innehållsområdet markerar du X:et i det övre högra hörnet av rutan med vydetaljer.

Till exempel:

![moderation-history](assets/moderation-history.png)

#### Visa detaljer {#view-detail}

![visa](assets/view.png)

När du arbetar med ett enstaka inlägg kan du visa mer information genom att öppna UGC i detaljläge.

Om du vill göra det håller du muspekaren över inlägget för att visa `View Detail` och markera den för att visa en panel med mer information om inlägget.

Om du vill återgå till visning av flera UGC-inlägg i innehållsområdet markerar du X:et i det övre högra hörnet av rutan med vydetaljer.

Till exempel:

![view1](assets/view1.png)
