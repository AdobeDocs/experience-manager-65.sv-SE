---
title: Strukturera ett program
description: Följ den här sidan om du vill veta mer om hur du skapar en struktur för ett program. Den här sidan beskriver hur du strukturerar mallar och komponenter tillsammans med information om JavaScript och CSS Clientlibs.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: f37f239f-065b-44f8-acb1-93485b713b49
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 0%

---

# Strukturera ett program{#structure-an-app}

{{ue-over-mobile}}

Ett AEM Mobile-projekt innehåller en mängd olika innehållstyper, bland annat sidor, JavaScript- och CSS-klientbibliotek, återanvändbara AEM, Content Sync-konfigurationer och PhoneGap-appskalinnehåll. Att bygga din nya AEM Mobile-app på [Starter Kit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) är ett bra sätt att få in alla olika typer av innehåll i vår rekommenderade struktur för att underlätta både portabilitet och underhåll på lång sikt.

## Sidinnehåll {#page-content}

Sidorna för ditt program ska alla finnas under /content/mobileapps för att de ska identifieras av AEM Mobile-konsolen.

![chlimage_1-52](assets/chlimage_1-52.png)

Som AEM bör den första sidan i appen vara en omdirigering till ett av dess underordnade objekt, som fungerar som standardspråk för appen (en i både Geometrixx- och Starter Kit-fall). Språksidan på den översta nivån ärver vanligtvis från startsidans grundkomponent (/libs/mobileapps/components/splash-page), som tar hand om den initiering som krävs för installation av innehållssynkroniseringsuppdateringar (contentInit-koden finns på /etc/clientlibs/mobile/content-sync/js/contentInit.js).

## Mallar och komponenter {#templates-and-components}

Mallen och komponentkoden för ditt program ska vara i /apps/&lt;varumärkesnamn>/&lt;appnamn>. I enlighet med vedertagna regler bör du placera mallen och komponentkoden i /apps/&lt;varumärkesnamn>/&lt;programnamn>. Det här mönstret bör vara bekant för utvecklare som redan har arbetat med Site in AEM. Den följs vanligtvis när /apps/ är låst för anonym åtkomst som standard för publiceringsinstanser. Din råa JSP-kod är dold för potentiella angripare.

Appspecifika mallar kan konfigureras så att de bara presenteras med egenskapsnoden `allowedPaths` i själva mallen och dess värde anges till /content/mobileapps(/.&ast;)?&#39; - eller något mer specifikt om mallen bara ska kunna användas för ett enstaka program. Egenskaperna `allowedParents` och `allowedChildren` kan också användas för att finjustera vilka mallar som är tillgängliga för en författare baserat på var den nya sidan skapas.

När du skapar en programsideskomponent från grunden bör du ange egenskapen `sling:resourceSuperType` till&quot;mobileapps/components/angular/ng-page&quot;. Då konfigureras sidan för både redigering och återgivning som ett enkelsidigt program och du kan täcka över alla .jsp-filer som komponenten kan behöva ändra. Eftersom ng-page inte innehåller något gränssnittsramverk alls, blir utvecklaren vanligtvis överlagrad (åtminstone) template.jsp (overlay from /libs/mobileapps/components/angular/ng-page/template.jsp).

Redigerbara sidkomponenter som vill använda AngularJS har en motsvarande `sling:resourceSuperType`-komponent på /libs/mobileapps/components/angular/ng-component som kan överlappas och anpassas på samma sätt.

## JavaScript och CSS Clientlibs {#javascript-and-css-clientlibs}

I klientbibliotek finns det ett fåtal alternativ som utvecklaren kan välja var de ska placeras i databasen. Följande mönster kan användas som vägledning, men är inget svårt krav.

Om din klientsidkod kan stå för sig själv och inte gäller en viss komponent i programmet, vilket innebär att den kan återanvändas i andra program, rekommenderar Adobe att du lagrar den i /etc/clientlibs/&lt;varumärkesnamn>/&lt;lib name>. Om däremot klientlib är specifikt för ett fristående program kan du kapsla det som underordnat till din apps designnod, /etc/designs/phonegap/&lt;varumärkesnamn>/&lt;appnamn>/clientlibs. Använd inte denna clientlibs kategori med andra libs, utan bädda in andra libs efter behov. Med det här mönstret slipper utvecklaren lägga till nya konfigurationer för innehållssynkronisering varje gång ett klientbibliotek läggs till i appen. I stället behöver utvecklaren bara uppdatera egenskapen&quot;embed&quot; för appens designklipp. Titta till exempel på konfigurationsnoden Geometrixx clientlibs-all Content Sync på /content/phonegap/geometrixx-outdoor/en/jcr:content/page-app/app-config/clientlibs-all.

Om klientsidans kod är nära kopplad till en viss komponent placerar du den koden i ett klientbibliotek som är kapslat under komponentens plats i /apps/ och bäddar in dess kategori i appens &#39;design&#39;-klientlib.

## PhoneGap-konfiguration {#phonegap-configuration}

Varje AEM Mobile-program innehåller en katalog som är värd för de konfigurationsfiler som används av kommandoradsgränssnittet [i PhoneGap ](https://github.com/phonegap/phonegap-cli) och PhoneGap Build på `https://build.phonegap.com/` för att göra webbinnehållet till ett körbart program. I exemplet med Geometrixx är den här katalogen (/content/phonegap/geometrixx-outdoor/shell/jcr:content/page-app/app-content) placerad som en del av Shell. Ett designbeslut fattas eftersom den bara innehåller innehåll som inte kan uppdateras över hela flödet, till exempel plugin-program som hanterar enhets-API:er och konfigurationen av själva appen.

I den här katalogen finns även [Cordova-kopplingar](https://cordova.apache.org/docs/en/dev/guide/appdev/hooks/index.html#Hooks%20Guide) som kan användas för att installera plugin-program, placera resursfiler på deras plattformsspecifika platser och andra åtgärder som ska utföras som en del av bygget. Obs! Som ett alternativ till att hämta varje plugin-program som en del av bygget kan du följa mönstret för Kitchen Sink-appen och inkludera plugin-källkoden <!-- THIS URL IS 404 (https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) --> med resten av ditt appprojekt.

## Nästa steg {#the-next-steps}

När du har lärt dig mer om appens struktur kan du läsa [Skapa och redigera appar med App Console](/help/mobile/phonegap-apps-console.md).
