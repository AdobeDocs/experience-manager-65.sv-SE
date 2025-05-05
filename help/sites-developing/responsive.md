---
title: Responsiv design för webbsidor
description: Med responsiv design kan samma sidor visas effektivt på flera enheter i flera olika orienteringar.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
legacypath: /content/docs/en/aem/6-0/develop/mobile/responsive
exl-id: c705710b-a94a-4f4f-affa-ddd4fc6cb0ec
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '5260'
ht-degree: 0%

---

# Responsiv design för webbsidor{#responsive-design-for-web-pages}

{{ue-over-mobile}}

>[!NOTE]
>
>Olika exempel baseras på exempelinnehållet i Geometrixx, som inte längre levereras med AEM (Adobe Experience Manager), som har ersatts av We.Retail. I dokumentet [Referensimplementering för butik](/help/sites-developing/we-retail.md#we-retail-geometrixx) finns information om hur du hämtar och installerar Geometrixx.

Utforma dina webbsidor så att de anpassas till den klientvisningsruta där de visas. Med responsiv design kan samma sidor visas effektivt på flera enheter i båda riktningarna. I följande bild visas några sätt på vilka en sida kan reagera på ändringar i visningsrutans storlek:

* Layout: Använd layouter med en kolumn för mindre visningsrutor och layouter med flera kolumner för större visningsrutor.
* Textstorlek: Använd större textstorlek (vid behov, t.ex. rubriker) i större visningsrutor.
* Innehåll: Inkludera endast det viktigaste innehållet när det visas på mindre enheter.
* Navigering: Enhetsspecifika verktyg finns för åtkomst till andra sidor.
* Bilder: Serverar bildåtergivningar som passar för klientvisningsrutan. enligt fönstrets mått.

![chlimage_1-4](assets/chlimage_1-4a.png)

Utveckla Adobe Experience Manager-program (AEM) som genererar HTML 5-sidor som anpassar sig efter olika fönsterstorlekar och orienteringar. Följande intervall med visningsrutebredder motsvarar till exempel olika enhetstyper och orienteringar

* Maximal bredd på 480 pixlar (telefon, stående)
* Maximal bredd på 767 pixlar (telefon, liggande)
* Bredd mellan 768 pixlar och 979 pixlar (surfplatta, stående)
* Bredd mellan 980 pixlar och 1 199 pixlar (surfplatta, liggande)
* Bredd 1 200 pixlar eller mer (skrivbord)

Mer information om hur du implementerar responsiva designbeteenden finns i följande avsnitt:

* [Mediefrågor](/help/sites-developing/responsive.md#using-media-queries)
* [Flytande stödraster](/help/sites-developing/responsive.md#developing-a-fluid-grid)
* [Adaptiva bilder](/help/sites-developing/responsive.md#using-adaptive-images)

När du designar kan du använda **[!UICONTROL Sidekick]** för att förhandsgranska sidorna för olika skärmstorlekar.

## Innan du börjar utveckla {#before-you-develop}

Innan du utvecklar det AEM programmet som stöder dina webbsidor bör du fatta flera designbeslut. Du måste till exempel ha följande information:

* De enheter ni riktar er mot.
* Storleken på målvisningsrutan.
* Sidlayouterna för varje avsedd visningsruta.

### Programstruktur {#application-structure}

Den typiska AEM programstrukturen har stöd för alla responsiva designimplementeringar:

* Sidkomponenter finns under /apps/*application_name*/components
* Mallar finns under /apps/*application_name*/templates
* Designer finns under /etc/designs

## Använda mediefrågor {#using-media-queries}

Mediefrågor möjliggör selektiv användning av CSS-format för sidåtergivning. Med AEM utvecklingsverktyg och funktioner kan du effektivt och effektivt implementera mediefrågor i dina program.

W3C-gruppen tillhandahåller rekommendationen [Mediefrågor](https://www.w3.org/TR/mediaqueries-3/) som beskriver den här CSS3-funktionen och syntaxen.

### Skapa CSS-filen {#creating-the-css-file}

I CSS-filen definierar du mediefrågor baserat på egenskaperna för de enheter som du har som mål. Följande implementeringsstrategi är effektiv för att hantera format för varje mediefråga:

* Använd en ClientLibraryFolder för att definiera den CSS som sätts samman när sidan återges.
* Definiera varje mediefråga och tillhörande format i separata CSS-filer. Det är användbart att använda filnamn som representerar enhetsfunktionerna i mediefrågan.
* Definiera format som är gemensamma för alla enheter i en separat CSS-fil.
* I filen css.txt i ClientLibraryFolder ordnar du CSS-listfilerna så som krävs i den sammansatta CSS-filen.

Medieexemplet `We.Retail` använder den här strategin för att definiera format i webbplatsdesignen. CSS-filen som används av `We.Retail` är på `*/apps/weretail/clientlibs/clientlib-site/less/grid.less`.

I följande tabell visas filerna i css-mappen.

<table>
 <tbody>
  <tr>
   <th>Filnamn</th>
   <th>Beskrivning</th>
   <th>Mediefråga</th>
  </tr>
  <tr>
   <td>style.css</td>
   <td>Vanliga format.</td>
   <td>Ej tillämpligt</td>
  </tr>
  <tr>
   <td>bootstrap.css</td>
   <td>Vanliga format, som definieras av Twitter Bootstrap.</td>
   <td>Ej tillämpligt</td>
  </tr>
  <tr>
   <td>responsive-1200px.css</td>
   <td>Format för alla medier som är 1 200 pixlar breda eller bredare.</td>
   <td><p>@media (min-width: 1200 px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-980px-1199px.css</td>
   <td>Format för media som är mellan 980 pixlar och 1 199 pixlar breda.</td>
   <td><p>@media (min-width: 980 px) och (max-width: 1199 px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-768px-979px.css</td>
   <td>Format för media som är mellan 768 pixlar och 979 pixlar breda. </td>
   <td><p>@media (min-width: 768 px) och (max-width: 979 px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-767px-max.css</td>
   <td>Format för alla medier som är mindre än 768 pixlar breda.</td>
   <td><p>@media (max-width: 767 px) {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-480px.css</td>
   <td>Format för alla medier som är mindre än 481 pixlar breda.</td>
   <td>@media (max-width: 480 px) {<br /> ...<br /> }</td>
  </tr>
 </tbody>
</table>

Filen css.txt i mappen `/etc/designs/weretail/clientlibs` visar de CSS-filer som finns i klientbiblioteksmappen. Filernas ordning tillämpar formatprioritet. Format är mer specifika när enhetens storlek minskar.

`#base=css`

```
style.css
 bootstrap.css
```

```
responsive-1200px.css
 responsive-980px-1199px.css
 responsive-768px-979px.css
 responsive-767px-max.css
 responsive-480px.css
```

**Tips**: Med beskrivande filnamn kan du enkelt identifiera målvisningsrutans storlek.

### Använda mediefrågor med AEM sidor {#using-media-queries-with-aem-pages}

Inkludera klientbiblioteksmappen i JSP-skriptet för sidkomponenten. Om du gör det kan du generera CSS-filen som innehåller mediefrågorna och refererar till filen.

```xml
<ui:includeClientLib categories="apps.weretail.all"/>
```

>[!NOTE]
>
>Klientbiblioteksmappen `apps.weretail.all` bäddar in klientbiblioteksbiblioteket.

JSP-skriptet genererar följande HTML-kod som refererar till formatmallarna:

```xml
<link rel="stylesheet" href="/etc/designs/weretail/clientlibs-all.css" type="text/css">
<link href="/etc/designs/weretail.css" rel="stylesheet" type="text/css">
```

## Förhandsgranska för specifika enheter {#previewing-for-specific-devices}

Se förhandsgranskningar av sidorna i olika visningsrutestorlekar så att du kan testa beteendet i din responsiva design. I **[!UICONTROL Preview]**-läget innehåller **[!UICONTROL Sidekick]** en **[!UICONTROL Devices]**-listruta som du använder för att välja en enhet. När du väljer en enhet ändras sidan så att den anpassas till visningsrutans storlek.

![chlimage_1-5](assets/chlimage_1-5a.png)

Om du vill aktivera enhetsförhandsvisningen i **[!UICONTROL Sidekick]** måste du konfigurera sidan och tjänsten **[!UICONTROL MobileEmulatorProvider]**. En annan sidkonfiguration styr listan över enheter som visas i listan **[!UICONTROL Devices]**.

### Lägga till enhetslistan {#adding-the-devices-list}

Listan **[!UICONTROL Devices]** visas i **[!UICONTROL Sidekick]** när sidan innehåller JSP-skriptet som återger listan **[!UICONTROL Devices]**. Om du vill lägga till listan **[!UICONTROL Devices]** i **[!UICONTROL Sidekick]** tar du med skriptet `/libs/wcm/mobile/components/simulator/simulator.jsp` i avsnittet `head` på sidan.

Inkludera följande kod i JSP som definierar avsnittet `head`:

`<cq:include script="/libs/wcm/mobile/components/simulator/simulator.jsp"/>`

Öppna filen `/apps/weretail/components/page/head.jsp` i CRXDE Lite om du vill se ett exempel.

### Registrerar sidkomponenter för simulering {#registering-page-components-for-simulation}

Om du vill att enhetssimulatorn ska stödja dina sidor registrerar du dina sidkomponenter med fabrikstjänsten MobileEmulatorProvider och definierar egenskapen `mobile.resourceTypes`.

När du arbetar med AEM finns det flera metoder för att hantera konfigurationsinställningarna för sådana tjänster. Mer information finns i [Konfigurera OSGi](/help/sites-deploying/configuring-osgi.md).

Så här skapar du till exempel en ` [sling:OsgiConfig](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)`-nod i ditt program:

* Överordnad mapp: `/apps/application_name/config`
* Namn: `com.day.cq.wcm.mobile.core.impl.MobileEmulatorProvider-*alias*`

  Suffixet - `*alias*` krävs eftersom MobileEmulatorProvider-tjänsten är en fabrikstjänst. Använd ett alias som är unikt för den här fabriken.

* `jcr:primaryType`: `sling:OsgiConfig`

Lägg till följande nodegenskap:

* Namn: `mobile.resourceTypes`
* Typ: `String[]`
* Värde: Sökvägarna till de sidkomponenter som återger dina webbsidor. Geometrixx-media-appen använder till exempel följande värden:

  ```
  geometrixx-media/components/page
   geometrixx-unlimited/components/pages/page
   geometrixx-unlimited/components/pages/coverpage
   geometrixx-unlimited/components/pages/issue
  ```

### Ange enhetsgrupper {#specifying-the-device-groups}

Om du vill ange de enhetsgrupper som visas i listan Enheter lägger du till en `cq:deviceGroups`-egenskap i noden `jcr:content` på webbplatsens rotsida. Värdet för egenskapen är en array med sökvägar till enhetsgruppsnoderna.

Enhetsgruppnoderna finns i mappen `/etc/mobile/groups`.

Rotsidan för Geometrixx Media-webbplatsen är till exempel `/content/geometrixx-media`. Noden `/content/geometrixx-media/jcr:content` innehåller följande egenskap:

* Namn: `cq:deviceGroups`
* Typ: `String[]`
* Värde: `/etc/mobile/groups/responsive`

Använd verktygskonsolen för att [skapa och redigera enhetsgrupper](/help/sites-developing/groupfilters.md).

>[!NOTE]
>
>För enhetsgrupper som du använder för responsiv design redigerar du enhetsgruppen och väljer Inaktivera emulator på fliken Allmänt. Det här alternativet förhindrar att emulatorkarusellen visas, vilket inte är relevant för responsiv design.
>

## Använda adaptiva bilder {#using-adaptive-images}

Du kan använda mediefrågor för att välja en bildresurs som ska visas på sidan. Alla resurser som använder en mediefråga för att anpassa användningen hämtas dock till klienten. Mediefrågan avgör bara om den hämtade resursen visas.

När det gäller stora resurser som bilder är det inte effektivt att hämta alla resurser i kundens dataflöde. Om du vill hämta resurser selektivt använder du JavaScript för att initiera resursbegäran efter att mediefrågorna har utfört urvalet.

Följande strategi läser in en enskild resurs som väljs med hjälp av mediefrågor:

1. Lägg till ett DIV-element för varje version av resursen. Inkludera resursens URI som värde för ett attributvärde. Webbläsaren tolkar inte attributet som en resurs.
1. Lägg till en mediefråga till varje DIV-element som är lämpligt för resursen.
1. När dokumentet läses in eller fönstrets storlek ändras testas mediefrågan för varje DIV-element av JavaScript-koden.
1. Utifrån resultaten av frågorna kan du avgöra vilken resurs som ska inkluderas.
1. Infoga ett HTML-element i DOM som refererar till resursen.

### Utvärdera mediefrågor med JavaScript {#evaluating-media-queries-using-javascript}

Implementeringar av [MediaQueryList-gränssnittet](https://drafts.csswg.org/cssom-view/#the-mediaquerylist-interface) som definieras av W3C gör att du kan utvärdera mediefrågor med JavaScript. Du kan lägga till logik i mediafrågeresultaten och köra skript som är avsedda för det aktuella fönstret:

* Webbläsare som implementerar MediaQueryList-gränssnittet stöder funktionen `window.matchMedia()`. Den här funktionen testar mediefrågor mot en angiven sträng. Funktionen returnerar ett `MediaQueryList`-objekt som ger åtkomst till frågeresultaten.

* För webbläsare som inte implementerar gränssnittet kan du använda en `matchMedia()`-polyfyllning, till exempel [ matchMedia.js ](https://github.com/paulirish/matchMedia.js), ett kostnadsfritt tillgängligt JavaScript-bibliotek.

#### Välja mediespecifika resurser {#selecting-media-specific-resources}

W3C [picture-elementet](https://html.spec.whatwg.org/multipage/embedded-content.html#the-picture-element) använder mediefrågor för att avgöra vilken källa som ska användas för bildelement. Bildelementet använder elementattribut för att associera mediefrågor med bildsökvägar.

Biblioteket [&#128279;](https://github.com/scottjehl/picturefill) picturefill.js `picture` som är fritt tillgängligt har liknande funktioner som det föreslagna elementet  och använder en liknande strategi. Biblioteket picturefill.js anropar `window.matchMedia` för att utvärdera de mediefrågor som har definierats för en uppsättning med `div` element. Varje `div`-element anger också en bildkälla. Källan används när mediefrågan för elementet `div` returnerar `true`.

Biblioteket `picturefill.js` kräver HTML-kod som liknar följande exempel:

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
</div>
```

När sidan återges infogar picturefull.js ett `img`-element som det sista underordnade elementet i `<div data-picture>` -elementet:

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
    <img src="path to medium image">
</div>
```

På en AEM sida är värdet för attributet `data-src` sökvägen till en resurs i databasen.

### Implementera adaptiva bilder i AEM {#implementing-adaptive-images-in-aem}

Om du vill implementera adaptiva bilder i ditt AEM måste du lägga till de nödvändiga JavaScript-biblioteken och inkludera den nödvändiga HTML-koden på sidorna.

**Bibliotek**

Hämta följande JavaScript-bibliotek och inkludera dem i en klientbiblioteksmapp:

* [matchMedia.js](https://github.com/paulirish/matchMedia.js) (för webbläsare som inte implementerar gränssnittet MediaQueryList)
* [picturefill.js](https://github.com/scottjehl/picturefill)
* jquery.js (tillgänglig via klientbiblioteksmappen `/etc/clientlibs/granite/jquery` (category = jquery)
* [jquery.debouncedresize.js](https://github.com/louisremi/jquery-smartresize) (en jquery-händelse som inträffar en gång efter att fönstret har ändrat storlek)

**Tips!** Du kan automatiskt sammanfoga flera klientbiblioteksmappar genom att [bädda in](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries).

**HTML**

Skapa en komponent som genererar de div-element som förväntas av koden picturefill.js. På en AEM sida är värdet för data-src-attributet sökvägen till en resurs i databasen. En sidkomponent kan till exempel hårdkoda mediefrågor och de associerade sökvägarna för bildåtergivningar i DAM. Du kan också skapa en anpassad bildkomponent som gör att författare kan välja bildåtergivningar eller ange alternativ för körtidsåtergivning.

I följande exempel väljs HTML från två DAM-renderingar av samma bild.

```xml
<div data-picture>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png'></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.319.319.png'    data-media="(min-width: 769px)"></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.140.100.png'   data-media="(min-width: 481px)"></div>
</div>
```

>[!NOTE]
>
>Baskomponenten Adaptive Image implementerar adaptiva bilder:
>
>* Klientbiblioteksmapp: `/libs/foundation/components/adaptiveimage/clientlibs`
>* Skript som genererar HTML: `/libs/foundation/components/adaptiveimage/adaptiveimage.jsp`
>
>Följande avsnitt innehåller information om den här komponenten.
>

### Bildåtergivning i AEM {#understanding-image-rendering-in-aem}

Om du vill anpassa bildåtergivning bör du känna till standardimplementeringen AEM statisk bildåtergivning. AEM innehåller bildkomponenten och en bildåtergivningsservett som fungerar tillsammans för att återge bilder för webbsidor. Följande händelsesekvenser inträffar när bildkomponenten inkluderas i sidans styckesystem:

1. Redigering: Författare redigerar bildkomponenten för att ange vilken bildfil som ska inkluderas på en HTML-sida. Filsökvägen lagras som ett egenskapsvärde för Image-komponentnoden.
1. Sidbegäran: Sidkomponentens JSP genererar HTML-koden. JSP för Image-komponenten genererar och lägger till ett img-element på sidan.
1. Bildbegäran: Webbläsaren läser in sidan och begär bilden enligt img-elementets src-attribut.
1. Bildåtergivning: Bildåtergivningsservern returnerar bilden till webbläsaren.

![chlimage_1-6](assets/chlimage_1-6a.png)

JSP för komponenten Image genererar till exempel följande HTML-element:

`<img title="My Image" alt="My Image" class="cq-dd-image" src="/content/mywebsite/en/_jcr_content/par/image_0.img.jpg/1358372073597.jpg">`

När webbläsaren läser in sidan begär den bilden med hjälp av src-attributets värde som URL. Sling bryter URL-adressen:

* Resurs: `/content/mywebsite/en/_jcr_content/par/image_0`
* Filnamnstillägg: `.jpg`
* Väljare: `img`
* Suffix: `1358372073597.jpg`

Noden `image_0` har värdet `jcr:resourceType`, `foundation/components/image`, som har värdet `sling:resourceSuperType` `foundation/components/parbase`. Parbase-komponenten innehåller skriptet img.GET.java som matchar väljaren och filnamnstillägget för begärande-URL:en. CQ använder det här skriptet (servlet) för att återge bilden.

Använd CRXDE Lite för att öppna `/libs/foundation/components/parbase/img.GET.java` om du vill se skriptets källkod
-fil.

## Skalförändra bilder för den aktuella visningsrutans storlek {#scaling-images-for-the-current-viewport-size}

Skala bilder vid körning enligt egenskaperna för klientens visningsruta för att tillhandahålla bilder som följer principerna för responsiv design. Använd samma designmönster som statisk bildåtergivning, med en servett och en redigeringskomponent.

Komponenten måste utföra följande uppgifter:

* Lagra sökvägen och de önskade dimensionerna för bildresursen som egenskapsvärden.
* Generera `div` element som innehåller medieväljare och serviceanrop för återgivning av bilden.

>[!NOTE]
>
>Webbklienten använder JavaScript-biblioteken matchMedia och Picturefill (eller liknande bibliotek) för att utvärdera medieväljarna.
>

Servern som bearbetar bildbegäran måste utföra följande uppgifter:

* Hämta bildens bana och mått från komponentegenskaperna.
* Skala bilden enligt egenskaperna och returnera bilden.

**Tillgängliga lösningar**

AEM installerar följande implementeringar som du kan använda eller utöka.

* Den adaptiva Image Foundation-komponenten som genererar mediefrågor och HTTP-begäranden till den adaptiva Image Component Server som skalar bilderna.
* Geometrixx Commons-paketet installerar exempelservetterna i Image Reference Modification Servlet som ändrar bildupplösningen.

### Förstå komponenten Adaptiv bild {#understanding-the-adaptive-image-component}

Komponenten Adaptiv bild genererar anrop till adaptiv bildkomponentserver för att återge en bild som har samma storlek som enhetsskärmen. Komponenten innehåller följande resurser:

* JSP: Lägger till div-element som associerar mediefrågor med anrop till Adaptive Image Component Server.
* Klientbibliotek: Mappen clientlibs är en `cq:ClientLibraryFolder` som sätter ihop JavaScript-biblioteket matchMedia polyfill och ett modifierat JavaScript-bibliotek för Picturefill.
* Dialogrutan Redigera: Noden `cq:editConfig` åsidosätter CQ Foundation-bildkomponenten så att släppmålet skapar en adaptiv bildkomponent i stället för en grundläggande bildkomponent.

#### Lägga till DIV-element {#adding-the-div-elements}

Skriptet adaptive-image.jsp innehåller följande kod som genererar div-element och mediefrågor:

```
<div data-picture data-alt='<%= alt %>'>
    <div data-src='<%= path + ".img.320.low." + extension + suffix %>'       data-media="(min-width: 1px)"></div>                                        <%-- Small mobile --%>
    <div data-src='<%= path + ".img.320.medium." + extension + suffix %>'    data-media="(min-width: 320px)"></div>  <%-- Portrait mobile --%>
    <div data-src='<%= path + ".img.480.medium." + extension + suffix %>'    data-media="(min-width: 321px)"></div>  <%-- Landscape mobile --%>
    <div data-src='<%= path + ".img.476.high." + extension + suffix %>'      data-media="(min-width: 481px)"></div>   <%-- Portrait iPad --%>
    <div data-src='<%= path + ".img.620.high." + extension + suffix %>'      data-media="(min-width: 769px)"></div>  <%-- Landscape iPad --%>
    <div data-src='<%= path + ".img.full.high." + extension + suffix %>'     data-media="(min-width: 1025px)"></div> <%-- Desktop --%>

    <%-- Fallback content for non-JS browsers. Same img src as the initial, unqualified source element. --%>
    <noscript>
        <img src='<%= path + ".img.320.low." + extension + suffix %>' alt='<%= alt %>'>
    </noscript>
</div>
```

Variabeln `path` innehåller sökvägen för den aktuella resursen (komponentnoden adaptive-image). Koden genererar en serie med `div` element med följande struktur:

`<div data-scr = "*path-to-parent-node*.adaptive-image.adapt.*width*.*quality*.jpg" data-media="*media query*"></div>`

Värdet för attributet `data-scr` är en URL som Sling löser till den Adaptive Image Component Server som återger bilden. Attributet data-media innehåller den mediefråga som utvärderas mot klientegenskaperna.

Följande HTML-kod är ett exempel på `div`-element som JSP genererar:

```xml
<div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.low.jpg'></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.medium.jpg'    data-media="(min-width: 320px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.480.medium.jpg'    data-media="(min-width: 321px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.476.high.jpg'     data-media="(min-width: 481px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.620.high.jpg'     data-media="(min-width: 769px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.full.high.jpg'     data-media="(min-width: 1025px)"></div>
```

#### Ändra bildstorleksväljare {#changing-the-image-size-selectors}

Om du anpassar den adaptiva bildkomponenten och ändrar breddväljarna måste du även konfigurera den adaptiva bildkomponentservern så att den stöder bredderna.

### Förstå komponentservern för adaptiv bild {#understanding-the-adaptive-image-component-servlet}

Servleten Adaptive Image Component ändrar storlek på en JPEG-bild enligt en angiven bredd och ställer in JPEG-kvaliteten.

#### Gränssnittet för den adaptiva bildkomponentservern {#the-interface-of-the-adaptive-image-component-servlet}

Adaptive Image Component Server är bunden till standardservern Sling och stöder filtilläggen .jpg, .jpeg, .gif och .png. Serverväljaren är img.

>[!CAUTION]
>
>Animerade GIF-filer stöds inte i AEM för adaptiva återgivningar.

Sling löser därför URL:er för HTTP-begäran i följande format till den här servern:

`*path-to-node*.img.*extension*`

Till exempel Sling forwards HTTP-begäranden med URL:en `http://localhost:4502/content/geometrixx/adaptiveImage.img.jpg` till Adaptive Image Component Server.

Två ytterligare väljare anger önskad bildbredd och JPEG-kvalitet. I följande exempel efterfrågas en bild med bredden 480 pixlar och medelkvaliteten:

`http://localhost:4502/content/geometrixx/adaptiveImage.adapt.480.MEDIUM.jpg`

**Bildegenskaper som stöds**

Servern accepterar ett begränsat antal bildbredder och -egenskaper. Följande bredder stöds som standard (i pixlar):

* full
* 320
* 480
* 476
* 620

Det fullständiga värdet anger ingen skalförändring.

Följande värden för JPEG-kvalitet stöds:

* LÅG
* MEDIUM
* HÖG

De numeriska värdena är 0,4, 0,82 och 1,0.

**Ändra standardbredderna som stöds**

Använd webbkonsolen ([http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)) eller en sling:OsgiConfig-nod för att konfigurera bredderna som stöds i Adobe CQ Adaptive Image Component Server.

Mer information om hur du konfigurerar AEM tjänster finns i [Konfigurera OSGi](/help/sites-deploying/configuring-osgi.md).

<table>
 <tbody>
  <tr>
   <th> </th>
   <th>Webbkonsol</th>
   <th>sling:OsgiConfig</th>
  </tr>
  <tr>
   <th>Tjänst- eller nodnamn</th>
   <td>Tjänstnamnet på fliken Konfiguration är Adobe CQ Adaptive Image Component Server</td>
   <td>com.day.cq.wcm.foundation.impl. AdaptiveImageComponentServer</td>
  </tr>
  <tr>
   <th>Egenskap</th>
   <td><p>Bredder som stöds</p>
    <ul>
     <li>Om du vill lägga till en bredd som stöds klickar du på en +-knapp och anger ett positivt heltal.</li>
     <li>Om du vill ta bort en bredd som stöds klickar du på den associerade knappen -.</li>
     <li>Om du vill ändra en bredd som stöds redigerar du fältvärdet.</li>
    </ul> </td>
   <td><p>adapt.supported.widths</p>
    <ul>
     <li>Egenskapen är ett strängvärde med flera värden.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

#### Implementeringsinformation {#implementation-details}

Klassen `com.day.cq.wcm.foundation.impl.AdaptiveImageComponentServlet` utökar klassen [ AbstractImageServlet](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) . Källkoden för AdaptiveImageComponentServer finns i mappen `/libs/foundation/src/impl/src/com/day/cq/wcm/foundation/impl`.

Klassen använder Felix SCR-anteckningar för att konfigurera resurstypen och filtillägget som serverleten är associerad med och namnet på den första väljaren.

```java
@Component(metatype = true, label = "Adobe CQ Adaptive Image Component Servlet",
        description = "Render adaptive images in a variety of qualities")
@Service
@Properties(value = {
    @Property(name = "sling.servlet.resourceTypes", value = "foundation/components/adaptiveimage", propertyPrivate = true),
    @Property(name = "sling.servlet.selectors", value = "img", propertyPrivate = true),
    @Property(name = "sling.servlet.extensions", value ={
            "jpg",
            "jpeg",
            "png",
            "gif"
    }, propertyPrivate = true)
})
```

Servottleten använder Property SCR-anteckningen för att ange bildkvalitet och dimensioner som stöds som standard.

```java
@Property(value = {
            "320", // iPhone portrait
            "480", // iPhone landscape
            "476", // iPad portrait
            "620" // iPad landscape
    },
            label = "Supported Widths",
            description = "List of widths this component is permitted to generate.")
```

Klassen `AbstractImageServlet` innehåller metoden `doGet` som bearbetar HTTP-begäran. Den här metoden avgör vilken resurs som är associerad med begäran, hämtar resursegenskaper från databasen och returnerar dem i ett [ImageContext](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html) -objekt.

>[!NOTE]
>
>Klassen [com.day.cq.commons.DownloadResource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/DownloadResource.html) innehåller `getFileReference method`, som hämtar värdet för resursens `fileReference`-egenskap.

Klassen `AdaptiveImageComponentServlet` åsidosätter metoden `createLayer`. Metoden hämtar sökvägen för bildresursen och den begärda bildbredden från objektet `ImageContext`. Därefter anropas metoderna för klassen `info.geometrixx.commons.impl.AdaptiveImageHelper` som utför den faktiska bildskalningen.

Klassen AdaptiveImageComponentServer åsidosätter också writeLayer-metoden. Med den här metoden används bildens JPEG-kvalitet.

### Image Reference Modification Server (Geometrixx Common) {#image-reference-modification-servlet-geometrixx-common}

Exemplet Image Reference Modification Server genererar storleksattribut för img-elementet för att skala en bild på webbsidan.

#### Anropa serverleten {#calling-the-servlet}

Servern är bunden till `cq:page` resurser och stöder filtillägget .jpg. Serverväljaren är `image`. Sling löser därför URL:er för HTTP-begäran i följande format till den här servern:

`path-to-page-node.image.jpg`

Exempel: Sling vidarebefordrar HTTP-begäranden med URL:en `http://localhost:4502/content/geometrixx/en.image.jpg` till Image Reference Modification Server.

Tre ytterligare väljare anger den önskade bildens bredd, höjd och (valfritt) kvalitet. I följande exempel efterfrågas en bild med bredden 770 pixlar, höjden 360 pixlar och medelkvaliteten.

`http://localhost:4502/content/geometrixx/en.image.770.360.MEDIUM.jpg`

**Bildegenskaper som stöds**

Servern accepterar ett begränsat antal bilddimensioner och kvalitetsvärden.

Följande värden stöds som standard (widthXheight):

* 256x192
* 370x150
* 480x200
* 127x127
* 770x360
* 620x290
* 480x225
* 320x150
* 375x175
* 303x142
* 1170x400
* 940x340
* 770x300
* 480x190

Följande värden för bildkvalitet stöds:

* låg
* medium
* hög

När du arbetar med AEM finns det flera metoder för att hantera konfigurationsinställningarna för sådana tjänster. Mer information finns i [Konfigurera OSGi](/help/sites-deploying/configuring-osgi.md).

#### Ange bildresursen {#specifying-the-image-resource}

Bildsökvägen, dimensionerna och kvalitetsvärdena måste lagras som egenskaper för en nod i databasen:

* Nodnamnet är `image`.
* Den överordnade noden är `jcr:content`-noden för en `cq:page`-resurs.

* Bildsökvägen lagras som värdet för egenskapen `fileReference`.

När du redigerar en sida använder du **Sidekick** för att ange bilden och lägga till noden `image` i sidegenskaperna:

1. I **Sidekick** klickar du på fliken **Sida** och sedan på **Sidegenskaper**.
1. Klicka på fliken **Bild** och ange bilden.
1. Klicka på **OK**.

#### Implementeringsinformation {#implementation-details-1}

Klassen info.geometrixx.Commons.impl.servlets.ImageReferenceModificationServlet utökar klassen [AbstractImageServlet](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html). Om du har installerat paketet cq-geometrixx-Commons-pkg finns källkoden för ImageReferenceModificationServlet i mappen `/apps/geometrixx-commons/src/core/src/main/java/info/geometrixx/commons/impl/servlets`.

Klassen använder Felix SCR-anteckningar för att konfigurera resurstypen och filtillägget som serverleten är associerad med och namnet på den första väljaren.

```java
@Component(metatype = true, label = "Adobe CQ Image Reference Modification Servlet",
        description = "Render the image associated with a page in a variety of dimensions and qualities")
@Service
@Properties(value = {
    @Property(name = "sling.servlet.resourceTypes", value = NameConstants.NT_PAGE, propertyPrivate = true),
    @Property(name = "sling.servlet.selectors", value = "image", propertyPrivate = true),
    @Property(name = "sling.servlet.extensions", value = "jpg", propertyPrivate = true)
})
```

Servottleten använder Property SCR-anteckningen för att ange bildkvalitet och dimensioner som stöds som standard.

```java
@Property(label = "Image Quality",
            description = "Quality must be a double between 0.0 and 1.0", value = "0.82")
@Property(value = {
                "256x192", // Category page article list images
                "370x150", // "Most popular" desktop & iPad & carousel min-width: 1px
                "480x200", // "Most popular" phone
                "127x127", // article summary phone square images
                "770x360", // article summary, desktop
                "620x290", // article summary, tablet
                "480x225", // article summary, phone (landscape)
                "320x150", // article summary, phone (portrait) and fallback
                "375x175", // 2-column article summary, desktop
                "303x142", // 2-column article summary, tablet
                "1170x400", // carousel, full
                "940x340",  // carousel min-width: 980px
                "770x300",  // carousel min-width: 768px
                "480x190"   // carousel min-width: 480px
            },
            label = "Supported Resolutions",
            description = "List of resolutions this component is permitted to generate.")
```

Klassen `AbstractImageServlet` innehåller metoden `doGet` som bearbetar HTTP-begäran. Den här metoden avgör vilken resurs som är associerad med anropet, hämtar resursegenskaper från databasen och sparar dem i ett [ImageContext](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html) -objekt.

Klassen `ImageReferenceModificationServlet` åsidosätter metoden `createLayer` och implementerar logiken som bestämmer vilken bildresurs som ska återges. Metoden hämtar en underordnad nod till sidans `jcr:content`-nod med namnet `image`. Ett [Bild](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/foundation/Image.html)-objekt skapas från den här `image`-noden och metoden `getFileReference` returnerar sökvägen till bildfilen från bildnodens `fileReference`-egenskap.

>[!NOTE]
>Klassen [com.day.cq.commons.DownloadResource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/DownloadResource.html) innehåller metoden getFileReference.
>

## Utveckla ett flytande stödraster {#developing-a-fluid-grid}

AEM gör det möjligt att effektivt implementera flytande stödraster. På den här sidan beskrivs hur du kan integrera ditt flytande stödraster eller en befintlig stödrasterimplementering (till exempel [Bootstrap](https://github.com/topics/twitter-bootstrap?l=css)) i ditt AEM.

Om du inte känner till flytande stödraster läser du avsnittet [Introduktion till flytande stödraster](/help/sites-developing/responsive.md#developing-a-fluid-grid) längst ned på den här sidan. Den här introduktionen ger en översikt över flytande stödraster och riktlinjer för hur du utformar dem.

### Definiera stödrastret med en sidkomponent {#defining-the-grid-using-a-page-component}

Använd sidkomponenter för att generera de element i HTML som definierar innehållsblocken på sidan. ClientLibraryFolder som sidreferensen refererar till innehåller CSS som styr layouten för innehållsblocken:

* Sidkomponent: Lägger till div-element som representerar rader med innehållsblock. De div-element som representerar innehållsblock innehåller en parsyskomponent där författare lägger till innehåll.
* Klientbiblioteksmapp: Tillhandahåller CSS-filen som innehåller mediefrågor och format för div-elementen.

Exempelprogrammet för geometrixx-media innehåller exempelvis mediahemkomponenten. Den här sidkomponenten infogar två skript som genererar två `div` element av klassen `row-fluid`:

* Den första raden innehåller ett `div`-element av klassen `span12` (innehållet omfattar 12 kolumner). Elementet `div` innehåller parsys-komponenten.

* Den andra raden innehåller två `div`-element, den ena av klassen `span8` och den andra av klassen `span4`. Varje `div`-element innehåller parsys-komponenten.

```xml
<div class="page-content">
    <div class="row-fluid">
        <div class="span12">
            <cq:include path="grid-12-par" resourceType="foundation/components/parsys" />
        </div>
    </div>
    <div class="row-fluid">
        <div class="span8">
            <cq:include path="grid-8-par" resourceType="foundation/components/parsys" />
        </div>
        <div class="span4">
            <cq:include path="grid-4-par" resourceType="foundation/components/parsys" />
        </div>
    </div>
</div>
```

>[!NOTE]
>
>När en komponent innehåller flera `cq:include`-element som refererar till den parsys-komponenten, måste varje `path`-attribut ha ett annat värde.
>

#### Skalförändra sidkomponentens stödraster {#scaling-the-page-component-grid}

Designen som är associerad med sidkomponenten geometrixx-media (`/etc/designs/geometrixx-media`) innehåller `clientlibs` ClientLibraryFolder. Den här ClientLibraryFolder definierar CSS-format för `row-fluid`-klasser, `span*`-klasser och `span*`-klasser som är underordnade `row-fluid`-klasser. Mediefrågor gör att format kan definieras om för olika visningsrutestorlekar.

Följande exempel på CSS är en deluppsättning av dessa format. Den här delmängden fokuserar på klasserna `span12`, `span8` och `span4` samt på mediefrågor för två visningsrutestorlekar. Observera följande egenskaper för CSS:

* `.span`-formaten definierar elementbredder med absoluta tal.
* `.row-fluid .span*`-formaten definierar elementbredder som procentandelar av det överordnade objektet. Procenttal beräknas utifrån de absoluta bredderna.
* Mediefrågor för större visningsrutor tilldelar större absoluta bredder.

>[!NOTE]
>
>Geometrixx Media-exemplet integrerar JavaScript-ramverket [Bootstrap](https://getbootstrap.com/2.0.2/) med dess flytande stödrasterimplementering. Ramverket Bootstrap innehåller filen bootstrap.css.

```xml
/* default styles (no media queries) */
 .span12 { width: 940px }
 .span8 { width: 620px }
 .span4 { width: 300px }
 .row-fluid .span12 { width: 100% }
 .row-fluid .span8 { width: 65.95744680851064% }
 .row-fluid .span4 { width: 31.914893617021278% }

@media (min-width: 768px) and (max-width: 979px) {
 .span12 { width: 724px; }
 .span8 {     width: 476px; }
 .span4 {     width: 228px; }
 .row-fluid .span12 {     width: 100%;}
 .row-fluid .span8 {     width: 65.74585635359117%; }
 .row-fluid .span4 {     width: 31.491712707182323%; }
}

@media (min-width: 1200px) {
 .span12 { width: 1170px }
 .span8 { width: 770px }
 .span4 { width: 370px }
 .row-fluid .span12 { width: 100% }
 .row-fluid .span8 { width: 65.81196581196582% }
 .row-fluid .span4 { width: 31.623931623931625% }
}
```

#### Flytta innehåll i sidkomponentens stödraster {#repositioning-content-in-the-page-component-grid}

Geometrixx Medias exempelsidor distribuerar innehållsblockrader vågrätt i breda visningsrutor. I mindre visningsrutor fördelas samma block lodrätt. I följande exempel visas CSS-formaten som implementerar det här beteendet för HTML-koden som genereras av sidkomponenten media-home:

* CSS-standardformatet för sidan mediavälkomstsida tilldelar formatet `float:left` för `span*` -klasser som finns inuti `row-fluid` -klasser.

* Mediefrågor för mindre visningsrutor tilldelar formatet `float:none` för samma klasser.

```xml
/* default styles (no media queries) */
    .row-fluid [class*="span"] {
        width: 100%;
        float: left;
}

@media (max-width: 767px) {
    [class*="span"], .row-fluid [class*="span"] {
        float: none;
        width: 100%;
    }
}
```

#### Modularisera sidkomponenterna {#tip-modularize-your-page-components}

Modularisera komponenterna så att du kan använda koden effektivt. På webbplatsen används förmodligen flera olika typer av sidor, som välkomstsidor, artikelsidor eller produktsidor. Varje sidtyp innehåller olika typer av innehåll och använder troligen olika layouter. Men om vissa element i varje layout är gemensamma för flera sidor kan du återanvända koden som implementerar den delen av layouten.

**Använd sidkomponentövertäckningar**

Skapa en huvudsideskomponent som innehåller skript för generering av olika delar av en sida, till exempel `head` och `body` avsnitt samt `header`, `content` och `footer` avsnitt i brödtexten.

Skapa andra sidkomponenter som använder huvudsidkomponenten som `cq:resourceSuperType`. Dessa komponenter innehåller skript som åsidosätter skripten på huvudsidan efter behov.

Till exempel innehåller goemetrixx-media-programmet sidkomponenten (`sling:resourceSuperType` är bassidans komponent). Flera underordnade komponenter (som artikel, kategori och media-home) använder den här sidkomponenten som `sling:resourceSuperType`. Varje underordnad komponent innehåller en content.jsp-fil som åsidosätter content.jsp-filen för sidkomponenten.

**Återanvänd skript**

Skapa flera JSP-skript som genererar rad- och kolumnkombinationer som är gemensamma för flera sidkomponenter. Skriptet `content.jsp` för artikeln och mediahemskomponenterna refererar till exempel båda till skriptet `8x4col.jsp`.

**Ordna CSS-format efter visningsrutans målstorlek**

Inkludera CSS-format och mediefrågor för olika visningsrutor i separata filer. Använd klientbiblioteksmappar för att sammanfoga dem.

### Infoga komponenter i sidstödrastret {#inserting-components-into-the-page-grid}

När komponenter genererar ett enda innehållsblock styr vanligtvis stödrastret som sidkomponenten skapar innehållets placering.

Som författare kan innehållsblocket återges i olika storlekar och relativa positioner. Innehållstext ska inte använda relativa riktningar för att referera till andra innehållsblock.

Om det behövs ska komponenten tillhandahålla alla CSS- eller JavaScript-bibliotek som krävs för den HTML-kod som den genererar. Använd en klientbiblioteksmapp inuti komponenten så att CSS- och JS-filerna genereras. Om du vill visa filerna skapar [du ett beroende eller bäddar in biblioteket](/help/sites-developing/clientlibs.md#creating-client-library-folders) i en annan klientbiblioteksmapp under mappen /etc.

**Underrutnät**

Om komponenten innehåller flera innehållsblock lägger du till innehållsblocken i en rad för att skapa ett underrutnät på sidan:

* Använd samma klassnamn som den innehållande sidkomponenten så att du kan uttrycka div-element som rader och innehållsblock.
* Om du vill åsidosätta beteendet som siddesignens CSS implementerar använder du ett andra klassnamn för rad-div-elementet och anger tillhörande CSS i en klientbiblioteksmapp.

Komponenten `/apps/geometrixx-media/components/2-col-article-summary` genererar till exempel två kolumner med innehåll. HTML som genereras har följande struktur:

```xml
<div class="row-fluid mutli-col-article-summary">
    <div class="span6">
        <article>
            <div class="article-summary-image">...</div>
            <div class="social-header">...</div>
            <div class="article-summary-description">...</div>
            <div class="social">...</div>
        </article>
    </div>
</div>
```

`.row-fluid .span6`-väljarna för sidans CSS gäller för `div`-elementen i samma klass och struktur i den här HTML. Komponenten innehåller dock även klientbiblioteksmappen /apps/geometrixx-media/components/2-col-article-summary/clientlibs:

* CSS använder samma mediefrågor som sidkomponenten för att skapa ändringar i layouten med samma diskreta sidbredder.
* Väljare använder klassen `multi-col-article-summary` i elementet row `div` för att åsidosätta beteendet för sidans `row-fluid`-klass.

Följande format ingår till exempel i filen `/apps/geometrixx-media/components/2-col-article-summary/clientlibs/css/responsive-480px.css`:

```xml
@media (max-width: 480px) {
    .mutli-col-article-summary .article-summary-image {
        float: left;
        width: 127px;
    }
    .mutli-col-article-summary .article-summary-description {
        width: auto;
        margin-left: 127px;
    }
    .mutli-col-article-summary .article-summary-description h4 {
        padding-left: 10px;
    }
    .mutli-col-article-summary .article-summary-text {
        margin-left: 127px;
        min-height: 122px;
        top: 0;
    }
}
```

## Introduktion till flytande stödraster {#introduction-to-fluid-grids}

Med flytande stödraster kan sidlayouter anpassas efter kundens visningsruta. Stödraster består av logiska kolumner och rader som placerar innehållsblocken på sidan.

* Kolumner bestämmer de vågräta placeringarna och bredderna för innehållsblocken.
* Rader bestämmer de relativa lodräta positionerna för innehållsblocken.

Med HTML5-tekniken kan du implementera rutnätet och ändra det för att anpassa sidlayouter till olika visningsrutestorlekar:

* HTML `div`-element innehåller innehållsblock som sträcker sig över vissa kolumner.
* Ett eller flera av dessa div-element består av en rad när de delar ett gemensamt överordnat div-element.

### Använda diskreta bredder {#using-discrete-widths}

Använd en statisk sidbredd och innehållsblock med konstant bredd för varje intervall av visningsrutor som du anger som mål. När du ändrar storlek på ett webbläsarfönster manuellt ändras innehållsstorleken vid olika fönsterbredder (kallas även brytpunkter). Därför följs siddesignen närmare, vilket maximerar användarupplevelsen.

#### Skalförändra stödrastret {#scaling-the-grid}

Använd rutnät för att skala innehållsblock så att de anpassas till olika visningsrutestorlekar. Innehållsblock sträcker sig över ett visst antal kolumner. När kolumnbredderna ökar eller minskar för att passa olika visningsrutestorlekar, ökar eller minskar bredderna för innehållsblocken därefter. Skalning kan stödja både stora och medelstora visningsrutor som är tillräckligt breda för att rymma innehållsblockens placering sida vid sida.

![Bild av två stödraster, den ena som är mindre än den andra.](do-not-localize/chlimage_1-1a.png)

#### Flytta innehåll i stödrastret {#repositioning-content-in-the-grid}

Storleken på innehållsblock kan begränsas av en minsta bredd, bortom vilken skalningen inte längre är effektiv. För mindre visningsrutor kan stödrastret användas för att lodrätt distribuera innehållsblock i stället för vågrätt.

![Bild av två stödraster, den ena som är placerad mindre än den andra.](do-not-localize/chlimage_1-2a.png)

### Utforma stödrastret {#designing-the-grid}

Ange vilka kolumner och rader som du måste placera innehållsblocken på sidorna. Sidlayouterna bestämmer hur många kolumner och rader som spänner över stödrastret.

**Antal kolumner**

Inkludera tillräckligt många kolumner för att vågrätt placera innehållsblocken i alla dina layouter, för alla visningsrutestorlekar. Använd fler kolumner än vad som behövs för att få plats med framtida siddesign.

**Radinnehåll**

Använd rader för att styra den lodräta placeringen av innehållsblock. Bestäm vilka innehållsblock som delar samma rad:

* Innehållsblock som placeras intill varandra vågrätt i någon av layouterna finns på samma rad.
* Innehållsblock som finns bredvid varandra vågrätt (bredare visningsrutor) och lodrätt (mindre visningsrutor) placeras på samma rad.

### Implementeringar av stödraster {#grid-implementations}

Skapa CSS-klasser och format så att du kan styra layouten för innehållsblocken på en sida. Siddesignen baseras ofta på den relativa storleken och placeringen av innehållsblocken i visningsrutan. Visningsrutan avgör den faktiska storleken på innehållsblocken. CSS måste ta hänsyn till de relativa och absoluta storlekarna. Du kan implementera ett flytande stödraster med hjälp av tre typer av CSS-klasser:

* En klass för ett `div`-element som är en behållare för alla rader. Den här klassen anger stödrastrets absoluta bredd.
* En klass för `div` element som representerar en rad. Den här klassen styr den vågräta eller lodräta placeringen av innehållsblocken som den innehåller.
* Klasser för `div` element som representerar innehållsblock med olika bredder. Bredder anges i procent för det överordnade objektet (raden).

Målbredder (och tillhörande mediefrågor) avgränsar olika bredder som används för en sidlayout.

#### Bredder på innehållsblock {#widths-of-content-blocks}

I allmänhet baseras `width`-formaten för innehållsblockklasserna på följande egenskaper för sidan och stödrastret:

* Den absoluta sidbredd som du använder för varje avsedd visningsportstorlek. Kända värden.
* Den absoluta bredden på stödrasterkolumnerna för varje sidbredd. Du bestämmer dessa värden.
* Den relativa bredden för varje kolumn som en procentandel av den totala sidbredden. Du beräknar dessa värden.

CSS innehåller en serie mediefrågor som använder följande struktur:

```xml
@media(query_for_targeted_viewport){

  .class_for_container{ width:absolute_page_width }
  .class_for_row { width:100%}

  /* several selectors for content blocks   */
  .class_for_content_block1 { width:absolute_block_width1 }
  .class_for_content_block2 { width:absolute_block_width2 }
  ...

  /* several selectors for content blocks inside rows */
  .class_for_row .class_for_content_block1 { width:relative_block_width1 }
  .class_for_row .class_for_content_block2 { width:relative_block_width2 }
  ...
}
```

Använd följande algoritm som utgångspunkt när du utvecklar elementklasser och CSS-format för sidorna.

1. Definiera ett klassnamn för div-elementet som innehåller alla rader, till exempel `content.`
1. Definiera en CSS-klass för div-element som representerar rader, till exempel `row-fluid`.
1. Definiera klassnamn för innehållsblockelement. En klass krävs för alla möjliga bredder, vad gäller kolumnintervall. Använd till exempel klassen `span3` för `div`-element som sträcker sig över tre kolumner, använd `span4`-klasser för intervall om fyra kolumner. Definiera så många klasser som det finns kolumner i rutnätet.

1. För varje visningsrutestorlek som du anger som mål lägger du till motsvarande mediefråga i CSS-filen. Lägg till följande objekt i varje mediefråga:

   * En väljare för klassen `content`, till exempel `.content{}`.
   * Väljare för varje intervallklass, till exempel `.span3{ }`.
   * En väljare för klassen `row-fluid`, till exempel `.row-fluid{ }`
   * Väljare för intervallklasser som finns inuti klasser för radflykt, till exempel `.row-fluid span3 { }`.

1. Lägg till breddformat för varje väljare:

   1. Ange bredden för `content` väljare till den absoluta sidstorleken, till exempel `width:480px`.
   1. Ställ in bredden för alla väljare för radvätskor till 100 %.
   1. Ange bredden för alla intervallväljare till innehållsblockets absoluta bredd. Ett trivialt rutnät använder jämnt fördelade kolumner med samma bredd: `(absolute width of page)/(number of columns)`.
   1. Ange bredden för `.row-fluid .span` väljare som en procentandel av den totala bredden. Beräkna den här bredden med formeln `(absolute span width)/(absolute page width)*100`.

#### Placera innehållsblock i rader {#positioning-content-blocks-in-rows}

Använd det flytande formatet för klassen `.row-fluid` så att du kan kontrollera om innehållsblocken i en rad är ordnade vågrätt eller lodrätt.

* Stilen `float:left` eller `float:right` skapar den vågräta fördelningen av underordnade element (innehållsblock).

* Stilen `float:none` orsakar en lodrät fördelning av underordnade element.

Lägg till formatet i `.row-fluid`-väljaren i varje mediefråga. Ange värdet enligt den sidlayout som du använder för den mediefrågan. I följande diagram visas en rad som fördelar innehållet vågrätt för breda visningsrutor och lodrätt för smala visningsrutor.

![Två bilder av innehållsblock i en rad, den andra bilden med raden flyttad.](do-not-localize/chlimage_1-3a.png)

Följande CSS kan implementera detta beteende:

```xml
@media (min-width: 768px) and (max-width: 979px) {
   .row-fluid {
       width:100%;
       float:left
   }
}

@media (max-width:480px){
    .row-fluid {
       width:100%;
       float:none
   }
}
```

#### Tilldela klasser till innehållsblock {#assigning-classes-to-content-blocks}

För sidlayouten för varje visningsrutestorlek som du anger, bestämmer du antalet kolumner som varje innehållsblock omfattar. Bestäm sedan vilken klass som ska användas för div-elementen i dessa innehållsblock.

När du har etablerat div-klasserna kan du implementera rutnätet med ditt AEM program.
