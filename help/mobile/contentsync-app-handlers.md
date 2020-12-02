---
title: Out of the Box App Handlers
seo-title: Out of the Box App Handlers
description: Följ den här sidan för att lära dig mer om användningsklara hanterare för Adobe PhoneGap Enterprise med AEM.
seo-description: Följ den här sidan för att lära dig mer om användningsklara hanterare för Adobe PhoneGap Enterprise med AEM.
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 0%

---


# Out of the Box App Handlers{#out-of-the-box-app-handlers}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

Se följande riktlinjer för utveckling av Hanterare för innehållssynkronisering:

* Hanterare måste implementera *com.day.cq.contentsync.handler.ContentUpdateHandler* (antingen direkt eller genom att utöka en klass som gör det)
* Hanterare kan utöka *com.adobe.cq.moile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* Hanteraren får bara rapportera true om de uppdaterade ContentSync-cachen. Felaktig rapportering av true tillåter AEM att skapa en uppdatering.
* Hanteraren bör bara uppdatera cacheminnet om innehållet faktiskt ändras. Skriv inte till cacheminnet om en vit bild inte behövs och undvik att skapa en onödig uppdatering.

## Out of the Box Handlers {#out-of-the-box-handlers}

I följande lista visas färdiga apphanterare:

**mobileapppagesÅterger** appsidor.

* ***type - String***  - mobileapppages
* ***path - String***  - path to a page
* ***extension - String***  - Extension that should be used in the request. För sidor är detta nästan alltid *html*, men andra är fortfarande möjliga.

* ***väljare - Sträng***  - Valfria väljare avgränsade med punkt. Vanliga exempel är *touch* för återgivning av mobilversioner av en sida.

* ***deep - Boolean***  - Valfri boolesk egenskap som även avgör om underordnade sidor ska inkluderas. Standardvärdet är *true.*

* ***includeImages - Boolean***  - Valfri boolesk egenskap som avgör om bilder ska inkluderas. Standardvärdet är *true*.

   * Som standard beaktas endast bildkomponenter med en resurstyp för grund/komponenter/bild.

* ***includeVideos - Boolean***  - Valfri boolesk egenskap avgör om videoklipp ska inkluderas. Standardvärdet är *true*.

* ***includeModifiedPagesOnly - Boolean*** - Om värdet är false eller utelämnas återger du alla sidor och kontrollerar uppdateringarna vid återgivningen. Om värdet är true tonas basen av ändringar av sidorna lastModified.
* ***+ rewrite (node)***
   ***- relativeParentPath - String***  - sökvägen som alla andra sökvägar ska skrivas i förhållande till.

>[!NOTE]
>
>Resurstypen för de bild- och videokomponenter som påverkas av den här hanteraren anges genom att egenskaperna för *com.adobe.cq.mogallan.platform.impl.contentsync.handler* konfigureras.*Tjänsten* MobilePagesUpdateHandler OSGi.

**mobilepage** resurserSamlar resurser på appsidor.

**mobilecontentlisting** Visar innehållet i zip-filen ContentSync. Detta används av klientsidan js på enheten för att utföra den initiala filkopiering som krävs för AEM program.

Hanteraren bör läggas till i alla AEM Apps ContentSync Config.

* ***type - String - mobilecontentlisting***
* ***path*** - String - keep empty, must be present to be be displayed as a valid handler, but path is included to be the current ContentSync cache. Detta värde ignoreras.
* ***targetRootDirectory* -**String - det prefix som ska läggas till i sökvägar som målrot för innehållsuppdatering för hanteraren.
* ***order - Long* -**Order for ContentSync för att köra hanteraren. Det här talet ska anges högre än alla andra hanterare, till exempel 100. Den ska köras efter traditionella innehållshanterare.

```xml
{
  "files": [
    "config.xml",
    "res/screens/ios/screen-ipad-portrait-2x.png",
    "res/screens/ios/screen-ipad-landscape.png",
    "res/screens/ios/screen-iphone-portrait-2x.png",
    "res/screens/ios/screen-iphone-landscape.png",
    "res/screens/ios/screen-iphone-portrait.png",
    "apps/weretail-app/components/splash-page/clientlibs.css",
    ...
    "pge-content-packages.json"
  ],
  "count": 382,
  "lastModified": 1422902754733
}
```

**** mobilecontentpackageslistaVisar AEM innehållspaket i en viss app samt serverURL som uppdateringsbegäranden ska göras till. Detta används för att begära innehållsuppdateringar från klientsidan på enheten

Hanteraren ska användas i AEM App Shell ContentSync Config (nod med page-type=app-instance)

* ***type - String - mobilecontentpackageslista***
* ***path **-**String*** - Path to an app shell (node with page-type=app-instance).
* ***targetRootDirectory - String***  - det prefix som ska läggas till i sökvägar som målrot för innehållsuppdatering för hanteraren.
* ***order - Long* -**Order for ContentSync för att köra hanteraren. Det här talet ska anges högre än alla andra hanterare, till exempel 100. Den ska köras efter traditionella innehållshanterare.

>[!NOTE]
>
>Följande kodblock är inte en exakt implementering och ska användas som ett referensexempel:

```xml
{
  "content": [
    {
      "name": "en",
      "title": "We Retail Mobile App - English",
      "type": "CONTENT",
      "path": "/content/phonegap/weretail-outdoors/en",
      "updatePath": "/content/phonegap/weretail/en/jcr:content/pge-app/app-config"
    },
    {
      "name": "shell",
      "title": "We Retail Mobile App",
      "type": "INSTANCE",
      "path": "/content/phonegap/weretail-outdoors/shell",
      "updatePath": "/content/phonegap/weretail/shell/jcr:content/pge-app/app-config"
    }
  ],
  "serverURL": "http://localhost:4503/"
}
```

**widgetconfig** Innehåller en uppdaterad config.xml som sammanfogar alla redigeringar som gjorts via kommandocentralen med en angiven config.xml. Om den här hanteraren inte inkluderas ingen appinformation som ändras via administrationsgränssnittet i cachen.

Hanteraren ska användas i en AEM App Shell ContentSync-konfiguration (nod med page-type=[app-instance]).

* ***type - String* - **widgetconfig
* ***path **-**String*** - Path to any app shell child node (node with page-type=[app-instance]).
* ***targetRootDirectory - String***  - det prefix som ska läggas till i sökvägar som målrot för innehållsuppdatering för hanteraren.
* ***targetIconDirectory - String***  - den katalog som ikonerna för programmet ska placeras i

**mobileADBMomobileConfigJSONInkludera filen ADBMobleConfig.JSON om AMS-molntjänsten har konfigurerats.** 

Detta används vid kompileringen för att konfigurera AMS-plugin-programmet för analysstöd.

Hanteraren ska användas i AEM App Shell ContentSync Config (nod med page-type=app-instance)

* ***type - String*** - mobileADBMobleConfigJSON
* ***path - String***  - Path to an app shell (node with page-type=app-instance or a RT that extends /libs/mobileapps/core/components/instance)
* ***targetRootDirectory - String***  - det prefix som ska läggas till i sökvägar som målrot för innehållsuppdatering för hanteraren

**meddelandenconfigExtraherar** meddelandekonfigurationer som krävs på enheten. Egenskaperna extraheras från respektive push-tjänstmolntjänstkonfiguration som är kopplad till appen.

Egenskaper som inte är AEM i molntjänstens jcr:content-nod extraheras och läggs till i JSON-filen **page-notifications-config.json** för att inkluderas i programinnehållets www-rot.

AEM är de som är namnmellanrumsbaserade med&quot;cq&quot;,&quot;sling&quot; eller&quot;jcr&quot;. Andra egenskaper kan exkluderas med hjälp av egenskapen excludeProperties på konfigurationsnoden för innehållssynkronisering.

* ***type - String*** - notificationconfig
* ***excludeProperties - String[]*** - properties to exclude

**** contentSyncConfigInnehåller innehåll från en befintlig ContentSync-konfiguration.

* ***type - String***  - contentsyncconfigcontent
* ***path - String***  - Path to one of:

   * en annan ContentSync-konfiguration
   * till ett innehållspaket (använder egenskapen phonegap-exportTemplate för att hitta dess ContentSync-konfiguration)
   * till en mobilresurs (appinnehåll hittas under den resursen och, om innehållspaketen har en page-includeInBuild-egenskap som är true, används phonegap-exportTemplate för att hitta dess ContentSync-konfiguration)

* ***autoCreateFirstUpdateBeforeImport - Boolean*** - om true, skapar du en inledande  **** uppdatering i målkonfigurationen före import om det inte redan finns en sådan uppdatering

* ***autoFillBeforeImport - Boolean*** - om true, uppdatera/fyll målkonfigurationen innan import
* ***configSuffix - String***  - en sträng som ska läggas till i sökvägen som anges i egenskapen &quot;phonegap-exportTemplate&quot; för app-content. Detta kan användas för att skilja olika exportmallar åt. Den här egenskapen kan till exempel anges till **&quot;-dev&quot;** för att ange att *&quot;/../../../appconfig-dev&quot;* ska användas (till skillnad från *&quot;/../../../appconfig&quot;*).

**app-** assetsInkluderar alla resurser som är associerade med en programinstans. Hanteraren inkluderar alla resurser som hittas under den angivna sökvägen tillsammans med alla resurser som refereras av en programinstans appAssetPath-egenskap.

* ***type - String*** - app-assets

* ***path **-**String*** - path to a location under an app instance where app assets are stored

**** mobileappoffersEn ny synkhanterare för innehåll har introducerats för personalisering för att återge riktat innehåll. Hanteraren mobileappoffers vet hur man återger associerade målerbjudanden som har skapats av innehållsförfattaren. Hanteraren för mobileappoffers utökar den abstrakta siduppdateringshanteraren, vilket innebär att många av egenskaperna liknar varandra. Mer information om hanteraren för mobileappoffers har följande egenskaper.

Hanteraren för mobileappers utökar hanteraren för mobileappspages och lägger till följande egenskaper:

* ***locationRoot - String***  - ange platsen för mobilprogrammet
* ***includePageTypes - String*** - standard för stöd av cq/personalization/components/teaserpage och cq/personalization/components/offerproxy
* ***selector - String***  - should set to Standard
* ***path - String*** - the path to the campaign&#39;s brand

**Synkroniseringshanteraren för** mobileappconfig-innehåll ger ett sätt att mata in JSON-data i MobileAppsConfig.json. För att registrera en leverantörsklass lägger utvecklare till sin MobileAppsInfoProvider-klass med listan över providers. Hanteraren itererar över listan med MobileAppsInfoProviders och tillåter att providern matar in data i den resulterande JSON-filen. Listan med egenskaper som den här hanteraren stöder är:

* ***path **-**String*** - sökvägen till en programinstansnod med pge-type=app-instance eller en RT som utökar /libs/mobileapps/core/components/instance
* ***providers - String*** `[]` - the list of fully Qualified MobileAppsInfoProviders
* ***targetRootDirectory - String***  - katalogen där filen MobileAppsConfig.json ska skrivas.
* **fileName - String** - valfritt namn på filen som JSON ska skrivas till, standard är MobileAppsConfig.json

Det går att ha flera hanterare för mobilappconfig konfigurerade var och en med en unik uppsättning providers som skriver till olika JSON-filer.

### Testar hanterare för innehållssynkronisering {#testing-content-sync-handlers}

**Steg för att kontrollera cacheminnet** IntegrityClear

* Rensa cache
* Kör hanteraren (cachen har uppdaterats)
* Kör hanteraren igen (cachen bör inte uppdateras)

**Steg för felsökning**

* Kör konfigurationen
* Exportera din konfiguration eller granskning på enheten
* Om återgivningen misslyckas kontrollerar du om *stilar/resurser/libs* saknas eller söker efter felaktiga sökvägar till *stilar/resurser/libs*

**LoggingAktivera** ContentSync-felsökningsloggning via OSGI-loggningskonfigurationer i paketet  `com.day.cq.contentsync` Detta gör att du kan spåra vilka hanterare som har körts och om de har uppdaterat cachen och rapporterat att de har uppdaterat cachen.

## Ytterligare resurser {#additional-resources}

Mer information om roller och ansvar för en administratör och utvecklare finns i resurserna nedan:

* [Skapa för Adobe PhoneGap Enterprise med AEM](/help/mobile/phonegap.md)
* [Administrera innehåll för Adobe PhoneGap Enterprise med AEM](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>Klicka [här](/help/mobile/getting-started-aem-mobile.md) för att komma igång med utvecklingen av AEM Mobile-appar.

