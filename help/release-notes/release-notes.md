---
title: Versionsinformation för [!DNL Adobe Experience Manager] 6.5
description: '"[!DNL Adobe Experience Manager] 6.5 som beskriver versionsinformation, nyheter, hur man installerar och detaljerade ändringslistor."'
mini-toc-levels: 3
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: a45d66dc2226dbe2879aa61d95cc5379dce882bb
workflow-type: tm+mt
source-wordcount: '3750'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] 6.5 Versionsinformation om senaste Service Pack {#aem-service-pack-release-notes}

## Versionsinformation {#release-information}

| Produkt | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.13.0 |
| Typ | Service Pack-version |
| Date | 26 maj 2022 |
| Hämta URL | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.13.0.zip) |

## Vad ingår i [!DNL Experience Manager] 6.5.13.0 {#what-is-included-in-aem}

[!DNL Experience Manager] 6.5.13.0 innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat samt prestanda-, stabilitets- och säkerhetsförbättringar som släppts sedan den första tillgängligheten av 6.5 i april 2019. [Installera detta Service Pack](#install) på [!DNL Experience Manager] 6.5.

De viktigaste funktionerna och förbättringarna i [!DNL Adobe Experience Manager] 6.5.13.0 är:

* Använd osynlig CAPTCHA i adaptiv form: Du kan nu använda en osynlig CAPTCHA för att visa CAPTCHA-utmaningen endast om en misstänkt aktivitet inträffar. Om ingen misstänkt aktivitet hittas visas inte CAPTCHA-utmaningen. Det gör det lättare att bedöma om formulär ska fyllas i av människor utan att det behövs kryssrutor, minska anpassningsarbetet och förbättra slutanvändarens upplevelse. (NPR-38500)

* Stöd har lagts till för att hämta svarshuvuden i efterbearbetningen av formulärdatamodellen för REST-slutpunkter. (NPR-38275)

* När du genererar en adaptiv formuläröversättningsfil är nu samma textsekvens som den genererade XLIFF-filen identisk med komponentsekvensen i motsvarande adaptiva formulär. (NPR-37700)

* När du lokaliserar ett adaptivt formulär och gör en liten ändring av texten i basspråket, saknas den fullständiga översättningen för alla andra språk. Problemet är åtgärdat i [!DNL Experience Manager] 6.5.13.0 (NPR-37189)

* Tillgänglighetsförbättringar för Forms:

   * Stöd för skärmläsare har lagts till för att identifiera tabellens rubrik och brödtext som fortsätter och anslutna enheter. Det hjälper skärmläsare att navigera i tabellerna på rätt sätt. (NPR-37139)
   * Stöd för att skärmläsare ska sluta navigera på arbetsytan i HTML tills en dialogruta är öppen har lagts till. (NPR-37134)
   * Lagt till möjlighet att ange Reader-text på skärmen för hyperlänkar i Forms Designer.(NPR-36221)

Följande felkorrigeringar, viktiga funktioner och förbättringar introducerades i [!DNL Experience Manager] 6.5.13.0:

<!-- The following issues are fixed in [!DNL Experience Manager] 6.5.13.0: -->

## [!DNL Assets] {#assets-6513}

* När du försöker redigera ett skrivskyddat listrutefält återställs listrutans värde till tomt. (NPR-38389)
* Användaren kan inte importera en videoresurs (.mp4) om det inte finns något ljud i videofilen. Arbetsflödet för DAM-uppdatering av resurser misslyckas och visar ett felmeddelande. (NPR-38116)
* När du använder guiden Flytta resurser för att flytta en mapp som innehåller resurser misslyckas arbetsflödet och ett felmeddelande visas. (NPR-38061)
* Arbetsflödet för MPEG-omkodning misslyckades för FLV-videoprofilen. (CQ-4343249)
* Efter uppdatering till [!DNL Experience Manager] 6.5 SP10, redigeraren för metadata för resurs fungerar inte som den ska. (CQ-4341359)
* När du öppnar en smart samling som har sparats med sökfiltret tillämpat som Publicera, ändras sökfiltret automatiskt till Opublicerad. (CQ-4341191)
* När du byter språk **[!UICONTROL User Preference]**, etiketten **[!UICONTROL Sort By]**, nedrullningsknappen och andra alternativ i sorteringsalternativen på startsidan för Resurser visas inte på det valda språket. (CQ-4339306)
* När du lägger till en regel i ett nedrullningsbart fält i **[!UICONTROL Metadata Schema]**, **[!UICONTROL Dependent On]** listan återspeglar inte fältetiketten för listrutan. (ASSETS-9442)
* Metadata för resurser har inaktiverats i den nedrullningsbara listan utan att värden behålls. (ASSETS-8918)
* När du visar resursen med **[!UICONTROL More Details]** alternativ i **[!UICONTROL Column]** visas felaktiga anteckningar. (ASSETS-8851)
* När du skapar en duplicerad resurs med en annan version genereras inte återgivningarna. (ASSETS-8607)

* En icke-admin-användare kan publicera en resurs som redan är utcheckad av en annan användare. (NPR-38128)
* Dimensionellt visningsprogram fungerar inte i Chrome 97. (CQ-4340456)
* Knappen för att hämta resurser visar inte hela menyn på sidan med resursinformation. (CQ-4336703)
* När du använder Länkdelning är vissa av strängarna i länkdelningsfönstret inte lokaliserade. (CQ-4330540)
* När du lägger till objekt i Hantera publikation lokaliseras inte strängen som visar antalet markerade objekt. (CQ-4330491)

### [!DNL Dynamic Media] {#dynamic-media-6513}

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Zero day exploit with the Java™ Spring Core Framework (CVE-2022-22963) impacting Experience Manager 6.5.12. (ASSETS-9031) -->
* Tokenbaserad säker förhandsgranskning för Dynamic Media-material på AEM Authors. (ASSETS-4995)
* När du skapar en bildförinställning för Dynamic Media i [!DNL Experience Manager], är det tillåtna maxvärdet begränsat till 2 000 × 2 000 pixlar i användargränssnittet. När värdet ökas till 2 001 pixlar för antingen bredd eller höjd visas **[!UICONTROL Save]** knappen är inaktiverad. (ASSETS-5691)
* Användaren kan förhindra att vissa filformat överförs till Dynamic Media. (ASSETS-5693)
* Hjälpmedel - Visuellt utmanade användare som förlitar sig på skärmläsare påverkas om Alt-attributet inte implementeras på en bild i användargränssnittet för bildförinställningar. (ASSETS-9817)
* Hjälpmedel - Skärmläsare påverkas när skärmläsare lägger till en berättarröst utan etikett för bilderna som finns i tidslinjesegmentet och på fliken Åtgärder när de navigeras till i nedpilsläge. (ASSETS-5651)
* Hjälpmedel - Skärmläsare påverkas eftersom skärmläsare (NVDA/JAWS) inte berättar beskrivande namn (skicka e-post) för knappen&quot;Skicka e-post&quot; i dialogrutan&quot;E-postlänk&quot; i videospelaren när de navigerar i läget (Bläddra/pekare). (ASSETS-5641)
* Hjälpmedel - Tangentbordsfokus flyttas inte till knappen Gör om, som visas när knappen Ångra har anropats på sidan Bilduppsättningsredigerare, medan du navigerar med tabbtangenten på tangentbordet. (ASSETS-5582)
* Hjälpmedel - Användare som förlitar sig på skärmläsare påverkas eftersom Alt-attributet inte anges för en bilduppsättningsbild som finns under rubriken Egenskaper. (ASSETS-5576)
* Hjälpmedel - Skärmläsare lägger inte till en berättarröstroll för `Cannot save this set` text i `Cannot save this set` varning, vid navigering med hjälp av kortkommando för rubrik `H`och nedpilen. (ASSETS-5569)
* Tillgänglighet - Användare som förlitar sig på skärmläsare påverkas för att navigera i formulären. De har svårt att förstå informationen om formulärkontrollerna om NVDA inte lägger till en berättarröst för rotationskontrollerna &quot;Bredd och höjd&quot;. Dessa kontroller som finns under rubriken Responsiv bildbeskärning vid navigering i NVDA-formulärläge&quot;F&quot;. (ASSETS-5393)
* När du har lagt till en Dynamic Media-komponent på en webbplats och har publicerat sidan visas inte den nyligen tillagda Dynamic Media-resursen på den publicerade sidan och den kan inte heller visas på förhandsgranskningssidan. Problemet uppstod för både bild- och videoresurstyper. (ASSETS-9467)

## Handel {#commerce-6513}

* &quot;alla&quot; har jcr:skriv på `/content/usergenerated/etc/commerce/smartlists`. (NPR-35230)
* Lokal sortering av Commerce Products fungerar inte längre. (CQ-4343750)
* Det går inte att snabbpublicera en produkt från sökresultatsidan efter ändring av egenskaper. (CQ-4343318)

## CRX {#crx-6513}

* Det går inte att hämta ett paket om det har specialtecknet `+` i paketnamnet. (NPR-38102)

## [!DNL Forms] {#forms-65130}

* När du använder förifyllningstjänsten för att fylla i ett adaptivt formulär som innehåller ett fragment och fragmentet innehåller en textruta som stöder formaterad text, skickas inte formuläret och följande fel inträffar:

   `[AF] [AEM-AF-901-004]: Encountered an internal error while submitting the form.` (NPR-38542)

* Komponenterna Radio button, Checkbox, and File Upload är inte korrekt översatta från tyska till engelska. (NPR-38527)
* PDF417-streckkodskodningen som produceras av [!DNL Experience Manager] Forms är ogiltigt för en alternativknappsgrupp. (NPR-38525)
* Följande fel inträffar när ett adaptivt formulär skickas.
   `WARN [10.172.114.236 [1650871578492] POST /lc/content/forms/af/public/DHS-3754-ENG/jcr:content/guideContainer.af.internalsubmit.jsp HTTP/1.1] com.adobe.aemds.guide.internal.impl.utils.SubmitDataCollector TemplateKey not found in merge json:cq:responsive` (NPR-38520)
* Alternativet Uteslut dolda fält från postdokument fungerar inte. (NPR-38512)
* När du har lagt till Forms Container-komponenten på en Sites-sida kan användarna inte gå till en annan Sites-sida och Sites-sidan hänger sig ibland. Problemet uppstår ibland. (NPR-38506)
* Användare upplever överlappande text i Adaptive Forms efter användning [!DNL Experience Manager] 6.5 Service Pack 11. (NPR-38376, CQ-4342472)
* Användarna får ett undantag när anpassningsbara formulärpaneler flyttas till en ny responsiv layout. (NPR-38369)
* Stöd för ECMASCRIPT 6 (ES6) är inte aktiverat för klientbiblioteket ` /libs/fd/expeditor/clientlibs/view`. (NPR-38358)
* När du använder en [!DNL Experience Manager] I arbetsflödet för att skicka e-post på hebreiska innehåller e-postmeddelandet som togs emot i användarens slut frågetecken (?) i stället för hebreisk text (NPR-38296).
* Användare loggas ut slumpmässigt från [!DNL Experience Manager] Publicera instanser och ett adaptivt formulär kan inte skickas. Problemet visas på [!DNL Experience Manager] instanser som använder Dispatcher. (NPR-38285)
* När du använder alternativet getFormDataString i en Adobe Launch-regel för att hämta adaptiva formulärdata, returnerar alternativet inte adaptiva Forms-data. (NPR-38283)
* [!DNL Experience Manager] 6.5 Forms har ersatt java.acl.Group-related API och följande felmeddelanden visas i error.log-filen:
   ` *WARN* [default task-36] org.apache.jackrabbit.oak.spi.security.principal.AclGroupDeprecation use of deprecated java.acl.Group-related API - this method is going to be removed in future Oak releases - see OAK-7358 for details` (NPR-38282)
* Forms som skapats på tyska kan inte översättas till engelska eller något annat språk. (NPR-38280)
* När du använder en lokaliserad version av ett adaptivt formulär lokaliseras inte motsvarande DoR-dokument (Document of Record). (NPR-38235)
* När du använder steget Skicka e-post för att skicka en bifogad fil tillsammans med e-post, kommer den bifogade filen inte att behålla det namn som angetts i arbetsflödessteget. (NPR-38216)
* När en ny version av brevet publiceras, kan användare inte öppna utkasten för tidigare versioner av bokstäverna. (NPR-38215, CQ-4342515)
* SOAP-tjänsten misslyckas med följande undantag när en AEM Forms JEE-tjänsts SOAP-slutpunktstjänstmetod anropas med en knapp som konfigurerats som en regel för adaptiv form:
   `ERROR* [0:0:0:0:0:0:0:1 [1624362360493] POST /content/forms/af/testsoapwsdl/jcr:content/guideContainer.af.dermis HTTP/1.1] com.adobe.aemds.guide.addon expeditor.servlet.ExpEditorServiceManager Error while making web service related call java.lang.Exception: createSOAPParam: JSONException`
* Om du använder com.adobe.fd.pdfutility.services.PDFUtilityService#convertPDFtoXDP för att konvertera ett PDF till XDP-format returneras en ogiltig XDP-fil. (NPR-38140, CQ-4342099)
* När flera användare använder Correspondence Management för att generera olika bokstäver visas ett felaktigt brev för vissa användare vid förhandsgranskningen. (NPR-38134)
* AEM Forms-komponenten som är inbäddad på SITES-sidan använder breddattributet som har värdet i % och som inte är giltigt enligt W3C HTML-valideringen. Användarna stöter på ett felaktigt tolkningsfel under valideringen av HTML. (NPR-38124)
* Alternativknappar och kryssruteobjekt för de flesta OTB-teman i anpassningsbara former ingår inte i tabbordningen (NPR-38108)
* När en användare lägger till HTML-taggar i kommentaravsnittet när ett arbetsflöde körs återges HTML-taggarna. (NPR-37591)
* Om du importerar och publicerar ett brev som innehåller en ny XDP-fil kan bokstäverna inte förhandsgranskas i Publish-instansen. Om bokstäverna importeras och publiceras en andra gång med samma CMP-fil kommer bokstäverna att förhandsgranskas korrekt. (CQ-4343599)
* Ett formulär med egenskapen Förbered dataprocess angiven kan inte återges i HTML Workspace. (CQ-4343294)
* För statisk PDF forms som skapats med Forms 6.5 Designer misslyckas tillgängligheten för PDF med fel `Tab order entry in page with annotations not set to "S"`. (CQ-4343117)
* Det går inte att konvertera en bild till PDF med PDFG-tjänsten med OCR efter att korrigeringsfilen AEMForms-6.5.0-0038 (log4jv2.16) har tillämpats. (CQ-4342450)
* Felaktigt värde visas för streckkoden SSCC-18. Forms-servrar utelämnar värdet till höger om streckkoden. (CQ-4342400)
* Det går inte att importera en Microsoft® Word-fil till Forms Designer. Fel vid användarstöttningar `Word (version XP or onwards) could not be found on the machine`. (CQ-4342146)
* När du öppnar ett formulär som har skapats med Forms 6.1 Designer i Forms 6.5 Designer och redigerar en textruta överskrider styckeavståndet det angivna utrymmet. Alla tidigare inställningar för utrymmet tas bort och du måste formatera om textrutan manuellt. (CQ-4341899)
* Användaren kan inte ange anpassad tid i schemaläggaren för jobbrensning. (CQ-4339192)
* Användaren kan inte uppdatera någon konfiguration under användargränssnittet för slutpunktshantering och stöttningsfel ` Uncaught ReferenceError: updateEndpoint_required is not defined`. (CQ-4331523)
* För ogiltiga taggar fungerar inte felmeddelandet korrekt. (NPR-38106 och CQ-4337173)

>[!NOTE]
>
>* [!DNL Experience Manager Forms] släpper tilläggspaketen en vecka efter den schemalagda [!DNL Experience Manager] Lanseringsdatum för Service Pack.


## Granit {#granite-6513}

* Omnissearch returnerar resultat för användare utan läsbehörighet. (NPR-38373)
* Aktivera ES6 för `/libs/granite/configurations/clientlibs/confbrowser`. (NPR-38300)

## Integreringar {#integrations-6513}

* Slut på resurslösningssessioner på tjänsten Test och Target från utgått UserInfoServlet. (NPR-38112)

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * AEM‑OP‑13 ‑ HTTP Parameter Pollution in `com.day.cq.searchpromote.impl.servlet`. (NPR-38033) -->
<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Analytics 2.0 IMS support added to Experience Manager 6.5. (NPR-37914) -->

## Oak - indexering och frågor {#oak-6513}

* OS-versionen för 6.5.13.0 har nu uppdaterats till 1.22.11. (NPR-38084) —>

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Create a CFP based on latest 6.5.12 and update Oak-related bundle versions. (NPR-38144) -->

## Plattform {#platform-6513}

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * RTC : Universal XSS through cq-rewriter HtmlParser. (NPR-38064) -->
* Uppgraderingsberoende av `org.apache.httpcomponents.httpclient` in [!DNL Experience Manager] 6.5. (NPR-37999)
* Hög författarbelastning på grund av förslag på sökvägsfält. (CQ-4341826)
* Användaren måste uppdatera sidan när han/hon ändrar projektet från kortvyn till kalendervyn. (CQ-4340368)
* Taggar går förlorade på grund av behörighetsbegränsningar. (CQ-4339543)
* Flera problem som rapporterats med Sök och filtrera i Banmarkering fungerar inte. (CQ-4339402)
* Sluta använda DTM på 6.5 - byt till Launch för Omega Instrumentation och lägg till stöd för Gainsight. (CQ-4337809)
* Begränsa sökfunktionen för banfältskomponenter baserat på filteregenskapen för sökvägar som har angetts. (CQ-4309556)
* [!DNL Experience Manager] Plattform 6.5: Namngivningsåtgärder för kinesiska. (CQ-4308978)
* Växla till Starta för Omega Instrumentation. (NPR-38377)
* [!DNL Experience Manager] Plattform 6.5: Korrigeringar för kinesiska språkversioner. (CQ-4308978)

## Replikering {#replication-6513}

* Publicering av användarnod misslyckades från författare till utgivare. (NPR-38005)

## [!DNL Sites] {#sites-6513}

### Administratör {#sites-admin-6513}

* Åtgärda regressionen som introducerades med SP 12 som kan ha orsakat ett problem när sidor flyttades. (SITES-5298)

### Klassiskt användargränssnitt {#sites-classicui-6513}

* RTE: Uppdaterad bild visas inte när en ny bild dras över en befintlig bild. (NPR-38141)

<!-- version 2 of description above * Updated Image is not visible When a new image is dragged on top of an existing image the updated image is not visible in RTE - Classic UI. (NPR-38141) -->

### Innehållsfragment {#sites-contentfragments-6513}

* Stöd för att skapa modeller för innehållsfragment i underkonfigurationer. (NPR-38054)

<!-- version 2 of description above * The Configuration Manager now allows you to set the Content Fragment Model config on a sub-config folder. (NPR-38054) -->
* Förbättra prestanda när du använder valideringen Unikt fält i modellen för innehållsfragment. (NPR-38142)

<!-- version 2 of description above * The unique field validation query is now fixed. (NPR-38142) -->
* Förbättra svarstiden när Content Fragment Model Editor öppnas. Kunder med många fragment i Assets kan ha sett fel när de öppnades. (SITES-6284)

<!-- version 2 of description above * If the customer is trying to access the editor of the content fragment models, they get a query error because of too many fragments on the dam. (SITES-6284) -->
* Korrigera regression som introducerades vid uppdatering från 6.5.11 till 6.5.12 som kan ha orsakat fel i modellredigeraren för innehållsfragment. (SITES-5088 and SITES-4967)

<!-- version 2 of description above * Paths were getting deleted when AEM 6.5.12.0 was installed on existing 6.5.11.0 instance. (SITES-5088)
* Apple 6.5.10 system crashing when using CF model editor, due to erroneous feature toggle check. (SITES-4967) -->
* Förbättra lokaliseringen av användargränssnittet i Modellredigeraren för innehållsfragment. (NPR-38126)

<!-- version 2 of description above * Some strings in the Content Fragment Model editor are not localized. (NPR-38126) -->
* Åtgärda problem som kan uppstå när redigeraren för innehållsfragment stängs när författarservern används med Dispatcher. (NPR-38205)

<!-- version 2 of description above * Update of Content Fragment references is returning an invalid JSON response via Dispatcher. (NPR-38205) -->
* Åtgärda problem med att det inte gick att spara en modell när valideringen användes i ett RTE-fält. (NPR-38210)

<!--version 2 of description above * Content Fragment Model Rich Text Validation Prevents Blocks Saving a Content Fragment Model. (NPR-38210) -->
* Content Fragment problem med den booleska egenskapen som inte visar Field Text i title i stället för Property Name. (NPR-38244)
* Ett fel uppstod när en beständig fråga kördes med en frågevariabel via Postman. (NPR-38251, NPR-38057)
<!--version 2 of description above * An unexpected error message is coming in Postman, when executing the graphQL persisted query having query variables. (NPR-38251) -->
* Innehållsfragmentkomponent: Regression i alternativet Hantera rubriker som stycken som korrigerades som var 6.5 SP7. (NPR-38055)

<!--version 2 of description above * After applying SP11 to the Publish instance of AEM 6.5.6, the display result of the Content Fragment set in the published page changes. (NPR-38055) -->
* Korrigera regression som introducerades i 6.5.11 som kan ha orsakat fel i resurssökningen. (SITES-4784)

<!--version 2 of description above * Adapt external index package to use selection Policy (fragment versus asset index). (SITES-4784) -->
* Använda **[!UICONTROL Edit]** från sökresultaten kan resultera i en `Not Found` fel. (NPR-37810)

<!--version 2 of description above * When editing Content Fragment from the Assets Search Rail results page, it throws 'Not Found' error. (NPR-37810) -->

### ContentHub {#sites-contenthub-6513}

* Gränssnittsmodeller för kontextnav återges inte korrekt utan en uppdatering av sidan. (NPR-38212)

### E-postredigerare {#sites-emaileditor-6513}

* Aktivera stöd för kommande releaser av E-Mail Core Components [https://github.com/adobe/aem-core-email-components](https://github.com/adobe/aem-core-email-components). (NPR-38445 och NPR-38204)

<!-- version 2 of description above * Allow new email templated under campaign and ambit. (NPR-38445) * The "Approve for Adobe Campaign" workflow was only running for pages which are of type or extending the resource types: "mcm/neolane/components/newsletter", "mcm/campaign/components/newsletter" and "mcm/campaign/components/campaign_newsletterpage". (NPR-38204) -->

### Experience Fragments {#sites-experiencefragments-6513}

* När du använder åtgärden Navigera till sida i Referenser för ett Experience Fragment, öppnas fel sida. (NPR-38062)
* Layoutegenskaper som kommer från XF-mall visas inte bredvid en sida. (NPR-38214)
* Förbättrade prestanda för XF-referensberäkning. (NPR-38269)

<!-- version 2 of description above * Job queue configuration is incorrect - The OSGi configuration for the reference updater job queue has not been ported back to 6.5. This issue leads to jobs being run in the main queue, which has a higher priority and allows more jobs to run in parallel. This flow can lead to CPU exhaustion. (NPR-38269) -->

### Page Editor {#sites-pageeditor-6513}

* Förbättra ångra för komponenter som inte har funktionen inlineEditing eller dropTarget i `cq:editConfig`. (NPR-38361)

<!-- version 2 of the description above * When out of the box components that don't have inlineEditing or dropTarget feature in the _cq_editConfig file (navigation, breadcrumb, embed) are deleted > undeleted (by way of Undo), all configurations are lost and empty placeholder reappears. Component must be reconfigured from scratch. (NPR-38361) -->
* Listrutan Formatsystem kan ha placerats högst upp på sidan i stället för i sitt sammanhang för komponenten - för komponenter som använder `cq:editConfig` &quot;afteredit: REFRESH_PAGE&quot;. Problemet är nu löst. (NPR-38384)

<!-- version 2 of description above* When selecting a style option on a component, the Styles box shifts to the upper left corner of the screen, rather than staying put below the style icon. Happens for components that have  cq:editConfig “afteredit: REFRESH_PAGE”. (NPR-38384) -->
* Textkomponenten är feljusterad när den läggs till i kapslade layoutbehållare. (NPR-38193)
* En tom formatflik visades när det inte fanns någon formatsystemskonfiguration för en komponent; fliken är nu dold när det inte finns någon konfiguration. (NPR-38218)
<!-- version 2 of description above * Style tab is blank on components without styles/policies. (NPR-38218) -->
* Egenskapen `useLegacyResponsiveBehaviour` fungerar bara när de autentiseras. (NPR-37996)
* Uppgraderingen av jquery-ui till den senaste versionen ledde till att redigeraren bröts. (SITES-5647)

### Dokumentskydd {#sites-security-6513}

* Användargränssnittet för användargruppshantering kunde ibland inte ta bort användare, särskilt i grupper med +20 användare. (NPR-38041)

<!--version 2 of description above * Cannot remove users from user groups. (NPR-38041) -->

### SEO {#sites-seo-6513}

* Taggen Sitemap Generator och Canonical har stöd för URL:er utan .html. (CIF-2647)
* Lägg till stöd för att ta bort alternativa språk med noindex-konfigurationen. (CIF-2496)
* Lägg till stöd för att ange en anpassad URL som skriver över den kanoniska standardwebbadressen för sidor som har nästan identiskt innehåll. (CIF-2747)

### SPA Editor och SDK {#sites-spa-sdk-6513}

* Från och med 6.5.13 behöver du inte längre skapa behållarkomponentnoden i JCR innan du redigerar via SPA Editor. A `virtual container` skapas innan den sparas med SDK. (SITES-5762)

<!-- version 2 of description above * Virtual container support - Adding a child component to a virtual container that is not yet present in the database implies the creation of a node to represent the container in content structure. (SITES-5762) -->

### Mallredigerare {#sites-templateeditor-6513}

* Åtgärda regressionen att publicering av en ändrad mall inte publicerade alla beroenden. (NPR-38274)

<!-- version 2 of description above * Template changes do not get published until you publish a page that uses that template. (NPR-38274) -->
* TemplatedResource valueMap bör tillåta djupa läsningar enligt ValueMap API. (NPR-38439)

## Sling {#sling-6513}

* Minnesläcka in `DiscoveryLiteDescriptor`. (NPR-38288)
* Uppdatera `sling-javax.activation` paket med fix SLING-8777. (NPR-38077)
<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Security issues reported under `org.apache.sling.scripting.jst`. (NPR-38067) -->

## Översättningsprojekt {#translation-6513}

* Flera starter skapas för refererade sidor/xf. (NPR-38263)
* Ändrat beteende för att lägga till sidor i översättningsprojekt sedan Service Pack 10. Översättningsprojektet innehåller inte en ny sida [ex: test-page-Women-2] i listan, när det är markerat som överordnat till den nyligen skapade sidan [inte den nya sidan direkt]. (NPR-38256)
* Lägg till `cq:isTranslationLaunch` i Startar som skapats av översättningsprojekt. (NPR-38224)
* Launch skapas för en sida med en refererad XF-fil som innehåller en resurs. (NPR-38199)
* [!DNL Experience Manager] uppdateringsöversättningsminnet fungerar inte. (NPR-38196)
* Aktivera ES6 för `/libs/cq/gui/components/projects/admin/translation/job/addcontent/clientlibs.js`. (NPR-38306)
* Senaste 18n-paketet för översättningar för [!DNL Experience Manager] 6.5. (CQ-4339505)

## Användargränssnitt {#ui-6513}

* När du är på startsidan > Verktyg och klickar på [!DNL Experience Manager] -ikonen [!DNL Experience Manager] Navigeringsskärmen ska visas. (NPR-38417)
* Aktivera ES6 för `/libs/granite/ui/references/clientlibs/coral/references`. (NPR-38303)
* Aktivera ES6 för `/libs/granite/datavisualization/clientlibs/d3-3.x`. (NPR-38302)

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * AEM‑OP‑09 ‑ Persistent cross‑site scripting selecting paths in templates. (NPR-38301) -->
* Datumväljaren med pekskärmsgränssnitt visas på koreanska. (NPR-38079)
* Dialogrutan för redigering med multifält visas när du ändrar ordning på fälten och alternativknappens markeringsvärde försvinner. (NPR-38063)

## WCM {#wcm-6513}

* [!DNL Experience Manager] MCM (Campaign) 6.5: Namngivningsåtgärder för kinesiska. (CQ-4308973)
* Ostängd ResourceResolver i com.day.cq.wcm.workflow.impl.WcmWorkflowServiceImpl.autoSubmitPageAfterModification (NPR-38286)

## Installera [!DNL Experience Manager] 6.5.13.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback -->

* [!DNL Experience Manager] 6.5.13.0 kräver [!DNL Experience Manager] 6.5. Se [uppgraderingsdokumentation](/help/sites-deploying/upgrade.md) för detaljerade anvisningar.
* Service Pack-nedladdning finns på Adobe [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* På en distribution med MongoDB och flera instanser installerar du [!DNL Experience Manager] 6.5.13.0 på en av författarinstanserna med hjälp av Package Manager.

>[!NOTE]
>
>Adobe rekommenderar inte att du tar bort eller avinstallerar [!DNL Experience Manager] 6.5.13.0-paket.

### Installera Service Pack på [!DNL Experience Manager] 6.5 {#install-service-pack}

1. Starta om instansen innan installationen om instansen är i uppdateringsläge (när instansen uppdaterades från en tidigare version). Adobe rekommenderar att du startar om om den aktuella upptiden för en instans är hög.

1. Ta en ögonblicksbild eller en ny säkerhetskopia av din [!DNL Experience Manager] -instans.

1. Hämta Service Pack från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.13.0.zip).

1. Öppna Pakethanteraren och klicka på **[!UICONTROL Upload Package]** för att överföra paketet. Mer information finns på [Pakethanteraren](/help/sites-administering/package-manager.md).

1. Markera paketet och klicka på **[!UICONTROL Install]**.

1. Om du vill uppdatera S3-anslutningen stoppar du instansen efter installationen av Service Pack, byter ut den befintliga kopplingen mot en ny binär fil som finns i installationsmappen och startar om instansen. Se [Amazon S3 - datalager](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Dialogrutan för pakethanterarens gränssnitt avslutas ibland när Service Pack installeras. Adobe rekommenderar att du väntar på att felloggarna ska stabiliseras innan du får åtkomst till distributionen. Vänta på de specifika loggarna för avinstallationen av uppdateringspaketet innan du försäkrar dig om att installationen lyckas. Vanligtvis inträffar detta problem i [!DNL Safari] webbläsare, men kan ibland inträffa i vilken webbläsare som helst.

**Automatisk installation**

Det finns två olika metoder som du kan använda för att installera automatiskt [!DNL Experience Manager] 6.5.13.0

* Placera paketet i `../crx-quickstart/install` när servern är tillgänglig online. Paketet installeras automatiskt.
* Använd [HTTP-API från Package Manager](/help/sites-administering/package-manager.md#package-share). Använd `cmd=install&recursive=true` så att de kapslade paketen installeras.

>[!NOTE]
>
>[!DNL Experience Manager] 6.5.13.0 stöder inte installation av Bootstrap.

**Validera installationen**

Om du vill veta vilka plattformar som är certifierade för att fungera med den här versionen kan du läsa [tekniska krav](/help/sites-deploying/technical-requirements.md).

1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience Manager (6.5.13.0)` under [!UICONTROL Installed Products].

1. Alla OSGi-paket är antingen **[!UICONTROL ACTIVE]** eller **[!UICONTROL FRAGMENT]** i OSGi Console (Use Web Console: `/system/console/bundles`).

1. OSGi-paketet `org.apache.jackrabbit.oak-core` är version 1.2.2.3 eller senare (Använd webbkonsol: `/system/console/bundles`).


### Installera [!DNL Experience Manager] Forms tilläggspaket {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Hoppa över om du inte använder [!DNL Experience Manager] Forms. Korrigeringar i [!DNL Experience Manager] Forms levereras via ett separat tilläggspaket en vecka efter den schemalagda [!DNL Experience Manager] Service Pack-version.

1. Kontrollera att du har installerat [!DNL Experience Manager] Service Pack.
1. Ladda ned motsvarande tilläggspaket från Forms på [AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) för ditt operativsystem.
1. Installera Forms tilläggspaket enligt beskrivningen i [Installera AEM Forms tilläggspaket](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).
1. Om du använder bokstäver i Experience Manager 6.5 Forms installerar du [senaste AEMFD-kompatibilitetspaket](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates).

### Installera [!DNL Experience Manager] Forms på JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Hoppa över om du inte använder AEM Forms på JEE. Korrigeringar i [!DNL Experience Manager] Forms på JEE levereras via ett separat installationsprogram.

Mer information om hur du installerar det kumulativa installationsprogrammet för [!DNL Experience Manager] Forms on JEE och konfiguration efter driftsättning finns i [versionsinformation](jee-patch-installer-65.md).

>[!NOTE]
>
>Efter installation av det kumulativa installationsprogrammet för [!DNL Experience Manager] Forms på JEE, installera det senaste Forms-tilläggspaketet, ta bort Forms-tilläggspaketet från `crx-repository\install` och starta om servern.

### UberJar {#uber-jar}

UberJar för [!DNL Experience Manager] 6.5.13.0 finns i [Maven Central-arkivet](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.13/)(https://).

Information om hur du använder UberJar i ett Maven-projekt finns i [använda UberJar](/help/sites-developing/ht-projects-maven.md) och inkludera följande beroende i projektens POM:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.13</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar och andra tillhörande artefakter finns tillgängliga i Maven Central Repository i stället för i Adobe Public Maven-arkivet (`repo.adobe.com`). Huvudfilen för UberJar har bytt namn till `uber-jar-<version>.jar`. Så det finns ingen `classifier`, med `apis` som värdet, för `dependency` -tagg.

## Föråldrade funktioner {#removed-deprecated-features}

Nedan finns en lista över funktioner som är markerade som borttagna [!DNL Experience Manager] 6.5.7.0 Funktioner markeras som borttagna från början och senare i en framtida version. Ett alternativt alternativ anges.

Granska om du använder en funktion eller en funktion i en distribution. Planera också att ändra implementeringen så att ett alternativt alternativ används.

| Yta | Funktion | Ersättning |
|---|---|---|
| Integreringar | The **[!UICONTROL AEM Cloud Services Opt-In]** skärmen är föråldrad sedan [!DNL Experience Manager] och [!DNL Adobe Target] integreringen uppdateras i [!DNL Experience Manager] 6.5. Integreringen stöder Adobe Target Standard API. API:t använder autentisering via Adobe IMS och [!DNL Adobe I/O]. Det stöder den växande rollen för Adobe Launch till instrument [!DNL Experience Manager] för analys och personalisering är anmälningsguiden funktionellt irrelevant. | Konfigurera systemanslutningar, Adobe IMS-autentisering och [!DNL Adobe I/O] integreringar via respektive [!DNL Experience Manager] molntjänster. |
| Anslutningar | Adobe JCR Connector för Microsoft® SharePoint 2010 och Microsoft® SharePoint 2013 är föråldrad för [!DNL Experience Manager] 6.5. | Ej tillämpligt |

## Kända fel {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THE LIST.
 -->

<!-- VULNERABILITY ISSUE - REMOVED MAY 23, 2022 AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * If you are using Content Fragments and GraphQL, Adobe recommends that you install the following packages on top of 6.5.12.0:

  * [AEM 6.5.12 Sites HotFix-NPR-38144](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Faem-service-pkg-6.5.12.0-NPR-38144-B0002.zip) (this hot fix replaces SP12, but can be installed on top of SP12) -->

* [AEM innehållsfragment med GraphQL-indexpaket 1.0.3](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.3.zip)

* Som [!DNL Microsoft® Windows Server 2019] stöder inte [!DNL MySQL 5.7] och [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] stöder inte körklara installationer för [!DNL AEM Forms 6.5.10.0].

* Om du uppgraderar dina [!DNL Experience Manager] från version 6.5 till 6.5.10.0 kan du visa `RRD4JReporter` undantag i `error.log` -fil. Starta om instansen för att lösa problemet.

* Om du installerar [!DNL Experience Manager] 6.5 Service Pack 10 eller ett tidigare Service Pack på [!DNL Experience Manager] 6.5, runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) tas bort.
Om du vill hämta körtidskopian rekommenderar Adobe att du synkroniserar designtidskopian av den anpassade arbetsflödesmodellen med körtidskopian med hjälp av HTTP API:
   `<designModelPath>/jcr:content.generate.json`.

* Användare kan byta namn på en mapp i en hierarki i [!DNL Assets] och publicera en kapslad mapp i [!DNL Brand Portal]. Mappens namn uppdateras dock inte i [!DNL Brand Portal] tills rotmappen publiceras på nytt.

* När en användare väljer att konfigurera ett fält för första gången i ett adaptivt formulär visas inte alternativet att spara en konfiguration i egenskapsläsaren. Om du väljer att konfigurera ett annat fält i det adaptiva formuläret i samma redigerare åtgärdas problemet.

* Följande fel och varningsmeddelanden kan visas under installationen av [!DNL Experience Manager] 6.5.x.x:
   * &quot;När Adobe Target-integreringen är konfigurerad i [!DNL Experience Manager] med Target Standard API (IMS-autentisering) och sedan exportera Experience Fragments till Target så att fel erbjudandetyper skapas. I stället för att skriva&quot;Experience Fragment&quot;/källa&quot;Adobe Experience Manager&quot; skapar Target flera erbjudanden med typen&quot;HTML&quot;/källa&quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Validering på serversidan av adaptiva formulär misslyckas när sammanställningsfunktioner som SUM, MAX och MIN används (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Aktiveringspunkten i en interaktiv Dynamic Media-bild syns inte när du förhandsvisar mediefilen via Shoppable Banner Viewer.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tidsgränsen överskreds i väntan på att reg.ändringen skulle slutföras utan registrering.

* När du försöker flytta/ta bort/publicera antingen innehållsfragment eller webbplatser/sidor uppstår ett problem när referenser till innehållsfragment hämtas, eftersom bakgrundsfrågan misslyckas. d.v.s. funktionen fungerar inte.
Du måste lägga till följande egenskaper i indexdefinitionsnoden för att få en korrekt åtgärd `/oak:index/damAssetLucene` (ingen omindexering krävs):

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## OSGi-paket och innehållspaket som ingår {#osgi-bundles-and-content-packages-included}

Följande textdokument listar de OSGi-paket och innehållspaket som ingår i [!DNL Experience Manager] 6.5.13.0:

* [Förteckning över OSGi-paket som ingår i Experience Manager 6.5.13.0](/help/release-notes/assets/65130_bundles.txt)

* [Förteckning över innehållspaket som ingår i Experience Manager 6.5.13.0](/help/release-notes/assets/65130_packages.txt)

## Begränsade webbplatser {#restricted-sites}

Dessa webbplatser är bara tillgängliga för kunder. Om du är kund och behöver åtkomst kontaktar du din kontoansvarige på Adobe.

* [Nedladdning av produkt på licensing.adobe.com](https://licensing.adobe.com/)
* [Kontakta Adobe kundsupport](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] produktsida](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* [Prenumerera på produktuppdateringar med Adobe prioritet](https://www.adobe.com/subscription/priority-product-update.html)

