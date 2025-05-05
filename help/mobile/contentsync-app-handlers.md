---
title: Out of the Box App Handlers
description: Följ den här sidan för att lära dig mer om användningsklara hanterare för Adobe PhoneGap Enterprise med AEM.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 0%

---

# Out of the Box App Handlers{#out-of-the-box-app-handlers}

{{ue-over-mobile}}

Se följande riktlinjer för utveckling av Hanterare för innehållssynkronisering:

* Hanterare måste implementera *com.day.cq.contentsync.handler.ContentUpdateHandler* (antingen direkt eller genom att utöka en klass som gör det)
* Hanterare kan utöka *com.adobe.cq.moile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* Hanteraren får bara rapportera true om de uppdaterade ContentSync-cachen. Felaktig rapportering av true tillåter AEM att skapa en uppdatering.
* Hanteraren bör bara uppdatera cacheminnet om innehållet faktiskt ändras. Skriv inte till cacheminnet om en vit bild inte behövs och undvik att skapa en onödig uppdatering.

## Out-of-Box Handlers {#out-of-the-box-handlers}

I följande lista visas färdiga apphanterare:

**mobileapppages** Återger appsidor.

* ***type - String*** - mobileapppages
* ***path - String*** - path to a page
* ***extension - String*** - Tillägg som ska användas i begäran. För sidor är detta nästan alltid *html*, men andra är fortfarande möjliga.

* ***selector - String*** - Valfria väljare avgränsade med punkt. Vanliga exempel är *touch* för återgivning av mobilversioner av en sida.

* ***deep - Boolean*** - Valfri boolesk egenskap som avgör om underordnade sidor också ska inkluderas. Standardvärdet är *true.*

* ***includeImages - Boolean*** - Valfri boolesk egenskap som avgör om bilder ska inkluderas. Standardvärdet är *true*.

   * Som standard beaktas endast bildkomponenter med en resurstyp för grund/komponenter/bild.

* ***includeVideos - Boolean*** - Valfri boolesk egenskap avgör om videoklipp ska inkluderas. Standardvärdet är *true*.

* ***includeModifiedPagesOnly - Boolean*** - Om värdet är false eller utelämnas återges alla sidor och uppdateringar kontrolleras vid återgivningen. Om värdet är true tonas basen av ändringar av sidorna lastModified.
* ***+ omskrivning (nod)***
  ***- relativeParentPath - String*** - sökvägen för att skriva alla andra sökvägar relativt.

>[!NOTE]
>
>Resurstypen för de bild- och videokomponenter som påverkas av den här hanteraren anges genom att egenskaperna för *com.adobe.cq.moile.platform.impl.contentsync.handler* konfigureras.*Tjänsten MobilePagesUpdateHandler OSGi*.

**mobilepageassets** Samlar in resurser på appsidor.

**mobilecontentlisting** Visar innehållet i ContentSync zip. Detta används av klientsidan js på enheten för att utföra den initiala filkopiering som krävs för AEM program.

Hanteraren bör läggas till i alla AEM Apps ContentSync Config.

* ***type - String - mobilecontentlisting***
* ***path*** - String - keep empty, måste finnas för att kunna ses som en giltig hanterare, men path härleds till aktuell ContentSync-cache. Det här värdet ignoreras.
* ***targetRootDirectory* -**&#x200B;String - det prefix som ska läggas till i sökvägar som målrot för innehållsuppdatering för hanteraren.
* ***order - Long* -**&#x200B;Order for ContentSync to execute this handler. Det här talet ska anges högre än alla andra hanterare, till exempel 100. Den ska köras efter traditionella innehållshanterare.

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

**mobilecontentpackageslista** Visar AEM innehållspaket i en viss app och serverURL att göra uppdateringsbegäranden till. Detta används för att begära innehållsuppdateringar från klientsidan på enheten

Hanteraren ska användas i AEM App Shell ContentSync Config (nod med page-type=app-instance)

* ***type - String - mobilecontentpackageslisting***
* ***path &#x200B;**-**String*** - Sökväg till ett programskal (nod med page-type=app-instance).
* ***targetRootDirectory - String*** - det prefix som ska läggas till i sökvägar som målrot för innehållsuppdatering för hanteraren.
* ***order - Long* -**&#x200B;Order for ContentSync to execute this handler. Det här talet ska anges högre än alla andra hanterare, till exempel 100. Den ska köras efter traditionella innehållshanterare.

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

Hanteraren bör användas i en AEM App Shell ContentSync-konfiguration (nod med page-type=[app-instance]).

* ***type - String* - &#x200B;** widgetconfig
* ***path &#x200B;**-**String*** - Sökväg till en underordnad programgränssnittsnod (nod med page-type=[app-instance]).
* ***targetRootDirectory - String*** - det prefix som ska läggas till i sökvägar som målrot för innehållsuppdatering för hanteraren.
* ***targetIconDirectory - String*** - katalogen där ikonerna för programmet ska placeras

**mobileADBMomobileConfigJSON** Inkludera filen ADBMobleConfig.JSON om AMS-molntjänsten har konfigurerats.

Detta används vid kompileringen för att konfigurera AMS-plugin-programmet för analysstöd.

Hanteraren ska användas i AEM App Shell ContentSync Config (nod med page-type=app-instance)

* ***type - String*** - mobileADBMobleConfigJSON
* ***path - String*** - Sökväg till ett programskal (nod med pge-type=app-instance eller en RT som utökar /libs/mobileapps/core/components/instance)
* ***targetRootDirectory - String*** - det prefix som ska läggas till i sökvägar som målrot för innehållsuppdatering för hanteraren

**meddelandenconfig** Extraherar de meddelandekonfigurationer som krävs på enheten. Egenskaperna extraheras från respektive push-tjänstmolntjänstkonfiguration som är kopplad till appen.

Egenskaper som inte är AEM i molntjänstens jcr:content-nod extraheras och läggs till i JSON-filen **pge-notifications-config.json** för att inkluderas i programinnehållets www-rot.

AEM är de som är namnmellanrumsbaserade med&quot;cq&quot;,&quot;sling&quot; eller&quot;jcr&quot;. Andra egenskaper kan exkluderas med hjälp av egenskapen excludeProperties på konfigurationsnoden för innehållssynkronisering.

* ***type - String*** - meddelandenconfig
* ***excludeProperties - String[]*** - egenskaper som ska uteslutas

**contentsyncconfigcontent** Samlar in innehåll från en befintlig ContentSync-konfiguration.

* ***type - String*** - contentsyncconfigcontent
* ***path - String*** - Path to one of:

   * en annan ContentSync-konfiguration
   * till ett innehållspaket (använder egenskapen phonegap-exportTemplate för att hitta dess ContentSync-konfiguration)
   * till en mobilresurs (appinnehåll hittas under den resursen och, om innehållspaketen har en page-includeInBuild-egenskap som är true, används phonegap-exportTemplate för att hitta dess ContentSync-konfiguration)

* ***autoCreateFirstUpdateBeforeImport - Boolean*** - Om värdet är true skapar du en inledande **update** i målkonfigurationen innan du importerar om det inte redan finns en sådan uppdatering

* ***autoFillBeforeImport - Boolean*** - Om värdet är true måste målkonfigurationen uppdateras/fyllas i före importen
* ***configSuffix - String*** - en sträng som ska läggas till i sökvägen som anges i egenskapen &quot;phonegap-exportTemplate&quot; för programinnehåll. Detta kan användas för att skilja olika exportmallar åt. Den här egenskapen kan till exempel ställas in på **&quot;-dev&quot;** för att ange att *&quot;/../../../appconfig-dev&quot;* ska användas (till skillnad från *&quot;/../../../appconfig&quot;*).

**app-assets** Inkluderar alla resurser som är associerade med en programinstans. Hanteraren inkluderar alla resurser som hittas under den angivna sökvägen tillsammans med alla resurser som refereras av en programinstans appAssetPath-egenskap.

* ***type - String*** - app-assets

* ***sökväg &#x200B;**-**sträng*** - sökväg till en plats under en programinstans där appresurser lagras

**mobileappoffers** En ny innehållssynkroniseringshanterare har introducerats för Personalization-användningsfall för att återge målinnehåll. Hanteraren mobileappoffers vet hur man återger associerade målerbjudanden som har skapats av innehållsförfattaren. Hanteraren för mobileappoffers utökar den abstrakta siduppdateringshanteraren, vilket innebär att många av egenskaperna liknar varandra. Mer information om hanteraren för mobileappoffers har följande egenskaper.

Hanteraren för mobileappers utökar hanteraren för mobileappspages och lägger till följande egenskaper:

* ***locationRoot - String*** - ange platsen för mobilprogrammet
* ***includePageTypes - String*** - som standard stöds cq/personalization/components/teaserpage och cq/personalization/components/offerproxy
* ***selector - String*** - ska anges som standard
* ***path - String*** - the path to the campaign&#39;s brand

**mobileappconfig** Hanteraren för innehållssynkronisering i mobileappconfig erbjuder ett sätt att mata in JSON-data i MobileAppsConfig.json. För att registrera en leverantörsklass lägger utvecklare till sin MobileAppsInfoProvider-klass med listan över providers. Hanteraren itererar över listan med MobileAppsInfoProviders och tillåter att providern matar in data i den resulterande JSON-filen. Listan med egenskaper som hanteraren stöder är:

* ***path &#x200B;**-**String*** - sökvägen till en programinstansnod med pge-type=app-instance eller en RT som utökar /libs/mobileapps/core/components/instance
* ***providers - String*** `[]` - listan med fullständigt kvalificerade MobileAppsInfoProviders
* ***targetRootDirectory - String*** - katalogen där filen MobileAppsConfig.json ska skrivas.
* **fileName - String** - valfritt namn på filen som JSON ska skrivas till, standard är MobileAppsConfig.json

Det går att ha flera hanterare för mobilappconfig konfigurerade var och en med en unik uppsättning providers som skriver till olika JSON-filer.

### Testar Content Sync-hanterare {#testing-content-sync-handlers}

**Steg för att kontrollera integriteten** Rensa cache

* Rensa cache
* Kör hanteraren (cache uppdaterad)
* Kör hanteraren igen (cachen bör inte uppdateras)

**Steg för felsökning**

* Kör konfigurationen
* Exportera din konfiguration eller granskning på enheten
* Om återgivningen misslyckas kontrollerar du om det saknas *format/resurser/libs* eller om det finns felaktiga sökvägar till *format/resurser/libs*

**Loggning** Aktivera ContentSync-felsökningsloggning via OSGI-loggningskonfigurationer i paketet `com.day.cq.contentsync` Detta gör att du kan spåra vilka hanterare som har körts och om de har uppdaterat cachen och rapporterat att cachen har uppdaterats.

## Ytterligare resurser {#additional-resources}

Mer information om roller och ansvar för en administratör och utvecklare finns i resurserna nedan:

* [Skapa för Adobe PhoneGap Enterprise med AEM](/help/mobile/phonegap.md)
* [Administrera innehåll för Adobe PhoneGap Enterprise med AEM](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>Klicka [här](/help/mobile/getting-started-aem-mobile.md) om du vill komma igång med utvecklingen av AEM Mobile-appar.
