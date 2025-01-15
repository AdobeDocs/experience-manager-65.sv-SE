---
title: Enkelsidiga program
description: Följ den här sidan för att lära dig mer om single page-applikationer, det vill säga du kan skapa ett program som fungerar likadant som ett datorprogram eller mobilprogram.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: daf7bf39-a105-46eb-ab7b-1c59484949e2
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 0%

---

# Enkelsidiga program{#single-page-applications}

{{ue-over-mobile}}

[Single-Page-program](https://en.wikipedia.org/wiki/Single-page_application) (SPA) har nått en kritisk massa, som allmänt anses vara det mest effektiva mönstret för att skapa sömlösa upplevelser med webbteknik. Genom att följa ett SPA mönster kan du skapa ett program som fungerar likadant som ett skrivbordsprogram eller mobilprogram, men som når en mängd olika enhetsplattformar och formfaktorer på grund av dess grund i öppna webbstandarder.

I allmänhet verkar SPA mer presterande än traditionella sidbaserade webbplatser eftersom de normalt bara läser in den fullständiga HTML-sidan **en gång** (inklusive CSS, JS och teckensnittsinnehåll som stöds) och sedan bara läser in exakt det som är nödvändigt varje gång en lägesändring inträffar i appen. Vad som är nödvändigt för den här tillståndsändringen kan variera beroende på vilken uppsättning tekniker som väljs, men innehåller vanligtvis ett enda HTML-fragment som ersätter den befintliga vyn och körningen av ett JS-kodblock som gör att den nya vyn kan sammanställas och att mallåtergivning på klientsidan kan utföras om det behövs. Den här lägesändringens hastighet kan förbättras ytterligare genom stöd för mekanismer för mallcachelagring, eller till och med offlineåtkomst till mallinnehåll om Adobe PhoneGap används.

AEM 6.1 stöder uppbyggnad och hantering av SPA via AEM appar. I den här artikeln ges en introduktion till begreppen bakom SPA och hur de använder [AngularJS](https://angularjs.org/) för att överföra ditt varumärke till App Store och Google Play.

## SPA i AEM appar {#spa-in-aem-apps}

Single-Page Application Framework i AEM Apps möjliggör höga prestanda för en AngularJS-app, samtidigt som författare (eller annan icke-teknisk personal) kan skapa och hantera appens innehåll via den pekoptimerade dra och släpp-redigeringsmiljön som traditionellt har reserverats för hantering av webbplatser. Har du redan skapat en webbplats med AEM? Det är enkelt att återanvända innehåll, komponenter, arbetsflöden, resurser och behörigheter med AEM program.

## AngularJS Application Module {#angularjs-application-module}

AEM Apps hanterar mycket av AngularJS-konfigurationen åt dig, inklusive att sätta samman appens modul på den översta nivån. Som standard heter den här modulen&quot;AEMAngularApp&quot; och skriptet som ansvarar för dess generering finns på /libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp.

En del av initieringen av din app är att ange vilka AngularJS-moduler som appen är beroende av. Listan med moduler som används av din app anges av ett skript som finns på /libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp, och kan överlappas av dina egna programs sidkomponent för att dra in ytterligare AngularJS-moduler som din app kräver. Du kan till exempel jämföra skriptet ovan med implementeringen av Geometrixx (finns på /apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp).

För att ge stöd för navigering mellan de olika lägena i din app, itererar skriptet angular-app-module igenom alla underordnade sidor på din programsida på den översta nivån för att generera en uppsättning rutter och konfigurerar varje sökväg på Angularnas $routeProvider-tjänst. Ett exempel på hur det här ser ut i praktiken finns i skriptet angular-app-module som genereras av Geometrixx Outdoors programexempel: (länk kräver en lokal instans) [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

När du loggar in på den genererade AEMAngularApp hittar du en serie vägar som anges enligt följande:

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

Exemplet ovan visar i synnerhet ett exempel på hur en parameter skickas som en del av banan. I det här exemplet anger det att när en sökväg som uppfyller det angivna mönstret (/content/phonegap/geometrixx-outdoor/en/home/products/:id) begärs, ska den hanteras av mallen home/products.template.html och använda styrenheten&quot;contentphonegapgeometrixxoutdoorsenhomeproducts&quot;.

Den mall som ska läsas in när den här vägen begärs anges av egenskapen templateUrl. Den här mallen innehåller HTML från AEM komponenter som har inkluderats på sidan och eventuella AngularJS-direktiv som krävs för att ansluta klientsidan av programmet. Ett exempel på ett AngularJS-direktiv i en Geometrixx-komponent finns på rad 45 i swipe-carousels template.jsp (/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp).

## Sidkontroller {#page-controllers}

I Angularnas egna ord är&quot;en styrenhet är en konstruktorfunktion i JavaScript som används för att förstärka Angularnas omfång&quot;. ([källa](https://docs.angularjs.org/guide/controller)) Varje sida i en AEM-app ansluts automatiskt till en kontrollenhet som kan utökas av en kontrollenhet som anger `frameworkType` av `angular`. Titta på ng-text-komponenten som ett exempel (/libs/mobileapps/components/angular/ng-text), inklusive cq:template-noden som ser till att den här komponenten läggs till på en sida varje gång den läggs till innehåller den här viktiga egenskapen.

Om du vill ha ett mer komplext exempel på en kontrollenhet öppnar du skriptet ng-template-page controller.jsp (på /apps/geometrixx-outdoor-app/components/angular/ng-template-page). Särskilt intressant är den JavaScript-kod som genereras när den körs, som återges enligt följande:

```xml
// Controller for page 'products'
.controller('contentphonegapgeometrixxoutdoorsenhomeproducts', ['$scope', '$http', '$routeParams',
    function($scope, $http, $routeParams) {
        var sku = $routeParams.id;
        var productPath = '/' + sku.substring(0, 2) + '/' + sku.substring(0, 4) + '/' + sku;
        var data = $http.get('home/products' + productPath + '.angular.json' + cacheKiller);

        /* ng-product component controller (path: content-par/ng-product) */
        data.then(function(response) {
            $scope.contentparngproduct = response.data["content-par/ng-product"].items;
        });

        /* ng-image component controller (path: content-par/ng-product/ng-image) */
        data.then(function(response) {
            $scope.contentparngproductngimage = response.data["content-par/ng-product/ng-image"].items;
        });
    }
])
```

I exemplet ovan tas parametern från tjänsten `$routeParams` och sedan masseras den till den katalogstruktur där JSON-data lagras. Genom att hantera SKU:n `id` på det här sättet kan du leverera en enda produktmall som kan återge produktdata för potentiellt tusentals olika produkter. Det här är en mycket mer skalbar modell som kräver en individuell väg för varje objekt i en (potentiellt) enorm produktdatabas.

Det finns också två komponenter som är på gång här: ng-product förbättrar omfattningen med de data som extraheras från det ovan angivna `$http`-anropet. Det finns också en ng-image på den här sidan som i sin tur ökar omfattningen med det värde som hämtas från svaret. I enlighet med Angularnas `$http`-tjänst väntar varje komponent tålmodigt tills begäran är slutförd och det löfte den skapades är uppfyllt.

## Nästa steg {#the-next-steps}

När du har lärt dig mer om Single Page-program kan du läsa [Utveckla appar med PhoneGap CLI](/help/mobile/phonegap-apps-pg-cli.md).
