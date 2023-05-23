---
title: AEM Mobile innehållspersonalisering
seo-title: AEM Mobile content personalization
description: Följ den här sidan för att lära dig mer om AEM Mobile innehållspersonaliseringsfunktion som gör det möjligt för AEM att personalisera mobilappsinnehåll genom att utnyttja Adobe Target.
seo-description: Follow this page to learn about AEM Mobile content personalization feature that allows AEM authors to personalize mobile app content by leveraging Adobe Target.
uuid: 9078edd1-8399-485f-8a63-a07e766f7ef9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c9c818dc-c5c4-4a96-94fe-9dc9fe75705b
exl-id: 70d7ee0d-2f6d-4f97-a6e2-b02d84a0ca42
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '2673'
ht-degree: 0%

---

# AEM Mobile innehållspersonalisering{#aem-mobile-content-personalization}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Det här dokumentet är en del av [Komma igång med AEM Mobile](/help/mobile/getting-started-aem-mobile.md) Guide, en rekommenderad startpunkt för AEM Mobile.

Med funktionen för innehållspersonalisering i AEM Mobile kan [AEM Authors](#author) personalisera mobilappsinnehåll genom att utnyttja [Adobe Target](https://www.adobe.com/ca/marketing-cloud/testing-targeting.html). Detta gör att man kan leverera riktade erbjudanden till användare av mobilappar. Adobe Experience Manager Mobile ger möjlighet att skapa, målinrikta och leverera innehåll som ger användaren innehåll som är specifikt för den egna smaken.

Så ofta är fallet i AEM, för att författare ska kunna börja skapa det här innehållet, måste administratörer och utvecklare först förbereda miljön.

[AEM](#administrator) måste upprätta en anslutning mellan AEM Mobile och Adobe Target Cloud Service.

AEM Mobile [utvecklare](#developer) måste ändra sina befintliga skript för att underlätta framtagning av riktat innehåll.

## För administratörer {#for-administrators}

Det finns ett antal steg som måste sammanställas innan innehållsförfattare kan börja generera riktat innehåll för mobilappar: Vi får rätt behörighetsgrupp för användare och grupper, skapar molntjänster, konfigurerar programmet för aktiviteten och till slut skapar innehållet.

I den här artikeln beskrivs hur du konfigurerar [AEM Mobile Hybrid Reference Application](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) för målinriktning.

Det förutsätts att AEM Mobile Hybrid Reference Application har distribuerats och är tillgängligt via AEM Mobile Dashboard.

Innan författare kan generera riktat innehåll i ett program måste AEM vara [konfigureras med Adobe Target-Cloud Servicen.](/help/mobile/aem-mobile-configuring-cloud-service.md)

### Behörigheter {#permissions}

Användare som behöver åtkomst till personaliseringskonsolen måste vara en del av `target-activity-authors` grupp.

Som en del av användar- och gruppinställningarna bör målaktivitetsgruppen läggas till i gruppen som administrerar program. Genom att lägga till gruppen target-activity-authors kan användarna se menyposten för personalisering.

>[!NOTE]
>
>Om du glömmer att lägga till de användare eller grupper som du vill ska ha tillgång till Admin Console för personalisering i gruppen target-activity-authors kommer det att förhindra användare från att se personaliseringskonsolen.

### Cloud Services {#cloud-services}

För att få målinriktat innehåll att fungera för mobilprogram finns det två tjänster som måste konfigureras: Adobe Target och Adobe Mobile Services. Adobe Target-tjänsten tillhandahåller motorn för bearbetning av klientförfrågningar och returnering av det anpassade innehållet. Tjänsten Adobe Mobile Services tillhandahåller anslutningen mellan Adobes tjänster och mobilprogrammet via filen ADBMomobileConfig.json som används av plugin-programmet AMS Cordova. Från AEM Mobile Dashboard kan du konfigurera programmet genom att lägga till de två tjänsterna.

På AEM Mobile Dashboard går du till Cloud Servicens Hantera och klickar på plusknappen (+).

![chlimage_1-38](assets/chlimage_1-38.png)

I guiden Lägg till Cloud Service väljer du molntjänstkortet&quot;Adobe Target&quot; och klickar på Nästa.

![chlimage_1-39](assets/chlimage_1-39.png)

I listrutan Välj en konfiguration kan du antingen skapa en ny konfiguration eller välja en befintlig konfiguration. Om du vill skapa en ny konfiguration väljer du Skapa konfiguration i listrutan. Ange en rubrik för målkonfigurationen. Ange klientkod, e-postadress och lösenord som är kopplade till ditt Target-konto. Om du inte känner till värdena för dessa fält kontaktar du Adobe Target support. Klicka på Verifiera för att validera inloggningsuppgifterna. Klicka på knappen Skicka för att skapa molntjänsten.

>[!NOTE]
>
>Molntjänsten som skapas kopplas automatiskt till mobilprogrammet via guiden. Egenskapsvärdet cq:cloudserviceconfigs ställs in på jcr:content-noden i programgruppsnoden. För hybridappexemplet ställs det in på /content/mobileapps/hybrid-reference-app/jcr:content med värdet som pekar på den automatiskt genererade ramverksnoden som finns på /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. Ramverksnoden har två egenskaper inställda som standard, kön och ålder. Ramverket används bara för AEM förhandsgranskning och påverkar inte enheten.

När guiden har slutförts innehåller rutan Hantera Cloud Service molntjänsten Target, men den innehåller en varning om att ett Adobe-mobiltjänstkonto saknas.

![chlimage_1-40](assets/chlimage_1-40.png)

### Adobe Mobile Services {#adobe-mobile-services}

Det är också nödvändigt att länka ett AMS-konto (Adobe Mobile Services) till programmet. AMS-tjänsten tillhandahåller den ADBMobleConfig.json-fil som krävs och som innehåller målklientens kodinformation. Innan du skapar en association med AMS-kontot måste AMS-kontot ändras av en användare som har behörighet till AMS.

### Klientkod {#client-code}

Om du vill logga in på AMS-tjänsterna går du till [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/)markerar du mobilprogrammet och klickar på inställningarna. Leta reda på fältet SDK-målalternativ, placera klientkoden i fältet och klicka på Spara.

![chlimage_1-41](assets/chlimage_1-41.png)

När nu klientkoden har kopplats till mobilprogrammet levereras inställningarna för tjänsten via ADBMobilConfig.json-filen när molntjänsten AMS har konfigurerats via Adobe Mobile Dashboard.

### Adobe Mobile Service Cloud Service {#adobe-mobile-service-cloud-service}

Nu när AMS har konfigurerats är det dags att associera mobilappen i Adobe Mobile Dashboard. På AEM Mobile Dashboard går du till Cloud Servicens Hantera och klickar på plusknappen (+).

![chlimage_1-42](assets/chlimage_1-42.png)

Markera Adobe Mobile Services-kortet och klicka på Next.

![chlimage_1-43](assets/chlimage_1-43.png)

Välj listrutan Mobiltjänst i steget Skapa eller Välj guide och välj posten Skapa konfiguration. Ange titel, företag, användarnamn, lösenord och välj lämpligt datacenter. Om du inte känner till de här värdena kontaktar du Adobe-administratören för mobila tjänster för att få dem. När alla fält har fyllts i klickar du på knappen Verifiera. Verifieringsprocessen går till AMS och verifierar kontots inloggningsuppgifter, och när valideringen är klar fylls en lista över mobilprogram i där du väljer det associerade mobilprogrammet i listrutan. Klicka på knappen Skicka för att slutföra guiden. Det kan ta en stund att hämta konfigurationsdata och associerade analyser till programmet. När processen är klar klickar du på knappen Klar på den modala för att återgå till instrumentpanelen för mobiler i Adobe.

Om du går tillbaka till Mobile Dashboard innehåller rutan Hantera Cloud Services AMS-molntjänsten. Du kommer också att lägga märke till att rutan Analysera mått fylls i med livscykelrapporter.

![chlimage_1-44](assets/chlimage_1-44.png)

## För författare {#for-authors}

**Krav:** Som nämnts ovan måste administratörer konfigurera anslutningen till Adobe Target-tjänsten innan författare kan generera nytt riktat innehåll.

När administratören har konfigurerat de två molntjänsterna och utvecklaren har konfigurerat hanteraren för mobilappserbjudanden kan innehållsförfattare nu börja generera målinriktade upplevelser.

När du redigerar riktat innehåll i en AEM Mobile-app följer du en liknande procedur som när du skapar AEM Sites:

Här finns en fullständig översikt över [Skapa riktat innehåll i AEM](/help/sites-authoring/personalization.md)

## För utvecklare {#for-developers}

AEM utvecklare som skapar mobilapplikationer bör fortsätta att följa de mönster som ofta används AEM under utvecklingen av komponenter. Här följer de steg som krävs för att innehållsförfattare ska kunna skapa riktat innehåll:

### Adobe Target ContentSync-hanterare {#adobe-target-contentsync-handlers}

Att leverera innehåll till användarens enhetsinnehåll genereras genom att de erbjudanden som skapas AEM innehållsförfattare återges. Det finns en ny hanterare för innehållssynkronisering som hanterar återgivningen av målerbjudanden. Med Hybrid Reference Application som exempel innehåller det engelska innehållspaketet ContentSyncConfig med en [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) hanterare. Nästa steg är avgörande för att återge erbjudanden till enheten. Hanteraren för mobileappoffers har en path-egenskap som identifierar sökvägen till den personaliseringsaktivitet som ska användas för programmet.

Om det till exempel finns en aktivitet som finns på */content/campaign/hybridref* kopiera den här sökvägen och klistra in den som ett värde till *bana* egenskapen för hanteraren mobileappoffers.

>[!NOTE]
>
>För Hybrid Reference Application finns två mobileappoffers-hanterare en för dev och en för produktioner.

När aktivitetssökvägen har angetts i mobileappoffers-hanterarens path-egenskap sparar du hanteraren. Hanteraren är nu redo att börja återge erbjudanden för våra mobila enheter.

### Återgivningsläge {#render-mode}

Hanteraren för mobileappoffers är annorlunda konfigurerad för publicerings- och utvecklingsinställningar. För publiceringsinställningar finns det en egenskap som heter *renderMode* med värdet *publicera* anges på cq:ContentSyncConfig-noden. Hanteraren mobileappoffers refererar till renderMode och, om den anges för publicering, ändrar mbox-ID:t som skapas. Som standard har rutor som skapas av AEM ett —author-värde tillagt till mbox-ID:t. Detta identifierar att aktiviteten inte har publicerats och bör använda den opublicerade kampanjen för erbjudandelösningar.

När innehåll mellanlagras via Adobe Mobile Dashboard betraktas mellanlagrat innehåll som produktionsklart innehåll och återges via den icke-dev-konfiguration för innehållssynkronisering. Om du återger på det här sättet tas —author bort från alla mbox-ID:n och en publicerad aktivitet förväntas bli tillgänglig på målservern. Kontrollera att aktiviteten har publicerats innan du testar mellanlagrat innehåll.

### Apputveckling för personalisering {#personalization-app-development}

#### Komponenter {#components}

Grunden för allt innehåll är vanligtvis en sidkomponent som utökar någon av de grundläggande AEM sidkomponenterna wcm/foundation/components/page eller foundation/components/page beroende på om du använder HTML eller JSP. Längden på dessa steg kommer att fokusera på att använda komponenten wcm/foundation/components/page. Den grundläggande strukturen för sidkomponenten är uppdelad i flera skript, där varje skript har det specifika syftet att låta utvecklaren ordna och åsidosätta koden om det behövs. De två skript som är intressanta för personalisering är head.html och body.html. De här två skripten utgör ett område där kod kan injiceras för att ge stöd åt kontextnavet, Cloud Servicens och mobilutveckling.

Här är en översikt över de två primära skripten som används för att aktivera målinriktning av innehåll.

#### head.html {#head-html}

För att författaren ska kunna ange sitt innehåll som mål måste målmenyn läggas till på sidan så att författaren kan ändra sammanhanget från redigeringsläge till målinriktningsläge. Om du vill aktivera den här funktionen bör utvecklaren ändra skriptet head.html så att det innehåller följande kodfragment nära den övre delen av head.html eller så nära den &lt;title>&lt;/title> -element som möjligt.

```xml
<meta data-sly-test="${!wcmmode.disabled}">
    <div data-sly-call="${clientLib.all @ categories='personalization.kernel'}" data-sly-unwrap></div>
    <div data-sly-resource="${'config' @ resourceType='cq/personalization/components/clientcontext_optimized/config'}" data-sly-unwrap></div>
    <div data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}" data-sly-unwrap></div>
</meta>
```

>[!NOTE]
>
>Observera att skriptet endast ska inkluderas när WCM-läget inte har inaktiverats så att skriptet inte inkluderas i den slutliga programkoden när WCM-läget är inaktiverat (mer information finns i avsnittet för ContentSync-hanteraren).

För att författarna ska kunna förhandsgranska målinnehållet måste redigeraren kunna hitta konfigurationen för Adobe Target molntjänst. Kodblocket nedan lägger till två viktiga skript. Först lägger du till möjligheten för sidan att hitta den associerade molntjänsten Target och ringa samtal till Adobe Target. Den andra är tillägget för kategorin cq.apps.targeting.

The **cq.apps.targeting** -kategorin åsidosätter standardkomponenten cq/personalization/component/target och använder mobilapparna/komponenterna/målkomponenten som renderar erbjudanden specifikt för användning i mobilappar. Mer information om detta finns under Målkomponent.

Koden ska läggas till i head.html och placeras precis före slutet av &lt;/head> -element.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-include="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" data-sly-unwrap></div>
    <meta data-sly-call="${clientLib.all @ categories='cq.apps.targeting'}" data-sly-unwrap></meta>
</div>
```

>[!NOTE]
>
>Observera att kodblocket kapslas i ett WCM-läge och inte inaktiveras. Därför börjar det bara spelas upp när innehållsförfattaren arbetar med att skapa innehåll. Molntjänstskripten läggs inte till i den genererade koden för mobilmiljön.

#### body.html {#body-html}

För att innehållsförfattaren ska kunna testa olika profiler måste skriptet body.html innehålla följande kodblock som det första underordnade elementet i body-elementet.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'clientcontext' @ resourceType='cq/personalization/components/clientcontext_optimized'}" data-sly-unwrap></div>
</div>
```

Den sista biten av koden som krävs finns längst ned i body.html. Den här kodbiten söker efter den associerade molntjänsten och injicerar lämplig målmotorkod.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'cloudservices' @ resourceType='cq/cloudserviceconfigs/components/servicecomponents'}" data-sly-unwrap></div>
</div>
```

### Referensprogram {#reference-application}

Exempel på head.html och body.html finns i [AEM Mobile Hybrid Reference Application](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) som visar var skriptblocken ska placeras i de två skripten.

### Hanterare för innehållssynkronisering {#content-sync-handlers}

När innehållsförfattaren är klar med att skapa innehåll för mobilprogrammet är nästa steg att hämta källan och skapa programmet, eller att mellanlagra innehållet som ska publiceras. Det finns ett antal steg som utvecklaren är involverad i för att detta ska hända. För att underlätta återgivningen av innehåll använder AEM Mobile synkhanterare för innehåll för att återge och paketera innehållet. En ny hanterare för innehållssynkronisering har introducerats för att återge anpassat innehåll. Hanteraren mobileappoffers vet hur man återger associerade målerbjudanden som har skapats av innehållsförfattaren. Hanteraren för mobileappoffers utökar uppdateringshanteraren för abstrakta sidor, därför liknar många av egenskaperna. Mer information om hanteraren för mobileappoffers har följande egenskaper.

<table>
 <tbody>
  <tr>
   <td><strong>Egenskap</strong></td>
   <td><strong>Värde</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>rewrite</td>
   <td>+ relativeParentPath<p> - "/"</p> </td>
   <td>Egenskapen rewrite identifierar hur sökvägar i innehållet ska skrivas om.</td>
  </tr>
  <tr>
   <td>includedPageTypes</td>
   <td><p>"cq/personalization/components/teaserpage",</p> <p>"cq/personalization/components/offerproxy"</p> </td>
   <td>Egenskapen includePageTypes är valfri och används som standard för sidor med resurstyperna cq/personalization/components/teaserpage och cq/personalization/components/offerproxy. De här två resurstyperna är standardresurstyper som används när innehållet är avsett. Om ytterligare resurstyper måste stödjas bör de läggas till i listan med includePageTypes.</td>
  </tr>
  <tr>
   <td>locationRoot</td>
   <td>/content/mobileapps/&lt;app&gt;</td>
   <td>Appens plats.</td>
  </tr>
  <tr>
   <td>type</td>
   <td>mobileappoffers</td>
   <td>Namnet på hanteraren som är mobileappoffers.</td>
  </tr>
  <tr>
   <td>väljare</td>
   <td>Standard</td>
   <td>Standardväljaren används för att återge målinnehållet. </td>
  </tr>
  <tr>
   <td>targetRootDirectory</td>
   <td>www</td>
   <td>Rotkatalogen där det återgivna innehållet ska sparas.</td>
  </tr>
  <tr>
   <td>includeImages</td>
   <td>true | false</td>
   <td>Om true återges alla bilder som ingår i erbjudandet. Om false-bilder hoppas över.</td>
  </tr>
  <tr>
   <td>includeVideos</td>
   <td>true | false</td>
   <td>Om värdet är true återges alla videor som ingår i erbjudandet. Om false-videor hoppas över.</td>
  </tr>
  <tr>
   <td>bana</td>
   <td>/content/campaign/&lt;brand&gt;</td>
   <td>pekar på kampanjens varumärke som erbjudandena deltar i. För närvarande måste alla erbjudanden komma från samma kampanj.</td>
  </tr>
  <tr>
   <td>djup</td>
   <td>true | false</td>
   <td>Om värdet är true återges alla underordnade sidor rekursivt, och false returneras inte. </td>
  </tr>
  <tr>
   <td>extension</td>
   <td>html</td>
   <td>Anger tillägget för resursen som återges. Ange som html så att sidorna har filnamnstillägget .html.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>The [AEM Mobile Hybrid Reference App](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) har standardkonfigurationen för hanteraren för mobileappoffer. Egenskapen path i exemplet är tom eftersom den beror på kampanjplatsen. När en Campaign-författare har skapat en Campaign bör programadministratören associera Campaign med hanteraren genom att ange egenskapen path så att den pekar på Campaign.

### Målkomponent {#target-component}

För att hjälpa till att återge innehåll specifikt för mobilprogram använder AEM Mobile mobilapparna/komponenterna/målkomponenten. Den mobila målkomponenten utökar cq/personalization/components/target-komponenten och åsidosätter skriptet engine_tnt.jsp. Genom att åsidosätta engine_tnt.jsp kan AEM Mobile styra det genererade HTML för mobilapparnas användningsfall. För varje komponent som har en innehållsförfattare som mål skapas en associerad mbox av engine_tnt.jsp.

För varje mbox är attributet **cq-targeting** har lagts till så att programutvecklare kan skriva egen kod som konsumerar och använder den som de vill. The [AEM Mobile Hybrid Reference App](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) har ett exempel på ett Angular-direktiv som använder attributet cq-targeting. Det är i högsta grad upp till mobilutvecklaren att bestämma när och hur innehåll ska ersättas. Det finns en mobil-SDK som levereras via AEM /etc/clientlibs/mobileapps/js/mobileapps.js som tillhandahåller ett API för att anropa tjänsten Adobe Targeting. Det är programutvecklaren som bestämmer när anropet ska göras enligt utformningen av programmet.

## Vad händer nu? {#what-s-next}

1. [Starta min appupplevelse från AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Hantera appens innehåll](/help/mobile/phonegap-manage-app-content.md)
1. [Bygg min applikation](/help/mobile/building-app-mobile-phonegap.md)
1. [Spåra appens prestanda med Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Leverera en personaliserad appupplevelse med Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Skicka viktiga meddelanden till mina användare](/help/mobile/phonegap-push-notifications.md)
