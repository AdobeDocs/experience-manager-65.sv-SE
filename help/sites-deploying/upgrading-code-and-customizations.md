---
title: Uppgradera kod och anpassningar
seo-title: Uppgradera kod och anpassningar
description: Läs mer om hur du uppgraderar anpassad kod i AEM.
seo-description: Läs mer om hur du uppgraderar anpassad kod i AEM.
uuid: dec11ef0-bf85-4e4e-80ac-dcb94cc3c256
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 59780112-6a9b-4de2-bf65-f026c8c74a31
docset: aem65
targetaudience: target-audience upgrader
translation-type: tm+mt
source-git-commit: 5035c9630b5e861f4386e1b5ab4f4ae7a8d26149

---


# Uppgradera kod och anpassningar{#upgrading-code-and-customizations}

När man planerar en uppgradering måste man undersöka och åtgärda följande områden i en implementering.

* [Uppgradera kodbasen](#upgrade-code-base)
* [Justera med 6.5-databasstruktur](#align-repository-structure)
* [AEM-anpassningar](#aem-customizations)
* [Testförfarande](#testing-procedure)

## Översikt {#overview}

1. **Mönsteravkännare** - Kör mönsteravkännaren enligt beskrivningen i uppgraderingsplaneringen och beskrivs i detalj på [den här sidan](/help/sites-deploying/pattern-detector.md) för att få en mönsterdetektorrapport som innehåller mer information om områden som behöver åtgärdas utöver de otillgängliga API:erna/paketen i målversionen av AEM. Rapporten Mönsteridentifiering bör ge dig en indikation på eventuella inkompatibiliteter i koden, om det inte finns någon sådan, så är din distribution redan 6.5-kompatibel, du kan fortfarande välja att göra ny utveckling för att använda 6.5-funktionalitet, men du behöver den inte bara för att bibehålla kompatibiliteten. Om inkompatibiliteter rapporteras kan du välja att antingen a) köra i kompatibilitetsläge och skjuta upp utvecklingen för nya 6.5-funktioner eller kompatibilitet, b) välja att göra utvecklingen efter uppgraderingen och gå vidare till steg 2. Mer information finns i [Bakåtkompatibilitet i AEM 6.5](/help/sites-deploying/backward-compatibility.md) .

1. **Utveckla kodbas för 6.5 **- Skapa en dedikerad gren eller databas för kodbasen för Target-versionen. Använd information från Kompatibilitet före uppgradering för att planera områden med kod att uppdatera.
1. **Kompilera med 6.5 Uber jar **- Uppdatera källkodens POM till 6.5 uber jar och kompilera koden mot detta.
1. **Uppdatera AEM-anpassningar*** - *Alla anpassningar eller tillägg till AEM bör uppdateras/valideras för att fungera i 6.5 och läggas till i 6.5-kodbasen. Innefattar användargränssnittets sökformulär, anpassningar av resurser, allt som använder /mnt/overlay

1. **Driftsätt till 6.5-miljö** - En ren instans av AEM 6.5 (författare + publicering) bör stå upp i en Dev/QA-miljö. Uppdaterad kodbas och ett representativt urval av innehåll (från aktuell produktion) bör distribueras.
1. **QA-validering och felkorrigering** - QA ska validera programmet både i Author- och Publish-instanser av 6.5. Eventuella fel som hittas ska korrigeras och implementeras i 6.5-kodbasen. Upprepa Dev-Cycle tills alla fel är åtgärdade.

Innan du fortsätter med en uppgradering bör du ha en stabil programkodbas som har testats noggrant mot målversionen av AEM. Baserat på observationer som gjorts i testningen kan det finnas sätt att optimera den anpassade koden. Detta kan innefatta omfaktorisering av koden för att undvika att gå igenom databasen, anpassad indexering för att optimera sökningen eller användning av osorterade noder i JCR, bland annat.

Förutom möjligheten att uppgradera din kodbas och anpassa den till den nya AEM-versionen, hjälper 6.5 dig även att hantera dina anpassningar effektivare med funktionen Bakåtkompatibilitet som beskrivs på [den här sidan](/help/sites-deploying/backward-compatibility.md).

Som vi nämnt ovan och som visas i diagrammet nedan, kan du genom att köra [Mönsteravkännaren](/help/sites-deploying/pattern-detector.md) i det första steget göra det enklare att bedöma uppgraderingens totala komplexitet och om du vill köra i kompatibilitetsläge eller uppdatera dina anpassningar till alla nya AEM 6.5-funktioner. Mer information finns på sidan [Bakåtkompatibilitet i AEM 6.5](/help/sites-deploying/backward-compatibility.md) .
[ ![opt_cropped](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## Uppgradera kodbasen {#upgrade-code-base}

### Skapa en dedikerad gren för 6.5-kod i versionskontrollen {#create-a-dedicated-branch-for-6.5-code-in-version-control}

All kod och alla konfigurationer som krävs för din AEM-implementering bör hanteras med någon form av versionskontroll. En dedikerad gren i versionskontrollen bör skapas för att hantera ändringar som behövs för kodbasen i målversionen av AEM. Interaktiv testning av kodbasen mot målversionen av AEM och efterföljande felkorrigeringar hanteras i den här grenen.

### Uppdatera JAR-versionen för AEM Uber {#update-the-aem-uber-jar-version}

AEM Uber jar innehåller alla AEM API:er som ett enda beroende i Maven-projektets `pom.xml`. Det är alltid en god vana att inkludera Uber Jar som ett enda beroende i stället för att inkludera enskilda AEM API-beroenden. När du uppgraderar kodbasen bör du ändra Uber Jar-versionen så att den pekar på målversionen av AEM. Om ditt projekt utvecklades på en version av AEM innan Uber Jar fanns bör alla enskilda AEM API-beroenden tas bort och ersättas med en enda inkludering av Uber Jar för målversionen av AEM. Kodbasen ska sedan kompileras om mot den nya versionen av Uber Jar. Alla inaktuella API:er eller metoder bör uppdateras så att de är kompatibla med målversionen av AEM.

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

Användning av en administrativ session via `SlingRepository.loginAdministrative()` och `ResourceResolverFactory.getAdministrativeResourceResolver()` var mycket vanligt i kodbaser före AEM 6.0. Dessa metoder har tagits bort av säkerhetsskäl eftersom de ger för stor åtkomstnivå. [I framtida versioner av Sling kommer dessa metoder att tas bort](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication). Vi rekommenderar att du omfaktoriserar kod så att du kan använda tjänstanvändare i stället. Mer information om tjänstanvändare och [hur du fasar ut administrativa sessioner finns här](/help/sites-administering/security-service-users.md#how to phase out admin sessions).

### Frågor och ekindexvärden {#queries-and-oak-indexes}

All användning av frågor i kodbasen måste noggrant testas som en del av uppgraderingen av kodbasen. För kunder som uppgraderar från Jackrabbit 2 (versioner av AEM äldre än 6.0) är detta särskilt viktigt eftersom Oak inte indexerar innehåll automatiskt och anpassade index kan behöva skapas. Om du uppgraderar från en AEM 6.x-version kan det bero på att indexdefinitionerna för &quot;out of the box Oak&quot; har ändrats och kan påverka befintliga frågor.

Det finns flera verktyg för analys och granskning av frågeprestanda:

* [AEM Index Tools](/help/sites-deploying/queries-and-indexing.md)

* [Diagnostikverktyg för åtgärder - Frågeprestanda](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

* [Eak Utils](https://oakutils.appspot.com/). Detta är ett verktyg med öppen källkod som inte underhålls av Adobe.

### Klassisk gränssnittsredigering {#classic-ui-authoring}

Det går fortfarande att skapa klassiskt gränssnitt i AEM 6.5, men det är borttaget. Mer information finns [här](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release). Om ditt program körs i den klassiska användargränssnittets redigeringsmiljö rekommenderar vi att du uppgraderar till AEM 6.5 och fortsätter använda det klassiska användargränssnittet. Migrering till Touch-gränssnittet kan sedan planeras som ett separat projekt som ska slutföras under flera utvecklingscykler. För att kunna använda det klassiska användargränssnittet i AEM 6.5 måste flera OSGi-konfigurationer implementeras i kodbasen. Mer information om hur du konfigurerar detta finns [här](/help/sites-administering/enable-classic-ui.md).

## Justera med 6.5-databasstruktur {#align-repository-structure}

För att underlätta uppgraderingarna och säkerställa att konfigurationerna inte skrivs över under en uppgradering har databasen omstrukturerats i 6.4 för att skilja innehåll från konfiguration.

Därför måste ett antal inställningar flyttas så att de inte längre finns under `/etc` som tidigare. För att se över alla omstruktureringsproblem i databasen som måste ses över och anpassas i uppdateringen till AEM 6.4, se [Omstrukturering av databaser i AEM 6.4](/help/sites-deploying/repository-restructuring.md).

## AEM-anpassningar {#aem-customizations}

Alla anpassningar av AEM-redigeringsmiljön i källversionen av AEM måste identifieras. När du har identifierat dem rekommenderar vi att du lagrar alla anpassningar i versionskontrollen eller åtminstone säkerhetskopierar dem som en del av ett innehållspaket. Alla anpassningar bör driftsättas och valideras i en QA- eller mellanlagringsmiljö som kör målversionen av AEM före en produktionsuppgradering.

### Övertäckningar i allmänhet {#overlays-in-general}

Det är vanligt att utöka AEM-funktionaliteten genom att lägga över noder och/eller filer under /libs med ytterligare noder under /apps. Dessa övertäckningar bör spåras i versionskontroll och testas mot målversionen av AEM. Om en fil (oavsett om det är JS, JSP eller HTL) är överlagrad bör du lämna en kommentar om vilka funktioner som har förbättrats för enklare regressionstestning i målversionen av AEM. Mer information om övertäckningar finns [här](/help/sites-developing/overlays.md). Instruktioner för specifika AEM-övertäckningar finns nedan.

### Uppgraderar anpassade sökformulär {#upgrading-custom-search-forms}

Anpassade sökfaktorer kräver vissa manuella justeringar efter uppgraderingen för att de ska fungera korrekt. Mer information finns i [Uppgradera anpassade sökformulär](/help/sites-deploying/upgrading-custom-search-forms.md).

### Användargränssnittsanpassningar för resurser {#assets-ui-customizations}

>[!NOTE]
>
>Den här proceduren krävs endast för uppgraderingar från versioner äldre än AEM 6.2.

Instanser som har anpassade Assets-distributioner måste förberedas för uppgraderingen. Detta krävs för att säkerställa att allt anpassat innehåll är kompatibelt med den nya 6.4-nodstrukturen.

Du kan förbereda anpassningar av resursgränssnittet genom att göra följande:

1. Öppna CRXDE Lite på den instans som ska uppgraderas genom att gå till *https://server:port/crx/de/index.jsp*

1. Gå till följande nod:

   * `/apps/dam/content`

1. Byt namn på innehållsnoden till **content_backup**. Du kan göra detta genom att högerklicka på utforskarrutan till vänster i fönstret och välja **Byt namn**.

1. När noden har bytt namn skapar du en ny nod med namnet content under `/apps/dam` namngivet **content** och anger nodtypen till **sling:Folder**.

1. Flytta alla underordnade noder för **content_backup** till den nya innehållsnoden. Du kan göra detta genom att högerklicka på varje underordnad nod i utforskarrutan och välja **Flytta**.

1. Ta bort noden **content_backup** .

1. De uppdaterade noderna under `/apps/dam` med rätt nodtyp för `sling:Folder` bör helst sparas i versionskontrollen och distribueras med kodbasen eller åtminstone säkerhetskopieras som innehållspaket.

### Genererar resurs-ID:n för befintliga resurser {#generating-asset-ids-for-existing-assets}

Om du vill generera resurs-ID:n för befintliga mediefiler uppgraderar du mediefilerna när du uppgraderar din AEM-instans till att köra AEM 6.5. Detta krävs för att aktivera funktionen [](/help/assets/touch-ui-asset-insights.md)Resursinsikter. Mer information finns i [Lägga till inbäddningskod](/help/assets/touch-ui-using-page-tracker.md#add-embed-code).

Om du vill uppgradera resurser konfigurerar du paketet Associate Asset IDs i JMX-konsolen. Beroende på antalet resurser i databasen kan det `migrateAllAssets` ta lång tid. Våra interna tester beräknar cirka en timme för 125 000 tillgångar på TjärMK.

![1487758945977](assets/1487758945977.png)

Om du behöver resurs-ID:n för en delmängd av hela dina resurser använder du `migrateAssetsAtPath` -API:t.

Använd API:t för alla andra ändamål `migrateAllAssets()` .

### InDesign Script Customizations {#indesign-script-customizations}

Adobe rekommenderar att du placerar egna skript `/apps/settings/dam/indesign/scripts` där. Mer information om anpassning av InDesign-skript finns [här](/help/assets/indesign.md#configuring-the-aem-assets-workflow).

### Återställer ContextHub-konfigurationer {#recovering-contexthub-configurations}

ContextHub-konfigurationer genomförs med en uppgradering. Instruktioner om hur du återställer befintliga ContextHub-konfigurationer finns [här](/help/sites-administering/contexthub-config.md#recovery contexthub configurations after upgrade).

### Anpassningar av arbetsflöden {#workflow-customizations}

Det är vanligt att uppdatera ändringar som görs direkt i arbetsflöden för att lägga till eller ta bort funktioner som inte behövs. Ett vanligt arbetsflöde som är anpassat är arbetsflödet för DAM-uppdatering av resurser. Alla arbetsflöden som krävs för en anpassad implementering bör säkerhetskopieras och lagras i versionskontroll eftersom de kan skrivas över under en uppgradering.

### Redigerbara mallar {#editable-templates}

>[!NOTE]
>
>Den här proceduren krävs endast för webbplatsuppgraderingar som använder redigerbara mallar från AEM 6.2

Strukturen för redigerbara mallar har ändrats mellan AEM 6.2 och 6.3. Om du uppgraderar från 6.2 eller tidigare och om ditt webbplatsinnehåll byggs med redigerbara mallar måste du använda [verktyget](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration)för rensning av responsiva noder. Verktyget ska köras **efter** en uppgradering för att rensa upp innehållet. Den måste köras på både författarnivå och publiceringsnivå.

### Ändringar av CUG-implementering {#cug-implementation-changes}

Implementeringen av slutna användargrupper har ändrats avsevärt för att åtgärda prestandabegränsningar och skalbarhetsbegränsningar i tidigare versioner av AEM. Den tidigare versionen av CUG har tagits bort i 6.3 och den nya implementeringen stöds bara i Touch-gränssnittet. Om du uppgraderar från 6.2 eller tidigare finns instruktioner för att migrera till den nya CUG-implementeringen [här](/help/sites-administering/closed-user-groups.md#upgradetoaem63).

## Testförfarande {#testing-procedure}

En omfattande testplan bör utarbetas för testning av uppgraderingar. Testning av den uppgraderade kodbasen och programmet måste göras i lägre miljöer först. Alla buggar som hittas bör fixeras på ett iterativt sätt tills kodbasen är stabil, men endast då bör högre nivåmiljöer uppgraderas.

### Testa uppgraderingsproceduren {#testing-the-upgrade-procedure}

Uppgraderingsproceduren som beskrivs här bör testas i Dev- och QA-miljöer enligt din anpassade körningsbok (se [Planera uppgraderingen](/help/sites-deploying/upgrade-planning.md)). Uppgraderingsproceduren bör upprepas tills alla steg har dokumenterats i uppgraderingsboken och uppgraderingsprocessen är smidig.

### Implementeringstestområden {#implementation-test-areas-}

Nedan visas viktiga delar av en AEM-implementering som bör ingå i testplanen när miljön har uppgraderats och den uppgraderade kodbasen har distribuerats.

<table>
 <tbody>
  <tr>
   <td><strong>Funktionellt testområde</strong></td>
   <td><strong>Beskrivning</strong></td>
  </tr>
  <tr>
   <td>Publicerade webbplatser</td>
   <td>Testa AEM-implementeringen och associerad kod på publiceringsnivån<br /> via dispatchern. Bör innehålla kriterier för siduppdatering och<br /> cacheogiltigförklaring.</td>
  </tr>
  <tr>
   <td>Redigering</td>
   <td>Testar AEM-implementeringen och associerad kod på författarnivån. Bör innehålla sidor, komponentredigering och dialogrutor.</td>
  </tr>
  <tr>
   <td>Integrering med Marketing Cloud-lösningar</td>
   <td>Validera integreringar med produkter som Analytics, DTM och Target.</td>
  </tr>
  <tr>
   <td>Integrering med system från tredje part</td>
   <td>Alla integreringar från tredje part ska valideras på både författarnivå och publiceringsnivå.</td>
  </tr>
  <tr>
   <td>Autentisering, säkerhet och behörigheter</td>
   <td>Alla autentiseringsmekanismer som LDAP/SAML bör valideras.<br /> Behörigheter och grupper ska testas på både författarnivå och publiceringsnivå<br /> .</td>
  </tr>
  <tr>
   <td>Frågor</td>
   <td>Anpassade index och frågor bör testas tillsammans med frågeprestanda.</td>
  </tr>
  <tr>
   <td>Anpassningar av användargränssnitt</td>
   <td>Tillägg eller anpassningar av AEM-gränssnittet i författarmiljön.</td>
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

En testplan bör skapas som omfattar de ovannämnda testområdena för implementering. I många fall är det bra att separera testplanen med uppgiftslistorna Skapat av och Publicera. Testplanen ska köras i Dev-, QA- och Stage-miljöer innan du uppgraderar produktionsmiljöer. Testresultat och prestandamått bör samlas in i lägre miljöer för att ge en jämförelse när du uppgraderar scen- och produktionsmiljöer.
