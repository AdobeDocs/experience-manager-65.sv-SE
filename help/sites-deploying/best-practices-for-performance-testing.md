---
title: Bästa metoder för prestandatestning
seo-title: Best Practices for Performance Testing
description: I den här artikeln beskrivs de övergripande strategier och metoder som används för prestandatestning samt några av de verktyg som är tillgängliga som hjälp i processen.
seo-description: This article outlines the overall strategies and methodologies used for performance testing as well as some of the tools that are available to assist in the process.
uuid: ab8720d6-b864-4d00-9e07-2e1699cfe7db
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 669018a0-f6ef-42b2-9c6f-83d7dd5a7095
exl-id: fcac75e1-15c1-4a37-8d43-93c95267b903
source-git-commit: e8320b1dac681fd2c9e749344e8c126487d840ba
workflow-type: tm+mt
source-wordcount: '1897'
ht-degree: 0%

---

# Bästa metoder för prestandatestning{#best-practices-for-performance-testing}

## Introduktion {#introduction}

Prestandatestning är en viktig del i all AEM. Beroende på kundens krav kan prestandatestning utföras på publiceringsinstanser, författarinstanser eller både och.

Denna dokumentation kommer att innehålla en beskrivning av övergripande strategier och metoder för att utföra prestandatester samt några av de verktyg som Adobe tillhandahåller för att hjälpa till i processen. Slutligen kommer vi att analysera några av de verktyg som finns i AEM 6 som hjälp vid prestandajustering, både från kodanalys och systemkonfigurationsperspektiv.

### Simulera verklighet {#simulating-reality}

Det som är viktigast när du utför prestandatester är att se till att du härmar en produktionsmiljö så nära som möjligt. Detta kan ofta vara svårt, men det är av största vikt att säkerställa att dessa tester är korrekta. När du arbetar med att utforma prestandatester är det viktigt att tänka på följande:

* Produktionsliknande material

Många prestandamått i AEM, t.ex. svarstid för frågor, kan påverkas av storleken på innehållet i systemet. Det är viktigt att se till att testmiljön har så nära en kopia som möjligt av produktionsdata.

* Produktionskod

De AEM versionerna och snabbkorrigeringarna som används i produktionen bör vara desamma i testmiljön. Det är också viktigt att testa vilken version av koden som distribueras till produktionen.

* Produktionsliknande maskinvara och nätverkskonfiguration

Testerna är meningslösa utan en miljö som liknar produktionen så nära som möjligt. I idealfallet bör maskinvaruspecifikationerna, nätverksgränssnitten, belastningsutjämnarna och CDN vara identiska med produktionen i testmiljön.

* Produktionsbelastning

Många prestandaproblem uppstår inte förrän systemet är hårt belastat. Goda prestandatester bör simulera den belastning som produktionssystemen kommer att vara under vid sin topp.

### Ange mål {#setting-goals}

Innan prestandatestning börjar måste icke-funktionella krav ställas för att specificera belastnings- och svarstider. Om du migrerar från ett befintligt system bör du se till att svarstiden liknar dina aktuella produktionsvärden. För belastning är det bäst att ta den aktuella toppbelastningen och dubbla den. Detta säkerställer att webbplatsen kan fortsätta fungera som den ska.

### Verktyg {#tools}

Det finns många kommersiellt tillgängliga verktyg för prestandatestning på marknaden. När du kör ett lastgenereringsverktyg är det viktigt att se till att de datorer som utför testerna har tillräcklig nätverksbandbredd. I annat fall genereras ingen ytterligare belastning i den miljö som testas när provningsmaskinen når anslutningens gränser.

#### Testverktyg {#testing-tools}

* Adobe **Tålig dag** kan användas för att generera inläsning AEM instanser och samla in prestandadata. Adobe AEM tekniker använder faktiskt verktyget för att själv testa AEM. Skript som körs under Tough Day konfigureras via egenskapsfiler och JMX XML-filer. Mer information finns i [Dokumentation om tuffa dagar](/help/sites-developing/tough-day.md).

* AEM innehåller färdiga verktyg för att snabbt se problematiska frågor, förfrågningar och felmeddelanden. Mer information finns i [Diagnosverktyg](/help/sites-administering/operations-dashboard.md#diagnosis-tools) i dokumentationen för kontrollpanelen för åtgärder.
* Apache tillhandahåller en produkt som kallas **JMeter** som kan användas för prestanda- och belastningstestning samt funktionellt beteende. Det är programvara med öppen källkod och kan användas, men har en mindre funktionsuppsättning än företagsprodukter och en brantare inlärningskurva. JMeter finns på Apache webbplats på [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **Load Runner** är en lasttestningsprodukt i enterpriseklass. Det finns en kostnadsfri utvärderingsversion. Mer information finns på [https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)

* Molnbaserade lasttestningsverktyg som [Neustar](https://www.neustar.biz/services/web-performance/load-testing) kan också användas.
* När det gäller att testa mobila eller responsiva webbplatser måste en separat uppsättning verktyg användas. De fungerar genom att begränsa nätverksbandbredden och simulera långsammare mobilanslutningar som 3G eller EDGE. Bland de verktyg som används mest finns följande:

   * **[Nätverkslänkvillkor](https://nshipster.com/network-link-conditioner/)** - det ger ett användarvänligt gränssnitt och fungerar på en ganska låg nivå i nätverksstacken. Den innehåller versioner för OS X och iOS.
   * [**Charles**](https://www.charlesproxy.com/) - en proxyapplikation för webbfelsökning som förutom flera andra användningsområden ger nätverksbegränsning. Versioner finns för Windows, OS X och Linux.

#### Optimeringsverktyg {#optimization-tools}

**Övervakning**

The [Övervakningsprestanda](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance) dokumentation är en bra resurs för verktyg och metoder som kan användas för att diagnostisera problem och identifiera områden för justering.

**Utvecklarläge i Touch UI**

En av de nya funktionerna i pekgränssnittet AEM 6 är utvecklarläget. Precis som författare kan växla mellan redigerings- och förhandsgranskningslägena kan utvecklare växla till utvecklarläget i redigeringsgränssnittet för att se renderingstiden för varje komponent på sidan och för att se stackspårningar av eventuella fel. Mer information om utvecklarläget finns i [CQ Gems-presentation](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html).

**Läs begärandeloggarna med rlog.jar**

För en mer omfattande analys av begärandeloggarna i ett AEM. `rlog.jar` kan användas för att söka igenom och sortera `request.log` filer som AEM genererar. Denna jar-fil ingår i en AEM installation i `/crx-quickstart/opt/helpers` mapp. Mer information om loggverktyget och förfrågningsloggen i allmänhet finns i [Övervakning och underhåll](/help/sites-deploying/monitoring-and-maintaining.md) dokumentation.

**Verktyget Förklara fråga**

The [Förklara fråga](/help/sites-administering/operations-dashboard.md#explain-query) i ACS AEM Verktyg kan användas för att visa index som används när en fråga körs. Det här kan vara mycket användbart när du optimerar långsamma frågor.

**PageSpeed-verktyg**

Google PageSpeed-verktyg erbjuder webbplatsanalys för att följa vedertagna standarder för sidprestanda och en plugin som kan installeras tillsammans med dispatchern på en Apache-instans för ytterligare optimeringar. Mer information finns i [PageSpeed Tools Website](https://developers.google.com/speed/pagespeed/).

## Författarmiljö {#author-environment}

### Utföra tester {#performing-tests}

För att kunna utföra prestandatestning i författarmiljön måste du simulera upplevelsen hos författare. Detta innebär att författarinstallationerna måste innehålla alla komponenter, OSGi-paket, gränssnittsanpassning, anpassade index och andra tillägg som du har gjort för produktionsförfattarinstanserna.

Det finns många automatiseringsramverk som är utformade för prestanda- och belastningstestning. Anpassade skript kan spelas in i dessa verktyg och sedan spelas upp för att simulera ett oändligt antal skribenter som samtidigt utför liknande åtgärder för att skapa och aktivera innehåll. Vi rekommenderar att du använder verktyget Tough Day för att simulera aktiviteter som att överföra tusentals resurser eller aktivera ett stort antal sidor.

För de typer av miljöer som kräver mycket resurser eller sidredigering är det av största vikt att använda verktyg som t.ex. Tough Day för att säkerställa att miljön fungerar effektivt under toppbelastning. [WebDAV](/help/sites-administering/webdav-access.md) är ett verktyg som inte kräver skript och som också kan användas för att läsa in stora mängder resurser.

#### MongoDB-specifika steg {#mongodb-specific-steps}

På system med MongoDB-backendar har AEM flera [JMX](/help/sites-administering/jmx-console.md) MBeans som behöver övervakas vid belastnings- eller prestandatester:

* The **Statistik för konsoliderad cache** MBean. Du kommer åt den direkt genom att gå till:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

För namngiven cache **Document-Diff** bör träfffrekvensen vara över `.90`. Om träfffrekvensen är under 90 % är det troligt att du måste ändra din `DocumentNodeStoreService` konfiguration. Adobe produktsupport kan rekommendera optimala inställningar för din miljö.

* The **Oak-databasstatistik** Mbean. Du kommer åt den direkt genom att gå till:

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

The **ObservationQueueMaxLength** -avsnittet visar antalet händelser i Oaks observationskö under de senaste timmarna, minuterna, sekunderna och veckorna. Hitta det största antalet händelser i avsnittet&quot;per timme&quot;. Det här numret måste jämföras med `oak.observation.queue-length` inställning. Om det högsta antalet som visas för observationskön överstiger `queue-length` inställning:

1. Skapa en fil med namnet: `com.adobe.granite.repository.impl.SlingRepositoryManager.cfg` innehåller parametern `oak.observation.queue‐length=50000`
1. Placera den under mappen /crx-quickstart/install.

>[!NOTE]
>Se även KB-artikeln om [AEM 6.x | Prestandajusteringstips](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)

Standardinställningen är 10 000, men för de flesta distributioner måste den oftast höjas till 20 000 eller 50 000.

## Publiceringsmiljö {#publish-environment}

### Utföra tester {#performing-tests-1}

Den viktigaste delen av en distribution som behöver genomgå inläsningstester är den publicerings- eller utskicksmiljö som slutanvändaren är intresserad av.

Automatiska testverktyg från tredje part kan användas för att testa webbplatsens prestanda. Med de här verktygen kan du spela in steg som användare ska gå igenom på webbplatsen och köra många av dessa sessioner samtidigt för att simulera den belastning som är typisk för en produktionswebbplats.

De flesta webbplatser för produktion har optimeringar på plats, som dispatcher caching och ett leveransnätverk. När du testar måste du se till att även dessa optimeringar är tillgängliga för testmiljön. Förutom att övervaka svarstiderna för slutanvändarna måste du också övervaka systemstatistik på publiceringsservrarna och utskickarna för att säkerställa att systemet inte begränsas av maskinvaruresurser.

På ett system som inte kräver en hög nivå av personalisering bör avsändaren cachelagra de flesta förfrågningar. Därför bör inläsningen av publiceringsinstansen förbli relativt platt. Om det krävs en hög nivå av personalisering rekommenderar vi att du använder tekniker som iFrames eller AJAX förfrågningar för det personaliserade innehållet för att tillåta så mycket dispatcher-cachning som möjligt.

För grundläggande tester kan Apache Bench användas för att mäta svarstider på webbservern och för att skapa belastning för att mäta minnesläckage. Mer information finns i exemplet i [Övervakningsdokumentation](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench).

## Felsökning av prestandaproblem {#troubleshooting-performance-issues}

När du har kört prestandatester på författarinstansen måste eventuella problem undersökas, diagnostiseras och åtgärdas. Du kan använda flera verktyg och tekniker när du utför analyser och åtgärdar problem:

* Du kan granska [Prestandalogg för begäran](/help/sites-administering/operations-dashboard.md#request-performance) i kontrollpanelen för åtgärder. Det här verktyget kan användas för att identifiera långsamma sidförfrågningar
* Analysera långsamma frågor med [Verktyget Frågeprestanda](/help/sites-administering/operations-dashboard.md#query-performance)

* Se fellistan för fel eller varningar. Mer information finns i [Loggning](/help/sites-deploying/configure-logging.md)
* Övervaka systemmaskinvaruresurser som minne och processoranvändning, disk-I/O eller nätverks-I/O. Dessa resurser är ofta orsaken till flaskhalsar i prestandan
* Optimera sidornas arkitektur och adressering för att minimera användningen av URL-parametrar för att tillåta så mycket cachelagring som möjligt
* Följ [Prestandaoptimering](/help/sites-deploying/configuring-performance.md) och [Tips för prestandajustering](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) dokumentation

* Om det är problem med att redigera vissa sidor eller komponenter på författarinstanser använder du TouchUI Developer Mode för att granska sidan i fråga. Detta ger en beskrivning av varje innehållsområde på sidan samt dess inläsningstid
* Minimera alla JS och CSS på webbplatsen. Mer information om hur du gör detta finns i [blogginlägg](https://blogs.adobe.com/foxes/enable-js-and-css-minification/).
* Eliminera inbäddad CSS och JS från komponenterna. De bör inkluderas och minimeras med klientbiblioteken för att minimera antalet begäranden som krävs för att återge sidan
* Använd webbläsarverktyg som Chrome&#39;s Network tab för att inspektera serverförfrågningarna och se vilka som tar längst tid.

När problemområden har identifierats kan programkoden genomsökas efter prestandaoptimeringar. Alla AEM som inte fungerar som de ska kan hanteras med Adobe Support.
