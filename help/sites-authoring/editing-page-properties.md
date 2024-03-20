---
title: Redigera egenskaper för innehållssidor
description: Definiera de egenskaper som krävs för en sida i Adobe Experience Manager.
exl-id: 3cd9374f-6f16-40fb-97cf-5f9a750b8dd2
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1855'
ht-degree: 1%

---

# Redigera sidegenskaper{#editing-page-properties}

Du kan definiera de egenskaper som krävs för en sida. Dessa kan variera beroende på sidans beskaffenhet. Vissa sidor kan t.ex. vara kopplade till en live-kopia medan andra inte är det och live-kopieringsinformationen blir tillgänglig om det är lämpligt.

## Sidegenskaper {#page-properties}

Egenskaperna fördelas på flera flikar.

### Grundläggande {#basic}

* **Titel**

  Sidans rubrik visas på olika platser. Till exempel **Webbplatser** tabblista och **Webbplatser** kort-/listvyer.

  Detta är ett obligatoriskt fält.

* **Taggar**

  Här kan du lägga till eller ta bort taggar från sidan genom att uppdatera listan i valrutan:

   * När du har valt en tagg visas den under markeringsrutan. Du kan ta bort en tagg från den här listan med hjälp av x.
   * Du kan ange en ny tagg genom att skriva namnet i en tom markeringsram.

      * Den nya taggen skapas när du trycker på Enter.
      * Den nya taggen visas med en liten stjärna till höger som anger att det är en ny tagg.

   * Med den nedrullningsbara menyn kan du välja bland befintliga taggar.
   * Ett x-tecken visas när du för musen över en taggpost i markeringsrutan, som kan användas för att ta bort taggen för den här sidan.

  Mer information om taggar finns i [Använda taggar](/help/sites-authoring/tags.md).

* **Dölj i navigering**

  Anger om sidan visas eller döljs i sidnavigeringen på den slutliga platsen.

* **Varumärke**

  Använd en enhetlig varumärkesidentitet på alla sidor genom att lägga till en instruktionsmarginal till varje sidrubrik. Den här funktionen kräver att du använder Page Component från version 2.14.0 eller senare av [Kärnkomponenter.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)

   * **Åsidosätt** - Markera för att definiera instruktionsmarginalen för varumärket på den här sidan.
      * Värdet ärvs av alla underordnade sidor såvida de inte också har sina **Åsidosätt** värden har angetts.
   * **Åsidosätt värde** - Texten i instruktionsmarginalen som ska läggas till i sidrubriken.
      * Värdet läggs till i sidrubriken efter ett lodstreck som &quot;Cycling Tuscany&quot; | Alltid redo för WKND&quot;
* **Sidrubrik**

  En rubrik som ska användas på sidan. Används vanligtvis av titelkomponenter. Om den är tom visas **Titel** används.

* **Navigeringsrubrik**

  Du kan ange en separat rubrik som ska användas i navigeringen (om du till exempel vill ha något mer koncist). Om den är tom visas **Titel** används.

* **Underrubrik**

  En underrubrik som ska användas på sidan.

* **Beskrivning**

  Din beskrivning av sidan, dess syfte eller annan information som du vill lägga till.

* **I tid**

  Det datum och den tidpunkt då den publicerade sidan aktiveras. När sidan publiceras förblir den vilande till den angivna tiden.

  Lämna dessa fält tomma för sidor som du vill publicera omedelbart (det normala scenariot).

* **Fråntid**

  Den tidpunkt då den publicerade sidan inaktiveras.

  Lämna dessa fält tomma igen så att du kan agera direkt.

* **Vanity URL**

  Ange en innehålls-URL för den här sidan, vilket kan ge dig en kortare och/eller mer uttrycksfull URL.

  Om Vanity-URL:en till exempel är inställd på `welcome`till den sida som identifieras av sökvägen `/v1.0/startpage`för webbplatsen `http://example.com,` sedan `http://example.com/welcome`skulle vara den vanligaste URL:en för `http://example.com/content/v1.0/startpage`

  >[!CAUTION]
  >
  >Vanity URL:er:
  >
  >* Måste vara unikt. Kontrollera att värdet inte redan används av en annan sida.
  >* Använd inte regex-mönster.
  >* Ska inte anges till en befintlig sida.
  >

  Konfigurera Dispatcher för att aktivera åtkomst till mål-URL:er. Se [Aktivera åtkomst till Vanity-URL:er](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-access-to-vanity-urls-vanity-urls) för mer information.

* **URL för omdirigering av vanity**

  Anger om du vill att sidan ska använda fågel-URL:en.

### Avancerat {#advanced}

* **Språk**

  Sidspråket.

* **Språkrot**

  Måste kontrolleras om sidan är roten i en språkkopia.

* **Omdirigering**

  Ange den sida som den här sidan automatiskt ska omdirigeras till.

* **Design**

  Ange [design](/help/sites-developing/designer.md) som ska användas för den här sidan.

* **Alias**

  Ange ett alias som ska användas med den här sidan.

   * Om du till exempel definierar ett alias för `private` för sidan `/content/wknd/us/en/magazine/members-only`kan den här sidan också öppnas via `/content/wknd/us/en/magazine/private`
   * När du skapar ett alias anges `sling:alias` på sidnoden, vilket bara påverkar resursen, inte databassökvägen.
   * Sidor som används av alias i redigeraren kan inte publiceras. [Publiceringsalternativ](/help/sites-authoring/publishing-pages.md) i redigeraren är bara tillgängliga för sidor som du kommer åt via de faktiska sökvägarna.
   * Mer information finns i [Lokaliserade sidnamn under SEO och URL Management Best Practices](/help/managing/seo-and-url-management.md#localized-page-names).

* **Ärvs från &lt;*bana*>**

  Anger om sidan ärvs. och varifrån kommer.

* **Molnkonfiguration**

  Sökvägen till konfigurationen.

* **Tillåtna mallar**

  [Definiera listan med tillgängliga mallar](/help/sites-authoring/templates.md#allowingatemplate) inom denna underavdelning.

* **Aktivera** (Autentiseringskrav)

  Aktivera (eller inaktivera) användningen av autentisering så att du kan komma åt sidan.

  >[!NOTE]
  >
  >Stängda användargrupper för sidan definieras på **[Behörigheter](/help/sites-authoring/editing-page-properties.md#permissions)** -fliken.

  >[!CAUTION]
  >
  >The **[Behörigheter](/help/sites-authoring/editing-page-properties.md#main-pars-procedure-949394300)** kan du redigera CUG-konfigurationer baserat på närvaron av `granite:AuthenticationRequired` blanda. Om sidbehörigheter konfigureras med hjälp av inaktuella CUG-konfigurationer, baserat på förekomsten av `cq:cugEnabled` egenskap, visas ett varningsmeddelande under **Autentiseringskrav** och alternativet går inte att redigera, och inte heller [Behörigheter](/help/sites-authoring/editing-page-properties.md#permissions) redigerbar.
  >
  >
  >I så fall måste CUG-behörigheterna redigeras i [klassiskt användargränssnitt](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

* **Inloggningssida**

  Den sida som ska användas för inloggning.

* **Exportera konfiguration**

  Ange en exportkonfiguration.

### Miniatyrbild {#thumbnail}

Visar sidminiatyrbilden. Du kan:

* **Generera förhandsgranskning**

  Generera en förhandsvisning av sidan som du vill använda som miniatyrbild.

* **Överför bild**

  Överför en bild som du vill använda som miniatyrbild.

* **Välj bild**

  Välj en befintlig resurs som du vill använda som miniatyrbild.

* **Återställ**

  Det här alternativet blir tillgängligt när du har ändrat miniatyrbilden. Om du inte vill behålla ändringen kan du återställa den innan du sparar.

### Sociala medier {#social-media}

* **Delning i sociala medier**

  Definierar de delningsalternativ som är tillgängliga på sidan. Visar de alternativ som är tillgängliga för [Dela kärnkomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/sharing.html).

   * **Aktivera användardelning för Facebook**
   * **Aktivera användardelning för Pinterest**
   * **Önskad XF-variation**
Definiera Experience Fragment-variation som används för att generera metadata för en sida

### Cloud Service {#cloud-services}

* **Cloud Service**

  Definiera egenskaper för [molntjänster](/help/sites-developing/extending-cloud-config.md).

### Personalisering {#personalization}

* **ContextHub-konfigurationer**

  Välj [KontextHub-konfiguration](/help/sites-developing/ch-configuring.md) och [Segmentsökväg](/help/sites-administering/segmentation.md).

* **Målkonfiguration**

  Välj en [Varumärke som anger ett omfång för målanpassning](/help/sites-authoring/target-adobe-campaign.md).

  >[!NOTE]
  >Det här alternativet kräver att användarkontot finns i `Target Adminstrators`grupp.

### Behörigheter {#permissions}

* **Behörigheter**

  På den här fliken kan du:

   * [Lägg till behörigheter](/help/sites-administering/user-group-ac-admin.md)
   * [Redigera stängd användargrupp](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)

   * Visa [Effektiva behörigheter](/help/sites-administering/user-group-ac-admin.md)

  >[!CAUTION]
  >
  >The **Behörigheter** -fliken tillåter redigering av CUG-konfigurationer baserat på närvaron av `granite:AuthenticationRequired` blanda. Om sidbehörigheter konfigureras med hjälp av inaktuella CUG-konfigurationer, baserat på förekomsten av `cq:cugEnabled` -egenskapen visas ett varningsmeddelande och CUG-behörigheterna kan inte redigeras, inte heller är autentiseringskravet på [Avancerat](/help/sites-authoring/editing-page-properties.md#advanced) går att redigera.
  >
  >
  >I så fall måste CUG-behörigheterna redigeras i [klassiskt användargränssnitt](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

  >[!NOTE]
  >
  >På fliken Behörigheter går det inte att skapa tomma CUG-grupper, vilket kan vara ett enkelt sätt att neka alla användare åtkomst. För att göra detta måste CRX Explorer användas. Se dokumentet [Behörighetsadministration för användare, grupper och åtkomst](/help/sites-administering/user-group-ac-admin.md) för mer information.

### Blueprint {#blueprint}

* **Blueprint**

  Definiera egenskaper för en designsida i [hantering av flera webbplatser](/help/sites-administering/msm.md). Styr under vilka omständigheter ändringar ska spridas till Live Copy.

### Live Copy {#live-copy}

* **Livecopy**

  Definiera egenskaper för en Live Copy-sida i [hantering av flera webbplatser](/help/sites-administering/msm.md). Styr under vilka omständigheter ändringar ska spridas från utkast.

### Webbplatsstruktur {#site-structure}

* Tillhandahålla länkar till sidor som innehåller funktioner för hela webbplatsen, till exempel **Registreringssida**, **Offlinesida**, bland annat.

## Redigera sidegenskaper {#editing-page-properties-1}

Du kan definiera sidegenskaper:

* Från **Webbplatser** konsol:

   * [Skapa en sida](/help/sites-authoring/managing-pages.md#creating-a-new-page) (en delmängd av egenskaperna)

   * Klicka eller peka **Egenskaper**

      * För en enstaka sida
      * För flera sidor (endast en deluppsättning av egenskaperna är tillgängliga för redigering av en masse)

* Från sidredigeraren:

   * Med **Sidinformation** (och sedan **Öppna egenskaper**)

### Från webbplatskonsolen - en sida {#from-the-sites-console-single-page}

Klicka eller peka **Egenskaper** för att definiera sidegenskaperna:

1. Använda **Webbplatser** navigera till platsen för sidan som du vill visa och redigera egenskaper för.

1. Välj **Egenskaper** för den önskade sidan med något av följande:

   * [Snabbåtgärder](/help/sites-authoring/basic-handling.md#quick-actions)
   * [Markeringsläge](/help/sites-authoring/basic-handling.md#selectionmode)

   Sidegenskaperna visas med rätt flikar.

1. Visa eller redigera egenskaperna efter behov.

1. Använd sedan **Spara** för att spara uppdateringar följt av **Stäng** så att du kan gå tillbaka till konsolen.

### När en sida redigeras {#when-editing-a-page}

När du redigerar en sida kan du använda **Sidinformation** för att definiera sidegenskaperna:

1. Öppna sidan som du vill redigera egenskaper för.

1. Välj **Sidinformation** -ikon för att öppna markeringsmenyn:

   ![screen_shot_2018-03-22at095740](assets/screen_shot_2018-03-22at095740.png)

1. Välj **Öppna egenskaper** och en dialogruta öppnas där du kan redigera egenskaperna, sorterade efter lämplig flik. Följande knappar finns också till höger om verktygsfältet:

   * **Avbryt**
   * **Spara och stäng**

1. Använd **Spara och stäng** för att spara ändringarna.

### Från webbplatskonsolen - flera sidor {#from-the-sites-console-multiple-pages}

Från **Webbplatser** konsolen kan du markera flera sidor och sedan använda **Visa egenskaper** för att visa och/eller redigera sidegenskaperna. Detta kallas massredigering av sidegenskaper.

>[!NOTE]
>
>Det finns även massredigering av egenskaper för Assets. Den liknar, men skiljer sig på några punkter. Se [Redigera egenskaper för flera resurser](/help/assets/metadata.md) för mer information.
>
>Det finns också [Massredigerare](/help/sites-administering/bulk-editor.md). Med den här redigeraren kan du söka efter innehåll från flera sidor med hjälp av GQL (Google Query Language) och sedan redigera innehållet direkt med hjälp av gruppredigeraren innan du sparar ändringarna på originalsidorna.

Du kan välja flera sidor för massredigering på olika sätt, bland annat:

* När du bläddrar **Webbplatser** konsol
* Efter användning **Sök** för att hitta en uppsättning sidor

![epp-01](assets/epp-01.png)

När du har markerat sidorna och sedan klickat eller tryckt på **Egenskaper, alternativ**, visas bulkegenskaperna:

![epp-02](assets/epp-02.png)

Du kan bara redigera sidor som:

* Dela samma resurstyp
* Är inte en del av en livecopy

   * Om någon av sidorna finns i en live-kopia visas ett meddelande när egenskaperna öppnas.

När du har valt Massredigering kan du göra följande:

* **Visa**

  När du visar Sidegenskaper för flera sidor kan du se följande:

   * En lista över de sidor som påverkas

      * Du kan markera/avmarkera vid behov

   * Tabbar

      * På samma sätt som när du visar egenskaper för en enskild sida ordnas egenskaperna under flikar.

   * En deluppsättning med egenskaper

      * Egenskaper som är tillgängliga på alla markerade sidor och som uttryckligen har definierats som tillgängliga för massredigering visas.
      * Om du minskar sidmarkeringen till en sida visas alla egenskaper.

   * Vanliga egenskaper med ett gemensamt värde

      * Endast egenskaper med ett gemensamt värde visas i visningsläget.
      * När fältet har flera värden (till exempel Taggar) visas värden bara när *alla* är vanliga. Om bara vissa är vanliga visas de bara vid redigering.

  När det inte finns några egenskaper med ett gemensamt värde visas ett meddelande.

* **Redigera**

  När du redigerar Sidegenskaper för flera sidor:

   * Du kan uppdatera värdena i de tillgängliga fälten.

      * De nya värdena tillämpas på alla markerade sidor när du markerar **Klar**.
      * När fältet har flera värden (till exempel Taggar) kan du antingen lägga till ett nytt värde eller ta bort ett gemensamt värde.

   * Fält som är gemensamma, men har olika värden på de olika sidorna, anges med ett särskilt värde, t.ex. text `<Mixed Entries>`.

>[!NOTE]
>
>Sidkomponenten kan konfigureras för att ange de fält som är tillgängliga för massredigering. Se [Konfigurera sidan för massredigering av sidegenskaper](/help/sites-developing/bulk-editing.md).
