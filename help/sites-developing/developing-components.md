---
title: Utveckla AEM
seo-title: Developing AEM Components
description: AEM används för att lagra, formatera och återge innehåll som är tillgängligt på dina webbsidor.
seo-description: AEM components are used to hold, format, and render the content made available on your webpages.
uuid: 1f39daa6-7277-45a2-adcc-74b58c93b8e4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 8cdb6db4-adaa-4eda-af7d-310a0b44b80b
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
exl-id: 573cdc36-e9c3-4803-9c4e-cebd0cf0a56f
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '3454'
ht-degree: 0%

---

# Utveckla AEM{#developing-aem-components}

AEM används för att lagra, formatera och återge innehåll som är tillgängligt på dina webbsidor.

* När [skapa sidor](/help/sites-authoring/default-components.md)gör komponenterna att författarna kan redigera och konfigurera innehållet.

   * När en [Handel](/help/commerce/cif-classic/administering/ecommerce.md) -plats kan komponenterna till exempel samla in och återge information från katalogen.
Se [Utveckla e-handeln](/help/commerce/cif-classic/developing/ecommerce.md) för mer information.

   * När en [Communities](/help/communities/author-communities.md) sajten som komponenterna kan tillhandahålla information till och samla in information från era besökare.
Se [Utveckla webbgrupper](/help/communities/communities.md) för mer information.

* I publiceringsinstansen återger komponenterna ditt innehåll och presenterar det som du vill för webbplatsens besökare.

>[!NOTE]
>
>Den här sidan är en fortsättning på dokumentet [AEM - Grunderna](/help/sites-developing/components-basics.md).

>[!CAUTION]
>
>Komponenter nedan `/libs/cq/gui/components/authoring/dialog` ska bara användas i redigeraren (komponentdialogrutor i redigeringsverktyget). Om de används någon annanstans (t.ex. i en guidedialogruta) kanske de inte fungerar som förväntat.

## Kodexempel {#code-samples}

Den här sidan innehåller referensdokumentation (eller länkar till referensdokumentation) som krävs för att utveckla nya komponenter för AEM. Se [Utveckla AEM - kodexempel](/help/sites-developing/developing-components-samples.md) för några praktiska exempel.

## Struktur {#structure}

En komponents grundläggande struktur beskrivs på sidan [AEM - Grunderna](/help/sites-developing/components-basics.md#structure). Dokumentet omfattar både pekaktiverade och klassiska användargränssnitt. Även om du inte behöver använda de klassiska inställningarna i den nya komponenten kan det vara bra att känna till dem när du ärver från befintliga komponenter.

## Utöka befintliga komponenter och dialogrutor {#extending-existing-components-and-dialogs}

Beroende på vilken komponent du vill implementera kan det vara möjligt att utöka eller anpassa en befintlig instans i stället för att definiera och utveckla hela [struktur](#structure) från scratch.

När du utökar eller anpassar en befintlig komponent eller dialogruta kan du kopiera eller replikera antingen hela strukturen eller den struktur som krävs för dialogrutan innan du gör ändringarna.

### Utöka en befintlig komponent {#extending-an-existing-component}

Du kan utöka en befintlig komponent med [Hierarki för resurstyp](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) och tillhörande arvsmekanismer.

>[!NOTE]
>
>Komponenter kan också definieras om med en övertäckning som baseras på sökvägslogiken. I sådana fall gäller dock att [Samla resurser](/help/sites-developing/sling-resource-merger.md) aktiveras inte och `/apps` måste definiera hela övertäckningen.

>[!NOTE]
>
>The [komponent för innehållsfragment](/help/sites-developing/customizing-content-fragments.md) kan också anpassas och utökas, men hela strukturen och relationerna med Assets måste beaktas.

### Anpassa en befintlig komponentdialogruta {#customizing-a-existing-component-dialog}

Du kan även åsidosätta en *komponentdialogruta* med [Samla resurser](/help/sites-developing/sling-resource-merger.md) och definiera egenskapen `sling:resourceSuperType`.

Det innebär att du bara behöver definiera om skillnaderna, i stället för att definiera om hela dialogrutan (med `sling:resourceSuperType`). Den här metoden rekommenderas nu för att utöka en komponentdialogruta

Se [Samla resurser](/help/sites-developing/sling-resource-merger.md) för mer information.

## Definiera markeringen {#defining-the-markup}

Komponenten återges med [HTML](https://www.w3schools.com/htmL/html_intro.asp). Komponenten måste definiera den HTML som behövs för att ta det önskade innehållet och sedan återge det som det behövs, både i författarmiljön och i publiceringsmiljön.

### Använda mallspråket HTML {#using-the-html-template-language}

The [HTML (HTML Templating Language)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html), som introducerades med AEM 6.0, ersätter JSP (JavaServer Pages) som det rekommenderade serversidesmallsystemet för HTML. För webbutvecklare som behöver bygga robusta företagswebbplatser kan HTML bidra till ökad säkerhet och effektivare utveckling.

>[!NOTE]
>
>Även om både HTML och JSP kan användas för att utveckla komponenter illustrerar vi utvecklingen med HTML på den här sidan, eftersom det är det rekommenderade skriptspråket för AEM.

## Utveckla innehållslogiken {#developing-the-content-logic}

Denna valfria logik markerar och/eller beräknar innehållet som ska återges. Den anropas från HTML-uttryck med rätt Use-API-mönster.

Mekanismen för att skilja logik från utseende gör det lättare att klargöra vad som krävs för en viss vy. Det möjliggör också olika logik för olika vyer av samma resurs.

### Använda Java {#using-java}

[Använd-API:t för HTL Java gör att en HTML-fil kan få åtkomst till hjälpmetoder i en anpassad Java-klass](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html?lang=en). Detta gör att du kan använda Java-kod för att implementera logiken för att välja och konfigurera komponentinnehållet.

### Använda JavaScript {#using-javascript}

[Använd-API:t för HTML JavaScript gör att en HTML-fil kan komma åt hjälpkod som skrivits i JavaScript](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html?lang=en). Detta gör att du kan använda JavaScript-kod för att implementera logiken för att välja och konfigurera komponentinnehållet.

### Använda HTML-bibliotek på klientsidan {#using-client-side-html-libraries}

Moderna webbplatser är starkt beroende av bearbetning på klientsidan som styrs av komplex JavaScript- och CSS-kod. Det kan vara komplicerat att organisera och optimera serveringen av den här koden.

AEM tillhandahåller **Biblioteksmappar på klientsidan**, som gör att du kan lagra din klientkod i databasen, ordna den i kategorier och definiera när och hur varje kodkategori ska skickas till klienten. Klientsidans bibliotekssystem tar sedan hand om att skapa rätt länkar på den slutliga webbsidan för att läsa in rätt kod.

Läs [Använda HTML-bibliotek på klientsidan](/help/sites-developing/clientlibs.md) för mer information.

## Konfigurera redigeringsbeteendet {#configuring-the-edit-behavior}

Du kan konfigurera redigeringsbeteendet för en komponent, inklusive attribut som åtgärder som är tillgängliga för komponenten, egenskaper för redigeraren och avlyssnare som är relaterade till händelser för komponenten. Konfigurationen är gemensam för det beröringsaktiverade och klassiska användargränssnittet, men med vissa specifika skillnader.

The [redigeringsbeteendet för en komponent är konfigurerat](/help/sites-developing/components-basics.md#edit-behavior) genom att lägga till en `cq:editConfig` nod av typen `cq:EditConfig` nedanför komponentnoden (av typen `cq:Component`) och genom att lägga till specifika egenskaper och underordnade noder.

## Konfigurera förhandsvisningsbeteendet {#configuring-the-preview-behavior}

The [WCM Mode](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) cookie är inställd vid växling till **Förhandsgranska** även när sidan inte uppdateras.

Komponenter med en återgivning som är känslig för WCM-läget måste definieras så att de uppdateras specifikt och sedan förlitar sig på värdet för cookien.

>[!NOTE]
>
>I det beröringskänsliga användargränssnittet är endast värdena `EDIT` och `PREVIEW` används för [WCM Mode](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) cookie.

## Skapa och konfigurera en dialogruta {#creating-and-configuring-a-dialog}

I dialogrutor kan författaren interagera med komponenten. Med en dialogruta kan författare och/eller administratörer redigera innehåll, konfigurera komponenten eller definiera designparametrar (med en [Designdialogruta](#creating-and-configuring-a-design-dialog))

### Gränssnittet för korall och GRENITE {#coral-ui-and-granite-ui}

[Coral UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) och [Granite-gränssnitt](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) definiera det moderna utseendet och känslan hos AEM.

[Gränssnittet i Granite innehåller ett stort urval av de grundläggande komponenterna (widgetar)](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) behövs för att skapa en dialogruta i redigeringsmiljön. Vid behov kan du utöka markeringen och [skapa en egen widget](#creatinganewwidget).

Mer information finns i:

* Coral UI

   * Ett enhetligt gränssnitt för alla molnlösningar
   * [Koncepten i det AEM användargränssnittet med pekskärmsfunktioner - Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Användargränssnittshandbok för Coral](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html)

* Granite-gränssnitt

   * Innehåller Coral UI-kod inkapslad i Sling-komponenter för att bygga UI-konsoler och dialogrutor
   * [AEM för användargränssnitt med pekskärmsfunktion - GRE](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Bevilja gränssnittsdokumentation](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)

>[!NOTE]
>
>På grund av karaktären hos GRE-komponenterna (och skillnaderna mellan ExtJS-widgetarna) finns det vissa skillnader mellan hur komponenterna interagerar med det beröringsaktiverade gränssnittet och [klassiskt användargränssnitt](/help/sites-developing/developing-components-classic.md).

### Skapa en ny dialogruta {#creating-a-new-dialog}

Dialogrutor för användargränssnittet med pekskärm:

* är namngivna `cq:dialog`.
* definieras som en `nt:unstructured` noden med `sling:resourceType` egenskapsuppsättning.

* finns under deras `cq:Component` och bredvid deras komponentdefinition.
* återges på serversidan (som Sling-komponenter), baserat på deras innehållsstruktur och `sling:resourceType` -egenskap.
* använda GRI-ramverket för Granite.
* innehåller en nodstruktur som beskriver fälten i dialogrutan.

   * de här noderna är `nt:unstructured` med de `sling:resourceType` -egenskap.

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
>Om en komponent inte har någon dialogruta definierad för det beröringsaktiverade användargränssnittet, används den klassiska användargränssnittsdialogrutan som reserv i ett kompatibilitetslager. Om du vill anpassa en sådan dialogruta måste du anpassa den klassiska användargränssnittsdialogrutan. Se [AEM komponenter för det klassiska användargränssnittet](/help/sites-developing/developing-components-classic.md).

### Anpassa dialogrutefält {#customizing-dialog-fields}

>[!NOTE]
>
>Se:
>
>* AEM Gems-sessionen den [Anpassa dialogrutefält](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=en).
>* den exempelkod som omfattas av [Kodexempel - Anpassa dialogrutefält](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields).
>

#### Skapa ett nytt fält {#creating-a-new-field}

Widgetar för det beröringsaktiverade användargränssnittet implementeras som GRE-komponenter.

Om du vill skapa en ny widget som ska användas i en komponentdialogruta för det beröringsaktiverade användargränssnittet måste du [skapa en ny gränssnittskomponent för Granite](/help/sites-developing/granite-ui-component.md).

>[!NOTE]
>
>Mer information om GRENITE finns i [Granite UI-dokumentation](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html).

Om du ser dialogrutan som en enkel behållare för ett formulärelement kan du även se det primära innehållet i dialogrutan som formulärfält. När du skapar ett nytt formulärfält måste du skapa en resurstyp. Det motsvarar att skapa en ny komponent. För att du ska få hjälp med den uppgiften erbjuder Granite UI en generisk fältkomponent att ärva från (med `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

Mer specifikt ger GRE UI ett antal fältkomponenter som är lämpliga att använda i dialogrutor (eller mer allmänt i [formulär](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)).

>[!NOTE]
>
>Detta skiljer sig från det klassiska användargränssnittet, där widgetar representeras av `cq:Widgets` noder, var och en med en viss `xtype` för att fastställa relationen med deras motsvarande ExtJS-widget. Från en implementeringssynvinkel renderades dessa widgetar på klientsidan av ExtJS-ramverket.

När du har skapat resurstypen kan du skapa en instans av fältet genom att lägga till en ny nod i dialogrutan med egenskapen `sling:resourceType` refererar till den resurstyp som du just har introducerat.

#### Skapa ett klientbibliotek för stil och beteende {#creating-a-client-library-for-style-and-behavior}

Om du vill definiera format och beteende för komponenten kan du skapa en dedikerad [klientbibliotek](/help/sites-developing/clientlibs.md) som definierar din egen CSS/LESS och JS.

Om du vill att klientbiblioteket ska läsas in enbart för komponentdialogrutan (d.v.s. den inte ska läsas in för en annan komponent) måste du ange egenskapen `extraClientlibs`** **i dialogrutan till kategorinamnet för det klientbibliotek du just har skapat. Detta rekommenderas om klientbiblioteket är stort och/eller om fältet är specifikt för den dialogrutan och inte behövs i andra dialogrutor.

Om du vill att klientbiblioteket ska läsas in för alla dialogrutor anger du kategoriegenskapen för klientbiblioteket till `cq.authoring.dialog`. Det här är kategorinamnet för klientbiblioteket som inkluderas som standard när alla dialogrutor återges. Du vill göra det om klientbiblioteket är litet och/eller fältet är generiskt och kan återanvändas i andra dialogrutor.

Se följande exempel:

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * tillhandahålls av [Kodexempel](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Utöka (ärva från) ett fält {#extending-inheriting-from-a-field}

Beroende på dina behov kan du antingen:

* Utöka ett visst GRE-fält efter komponentarv ( `sling:resourceSuperType`)
* Utöka en given widget från det underliggande widgetbiblioteket (för Granite-gränssnittet är det korallgränssnitt) genom att följa widgetens biblioteks-API (JS/CSS-arv)

#### Åtkomst till dialogrutefält {#access-to-dialog-fields}

Du kan också använda återgivningsvillkor ( `rendercondition`) för att styra vem som har åtkomst till specifika flikar/fält i dialogrutan, till exempel:

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### Hantera fälthändelser {#handling-field-events}

Metoden för att hantera händelser i dialogrutefält är nu klar med [avlyssnare i ett anpassat klientbibliotek](#listeners-in-a-custom-client-library). Detta är en förändring från den äldre metoden att [avlyssnare i innehållsstrukturen](#listenersinthecontentstructureclassicui).

#### Lyssnare i ett anpassat klientbibliotek {#listeners-in-a-custom-client-library}

Om du vill mata in logik i fältet bör du:

1. Har fältet markerat med en viss CSS-klass ( *krok*).
1. I klientbiblioteket definierar du en JS-avlyssnare som är kopplad till det CSS-klassnamnet (detta garanterar att din anpassade logik endast omfattar fältet och inte påverkar andra fält av samma typ).

För att uppnå detta måste du känna till det underliggande widgetbiblioteket som du vill interagera med. Se [Dokumentation för Coral UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) identifiera vilken händelse du vill reagera på. Detta liknar den process du tidigare har utfört med ExtJS: hitta dokumentationssidan för en viss widget och kontrollera informationen om dess händelse-API.

Se följande exempel:

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * tillhandahålls av [Kodexempel](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Lyssnare i innehållsstrukturen {#listeners-in-the-content-structure}

I det klassiska användargränssnittet med ExtJS var det vanligt att ha avlyssnare för en viss widget i innehållsstrukturen. Att uppnå samma sak i det beröringskänsliga användargränssnittet skiljer sig från JS-avlyssnarkoden (eller vilken kod som helst) som inte längre är definierad i innehållet.

Innehållsstrukturen beskriver den semantiska strukturen. Den ska (måste) inte innebära den underliggande widgetens typ. Genom att inte ha JS-kod i innehållsstrukturen kan du ändra implementeringsinformationen utan att behöva ändra innehållsstrukturen. Du kan med andra ord ändra widgetbiblioteket utan att behöva ändra innehållsstrukturen.

#### Dialogrutans tillgänglighet identifieras {#dialog-ready}

Om du har ett anpassat JavaScript som bara behöver köras när dialogrutan är tillgänglig och klar bör du avlyssna `dialog-ready` -händelse.

Den här händelsen utlöses när dialogrutan läses in (eller läses in igen) och är klar att användas, vilket innebär när det finns en ändring (skapa/uppdatera) i DOM för dialogrutan.

`dialog-ready` kan användas för att koppla i anpassad JavaScript-kod som utför anpassningar av fälten i en dialogruta eller liknande åtgärder.

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

Fältvalidering i GRA-gränssnitt och GRA-komponenter (motsvarande widgetar) görs med `foundation-validation` API. [Se `foundation-valdiation` Behåll dokumentation för mer information.](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

Se till exempel:

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * tillhandahålls av [Kodexempel](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## Skapa och konfigurera en designdialogruta {#creating-and-configuring-a-design-dialog}

Dialogrutan Design visas när en komponent har designdetaljer som kan redigeras i [Designläge](/help/sites-authoring/default-components-designmode.md).

Definitionen liknar den för en [dialogruta som används för att redigera innehåll](#creating-a-new-dialog), med skillnaden att det är definierat som en nod:

* Nodnamn: `cq:design_dialog`
* Typ: `nt:unstructured`

## Skapa och konfigurera en Inplace-redigerare {#creating-and-configuring-an-inplace-editor}

Med en infogningsredigerare kan användaren redigera innehåll direkt i styckeflödet utan att behöva öppna en dialogruta. Standardkomponenterna Text och Title har till exempel båda en infogad redigerare.

En infogningsredigerare är inte nödvändig/meningsfull för varje komponenttyp.

Se [Utöka sidredigering - Lägg till ny infogningsredigerare](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor) för mer information.

## Anpassa komponentverktygsfältet {#customizing-the-component-toolbar}

The [Komponentverktygsfältet](/help/sites-developing/touch-ui-structure.md#component-toolbar) ger användaren tillgång till en rad åtgärder för komponenten, till exempel redigera, konfigurera, kopiera och ta bort.

Se [Utöka sidredigering - Lägg till ny åtgärd i ett komponentverktygsfält](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) för mer information.

## Konfigurera en komponent för referenslinjen (lånad/lånad) {#configuring-a-component-for-the-references-rail-borrowed-lent}

Om den nya komponenten refererar till innehåll från andra sidor kan du överväga om du vill att den ska påverka **Lånat innehåll** och **Utlånat innehåll** avsnitt i [**Referenser**](/help/sites-authoring/basic-handling.md#references) Rail.

AEM markerar bara komponenten Reference. Om du vill lägga till din komponent måste du konfigurera OSGi-paketet **Referenskonfiguration för WCM-redigeringsinnehåll**.

Skapa en ny post i definitionen som anger komponenten tillsammans med den egenskap som ska kontrolleras. Till exempel:

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>När du arbetar med AEM finns det flera metoder för att hantera konfigurationsinställningarna för sådana tjänster. Se [Konfigurerar OSGi](/help/sites-deploying/configuring-osgi.md) om du vill ha mer information och rekommenderade rutiner.

## Aktivera och lägga till komponenten i styckesystemet {#enabling-and-adding-your-component-to-the-paragraph-system}

När komponenten har utvecklats måste den aktiveras för användning i ett lämpligt styckesystem, så att den kan användas på de sidor som krävs.

Detta kan göras antingen genom att:

* använda [Designläge](/help/sites-authoring/default-components-designmode.md) när du redigerar en viss sida.
* [definiera `components` egenskap i en malls styckesystem](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system).

## Konfigurera ett styckesystem så att en komponentinstans skapas när en resurs dras {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

AEM erbjuder möjlighet att konfigurera ett styckesystem på sidan så att [en instans av den nya komponenten skapas automatiskt när en användare drar en (lämplig) resurs till en instans av sidan](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) (i stället för att alltid behöva dra en tom komponent till sidan).

Detta beteende och den nödvändiga relationen mellan resurser och komponenter kan konfigureras:

1. Under styckedefinitionen för siddesignen. Till exempel:

   * `/etc/designs/<myApp>/page/par`

   Skapa en ny nod:

   * Namn: `cq:authoring`
   * Typ: `nt:unstructured`

1. Skapa en ny nod under detta för att innehålla alla mappningar av resurs-till-komponent:

   * Namn: `assetToComponentMapping`
   * Typ: `nt:unstructured`

1. Skapa en nod för varje resurs-till-komponent-mappning:

   * Namn: text; vi rekommenderar att namnet anger resursen och den relaterade komponenttypen, till exempel bild
   * Typ: `nt:unstructured`

   Alla med följande egenskaper:

   * `assetGroup`:

      * Typ: `String`
      * Värde: den grupp som den relaterade tillgången tillhör, till exempel `media`

   * `assetMimetype`:

      * Typ: `String`
      * Värde: den relaterade tillgångens mime-typ, till exempel `image/*`

   * `droptarget`:

      * Typ: `String`
      * Värde: släppmålet, till exempel `image`

   * `resourceType`:

      * Typ: `String`
      * Värde: den relaterade komponentresursen, till exempel `foundation/components/image`

   * `type`:

      * Typ: `String`
      * Värde: typen, till exempel `Images`

Se exempel:

* `/etc/designs/geometrixx/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-outdoors/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-media/jcr:content/article/article-content-par/cq:authoring`

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna aem-project-archietype-projekt på GitHub](https://github.com/adobe/aem-project-archetype)
* Hämta projektet som [en ZIP-fil](https://github.com/adobe/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>Det automatiska skapandet av komponentinstanser kan nu enkelt konfigureras i användargränssnittet när du använder [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) och redigerbara mallar. Se [Skapa sidmallar](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) om du vill ha mer information om hur du definierar vilka komponenter som automatiskt associeras med de angivna medietyperna.

## Använda AEM Brackets Extension {#using-the-aem-brackets-extension}

The [AEM Brackets Extension](/help/sites-developing/aem-brackets.md) ger ett smidigt arbetsflöde för att redigera AEM komponenter och klientbibliotek. Den baseras på [Parenteser](https://brackets.io/) kodredigerare.

Tillägg:

* Förenklar synkronisering (ingen Maven eller filvalv krävs) för att öka utvecklarens effektivitet och även hjälpa gränssnittsutvecklare med begränsade AEM att delta i projekt.
* Tillhandahåller vissa [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) stöd, det mallspråk som är utformat för att förenkla komponentutvecklingen och öka säkerheten.

>[!NOTE]
>
>Hakparenteser är den rekommenderade mekanismen för att skapa komponenter. Den ersätter funktionaliteten CRXDE Lite - Skapa komponent, som har utformats för det klassiska användargränssnittet.

## Migrera från en klassisk komponent {#migrating-from-a-classic-component}

När du migrerar en komponent som har utformats för användning med det klassiska användargränssnittet till en komponent som kan användas med det beröringsaktiverade användargränssnittet (antingen enbart eller tillsammans) bör du tänka på följande:

* HTL

   * Användning av [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) är inte obligatoriskt, men om komponenten behöver uppdateras är det ett bra tillfälle att överväga [migrera från JSP till HTML](/help/sites-developing/components-basics.md#htl-vs-jsp).

* Komponenter

   * Migrera [`cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) kod som använder klassiska gränssnittsspecifika funktioner
   * RTE-plugin, mer information finns i [Konfigurera RTF-redigeraren](/help/sites-administering/rich-text-editor.md).
   * [Migrera `cq:listener` kod](#migrating-cq-listener-code) som använder funktioner som är specifika för det klassiska användargränssnittet

* Dialogrutor

   * Skapa en dialogruta för användning i det beröringsaktiverade användargränssnittet. Av kompatibilitetsskäl kan emellertid det beröringsaktiverade användargränssnittet använda definitionen för en klassisk användargränssnittsdialogruta när ingen dialogruta har definierats för det beröringsaktiverade användargränssnittet.
   * The [Verktyg för AEM](/help/sites-developing/modernization-tools.md) som hjälper dig att utöka befintliga komponenter.
   * [Mappa ExtJS till GRE UI-komponenter](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) ger dig en praktisk översikt över ExtJS-xtyper och nodtyper med motsvarande Granite-resurstyper.
   * Anpassa fält, mer information finns i AEM Gems-sessionen på [Anpassa dialogrutefält](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=en).
   * Migrera från vyper till [Verifiering av GRI](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * Mer information finns i Använda JS-avlyssnare [Hantera fälthändelser](#handling-field-events) och AEM Gems-sessionen [Anpassa dialogrutefält](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=en).

### Migrera cq:avlyssnarkod {#migrating-cq-listener-code}

Om du migrerar ett projekt som har utformats för det klassiska användargränssnittet ska du `cq:listener` kod (och komponentrelaterade klienter) kan använda funktioner som är specifika för det klassiska användargränssnittet (till exempel `CQ.wcm.*`). För migreringen måste du uppdatera sådan kod med motsvarande objekt/funktioner i det beröringsaktiverade användargränssnittet.

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
* Och så vidare

Därför är det enkelt att göra befintliga dokumentationsmarkeringar tillgängliga i själva komponenten.

Placera en `README.md` i komponentstrukturen. Den här markeringen visas i dialogrutan [komponentkonsol](/help/sites-authoring/default-components-console.md).

![chlimage_1-7](assets/chlimage_1-7.png)

Den kod som stöds är densamma som den som [innehållsfragment](/help/assets/content-fragments/content-fragments-markdown.md).
