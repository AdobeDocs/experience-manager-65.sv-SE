---
title: Uppgradera kod och anpassningar
seo-title: Upgrading Code and Customizations
description: Läs mer om hur du uppgraderar kod och anpassningar i AEM.
seo-description: Learn more about upgrading custom code in AEM.
uuid: dec11ef0-bf85-4e4e-80ac-dcb94cc3c256
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 59780112-6a9b-4de2-bf65-f026c8c74a31
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: a36a310d-5943-4ff5-8ba9-50eaedda98c5
source-git-commit: e54c1d422f2bf676e8a7b0f50a101e495c869c96
workflow-type: tm+mt
source-wordcount: '2113'
ht-degree: 0%

---

# Uppgradera kod och anpassningar{#upgrading-code-and-customizations}

När man planerar en uppgradering måste man undersöka och åtgärda följande områden i en implementering.

* [Uppgradera kodbasen](#upgrade-code-base)
* [Justera med 6.5-databasstruktur](#align-repository-structure)
* [AEM](#aem-customizations)
* [Testförfarande](#testing-procedure)

## Översikt {#overview}

1. **Mönsteravkännare** - Kör mönsteravkännaren enligt beskrivningen i uppgraderingsplaneringen och beskrivs i detalj i [den här sidan](/help/sites-deploying/pattern-detector.md). Du får en mönsterdetektorrapport som innehåller mer information om områden som måste åtgärdas utöver de otillgängliga API:erna/paketen i målversionen av AEM. Rapporten Mönsteridentifiering ger dig en indikation på eventuella inkompatibiliteter i koden. Om det inte finns någon är din distribution redan 6.5-kompatibel. Du kan fortfarande välja att göra ny utveckling för att använda 6.5-funktioner, men du behöver den inte bara för att bibehålla kompatibiliteten. Om inkompatibiliteter rapporteras kan du välja att köra i kompatibilitetsläge och skjuta upp utvecklingen för nya 6.5-funktioner eller kompatibilitet. Eller så kan du välja att göra utvecklingen efter uppgraderingen och gå vidare till steg 2. Se [Bakåtkompatibilitet i AEM 6.5](/help/sites-deploying/backward-compatibility.md) för mer information.

1. **Utveckla kodbas för 6.5 **- Skapa en dedikerad gren eller databas för kodbasen för Target-versionen. Använd information från Kompatibilitet före uppgradering för att planera områden med kod att uppdatera.
1. **Kompilera med 6.5 Uber jar **- Uppdatera källkodens POM till 6.5 uber jar och kompilera koden mot den.
1. **Uppdatera AEM*** - *Alla anpassningar eller tillägg till AEM ska uppdateras/valideras så att de fungerar i 6.5 och läggas till i 6.5-kodbasen. Innehåller användargränssnittssökning i Forms, anpassning av resurser, allt som använder /mnt/overlay

1. **Distribuera till 6.5-miljö** - En ren instans av AEM 6.5 (Författare + Publicera) ska ställas upp i en Dev/QA-miljö. Uppdaterad kodbas och ett representativt urval av innehåll (från aktuell produktion) bör distribueras.
1. **QA-validering och felkorrigering** - QA bör validera programmet både i Author- och Publish-instanser av 6.5. Eventuella fel som hittas ska korrigeras och implementeras i 6.5-kodbasen. Upprepa Dev-Cycle tills alla fel är åtgärdade.

Innan du fortsätter med en uppgradering bör du ha en stabil programkodbas som har testats noggrant mot målversionen av AEM. Baserat på observationer från testningen kan det finnas sätt att optimera den anpassade koden. Det kan till exempel vara att omfaktorisera koden för att undvika att gå igenom databasen, anpassa indexeringen för att optimera sökningen eller använda osorterade noder i JCR, bland annat.

Förutom att du kan uppgradera din kodbas och anpassa den så att den fungerar med den nya AEM-versionen kan 6.5 också hantera dina anpassningar effektivare med funktionen Bakåtkompatibilitet som beskrivs på [den här sidan](/help/sites-deploying/backward-compatibility.md).

Som nämnts ovan och visas i diagrammet nedan, kör [Mönsteravkännare](/help/sites-deploying/pattern-detector.md) i det första steget kan hjälpa dig att bedöma hur komplicerad uppgraderingen är generellt. Det kan också hjälpa dig att avgöra om du vill köra i kompatibilitetsläge eller uppdatera dina anpassningar så att de använder alla nya AEM 6.5-funktioner. Se [Bakåtkompatibilitet i AEM 6.5](/help/sites-deploying/backward-compatibility.md) sida för mer information.
[![opt_cropped](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## Uppgradera kodbasen {#upgrade-code-base}

### Skapa en dedikerad gren för 6.5-kod i versionskontrollen {#create-a-dedicated-branch-for-6.5-code-in-version-control}

All kod och alla konfigurationer som krävs för AEM ska hanteras med någon form av versionskontroll. En dedikerad gren i versionskontrollen bör skapas för att hantera ändringar som behövs för kodbasen i målversionen av AEM. Interaktiv testning av kodbasen mot målversionen av AEM och efterföljande felkorrigeringar hanteras i den här grenen.

### Uppdatera den AEM Uber Jar-versionen {#update-the-aem-uber-jar-version}

AEM Uber jar innehåller alla AEM-API:er som ett enda beroende i Maven-projektets `pom.xml`. Det är alltid en god vana att inkludera Uber Jar som ett enda beroende i stället för att inkludera enskilda AEM API-beroenden. När du uppgraderar kodbasen ändrar du versionen av Uber Jar så att den pekar på målversionen av AEM. Om ditt projekt utvecklades på en version av AEM innan Uber Jar fanns, tar du bort alla enskilda AEM API-beroenden. Ersätt dem med en enda inkludering av Uber Jar för målversionen av AEM. Kompilera om kodbasen mot den nya versionen av Uber Jar. Uppdatera alla inaktuella API:er eller metoder så att de är kompatibla med målversionen av AEM.

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### Avveckla användningen av den administrativa resurslösaren {#phase-out-use-of-administrative-resource-resolver}

Användning av en administrativ session via `SlingRepository.loginAdministrative()` och `ResourceResolverFactory.getAdministrativeResourceResolver()` var vanligast i kodbaser före AEM 6.0. Dessa metoder har tagits bort av säkerhetsskäl eftersom de ger för stor åtkomstnivå. [I framtida versioner av Sling kommer dessa metoder att tas bort](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication). Vi rekommenderar att du omfaktoriserar kod så att du kan använda tjänstanvändare i stället. Mer information om tjänstanvändare och [hur du fasar ut administrativa sessioner finns här](/help/sites-administering/security-service-users.md#how-to-phase-out=admin-sessions).

### Frågor och ekindexvärden {#queries-and-oak-indexes}

All användning av frågor i kodbasen måste noggrant testas som en del av uppgraderingen av kodbasen. För kunder som uppgraderar från Jackrabbit 2 (versioner av AEM äldre än 6.0) är den här testningen särskilt viktig eftersom Oak inte indexerar innehåll automatiskt och anpassade index bör skapas. Om du uppgraderar från en AEM 6.x-version kan indexdefinitionerna för &quot;out of the box Oak&quot; ha ändrats och påverka befintliga frågor.

Följande verktyg är tillgängliga för att analysera och inspektera frågeprestanda:

* [AEM](/help/sites-deploying/queries-and-indexing.md)

* [Diagnostikverktyg för åtgärder - frågeprestanda](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

<!-- URL is 404 as of 04/24/23; commenting out * [Oak Utils](https://oakutils.appspot.com/). This is an open source tool that is not maintained by Adobe. -->

### Skapa klassiskt användargränssnitt {#classic-ui-authoring}

Klassisk gränssnittsredigering är fortfarande tillgängligt i AEM 6.5, men är nu föråldrat. Mer information finns [här](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release). Om ditt program körs i den klassiska användargränssnittets redigeringsmiljö bör du uppgradera till AEM 6.5 och fortsätta använda det klassiska användargränssnittet. Migrering till Touch-gränssnittet kan sedan planeras som ett separat projekt som kan slutföras under flera utvecklingscykler. Om du vill använda det klassiska användargränssnittet i AEM 6.5 måste flera OSGi-konfigurationer implementeras i kodbasen. Mer information om hur du gör konfigurationen finns [här](/help/sites-administering/enable-classic-ui.md).

## Justera med 6.5-databasstruktur {#align-repository-structure}

För att underlätta uppgraderingarna och säkerställa att konfigurationerna inte skrivs över under en uppgradering har databasen omstrukturerats i 6.4 för att skilja innehåll från konfiguration.

Därför måste flera inställningar flyttas så att de inte längre finns under `/etc` som tidigare varit fallet. För att se över alla omstruktureringsproblem i databasen som måste ses över och hanteras i den uppdaterade versionen till AEM 6.4, se [Omstrukturering av lager i AEM 6.4](/help/sites-deploying/repository-restructuring.md).

## AEM  {#aem-customizations}

Alla anpassningar av AEM redigeringsmiljö i källversionen av AEM måste identifieras. När du har identifierat dem rekommenderar vi att du lagrar alla anpassningar i versionskontrollen eller åtminstone säkerhetskopierar dem som en del av ett innehållspaket. Alla anpassningar bör driftsättas och valideras i en QA- eller mellanlagringsmiljö som kör målversionen av AEM före en produktionsuppgradering.

### Övertäckningar i allmänhet {#overlays-in-general}

Det är vanligt att utöka AEM genom att lägga över noder och/eller filer under /libs med ytterligare noder under /apps. Dessa övertäckningar bör spåras i versionskontroll och testas mot målversionen av AEM. Om en fil (till exempel JS, JSP och HTL) överlappas rekommenderar Adobe att du lämnar en kommentar om vilken funktion som utökats för enklare regressionstestning i målversionen av AEM. Mer information om övertäckningar finns i allmänhet [här](/help/sites-developing/overlays.md). Instruktioner för specifika AEM finns nedan.

### Uppgraderar Forms för anpassad sökning {#upgrading-custom-search-forms}

Anpassade sökytor kräver vissa manuella justeringar efter uppgraderingen för att fungera korrekt. Mer information finns i [Uppgraderar Forms för anpassad sökning](/help/sites-deploying/upgrading-custom-search-forms.md).

### Användargränssnittsanpassningar för resurser {#assets-ui-customizations}

>[!NOTE]
>
>Den här proceduren krävs endast för uppgraderingar från äldre versioner än AEM 6.2.

Instanser som har anpassade Assets-distributioner måste förberedas för uppgraderingen. Den här åtgärden är nödvändig för att säkerställa att allt anpassat innehåll är kompatibelt med den nya 6.4-nodstrukturen.

Du kan förbereda anpassningar av resursgränssnittet genom att göra följande:

1. Öppna CRXDE Lite genom att gå till den instans som ska uppgraderas *https://server:port/crx/de/index.jsp*

1. Gå till följande nod:

   * `/apps/dam/content`

1. Byt namn på innehållsnoden till **content_backup** genom att högerklicka på utforskarrutan till vänster i fönstret och välja **Byt namn**.

1. Skapa en nod med namnet content under när noden har bytt namn `/apps/dam` namngiven **innehåll** och ange dess nodtyp till **sling:mapp**.

1. Flytta alla underordnade noder för **content_backup** till noden för nytt innehåll genom att högerklicka på varje underordnad nod i utforskarrutan och välja **Flytta**.

1. Ta bort **content_backup** nod.

1. De uppdaterade noderna under `/apps/dam` med rätt nodtyp för `sling:Folder` bör helst sparas i versionskontrollen och distribueras med kodbasen eller åtminstone säkerhetskopieras som innehållspaket.

### Genererar resurs-ID:n för befintliga resurser {#generating-asset-ids-for-existing-assets}

Om du vill generera resurs-ID:n för befintliga resurser ska du uppgradera resurserna när du uppgraderar din AEM så att AEM 6.5 körs. Det här steget krävs för att aktivera [Funktionen för resursinsikter](/help/assets/asset-insights.md). Mer information finns i [Lägg till inbäddningskod](/help/assets/use-page-tracker.md#add-embed-code).

Om du vill uppgradera resurser konfigurerar du paketet Associate Asset IDs i JMX-konsolen. Beroende på antalet resurser i databasen, `migrateAllAssets` kan ta lång tid. Adobe interna tester beräknar ungefär en timme för 125000 resurser på tarMK.

![1487758945977](assets/1487758945977.png)

Om du behöver resurs-ID:n för en delmängd av dina hela resurser använder du `migrateAssetsAtPath` API.

För alla andra ändamål använder du `migrateAllAssets()` API.

### Anpassa InDesign-skript {#indesign-script-customizations}

Adobe rekommenderar att du skickar egna skript på `/apps/settings/dam/indesign/scripts` plats. Mer information om anpassning av InDesign Script finns [här](/help/assets/indesign.md#configuring-the-aem-assets-workflow).

### Återställer ContextHub-konfigurationer {#recovering-contexthub-configurations}

ContextHub-konfigurationer påverkas av en uppgradering. Instruktioner om hur du återställer befintliga ContextHub-konfigurationer finns [här](/help/sites-developing/ch-configuring.md#recovering-contexthub-configurations-after-upgrading).

### Anpassningar av arbetsflöden {#workflow-customizations}

Det är vanligt att du redigerar direkt i arbetsflödet för att lägga till eller ta bort funktioner som inte behövs. Ett vanligt arbetsflöde som är anpassat är [!UICONTROL DAM Update Asset] arbetsflöde. Alla arbetsflöden som krävs för en anpassad implementering bör säkerhetskopieras och lagras i versionskontroll eftersom de kan skrivas över under en uppgradering.

### Redigerbara mallar {#editable-templates}

>[!NOTE]
>
>Den här proceduren krävs endast för webbplatsuppgraderingar som använder Redigerbara mallar från AEM 6.2

Strukturen för redigerbara mallar har ändrats mellan AEM 6.2 och 6.3. Om du uppgraderar från 6.2 eller tidigare och om webbplatsinnehållet byggs med redigerbara mallar måste du använda [Verktyget Rensa responsiva noder](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration). Verktyget ska köras **efter** en uppgradering för att rensa upp i materialet. Kör på både författarnivå och publiceringsnivå.

### Ändringar av CUG-implementering {#cug-implementation-changes}

Implementeringen av stängda användargrupper har ändrats avsevärt för att åtgärda prestandabegränsningar och skalbarhetsbegränsningar i tidigare versioner av AEM. Den tidigare versionen av CUG har tagits bort i 6.3 och den nya implementeringen stöds bara i Touch-gränssnittet. Om du uppgraderar från 6.2 eller tidigare finns instruktioner för att migrera till den nya CUG-implementeringen [här](/help/sites-administering/closed-user-groups.md#upgradetoaem63).

## Testförfarande {#testing-procedure}

En omfattande testplan bör utarbetas för testning av uppgraderingar. Testning av den uppgraderade kodbasen och programmet måste göras i lägre miljöer först. Alla buggar som hittas bör fixeras på ett iterativt sätt tills kodbasen är stabil, men endast då bör högnivåmiljöer uppgraderas.

### Testa uppgraderingsproceduren {#testing-the-upgrade-procedure}

Uppgraderingsproceduren som beskrivs här bör testas i Dev- och QA-miljöer så som de beskrivs i din anpassade körbok (se [Planera din uppgradering](/help/sites-deploying/upgrade-planning.md)). Uppgraderingsproceduren bör upprepas tills alla steg har dokumenterats i uppgraderingsboken och uppgraderingsprocessen är smidig.

### Implementeringstestområden  {#implementation-test-areas-}

Nedan visas viktiga delar av AEM implementering som ska ingå i testplanen när miljön har uppgraderats och den uppgraderade kodbasen har distribuerats.

<table>
 <tbody>
  <tr>
   <td><strong>Funktionellt testområde</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>Publicerade webbplatser</td>
   <td>Testa AEM implementering och associerad kod på publiceringsnivån<br /> genom Dispatcher. Bör innehålla kriterier för siduppdateringar och<br /> cacheogiltigförklaring.</td>
  </tr>
  <tr>
   <td>Redigering</td>
   <td>Testar AEM implementering och associerad kod på författarnivån. Bör innehålla sidor, komponentredigering och dialogrutor.</td>
  </tr>
  <tr>
   <td>Integrering med Experience Cloud Solutions</td>
   <td>Validera integreringar med produkter som Analytics, DTM och Target.</td>
  </tr>
  <tr>
   <td>Integrering med tredjepartssystem</td>
   <td>Validera integreringar från tredje part på både författarnivå och publiceringsnivå.</td>
  </tr>
  <tr>
   <td>Autentisering, säkerhet och behörigheter</td>
   <td>Alla autentiseringsmekanismer som LDAP/SAML bör valideras.<br /> Behörigheter och grupper ska testas både för författare och publicering<br /> lager.</td>
  </tr>
  <tr>
   <td>Frågor</td>
   <td>Anpassade index och frågor bör testas tillsammans med frågeprestanda.</td>
  </tr>
  <tr>
   <td>Anpassningar av användargränssnitt</td>
   <td>Alla tillägg eller anpassningar av det AEM användargränssnittet i författarmiljön.</td>
  </tr>
  <tr>
   <td>Arbetsflöden</td>
   <td>Anpassade arbetsflöden och funktioner och/eller inte.</td>
  </tr>
  <tr>
   <td>Prestandatestning</td>
   <td>Belastningstestning bör utföras på både författarnivå och publiceringsnivå som simulerar verkliga scenarier.</td>
  </tr>
 </tbody>
</table>

### Dokumenttestplan och resultat {#document-test-plan-and-results}

En testplan bör skapas som omfattar de ovannämnda testområdena för implementering. Det är ofta klokt att separera testplanen med uppgiftslistorna Skapat av och Publicera. Testplanen bör köras i Dev-, QA- och Stage-miljöer innan du uppgraderar produktionsmiljöer. Testresultat och prestandamått bör samlas in i lägre miljöer för att ge en jämförelse när du uppgraderar scen- och produktionsmiljöer.
