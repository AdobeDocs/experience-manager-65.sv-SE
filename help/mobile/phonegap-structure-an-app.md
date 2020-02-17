---
title: Strukturera ett program
seo-title: Strukturera ett program
description: Följ den här sidan om du vill veta mer om hur du skapar en struktur för ett program. Den här sidan beskriver hur du strukturerar mallar och komponenter tillsammans med information om JavaScript och CSS Clientlibs.
seo-description: Följ den här sidan om du vill veta mer om hur du skapar en struktur för ett program. Den här sidan beskriver hur du strukturerar mallar och komponenter tillsammans med information om JavaScript och CSS Clientlibs.
uuid: bf0e8b0c-a075-4847-b56d-de458715027c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c614a7ff-0d13-4407-bda0-c0a402a13dcd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Strukturera ett program{#structure-an-app}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

Ett AEM Mobile-projekt innehåller en mängd olika innehållstyper, bland annat sidor, JavaScript- och CSS-klientbibliotek, återanvändbara AEM-komponenter, konfigurationer för innehållssynkronisering och PhoneGap-appskalinnehåll. Att bygga din nya AEM Mobile-app på [Starter Kit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) är ett bra sätt att få in alla olika typer av innehåll i vår rekommenderade struktur för att underlätta både bärbarhet och underhåll på lång sikt.

## Sidinnehåll {#page-content}

Sidorna i ditt program ska alla finnas under /content/mobileapps för att de ska kännas igen av AEM Mobile-konsolen.

![chlimage_1-52](assets/chlimage_1-52.png)

Enligt AEM-regeln bör den första sidan i appen vara en omdirigering till ett av programmets underordnade, som fungerar som standardspråk för appen (en i både Geometrixx- och Starter Kit-fall). Språksidan på den översta nivån ärver vanligtvis från startsidans grundkomponent (/libs/mobileapps/components/splash-page), som tar hand om den initiering som krävs för installation av innehållssynkroniseringsuppdateringar (contentInit-koden finns på /etc/clientlibs/mobile/content-sync/js/contentInit.js).

## Mallar och komponenter {#templates-and-components}

Mallen och komponentkoden för ditt program ska finnas i /apps/&lt;varumärkesnamn>/&lt;appnamn>. I enlighet med vedertagna regler bör du placera mallen och komponentkoden i /apps/&lt;varumärkesnamn>/&lt;programnamn>. Det här mönstret bör vara bekant för utvecklare som redan har arbetat med Site i AEM. Den följs vanligtvis när /apps/ är låst för anonym åtkomst som standard för publiceringsinstanser. Därför är din råa JSP-kod dold för potentiella angripare.

Appspecifika mallar kan konfigureras så att de bara presenteras med egenskapsnoden i själva mallen och genom att ange dess värde som /content/mobileapps(/. `allowedPaths`&amp;ast;)?&#39; - eller något mer specifikt om mallen bara ska kunna användas för ett enstaka program. Egenskaperna `allowedParents` och `allowedChildren` kan också användas för mycket detaljerad kontroll av vilka mallar som ska vara tillgängliga för en författare baserat på var den nya sidan skapas.

När du skapar en ny programsidkomponent från början bör du ställa in dess `sling:resourceSuperType` egenskap på&quot;mobileapps/components/angular/ng-page&quot;. Detta gör att sidan ställs in för både redigering och återgivning som ett enkelsidigt program och att du kan täcka över alla .jsp-filer som komponenten kan behöva ändra. Eftersom ng-page inte innehåller något gränssnittsramverk alls, kommer utvecklaren vanligtvis att lägga över (åtminstone) template.jsp (overlay from /libs/mobileapps/components/angular/ng-page/template.jsp).

Redigerbara sidkomponenter som vill utnyttja AngularJS har en motsvarande `sling:resourceSuperType` komponent som finns på /libs/mobileapps/components/angular/ng-component som kan överlappas och anpassas på samma sätt.

## JavaScript och CSS Clientlibs {#javascript-and-css-clientlibs}

När det gäller klientbibliotek finns det ett fåtal alternativ som utvecklaren kan välja var de ska placeras i databasen. Följande mönster kan användas som vägledning, men är inget svårt krav.

Om din klientsidkod kan stå fristående och inte relaterar till en viss komponent i programmet, vilket innebär att den kan återanvändas i andra program, rekommenderar vi att du lagrar den i /etc/clientlibs/&lt;varumärkesnamn>/&lt;lib name>. Om klientlib däremot är specifikt för ett fristående program kan du kapsla det som underordnat till appens designnod; /etc/designs/phonegap///clientlibs. Den här kategorin av klientlib ska inte användas av andra libs och ska användas för att bädda in andra libs efter behov. Med dessa mönster slipper utvecklaren lägga till nya konfigurationer för innehållssynkronisering varje gång ett klientbibliotek läggs till i appen. I stället behöver utvecklaren bara uppdatera egenskapen&quot;embedding&quot; för appens designklipp. Ta till exempel en titt på konfigurationsnoden Geometrixx clientlibs-all Content Sync på /content/phonegap/geometrixx-outdoor/en/jcr:content/page-app/app-config/clientlibs-all.

Om klientsidans kod är nära kopplad till en viss komponent, placerar du den koden i ett klientbibliotek som är kapslat under komponentens plats i /apps/ och bäddar in dess kategori i programklienten.

## PhoneGap-konfiguration {#phonegap-configuration}

Varje AEM Mobile-app innehåller en katalog som är värd för de konfigurationsfiler som används av [kommandoradsgränssnittet](https://github.com/phonegap/phonegap-cli) för PhoneGap och [PhoneGap-bygget](https://build.phonegap.com/) för att göra webbinnehållet till ett körbart program. I Geometrixx-exemplet är den här katalogen (/content/phonegap/geometrixx-outdoor/shell/jcr:content/page-app/app-content) placerad som en del av Shell, ett designbeslut som fattas på grund av att det bara innehåller innehåll som inte kan uppdateras direkt, till exempel plugin-program som hanterar enhets-API:er och konfigurationen av själva appen.

I den här katalogen hittar du även ett antal [Cordova-kopplingar](https://cordova.apache.org/docs/en/edge/guide_appdev_hooks_index.md.html#Hooks%20Guide) som kan användas för att installera plugin-program, placera resursfiler på deras plattformsspecifika platser och andra åtgärder som ska utföras som en del av bygget. Obs! som ett alternativ till att hämta varje plugin-program som en del av bygget kan du följa mönstret i Kitchen Sink-appen och [inkludera plugin-källkod](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) i resten av programprojektet.

## Nästa steg {#the-next-steps}

När du har lärt dig mer om appens struktur kan du läsa [Skapa och redigera appar med App Console](/help/mobile/phonegap-apps-console.md).
