---
title: Bästa tillvägagångssätt för arbete med anpassningsbara formulär
description: Beskriver de bästa sätten att skapa ett AEM Forms-projekt, utveckla adaptiva formulär och optimera prestanda för AEM Forms-system.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms, Foundation Components
exl-id: 5c75ce70-983e-4431-a13f-2c4c219e8dde
source-git-commit: d85fc98d9a31bc4014aef4311ba0f838c7ef619a
workflow-type: tm+mt
source-wordcount: '4666'
ht-degree: 0%

---

# Bästa tillvägagångssätt för arbete med anpassningsbara formulär {#best-practices-for-working-with-adaptive-forms}

<span class="preview"> Adobe rekommenderar att man använder modern och utbyggbar datainhämtning [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) for [skapa ny Adaptive Forms](/help/forms/using/create-an-adaptive-form-core-components.md) eller [lägga till adaptiv Forms på AEM Sites-sidor](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter. </span>

## Ökning {#overview}

Adobe Experience Manager (AEM)-formulär kan hjälpa er att omvandla komplexa transaktioner till enkla, roliga digitala upplevelser. Det kräver dock samordnade insatser för att implementera, bygga, genomföra och underhålla ett effektivt och produktivt AEM Forms-ekosystem.

Det här dokumentet innehåller riktlinjer och rekommendationer som formuläradministratörer, författare och utvecklare kan dra nytta av när de arbetar med AEM Forms, särskilt adaptiva formulärkomponenter. Här diskuteras de effektivaste strategierna, från att skapa ett formulärutvecklingsprojekt till att konfigurera, anpassa, skapa och optimera AEM Forms. Dessa bästa metoder bidrar tillsammans till AEM Forms ekosystems allmänna prestanda.

Här finns dessutom några rekommenderade läsningar för allmänna AEM bästa praxis:

* [God praxis: distribuera och underhålla AEM](/help/sites-deploying/best-practices.md)
* [God praxis: Skapa innehåll](/help/sites-authoring/best-practices.md)
* [God praxis: Administrera AEM](/help/sites-administering/administer-best-practices.md)
* [God praxis: Utveckla lösningar](/help/sites-developing/best-practices.md)

## Konfigurera och konfigurera AEM Forms {#set-up-and-configure-aem-forms}

### Konfigurera formulärutvecklingsprojekt {#setting-up-forms-development-project}

En förenklad och standardiserad projektstruktur kan avsevärt minska arbetet med utveckling och underhåll. Apache Maven är ett verktyg med öppen källkod som rekommenderas för att bygga AEM projekt.

* Använd Apache Maven `aem-project-archetype` för att skapa och hantera struktur för AEM projekt. Den skapar rekommenderade strukturer och mallar för AEM projekt. Dessutom innehåller det system för automatisering och ändringskontroll som underlättar hanteringen av projektet.

   * Använd maven `archetype:generate` för att generera den ursprungliga strukturen.
   * Använd maven `eclipse:eclipse` om du vill generera projektfiler som är förmörkade och importera projektet till förmörkade filer.

Mer information finns i [Skapa AEM projekt med Apache Maven](/help/sites-developing/ht-projects-maven.md).

* Med FileVault-verktyget eller VLT kan du mappa innehållet i en CRX- eller AEM-instans till filsystemet. Den innehåller åtgärder för ändringshantering, som in- och utcheckning av AEM projektinnehåll. Se [Så här använder du VLT-verktyget](/help/sites-developing/ht-vlttool.md).

* Om du använder en Eclipse-integrerad utvecklingsmiljö kan du använda AEM utvecklingsverktyg för smidig integrering av Eclipse IDE med AEM instanser för att skapa AEM program. Mer information finns i [AEM för Eclipse](/help/sites-developing/aem-eclipse.md).

* Lagra inte något innehåll och gör inga ändringar i mappen /libs. Skapa övertäckningar i /app-mappar för att utöka eller skriva över standardfunktioner.

* När du skapar paket för att flytta innehåll måste du se till att paketfiltersökvägarna är korrekta och bara obligatoriska sökvägar anges.

* Lagra inte något innehåll och gör inga ändringar i mappen /libs. Skapa övertäckningar i /app-mappar för att utöka eller skriva över standardfunktioner.

* Definiera korrekta beroenden för paketen för att framtvinga en förbestämd installationsordning/sekvens.

* Skapa ingen referensnod i /libs eller /apps.

### Planering för redigeringsmiljö {#planning-for-authoring-environment}

När du väl har skapat AEM projekt kan du definiera en strategi för att skapa och anpassa anpassningsbara blankettmallar och komponenter.

* En adaptiv formulärmall är en specialiserad AEM som definierar struktur och sidhuvud/sidfot-information i ett adaptivt formulär. En mall har förkonfigurerade layouter, format och grundstruktur för ett adaptivt formulär. AEM Forms innehåller färdiga mallar och komponenter som du kan använda för att skapa anpassningsbara formulär. Du kan dock skapa egna mallar och komponenter efter behov. Vi rekommenderar att du samlar in krav för ytterligare mallar och komponenter som du behöver i dina adaptiva formulär. Mer information finns i [Anpassa adaptiva formulär och komponenter](/help/forms/using/adaptive-forms-best-practices.md#customize-components).
* Med AEM Forms kan du skapa anpassningsbara formulär baserade på följande formulärmodeller. Blankettmodellerna fungerar som gränssnitt för datautbyte mellan ett formulär och AEM och ger en XML-baserad struktur för dataflöde både innanför och utanför ett adaptivt formulär. Formulärmodellerna innehåller dessutom regler och begränsningar för anpassningsbara formulär i form av schema- och XFA-begränsningar.

   * **Ingen**: Anpassningsbara formulär som skapas med det här alternativet använder inte någon formulärmodell. Data-XML som genereras från sådana formulär har en platt struktur med fält och motsvarande värden.
   * **XML- eller JSON-schema**: XML- och JSON-scheman representerar den struktur i vilken data produceras eller förbrukas av organisationens serversystem. Du kan koppla ett schema till ett anpassat formulär och använda dess element för att lägga till dynamiskt innehåll i det anpassningsbara formuläret. Elementen i schemat är tillgängliga på fliken Datamodellsobjekt i innehållsläsaren för att skapa adaptiva formulär. Du kan dra och släppa schemaelementen för att skapa formuläret.
   * **XFA-formulärmall**: Det är en idealisk formulärmodell om du har investeringar i XFA-baserade HTML5-formulär. Det är ett direkt sätt att konvertera XFA-baserade formulär till anpassningsbara formulär. Alla befintliga XFA-regler behålls i de tillhörande adaptiva formulären. De färdiga adaptiva formulären har stöd för XFA-konstruktioner, till exempel valideringar, händelser, egenskaper och mönster.
   * **Formulärdatamodell**: Det är en standardformulärmodell om du vill integrera backend-system som databaser, webbtjänster och AEM användarprofil för att fylla i anpassade formulär i förväg och skriva in skickade formulärdata i backend-systemen. Med en redigerare för formulärdatamodell kan du definiera och konfigurera enheter och tjänster i en formulärdatamodell som du kan använda för att skapa adaptiva formulär. Mer information finns i [AEM Forms dataintegrering](/help/forms/using/data-integration.md).

Det är viktigt att du noga väljer den datamodell som inte bara passar dina behov utan också utökar dina befintliga investeringar i XFA- och XSD-resurser, om det finns några. Använd XSD-modellen för att skapa formulärmallar eftersom den genererade XML-filen innehåller data enligt XPATH som definieras av schemat. Att använda XSD-modell som standardval för formulärdatamodell är också till hjälp eftersom det frigör formulärdesignen från det bakomliggande system som bearbetar och förbrukar data och förbättrar formulärens prestanda på grund av en-till-en-mappning av formulärfält. Dessutom kan BindRef för fältet göras till XPATH för dess datavärde i XML.

Mer information finns i [Skapa ett anpassat formulär](/help/forms/using/creating-adaptive-form.md).

* Det finns några vanliga avsnitt i adaptiva formulär. Ni kan identifiera dem och definiera en strategi för att främja återanvändning av innehåll. Med adaptiva formulär kan du skapa fristående fragment och återanvända dem i olika formulär. Du kan också spara en panel i ett anpassat formulär som ett fragment. Alla ändringar i ett fragment återspeglas i alla associerade formulär. Det hjälper er att minska utvecklingstiden och säkerställa enhetlighet i alla formulär. Dessutom gör användningen av fragment att adaptiva formulär blir lätta, vilket ger en förbättrad redigeringsupplevelse, särskilt för stora formulär. Mer information finns i [Anpassningsbara formulärfragment](/help/forms/using/adaptive-form-fragments.md).

### Anpassa adaptiva formulär och komponenter {#customize-components}

* AEM Forms har färdiga anpassningsbara formulärmallar som du kan använda för att skapa anpassningsbara formulär. Du kan också skapa egna mallar. AEM innehåller statiska och redigerbara mallar.

   * Statiska mallar definieras och konfigureras av utvecklare.
   * Redigerbara mallar skapas av författare med hjälp av mallredigeraren. Med mallredigeraren kan du definiera en grundläggande struktur och ursprungligt innehåll i en mall. Alla ändringar i strukturlagret återspeglas i alla formulär som använder den mallen. Det ursprungliga innehållet kan innehålla förkonfigurerat tema, förifyllningstjänst, skicka-åtgärd och så vidare. Dessa inställningar kan dock ändras för ett formulär med formulärredigeraren. Mer information finns i [Adaptiva formulärmallar](/help/forms/using/template-editor.md).

* Om du vill formatera ett visst fält eller en viss panelinstans använder du [infogad formatering](/help/forms/using/inline-style-adaptive-forms.md). Du kan också definiera en klass i en CSS-fil och ange klassnamnet i komponentens CSS-klassegenskap.
* Inkludera ett klientbibliotek i en komponent för att konsekvent tillämpa format på adaptiva formulär eller fragment som använder den komponenten. Mer information finns i [Skapa en adaptiv komponent för formulärsidor](/help/forms/using/custom-adaptive-forms-templates.md).
* Använd format som har definierats i ett klientbibliotek för att välja adaptiva formulär genom att ange sökvägen till klientbiblioteket i fältet CSS-filsökväg i egenskaperna för den adaptiva formulärbehållaren.
* Om du vill skapa ett klientbibliotek med dina format kan du konfigurera den anpassade CSS-filen i Theme Editor-basklienten eller i egenskaperna för formulärbehållaren.
* Med adaptiva formulär kan du skapa panellayouter, som responsiva, tabbade, dragspel och guide, för att styra hur formulärkomponenter placeras ut på en panel. Du kan skapa anpassade panellayouter och göra dem tillgängliga för formulärförfattare. Mer information finns i [Skapa anpassade layoutkomponenter för anpassade formulär](/help/forms/using/custom-layout-components-forms.md).
* Du kan också anpassa specifika adaptiva formulärkomponenter som fält och panellayout.

   * Använd [Övertäckning](/help/sites-developing/overlays.md) AEM funktioner för att ändra en kopia av en komponent. Du bör inte ändra standardkomponenter.
   * Om du vill anpassa layouten för färdiga adaptiva formulärkomponenter i /libs, [skapa anpassade layoutkomponenter](/help/forms/using/custom-layout-components-forms.md) utöver [standardlayouter](/help/forms/using/layout-capabilities-adaptive-forms.md).
   * Lägg in anpassade interaktiva funktioner genom att skapa anpassade widgetar eller utseenden. Du bör inte ändra standardkomponenter. Mer information finns i [Utseenderamverk](/help/forms/using/introduction-widgets.md).

* Se [Hantera personligt identifierbar information](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p) för rekommendationer om hur PII-data ska hanteras.

### Skapa formulärmallar

Du kan skapa ett anpassat formulär med formulärmallarna som är aktiverade i **Konfigurationsläsaren**. Information om hur du aktiverar formulärmallarna finns i [Skapa anpassad formulärmall](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/creating-your-first-adaptive-form/create-adaptive-form-template.html?lang=en).

Formulärmallarna kan också laddas upp från adaptiva formulärpaket som skapats på en annan författardator. Formulärmallar är tillgängliga genom installation [aemforms-references-*-paket](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en). Några av de bästa metoderna som rekommenderas är:

* The **nosamplingContent** runmode rekommenderas endast för författaren och inte för publiceringsnoderna.
* Redigering av resurser som anpassningsbara formulär, teman, mallar eller molnkonfigurationer utförs endast via redigeringsnoder, som kan publiceras på de konfigurerade publiceringsnoderna.
Mer information finns i [Publicera och avpublicera formulär och dokument](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=en)
* Forms-tilläggspaket krävs för redigering och publicering för att dokumenttjänståtgärderna ska kunna hanteras. Det kan därför anses vara ett beroende.
Om du bara vill hämta Forms-relaterade exempelmallar, teman och DOR-paket kan du hämta dem från [aemforms-references-*-paket](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=en).

Mer information finns i de effektivaste strategierna i [Introduktion till utveckling av anpassningsbara formulär](/help/forms/using/introduction-forms-authoring.md).

## Skapa anpassningsbara formulär {#author-adaptive-forms}

### Använda pekoptimerat användargränssnitt för redigering {#using-touch-optimized-ui-for-authoring}

* Använd objektwebbläsaren i sidlisten för att snabbt komma åt fält som är djupa i formulärhierarkin. Du kan använda sökrutan för att söka efter objekt i formulär- eller objektträdet och navigera mellan olika objekt.
* Om du vill visa och redigera egenskaperna för en komponent i komponentwebbläsaren i sidofältet markerar du komponenten och klickar på ![cmppr-1](assets/cmppr-1.png). Du kan också dubbelklicka på en komponent om du vill visa dess egenskaper i egenskapsläsaren.
* Använd kortkommandon för att vidta snabba åtgärder i formulären. Se [AEM Forms-kortkommandon](/help/forms/using/keyboard-shortcuts.md).

* Adaptiva formulärkomponenter rekommenderas för användning endast i adaptiva formulärsidor. Komponenterna är beroende av sin överordnade hierarki. Använd dem därför inte på en AEM sida.

Se även komponentbeskrivningar och metodtips i [Introduktion till utveckling av anpassningsbara formulär](/help/forms/using/introduction-forms-authoring.md).

### Använda regler i anpassningsbara formulär {#using-rules-in-adaptive-forms}

AEM Forms erbjuder [regelredigerare](/help/forms/using/rule-editor.md) som gör att du kan skapa regler för att lägga till dynamiskt beteende i adaptiva formulärkomponenter. Med dessa regler kan du utvärdera villkor och utlösa åtgärder för komponenter, som att visa eller dölja fält, beräkna värden, ändra listrutan dynamiskt och så vidare.

Regelredigeraren innehåller en visuell redigerare och en kodredigerare för att skriva regler. Tänk på följande när du skriver regler i kodredigeringsläget:

* Använd meningsfulla och unika namn för formulärfält och komponenter för att undvika eventuella konflikter när du skriver regler.
* Använd `this` för en komponent att referera till sig själv i ett regeluttryck. Det ser till att regeln förblir giltig även om komponentnamnet ändras. Till exempel: `field1.valueCommit script: this.value > 10`.

* Använd komponentnamn när du refererar till andra formulärkomponenter. Använd `value` för att hämta värdet för ett fält eller en komponent. Till exempel: `field1.value`.

* Referera komponenter efter en relativ unik hierarki för att undvika konflikter. Till exempel: `parentName.fieldName`.

* När du hanterar komplexa eller ofta använda regler bör du överväga att skriva affärslogik som funktioner i ett separat klientbibliotek som du kan ange och återanvända i adaptiva formulär. Klientbiblioteket ska vara ett självständigt bibliotek och inte ha några externa beroenden, förutom jQuery och Underscore.js. Du kan också använda klientbiblioteket för att framtvinga [omvalidering på serversidan](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form) av inlämnade formulärdata.
* Adaptiva formulär innehåller en uppsättning API:er som du kan använda för att kommunicera med och utföra åtgärder på adaptiva formulär. Några av de viktigaste API:erna är följande. Mer information finns i [API-referens för JavaScript-bibliotek för Adaptiv Forms](https://adobe.com/go/learn_aemforms_documentation_63).

   * `guideBridge.reset()`: Återställer ett formulär.
   * `guideBridge.submit()`: Skickar ett formulär.
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`: Anger fokus till ett fält.
   * `guideBridge.validate(errorList, somExpression, focus)`: Validerar ett formulär.
   * `guideBridge.getDataXML(options)`: Hämtar formulärdata som XML.
   * `guideBridge.resolveNode(somExpression)`: Hämtar ett formulärobjekt.
   * `guideBridge.setProperty(somList, propertyName, valueList)`: Anger egenskapen för ett formulärobjekt.
   * Du kan dessutom använda följande fältegenskaper:

      * `field.value` om du vill ändra ett fälts värde.
      * `field.enabled` för att aktivera/inaktivera ett fält.
      * `field.visible` om du vill ändra synlighet för ett fält.

* Anpassa formulärförfattare kan behöva skriva JavaScript-kod för att skapa affärslogik i ett formulär. JavaScript är kraftfullt och effektivt, men det kan troligtvis påverka säkerheten. Därför måste du se till att formulärförfattaren är en betrodd person och det finns processer för att granska och godkänna JavaScript-koden innan ett formulär börjar användas. Administratören kan begränsa åtkomsten till regelredigeraren till användargrupper baserat på deras roll eller funktion. Se [Bevilja regelredigeraråtkomst för valda användargrupper](/help/forms/using/rule-editor-access-user-groups.md).
* Du kan använda uttryck i regler för att göra adaptiva formulär dynamiska. Alla uttryck är giltiga JavaScript-uttryck och använder API:er för adaptiva formulär. Dessa uttryck returnerar värden av vissa typer. Mer information om uttryck och metodtips kring dem finns i [Adaptiva formuläruttryck](/help/forms/using/adaptive-form-expressions.md).

* Adobe rekommenderar att du använder synkrona JavaScript-åtgärder över asynkrona när du skapar regler med Regelredigeraren. Asynkrona åtgärder bör inte användas. Om du befinner dig i en situation där asynkrona åtgärder inte kan undvikas är det viktigt att du implementerar JavaScript-stängningsfunktioner. På så sätt kan ni effektivt skydda er mot alla tänkbara konkurrensförhållanden och säkerställa att regelimplementeringarna ger optimala prestanda och upprätthåller stabilitet genom hela processen.

  Låt oss anta att vi behöver hämta data från ett externt API och sedan tillämpa några regler som baseras på dessa data. Vi använder en stängning för att hantera det asynkrona API-anropet och se till att reglerna tillämpas efter att data har hämtats. Här är exempelkoden:

  ```JavaScript
       function fetchDataFromAPI(apiEndpoint, callback) {
        // Simulate asynchronous API call with setTimeout
        setTimeout(() => {
          // Assuming the API call is successful, we receive some data
          const data = {
            someValue: 42,
          };
          // Invoke the callback with the fetched data
          callback(data);
        }, 2000); // Simulate a 2-second delay for the API call
      }
      // Rule implementation using Closure
      function ruleImplementation(apiEndpoint) {
        // Using a closure to handle the asynchronous API call and rule application
        // say you have set this value in street field inside address panel
        var streetField = address.street;
        fetchDataFromAPI(apiEndpoint, (data) => {
          streetField.value = data.someValue;
        });
      }
      // Example usage of the rule implementation
      const apiEndpoint = "https://example-api.com/data";
      ruleImplementation(apiEndpoint);
  ```

  I detta exempel `fetchDataFromAPI` simulerar ett asynkront API-anrop med `setTimeout`. När data har hämtats anropas den angivna callback-funktionen, som är stängningen för att hantera det efterföljande regelprogrammet. The `ruleImplementation` -funktionen innehåller regellogiken.


### Arbeta med teman {#working-with-themes}

Med anpassningsbara teman kan du skapa återanvändbara format som kan användas i olika formulär för enhetlig utformning och formatering. Använd teman för att definiera format för formulärkomponenter och paneler. Här följer några tips om teman:

* Använd resursbiblioteket för snabb användning av textformat, bakgrund och bilder. När ett format läggs till i resursbiblioteket är det tillgängligt för andra teman och i formredigerarens formatläge.
* Använd globala inställningar som teckensnitt och sidbakgrund med sidnivåväljaren.
* Använd klientbibliotek för att importera befintlig eller avancerad formatering till dina teman.
* Du kan åsidosätta formateringen för specifika fält, paneler eller knappar i ett formulärformatslager.
* Om ett tema inte uppfyller dina formatkrav kan du använda fördefinierade klasser som guideFieldNode, guideFieldLabel, guideFieldWidget och guidePanelNode för att använda samma format i alla formulär.

Mer information finns i [Teman](/help/forms/using/themes.md).

### Optimera prestanda för stora och komplexa formulär {#optimizing-performance-of-large-and-complex-forms}

Formulärförfattare och slutanvändare har oftast prestandaproblem när de läser in stora formulär i redigeringsläge eller vid körning. När antalet objekt (fält och paneler) i formuläret ökar försämras upplevelsen av redigering och körning. Det förhindrar också att flera författare samarbetar och skapar ett formulär samtidigt.

Använd följande metodtips för att lösa prestandaproblem med stora formulär:

* Vi rekommenderar att du skapar anpassningsbara formulär med XSD-formulärdatamodell, även när du konverterar en XFA till anpassat formulär, om det är möjligt.
* Inkludera endast de fält och paneler i anpassningsbara formulär som hämtar information från användaren. Tänk på att behålla statiskt innehåll så lite som möjligt eller använd URL:er för att öppna dem i ett separat fönster.
* Alla formulär har utformats för ett specifikt ändamål, men det finns några vanliga segment i de flesta formulär. Exempel: personuppgifter, adress, anställningsinformation osv. Skapa [adaptiva formulärfragment](/help/forms/using/adaptive-form-fragments.md) för gemensamma formulärelement och -avsnitt och använda dem i olika formulär. Du kan också spara en panel i ett befintligt formulär som ett fragment. Alla ändringar i ett fragment återspeglas i alla tillhörande adaptiva former. Det främjar samarbete när flera författare kan arbeta samtidigt i olika fragment som utgör ett formulär.

   * Precis som adaptiva formulär rekommenderar vi att alla fragmentspecifika format och anpassade skript definieras i klientbiblioteket med hjälp av dialogrutan fragmentbehållare. Försök också att skapa egna fragment som inte är beroende av objekt utanför den.
   * Undvik att använda korsfragmentsskript. Om det finns något objekt utanför fragmentet som du måste referera till, kan du försöka göra det objektet till en del av det överordnade formuläret. Om objektet fortfarande måste finnas i ett annat fragment refererar du till det med namnet i skriptet.

* Använd Spara och fortsätt med autosparande för att spara det anpassade formuläret regelbundet och göra det möjligt för användare att gå tillbaka senare för att fylla i formuläret.
* Konfigurera fragment för att läsa in lager. Vid körning återges fragment som markerats för att läsa in lager endast när de behövs. Det minskar inläsningstiden avsevärt för stora formulär. Den stöds även i fragment med repeterbara paneler. Mer information finns i [Konfigurera lazy loading](/help/forms/using/lazy-loading-adaptive-forms.md).

   * Konfigurera inte lazy loading på fragment i en responsiv rutnätslayout eller i den första panelen.
   * Komponenter för bifogade filer och villkor stöds inte i lagerinlästa fragment.
   * Markera ett värde i en lat inläst panel som Använd värdet globalt om det värdet används i någon annan del av formuläret, så att värdet är tillgängligt för användning när behållarpanelen tas bort.
   * Överväg att skriva synlighetsregler för fragment som ska visas eller döljas baserat på ett villkor.
* Ange värdet för **Antal samtal per begäran** i **Apache Sling Main Servlet** till ett ganska stort tal. Det gör att Forms-servern kan tillåta ytterligare samtal. Konfigurationen visar standardvärdet 1500. Värdet, 1 500 anrop, avser andra Experience Manager-komponenter som Sites and Assets. Standardvärdet för adaptiva formulär är 20000. Om du stöter på `too many calls` fel i loggar eller formuläret inte kan återges, försök att öka värdet till ett stort antal för att lösa problemet. Om antalet anrop överstiger 20000 innebär det att formuläret är komplext och det kan ta en stund att återge formuläret i webbläsaren. Det här händer bara första gången som formuläret läses in, efter att formuläret har cache-lagrats och när formuläret har cache-lagrats påverkas inte prestanda i någon större utsträckning.

### Förifyllning av anpassningsbara formulär {#prefilling-adaptive-forms}

Du kan förifylla anpassningsbara formulärfält med data som hämtats från backend-sidan för att hjälpa användarna att snabbt fylla i formuläret och undvika skrivfel.

* AEM Forms tillhandahåller en förifyllningstjänst för att läsa data från en fördefinierad XML-datafil och förifylla fälten i ett adaptivt formulär med innehållet i XML-filen för förifyllnad.
* XML-koden för förifyllda data måste vara kompatibel med schemat för den formulärmodell som är associerad med det adaptiva formuläret.
* Inkludera `afBoundedData` och `afUnBoundedData` för att fylla i både bundna och obundna fält i ett adaptivt formulär i förväg i XML.

* För anpassningsbara formulär baserade på formulärdatamodell tillhandahåller AEM Forms en färdig tjänst för förifyllning av formulärdatamodell. förifyllningstjänsten söker efter datakällor för datamodellobjekt i det adaptiva formuläret och fyller i fältvärden i förväg när formuläret återges.
* Du kan också använda de adaptiva formulären för förifyllnad av filer, krökningar, tjänster och http-protokoll.
* AEM Forms har stöd för anpassade förifyllningstjänster som du kan använda som en OSGi-tjänst för att förifylla adaptiva formulär.

Mer information finns i [Förifyll anpassningsbara formulärfält](/help/forms/using/prepopulate-adaptive-form-fields.md).

### Signera och skicka adaptiva formulär {#signing-and-submitting-adaptive-forms}

För adaptiva formulär krävs Skicka-åtgärder för att bearbeta användarspecificerade data. En Skicka-åtgärd avgör vilken uppgift som utförs på de data som du skickar med ett anpassat formulär.

* Det finns flera inskickningsåtgärder som är tillgängliga i anpassningsbara formulär. Mer information finns i [Konfigurera åtgärden Skicka](/help/forms/using/configuring-submit-actions.md).
* Du kan skriva en anpassad sändningsåtgärd om standardåtgärderna för att skicka inte uppfyller ditt användningssätt. Mer information finns i [Skriva anpassad skickaåtgärd för anpassningsbara formulär](/help/forms/using/custom-submit-action-form.md).
* Inkludera validering på serversidan för att förhindra att ogiltiga data skickas.

Du kan använda multisigneringsfunktionen i Adobe Sign i adaptiva formulär. Tänk på följande när du konfigurerar Adobe Sign i adaptiva formulär. Mer information finns i [Använda Adobe Sign i en adaptiv form](/help/forms/using/working-with-adobe-sign.md).

* Anpassningsbart formulär som aktiveras av Adobe Sign skickas endast när alla signerare har signerat formuläret. Forms visas i Väntande signering tills formuläret har signerats av alla signerare.
* Du kan konfigurera signeringsupplevelsen i ett formulär eller dirigera om signerare till en signeringssida när de skickas.
* Konfigurera sekventiell eller parallell signering efter behov.

### Genererar postdokument {#generating-document-of-record}

Ett urkunder är en förenklad PDF-version av ett adaptivt formulär som du kan skriva ut, signera eller arkivera.

* Beroende på vilken formulärdatamodell ett anpassat formulär baseras på kan du konfigurera en mall för DoR enligt följande:

   * **XFA-formulärmall**: Använd den associerade XDP-filen som DoR-mall.
   * **XSD-schema**: Använd den associerade XFA-mallen som använder samma XML-schema som det adaptiva formuläret.
   * **Ingen**: Använd autogenererad DoR.

* Konfigurera sidhuvud, sidfot, bilder, färg, teckensnitt och så vidare, direkt från fliken Dokument i den adaptiva formulärredigeraren.
* Använd `DoRService` för att generera DoR-koden programmatiskt.
* Uteslut dolda fält från DoR.
* Använd `afAcceptLang` begär parameter för att visa DoR i en annan språkinställning.

### Felsöka och testa anpassningsbara formulär {#debugging-and-testing-adaptive-forms}

[AEM Chrome Plug-in](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) är ett webbläsartillägg för Google Chrome som innehåller verktyg för felsökning av adaptiva formulär. Formulärförfattare och utvecklare kan använda dessa verktyg för att:

* Identifiera flaskhalsar och optimera formuläråtergivningens prestanda
* Felsöka nyckelord och bindRef-fel i formuläret
* Aktivera och konfigurera loggar
* Felsöka regler och skript i formuläret
* Utforska och lär dig mer om guideBridge API:er

Mer information finns i [AEM Chrome Plug-in - Adaptiv form](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/).

### Validerar anpassningsbara formulär på AEM server {#validating-adaptive-forms-on-aem-server}

Valideringar på serversidan krävs för att förhindra försök att kringgå valideringar på klienten och eventuella kompromisser med inskickade data och överträdelser av affärsregler. Valideringar på serversidan körs på servern genom att det nödvändiga klientbiblioteket läses in.

* Inkludera funktioner i ett klientbibliotek för att validera uttryck i adaptiva formulär och ange klientbiblioteket i dialogrutan för adaptiva formulärbehållare. Mer information finns i [Omvalidering på serversidan](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p).
* Validering på serversidan validerar formulärmodellen. Vi rekommenderar att du skapar ett separat klientbibliotek för validering och inte blandar det med andra saker som formatering av HTML och DOM-manipulering i samma klientbibliotek.

### Lokalisera anpassningsbara formulär {#localizing-adaptive-forms}

AEM tillhandahåller översättningsarbetsflöden som du kan använda för att lokalisera adaptiva formulär. Mer information finns i [Använda arbetsflöde AEM översättning för att lokalisera anpassningsbara formulär](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

Nedan beskrivs några tips om hur du översätter anpassningsbara formulär:

* Använd adaptiva formulärfragment för gemensamma element i olika formulär och lokalisera fragment. Det gör att du kan lokalisera ett fragment en gång och det återspeglas i alla former där det lokaliserade fragmentet används.
* Ändringar som att lägga till en ny komponent eller använda ett skript i ett lokaliserat formulär lokaliseras inte automatiskt. Därför måste du slutföra ett formulär innan du lokaliserar det för att undvika flera lokaliseringscykler.
* Använd `afAcceptLang` begär-parameter för att åsidosätta webbläsarens språkområde och återge formuläret i det angivna språkområdet. Följande URL måste till exempel återge formuläret på japanska, oavsett vilket språk som har angetts i webbläsarinställningen:

  `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* AEM Forms har för närvarande stöd för lokalisering av anpassningsbara formulärinnehåll på engelska (en), spanska (es), franska (fr), italienska (it), tyska (de), japanska (ja), portugisiska-brasilianska (pt-BR), kinesiska (zh-CN), kinesiska-taiwanesiska (zh-TW) och koreanska (ko-KR). Du kan dock lägga till stöd för nya språk för adaptiva formulär vid körning. Mer information finns i [Stöd för nya språk för lokalisering av adaptiva formulär](/help/forms/using/supporting-new-language-localization.md).

## Förbered formulärprojekt för produktion {#prepare-forms-project-for-production}

### Lägger till server för bearbetning av formulär {#adding-forms-processing-server}

Du kan konfigurera ytterligare en instans av AEM Forms-servern som finns bakom brandväggen i en skyddad zon. Du kan använda den här instansen för:

* **Gruppbearbetning**: jobb som är återkommande eller schemalagda i batchar med stor belastning. Du kan till exempel skriva ut programsatser, generera korrespondenser och använda dokumenttjänster som PDF Generator, Utdata och Assembler.
* **Lagra PII-data**: Spara PII-data på bearbetningsservern. Det är inte nödvändigt om du redan använder en anpassad lagringsleverantör för att lagra PII-data.

### Flyttar projekt till en annan miljö {#moving-project-to-another-environment}

Du behöver ofta flytta dina AEM projekt från en miljö till en annan. Några av de viktigaste saker man bör komma ihåg när man rör sig är följande:

* Säkerhetskopiera befintliga klientbibliotek, anpassad kod och konfigurationer.
* Distribuera produktpaket och korrigeringsfiler manuellt och i angiven ordning i den nya miljön.
* Distribuera projektspecifika kodpaket och paket manuellt och som ett separat paket eller paket på den nya AEM servern.
* (*Endast AEM Forms på JEE*) Distribuera LCA och DSC manuellt på Forms Workflow-servern.
* Använd [Export-Import](/help/forms/using/import-export-forms-templates.md) funktioner för att flytta resurser till den nya miljön. Du kan också konfigurera replikeringsagenten och publicera resurserna.
* När du uppgraderar ersätter du alla föråldrade API:er och funktioner med nya API:er och funktioner.

### Konfigurera AEM {#configuring-aem}

Nedan beskrivs några tips om hur du konfigurerar AEM för att förbättra prestanda generellt:

* Aktivera HTML-klientbibliotekskomprimering för JavaScript och CSS från Felix Console.
* Cachelagra alla klientbibliotek på `/etc.clientlibs/fd` och eventuella ytterligare anpassade klientbibliotek på AEM Dispatcher för att öka svarstiderna och säkerheten i de publicerade formulären. Mer information finns i [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html).

* Cachelagra inte `/content/forms/af/` och `/content/dam/formsanddocuments/*` banor. Mer information om hur du konfigurerar cachning för adaptiva formulär finns i [Cachelagra anpassningsbara formulär](/help/forms/using/configure-adaptive-forms-cache.md).

* Aktivera HTML via webbserverkomprimeringsmodulen. Mer information finns i [Prestandajustering av AEM Forms-server](/help/forms/using/performance-tuning-aem-forms.md).
* Öka antalet anrop per begäran för stora formulär. Se [Optimera prestanda för stora och komplexa formulär](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms).
* Skapa [anpassade felsidor som visas av felhanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html).
* Säker AEM Forms-server.

   * Använd `nosamplecontent` körningsläge för att säkerställa att det inte finns något exempelinnehåll och exempelanvändare distribuerade på produktionsservern. Se [Köra AEM i produktionsklart läge](/help/sites-administering/production-ready.md).

* Behåll stackstorleken till minst 8 GB. Andra inställningar finns i [Prestandajustering av AEM Forms-server](/help/forms/using/performance-tuning-aem-forms.md).
* Använd tjänstanvändarsessioner i stället för administratörssessioner för att köra uppgifter på tjänstnivå. Mer information finns i [Tjänstautentisering](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html).

>[!VIDEO](https://vimeo.com/)

### Konfigurera extern lagring för utkast och skickade formulärdata {#external-storage}

I en produktionsmiljö bör du inte lagra inskickade formulärdata i AEM. I standardimplementeringen av Forms Portal Store, Store Content och Store PDF används AEM att lagra formulärdata. De här Skicka-åtgärderna är endast avsedda för demonstrationssyften. Dessutom används portallagring som standard för funktionerna Spara, Återuppta och Spara automatiskt. Ta därför följande rekommendationer i beaktande:

* **Lagra utkastdata**: Om du använder funktionen Utkast i adaptiva formulär bör du implementera ett anpassat SPI-gränssnitt (Service Provide Interface) för att lagra utkastdata i en säkrare lagringsplats, som en databas. Mer information finns i [Exempel för att integrera komponent för utkast och inlämning med databas](/help/forms/using/integrate-draft-submission-database.md).

* **Lagra inskickningsdata**: Om du använder Form Portal Submit Store bör du implementera en anpassad SPI för att lagra data i en databas. Se [Exempel för att integrera komponent för utkast och inlämning med databas](/help/forms/using/integrate-draft-submission-database.md) för en exempelintegrering.

  Du kan också skriva en anpassad skicka-åtgärd som lagrar formulärdata och bifogade filer i säker lagring. Se [Skriva anpassad skickaåtgärd för anpassningsbara formulär](/help/forms/using/custom-submit-action-form.md) för mer information.

* **Utkast-ID:ts längd**: När du sparar ett anpassat formulär som ett utkast genereras ett utkast-ID som unikt identifierar utkastet. Minsta tillåtna värde för längden på utkastets ID-fält är 26 tecken. Adobe rekommenderar att du anger 26 eller fler tecken för utkast-ID:t.

### Hantera personligt identifierbar information {#handling-personally-identifiable-information}

En av de största utmaningarna för organisationer är att hantera personligt identifierbara data. Här följer några tips som kan hjälpa dig att hantera sådana data:

* Använd en säker, extern lagringsplats som databas för att lagra data från utkast och skickade formulär. Se [Konfigurera extern lagring för utkast och skickade formulärdata](/help/forms/using/adaptive-forms-best-practices.md#external-storage).
* Använd formulärkomponenten Villkor om du vill få uttryckligt medgivande från användaren innan du aktiverar automatiskt sparande. I det här fallet aktiverar du bara Spara automatiskt när användaren godkänner villkoren i villkorskomponenten.


