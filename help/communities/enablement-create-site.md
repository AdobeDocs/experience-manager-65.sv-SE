---
title: Skapa en ny communitywebbplats för aktivering
seo-title: Skapa en ny communitywebbplats för aktivering
description: Skapa en communitywebbplats för aktivering
seo-description: Skapa en communitywebbplats för aktivering
uuid: a75fa566-a570-45fd-aabc-23651ef819cc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: b9333558-6af9-46b2-9f03-3722645c69a6
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1724'
ht-degree: 1%

---


# Skapa en ny communitywebbplats för aktivering {#author-a-new-community-site-for-enablement}

## Skapa communitywebbplats {#create-community-site}

[Community Site ](/help/communities/sites-console.md) creationanvänder en guide som vägleder dig genom de olika stegen för att skapa en community-webbplats. Du kan gå vidare till `Next`-steget eller `Back` till föregående steg innan du implementerar platsen i det sista steget.

Så här kommer du igång med att skapa en ny community-webbplats:

Använda [författarinstansen](https://localhost:4502/)

* Logga in med administratörsbehörighet och navigera till **[!UICONTROL Communities]** > **[!UICONTROL Sites]**.

* Välj **Skapa**.

### Steg 1: Platsmall {#step-site-template}

![aktivera webbplatsmall](assets/enablement-site-template.png)

I steget **Webbplatsmall** anger du en titel, beskrivning, namn för webbadressen och väljer en mall för en community-webbplats, till exempel:

* **Webbplatstitel** för communityn:  `Enablement Tutorial`.

* **Beskrivning** av communityplats:  `A site for enabling the community to learn.`

* **Rotadress** för communityplats: (lämna tomt för standardroten  `/content/sites`)

* **Molnkonfigurationer**: (lämna tomt om ingen molnkonfiguration har angetts) ange sökvägen till de angivna molnkonfigurationerna.
* **Grundspråk** för communitywebbplats: (lämnas orört för ett enda språk: På engelska) använder du listrutan för att välja ett  *eller* flera språk bland de tillgängliga språken - tyska, italienska, franska, japanska, spanska, portugisiska (Brasilien), kinesiska (traditionell) och kinesiska (förenklad). En communityplats skapas för varje språk som läggs till och finns i samma webbplatsmapp enligt den bästa praxis som beskrivs i [Översätta innehåll för flerspråkiga platser](/help/sites-administering/translation.md). Rotsidan för varje webbplats kommer att innehålla en underordnad sida med språkkoden för ett av de valda språken, till exempel &quot;en&quot; för engelska eller &quot;fr&quot; för franska.

* **Namn på** communitywebbplats:  `enable`

   * Den inledande URL:en visas under namnet på communitywebbplatsen
   * Ange en giltig URL genom att lägga till en baskod + &quot;.html&quot;
      *Till exempel* https://localhost:4502/content/sites/  `enable/en.html`

* **Referensplatsmall**: dra nedåt för att välja  `Reference Structured Learning Site Template`

Välj **Nästa**.

### Steg 2: Design {#step-design}

Designsteget presenteras i två avsnitt där du kan välja tema och varumärkesbanderoll:

#### TEMA FÖR GEMENSKAPENS WEBBPLATS {#community-site-theme}

Välj det format som du vill använda på mallen. När du väljer det här alternativet överlagras temat med en bockmarkering.

#### GEMENSKAPENS WEBBPLATSVARNING {#community-site-branding}

(Valfritt) Ladda upp en banderollbild som ska visas på webbplatsens sidor. Banderollen är fäst vid webbläsarens vänstra kant, mellan communitywebbplatsens sidhuvud och meny (navigeringslänkar). Banderollhöjden beskärs till 120 pixlar. Banderollens storlek ändras inte så att den passar webbläsarens bredd och höjden 120 pixlar.

![chlimage_1-449](assets/chlimage_1-449.png)

![chlimage_1](assets/chlimage_1.jpeg)

Välj **Nästa**.

### Steg 3: Inställningar {#step-settings}

Innan du väljer `Next` i steget Inställningar finns det sju avsnitt som ger åtkomst till konfigurationer som användarhantering, taggning, roller, moderering, analys, översättning och aktivering.

#### ANVÄNDARHANTERING {#user-management}

Vi rekommenderar att [aktiveringsgrupper](/help/communities/overview.md#enablement-community) är privata.

En communitywebbplats är privat när anonyma besökare på webbplatsen nekas åtkomst, inte får registrera sig själv och inte får använda social inloggning.

Kontrollera att de flesta kryssrutor är avmarkerade för [Användarhantering](/help/communities/sites-console.md#user-management):

* Tillåt INTE webbplatsbesökare att registrera sig själva.
* Tillåt INTE anonyma webbplatsbesökare att visa webbplatsen.
* Valfritt om meddelanden ska tillåtas bland communitymedlemmar eller inte.
* Tillåt INTE inloggning med Facebook.
* Tillåt INTE inloggning med Twitter.

![user-mgmt](assets/user-mgmt.png)

#### TAGGAR {#tagging}

De taggar som kan användas för communityinnehåll kontrolleras genom att AEM namnutrymmen som tidigare definierats via [taggningskonsolen](/help/sites-administering/tags.md#tagging-console) (till exempel namnutrymmet [Tutorial](/help/communities/enablement-setup.md#create-tutorial-tags)) väljs.

Om du väljer Taggnamnutrymmen för communitywebbplatsen begränsas dessutom det urval som visas när du definierar kataloger och aktiveringsresurser. Se [Tagga aktiveringsresurser](/help/communities/tag-resources.md) för viktig information.

Det är enkelt att hitta namnutrymmen med typsnittssökning. Till exempel,

* Typ `tut`
* Välj `Tutorial`

![enablement-tagging](assets/enablement-tagging.png)

### ROLLER {#roles}

[Gruppmedlemsroller ](/help/communities/users.md) tilldelas via inställningarna i avsnittet Roller.

Om du vill att en community-medlem (eller grupp av medlemmar) ska kunna uppleva webbplatsen som community-hanterare använder du typsnittssökningen och väljer medlemmens eller gruppens namn bland alternativen i listrutan.

Till exempel,

* Typ `q`
* Välj [Quinn Harper](/help/communities/enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[Tunneltjänsten ](/help/communities/deploy-communities.md#tunnel-service-on-author) gör det möjligt att välja medlemmar och grupper som finns endast i publiceringsmiljön.

![aktiveringsroller](assets/site-admin.png)

#### MODERATION {#moderation}

Acceptera de globala standardinställningarna för [moderering](/help/communities/sites-console.md#moderation) användargenererat innehåll (UGC).

![chlimage_1-452](assets/chlimage_1-452.png)

#### ANALYTIK {#analytics}

I listrutan väljer du Analytics-molntjänstramverket som är konfigurerat för den här communitywebbplatsen.

Markeringen som visas på skärmbilden `Communities` är ett ramverksexempel från [konfigurationsdokumentationen.](/help/communities/analytics.md#aem-analytics-framework-configuration)

![chlimage_1-454](assets/chlimage_1-454.png)

#### TRANSLATION {#translation}

[Översättningsinställningarna](/help/communities/sites-console.md#translation) anger om UGC kan översättas eller inte och till vilket språk, om så är fallet.

* Kontrollera **Tillåt maskinöversättning**
* Använd standardinställningarna

![chlimage_1-456](assets/chlimage_1-456.png)

#### AKTIVERA {#enablement}

För en aktiveringscommunity måste du identifiera en eller flera aktiveringsansvariga i communityn.

* **Aktivera hanterare**
 (krävs) Medlemmar i 
`Community Enablement Managers` gruppen är tillgänglig för att väljas för att hantera den här communitywebbplatsen.

   * Typ `s`
   * Välj `Sirius Nilson`

* **Marketing Cloud Org ID**
 (valfritt) ID:t för ett Adobe Analytics-konto som krävs när  [Video Heartbeat ](/help/communities/analytics.md#video-heartbeat-analytics) Analytics inkluderas i aktiveringsrapporten.

![chlimage_1-457](assets/chlimage_1-457.png)

Välj **Nästa**.

### Steg 4: Skapa communitywebbplats {#step-create-community-site}

Välj **Skapa.**

![chlimage_1-458](assets/chlimage_1-458.png)

När processen är klar visas mappen för den nya platsen i konsolen Communities > Sites.

![enablementsitecreated](assets/enablementsitecreated.png)

### Publicera den nya communitywebbplatsen {#publish-the-new-community-site}

Den skapade webbplatsen bör hanteras från konsolen Communities - Sites, samma konsol som nya platser kan skapas från.

När du har valt communityplatsens mapp för du muspekaren över platsikonen så att fyra åtgärdsikoner visas:

![siteactionicons](assets/siteactionicons.png)

När du väljer ellipsikonen (ikonen Fler åtgärder) visas alternativen Exportera plats och Ta bort plats.

![siteactionsnya](assets/siteactionsnew.png)

Från vänster till höger är de:

* **Öppna webbplats**

   Välj pennikonen för att öppna communitywebbplatsen i redigeringsläge för författare för att lägga till och/eller konfigurera sidkomponenter.

* **Redigera webbplats**

   Välj egenskapsikonen för att öppna communitywebbplatsen för ändring av egenskaper, till exempel titeln, eller för att ändra temat.

* **Publicera webbplats**

   Välj ikonen world om du vill publicera communitywebbplatsen (till localhost:4503 som standard).

* **Exportera plats**

   Välj exportikonen om du vill skapa ett paket för communitywebbplatsen som både lagras i [pakethanteraren](/help/sites-administering/package-manager.md) och hämtas.
Observera att UGC inte ingår i platspaketet.

* **Ta bort plats**

   Om du vill ta bort communitywebbplatsen väljer du ikonen Ta bort plats som visas när du håller muspekaren över webbplatsen i Webbplatskonsolen. Den här åtgärden tar bort alla objekt som är associerade med platsen, till exempel UGC, användargrupper, resurser och databasposter.

   ![aktiveraAktivitetsåtgärder](assets/enablesiteactions.png)

#### Välj Publicera {#select-publish}

Välj världsikonen för att publicera communitywebbplatsen.

![chlimage_1-465](assets/chlimage_1-465.png)

Det kommer att finnas en indikation på att webbplatsen har publicerats.

![chlimage_1-466](assets/chlimage_1-466.png)

## Community-användare och användargrupper {#community-users-user-groups}

### Meddelande om nya användargrupper i användargruppen {#notice-new-community-user-groups}

Tillsammans med den nya communitywebbplatsen skapas nya användargrupper som har rätt behörigheter för olika administrativa funktioner. Mer information finns i [Användargrupper för Community Sites](/help/communities/users.md#usergroupsforcommunitysites).

Med tanke på webbplatsens namn &quot;enable&quot; i steg 1 kan de nya användargrupperna som finns i publiceringsmiljön ses från [webbgruppskonsolen](/help/communities/members.md#groups-console):

![community_usergroup](assets/community_usergroup.png)

### Tilldela medlemmar till gruppen Aktivera medlemmar {#assign-members-to-community-enable-members-group}

Om tunneltjänsten är aktiverad för författaren kan du tilldela [användarna som skapades under den första konfigurationen](/help/communities/enablement-setup.md#publishcreateenablementmembers) till communitymedlemsgruppen för den nyligen skapade communitywebbplatsen.

Med hjälp av gruppkonsolen kan medlemmar läggas till individuellt eller genom medlemskap i en grupp.

I det här exemplet läggs gruppen `Community Ski Class` till som medlem i gruppen `Community Enable Members` och medlem `Quinn Harper`.

* Navigera till **Communities, Groups**-konsolen
* Välj gruppen *Aktivera communitymedlemmar*
* Ange &#39;ski&#39; i sökrutan **Lägg till medlemmar i grupp**
* Välj *Community Ski Class* (grupp av elever)
* Ange &#39;quinn&#39; i sökrutan
* Välj *Quinn Harper* (aktivera resurskontakt)

* Välj **Spara**

![chlimage_1-418](assets/chlimage_1-418.png)

## Konfigurationer vid publicering {#configurations-on-publish}

`https://localhost:4503/content/sites/enable/en.html {#http-localhost-content-sites-enable-en-html}`

![enablement-login](assets/enablement-login.png)

### Konfigurera för autentiseringsfel {#configure-for-authentication-error}

När en webbplats har konfigurerats och publicerats konfigurerar [du inloggningsmappningen](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`) på publiceringsinstansen. Fördelen är att när inloggningsuppgifterna inte anges korrekt kommer autentiseringsfelet att visa inloggningssidan för communitywebbplatsen igen med ett felmeddelande.

Lägg till en `Login Page Mapping` som:

* `/content/sites/enable/en/signin:/content/sites/enable/en`

### (Valfritt) Ändra standardstartsidan {#optional-change-the-default-home-page}

När du arbetar med publiceringswebbplatsen i demonstrationssyfte kan det vara praktiskt att ändra standardhemsidan till den nya webbplatsen.

Om du vill göra det måste du använda [CRX|DE](https://localhost:4503/crx/de) Lite för att redigera resursmappningstabellen [vid publicering.](/help/sites-deploying/resource-mapping.md)

Så här kommer du igång:

1. Vid publicering får du åtkomst till CRXDE och loggar in med administratörsbehörighet

   * Bläddra till exempel till [https://localhost:4503/crx/de](https://localhost:4503/crx/de) och logga in med `admin/admin`

1. Expandera `/etc/map` i projektwebbläsaren
1. Välj noden `http`

   * Välj **Skapa nod**

      * **** Namelocalhost.4503

         (do *not* use &#39;:&#39;)

      * **** [typbestämning:mappning](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. Med den nyskapade `localhost.4503`-noden markerad

   * Lägg till egenskap

      * **** namngivning:matchning
      * **** TypeString
      * **** Valuelocalhost.4503/$

   (måste sluta med tecknet &#39;$&#39;)

   * Lägg till egenskap

      * **** namngivning:internalRedirect
      * **** TypeString
      * **Värde** /content/sites/enable/en.html


1. Välj **Spara alla**
1. (Valfritt) Ta bort webbläsarhistoriken
1. Gå till https://localhost:4503/

   * Ankomst till https://localhost:4503/content/sites/enable/en.html

>[!NOTE]
>
>Om du vill inaktivera kan du förpend egenskapsvärdet `sling:match` med x - `xlocalhost.4503/$` - och **Spara alla**.

![chlimage_1-364](assets/chlimage_1-364.png)

#### Felsökning: Det gick inte att spara kartan {#troubleshooting-error-saving-map}

Om det inte går att spara ändringarna måste du kontrollera att nodnamnet är `localhost.4503`, har en punktavgränsare och inte `localhost:4503` med en kolonavgränsare, eftersom `localhost` inte är ett giltigt namnområdesprefix.

![chlimage_1-365](assets/chlimage_1-365.png)

#### Felsökning: Det gick inte att omdirigera {#troubleshooting-fail-to-redirect}

&#39;**$**&#39; i slutet av det reguljära uttrycket `sling:match`-strängen är avgörande, så att endast exakt `https://localhost:4503/` mappas, annars läggs omdirigeringsvärdet till alla sökvägar som kan finnas efter server:port i URL:en. När AEM försöker dirigera om till inloggningssidan misslyckas den alltså.

## Ändra communityplatsen {#modifying-the-community-site}

När webbplatsen har skapats kan författare använda ikonen [Öppna plats](/help/communities/sites-console.md#authoring-site-content) för att utföra AEM.

Dessutom kan administratörer använda ikonen [Redigera plats](/help/communities/sites-console.md#modifying-site-properties) för att ändra egenskaper för platsen, till exempel titeln.

När du har ändrat något bör du komma ihåg att **spara** och göra om-**Publicera** webbplatsen.

>[!NOTE]
>
>Om du inte känner till AEM kan du läsa dokumentationen om [grundläggande hantering](/help/sites-authoring/basic-handling.md) och en [snabbguide till redigeringssidor](/help/sites-authoring/qg-page-authoring.md).

### Lägg till en katalog {#add-a-catalog}

Den communityplatsmall som valts för den här communitywebbplatsen bör innehålla katalogfunktionen.

Om inte kan du enkelt lägga till katalogfunktionen. På så sätt kan andra medlemmar i communityn, som inte är tilldelade till aktiveringsresurser eller en utbildningsväg, välja aktiveringsresurser från en katalog.

Om platsstrukturen redan innehåller katalogfunktionen kan dess namn ändras.

Om du vill ändra platsens struktur går du till **[!UICONTROL Communities]** > **[!UICONTROL Sites]**-konsolen, öppnar mappen `enable` och väljer ikonen **Redigera plats** för att komma åt egenskaperna för `Enablement Tutorial`.

Välj STRUKTURpanelen om du vill lägga till en katalog eller ändra en befintlig katalog:

* **Titel**:  `Ski Catalog`

* **URL**:  `catalog`

* **Markera alla namnutrymmen**: lämna som standard.

* Välj **Spara**.

![chlimage_1-299](assets/chlimage_1-299.png)

Använd placeringsikonen för att flytta katalogfunktionen till den andra positionen, efter tilldelningar.

![chlimage_1-300](assets/chlimage_1-300.png)

Välj **Spara** i det övre högra hörnet för att spara ändringarna på communitywebbplatsen.

Gör sedan om -**Publicera** webbplatsen.

