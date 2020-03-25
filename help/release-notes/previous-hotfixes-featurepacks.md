---
title: AEM 6.5 Previous Service Pack Release Notes
description: Versionsinformation om Adobe Experience Manager 6.5 Service Pack 3 och tidigare.
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
translation-type: tm+mt
source-git-commit: 7345d629aa628c2e2e094a8194d9306d7c3d2d60

---


# Programfixar och funktionspaket som ingår i tidigare servicepaket {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## AEM 6.5.3.0

Adobe Experience Manager 6.5.3.0 är en viktig version som innehåller prestanda, stabilitet, säkerhet och viktiga kundkorrigeringar och förbättringar som släppts sedan den allmänna tillgängligheten av version 6.5 i **april 2019**. Den kan installeras ovanpå Adobe Experience Manager (AEM) 6.5.

Några viktiga höjdpunkter i den här Service Pack-versionen är:

* Den inbyggda databasen (Apache Jackrabbit Oak) uppdateras till version 1.10.6.

* Adobe Experience Manager Assets har nu stöd för ZIP-arkiv som skapats med algoritmen Deflate64.

* Ny kolumn för skapat datum, som är sorterbar, har lagts till i DAM-listvyn och i resurssökningsresultat i listvyn.

* Resurssortering baserad på namnkolumnen har aktiverats i listvyn.

* Dynamic Media har nu stöd för videomaterial för Smart Crop. Smart Crop är en maskininlärningsdriven funktion som återbeskär en video medan bildrutan flyttas för att följa scenens fokuspunkt.

* Dynamic Media har stöd för Smart Imaging.

* Möjlighet att [ange inställningar för frånvaro](../forms/using/configure-out-of-office-settings.md) i AEM-arbetsflöden.

* Möjlighet att [dela inkorgs- eller inkorgsobjekt](../forms/using/configure-shared-queues-osgi.md) med andra användare i AEM-arbetsflöden.

* Möjlighet att [generera interaktiv kommunikation i batchläge](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

* Uppdaterad version av jQuery som paketerats i ContextHub till 3.4.1.

### Assets {#assets-6530-enhancements}

**Produktförbättringar**

* Experience Manager Assets har nu stöd för ZIP-arkiv som skapats med algoritmen Deflate 64 (NPR-27573).

* Ny kolumn för skapat datum, som är sorterbar, har lagts till i DAM-listvyn och i resurssökningsresultat i listvyn (NPR-31312).

* Resurssortering baserat på namnkolumnen är tillåtet i listvyn (NPR-31299).

* Resursfilerna GLB, GLTF, OBJ och STL har stöd för förhandsgranskning av resurser på sidan Resursinformation i DAM (CQ-4282277).

* ReplicationOnModifyListener-händelsen utlöses för segmentnoder under segmentöverföring i Dynamic Media (CQ-4281279).

* Dynamic Media har nu stöd för videomaterial för Smart Crop. Smart Crop är en maskininlärningsdriven funktion som återbeskär en video samtidigt som bildrutan flyttas för att följa scenens fokuspunkt (CQ-4278995).

* Dynamic Media stöder Smart Imaging (CQ-422249).

* Vyn Sök/bläddra har angetts som standardvy i Foundation-väljaren om frågeparametrar skickas i begäran (NPR-31601).

**Korrigeringar**

* Metadata för vissa PDF-dokument uppdateras inte och sparas i PDF-filen när titeln ändras (NPR-31629).

* Resursdelning fungerar inte för resurser som har plustecknet + i sina namn (NPR-31547).

* Redigeringar i standardsökformuläret Resurser Admin * Search Rail fungerar inte som förväntat (NPR-31502).

* Förslag visas inte när du använder Omnissearch on assets view för att söka efter resurser (NPR-31496).

* Resursreferenser i samlingar uppdateras inte när de refererade resurserna flyttas till en annan plats, om samma resurser refereras till av olika samlingar av olika användare (NPR-31486).

* Duplicerade IPTC-taggar läggs till i metadata för resurser (NPR-31328).

* Antalet sökresultat i det övre högra hörnet uppdateras inte korrekt när sökningen utlöses från filterfältet (NPR-31316).

* Alla kryssrutor är avmarkerade när kryssrutorna på den andra nivån avmarkeras i filtypsfiltret, och texten i sökfältet är inte synkroniserad med de valda/omarkerade egenskaperna (NPR-31287).

* Det går inte att ta bort alla medlemmar (användare/grupper) från en mapps medlemsdel. När användaren försöker ta bort alla användare läggs den inloggade användaren till i listan (NPR-31171).

* Resurser med plustecken (+) i filnamnet kan inte tas bort (NPR-31162).

* Menyn Skapa, som visas på den övre menyn när du väljer en mapp, visar inte &quot;Mapp&quot; som ett alternativ för att skapa (NPR-30877).

* Mappval Skapa > FileUpload-åtgärdsobjekt saknas när ACL för Deny jcr:removeChildNodes och jcr:removeNode på sökväg tillämpas för en användare (NPR-30840).

* DAM-arbetsflöden försätts i viloläge när vissa mp4-resurser överförs, vilket gör att alla återstående arbetsflöden försätts i viloläge (NPR-30662).

* Slut på minne uppstår när stora PDF-filer (av flera gigabyte) överförs till DAM och dess underresurser bearbetas (NPR-30614).

* Massförflyttning av resurser misslyckas och ett varningsmeddelande visas (NPR-30610).

* Resursnamn ändras till gemener när resurser flyttas från en mapp till en annan i AEM som körs i körläget Dynamic Media Scene 7 (NPR-31630).

* Ett fel uppstod när en fjärrbilduppsättning redigerades för bilden som finns i mappen som heter same som namnet på Scene 7-företaget (NPR-31340).

* Dynamiska medieresurser som innehåller referenser publiceras inte (NPR-31180).

* Överföringar från AEM Dynamic Media - Scene 7-miljön till Scene 7 tar för lång tid att slutföra (NPR-31048).

* Aktiveringspunkten som läggs till i en bildresurs är inte synlig via Interactive Image Viewer på sidan med resursinformation (NPR-30979).

* Enorma snedningsjobb skapas och Bearbetningsbanderollen visas igen när åtgärder som utförs på resurser i AEM Assets skickas till Scene 7 (NPR-30947).

* En konflikt inträffar när en språkkopia av resurser skapas och resurser inte överförs till Scene 7 (NPR-30932).

* Dynamiska återgivningar som hämtats från AEM som körs i läget Dynamic Media Hybrid är brutna (de är av texttyp med innehållet&quot;det går inte att hitta bilden&quot; i stället för bildinnehållstypen) (NPR-30876).

* Arbetsflödet för Dynamic Media Encode Video misslyckas med att generera miniatyrbilder för videon som migreras från Scene 7 till Dynamic Media - körningsläget Scene 7 (CQ-4282011).

* IpsApiException observerades när resurser migrerades från en instans till en annan med olika företags-ID för Scene 7 (CQ-4280548).

* Miniatyrbilden av 3D-resursen är inte informativ när en 3D-modell som stöds har importerats till AEM (CQ-4283701).

* Rullningsknappar visas i visningsprogrammet om en 3D-resurs har få kameravinklar (CQ-4283322).

* Felaktig behållarhöjd för en överförd 3D-modell som förhandsvisats i DimensionalViewer på sidan Resursinformation (CQ-4283309).

* Videor kan inte spelas upp med SmartCropVideoViewer i Internet Explorer 11 och Safari (CQ-4281422).

* Användning av flyttningsknappen för att flytta flera resurser, från en mapp till en annan, misslyckas i AEM-körning på dynamiska media - scen7-körningsläge (CQ-4280384).

* Förvrängd video visas i resursinformation när MIME-typen är en annan än MP4 (CQ-4279704).

* Videoklipp som nyligen har infogats i mappar med en videoprofil är fortfarande i bearbetningstillstånd även när kodens procenttal har slutförts till 100 % (CQ-4279389).

* När du flyttar resurser från en mapp skapas ett stort antal snedstreck (API-anrop för Scene 7) än vad som helst krävs (CQ-4278664).

* Namn på bilduppsättningen ändras till gemener i Scen 7 när bilduppsättning (eller mediaset) skapas och namnges med lämplig namnkonvention i DAM (CQ-428112).

* Scene 7 Migrator anger felaktigt publiceringstillstånd (CQ-4263492).

* Touch UI-sökning (utförd via Omnissearch)-resultatsidan rullar automatiskt upp och förlorar användarens rullningsposition i innehållsfragment (CQ-4282898).

* PDF-filer är inte indexerade och innehållet i dem är inte sökbart (CQ-4278916).

* Felmeddelandet&quot;Grupp visas inte av användarväljaren: false förväntas vara lika med true&quot; visas när en stängd användargrupp läggs till med ett annat värde `principalName` och `authorizableId` (CQ-4278177).

* Resursens gränssnittskolumnvy visar alla sökvägar oavsett vilken sökväg en klientorganisation har (CQ-4278175).

* Resursväljarens sökning fungerar inte som förväntat (CQ-4275886).

* Återgivningsarbetsflöden misslyckas (CQ-4271928).

* DAM-händelserensning tar bort den senaste (maxSavedActivities) händelseinformationen och lagrar data som skapats tidigare (NPR-31336).

* Touch UI-sökning (utförd via Omnissearch)-resultatsidan rullar automatiskt upp och förlorar användarens rullningsposition (NPR-31307).

* Åtgärdsfältet och antalet resurser uppdateras inte när du markerar alla och sedan avmarkerar vissa objekt (mappar/enskilda resurser) i Touch UI (NPR-3118).

* Ett undantag visas i AEM vid avsökning efter jobbinformation för en resurs (CQ-4283569).

### Sites {#sites}

* Om LiveCopy-arvet bryts visas länkar för språkkopiering i stället för länkar för LiveCopy (NPR-30980).
* Om antalet poster är fler än 40 visas bara de första 40 posterna för en ny utkast. I utkast visas tomma rader för resten av posterna (NPR-31182).
* När en användare lägger till japanska eller koreanska tecken i egenskapen description på en meny, visas förvrängda tecken för japansk och koreansk text på menyn. (NPR-31331).
* Det går inte att infoga en inbäddad tabell som listobjekt (NPR-30879) i RTF-redigeraren.
* När du har gjort en avskalning av RTF-redigerare (Rich Text Editor). använder textbunden teckensnittsstorlek för element, oväntat (NPR-31284).
* När en användare fokuserar på fält med vänster stödlinje och använder ett kortkommando för att klistra in innehåll, klistras innehållet i sidredigerarens urklipp in i stället för innehållet som kopieras från de vänstra fältspåren (NPR-31172).
* När en användare lägger till ett filöverföringsfält i ett flerfält lagras bildsökvägen i komponentnoden i stället för i flerfältsnoden (NPR-30882).
* API:t ResponsiveGridExporter returnerar inte gränssnittet com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter. Paketet com.day.cq.wcm.foundation.model.impl deklareras som ett privat paket (NPR-31398).
* När en sida som innehåller vissa ExperienceFragments öppnas i icke-redigerarläge (antingen i Författare utan prefixet och `editor.html` `wcmmode=disabled`, eller i Utgivare), avslutas begäran med HTTP-statusfelkoden 500 (NPR-30743).
* Användare kan inte ändra sitt lösenord och komma åt sin profilsida (NPR-31161).

### Sök- och användargränssnitt {#search-ui-interface}

* När du växlar från kortvyn till listvyn på en sökresultatsida uppstår en fördröjning innan sidan kan rullas (NPR-31286).

* Kryssrutan Markera alla är dold i listvyn i användargränssnittet för webbplatser (NPR-31614).

* Antalet Markera alla på en sökresultatsida är felaktigt (NPR-31120).

* I metadataredigeraren visas taggar som inte finns (NPR-31119).

### Översättning {#translation}

* Två popup-fönster visas när du väljer alternativet Förfallodatum i ett översättningsjobb (NPR-31270).

### Platform {#platform}

* Alternativet Mime-typ i webbkonsolen fungerar inte (NPR-31108).

* Klientcertifikatet accepteras inte när enkel inloggning konfigureras (NPR-31165).

* Uppdateringar i buffertstorlekskonfigurationen för Jetty-baserad HTTP-tjänst sparas inte (NPR-30925).

* QueryBuilder har nu stöd för orderby ``fn:name()`` i XPath-frågor (NPR-31322).

* Dubblettaktiveringsträdet skapas vid uppgradering från AEM 6.3 (NPR-31513).

* Vidarebefordrade begäranden bevarar inte svarshuvuden som ställs in vid slingautentisering (NPR-30013).

* Det går inte att söka i väljarkomponenterna (NPR-31692).

* Ett fel visas när en ZIP-fil bifogas till ett AEM Communities-inlägg på grund av olika versioner av Apache POI- och Apache Tika-paketet (NPR-31018).

* Paketet är dolt i konfigurationshanteraren och är därför inte tillgängligt för anpassade paket (NPR-31720). ``org.apache.sling.distribution.api``

### Projekt {#projects}

* Det går inte att växla kalendervyer (NPR-31271).

### Varumärkesportal {#assets-brand-portal}

**Produktförbättringar**

* Arbetsflödet för import av mediekällor i AEM Resurser ändras så att endast de nyskapade resurserna från Brand Portal hämtas till AEM, och de resurser som redan finns i mappen NEW hoppas över för att undvika replikering (CQ-4278527).

**Korrigeringar**

* En felaktig ikon visas när en ny Contribute-mapp skapas i funktionen Resurser (CQ-4282825).
* När du skapar en ny Contribute-mapp visas inte en eller båda undermapparna (NYTT och DELAT) i Contribute-mappen (CQ-4282424).
* Systemet genererar ett undantag om användaren försöker publicera om Contribute-mappen från AEM till Brand Portal efter att ha tagit emot nya resurser i Contribute-mappen från Brand Portal end (CQ-4279740).
* Det är inte tillåtet att skapa en Contribute-mapp i en Contribute-mapp (kapslad mapp) för att undvika komplexitet (CQ-4278391).
* Systemet genererar ett undantag när användarlistan för varumärkesportalen (.csv-fil) som importeras från AEM Admin Console överförs. Endast fälten Email, FirstName och LastName i CSV-filen är obligatoriska (CQ-4278390).

### Communities {#communities}

**Korrigeringar**

* Snabblänkar för att hantera grupper (Öppna/Redigera/Publicera/Ta bort grupper) är inte synliga för communityadministratörer (Gruppadministratör/Webbplatsadministratör) (NPR-31627).
* En inskickad blogg visas bara om sidan uppdateras/läses in manuellt (NPR-31599).
* JCR-frågan som används av funktionen &quot;Mentions&quot; är skiftlägeskänslig och tar för lång tid att returnera resultaten (NPR-31475).
* AEM 6.5 UberJar-filen genererar ett undantag, paket saknas i AEM 6.5 UberJar-filen (NPR-31186). `cq-social-translation`
* Jackson Database-bibliotek uppdaterade till version 2.9.9.3 för att åtgärda nya säkerhetsluckor (NPR-30967).
* Aktiviteter och meddelandetitlar är inkonsekventa (NPR-30941).
* Sidindelningen fungerar inte korrekt i webbgruppsbloggar (NPR-30914).
* Analysrapporter fylls inte i i AEM-redigeringsmiljön. En tom sida visas (NPR-30913).

### Oak {#oak}

* Uppdateringar av Lucene-index gör att författarservern sinkas (NPR-31548).

### Formulär {#forms-6530}

>[!NOTE]
>
>AEM Service Pack innehåller inte korrigeringar för AEM Forms. De levereras med ett separat Forms-tilläggspaket. Dessutom släpps ett kumulativt installationsprogram med korrigeringar för AEM Forms på JEE. Mer information finns i [Installera tillägget](#install-aem-forms-add-on-package) AEM Forms och [Installera AEM Forms på JEE](#install-aem-forms-jee-installer).

#### Formulärtilläggspaket {#forms-add-on-package-6530}

**Adaptiva former**

* Strängar innehåller ordlistenyckeln när adaptiva former lokaliseras (NPR-31110).

**Interaktiv kommunikation**

* **MissingNode.toString()** returnerar felaktiga resultat efter uppgradering av Jackson-bibliotek till 2.10.0 (NPR-31549).

* Textredigeraren tar slumpmässigt bort blankstegstecken från text som kopieras från Microsoft Word (NPR-31113).

**Korrespondenshantering**

* Bildtexter och verktygstips visas inte när bokstäver migreras från LiveCycle ES4SP1 till AEM 6.5 (NPR-31615).

* **Textflödesformatering stöds** inte längre i felmeddelanden när bokstäver sparas som utkast (NPR-30463).

**Arbetsflöde**

* OSGi-arbetsflödet misslyckas på grund av 100 % processoranvändning (NPR-31233).

**HTML5-formulär**

* När du genererar HTML5-förhandsgranskning av ett XDP-formulär visas ett flimmer när instanser av ett delformulär läggs till (NPR-30909).

#### Formulär i JEE-installationsprogram {#forms-jee-installer-6530}

**Formulär - dokumenttjänster**

* SOAP-webbtjänst som använder MTOM i ett .NET-projekt visar undantag för AssemblerServiceClient-anrop och HTMLToPDF2-metoder (NPR-4281771).

**Foundation JEE**

* Åtgärdskonfigurationen läser inte in processnamnen för åtgärden Anropa ett formulärarbetsflöde för att skicka (NPR-31478).

### Funktionspaket ingår {#feature-packs-included-6530}

>[!NOTE]
>
>För AEM Forms-kunder är det viktigt att installera AEM Forms-tilläggspaket efter installation av AEM Service Pack, Cumulative Fix Pack eller Feature Pack.

#### Formulär - Foundation JEE {#forms-foundation-jee-feature}

* Stöd för AEM Forms i Oracle 18c (NPR-29155).

## AEM 6.5.2.0

AEM 6.5.2.0 är en viktig version som innehåller prestanda, stabilitet, säkerhet samt viktiga kundkorrigeringar och förbättringar som släppts sedan den allmänna tillgängligheten av AEM 6.5 i **april 2019**. Den kan installeras ovanpå AEM 6.5.

Några viktiga höjdpunkter i den här Service Pack-versionen är:

* Den inbyggda databasen (Apache Jackrabbit Oak) uppdateras till version 1.10.3.
* En konfigurationsegenskap som tillåter export av Experience Fragments direkt till användardefinierade arbetsytor för Adobe Target har lagts till.
* Resurser som användare kan söka efter visuellt liknande bilder. AEM visar smarta taggade bilder från DAM-databasen som liknar den användarvalda bilden. Se [visuell sökning](../assets/search-assets.md#visualsearch).

* Förbättrade funktionerna för anslutna resurser för att lägga till stöd för att hämta dokument från DAM-fjärrdistributioner. Webbplatsförfattare kan nu söka efter och filtrera dokumenttyper som stöds i Content Finder. Fjärrdokumenten kan läggas till i komponenten Download på webbsidor. Se [Använda anslutna resurser](../assets/use-assets-across-connected-assets-instances.md).

* Förbättra dokumenttypsfilter med fler MIME-typer som stöder flervärdesalternativ.
* Ett externt arbetsflöde för ombearbetning har introducerats för stöd för flera resurser.
* Optimerade prestanda för dynamiska media genom att använda standardresursfilter för replikering.
* Återställt redigeringsalternativ för beskärning/rotering av resurser för DMS7.
* Implementerade ett alternativ för att stänga av ljudet för en video vid inläsning i VideoPlayer.
* Åtgärda problemet så att kolumnvyn i resursanvändargränssnittet bara visar innehåll som är specifikt för innehavaren.
* Korrigera så att formatdragspelsändringar återspeglas i sökresultaten.

### Assets {#assets}

**Produktförbättringar**

* Förbättrade funktionerna för anslutna resurser för att lägga till stöd för att hämta dokument från DAM-fjärrdistributioner. Webbplatsförfattare kan nu söka efter och filtrera dokumenttyper som stöds i Content Finder. Fjärrdokumenten kan läggas till i komponenten Download på webbsidor. Programfix för CQ-4270245. Se [Använda anslutna resurser](/help/assets/use-assets-across-connected-assets-instances.md).

* Resurser som användare kan söka efter visuellt liknande bilder. AEM visar smarta taggade bilder från DAM-databasen som liknar den användarvalda bilden. Se [visuell sökning](../assets/search-assets.md#visualsearch).

**Korrigeringar**

* Resurssökvägar i URL:er och mappmetadata som genereras av AVS-API:t är inte URL-kodade. GRANITE-26198: Programfix för CQ-4271814
* Det går inte att öppna ett arkiv med en mapp som har ett procenttecken (%) i namnet med hjälp av gränssnittet Resurser. NPR-29989: Programfix för CQ-4270467
* Pekgränssnitt: Under guiden Hantera publicering läggs referenser till efter sidan i postbegärandetexten, vilket gör att alla resurser publiceras efter sidan, och när sidan återges missas en del av resurserna i publiceringsinstansen. NPR-29985: Programfix för CQ-4270724
* Funktionen för att ta bort kopplingar till resurser fungerar inte för relaterade resurser som har specialtecken (tecken som blir URI-kodade) i namnet. NPR-30387: Programfix för CQ-427446
* När du redigerar ett innehållsfragment skapas versionen med fel användare.
* Ett fel uppstod när samlingar skapades i ett klientbaserat system. NPR-30114: Programfix för CQ-4272948
* Resursgränssnittskolumnvyn respekterar inte den aktuella klientens dam-root-sökväg, men använder alla tenant-dammsökvägar. NPR-30636: Programfix för CQ-4275481
* Möjlig XSS-attack (cross-site scripting) via ett begränsat varningsfönster eftersom den injicerade bilden kan ses. NPR-30617: Programfix för CQ-4270133
* MultiTenant: Innehavare som sparar mappegenskaper observerar både meddelande om att åtgärden lyckades och felmeddelande som beskriver åtgärden misslyckades:&quot;Det går inte att redigera egenskaper. Otillräckliga behörigheter.&quot; och förvirrar dem. NPR-30545: Programfix för CQ-4275333
* Dialogrutan Resursväljare tillåter inte val av resurs och kan därför inte uppdatera källan med hjälp av funktionen för relaterat källbyte. NPR-30502: Programfix för CQ-4275029
* DAM Update Asset Workflow - I inaktivt läge vid överföring av stora MP4-filer. NPR-30480: Programfix för CQ-4271352
* Funktionen Skapa granskningsuppgift fungerar inte eftersom null-nyttolast gör att alla efterföljande granskningsuppgiftrelaterade åtgärder misslyckas. NPR-30468: Programfix för CQ-4274263
* Adobe Smart Tag-anslutningsproblem via DataPower. NPR-30026: Programfix för CQ-4269457
* Resursens användargränssnittskolumnvy genererar ett fel vid försök att öppna filtren från listen. NPR-30501: Programfix för CQ-4273862
* När du lägger till grupper som synkroniserats från LDAP i CUG-egenskaperna (Closed User Group) för en resursmapp, sparas och hämtas inte gruppen. NPR-30615: Programfix för CQ-4274689
* Filtersökningsformat och orienteringsfält använder inte det automatiskt ifyllda värdet på sökfrågan. NPR-30620: Programfix för CQ-4275724
* Resursresurslänken i en mapp med blanksteg och tecknet &quot;&amp;&quot; i namnet visar tomma grå kort för vissa resurser. NPR-30557: Programfix för CQ-4270187
* Schemaformuläret för mappmetadata identifierar inte automatiskt datatyp och skapar därför inte den relaterade TypeHint-typen när formuläret skickas. NPR-30599: Programfix för CQ-4275227
* Alternativen för att beskära och rotera resurser är inaktiverade i DMS7-redigeringsgränssnittet. NPR-30118: Programfix för CQ-4273221
* Funktionen Dela länk fungerar inte på AEM-instanser med DMS7-konfiguration. NPR-30080, NPR-30492: Programfix för CQ-4273651
* Om du lägger till Dynamic Media Scene7-komponenten på sidan och sedan publicerar sidan aktiveras inte DMscene7-konfigurationen varje gång. NPR-30641: Programfix för CQ-4275962
* Lade till en IPSJobJournal i AEM för att skapa endast ett IPS-jobb (Intrusion Prevention Systems) per bearbetningsprofil. NPR-30490: Programfix för CQ-4273614
* Dynamiska medier: Lagt till standardfilter för att utesluta att resurser replikeras till AEM-publiceringsnoden. NPR-30538: Programfix för CQ-4274678
* Ett externt arbetsflöde för ombearbetning har introducerats för stöd för flera resurser så att mappen kan användas som nyttolast. Arbetsflödet består av två steg: ombearbetar resurser utan handtag via metadatamappning till nästa steg och överför alla resurser utan resurshandtag till S7 i ett enda IPS-jobb. Mer information finns i Konfigurera Dynamic Media Cloud-tjänster. NPR-30489: Programfix för CQ-4272903
* När du laddar upp en felaktig CSV-fil efter att du korrigerat CSV-filen raderas den korrekta CSV-filen. Programfix för CQ-4277694, CQ-4277814
* Den felaktiga ikonen som är specifik för de bidragsmappar som ska tas bort. Programfix för CQ-4277580
* När du väljer en användare i användarväljaren på fliken Resursbidrag visas inte användarens namn i tabellen och dialogrutan Ta bort användare på egenskapssidan visar fel text. Programfix för CQ-4277875
* Medarbetare kan inte läggas till i resursavgiftsmappen från användarväljaren genom att markera användare och klicka på Lägg till. Programfix för CQ-4277824, CQ-4278087
* Det går inte att söka efter användarnamn med gemener i användarväljaren. Programfix för CQ-4277958, CQ-4277930
* Icke-administratörer kan publicera resurser i en ny mapp i en resursavgiftsmapp. Programfix för CQ-4278200
* dam-user (icke-admin) har inte möjlighet att lägga till medarbetare i resursavgiftsmappen. Programfix för CQ-4278192
* Knappen&quot;Skapa&quot; visas i mappen Resursbidrag. Programfix för CQ-4277560
* Om du sorterar sökfrågan efter relevans returneras InDesign-dokument tillsammans med InDesign-mallar. Programfix för CQ-4273864
* Om användaren har ett e-post-ID med versaler kan användarna inte checka in de resurser som tidigare har checkats ut. Programfix för CQ-4276575
* Åtgärden Ta bort gäller bara för de förinställningar som är markerade, och om skärmen automatiskt uppdaterar listan efter åtgärden visas andra förinställningar som redan har uppdaterats. Programfix för CQ-4261461
* Om du konfigurerar Dynamic Media Cloud-tjänster i DMHybrid-läge skapas flera tomma rapportsviter som skapats i Analytics, och utan något rapportsvits-ID lagrat i AEM, vilket leder till dubblering av rapportsviten. Programfix för CQ-4249780
* Det går inte att synkronisera om namnbytet i AEM-resursen till det duplicerade namnet till Scene7. Programfix för CQ-4276763
* Användargenererat innehåll visas felaktigt på sökfilterpanelen. Programfix för CQ-4273875
* Alternativet Sök efter liknande är inte tillgängligt för TIFF-bilder. Programfix för CQ-4278238
* Implementerat alternativ för att stänga av video vid inläsning i VideoPlayer. Programfix för CQ-4266465
* Visare - VideoViewer: affisch=none fungerar inte korrekt om en extern video används. Programfix för CQ-4265536
* Vänteikonen visas när videon spelas upp i IE11- och MS Edge-webbläsare. Programfix för CQ-4251539
* 3.8 SDK- och 5.13-visningsprogram - README-filer uppdateras inte och innehåller information från tidigare versioner. Programfix för CQ-4273737
* Innehållsfragment får versionsnummer även innan ändringarna sparas. NPR-30616: Programfix för CQ-4273088
* Ersätt Asset#getMetadata(String) med Asset#getMetadataValueFromJcr(String) i en miniatyrprocess. NPR-30491: Programfix för CQ-4273067
* Om du överför jpg uppstår flera instanser av meddelandet: &quot;ReplicateOnModifyWorker Replicating UPDATED&quot; för varje resurs, vilket ger sämre prestanda.
* Uppackning av zip-arkiv med funktionen Extrahera arkiv orsakar problem med mappar vars namn innehåller procent (%) i titeln. NPR-29990: Programfix för CQ-4270467

### Sites {#sites-6520}

* Om LiveCopy-arvet bryts visas länkar för språkkopiering i stället för länkar för LiveCopy. (NPR-30980)
* Om antalet poster är fler än 40 visas endast de första 40 posterna för en ny utkast. I utkast visas tomma rader för resten av posterna. (NPR-31182)
* Plugin-programmet RTE (Rich Text Editor) för textkomponenten visar förvrängda tecken för japansk och koreansk text. (NPR-31331)
* Det går inte att infoga en inbäddad tabell som listobjekt i RTF-redigeraren. (NPR-30879)
* Vid skalning av RTF-redigerare (Rich Text Editor) används oväntat textbunden teckensnittsstorlek för element. (NPR-31284)
* När en användare fokuserar på fält på den vänstra listen och använder kortkommandon för att klistra in innehåll, klistras innehållet i sidredigerarens urklipp in i stället för innehållet som kopieras från fält på den vänstra listen. (NPR-31172)
* När en användare lägger till ett filöverföringsfält i ett flerfält lagras bildsökvägen i komponentnoden i stället för i flerfältsnoden. (NPR-30882)
* API:t ResponsiveGridExporter returnerar inte gränssnittet com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter. Paketet com.day.cq.wcm.foundation.model.impl deklareras som ett privat paket. (NPR-31398)
* När en sida som innehåller vissa ExperienceFragments öppnas i icke-redigerarläge (antingen i redigerarläge utan prefixet och `editor.html` `wcmmode=disabled`i Publisher) avslutas begäran med HTTP-statusfelkod 500. (NPR-30743)

### WCM - sidredigeraren {#wcm-page-editor-6520}

**Produktförbättringar**

* Förbättra dokumenttypsfilter med fler MIME-typer som stöder alternativ med flera värden. Programfix för CQ-4270694

### Hantering av innehållsfragment {#content-fragment-management-6520}

* Frågan som används av gränssnittet för modeller för innehållsfragment är mycket långsam och resulterar till slut i ett fel. Programfix för CQ-4270807

### UI - Foundation {#ui-foundation}

* Kortkommandon som utlöser ett fel som gör att användaren inte kan använda &#39;m,&#39; &#39;p,&#39; &#39;e&#39; i ett visst användargränssnitt. NPR-30355: Programfix för GRANITE-26346
* När du stänger gränssnittet för resurssökning återställs inte den vänstra listen till Innehållsval, vilket förhindrar användaren från att öppna filterfältet den andra gången. NPR-30509: Programfix för CQ-4274716
* Flerklientmiljö: Övre navigering i resursgränssnittet är inte tillgängligt och orsakar JavaScript-fel. NPR-30104: Programfix för GRANITE-26344

### Översättning {#translation-6520}

* Översättningsproblem - Endast ett fåtal komponenter översätts med maskinöversättning. NPR-30079: Programfix för CQ-4273764

### Platform {#platform-6520}

* AEM Default Mail Sender kan inte skicka e-post till en SMTP-fjärrserver via TLS v1.2. NPR-30476: Programfix för GRANITE-26605

### Projekt {#projects-6520}

* dam:folderThumbnailPaths-värden uppdateras inte och gamla miniatyrer visas inte ens när resurserna i mappen har tagits bort. NPR-30424: Programfix för CQ-4273667
* När du slutför flyttalternativet ändras inte resursens namn och namn. NPR-30647: Programfix för CQ-4276265

### Communities {#communities-6520}

* Diagnostik för användarsynkronisering är helt bruten och fungerar inte. NPR-30004, NPR-29943: Programfix för CQ-4270287, CQ-4271348

### Sling {#sling}

* Uppgraderade instanser från 6.3.3.2 till 6.5 resulterar i duplicerade OSGi-konfigurationer. NPR-30130: Programfix för CQ-4274016

### Integrering {#integration}

* Det anpassade innehållet visas inte korrekt på publiceringsinstansen förrän instansen startas om. NPR-30377: Programfix för CQ-4273706
* När du konfigurerar Launch på en webbplats har biblioteksadressen ett snedstreck (/) som är förinställt, vilket kan orsaka manuella åtgärder varje gång. NPR-30694: Programfix för CQ-4275501

### Formulär {#forms-6520}

>[!NOTE]
>
>AEM Service Pack innehåller inte korrigeringar för AEM Forms. De levereras med ett separat Forms-tilläggspaket. Dessutom släpps ett kumulativt installationsprogram med korrigeringar för AEM Forms på JEE. Mer information finns i [Installera tillägget](#install-aem-forms-add-on-package) AEM Forms och [Installera installationsprogrammet](#forms-jee-installer)för AEM Forms JEE.

De viktigaste nyheterna i AEM 6.5.2.0-formulär är:

* Inställningen Auto har lagts till `RenderAtClient` i `PDFFormRenderOptions` API för AEM Forms OSGi.

#### Formulärtilläggspaket {#forms-add-on-package}

**Integrering med back end**

* Det går inte att konfigurera formulärdatamodellen med en värdbaserad, belastningsutjämnad URL. NPR-30123: Programfix för CQ-4273359
* När formulärdatamodellen (FDM) skapas med WSDL (Web Service Definition Language) `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type` returneras felmeddelandet: NPR-30477: Programfix för CQ-4272921

**Korrespondenshantering**

* &quot;Återgivningen av CCR-gränssnittet (Create Correspondence UI) misslyckas ibland med följande fel i konsolen:
   `- Uncaught Error: variable [object Object]is already known the letter`- NPR-30127

**Interaktiv kommunikation**

* Ett fält som är markerat som obligatoriskt i formulärdatamodellen visas enligt kraven i användargränssnittet för Skapa korrespondens (CCR UI). NPR-30623: Programfix för CQ-4274902

**Formulär - arbetsflöde**

* Omappade utdatavariabler i Bevakade mappar gör att anropet misslyckas. Programfix för CQ-4264451

**HTML5-formulär**

* När den anpassade koden eller projektet distribueras för andra gången återges inte sidan och följande fel inträffar:

   `org.apache.sling.scripting.sightly.SightlyException.`

   NPR-30539: Programfix för CQ-4272509

* När du använder NonVisual Desktop Access i bläddringsläge för att läsa ett HTML5-formulär, läser webbläsaren Chrome &quot;graphic&quot; före varje Scalable Vector Graphic (SVG) i formulärdesignen. NPR-30449: Programfix för CQ-4274732

#### Formulär-JEE-installationsprogram {#forms-jee-installer}

**Formulär - dokumentsäkerhet**

* Det går inte att använda en signatur med tidsstämpel. Fel: ALC-DSC-003-000: com.adobe.idp.dsc.DSCInvocationException: Anropsfel. NPR-30820: Programfix för CQ-4275852

**Formulär - dokumenttjänster**

* Om &quot;SubmitURL&quot; innehåller ett et-tecken (&amp;), visas tolkningsfel i loggen när POST-begäran görs till renderpdf-servern. NPR-30865: Programfix för CQ-4278232

**Formulär - Foundation JEE**

* HTMLtoPDF-tjänsten visar inte maxReuseCount i JMX-konsolen. NPR-30134, NPR-30304: Programfix för CQ-4273763
* Om du lägger till eller redigerar en webbtjänstanslutning genom att anropa webbtjänster från AEM Forms Workbench uppstår ett fel: ClassNotFoundException org.apache.axis.message.SOAPBodyElement. NPR-30105: Programfix för CQ-4273217

### Funktionspaket ingår {#feature-packs-included}

>[!NOTE]
>
>För AEM Forms-kunder är det viktigt att installera AEM Forms-tilläggspaket efter installation av AEM Service Pack, Cumulative Fix Pack eller Feature Pack.

#### Sites {#sites-feature-packs-included}

* En konfigurationsegenskap som tillåter export av Experience Fragments direkt till användardefinierade arbetsytor för Adobe Target har lagts till. NPR-29189: Programfix för CQ-4249782

#### Formulär - dokumenttjänster {#forms-document-services-1}

* Inställningen Auto har lagts till `RenderAtClient` i `PDFFormRenderOptions` API för AEM Forms OSGi. NPR-30759: Programfix för CQ-4278193

## AEM 6.5.1.0 {#release-6510}

AEM 6.5.1.0 är en viktig version som innehåller prestanda, stabilitet, säkerhet samt viktiga kundkorrigeringar och förbättringar som släppts sedan den allmänna tillgängligheten av AEM 6.5 i *april 2019.* Den kan installeras ovanpå AEM 6.5.

Några viktiga höjdpunkter i den här Service Pack-versionen är:

* Aktiverade inkludering av dynamiskt gränssnittsläge i spårningshändelser som anpassade attribut.
* Inkluderat stöd för leverans av 360-graders videomaterial i Dynamic Media Scene 7.
* Aktiverade *japansk radbrytning* via stilpluginen i RTF-redigeraren. Mer information finns i [Konfigurera japansk radbrytning](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### Assets

* DAM DMGGateway-gränssnittet för S3-multipart-stöd har uppdaterats. NPR-29740: Programfix för CQ-4226303
* Förhandsgranska återgivningar genererar `Only empty tenantId is currently supported` fel efter uppgradering till AEM 6.5\. NPR-29986: Programfix för CQ-4272353
* Dialogrutan Ta bort är inte synlig så att du kan ta bort jobb. NPR-29720: Programfix för CQ-4271074
* När en användare har lagt till en objekttitel på egenskapssidan öppnas egenskapssidan igen när användaren försöker stänga sidan. NPR-29627: Programfix för CQ-4264929
* VersioningTimelineEventProvider ska tillhandahålla rotversionen tillsammans med noden av typen nt: version. Programfix för GRANITE-26063
* Implementerade möjligheten att överföra och spela upp 360 sfäriska videor i AEM DM-Scene7-läge. Programfix för CQ-4265131
* Live-kopian hämtar felaktig status om källan redigeras. Programfix för CQ-4265451
* Aktiverat stöd för flera Platshanterare för resurser. Programfix för CQ-4271453, CQ-4268621, CQ-4257491
* AEM-gränssnittet bör visa ytterligare en post för den aktuella versionen av resursen i tidslinjehistoriken och visa den senaste incheckningskommentaren från Adobe Asset Link. Programfix för CQ-4262864
* Tidslinjen för innehållsfragment visar ett felmeddelande när egenskaper saknas. Programfix för CQ-4272560
* Ett problem med Scene 7-videospelaren när den expanderar till helskärm. Programfix för CQ-4266700
* ZoomVerticalViewer: Panoreringsknappar ska inte visas om en enda bildresurs används. Programfix för CQ-4264795
* Om du tar bort en underordnad nod i live-kopian bör liveRelationship frigöras. Programfix för CQ-4270395
* Metadataschemat innehåller bara objekt från den globala konfigurationen och saknar dem från den aktiva klientorganisationen. URL-värdet för formPath återställs till standard även om det ändras. NPR-29945: Programfix för CQ-4262898
* Publicera bildförinställningar till varumärkesportalen misslyckas med 500-felkod. NPR-29510: Programfix för CQ-4268659

### Sites

* Tomma egenskaper och flera egenskaper sprids inte från utkast under utrullning. Det går inte att återställa live-kopia med utkast för komponenter. NPR-29253: Programfix för CQ-4264928, CQ-4264926, CQ-4267722
* CoralUI, när det används med `Multifield`, lagrar `fileReferenceParameter` på komponentnivå i stället för på multifältnivå. NPR-29537: Programfix för CQ-4266129
* Förbättring av AEM-textkomponenten och textredigeraren till japanska. NPR-29785: Programfix för CQ-4265090
* Sidan som återställs med Timewarp ska referera till rätt bild vid versionshanteringen. NPR-29431: Programfix för CQ-4262638
* Ett problem med arv av Style System-noder från överordnad till underordnad. NPR-29516: Programfix för CQ-4270330
* Ett felmeddelande visas när den sociala publiceringen konfigureras för Facebook-autentisering. NPR-29211: Programfix för CQ-4266630
* Den återgivna miniatyrbilden för innehållsfragment visar intern kalenderrepresentation för fältet Datum och Tid. NPR-29531: Programfix för CQ-4269362
* Knapparna visas inte när du öppnar fliken Behörigheter i Coral2-implementeringen. Programfix för CQ-4269419

### Handel

* ConstraintViolationException, när lat innehåll migreras för e-handel. NPR-29247: Programfix för CQ-4264383

### Hantering av innehållsfragment

* Tolkningsfel vid öppning av ett innehållsfragment med tecken som består av dollartecken `($)` och inledande klammerparentes `({)`. Programfix för CQ-4270266

### Experience Fragments

* Exportera AEM Experience Fragments till Adobe Target. Programfix för CQ-4265469
* Experience Fragments export till target misslyckas med smarta bilder. Programfix för CQ-4269606

* Användaren stöter på en återvändsgränd när försöker flytta Experience Fragments via Omnissearch i kortvyn. Programfix för CQ-4263848

### WCM - sidredigeraren

* XSS (Cross-site scripting) speglades när en ogiltig väljare användes. Programfix för CQ-4270397

### Replikering

* Data som tillhandahålls av användaren kan inte utelämnas vid utdata i `cq/replication/components/agent` komponenten, vilket resulterar i en lagrad XSS-säkerhetslucka (Cross-site scripting). Programfix för CQ-4266263

### Arbetsflöde

* Dialogdeltagarens kalenderväljarfält har brutits. NPR-29727: Programfix för CQ-4270423

### WCM - SPA-redigerare

* Aktiverat hämtning av föråtergivet innehåll från en fjärrslutpunkt. Programfix för CQ-4270238
* Varningar i loggar när en SPA-mallsida öppnas på serversidan. Programfix för CQ-4270238

### WCM - MSM

* Uppgradera till AEM 6.4.3 så att det tar lång tid att driftsätta Multi-Site Manager. Programfix för CQ-4271410

### Integrering

* BrightEdge-autentiseringsuppgifter misslyckas med anslutningsfel. NPR-29168: Programfix för CQ-4265872

* Ett undantagsmeddelande visas när du försöker redigera och spara AEM-startkonfigurationen. NPR-29176: Programfix för CQ-4265782/CQ-4266153

### Användargränssnitt

* Stöd för att spåra dynamiska gränssnittslägen som anpassade attribut har lagts till samtidigt som vissa händelser i grundspårnings-API:t spåras. Programfix för GRANITE-26283
* Det går inte att ange spårningsfunktionen på skicka-knappen. Programfix för GRANITE-26326
* Guiden kan inte ställa in spårningsfunktionen på skicka-knappen. NPR-29995, NPR-30025: Programfix för CQ-4264289

### Communities

* Det går inte att justera nya märken i listrutan på medlemsprofilsidan. NPR-29381: Programfix för CQ-4267987
* Besökare och medlemmar utan moderatorbehörighet kan se ej godkända/väntande inlägg genom att klistra in URL:en. NPR-29724: Programfix för CQ-4271124, CQ-4271441
* En hög svarstid på upp till 40-50 sekunder observeras vid användarinloggning för Community. NPR-29677: Programfix för CQ-4269444

### Replikering

* Replikeringsagentkomponenten är känslig för en sårbarhet som avslöjar känslig information för obehöriga användare. NPR-29611: Programfix för GRANITE-25070

* Sessionsläckage under OAuth för varje replikering till Varumärksportal. NPR-30001: Programfix för GRANITE-26196

### Projekt

* Publicera resurser från AEM Author /content/dam/mac-mappen till Brand Portal fungerar inte. NPR-29819: Programfix för CQ-4271118

### Plattform

* HtmlLibraryManager tar bort allt innehåll i crx-quickstart vid cacheogiltigförklaring. NPR-29863: Programfix för GRANITE-26197

### Felix

* Information om minnesanvändning visas inte i systemkonsolen när Java11 används. NPR-29669

### Formulär

De viktigaste nyheterna i AEM 6.5.1.0-formulär är:

* Endast OSGi: Ett nytt attribut har lagts till `PAGECOUNT` i Output and Forms Service.

* Endast OSGI: Stöd för att skapa statiska PDF-filer med Forms Service har aktiverats.
* Behörigheter för XMLForm.exe har aktiverats för administratör och rotanvändare.
* Aktiverat stöd för ADFS v3.0 för Dynamics lokal integrering.

#### Formulärtilläggspaket

**Integrering med backend**

* Det gick inte att hämta WSDL (Protected Web Service Definition Language). NPR-29944: Programfix för CQ-4270777
* När AEM Forms är installerat på IBM WebSphere misslyckas skapandet av en formulärdatamodell baserad på SOAP. Programfix för CQ-4251134
* Aktiverat stöd för ADFS (Active Directory Federation Services) v3.0 för integrering på plats i Microsoft Dynamics. Programfix för CQ-4270586
* När en datakällas titel ändras visas inte den uppdaterade titeln i formulärdatamodellen. Programfix för CQ-4265599
* Om namnet på en entitet eller ett attribut innehåller bindestreck eller blanksteg, kan uttrycken inte utvärdera sådana entiteter och attribut. Programfix för CQ-4225129

* Felaktiga utdata visas när ett kolon finns i den primitiva strängutdata. Programfix för CQ-4260825

* Även om inget innehåll förväntas från REST API-utdata genereras ett fel av formulärdatamodellens invoke-åtgärd. Programfix för CQ-4268828

**Adaptiva former**

* Det gick inte att lägga till en ny instans i adaptivt formulärfragment under en lat inläsning. NPR-29818: Programfix för CQ-4269875
* Verifiera att komponenten inte loggar eller visar något fel för dokumentmallar. Programfix för CQ-4272999
* Stöd har lagts till för att inaktivera layoutredigeraren för adaptiva formulär. Programfix för CQ-4270810
* Verifieringssteget för adaptiva formulär i AEM 6.5 har återställts. Programfix för CQ-4269583

* Valideringsfel för anpassade formulärfält bryter Adobe Sign. Programfix för CQ-4269463
* När en AEM Forms-instans har fler än 20 adaptiva formulärfragment och namnet på alla formulärfragment börjar med samma sträng, returnerar sökningen inga eller bara de 20 senast skapade fragmenten. Programfix för CQ-4264414, CQ-4264914

* Prestandaproblem när appen Adaptive Forms används med stor datamängd. . Programfix för CQ-4235310

* Om det öppnas via ett anonymt konto på en publiceringsinstans går det inte att läsa in GuideRuntime-skriptet. Programfix för CQ-4268679

**Formulär - Interaktiv kommunikation**

* Mallen för interaktiv kommunikation listar inte sidhuvuds- och sidfotskomponenter i listan över tillåtna komponenter. Programfix för CQ-4237895
* När du skapar en interaktiv utskriftsmall för kommunikation som innehåller ett bildfält, ställs diagrammets rubrik in på tom. Programfix för CQ-4264772
* När du tar bort linjefärgen i ett diagram anges värdet undefined. Programfix för CQ-4264762
* Ändringar av layoutlager som görs i dokumentfragment försvinner när ändringar synkroniseras. Programfix för CQ-4266054
* Formulärdatamodellelement i ett dokumentfragment som är bundet till ett textfält visar inte arvsikon och tillåter bindning. Programfix för CQ-4261089
* Återgivnings-API för utskriftskanal har inte möjlighet att skicka data som en parameter i API:t. Programfix för CQ-4263540
* Agentinställningarna visas inte eftersom kryssrutan Redigerbar av agent avmarkeras när bindningstypen ändras från textfragment till Inget/Datamodellobjekt för strängfält/variabel. Programfix för CQ-4261953
* När agentanvändargränssnittet skickas lagrar den resulterande webbdatajson-filen information för arvsannullerade obundna fält. Programfix för CQ-4265621

**Formulär - arbetsflöde**

* När ett formulär skickas på nytt från utkorgen för adaptiva formulärprogram, förlorar det data. NPR-28345: Programfix för CQ-4260929
* Dokumenten stängs inte när de sparas för ärenden som inte är variabla. Programfix för CQ-4269784
* Appen Adaptive Forms har inte stöd för Microsoft Windows 8.1\. Programfix för CQ-4265274
* När en bild på mer än 2 MB bifogas som en bifogad fil på fältnivå till ett formulär i Android-versionen av AEM Forms-appen kraschar programmet. Programfix för CQ-4265578

* Aktiverade förifyllningsalternativ för Interactive Communication Print Channel i Tilldela-aktiviteten. Programfix för CQ-4265577
* Användarna kan inte visa en delad uppgift förrän de blir medlemmar i den grupp som uppgiften är tilldelad till. Programfix för CQ-4248733
* Det går inte att spara eller skicka JEE-program i appen Adaptiv form i Windows. Programfix för CQ-4268704
* Den formulärdatamodell som är associerad med formulärdatamodellvariabeln är inte synlig. Programfix för CQ-4266554
* Inget stöd för statusvariabeln för dokumentsignering med variabelstöd. Programfix för CQ-4266312
* Det går inte att skicka från arbetsytan med ett omljud. Programfix för CQ-4263172
* Om arbetsflödet öppnas för redigering i en uppgraderad konfiguration visas ett fel i stället för arbetsflödets namn i det bevakade mappgränssnittet. Programfix för CQ-4238579

**Formulär - hantering**

* När ett tillägg som inte är xsd eller schema.json överförs, sker ingen överföring och inget felmeddelande genereras. Programfix för CQ-4266716

**Formulär - korrespondenshantering**

* AEM 6.5 Forms Create Correspondence UI (CCR UI) kan inte öppna korrespondens som skapats med AEM 6.3-formulär. Programfix för CQ-4266392
* Summeringsfunktionen i XDP fungerar inte om DDE-datatypen är av typen number. Programfix för CQ-4227403
* Inaktiveringslogik för bokstavscache i minnet uppdateras eftersom den senaste ändringstiden inte uppdateras när en resurs publiceras. Programfix för CQ-4250465
* Det går inte att publicera dokumentfragment, DD och Letters. Programfix för CQ-4272893

#### Formulär-JEE-installationsprogram

**PDF Generator**

* Konverteringen av CAD-filer till PDF misslyckas med 64-bitars JDK. NPR-29924, NPR-29925: Programfix för CQ-4272113
* Ersatte namnet på PhantomJS till WebToPDF för HTML-till-PDF-konvertering. NPR-29933: Programfix för CQ-4234545
* Ett fel genereras när zip-filen konverteras till PDF. Programfix för CQ-4268628

**Formulär - Designer**

* När en fullständig tillgänglighetskontroll utförs för den statiska PDF-filen som skapats med AEM Form Designer misslyckas kontrollen Primary Language på grund av att språkattributet saknas. Programfix för CQ-4272923, CQ-4271002

**Formulär - dokumentsäkerhet**

* Digital signatur med HSM (Hardware Security Module) fungerar inte med OSGi Linux på Java 11 och Java 8\. NPR-29838: Programfix för CQ-4270441
* Digital signatur med HSM (Hardware Security Module) fungerar inte med JEE Linux och alla appservrar som stöds, dvs. JBoss och Websphere. NPR-29839: Programfix för CQ-4266721
* Verifiering av signaturer i en PDF med hjälp av PDF Advanced Electronic Signatures (PAdES) genererar InvalidOperationException. NPR-29842: Programfix för CQ-4244837
* Utökat stöd för Document Security Extension för Office 2019\. Programfix för CQ-4254369, CQ-4259764

**Formulär - dokumenttjänster**

* PDF-filen kan inte konverteras till PDF/A-1b med formulärfältet har ingen utseendeordlista. NPR-29940: Programfix för CQ-4269618

* OSGi: Det går inte att avgöra antalet sidor som genereras under återgivningen. NPR-28922: Programfix för CQ-4270870
* Stöd för statiska PDF-filer har aktiverats med Forms Service i AEM Forms OSGi. NPR-28572: Programfix för CQ-4270869
* Det går inte att ändra behörigheten för XMLForm.exe. NPR-29828, NPR-29237: Programfix för Q-4267080
* Den statiska PDF-fil som skapas av AEM Forms-serverns utdatamoddul fyller inte i språkattributet/taggen med språket för det dokument som skapas. NPR-27332: Programfix för CQ-4271002

**Formulär - Foundation JEE**

* Om pdfg_srt inte är tillgänglig i de sista artefakterna misslyckas installationsprogrammet. NPR-29854: Programfix för CQ-4270137
* LCBackupMode.sh fungerar inte. NPR-29840: Programfix för CQ-4269424
* UDP-portreferens ska tas bort från användargränssnittet för WebSphere. Programfix för CQ-4264782

### Funktionspaket ingår

#### Resurser - inkluderade

* Aktiverat stöd för flera Platshanterare för resurser. Mer information finns i [Återanvända resurser med MSM för resurser](https://helpx.adobe.com/experience-manager/6-5/help/assets/reuse-assets-using-msm.html). NPR-29199: Programfix för CQ-4259922

#### Webbplatser - ingår

* Exportera AEM Experience Fragments till Adobe Target. Mer information finns [i Experience Fragment Link Rewriter Provider - HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML). Programfix för CQ-4265469

#### Formulär - dokumenttjänster - ingår

* Endast OSGi: Ett nytt attribut har lagts till i PAGECOUNT i Output and Forms Service. NPR-28922: Programfix för CQ-4270870
* Endast OSGi: Stöd för att skapa statiska PDF-filer med Forms Service har aktiverats. NPR-28572: Programfix för CQ-4270869
* Behörigheter för XMLForm.exe har aktiverats för administratör och rotanvändare. NPR-29237: Programfix för CQ-4267080

### OSGi-paket och innehållspaket

Följande textdokument innehåller en lista över de OSGi-paket och innehållspaket som ingår i AEM 6.5.1.0

Lista över OSGi-paket som ingår i AEM 6.5.1.0

[Hämta fil](assets/6_5-bundle-list.txt)

Lista över innehållspaket som ingår i AEM 6.5.1.0

[Hämta fil](assets/6_5-content-package-list.txt)
