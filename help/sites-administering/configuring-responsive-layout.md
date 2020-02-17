---
title: Konfigurera layoutbehållare och layoutläge
seo-title: Konfigurera layoutbehållare och layoutläge
description: Lär dig hur du konfigurerar layoutbehållaren och layoutläget.
seo-description: Lär dig hur du konfigurerar layoutbehållaren och layoutläget.
uuid: 952b7c86-76ab-4699-8530-8638e46bb50f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 10940000-808a-48ae-8e46-61eccef71eab
legacypath: /content/docs/en/aem/6-2/administer/operations/page-authoring/configuring-responsive-layouting
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konfigurera layoutbehållare och layoutläge{#configuring-layout-container-and-layout-mode}

[Responsiv layout](/help/sites-authoring/responsive-layout.md) är en mekanism för att förverkliga [responsiv webbdesign](https://en.wikipedia.org/wiki/Responsive_web_design). På så sätt kan användaren skapa webbsidor som har en layout och dimensioner som är beroende av vilka enheter som användarna använder.

>[!NOTE]
>
>Detta kan jämföras med [Mobile Web](/help/sites-developing/mobile-web.md) -funktionerna, som använder adaptiv webbdesign (främst för det klassiska användargränssnittet).

AEM implementerar responsiv layout för dina sidor med en kombination av mekanismer:

* [**Komponenten Layoutbehållare **](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)

   Den här komponenten har ett rutnätsstyckesystem där du kan lägga till och placera komponenter i ett responsivt rutnät. Den kan användas som standardparsyta för sidan och/eller göras tillgänglig för författare i komponentwebbläsaren.

   * Standardkomponenten för **Layoutbehållare** definieras under:

      /libs/wcm/foundation/components/responsivegrid

   * Du kan definiera layoutbehållare:

      * Som en komponent som användaren kan lägga till på en sida.
      * Som standardparsys för sidan.
      * Båda.

         Du kan ha layoutbehållaren som standard för sidan, samtidigt som användaren kan lägga till fler layoutbehållare i den här versionen. till exempel för att uppnå kolumnkontroll.

* **[Layoutläge](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**När layoutbehållaren har placerats på sidan kan du använda **layoutläget**för att placera innehåll i det responsiva rutnätet.

* [**Emulator **](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)Med den här funktionen kan du skapa och redigera responsiva webbplatser som ordnar om layouten enligt enhetens/fönstrets storlek genom att ändra storlek på komponenterna interaktivt. Användaren kan sedan se hur innehållet återges med hjälp av emulatorn.

>[!CAUTION]
>
>Även om komponenten **Layoutbehållare** är tillgänglig i det klassiska användargränssnittet, är dess fullständiga funktioner bara tillgängliga i det beröringskänsliga användargränssnittet.

Med dessa responsiva rutnätsmekanismer kan du:

* Använd brytpunkter (som indikerar enhetsgruppering) för att definiera olika innehållsbeteenden baserat på enhetslayout.
* Dölj komponenter baserat på enhetsgrupp (definiera på vilken brytpunkt en komponent ska döljas).
* Använd vågrät fäst mot rutnät (placera komponenter i rutnätet, ändra storlek efter behov, definiera när de ska komprimeras/omformas så att de ligger sida vid sida eller ovanför/nedanför).
* Uppnå kolumnkontroll.

>[!NOTE]
>
>I en körklar installation har responsiv layout konfigurerats för [webbbutikens](/help/sites-developing/we-retail.md)referensplats. Du måste fortfarande [aktivera layoutbehållarkomponenten](#enable-the-layout-container-component-for-page) för andra sidor.

## Konfigurera den responsiva emulatorn {#configuring-the-responsive-emulator}

Med de här åtgärderna kan du se den responsiva **emulatorn** på din plats.

### Registrera dina sidkomponenter för emulering {#register-your-page-components-for-emulation}

Om du vill att emulatorn ska ha stöd för dina sidor måste du registrera sidkomponenterna. Se [Registrera sidkomponenter för simulering](/help/sites-developing/responsive.md#registering-page-components-for-simulation).

### Ange enhetsgrupper {#specify-the-device-groups}

Information om hur du anger enhetsgrupperna som visas i emulatorns enhetslista finns i [Ange enhetsgrupper](/help/sites-developing/responsive.md#specifying-the-device-groups).

### Länka platsen till de angivna enhetsgrupperna {#link-your-site-to-the-specified-device-groups}

Om du vill inkludera emulatorn måste du länka din plats till enhetsgrupperna. Se [Lägga till enhetslistan](/help/sites-developing/responsive.md#adding-the-devices-list) (för både det klassiska och pekoptimerade användargränssnittet).

## Aktivera layoutläge för webbplatsen {#activate-layout-mode-for-your-site}

Dessa procedurer används för att aktivera **layoutläget** på din plats.

### Konfigurera brytpunkterna {#configure-the-breakpoints}

[Brytpunkter](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate):

* Används i responsiv design.
* Kan definieras:

   * På sidmallen, varifrån inställningarna kopieras till alla sidor som skapas med den mallen.
   * På sidnoden, varifrån inställningarna ärvs av underordnade sidor.

* Definiera en titel och en bredd:

   * Titeln beskriver den generiska enhetsgrupperingen, med orientering om så krävs. till exempel telefon, surfplatta, bordslandskap.
   * Bredden definierar den maximala bredden i pixlar för den allmänna enhetsgrupperingen. Om till exempel brytpunktstelefonen har en bredd på 768 är det den maximala bredden för den layout som används för en telefonenhet.

* Är synliga som markörer högst upp i sidredigeraren när du använder emulatorn.
* Ärvs från den överordnade nodhierarkin och kan åsidosättas när som helst.
* Det finns en standardbrytpunkt som täcker allt ovanför den senast *konfigurerade* brytpunkten.

De kan definieras med CRXDE Lite eller XML.

>[!NOTE]
>
>Om du skapar ett nytt projekt:
>
>* du behöver lägga till brytpunkter i mallarna.
>
>
Om du migrerar ett befintligt projekt (med befintligt innehåll) måste du:
>
>* lägga till brytpunkter i mallar
>* lägga till samma brytpunkter på befintliga sidor
   >  När arv används kan du begränsa detta till innehållets rotsida.
>



#### Konfigurera brytpunkter med CRXDE Lite {#configuring-breakpoints-using-crxde-lite}

1. Navigera med CRXDE Lite (eller motsvarande) till antingen:

   * Din malldefinition.
   * Sidans `jcr:content` nod.

1. Skapa noden under `jcr:content` :

   * Namn: `cq:responsive`
   * Typ: `nt:unstructured`

1. Skapa noden här:

   * Namn: `breakpoints`
   * Typ: `nt:unstructured`

1. Under brytpunktsnoden kan du skapa valfritt antal brytpunkter. Varje definition är en enda nod med följande egenskaper:

   * Namn: `<descriptive name>`
   * Typ: `nt:unstructured`
   * Titel: `String` * `<descriptive title seen in Emulator>`*
   * Bredd: `Decimal` * `<value of breakpoint>`*

#### Konfigurera brytpunkter med XML {#configuring-breakpoints-using-xml}

Brytpunkter finns i avsnittet `<jcr:content>` i `.context.html` under lämplig mallmapp (eller innehållsmapp).

En exempeldefinition:

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

### Lägg till en leverantör av responsiv information {#add-a-responsive-information-provider}

>[!NOTE]
>
>Detta behövs bara om sidkomponenten inte är baserad på bassidans komponent.

Kopiera följande `cq:infoProviders` nodstruktur till den överordnade sidkomponenten:

`/libs/foundation/components/page/cq:infoProviders/responsive`

## Aktivera komponentstorleksändring för sidan {#enable-component-resizing-for-the-page}

Dessa procedurer krävs så att du kan ändra storlek på komponenter i **layoutläget** .

### Ange layoutbehållare som huvudparsys {#set-layout-container-as-main-parsys}

Om du vill ange att huvudparsytan på sidan ska vara en layoutbehållare måste du definiera parametrarna som:

`wcm/foundation/components/responsivegrid`

I något av följande:

* Sidkomponent
* Sidmall (för framtida bruk)

I följande två exempel visas definitionen:

* **HTML:**

   ```xml
   <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
   ```

* **JSP:**

   ```
   <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
   ```

### Inkludera responsiv CSS {#include-the-responsive-css}

#### CSS för brytpunkter med LESS {#css-for-breakpoints-using-less}

AEM använder LESS för att generera delar av den CSS som behövs, och dessa måste ingå i dina projekt.

Du måste också skapa ett [klientbibliotek](https://docs.adobe.com/content/docs/en/aem/6-0/develop/the-basics/clientlibs.html) för att kunna tillhandahålla ytterligare konfigurations- och funktionsanrop. Följande LESS-extrakt är ett exempel på det minsta du behöver lägga till i ditt projekt:

```java
@import (once) "/libs/wcm/foundation/clientlibs/grid/grid_base.less";

/* maximum amount of grid cells to be provided */
@max_col: 12;

/* default breakpoint */
.aem-Grid {
  .generate-grid(default, @max_col);
}

/* phone breakpoint */
@media (max-width: 768px) {
  .aem-Grid {
    .generate-grid(phone, @max_col);
  }
}

/* tablet breakpoint */
@media (min-width: 769px) and (max-width: 1200px) {
  .aem-Grid {
    .generate-grid(tablet, @max_col);
  }
}
```

Basrutnätsdefinitionen finns under:

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### Fundera på formatering {#styling-considerations}

Komponenter som finns i en responsiv behållare ändrar storlek (tillsammans med deras respektive HTML DOM-element) beroende på stödrastrets responsiva storlek. Därför bör du under dessa omständigheter undvika (eller uppdatera) definitioner av DOM-element med fast bredd (som finns).

Exempel:

* Före:

   * `width=100px`

* Efter:

   * `max-width=100px`

#### Storleksändring och adaptiv bildkompatibilitet {#resizing-and-adaptive-image-compliance}

Om du ändrar storlek på en komponent i rutnätet utlöses följande avlyssnare om det är lämpligt:

* `beforeedit`
* `beforechildedit`
* `afteredit`

* `afterchildedit`

Om du vill ändra storlek på och uppdatera innehållet i en adaptiv bild som ingår i ett responsivt rutnät måste du lägga till en uppsättning som `afterEdit` avlyssnare i `REFRESH_PAGE` `EditConfig` filen för varje ingående komponent.

Exempel:

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

Den adaptiva bildmekanismen görs tillgänglig via ett skript som styr valet av rätt bild för fönstrets aktuella storlek. Den aktiveras när DOM är redo eller när en dedikerad händelse tas emot. För närvarande måste sidan uppdateras för att korrekt återspegla resultatet av användarens åtgärd.

>[!CAUTION]
>
>Klientlibs för anpassade formatmallar måste läsas in som en del av sidhuvudet för att de ska fungera korrekt både när de skapas och publiceras.

## Aktivera layoutbehållarkomponenten för sidan {#enable-the-layout-container-component-for-page}

Med de här åtgärderna kan författare dra instanser av komponenten **Layoutbehållare** till sidan.

### Aktivera layoutbehållarkomponenten för sidredigering {#enable-the-layout-container-component-for-page-editing}

Om du vill att författare ska kunna lägga till fler responsiva rutnät på innehållssidorna måste du aktivera layoutbehållarkomponenten för sidan. Du kan göra detta med:

* **Författarmiljö**

   Använd [designläget](/help/sites-authoring/default-components-designmode.md) för att aktivera **lagerbehållarkomponenten** för en sida.

* **Komponentdefinition**

   Använd `allowedComponent` eller en statisk include när du definierar komponenten.

### Konfigurera stödrastret för layoutbehållaren {#configure-the-grid-of-the-layout-container}

Du kan konfigurera antalet kolumner som är tillgängliga för varje särskild instans av layoutbehållaren:

1. **Författarmiljö**

   Du kan konfigurera antalet kolumner som är tillgängliga för varje enskild instans av layoutbehållaren.

   Det gör du genom att använda [designläget](/help/sites-authoring/default-components-designmode.md)och sedan öppna designdialogrutan för önskad behållare. Här kan du ange hur många kolumner som ska vara tillgängliga för placering och storleksändring. Standardvärdet är 12.

1. **XML**

   Definitioner för det responsiva rutnätet anges i:

   `etc/design/<*your-project-name*>/.content.xml`

   Följande parametrar kan definieras:

   * Antal tillgängliga kolumner:

      * `columns="{String}8"`
   * Komponenter som kan läggas till i den aktuella komponenten:

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`


