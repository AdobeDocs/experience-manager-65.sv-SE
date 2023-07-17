---
title: Adobe Experience Manager Mobile innehållspersonalisering
description: Följ den här sidan för att lära dig mer om funktionen Adobe Experience Manager (AEM) för anpassning av mobilinnehåll, som gör att AEM kan anpassa mobilappsinnehåll med Adobe Target.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 70d7ee0d-2f6d-4f97-a6e2-b02d84a0ca42
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '2609'
ht-degree: 0%

---

# AEM Mobile innehållspersonalisering{#aem-mobile-content-personalization}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Det här dokumentet är en del av [Komma igång med AEM Mobile](/help/mobile/getting-started-aem-mobile.md) Guide, en rekommenderad startpunkt för AEM Mobile.

Med funktionen för innehållspersonalisering i AEM Mobile kan [AEM Authors](#author) för att personalisera mobilappsinnehåll genom att använda [Adobe Target](https://business.adobe.com/products/target/adobe-target.html). Detta gör att man kan leverera riktade erbjudanden till användare av mobilappar. Adobe Experience Manager Mobile ger möjlighet att skapa, målinrikta och leverera innehåll som ger användaren innehåll som är specifikt för den egna smaken.

I AEM måste administratörer och utvecklare först förbereda miljön för att kunna börja skapa det här innehållet.

[AEM administratörer](#administrator) måste upprätta en anslutning mellan AEM Mobile och Adobe Target Cloud Service.

AEM Mobile [utvecklare](#developer) måste redigera sina befintliga skript för att underlätta framtagning av riktat innehåll.

## För administratörer {#for-administrators}

Det finns flera steg som måste utföras innan innehållsförfattare kan börja generera riktat innehåll för mobilappar: Vi får rätt behörighetsgrupp för användare och grupper, skapar molntjänster, konfigurerar programmet för aktiviteten och till slut skapar innehållet.

I den här artikeln får du hjälp med att konfigurera [AEM Mobile Hybrid Reference Application](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) för målinriktning.

Det förutsätts att AEM Mobile Hybrid Reference Application har distribuerats och är tillgängligt via AEM Mobile Dashboard.

Innan författare kan generera riktat innehåll i ett program måste AEM vara [konfigureras med Adobe Target-Cloud Servicen.](/help/mobile/aem-mobile-configuring-cloud-service.md)

### Behörigheter {#permissions}

Användare som behöver åtkomst till personaliseringskonsolen måste vara en del av `target-activity-authors` grupp.

Som en del av användar- och gruppinställningarna bör målaktivitetsgruppen läggas till i gruppen som administrerar program. Genom att lägga till gruppen target-activity-authors kan användarna se menyposten för personalisering.

>[!NOTE]
>
>Om du glömmer att lägga till de användare eller grupper som du vill ska ha tillgång till Admin Console i personaliseringen i gruppen target-activity-authors, kan användarna inte se personaliseringskonsolen.

### Cloud Services {#cloud-services}

För att få målinriktat innehåll att fungera för mobilprogram finns det två tjänster som måste konfigureras: Adobe Target och Adobe Mobile Services. Adobe Target-tjänsten tillhandahåller motorn för bearbetning av klientförfrågningar och returnering av det anpassade innehållet. Tjänsten Adobe Mobile Services tillhandahåller anslutningen mellan Adobes tjänster och mobilprogrammet via filen ADBMomobileConfig.json som används av plugin-programmet AMS Cordova. Från AEM Mobile Dashboard kan du konfigurera programmet genom att lägga till de två tjänsterna.

Gå till Cloud Servicens Hantera på AEM Mobile Dashboard och klicka på plusknappen (+).

![chlimage_1-38](assets/chlimage_1-38.png)

I guiden Lägg till Cloud Service väljer du molntjänstkortet&quot;Adobe Target&quot; och klickar på Nästa.

![chlimage_1-39](assets/chlimage_1-39.png)

I listrutan Välj en konfiguration kan du antingen skapa en konfiguration eller välja en befintlig konfiguration. Om du vill skapa en konfiguration väljer du Skapa konfiguration i listrutan. Ange en rubrik för målkonfigurationen. Ange klientkod, e-postadress och lösenord som är kopplade till ditt Target-konto. Om du inte känner till värdena för dessa fält kan du kontakta Adobe Target support. Klicka på Verifiera för att validera inloggningsuppgifterna. Klicka på knappen Skicka för att skapa molntjänsten.

>[!NOTE]
>
>Molntjänsten som skapas kopplas automatiskt till mobilprogrammet via guiden. Egenskapsvärdet cq:cloudserviceconfigs ställs in på jcr:content-noden i programgruppsnoden. För hybridappexemplet ställs det in på /content/mobileapps/hybrid-reference-app/jcr:content med värdet som pekar på den automatiskt genererade ramverksnoden på /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. Ramverksnoden har två egenskaper inställda som standard, kön och ålder. Ramverket används bara för AEM förhandsgranskning och påverkar inte enheten.

När guiden har slutförts innehåller rutan Hantera Cloud Service molntjänsten Target. Det innehåller dock en varning om att ett Adobe-mobiltjänstkonto saknas.

![chlimage_1-40](assets/chlimage_1-40.png)

### Adobe Mobile Services {#adobe-mobile-services}

Det är också nödvändigt att länka ett AMS-konto (Adobe Mobile Services) till programmet. AMS-tjänsten tillhandahåller den ADBMobleConfig.json-fil som krävs och som innehåller målklientens kodinformation. Innan du skapar en association med AMS-kontot måste AMS-kontot ändras av en användare som har behörighet till AMS.

### Klientkod {#client-code}

Logga in på AMS-tjänsterna på [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/)markerar du mobilprogrammet och klickar på inställningarna. Leta reda på fältet SDK-målalternativ, placera klientkoden i fältet och klicka på Spara.

![chlimage_1-41](assets/chlimage_1-41.png)

När nu klientkoden har kopplats till mobilprogrammet levereras inställningarna för tjänsten via ADBMobilConfig.json-filen när molntjänsten AMS har konfigurerats via Adobe Mobile Dashboard.

### Adobe Mobile Service Cloud Service {#adobe-mobile-service-cloud-service}

Nu när AMS har konfigurerats är det dags att associera mobilappen i Adobe Mobile Dashboard. Gå till Cloud Servicens Hantera på AEM Mobile Dashboard och klicka på plusknappen (+).

![chlimage_1-42](assets/chlimage_1-42.png)

Markera Adobe Mobile Services-kortet och klicka på Next.

![chlimage_1-43](assets/chlimage_1-43.png)

Välj listrutan Mobiltjänst i steget Skapa eller Välj guide och välj posten Skapa konfiguration. Ange titel, företag, användarnamn, lösenord och välj lämpligt datacenter. Om du inte känner till de här värdena kontaktar du Adobe-administratören för mobiltjänsten för att få dem. När alla fält har fyllts i klickar du på **Verifiera**. Verifieringsprocessen går till AMS och verifierar kontots inloggningsuppgifter. När verifieringen är klar fylls en lista över mobilprogram i där du väljer det associerade mobilprogrammet i listrutan. Klicka **Skicka** för att slutföra guiden. Det kan ta en stund att hämta konfigurationsdata och associerade analyser till programmet. När processen är klar klickar du på **Klar** för att återgå till Adobe Mobile Dashboard.

Återgår till Mobile Dashboard och rutan Hantera Cloud Services innehåller AMS-molntjänsten. Observera också att rutan Analysera mått är ifylld med livscykelrapporter.

![chlimage_1-44](assets/chlimage_1-44.png)

## För författare {#for-authors}

**Krav:** Som nämnts ovan måste administratörer konfigurera anslutningen till Adobe Target-tjänsten innan författare kan generera nytt riktat innehåll.

När administratören har konfigurerat de två molntjänsterna och utvecklaren har konfigurerat hanteraren för mobilappserbjudanden kan innehållsförfattare nu börja generera målinriktade upplevelser.

När du redigerar riktat innehåll i en AEM Mobile-app följer du en liknande procedur som när du skapar AEM Sites:

Här finns en fullständig översikt över [Skapa riktat innehåll i AEM](/help/sites-authoring/personalization.md)

## För utvecklare {#for-developers}

AEM utvecklare som skapar mobilapplikationer bör fortsätta att följa de mönster som ofta används AEM under utvecklingen av komponenter. Här går Adobe igenom de steg som krävs för att innehållsförfattare ska kunna skapa riktat innehåll:

### Adobe Target ContentSync-hanterare {#adobe-target-contentsync-handlers}

För att leverera innehåll till användarens enhet genereras innehållet genom att de erbjudanden som skapas av AEM återges. För att hantera återgivningen av målerbjudanden finns det en ny hanterare för innehållssynkronisering som behandlar erbjudandena. Med Hybrid Reference Application som exempel innehåller det engelska (engelska) innehållspaketet ContentSyncConfig med en [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) hanterare. Nästa steg är avgörande för att återge erbjudanden till enheten. Hanteraren för mobileappoffers har en path-egenskap som identifierar sökvägen till den personaliseringsaktivitet som ska användas för programmet.

Om det till exempel finns en aktivitet på */content/campaign/hybridref*, kopiera den här sökvägen och klistra in den som ett värde på *bana* egenskapen för hanteraren mobileappoffers.

>[!NOTE]
>
>För Hybrid Reference Application finns det två mobileappoffers-hanterare, en för dev och en för produktioner.

När aktivitetssökvägen har angetts i mobileappoffers-hanterarens path-egenskap sparar du hanteraren. Hanteraren är nu redo att börja återge erbjudanden för mobila enheter.

### Återgivningsläge {#render-mode}

Hanteraren för mobileappoffers är annorlunda konfigurerad för publicerings- och utvecklingsinställningar. För publiceringsinställningar finns det en egenskap som heter *renderMode* med värdet *publicera* anges på cq:ContentSyncConfig-noden. Hanteraren mobileappoffers refererar till renderMode och redigerar, om den är inställd på publicering, det mbox-id som skapas. Som standard har rutor som skapas av AEM ett —author-värde tillagt till mbox-ID:t. Detta identifierar att aktiviteten inte har publicerats och bör använda den opublicerade kampanjen för erbjudandelösningar.

När innehåll mellanlagras via Adobe Mobile Dashboard betraktas mellanlagrat innehåll som produktionsklart innehåll och återges via den icke-dev-konfiguration för innehållssynkronisering. Om du återger på det här sättet tas —author bort från alla mbox-ID:n och en publicerad aktivitet förväntas bli tillgänglig på målservern. Innan du testar mellanlagrat innehåll måste du kontrollera att aktiviteten redan är publicerad.

### Apputveckling för personalisering {#personalization-app-development}

#### Komponenter {#components}

Grunden för allt innehåll är vanligtvis en sidkomponent som utökar någon av de grundläggande AEM sidkomponenterna wcm/foundation/components/page eller foundation/components/page beroende på om du använder HTML eller JSP. Längden på de här stegen fokuserar på att använda komponenten wcm/foundation/components/page. Den grundläggande strukturen för sidkomponenten är uppdelad i flera skript, där varje skript har det specifika syftet att låta utvecklaren ordna och åsidosätta koden om det behövs. De två skript som är intressanta för personalisering är head.html och body.html. De här två skripten utgör ett område där kod kan injiceras för att ge stöd åt kontextnavet, Cloud Servicens och mobilutveckling.

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
>Inkludera bara skriptet när WCM-läget är inaktiverat så att skriptet inte inkluderas i den slutliga programkoden när WCM-läget är inaktiverat (mer information finns i avsnittet för ContentSync-hanteraren).

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
>Kodblocket kapslas i ett WCM-läge och inaktiveras inte. Därför börjar det bara spelas upp när innehållsförfattaren arbetar med att skapa innehåll. Molntjänstskripten läggs inte till i den genererade koden för mobilmiljön.

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

När innehållsförfattaren är klar med att skapa innehåll för mobilprogrammet är nästa steg att hämta källan och skapa programmet, eller att mellanlagra innehållet som ska publiceras. Det finns flera steg som utvecklaren är involverad i för att detta ska hända. AEM Mobile använder Content sync-hanterare för att återge och paketera innehållet, vilket underlättar återgivningen av innehållet. En ny hanterare för innehållssynkronisering har introducerats för att återge anpassat innehåll. Hanteraren mobileappoffers vet hur man återger associerade målerbjudanden som har skapats av innehållsförfattaren. Hanteraren för mobileappoffers utökar uppdateringshanteraren för abstrakta sidor, därför liknar många av egenskaperna. Information om hanteraren för mobileappoffers har följande egenskaper.

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
   <td>Egenskapen includePageTypes är valfri och används som standard för sidor med resurstyperna cq/personalization/components/teaserpage och cq/personalization/components/offerproxy. De här två resurstyperna är standardresurstyper som används när innehållet är avsett. Om ytterligare resurstyper måste stödjas lägger du till dem i listan med includePageTypes.</td>
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
   <td>Om true återges alla bilder som ingår i erbjudandet. Om false hoppas bilder över.</td>
  </tr>
  <tr>
   <td>includeVideos</td>
   <td>true | false</td>
   <td>Om värdet är true återges alla videor som ingår i erbjudandet. Om false hoppas videoklipp över.</td>
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

För varje mbox är attributet **cq-targeting** har lagts till så att programutvecklare kan skriva egen kod som konsumerar och använder hur de vill. The [AEM Mobile Hybrid Reference App](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) har ett exempel på ett Angular-direktiv som använder attributet cq-targeting. Det är upp till utvecklaren av mobilapplikationer som bestämmer när och hur innehållet ska ersättas. Det finns en mobil-SDK som levereras via AEM /etc/clientlibs/mobileapps/js/mobileapps.js som tillhandahåller ett API för att anropa tjänsten Adobe Targeting. Det är programutvecklaren som bestämmer när anropet ska göras enligt utformningen av programmet.

## Vad händer nu? {#what-s-next}

1. [Starta min appupplevelse från AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Hantera appens innehåll](/help/mobile/phonegap-manage-app-content.md)
1. [Bygg min applikation](/help/mobile/building-app-mobile-phonegap.md)
1. [Spåra appens prestanda med Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Leverera en personaliserad appupplevelse med Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Skicka viktiga meddelanden till mina användare](/help/mobile/phonegap-push-notifications.md)
