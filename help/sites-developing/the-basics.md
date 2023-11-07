---
title: AEM Core Concepts
description: En översikt över de centrala begreppen för hur Adobe Experience Manager (AEM) är uppbyggt och hur man utvecklar vidare, inklusive förståelse av JCR, Sling, OSGi, Dispatcher, arbetsflöden och MSM.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: f6f32290-422e-4037-89d8-d9f414332e8e
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '3306'
ht-degree: 0%

---

# AEM Core Concepts {#aem-core-concepts}

>[!NOTE]
>
>Innan du börjar använda Adobe Experience Manager (AEM) rekommenderar Adobe att du slutför WKND-självstudiekursen i [Komma igång med att utveckla AEM Sites](/help/sites-developing/getting-started.md) -dokument. Den innehåller en översikt över AEM utvecklingsprocess och en introduktion till centrala koncept.

## Krav för utveckling av AEM {#prerequisites-for-developing-on-aem}

Du behöver följande kunskaper för att kunna utveckla AEM:

* Baskunskaper om webbtillämpningstekniker, inklusive:

   * cykeln request -response (XMLHttpRequest / XMLHttpResponse)
   * HTML
   * CSS
   * JavaScript

* Arbetskunskaper i Experience Server (CRX), inklusive Content Explorer
* För utveckling i det klassiska användargränssnittet krävs även grundläggande kunskaper i JSP (JavaServer Pages), inklusive möjligheten att förstå och ändra enkla JSP-exempel.

Vi rekommenderar att du läser och följer [Riktlinjer och bästa praxis](/help/sites-developing/dev-guidelines-bestpractices.md).

## Java™ Content Repository {#java-content-repository}

Java™ Content Repository (JCR), [JSR 283](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html), anger ett leverantörsoberoende och implementeringsoberoende sätt att få åtkomst till innehåll dubbelriktat på en detaljnivå i en innehållsdatabas.

Adobe Research (Schweiz) AG har en ledande specialiseringsbefattning.

The [JCR API 2.0](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) package, javax.jcr.&amp;ast; används för direkt åtkomst och redigering av databasinnehåll.

## Experience Server (CRX) och Jackrabbit {#experience-server-crx-and-jackrabbit}

Experience Server innehåller de Experience Services som AEM bygger på och som kan användas för att skapa anpassade program, och den bäddar in innehållsdatabasen baserat på Jackrabbit.

[Apache Jackrabbit](https://jackrabbit.apache.org/jcr/index.html) är en fullt kompatibel implementering av JCR API 2.0 med öppen källkod.

## Bearbetning av försäljningsbegäran {#sling-request-processing}

### Introduktion till Sling {#introduction-to-sling}

AEM byggs med [Sling](https://sling.apache.org/index.html), ett ramverk för webbapplikationer som bygger på REST-principer och som enkelt utvecklar innehållsorienterade applikationer. Sling använder en JCR-databas, t.ex. Apache Jackrabbit eller, om det finns AEM, CRX Content Repository som datalager. Sling har bidragit till Apache Software Foundation - mer information finns på Apache.

Med Sling är den typ av innehåll som ska återges inte den första bearbetningen. Det viktigaste är i stället om URL:en tolkas till ett innehållsobjekt för vilket ett skript sedan kan användas för återgivningen. Detta ger ett utmärkt stöd för dem som skapar webbmaterial att bygga sidor som enkelt kan anpassas efter deras behov.

Fördelarna med den här flexibiliteten är uppenbara i program med många olika innehållselement eller när du behöver sidor som enkelt kan anpassas. Detta gäller särskilt när man implementerar ett webbinnehållshanteringssystem som WCM i AEM.

Se [Sling på 15 minuter](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) för de första stegen för att utveckla med Sling.

I följande diagram förklaras Sling-skriptupplösningen. Den visar hur du hämtar från HTTP-begäran till innehållsnoden, från innehållsnod till resurstyp, från resurstyp till skript och vilka skriptvariabler som är tillgängliga.

![Om Apache Sling-skriptupplösningen](assets/sling-cheatsheet-01.png)

I följande diagram förklaras alla dolda, men kraftfulla, frågeparametrar som du kan använda när du arbetar med SlingPostServlet. Den innehåller standardhanteraren för alla begäranden om POST som ger dig oändliga alternativ för att skapa, ändra, ta bort, kopiera och flytta noder i databasen.

![Använda SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling är innehållscentrerat {#sling-is-content-centric}

Sling är *innehållscentrerad*. Detta innebär att bearbetningen är inriktad på innehållet eftersom varje HTTP-begäran mappas till innehåll i form av en JCR-resurs (en databasnod):

* det första målet är den resurs (JCR-nod) som innehåller innehållet
* för det andra, representationen, eller skriptet, finns från resursegenskaperna i kombination med vissa delar av begäran (till exempel väljare och/eller tillägget)

### RESTful Sling {#restful-sling}

På grund av den innehållsorienterade filosofin implementerar Sling en REST-orienterad server och har därför ett nytt koncept i ramverk för webbapplikationer. Fördelarna är:

* RESTful, inte bara på ytan; resurser och representationer är korrekt modellerade inuti servern
* tar bort en eller flera datamodeller

   * Tidigare behövdes följande: URL-struktur, affärsobjekt, DB-schema.
   * detta reduceras nu till: URL = resource = JCR-struktur

### URL-disposition {#url-decomposition}

Vid Sling styrs bearbetningen av URL:en för användarförfrågningen. Här definieras vilket innehåll som ska visas av rätt skript. Det gör du genom att extrahera information från webbadressen.

Om du analyserar följande URL:

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

Du kan dela upp den i dess sammansatta delar:

| protocol | värd | innehållsbana | väljare | extension |  | suffix |  | parametrar |
|---|---|---|---|---|---|---|---|---|
| https:// | myhost | verktyg/spion | .printable.a4. | html | / | a/b | ? | x=12 |

**protocol** HTTP

**värd** Webbplatsens namn.

**innehållsbana** Sökväg som anger det innehåll som ska återges. Används tillsammans med tillägget. I det här exemplet översätts de till `tools/spy.html`.

**väljare** Används för alternativa metoder för återgivning av innehållet. I det här exemplet används en utskriftsvänlig version i A4-format.

**extension** Innehållsformat; anger också det skript som ska användas för återgivning.

**suffix** Kan användas för att ange ytterligare information.

**parametrar** Alla parametrar som krävs för dynamiskt innehåll.

#### Från URL till innehåll och skript {#from-url-to-content-and-scripts}

Använd dessa principer:

* mappningen använder innehållssökvägen som extraheras från begäran för att hitta resursen
* när rätt resurs finns extraheras sling-resurstypen och används för att hitta skriptet som ska användas för återgivning av innehållet

Bilden nedan visar vilken mekanism som används, vilket beskrivs mer ingående i följande avsnitt.

![chlimage_1-86](assets/chlimage_1-86a.png)

Med Sling anger du vilket skript som ska återge en viss enhet (genom att ange `sling:resourceType` i JCR-noden). Den här mekanismen ger mer frihet än en där skriptet får åtkomst till datatabellerna (som en SQL-sats i ett PHP-skript skulle göra) eftersom en resurs kan ha flera renderingar.

#### Mappa begäranden till resurser {#mapping-requests-to-resources}

Begäran är uppdelad och nödvändig information extraheras. Databasen genomsöks efter den begärda resursen (innehållsnod):

* first Sling kontrollerar om det finns en nod på den plats som anges i begäran, till exempel `../content/corporate/jobs/developer.html`
* Om ingen nod hittas tas tillägget bort och sökningen upprepas, till exempel `../content/corporate/jobs/developer`
* Om ingen nod hittas returnerar Sling http-koden 404 (Hittades inte).

Med Sling kan även andra saker än JCR-noder vara resurser, men det här är en avancerad funktion.

### Hitta skriptet {#locating-the-script}

När rätt resurs (innehållsnod) finns, **slingresurstyp** extraheras. Detta är en sökväg som letar upp skriptet som ska användas för återgivning av innehållet.

Sökvägen som anges av `sling:resourceType` kan antingen vara:

* absolut
* relativt till en konfigurationsparameter

  Relativa sökvägar rekommenderas av Adobe när de ökar portabiliteten.

Alla Sling-skript lagras i undermappar till båda `/apps` eller `/libs`, som söks igenom i den här ordningen (se [Anpassa komponenter och andra element](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

Några andra punkter att notera är:

* När metoden (GET, POST) krävs anges den i versaler enligt HTTP-specifikationen, till exempel job.POST.esp (se nedan)
* olika skriptmotorer stöds:

   * HTML (HTML Template Language - Adobe Experience Manager preferred and recommended server-side template system for HTML): `.html`
   * ECMAScript-sidor (JavaScript) (körning på serversidan): `.esp, .ecma`
   * Java™ Server Pages (körning på serversidan): `.jsp`
   * Java™ Servlet Compiler (körning på serversidan): `.java`
   * JavaScript-mallar (körning på klientsidan): `.jst`

Listan över skriptmotorer som stöds av den angivna AEM finns på Felix Management Console ( `http://<host>:<port>/system/console/slingscripting`).

Dessutom har Apache Sling stöd för integrering med andra populära skriptmotorer (till exempel Groovy, JRuby, Freemarker) och är ett sätt att integrera nya skriptmotorer.

Använda ovanstående exempel om `sling:resourceType` är `hr/jobs` sedan för:

* GET/HEAD och URL:er som slutar på .html (standardtyper, standardformat)

  Skriptet är /apps/hr/jobs/jobs.esp; det sista avsnittet i sling:resourceType är filnamnet.

* Begäranden om POST (alla begärandetyper utom GET/HEAD, metodnamnet måste vara versaler)

  POST används i skriptnamnet.

  Skriptet är `/apps/hr/jobs/jobs.POST.esp`.

* URL-adresser i andra format, slutar inte med .html

  Till exempel, `../content/corporate/jobs/developer.pdf`

  Skriptet är `/apps/hr/jobs/jobs.pdf.esp`; suffixet läggs till i skriptnamnet.

* URL:er med väljare

  Väljare kan användas för att visa samma innehåll i ett alternativt format. Till exempel en utskriftsvänlig version, ett RSS-flöde eller en sammanfattning.

  Om du tittar på en utskriftsvänlig version där väljaren kan vara *print*, som i `../content/corporate/jobs/developer.print.html`

  Skriptet är `/apps/hr/jobs/jobs.print.esp`; väljaren läggs till i skriptnamnet.

* Om ingen sling:resourceType har definierats:

   * innehållssökvägen används för att söka efter ett lämpligt skript (om den sökvägsbaserade ResourceTypeProvider är aktiv).

     Skriptet för `../content/corporate/jobs/developer.html` skulle generera en sökning i `/apps/content/corporate/jobs/`.

   * den primära nodtypen används.

* Om inget skript hittas används standardskriptet.

  Standardåtergivningen stöds som oformaterad text (.txt), HTML (.html) och JSON (.json), som alla innehåller nodens egenskaper (lämpligt formaterade). Standardåtergivningen för filnamnstillägget .res, eller begäranden utan tillägg, är att resursen (där det är möjligt) ska placeras i mellanrum.
* För http-felhantering (kod 403 eller 404) söker Sling efter ett skript på antingen:

   * platsen /apps/sling/servlet/errorhandler för [anpassade skript](/help/sites-developing/customizing-errorhandler-pages.md)
   * eller platsen för standardskripten /libs/sling/servlet/errorhandler/403.esp respektive 404.esp.

Om flera skript gäller för en viss begäran väljs det skript som matchar bäst. Ju mer specifik en matchning är, desto bättre blir den; med andra ord matchar väljaren bättre, oavsett vilket tillägg eller metodnamn som används i begäran.

Ta till exempel en begäran om åtkomst till resursen
`/content/corporate/jobs/developer.print.a4.html`
av typen
`sling:resourceType="hr/jobs"`

Anta att du har följande lista med skript på rätt plats:

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

Sedan är ordningen (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1).

Förutom resurstyperna (definieras primärt av `sling:resourceType` ) finns också resursens supertyp. Detta anges av `sling:resourceSuperType` -egenskap. De här supertyperna beaktas också när du försöker hitta ett skript. Fördelen med resurssupertyper är att de kan utgöra en hierarki av resurser där standardresurstypen är `sling/servlet/default` (används av standardservletarna) är roten.

Resursens överordnade typ kan definieras på två sätt:

* av `sling:resourceSuperType` resursens egenskap.
* av `sling:resourceSuperType` egenskapen för noden som `sling:resourceType` punkter.

Till exempel:

* /

   * a
   * b

      * sling:resourceSuperType = a

   * c

      * sling:resourceSuperType = b

   * x

      * sling:resourceType = c

   * y

      * sling:resourceType = c
      * sling:resourceSuperType = a

Typhierarkin för:

* `/x`
   * är `[ c, b, a, <default>]`
* while för `/y`
   * hierarkin är `[ c, a, <default>]`

Det beror på att `/y` har `sling:resourceSuperType` egenskap. `/x` inte och dess supertyp tas därför från sin resurstyp.

#### Sling Scripts kan inte anropas direkt {#sling-scripts-cannot-be-called-directly}

I Sling kan skript inte anropas direkt eftersom det skulle bryta det strikta begreppet med en REST-server. Du skulle blanda resurser och representationer.

Om du anropar representationen (skriptet) direkt döljer du resursen i skriptet, så att ramverket (Sling) inte längre vet om det. Därför förlorar du vissa funktioner:

* automatisk hantering av andra http-metoder än GET, inklusive:

   * POST, PUT, DELETE som hanteras med en Sing-standardimplementering
   * den `POST.jsp` skript i din sling:resourceType-plats

* kodarkitekturen är inte längre så ren eller så tydligt strukturerad som den ska vara; av största vikt för storskalig utveckling

### Sling API {#sling-api}

Detta använder Sling API-paketet org.apache.sling.&amp;ast; och taggbibliotek.

### referera till befintliga element med sling:include {#referencing-existing-elements-using-sling-include}

En sista sak är behovet av att referera till befintliga element i skripten.

Mer komplicerade skript (sammanställning av skript) måste ha åtkomst till flera resurser (navigering, sidospalt, sidfot, element i en lista, till exempel) och göra det genom att inkludera *resurs*.

Använd följande snedstreck: include(&quot;/&lt;path>/&lt;resource>&quot;). Detta inkluderar effektivt definitionen av den refererade resursen, som i följande programsats som refererar till en befintlig definition för återgivning av bilder:

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## OSGI {#osgi}

OSGi definierar en arkitektur för utveckling och driftsättning av modulära program och bibliotek (kallas även Dynamic Module System för Java™). Med OSGi-behållare kan du dela in programmet i enskilda moduler (som är jar-filer med ytterligare metainformation och kallas buntar i OSGi-terminologi) och hantera korsberoenden mellan dem med:

* tjänster som implementeras i behållaren
* ett kontrakt mellan behållaren och programmet

Dessa tjänster och kontrakt utgör en arkitektur som gör att enskilda element dynamiskt kan identifiera varandra för samarbete.

Ett OSGi-ramverk ger dig dynamisk inläsning/borttagning, konfiguration och kontroll av dessa paket - utan att du behöver starta om.

>[!NOTE]
>
>Fullständig information om OSGi-teknik finns på [OSGi-webbplats](https://www.osgi.org).
>
>På sidan Grundläggande utbildning finns en samling presentationer och självstudiekurser.

Med den här arkitekturen kan du utöka Sling med programspecifika moduler. Sling, och därmed CQ5, använder [Apache Felix](https://felix.apache.org/documentation/index.html) implementering av OSGI (Open Services Gateway-initiativ) och baseras på OSGi Service Platform version 4 version 4.2 Specifications. De är båda samlingar av OSGi-paket som körs i ett OSGi-ramverk.

Detta gör att du kan utföra följande åtgärder på något av paketen i din installation:

* installera
* start
* stop
* uppdatera
* avinstallera
* visa status
* få mer detaljerad information (t.ex. symboliskt namn, version och plats) om specifika paket

Se [webbkonsolen](/help/sites-deploying/web-console.md), [OSGI-konfiguration](/help/sites-deploying/configuring-osgi.md)och [Konfigurationsinställningar för OSGi](/help/sites-deploying/osgi-configuration-settings.md) för mer information.

## Utvecklingsobjekt i AEM {#development-objects-in-the-aem-environment}

Följande är av intresse för utvecklingen:

**Objekt** Ett objekt är antingen en nod eller en egenskap.

Mer information om hur du hanterar Item-objekt finns i [Java™ docs](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html) av Interface javax.jcr.Item

**Nod (och deras egenskaper)** Noder och deras egenskaper definieras i JCR API 2.0-specifikationen (JSR 283). De lagrar innehåll, objektdefinitioner, återgivningsskript och andra data.

Noderna definierar innehållsstrukturen och deras egenskaper lagrar det faktiska innehållet och metadata.

Innehållsnoder styr återgivningen. Sling hämtar innehållsnoden från den inkommande begäran. Egenskapen sling:resourceType för den här noden pekar på den Sling-återgivningskomponent som ska användas.

En nod, som är ett JCR-namn, kallas också en resurs i Sling-miljön.

Om du till exempel vill hämta egenskaperna för den aktuella noden kan du använda följande kod i skriptet:

`PropertyIterator properties = currentNode.getProperties();`

currentNode är det aktuella nodobjektet.

Mer information om hur du hanterar nodobjekt finns i [Java™ docs](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html).

**Widget** I AEM hanteras alla användarindata av widgetar. De används ofta för att styra redigeringen av ett visst innehåll.

Dialogrutor skapas genom att widgetar kombineras.

AEM har utvecklats med ExtJS-biblioteket med widgetar.

**Dialog** En dialogruta är en speciell typ av widget.

För att redigera innehåll använder AEM dialogrutor som definieras av programutvecklaren. Dessa kombinerar en serie widgetar för att ge användaren alla fält och åtgärder som behövs för att redigera det relaterade innehållet.

Dialogrutor används också för att redigera metadata och för olika administrationsverktyg.

**Komponent** En programvarukomponent är ett systemelement som erbjuder en fördefinierad tjänst eller händelse och kan kommunicera med andra komponenter.

I AEM används ofta en komponent för att återge innehållet i en resurs. När resursen är en sida, kallas komponentåtergivningen för en komponent på översta nivån eller en sidkomponent. En komponent behöver dock inte återge innehåll eller vara länkad till en viss resurs. En navigeringskomponent visar till exempel information om flera resurser.

Definitionen av en komponent omfattar följande:

* koden som används för att återge innehållet
* en dialogruta för användarindata och konfigurationen av det resulterande innehållet.

**Mall** En mall är basen för en viss typ av sida. När användaren skapar en sida på fliken Webbplatser måste han eller hon välja en mall. Den nya sidan skapas sedan genom att den här mallen kopieras.

En mall är en hierarki med noder som har samma struktur som den sida som ska skapas, men utan något verkligt innehåll.

Den definierar den sidkomponent som används för att återge sidan och standardinnehållet (primärt innehåll på den översta nivån). Innehållet definierar hur det återges när AEM är innehållscentrerat.

**Sidkomponent (komponent på översta nivån)** Komponenten som ska användas för att återge sidan.

**Sida** En sida är en förekomst av en mall.

En sida har en hierarkinod av typen cq:Page och en innehållsnod av typen cq:PageContent. Egenskapen sling:resourceType för innehållsnoden pekar på den sidkomponent som används för återgivning av sidan.

Om du till exempel vill hämta namnet på den aktuella sidan kan du använda följande kod i skriptet:

S`tring pageName = currentPage.getName();`

AktuellSida är det aktuella sidobjektet. Mer information om hur du hanterar sidobjekt finns i [Java™ docs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Page.html).

**Sidhanteraren** Sidhanteraren är ett gränssnitt som innehåller metoder för åtgärder på sidnivå.

Om du till exempel vill hämta innehållssidan för en resurs kan du använda följande kod i skriptet:

Sida myPage = pageManager.getContainingPage(myResource);

pageManager är sidhanterarobjektet och myResource är ett resursobjekt. Mer information om de metoder som sidhanteraren tillhandahåller finns i [Java™ docs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/PageManager.html).

## Struktur i databasen {#structure-within-the-repository}

I följande lista visas en översikt över strukturen som du ser i databasen.

>[!CAUTION]
>
>Den här strukturen, eller de filer som finns i den, bör ändras med försiktighet.
>
>Ändringar behövs när du utvecklar, men du bör vara noga med att förstå konsekvenserna av de ändringar du gör.

>[!CAUTION]
>
>Ändra ingenting i dialogrutan `/libs` bana. Kopiera objektet från för konfiguration och andra ändringar `/libs` till `/apps` och göra ändringar i `/apps`.

* `/apps`

  Programrelaterade; innehåller komponentdefinitioner som är specifika för webbplatsen. Komponenterna som du utvecklar kan baseras på de färdiga komponenterna som finns på `/libs/foundation/components`.

* `/content`

  Innehåll som skapats för din webbplats.

* `/etc`

* `/home`

  Användar- och gruppinformation.

* `/libs`

  Bibliotek och definitioner som tillhör kärnan i AEM. Undermapparna i `/libs` representerar färdiga AEM funktioner som sökning eller replikering. Innehållet i `/libs` inte ändras eftersom det påverkar hur AEM fungerar. Funktioner som är specifika för din webbplats bör utvecklas under `/apps` (se [Anpassa komponenter och andra element](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)).

* `/tmp`

  Tillfälligt arbetsområde.

* `/var`

  Filer som ändras och uppdateras av systemet, till exempel granskningsloggar, statistik, händelsehantering.

## Miljöer {#environments}

Med AEM består en produktionsmiljö ofta av två olika typer av instanser: en [Författare och en publiceringsinstans](/help/sites-deploying/deploy.md#author-and-publish-installs).

## Dispatcher {#the-dispatcher}

Dispatcher är ett Adobe-verktyg för både cachelagring och/eller belastningsutjämning. Ytterligare information finns under [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=en).

## FileVault (system för källrevision) {#filevault-source-revision-system}

FileVault förser JCR-databasen med filsystemsmappning och versionskontroll. Det kan användas för att hantera AEM utvecklingsprojekt med fullt stöd för lagring och versionshantering av projektkod, innehåll, konfigurationer och så vidare i standardversionskontrollsystem (till exempel Subversion).

Se [FileVault-verktyget](/help/sites-developing/ht-vlttool.md) detaljerad information.

## Arbetsflöden {#workflows}

Ditt innehåll omfattas ofta av organisatoriska processer, inklusive steg som godkännande och godkännande från olika deltagare. Dessa processer kan representeras som arbetsflöden, [definieras och utvecklas inom AEM](/help/sites-developing/workflows-models.md)och sedan tillämpas på [lämpliga innehållssidor](/help/sites-administering/workflows.md) eller [digitala resurser](/help/assets/assets-workflow.md) efter behov.

Arbetsflödesmotorn används för att hantera implementeringen av dina arbetsflöden och deras efterföljande program till ditt innehåll.

## Hantering av flera webbplatser {#multi-site-management}

Med Multi Site Manager (MSM) kan du enkelt hantera flera webbplatser som delar gemensamt innehåll. Med MSM kan du definiera relationer mellan platserna så att innehållsändringar på en plats automatiskt replikeras på andra platser.

Webbplatser finns till exempel ofta på flera språk för internationella målgrupper. När antalet webbplatser på samma språk är lågt (tre till fem) går det att synkronisera innehåll manuellt mellan webbplatser. Men när antalet webbplatser växer eller när flera språk används blir det effektivare att automatisera processen.

* Hantera effektivt olika språkversioner av en webbplats.
* Uppdatera en eller flera webbplatser automatiskt baserat på en källplats:

   * Använd en gemensam grundstruktur och använd gemensamt innehåll på flera webbplatser.
   * Använd tillgängliga resurser maximalt.
   * Bibehåll ett gemensamt utseende och en gemensam känsla.
   * Fokusera på hanteringen av innehåll som skiljer sig mellan webbplatserna.

Mer information finns i [Multi Site Manager](/help/sites-administering/msm.md).
