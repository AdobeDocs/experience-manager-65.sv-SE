---
title: Konfigurationsinställningar för OSGi
seo-title: Konfigurationsinställningar för OSGi
description: Den här artikeln innehåller information om de OSGi-konfigurationsinställningar (listade enligt paket) som är relevanta för projektimplementeringen. Förteckningen fungerar som riktlinjer och är inte uttömmande.
seo-description: Den här artikeln innehåller information om de OSGi-konfigurationsinställningar (listade enligt paket) som är relevanta för projektimplementeringen. Förteckningen fungerar som riktlinjer och är inte uttömmande.
uuid: 192d3287-ec99-403b-bab0-45721e4e3abd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: ed3a858c-7a43-4515-a2ff-43ca465c7d7d
docset: aem65
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3806'
ht-degree: 0%

---


# Konfigurationsinställningar för OSGi{#osgi-configuration-settings}

[OSG ](https://www.osgi.org/) är en viktig del i AEM. Det används för att styra de sammansatta AEM och deras konfiguration.

OSGi &quot;*innehåller standardiserade primitiver som gör det möjligt att konstruera program från små, återanvändbara och samarbetskomponenter. Dessa komponenter kan sättas samman till ett program och distribueras*.

Detta gör det enkelt att hantera paket när de kan stoppas, installeras och startas individuellt. De inbördes beroendena hanteras automatiskt. Varje OSGi-komponent (se [OSGi-specifikationen](https://www.osgi.org/Specifications/HomePage)) finns i ett av de olika paketen. När du arbetar med AEM finns det flera metoder för att hantera konfigurationsinställningarna för sådana paket. Mer information och rekommenderade metoder finns i [Konfigurera OSGi](/help/sites-deploying/configuring-osgi.md).

Följande OSGi-konfigurationsinställningar (listade efter paket) är relevanta för projektimplementeringen. Alla inställningar som visas behöver inte justeras, vissa anges för att du ska förstå hur AEM fungerar.

>[!CAUTION]
>
>Förteckningen är avsedd att fungera som riktlinjer och är inte uttömmande. Alla paket visas inte och inte heller alla parametrar för vissa av de paket som ingår.
>
>Den konfiguration som krävs varierar från projekt till projekt.
>
>Se webbkonsolen för värden och detaljerad information om parametrar.

>[!NOTE]
>
>OSGi Configuration Diff-verktyget, som ingår i [AEM Tools](https://helpx.adobe.com/experience-manager/kb/tools/aem-tools.html), kan användas för att lista OSGi-standardkonfigurationer.

>[!NOTE]
>
>Ytterligare programpaket kan behövas för specifika funktionsområden inom AEM. I dessa fall finns konfigurationsinformation på sidan som rör lämplig funktion.

**AEM Replication Event** ListenerConfigure:

* **Körningslägena** där replikeringshändelser distribueras till avlyssnare. Om det till exempel definieras som författare är detta det system som kommer att&quot;initiera&quot; replikeringen.

* Körningsläget **publish** måste läggas till om projektkoden bearbetar replikeringshändelser (omvänd replikering) i en publiceringsmiljö. Om dispatchern till exempel används för att tömma från publiceringsmiljön eller när standardreplikering till andra publiceringsinstanser sker.

**AEM Repository change** listenerConfigure:

* **Sökvägar**, platser att avlyssna databashändelser som är klara för distribution.

**CRX Sling Client** RepositoryKonfigurera åtkomst till den underliggande innehållsdatabasen.

* **Administratörslösenordet** bör ändras efter installationen för att säkerställa [säkerheten](/help/sites-administering/security-checklist.md) för din instans.
* Andra ändringar bör inte vara nödvändiga och försiktighet måste vidtas eftersom de kan påverka åtkomsten till databasen.

**Wiki Mail-** tjänstKonfigurera e-postinställningarna för e-post som skickas av en wiki.

**Apache Felix OSGi Management** ConsoleKonfigurera:

* **Plugins**, de viktigaste navigeringsobjekten (konsolplugin) som finns i  **Apache Felix Web Management** Console som menyalternativ på den översta nivån. Inaktivera allt du inte behöver eftersom utrymme och resurser krävs för varje åtgärd.

>[!CAUTION]
>
>Var noga med att konfigurera följande:
>
>**Användarnamn** och  **lösenord**, autentiseringsuppgifter för åtkomst till själva Apache Felix Web Management Console.
>Lösenordet måste ändras efter den första installationen för att säkerställa att [security](/help/sites-administering/security-checklist.md) för din instans.

>[!NOTE]
>
>Den här konfigurationen bör göras med Felix Console så som den behövs vid start - innan databasen är tillgänglig.

**Apache Sling Customizable Request Data** LoggerKonfigurera:

* **Loggningsnamn** och  **loggformat** för att konfigurera plats och format för begäran och åtkomstloggning (standard:  `request.log`). Den här loggfilen är viktig när du analyserar prestanda eller felsökningsfunktioner som är relaterade till webbkedjan.
Detta är tillsammans med [Loggaren för Apache Sling-begäran](#apacheslingrequestlogger).

Mer information finns i [AEM Logging](/help/sites-deploying/configure-logging.md) och [Sling Logging](https://sling.apache.org/site/logging.html).

**Konfiguration av** händelseavlyssningstrådar för ApacheSling:

* **Minsta poolstorlek** och  **maximal poolstorlek**, storleken på poolen som används för att lagra händelsetrådar.

* **Köstorlek** är den maximala storleken på trådkön om poolen är slut.
Det rekommenderade värdet är `-1` eftersom kön då anges till obegränsad. om en gräns anges kan förluster uppstå när den överskrids.

* Om du ändrar de här inställningarna kan du förbättra prestandan i scenarier med ett stort antal händelser. till exempel AEM DAM eller arbetsflöde.
* Värden som är specifika för ditt scenario bör fastställas med hjälp av tester.
* De här inställningarna kan påverka instansens prestanda, så ändra dem inte utan orsak och vederbörlig hänsyn.

**Apache Sling GET** ServletKonfigurera vissa återgivningsaspekter:

* **Auto** Indexför att aktivera/inaktivera katalogåtergivning för bläddring.
* **Aktivera**  (eller inaktivera) standardåtergivningar, till exempel  **HTML**,  **oformaterad text**,  **** JSONeller  **XML**.
Du bör inte inaktivera JSON.

>[!NOTE]
>
>Den här inställningen konfigureras automatiskt för produktionsinstanser om du kör AEM i [produktionsklart läge](/help/sites-administering/production-ready.md).

**Apache Sling Java Script** HandlerKonfigurera inställningar för kompilering av Java-filer som skript (servlets).

Vissa inställningar kan påverka prestandan. De bör inaktiveras där det är möjligt, särskilt för en produktionsinstans.

* S **VM** och **Mål-VM**, definierar JDK-versionen som den som används som JVM för körning

* för produktionsinstanser:

   * inaktivera **Generera felsökningsinformation**

**Apache Sling JCR** InstallerDe här parametrarna behöver förmodligen inte konfigureras, men kan vara användbara att känna till när du utvecklar eller felsöker. Installationsmappen kan till exempel vara användbar för att checka in/ut eller skapa ett paket.

* **Installationsmapparnas namn** återutökar  **maximalt hierarkidjup för installationsmappar**  - ange var och till vilket djup databasmappar ska sökas efter resurser som ska installeras. När ett jokertecken används (som i .*/install) söks igenom alla matchningar, till exempel `/libs/sling/install` och `/libs/cq/core/install`.

* **Sökväg**, lista med sökvägar som installeras söker efter resurser som ska installeras, tillsammans med en siffra som anger viktningsfaktorn för sökvägen.

**Apache Sling Job Event** HandlerKonfigurera parametrar som hanterar jobbplanering:

* **Återförsöksintervall**,  **maximalt antal återförsök**,  **maximalt antal parallella jobb**,  **bekräfta väntetid**, bland annat.

* Om du ändrar dessa inställningar kan prestandan förbättras i scenarier med ett stort antal jobb. till exempel stor användning av AEM DAM och arbetsflöden.
* Värden som är specifika för ditt scenario bör fastställas med hjälp av tester.
* Ändra inte de här inställningarna utan orsak. Ändra bara efter vederbörlig hänsyn.

**Apache Sling JSP Script** HandlerKonfigurera prestandarelevanta inställningar för JSP-skripthanteraren. För att förbättra prestanda bör du inaktivera så mycket som möjligt.

Särskilt för produktionsinstanser:

* inaktivera **Generera felsökningsinformation**
* inaktivera **Behåll genererad Java**
* inaktivera **Mappat innehåll**
* inaktivera **Visa källfragment**

>[!NOTE]
>
>Den här inställningen konfigureras automatiskt för produktionsinstanser om du kör AEM i [produktionsklart läge](/help/sites-administering/production-ready.md).

**Loggningskonfiguration** för Apache SlingKonfigurera:

* **Loggnivå** och  **loggfil** för att definiera platsen och loggnivån för konfigurationen för central loggning (error.log). Nivån kan anges till en av `DEBUG`, `INFO`, `WARN`, `ERROR` och `FATAL`.

* **Antal loggfiler** och  **loggfilströskelvärden** som definierar loggfilens storlek och versionsrotation.

* **Meddelandemönster** definierar loggmeddelandenas format.

Mer information finns i [AEM Logging](/help/sites-deploying/configure-logging.md#global-logging) och [Sling Logging](https://sling.apache.org/site/logging.html).

**Konfiguration av loggningslogg för Apache Sling (Factory Configuration)** Konfigurera:

* **Loggnivå**,  **Loggfil** och  **meddelandeformat** för att definiera information om loggfilen och meddelanden.

* **** Loggboken för att definiera kategorin. till exempel bara log för com.day.cq.

* Genom att använda **Fabrikskonfigurationer** kan valfritt antal ytterligare konfigurationer läggas till för att passa de olika loggnivåer och kategorier som behövs.
* Sådana konfigurationer är till hjälp vid utvecklingen. om du till exempel vill logga TRACE-meddelanden för en viss tjänst i en viss loggfil.
* Sådana konfigurationer är användbara i en produktionsmiljö. om du till exempel vill att meddelanden om en viss tjänst ska loggas i en enskild loggfil för enklare övervakning.

Mer information finns i [AEM Logging](/help/sites-deploying/configure-logging.md) och [Sling Logging](https://sling.apache.org/site/logging.html).

**Konfiguration av skrivprogram för Apache Sling Logging (fabrikskonfiguration)** Konfigurera:

* **Logga** fil för att definiera om det finns en loggfil.
* **Antal loggfiler** som definierar versionsrotationen.

* Skrivaren kan användas av en **konfiguration för loggningsloggning för Apache Sling**.

* Sådana konfigurationer är till hjälp vid utvecklingen. om du till exempel vill logga TRACE-meddelanden för en viss tjänst i en viss loggfil.
* Sådana konfigurationer är användbara i en produktionsmiljö. om du till exempel vill att meddelanden om en viss tjänst ska loggas i en enskild loggfil för enklare övervakning.

Mer information finns i [AEM Logging](/help/sites-deploying/configure-logging.md) och [Sling Logging](https://sling.apache.org/site/logging.html).

**Apache Sling Main** ServerConfigure:

* **Antal anrop per** begärande och  **rekursionsdjup** för att skydda datorn mot oändlig rekursion och för många skriptanrop.

**Apache Sling MIME Type** ServiceConfigure:

* **MIME-** typsnitt för att lägga till de som krävs för projektet i systemet. Detta gör att en `GET`-begäran för en fil kan ställa in rätt innehållstypsrubrik för länkning av filtypen och programmet.

**Apache Sling Referrer** FilterFör att åtgärda kända säkerhetsproblem med CSRF (Cross-Site Request Forgery) i CRX WebDAV och Apache Sling måste du konfigurera referensfiltret.

Refererarfiltertjänsten är en OSGi-tjänst som gör att du kan konfigurera:

* vilka http-metoder som ska filtreras
* om en tom referensrubrik tillåts
* och en lista över servrar som ska tillåtas utöver servervärden.

Mer information finns i [Säkerhetschecklistan - Problem med Förfalskning av begäran mellan webbplatser](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery).

>[!NOTE]
>
>Refererarfiltret för Apache Sling är beroende av att ett snabbkorrigeringspaket har installerats.

**Logger för Apache Sling-begäran** Konfigurera:

* olika parametrar för att definiera hur begäranden loggas.
* **Aktivera begärandelogg** för att aktivera eller inaktivera.

* **Aktivera åtkomstlogg** för att aktivera eller inaktivera.

Detta är tillsammans med [Apache Sling Customizable Request Data Logger](#apacheslingcustomizablerequestdatalogger).

Mer information finns i [AEM Logging](/help/sites-deploying/configure-logging.md) och [Sling Logging](https://sling.apache.org/site/logging.html).

**Apache Sling Resource Resolver** FactoryKonfigurera centrala aspekter av Sling-resursupplösning:

* **Sökväg** till resursen, lägg till projektspecifika sökvägar (men ta inte bort  `/libs` eller  `/apps`).

* **Virtuella** URL:er för att definiera dina egna URL-mappningar.

* **URL-** mappningar för att definiera alias, till exempel från  `/content` till  `/`.

* **Mappningsplats**, mappningskonfigurationen är externaliserad i  `/etc/map`.

* Använd den lokala installationen (använd till exempel `https://localhost:4502/system/console/jcrresolver`) för att avgöra vilken resurslösare som är aktiv.

Mer information finns i: [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>Dessa alternativ måste särskilt konfigureras i databasen.
>
>I annat fall kan ändringar som görs i **URL-mappningar** med Felix-konsolen skrivas över av AEM vid nästa start.

**Apache Sling Server/Script Resolver och Error** HandlerSling Server och Script Resolver har flera uppgifter:

1. Den används som `ServletResolver` för att välja den server eller det skript som ska anropas för att hantera begäran.

1. Det fungerar som `SlingScriptResolver`.

1. Den hanterar felhantering genom att implementera gränssnittet `ErrorHandler` med samma algoritm för att välja felhanteringsservrar och skript som används för att matcha servrar och skript för begärandebearbetning.

Du kan ange olika parametrar, bland annat:

* **Körningsbanor** visar sökvägarna för körbara skript. genom att konfigurera specifika sökvägar kan du begränsa vilka skript som kan köras. Om ingen sökväg är konfigurerad används standardvärdet ( `/` = root), vilket gör att alla skript kan köras.
Om ett konfigurerat sökvägsvärde avslutas med ett snedstreck genomsöks hela underträdet. Utan ett sådant avslutande snedstreck kommer skriptet endast att köras om det är en exakt matchning.

* **Skriptanvändare**  - den här valfria egenskapen kan ange det databasanvändarkonto som används för att läsa skripten. Om inget konto anges används användaren `admin` som standard.

* **Standardtillägg:** Listan med tillägg som standardbeteendet ska användas för. Det innebär att det sista sökvägssegmentet i resurstypen kan användas som skriptnamn.

**Day Commons GFX Font** HelperNär du återger grafik kan du använda DrawText för att bädda in text. För detta kan du även installera egna teckensnitt:

* Definiera den **teckensnittssökväg** som ska genomsökas efter projektspecifika teckensnitt.
Till exempel, `/apps/myapp/fonts`.

**Konfiguration av Apache HTTP Components Proxy** ConfigurationProxy för all kod som använder Apache HTTP-klienten, som används när en HTTP görs. till exempel vid replikering.

När du skapar en ny konfiguration ska du inte ändra fabrikskonfigurationen utan i stället skapa en ny fabrikskonfiguration för den här komponenten med hjälp av konfigurationshanteraren som finns här: **https://localhost:4502/system/console/configMgr/**. Proxykonfigurationen är tillgänglig i **org.apache.http.proxyconfigurator.**

>[!NOTE]
>
>I AEM 6.0 och tidigare versioner konfigurerades proxy i Day Commons HTTP Client. Från och med AEM 6.1 och senare versioner har proxykonfigurationen flyttats till proxykonfigurationen för Apache HTTP Components i stället för konfigurationen för Day Commons HTTP Client.

**Day CQ** AntispamKonfigurera den antispam-tjänst (Akismet) som används. Du måste registrera:

* **Provider**
* **API-nyckel**
* **Registrerad URL**

**Adobe Granite HTML Library** ManagerKonfigurera detta för att styra hanteringen av klientbibliotek (css eller js). inklusive, till exempel, hur den underliggande strukturen ses.

* För produktionsinstanser:

   * aktivera **Minify** (för att ta bort CRLF- och blankstegstecken).
   * aktivera **Gzip** (om du vill tillåta att filer grupperas och nås med en begäran).
   * inaktivera **Felsök**
   * inaktivera **Timing**

* För JS-utveckling (särskilt vid felsökning/felsökning):

   * inaktivera **Minify**
   * aktivera **Debug** för att separera filerna för felsökning och använda med brandbug.
   * aktivera **Timing** vid intresse för timing.
   * aktivera **Debug**-konsolen för att visa JS-konsolens loggmeddelanden.

>[!CAUTION]
>
>När du ändrar inställningen för antingen **Minify** eller **Gzip** måste du även ta bort innehållet i `/var/clientlibs`. Det här är en cachelagrad version av klientlibs och kommer att byggas om nästa gång du begär det.

>[!NOTE]
>
>Den här inställningen konfigureras automatiskt för produktionsinstanser om du kör AEM i [produktionsklart läge](/help/sites-administering/production-ready.md).

**Day CQ HTTP Header Authentication** HandlerSystemövergripande inställningar för den grundläggande autentiseringsmetoden i HTTP-begäran.

När du använder [stängda användargrupper](/help/sites-administering/cug.md) kan du konfigurera (bland annat):

* **HTTP-sfär**
* **Standardinloggningssida**

**Day CQ Link Checker** ServiceCheck och konfigurera vid behov:

* **Schemaläggarens** period för att definiera intervallet där externa länkar ska kontrolleras automatiskt.

* Markera **Felaktigt intervall för länktolerans** för den period efter vilken en felaktig extern länk anses vara skadad.
* **Länkkontroll åsidosätt mönster**, för att definiera de banor som ska uteslutas från länkkontroll.

**CQ Link Checker-** uppgift för DagKonfigurera inställningar för en enda länkkontrollåtgärd (en uppgift som kontrollerar en extern länk):

* Kontrollera intervallen som definierats i **Testintervall för bra länkar** och **Testintervall för felaktig länk**

* De olika parametrar som rör proxy för Internetåtkomst och NTLM som behövs för extern åtkomst när en länk kontrolleras.

**Day CQ Mail** ServiceKonfigurera värdnamn och åtkomstinformation för e-postservern. Se avsnittet Konfigurera e-posttjänsten.

**Day CQ MCM** NewsletterKonfigurera de olika inställningar som används i nyhetsbrevet.

**Dag CQ-** rotmappningKonfigurera:

* **Målsökväg** som definierar var en begäran till &quot;  `/`&quot; kommer att omdirigeras till.

Det finns två gränssnitt i AEM:

* det pekaktiverade användargränssnittet är standardgränssnittet
* och det inaktuella klassiska användargränssnittet fungerar fortfarande

Med hjälp AEM rotmappning kan du konfigurera det användargränssnitt som du vill använda som standard för din instans:

* **Målsökvägen** ska peka på följande om du vill att det pekaktiverade användargränssnittet ska vara standardgränssnitt:

   ```
      /projects.html
   ```

* Om du vill att det klassiska användargränssnittet ska vara standardgränssnittet pekar målsökvägen **till:**

   ```
      /welcome.html
   ```

>[!NOTE]
>
>Vid en standardinstallation är det pekoptimerade användargränssnittet standardgränssnittet.

**Adobe Granite SSO Authentication** HandlerKonfigurera enkel inloggning (SSO) information; dessa behövs ofta i Enterprise Author Setup, ofta tillsammans med LDAP.

Det finns olika konfigurationsegenskaper:

* ****
PathPath som den här autentiseringshanteraren är aktiv för. Om den här parametern lämnas tom inaktiveras autentiseringshanteraren. Sökvägen / gör att autentiseringshanteraren används för hela databasen.

* **Rankningsvärdet för tjänsten**
OSGi Framework Service Ranking används för att ange den order som används för att anropa den här tjänsten. Det här är en 
`int` där högre värden anger högre prioritet.
Standardvärdet är `0`.

* **Rubriknamn**
Namnet på rubriker som kan innehålla ett användar-ID.

* **Cookie-**
namnNamnet/namnen på cookies som kan innehålla ett användar-ID.

* **Parameternamn**
Namnet/namnen på parametrarna som kan ange användar-ID.

* **User**
MapFör valda användare kan användarnamnet som extraheras från HTTP-begäran ersättas med ett annat i autentiseringsobjektet. Mappningen definieras här. Om användarnamnet 
`admin` visas på båda sidor om kartan, kommer mappningen att ignoreras. Observera att tecknet &quot;=&quot; måste föregås av ett &quot;\&quot;-tecken.

* **Format**
Anger i vilket format användar-ID:t anges. Användning:

   * `Basic` om användar-ID är kodat i HTTP Basic Authentication-format
   * `AsIs` om användar-ID anges i oformaterad text eller ett reguljärt uttryck ska användas som det är eller ett reguljärt uttryck

**Dag CQ WCM Felsökningsfilter** Detta är användbart vid utveckling eftersom det tillåter användning av suffix som ?debug=layout vid åtkomst av en sida. https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout tillhandahåller till exempel layoutinformation som kan vara av intresse för utvecklaren.

* Inaktivera detta på produktionsinstanser för att säkerställa prestanda och säkerhet.

**Dag CQ WCM-** filterKonfigurera:

* **WCM-läge **för att definiera standardläge.
* I en författarinstans kan det vara `edit`, `disable,preview` eller `analytics`.
De andra lägena kan nås från sidosparken eller så kan suffixet `?wcmmode=disabled` användas för att emulera en produktionsmiljö.

* I en publiceringsinstans måste detta anges till `disabled` för att säkerställa att inget annat läge är tillgängligt.

>[!NOTE]
>
>Den här inställningen konfigureras automatiskt för produktionsinstanser om du kör AEM i [produktionsklart läge](/help/sites-administering/production-ready.md).

**Dag CQ WCM Link Checker** ConfiguratorKonfigurera:

* **Lista med** konfigurationer för omskrivning för att ange en lista med platser för innehållsbaserade länkkontrollerarkonfigurationer. Konfigurationerna kan baseras på körläge. det är viktigt att kunna skilja mellan redigerings- och publiceringsmiljöer, eftersom inställningarna för länkkontroll kan variera.

**Day CQ WCM Page** ProcessorConfigure:

* **Banor** är en lista över platser där systemet lyssnar efter sidändringar innan en utlösare aktiveras  `jcr:Event`.

**Adobe Page Impressions** TrackerKonfigurera för en författarinstans:

* **sling.auth.requirements**: ange värdet för den här egenskapen till  `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>Den här konfigurationen tillåter anonyma begäranden till spårningstjänsten.

>[!NOTE]
>
>Mer information finns i [Sidavbildningar](/help/sites-deploying/configuring.md#enabling-page-impressions).

**Day CQ WCM Page** StatisticsKonfigurera för en publiceringsinstans:

* **URL för att skicka** data måste konfigurera den URL som används för att spåra sidstatistik (är avgörande om en spårningsbegäran går igenom dispatchern). Standardvärdet är till exempel  `https://localhost:4502/libs/wcm/stats/tracker`.

* **Spårningsskript** aktiverade för att aktivera (  `true`) eller inaktivera (  `false`) inkludering av spårningsskriptet på sidorna. Standardvärdet är `false`.

>[!NOTE]
>
>Mer information finns i [Sidavbildningar](/help/sites-deploying/configuring.md#enabling-page-impressions).

**Day CQ WCM Version** ManagerKontrollera om och hur versionerna hanteras i systemet:

* **Skapa version vid aktivering**, aktiverad i en standardinstallation
* **Aktivera tömning**

* **Rensa banor**, sökvägarna som en sökåtgärd söker efter
* **Implicit versionssökvägar**, de sökvägar där implicit versionshantering är aktiv.

* **Högsta versionsålder**, högsta ålder (i dagar) för en version

* **Max antal versioner**, maximalt antal versioner att behålla

Mer information finns i [Rensning av version](/help/sites-deploying/version-purging.md).

**Day CQ Workflow Email Notification** ServiceKonfigurera e-postinställningarna för meddelanden som skickas av ett arbetsflöde.

**Day CQSE HTTP** ServiceKontrollera CQ-servermotorn:

* **NIO för HTTP, **Om NIO ska användas för HTTP eller inte. Standardvärdet är true. Används endast om HTTP är aktiverat.
* **Timeout för anslutning, **Timeout för anslutning i millisekunder. Den här egenskapen gäller för både HTTP- och HTTPS-anslutningar. Standardvärdet är 60 sekunder.

* **Aktivera HTTPS,** oavsett om HTTPS är aktiverat eller inte. Standardvärdet är false.
* **Sessionstimeout**, standardlivstid för en HTTP-session angiven i minuter. Om tidsgränsen är 0 eller mindre kommer sessionerna aldrig att tidsgränsen överskrids. Standardvärdet är 10 minuter.
* **Felsökningsloggning**, om meddelanden på DEBUG-nivå ska skrivas eller inte. Standardvärdet är false.
* **Begär buffertstorlek**, buffertstorlek för begäranden i byte. Standardvärdet är 8 kB.
* **Maximalt antal trådar**, maximalt antal trådar som kan användas för att hantera begäranden. Standardvärdet är 200.

Följande egenskaper gäller bara om HTTPS är aktiverat.

* **HTTPS-port**, port att lyssna på för HTTPS-begäran. Standardvärdet är 433.
* **NIO för HTTPS**, om NIO ska användas för HTTP eller inte. Standardvärdet är värdet för egenskapen NIO för HTTP.
* **Keystore**, Absolut sökväg till Keystore som ska användas för HTTPS. Krävs om HTTPS är aktiverat.
* **Lösenord** för nyckelbehållare, lösenord för att komma åt nyckelbehållaren.
* **Nyckelalias**, alias för den hemliga nyckeln i nyckelbehållaren.
* **Nyckellösenord**, Lösenord för att låsa upp den hemliga nyckeln i nyckelbehållaren.
* **Klientcertifikat**, krav på att klienten ska tillhandahålla ett giltigt certifikat. Standardvärdet är ingen.

Se även [Aktivera HTTP över SSL](/help/sites-administering/ssl-by-default.md) för mer information om SSL-relaterade alternativ och en fullständig beskrivning av hur du aktiverar HTTPS för CQSE.

**CQ Rewriter HTML Parser Factory**

Styr HTML-tolken för CQ-omskrivaren.

* **Ytterligare taggar att bearbeta**  - Du kan lägga till eller ta bort HTML-taggar som ska bearbetas av parsern. Som standard bearbetas följande taggar: A,IMG,AREA,FORM,BASE,LINK,SCRIPT,BODY,HEAD.
* **Bevara kamerafodral** - Som standard konverterar HTML-tolken attribut i kamelfodral (t.ex. eBay) till gemener (t.ex. ebay). Du kan stänga av det här om du vill bevara attributen för kamerans skiftläge. Detta är användbart när du använder ramverk som Angular 2.

**JDBC Connections-** poolen DagKonfigurera åtkomst till en extern databas som används som innehållskälla.

Detta är en fabrikskonfiguration, så det går att konfigurera flera instanser.

**Adobe CQ Media DPS Sessions** ServiceHantera DPS-sessioner för användning med publikationer.

Du kan särskilt definiera `dps.session.service.url.name`: standard är [https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions](https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions)

**CDN** RewriterKommunikation mellan AEM och CDN måste säkerställas så att resurser och binära filer levereras till slutanvändaren på ett säkert sätt. Detta innebär två uppgifter:

* Åtkomst till resursen från AEM via CDN första gången (eller efter att den har gått ut i cache).
* Åtkomst till resursen som cachelagrats i CDN på ett säkert sätt eftersom resursen cachelagras i CDN, begäran inte går till AEM och alla användare som har åtkomst till resursen på ska hanteras från CDN.

AEM innehåller en omskrivare för att skriva om interna URL:er för resurser till externa CDN-URL:er. Den skriver om länkar som ska skickas vidare till CDN, inklusive en JWS-signatur, och anger att resursen ska kunna nås på ett säkert sätt. Den här funktionen ska användas på författarinstanser.

Det övergripande flödet är följande:

1. Användaren autentiserar med AEM och begär en sida med resurser.
1. Den begärda sidan innehåller en resurs som liknar `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. Omskrivare omvandlar länken till en CDN-URL som innehåller en JWS-signatur:
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. Användarens webbläsare vidarebefordrar sedan resursbegäran till CDN-servern
1. CDN bör konfigureras för att vidarebefordra begäran till AEM med `cdn_sign`-parametern.
1. En autentiseringshanterare validerar parametern `cdn_sign` och returnerar resursen till CDN som sedan levereras till användaren

Flödet mellan användarens webbläsare, CDN och AEM kan visas på följande sätt.

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>Den här funktionen är för närvarande bara aktiverad för AEM författarinstanser.

**** CDNConfigServiceImplTillhandahåller CDN-konfigurationer

CDN-omskrivningsfunktionen kan aktiveras genom att du anger **CDN-distributionsdomännamnet** i konfigurationen för com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl.

Tjänsten innehåller även andra konfigurationsalternativ som att aktivera/inaktivera CDN-omskrivning, sökvägsprefix som CDN-omskrivning utförs för, TTL-värden och protokoll (HTTP eller HTTPS).

**** CDNRewriterEn omskrivare för att skriva om interna bild-URL:er till CDN-URL:er

Värdet **Taggattribut** i com.adobe.cq.cdn.rewriter.impl.CDNRewriter kan definieras så att endast selektiva bildlänkar skrivs om.
