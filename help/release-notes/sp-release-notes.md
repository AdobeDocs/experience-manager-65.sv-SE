---
title: Versionsinformation om Adobe Experience Manager 6.5 Service Pack
description: Versionsinformation om Adobe Experience Manager 6.5 Service Pack 5.
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: ca965d8495c0460b2b6bc5e08d8818b91f9fcdee
workflow-type: tm+mt
source-wordcount: '4415'
ht-degree: 0%

---


# Versionsinformation om Adobe Experience Manager 6.5 Service Pack {#aem-service-pack-release-notes}

## Versionsinformation {#release-information}

| Produkter | Adobe Experience Manager 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.5.0 |
| Typ | Service Pack-version |
| Date | 4 juni 2020 |
| Hämta URL | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip) |

## Vad ingår i Adobe Experience Manager 6.5.5.0 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.5.0 är en viktig uppdatering som innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat samt prestanda, stabilitet och säkerhetsförbättringar som släppts sedan den allmänna tillgängligheten av 6.5-utgåvan i **april 2019**. Den kan installeras ovanpå Adobe Experience Manager 6.5.

Några viktiga funktioner och förbättringar i Adobe Experience Manager 6.5.5.0:

* Anpassa kolumnnamnen som visas i Adobe Experience Manager Inbox.

* Förbättrad tillgänglighet inom olika områden i Experience Manager Web Content Management (WCM), t.ex. sidredigeraren, kärnkomponenter, RTE och administratörsgränssnittet.

* Spara ett [!DNL Interactive Communication] utkast.

* Stöd [!DNL Oracle WebLogic 12] för Experience Manager Forms på JEE.

* Förbättrad undantagshantering i [!DNL Adobe Experience Manager Assets] användargränssnittets flöde.

* För att hämta publicerings-URL för Dynamic Media Scene7 `getRemoteAssetPublishURL` läggs en ny metod till i `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi` gränssnittet.

* [Tillgänglighetsförbättringar](#assets-6550) i enlighet [!DNL Adobe Experience Manager Assets] med Web Content Accessibility Guidelines (WCAG).

* Paketdelningsintegrering har tagits bort från Adobe Experience Manager.

* Den inbyggda databasen (Apache Jackrabbit Oak) uppdateras till version 1.2.3.

En fullständig lista över funktioner, viktiga högdagrar, viktiga funktioner som introducerades i Service Pack 5 för Experience Manager 6.5 finns i [Nyheter i Adobe Experience Manager 6.5 Service Pack 5](new-features-latest-service-pack.md) .

Nedan följer en lista över korrigeringar i version [!DNL Experience Manager] 6.5.5.0.

### [!DNL Sites] {#sites-6550}

* Med Experience Manager Sites kan du publicera eller avpublicera en sida från dess alias. Alternativet fungerar inte (NPR-33415).
* När en layoutbehållare tas bort från en mall som innehåller flera mallar återges inte mallen korrekt (NPR-33347).
* När en Experience Manager Sites-sida är en del av en stor innehållsuppsättning med flera live-kopior går det inte att läsa in förhandsgranskningen av sidversionshistoriken (NPR-33311).
* När du använder kommandot Flytta för att byta namn på en Experience Manager-platssida uppdateras inte sidtiteln (NPR-33264).
* När du flyttar sidor genom kolumnvyn försvinner kolumnerna (NPR-33216).
* När namnet på en lokal komponent i en språkkopia är identiskt med namnet på en komponent i utkastet och komponenten rullas ut från utkast, läggs termen inte till i namnet på den lokala komponenten (NPR-33208). `_msm_moved`
* Servern för sidomdirigering lägger till .html till en URL för Experience Manager-platser där ResourceType inte är `cq:Page` (NPR-33176).
* När du klistrar in ett underträd finns det inget alternativ för att bestämma om motsvarande undersidor ska klistras in eller inte (NPR-33149).
* Antalet resultat i direktanvändning av en komponent är begränsat till nummer 49 (NPR-33058).
* När du baserar ett innehållsfragment på ett schema och det innehåller ett obligatoriskt textområde eller ett sökvägsfält, kan innehållsfragmentet inte sparas (NPR-33007).
* När du skapar en anpassad komponent med hjälp av standardkomponenten för Experience Fragment och använder den på Experience Manager Sites-sidor, visar inte Experience Manager referenser (användning) för den anpassade komponenten (NPR-32852).
* När du byter namn på en mapp med ett stort antal referenser uppdateras inte många referenser till mappen (NPR-32765).
* När du aktiverar källredigeringsalternativet blir det tillgängligt för alternativ för helskärmsvisning, men saknas för redigeringsdialogruta och helskärmsalternativ i textredigeraren (NPR-32763).
* Om du har ett flerfält och det innehåller ett obligatoriskt fält (till exempel en listruta eller ett sökvägsfält) i sidegenskaperna för en plan, sparas inte sidegenskaperna för live-kopian när en sida som innehåller ett sådant flerfält öppnas (NPR-32751).
* Skärmläsare kan inte använda rubrikstrukturen för att navigera på en sida. Dessutom har fliken Komponenter fel etikett (NPR-32648).
* När sidnumreringen startar läses inte Experience Fragments Picker in alla objekt (NPR-32605).
* Författarbehörigheter för att läsa, ändra, skapa och ta bort live-kopior återkallas. Varje författare måste uttryckligen ange läs- och ändringsbehörigheter för att kunna flytta sidor i en utkast (NPR-32550).
* Innehållsförfattare kan inte skapa Launch för en sida som är integrerad med Adobe Analytics (NPR-32548).
* När en användare återupptar arv med synkronisering synkroniseras inte den överordnade sidans live-kopia med ritningen och visar en felaktig status (NPR-32500).
* Det tar mer än 15 sekunder att läsa in redigeringssidan för Experience Manager Sites (NPR-32413).
* I vissa fält visas inte alternativet Avbryt arv (NPR-32362).
* När du markerar en sökväg för en Experience Fragment-komponent och markerar kryssrutan Öppna dialogrutan Markering, navigeras du inte till den valda sökvägen i sökvägsläsaren (NPR-32308).
* När du uppgraderar från Experience Manager 6.2 till Experience Manager 6.5 visas inte Parsys-komponenten för statiska mallar korrekt. Parsys-komponentens höjd anges till 0 och komponenterna i den är inte synliga (NPR-33663).
* När en användare kopierar och klistrar in en layoutbehållare på samma sida visas inte komponenterna i en layoutbehållare (NPR-33648).
* Hälsokontrollen för utskickaren visar `Invalid cookie header` varningsmeddelandet i loggfilerna (NPR-33629).
* Speglad XSS i PreferencesServlet (NPR-33438).
* Anonyma användare har tillgång till CRX DE Lite-funktioner (GRANITE-27790).

### [!DNL Assets] {#assets-6550}

**Tillgänglighetsförbättringar i Experience Manager Assets**

* Nu går det att sätta tangentbordsfokus på [!UICONTROL Comments] listan och klickbara alternativ till [!UICONTROL Create] versionskommentarer under [!UICONTROL Create new version] i [!UICONTROL Timeline] resurspanelen (NPR-33424).

* Nu går det att nå [!UICONTROL View Settings] alternativ för resurser och ändra inställningar i [!UICONTROL View Settings] dialogrutan med hjälp av tangentbordstangenter (NPR-33420).

* Listrutans popup-meny för kombinationsrutan (i olika fält på olika sidor) visar nu poster som en lista med alternativ som kan tillkännages av skärmläsare (NPR-33516).

* Sorteringsfunktionerna för sorterbara rubriker (i listvyn, [!UICONTROL Timeline] vyn och [!UICONTROL Manage Publication] sidan) presenteras nu av skärmläsare och sorteringskontrollerna för kolumnrubriker är tillgängliga via tangentbordet (NPR-32979).

* Klickbara element som kommentarkort, versionsuppdateringar, kombinationsrutor och ikoner för menyerna kan nu fokuseras och interagera med tangentbordet (NPR-33514).

* Funktionaliteten (eller syftet med åtgärden) för insikter-ikoner (för användning, visningar och klickningar) på [!UICONTROL Insights View] presenteras nu korrekt av skärmläsare (NPR-33513).

* Skrivskyddade formulärfält (t.ex. inaktiverade fält på [!UICONTROL Basic tab] resurser [!UICONTROL Properties]) kan nu fokuseras med tangentbordet (NPR-33493, CQ-4273031).

* Etiketter i olika indatafält är nu permanenta etiketter (så att de är tillgängliga) och inte bara platshållaretiketter, som försvinner när texten skrivs (NPR-33475).

* Olika rubriknivåer (t.ex. sidrubriker och avsnittsrubriker) uppfattas nu som rubriker med olika nivåer för skärmläsaranvändare (NPR-33471).

* Interaktiva element i användargränssnittet, t.ex. länkar och alternativ (för rubrik- och zoomalternativ på tillgångssidan, mappnavigering), är nu tillgängliga via ett tangentbord (NPR-33468, CQ-4271412).

* Indikatorerna för [!UICONTROL Options], [!UICONTROL Scope]och [!UICONTROL Workflows] förlopp på [!UICONTROL Manage Publication] sidan läses nu ut korrekt av skärmläsare som förloppsindikatorer, i stället för som tabbar (NPR-33416).

* Färgen på stjärngraderingsikoner (t.ex. i [!UICONTROL Rating] avsnitt på [!UICONTROL Advanced] fliken i resursen [!UICONTROL Properties] eller i kortvyn) ändras så att lämplig kontrast blir synlig för användare med begränsad syn och utan att de uppfattar färg (NPR-33414).

* Du kan nu komma åt uppåtpilen för spolen bredvid [!UICONTROL Comment] fältet på sidan med tillgångsinformation med hjälp av tangentbordstangenter (NPR-33397).

* De utökade och komprimerade lägena i [!UICONTROL Tags] dialogrutan för navigering till resurser [!UICONTROL Properties] och vänster järnväg (i användargränssnittet för resurser) presenteras nu korrekt av skärmläsare (NPR-33396).

* Titlarna på alla bläddrade sidor på [!DNL Adobe Experience Manager] Assets är nu unika (NPR-33343).

* När du navigerar i trädstrukturen visas nu olika element i trädvykontrollen korrekt av skärmläsare (NPR-33304).

* Olika versioner av resurser i [!UICONTROL Timeline] vyn på sidan med tillgångsinformation är nu tillgängliga med tangentbordstangenter (NPR-33283).

* Namn på sökförslag som visas i kombinationsrutan Omnissearch meddelas nu av skärmläsare när sökfunktionen används (NPR-33280).

* Klickbara element och [!UICONTROL Go to link] i [!UICONTROL References rail] presenteras nu som klickbara element av skärmläsare (NPR-33278).

* Tabellstrukturinformation (t.ex. rad 1, cell 1, tabell) i dialogrutan visas inte längre av skärmläsare när dialogrutan öppnas (NPR-33268). [!UICONTROL Share Link]

* Syftet med olika kombinationsruteelement (t.ex. fältet Sökväg och alternativet att öppna dialogrutan Markering på fliken Grundläggande i resursegenskaper) har nu annonserats korrekt av skärmläsare (NPR-33235).

* Information om att raderna i listvytabellen kan markeras skickas nu till skärmläsaranvändare när tangentbordsfokus är på dem. När en pekare placeras på raderna visas informationen (NPR-33234).

* Alternativen ( [!UICONTROL x]att ta bort) för de markerade taggarna under [!UICONTROL Tags] fältet på fliken [!UICONTROL Basic] i [!UICONTROL Properties] är nu tillgängliga för skärmläsare (NPR-33206).

* Kalenderns datumväljare kan nu fokuseras och användas med tangentbordet av skärmläsaranvändare och synkade tangentbordsanvändare (NPR-33200).

* Växlingen mellan listvyn och kortvyn visar nu funktionen (vid justering av vyer) korrekt för skärmläsaren (NPR-33069).

* Menyn i den vänstra listen är nu tillgänglig. Funktionaliteten och syftet med att expandera menyn meddelas av skärmläsare (NPR-33068).

* Listrutan och många andra element i användargränssnittet är nu tillgängliga för användare med skärmläsare som inte är synliga, och följande information om dem presenteras av skärmläsare (NPR-33040):

   * om användarindata krävs för ett element innan formuläret skickas.
   * om ett element inte kan redigeras.
   * om en widget är markerad eller inte.

* Nu går det att öppna filtersidofältet med tangentbordet (NPR-32842, CQ-4273018).

* Kryssrutekontrollen i kolumnrubriken i listvyn är nu tillgänglig och syftet med att använda kontrollen presenteras av skärmläsare (NPR-32722, NPR-33005).

* Etiketter för timmar (HH) och minuter (mm) i kalenderdatumväljaren är nu permanenta etiketter i stället för platshållaretiketter, och försvinner inte när användaren skriver text i dessa fält (NPR-32720).

* Länktexten i meddelanden (som visas när du har klickat på klockikonen) visas nu för skärmläsaranvändare som använder tabb för att komma åt varje länk (NPR-32645).

* [!UICONTROL Select], [!UICONTROL Download], [!UICONTROL Properties]och [!UICONTROL More Actions] alternativ på tillgångskort i [!UICONTROL Insights View] är nu tillgängliga via tangentbordet (NPR-32609).

* Visuellt dolt innehåll (t.ex. innehåll i sidhuvudsmenyraden i sökresultat) annonseras inte längre av skärmläsare när de öppnas med tangentbordet (NPR-32606).

* Ändamålet med etiketterna på kontroller för att gå över till nästa och föregående månad i datumväljaren presenteras nu av skärmläsare (NPR-32604).

* Stjärngraderingsikoner kan nu fokuseras och användas med tangentbordstangenter (NPR-32513).

* Funktioner för att styra videovolymen är nu tillgängliga via tabb (för att fokusera på volymreglaget) och piltangenter (för att justera volymen) på tangentbordet (NPR-32065).

* Syftet med indatafält med nedre gräns ([!UICONTROL From]) och övre gräns ([!UICONTROL To]) för filstorleksfiltret har nu annonserats för användare med skärmläsare som inte är synkade (NPR-32064).

* Menyn [!UICONTROL Languages] i [!UICONTROL Create and Translate] formuläret är nu tillgänglig för skärmläsare i bläddringsläge (CQ-4293906).

* Panelen är nu tillgänglig med följande förbättringar (NPR-33261, CQ-4293798): [!UICONTROL References]

   * I bläddringsläge flyttas inte längre skärmläsarens fokus till dolda redigeringsfält med flera rader under [!UICONTROL Site References], [!UICONTROL Asset References], [!UICONTROL Copies]och [!UICONTROL Form References] avsnitt.

   * Skärmläsare presenterar nu rollen för [!UICONTROL Site References] och [!UICONTROL Language Copies] element.

   * Skärmläsarnas fokus i bläddringsläge ändras i en meningsfull sekvens till olika element.

* [!UICONTROL Metadata Schema Editor] sidan och dess element är nu tillgängliga via tangentbordet och är skärmläsarvänliga (CQ-4290962, CQ-4272953).

* Symbolens syfte att ta bort de markerade taggarna visas nu av skärmläsare tillsammans med antalet markerade taggar (CQ-4273017). `X`

* För att undvika förvirring för användare som inte är synkade med skärmläsare ignoreras nu dekorativa ikoner och bilder av skärmläsare (CQ-4272944).

**Problem som har korrigerats i Experience Manager Assets**

[!DNL Adobe Experience Manager] 6.5.5.0 Resurser innehåller korrigeringar av följande:

* [!UICONTROL Start] i dialogrutan för resurser i en samling är inaktiverat, vilket förhindrar att arbetsflödet aktiveras (NPR-32471). [!UICONTROL Create Workflow]

* När du använder överlappande popup-fönster i metadatamatcheringar försvinner det valda alternativet för apostrof när du väljer och sparar ett nedrullningsbart alternativ som innehåller en apostrof (från den underordnade listrutan) efter att resursen öppnats [!UICONTROL Properties] (NPR-32649).

* [!UICONTROL Asset Insights Sync Job] stoppar och misslyckas om ogiltiga poster påträffas (på analyssidan) i stället för att nästa post (NPR-32674) flyttas.

* Gyroscope fungerar inte eftersom rörelsesensorerna är inaktiverade som standard i mobilwebbläsare i panoramavisare (CQ-4272937).

* [!UICONTROL Connected Assets Configuration] guide fungerar inte med 404-fel vid installation av 6.5.3 i 6.5.1 (NPR-32730).

* Under XMP tillbakaskrivning ändrar alla anpassade namnutrymmesmetadataegenskaper det anpassade namnområdesprefixet till ns2 i motsats till det namnområdesprefix som har konfigurerats (NPR-32748).

* Lazy-inläsning aktiveras inte och endast 100 resurser visas när du väljer att granska uppgifter från meddelandeinkorgen (NPR-32750).

* `NullPointerException` observeras på grund av att nodinställningar saknas i den nyligen skapade användarprofilen (SAML/SSO). Detta fel förhindrar att nyinloggade användare använder [!DNL Adobe Experience Manager Stock] integrering (NPR-32777).

* Traversal-varningar observeras i loggar när en smart samling som innehåller mer än 10 000 resurser öppnas (NPR-32980).

* Resursnamn ändras till gemener när du flyttar resurser från en mapp till en annan i [!DNL Adobe Experience Manager] läget Dynamic Media Scene7 (NPR-32995).

* Det går inte att ta bort en sökresurs efter att ha navigerat till dess egenskaper från sökresultaten och sedan gå tillbaka till sökresultaten för att ta bort den (NPR-32998).

* [!UICONTROL Next] alternativet förblir inaktiverat när målmappen väljs i [!UICONTROL Move Assets] gränssnittet (NPR-33356).

* [!UICONTROL Next] är inte aktiverat när du väljer överordnad nod (där en underordnad mapp är synlig) och sedan väljer underordnad mapp (NPR-33275).

* Inchecknings- och utcheckningsbehörigheter är inaktiverade på Adobe Asset Link (AAL) för användare med borttagningsbehörighet, även om andra behörigheter som läsning, skapande eller ändring beviljas (NPR-33272).

* Smart Crop-renderingar är inte tillgängliga i dialogrutan för hämtning av resurser (NPR-33167).

* Undantag observeras i loggar vid öppning av renderingsspår för en PDF-fil i en mapp med en smart beskärningsprofil (CQ-4294201).

* Bildförinställningar publiceras inte om [!UICONTROL Dynamic Media sync mode] är inaktiverat som standard i Experience Manager med Scene7-körningsläget Dynamic Media (CQ-4294200).

* Resursbearbetning när massöverföring fastnar och arbetsflödesinstansen visar fasta instanser av DAM-uppdateringsresurs (CQ-4293916).

* Det går att skapa en dynamisk mediekonfiguration i Experience Manager, men i användargränssnittet händer inget när du väljer Spara (CQ-4292442).

* Förhandsgranskning av F4V-videomaterial fungerar inte i progressiv uppspelning på Safari/Mac (CQ-4289844).

* En extra mapp skapas vid smart beskärning av en resurs som finns i en överordnad mapp med ett punkttecken i namnet (CQ-4289337). `.`

* Miniatyrbilden är trasig och videobearbetningsbanderollen visas inte när en video kopieras (CQ-4284125).

* Dimensionella visningsprogram visar felaktigt tomma miniatyrbilder i Firefox för vissa modeller med tomma kameravinklar (CQ-4283447).

* Prestandaproblem som åtgärdas i 6.5.5.0 är (CQ-4279206):

   * Det tar för lång tid att överföra stora binära filer till servrar för bildbearbetning i dynamiska media.

   * Genereringstiden för miniatyrbilder på Experience Manager ökar på grund av Scene7-arkitekturen för dynamiska media.

* Dynamic Media Scene7 migreringsproblem misslyckas för kunder med ett stort antal mediefiler (CQ-4279206).

* Layouten i visningsprogrammet för video 360 bryts om `setVideo` används, och videon ändras när den används `video= modifier` (CQ-4263201).

* Ett felmeddelande visas när Experience Manager SDL-paketet (NPR-33175) installeras.

* SSRF-sårbarhet i Experience Manager (NPR-33435).

### Platform {#platform-6550}

* Filtret anropas inte om [!DNL Sling] mappningsposten skapas under `sling:match` `/etc/maps` (NPR-33362).
* Experience Manager kraschar på grund av segmenteringsfel med [!DNL Apache Lucene] (NPR-32988).
* [!DNL Jackson] kärnpaket saknas i filen Experience Manager uberjar (NPR-32848).
* CRXDE Lite läser inte in innehåll för användare utan läsbehörighet för en nods egenskap (NPR-32611). `jcr:primaryType`
* [!DNL Granite] Schemaläggaren för underhållsaktiviteter initieras om för ofta under distributioner av Experience Manager (CQ-4294627).
* När en SQL-fråga körs länge, till exempel 7 timmar, slutar Experience Manager svara (NPR-33044).

### Användargränssnitt {#ui-6550}

* Alternativknappsmarkeringen finns inte kvar i ett multifält (NPR-33309).
* Lazy-inläsningsgränsen fungerar inte för listvyn (NPR-33124).
* Sidan med omsökningsresultat visar inget meddelande om det inte finns några matchningar (NPR-32974).
* Omsökningsfiltret returnerar alla matchningar under `/content` noden som ignorerar den valda platsen (NPR-32849).

### Integreringar {#integrations-6550}

* Intern cache rensas när en sida med en Adobe Target-komponent publiceras (NPR-33162).
* Integrering med Adobe Target fungerar inte på [!DNL Windows Internet Explorer] 11 (NPR-33111).
* När du konfigurerar Adobe Target visas inte fälten [!UICONTROL Company] och [!UICONTROL Report Suite] när du väljer en rapportkälla (NPR-32502).
* När du exporterar [!DNL Experience Fragments] med Adobe I/O exporteras inte metadata som Source Product till Adobe Target (NPR-32159).
* Auktoriserade IMS-användare i den lokala Experience Manager-administratörsgruppen kan inte skapa eller ändra IMS-konfigurationer (NPR-33045).
* Konfigurationssidan för Adobe Launch visar inte alla poster (NPR-33011).
* Användare i gruppen content-authors kan inte redigera egenskaper för en Adobe Target-komponent på grund av ett JavaScript-fel (NPR-32996).
* Serveröverskridande skriptning för JSON (NPR-32744).

### Översättningsprojekt {#translation-6550}

* Översatta taggar importeras inte till Experience Manager från översättningstjänster från tredje part (NPR-33154).
* Översättningskonfigurationssidan visar en felaktig översättningsprovider än den som används för översättningen (NPR-32971).
* Om du lägger till en upplevelsefragmentmapp i ett befintligt översättningsprojekt skapas ett nytt projekt (NPR-32843).
* Ett `NullPointerException` fel visas i loggarna när ett översättningsjobb körs (NPR-32628).

### WCM {#wcm-6550}

* Page Editor - [!DNL Sites] Page Editor tillåter inte att användare med endast tangentbord hoppar över huvudinnehållet i stället för att växla tabbfokus mellan alla alternativ som är tillgängliga i sidhuvudet (CQ-4293883).
* Page Editor - Paneler som använder Well-komponenten och inkluderar sparade data visas inte på grund av uppdateringar i [!DNL Chrome] - och [!DNL Firefox] -versioner (CQ-4292995).
* MSM - Om du tar bort en komponent från sidan tas inte komponenten bort från den publicerade versionen av sidan (CQ-4292360).

### [!DNL Brand Portal] {#assets-brand-portal-6550}

* Om du tar bort ett publicerat metadataschema från [!DNL Brand Portal] skapas ett fel (CQ-4292063).
* Om en administratör konfigurerar [!DNL Experience Manager Assets] 6.5.4 med varumärkesportalen via Adobe Developer Console kan [!DNL Brand Portal] användaren inte publicera en resurs i en mapp från [!DNL Brand Portal] till [!DNL Experience Manager] (NPR-33046).
* Duplicerad replikering av de överordnade mapparna som orsakar konflikter (NPR-33001).

### [!DNL Communities] {#communities-6550}

* Det går inte att ta bort ett kort i en moderationskonsol med hjälp av snabbredigeringsmenyalternativet (NPR-33117).
* Ett fel inträffar vid åtkomst till [!UICONTROL Activity Stream] sidan (NPR-33146).
* Grupper som tas bort från författarinstansen tas inte bort från alla publiceringsinstanser (NPR-33199).
* Författare som har skapat en ny grupp omdirigeras inte till avsnittet [!UICONTROL Community Group] i [!DNL Internet Explorer] 11 (NPR-33205).
* Om du öppnar ett meddelande i Inkorgen i Experience Manager ändras inte meddelandets status till Läs (NPR-32764).
* När du redigerar en [!DNL Communities] grupp och ändrar miniatyrbilden uppdateras inte gruppens miniatyrbild (NPR-32599).
* En användare kan inte skicka ett e-postmeddelande till en annan användare i en community (NPR-32598).
* En skickad blogg visas inte förrän användaren uppdaterar sidan (NPR-32391).
* När du skapar en version av meddelanden och prenumerationer på användargenererat innehåll (UGC) lagras ett felaktigt ID för källsidan (CQ-4279355, CQ-4289703).
* Serveröverskridande skriptproblem (NPR-33203).

### Arbetsflöde {#workflow-6550}

* Alternativet [!UICONTROL Timeline] i den vänstra listen tar längre tid att ladda än förväntat (NPR-32851).
* När du har startat om en Experience Manager-instans innehåller e-postmeddelandet för granskningsaktiviteten för en samling en felaktig nyttolastlänk (NPR-32774).

### [!DNL Forms] {#forms-6550}

>[!NOTE]
>
>Experience Manager Service Pack innehåller inga korrigeringar för [!DNL Forms]. De levereras med ett separat Forms-tilläggspaket. Dessutom släpps ett kumulativt installationsprogram med korrigeringar för AEM Forms på JEE. Mer information finns i [Installera AEM Forms-tillägg](#install-aem-forms-add-on-package) och [Installera AEM Forms på JEE](#install-aem-forms-jee-installer).

* Korrespondenshantering: Ordningen på tillgångarna i ett målområde blandas efter att en skrivelse har lämnats in (NPR-33359, NPR-33153).
* Adaptiv Forms: När en användare redigerar ett anpassat formulär fungerar inte det [!UICONTROL Start Workflow] alternativ som finns på [!UICONTROL Page Information] menyn (NPR-33004).
* Adaptiv Forms: Användaren kan inte spara ett anpassat formulär med mer än en bifogad fil (NPR-32997).
* Adaptiv Forms: Om du ändrar panellayouten i ett adaptivt formulär uppstår ett fel (CQ-4293880).
* Adaptiv Forms: En ny rad i en sträng i en ordlista med adaptiva formulär lägger till `&#xa;` tecken i ordlistan (NPR-33266).
* Adaptiv tillgänglighet för Forms: När en användare förhandsgranskar ett anpassat formulär som ett HTML-formulär kan [!UICONTROL Scribble Signature] fältet inte behålla tabbfokus (NPR-33159).
* Adaptiv tillgänglighet för Forms: Felmeddelandena som visas när ett anpassat formulär skickas länkar inte till ett `aria-describedBy` -attribut (NPR-33071).
* Adaptiv tillgänglighet för Forms: Fält som markerats som obligatoriska i en adaptiv form har inte det obligatoriska attributet inställt på True i ARIA-hjälpmedelsschemat (NPR-33070).
* PDFG-tjänst: När en användare konverterar en textfil till en PDF-fil återges inte japanska tecken korrekt (NPR-33238).
* PDFG-tjänst: `CreatePDF` kan inte konvertera en PDF-fil till PDF OCR-format (NPR-32994).
* PDFG-tjänst: PDF-konverteringen misslyckas för den 200:e instansen av ett [!DNL OpenOffice] dokument (NPR-32766).
* BackendIntegration: Begäranden från formulärdatamodellen misslyckas eftersom uppdateringstoken förfaller på grund av ett inaktivt tillstånd (NPR-33169).
* Designer: Skärmläsare kör tabbordningen baserat på den geografiska standardordningen i stället för den anpassade tabbordningen som definieras i XDP-filen (NPR-32160).
* Designer: Om taggningsalternativet är aktiverat försvinner delformulärsramen i den genererade PDF-utdatafilen (NPR-32778).
* Lagrade XSS med GuideSOMProviderServlet (NPR-32700).

## Installera 6.5.5.0 {#install}

**Installationskrav**

* AEM 6.5.5.0 kräver AEM 6.5. Mer information finns i [uppgraderingsdokumentationen](/help/sites-deploying/upgrade.md) .
* Nedladdningen av Service Pack finns på Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* Installera AEM 6.5.5.0 på en av Author-instanserna med Package Manager på en distribution med MongoDB och flera instanser.
* Ta en ögonblicksbild eller en ny säkerhetskopia av AEM innan du installerar.
* Starta om instansen innan du installerar den. Detta behövs bara när instansen fortfarande är i uppdateringsläge (och detta är fallet när instansen uppdaterades från en tidigare version), men vi rekommenderar att instansen körs under en längre period.

>[!NOTE]
>
>Adobe rekommenderar inte att du tar bort eller avinstallerar Adobe Experience Manager 6.5.5.0-paketet.

### Installera Service Pack {#install-service-pack}

Så här installerar du Service Pack på en befintlig Adobe Experience Manager 6.5-instans:

1. Hämta Service Pack från [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip).

1. Öppna Pakethanteraren och klicka på **[!UICONTROL Upload Package]** för att överföra paketet. Mer information om hur du använder paketet finns i [Pakethanteraren](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html).

1. Markera paketet och klicka på **[!UICONTROL Install]**.

>[!NOTE]
>
>Dialogrutan för pakethanterarens gränssnitt avslutas ibland när Service Pack installeras. Adobe rekommenderar att du väntar på att felloggarna ska stabiliseras innan du får åtkomst till distributionen. Vänta på de specifika loggarna för avinstallationen av uppdateringspaketet innan du försäkrar dig om att installationen lyckas. Vanligtvis händer detta på [!DNL Safari] men kan inträffa i alla webbläsare.

**Automatisk installation**

Det finns två sätt att installera Adobe Experience Manager 6.5.5.0 automatiskt på en fungerande instans:

S. Placera paketet i en `../crx-quickstart/install` mapp när servern är tillgänglig online. Paketet installeras automatiskt.

B. Använd [HTTP API från Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html). Använd `cmd=install&recursive=true` så att kapslade paket installeras.

>[!NOTE]
>
>Adobe Experience Manager 6.5.5.0 stöder inte installation av Bootstrap.

**Validera installation**

1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience Manager (6.5.5.0)` under [!UICONTROL Installed Products].

1. Alla OSGi-paket finns antingen **[!UICONTROL ACTIVE]** eller **[!UICONTROL FRAGMENT]** i OSGi Console (Använd webbkonsol: `/system/console/bundles`).

1. OSGI-paketet `org.apache.jackrabbit.oak-core` är version 1.2.2.3 eller senare (Använd webbkonsol: `/system/console/bundles`).

Om du vill veta vilka plattformar som är certifierade för att fungera med den här versionen läser du de [tekniska kraven](/help/sites-deploying/technical-requirements.md).

### Installera Adobe Experience Manager Forms tilläggspaket {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Hoppa över om du inte använder AEM Forms. Korrigeringar i Adobe Experience Manager Forms levereras via ett separat tilläggspaket.

1. Kontrollera att du har installerat Adobe Experience Manager Service Pack.
1. Ladda ned motsvarande tilläggspaket från Forms som finns i [AEM Forms-utgåvor](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) för ditt operativsystem.
1. Installera Forms tilläggspaket enligt beskrivningen i [Installera AEM Forms tilläggspaket](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Installera Adobe Experience Manager Forms i JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Hoppa över om du inte använder AEM Forms på JEE. Korrigeringar i Adobe Experience Manager Forms på JEE levereras via ett separat installationsprogram.

Information om hur du installerar det kumulativa installationsprogrammet för Experience Manager Forms på JEE och konfigurationen efter distributionen finns i [versionsinformationen för korrigering 0014](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0014.html).

### UberJar {#uber-jar}

UberJar för Experience Manager 6.5.5.0 finns i [Adobe Public Maven-databasen](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.5/).

Om du vill använda UberJar i ett Maven-projekt ska du läsa [hur du använder UberJar](/help/sites-developing/ht-projects-maven.md) och inkludera följande beroende i projektstrukturen:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.5</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## Deprecated features {#removed-deprecated-features}

I det här avsnittet visas funktioner som har markerats som borttagna i AEM 6.5.5.0. Funktioner som ska tas bort i en framtida version är först inaktuella, med ett alternativt alternativ att använda.

Kunderna rekommenderas att granska om de använder funktionen eller funktionen i den aktuella distributionen och planera för att ändra implementeringen så att den använder det alternativa alternativet.

| Yta | Funktion | Ersättning |
|---|---|---|
| Integreringar | Skärmen är föråldrad **[!UICONTROL AEM Cloud Services Opt-In]** . Med integreringen av AEM och Target uppdaterades i AEM 6.5 för att stödja Target Standard API, som använder autentisering via Adobe IMS och I/O, och den växande rollen hos Adobe Launch för att instrumentera AEM sidor för analys och personalisering, har guiden för att välja In blivit funktionellt irrelevant. | Konfigurera systemanslutningar, Adobe IMS-autentisering och Adobe I/O-integreringar via respektive AEM-molntjänster. |
| Anslutningar | Adobe JCR Connector för Microsoft SharePoint 2010 och Microsoft SharePoint 2013 är borttagen för AEM 6.5. | Ej tillämpligt |

## Known issues {#known-issues}

* Om du installerar [!DNL Experience Manager] 6.5.5.0 med [!DNL Java] 11 startar du om servern när du har installerat Service Pack. Du behöver inte starta om om du installerar Service Pack med [!DNL Java] 8.

* Om en mapp i hierarkin byter namn i [!DNL Experience Manager Assets] och den kapslade mappen som innehåller en resurs publiceras [!DNL Brand Portal]i, uppdateras inte mappens rubrik [!DNL Brand Portal] förrän rotmappen publiceras igen.

* När AEM 6.5.5.0 installeras orsakar en uppdatering av [!DNL Chrome] version 83 ett problem när paket byggs. Lös problemet genom att använda andra tillgängliga webbläsare, till exempel [!DNL Internet Explorer] och [!DNL Firefox]eller andra AEM standardalternativ för paketinstallation. Problemet åtgärdas efter installation av AEM 6.5.5.0.

* Det går inte att skicka ett e-postmeddelande till SMTP-fjärrservern med AEM standardavsändare, eftersom det bara tillåter kommunikation med TLS v1.2. Ta bort paketet `javax.mail:mail:1.5.0-b01` från `system/console` och uppdatera paketen för att lösa problemet.

* När en användare väljer att konfigurera ett fält för första gången i ett adaptivt formulär visas inte alternativet att spara en konfiguration i egenskapsläsaren. Om du väljer att konfigurera ett annat fält i det adaptiva formuläret i samma redigerare åtgärdas problemet.

* Om [!UICONTROL Connected assets configuration] guiden returnerar ett 404-felmeddelande efter installationen måste du installera om `cq-remotedam-client-ui-content` - och `cq-remotedam-client-ui-components` -paketen manuellt med hjälp av pakethanteraren.

* Följande fel och varningsmeddelanden kan visas under installationen av AEM 6.5.x.x:
   * &quot;När Target-integrationen har konfigurerats i AEM med Target Standard API (IMS-autentisering) skapas felaktiga erbjudandetyper när Experience Fragments exporteras till Target. I stället för att skriva&quot;Experience Fragment&quot;/källa&quot;Adobe Experience Manager&quot; skapar Target flera erbjudanden med typen&quot;HTML&quot;/källa&quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Validering på serversidan av adaptiva formulär misslyckas när sammanställningsfunktioner som SUM, MAX och MIN används. CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Aktiveringspunkten i en interaktiv bild i Dynamic Media är inte synlig när du förhandsgranskar resursen via visningsprogrammet för den köpbara kanalen.

## OSGi-paket och innehållspaket som ingår {#osgi-bundles-and-content-packages-included}

Följande textdokument innehåller en lista över de OSGi-paket och innehållspaket som ingår i AEM 6.5.5.0:

* [Förteckning över OSGi-paket som ingår i AEM 6.5.5.0](assets/6550_bundles.txt)

* [Förteckning över innehållspaket som ingår i AEM 6.5.5.0](assets/6550_packages.txt)

## Begränsade platser {#restricted-sites}

Dessa webbplatser är bara tillgängliga för kunder. Om du är kund och behöver åtkomst kontaktar du din kontoansvarige på Adobe.

* [Nedladdning av produkt på licensing.adobe.com](https://licensing.adobe.com/)
* [Kontakta kundsupport](https://docs.adobe.com/content/help/en/customer-one/using/home.html)Mer information om hur du går till supportportalen finns i [Gå till supportportalen](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html).

>[!MORELIKETHIS]
>
>* [Versionsinformation för AEM 6.5](/help/release-notes/release-notes.md)
>* [AEM produktsida](https://www.adobe.com/marketing/experience-manager.html)
>* [AEM 6.5-dokumentation](https://helpx.adobe.com/support/experience-manager/6-5.html)
>* Prenumerera på produktuppdateringar med [Adobe prioritet](https://www.adobe.com/subscription/priority-product-update.html)

