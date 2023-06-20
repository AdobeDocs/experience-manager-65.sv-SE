---
title: The Anatomy of an App
seo-title: The Anatomy of an App
description: Den här sidan innehåller en beskrivning av de sidkomponenter du skapar för ditt program baserat på /libs/mobileapps/components/angular/ng-page-komponenten (CRXDE Lite på en lokal server).
seo-description: This page provides description of the page components that you create for your app are based on the /libs/mobileapps/components/angular/ng-page component (CRXDE Lite on a local server).
uuid: 4c1a74c1-85af-4a79-b723-e9fbfc661d35
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 55667e62-a61b-4794-b292-8d54929c41ac
exl-id: ab4f1c61-be83-420e-a339-02cf1f33efed
source-git-commit: 17d13e9b201629d9d1519fde4740cf651fe89d2c
workflow-type: tm+mt
source-wordcount: '2687'
ht-degree: 0%

---

# The Anatomy of an App{#the-anatomy-of-an-app}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

## Sidmallar för mobilappar {#page-templates-for-mobile-apps}

Sidkomponenter som du skapar för din app baseras på /libs/mobileapps/components/angular/ng-page-komponenten ([öppna i CRXDE Lite på en lokal server](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page)). Den här komponenten innehåller följande JSP-skript som din komponent antingen ärver eller åsidosätter:

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

Bestämmer namnet på programmet med `applicationName` och visar den via pageContext.

Innehåller head.jsp och body.jsp.

### head.jsp {#head-jsp}

Skriver ut `<head>` -element på programsidan.

Om du vill åsidosätta metaegenskapen för visningsrutan för appen är det den här filen som du åsidosätter.

Enligt bästa praxis inkluderar appen css-delen av klientbiblioteken i huvudet, medan JS inkluderas vid avslutande &lt; `body>` -element.

### body.jsp {#body-jsp}

Innehållet på en Angular återges på olika sätt beroende på om wcmMode identifieras (!= WCMMode.DISABLED) för att avgöra om sidan öppnas för redigering eller som en publicerad sida.

**Författarläge**

I redigeringsläge återges varje enskild sida separat. Angular hanterar inte dirigering mellan sidor och inte heller en ng-view som används för att läsa in en del av en mall som innehåller sidans komponenter. I stället inkluderas sidmallens innehåll (template.jsp) på serversidan via `cq:include` -tagg.

Den här strategin aktiverar författarfunktioner (som att lägga till och redigera komponenter i styckesystemet, Sidekick, designläge osv.) att fungera utan ändringar. Sidor som förlitar sig på klientsidans återgivning, t.ex. de för appar, fungerar inte så bra i AEM.

Observera att include i template.jsp finns i en `div` elementet som innehåller `ng-controller` -direktivet. Den här strukturen gör att DOM-innehållet kan länkas till kontrollenheten. Även om sidor som återges på klientsidan misslyckas, fungerar därför enskilda komponenter som gör det bra (se avsnittet Komponenter nedan).

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**Publiceringsläge**

I publiceringsläge (t.ex. när appen exporteras med Innehållssynkronisering) blir alla sidor en app för en sida (SPA). (Mer information om SPA finns i självstudiekursen om Angular. [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07).)

Det finns bara en HTML-sida i en SPA (en sida som innehåller `<html>` element). Den här sidan kallas för&quot;layoutmall&quot;. I Angularnas terminologi är det..en mall som är gemensam för alla vyer i programmet.&quot; Se den här sidan som den översta appsidan. Appsidan på den översta nivån är `cq:Page` noden i programmet som är närmast roten (och inte är en omdirigering).

Eftersom den faktiska URI:n för din app inte ändras i publiceringsläget måste referenser till externa resurser från den här sidan använda relativa sökvägar. Därför finns det en särskild bildkomponent som tar hänsyn till den här sidan på den översta nivån när bilder återges för export.

Som SPA genererar den här layoutmallsidan helt enkelt ett div-element med ett ng-view-direktiv.

```xml
 <div ng-view ng-class="transition"></div>
```

I flödestjänsten för Angular används det här elementet för att visa innehållet på alla sidor i appen, inklusive det redigerbara innehållet på den aktuella sidan (som finns i template.jsp).

Filen body.jsp innehåller header.jsp och footer.jsp som är tomma. Om du vill ange statiskt innehåll på varje sida kan du åsidosätta dessa skript i appen.

Slutligen finns javascript-klienter längst ned i &lt;body> -element inklusive två speciella JS-filer som genereras på servern: *&lt;page name=&quot;&quot;>*.angular-app-module.js och *&lt;page name=&quot;&quot;>*.angular-app-controller.js.

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

Skriptet definierar programmodulen Angular. Skriptets utdata är länkade till koden som resten av mallkomponenten genererar via `html` element i ng-page.jsp, som innehåller följande attribut:

```xml
ng-app="<c:out value='${applicationName}'/>"
```

Det här attributet anger för Angularna att innehållet i det här DOM-elementet ska länkas till följande modul. Den här modulen länkar vyerna (i AEM är de cq:Page-resurser) till motsvarande kontrollenheter.

Den här modulen definierar även en kontrollenhet på den översta nivån med namnet `AppController` som visar `wcmMode` variabel till omfånget och konfigurerar den URI som innehållssynkroniseringens uppdateringsnyttolaster ska hämtas från.

Slutligen itererar den här modulen igenom varje underordnad sida (inklusive sig själv) och återger innehållet i flödesfragmentet för varje sida (via väljaren angular-route-fragment.js och tillägget), inklusive det som en config-post till Angularnas $routeProvider. Med andra ord anger $routeProvider vilket innehåll som ska återges när en viss sökväg begärs.

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

Det här skriptet genererar ett JavaScript-fragment som måste ha följande format:

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

Den här koden anger för $routeProvider (definieras i angular-app-module.js.jsp) att &#39;/&lt;path>&#39; ska hanteras av resursen på `templateUrl`och som kopplades upp av `controller` (som vi kommer till nästa).

Om det behövs kan du åsidosätta det här skriptet för att hantera mer komplexa banor, inklusive de med variabler. Ett exempel på detta finns i /apps/geometrixx-outdoors-app/components/angular/ng-template-page/angular-route-fragment.js.jsp-skriptet som installeras med AEM:

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

I Angular sammanställer styrenheter variabler i $scope och visar dem för vyn. Skriptet angular-app-controllers.js.jsp följer det mönster som illustreras av angular-app-module.js.jsp på så sätt att det itererar genom varje underordnad sida (inklusive sig själv) och matar ut det kontrollenhetsfragment som varje sida definierar (via controller.js.jsp). Modulen som definieras anropas `cqAppControllers` och måste listas som ett beroende för den översta programmodulen så att sidstyrenheterna blir tillgängliga.

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

Observera att `data` variabeln tilldelas det löfte som returneras av Angularna `$http.get` -metod. Alla komponenter på den här sidan kan, om så önskas, göra en del .json-innehåll tillgängligt (via skriptet angular.json.jsp) och agera på innehållet i den här begäran när den löses. Begäran är mycket snabb på mobila enheter eftersom den bara använder filsystemet.

För att en komponent ska kunna vara en del av kontrollenheten på det här sättet bör den utöka komponenten /libs/mobileapps/components/angular/ng-component och innehålla `frameworkType: angular` -egenskap.

### template.jsp {#template-jsp}

Först introducerades i body.jsp-avsnittet, innehåller template.jsp helt enkelt sidans parsys. I publiceringsläge refereras det här innehållet direkt (på &lt;page-path>.template.html) och läses in i SPA via templateUrl som är konfigurerad på $routeProvider.

Parsyserna i det här skriptet kan konfigureras så att alla typer av komponenter accepteras. Försiktighet måste dock iakttas vid hantering av komponenter som är byggda för en traditionell webbplats (till skillnad från SPA). Till exempel fungerar bildkomponenten som grund bara korrekt på appsidan på den översta nivån eftersom den inte är utformad för att referera till resurser som finns inuti en app.

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

Det här skriptet ger helt enkelt Angular-beroenden för den översta programmodulen för Angular. Det hänvisas till av angular-app-module.js.jsp.

### header.jsp {#header-jsp}

Ett skript som placerar statiskt innehåll högst upp i programmet. Det här innehållet inkluderas av den översta sidan, utanför omfattningen av ng-view.

### footer.jsp {#footer-jsp}

Ett skript som placerar statiskt innehåll längst ned i programmet. Det här innehållet inkluderas av den översta sidan, utanför omfattningen av ng-view.

### js_clientlibs.jsp {#js-clientlibs-jsp}

Åsidosätt det här skriptet så att det innehåller dina JavaScript-klienter.

### css_clientlibs.jsp {#css-clientlibs-jsp}

Åsidosätt det här skriptet om du vill inkludera dina CSS-klienter.

## Appkomponenter {#app-components}

Programkomponenter får inte bara fungera på en AEM (publicera eller författare), utan även när programinnehållet exporteras till filsystemet via Innehållssynkronisering. Komponenten måste därför innehålla följande egenskaper:

* Alla resurser, mallar och skript i ett PhoneGap-program måste refereras relativt.
* Hanteringen av länkar skiljer sig om AEM fungerar i redigerings- eller publiceringsläge.

### Relativa resurser {#relative-assets}

URI:n för en given resurs i ett PhoneGap-program skiljer sig inte bara åt på plattformsbasis, utan är unik för varje programinstallation. Observera till exempel följande URI för ett program som körs i iOS-simulatorn:

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en/home.html`

Observera GUID &#39;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&#39; i sökvägen.

Som PhoneGap-utvecklare finns det innehåll du är intresserad av under www-katalogen. Använd relativa sökvägar för att komma åt appresurserna.

För att lösa in problemet använder PhoneGap-programmet appmönstret för en sida (SPA) så att bas-URI:n (exklusive hash) aldrig ändras. Därför måste alla resurser, mallar och skript som du refererar till **vara relativa till den översta sidan. **På den översta sidan initieras Angularnas routning och styrenheter med hjälp av `*<name>*.angular-app-module.js` och `*<name>*.angular-app-controllers.js`. Den här sidan ska vara den närmaste sidan till databasens rot som *inte *utökar en sling:redirect.

Det finns flera hjälpmetoder för att hantera relativa sökvägar:

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

Om du vill se exempel på hur de används öppnar du mobilappskällan som finns på /libs/mobileapps/components/angular.

### Länkar {#links}

Länkarna måste använda `ng-click="go('/path')"` för att stödja alla WCM-lägen. Den här funktionen är beroende av värdet på en omfångsvariabel för att kunna avgöra länkåtgärden korrekt:

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

När `$scope.wcmMode == true` vi hanterar varje navigeringshändelse på vanligt sätt, så att resultatet blir en ändring av sökvägen och/eller siddelen i URL:en.

Alternativt om `$scope.wcmMode == false`resulterar varje navigeringshändelse i en ändring av hash-delen av URL:en som löses internt av Angularnas ngRoute-modul.

### Information om komponentskript {#component-script-details}

![chlimage_1-144](assets/chlimage_1-144.png)

#### ng-component.jsp {#ng-component-jsp}

Skriptet visar antingen komponentinnehållet eller en lämplig platshållare när redigeringsläget identifieras.

#### template.jsp {#template-jsp-1}

Skriptet template.jsp återger komponentens kod. Om komponenten i fråga drivs av JSON-data som har extraherats från AEM (till exempel &#39;ng-text&#39;): /libs/mobileapps/components/angular/ng-text/template.jsp) kommer det här skriptet att vara ansvarigt för att dra markeringen med data som exponeras av sidans kontrollomfång.

Prestandakraven kan dock ibland innebära att ingen klientsidans mall (dvs databindning) utförs. I det här fallet återger du bara komponentens kod på serversidan, så inkluderas den i sidmallsinnehållet.

#### overhead.jsp {#overhead-jsp}

I komponenter som drivs av JSON-data (till exempel &#39;ng-text&#39;): /libs/mobileapps/components/angular/ng-text), overhead.jsp kan användas för att ta bort all Java-kod från template.jsp. Den refereras sedan från template.jsp och alla variabler som den visar på begäran är tillgängliga för användning. Den här strategin uppmuntrar till separation av logik från presentation och begränsar mängden kod som måste kopieras och klistras in när en ny komponent härleds från en befintlig.

#### controller.js.jsp {#controller-js-jsp-1}

Så som beskrivs i AEM Page Templates kan varje komponent generera ett JavaScript-fragment för att förbruka det JSON-innehåll som exponeras av `data` löfte. I enlighet med Angularnas konventioner bör en kontrollenhet endast användas för att tilldela variabler till omfånget.

#### angular.json.jsp {#angular-json-jsp}

Det här skriptet är inkluderat som ett fragment på sidan som är bred&lt;page-name>.angular.json&#39;-fil som exporteras för varje sida som utökar ng-page. I den här filen kan komponentutvecklaren visa alla JSON-strukturer som komponenten behöver. I exemplet &#39;ng-text&#39; inkluderar den här strukturen bara komponentens textinnehåll och en flagga som anger om komponenten innehåller RTF-text eller inte.

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

## Innehåll i hämtningen av CLI-resurser {#contents-of-the-cli-assets-download}

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

Den här katalogen innehåller [CLI-krokar](https://cordova.apache.org/docs/en/10.x/guide/appdev/hooks/). Mapparna i hooks-katalogen innehåller node.js-skript som körs vid exakta punkter under bygget.

#### .cordova/hooks/after-platform_add/ {#cordova-hooks-after-platform-add}

Katalogen after-platform_add innehåller `copy_AMS_Conifg.js` -fil. Det här skriptet kopierar en konfigurationsfil som stöder samlingen av Adobe Mobile Services-analyser.

#### .cordova/hooks/after-prepare/ {#cordova-hooks-after-prepare}

Katalogen after-prepare innehåller `copy_resource_files.js` -fil. Skriptet kopierar ett antal ikoner och välkomstskärmsbilder till plattformsspecifika platser.

#### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

Före_platform_add-katalogen innehåller `install_plugins.js` -fil. Skriptet itererar genom en lista med identifierare för Cordova-plugin-program, och installerar de som identifieras inte redan är tillgängliga.

Den här strategin kräver inte att du paketerar och installerar plugin-program för att AEM varje gång Maven `content-package:install` kommandot körs. Den alternativa strategin för att checka in filerna i SCM-systemet kräver repetitiva paketerings- och installationsaktiviteter.

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

Den här katalogen är tom tills du kör `phonegap run <platform>` -kommando i projektet. För närvarande `<platform>` kan vara antingen `ios` eller `android`.

När du har skapat programmet för en viss plattform skapas motsvarande katalog och den innehåller den plattformsspecifika programkoden.

#### plugin-program/ {#plugins}

Katalogen för plugin-program fylls i av varje plugin-program som visas i `.cordova/hooks/before_platform_add/install_plugins.js` efter att du har kört `phonegap run <platform>` -kommando. Katalogen är från början tom.

#### www/ {#www}

Katalogen www innehåller allt webbinnehåll (HTML, JS och CSS-filer) som implementerar programmets utseende och beteende. Med undantag för de undantag som beskrivs nedan kommer det här innehållet från AEM och exporteras till dess statiska form via Innehållssynkronisering.

#### www/config.xml {#www-config-xml}

PhoneGap-dokumentationen (`https://docs.phonegap.com`) refererar till den här filen som en&quot;global konfigurationsfil&quot;. config.xml innehåller många appegenskaper, till exempel namnet på programmet, programmets inställningar (till exempel om en iOS-webbvy tillåter överrullning) och plugin-beroenden som är *endast* används av PhoneGap-bygge.

Filen config.xml är en statisk fil i AEM och exporteras i befintligt skick via Innehållssynkronisering.

#### www/index.html {#www-index-html}

Filen index.html dirigeras om till programmets startsida.

Filen config.xml innehåller `content` element:

`<content src="content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en.html" />`

I PhoneGap-dokumentationen (`https://docs.phonegap.com`), det här elementet beskrivs som&quot;Det valfria &lt;content> -elementet definierar programmets startsida i webbresurskatalogen på den översta nivån. Standardvärdet är index.html, som vanligtvis visas i projektets toppnivåkatalog www.&quot;

PhoneGap-bygget misslyckas om det inte finns någon index.html-fil. Därför inkluderas den här filen.

#### www/res {#www-res}

Katalogen res innehåller bilder och ikoner på välkomstskärmen. The `copy_resource_files.js` skriptet kopierar filerna till deras plattformsspecifika platser under `after_prepare` byggfasen.

#### www/etc {#www-etc}

AEM noden /etc innehåller som standard statiskt clientlib-innehåll. Katalogen etc innehåller biblioteken Toprock, AngularJS och Geometrixx ng-clientlibsall.

#### www/apps {#www-apps}

Programkatalogen innehåller kod som är relaterad till välkomstsidan. Den unika egenskapen hos startsidan för en AEM är att den initierar programmet utan någon användarinteraktion. Klientlibbinnehållet (både CSS och JS) i appen är därför minimalt för att maximera prestanda.

#### www/content {#www-content}

Innehållskatalogen innehåller resten av programmets webbinnehåll. Innehållet kan innehålla, men är inte begränsat till, följande filer:

* HTML page content, which authoring directly in AEM
* Bildresurser som är associerade med AEM
* JavaScript-innehåll som serverskript genererar
* JSON-filer som beskriver sidor- eller komponentinnehåll

#### www/package.json {#www-package-json}

Filen package.json är en manifestfil som listar filerna som en **full** Innehållssynkronisering innehåller. Den här filen innehåller även den tidsstämpel som användes när nyttolasten för Innehållssynkronisering skapades ( `lastModified`). Den här egenskapen används vid begäran om partiella uppdateringar av appen från AEM.

#### www/package-update.json {#www-package-update-json}

Om den här nyttolasten är en hämtning av hela programmet innehåller manifestet den exakta listan över filer som `package.json`.

Om nyttolasten är en partiell uppdatering, `package-update.json` innehåller endast de filer som ingår i den här speciella nyttolasten.

### Nästa steg {#the-next-steps}

När du har lärt dig mer om appens Anatomi finns mer information i [Enkelsidiga program](/help/mobile/phonegap-single-page-applications.md).
