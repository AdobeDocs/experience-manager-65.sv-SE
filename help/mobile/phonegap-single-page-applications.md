---
title: Enkelsidiga program
seo-title: Enkelsidiga program
description: Följ den här sidan för att lära dig mer om single page-applikationer, det vill säga du kan skapa ett program som fungerar likadant som ett datorprogram eller mobilprogram.
seo-description: Följ den här sidan för att lära dig mer om single page-applikationer, det vill säga du kan skapa ett program som fungerar likadant som ett datorprogram eller mobilprogram.
uuid: d1865e79-6e7c-4149-95c0-556e61478b01
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: a5b5e40e-2457-45fe-9632-baf5008fe8bf
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Enkelsidiga program{#single-page-applications}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

[Single-Page Applications](https://en.wikipedia.org/wiki/Single-page_application) (SPA) har nått en kritisk massa som allmänt anses vara det mest effektiva mönstret för att skapa sömlösa upplevelser med webbteknik. Genom att följa ett SPA-mönster kan du skapa ett program som fungerar likadant som ett skrivbordsprogram eller mobilprogram, men som når en mängd olika enhetsplattformar och formfaktorer på grund av sin grund i öppna webbstandarder.

I allmänhet verkar SPA-program mer avancerade än traditionella sidbaserade webbplatser, eftersom de vanligtvis läser in en hel HTML-sida **endast en gång** (inklusive CSS, JS och teckensnittsinnehåll som stöds) och sedan bara läser in exakt det som är nödvändigt varje gång en lägesändring inträffar i programmet. Vad som är nödvändigt för den här tillståndsändringen kan variera beroende på vilken uppsättning tekniker som väljs, men innehåller vanligtvis ett enda HTML-fragment som ersätter den befintliga vyn, och körningen av ett JS-kodblock som gör att den nya vyn kan visas och utföra eventuell mallåtergivning på klientsidan som behövs. Den här lägesändringens hastighet kan förbättras ytterligare genom stöd för mekanismer för mallcachelagring, eller till och med offlineåtkomst till mallinnehåll om Adobe PhoneGap används.

AEM 6.1 har stöd för utveckling och hantering av SPA-program via AEM-appar. I den här artikeln ges en introduktion till begreppen bakom SPA och hur de utnyttjar [AngularJS](https://angularjs.org/) för att föra ert varumärke till App Store och Google Play.

## SPA i AEM-appar {#spa-in-aem-apps}

Single-Page Application Framework i AEM Apps möjliggör höga prestanda för en AngularJS-app, samtidigt som författare (eller annan icke-teknisk personal) kan skapa och hantera appens innehåll via den pekoptimerade dra och släpp-redigeringsmiljön som traditionellt har reserverats för hantering av webbplatser. Har du redan skapat en webbplats med AEM? Det är enkelt att återanvända innehåll, komponenter, arbetsflöden, resurser och behörigheter med AEM-appar.

## AngularJS Application Module {#angularjs-application-module}

AEM-appar hanterar mycket av AngularJS-konfigurationen åt dig, inklusive att sätta samman appens modul på den översta nivån. Som standard heter den här modulen&quot;AEMAngularApp&quot; och skriptet som ansvarar för dess generering finns på /libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp.

En del av initieringen av din app är att ange vilka AngularJS-moduler appen är beroende av. Listan med moduler som används av din app anges av ett skript som finns på /libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp, och kan överlappas av dina egna programs sidkomponent för att dra in ytterligare AngularJS-moduler som din app kräver. Jämför till exempel ovanstående skript med Geometrixx-implementeringen (finns på /apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp).

För att ge stöd för navigering mellan de olika lägena i appen itererar skriptet angular-app-module igenom alla underordnade sidor på appsidan på den översta nivån för att generera en uppsättning rutter och konfigurerar varje sökväg på Angular&#39;s $routeProvider service. Ett exempel på hur detta ser ut i praktiken är hur du tittar på skriptet för vinkelmodulen app som genereras av appexemplet Geometrixx Outdoor: (länk kräver en lokal instans) [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

Om du loggar in på den genererade AEMAngularApp hittar du en serie vägar som anges enligt följande:

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

Exemplet ovan visar i synnerhet ett exempel på hur en parameter skickas som en del av banan. I det här exemplet anger vi att när en sökväg som uppfyller det angivna mönstret (/content/phonegap/geometrixx-outdoor/en/home/products/:id) begärs, ska den hanteras av mallen home/products.template.html och använda kontrollenheten&quot;contentphonegapgeometrixxoutdoorsenhomeproducts&quot;.

Den mall som ska läsas in när den här vägen begärs anges av egenskapen templateUrl. Den här mallen innehåller HTML från AEM-komponenter som har inkluderats på sidan samt eventuella AngularJS-direktiv som krävs för att ansluta klientsidan av programmet. Om du vill se ett exempel på ett AngularJS-direktiv i en Geometrixx-komponent kan du titta på rad 45 i swipe-carousels template.jsp (/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp).

## Sidkontroller {#page-controllers}

I vinkelns egna ord är&quot;en styrenhet är en JavaScript-konstruktorfunktion som används för att förstärka vinkelomfånget&quot;. ([källa](https://docs.angularjs.org/guide/controller)) Varje sida i en AEM-app ansluts automatiskt till en styrenhet som kan utökas av en styrenhet som anger en `frameworkType` av `angular`. Ta en titt på ng-text-komponenten som ett exempel (/libs/mobileapps/components/angular/ng-text), inklusive cq:template-noden som ser till att den här komponenten läggs till på en sida varje gång den läggs till innehåller den här viktiga egenskapen.

Om du vill ha ett mer komplext exempel på en kontrollenhet öppnar du skriptet ng-template-page controller.jsp (finns på /apps/geometrixx-outdoor-app/components/angular/ng-template-page). Särskilt intressant är den javascript-kod som genereras när den körs, som återges enligt följande:

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

I ovanstående exempel kommer du att märka att vi tar en parameter från `$routeParams` tjänsten och sedan masserar den i den katalogstruktur som våra JSON-data lagras i. Genom att hantera sku `id` på det här sättet kan vi leverera en enda produktmall som kan återge produktdata för potentiellt tusentals olika produkter. Det här är en mycket mer skalbar modell som kräver en individuell väg för varje objekt i en (potentiellt) enorm produktdatabas.

Det finns också två komponenter här: ng-product extensions with the data it extract from the above `$http` call. Det finns också en ng-image på den här sidan som i sin tur ökar omfattningen med det värde som hämtas från svaret. Med hjälp av Angulles `$http` tjänst väntar varje komponent tålmodigt tills begäran är klar och det löfte den gav är uppfyllt.

## Nästa steg {#the-next-steps}

När du har lärt dig mer om Single Page-program kan du läsa [Utveckla appar med PhoneGap CLI](/help/mobile/phonegap-apps-pg-cli.md).
