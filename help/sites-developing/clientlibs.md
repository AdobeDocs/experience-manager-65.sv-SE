---
title: Använda bibliotek på klientsidan
seo-title: Using Client-Side Libraries
description: AEM tillhandahåller biblioteksmappar på klientsidan, som gör att du kan lagra klientsidans kod i databasen, ordna den i kategorier och definiera när och hur varje kodkategori ska skickas till klienten
seo-description: AEM provides Client-side Library Folders, which allow you to store your client-side code in the repository, organize it into categories, and define when and how each category of code is to be served to the client
uuid: f12b13cc-6651-4c9a-9c52-19a22bb82b28
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 3d14837d-41a8-480a-83ba-392e32f84c65
docset: aem65
exl-id: 408ac30c-60ab-4d6c-855c-d544af8d5cf9
source-git-commit: 4789b2b5105e5a883ab816c82c9ff07ea76978ff
workflow-type: tm+mt
source-wordcount: '2848'
ht-degree: 0%

---

# Använda bibliotek på klientsidan{#using-client-side-libraries}

Moderna webbplatser är starkt beroende av bearbetning på klientsidan som styrs av komplex JavaScript- och CSS-kod. Det kan vara komplicerat att organisera och optimera serveringen av koden.

AEM tillhandahåller **Biblioteksmappar på klientsidan**, som gör att du kan lagra din klientkod i databasen, ordna den i kategorier och definiera när och hur varje kodkategori ska skickas till klienten. Klientsidans bibliotekssystem tar sedan hand om att skapa rätt länkar på den slutliga webbsidan för att läsa in rätt kod.

## Hur klientbibliotek fungerar i AEM {#how-client-side-libraries-work-in-aem}

Standardsättet att inkludera ett klientbibliotek (dvs. en JS- eller CSS-fil) HTML på en sida är att bara inkludera en `<script>` eller `<link>` -taggen i JSP för den sidan, som innehåller sökvägen till filen i fråga. Till exempel,

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

Detta tillvägagångssätt fungerar i AEM, men kan leda till problem när sidor och deras beståndsdelar blir komplexa. I sådana fall finns det en risk för att flera exemplar av samma JS-bibliotek kan ingå i den slutliga utskriften för HTML. För att undvika detta och för att tillåta logisk organisering av klientbibliotek AEM använder **biblioteksmappar på klientsidan**.

En biblioteksmapp på klientsidan är en databasnod av typen `cq:ClientLibraryFolder`. Det är en definition i [CND-notation](https://jackrabbit.apache.org/node-type-notation.html) är

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

Som standard `cq:ClientLibraryFolder` kan placeras var som helst i `/apps`, `/libs` och `/etc` underträd i databasen (dessa standardinställningar och andra inställningar kan styras via **Bibliotekshanteraren Adobe Granite HTML** panelen [Systemkonsol](https://localhost:4502/system/console/configMgr)).

Varje `cq:ClientLibraryFolder` innehåller en uppsättning JS- och/eller CSS-filer, tillsammans med några stödfiler (se nedan). Egenskaperna för `cq:ClientLibraryFolder` är konfigurerade enligt följande:

* `categories`: Identifierar de kategorier i vilka uppsättningen JS- och/eller CSS-filer i den här `cq:ClientLibraryFolder` höst. The `categories` eftersom en biblioteksmapp är flervärdesdel kan den ingå i mer än en kategori (se nedan hur detta kan vara användbart).

* `dependencies`: Det här är en lista över andra klientbibliotekskategorier som den här biblioteksmappen är beroende av. Anges till exempel två `cq:ClientLibraryFolder` noder `F` och `G`, om det finns en fil i `F` kräver en annan fil i `G` för att fungera på rätt sätt måste minst en av `categories` av `G` ska vara bland `dependencies` av `F`.

* `embed`: Används för att bädda in kod från andra bibliotek. Om nod F bäddar in noderna G och H blir HTML en koncentration av innehållet från noderna G och H.
* `allowProxy`: Om ett klientbibliotek finns under `/apps`, tillåter den här egenskapen åtkomst till den via en proxyserver. Se [Hitta en klientbiblioteksmapp och använda servern för proxyklientbibliotek](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) nedan.

## Referera till bibliotek på klientsidan {#referencing-client-side-libraries}

Eftersom HTML är den rekommenderade tekniken för att utveckla AEM webbplatser bör HTML användas för att inkludera klientbibliotek i AEM. Det går dock även att göra det med JSP.

### Använda HTML {#using-htl}

I HTML läses klientbibliotek in via en hjälpmall från AEM, som du kommer åt via [ `data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use). Det finns tre tillgängliga mallar i den här filen som du kan anropa genom [ `data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call):

* **css** - Läser bara in CSS-filerna för de refererade klientbiblioteken.
* **js** - Läser bara in JavaScript-filer från de refererade klientbiblioteken.
* **alla** - Läser in alla filer i de refererade klientbiblioteken (både CSS och JavaScript).

Varje hjälpmall förväntar sig en `categories` för att referera till önskade klientbibliotek. Det alternativet kan antingen vara en array med strängvärden eller en sträng som innehåller en kommaseparerad värdelista.

Mer information och exempel på användning finns i dokumentet [Komma igång med mallspråket HTML](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries).

### Använda JSP {#using-jsp}

Lägg till en `ui:includeClientLib` lägga till en länk till klientbibliotek på den genererade HTML-sidan i JSP-koden. Om du vill referera till biblioteken använder du värdet för `categories` egenskapen för `ui:includeClientLib` nod.

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

Till exempel `/etc/clientlibs/foundation/jquery` noden är av typen `cq:ClientLibraryFolder` med en kategoriegenskap för värde `cq.jquery`. Följande kod i en JSP-fil refererar till biblioteken:

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

Den genererade HTML-sidan innehåller följande kod:

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

Fullständig information, inklusive attribut för filtrering av JS-, CSS- eller temabibliotek finns i [ui:includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib).

>[!CAUTION]
>
>`<cq:includeClientLib>`, som tidigare ofta användes för att inkludera klientbibliotek, har tagits bort sedan AEM 5.6. [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) ska användas i stället så som beskrivs ovan.

## Skapar klientbiblioteksmappar {#creating-client-library-folders}

Skapa en `cq:ClientLibraryFolder` för att definiera JavaScript- och Cascading Style Sheet-bibliotek och göra dem tillgängliga för HTML-sidor. Använd `categories` för noden för att identifiera de bibliotekskategorier som den tillhör.

Noden innehåller en eller flera källfiler som vid körning sammanfogas till en enda JS- och/eller CSS-fil. Den genererade filens namn är nodnamnet med antingen `.js` eller `.css` filnamnstillägg. Biblioteksnoden med namnet `cq.jquery` resultat i den genererade filen med namnet `cq.jquery.js` eller `cq.jquery.css`.

Klientbiblioteksmappar innehåller följande objekt:

* JS- och/eller CSS-källfilerna som ska sammanfogas.
* Resurser som stöder CSS-format, t.ex. bildfiler.

   **Obs!** Du kan använda undermappar för att ordna källfiler.
* Ett `js.txt` fil och/eller en `css.txt` som identifierar de källfiler som ska sammanfogas i de genererade JS- och/eller CSS-filerna.

![clientlibarch](assets/clientlibarch.png)

Mer information om krav som är specifika för klientbibliotek för widgetar finns i [Använda och utöka widgetar](/help/sites-developing/widgets.md).

Webbklienten måste ha behörighet att komma åt `cq:ClientLibraryFolder` nod. Du kan också visa bibliotek från skyddade områden i databasen (se Inbädda kod från andra bibliotek nedan).

### Åsidosätta bibliotek i /lib {#overriding-libraries-in-lib}

Klientbiblioteksmappar som finns nedan `/apps` har företräde framför mappar med samma namn som finns i `/libs`. Till exempel: `/apps/cq/ui/widgets` har företräde framför `/libs/cq/ui/widgets`. När dessa bibliotek tillhör samma kategori visas biblioteket nedan `/apps` används.

### Hitta en klientbiblioteksmapp och använda servern för proxyklientbibliotek {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

I tidigare versioner fanns klientbiblioteksmapparna nedan `/etc/clientlibs` i databasen. Detta stöds fortfarande, men vi rekommenderar att klientbibliotek nu finns under `/apps`. Det här är för att hitta klientbiblioteken nära de andra skripten, som beskrivs nedan `/apps` och `/libs`.

>[!NOTE]
>
>Statiska resurser under klientbiblioteksmappen måste finnas i en mapp som kallas *resurser*. Om du inte har statiska resurser, till exempel bilder, under mappen *resurser* kan det inte refereras till i en publiceringsinstans. Här är ett exempel: https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>För att kunna isolera kod från innehåll och konfiguration rekommenderar vi att du letar upp klientbibliotek under `/apps` och visa dem via `/etc.clientlibs` genom att använda `allowProxy` -egenskap.

I ordning för klientbiblioteken under `/apps` För att vara tillgänglig används en proxyserver. Åtkomstkontrollistorna används fortfarande i klientbiblioteksmappen, men med den kan innehållet läsas via `/etc.clientlibs/` om `allowProxy` egenskapen är inställd på `true`.

En statisk resurs kan bara nås via proxyn om den finns under en resurs under klientbiblioteksmappen.

Exempel:

* Du har en klientlib i `/apps/myproject/clientlibs/foo`
* Du har en statisk bild i `/apps/myprojects/clientlibs/foo/resources/icon.png`

Sedan ställer du in `allowProxy` egenskap på `foo` till true.

* Du kan sedan begära `/etc.clientlibs/myprojects/clientlibs/foo.js`
* Sedan kan du referera till bilden via `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

>[!CAUTION]
>
>När du använder proxiderade klientbibliotek kan konfigurationen för AEM Dispatcher kräva en uppdatering för att säkerställa att URI:er med tilläggets klienter tillåts.

>[!CAUTION]
>
>Adobe rekommenderar att du hittar klientbibliotek under `/apps` och göra dem tillgängliga med proxyservern. Tänk dock på att bästa praxis fortfarande kräver att offentliga webbplatser aldrig innehåller något som serveras direkt via en `/apps` eller `/libs` bana.

### Skapa en biblioteksmapp för klient {#create-a-client-library-folder}

1. Öppna CRXDE Lite i en webbläsare ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Markera mappen där du vill leta upp klientbiblioteksmappen och klicka på **Skapa > Skapa nod**.
1. Ange ett namn för biblioteksfilen och välj `cq:ClientLibraryFolder`. Klicka **OK** och sedan klicka **Spara alla**.
1. Om du vill ange den eller de kategorier som biblioteket tillhör väljer du `cq:ClientLibraryFolder` lägg till följande egenskap och klicka sedan på **Spara alla**:

   * Namn: kategorier
   * Typ: Sträng
   * Värde: Kategorinamnet
   * Flera: Välj

1. Lägg till källfiler i biblioteksmappen på alla sätt. Använd till exempel en WebDav-klient för att kopiera filer, eller skapa en fil och redigera innehållet manuellt.

   **Obs!** Du kan ordna källfiler i undermappar om du vill.

1. Markera klientbiblioteksmappen och klicka på **Skapa > Skapa fil**.
1. Skriv något av följande filnamn i rutan Filnamn och klicka på OK:

   * **`js.txt`:** Använd det här filnamnet för att generera en JavaScript-fil.
   * **`css.txt`:** Använd det här filnamnet för att generera en CSS (Cascading Style Sheet).

1. Öppna filen och skriv följande text för att identifiera källfilernas rot:

   `#base=*[root]*`

   Ersätt * `[root]`* med sökvägen till mappen som innehåller källfilerna i förhållande till TXT-filen. Använd till exempel följande text när källfilerna finns i samma mapp som TXT-filen:

   `#base=.`

   Följande kod anger roten som mappen mobile under `cq:ClientLibraryFolder` nod:

   `#base=mobile`

1. På raderna nedan `#base=[root]`anger du sökvägarna för källfilerna i förhållande till roten. Placera varje filnamn på en separat rad.
1. Klicka **Spara alla**.

### Länka till beroenden {#linking-to-dependencies}

När koden i klientbiblioteksmappen refererar till andra bibliotek identifierar du de andra biblioteken som beroenden. I JSP:n `ui:includeClientLib` -taggen som refererar till din klientbiblioteksmapp gör att HTML-koden innehåller en länk till den biblioteksfil som genereras samt beroenden.

Beroenden måste vara ett annat `cq:ClientLibraryFolder`. Om du vill identifiera beroenden lägger du till en egenskap i `cq:ClientLibraryFolder` nod med följande attribut:

* **Namn:** beroenden
* **Typ:** Sträng[]
* **Värden:** Värdet på egenskapen categories för den cq:ClientLibraryFolder-nod som den aktuella biblioteksmappen är beroende av.

Till exempel är / `etc/clientlibs/myclientlibs/publicmain` är beroende av `cq.jquery` bibliotek. Den JSP som refererar till huvudklientbiblioteket genererar HTML som innehåller följande kod:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Bädda in kod från andra bibliotek {#embedding-code-from-other-libraries}

Du kan bädda in kod från ett klientbibliotek i ett annat klientbibliotek. Vid körning innehåller de genererade JS- och CSS-filerna för inbäddningsbiblioteket koden för det inbäddade biblioteket.

Inbäddning av kod är användbart för att ge åtkomst till bibliotek som lagras i skyddade områden i databasen.

#### Appspecifika klientbiblioteksmappar {#app-specific-client-library-folders}

Det är en god vana att behålla alla programrelaterade filer i programmappen nedan `/app`. Det är också en god vana att neka åtkomst för webbplatsbesökare till `/app` mapp. Skapa en klientbiblioteksmapp under `/etc` mapp som bäddar in klientbiblioteket som finns under `/app`.

Använd egenskapen categories för att identifiera klientbiblioteksmappen som ska bäddas in. Om du vill bädda in biblioteket lägger du till en egenskap i inbäddningen `cq:ClientLibraryFolder` nod, med följande egenskapsattribut:

* **Namn:** embed
* **Typ:** Sträng[]
* **Värde:** Värdet för egenskapen categories i `cq:ClientLibraryFolder` nod att bädda in.

#### Använda inbäddning för att minimera begäranden {#using-embedding-to-minimize-requests}

I vissa fall kan det finnas ett relativt stort antal HTML som har skapats för en vanlig sida av publiceringsinstansen `<script>` -element, särskilt om webbplatsen använder klientkontextinformation för analys eller målgruppsanpassning. I ett icke-optimerat projekt kan du till exempel hitta följande serie med `<script>` -element i HTML för en sida:

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

I sådana fall kan det vara användbart att kombinera all nödvändig klientbibliotekskod till en enda fil så att antalet fram- och tillbaka-begäranden vid sidinläsning minskar. För att göra detta kan du `embed` de nödvändiga biblioteken i ditt programspecifika klientbibliotek med hjälp av egenskapen embed i `cq:ClientLibraryFolder` nod.

Följande klientbibliotekskategorier ingår i AEM. Du bör endast bädda in de som krävs för att din webbplats ska fungera. Men **du bör behålla den beställning som anges här**:

1. `browsermap.standard`
1. `browsermap`
1. `jquery-ui`
1. `cq.jquery.ui`
1. `personalization`
1. `personalization.core`
1. `personalization.core.kernel`
1. `personalization.clientcontext.kernel`
1. `personalization.stores.kernel`
1. `personalization.kernel`
1. `personalization.clientcontext`
1. `personalization.stores`
1. `cq.collab.comments`
1. `cq.collab.feedlink`
1. `cq.collab.ratings`
1. `cq.collab.toggle`
1. `cq.collab.forum`
1. `cq.cleditor`

#### Sökvägar i CSS-filer {#paths-in-css-files}

När du bäddar in CSS-filer använder den genererade CSS-koden sökvägar till resurser som är relativa till inbäddningsbiblioteket. Till exempel det bibliotek som är tillgängligt för allmänheten `/etc/client/libraries/myclientlibs/publicmain` bäddar in `/apps/myapp/clientlib` klientbibliotek:

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

The `main.css` filen innehåller följande format:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

CSS-filen som `publicmain` noden genererar följande format med den ursprungliga bildens URL:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### Använda ett bibliotek för specifika mobilgrupper {#using-a-library-for-specific-mobile-groups}

Använd `channels` egenskapen för en klientbiblioteksmapp för att identifiera den mobilgrupp som använder biblioteket. The `channels` är användbar när bibliotek i samma kategori har utformats för olika enhetsfunktioner.

Om du vill associera en klientbiblioteksmapp med en enhetsgrupp lägger du till en egenskap i `cq:ClientLibraryFolder` nod med följande attribut:

* **Namn:** kanaler
* **Typ:** Sträng[]
* **Värden:** Namnet på mobilgruppen. Om du vill utesluta biblioteksmappen från en grupp anger du ett utropstecken (&quot;!&quot;) för namnet.

I följande tabell visas till exempel värdet för `channels` egenskapen för varje klientbiblioteksmapp i `cq.widgets` kategori:

| Klientbiblioteksmapp | Värde för kanalegenskap |
|---|---|
| `/libs/cq/analytics/widgets` | `!touch` |
| `/libs/cq/analytics/widgets/themes/default` | `!touch` |
| `/libs/cq/cloudserviceconfigs/widgets` | `!touch` |
| `/libs/cq/touch/widgets` | `touch` |
| `/libs/cq/touch/widgets/themes/default` | `touch` |
| `/libs/cq/ui/widgets` | `!touch` |
| `/libs/cq/ui/widgets/themes/default` | `!touch` |

<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets` | `!touch` | -->
<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets/themes/default` |*[no value]* -->

## Använda preprocessorer {#using-preprocessors}

AEM gör det möjligt att ansluta till förprocessorer och levereras med stöd för [YUI-kompressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) för CSS och JavaScript och [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/) för JavaScript med YUI inställt som AEM standardpreprocessor.

De anslutningsbara preprocessorerna möjliggör flexibel användning, inklusive:

* Definiera ScriptProcessors som kan bearbeta skriptkällor
* Processorer kan konfigureras med alternativ
* Processorer kan användas för miniatyrbilder, men även för icke-miniatyrärenden
* clientlib kan definiera vilken processor som ska användas

>[!NOTE]
>
>Som standard använder AEM YUI-kompressor. Se [YUI Compressor GitHub-dokumentation](https://github.com/yui/yuicompressor/issues) om du vill se en lista över kända fel. Om du växlar till GCC-komprimerare för vissa klienter kan vissa problem som uppstår när du använder YUI lösas.

>[!CAUTION]
>
>Placera inte ett miniatyrbibliotek i ett klientbibliotek. Ange i stället Raw-biblioteket och om miniatyrbilder krävs använder du alternativen för preprocessorerna.

### Användning {#usage}

Du kan välja att konfigurera preprocessorer-konfigurationen per klientbibliotek eller system i hela systemet.

* Lägg till flervärdesegenskaper `cssProcessor` och `jsProcessor` på klientbiblioteksnoden

* Eller definiera systemets standardkonfiguration via **HTML Library Manager** OSGi-konfiguration

En preprocessorkonfiguration på klientlib-noden har företräde framför OSGI-konfigurationen.

### Format och exempel {#format-and-examples}

#### Format {#format}

```xml
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

#### YUI-kompressor för CSS Minification och GCC för JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### Typescript to Preprocess and then GCC to Minify and Obfuscate {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```xml
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

#### Fler GCC-alternativ {#additional-gcc-options}

```xml
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

Mer information om GCC-alternativ finns i [GCC-dokumentation](https://developers.google.com/closure/compiler/docs/compilation_levels).

### Ange systemstandardminiatyr {#set-system-default-minifier}

YUI anges som standardminifierare i AEM. Följ de här stegen för att ändra detta till GCC.

1. Gå till Apache Felix Config Manager på [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Sök och redigera **Bibliotekshanteraren Adobe Granite HTML**.
1. Aktivera **Minify** (om det inte redan är aktiverat).
1. Ange värdet **Standardkonfigurationer för JS-processor** till `min:gcc`.

   Alternativ kan skickas om de avgränsas med ett semikolon, t.ex. `min:gcc;obfuscate=true`.

1. Klicka **Spara** för att spara ändringarna.

## Felsökningsverktyg {#debugging-tools}

AEM innehåller flera verktyg för felsökning och testning av klientbiblioteksmappar.

### Se Inbäddade filer {#see-embedded-files}

Om du vill spåra ursprunget för inbäddad kod eller se till att inbäddade klientbibliotek ger det förväntade resultatet, kan du se namnen på de filer som bäddas in under körning. Om du vill se filnamnen lägger du till `debugClientLibs=true` parametern till webbsidans URL. Biblioteket som skapas innehåller `@import` -programsatser i stället för den inbäddade koden.

I exemplet i föregående [Bädda in kod från andra bibliotek](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries) -avsnittet, `/etc/client/libraries/myclientlibs/publicmain` klientbiblioteksmappen bäddar in `/apps/myapp/clientlib` biblioteksmapp för klient. Om du lägger till parametern på webbsidan skapas följande länk i webbsidans källkod:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

Öppna `publicmain.css` filen visar följande kod:

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. Lägg till följande text i URL:en för HTML i webbläsarens adressruta:

   `?debugClientLibs=true`
1. Visa sidans källa när sidan läses in.
1. Klicka på länken som anges som href för länkelementet för att öppna filen och visa källkoden.

### Identifiera klientbibliotek {#discover-client-libraries}

The `/libs/cq/granite/components/dumplibs/dumplibs` genererar en sida med information om alla klientbiblioteksmappar i systemet. The `/libs/granite/ui/content/dumplibs` -noden har komponenten som en resurstyp. Om du vill öppna sidan använder du följande URL (ändra värd och port efter behov):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

Informationen omfattar bibliotekets sökväg och typ (CSS eller JS) samt värdena för biblioteksattributen, t.ex. kategorier och beroenden. Efterföljande tabeller på sidan visar biblioteken i varje kategori och kanal.

### Se genererade utdata {#see-generated-output}

The `dumplibs` -komponenten innehåller en testväljare som visar den källkod som genereras för `ui:includeClientLib` -taggar. Sidan innehåller kod för olika kombinationer av js-, css- och temaattribut.

1. Använd någon av följande metoder för att öppna sidan Testa utdata:

   * Från `dumplibs.html` klickar du på länken på sidan **Klicka här för utdatatestning** text.

   * Öppna följande URL i webbläsaren (använd en annan värd och port efter behov):

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`

   Standardsidan visar utdata för taggar utan värde för attributet categories.

1. Om du vill visa utdata för en kategori anger du värdet för klientbibliotekets `categories` egenskap och klicka på **Skicka fråga**.

## Konfigurera bibliotekshantering för utveckling och produktion {#configuring-library-handling-for-development-and-production}

HTML Library Manager-tjänstprocesserna `cq:ClientLibraryFolder` taggar och genererar biblioteken vid körning. Typ av miljö, utveckling eller produktion, avgör hur du ska konfigurera tjänsten:

* Öka säkerheten: Inaktivera felsökning
* Förbättra prestanda: Ta bort tomt utrymme och komprimera bibliotek.
* Förbättra läsbarheten: Inkludera tomt utrymme och komprimera inte.

Mer information om hur du konfigurerar tjänsten finns i [AEM HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager).
