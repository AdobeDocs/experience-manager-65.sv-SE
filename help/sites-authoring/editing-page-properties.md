---
title: Redigera sidegenskaper
seo-title: Redigera sidegenskaper
description: Definiera de egenskaper som krävs för en sida
seo-description: Definiera de egenskaper som krävs för en sida
uuid: d3a2183b-8082-4cfc-aeed-26facbf3f3e6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1e9dd0d7-209a-4989-b66b-bca0d04b437a
docset: aem65
translation-type: tm+mt
source-git-commit: 47a284a55f8d8f00ecda7be0bdcb8125cf976e3b

---


# Redigera sidegenskaper{#editing-page-properties}

Du kan definiera de egenskaper som krävs för en sida. Dessa kan variera beroende på sidans beskaffenhet. Vissa sidor kan till exempel vara kopplade till en live-kopia medan andra inte är det och live-kopieringsinformationen är tillgänglig efter behov.

## Sidegenskaper {#page-properties}

Egenskaperna fördelas på flera flikar.

### Grundläggande {#basic}

* **Titel**

   Sidans rubrik visas på olika platser. Till exempel fliklistan **Webbplatser** och vyerna **Webbplatser** .

   Detta är ett obligatoriskt fält.

* **Taggar**

   Här kan du lägga till eller ta bort taggar från sidan genom att uppdatera listan i valrutan:

   * När du har valt en tagg visas den under markeringsrutan. Du kan ta bort en tagg från den här listan med hjälp av x.
   * Du kan ange en helt ny tagg genom att skriva namnet i en tom markeringsruta.

      * Den nya taggen skapas när du trycker på Retur.
      * Den nya taggen visas sedan med en liten stjärna till höger som anger att det är en ny tagg.
   * Med den nedrullningsbara menyn kan du välja bland befintliga taggar.
   * Ett x-tecken visas när du för musen över en taggpost i markeringsrutan, som kan användas för att ta bort taggen för den här sidan.
   Mer information om taggar finns i [Använda taggar](/help/sites-authoring/tags.md).

* **Dölj i navigering**

   Anger om sidan visas eller döljs i sidnavigeringen på den slutliga platsen.

* **Sidrubrik**

   En rubrik som ska användas på sidan. Används vanligtvis av titelkomponenter. Om den är tom används **rubriken** .

* **Navigeringsrubrik**

   Du kan ange en separat rubrik som ska användas i navigeringen (om du till exempel vill ha något mer koncist). Om den är tom används **rubriken** .

* **Underrubrik**

   En underrubrik som ska användas på sidan.

* **Beskrivning**

   Din beskrivning av sidan, dess syfte eller annan information som du vill lägga till.

* **I tid**

   Det datum och den tidpunkt då den publicerade sidan ska aktiveras. När den publiceras kommer den här sidan att vara vilande tills den angivna tiden.

   Lämna dessa fält tomma för sidor som du vill publicera omedelbart (det normala scenariot).

* **Fråntid**

   Den tidpunkt då den publicerade sidan inaktiveras.

   Lämna dessa fält tomma igen så att du kan agera direkt.

* **Vanity URL**

   Gör att du kan ange en fågel-URL för den här sidan, vilket kan ge dig en kortare och/eller mer uttrycksfull URL.

   Om Vanity-URL:en till exempel är inställd `welcome`på den sida som identifieras av sökvägen `/v1.0/startpage`för webbplatsen `http://example.com,` blir `http://example.com/welcome`vanity-URL:en för `http://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >Vanity URL:er:
   >
   >* Måste vara unikt så du bör vara försiktig med att värdet inte redan används av en annan sida.
   >* Använd inte regex-mönster.
   >* Ska inte anges till en befintlig sida.


   Du måste också konfigurera Dispatcher för att kunna få åtkomst till användar-URL:er. Mer information finns i [Aktivera åtkomst till Vanity-URL](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-access-to-vanity-urls-vanity-urls) .

* **URL för omdirigering**

   Anger om du vill att sidan ska använda fågel-URL:en.

### Avancerat {#advanced}

* **Språk:**

   Sidspråket.

* **Språkrot**

   Måste kontrolleras om sidan är roten i en språkkopia.

* **Omdirigering**

   Ange den sida som den här sidan automatiskt ska omdirigeras till.

* **Design**

   Ange vilken [design](/help/sites-developing/designer.md) som ska användas för den här sidan.

* **Alias**

   Ange ett alias som ska användas med den här sidan.

   >[!NOTE]
   >
   >Alias anger egenskapen för att definiera ett aliasnamn för resursen (detta påverkar bara resursen, inte sökvägen). `sling:alias`
   >
   >Till exempel: om du definierar ett alias för `latin-lang` noden `/content/we-retail/spanish` kan du komma åt den här sidan via `/content/we-retail/latin-language`
   >
   >Mer information finns i [Lokaliserade sidnamn under SEO och Bästa praxis](/help/managing/seo-and-url-management.md#localized-page-names)för URL-hantering.

* **Ärvs från &lt;*path*>**

   Anger om sidan ärvs. och varifrån kommer.

* **Molnkonfiguration**

   Sökvägen till konfigurationen.

* **Tillåtna mallar**

   [Definiera listan med mallar som ska vara tillgängliga](/help/sites-authoring/templates.md#allowingatemplate) i den här undergrenen.

* **Aktivera** (autentiseringskrav)

   Aktivera (eller inaktivera) autentisering för att få åtkomst till sidan.

   >[!NOTE]
   >
   >Stängda användargrupper för sidan definieras på fliken **[Behörigheter](/help/sites-authoring/editing-page-properties.md#permissions)**.

   >[!CAUTION]
   >
   >På fliken **[Behörigheter](/help/sites-authoring/editing-page-properties.md#main-pars-procedure-949394300)**kan du redigera CUG-konfigurationer baserat på förekomsten av`granite:AuthenticationRequired`mixin. Om sidbehörigheter konfigureras med inaktuella CUG-konfigurationer, baserat på närvaro av`cq:cugEnabled`egenskap, visas ett varningsmeddelande under **Autentiseringskrav**och alternativet går inte att redigera och[behörigheterna](/help/sites-authoring/editing-page-properties.md#permissions)går inte heller att redigera.
   >
   >
   >I så fall måste CUG-behörigheterna redigeras i det [klassiska användargränssnittet](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

* **Inloggningssida**

   Den sida som ska användas för inloggning.

* **Exportera konfiguration**

   Ange en exportkonfiguration.

### Miniatyrbild {#thumbnail}

Visar sidminiatyrbilden. Du kan:

* **Generera förhandsgranskning**

   Generera en förhandsgranskning av sidan som ska användas som miniatyrbild.

* **Överför bild**

   Överför en bild som ska användas som miniatyrbild.

* **Välj bild**

   Välj en befintlig resurs som du vill använda som miniatyrbild.

* **Återställ**

   Det här alternativet blir tillgängligt när du har ändrat miniatyrbilden. Om du inte vill behålla ändringen kan du återställa den innan du sparar.

### Sociala medier {#social-media}

* **Delning i sociala medier**

   Definierar de delningsalternativ som är tillgängliga på sidan. Visar de alternativ som är tillgängliga för kärnkomponenten [](https://helpx.adobe.com/experience-manager/core-components/using/sharing.html)Delning.

   * **Aktivera användardelning för Facebook**
   * **Aktivera användardelning för Pinterest**
   * **Önskad XF-variation** Definiera variant av upplevelsefragment som används för att generera metadata för sidan

### Molntjänster {#cloud-services}

* **Molntjänster**

   Definiera egenskaper för [molntjänster](/help/sites-developing/extending-cloud-config.md).

### Personalisering {#personalization}

* **ContextHub-konfigurationer**

   Välj [ContextHub Configuration](/help/sites-administering/contexthub-config.md) and [Segments Path](/help/sites-administering/segmentation.md).

* **Målkonfiguration**

   Välj ett [varumärke om du vill ange ett omfång för målgruppsanpassning](/help/sites-authoring/target-adobe-campaign.md).

### Permissions {#permissions}

* **Behörigheter**

   På den här fliken kan du:

   * [Lägg till behörigheter](/help/sites-administering/user-group-ac-admin.md)
   * [Redigera stängd användargrupp](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)

   * Visa [gällande behörigheter](/help/sites-administering/user-group-ac-admin.md)
   >[!CAUTION]
   >
   >På fliken **Behörigheter** kan du redigera CUG-konfigurationer baserat på förekomsten av `granite:AuthenticationRequired` mixin. Om sidbehörigheter konfigureras med inaktuella CUG-konfigurationer, baserat på närvaro av `cq:cugEnabled` egenskap, visas ett varningsmeddelande och CUG-behörigheterna kan inte redigeras. Autentiseringskravet på fliken [Avancerat](/help/sites-authoring/editing-page-properties.md#advanced) kan inte heller redigeras.
   >
   >
   >I så fall måste CUG-behörigheterna redigeras i det [klassiska användargränssnittet](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

   >[!NOTE]
   >
   >På fliken Behörigheter går det inte att skapa tomma CUG-grupper, vilket kan vara ett enkelt sätt att neka alla användare åtkomst. För att kunna göra detta måste Utforskaren för CRX användas. Mer information finns i dokumentet [Användare, Gruppering och Behörighetsadministration](/help/sites-administering/user-group-ac-admin.md) .

### Blueprint {#blueprint}

* **Blueprint**

   Definiera egenskaper för en designsida inom hantering [av](/help/sites-administering/msm.md)flera webbplatser. Styr under vilka omständigheter ändringar ska spridas till Live Copy.

### Live Copy {#live-copy}

* **Livecopy**

   Definiera egenskaper för en Live Copy-sida inom hantering [av](/help/sites-administering/msm.md)flera webbplatser. Styr under vilka omständigheter ändringar ska spridas från utkast.

### Webbplatsstruktur {#site-structure}

* Tillhandahåll länkar till sidor som innehåller funktioner för hela webbplatsen, till exempel **Registreringssida** och **Offlinesida**.

## Redigera sidegenskaper {#editing-page-properties-1}

Du kan definiera sidegenskaper:

* Från **webbplatskonsolen** :

   * [Skapa en ny sida](/help/sites-authoring/managing-pages.md#creating-a-new-page) (en deluppsättning av egenskaperna)

   * Klicka eller peka på **Egenskaper**

      * För en enstaka sida
      * För flera sidor (endast en deluppsättning av egenskaperna är tillgängliga för redigering av en masse)

* Från sidredigeraren:

   * Använda **sidinformation** (och sedan **Öppna egenskaper**)

### Från webbplatskonsolen - en sida {#from-the-sites-console-single-page}

Klicka eller tryck på **Egenskaper** för att definiera sidegenskaperna:

1. Använd **webbplatskonsolen** för att navigera till platsen för sidan som du vill visa och redigera egenskaper för.

1. Välj alternativet **Egenskaper** för den önskade sidan med något av följande alternativ:

   * [Snabbåtgärder](/help/sites-authoring/basic-handling.md#quick-actions)
   * [Markeringsläge](/help/sites-authoring/basic-handling.md#selectionmode)
   Sidegenskaperna visas med rätt flikar.

1. Visa eller redigera egenskaperna efter behov.

1. Använd sedan **Spara** för att spara uppdateringarna följt av **Stäng** för att återgå till konsolen.

### När en sida redigeras {#when-editing-a-page}

När du redigerar en sida kan du använda **Sidinformation** för att definiera sidegenskaperna:

1. Öppna sidan som du vill redigera egenskaper för.

1. Välj ikonen **Sidinformation** för att öppna markeringsmenyn:

   ![screen_shot_2018-03-22at095740](assets/screen_shot_2018-03-22at095740.png)

1. Välj **Öppna egenskaper** så öppnas en dialogruta där du kan redigera egenskaperna, sorterade efter lämplig flik. Följande knappar finns också till höger om verktygsfältet:

   * **Avbryt**
   * **Spara och stäng**

1. Spara ändringarna med knappen **Spara och stäng** .

### Från webbplatskonsolen - flera sidor {#from-the-sites-console-multiple-pages}

På **webbplatskonsolen** kan du markera flera sidor och sedan använda **Visa egenskaper** för att visa och/eller redigera sidegenskaperna. Detta kallas massredigering av sidegenskaper.

>[!NOTE]
>
>Det finns även massredigering av egenskaper för Assets. Den är mycket lik, men skiljer sig på några punkter. Mer information finns i [Redigera egenskaper för flera resurser](/help/assets/managing-multiple-assets.md) .
>
>Här finns också [gruppredigeraren](/help/sites-administering/bulk-editor.md)där du kan söka efter innehåll från flera sidor med GQL (Google Query Language) och sedan redigera innehållet direkt i gruppredigeraren innan du sparar ändringarna på originalsidorna.

Du kan välja flera sidor för massredigering på olika sätt, bland annat:

* När du bläddrar i **webbplatskonsolen**
* När du har använt **Sök** för att hitta en uppsättning sidor

![epp-01](assets/epp-01.png)

När du har markerat sidorna och sedan klickat på eller klickat på alternativet **** Egenskaper, visas bulkegenskaperna:

![epp-02](assets/epp-02.png)

Du kan bara redigera sidor som:

* Dela samma resurstyp
* Är inte en del av en livecopy

   * Om någon av sidorna finns i en live-kopia visas ett meddelande när egenskaperna öppnas.

När du har valt Massredigering kan du:

* **Visa**

   När du visar Sidegenskaper för flera sidor kan du se:

   * En lista över de sidor som påverkas

      * Du kan markera/avmarkera vid behov
   * Tabbar

      * På samma sätt som när du visar egenskaper för en enskild sida ordnas egenskaperna under flikar.
   * En deluppsättning med egenskaper

      * Egenskaper som är tillgängliga på alla markerade sidor och som uttryckligen har definierats som tillgängliga för massredigering visas.
      * Om du minskar sidmarkeringen till en sida visas alla egenskaper.
   * Vanliga egenskaper med ett gemensamt värde

      * Endast egenskaper med ett gemensamt värde visas i visningsläget.
      * När fältet har flera värden (till exempel Taggar) visas värden bara när *alla* är gemensamma. Om bara vissa är vanliga visas de bara när du redigerar.
   När det inte finns några egenskaper med ett gemensamt värde visas ett meddelande.

* **Redigera**

   När du redigerar Sidegenskaper för flera sidor:

   * Du kan uppdatera värdena i de tillgängliga fälten.

      * De nya värdena tillämpas på alla markerade sidor när du väljer **Klar**.
      * När fältet har flera värden (till exempel Taggar) kan du antingen lägga till ett nytt värde eller ta bort ett gemensamt värde.
   * Fält som är gemensamma, men har olika värden på de olika sidorna, markeras med ett särskilt värde, t.ex. texten `<Mixed Entries>`. Du bör vara försiktig när du redigerar sådana fält för att förhindra dataförlust.


>[!NOTE]
>
>Sidkomponenten kan konfigureras för att ange de fält som är tillgängliga för massredigering. Se [Konfigurera sidan för massredigering av sidegenskaper](/help/sites-developing/bulk-editing.md).
