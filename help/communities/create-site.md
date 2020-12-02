---
title: Skapa en ny communitywebbplats
seo-title: Skapa en ny communitywebbplats
description: Så här skapar du en ny AEM Communities-webbplats
seo-description: Så här skapar du en ny AEM Communities-webbplats
uuid: 4f609f5f-ef07-44fc-aeb3-1c616e120d46
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8ae324ea-8b84-47a3-aabf-1fee2a3bd46d
docset: aem65
translation-type: tm+mt
source-git-commit: 2daf00f17058de8b901848fcf1128a5ee9770368
workflow-type: tm+mt
source-wordcount: '1640'
ht-degree: 1%

---


# Skapa en ny communitywebbplats{#author-a-new-community-site}

## Skapa en communitywebbplats {#create-a-community-site}

Använd författarinstansen för att skapa en community-webbplats. I AEM Author-instans:

1. Logga in med administratörsbehörighet.
1. Från global navigering går du till **[!UICONTROL Communities]** > **[!UICONTROL Sites]**.

Konsolen Communities Sites innehåller en guide som hjälper dig att skapa en communityplats. Du kan gå vidare till `Next`-steget eller `Back` till föregående steg innan du implementerar platsen i det sista steget.

Så här börjar du skapa en ny community-webbplats:

* Välj knappen `Create`.

![createcommunitysite](assets/createcommunitysite.png)

### Steg 1: Platsmall {#step-site-template}

![mall för att skapa webbplats](assets/create-site.png)

I [steget Webbplatsmall](/help/communities/sites-console.md#step2013asitetemplate) anger du en titel, beskrivning, namn för webbadressen och väljer en mall för en community-webbplats, till exempel:

* **Webbplatstitel** för communityn:  `Getting Started Tutorial`
* **Beskrivning** av communityplats:  `A site for engaging with the community.`
* **Rotadress** för communityplats: (lämna tomt för standardroten  `/content/sites`)
* **Molnkonfigurationer**: (lämna tomt om ingen molnkonfiguration har angetts) ange sökvägen till de angivna molnkonfigurationerna.
* **Grundspråk** för communitywebbplats: (lämnas orört för ett enda språk: På engelska) använder du listrutan för att välja ett  *eller* flera språk bland de tillgängliga språken - tyska, italienska, franska, japanska, spanska, portugisiska (Brasilien), kinesiska (traditionell) och kinesiska (förenklad). En communityplats skapas för varje språk som läggs till och finns i samma webbplatsmapp enligt den bästa praxis som beskrivs i [Översätta innehåll för flerspråkiga platser](/help/sites-administering/translation.md). Rotsidan för varje webbplats kommer att innehålla en underordnad sida med språkkoden för ett av de valda språken, till exempel &quot;en&quot; för engelska eller &quot;fr&quot; för franska.

* **Namn på** communitywebbplats: engagera

   * Dubbelkontrollera namnet eftersom det inte är lätt att ändra efter att webbplatsen har skapats
   * Den inledande URL:en visas under namnet på communitywebbplatsen
   * Ange en giltig URL genom att lägga till en baskod + &quot;.html&quot;
   * *Till exempel* https://localhost:4502/content/sites/  `engage/en.html`

* **Mall**: dra nedåt för att välja  `Reference Site`

* Välj **Nästa**.

### Steg 2: Design {#step-design}

Designsteget presenteras i två avsnitt där du kan välja tema och varumärkesbanderoll:

#### TEMA FÖR GEMENSKAPENS WEBBPLATS {#community-site-theme}

Välj det format som du vill använda på mallen. När du väljer det här alternativet kommer temat att överlappas av en bock.

#### GEMENSKAPENS WEBBPLATSVARNING {#community-site-branding}

(Valfritt) Ladda upp en banderollbild som ska visas på webbplatsens sidor. Banderollen är fäst vid webbläsarens vänstra kant, mellan communitysidhuvudet och navigeringslänkarna. Banderollhöjden beskärs till 120 pixlar. Banderollens storlek ändras inte så att den passar webbläsarens bredd och höjden 120 pixlar.

![community-site-branding](assets/community-site-branding.png)

![upload-image-site](assets/upload-image-site.png)

Välj **Nästa**.

### Steg 3: Inställningar {#step-settings}

Observera, innan du väljer `Next` i steget Inställningar, att det finns sju avsnitt som ger åtkomst till konfigurationer som användarhantering, taggning, moderering, grupphantering, analys, översättning och aktivering.

Gå till självstudiekursen [Getting Started with AEM Communities for Enablement](/help/communities/getting-started-enablement.md) för att få information om hur du arbetar med aktiveringsfunktionerna.

#### Användarhantering {#user-management}

Markera alla kryssrutor för [Användarhantering](/help/communities/sites-console.md#user-management)

* Tillåta besökare att registrera sig själva
* Så här kan besökare på webbplatsen visa den utan att logga in
* Så här tillåter du medlemmar att skicka och ta emot meddelanden från andra communitymedlemmar
* Tillåt inloggning på Facebook i stället för att registrera och skapa en profil
* Så här tillåter du inloggning med Twitter i stället för att registrera och skapa en profil

>[!NOTE]
>
>För en produktionsmiljö är det nödvändigt att skapa anpassade Facebook- och Twitter-program. Se [Social inloggning på Facebook och Twitter](/help/communities/social-login.md).

![communityinställningar](assets/site-settings.png)

#### TAGGAR {#tagging}

De taggar som kan användas för communityinnehåll kontrolleras genom att AEM namnutrymmen som tidigare definierats via [taggningskonsolen](/help/sites-administering/tags.md#tagging-console) (till exempel namnutrymmet [Tutorial](/help/communities/setup.md#create-tutorial-tags)) väljs.

Det är enkelt att hitta namnutrymmen med typsnittssökning. Till exempel,

* Typ `tut`
* Välj `Tutorial`

![taggning](assets/tagging.png)

#### ROLLER {#roles}

[Gruppmedlemsroller ](/help/communities/users.md) tilldelas via inställningarna i avsnittet Roller.

Om du vill att en community-medlem (eller grupp av medlemmar) ska kunna uppleva webbplatsen som community-hanterare använder du typsnittssökningen och väljer medlemmens eller gruppens namn bland alternativen i listrutan.

Till exempel,

* Typ `q`
* Välj [Quinn Harper](/help/communities/enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[Tunneltjänsten ](https://helpx.adobe.com/experience-manager/6-3/help/communities/deploy-communities.html#tunnel-service-on-author) gör det möjligt att välja medlemmar och grupper som finns endast i publiceringsmiljön.

![användarroller på ny plats](assets/site-admin-1.png)

#### MODERATION {#moderation}

Acceptera de globala standardinställningarna för [moderering](/help/communities/sites-console.md#moderation) användargenererat innehåll (UGC).

![moderering](assets/moderation1.png)

#### ANALYTIK {#analytics}

Om Adobe Analytics är licensierat och en molntjänst och ett ramverk för Analytics har konfigurerats går det att aktivera Analytics och välja ramverket.

Se [Analyskonfiguration för communityfunktioner](/help/communities/analytics.md).

![analys](assets/analytics.png)

#### TRANSLATION {#translation}

[Översättningsinställningarna](/help/communities/sites-console.md#translation) anger webbplatsens grundspråk samt om UGC kan översättas eller inte och i så fall till vilket språk.

* Kontrollera **Tillåt maskinöversättning**
* Låt standardspråken vara markerade för översättning av standardmaskinöversättningstjänsten
* Lämna standardöversättningsprovider och -konfiguration
* Ingen global butik behövs eftersom det inte finns några språkversioner
* Välj **Översätt hela sidan**
* Lämna standardalternativet för beständighet

![translation-settings](assets/translation-settings.png)

#### AKTIVERA {#enablement}

Lämna tomt när du skapar en engagemangscommunity.

En liknande självstudiekurs för att snabbt skapa en [aktiveringscommunity](/help/communities/overview.md#enablement-community) finns i [Komma igång med AEM Communities för att aktivera](/help/communities/getting-started-enablement.md).

Välj **Nästa**.

![aktivering](assets/enablement.png)

### Steg 4: Skapa webbgruppsplats {#step-create-communities-site}

Välj **Skapa.**

![create-site](assets/create-site2.png)

När processen är klar visas mappen för den nya platsen i konsolen Communities - Sites.

![communityerplatskonsol](assets/communitiessitesconsole.png)

## Publicera communitywebbplatsen {#publish-the-community-site}

Den skapade webbplatsen bör hanteras från konsolen Communities - Sites, samma konsol som nya platser kan skapas från.

När du har valt att öppna gruppplatsens mapp för att öppna den håller du pekaren över platsikonen så att fyra åtgärdsikoner visas:

![siteactionicons-1](assets/siteactionicons-1.png)

När du väljer den fjärde ellipsikonen (Fler åtgärder) visas alternativen Exportera plats och Ta bort plats.

![siteactionsnew-1](assets/siteactionsnew-1.png)

Från vänster till höger är de:

* **Öppna webbplats**

   Välj pennikonen för att öppna communitywebbplatsen i redigeringsläge för författare, för att lägga till och/eller konfigurera sidkomponenter

* **Redigera webbplats**

   Välj egenskapsikonen för att öppna communitywebbplatsen för ändring av egenskaper, som titeln eller för att ändra temat

* **Publicera webbplats**

   Välj världsikonen om du vill publicera communitywebbplatsen (till exempel om publiceringsservern körs på den lokala datorn, och sedan till localhost:4503 som standard)

* **Exportera plats**

   Välj exportikonen om du vill skapa ett paket för communitywebbplatsen som både lagras i [pakethanteraren](/help/sites-administering/package-manager.md) och hämtas.
Observera att UGC inte ingår i platspaketet.

* **Ta bort plats**

   Välj ikonen Ta bort om du vill ta bort communitywebbplatsen från **[!UICONTROL Communities > Sites console]**. Den här åtgärden tar bort alla objekt som är associerade med platsen, till exempel UGC, användargrupper, resurser och databasposter.

![webbplatseråtgärder](assets/siteactions.png)

>[!NOTE]
>
>Om du inte använder standardporten 4503 för publiceringsinstansen redigerar du standardreplikeringsagenten och anger portnumret till rätt värde.
>
>På författarinstansen från huvudmenyn:
>
>1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Replication]**-menyn.
>1. Välj **[!UICONTROL Agents on author]**.
>1. Välj **[!UICONTROL Default Agent (publish)]**.
>1. Välj **[!UICONTROL Edit]** bredvid **[!UICONTROL Settings]**.
>1. Välj fliken **[!UICONTROL Transport]** i popup-dialogrutan för agentinställningar.
>1. I URI ändrar du portnumret 4503 till önskat portnummer. Om du till exempel vill använda port 6103: https://localhost:6103/bin/receive?sling:authRequestLogin=1
>1. Välj **[!UICONTROL OK]**.
>1. (Valfritt) Välj **[!UICONTROL Clear]** eller **[!UICONTROL Force Retry]** om du vill återställa replikeringskön.


### Välj Publicera {#select-publish}

När du har kontrollerat att publiceringsservern körs väljer du världsikonen för att publicera communitywebbplatsen.

![publicera-webbplats](assets/publish-site.png)

När communitywebbplatsen har publicerats visas ett kort meddelande med texten&quot;Publicerad webbplats&quot;.

### Nya användargrupper i användargruppen {#new-community-user-groups}

Tillsammans med den nya communitywebbplatsen skapas nya användargrupper som har rätt behörigheter för olika administrativa funktioner. Mer information finns i [Användargrupper för Community Sites](/help/communities/users.md#usergroupsforcommunitysites).

Med tanke på webbplatsens namn&quot;engage&quot; i steg 1 kan de fyra nya användargrupperna ses från [Groups console](/help/communities/members.md) (global navigering: Communities, Groups):

* Community Engage Community managers
* Administratörer för communityinteraktionsgrupper
* Medlemmar i communityengagemang
* Moderatorer för communityengagemang
* Privilegierade medlemmar för communityengagemang
* Content Manager för communitywebbplats

Observera att [Aaron McDonald](/help/communities/tutorials.md#demo-users) är medlem i

* Community Engage Community managers
* Moderatorer för communityengagemang
* Medlemmar i communityn (indirekt som medlem i gruppen Moderatorer)

![användargrupp](assets/user-group.png)

#### https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![engagera](assets/engage.png)

## Konfigurera för autentiseringsfel {#configure-for-authentication-error}

När en webbplats har konfigurerats och publicerats konfigurerar [du inloggningsmappningen](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`) på publiceringsinstansen. Fördelen är att när inloggningsuppgifterna inte anges korrekt kommer autentiseringsfelet att visa inloggningssidan för communitywebbplatsen igen med ett felmeddelande.

Lägg till en `Login Page Mapping` som

* `/content/sites/engage/en/signin:/content/sites/engage/en`

## Valfria steg {#optional-steps}

### Ändra standardstartsidan {#change-the-default-home-page}

När du arbetar med publiceringswebbplatsen i demonstrationssyfte kan det vara praktiskt att ändra standardhemsidan till den nya webbplatsen.

Om du vill göra det måste du använda [CRXDE](https://localhost:4503/crx/de) Lite för att redigera tabellen [resource-mapping](/help/sites-deploying/resource-mapping.md) vid publicering.

Så här kommer du igång:

1. Logga in med administratörsbehörighet vid publicering.
1. Bläddra till [https://localhost:4503/crx/de](https://localhost:4503/crx/de).
1. Expandera `/etc/map.` i projektwebbläsaren
1. Markera noden `http`:

   * Välj **Skapa nod:**

      * **** Namelocalhost.4503 (använd  ** inte &#39;:&#39;)

      * **** [typbestämning:mappning](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. Med den nyskapade `localhost.4503`-noden markerad:

   * Lägg till egenskap:

   * **** namngivning:matchning
      * **** TypeString
      * **** Valuelocalhost.4503/$ (måste avslutas med tecknet &#39;$&#39;)
   * Lägg till egenskap:

      * **** namngivning:internalRedirect
      * **** TypeString
      * **Värde** /content/sites/engage/en.html


1. Välj **Spara alla.**
1. (Valfritt) Ta bort webbläsarhistoriken.
1. Gå till https://localhost:4503/.

   * Ankomst till https://localhost:4503/content/sites/engage/en.html

>[!NOTE]
>
>Om du vill inaktivera det anger du bara ett prefix för egenskapsvärdet `sling:match` med x - `xlocalhost.4503/$` - och **Spara alla**.

![valfria steg](assets/optional-steps.png)

#### Felsökning: Det gick inte att spara kartan {#troubleshooting-error-saving-map}

Om det inte går att spara ändringarna måste du kontrollera att nodnamnet är `localhost.4503`, med en punktavgränsare och inte `localhost:4503` med en kolonavgränsare, eftersom `localhost`inte är ett giltigt namnområdesprefix.

![error-message](assets/error-message.png)

#### Felsökning: Det gick inte att omdirigera {#troubleshooting-fail-to-redirect}

&#39;**$**&#39; i slutet av det reguljära uttrycket `sling:match`strängen är avgörande, så att endast exakt `https://localhost:4503/` mappas, annars prefixeras omdirigeringsvärdet till alla sökvägar som kan finnas efter server:port i URL:en. När AEM försöker dirigera om till inloggningssidan misslyckas den alltså.

### Ändra platsen {#modify-the-site}

När webbplatsen har skapats kan författare använda ikonen [Öppna plats](/help/communities/sites-console.md#authoring-site-content) för att utföra AEM.

Dessutom kan administratörer använda ikonen [Redigera plats](/help/communities/sites-console.md#modifying-site-properties) för att ändra egenskaper för platsen, till exempel titeln.

När du har ändrat något bör du komma ihåg att **spara** och göra om-**Publicera** webbplatsen.

>[!NOTE]
>
>Om du inte känner till AEM kan du läsa dokumentationen om [grundläggande hantering](/help/sites-authoring/basic-handling.md) och en [snabbguide till redigeringssidor](/help/sites-authoring/qg-page-authoring.md).
