---
title: '[!DNL Adobe Experience Manager] 6.5 Versionsinformation om föregående Service Pack.'
description: Versionsinformation för [!DNL Adobe Experience Manager] 6.5 Service Packs.
contentOwner: AK
translation-type: tm+mt
source-git-commit: 22112319b31576d542d04bdc3519795b02db356c
workflow-type: tm+mt
source-wordcount: '14525'
ht-degree: 0%

---


# Programfixar och funktionspaket som ingår i tidigare servicepaket {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## [!DNL Adobe Experience Manager] 6.5.6.0 {#experience-manager-6560}

Adobe Experience Manager 6.5.6.0 är en viktig uppdatering som innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat samt prestanda, stabilitet och säkerhetsförbättringar som släppts sedan den allmänna tillgängligheten av 6.5-utgåvan i **april 2019**. Den kan installeras ovanpå Adobe Experience Manager 6.5.

De viktigaste funktionerna och förbättringarna i Adobe Experience Manager 6.5.6.0 är:

* Publicera eller avpublicera resurser selektivt till antingen [!DNL Experience Manager] eller [!DNL Dynamic Media] med hjälp av [!UICONTROL Quick Publish] eller [!UICONTROL Manage Publication] guide.

* Använd [!DNL Dynamic Media] användargränssnittet för att göra Cachelagrat innehåll i Content Delivery Network (CDN) ogiltigt.

* Publicering av resursavgiftsmappar från Brand Portal till Experience Manager Assets stöds nu även via proxyservern.

* De automatiskt genererade grupperna med privata mappar rensas nu bort när den privata mappen tas bort i [!DNL Experience Manager Assets].

* Beskrivningarna av modifierare i videoförinställningsredigeraren [!UICONTROL Viewer] har uppdaterats i [!DNL Dynamic Media].

* En ny företagsinställning anges för att återspegla status för [!DNL Dynamic Media] kopplingen.

* Standardalternativen för `test` och `aiprocess` uppdateras till `Thumbnail`, från `Rasterize` tidigare versioner i Dynamic Media, för att säkerställa att användarna bara behöver skapa miniatyrbilder och hoppa över sidextraheringen och extraheringen av nyckelord.

* [Fyll i ett anpassat formulär i förväg på klienten](../../help/forms/using/prepopulate-adaptive-form-fields.md#prefill-at-client).

* [Integrering av formulärdatamodell med RESTful API:er på en server med tvåvägs SSL-implementering](../../help/forms/using/configure-data-sources.md).

* [Förbättrad cachning för översatta adaptiva formulärsidor](../../help/forms/using/configure-adaptive-forms-cache.md).

* Stöd för [Adobe Sign-texttaggar i Automated forms conversion Service](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html).

* Stöd för att [konvertera färgade formulär till adaptiva formulär](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html) med [!DNL Automated Forms Conversion service].

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

   *Bild: [!UICONTROL Search for Help] på [!UICONTROL Help] menyn.*

   * Felmeddelandet om ett felaktigt värde anges i [!UICONTROL Impersonate as] fältet under [!UICONTROL User] alternativet och fokus flyttas korrekt till textfältet (NPR-33804).

   ![Användarmeny i sidhuvud](assets/User_aem_header.png)

   *Bild: [!UICONTROL Impersonate as] i [!UICONTROL User] menyn i sidhuvudet.*

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
* Alla konfigurationer visas inte i [Configuration Browser](/help/sites-administering/configurations.md) -gränssnittet (NPR-33644).
* När du trycker på `Esc` **[!UICONTROL User]** tangenten när du söker efter användare som ska personifiera, stängs dialogrutan i stället för användarlistan (NPR-34084).

### Integreringar {#integrations-6560}

* Aktiviteter med långa namn synkroniseras inte med [!DNL Adobe Target] (NPR-34254).

* Om du väljer en egenskap när du skapar en ny konfiguration för Adobe Launch visas följande felmeddelande (NPR-33947):

   ```javascript
   GET http://hostname:Port/libs/cq/dtm-reactor/content/configurations/createcloudconfigwizard/jcr:content/body/items/form/items/wizard/items/general/items/fixedcolumns/items/container/items/general/items/property/data.html?query=&start=0&end=25&imsConfigurationId=Adobe%20Launch&companyId=&_charset_=utf-8 400 (Bad Request)
   ```

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

Efter installation av tilläggspaketet [!DNL Experience Manager Forms] 6.5.6.0:

* Stoppa [!DNL Experience Manager Forms] instansen.

* Ta bort `bcpkix-1.51`-, `bcmail-1.51`- och `bcprov-1.51` JAR-filer från `crx-repository\launchpad\ext` katalogen.

* Ta bort` sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider` egenskapen från `sling.properties` filen.

* Starta om [!DNL Experience Manager Forms] instansen.

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

* När du öppnar fältkonfigurationen för första gången visas inte egenskapsikonen (CQ-4296284).

* Användarna kan redigera inskickningsmetadata, till exempel `afPath``afSubmissionTime` och `signers`när de skickar in ett anpassat formulär. För att lösa problemet tas metadatavärdena bort från informationen om att skicka formulär på klientsidan. Användare kan använda objektet `FormSubmitInfo` för att hämta dessa värden från servern (NPR-33654).

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

## [!DNL Adobe Experience Manager] 6.5.5.0 {#experience-manager-6550}

Adobe Experience Manager 6.5.5.0 är en viktig uppdatering som innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat samt prestanda, stabilitet och säkerhetsförbättringar som släppts sedan den allmänna tillgängligheten av 6.5-utgåvan i **april 2019**. Den kan installeras ovanpå Adobe Experience Manager 6.5.

Några viktiga funktioner och förbättringar som introducerades i [!DNL Adobe Experience Manager] 6.5.5.0 är:

* Anonym åtkomst till CRXDE Lite är inte tillåten. I stället dirigeras användarna till inloggningsskärmen. Se [Utveckla med CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

* Anpassa kolumnnamnen som visas i [!DNL Adobe Experience Manager] Inkorgen.

* Förbättrad tillgänglighet inom olika områden i Experience Manager Web Content Management (WCM), t.ex. sidredigeraren, Core Components, RTE och administratörsgränssnittet.

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
* När du aktiverar källredigeringsalternativet blir det tillgängligt för alternativ för helskärmsvisning, men saknas för redigeringsdialogruta och alternativ för helskärmsvisning i textredigeraren (NPR-32763).
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
* Anonyma användare har tillgång till CRXDE Lite-funktioner (GRANITE-27790).

### [!DNL Assets] {#assets-6550}

>[!IMPORTANT]
>
>Windows-användare av [!DNL Experience Manager desktop app] rekommenderas att uppgradera till [datorprogramversion 2.0.3.2](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html#whats-new-added) för att få åtkomst till DAM-databasen på [!DNL Adobe Experience Manager 6.5.5.0] en instans. Eftersom de kan stöta på problem vid åtkomst till DAM-databasen på [!DNL Adobe Experience Manager] 6.5.5.0-instansen med skrivbordsappens version 2.0.2.

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
>Experience Manager Service Pack innehåller inga korrigeringar för [!DNL Forms]. De levereras med ett separat Forms-tilläggspaket. Dessutom släpps ett kumulativt installationsprogram med korrigeringar för AEM Forms på JEE. Mer information finns i [Installera tillägget](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) Experience Manager Forms och [Installera Experience Manager Forms på JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

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

## Adobe Experience Manager 6.5.4.0 {#experience-manager-6540}

Adobe Experience Manager 6.5.4.0 är en viktig uppdatering som innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat och prestanda, stabilitet, säkerhetsförbättringar som släppts sedan den allmänna tillgängligheten av version 6.5 i **april 2019**. Den kan installeras ovanpå Adobe Experience Manager 6.5.

Några viktiga funktioner och förbättringar i Adobe Experience Manager 6.5.4.0:

* Adobe Experience Manager Assets har nu konfigurerats med Brand Portal via Adobe I/O Console.

* Nu finns ett nytt [Generate Output](../forms/using/aem-forms-workflow-step-reference.md) -steg för Adobe Experience Manager Forms-arbetsflöden.

* [Flerkolumnsstöd](../forms/using/resize-using-layout-mode.md) för layoutläge för adaptiva formulär och interaktiv kommunikation.

* Stöd för [RTF](../forms/using/designing-form-template.md) i HTML5-formulär.

* [Tillgänglighetsförbättringar](new-features-latest-service-pack.md#accessibility-enhancements) i Experience Manager Assets.

* Den inbyggda databasen (Apache Jackrabbit Oak) uppdateras till version 1.10.8.

* Nu kan du synkronisera selektiva underträd till *Dynamic Media - Scene7-läge* i stället för alla tillgängliga på `content/dam`.

* Integrering av formulärdatamodell med SOAP-webbtjänst har nu stöd för urvalsgrupper eller attribut för element.

* SOAP-indata eller -utdata och komplexa datastrukturer har nu stöd för dynamisk gruppersättning.

En fullständig lista över funktioner och viktiga högdagrar som introducerats i de senaste servicepaketen finns i [Nyheter i Adobe Experience Manager 6.5 Service Pack](new-features-latest-service-pack.md).

### Sites {#sites-fixes}

* När en URL för en Adobe Experience Manager Sites-sida innehåller ett kolon (`:`) eller en procentsymbol (`%`) slutar webbläsaren att svara och CPU-användningstoppar (NPR-32369, NPR-31918).

* När en Experience Manager Sites-sida öppnas för redigering och en komponent kopieras, är inklistringsåtgärden inte tillgänglig för vissa platshållare (NPR-32317).

* När guiden Hantera publikation öppnas visas inte ett Experience Fragment som är länkat till en Core-komponent i listorna med publicerade referenser (NPR-32233).

* Översikt över Live-kopian i Touch-gränssnittet tar mycket längre tid än det klassiska användargränssnittet att återge (NPR-32149).

* När servertid och maskintid är i olika tidszoner visar schemalagd publiceringstid servertid i Touch UI, medan datortid visas i Classic UI (NPR-32077).

* Experience Manager Sites kan inte öppna en sida med ett suffix i URL:en (NPR-32072).

* När en användare redigerar ett innehållsfragment återställs en borttagen variant av innehållsfragmentet (NPR-32062).

* Användare kan spara ett innehållsfragment utan att lämna någon information i de obligatoriska fälten (NPR-31988).

* kernel.js och ui.js är inte i förväg ifyllda eller cachelagrade. Det leder till extra tid vid återgivning av sidor (NPR-31891).

* När PageEventAuditListener är aktiverat ökar längden på implementeringskön. Det påverkar prestandan för många verksamheter, t.ex. bulkpublicering, navigering och flyttning av bulktillgångar (NPR-31890).

* När Experience Fragments dras, observeras en hög responstid (NPR-31878).

* När du markerar Drag-komponenten här i platshållaren för ett responsivt rutnät skickas en GET-begäran och begäran resulterar i HTTP 403-fel (NPR-31845).

* När du flyttar innehållet i samma mapp är alternativet för sidflyttning inaktiverat (NPR-31840).

* I strukturläget för redigerbara mallar visas felaktiga resultat i listan över tillåtna komponenter i layoutbehållaren. Endast komponenter med designdialogrutan visas i layoutbehållaren (NPR-31816).

* När en sida har skrivskyddad behörighet för en användare visas alternativet Öppna egenskaper i sites.html, men inte i editor.html (NPR-31770).

* När en användare klickar på knappen Skapa är sidalternativet inte tillgängligt (NPR-31756).

* Det går inte att synkronisera kampanjen i Adobe-kampanjen som innehåller OTB-designimportkomponenten (utanför rutan) (NPR-31728).

* När du försöker ändra en punktlista till en numrerad lista ändras bara de två första punkterna i listan (NPR-31636).

* När en sida inte har skapats och den underordnade noden har valts visas den inledande noden fortfarande i urvalsdialogrutan. När sidan har skapats och användaren klickar på Bläddra, dirigeras sidan om till rotnoden i stället för den redigerade noden (NPR-31618).

* Visningskonfigurationsdialogrutan fungerar inte som den ska för funktionen för anpassning av inkorgen (NPR-32503 och NPR-32492).

* Ett felmeddelande visas när arbetsflödesinformation visas med Inbox (CQ-4282168).

### Assets {#assets-6540-enhancements}

* Knappen som utlöser arbetsflödet på sidan för resurssamling är inaktiverad (NPR-32471).

* En mapp utan namn skapas i SPS (Scene7 Publishing System) när en resurs flyttas från en mapp till en annan i Experience Manager med Dynamic Media Scene7-konfiguration (NPR-32440).

* Åtgärden för att flytta alla resurser (med Markera alla och sedan flytta) till en mapp som innehåller publicerade resurser misslyckas med felet (NPR-32366).

* Återgivningsgenerering för resurser med ${extension} misslyckas (NPR-32294).

* Versionshistorik-URL:er visas under fältet Refererat av på egenskapssidan för resurser (NPR-31889).

* ZIP-filen som hämtas från DAM kan inte öppnas med WinZip (NPR-32293).

* Ursprungliga behörigheter för en mapp uppdateras när mappinställningar öppnas för att ändra mappens titel eller miniatyrbild och sedan sparas (NPR-32292).

* Kalenderikonen för den schemalagda aktiveringen visas inte i statuskolumnen (i Klassiskt användargränssnitt för DAM-tillgångslista) för resurser vars aktivering är schemalagd för ett senare datum och en senare tid (NPR-32291).

* När du skapar fragment med fragmentmallar uppstår ett fel när du söker efter samlingar när fragmentet skapas (NPR-32290).

* Flera sökfrågor utlöses när flera taggar väljs från sökfiltret (NPR-32143).

* Användargränssnittet för Experience Manager-resurser visar trunkerade filnamn när resurser med fler än 50 tecken i filnamnet överförs (NPR-32054).

* Alla kryssrutor på panelen Filter avmarkeras när den första och den andra kryssrutan avmarkeras när du har markerat två kryssrutor i kryssruteträdet i Adobe Stock (NPR-31919).

* Filer- och mappsökning med Omnisearch-ansikten ger undantag (NPR-31872).

* Fältmarkering för obligatoriskt fältval i metadataredigeraren tas inte bort även efter att det obligatoriska fältet har markerats, när beroendereglerna har angetts i motsvarande metadatamatchformulär (NPR-31834).

* Fullständiga namn på taggar på lövnivå (från tagghierarkin) visas inte på egenskapssidan för resurser (NPR-31820).

* Om du använder kommandot back från objektets egenskapssida i webbläsaren Safari uppstår ett fel (NPR-31753).

* Touch UI-sökning (utförd via Omnissearch)-resultatsidan rullar automatiskt upp och förlorar användarens rullningsposition (NPR-31307).

* Assets detail page of PDF assets does not show action buttons except To Collection and Add Rendition buttons in Experience Manager running on Dynamic Media Scene7 run mode (CQ-4286705).

* Resurserna tar för lång tid att bearbeta genom batchöverföringen i Scene7 (CQ-4286445).

* Knappen Spara importerar inte fjärruppsättningen när användaren inte har gjort några ändringar i Set Editor i Dynamic Media Client (CQ-4285690).

* Miniatyrbilden av 3D-resursen är inte informativ när en 3D-modell som stöds har importerats till Experience Manager (CQ-4283701).

* Den obearbetade statusen för visningsförinställningen för smart beskärning visas två gånger på banderolltexten bredvid förinställningsnamnet (CQ-4283517).

* Felaktig behållarhöjd för en överförd 3D-modell som förhandsvisats i 3D-visningsprogrammet visas på objektets informationssida (CQ-4283309).

* Carousel Editor öppnas inte i IE 11 i läget Experience Manager Dynamic Media Hybrid (CQ-425590).

* Tangentbordsfokus fastnar i den nedrullningsbara menyn E-post i hämtningsdialogrutan i webbläsarna Chrome och Safari (NPR-32067).

* Kryssrutan Synkronisera allt innehåll är inte aktiverad som standard när du försöker lägga till DM-molnkonfiguration på Experience Manager (CQ-4288533).

### Foundation UI {#foundation-ui-6540}

* Muskontrollen flyttas till föregående filterfält i stället för att finnas kvar i det befintliga filterfältet när resurser söks med hjälp av filterpanelen (NPR-32538).

* Plattformstaggning: Om du söker efter taggar genom att skriva i taggfälten visas taggar utanför rotgränserna och egenskapen för taggfält respekteras inte (NPR-31895). `rootPath`

* Plattformsgränssnitt: Webbläsaren för sökvägen bryts om en ogiltig sökväg läggs till i textfältet (NPR-31884).

* Meddelande döljs bakom en klistermeny vid sidval (NPR-31628).

### Platform {#platform-sling-6540}

* (HTL) Understrykningar ersätter kolon i sökvägsavsnittet i URL (NPR-32231).

### Projekt {#projects-6540}

* Knappen Skapa är inte synlig för användaren även om användaren har behörighet att skapa projekt i undermappen (NPR-31832).

### Projektöversättning {#projects-translation-6540}

* När ett översättningsprojekt skapas bryts gränssnittet när alternativet Trimma mellanslag aktiveras i `Apache Sling JSP Script Handler` (NPR-32154).

* Fel i användargränssnitt och Null-punktsundantag i felloggar observeras när en tagg, som ska översättas, läggs till i ett översättningsprojekt (NPR-31896).

### Integreringar {#integrations-6540}

* Generering av URL för startbibliotek baseras endast på `path` och `library_name` värden från API:t Launch och är inte baserat på `library_path` värde (NPR-31550).

* Ett felmeddelande visas när LiveFyre-relaterade objekt bearbetas (FYR-12420).

* ReportSuitesServlet är sårbart för SSRF (NPR-32156).

### WCM-mallredigerare {#wcm-template-editor-6540}

* I redigerbart mallstrukturläge visas inte länkknappskomponenten i listan över tillåtna komponenter i layoutbehållaren (CQ-4282099).

### WCM Page Editor {#wcm-page-editor-6540}

* Det uppstod ett fel när en övertäckning skulle markeras och därefter när responsiva rutnätskomponenter skulle markeras här (CQ-4283342).

### Kampanjanpassning {#campaign-targeting-6540}

* Målmolnkonfigurationen misslyckades med felet när mbox-begäran skulle hämtas (CQ-4279880).

### Varumärkesportal {#assets-brand-portal-6540}

* Användare av varumärkesportalen kan inte publicera resurser i mappen för bidrag [!DNL Assets] när de uppgraderar till Adobe I/O på Experience Manager 6.5.4 (CQDOC-15655). Om du vill åtgärda problemet direkt på Experience Manager 6.5.4 rekommenderar vi att du [hämtar snabbkorrigeringen](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041) och installerar den på din författarinstans.

* Popup-värden för metadataschemat visas inte i resursegenskaper (CQ-4283287).

* Delschemat Metadata visar inte tabbar baserade på mimeType i resursegenskaper (CQ-4283288).

* Ett felmeddelande fylls i när metadatamatchemat avpubliceras, även om schemat tas bort vid backend.

* Förhandsvisningsbilden visas inte för en publicerad resurs (CQ-4285886).

* Användaren kan inte publicera eller avpublicera resurser som innehåller ett enkelt citattecken i namnet (CQ-4272686).

* Villkoren visas inte vid hämtning av flera resurser (CQ-4281224).

* Mindre säkerhetsluckor har åtgärdats.

### Communities {#communities-6540}

* Formuläret Skapa medlem visas som en tom sida (NPR-31997).

* Användaren kan inte visa Analytics-rapporten för författarinstansen (NPR-30913).

### Oak-indexering och frågor {#oak-indexing-6540}

* MS Word- och MS Excel-dokument som innehåller JPEG-bilder kan inte tolkas när de tolkas med Tika-tolken, och fel som inte hittas av klassen observeras (NPR-31952).

### Forms {#forms-6540}

>[!NOTE]
>
>Experience Manager Service Pack innehåller inga korrigeringar för Experience Manager Forms. De levereras med ett separat Forms-tilläggspaket. Dessutom släpps ett kumulativt installationsprogram med korrigeringar för Adobe Experience Manager Forms på JEE. Mer information finns i [Installera tillägget](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) Experience Manager Forms och [Installera Experience Manager Forms på JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

* Korrespondenshantering: Bokstäverna visar extra tecken efter överföring för att bokföra processarbetsflöden (NPR-32626).

* Korrespondenshantering: Bokstäverna visar en nedrullningsbar platshållare som en textkomponent efter att de skickats in till arbetsflöden efter bearbetning (NPR-32539).

* Korrespondenshantering: Standardvärdena som definieras i brevmallen visas inte i förhandsvisningsläget (NPR-32511).

* Mobile Forms: Skicka-knappen visas som utökad när ett XDP-formulär återges i en HTML-version (NPR-32514).

* Dokumenttjänster: Problem med URL-åtkomst för brev och vissa andra sidor efter att Service Pack 2 har tillämpats (NPR-32508, NPR-32509).

* Dokumenttjänster: Om antalet transaktioner på en server överstiger en viss gräns misslyckas konverteringen från HTML till PDF och filtypsinställningarna tas bort från [!DNL Forms] servern (NPR-32204).

* Adaptiv Forms: Verktyget Webbläsartillgänglighet rapporterar fel i adaptiva formulär enligt riktlinjerna för WCAG2 Level AA (NPR-32312, NPR-32309, CQ-4285439).

* Adaptiv Forms: Webbläsarhjälpmedelsverktyget i Chrome rapporterar ett fel med bästa praxis (NPR-32310).

* Adaptiv Forms: Översättningsproblem vid konfiguration av ett adaptivt formulär inbäddat på en Experience Manager Sites-sida (NPR-32168).

* Workbench: Ett felmeddelande visas när åtgärden Hämta PDF-egenskaper används för tjänsten PDF Utilities (NPR-32150).

* Dokumentsäkerhet: En skyddad PDF-fil kan inte öppnas offline med alternativet DisableGlobalOfflineSynchronizationData inställt på True (NPR-32078).

* Designer: Om taggningsalternativet är aktiverat försvinner delformulärsramen i den genererade PDF-utdatafilen (NPR-32547, NPR-31983, NPR-31950).

* Designer: Om det finns sammanfogade celler i en tabell misslyckas hjälpmedelstestet för PDF-utdatafilen som konverterats från ett XDP-formulär med hjälp av utdatatjänsten (CQ-4285372).

* Foundation JEE: Om en Experience Manager Forms-server är frånkopplad från ett kluster kan cachelagring förhindra att den återansluter till servern (NPR-32412).

## Adobe Experience Manager 6.5.3.0 {#experience-manager-6530}

[!DNL Adobe Experience Manager] 6.5.3.0 är en viktig version som innehåller prestanda, stabilitet, säkerhet och viktiga kundkorrigeringar och förbättringar som släppts sedan den allmänna tillgängligheten av 6.5-utgåvan i **april 2019**. Den kan installeras ovanpå [!DNL Adobe Experience Manager] 6.5.

Några viktiga höjdpunkter i den här Service Pack-versionen är:

* Den inbyggda databasen (Apache Jackrabbit Oak) uppdateras till version 1.10.6.

* [!DNL Experience Manager Assets] har nu stöd för ZIP-arkiv som skapats med algoritmen Deflate64.

* Ny kolumn för skapat datum, som är sorterbar, har lagts till i DAM-listvyn och i resurssökningsresultat i listvyn.

* Resurssortering baserad på namnkolumnen har aktiverats i listvyn.

* [!DNL Dynamic Media] har nu stöd för videomaterial för Smart Crop. Smart Crop är en maskininlärningsdriven funktion som återbeskär en video medan bildrutan flyttas för att följa scenens fokuspunkt.

* [!DNL Dynamic Media] har stöd för Smart Imaging.

* Möjlighet att [ange inställningar för frånvaro](../forms/using/configure-out-of-office-settings.md) i [!DNL Experience Manager] arbetsflöden.

* Möjlighet att [dela inkorgs- eller inkorgsobjekt](../forms/using/configure-shared-queues-osgi.md) med andra användare i [!DNL Experience Manager] arbetsflöden.

* Möjlighet att [generera interaktiv kommunikation i batchläge](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

* Uppdaterad version av jQuery som paketerats i ContextHub till 3.4.1.

### Assets {#assets-6530-enhancements}

**Produktförbättringar**

* [!DNL Experience Manager Assets] har nu stöd för ZIP-arkiv som skapats med algoritmen Deflate64 (NPR-27573).

* Ny kolumn för skapat datum, som är sorterbar, läggs till i DAM-listvyn och i resurssökningsresultat i listvyn (NPR-31312).

* I listvyn kan användare sortera listan med resurser med hjälp av [!UICONTROL Name] kolumnen (NPR-31299).

* GLB-, GLTF-, OBJ- och STL-filerna kan förhandsgranskas på [!UICONTROL Asset Details] sidan i DAM (CQ-4282277).

* `ReplicationOnModifyListener` -händelsen utlöses för segmentnoder under segmentöverföring i [!DNL Dynamic Media] (CQ-4281279).

* [!DNL Dynamic Media] har nu stöd för videomaterial för Smart Crop. Smart Crop är en maskininlärningsdriven funktion som återbeskär en video samtidigt som bildrutan flyttas för att följa scenens fokuspunkt (CQ-4278995).

* [!DNL Dynamic Media] har stöd för Smart Imaging (CQ-422249).

* Vyn Sök eller Bläddra anges som standardvy i Foundation-väljaren om frågeparametrar skickas i begäran (NPR-31601).

**Korrigeringar**

* Metadata för vissa PDF-dokument uppdateras inte och sparas i PDF-filen när titeln ändras (NPR-31629).

* Resursdelning fungerar inte för en resurs som har plustecken (`+`) i filnamnet (NPR-31547).

* Redigeringar i standardsökformuläret Resurser Admin Search Rail fungerar inte som förväntat (NPR-31502).

* Förslag visas inte när du använder Omnissearch on assets view för att söka efter resurser (NPR-31496).

* Resursreferenser i samlingar uppdateras inte när de refererade resurserna flyttas till en annan plats, om samma resurser refereras till av olika samlingar av olika användare (NPR-31486).

* Duplicerade IPTC-taggar läggs till i metadata för resurser (NPR-31328).

* Antalet sökresultat uppdateras inte korrekt när en sökning utlöses från filterfältet (NPR-31316).

* Alla kryssrutor är avmarkerade när kryssrutorna på den andra nivån avmarkeras i filtypsfiltret, och texten i sökfältet är inte synkroniserad med de markerade eller avmarkerade egenskaperna (NPR-31287).

* Det går inte att ta bort alla medlemmar (användare/grupper) från en mapps medlemsdel. När användaren försöker ta bort alla användare läggs den inloggade användaren till i listan (NPR-31171).

* Resurser med plustecken (`+`) i filnamnet kan inte tas bort (NPR-31162).

* Menyn Skapa, som visas på den övre menyn när du väljer en mapp, visar inte &quot;Mapp&quot; som ett alternativ för att skapa (NPR-30877).

* Mappval Skapa > FileUpload-åtgärdsobjekt saknas när ACL för Neka `jcr:removeChildNodes` och `jcr:removeNode` på sökväg tillämpas för en användare (NPR-30840).

* DAM-arbetsflöden försätts i viloläge när vissa mp4-resurser överförs, vilket gör att alla återstående arbetsflöden försätts i viloläge (NPR-30662).

* Slut på minne uppstår när stora PDF-filer (av flera gigabyte) överförs till DAM och dess underresurser bearbetas (NPR-30614).

* Massförflyttning av resurser misslyckas och ett varningsmeddelande visas (NPR-30610).

* Resursnamn ändras till gemener när du flyttar resurser från en mapp till en annan i [!DNL Experience Manager] läget [!DNL Dynamic Media]-Scene7 (NPR-31630).

* Ett fel uppstod när en fjärrbilduppsättning redigerades för bilden i mappen som heter samma som Scene7 företagsnamn (NPR-31340).

* [!DNL Dynamic Media] resurser som innehåller referenser publiceras inte (NPR-31180).

* Överföringar från [!DNL Dynamic Media]7-Scene7 till [!DNL Dynamic Media Classic] tar för lång tid att slutföra (NPR-31048).

* Aktiveringspunkten som läggs till i en bildresurs är inte synlig via Interactive Image Viewer på sidan med resursinformation (NPR-30979).

* Enorma snedningsjobb skapas och Bearbetningsbanderollen visas igen när åtgärder som utförs på resurser i [!DNL Experience manager Assets] skickas till Scene7 (NPR-30947).

* En konflikt uppstår när du skapar en språkkopia av resurser och resurser inte överförs till Scene7 (NPR-30932).

* Dynamiska återgivningar som hämtats från [!DNL Experience Manager] att ha [!DNL Dynamic Media]Hybrid-läge är brutna (de är av texttyp med innehållet&quot;det går inte att hitta bilden&quot; i stället för bildinnehållstypen) (NPR-30876).

* [!DNL Dynamic Media] Arbetsflödet för kodning av video kan inte generera miniatyrbilder för den video som migreras från [!DNL Dynamic Media Classic] till [!DNL Dynamic Media]Scene7-läge i Adobe Experience Manager (CQ-4282011).

* IpsApiException observerades när resurser migrerades från en instans till en annan med olika Scene7-företags-ID:n (CQ-4280548).

* Miniatyrbilden av 3D-resursen är inte informativ när en 3D-modell som stöds har importerats till [!DNL Experience Manager] (CQ-4283701).

* Rullningsknappar visas i visningsprogrammet om en 3D-resurs har få kameravinklar (CQ-4283322).

* Felaktig behållarhöjd för en överförd 3D-modell som förhandsvisats i DimensionalViewer på sidan Resursinformation (CQ-4283309).

* Videor kan inte spelas upp med SmartCropVideoViewer i Internet Explorer 11 och Safari (CQ-4281422).

* Om du använder flyttningsknappen för att flytta flera resurser, från en mapp till en annan, går det inte att [!DNL Experience Manager] köra i [!DNL Dynamic Media]-Scene7 (CQ-4280384).

* Förvrängd video visas i resursinformation när MIME-typen är en annan än MP4 (CQ-4279704).

* Videoklipp som nyligen har infogats i mappar med en videoprofil är fortfarande i bearbetningstillstånd även när kodens procenttal har slutförts till 100 % (CQ-4279389).

* När du flyttar resurser från en mapp skapas ett stort antal snedstreck (Scene7 API-anrop) än vad som helst krävs (CQ-4278664).

* Namn på bilduppsättningen ändras till gemener i Scene7 när bilduppsättning (eller mediaset) skapas och namnges med lämplig namnkonvention i DAM (CQ-4281112).

* Scene7 Migrator anger felaktigt publiceringstillstånd (CQ-4263492).

* Touch UI-sökning (utförd via Omnissearch)-resultatsidan rullar automatiskt upp och förlorar användarens rullningsposition i innehållsfragment (CQ-4282898).

* PDF-filer är inte indexerade och innehållet i dem är inte sökbart (CQ-4278916).

* Felmeddelandet&quot;Grupp visas inte av användarväljaren: false förväntas vara lika med true&quot; visas när en stängd användargrupp läggs till med ett annat värde `principalName` och `authorizableId` (CQ-4278177).

* Resursens gränssnittskolumnvy visar alla sökvägar oavsett vilken sökväg en klientorganisation har (CQ-4278175).

* Resursväljarens sökning fungerar inte som förväntat (CQ-4275886).

* Återgivningsarbetsflöden misslyckas (CQ-4271928).

* DAM-händelsetömning tar bort de senaste (`maxSavedActivities`) händelsedata och lagrar data som skapats tidigare (NPR-31336).

* Touch UI-sökning (utförd via Omnissearch)-resultatsidan rullar automatiskt upp och förlorar användarens rullningsposition (NPR-31307).

* Åtgärdsfältet och antalet resurser uppdateras inte när du markerar alla och sedan avmarkerar vissa objekt (mappar/enskilda resurser) i Touch UI (NPR-3118).

* Ett undantag visas i [!DNL Experience Manager] vid avsökning efter jobbinformation för en resurs (CQ-4283569).

### Sites

* Om LiveCopy-arvet bryts visas länkar för språkkopiering i stället för länkar för LiveCopy (NPR-30980).
* Om antalet poster är fler än 40 visas bara de första 40 posterna för en ny utkast. I utkast visas tomma rader för resten av posterna (NPR-31182).
* När en användare lägger till japanska eller koreanska tecken i egenskapen description på en meny visas förvrängda tecken för japansk och koreansk text på menyn (NPR-31331).
* Det går inte att infoga en inbäddad tabell som listobjekt (NPR-30879) i RTF-redigeraren.
* När du har gjort en avskalning av RTF-redigerare (Rich Text Editor). använder textbunden teckensnittsstorlek för element, oväntat (NPR-31284).
* När en användare fokuserar på fält med vänster stödlinje och använder ett kortkommando för att klistra in innehåll, klistras innehållet i sidredigerarens urklipp in i stället för innehållet som kopieras från de vänstra fältspåren (NPR-31172).
* När en användare lägger till ett filöverföringsfält i ett flerfält lagras bildsökvägen i komponentnoden i stället för i flerfältsnoden (NPR-30882).
* API:t `ResponsiveGridExporter` returnerar inte `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` gränssnittet. Paketet `com.day.cq.wcm.foundation.model.impl` deklareras som ett privat paket (NPR-31398).

<!-- Review: NPR-31398 has fixVersion as 6530. However, it is mentioned twice in 6530 and 6520 as fixed. 
Remove one mention of this fix.
-->

* När en sida som innehåller vissa Experience Fragments öppnas i icke-redigerarläge (antingen i Författare utan prefixet och `editor.html` , eller i Utgivare), avslutas begäran med HTTP-statusfelkoden `wcmmode=disabled``500` (NPR-30743).
* Användare kan inte ändra sitt lösenord och komma åt sin profilsida (NPR-31161).

### Sök- och användargränssnitt {#ui-interface-and-search}

* När du växlar från kortvyn till listvyn på en sökresultatsida uppstår en fördröjning innan sidan kan rullas (NPR-31286).

* Kryssrutan är [!UICONTROL Select All] dold i listvyn i [!DNL Sites] användargränssnittet (NPR-31614).

* Antalet [!UICONTROL Select All] på en sökresultatsida är felaktigt (NPR-31120).

* I metadataredigeraren visas taggar som inte finns (NPR-31119).

### Översättning {#translation}

* Två popup-fönster visas när du väljer alternativet Förfallodatum i ett översättningsjobb (NPR-31270).

### Plattform

* Alternativet Mime-typ i webbkonsolen fungerar inte (NPR-31108).

* Klientcertifikatet accepteras inte när enkel inloggning konfigureras (NPR-31165).

* Uppdateringar i buffertstorlekskonfigurationen för Jetty-baserad HTTP-tjänst sparas inte (NPR-30925).

* QueryBuilder har nu stöd för orderby `fn:name()` i XPath-frågor (NPR-31322).

* Dubblettaktiveringsträdet skapas vid uppgradering från [!DNL Experience Manager] 6.3 (NPR-31513).

* Vidarebefordrade begäranden bevarar inte svarshuvuden som ställs in vid slingautentisering (NPR-30013).

* Det går inte att söka i väljarkomponenterna (NPR-31692).

* Ett fel visas när en ZIP-fil bifogas till ett [!DNL Experience Manager Communities] inlägg på grund av olika versioner av Apache POI- och Apache Tika-paketet (NPR-31018).

* Paketet är dolt i konfigurationshanteraren och är därför inte tillgängligt för anpassade paket (NPR-31720). `org.apache.sling.distribution.api`

### Projekt

* Det går inte att växla kalendervyer (NPR-31271).

### Varumärkesportal {#assets-brand-portal-6530}

**Produktförbättringar**

* Arbetsflödet för import av mediekällor i [!DNL Experience Manager Assets] ändras så att endast de nyskapade resurserna hämtas från [!DNL Brand Portal] till [!DNL Experience Manager], och de resurser som redan finns i mappen NEW hoppas över för att undvika replikering (CQ-4278527).

**Korrigeringar**

* En felaktig ikon visas när en ny Contribute-mapp skapas i funktionen Resurser (CQ-4282825).
* När du skapar en ny Contribute-mapp visas inte en eller båda undermapparna (NYTT och DELAT) i Contribute-mappen (CQ-4282424).
* Systemet genererar ett undantag om användaren försöker publicera om Contribute-mappen från [!DNL Experience Manager] till [!DNL Brand Portal] efter att ha tagit emot nya resurser i Contribute-mappen från [!DNL Brand Portal] slutet (CQ-4279740).
* Det är inte tillåtet att skapa en Contribute-mapp i en Contribute-mapp (kapslad mapp) för att undvika komplexitet (CQ-4278391).
* Systemet genererar ett undantag när användarlistan (.csv-fil) som [!DNL Brand Portal] importeras från [!DNL Experience Manager] Admin Console överförs. Endast fälten Email, FirstName och LastName i CSV-filen är obligatoriska (CQ-4278390).

### Communities {#communities-6530}

**Korrigeringar**

* Snabblänkar för att hantera grupper (Öppna/Redigera/Publicera/Ta bort grupper) är inte synliga för communityadministratörer (Gruppadministratör/Webbplatsadministratör) (NPR-31627).
* En inskickad blogg visas bara om sidan uppdateras/läses in manuellt (NPR-31599).
* JCR-frågan som används av funktionen &quot;Mentions&quot; är skiftlägeskänslig och tar för lång tid att returnera resultaten (NPR-31475).
* [!DNL Experience Manager] 6.5 UberJar-filen genererar ett undantag, paket saknas i `cq-social-translation` [!DNL Experience Manager] 6.5 UberJar-filen (NPR-31186).
* Jackson Database-bibliotek uppdaterade till version 2.9.9.3 för att åtgärda nya säkerhetsluckor (NPR-30967).
* Aktiviteter och meddelandetitlar är inkonsekventa (NPR-30941).
* Sidindelningen fungerar inte korrekt i [!DNL Communities] bloggar (NPR-30914).
* Analysrapporter fylls inte i i [!DNL Experience Manager] författarmiljön. En tom sida visas (NPR-30913).

### Oak {#oak}

* Uppdateringar av Lucene-index gör att författarservern sinkas (NPR-31548).

### Forms {#forms-6530}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack innehåller inga korrigeringar för [!DNL Experience Manager Forms]. De levereras med ett separat Forms-tilläggspaket. Dessutom släpps ett kumulativt installationsprogram som innehåller korrigeringar för [!DNL Experience Manager Forms] JEE. Mer information finns i [Installera tillägget](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) Experience Manager Forms och [Installera Experience Manager Forms på JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

#### Forms tilläggspaket {#forms-add-on-package-6530}

**Adaptiv Forms**

* Strängar innehåller ordlistenyckeln när adaptiva former lokaliseras (NPR-31110).

**Interaktiv kommunikation**

* **MissingNode.toString()** returnerar felaktiga resultat efter uppgradering av Jackson-bibliotek till 2.10.0 (NPR-31549).

* Textredigeraren tar slumpmässigt bort blankstegstecken från text som kopieras från Microsoft Word (NPR-31113).

**Korrespondenshantering**

* Bildtexter och verktygstips visas inte när bokstäver migreras från LiveCycle ES4SP1 till [!DNL Experience Manager] 6.5 (NPR-31615).

* **Textflödesformatering stöds** inte längre i felmeddelanden när bokstäver sparas som utkast (NPR-30463).

**Arbetsflöde**

* OSGi-arbetsflödet misslyckas på grund av 100 % processoranvändning (NPR-31233).

**HTML5 Forms**

* När du genererar HTML5-förhandsgranskning av ett XDP-formulär visas ett flimmer när instanser av ett delformulär läggs till (NPR-30909).

#### Forms på JEE-installationsprogram {#forms-jee-installer-6530}

**Forms - dokumenttjänster**

* SOAP-webbtjänst som använder MTOM i ett .NET-projekt visar undantag för AssemblerServiceClient-anrop och HTMLToPDF2-metoder (NPR-4281771).

* Säkerhetsluckan 2012-5784 och 2014-3596 har hittats med AXIS 1.4 jar och korrigeringen finns i [AXIS1.4.1 jar](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0014.html) (NPR-31015).

**Foundation JEE**

* Åtgärdskonfigurationen läser inte in processnamnen för åtgärden Anropa en Forms Workflow skicka (NPR-31478).

### Funktionspaket ingår {#feature-packs-included-6530}

>[!NOTE]
>
>För [!DNL Experience Manager Forms] kunderna är det viktigt att installera [!DNL Experience Manager Forms] tilläggspaket efter installation av [!DNL Experience Manager] Service Pack, Cumulative Fix Pack eller Feature Pack.

#### Forms - Foundation JEE {#forms-foundation-jee-feature}

* [!DNL Experience Manager] Forms-stöd för Oracle 18c (NPR-29155).

## Adobe Experience Manager 6.5.2.0 {#experience-manager-6520}

[!DNL Adobe Experience Manager] 6.5.2.0 är en viktig version som innehåller prestanda, stabilitet, säkerhet samt viktiga kundkorrigeringar och förbättringar som släppts sedan den allmänna tillgängligheten av [!DNL Adobe Experience Manager] 6.5 i **april 2019**. Den kan installeras ovanpå [!DNL Experience Manager] 6.5.

Några viktiga höjdpunkter i den här Service Pack-versionen är:

* Den inbyggda databasen (Apache Jackrabbit Oak) uppdateras till version 1.10.3.
* En konfigurationsegenskap har lagts till som tillåter export av Experience Fragments direkt till användardefinierade arbetsytor för [!DNL Adobe Target].
* Resurser som användare kan söka efter visuellt liknande bilder. [!DNL Experience Manager] visar smarta taggade bilder från DAM-databasen som liknar den användarvalda bilden. Se [visuell sökning](../assets/search-assets.md#visualsearch).

* Förbättrade funktionerna för anslutna resurser för att lägga till stöd för att hämta dokument från DAM-fjärrdistributioner. Webbplatsförfattare kan nu söka efter och filtrera dokumenttyper som stöds i Content Finder. Fjärrdokumenten kan läggas till i komponenten Download på webbsidor. Se [Använda anslutna resurser](../assets/use-assets-across-connected-assets-instances.md).

* Förbättra dokumenttypsfilter med fler MIME-typer som stöder flervärdesalternativ.
* Ett externt arbetsflöde för ombearbetning har introducerats för stöd för flera resurser.
* Optimerade [!DNL Dynamic Media] prestanda genom att använda standardresursfilter för replikering.
* Återställt redigeringsalternativ för beskärning/rotering av resurser för DMS7.
* Implementerade ett alternativ för att stänga av ljudet för en video vid inläsning i VideoPlayer.
* Åtgärda problemet så att kolumnvyn i resursanvändargränssnittet bara visar innehåll som är specifikt för innehavaren.
* Korrigera så att formatdragspelsändringar återspeglas i sökresultaten.

### Assets

**Produktförbättringar**

* Förbättrade funktionerna för anslutna resurser för att lägga till stöd för att hämta dokument från DAM-fjärrdistributioner. Webbplatsförfattare kan nu söka efter och filtrera dokumenttyper som stöds i Content Finder. Fjärrdokumenten kan läggas till i komponenten Download på webbsidor. Programfix för CQ-4270245. Se [Använda anslutna resurser](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Experience Manager Assets] -användare kan söka visuellt liknande bilder. [!DNL Experience Manager] visar smarta taggade bilder från DAM-databasen som liknar den användarvalda bilden. Se [visuell sökning](../assets/search-assets.md#visualsearch).

**Korrigeringar**

* Resurssökvägar i URL:er och mappmetadata som genereras av AVS-API:t är inte URL-kodade. GRANITE-26198: Programfix för CQ-4271814
* Det går inte att öppna ett arkiv med en mapp som har ett procenttecken (%) i namnet med hjälp av [!DNL Experience Manager Assets] gränssnittet. NPR-29989: Programfix för CQ-4270467
* Pekgränssnitt: Under guiden Hantera publicering läggs referenser till efter sidan i postbegärandetexten, vilket gör att alla resurser publiceras efter sidan, och när sidan återges missas en del av resurserna i publiceringsinstansen. NPR-29985: Programfix för CQ-4270724
* Funktionen för att ta bort kopplingar till resurser fungerar inte för relaterade resurser som har specialtecken (tecken som blir URI-kodade) i namnet. NPR-30387: Programfix för CQ-427446
* När du redigerar ett innehållsfragment skapas versionen med fel användare.
* Ett fel uppstod när samlingar skapades i ett klientbaserat system. NPR-30114: Programfix för CQ-4272948
* Resursgränssnittskolumnvyn respekterar inte den aktuella klientens dam-root-sökväg, men använder alla tenant-dammsökvägar. NPR-30636: Programfix för CQ-4275481
* Möjlig XSS-attack (cross-site scripting) via ett begränsat varningsfönster eftersom den injicerade bilden kan ses. NPR-30617: Programfix för CQ-4270133
* MultiTenant: Innehavare som sparar mappegenskaper observerar både meddelande om att åtgärden lyckades och felmeddelande som beskriver åtgärden misslyckades:&quot;Det går inte att redigera egenskaper. Otillräckliga behörigheter.&quot; och förvirrar dem. NPR-30545: Programfix för CQ-4275333
* Dialogrutan Resursväljare tillåter inte val av resurs och kan därför inte uppdatera källan med hjälp av funktionen för relaterat källbyte. NPR-30502: Programfix för CQ-4275029
* [!UICONTROL DAM Update Asset] arbetsflöde - I inaktuellt läge vid överföring av stora mp4-filer. NPR-30480: Programfix för CQ-4271352
* Funktionen Skapa granskningsaktivitet fungerar inte på grund av null-nyttolast, vilket gör att alla efterföljande granskningsåtgärder misslyckas. NPR-30468: Programfix för CQ-4274263
* Anslutningsproblem med Adobe Smart Tag via DataPower. NPR-30026: Programfix för CQ-4269457
* Resursens användargränssnittskolumnvy genererar ett fel vid försök att öppna filtren från listen. NPR-30501: Programfix för CQ-4273862
* När du lägger till grupper som synkroniserats från LDAP i CUG-egenskaperna (Closed User Group) för en resursmapp, sparas och hämtas inte gruppen. NPR-30615: Programfix för CQ-4274689
* Filtersökningsformat och orienteringsfält använder inte det automatiskt ifyllda värdet på sökfrågan. NPR-30620: Programfix för CQ-4275724
* Resursresurslänken i en mapp med blanksteg och tecknet &quot;&amp;&quot; i namnet visar tomma grå kort för vissa resurser. NPR-30557: Programfix för CQ-4270187
* Schemaformuläret för mappmetadata identifierar inte automatiskt datatyp och skapar därför inte den relaterade TypeHint-typen när formuläret skickas. NPR-30599: Programfix för CQ-4275227
* Alternativen för att beskära och rotera resurser är inaktiverade i DMS7-redigeringsgränssnittet. NPR-30118: Programfix för CQ-4273221
* Funktionen Dela länk fungerar inte på [!DNL Experience Manager] instanser med DMS7-konfiguration. NPR-30080, NPR-30492: Programfix för CQ-4273651
* Om du lägger till [!DNL Dynamic Media]-Scene7-komponenten på sidan och sedan publicerar sidan aktiveras inte dmscene7-konfigurationen varje gång. NPR-30641: Programfix för CQ-4275962
* Lade till en IPSJobJournal i [!DNL Experience Manager] för att skapa endast ett IPS-jobb (Intrusion Prevention Systems) per bearbetningsprofil. NPR-30490: Programfix för CQ-4273614
* [!DNL Dynamic Media]: Lagt till standardfilter för att utesluta resurser från replikering till [!DNL Experience Manager] publiceringsnoden. NPR-30538: Programfix för CQ-4274678
* Ett externt arbetsflöde för ombearbetning har introducerats för stöd för flera resurser så att mappen kan användas som nyttolast. Arbetsflödet består av två steg: ombearbetar resurser utan handtag via metadatamappning till nästa steg och överför alla resurser utan resurshandtag till S7 i ett enda IPS-jobb. Mer information finns i Konfigurera [!DNL Dynamic Media] Cloud Services. NPR-30489: Programfix för CQ-4272903
* När du laddar upp en felaktig CSV-fil efter att du korrigerat CSV-filen raderas den korrekta CSV-filen. Programfix för CQ-4277694, CQ-4277814
* Den felaktiga ikonen som är specifik för de bidragsmappar som ska tas bort. Programfix för CQ-4277580
* När du väljer en användare i användarväljaren på fliken Resursbidrag visas inte användarens namn i tabellen och dialogrutan Ta bort användare på egenskapssidan visar fel text. Programfix för CQ-4277875
* Medarbetare kan inte läggas till i resursavgiftsmappen från användarväljaren genom att markera användare och klicka på Lägg till. Programfix för CQ-4277824, CQ-4278087
* Det går inte att söka efter användarnamn med gemener i användarväljaren. Programfix för CQ-4277958, CQ-4277930
* Icke-administratörer kan publicera resurser i en ny mapp i en resursavgiftsmapp. Programfix för CQ-4278200
* dam-user (icke-admin) har inte möjlighet att lägga till medarbetare i resursavgiftsmappen. Programfix för CQ-4278192
* Knappen&quot;Skapa&quot; visas i mappen Resursbidrag. Programfix för CQ-4277560
* Om du sorterar sökfrågan efter relevans returneras [!DNL InDesign] dokument tillsammans med [!DNL InDesign] mallar. Programfix för CQ-4273864
* Om användaren har ett e-post-ID med versaler kan användarna inte checka in de resurser som tidigare har checkats ut. Programfix för CQ-4276575
* Åtgärden Ta bort gäller bara för de förinställningar som är markerade, och om skärmen automatiskt uppdaterar listan efter åtgärden visas andra förinställningar som redan har uppdaterats. Programfix för CQ-4261461
* Om du konfigurerar [!DNL Dynamic Media] Cloud Services i [!DNL Dynamic Media]hybrid-läge skapas flera tomma rapportsviter i [!DNL Analytics]och inget rapportsuite-id sparas i [!DNL Experience Manager], vilket resulterar i duplicering av rapportsviten. Programfix för CQ-4249780
* Det går inte att synkronisera namnbytet i [!DNL Experience Manager] resursen till det duplicerade namnet till Scene7. Programfix för CQ-4276763
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

* Om LiveCopy-arvet bryts visas länkar för språkkopiering i stället för länkar för LiveCopy (NPR-30980).
* Om antalet poster är fler än 40 visas endast de första 40 posterna för en ny utkast. I utkast visas tomma rader för resten av posterna (NPR-31182).
* Plugin-programmet RTE (Rich Text Editor) för textkomponenten visar förvrängda tecken för japansk och koreansk text (NPR-31331).
* Det går inte att infoga en inbäddad tabell som listobjekt (NPR-30879) i RTF-redigeraren.
* Vid skalning av RTF-redigerare (Rich Text Editor) används teckensnittsstorleken för element, oväntat (NPR-31284).
* När en användare fokuserar på fält med vänster stödlinje och använder kortkommando för att klistra in innehåll, klistras innehållet i sidredigerarens urklipp in i stället för innehållet som kopieras från fält med vänster stödlinje (NPR-31172).
* När en användare lägger till ett filöverföringsfält i ett flerfält lagras bildsökvägen i komponentnoden i stället för i flerfältsnoden (NPR-30882).
* API:t `ResponsiveGridExporter` returnerar inte `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` gränssnittet. Paketet `com.day.cq.wcm.foundation.model.impl` deklareras som ett privat paket (NPR-31398).
* När en sida som innehåller vissa Experience Fragments öppnas i icke-redigerarläge (antingen i redigeringsläge utan `editor.html` prefix och `wcmmode=disabled`, eller i Publisher), avslutas begäran med HTTP-statusfelkod 500 (NPR-30743).

### WCM - sidredigeraren {#wcm-page-editor-6520}

**Produktförbättringar**

* Förbättra dokumenttypsfilter med fler MIME-typer som stöder alternativ med flera värden. Programfix för CQ-4270694

### Hantering av innehållsfragment {#content-fragment-management-6520}

* Frågan som används av gränssnittet för modeller för innehållsfragment är mycket långsam och resulterar till slut i ett fel. Programfix för CQ-4270807

### UI - Foundation {#ui-foundation}

* Kortkommandon som utlöser ett fel som gör att användaren inte kan använda &#39;m,&#39; &#39;p,&#39; &#39;e&#39; i ett visst användargränssnitt. NPR-30355: Programfix för GRANITE-26346
* När du stänger [!DNL Experience Manager Assets] sökgränssnittet återställs inte den vänstra listen till Innehållsval, vilket förhindrar användaren från att öppna filterfältet andra gången. NPR-30509: Programfix för CQ-4274716
* Flerklientmiljö: [!DNL Experience Manager Assets] Gränssnittets övre navigering är inte tillgänglig och orsakar JavaScript-fel. NPR-30104: Programfix för GRANITE-26344

### Översättning {#translation-6520}

* Översättningsproblem - Endast ett fåtal komponenter översätts med maskinöversättning. NPR-30079: Programfix för CQ-4273764

### Platform {#platform-6520}

* [!DNL Experience Manager] Standardavsändaren för e-post kan inte skicka e-post till en SMTP-fjärrserver via TLS v1.2. NPR-30476: Programfix för GRANITE-26605

### Projekt {#projects-6520}

* dam:folderThumbnailPaths-värden uppdateras inte och gamla miniatyrer visas inte ens när resurserna i mappen har tagits bort. NPR-30424: Programfix för CQ-4273667
* När du slutför flyttalternativet ändras inte resursens namn och namn. NPR-30647: Programfix för CQ-4276265

### Communities {#communities-6520}

* Diagnostik för användarsynkronisering är helt bruten och fungerar inte. NPR-30004, NPR-29943: Programfix för CQ-4270287, CQ-4271348

### Sling {#sling}

* Uppgraderade instanser från 6.3.3.2 till 6.5 resulterar i duplicerade OSGi-konfigurationer. NPR-30130: Programfix för CQ-4274016

### Integrering

* Det anpassade innehållet visas inte korrekt på publiceringsinstansen förrän instansen startas om. NPR-30377: Programfix för CQ-4273706
* När du konfigurerar Launch på en webbplats har biblioteksadressen ett snedstreck (/) som är förinställt, vilket ger manuella åtgärder varje gång. NPR-30694: Programfix för CQ-4275501

### Forms {#forms-6520}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack innehåller inga korrigeringar för [!DNL Experience Manager Forms]. De levereras med ett separat [!DNL Forms] tilläggspaket. Dessutom släpps ett kumulativt installationsprogram som innehåller korrigeringar för [!DNL Experience Manager Forms] JEE. Mer information finns i [Installera tillägget](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) Experience Manager Forms och [Installera Experience Manager Forms på JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

Viktiga högdagrar för [!DNL Experience Manager] 6.5.2.0-formulär är:

* Inställningen Auto har lagts till `RenderAtClient` i `PDFFormRenderOptions` API:t för [!DNL Experience Manager] Forms OSGi.

#### Forms tilläggspaket

**Integrering med back end**

* Det går inte att konfigurera formulärdatamodellen med en värdbaserad, belastningsutjämnad URL. NPR-30123: Programfix för CQ-4273359
* När formulärdatamodellen (FDM) skapas med WSDL (Web Service Definition Language) `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type` returneras felmeddelandet: NPR-30477: Programfix för CQ-4272921

**Korrespondenshantering**

* &quot;Återgivningen av CCR-gränssnittet (Create Correspondence UI) misslyckas ibland med följande fel i konsolen:
   `- Uncaught Error: variable [object Object]is already known the letter`- NPR-30127

**Interaktiv kommunikation**

* Ett fält som är markerat som obligatoriskt i formulärdatamodellen visas enligt kraven i användargränssnittet för Skapa korrespondens (CCR UI). NPR-30623: Programfix för CQ-4274902

**Forms - arbetsflöde**

* Omappade utdatavariabler i Bevakade mappar gör att anropet misslyckas. Programfix för CQ-4264451

**HTML5 Forms**

* När den anpassade koden eller projektet distribueras för andra gången återges inte sidan och följande fel inträffar:

   `org.apache.sling.scripting.sightly.SightlyException.`

   NPR-30539: Programfix för CQ-4272509

* När du använder NonVisual Desktop Access i bläddringsläge för att läsa ett HTML5-formulär, läser webbläsaren Chrome &quot;graphic&quot; före varje Scalable Vector Graphic (SVG) i formulärdesignen. NPR-30449: Programfix för CQ-4274732

#### Forms JEE-installationsprogram

**Forms - dokumentsäkerhet**

* Det går inte att använda en signatur med tidsstämpel. Fel: ALC-DSC-003-000: com.adobe.idp.dsc.DSCInvocationException: Anropsfel. NPR-30820: Programfix för CQ-4275852

**Forms - dokumenttjänster**

* Om &quot;SubmitURL&quot; innehåller ett et-tecken (&amp;), visas tolkningsfel i loggen när en begäran om POST görs till renderpdf-servern. NPR-30865: Programfix för CQ-4278232

**Forms - Foundation JEE**

* HTMLtoPDF-tjänsten visar inte maxReuseCount i JMX-konsolen. NPR-30134, NPR-30304: Programfix för CQ-4273763
* Om du lägger till eller redigerar en webbtjänstanslutning genom att anropa webbtjänster från [!DNL Experience Manager Forms] Workbench uppstår ett fel: ClassNotFoundException org.apache.axis.message.SOAPBodyElement. NPR-30105: Programfix för CQ-4273217

### Funktionspaket ingår

>[!NOTE]
>
>För [!DNL Experience Manager Forms] kunderna är det viktigt att installera [!DNL Experience Manager Forms] tilläggspaket efter installation av [!DNL Experience Manager] Service Pack, Cumulative Fix Pack eller Feature Pack.

#### Sites {#sites-feature-packs-included}

* En konfigurationsegenskap har lagts till som tillåter export av Experience Fragments direkt till användardefinierade arbetsytor för [!DNL Adobe Target]. NPR-29189: Programfix för CQ-4249782

#### Forms - dokumenttjänster {#forms-document-services-1}

* Inställningen Auto har lagts till `RenderAtClient` i `PDFFormRenderOptions` API för [!DNL Experience Manager Forms] OSGi. NPR-30759: Programfix för CQ-4278193

## Adobe Experience Manager 6.5.1.0 {#experience-manager-6510}

[!DNL Adobe Experience Manager] 6.5.1.0 är en viktig version som innehåller prestanda, stabilitet, säkerhet samt viktiga kundkorrigeringar och förbättringar som släppts sedan den allmänna tillgängligheten av [!DNL Adobe Experience Manager] 6.5 i *april 2019.* Den kan installeras ovanpå [!DNL Experience Manager] 6.5.

Några viktiga höjdpunkter i den här Service Pack-versionen är:

* Aktiverade inkludering av dynamiskt gränssnittsläge i spårningshändelser som anpassade attribut.
* Stöd för 360-graders videomaterial i [!DNL Dynamic Media]Scene7-läge ingår.
* Aktiverade *japansk radbrytning* via stilpluginen i RTF-redigeraren. Mer information finns i [Konfigurera japansk radbrytning](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### Assets

* DAM DMGGateway-gränssnittet för S3-multipart-stöd har uppdaterats. NPR-29740: Programfix för CQ-4226303
* Förhandsgranskning av återgivningar genererar `Only empty tenantId is currently supported` fel efter uppgradering till [!DNL Experience Manager] 6.5. NPR-29986: Programfix för CQ-4272353
* Dialogrutan Ta bort är inte synlig så att du kan ta bort jobb. NPR-29720: Programfix för CQ-4271074
* När en användare har lagt till en objekttitel på egenskapssidan öppnas egenskapssidan igen när användaren försöker stänga sidan [!DNL Experience Manager] . NPR-29627: Programfix för CQ-4264929
* VersioningTimelineEventProvider ska tillhandahålla rotversionen tillsammans med noden av typen nt: version. Programfix för GRANITE-26063
* Implementerade möjligheten att överföra och spela upp 360 sfäriska videor i [!DNL Experience Manager] DM-Scene7-läge. Programfix för CQ-4265131
* Live-kopian hämtar felaktig status om källan redigeras. Programfix för CQ-4265451
* Stöd för Multi-Site Manager har aktiverats för [!DNL Experience Manager Assets]. Programfix för CQ-4271453, CQ-4268621, CQ-4257491
* [!DNL Experience Manager] -gränssnittet bör visa ytterligare en post för den aktuella versionen av resursen i tidslinjehistoriken och visa den senaste incheckningskommentaren från [!DNL Adobe Asset Link]. Programfix för CQ-4262864
* Tidslinjen för innehållsfragment visar ett felmeddelande när egenskaper saknas. Programfix för CQ-4272560
* Ett problem med Scene7 videospelare när den expanderar till helskärm. Programfix för CQ-4266700
* ZoomVerticalViewer: Panoreringsknappar ska inte visas om en enda bildresurs används. Programfix för CQ-4264795
* Om du tar bort en underordnad nod i live-kopian bör liveRelationship frigöras. Programfix för CQ-4270395
* Metadataschemat innehåller bara objekt från den globala konfigurationen och saknar dem från den aktiva klientorganisationen. URL-värdet för formPath återställs till standard även om det ändras. NPR-29945: Programfix för CQ-4262898
* Publicera bildförinställningar som [!DNL Brand Portal] misslyckas med 500-felkod. NPR-29510: Programfix för CQ-4268659

### Sites

* Tomma egenskaper och flera egenskaper sprids inte från utkast under utrullning. Det går inte att återställa live-kopia med utkast för komponenter. NPR-29253: Programfix för CQ-4264928, CQ-4264926, CQ-4267722
* CoralUI, när det används med `Multifield`, lagrar `fileReferenceParameter` på komponentnivå i stället för på multifältnivå. NPR-29537: Programfix för CQ-4266129
* Förbättring av [!DNL Experience Manager] textkomponent och textredigerare för japanska. NPR-29785: Programfix för CQ-4265090
* Sidan som återställs med Timewarp ska referera till rätt bild vid versionshanteringen. NPR-29431: Programfix för CQ-4262638
* Ett problem med arv av Style System-noder från överordnad till underordnad. NPR-29516: Programfix för CQ-4270330
* Ett felmeddelande visas när den sociala publiceringen konfigureras för [!DNL Facebook] autentisering. NPR-29211: Programfix för CQ-4266630
* Den återgivna miniatyrbilden för innehållsfragment visar intern kalenderrepresentation för fältet Datum och Tid. NPR-29531: Programfix för CQ-4269362
* Knapparna visas inte när du öppnar fliken Behörigheter i Coral2-implementeringen. Programfix för CQ-4269419

### Handel

* ConstraintViolationException, när lat innehåll migreras för e-handel. NPR-29247: Programfix för CQ-4264383

### Hantering av innehållsfragment

* Tolkningsfel vid öppning av ett innehållsfragment med tecken som består av dollartecken `($)` och inledande klammerparentes `({)`. Programfix för CQ-4270266

### Experience Fragments

* Exportera [!DNL Experience Manager] Experience Fragments till [!DNL Adobe Target]. Programfix för CQ-4265469
* Experience Fragments export till target misslyckas med smarta bilder. Programfix för CQ-4269606

* Användaren stöter på en återvändsgränd när försöker flytta Experience Fragments via Omnissearch i kortvyn. Programfix för CQ-4263848

### WCM - sidredigeraren

* XSS (Cross-site scripting) speglades när en ogiltig väljare användes. Programfix för CQ-4270397

### Replikering

* Data som tillhandahålls av användaren kan inte utelämnas vid utdata i `cq/replication/components/agent` komponenten, vilket resulterar i en lagrad XSS-säkerhetslucka (Cross-site scripting). Programfix för CQ-4266263

### Arbetsflöde

* Dialogdeltagarens kalenderväljarfält har brutits. NPR-29727: Programfix för CQ-4270423

### WCM - SPA

* Aktiverat hämtning av föråtergivet innehåll från en fjärrslutpunkt. Programfix för CQ-4270238
* Varningar i loggar när en SPA mallsida öppnas på serversidan. Programfix för CQ-4270238

### WCM - MSM

* Uppgradera till [!DNL Experience Manager] 6.4.3 så att det tar lång tid att driftsätta Multi-Site Manager. Programfix för CQ-4271410

### Integrering

* BrightEdge-autentiseringsuppgifter misslyckas med anslutningsfel. NPR-29168: Programfix för CQ-4265872

* Ett undantagsmeddelande visas när du försöker redigera och spara [!DNL Experience Manager] startkonfigurationen. NPR-29176: Programfix för CQ-4265782/CQ-4266153

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

* Sessionsläckage under OAuth för varje replikering till [!DNL Brand Portal]. NPR-30001: Programfix för GRANITE-26196

### Projekt

* Publicera [!DNL Experience Manager Assets] från [!DNL Experience Manager] författarmappen /content/dam/mac till [!DNL Brand Portal] fungerar inte. NPR-29819: Programfix för CQ-4271118

### Plattform

* HtmlLibraryManager tar bort allt innehåll i crx-quickstart vid cacheogiltigförklaring. NPR-29863: Programfix för GRANITE-26197

### Felix

* Information om minnesanvändning visas inte i systemkonsolen när Java11 används. NPR-29669

### Forms

De viktigaste högdagrarna för [!DNL Experience Manager Forms] 6.5.1.0 är:

* Endast OSGi: Ett nytt attribut har lagts till `PAGECOUNT` i Output och Forms Service.

* Endast OSGI: Stöd för att skapa statiska PDF-filer med Forms Service har aktiverats.
* Behörigheter för XMLForm.exe har aktiverats för administratör och rotanvändare.
* Aktiverat stöd för ADFS v3.0 för Dynamics lokal integrering.

#### Forms tilläggspaket

**Integrering med backend**

* Det gick inte att hämta WSDL (Protected Web Service Definition Language). NPR-29944: Programfix för CQ-4270777
* När [!DNL Experience Manager Forms] är installerat på IBM WebSphere misslyckas skapandet av en formulärdatamodell baserad på SOAP. Programfix för CQ-4251134
* Aktiverat stöd för ADFS (Active Directory Federation Services) v3.0 för integrering på plats i Microsoft Dynamics. Programfix för CQ-4270586
* När en datakällas titel ändras visas inte den uppdaterade titeln i formulärdatamodellen. Programfix för CQ-4265599
* Om namnet på en entitet eller ett attribut innehåller bindestreck eller blanksteg, kan uttrycken inte utvärdera sådana entiteter och attribut. Programfix för CQ-4225129

* Felaktiga utdata visas när ett kolon finns i den primitiva strängutdata. Programfix för CQ-4260825

* Även om inget innehåll förväntas från REST API-utdata genereras ett fel av formulärdatamodellens invoke-åtgärd. Programfix för CQ-4268828

**Adaptiv Forms**

* Det gick inte att lägga till en ny instans i adaptivt formulärfragment under en lat inläsning. NPR-29818: Programfix för CQ-4269875
* Verifiera att komponenten inte loggar eller visar något fel för dokumentmallar. Programfix för CQ-4272999
* Stöd har lagts till för att inaktivera layoutredigeraren för Adaptive Forms. Programfix för CQ-4270810
* Verifieringssteget för Adaptive Forms återställdes i [!DNL Experience Manager] 6.5. Programfix för CQ-4269583

* Fel vid validering av adaptiva formulärfält [!DNL Adobe Sign]. Programfix för CQ-4269463
* När en [!DNL Experience Manager Forms] instans har fler än 20 adaptiva formulärfragment och namnet på alla formulärfragment börjar med samma sträng, returnerar sökningen inga eller bara de 20 senast skapade fragmenten. Programfix för CQ-4264414, CQ-4264914

* Prestandaproblem när Adaptiv Forms-app används med stor datauppsättning. . Programfix för CQ-4235310

* Om det öppnas via ett anonymt konto på en publiceringsinstans går det inte att läsa in GuideRuntime-skriptet. Programfix för CQ-4268679

**Forms - Interaktiv kommunikation**

* Mallen för interaktiv kommunikation listar inte sidhuvuds- och sidfotskomponenter i listan över tillåtna komponenter. Programfix för CQ-4237895
* När du skapar en interaktiv utskriftsmall för kommunikation som innehåller ett bildfält, ställs diagrammets rubrik in på tom. Programfix för CQ-4264772
* När du tar bort linjefärgen i ett diagram anges värdet undefined. Programfix för CQ-4264762
* Ändringar av layoutlager som görs i dokumentfragment försvinner när ändringar synkroniseras. Programfix för CQ-4266054
* Formulärdatamodellelement i ett dokumentfragment som är bundet till ett textfält visar inte arvsikon och tillåter bindning. Programfix för CQ-4261089
* Återgivnings-API för utskriftskanal har inte möjlighet att skicka data som en parameter i API:t. Programfix för CQ-4263540
* Agentinställningarna visas inte eftersom kryssrutan Redigerbar av agent avmarkeras när bindningstypen ändras från textfragment till Inget/Datamodellobjekt för strängfält/variabel. Programfix för CQ-4261953
* När agentanvändargränssnittet skickas lagrar den resulterande webbdatajson-filen information för arvsannullerade obundna fält. Programfix för CQ-4265621

**Forms - arbetsflöde**

* När ett formulär skickas på nytt från utkorgen för adaptiva formulärprogram, förlorar det data. NPR-28345: Programfix för CQ-4260929
* Dokumenten stängs inte när de sparas för ärenden som inte är variabla. Programfix för CQ-4269784
* Adaptiv Forms-app har upphört med stöd för Microsoft Windows 8.1. Programfix för CQ-4265274
* När en bild på mer än 2 MB bifogas som en bifogad fil på fältnivå till ett formulär i Android-versionen av [!DNL Experience Manager Forms] programmet kraschar programmet. Programfix för CQ-4265578

* Aktiverade förifyllningsalternativ för Interactive Communication Print Channel i Tilldela-aktiviteten. Programfix för CQ-4265577
* Användarna kan inte visa en delad uppgift förrän de blir medlemmar i den grupp som uppgiften är tilldelad till. Programfix för CQ-4248733
* Det går inte att spara eller skicka JEE-program i appen Adaptiv form i Windows. Programfix för CQ-4268704
* Den formulärdatamodell som är associerad med formulärdatamodellvariabeln är inte synlig. Programfix för CQ-4266554
* Inget stöd för statusvariabeln för dokumentsignering med variabelstöd. Programfix för CQ-4266312
* Det går inte att skicka från arbetsytan med ett omljud. Programfix för CQ-4263172
* Om arbetsflödet öppnas för redigering i en uppgraderad konfiguration visas ett fel i stället för arbetsflödets namn i det bevakade mappgränssnittet. Programfix för CQ-4238579

**Forms - hantering**

* När ett tillägg som inte är xsd eller schema.json överförs, sker ingen överföring och inget felmeddelande genereras. Programfix för CQ-4266716

**Forms - korrespondenshantering**

* [!DNL Experience Manager Forms] 6.5 Gränssnittet Create Correspondence UI (CCR UI) kan inte öppna korrespondens som skapats med [!DNL Experience Manager Forms] 6.3. Programfix för CQ-4266392
* Summeringsfunktionen i XDP fungerar inte om DDE-datatypen är av typen number. Programfix för CQ-4227403
* Inaktiveringslogik för bokstavscache i minnet uppdateras eftersom den senaste ändringstiden inte uppdateras när en resurs publiceras. Programfix för CQ-4250465
* Det går inte att publicera dokumentfragment, DD och Letters. Programfix för CQ-4272893

#### Forms JEE-installationsprogram

**PDF Generator**

* Konverteringen av CAD-filer till PDF misslyckas med 64-bitars JDK. NPR-29924, NPR-29925: Programfix för CQ-4272113
* Ersatte namnet på PhantomJS till WebToPDF för HTML-till-PDF-konvertering. NPR-29933: Programfix för CQ-4234545
* Ett fel genereras när zip-filen konverteras till PDF. Programfix för CQ-4268628

**Forms - Designer**

* När en fullständig tillgänglighetskontroll utförs för den statiska PDF-filen som skapats med [!DNL Experience Manager Forms Designer]misslyckas kontrollen Primärt språk på grund av att språkattribut saknas. Programfix för CQ-4272923, CQ-4271002

**Forms - dokumentsäkerhet**

* Digital signatur med HSM (Hardware Security Module) fungerar inte med OSGi Linux på Java 11 och Java 8\. NPR-29838: Programfix för CQ-4270441
* Digital signatur med HSM (Hardware Security Module) fungerar inte med JEE Linux och alla appservrar som stöds, dvs. JBoss och Websphere. NPR-29839: Programfix för CQ-4266721
* Verifiering av signaturer i en PDF med hjälp av PDF Advanced Electronic Signatures (PAdES) genererar InvalidOperationException. NPR-29842: Programfix för CQ-4244837
* Utökat stöd för Document Security Extension för Office 2019\. Programfix för CQ-4254369, CQ-4259764

**Forms - dokumenttjänster**

* PDF-filen kan inte konverteras till PDF/A-1b med formulärfältet har ingen utseendeordlista. NPR-29940: Programfix för CQ-4269618

* OSGi: Det går inte att avgöra antalet sidor som genereras under återgivningen. NPR-28922: Programfix för CQ-4270870
* Stöd för statiska PDF-filer med Forms Service i [!DNL Experience Manager Forms OSGi]. NPR-28572: Programfix för CQ-4270869
* Det går inte att ändra behörigheten för XMLForm.exe. NPR-29828, NPR-29237: Programfix för Q-4267080
* Den statiska PDF-fil som skapas av [!DNL Experience Manager Forms] serverns utdatamoddul fyller inte i språkattributet/taggen med språket för det dokument som skapas. NPR-27332: Programfix för CQ-4271002

**Forms - Foundation JEE**

* Om pdfg_srt inte är tillgänglig i de sista artefakterna misslyckas installationsprogrammet. NPR-29854: Programfix för CQ-4270137
* LCBackupMode.sh fungerar inte. NPR-29840: Programfix för CQ-4269424
* UDP-portreferens ska tas bort från användargränssnittet för WebSphere. Programfix för CQ-4264782

### Funktionspaket ingår

#### Resurser - inkluderade

* Stöd för Multi-Site Manager har aktiverats för [!DNL Experience Manager Assets]. Mer information finns i [Återanvända resurser med hjälp av MSM för Experience Manager Assets](https://docs.adobe.com/content/help/en/experience-manager-65/assets/using/reuse-assets-using-msm.html). NPR-29199: Programfix för CQ-4259922

#### Webbplatser - ingår

* Exportera [!DNL Experience Manager] Experience Fragments till [!DNL Adobe Target]. Mer information finns [i Experience Fragment Link Rewriter Provider - HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML). Programfix för CQ-4265469

#### Forms - dokumenttjänster - ingår

* Endast OSGi: Ett nytt attribut, PAGECOUNT, har lagts till i Output och Forms Service. NPR-28922: Programfix för CQ-4270870
* Endast OSGi: Stöd för att skapa statiska PDF-filer med Forms Service har aktiverats. NPR-28572: Programfix för CQ-4270869
* Behörigheter för XMLForm.exe har aktiverats för administratör och rotanvändare. NPR-29237: Programfix för CQ-4267080

### OSGi-paket och innehållspaket

Följande textdokument innehåller en lista över de OSGi-paket och innehållspaket som ingår i [!DNL Experience Manager] 6.5.1.0

Förteckning över OSGi-paket som ingår i [!DNL Experience Manager] 6.5.1.0

[Hämta fil](assets/6_5-bundle-list.txt)

Förteckning över innehållspaket som ingår i [!DNL Experience Manager] 6.5.1.0

[Hämta fil](assets/6_5-content-package-list.txt)
