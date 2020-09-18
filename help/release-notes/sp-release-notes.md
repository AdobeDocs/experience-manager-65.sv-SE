---
title: '[!DNL Adobe Experience Manager] 6.5 Service Pack versionsinformation.'
description: Versionsinformation för [!DNL Adobe Experience Manager] 6.5 Service Pack 6.
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 4f6b2bbb58f7f18798eb01a6c8f2cef4b02063a3
workflow-type: tm+mt
source-wordcount: '4225'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager] 6.5 Service Pack versionsinformation {#aem-service-pack-release-notes}

## Versionsinformation {#release-information}

| Produkter | Adobe Experience Manager 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.6.0 |
| Typ | Service Pack-version |
| Date | 3 september 2020 |
| Hämta URL | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.6.zip) |

## Vad ingår i Adobe Experience Manager 6.5.6.0 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.6.0 är en viktig uppdatering som innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat samt prestanda, stabilitet och säkerhetsförbättringar som släppts sedan den allmänna tillgängligheten av 6.5-utgåvan i **april 2019**. Den kan installeras ovanpå Adobe Experience Manager 6.5.

De viktigaste funktionerna och förbättringarna i Adobe Experience Manager 6.5.6.0 är:

* Publicering av resursavgiftsmappar från Brand Portal till Experience Manager Assets stöds nu även via proxyservern.

* De automatiskt genererade grupperna med privata mappar rensas nu bort när den privata mappen tas bort i [!DNL Experience Manager Assets].

* Beskrivningarna av modifierare i videoförinställningsredigeraren [!UICONTROL Viewer] har uppdaterats i [!DNL Dynamic Media].

* En ny företagsinställning anges för att återspegla status för [!DNL Dynamic Media] kopplingen.

* Standardalternativen för `test` och `aiprocess` uppdateras till `Thumbnail`, från `Rasterize` tidigare versioner i Dynamic Media, för att säkerställa att användarna bara behöver skapa miniatyrbilder och hoppa över sidextraheringen och extraheringen av nyckelord.

* Fyll i ett anpassat formulär i förväg på klienten.

* Integrering av formulärdatamodell med RESTful API:er på en server med tvåvägs SSL-implementering.

* Förbättrad cachning för översatta adaptiva formulärsidor.

* Stöd för Adobe Sign-texttaggar i den automatiska Forms Conversion Service.

* Support to convert colored forms to adaptive forms using [!DNL Automated Forms Conversion service].

* Stöd för SMB 2- och SMB 3-protokoll.

* Den inbyggda databasen (Apache Jackrabbit Oak) uppdateras till version 1.22.4.

En fullständig lista över funktioner och förbättringar som introducerats i Experience Manager 6.5.6.0 finns i [Nyheter i Adobe Experience Manager 6.5 Service Pack 6](new-features-latest-service-pack.md).

Nedan följer en lista över korrigeringar i version [!DNL Experience Manager] 6.5.6.0.

### [!DNL Sites] {#sites-6560}

* I [!DNL Sites] eller [!DNL Screens]väljer du ett projekt och klickar på [!UICONTROL Management Publications]. Användarna kan inte gå vidare i [!UICONTROL Manage Publication] guiden på grund av gränssnittsfel. Alternativet fungerar inte heller (NPR-34099). [!UICONTROL Publish]
* Positionen för iParsys (ärvt styckesystem) återställs inte till den ursprungliga standardpositionen efter avmarkering [!UICONTROL Cancel Inheritance] eller [!UICONTROL Disable Inheritance] alternativ (NPR-34097).
* Om användaren inte `RolloutConfigManagerFactoryImpl` kan läsa in en rollout-konfiguration försöker den inte läsa in de saknade konfigurationerna. Den returnerar de cachelagrade konfigurationerna (NPR-34092).
* I huvudkomponenten Text tas klassen från - `em` taggen bort när du har använt HTML-källredigeringsalternativet (NPR-34081).
* Efter uppgradering från Experience Manager 6.3.3 till Experience Manager 6.5.3 tar utrullningsprocessen mycket längre tid och utrullningen misslyckas med ett timeoutfel (NPR-34049).
* Attributvärdena kodas `htmlwriter` inte tillbaka. Den kod som finns i XF-koden exporteras med avkodade attributvärden (det vill säga `"` i stället för `&#34`). Det orsakar problem på målsidan med Visual Experience Composer som använder den exporterade XF-filen (NPR-34048).
* När du flyttar sidor i [!DNL Experience Manager Sites]kan du förbättra loggningen för att fånga upp det fel som uppstod när versionen skapades (NPR-34014).
* Om [!DNL Rich Text Editor] all text tas bort tas även stycketaggen bort (NPR-33976).
* När `siteadmin` sidan (i det klassiska användargränssnittet) öppnas eller uppdateras inaktiveras alternativen på `New` menyn (NPR-33949).

   ![Skärmbild som illustrerar problemet med saknade menyer i Classic UI](assets/33949_missing_menu.png)

* A [!DNL Content Fragment] kan inte användas som en `TemplatedResource` eftersom den misslyckas i `ContentFragmentUsePojo` (NPR-33911).
* Synkrona och asynkrona flyttningsåtgärder kan leda till fel på grund av samtidiga överföringar. Åtgärder för att flytta sidor är begränsade till synkron förflyttning. Den förhindrar samtidig flyttning av sidor (NPR-33875).
* [!UICONTROL Manage Publication] åtgärden att replikera innehåll från författare till publiceringsinstans misslyckas och genererar ett JavaScript-fel (NPR-33872).
* När flera sidor eller resurser har valts för att skapa versioner skapas den nya versionen endast för den senast valda sidan eller resursen (NPR-33866).
* Flytta en ritningssida med live-kopior till en annan mapp. När du flyttar den till den ursprungliga mappen misslyckas flyttåtgärden utan något fel (NPR-33864).
* När flyttningsåtgärden används för att byta namn på en webbsida i [!DNL Sites] konsolen visas två överlappande dialogrutor i det sista steget i guiden (NPR-33831).

   ![Skärmbild som illustrerar NPR-33831-utgåvan av dialogrutan för överlappande flyttning](assets/33831_rename_dialog.png)

* Egenskaperna `cq:acLinks` och `cq:acUUID` för [!DNL Adobe Campaign] kopian tas bort under kopierings- och klistra in-åtgärden (NPR-33794).
* När du försöker köra en utrullning på en underordnad sida för en frånkopplad överordnad live-kopia genereras ett null-pekarundantag (NPR-33676). [!DNL Experience Manager]
* Komponenterna i en [!DNL RTE] layoutbehållare syns inte när layoutbehållaren kopieras och klistras in igen på sidan. Komponenterna kan inte redigeras men visas vid uppdatering av sidan (NPR-33662). [!DNL RTE]
* När du ändrar storlek på en layoutkomponent för olika brytpunkter (mellanstora och stora) fungerar inte layouten som förväntat (NPR-33608).
* I infogat redigeringsläge i [!DNL RTE]fungerar inte det att dra en bild för textkomponenten (NPR-33602).
* Det går att skapa en komponent på en ritningssida med samma namn som sidnamnet. Under utrullning har `_msm_moved` suffixet för att byta namn på komponenten. Komponenten flyttas till slutet av [!UICONTROL Paragraph System] (NPR-33535).
* När offTime eller onTime är inställt på många sidor eller resurser är det resurskrävande och gör systemet långsammare vid start och avstängning (NPR-33482).
* En användare med CRUD-behörighet på `/content/experience-fragment` kan inte ta bort en mapp (NPR-33436).
* Du kan välja [!UICONTROL HTML & JSON] som alternativ för [!UICONTROL Adobe Target export format] en överordnad mapp i [!DNL Experience Fragments] avsnittet. Samma egenskaper visas i det Touch-aktiverade användargränssnittet för undermapparna i den här överordnade mappen. I CRXDE visas emellertid bara HTML i stället för `cq:adobeTargetExportFormat`att visas `html,json` (NPR-33423).
* Publicera eller Avpublicera från ett sidalias stöds inte. Ta bort alternativet som verkar göra anspråk på något annat (NPR-33415).
* En viss tagg kan flyttas från en plats till en annan i [!DNL Experience Manager]. Den kan även tillämpas på olika sidor före och efter att den flyttas. När du redigerar egenskaperna för sidorna visas inte taggen för redigering även om taggen är densamma (NPR-33353).
* En sidmall återges inte korrekt när en layoutbehållare tas bort från en mall som innehåller flera layoutbehållare (NPR-33347).
* I mallredigeraren kan du försöka ta bort en mall som används av mer än 100000 sidor under `/content/`. Ett fel visas utan något felmeddelande (NPR-33312).
* Omdirigering till [!DNL Experience Manager] sida med ankare fungerar inte på Author-instansen eftersom `PageRedirectServlets` frågesträngen placeras efter ett URL-fragment eller ett ankare (NPR-34288).
* Om du skapar ett varumärke under `/content/campaign` resulterar det i en struktur som inte gör det möjligt att skapa kampanjer. [!UICONTROL Create Brand] Alternativet lämnar det nyskapade varumärket utan möjlighet att skapa [!UICONTROL Offers and Activities] eftersom det inte finns något [!UICONTROL Create] alternativ (NPR-34113).
* Du kan göra uppehåll [!DNL Live Copy] i en sidas utseende och arv bryts som de visas i redigeringsläget. I sidegenskaperna indikerar ikonen som representerar arv felaktigt att arvet finns och inte är brutet (NPR-34017).
* Sidor med många referenser kan inte flyttas asynkront och ibland misslyckas flyttåtgärden (CQ-4297969).
* En webbsida med `/` tecken i URL:en slutar svara vid redigering. När en komponent läggs till under utvecklingen ökar processoranvändningen och webbläsaren slutar svara (CQ-4295749).
* I bläddringsläget lägger inte NVDA till en berättarröst för ett värde som är valt på menyalternativet Typ/Storlek. Det visuella fokus ligger inte på det markerade elementet. Användare som förlitar sig på en skärmläsare kan inte använda bläddringsläget (CQ-4294993).
* När du skapar en webbsida kan användare välja [!UICONTROL Content Page] mall. På [!UICONTROL Social Media] fliken väljer användarna en [!UICONTROL Preferred XF variation]. Användarna kan inte använda tangentbordstangenter för att välja ett Experience Fragment i NVDA-bläddringsläge (CQ-4292669).
* Hanteringsbiblioteket uppdaterades till den säkrare versionen v4.7.3 (NPR-34484).

### [!DNL Assets] {#assets-6560}

**Tillgänglighetsförbättringar i Experience Manager Assets**

* Med hjälp av tangentbordstangenterna kan användare nu komma åt och fokusera på de interaktiva alternativen för användargränssnittet i [!UICONTROL References] listan med resurser (NPR-34115).

* Skärmläsaren presenterar nu avsedd åtgärd för predikaten på söksidan (NPR-34104).

* Söksidan och sökresultatsidan har nu mer informativa titlar för att förstå skärmläsaranvändare bättre (NPR-34093).

* Skärmläsare meddelar nu alternativ för att ta bort de markerade taggarna på [!UICONTROL Basic] fliken för [!UICONTROL Properties] tillgångssidan (NPR-33972).

* Elementen i varje rad i listvyn presenteras nu som element i samma rad av skärmläsare (NPR-33932).

* Användarfokus när du navigerar med `Tab` tangenten går nu till stängningsalternativet i förhandsversionen (NPR-33863).

* Användarfokus flyttas nu till sökikonen när Omnisearch har stängts (NPR-33705).

* Alternativen i det användbara gränssnittet har nu ett mer framträdande visuellt fokus med förbättrad kontrast när du navigerar med tangentbordstangenter. Tangentbordsanvändare kan identifiera de fokuserade områdena (NPR-33542).

* Dragningsfunktionen med tangentbordet fungerar nu i [!UICONTROL Metadata Schema Editor] bläddringsläge för skärmläsare (CQ-4296326).

* När du navigerar i bläddringsläge i dialogrutan för länkdelning visas en skärmläsare,

   * Berättar inte tabellinformationen så fort dialogrutan har lästs in.

   * Kan navigera till alla automatiska förslag som visas.

   * Lägger till en berättarröst för de automatiska förslagen för [!UICONTROL Add Email Address/Search] (CQ-4294232).

* När du använder `Esc` tangenten för att ta bort snabbikonerna från kortvyn tas inte längre tangentbordsfokus bort från det sista objekt som är i fokus (CQ-4293554).

* För interaktiva alternativ i användargränssnittet meddelar skärmläsaren nu vad de är avsedda för och inte vad ikonerna har för litteralnamn (CQ-4272943).

* Tangentbordsfokus flyttas nu till [!UICONTROL Flyout], [!UICONTROL InlineZoom], [!UICONTROL Shoppable_Banner], [!UICONTROL Zoom_dark], [!UICONTROL Zoom_light]och [!UICONTROL ZoomVertical_dark]alternativ när du navigerar med tangentbordsfliktangenten [!UICONTROL ZoomVertical_light] i resursinformationen [!UICONTROL Viewers] [!DNL Dynamic Media] (CQ-4290605).

* [!UICONTROL Save & Close] kan du nu komma åt alternativ på [!UICONTROL Properties] resurssidan med hjälp av tangentbordstangenter (NPR-34107).

* Felmeddelanden på grund av felaktiga kombinationer av användarnamn och lösenord på inloggningssidan meddelas nu av skärmläsare varje gång felet inträffar (NPR-33722).

* I [!DNL Experience Manager] sidhuvudsavsnittet, vid navigering i bläddringsläge, visas nu skärmläsare,

   * Automatiskt redigerade förslag i [!UICONTROL Type to search] Omnissearch.

   * Läget som expanderat eller komprimerat för [!UICONTROL Solutions], [!UICONTROL Help], [!UICONTROL Inbox]och [!UICONTROL User] alternativ.

   * Det [!UICONTROL Searching Help] statusmeddelande som visas när användaren anger en söksträng i [!UICONTROL Search for Help] fältet under [!UICONTROL Help] alternativet.

   ![Hjälpmenyn i sidhuvudet](assets/Help_aem_header.png)

   *Bild:[!UICONTROL Search for Help]på[!UICONTROL Help]menyn.*

   * Felmeddelandet om ett felaktigt värde anges i [!UICONTROL Impersonate as] fältet under [!UICONTROL User] alternativet och fokus flyttas korrekt till textfältet (NPR-33804).

   ![Användarmeny i sidhuvud](assets/User_aem_header.png)

   *Bild:[!UICONTROL Impersonate as]i[!UICONTROL User]menyn i sidhuvudet.*

* Användaren kan nu ändra fokus med tangentbordet i:

   * [!UICONTROL Search/Add Email Address] i [!UICONTROL Link Sharing] dialogrutan.

   * [!UICONTROL Add User or Group] under [!UICONTROL Closed User Group] fliken [!UICONTROL Permissions] i mappen [!UICONTROL Properties] (NPR-34452).

**Problem som har korrigerats i Experience Manager Assets**

[!DNL Adobe Experience Manager] 6.5.6.0 [!DNL Assets] innehåller korrigeringar av följande:

* Anteckningar markeras inte när de väljs från resursens tidslinje (CQ-4302422).

* Förhandsgranskning av marknadsföringsmaterial (t.ex. broschyr, flygblad och visitkort) som skapats med [!DNL Adobe InDesign] mall visar inte radbrytningar och styckebrytningar (NPR-34268).

* Textextrahering och därmed fulltextsökning för de överförda PDF-filerna fungerar inte (NPR-34164). Du åtgärdar det genom att starta om [!DNL sAdobe Experience Manager] distributionen efter installation av Service Pack 6.

* På tidslinjen för flersidiga resurser visas anteckningar som används för alla underresurser när du bläddrar i resursen i tidslinjevyn i stället för att anteckningarna som är specifika för de specifika underresurserna visas (NPR-34100).

* Resursmappar publiceras inte med [!UICONTROL Manage Publication] alternativet om mapparna innehåller resurser i JavaScript-, CSS- eller JSON-filformat (NPR-34090).

* Om du avmarkerar eller tar bort de tillämpade taggarna eller filtren i Omnissearch körs sökfrågan flera gånger, vilket leder till att söktiden ökar (NPR-34078).

* I kortvyn när ett arbetsflöde (för en resurs i en mapp) pågår eller väntar, läses sidan in igen tills arbetsflödet har slutförts eller avslutats. Därför kan författare inte arbeta med de resurserna i den mapp som de måste rulla nedåt för (NPR-33986).

* Om användaren flyttar en publicerad resurs till en ny plats publiceras resursen om, även om [!UICONTROL Republish] alternativet avmarkeras. Detta leder till att många överblivna resurser ligger i publiceringsinstansen. Standardbeteendet är dock att om du flyttar en åtgärd på en publicerad resurs återpubliceras den automatiskt. den här resursen publiceras på nytt om författaren väljer alternativet [!UICONTROL Republish] när resursen flyttas (NPR-33934).

* Sidan för resurser i samlingar läser inte in allt HTML-innehåll, till exempel [!UICONTROL Move Assets] [!UICONTROL Adjust/ Republish] alternativet. Därför kan användare inte slutföra flyttåtgärden (NPR-33860).

* Om du flyttar en resurs och lägger till specialtecken i namnet och titeln på de flyttade resurserna skapas en extra mapp (med samma namn) på den nya platsen för resursen (NPR-33826).

* [!UICONTROL Download] knappen för en resurs inaktiveras när [!UICONTROL Email] alternativet väljs i [!UICONTROL Download] dialogrutan (NPR-33730).

* Felet&quot;Begär-URI för lång&quot; visas vid gruppåtgärder för resurser, t.ex. redigering av massmetadata (NPR-33723).

* JavaScript-fel observeras och användare kan inte markera eller ta bort de alternativ som genereras i [!UICONTROL Dropdown] fältet efter [!UICONTROL Add through JSON path] funktionalitet i [!UICONTROL Folder Metadata Schema Form Editor], om den överförda JSON-filen har blanksteg eller specialtecken i värde (NPR-33712).

* De statiska återgivningarna av resurser uppdateras inte när resursen uppdateras med alternativet [!UICONTROL Open] i [!DNL desktop app] eller [!DNL Adobe Asset Link] och synkroniseras tillbaka till [!DNL Adobe Experience Manager] (CQ-4296279).

* I kolumnvyn flyttar flyttåtgärden för en uppsättning resurser även de resurser som markerades innan du använde [!UICONTROL Filter] alternativet för dem. Observera att om du använder [!UICONTROL Filter] alternativet avmarkeras det tidigare urvalet (NPR-34018).

* Omvända snedstreck läggs till före specialtecken i sökförslag för resurser, som har specialtecken i sitt namn (NPR-33834).

* När du skapar regler för listrutor i [!UICONTROL Folder Metadata Schema Form]kan användaren inte välja värden från [!UICONTROL Field Choices] kolumnen (CQ-4297530).

* Körningskopian av resurser i en anpassad arbetsflödesmodell (skapas i `/var/workflow/models/dam`) tas bort när du installerar [!DNL Experience Manager] 6.5 Service Pack 5 eller en tidigare version på [!DNL Experience Manager] 6.5 (NPR-34532). Om du vill hämta körtidskopian synkroniserar du designtidskopian av arbetsflödesmodellen med körtidskopian med HTTP API:
   `<designModelPath>/jcr:content.generate.json`.

**Problem som har åtgärdats i Dynamic Media**

* Om användaren definierar kodningsinställningarna i redigeringar efter att videoprofilen har skapats, tas inställningarna för smart beskärning bort från videoprofiler (CQ-4299177).

* Resursflimmer vid sidinläsning när användaren växlar mellan alternativ för sidospår (till exempel [!UICONTROL Overview], [!UICONTROL Timeline], [!UICONTROL Viewers]) på sidan med tillgångsinformation (NPR-34235).

* Följande problem har observerats med omprocessjobb:

   * Jobb-ID saknas i jobbreferensen som returnerades av ombearbetningsjobbet.

   * Bearbeta om jobb för enbart videologgar med filnamn och inte fullständig sökväg.

   * Återbearbetningsjobbet har inte möjlighet att ange resurstypen som statisk.

   * `ExcludeFromAVS` finns inte (CQ-4298401).

* Funktionen för smart beskärning misslyckas med fel när en bildprofil läggs till i en mapp med flera (till exempel 11) proportioner (NPR-34082).

* Arbetsflödet för DAM-uppdateringsresurser utlöses när användaren rullar ned på [!UICONTROL Workflow Archive] sidan på [!UICONTROL Workflow] fliken [!UICONTROL Tools] i [!DNL Adobe Experience Manager] konfigurerats med Dynamic Media Scene7 (CQ-4299727).

* Symboler på [!UICONTROL Behavior] fliken för [!UICONTROL Viewer Preset Editor] är inte lokaliserade (CQ-4299026).

* I huvudvyn visas bilden i en felaktig layout som inte får plats i visningsprogrammet, om visningsprogrammet är i svarsläge (CQ-4298293).

* Ändringar av bildförinställningar i synkroniseras [!UICONTROL Adobe Experience Manager] inte med Scene7 Publishing System (CQ-4299713).

### [!DNL Commerce] {#commerce-6560}

* Länkar till resurser från produkter ändras inte när resurser flyttas (NPR-34098).

### Platform {#platform-6560}

* Det går inte att hämta loggar med diagnosverktyget på en uppgraderad Experience Manager-instans (NPR-34336).
* Uppgraderingen misslyckas med ett fel på grund av beroenden till en specifik version av `cq-wcm-api` grundpaketet (CQ-4300520).
* Standardvärdena för **[!UICONTROL Connect Timeout]** och **[!UICONTROL Socket Timeout]** inställningarna för standardagentkonfigurationen (publicering) har inte angetts (NPR-33707).
* Uppdateringar av mappningskonfigurationen under `/etc/map.publish` återspeglas inte på webbplatssidorna (NPR-34015).
* [API-referensdokumentationen](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html) innehåller inte dokumentationen för `com.day.cq.tagging` paketet (CQ-4295864).

### Användargränssnitt {#ui-6560}

* Gränssnittet för avlastningsläsaren visar inte alla jobbämnen (NPR-34308).
* Gränssnittet i Configuration Browser visar inte alla konfigurationer (NPR-33644).
* När du trycker på `Esc` **[!UICONTROL User]** tangenten när du söker efter användare som ska personifiera, stängs dialogrutan i stället för användarlistan (NPR-34084).

### Integreringar {#integrations-6560}

* Aktiviteter med långa namn synkroniseras inte med [!DNL Adobe Target] (NPR-34254).

### Översättningsprojekt {#translation-6560}

* Ett översättningsprojekt skapas inte om användarens `authorizableID` innehåller specialtecken (NPR-33828).

### Sling {#sling-6560}

* Hälsokontroll och Mönsteravkännare har överlappande funktioner. Följden är att hälsokontrollen tas bort från produkten (NPR-33928).

### WCM {#wcm-6560}

* Foundation Components - När du lägger till en grundläggande bildkomponent på en sida och refererar till en bild fungerar inte `Undo` åtgärden (NPR-34516).

* Det går inte att använda åtgärden Sidflyttning (CQ-4303028).

### [!DNL Communities] {#communities-6560}

* Att dela ett inlägg på sociala medier visar ett föråldrat alternativ, Google+ (NPR-33877).

* Community-medlemmen kan inte ändra gruppmallen eller andra gruppfunktionsinställningar (NPR-33530).

* Hyperlänkstaggar i bilder genereras inte korrekt i ett foruminlägg (NPR-33464).

* Tillgänglighetsfel identifieras i funktionen för communitytilldelning (NPR-33442).

* Befintliga användare i en community-grupp som lagts till via Admin Console tas bort från användarlistan vid ändringar i community-gruppkonsolen (NPR-34315).

<!--
* Tag filters are vulnerable to sensitive information disclosure (NPR-33868).
-->

### [!DNL Forms] {#forms-6560}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack innehåller inga korrigeringar för [!DNL Forms]. De levereras med ett separat [!DNL Forms] tilläggspaket. Dessutom släpps ett kumulativt installationsprogram som innehåller korrigeringar för [!DNL Experience Manager Forms] JEE. Mer information finns i [Installera AEM Forms-tillägg](#install-aem-forms-add-on-package) och [Installera AEM Forms på JEE](#install-aem-forms-jee-installer).

**Adaptiv Forms**

* Om det saknas ett adaptivt formulärfragment återges inte det adaptiva formuläret (NPR-34302).

* Hjälpinnehållsbeskrivningen för adaptiva formulärfält visar en HTML-stycketagg (NPR-34116).

* När du väljer **[!UICONTROL Revalidate on Server]** egenskapen skickas inte det adaptiva formuläret (NPR-33876).

* Det går inte att skicka- **[!UICONTROL Submit to REST endpoint]** åtgärden för ett anpassat formulär (CQ-4299044).

* Tillgänglighet: När du försöker skicka ett anpassat formulär utan att överföra en bilaga för ett obligatoriskt fält flyttas fokus inte automatiskt till bilagefältet (CQ-4298065).

* När du lägger till rader i en tabell i ett anpassat formulär visas inte rätt resultat i alternativen **[!UICONTROL Add to top]** och **[!UICONTROL Add to bottom]** (CQ-4297511).

* Skriptet [!UICONTROL Value Commit] aktiveras felaktigt, vilket resulterar i dataförlust i en adaptiv form (CQ-4296874).

* Datumväljaren fungerar inte korrekt för lokaliserade adaptiva formulär (NPR-34333).

* När det finns ett understreck eller blanksteg i filnamnet kan du inte bifoga filen till ett anpassat formulär (CQ-4301001).

* När en kapslad upprepningsbar panel har fler förekomster än den överordnade panelen, kan inte alla förekomster av den kapslade upprepningsbara panelen fyllas i i förväg (NPR-33666).

* Adaptiva formulär har vissa öppna resurslösningar. Detta leder till att det inte går att skicka in. Problemet inträffar då och då (CQ-4299407).

**Arbetsflöde**

* När en arbetsflödesgodkännare överför en bifogad fil får den bifogade filen ett nytt namn till `undefined` (NPR-33699).

* [!DNL Experience Manager] Åtgärd för tömning av arbetsflöde misslyckas och följande felmeddelande visas (NPR-33575):

   `java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory`

* [!DNL Experience Manager Forms] app för att [!DNL Windows] sluta svara efter att ett formulär har skickats (NPR-34409).

* När du installerar AEM Service Pack visas inte listan **Att göra** som länkar. Texten för **Att göra** -objekten innehåller HTML-taggar (NPR-34317).

**Interaktiv kommunikation**

* När du inkluderar ett textdokumentfragment med kapslade repeterbara komponenter, sparas inte det interaktiva meddelandet (NPR-34095).

**Korrespondenshantering**

* När du ändrar ett textdokumentfragment som innehåller data dictionary-värden slutar agentens användargränssnitt svara (NPR-33930).

* Om du kopierar och klistrar in innehåll från ett [!DNL Microsoft Word] dokument till ett textdokumentfragment i en bokstav uppstår formateringsproblem (NPR-33536).

**Dokumenttjänster**

* När du genererar en PDF-fil från en XDP-fil med hjälp av utdata och Forms-tjänster, leder det till att text saknas och överlappar (NPR-34237, CQ-4299331).

* När du konverterar en HTML-fil till PDF går det inte att konfigurera `MaxReuseCount` attributet (NPR-33470).

* När du laddar ned en PDF-fil som innehåller interaktiva funktioner för Reader Extensions kan du inte lägga till en bifogad fil i PDF-filen med [!DNL Adobe Reader] (NPR-33729).

**Dokumentsäkerhet**

* Det går inte att utföra signeringsåtgärden med HSM-baserade certifikat i en PDF-fil efter installation av [!DNL Experience Manager] Service Pack (NPR-34310).

**Designer**

* Det går inte att öppna Xformuläri Designer version 6.5.x (CQ-4295322).

* När du öppnar Designer visas ett felaktigt år på välkomstskärmen (CQ-4295289).

* När du installerar [!DNL Acrobat DC] på servern är **[!UICONTROL Distribute Form]** alternativet inaktivt (CQ-4296304).

Mer information om säkerhetsuppdateringar finns på [Experience Manager sida](https://helpx.adobe.com/security/products/experience-manager.html)med säkerhetsbulletiner.

## Installera 6.5.6.0 {#install}

**Installationskrav**

* AEM 6.5.6.0 kräver AEM 6.5. Mer information finns i [uppgraderingsdokumentationen](/help/sites-deploying/upgrade.md) .
* Nedladdningen av Service Pack finns på Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* Installera AEM 6.5.6.0 på en av Author-instanserna med Package Manager på en distribution med MongoDB och flera instanser.
* Ta en ögonblicksbild eller en ny säkerhetskopia av AEM innan du installerar.
* Starta om instansen innan du installerar den. Detta behövs bara när instansen fortfarande är i uppdateringsläge (och detta är fallet när instansen uppdaterades från en tidigare version), men vi rekommenderar att instansen körs under en längre period.

>[!NOTE]
>
>Adobe rekommenderar inte att du tar bort eller avinstallerar Adobe Experience Manager 6.5.6.0-paketet.

### Installera Service Pack {#install-service-pack}

Så här installerar du Service Pack på en befintlig Adobe Experience Manager 6.5-instans:

1. Hämta Service Pack från [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.6.zip).

1. Öppna Pakethanteraren och klicka på **[!UICONTROL Upload Package]** för att överföra paketet. Mer information om hur du använder paketet finns i [Pakethanteraren](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html).

1. Markera paketet och klicka på **[!UICONTROL Install]**.

>[!NOTE]
>
>Dialogrutan för pakethanterarens gränssnitt avslutas ibland när Service Pack installeras. Adobe rekommenderar att du väntar på att felloggarna ska stabiliseras innan du får åtkomst till distributionen. Vänta på de specifika loggarna för avinstallationen av uppdateringspaketet innan du försäkrar dig om att installationen lyckas. Vanligtvis händer detta på [!DNL Safari] men kan inträffa i alla webbläsare.

**Automatisk installation**

Det finns två sätt att installera Adobe Experience Manager 6.5.6.0 automatiskt på en fungerande instans:

S. Placera paketet i en `../crx-quickstart/install` mapp när servern är tillgänglig online. Paketet installeras automatiskt.

B. Använd [HTTP API från Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html). Använd `cmd=install&recursive=true` så att kapslade paket installeras.

>[!NOTE]
>
>Adobe Experience Manager 6.5.6.0 stöder inte installation av Bootstrap.

**Validera installation**

1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience Manager (6.5.6.0)` under [!UICONTROL Installed Products].

1. Alla OSGi-paket finns antingen **[!UICONTROL ACTIVE]** eller **[!UICONTROL FRAGMENT]** i OSGi Console (Använd webbkonsol: `/system/console/bundles`).

1. OSGi-paketet `org.apache.jackrabbit.oak-core` är version 1.2.3 eller senare (Använd webbkonsol: `/system/console/bundles`).

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

Information om hur du installerar det kumulativa installationsprogrammet för Experience Manager Forms på JEE och konfigurationen efter distributionen finns i [versionsinformationen för korrigering 0018](jee-patch-installer-65.md).

### UberJar {#uber-jar}

UberJar för Experience Manager 6.5.6.0 finns i [Maven Central-databasen](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.6-1.0/).

Om du vill använda UberJar i ett Maven-projekt ska du läsa [hur du använder UberJar](/help/sites-developing/ht-projects-maven.md) och inkludera följande beroende i projektstrukturen:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.6-1.0</version>  
      <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>Från och med den här versionen finns UberJar och andra relaterade artefakter tillgängliga i Maven Central Repository i stället för i Adobe Public Maven-databasen (repo.adobe.com). Huvudfilen för UberJar har bytt namn till `uber-jar-<version>.jar`. Därför finns det inget värde `classifier`för `apis` -taggen `dependency` som värde.

## Deprecated features {#removed-deprecated-features}

I det här avsnittet visas funktioner som har markerats som borttagna i Experience Manager 6.5.6.0. Funktioner som ska tas bort i en framtida version är först inaktuella, med ett alternativt alternativ att använda.

Kunderna rekommenderas att granska om de använder funktionen eller funktionen i den aktuella distributionen och planera för att ändra implementeringen så att den använder det alternativa alternativet.

| Yta | Funktion | Ersättning |
|---|---|---|
| Integreringar | Skärmen är föråldrad **[!UICONTROL AEM Cloud Services Opt-In]** . Med integreringen av AEM och Target uppdaterades i AEM 6.5 för att stödja Target Standard API, som använder autentisering via Adobe IMS och I/O, och den växande rollen hos Adobe Launch för att instrumentera AEM sidor för analys och personalisering, har guiden för att välja In blivit funktionellt irrelevant. | Konfigurera systemanslutningar, Adobe IMS-autentisering och Adobe I/O-integreringar via respektive AEM-molntjänster. |
| Anslutningar | Adobe JCR Connector för Microsoft SharePoint 2010 och Microsoft SharePoint 2013 är borttagen för AEM 6.5. | Ej tillämpligt |

## Known issues {#known-issues}

* Om du installerar [!DNL Experience Manager] 6.5 Service Pack 5 eller ett tidigare Service Pack på [!DNL Experience Manager] 6.5, tas körningskopian av din anpassade arbetsflödesmodell för resurser (skapad i `/var/workflow/models/dam`) bort.
För att hämta din körningskopia föreslår Adobe att designtidskopian av den anpassade arbetsflödesmodellen ska synkroniseras med körtidskopian med HTTP API:
   `<designModelPath>/jcr:content.generate.json`.

* Kontakta supporten för Adobe om du stöter på problem när du redigerar och skapar överlappande regler i [!UICONTROL Folder Metadata Schema Forms Editor] och [!UICONTROL Metadata Schema Forms Editor] med [!UICONTROL Define Rule] dialogrutan. Observera att reglerna som redan har skapats och sparats fungerar som förväntat.

* Om en mapp i hierarkin byter namn i [!DNL Experience Manager Assets] och den kapslade mappen som innehåller en resurs publiceras [!DNL Brand Portal]i, uppdateras inte mappens rubrik [!DNL Brand Portal] förrän rotmappen publiceras igen.

* När en användare väljer att konfigurera ett fält för första gången i ett adaptivt formulär visas inte alternativet att spara en konfiguration i egenskapsläsaren. Om du väljer att konfigurera ett annat fält i det adaptiva formuläret i samma redigerare åtgärdas problemet.

* Om [!UICONTROL Connected assets configuration] guiden returnerar ett 404-felmeddelande efter installationen måste du installera om `cq-remotedam-client-ui-content` - och `cq-remotedam-client-ui-components` -paketen manuellt med hjälp av pakethanteraren.

* Följande fel och varningsmeddelanden kan visas under installationen av AEM 6.5.x.x:
   * &quot;När Target-integrationen har konfigurerats i AEM med Target Standard API (IMS-autentisering) skapas felaktiga erbjudandetyper när Experience Fragments exporteras till Target. I stället för att skriva&quot;Experience Fragment&quot;/källa&quot;Adobe Experience Manager&quot; skapar Target flera erbjudanden med typen&quot;HTML&quot;/källa&quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Validering på serversidan av adaptiva formulär misslyckas när sammanställningsfunktioner som SUM, MAX och MIN används. CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Aktiveringspunkten i en interaktiv bild i Dynamic Media är inte synlig när du förhandsgranskar resursen via visningsprogrammet för den köpbara kanalen.

## OSGi-paket och innehållspaket som ingår {#osgi-bundles-and-content-packages-included}

Följande textdokument innehåller en lista över de OSGi-paket och innehållspaket som ingår i AEM 6.5.6.0:

* [Förteckning över OSGi-paket som ingår i AEM 6.5.6.0](assets/6560_bundles.txt)

* [Förteckning över innehållspaket som ingår i AEM 6.5.6.0](assets/6560_packages.txt)

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

