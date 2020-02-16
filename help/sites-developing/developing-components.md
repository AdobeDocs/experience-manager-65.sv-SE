---
title: Utveckla AEM-komponenter
seo-title: Utveckla AEM-komponenter
description: AEM-komponenter används för att lagra, formatera och återge innehåll som är tillgängligt på dina webbsidor.
seo-description: AEM-komponenter används för att lagra, formatera och återge innehåll som är tillgängligt på dina webbsidor.
uuid: 1f39daa6-7277-45a2-adcc-74b58c93b8e4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 8cdb6db4-adaa-4eda-af7d-310a0b44b80b
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Utveckla AEM-komponenter{#developing-aem-components}

AEM-komponenter används för att lagra, formatera och återge innehåll som är tillgängligt på dina webbsidor.

* När du [redigerar sidor](/help/sites-authoring/default-components.md)tillåter komponenterna författarna att redigera och konfigurera innehållet.

   * När du skapar en [Commerce](/help/sites-administering/ecommerce.md) -plats kan komponenterna till exempel samla in och återge information från katalogen.
Mer information finns i [Utveckla e-handel](/help/sites-developing/ecommerce.md) .

   * När du skapar en [Communities](/help/communities/author-communities.md) -webbplats kan komponenterna tillhandahålla information till och samla in information från era besökare.
Mer information finns i [Utveckla användargrupper](/help/communities/communities.md) .

* I publiceringsinstansen återger komponenterna ditt innehåll och presenterar det som du vill för webbplatsens besökare.

>[!NOTE]
>
>Den här sidan är en fortsättning på dokumentet [AEM Components - The Basics](/help/sites-developing/components-basics.md).

>[!CAUTION]
>
>Komponenter nedan `/libs/cq/gui/components/authoring/dialog` är avsedda att endast användas i redigeraren (komponentdialogrutor i redigering). Om de används någon annanstans (t.ex. i en guidedialogruta) kanske de inte fungerar som förväntat.

## Kodexempel {#code-samples}

Den här sidan innehåller referensdokumentation (eller länkar till referensdokumentation) som krävs för att utveckla nya komponenter för AEM. Se [Utveckla AEM-komponenter - Kodexempel](/help/sites-developing/developing-components-samples.md) för några praktiska exempel.

## Struktur {#structure}

En komponents grundläggande struktur beskrivs på sidan [AEM Components - The Basics](/help/sites-developing/components-basics.md#structure). Dokumentet omfattar både pekaktiverade och klassiska användargränssnitt. Även om du inte behöver använda de klassiska inställningarna i den nya komponenten kan det vara bra att känna till dem när du ärver från befintliga komponenter.

## Utöka befintliga komponenter och dialogrutor {#extending-existing-components-and-dialogs}

Beroende på vilken komponent du vill implementera kan det vara möjligt att utöka eller anpassa en befintlig instans i stället för att definiera och utveckla hela [strukturen](#structure) från början.

När du utökar eller anpassar en befintlig komponent eller dialogruta kan du kopiera eller replikera antingen hela strukturen eller den struktur som krävs för dialogrutan innan du gör ändringarna.

### Utöka en befintlig komponent {#extending-an-existing-component}

Du kan utöka en befintlig komponent med [Resurstypshierarki](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) och relaterade arvsmekanismer.

>[!NOTE]
>
>Komponenter kan också definieras om med en övertäckning som baseras på sökvägslogiken. I så fall aktiveras inte [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) och `/apps` hela övertäckningen måste definieras.

>[!NOTE]
>
>Komponenten [för](/help/sites-developing/customizing-content-fragments.md) innehållsfragment kan också anpassas och utökas, men den fullständiga strukturen och relationerna med Assets måste beaktas.

### Anpassa en befintlig komponentdialogruta {#customizing-a-existing-component-dialog}

Det går också att åsidosätta en *komponentdialogruta* med [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) och definiera egenskapen `sling:resourceSuperType`.

Det innebär att du bara behöver definiera om skillnaderna, i stället för att definiera om hela dialogrutan (med `sling:resourceSuperType`). Den här metoden rekommenderas nu för att utöka en komponentdialogruta

Mer information finns i [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) .

## Definiera markeringen {#defining-the-markup}

Komponenten återges med [HTML](https://www.w3schools.com/htmL/html_intro.asp). Komponenten måste definiera den HTML som behövs för att ta det önskade innehållet och sedan återge det som det behövs, både i författarmiljön och i publiceringsmiljön.

### Använda HTML-mallspråket {#using-the-html-template-language}

HTML- [mallspråket (HTL)](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html), som introducerades med AEM 6.0, ersätter JSP (JavaServer Pages) som det rekommenderade serversidesmallsystemet för HTML. För webbutvecklare som behöver bygga robusta företagswebbplatser kan HTML bidra till ökad säkerhet och effektivare utveckling.

>[!NOTE]
>
>Även om både HTML och JSP kan användas för att utveckla komponenter illustrerar vi utvecklingen med HTML på den här sidan, eftersom det är det rekommenderade skriptspråket för AEM.

## Utveckla innehållslogiken {#developing-the-content-logic}

Denna valfria logik markerar och/eller beräknar innehållet som ska återges. Den anropas från HTML-uttryck med rätt Use-API-mönster.

Mekanismen för att skilja logik från utseende gör det lättare att klargöra vad som krävs för en viss vy. Det möjliggör också olika logik för olika vyer av samma resurs.

### Använda Java {#using-java}

[Med HTL Java Use-API:t kan en HTML-fil få åtkomst till hjälpmetoder i en anpassad Java-klass](https://helpx.adobe.com/experience-manager/htl/using/use-api-java.html). På så sätt kan du använda Java-kod för att implementera logiken för att välja och konfigurera komponentinnehållet.

### Använda JavaScript {#using-javascript}

[Använd-API:t för HTML JavaScript gör att en HTML-fil kan få åtkomst till hjälpkod som skrivits i JavaScript](https://helpx.adobe.com/experience-manager/htl/using/use-api-javascript.html). På så sätt kan du använda JavaScript-kod för att implementera logiken för att välja och konfigurera komponentinnehållet.

### Använda HTML-bibliotek på klientsidan {#using-client-side-html-libraries}

Moderna webbplatser är starkt beroende av bearbetning på klientsidan som styrs av komplex JavaScript- och CSS-kod. Det kan vara komplicerat att organisera och optimera serveringen av koden.

För att underlätta hanteringen av det här problemet tillhandahåller AEM biblioteksmappar **på** klientsidan, som gör att du kan lagra koden på klientsidan i databasen, ordna den i kategorier och definiera när och hur varje kodkategori ska skickas till klienten. Klientsidans bibliotekssystem tar sedan hand om att skapa rätt länkar på den slutliga webbsidan för att läsa in rätt kod.

Läs [Använda HTML-bibliotek](/help/sites-developing/clientlibs.md) på klientsidan om du vill ha mer information.

## Konfigurera redigeringsbeteendet {#configuring-the-edit-behavior}

Du kan konfigurera redigeringsbeteendet för en komponent, inklusive attribut som åtgärder som är tillgängliga för komponenten, egenskaper för redigeraren och avlyssnare som är relaterade till händelser för komponenten. Konfigurationen är gemensam för det beröringsaktiverade och klassiska användargränssnittet, men med vissa specifika skillnader.

En komponents [redigeringsbeteende konfigureras](/help/sites-developing/components-basics.md#edit-behavior) genom att lägga till en `cq:editConfig` nod av typen `cq:EditConfig` nedanför komponentnoden (av typen `cq:Component`) och genom att lägga till specifika egenskaper och underordnade noder.

## Konfigurera förhandsvisningsbeteendet {#configuring-the-preview-behavior}

Cookien för [WCM-läge](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) anges när du växlar till **förhandsgranskningsläget** även när sidan inte uppdateras.

Komponenter med en återgivning som är känslig för WCM-läget måste definieras så att de uppdateras specifikt och sedan baseras på värdet för cookien.

>[!NOTE]
>
>I det pekaktiverade användargränssnittet används endast värdena `EDIT` och `PREVIEW` för [WCM-lägets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) cookie.

## Skapa och konfigurera en dialogruta {#creating-and-configuring-a-dialog}

I dialogrutor kan författaren interagera med komponenten. Med hjälp av en dialogruta kan författare och/eller administratörer redigera innehåll, konfigurera komponenten eller definiera designparametrar (med hjälp av en [designdialogruta](#creating-and-configuring-a-design-dialog))

### Gränssnittet för korall och GRENITE {#coral-ui-and-granite-ui}

[Gränssnittet Coral](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) och [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) definierar det moderna utseendet på AEM.

[Granite-gränssnittet innehåller ett stort urval av de grundläggande komponenter (widgetar)](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) som behövs för att skapa en dialogruta i redigeringsmiljön. Vid behov kan du utöka den här markeringen och [skapa en egen widget](#creatinganewwidget).

Mer information om hur du utvecklar komponenter med resurstyperna Koral och Granite finns i: [Skapa Experience Manager-komponenter med resurstyperna](https://helpx.adobe.com/experience-manager/using/aem64_coral_resourcetypes.html)Coral/Granite.

Mer information finns i:

* Coral UI

   * Ett enhetligt gränssnitt för alla molnlösningar
   * [AEM Touch-aktiverat användargränssnitt - Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Användargränssnittshandbok för Coral](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html)

* Granite-gränssnitt

   * Innehåller Coral UI-kod inkapslad i Sling-komponenter för att bygga UI-konsoler och dialogrutor
   * [AEM Touch-aktiverat användargränssnitt - Granite-gränssnitt](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Bevilja gränssnittsdokumentation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)

>[!NOTE]
>
>På grund av typen av GREND-komponenter (och skillnader i ExtJS-widgetar) finns det vissa skillnader mellan hur komponenterna interagerar med det beröringsaktiverade gränssnittet och det [klassiska gränssnittet](/help/sites-developing/developing-components-classic.md).

### Skapa en ny dialogruta {#creating-a-new-dialog}

Dialogrutor för det beröringskänsliga användargränssnittet:

* har namn `cq:dialog`.
* definieras som en `nt:unstructured` nod med `sling:resourceType` egenskapsuppsättningen.

* finns under deras `cq:Component` nod och bredvid deras komponentdefinition.
* återges på serversidan (som Sling-komponenter), baserat på deras innehållsstruktur och `sling:resourceType` egenskap.
* använda GRI-ramverket för Granite.
* innehåller en nodstruktur som beskriver fälten i dialogrutan.

   * dessa noder har `nt:unstructured` den obligatoriska `sling:resourceType` egenskapen.

En exempelnodstruktur kan vara:

```xml
newComponent (cq:Component)
  cq:dialog (nt:unstructured)
    content
      layout
      items
        column
          items
            file
            description
```

Att anpassa en dialogruta liknar att utveckla en komponent eftersom dialogrutan i sig är en komponent (d.v.s. markering som återges av ett komponentskript tillsammans med beteende/stil som tillhandahålls av ett klientbibliotek).

Se till exempel:

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>Om en komponent inte har någon dialogruta definierad för det beröringsaktiverade användargränssnittet, används den klassiska användargränssnittsdialogrutan som reserv i ett kompatibilitetslager. Om du vill anpassa en sådan dialogruta måste du anpassa den klassiska användargränssnittsdialogrutan. Se [AEM-komponenter för det klassiska användargränssnittet](/help/sites-developing/developing-components-classic.md).

### Anpassa dialogrutefält {#customizing-dialog-fields}

>[!NOTE]
>
>Se:
>
>* AEM Gems-sessionen om [anpassning av dialogrutefält](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html).
>* Den relaterade exempelkoden som beskrivs i [Kodexempel - Anpassa dialogrutefält](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields).
>



#### Skapa ett nytt fält {#creating-a-new-field}

Widgetar för det beröringsaktiverade användargränssnittet implementeras som GRE-komponenter.

Om du vill skapa en ny widget som ska användas i en komponentdialogruta för det beröringsaktiverade användargränssnittet måste du [skapa en ny granitfältskomponent](/help/sites-developing/granite-ui-component.md).

>[!NOTE]
>
>Fullständig information om GRI-gränssnittet för Granite finns i dokumentationen [för](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)GRI.

Om du ser dialogrutan som en enkel behållare för ett formulärelement kan du även se det primära innehållet i dialogrutan som formulärfält. Om du skapar ett nytt formulärfält måste du skapa en resurstyp; motsvarar att skapa en ny komponent. För att du ska få hjälp med den här uppgiften erbjuder Granite-gränssnittet en generisk fältkomponent att ärva från (med `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

Mer specifikt ger GRE UI ett antal fältkomponenter som är lämpliga att använda i dialogrutor (eller mer allmänt i [formulär](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)).

>[!NOTE]
>
>Detta skiljer sig från det klassiska användargränssnittet, där widgetar representeras av `cq:Widgets` noder, där var och en har en särskild funktion `xtype` för att etablera relationen med sin motsvarande ExtJS-widget. Från en implementeringssynvinkel renderades dessa widgetar på klientsidan av ExtJS-ramverket.

När du har skapat resurstypen kan du instansiera fältet genom att lägga till en ny nod i dialogrutan, där egenskapen refererar `sling:resourceType` till resurstypen som du just introducerat.

#### Skapa ett klientbibliotek för stil och beteende {#creating-a-client-library-for-style-and-behavior}

Om du vill definiera format och beteende för komponenten kan du skapa ett dedikerat [klientbibliotek](/help/sites-developing/clientlibs.md) som definierar din anpassade CSS/LESS och JS.

Om du vill att klientbiblioteket endast ska läsas in för komponentdialogrutan (d.v.s. inte ska läsas in för en annan komponent) måste du ställa in egenskapen `extraClientlibs`** **i dialogrutan till kategorinamnet för det klientbibliotek som du just har skapat. Detta rekommenderas om klientbiblioteket är stort och/eller om fältet är specifikt för den dialogrutan och inte behövs i andra dialogrutor.

Om du vill att klientbiblioteket ska läsas in för alla dialogrutor anger du kategoriegenskapen för klientbiblioteket till `cq.authoring.dialog`. Det här är kategorinamnet för klientbiblioteket som inkluderas som standard när alla dialogrutor återges. Du vill göra det om klientbiblioteket är litet och/eller fältet är generiskt och kan återanvändas i andra dialogrutor.

Se följande exempel:

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * anges i [kodexempel](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Utöka (ärva från) ett fält {#extending-inheriting-from-a-field}

Beroende på dina behov kan du antingen:

* Utöka ett visst GRE-fält efter komponentarv ( `sling:resourceSuperType`)
* Utöka en given widget från det underliggande widgetbiblioteket (för Granite-gränssnittet är det korallgränssnitt) genom att följa widgetens biblioteks-API (JS/CSS-arv)

#### Åtkomst till dialogrutefält {#access-to-dialog-fields}

Du kan också använda återgivningsvillkor ( `rendercondition`) för att styra vem som har åtkomst till specifika flikar/fält i dialogrutan. till exempel:

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### Hantera fälthändelser {#handling-field-events}

Metoden för att hantera händelser i dialogrutefält görs nu med [avlyssnare i ett anpassat klientbibliotek](#listeners-in-a-custom-client-library). Detta är en ändring från den äldre metoden att ha [avlyssnare i innehållsstrukturen](#listenersinthecontentstructureclassicui).

#### Lyssnare i ett anpassat klientbibliotek {#listeners-in-a-custom-client-library}

För att lägga in logik i fältet bör du:

1. Låt fältet vara markerat med en viss CSS-klass ( *kroken*).
1. I klientbiblioteket definierar du en JS-avlyssnare som är kopplad till det CSS-klassnamnet (detta garanterar att din anpassade logik endast omfattar fältet och inte påverkar andra fält av samma typ).

För att uppnå detta måste du känna till det underliggande widgetbiblioteket som du vill interagera med. Se dokumentationen [för](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) Coral UI för att se vilka händelser du vill reagera på. Detta liknar den process du tidigare använde för att utföra ExtJS: hitta dokumentationssidan för en viss widget och kontrollera sedan informationen om dess händelse-API.

Se följande exempel:

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * anges i [kodexempel](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Lyssnare i innehållsstrukturen {#listeners-in-the-content-structure}

I det klassiska användargränssnittet med ExtJS var det vanligt att ha avlyssnare för en viss widget i innehållsstrukturen. Att uppnå samma sak i det beröringskänsliga användargränssnittet skiljer sig från JS-avlyssnarkoden (eller vilken kod som helst) som inte längre är definierad i innehållet.

Innehållsstrukturen beskriver den semantiska strukturen. det ska (måste) inte antyda den underliggande widgetens karaktär. Genom att inte ha JS-kod i innehållsstrukturen kan du ändra implementeringsinformationen utan att behöva ändra innehållsstrukturen. Du kan med andra ord ändra widgetbiblioteket utan att behöva ändra innehållsstrukturen.

### Fältvalidering {#field-validation}

#### Obligatoriskt fält {#mandatory-field}

Om du vill markera ett givet fält som obligatoriskt anger du följande egenskap på innehållsnoden i fältet:

* Namn: `required`
* Typ: `Boolean`

Se följande exempel:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### Fältvalidering (GRÄNSSNITT) {#field-validation-granite-ui}

Fältvalidering i GRA-gränssnittet och GRA-gränssnittskomponenterna (motsvarar widgetar) görs med hjälp av `foundation-validation` API:t. [Mer information finns i dokumentationen för `foundation-valdiation` Granite.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

Se till exempel:

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * anges i [kodexempel](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## Skapa och konfigurera en designdialogruta {#creating-and-configuring-a-design-dialog}

Dialogrutan Design visas när en komponent har designdetaljer som kan redigeras i [designläge](/help/sites-authoring/default-components-designmode.md).

Definitionen liknar den i en [dialogruta som används för att redigera innehåll](#creating-a-new-dialog), men skillnaden är att den är definierad som en nod:

* Nodnamn: `cq:design_dialog`
* Typ: `nt:unstructured`

## Skapa och konfigurera en Inplace-redigerare {#creating-and-configuring-an-inplace-editor}

Med en infogningsredigerare kan användaren redigera innehåll direkt i styckeflödet utan att behöva öppna en dialogruta. Standardkomponenterna Text och Title har till exempel båda en infogad redigerare.

En infogningsredigerare är inte nödvändig/meningsfull för varje komponenttyp.

Mer information finns i [Utöka sidredigering - Lägg till ny infogningsredigerare](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor) .

## Anpassa komponentverktygsfältet {#customizing-the-component-toolbar}

Med [komponentverktygsfältet](/help/sites-developing/touch-ui-structure.md#component-toolbar) får användaren tillgång till en rad åtgärder för komponenten, som redigering, konfigurering, kopiering och borttagning.

Mer information finns i [Utöka sidredigering - Lägg till ny åtgärd i ett komponentverktygsfält](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) .

## Konfigurera en komponent för referenslinjen (lånad/lånad) {#configuring-a-component-for-the-references-rail-borrowed-lent}

Om den nya komponenten refererar till innehåll från andra sidor kan du överväga om du vill att den ska påverka avsnitten **Lånat innehåll** och **Lånat innehåll** i [**Reference **](/help/sites-authoring/basic-handling.md#references)Rail.

Körklar AEM-kontroll kontrollerar bara Reference-komponenten. Om du vill lägga till din komponent måste du konfigurera OSGi-paketet med **WCM-redigeringsreferenskonfiguration**.

Skapa en ny post i definitionen som anger komponenten tillsammans med den egenskap som ska kontrolleras. Exempel:

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>När du arbetar med AEM finns det flera metoder för att hantera konfigurationsinställningarna för sådana tjänster. Mer information och rekommenderade metoder finns i [Konfigurera OSGi](/help/sites-deploying/configuring-osgi.md) .

## Aktivera och lägga till komponenten i styckesystemet {#enabling-and-adding-your-component-to-the-paragraph-system}

När komponenten har utvecklats måste den aktiveras för användning i ett lämpligt styckesystem, så att den kan användas på de sidor som krävs.

Detta kan göras antingen genom att:

* i [designläge](/help/sites-authoring/default-components-designmode.md) när du redigerar en viss sida.
* [definiera `components` egenskapen i en malls](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system)styckesystem.

## Konfigurera ett styckesystem så att en komponentinstans skapas när en resurs dras {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

Med AEM kan du konfigurera ett styckesystem på sidan så att [en instans av den nya komponenten skapas automatiskt när en användare drar en (lämplig) resurs till en instans av sidan](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) (i stället för att alltid behöva dra en tom komponent till sidan).

Detta beteende och den nödvändiga relationen mellan resurser och komponenter kan konfigureras:

1. Under styckedefinitionen för siddesignen. Exempel:

   * `/etc/designs/<myApp>/page/par`
   Skapa en ny nod:

   * Namn: `cq:authoring`
   * Typ: `nt:unstructured`


1. Skapa en ny nod under detta för att innehålla alla mappningar av resurs-till-komponent:

   * Namn: `assetToComponentMapping`
   * Typ: `nt:unstructured`

1. Skapa en nod för varje resurs-till-komponent-mappning:

   * Namn: text, Det rekommenderas att namnet anger tillgången och den relaterade komponenttypen. till exempel bild
   * Typ: `nt:unstructured`
   Var och en med följande egenskaper:

   * `assetGroup`:

      * Typ: `String`
      * Värde: den grupp som den relaterade tillgången tillhör,
till exempel `media`
   * `assetMimetype`:

      * Typ: `String`
      * Värde: Mime-typen för den relaterade tillgången. till exempel `image/*`
   * `droptarget`:

      * Typ: `String`
      * Värde: släppmålet,
till exempel `image`
   * `resourceType`:

      * Typ: `String`
      * Värde: den tillhörande komponentresursen,
till exempel `foundation/components/image`
   * `type`:

      * Typ: `String`
      * Värde: typen, till exempel `Images`






Exempel:

* `/etc/designs/geometrixx/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-outdoors/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-media/jcr:content/article/article-content-par/cq:authoring`

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna aem-project-archietype-projekt på GitHub](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>Det automatiska skapandet av komponentinstanser kan nu enkelt konfigureras i användargränssnittet när du använder [kärnkomponenter](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) och redigerbara mallar. Mer information om hur du definierar vilka komponenter som automatiskt kopplas till de angivna medietyperna finns i [Skapa sidmallar](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) .

## Använda AEM Brackets Extension {#using-the-aem-brackets-extension}

Tillägget [](/help/sites-developing/aem-brackets.md) AEM Brackets ger ett smidigt arbetsflöde för redigering av AEM-komponenter och klientbibliotek. Den baseras på [Brackets](https://brackets.io/) kodredigerare.

Tillägget:

* Förenklar synkronisering (ingen Maven eller filvalv krävs) för att öka utvecklarens effektivitet och även hjälpa gränssnittsutvecklare med begränsade AEM-kunskaper att delta i projekt.
* Har stöd för [HTML](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) , mallspråket som är utformat för att förenkla komponentutvecklingen och öka säkerheten.

>[!NOTE]
>
>Hakparenteser är den rekommenderade mekanismen för att skapa komponenter. Den ersätter funktionen CRXDE Lite - Create Component, som är utformad för det klassiska användargränssnittet.

## Migrera från en klassisk komponent {#migrating-from-a-classic-component}

När du migrerar en komponent som har utformats för användning med det klassiska användargränssnittet till en komponent som kan användas med det beröringsaktiverade användargränssnittet (antingen enbart eller tillsammans) bör du tänka på följande:

* HTL

   * Det är inte obligatoriskt att använda [HTML](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) , men om komponenten behöver uppdateras är det ett bra tillfälle att överväga att [migrera från JSP till HTML](/help/sites-developing/components-basics.md#htl-vs-jsp).

* Komponenter

   * Migrera [`cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) kod som använder klassiska gränssnittsspecifika funktioner
   * RTE-plugin, mer information finns i [Konfigurera RTF-redigeraren](/help/sites-administering/rich-text-editor.md).
   * [Migrera `cq:listener` kod](#migrating-cq-listener-code) som använder funktioner som är specifika för det klassiska användargränssnittet

* Dialogrutor

   * Du måste skapa en ny dialogruta för användning i det beröringsaktiverade användargränssnittet. Av kompatibilitetsskäl kan emellertid det beröringsaktiverade användargränssnittet använda definitionen för en klassisk användargränssnittsdialogruta när ingen dialogruta har definierats för det beröringsaktiverade användargränssnittet.
   * Verktyget [för](/help/sites-developing/dialog-conversion.md) dialogkonvertering är till för att du ska kunna utöka befintliga komponenter.
   * [Genom att mappa ExtJS till Granite UI-komponenter](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) får du en bekväm översikt över ExtJS-xtyper och nodtyper med motsvarande Granite UI-resurstyper.
   * Mer information om hur du anpassar fält finns i AEM Gems-sessionen om [anpassning av dialogrutefält](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html).
   * Migrera från vtypes till [Granite-gränssnittsvalidering](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * Mer information om hur du använder JS-avlyssnare finns i [Hantera fälthändelser](#handling-field-events) och AEM Gems-sessionen om [anpassning av dialogrutefält](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html).

### Migrera cq:avlyssnarkod {#migrating-cq-listener-code}

Om du migrerar ett projekt som har utformats för det klassiska användargränssnittet kan det hända att `cq:listener` funktioner som är specifika för det klassiska användargränssnittet (t.ex. `CQ.wcm.*`) används i koden (och komponentrelaterade klienter). För migreringen måste du uppdatera sådan kod med motsvarande objekt/funktioner i det beröringsaktiverade användargränssnittet.

Om ditt projekt ska migreras helt till det beröringskänsliga användargränssnittet måste du ersätta den koden för att använda de objekt och funktioner som är relevanta för det beröringskänsliga användargränssnittet.

Om ditt projekt måste tillgodose både det klassiska användargränssnittet och det beröringsaktiverade användargränssnittet under migreringsperioden (det vanliga scenariot) måste du implementera en switch för att särskilja den separata koden som refererar till lämpliga objekt.

Den här switchmekanismen kan implementeras som:

```
if (Granite.author) {
    // touch UI
} else {
    // classic UI
}
```

## Dokumentera komponenten {#documenting-your-component}

Som utvecklare vill du ha enkel åtkomst till komponentdokumentation så att du snabbt kan förstå:

* Beskrivning
* Avsedd användning
* Innehållsstruktur och egenskaper
* Exponerade API:er och tilläggspunkter
* osv.

Därför är det ganska enkelt att göra befintliga dokumentationsmarkeringar tillgängliga i själva komponenten.

Allt du behöver göra är att placera en `README.md` fil i komponentstrukturen. Den här markeringen visas sedan i [komponentkonsolen](/help/sites-authoring/default-components-console.md).

![chlimage_1-7](assets/chlimage_1-7.png)

Den kod som stöds är densamma som för [innehållsfragment](/help/assets/content-fragments-markdown.md).
