---
title: Konsolen Webbplatser
seo-title: Communities Sites Console
description: Åtkomst till konsolen Communities Sites
seo-description: How to access the Communities Sites console
uuid: 74134281-244c-40da-a941-7f2f3e706d4b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 4130f952-5bb5-4e32-91d6-47b2885b30a4
docset: aem65
role: Admin
exl-id: 426e3adf-3723-4d17-a988-6eb050939e68
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '3276'
ht-degree: 0%

---

# Konsolen Webbplatser {#communities-sites-console}

Konsolen Communities Sites ger åtkomst till:

* Skapa webbplats
* Webbplatsredigering
* Platshantering
* [Skapa och redigera kapslade grupper](/help/communities/groups.md) (undergrupper)

Se [Komma igång med AEM Communities](/help/communities/getting-started.md) om du vill se hur snabbt en community kan skapas i författarmiljön, och hur du kan skapa communitygrupper från författarmiljön och publiceringsmiljöer.

>[!NOTE]
>
>De viktigaste webbgruppsmenyerna för att skapa [communitysajter](/help/communities/sites-console.md), [mallar för communitysajter](/help/communities/sites.md), [communitygruppsmallar](/help/communities/tools-groups.md) och [communityfunktioner](/help/communities/functions.md) används endast i författarmiljön.

## Förutsättningar {#prerequisites}

Innan du skapar en community-webbplats är det *obligatoriskt* till:

* Kontrollera att en eller flera publiceringsinstanser körs.
* Aktivera [tunneltjänst](/help/communities/deploy-communities.md#tunnel-service-on-author) för att hantera medlemmar och medlemsgrupper.
* Identifiera [primär utgivare](/help/communities/deploy-communities.md#primary-publisher).
* [Konfigurera replikering](/help/communities/deploy-communities.md#replication-agents-on-author) när den primära utgivarporten inte är standard (4503).

Det bästa sättet att se till att webbplatsen är förberedd för många funktioner är att utföra följande steg:

* Installera [senaste funktionspaketet](/help/communities/deploy-communities.md#latestfeaturepack).
* Aktivera [Adobe Analytics](/help/communities/analytics.md) för AEM Communities.
* Konfigurera [e-post](/help/communities/email.md)
* Identifiera [Community-administratörer](/help/communities/users.md#creating-community-members).
* [Aktivera OAuth-hanterare](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler) för social inloggning.

## Åtkomst till webbgruppskonsolen {#accessing-communities-sites-console}

För att nå konsolen Webbplatser i författarmiljön:

* Från global navigering: **[!UICONTROL Communities]** > **[!UICONTROL Sites]**

Konsolen Communities Sites visar alla befintliga communityplatser. Från den här konsolen kan communitywebbplatser skapas, redigeras, hanteras och tas bort.

Om du vill skapa en ny community-webbplats väljer du **Skapa** ikon.

Om du vill komma åt en befintlig communitywebbplats och redigera, publicera, exportera eller lägga till en kapslad grupp, markerar du platsens mappikon.

Följande bild visar till exempel huvudkonsolen Webbplatser i Communities som visar mapparna för två communityplatser: [enable](/help/communities/getting-started-enablement.md) och [engagera](/help/communities/getting-started.md):

![site-console](assets/site-console.png)

## Skapa webbplats {#site-creation}

Konsolen för att skapa webbplatser är en stegvis metod för att sätta ihop funktioner på webbplatsen baserat på ett valt [mall för communitywebbplats](/help/communities/sites.md) och inställningar.

Varje webbplats som skapas innehåller en inloggningsfunktion eftersom besökarna måste logga in innan de kan publicera innehåll, skicka meddelanden eller delta i en grupp. Andra funktioner som ingår är användarprofiler, meddelanden, meddelanden, webbplatsmenyer, sökning, teman och varumärken.

Processen startas genom att du väljer `Create` längst upp i webbgruppskonsolen.

Skapandeprocessen är en serie steg som presenteras som paneler med en uppsättning funktioner som ska konfigureras (presenteras som underpaneler). Det går att gå vidare till **Nästa** steg eller **Bakåt** till föregående steg innan webbplatsen implementeras i det sista steget.

### Steg 1: Webbplatsmall {#step-site-template}

![newsitetemplate](assets/newsitetemplate.png)

På panelen Platsmall anges titel, beskrivning, platsrot, grundspråk, namn och platsmall:

* **Rubrik för communitywebbplats**

   En visningsrubrik för webbplatsen.

   Titeln visas på den publicerade webbplatsen samt i användargränssnittet för webbplatsadministratörer.

* **Beskrivning av communityplats**

   En beskrivning av platsen.

   Beskrivningen visas inte på den publicerade webbplatsen.

* **Community-platsrot**

   Rotsökvägen till platsen.

   Standardroten är `/content/sites`, men roten kan flyttas till valfri plats på webbplatsen.

* **Bas-språk för communitywebbplats**

   (Ändra inte för ett enda språk: Engelska) Använd listrutan för att välja en *eller mer* basspråk från tillgängliga språk - tyska, italienska, franska, japanska, spanska, portugisiska (Brasilien), kinesiska (traditionell) och kinesiska (förenklad). En community-webbplats skapas för varje språk som läggs till och finns i samma webbplatsmapp enligt de rutiner som beskrivs i [Översätta innehåll för flerspråkiga webbplatser](/help/sites-administering/translation.md). Rotsidan för varje webbplats kommer att innehålla en underordnad sida med språkkoden för ett av de valda språken, till exempel &quot;en&quot; för engelska eller &quot;fr&quot; för franska.

* **Namn på communitywebbplats**:

   Namnet på webbplatsens rotsida som visas i URL:en.

   * Dubbelkontrollera namnet eftersom det inte är lätt att ändra efter att webbplatsen har skapats.
   * Bas-URL ( `https://server:port/site root/site name)` visas under `Community Site Name`.

   * Ange en giltig URL genom att lägga till en baskod + &quot;.html&quot;

      *Till exempel*, `https://localhost:4502/content/sites/mysight/en.html`

* **Community-webbplatsmall** meny

   Använd listrutan för att välja en tillgänglig [mall för communitywebbplats](/help/communities/tools.md).

* Välj **Nästa**.

### Steg 2: Design {#step-design}

Designpanelen innehåller två underpaneler för att välja tema och varumärkesbanderoll:

#### TEMA PÅ GEMENSKAPENS WEBBPLATS {#community-site-theme}

![sitetema](assets/sitetheme.png)

Ramverket använder `Twitter Bootstrap` för att ge webbplatsen en responsiv, flexibel design. Ett av de många förinlästa Bootstrap-temana kan väljas för att formatera den valda communitywebbplatsmallen, eller så kan ett Bootstrap-tema överföras.

När du väljer det här alternativet överlagras temat med en ogenomskinlig blå bockmarkering.

När communitywebbplatsen har publicerats är det möjligt att [redigera egenskaperna](#modifying-site-properties) och välj ett annat tema.

#### GEMENSKAPENS WEBBPLATSHANTERING {#community-site-branding}

![webbplatsmärkning](assets/site-branding.png)

Webbplatsmärkning är en bild som visas som en rubrik högst upp på varje sida.

Bilden bör storleksändras så att den blir lika bred som den förväntade visningen av sidan i webbläsaren och 120 pixlar hög.

Tänk på följande när du skapar eller markerar en bild:

* Bildens höjd beskärs till 120 pixlar från bildens överkant.
* Bilden är fäst vid webbläsarfönstrets vänstra kant.
* Det finns ingen storleksändring av bilden, så att när bildbredden är...

   * Bilden upprepas vågrätt om den är mindre än webbläsarens bredd.
   * Bilden kommer att beskäras mer än webbläsarens bredd.

* Välj **Nästa**.

### Steg 3: Inställningar {#step-settings}

Panelen Inställningar innehåller flera underpaneler med funktioner som ska konfigureras innan du går till det sista steget för att skapa webbplatsen.

* [ANVÄNDARHANTERING](#user-management)
* [TAGGNING](#tagging)
* [ROLLER](#roles)
* [MODERATION](#moderation)
* [ANALYS](#analytics)
* [ÖVERSÄTTNING](#translation)
* [AKTIVERING](#enablement)

>[!NOTE]
>
>**Aktivera tunneltjänsten**
>
>Flera av underpanelerna Inställningar tillåter tilldelning av en betrodd medlem till måttlig användargenererad kod, hantera grupper eller vara kontakter för aktiveringsresurser i publiceringsmiljön.
>
>Konventionen gäller för publicering [användare och användargrupper](/help/communities/users.md) (medlemmar och medlemsgrupper) ska inte dupliceras i författarmiljön.
>
>När du skapar en community-webbplats i författarmiljön och tilldelar betrodda medlemmar till olika roller måste du därför hämta medlemsdata från publiceringsmiljön.
>
>Detta uppnås genom att aktivera ` [AEM Communities Publish Tunnel Service](/help/communities/deploy-communities.md#tunnel-service-on-author)` för redigeringsmiljön.

#### ANVÄNDARHANTERING {#user-management}

![createplatserinställningar](assets/createsitesettings.png)

>[!NOTE]
>
>Vi rekommenderar att [communitysajter för aktivering](/help/communities/overview.md#enablement-community) vara privat (kontakta din kontorepresentant för mer information).
>
>En communitywebbplats är privat när anonyma besökare på webbplatsen nekas åtkomst, inte får registrera sig själv och inte får använda social inloggning.

* **Tillåt användarregistrering**

   Om det här alternativet är markerat kan besökarna bli communitymedlemmar genom självregistrering.
Om alternativet inte är markerat är communitywebbplatsen *begränsad* och besökarna måste tilldelas gruppplatsens medlemsgrupp, göra en förfrågan eller få en inbjudan via e-post. Om alternativet inte är markerat bör anonym åtkomst inte tillåtas.
Avmarkera *private* communitysajt. Standard är markerat.

* **Tillåt anonym åtkomst**

   Om det här alternativet är markerat är communitywebbplatsen *öppen *och alla besökare kan komma åt webbplatsen.
Om alternativet inte är markerat kan bara inloggade medlemmar få åtkomst till webbplatsen.
Avmarkera om det finns en *privat *community-webbplats. Standard är markerat.

* **Tillåt meddelanden**

   Om det här alternativet är markerat kan medlemmarna skicka meddelanden till varandra och till gruppen på communitywebbplatsen.
Om alternativet inte är markerat är meddelanden inte konfigurerade för communityn.
Standard är avmarkerat.

* **Tillåt sociala inloggningar: Facebook**

   Om det här alternativet är markerat kan webbplatsbesökare logga in med sina Facebook-kontouppgifter. Den markerade [Facebook molnkonfiguration](/help/communities/social-login.md#create-a-facebook-connect-cloud-service) bör konfigureras så att användare läggs till i communityplatsens medlemsgrupp när communitywebbplatsen har skapats.
Om du inte markerar det här alternativet visas ingen Facebook-inloggning.
Låt vara omarkerad för en *private* communitysajt. Standard är avmarkerat.

* **Tillåt sociala inloggningar: Twitter**

   Om det här alternativet är markerat kan webbplatsbesökare logga in med sina Twitter-kontouppgifter. Den markerade [Twitter molnkonfiguration](/help/communities/social-login.md#create-a-twitter-connect-cloud-service) bör konfigureras så att användare läggs till i communityplatsens medlemsgrupp när communitywebbplatsen har skapats.
Om du inte markerar det här alternativet visas ingen Twitter-inloggning.
Låt vara omarkerad för en *private* communitysajt. Standard är avmarkerat.

>[!NOTE]
>
>**Tillåta sociala inloggningar**
>
>Facebook- och Twitter-konfigurationer kan finnas och vara valbara för en [produktionsmiljö](/help/sites-administering/production-ready.md)måste du skapa anpassade Facebook- och Twitter-program. Se [Social inloggning med Facebook och Twitter](/help/communities/social-login.md).

#### TAGGNING {#tagging}

![webbplatstaggning](assets/site-tagging.png)

De taggar som kan användas på communityinnehåll kontrolleras genom att du väljer Taggnamnutrymmen som tidigare definierats i [Taggningskonsolen](/help/sites-administering/tags.md#tagging-console).

Om du väljer taggnamnutrymmen för communitywebbplatsen begränsas dessutom det urval som visas när du definierar kataloger och resurser. Se [Aktiveringsresurser för taggning](/help/communities/tag-resources.md) för viktig information.

* sökruta: Börja skriva för att identifiera taggar som kan användas på webbplatsen.

#### ROLLER {#roles}

![Community-roller](assets/site-admin-2.png)

The [roller för communitymedlemmar](/help/communities/users.md) har tilldelats med dessa inställningar.

Det är enkelt att hitta communitymedlemmar med hjälp av typsnittssökning.

* **Community Managers**

   Börja skriva för att välja en eller flera community-medlemmar eller medlemsgrupper som kan hantera community-medlemmar och medlemsgrupper.

* **Community-moderatorer**

   Börja skriva för att välja en eller flera communitymedlemmar eller medlemsgrupper som ska betraktas som pålitliga som moderatorer för användargenererat innehåll.

* **Medlemmar med behörighet i communityn**

   Börja skriva för att välja en eller flera communitymedlemmar eller medlemsgrupper som ska kunna skapa nytt innehåll när `Allow Privileged Member` har valts för en [communityfunktion](/help/communities/functions.md).

* **Community-administratörer**

   Börja skriva för att välja en eller flera webbplatsadministratörer som kan hantera webbplatsstrukturen oberoende av andra webbplatsadministratörer och standardadministratörer. De kan skapa grupper på vilken nivå som helst i hierarkin och bli standardadministratör för de kapslade grupperna (men de kan senare tas bort från administratörsrollen för kapslade grupper).

#### MODERATION {#moderation}

![webbplatsmoderering](assets/site-moderation.png)

Den globala inställningen för moderering av användargenererat innehåll (UGC) styrs av dessa inställningar. Enskilda komponenter har ytterligare inställningar för att styra modereringen.

* **Innehållet är förmodererat**

   Om det här alternativet är markerat visas inte publicerat communityinnehåll förrän det har godkänts av en moderator. Standard är avmarkerat. Mer information finns i [Moderating Community Content](/help/communities/moderate-ugc.md#premoderation).

* **Tröskelvärde för flagga innan innehåll döljs**

   Om värdet är större än 0 måste antalet gånger ett ämne eller ett inlägg flaggas innan det döljs för den offentliga vyn. Om värdet är -1 döljs aldrig det markerade ämnet eller inlägget från den offentliga vyn. Standardvärdet är 5.

#### ANALYS {#analytics}

![webbplatsanalys](assets/site-analytics.png)

* **Aktivera analys**

   Endast tillgängligt när Adobe Analytics har [konfigurerad](/help/communities/analytics.md) för communityfunktioner.
Standard är avmarkerat. När det här alternativet är markerat visas ytterligare en markeringsmeny:

![webbplatsanalys-aktivera](assets/site-analytics-enable.png)

* **Referens för Cloud Config Framework**

   I listrutan väljer du Analytics-molntjänstramverket som är konfigurerat för den här communitywebbplatsen.
   `Communities` är ramverkets exempel från [Analyskonfiguration för communityfunktioner](/help/communities/analytics.md#aem-analytics-framework-configuration) dokumentation.

#### ÖVERSÄTTNING {#translation}

![webbplatsöversättning](assets/site-translation.png)

* **Tillåt maskinöversättning**

   När det här alternativet är markerat (standardinställningen är avmarkerad) aktiveras maskinöversättning för UGC på platsen. Detta påverkar inte annat innehåll, t.ex. sidinnehåll, även om webbplatsen är konfigurerad som en flerspråkig webbplats. Se [Översätter användargenererat innehåll](/help/communities/translate-ugc.md) om du vill ha information om hur du konfigurerar en licensierad översättningstjänst för AEM Communities. Se [Översätta innehåll för flerspråkiga webbplatser](/help/sites-administering/translation.md) för en fullständig översikt.

![allow-machine-translation](assets/allow-machine-translation.png)

* **Aktivera maskinöversättning för valda språk**

   Språken som är aktiverade för maskinöversättning är standardinställningen för den systeminställning som anges av [konfiguration av översättningsintegrering](/help/communities/translate-ugc.md#translation-integration-configuration). Dessa standardinställningar kan åsidosättas för den här webbplatsen genom att standardinställningar tas bort och/eller genom att andra språk väljs i listrutan.

* **Välj översättningsleverantör**

   Som standard är tjänsteleverantören en provtjänst som använder `microsoft` endast för demonstrationer. Om ingen översättningstjänstleverantör är licensierad **Tillåt maskinöversättning** ska avmarkeras.

* **Välj globalt delat arkiv**

   För en webbplats med flera språkkopior innehåller ett globalt delat arkiv en enda konversationstråd som är synlig från varje språkkopia. Detta uppnås genom att välja ett av språken som ingår som en språkkopia. Standard är *Inget globalt delat arkiv*.

* **Välj konfiguration för översättningsprovider**

   Välj en [översättningsintegreringsramverk](/help/sites-administering/tc-tic.md) har skapats för den licensierade översättningsleverantören.

* **Välj översättningsalternativ för communitywebbplatsen**

   * **Översätt hela sidan**

      Om du väljer det här alternativet översätts all UGC på en sida till sidans basspråk.

      Standard är *inte markerad*.

   * **Översätt endast markering**

      Om du väljer det här alternativet visas ett översättningsalternativ intill varje inlägg som gör att enskilda inlägg kan översättas till sidans grundspråk.
Standard är *markerad*.

* **Välj alternativ för beständighet**

   * **Översätt avgifter på användarens begäran och fortsätt efteråt**
Om du väljer det här alternativet översätts inte innehållet förrän en begäran har gjorts. När översättningen är klar sparas översättningen i databasen.

      Standard är *inte markerad*.

   * **Behåll inte översättningar**

      Om du väljer det här alternativet lagras inte översättningar i databasen.

      Om det inte är markerat bevaras översättningar.

      Standard är *inte markerad*.

* **Smart rendering**

   Välj något av följande:

   * `Always show contributions in the original language` (standard)
   * `Always show contributions in user preferred language`
   * `Show contributions in user preferred language for only logged-in users`

#### AKTIVERING {#enablement}

![webbplatsaktivering](assets/site-enablement.png)

The `ENABLEMENT`inställningarna gäller när den valda communitywebbplatsmallen innehåller [tilldelningsfunktion](/help/communities/functions.md#assignments-function)som är tillgänglig när aktiveringsfunktionerna är licensierade och [konfigurerad](/help/communities/enablement.md). Referenswebbplatsmallen som innehåller tilldelningsfunktionen är `Reference Structured Learning Site Template.`

* **Aktivitetshanterare**
(Obligatoriskt) Endast medlemmar i `Community Enablementmanagers` gruppen är tillgänglig att väljas för att hantera den här aktiveringscommunityn. Aktivitetshanterare ansvarar för att tilldela medlemmar till resurser. Se även [Hantera användare och användargrupper](/help/communities/users.md).

* **Marketing Cloud organisation-ID**

   (valfritt) ID:t för en [Analys av pulsslag för video](/help/communities/analytics.md#video-heartbeat-analytics) licens.

* Välj **Nästa**.

### Steg 4: Skapa webbgruppsplats {#step-create-communities-site}

Om det behövs justeringar använder du **Bakåt** för att skapa dem.

En gång **Skapa** är markerat och startat kan processen att skapa platsen inte avbrytas.

När webbplatsen har skapats:

* Det går inte att ändra URL:en (nodnamn).
* Framtida ändringar av communitywebbplatsmallen kommer inte att påverka den skapade communitywebbplatsen.
* Om du inaktiverar communityplatsmallen påverkas inte den skapade communitywebbplatsen.
* Du kan redigera [STRUKTUR](#modify-structure) av en communitywebbplats genom att ändra dess egenskaper.

![create-site](assets/create-site1.png)

När processen är klar visas mappen för den nya platsen i konsolen Webbplatser, där författare kan lägga till sidinnehåll eller administratören kan ändra platsens egenskaper.

![modify-site-property](assets/modify-site-property.png)

Om du vill ändra en community-plats väljer du projektmappen för den:

![site-project](assets/site-project.png)

När du hovrar över en webbplats med en mus eller vidrör ett platskort visas ikoner som gör det möjligt att [redigera webbplatsen i redigeringsläge](#authoring-site-content), [öppna webbplatsegenskaperna för ändring](#modifying-site-properties), [publicera webbplatsen](#publishing-the-site), [exportera webbplatsen](#exporting-the-site)och [ta bort webbplatsen](#deleting-the-site).

## Skapa webbplatsinnehåll {#authoring-site-content}

Innehållet i en webbplats kan redigeras med samma verktyg som andra AEM. Om du vill öppna webbplatsen för redigering väljer du `Open Site` ikonen som visas när du hovrar webbplatsen med musen. Webbplatsen öppnas på en ny flik så att konsolen Webbplatser fortfarande är tillgänglig.

![webbplatsinnehåll](assets/site-content.png)

>[!NOTE]
>
>Om du inte känner till AEM kan du läsa dokumentationen om [grundläggande hantering](/help/sites-authoring/basic-handling.md) och [snabbguide till framtagning av sidor](/help/sites-authoring/qg-page-authoring.md).

## Ändra webbplatsegenskaper {#modifying-site-properties}

![edit-site](assets/edit-site.png)

Egenskaperna för en befintlig plats som anges när webbplatsen skapas kan ändras genom att välja `Edit Site`ikonen som visas när du hovrar webbplatsen med musen.

`Details of the following properties match the descriptions provided in the` [Skapa webbplats](#site-creation) -avsnitt.

![modify-site-basicinfo](assets/modify-site-basicinfo.png)

### Ändra grundläggande {#modify-basic}

På BASIC-panelen kan du ändra:

* Rubrik för communitywebbplats
* Beskrivning av communityplats

Det går inte att ändra namnet på communityplatsen.

Om du väljer en annan mall för en community-webbplats påverkas inte en befintlig community-webbplats eftersom det inte finns någon koppling mellan mallar och webbplatser.

I stället [STRUKTUR](#modify-structure) av communitywebbplatsen kan ändras.

### Ändra struktur {#modify-structure}

STRUKTURpanelen gör att du kan ändra den struktur som ursprungligen skapades från den valda mallen för communitywebbplatser. På panelen kan du:

* Dra och släpp ytterligare [communityfunktioner](/help/communities/functions.md) till webbplatsstrukturen.
* En instans av en communityfunktion i webbplatsstrukturen:

   * **`gear icon`**

      Redigera inställningar, inklusive visningsrubrik och URL-namn* samt [behöriga medlemsgrupper](/help/communities/users.md#privilegedmembersgroups).

   * **`trashcan icon`**

      Ta bort funktioner från platsstrukturen.

   * **`grid icon`**

      Ändra den ordning på funktioner som visas i navigeringsfältet på den översta nivån för webbplatsen.

>[!NOTE]
>
>Du kan ändra ordningen på alla funktioner i platsstrukturen förutom funktionen längst upp. Det innebär att det inte går att ändra startsidan för communitywebbplatsen.

>[!CAUTION]
>
>* Visningsrubriken kan ändras utan biverkningar, men du bör inte redigera URL-namnet för en community-funktion som tillhör en community-webbplats.
>
>Om du t.ex. byter namn på URL:en flyttas inte den befintliga UGC:n, vilket resulterar i&quot;UGC-förlust&quot;.

>[!CAUTION]
>
>Funktionen groups måste *not* vara *först eller bara* i platsstrukturen.
>
>Alla andra funktioner, till exempel [sidfunktion](/help/communities/functions.md#page-function), måste inkluderas och listas först.

#### Exempel: Lägga till en katalogfunktion i en community-platsstruktur {#example-adding-a-catalog-function-to-a-community-site-structure}

![add-catalog-site](assets/add-catalog-site.png)

### Ändra design {#modify-design}

På designpanelen kan du använda ett nytt tema:

* [Community Site Theme](#community-site-theme)
* [Varumärkning för communitysajter](#community-site-branding)

   * Bläddra till panelens nedre del för att ändra varumärkesbilden.

### Ändra inställningar {#modify-settings}

Med hjälp av inställningspanelen får du tillgång till de flesta inställningarna under underpanelerna i steg 3 för att skapa en community-webbplats:

* [Användarhantering](#user-management)
* [Taggar](#tagging)
* [Moderering](#moderation)
* [Medlemsroller](#roles)
* [Analyser](#analytics)
* [Översättning](#translation)

### Ändra miniatyrbild {#modify-thumbnail}

På panelen MINIATYRBILD kan en bild överföras för att representera webbplatsen i webbgruppskonsolen.

### Ändra aktivering {#modify-enablement}

ENABLEMENT-panelen ger åtkomst till inställningarna som anges när en community-webbplats skapas.

Se [AKTIVERING](#enablement) description.

## Publicera webbplatsen {#publishing-the-site}

När en community-webbplats har skapats eller ändrats på nytt kan du publicera (aktivera) webbplatsen genom att välja `Publish Site` -ikonen som visas när du hovrar musen över webbplatsen.

![publicera-webbplats](assets/publish-site.png)

En indikation visas när webbplatsen har publicerats.

![webbpublicerad](assets/site-published.png)

### Publicera med kapslade grupper {#publishing-with-nested-groups}

Efter publicering av en communitywebbplats är det nödvändigt att publicera varje undergrupp (kapslad grupp) som skapats med [Gruppkonsol](/help/communities/groups.md).

## Exportera platsen {#exporting-the-site}

![export-site](assets/export-site.png)

Välj exportikonen när du hovrar musen över webbplatsen för att skapa ett paket av communitywebbplatsen som båda lagras i [pakethanterare](/help/sites-administering/package-manager.md) och laddas ned.

Observera att UGC inte ingår i platspaketet.

## Tar bort platsen {#deleting-the-site}

![deleteicon](assets/deleteicon.png)

Om du vill ta bort communitywebbplatsen väljer du ikonen Ta bort plats som visas när du håller muspekaren över webbplatsen i Webbplatskonsolen. Den här åtgärden tar bort alla objekt som är associerade med platsen, till exempel UGC, användargrupper, resurser och databasposter.

## Skapade användargrupper i communityn {#created-community-user-groups}

När den nya communitywebbplatsen har publicerats skapas nya medlemsgrupper (användargrupper i publiceringsmiljön) som har rätt behörigheter för olika administrativa roller och medlemsroller.

Namnet som skapas för medlemsgrupperna innehåller *site-name* eftersom sajten [Steg 1](#step13asitetemplate) (namnet som visas i URL:en) samt ett unikt ID för att undvika konflikter med communitywebbplatser och grupper som har samma platsnamn för olika rötter i communityn.

Om namnet till exempel är &quot;engage&quot; för en webbplats med namnet &quot;Getting Started Tutorial&quot;, skulle användargruppen för moderatorer vara:

* titel: Moderatorer för communityengagemang
* namn: community-*engage-uid*-moderators

Observera att alla medlemmar som tilldelats roller som moderatorer eller gruppadministratörer när platsen skapas, kommer att tilldelas till rätt grupp samt till medlemsgruppen. Dessa grupper och medlemstilldelningar skapas vid publicering när den nya webbplatsen publiceras.

Mer information finns i [Hantera användare och användargrupper](/help/communities/users.md).

>[!NOTE]
>
>If [Tillåt social inloggning: Facebook](#user-management) aktiveras när användargruppen
>
>* `community-<site-name>-<uid>-members`
>
>skapas, används [Facebook molntjänst](/help/communities/social-login.md#createafacebookcloudservice) bör konfigureras för att lägga till användare i den här gruppen.

## Konfigurera för autentiseringsfel {#configure-for-authentication-error}

Som standard dirigeras en communitywebbplats om till en exempelinloggningssida när användaren anger fel inloggningsuppgifter och inte kan logga in. Detta exempel på inloggning kommer inte att finnas på en [produktionsserver](/help/sites-administering/production-ready.md).

Om du vill omdirigera korrekt, när en webbplats har konfigurerats och publicerats, slutför du de här stegen för att få autentiseringsfel att omdirigera till communitywebbplatsen:

* På varje AEM publiceringsinstans.
* Logga in med administratörsbehörighet.
* Öppna [Webbkonsol](/help/sites-deploying/configuring-osgi.md).

   * Till exempel: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

* Sök `Adobe Granite Login Selector Authentication Handler`.
* Välj `pencil` om du vill öppna konfigurationen för redigering.
* Ange **Mappningar av inloggningssidor** enligt följande:

   `/content/sites/<site-name>/path/to/login/page:/content/sites/<site-name>`

   Till exempel:
   `/content/sites/engage/en/signin:/content/sites/engage/en`

* Välj **Spara**.

![auth-error](assets/auth-error.png)

### Testa autentiseringsomdirigering {#test-authentication-redirection}

På samma AEM har publiceringsinstansen konfigurerats med en inloggningssidmappning för communitywebbplatsen:

* Bläddra till startsidan för communitywebbplatsen.

   * Till exempel: [https://localhost:4503/content/sites/engage/en.html](https://localhost:4503/content/sites/engage/en.html)

* Välj Logga ut.
* Välj Logga in.
* Ange uppenbart felaktiga inloggningsuppgifter, till exempel användarnamnet &quot;x&quot; och lösenordet &quot;x&quot;.
* Inloggningssidan ska visas med felmeddelandet&quot;ogiltig inloggning&quot;.

![test-authentication](assets/test-authentication.png)

## Åtkomst till communityplatser från huvudplatskonsolen {#accessing-community-sites-from-main-sites-console}

På den globala webbplatskonsolen finns communitywebbplatser i `Community Sites` mapp.

Det går att komma åt en community-webbplats på det här sättet, men för administrativa uppgifter bör communitywebbplatsen nås från konsolen Webbplatser för communities.

![webbplats](assets/access-site.png)
