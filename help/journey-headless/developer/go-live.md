---
title: Så här Live med ditt headless-program
description: I den här delen av AEM Headless Developer Journey lär du dig hur du driftsätter en headless-applikation live.
source-git-commit: 20d46a7c37663dac36e6af9582d569a7f782eab7
workflow-type: tm+mt
source-wordcount: '1903'
ht-degree: 0%

---

# Så här Live med ditt headless-program {#go-live}

I den här delen av [AEM Headless Developer Journey](overview.md), lär dig hur du driftsätter ett headless-program live.

## Story hittills {#story-so-far}

I det föregående dokumentet om den AEM resan utan headless [Så här uppdaterar du innehåll via AEM Assets API:er](update-your-content.md) har du lärt dig hur du uppdaterar det befintliga headless-innehållet i AEM via API, och du bör nu:

* Förstå AEM Assets HTTP API.

Den här artikeln bygger på dessa grundläggande funktioner så att du förstår hur du förbereder ett eget AEM headless-projekt för publicering.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå den AEM headless-publiceringskanalen och de prestandaöverväganden du behöver känna till innan du publicerar programmet.

* Läs mer om AEM SDK och de utvecklingsverktyg som krävs
* Konfigurera en lokal utvecklingsmiljö för att simulera ditt innehåll innan du publicerar det
* Förstå AEM innehållsreplikering och cachning
* Säkra och skala programmet före start
* Övervaka prestanda och felsökning

## AEM SDK {#the-aem-sdk}

AEM SDK används för att skapa och distribuera anpassad kod. Det är det viktigaste verktyget du behöver för att utveckla och testa din headless-applikation innan du publicerar den. Den innehåller följande artefakter:

* Quickstart jar - en körbar jar-fil som kan användas för att ställa in både en författare och en publiceringsinstans
* Dispatcher-verktyg - Dispatcher-modulen och dess beroenden för Windows- och UNIX-baserade system
* Java API Jar - Java Jar/Maven Dependency som visar alla Java API:er som kan användas för att utveckla mot AEM
* Javadoc jar - javadocs for the Java API jar

## Ytterligare utvecklingsverktyg {#additional-development-tools}

Förutom AEM SDK behöver du ytterligare verktyg som gör det lättare att utveckla och testa kod och innehåll lokalt:

* Java
* Git
* Apache Maven
* Biblioteket Node.js
* Den utvecklingsmiljö du vill använda

Eftersom AEM är ett Java-program måste du installera Java och Java SDK som stöd för utveckling av AEM as a Cloud Service.

Git är det ni kommer att använda för att hantera källkontrollen samt för att checka in ändringarna i Cloud Manager och sedan distribuera dem till en produktionsinstans.

AEM använder Apache Maven för att bygga projekt som skapats från AEM Maven Project-arkitypen. Alla större utvecklingsmiljöer har stöd för integrering av Maven.

Node.js är en JavaScript-körningsmiljö som används för att arbeta med de viktigaste resurserna i ett AEM projekt `ui.frontend` delprojekt. Node.js distribueras med npm, som är de facto-pakethanteraren Node.js, som används för att hantera JavaScript-beroenden.

## Lathund för komponenterna i ett AEM system {#components-of-an-aem-system-at-a-glance}

Nu ska vi titta på de olika delarna i en AEM.

En komplett AEM består av en författare, en publiceringsversion och en utskicksare. Samma komponenter kommer att göras tillgängliga i den lokala utvecklingsmiljön för att göra det enklare för dig att förhandsgranska koden och innehållet innan du publicerar.

* **Författartjänsten** är den plats där interna användare skapar, hanterar och förhandsgranskar innehåll.

* **Publiceringstjänsten** är&quot;Live&quot;-miljön och det är vanligtvis den slutanvändaren interagerar med. När innehållet har redigerats och godkänts av författartjänsten distribueras det (replikeras) till publiceringstjänsten. Det vanligaste distributionsmönstret med AEM headless-program är att ha produktionsversionen av programmet ansluten till en AEM Publish-tjänst.

* **Dispatcher** är en statisk webbserver som utökas med AEM. Den cachelagrar webbsidor som skapats av publiceringsinstansen för att förbättra prestandan.

## Arbetsflödet för lokal utveckling {#the-local-development-workflow}

Det lokala utvecklingsprojektet bygger på Apache Maven och använder Git för källkontroll. För att kunna uppdatera projektet kan utvecklarna använda den integrerade utvecklingsmiljö de föredrar, till exempel Eclipse, Visual Studio Code eller IntelliJ.

Om du vill testa kod- eller innehållsuppdateringar som ska importeras av ditt headless-program måste du distribuera uppdateringarna till den lokala AEM, som innehåller lokala instanser av AEM författare och publiceringstjänster.

Observera skillnaden mellan de olika komponenterna i den lokala AEM, eftersom det är viktigt att testa uppdateringarna där de är som viktigast. Testa till exempel innehållsuppdateringar på författaren eller testa ny kod på publiceringsinstansen.

I ett produktionssystem placeras en dispatcher och en http Apache-server alltid framför en AEM publiceringsinstans. De tillhandahåller cachelagring och säkerhetstjänster för AEM system, så det är viktigt att testa kod- och innehållsuppdateringar mot dispatchern också.

## Förhandsgranska kod och innehåll lokalt med den lokala utvecklingsmiljön {#previewing-your-code-and-content-locally-with-the-local-development-environment}

För att kunna förbereda AEM headless-projekt för lansering måste du se till att alla delar av projektet fungerar bra.

För att göra det måste ni sätta ihop allt: kod, innehåll och konfiguration och testa det i en lokal utvecklingsmiljö för live-beredskap.

Den lokala utvecklingsmiljön består av tre huvudområden:

1. Det AEM projektet - det innehåller all kod, konfiguration och innehåll som AEM utvecklare kommer att arbeta med
1. Local AEM Runtime - lokala versioner av AEM författare och publiceringstjänster som ska användas för att distribuera kod från det AEM projektet
1. Local Dispatcher Runtime - en lokal version av Apache htttpd-webbservern som innehåller Dispatcher-modulen

När den lokala utvecklingsmiljön har konfigurerats kan du simulera innehåll som skickas till React-appen genom att distribuera en statisk nodserver lokalt.

Om du vill få en mer detaljerad genomgång av hur du konfigurerar en lokal utvecklingsmiljö och alla beroenden som behövs för förhandsgranskning av innehåll kan du läsa [Produktionsdistributionsdokumentation](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=en#prerequisites).

## Förbered ditt AEM Headless-program för GoLive {#prepare-your-aem-headless-application-for-golive}

<!-- Start of CDN Review -->

Nu är det dags att göra ditt AEM headless-program redo för lansering enligt de rutiner som beskrivs nedan.

### Skydda ditt Headless-program innan du startar {#secure-and-scale-before-launch}

1. Förbered [Autentisering](/help/assets/content-fragments/graphql-authentication-content-fragments.md) för GraphQL-begäranden

### Modellstruktur jämfört med GraphQL-utdata {#structure-vs-output}

* Undvik att skapa frågor som genererar mer än 15 kB JSON (gzip-komprimerad). Långa JSON-filer är resurskrävande för att klientprogrammet ska kunna analysera.
* Undvik fler än fem kapslade nivåer av fragmenthierarkier. Ytterligare nivåer gör det svårt för innehållsförfattare att ta hänsyn till effekten av deras ändringar.
* Använd frågor med flera objekt i stället för att modellera frågor med beroendehierarkier i modellerna. På så sätt blir det flexiblare på lång sikt att omstrukturera JSON-utdata utan att man behöver göra en massa innehållsändringar.

### Maximera CDN-cacheträffrekvens {#maximize-cdn}

* Använd inte direkta GraphQL-frågor, såvida du inte begär direktinnehåll från ytan.
   * Använd beständiga frågor när det är möjligt.
   * Tillhandahåll CDN TTL över 600 sekunder för att CDN ska cachelagra dem.
   * AEM kan beräkna effekten av en modelländring av befintliga frågor.
* Dela JSON-filer/GraphQL-frågor mellan låg och hög förändringsfrekvens för innehåll för att minska klienttrafiken till CDN och tilldela högre TTL. Detta minimerar antalet CDN som validerar JSON med den ursprungliga servern.
* Om du vill göra innehåll från CDN ogiltigt använder du Mjuk tömning. På så sätt kan CDN ladda ned innehållet på nytt utan att orsaka ett cacheminne.

>[!NOTE]
>
>Se [Ytterligare resurser](#additional-resources) för mer information om CDN och cachning.

### Förkorta nedladdningstiden för headless Content {#improve-download-time}

* Kontrollera att HTTP-klienter använder HTTP/2.
* Kontrollera att HTTP-klienter accepterar rubrikbegäran för gzip.
* Minimera antalet domäner som används som värd för JSON och refererade artefakter.
* Utnyttja `Last-modified-since` för att uppdatera resurser.
* Använd `_reference` i JSON-fil för att börja ladda ned resurser utan att behöva tolka fullständiga JSON-filer.

<!-- End of CDN Review -->

## Distribuera till produktion {#deploy-to-production}

Distribuering till produktion kan vara beroende av om du har en *traditionell* AEM som distribuerar med hjälp av Maven, eller använder Adobe Managed Services (AMS) och därför använder Cloud Manager.

## Distribuera till produktion med Maven {#deploy-to-production-maven}

För *traditionell* distribution (ej AMS) med Maven ser du [WKND - självstudiekurs](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html?lang=en#build) för en översikt.

## Distribuera till produktion med Cloud Manager {#deploy-to-production-cloud-manager}

Om du är AMS-kund och använder Cloud Manager är du redo att skicka koduppdateringarna till en [centraliserad Git-databas i Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html).

När uppdateringarna har överförts till Cloud Manager kan de distribueras till AEM med [Cloud Managers pipeline för CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html).

<!-- Can't find a parallel link -->
<!--
You can start deploying your code by leveraging the Cloud Manager CI/CD pipeline, which is covered extensively [here](/help/implementing/deploying/overview.md).
-->

## Prestandaövervakning {#performance-monitoring}

För att användarna ska få bästa möjliga upplevelse när de använder det AEM headless-programmet är det viktigt att du övervakar nyckeltal enligt beskrivningen nedan:

* Validera förhandsgransknings- och produktionsversioner av appen
* Verifiera AEM statussidor för den aktuella tjänsttillgänglighetsstatusen
* Få resultatrapporter
   * Leveransprestanda
      * Ursprungsservrar - antal anrop, felfrekvens, CPU-belastning, nyttolaststrafik
   * Författarprestanda
      * Kontrollera antal användare, förfrågningar och inläsning
* Åtkomst till program- och utrymmesspecifika prestandarapporter
   * Kontrollera om de allmänna måtten är gröna/orange/röda när servern är på plats och identifiera sedan specifika appproblem
   * Öppna samma rapporter ovan filtrerade till program eller utrymme (t.ex. Photoshop desktop, paywall)
   * Använd API:er för Splunk-logg för att få åtkomst till service- och programprestanda
   * Kontakta kundsupport om det finns andra problem.

## Felsökning {#troubleshooting}

### Felsökning {#debugging}

Följ dessa metodtips som ett allmänt tillvägagångssätt vid felsökning:

* Validera funktionalitet och prestanda med förhandsgranskningsversionen av programmet
* Validera funktionalitet och prestanda med programmets produktionsversion
* Validera med JSON-förhandsvisningen i Content Fragment Editor
* Inspect JSON i klientprogrammet för att kontrollera om det finns problem med klientprogram eller leverans
* Inspect JSON använder GraphQL för att kontrollera om det finns problem med cachelagrat innehåll eller AEM

### Logga ett fel med support {#logging-a-bug-with-support}

Följ stegen nedan för att effektivt logga ett fel med support om du behöver mer hjälp:

* Ta skärmbilder av problemet, om det behövs
* Dokumentera ett sätt att återskapa problemet
* Dokumentera innehållet som problemet återger med
* Logga ett problem via AEM supportportal med rätt prioritet

## Resan slutar - eller gör det? {#journey-ends}

Grattis! Du har slutfört AEM Headless Developer Journey! Nu bör du förstå:

* Skillnaden mellan headless och headful content delivery.
* AEM headless-funktioner.
* Organisera och AEM Headless-projekt.
* Skapa innehåll utan rubriker i AEM.
* Så här hämtar och uppdaterar du headless-innehåll i AEM.
* Så här lever du med ett AEM Headless-projekt.
* Vad gör man efter det att de publicerats?

Antingen har du redan startat ditt första AEM Headless-projekt eller så har du nu all den kunskap du behöver för att göra det. Bra jobbat!

### Utforska Single Page-program {#explore-spa}

De headless butikerna i AEM behöver inte stanna här. Du kanske kommer ihåg i [Komma igång med en del av resan](getting-started.md#integration-levels) Vi diskuterade kortfattat hur AEM inte bara stöder headless-leverans och traditionella fullstacksmodeller, utan också kan stödja hybridmodeller som kombinerar fördelarna med båda.

Om den här typen av flexibilitet är något du behöver för ditt projekt kan du fortsätta med den valfria, extra delen av resan, [Skapa enkelsidiga program (SPA) med AEM.](create-spa.md)

## Ytterligare resurser {#additional-resources}

* [Utvecklingshandbok för AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/the-basics.html?lang=en)

* [WKND - självstudiekurs](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en)

* [Cloud Manager för AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=en)

* CDN-cache

   * [Kontrollera en CDN-cache](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#controlling-a-cdn-cache)

   * Konfigurera [CDN Rewriter](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html) (*sök efter CDN Rewriter*)
