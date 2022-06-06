---
title: Konfigurationsinställningar för OSGi
seo-title: OSGi Configuration Settings
description: Den här artikeln innehåller information om de OSGi-konfigurationsinställningar (listade enligt paket) som är relevanta för projektimplementeringen. Förteckningen fungerar som riktlinjer och är inte uttömmande.
seo-description: This article details the OSGi configuration settings (listed according to bundle) that are relevant to project implementation. The list acts as a guideline and it is not exhaustive.
uuid: 192d3287-ec99-403b-bab0-45721e4e3abd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: ed3a858c-7a43-4515-a2ff-43ca465c7d7d
docset: aem65
feature: Configuring
exl-id: 19eedcf2-140a-452d-aa8f-6fd7f219e5f8
source-git-commit: e8320b1dac681fd2c9e749344e8c126487d840ba
workflow-type: tm+mt
source-wordcount: '3557'
ht-degree: 0%

---

# Konfigurationsinställningar för OSGi{#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) är en grundläggande del i AEM. Det används för att styra de sammansatta AEM och deras konfiguration.

OSGi &quot;*innehåller standardmallar som gör det möjligt att konstruera program utifrån små, återanvändbara och samverkansbaserade komponenter. Dessa komponenter kan sammanställas i ett program och distribueras*&quot;.

Detta gör det enkelt att hantera paket när de kan stoppas, installeras och startas individuellt. De inbördes beroendena hanteras automatiskt. Varje OSGi-komponent (se [OSGi-specifikation](https://www.osgi.org/Specifications/HomePage)) finns i ett av de olika paketen. När du arbetar med AEM finns det flera metoder för att hantera konfigurationsinställningarna för sådana paket. se [Konfigurerar OSGi](/help/sites-deploying/configuring-osgi.md) om du vill ha mer information och rekommenderade rutiner.

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
>Diff-verktyget för OSGi-konfiguration, som ingår i [AEM](https://helpx.adobe.com/experience-manager/kb/tools/aem-tools.html), kan användas för att lista OSGi-standardkonfigurationer.

>[!NOTE]
>
>Ytterligare programpaket kan behövas för specifika funktionsområden inom AEM. I dessa fall finns konfigurationsinformation på sidan som rör lämplig funktion.

**Händelseavlyssnare för AEM** Konfigurera:

* The **Körningslägen**, i vilken replikeringshändelser distribueras till avlyssnare. Om det till exempel definieras som författare är detta det system som kommer att&quot;initiera&quot; replikeringen.

* Körningsläget **publicera** måste läggas till om projektkoden bearbetar replikeringshändelser (omvänd replikering) i en publiceringsmiljö. Om dispatchern till exempel används för att tömma från publiceringsmiljön eller när standardreplikering till andra publiceringsinstanser sker.

**AEM för databasändring** Konfigurera:

* The **Banor**, platser att avlyssna databashändelser som är klara för distribution.

**CRX Sling Client Repository** Konfigurera åtkomst till den underliggande innehållsdatabasen.

* The **Administratörslösenord** bör ändras efter installationen för att säkerställa att [säkerhet](/help/sites-administering/security-checklist.md) av din instans.
* Andra ändringar bör inte vara nödvändiga och försiktighet måste vidtas eftersom de kan påverka åtkomsten till databasen.

**Wiki Mail-tjänst** Konfigurera e-postinställningarna för e-post som skickas av en wiki.

**Apache Felix OSGi Management Console** Konfigurera:

* **Plugins**, de huvudsakliga navigeringsobjekten (konsolplugin-program) som ska vara tillgängliga i **Apache Felix Web Management Console** som menyalternativ på den översta nivån. Inaktivera allt du inte behöver eftersom utrymme och resurser krävs för varje åtgärd.

>[!CAUTION]
>
>Var noga med att konfigurera följande:
>
>**Användarnamn** och **Lösenord**, inloggningsuppgifterna för åtkomst till själva Apache Felix Web Management Console.
>Lösenordet måste ändras efter den första installationen för att säkerställa att [säkerhet](/help/sites-administering/security-checklist.md) av din instans.

>[!NOTE]
>
>Den här konfigurationen bör göras med Felix Console så som den behövs vid start - innan databasen är tillgänglig.

**Dataloggning för anpassningsbara Apache Sling-begäranden** Konfigurera:

* **Loggningsnamn** och **Loggformat** för att konfigurera plats och format för begäran och åtkomstloggning (standard: `request.log`). Den här loggfilen är viktig när du analyserar prestanda eller felsökningsfunktioner som är relaterade till webbkedjan.
Detta är tillsammans med [Apache Sling Request Logger](#apacheslingrequestlogger).

Mer information finns på [AEM loggning](/help/sites-deploying/configure-logging.md) och [Sling Logging](https://sling.apache.org/site/logging.html).

**Spetsig händelsetrådspool för Apache Sling** Konfigurera:

* **Minsta poolstorlek** och **Maximal poolstorlek**, storleken på poolen som används för att lagra händelsetrådar.

* **Köstorlek**, den maximala storleken för trådkön om poolen är slut.
Det rekommenderade värdet är `-1` eftersom kön då är obegränsad, om en gräns anges kan förluster uppstå när den överskrids.

* Om du ändrar de här inställningarna kan du förbättra prestandan i scenarier med ett stort antal händelser. till exempel AEM DAM eller arbetsflöde.
* Värden som är specifika för ditt scenario bör fastställas med hjälp av tester.
* De här inställningarna kan påverka instansens prestanda, så ändra dem inte utan orsak och vederbörlig hänsyn.

**Apache Sling GET Servlet** Konfigurera vissa återgivningsaspekter:

* **Automatiskt index** om du vill aktivera/inaktivera katalogåtergivning för bläddring.
* **Aktivera** (eller inaktivera) standardåtergivningar, som **HTML**, **Oformaterad text**, **JSON** eller **XML**.
Du bör inte inaktivera JSON.

>[!NOTE]
>
>Den här inställningen konfigureras automatiskt för produktionsinstanser om du kör AEM i [Produktionsklar läge](/help/sites-administering/production-ready.md).

**Apache Sling Java Script Handler** Konfigurera inställningar för kompilering av Java-filer som skript (serverlets).

Vissa inställningar kan påverka prestandan. De bör inaktiveras där det är möjligt, särskilt för en produktionsinstans.

* **Käll-VM** och **Mål-VM** definierar du JDK-versionen som den som används som JVM vid körning

* för produktionsinstanser:

   * disable **Generera felsökningsinformation**

**Installationsprogram för Apache Sling JCR** De här parametrarna behöver förmodligen inte konfigureras, men de kan vara användbara när du utvecklar eller felsöker. Installationsmappen kan till exempel vara användbar för att checka in/ut eller skapa ett paket.

* **Installationsmappens namn regexp** och **Maximalt hierarkidjup för installationsmappar** - ange var, och till vilket djup, databasmappar söks efter resurser som ska installeras. När ett jokertecken används (som i .&#42;/install) söks igenom alla matchningar, till exempel `/libs/sling/install` och `/libs/cq/core/install`.

* **Sökväg**, en lista med sökvägar som installeras söker efter resurser som ska installeras, tillsammans med en siffra som anger viktningsfaktorn för sökvägen.

**Händelsehanterare för Apache Sling-jobb** Konfigurera parametrar som hanterar jobbplanering:

* **Återförsöksintervall**, **Maximalt antal återförsök**, **Maximalt antal parallella jobb**, **Bekräfta väntetid**, bland annat.

* Om du ändrar dessa inställningar kan prestandan förbättras i scenarier med ett stort antal jobb. till exempel stor användning av AEM DAM och arbetsflöden.
* Värden som är specifika för ditt scenario bör fastställas med hjälp av tester.
* Ändra inte de här inställningarna utan orsak. Ändra bara efter vederbörlig hänsyn.

**Apache Sling JSP Script Handler** Konfigurera prestandainställningar som är relevanta för JSP-skripthanteraren. För att förbättra prestanda bör du inaktivera så mycket som möjligt.

Särskilt för produktionsinstanser:

* disable **Generera felsökningsinformation**
* disable **Behåll genererad Java**
* disable **Mappat innehåll**
* disable **Visa källfragment**

>[!NOTE]
>
>Den här inställningen konfigureras automatiskt för produktionsinstanser om du kör AEM i [Produktionsklar läge](/help/sites-administering/production-ready.md).

**Konfiguration av Apache Sling-loggning** Konfigurera:

* **Loggnivå** och **Loggfil**, för att definiera platsen och loggnivån för konfigurationen för central loggning (error.log). Nivån kan ställas in på något av `DEBUG`, `INFO`, `WARN`, `ERROR` och `FATAL`.

* **Antal loggfiler** och **Tröskelvärde för loggfil** om du vill definiera storleken och versionsrotationen för loggfilen.

* **Meddelandemönster** definierar loggmeddelandenas format.

Mer information finns på [AEM loggning](/help/sites-deploying/configure-logging.md#global-logging) och [Sling Logging](https://sling.apache.org/site/logging.html).

**Konfiguration av loggningslogg för Apache Sling (fabrikskonfiguration)** Konfigurera:

* **Loggnivå**, **Loggfil** och **Meddelandeformat** om du vill definiera information om loggfilen och meddelanden.

* **Logger** Definiera kategorin. till exempel bara log för com.day.cq.

* Genom att använda **Fabrikskonfigurationer** kan valfritt antal ytterligare konfigurationer läggas till för att tillgodose de olika loggnivåer och kategorier som behövs.
* Sådana konfigurationer är till hjälp vid utvecklingen. om du till exempel vill logga TRACE-meddelanden för en viss tjänst i en viss loggfil.
* Sådana konfigurationer är användbara i en produktionsmiljö. om du till exempel vill att meddelanden om en viss tjänst ska loggas i en enskild loggfil för enklare övervakning.

Mer information finns på [AEM loggning](/help/sites-deploying/configure-logging.md) och [Sling Logging](https://sling.apache.org/site/logging.html).

**Konfiguration av skrivprogram för Apache Sling-loggning (fabrikskonfiguration)** Konfigurera:

* **Loggfil** för att definiera om det finns en loggfil.
* **Antal loggfiler** för att definiera versionsrotationen.

* Skrivaren kan användas av en **Konfiguration av loggningsloggare för Apache Sling** konfiguration.

* Sådana konfigurationer är till hjälp vid utvecklingen. om du till exempel vill logga TRACE-meddelanden för en viss tjänst i en viss loggfil.
* Sådana konfigurationer är användbara i en produktionsmiljö. om du till exempel vill att meddelanden om en viss tjänst ska loggas i en enskild loggfil för enklare övervakning.

Mer information finns på [AEM loggning](/help/sites-deploying/configure-logging.md) och [Sling Logging](https://sling.apache.org/site/logging.html).

**Apache Sling Main Servlet** Konfigurera:

* **Antal samtal per begäran** och **Rekursionsdjup** för att skydda datorn mot oändlig rekursion och överdrivna skriptanrop.

**Apache Sling MIME Type Service** Konfigurera:

* **MIME-typer** för att lägga till de som krävs för ditt projekt i systemet. Detta gör att `GET` begära att en fil ska ange rätt innehållstypsrubrik för länkning av filtypen och programmet.

**Apache Sling Referer-filter** För att åtgärda kända säkerhetsproblem med CSRF (Cross-Site Request Forgery) i CRX WebDAV och Apache Sling måste du konfigurera referensfiltret.

Refererarfiltertjänsten är en OSGi-tjänst som gör att du kan konfigurera:

* vilka http-metoder som ska filtreras
* om en tom referensrubrik tillåts
* och en lista över servrar som ska tillåtas utöver servervärden.

Se [Säkerhetschecklista - Problem med förfalska begäran mellan webbplatser](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) för mer information.

>[!NOTE]
>
>Refererarfiltret för Apache Sling är beroende av att ett snabbkorrigeringspaket har installerats.

**Apache Sling Request Logger** Konfigurera:

* olika parametrar för att definiera hur begäranden loggas.
* **Aktivera begärandelogg**, för att aktivera eller inaktivera.

* **Aktivera åtkomstlogg**, för att aktivera eller inaktivera.

Detta är tillsammans med [Dataloggning för anpassningsbara Apache Sling-begäranden](#apacheslingcustomizablerequestdatalogger).

Mer information finns på [AEM loggning](/help/sites-deploying/configure-logging.md) och [Sling Logging](https://sling.apache.org/site/logging.html).

**Apache Sling Resource Resolver Factory** Konfigurera centrala aspekter av Sling-resursupplösning:

* **Sökväg för resurs**(s), lägga till projektspecifika sökvägar (men ta inte bort) `/libs` eller `/apps`).

* **Virtuella URL:er** för att definiera dina egna URL-mappningar.

* **URL-mappningar** Definiera alias. till exempel från `/content` till `/`.

* **Mappningsplats**, är mapparkonfigurationen externaliserad i `/etc/map`.

* Använd din lokala installation (använd till exempel `https://localhost:4502/system/console/jcrresolver`) för att avgöra vilken resurslösare som är aktiv.

Mer information finns i: [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>Dessa alternativ måste särskilt konfigureras i databasen.
>
>Andra ändringar gjorda i **URL-mappningar** att använda Felix-konsolen kan skrivas över av AEM nästa gång programmet startas.

**Apache Sling Servlet/Script Resolver och Error Handler** Sling Server och Script Resolver har flera åtgärder:

1. Det används som `ServletResolver` för att välja den server eller det skript som ska anropas för att hantera begäran.

1. Det fungerar som `SlingScriptResolver`.

1. Den hanterar felhantering genom att implementera `ErrorHandler` -gränssnitt som använder samma algoritm för att välja felhanteringsservrar och skript som används för att matcha servrar och skript för begärandebearbetning.

Du kan ange olika parametrar, bland annat:

* **Körningsbanor** visar sökvägarna för att söka efter körbara skript, genom att konfigurera specifika sökvägar kan du begränsa vilka skript som kan köras. Om ingen sökväg är konfigurerad används standardinställningen ( `/` = root), detta tillåter körning av alla skript.
Om ett konfigurerat sökvägsvärde avslutas med ett snedstreck genomsöks hela underträdet. Utan ett sådant avslutande snedstreck kommer skriptet endast att köras om det är en exakt matchning.

* **Skriptanvändare** - den här valfria egenskapen kan ange det databasanvändarkonto som används för att läsa skripten. Om inget konto anges `admin` används som standard.

* **Standardtillägg** Listan över tillägg som standardbeteendet ska användas för. Det innebär att det sista sökvägssegmentet i resurstypen kan användas som skriptnamn.

**Day Commons GFX Font Helper** När du återger bilder kan du använda DrawText för att bädda in text. För detta kan du även installera egna teckensnitt:

* Definiera **Teckensnittssökväg** som ska genomsökas efter projektspecifika teckensnitt.
Till exempel, `/apps/myapp/fonts`.

**Proxykonfiguration för Apache HTTP-komponenter** Proxykonfiguration för all kod med Apache HTTP-klienten som används när en HTTP görs. till exempel vid replikering.

När du skapar en ny konfiguration ska du inte ändra fabrikskonfigurationen utan i stället skapa en ny fabrikskonfiguration för den här komponenten med hjälp av konfigurationshanteraren som finns här: **https://localhost:4502/system/console/configMgr/**. Proxykonfigurationen är tillgänglig i **org.apache.http.proxyconfigurator.**

>[!NOTE]
>
>I AEM 6.0 och tidigare versioner konfigurerades proxy i Day Commons HTTP Client. Från och med AEM 6.1 och senare versioner har proxykonfigurationen flyttats till proxykonfigurationen för Apache HTTP Components i stället för konfigurationen för Day Commons HTTP Client.

**Day CQ Antispam** Konfigurera den antispamtjänst (Akismet) som används. Du måste registrera:

* **Provider**
* **API-nyckel**
* **Registrerad URL**

**Bibliotekshanteraren Adobe Granite HTML** Konfigurera detta för att styra hanteringen av klientbibliotek (css eller js), inklusive, till exempel, hur den underliggande strukturen ses.

* För produktionsinstanser:

   * enable **Minify** (för att ta bort CRLF- och blankstegstecken).
   * enable **Gzip** (för att tillåta att filer grupperas och öppnas med en begäran).
   * disable **Felsök**
   * disable **Timing**

* För JS-utveckling (särskilt vid felsökning/felsökning):

   * disable **Minify**
   * enable **Felsök** om du vill separera filerna för felsökning och använda dem med brandbug.
   * enable **Timing** när det gäller intresse för tidpunkt.
   * enable **Felsök** för att se JS-konsolens loggmeddelanden.

>[!CAUTION]
>
>När du ändrar inställningen för antingen **Minify** eller **Gzip** Du måste också ta bort innehållet i `/var/clientlibs`. Det här är en cachelagrad version av klientlibs och kommer att byggas om nästa gång du begär det.

>[!NOTE]
>
>Den här inställningen konfigureras automatiskt för produktionsinstanser om du kör AEM i [Produktionsklar läge](/help/sites-administering/production-ready.md).

**Hanterare för HTTP-huvudautentisering för daglig CQ** Systemomfattande inställningar för den grundläggande autentiseringsmetoden i HTTP-begäran.

När du använder [stängda användargrupper](/help/sites-administering/cug.md) du kan konfigurera (bland annat):

* **HTTP-sfär**
* The **Standardinloggningssida**

**Dag CQ Link Checker Service** Kontrollera och konfigurera vid behov:

* **Schemaläggningsperiod** för att definiera intervallet där externa länkar ska kontrolleras automatiskt.

* Kontrollera **Felaktigt toleransintervall för länkar** under den period efter vilken en misslyckad extern länk anses vara felaktig.
* **Åsidosättningsmönster för länkkontroll**, för att definiera sökvägar som ska uteslutas från länkkontroll.

**CQ-länkkontrolluppgift för dag** Konfigurera inställningar för en enskild länkkontrollåtgärd (en uppgift som kontrollerar en extern länk):

* Kontrollera intervallen som definieras i **Testintervall för bra länkar** och **Testintervall för felaktig länk**

* De olika parametrar som rör proxy för Internetåtkomst och NTLM som behövs för extern åtkomst när en länk kontrolleras.

**Dagens CQ-posttjänst** Konfigurera värdnamn och åtkomstinformation för e-postservern. Se avsnittet Konfigurera e-posttjänsten.

**Day CQ MCM Newsletter** Konfigurera de olika inställningar som används för nyhetsbrevet.

**CQ-rotmappning för dag** Konfigurera:

* **Målsökväg** för att definiera var en begäran ska `/`&quot; kommer att omdirigeras till.

Det finns två gränssnitt i AEM:

* det pekaktiverade användargränssnittet är standardgränssnittet
* och det inaktuella klassiska användargränssnittet fungerar fortfarande

Med hjälp AEM rotmappning kan du konfigurera det användargränssnitt som du vill använda som standard för din instans:

* Om du vill att det pekaktiverade användargränssnittet ska vara standardanvändargränssnittet **Målsökväg** ska peka på:

   ```shell
      /projects.html
   ```

* Om du vill att det klassiska användargränssnittet ska vara standardanvändargränssnittet **Målsökväg** ska peka på:

   ```shell
      /welcome.html
   ```

>[!NOTE]
>
>Vid en standardinstallation är det pekoptimerade användargränssnittet standardgränssnittet.

**Autentiseringshanterare för Adobe Granite SSO** Konfigurera SSO-information (Single Sign On); dessa behövs ofta i Enterprise Author Setup, ofta tillsammans med LDAP.

Det finns olika konfigurationsegenskaper:

* **Bana**
Sökväg som den här autentiseringshanteraren är aktiv för. Om den här parametern lämnas tom inaktiveras autentiseringshanteraren. Sökvägen / gör att autentiseringshanteraren används för hela databasen.

* **Servicerangordning**
OSGi Framework Service Ranking-värdet används för att ange den order som används för att anropa den här tjänsten. Det här är en 
`int` där högre värden anger högre prioritet.
Standardvärdet är `0`.

* **Rubriknamn**
Namn på rubriker som kan innehålla ett användar-ID.

* **Cookie-namn**
Namnet/namnen på cookies som kan innehålla ett användar-ID.

* **Parameternamn**
Namnet/namnen på parametrarna för begäran som kan ge användar-ID.

* **Användarkarta**
För valda användare kan användarnamnet som extraheras från HTTP-begäran ersättas med ett annat i autentiseringsobjektet. Mappningen definieras här. Om användarnamnet 
`admin` visas på båda sidor om kartan, kommer mappningen att ignoreras. Observera att tecknet &quot;=&quot; måste föregås av ett &quot;\&quot;-tecken.

* **Format**
Anger i vilket format användar-ID:t anges. Användning:

   * `Basic` om användar-ID är kodat i HTTP Basic Authentication-format
   * `AsIs` om användar-ID anges i oformaterad text eller ett reguljärt uttryck ska användas som det är eller ett reguljärt uttryck

**Dag CQ WCM-felsökningsfilter** Detta är användbart vid utveckling eftersom det tillåter användning av suffix som ?debug=layout vid åtkomst till en sida. https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout tillhandahåller till exempel layoutinformation som kan vara av intresse för utvecklaren.

* Inaktivera detta på produktionsinstanser för att säkerställa prestanda och säkerhet.

**Dag CQ WCM-filter** Konfigurera:

* **WCM-läge **för att definiera standardläge.
* I en författarinstans kan det vara `edit`, `disable,preview` eller `analytics`.
De andra lägena kan nås från sidosparken eller suffixet `?wcmmode=disabled` kan användas för att emulera en produktionsmiljö.

* I en publiceringsinstans måste detta anges till `disabled` för att säkerställa att inget annat läge är tillgängligt.

>[!NOTE]
>
>Den här inställningen konfigureras automatiskt för produktionsinstanser om du kör AEM i [Produktionsklar läge](/help/sites-administering/production-ready.md).

**Dag CQ WCM Link Checker Configurator** Konfigurera:

* **Lista över omskrivningskonfigurationer** för att ange en lista över platser för innehållsbaserade länkkontrollerarkonfigurationer. Konfigurationerna kan baseras på körläge. det är viktigt att kunna skilja mellan redigerings- och publiceringsmiljöer, eftersom inställningarna för länkkontroll kan variera.

**Day CQ WCM Page Manager Factory** Konfigurera:

* **Aktiveringskontroll för sidunderträd** för en användare (utan replikeringsbehörighet) att ta bort eller flytta sidor (även om sidorna inte är aktiverade).

**Dag CQ WCM-sidprocessor** Konfigurera:

* **Banor**, en lista med platser där systemet lyssnar efter sidändringar innan en `jcr:Event`.

**Spårare för Adobe-sidimage** Konfigurera för en författarinstans:

* **sling.auth.requirements**: ange värdet för den här egenskapen till `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>Den här konfigurationen tillåter anonyma begäranden till spårningstjänsten.

>[!NOTE]
>
>Se [Sidimeringar](/help/sites-deploying/configuring.md#enabling-page-impressions) för mer information.

**Dagens CQ WCM-sidstatistik** Konfigurera för en publiceringsinstans:

* **URL för att skicka data** konfigurera den URL som används för att spåra sidstatistik (är avgörande om en spårningsbegäran går igenom avsändaren), Standardvärdet är till exempel `https://localhost:4502/libs/wcm/stats/tracker`.

* **Spårningsskript har aktiverats** för att aktivera ( `true`) eller inaktivera ( `false`) inkluderar spårningsskriptet på sidorna. Standardvärdet är `false`.

>[!NOTE]
>
>Se [Sidimeringar](/help/sites-deploying/configuring.md#enabling-page-impressions) för mer information.

**Day CQ WCM Version Manager** Kontrollera om och hur versionerna hanteras i systemet:

* **Skapa version vid aktivering**, aktiverad i en standardinstallation
* **Aktivera tömning**

* **Rensa banor** sökvägarna som sökåtgärden söker efter
* **Underförstådda versionsbanor**, sökvägarna där implicit versionshantering är aktiv.

* **Högsta versionsålder**, högsta ålder (i dagar) för en version

* **Max antal versioner**, det maximala antalet versioner som ska behållas

Se [Rensning av version](/help/sites-deploying/version-purging.md) för mer information.

**Day CQ Workflow Email Notification Service** Konfigurera e-postinställningarna för meddelanden som skickas av ett arbetsflöde.

**CQ Rewriter HTML Parser Factory**

Styr HTML-parsern för CQ-omskrivaren.

* **Ytterligare taggar att bearbeta** - Du kan lägga till eller ta bort HTML-taggar som ska bearbetas av tolken. Som standard bearbetas följande taggar: A,IMG,AREA,FORM,BASE,LINK,SCRIPT,BODY,HEAD.
* **Bevara kamerafall** - Som standard konverterar HTML-tolken attribut i kamelskiftläge (t.ex. eBay) till gemener (t.ex. ebay). Du kan stänga av det här om du vill bevara attributen för kamerans skiftläge. Detta är användbart när du använder ramverk som Angular 2.

**JDBC-anslutningspool för dagkommentarer** Konfigurera åtkomst till en extern databas som används som innehållskälla.

Detta är en fabrikskonfiguration, så det går att konfigurera flera instanser.

**Tjänsten Adobe CQ Media DPS Sessions** Hantera DPS-sessioner för användning med publikationer.

I synnerhet kan du definiera `dps.session.service.url.name`: standard är inställd på [https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions](https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions)

**CDN Rewriter** Kommunikation mellan AEM och CDN måste säkerställas så att resurser och binära filer levereras till slutanvändaren på ett säkert sätt. Detta innebär två uppgifter:

* Åtkomst till resursen från AEM via CDN första gången (eller efter att den har gått ut i cache).
* Åtkomst till resursen som cachelagrats i CDN på ett säkert sätt eftersom resursen cachelagras i CDN, begäran inte går till AEM och alla användare som har åtkomst till resursen på ska hanteras från CDN.

AEM innehåller en omskrivare för att skriva om interna URL:er för resurser till externa CDN-URL:er. Den skriver om länkar som ska skickas vidare till CDN, inklusive en JWS-signatur, och anger att resursen ska kunna nås på ett säkert sätt. Den här funktionen ska användas på författarinstanser.

Det övergripande flödet är följande:

1. Användaren autentiserar med AEM och begär en sida med resurser.
1. Begärd sida innehåller en resurs som liknar `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. Omskrivare omvandlar länken till en CDN-URL som innehåller en JWS-signatur:
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. Användarens webbläsare vidarebefordrar sedan resursbegäran till CDN-servern
1. CDN bör konfigureras för att vidarebefordra begäran till AEM med `cdn_sign` parameter.
1. En autentiseringshanterare validerar `cdn_sign` parametern och returnerar resursen till CDN som sedan levereras till användaren

Flödet mellan användarens webbläsare, CDN och AEM kan visas på följande sätt.

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>Den här funktionen är för närvarande bara aktiverad för AEM författarinstanser.

**CDNConfigServiceImpl** Tillhandahåller CDN-konfigurationer

CDN-omskrivningsfunktionen kan aktiveras med **Namn på CDN-distributionsdomän** i konfigurationen för com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl.

Tjänsten innehåller även andra konfigurationsalternativ som att aktivera/inaktivera CDN-omskrivning, sökvägsprefix som CDN-omskrivning utförs för, TTL-värden och protokoll (HTTP eller HTTPS).

**CDNRewriter** En omskrivare för att skriva om URL:er för interna bilder till CDN-URL:er

The **Taggattribut** värdet i com.adobe.cq.cdn.rewriter.impl.CDNRewriter kan definieras så att endast selektiva bildlänkar skrivs om.
