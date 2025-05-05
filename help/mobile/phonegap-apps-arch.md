---
title: The Anatomy of an App
description: Den här sidan innehåller en beskrivning av de sidkomponenter du skapar för ditt program baserat på /libs/mobileapps/components/angular/ng-page-komponenten (CRXDE Lite på en lokal server).
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: ab4f1c61-be83-420e-a339-02cf1f33efed
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '2584'
ht-degree: 0%

---

# The Anatomy of an App{#the-anatomy-of-an-app}

{{ue-over-mobile}}

## Sidmallar för mobilappar {#page-templates-for-mobile-apps}

Sidkomponenter som du skapar för din app baseras på /libs/mobileapps/components/angular/ng-page-komponenten ([som är öppen i CRXDE Lite på en lokal server](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page)). Den här komponenten innehåller följande JSP-skript som din komponent antingen ärver eller åsidosätter:

* ng-page.jsp
* head.jsp
* body.jsp
* angular-app-module.js.jsp
* angular-route-fragment.js.jsp
* angular-app-controllers.js.jsp
* controller.js.jsp
* template.jsp
* angular-module-list.js.jsp
* header.jsp
* footer.jsp
* js_clientlibs.jsp
* css_clientlibs.jsp

### ng-page.jsp {#ng-page-jsp}

Bestämmer namnet på programmet med egenskapen `applicationName` och visar det via pageContext.

Innehåller head.jsp och body.jsp.

### head.jsp {#head-jsp}

Skriver ut elementet `<head>` på programsidan.

Om du vill åsidosätta metaegenskapen för visningsrutan för appen är det den här filen som du åsidosätter.

Enligt bästa praxis inkluderar appen css-delen av klientbiblioteken i huvudet, medan JS inkluderas i det avslutande &lt; `body>`-elementet.

### body.jsp {#body-jsp}

Innehållet på en Angular återges på olika sätt beroende på om wcmMode identifieras (!= WCMMode.DISABLED) för att avgöra om sidan öppnas för redigering eller som en publicerad sida.

**Författarläge**

I redigeringsläge återges varje enskild sida separat. Angular hanterar inte dirigering mellan sidor och inte heller en ng-view som används för att läsa in en del av en mall som innehåller sidans komponenter. I stället inkluderas sidmallens innehåll (template.jsp) på serversidan via taggen `cq:include`.

Med den här strategin kan författarfunktionerna (som att lägga till och redigera komponenter i styckesystemet, Sidekick, designläget och så vidare) fungera utan ändringar. Sidor som förlitar sig på klientsidans återgivning, t.ex. de för appar, fungerar inte så bra AEM redigeringsläget.

Include-elementet template.jsp kapslas i ett `div`-element som innehåller direktivet `ng-controller`. Den här strukturen gör att DOM-innehållet kan länkas till kontrollenheten. Även om sidor som återges på klientsidan misslyckas, fungerar därför enskilda komponenter som gör det bra (se avsnittet Komponenter nedan).

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**Publish Mode**

I publiceringsläge (t.ex. när appen exporteras med Innehållssynkronisering) blir alla sidor en app för en sida (SPA). (Om du vill lära dig mer om SPA kan du använda självstudiekursen för Angular, närmare bestämt [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07).)

Det finns bara en HTML-sida i en SPA (en sida som innehåller elementet `<html>`). Den här sidan kallas för&quot;layoutmall&quot;. I Angularnas terminologi är det &quot;...en mall som är gemensam för alla vyer i programmet&quot;. Se den här sidan som den översta appsidan. Programsidan på den översta nivån är `cq:Page`-noden i ditt program som ligger närmast roten (och är inte en omdirigering).

Eftersom den faktiska URI:n för din app inte ändras i publiceringsläget måste referenser till externa resurser från den här sidan använda relativa sökvägar. Därför finns det en särskild bildkomponent som tar hänsyn till den översta sidan när bilder återges för export.

Som SPA genererar den här layoutmallsidan helt enkelt ett div-element med ett ng-view-direktiv.

```xml
 <div ng-view ng-class="transition"></div>
```

I flödestjänsten används det här elementet för att visa innehållet på alla Angular i appen, inklusive det redigerbara innehållet på den aktuella sidan (som finns i template.jsp).

Filen body.jsp innehåller header.jsp och footer.jsp som är tomma. Om du vill ange statiskt innehåll på varje sida kan du åsidosätta dessa skript i appen.

Slutligen finns javascript-klienter längst ned i &lt;body>-elementet, inklusive två speciella JS-filer som genereras på servern: *&lt;sidnamn>*.angular-app-module.js och *&lt;sidnamn>*.angular-app-controller.js.

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

Det här skriptet definierar programmodulen Angular. Skriptets utdata är länkade till koden som resten av mallkomponenten genererar via elementet `html` i ng-page.jsp, som innehåller följande attribut:

```xml
ng-app="<c:out value='${applicationName}'/>"
```

Det här attributet anger för Angularna att innehållet i det här DOM-elementet ska länkas till följande modul. Den här modulen länkar vyerna (i AEM är de cq:Page-resurser) till motsvarande kontrollenheter.

Den här modulen definierar också en kontrollenhet på den översta nivån med namnet `AppController` som exponerar variabeln `wcmMode` för omfånget och konfigurerar URI:n som uppdateringsnyttolasterna för innehållssynkronisering ska hämtas från.

Slutligen itererar den här modulen igenom varje underordnad sida (inklusive sig själv) och återger innehållet i flödesfragmentet för varje sida (via väljaren angular-route-fragment.js och tillägget), inklusive det som en config-post till Angularnas $routeProvider. Med andra ord anger $routeProvider vilket innehåll som ska återges när en viss sökväg begärs.

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

Det här skriptet genererar ett JavaScript-fragment som måste ha följande format:

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

Den här koden anger för $routeProvider (definieras i angular-app-module.js.jsp) att &#39;/&lt;sökväg>&#39; ska hanteras av resursen på `templateUrl` och kabelanslutas av `controller` (som vi kommer till nästa).

Om det behövs kan du åsidosätta det här skriptet för att hantera mer komplexa banor, inklusive de med variabler. Ett exempel på detta finns i /apps/geometrixx-outdoors-app/components/angular/ng-template-page/angular-route-fragment.js.jsp-skriptet som installeras med AEM:

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

I Angular sammanfogar styrenheter variabler i $scope och visar dem för vyn. Skriptet angular-app-controllers.js.jsp följer det mönster som illustreras av angular-app-module.js.jsp på så sätt att det itererar genom varje underordnad sida (inklusive sig själv) och skapar det kontrollenhetsfragment som varje sida definierar (via controller.js.jsp). Modulen som definieras kallas `cqAppControllers` och måste listas som ett beroende av appmodulen på den översta nivån så att sidstyrenheterna blir tillgängliga.

### controller.js.jsp {#controller-js-jsp}

Skriptet controller.js.jsp genererar kontrollenhetsfragmentet för varje sida. Detta styrenhetsfragment har följande format:

```
.controller('<c:out value="${controllerNameStripped}"/>', ['$scope', '$http',
    function($scope, $http) {
        var data = $http.get('<c:out value="${relativeResourcePath}"/>.angular.json' + cacheKiller);

        // component fragments which consume the contents of `data` go here
    }
])
```

Variabeln `data` tilldelas det löfte som returneras av metoden `$http.get` för Angularna. Alla komponenter på den här sidan kan, om så önskas, göra en del .json-innehåll tillgängligt (via skriptet angular.json.jsp) och agera på innehållet i den här begäran när den löses. Begäran är mycket snabb på mobila enheter eftersom den bara använder filsystemet.

För att en komponent ska kunna vara en del av kontrollenheten på det här sättet bör den utöka komponenten /libs/mobileapps/components/angular/ng-component och innehålla egenskapen `frameworkType: angular`.

### template.jsp {#template-jsp}

Först introducerades i body.jsp-avsnittet, innehåller template.jsp helt enkelt sidans parsys. I publiceringsläge refereras det här innehållet direkt (på &lt;page-path>.template.html) och läses in i SPA via den templateUrl som konfigurerats på $routeProvider.

Parsytorna i det här skriptet kan konfigureras så att alla typer av komponenter accepteras. Försiktighet måste dock iakttas vid hantering av komponenter som är byggda för en traditionell webbplats (till skillnad från SPA). Till exempel fungerar bildkomponenten som grund bara korrekt på appsidan på den översta nivån eftersom den inte är utformad för att referera till resurser som finns inuti en app.

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

Det här skriptet ger helt enkelt Angular-beroenden för den översta programmodulen för Angular. Det hänvisas till av angular-app-module.js.jsp.

### header.jsp {#header-jsp}

Ett skript som placerar statiskt innehåll högst upp i programmet. Det här innehållet inkluderas av den översta sidan, utanför omfattningen av ng-view.

### footer.jsp {#footer-jsp}

Ett skript som placerar statiskt innehåll längst ned i programmet. Det här innehållet inkluderas av den översta sidan, utanför omfattningen av ng-view.

### js_clientlibs.jsp {#js-clientlibs-jsp}

Åsidosätt det här skriptet för att inkludera dina JavaScript-klienter.

### css_clientlibs.jsp {#css-clientlibs-jsp}

Åsidosätt det här skriptet om du vill inkludera dina CSS-klienter.

## Appkomponenter {#app-components}

Programkomponenter får inte bara fungera på en AEM (publicera eller författare), utan även när programinnehållet exporteras till filsystemet via Innehållssynkronisering. Komponenten måste därför innehålla följande egenskaper:

* Alla resurser, mallar och skript i ett PhoneGap-program måste refereras relativt.
* Hanteringen av länkar skiljer sig om AEM fungerar i redigerings- eller publiceringsläge.

### Relativ Assets {#relative-assets}

URI:n för en given resurs i ett PhoneGap-program skiljer sig inte bara åt på plattformsbasis, utan är unik för varje programinstallation. Observera till exempel följande URI för ett program som körs i iOS-simulatorn:

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en/home.html`

Observera GUID &#39;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&#39; i sökvägen.

Som PhoneGap-utvecklare finns det innehåll du är intresserad av under www-katalogen. Använd relativa sökvägar för att komma åt appresurserna.

För att lösa in problemet använder PhoneGap-programmet appmönstret för en sida (SPA) så att bas-URI:n (exklusive hash) aldrig ändras. Därför måste alla resurser, mallar och skript som du refererar till **vara relativa till den översta sidan. &#x200B;** Sidan på den översta nivån initierar Angularnas routning och styrenheter med hjälp av `*<name>*.angular-app-module.js` och `*<name>*.angular-app-controllers.js`. Den här sidan ska vara den närmaste sidan till databasens rot som *inte *utökar en sling:redirect.

Det finns flera hjälpmetoder för att hantera relativa sökvägar:

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

Om du vill se exempel på hur de används öppnar du mobilappskällan som finns på /libs/mobileapps/components/angular.

### Länkar {#links}

Länkarna måste använda funktionen `ng-click="go('/path')"` för att stödja alla WCM-lägen. Den här funktionen är beroende av värdet på en omfångsvariabel för att kunna avgöra länkåtgärden korrekt:

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

När `$scope.wcmMode == true` hanterar vi varje navigeringshändelse på vanligt sätt, så att resultatet blir en ändring av sökvägen och/eller siddelen i URL:en.

Om `$scope.wcmMode == false` är ett alternativ blir varje navigeringshändelse en ändring av hash-delen i URL:en som löses internt av Angularnas ngRoute-modul.

### Information om komponentskript {#component-script-details}

![chlimage_1-144](assets/chlimage_1-144.png)

#### ng-component.jsp {#ng-component-jsp}

Skriptet visar antingen komponentinnehållet eller en lämplig platshållare när redigeringsläget identifieras.

#### template.jsp {#template-jsp-1}

Skriptet template.jsp återger komponentens kod. Om den aktuella komponenten drivs av JSON-data som har extraherats från AEM (till exempel &#39;ng-text&#39;: /libs/mobileapps/components/angular/ng-text/template.jsp), ansvarar det här skriptet för att dra markeringen med data som visas av sidans kontrollomfång.

Prestandakraven kan dock ibland innebära att ingen klientsidans mallning (dvs databindning) utförs. I det här fallet återger du bara komponentens kod på serversidan, så inkluderas den i sidmallsinnehållet.

#### overhead.jsp {#overhead-jsp}

I komponenter som drivs av JSON-data (till exempel &#39;ng-text&#39;: /libs/mobileapps/components/angular/ng-text) kan overhead.jsp användas för att ta bort all Java-kod från template.jsp. Den refereras sedan från template.jsp och alla variabler som den visar på begäran är tillgängliga för användning. Den här strategin uppmuntrar till separation av logik från presentation och begränsar mängden kod som måste kopieras och klistras in när en ny komponent härleds från en befintlig.

#### controller.js.jsp {#controller-js-jsp-1}

Så som beskrivs i AEM Page Templates kan varje komponent generera ett JavaScript-fragment för att förbruka det JSON-innehåll som exponeras av `data`-löftet. I enlighet med Angularnas konventioner bör en kontrollenhet endast användas för att tilldela variabler till omfånget.

#### angular.json.jsp {#angular-json-jsp}

Skriptet inkluderas som ett fragment i den sidövergripande filen &lt;page-name>.angular.json som exporteras för varje sida som utökar ng-page. I den här filen kan komponentutvecklaren visa alla JSON-strukturer som komponenten behöver. I exemplet &#39;ng-text&#39; inkluderar den här strukturen bara komponentens textinnehåll och en flagga som anger om komponenten innehåller RTF-text eller inte.

Produktkomponenten för appen utomhus för Geometrixx är ett mer komplext exempel (/apps/geometrixx-outdoor-app/components/angular/ng-product):

```xml
{
    "content-par/ng-product": {
        "items": [{
            "name": "Cajamara",
            "description": "Bike",
            "summaryHTML": "",
            "price": "$610.00",
            "SKU": "eqsmcj",
            "numberOfLikes": "0",
            "numberOfComments": "0"
        }]
    },
    "content-par/ng-product/ng-image": {
        "items": [{
            "hasContent": true,
            "imgSrc": "home/products/eq/eqsm/eqsmcj/jcr_content/content-par/ng-product/ng-image.img.jpg/1377771306985.jpg",
            "description": "",
            "alt": "Cajamara",
            "title": "Cajamara",
            "hasLink": false,
            "linkPath": "",
            "attributes": [{
                "attributeName": "class",
                "attributeValue": "cq-dd-image"
            }]
        }]
    }
}
```

## Innehåll i CLI Assets Download {#contents-of-the-cli-assets-download}

Hämta CLI-resurser från Apps-konsolen för att optimera dem för en viss plattform och bygg sedan appen med PhoneGap-API:t för kommandoradsintegrering (CLI). Innehållet i ZIP-filen som du sparar i det lokala filsystemet har följande struktur:

```xml
.cordova/
  |- hooks/
     |- after_prepare/
     |- before_platform_add/
     |- Other Hooks
plugins/
www/
  |- config.xml
  |- index.html
  |- res/
  |- etc/
  |- apps/
  |- content/
  |- package.json
  |- package-update.json
```

### .cordova {#cordova}

Det här är en dold katalog som du kanske inte ser beroende på dina aktuella operativsystemsinställningar. Du bör konfigurera ditt operativsystem så att den här katalogen visas om du planerar att ändra programversionerna som den innehåller.

#### .cordova/hooks/ {#cordova-hooks}

Den här katalogen innehåller [CLI-krokarna](https://cordova.apache.org/docs/en/10.x/guide/appdev/hooks/). Mapparna i hooks-katalogen innehåller node.js-skript som körs vid exakta punkter under bygget.

#### .cordova/hooks/after-platform_add/ {#cordova-hooks-after-platform-add}

Katalogen after-platform_add innehåller filen `copy_AMS_Conifg.js`. Det här skriptet kopierar en konfigurationsfil som stöder samlingen av Adobe Mobile Services-analyser.

#### .cordova/hooks/after-prepare/ {#cordova-hooks-after-prepare}

Katalogen after-prepare innehåller filen `copy_resource_files.js`. Skriptet kopierar flera ikoner och välkomstskärmsbilder till plattformsspecifika platser.

#### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

Katalogen before_platform_add innehåller filen `install_plugins.js`. Det här skriptet itererar genom en lista med identifierare för Cordova-plugin-program, och installerar de som identifieras inte redan är tillgängliga.

Den här strategin kräver inte att du paketerar och installerar plugin-program för att AEM varje gång kommandot Maven `content-package:install` körs. Den alternativa strategin för att checka in filerna i SCM-systemet kräver repetitiva paketerings- och installationsaktiviteter.

#### .cordova/hooks/andra krokar {#cordova-hooks-other-hooks}

Inkludera andra krokar efter behov. Följande kopplingar är tillgängliga (enligt PhoneGap-exemplet hello world app):

* after_build
* before_build
* after_compile
* before_compile
* after_docs
* before_docs
* after_emulate
* before_emulate
* after_platform_add
* before_platform_add
* after_platform_ls
* before_platform_ls
* after_platform_rm
* before_platform_rm
* after_plugin_add
* before_plugin_add
* after_plugin_ls
* before_plugin_ls
* after_plugin_rm
* before_plugin_rm
* after_prepare
* before_prepare
* after_run
* before_run

#### plattformar/ {#platforms}

Den här katalogen är tom tills du kör kommandot `phonegap run <platform>` i projektet. För närvarande kan `<platform>` vara antingen `ios` eller `android`.

När du har skapat programmet för en viss plattform skapas motsvarande katalog och den innehåller den plattformsspecifika programkoden.

#### plugins/ {#plugins}

Katalogen plugin-program fylls i av varje plugin-program som visas i filen `.cordova/hooks/before_platform_add/install_plugins.js` när du har kört kommandot `phonegap run <platform>`. Katalogen är från början tom.

#### www/ {#www}

Katalogen www innehåller allt webbinnehåll (HTML, JS och CSS-filer) som implementerar utseendet och beteendet för programmet. Med undantag för de undantag som beskrivs nedan kommer det här innehållet från AEM och exporteras till dess statiska form via Innehållssynkronisering.

#### www/config.xml {#www-config-xml}

PhoneGap-dokumentationen (`https://docs.phonegap.com`) refererar till den här filen som en global konfigurationsfil. config.xml innehåller många appegenskaper, till exempel appens namn, programmets inställningar (till exempel om en iOS-webbvy tillåter överrullning) och plugin-beroenden som *endast* används av PhoneGap-bygget.

Filen config.xml är en statisk fil i AEM och exporteras i befintligt skick via Innehållssynkronisering.

#### www/index.html {#www-index-html}

Filen index.html dirigeras om till programmets startsida.

Filen config.xml innehåller elementet `content`:

`<content src="content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en.html" />`

I PhoneGap-dokumentationen (`https://docs.phonegap.com`) beskrivs det här elementet som&quot;Det valfria &lt;content>-elementet definierar programmets startsida i webbresurskatalogen på den översta nivån. Standardvärdet är index.html, som vanligtvis visas i projektets toppnivåkatalog www.&quot;

PhoneGap-bygget misslyckas om det inte finns någon index.html-fil. Därför inkluderas den här filen.

#### www/res {#www-res}

Katalogen res innehåller bilder och ikoner på välkomstskärmen. Skriptet `copy_resource_files.js` kopierar filerna till deras plattformsspecifika platser under byggfasen av `after_prepare`.

#### www/etc {#www-etc}

AEM noden /etc innehåller som standard statiskt clientlib-innehåll. Katalogen etc innehåller biblioteken Toprock, AngularJS och Geometrixx ng-clientlibsall.

#### www/apps {#www-apps}

Programkatalogen innehåller kod som är relaterad till välkomstsidan. Den unika egenskapen hos välkomstsidan för en AEM är att den initierar programmet utan någon användarinteraktion. Klientlibbinnehållet (både CSS och JS) i appen är därför minimalt för att maximera prestanda.

#### www/content {#www-content}

Innehållskatalogen innehåller resten av programmets webbinnehåll. Innehållet kan innehålla, men är inte begränsat till, följande filer:

* HTML page content, which authoring directly in AEM
* Bildresurser som är associerade med AEM
* JavaScript-innehåll som serverskript genererar
* JSON-filer som beskriver sidor- eller komponentinnehåll

#### www/package.json {#www-package-json}

Filen package.json är en manifestfil som listar de filer som en **full** Content Sync-hämtning innehåller. Den här filen innehåller också den tidsstämpel som nyttolasten för innehållssynkronisering genererades vid ( `lastModified`). Den här egenskapen används vid begäran om partiella uppdateringar av appen från AEM.

#### www/package-update.json {#www-package-update-json}

Om den här nyttolasten är en hämtning av hela programmet innehåller manifestet den exakta listan över filer som `package.json`.

Om nyttolasten är en partiell uppdatering innehåller `package-update.json` bara de filer som ingår i den aktuella nyttolasten.

### Nästa steg {#the-next-steps}

När du har lärt dig mer om appens Anatomi kan du läsa [Program för en sida](/help/mobile/phonegap-single-page-applications.md).
