---
title: Versionsinformation för [!DNL Adobe Experience Manager] 6.5
description: Hitta versionsinformation, nyheter, installationsanvisningar och en detaljerad ändringslista för [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
exl-id: 38227a66-f2a9-4909-9297-1eced4ed6e8c
source-git-commit: e73a65569963a5f60f7a4670998ada29deeb26b8
workflow-type: tm+mt
source-wordcount: '3999'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] 6.5 Versionsinformation om senaste Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession&cid=a915e87c-369a-480c-9daf-d13efc766798 -->

## Versionsinformation {#release-information}

| Produkt | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.15.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Typ | Service Pack-version |
| Date | 24 november 2022 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Hämta URL | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Vad ingår i [!DNL Experience Manager] 6.5.15.0 {#what-is-included-in-aem-6515}

[!DNL Experience Manager] 6.5.15.0 innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat, felkorrigeringar, prestanda, stabilitet och säkerhetsförbättringar som släppts sedan den första tillgängligheten av 6.5 i april 2019. [Installera detta Service Pack](#install) på [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_

* Added support for password reset for Dynamic Media Classic users within Experience Manager. (ASSETS-10298) -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6515}

* Om rörelsen av en resurs i Experience Manager misslyckas kan resursen fortfarande byta namn. (NPR-38753)
* När du visar resurserna i en [!UICONTROL List View], vissa av titlarna saknas. (CQ-4345746)
* Skärmläsaren meddelar inte undermenyn till [!UICONTROL Relate] på fliken Grundläggande på sidan Resursegenskaper. (ASSETS-6938)
* Skärmläsaren identifierar felaktigt mappikonerna på navigeringssidan Resurser med listan över mappar. (ASSETS-6936)
* När du kopierar en samling saknar bilden en tom `alt` attribute or role=&quot;presentation&quot;. Därför visas bilden för skärmläsaranvändare. (ASSETS-6932)
* Texten som visas när en resurs kommenteras har inte en 4:5:1 kontrastförhållande jämfört med bakgrundsfärgen. (ASSETS-6931)
* När du justerar sidbredden på fliken IPTC på sidan Resursegenskaper passas inte sidinnehållet korrekt och resultatet blir vågrät rullning. (ASSETS-6929)
* När du filtrerar resurser visas filtertexten i [!UICONTROL min] och [!UICONTROL max] fält försvinner när ett värde har angetts. (ASSETS-6925)
* I Experience Manager-samlingar visas inte skärmläsaren [!UICONTROL email] på hämtningsskärmen. (ASSETS-6923)
* En alternativ text saknas när elementen kommenteras. (ASSETS-6922)
* Om texten skrivs i fältet Timmar och Minuter i datumväljaren visas inget textfelmeddelande. Felet identifieras bara med den röda färgen. (ASSETS-6852, ASSETS-6921, ASSETS-6920, ASSETS-6907)
* Alternativ text i `[role='img']` i filtret Filer saknas. (ASSETS-6919)
* Felaktigt skärmläsarmeddelande för [!UICONTROL Create] undermeny. (ASSETS-6916)
* Ta bort-knappen i Experience Manager-samlingar `X` har ingen text att meddela skärmläsarna. (ASSETS-6912)
* När du använder Color Contrast Analyzer i Experience Manager finns det ingen färgskillnad mellan det aktuella datumet och det valda datumet i datumväljaren i kalenderwidgeten. Det saknas minst 3:1 kontrastförhållande i förhållande till de intilliggande färgerna. (ASSETS-6911)
* I Experience Manager-filer när du väljer något av alternativen i [!UICONTROL Scheduling] alternativknappen i Hantera publikation visas alternativknappens namn och läge av skärmläsaren. Men **Schemaläggning** etiketten visas inte. (ASSETS-6908, ASSETS-6906)
* Den alternativa texten saknas för sorteringsikonen. (ASSETS-6904)
* På sidan Resursegenskaper anger fältnamnet `Person` i fliketiketterna för IPTC-tillägg visas inte av skärmläsarna. Skärmläsaren meddelar endast redigerbara och tomma fält, men inte etikettnamnet. (ASSETS-6903, ASSETS-6848)
* Anteckningsverktyget kan inte visas med tangentbordet. En mus används för att rita en bild som visar anteckningsverktyget. (ASSETS-6899)
* I Experience Manager Collections (Samlingar) finns ett tomt fält på **Avancerat** på fliken visas ett felaktigt kontrastförhållande mellan gränsen och en intilliggande färg. (ASSETS-6895)
* Felaktiga ARIA-attributvärden för vissa element när du redigerar resurser. (ASSETS-6894)
* Skärmläsaren identifierar inte rubriken korrekt när ett arbetsflöde skapas. (ASSETS-6892)
* När du kopierar en samling tar du bort SVG-knappen `X` with role=&quot;img&quot; saknar en role=&quot;presentation&quot;. Därför visas bilden för skärmläsaranvändare. (ASSETS-6890)
* I **Grundläggande** på fliken Resursegenskaper kan skärmläsaren inte meddela att fältet Taggar är expanderat eller komprimerat på rätt sätt. (ASSETS-6889)
* The **Grundläggande** under Resursegenskaper innehåller sidor med duplicerat ID. (ASSETS-6888)
* Etiketten för textfältet som definierar en titel när du skapar ett arbetsflöde försvinner när du anger ett värde i textrutan. (ASSETS-6887)
* Listan över mottagare när en länk delas visas som en datatabell med rubriker, men identifieras inte semantiskt som en datatabell för skärmläsaranvändare. (ASSETS-6886)
* Inget felmeddelande som representerar ett tomt fält visas i `Add Email Address` fält. Felet representeras bara av en färg. (ASSETS-6885, ASSETS-6843)
* Platshållartexter, Bana och Alt-text har inte minst kontrastförhållandet 4,5:1 jämfört med bakgrundsfärgen. (ASSETS-6884, ASSETS-6865)
* Ogiltiga värden för vissa ARIA-attribut när en smart samling sparas. (ASSETS-6882)
* När du sparar en smart samling är vissa av etiketterna inte korrekt kopplade till skärmläsaren. (ASSETS-6881)
* På IPTC-fliken i Resursegenskaper meddelar skärmläsaren inte etiketten för nyckelordsformulärfälten. (ASSETS-6879)
* I Experience Manager-samlingar finns [!UICONTROL Email] fältet identifieras inte som ett obligatoriskt fält och inget felmeddelande visas om du inte anger något värde. (ASSETS-6877)
* I Experience Manager-filer visas inget felmeddelande i **Länkdelning** skärm visas i `Add Email Address`. Felet identifieras bara när en färg används. (ASSETS-6876, ASSETS-6875)
* [!UICONTROL Crop and Map] alternativ har inte programmatiska namn när en resurs redigeras. (ASSETS-6874)
* Filtertexten saknar kontrastförhållande på 4,5:1 jämfört med bakgrundsfärgen. (ASSETS-6873)
* Texten för mappnamnet på huvudnavigeringssidan har inte ett kontrastförhållande på 4,5:1 jämfört med bakgrundsfärgen. (ASSETS-6872)
* När du utför [!UICONTROL Copy] för samlingar, **[!UICONTROL Add User]** formulärkontroll för kombinationsruta är inte korrekt kopplad till dess synliga etikett. (ASSETS-6870)
* Skärmläsaren meddelar inte [!UICONTROL Create] alternativ på undermenyn. (ASSETS-6869)
* Alternativen Omfång, Arbetsflöden och Tidszon har inte ett kontrastförhållande på 4,5:1 jämfört med bakgrundsfärgen. (ASSETS-6868)
* Skärmläsaren meddelar felaktigt komprimeringsläget för **Tidslinje** kolumn. (ASSETS-6864)
* Underordnade element saknas för vissa ARIA-roller när en smart samling sparas. (ASSETS-6862)
* Nödvändiga ARIA-attribut för när en resurs delas `Search/Add Email Address` har inte angetts. (ASSETS-6860)
* The **map** kan inte visas med tangentbordet. Du måste i stället klicka med musen för att visa kartdialogrutan. (ASSETS-6859)
* Underordnade element saknas för vissa ARIA-roller på fliken Grundläggande på sidan Resursegenskaper. (ASSETS-6858)
* De tomma textinmatningsfälten, som finns på IPTC-fliken i Resursegenskaper, har inte ett kontrastförhållande på 3:1 jämfört med de intilliggande färgerna. (ASSETS-6854, ASSETS-6847)
* Profilikonerna i **Tidslinje** -avsnittet identifieras felaktigt av skärmläsarna. (ASSETS-6850)
* Skärmläsaren meddelar inte att kombinationsrutan Granskningsstatus, som finns på fliken Grundläggande i Resursegenskaper, är ett skrivskyddat fält. (ASSETS-6849)
* Skärmläsaren meddelar inte etiketten för kryssrutorna Markera alla och Anteckning korrekt. (ASSETS-6846)
* Tangentbordsfokus hoppar över `About Adobe Experience Manager` finns i **Visa hjälpen** -menyn. (ASSETS-6845)
* Skärmläsare meddelar inte de valda mapparna korrekt när de navigerar i mapplistan med tangentbordspilarna i kortvyn. (ASSETS-6844)
* När du överför ett PDF till Experience Manager ökar minnesanvändningen hela tiden. (ASSETS-16889)
* När ett arbetsflöde konverterar en ZIP-fil till ett mappnamn i Resurser, behålls inte skiftläget för ZIP-filnamnet. (ASSETS-16712)
* När du växlar från Brand Portal till Experience Manager 6.5 visas inte rätt resultat i predikatfiltret när du tillämpar filtret för första gången. (ASSETS-15932)
* Det går inte att kommentera en video. (ASSETS-15217)
* **Hantera publikation** alternativet försvinner för en användare utan replikåtkomst och `READ` och `WRITE` behörighet till `ETC` och `VAR`. (ASSETS-15007)
* Inläsningstiden för egenskapssidan ökar för en resurs med flera referenser. (ASSETS-14182)
* När en bild avpubliceras från Brand Portal återpubliceras den även av Experience Manager från Dynamic Media, och därför visas ingen bild på den publicerade webbplatsen. (ASSETS-14118)
* XSS-problem med Smart Crop-kort i Dynamic Media. (ASSETS-14212, ASSETS-14208, ASSETS-13704)
* XSS-problem i visningsförinställningar i Dynamic Media. (ASSETS-13822)
* Validera användaråtkomst när du förhandsgranskar DM-resurser på AEM. (CQ-4314757)


## Handel {#commerce-6515}

* Det gick inte att skapa en butikssida, vilket stoppar den övergripande katalogdistributionsprocessen. (CQ-4347181)

## [!DNL Forms] {#forms-6515}

### Viktiga funktioner {#keyfeatures}

* AEM Forms Designer finns nu i [Spanska](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html). (LC-3920051)
* Du kan nu använda [OAuth2 för autentisering med Microsoft® Office 365 e-postserverprotokoll (SMTP och IMAP)](/help/forms/using/oauth2-support-for-mail-service.md). (NPR-35177)
* Du kan ange [Återvalidera på servern](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#enabling-server-side-validation-br) egenskapen true för att identifiera dolda fält som ska uteslutas från ett postdokument på serversidan. (NPR-38149)
* AEM Forms Designer kräver 32-bitarsversionen av Visual C++ 2019 Redistributable (x86).  (NPR-36690)

### Korrigeringar {#fixes}

* När egenskapen data-disabled i ett adaptivt formulär är aktiverad ändras inte utseendet på alternativknappar och grupper med kryssrutor. (NPR-39368)
* När ett adaptivt formulär översätts saknas vissa översättningar och visas inte korrekt. (NPR-39367)
* När en sidas egenskap är dold tas sidan inte bort från formatuppsättningen. (NPR-39325)
* I ett postdokument finns inte det dynamiska fotnotsavsnittet i slutet av sidan. (NPR-39322)
* När ett postdokument genereras för ett anpassat formulär tillåts endast vertikal justering för alternativknappar och kryssrutor. Användaren kan inte ange vågrät justering för alternativknappar och kryssrutor. (NPR-39321)
* Efter driftsättning av Correspondence Management blir org.apache.sling.i18n.impl.JcrResourceBundle.loadPotentialLanguageRoots flaskhals och en majoritet av trådarna nås om flera användare försöker få åtkomst till ett formulär. Det tog ofta mer än en minut att läsa in olika förfrågningar från formulärsidor, även när servern har mycket låg belastning. (NPR-39176, CQ-4347710)
* När du använder ett RTF-fält i ett lazy loaded Adaptive Form-fragment i ett adaptivt format kan följande fel uppstå:
   * Du kan inte redigera innehållet eller lägga till något till RTF-fältet.
   * Visningsmönstret som används på den formaterade texten respekteras inte. 
   * Felmeddelandet för minsta fältlängd visas inte när formuläret skickas.
   * Innehållet i det här RTF-fältet tas med flera gånger i den färdiga submit-XML-filen. (NPR-39168)
* När datumväljaralternativet används i ett adaptivt formulär konverteras inte värdet till rätt format. (NPR-39156)
* När du förhandsgranskar ett anpassat formulär som ett HTML återges det inte korrekt, eftersom vissa av delformulären överlappar det överordnade formuläret. (NPR-39046)
* Om panelen har dold tabell och anpassningsbara formulär återges i tabellvy, visas inte fälten på den första fliken korrekt. (NPR-39025)
* The `Body` -taggen saknas för OTB-mallen (Out-of-the-Box). (NPR-39022)
* Registreringsdokumentet genereras inte på det anpassade formulärets språk. Den genereras alltid på engelska. (NPR-39020)
* När ett adaptivt formulär har flera paneler och vissa paneler använder de medföljande **Bifogad fil** -komponenten, `Error occurred while draft saving` fel inträffar. (NPR-38978)
* När `=` -tecknet används i fälten för kryssrutor, nedrullningsbara listor eller alternativknappar i ett adaptivt formulär och dokumentet för registrering genereras. `=` -tecknet är inte synligt i det genererade postdokumentet.(NPR-38859)
* Antalet meddelandebatchbearbetningsfel ökar dubbelt efter uppgraderingen av Service Pack 6.5.11.0. (NPR-39636)
* Om du inte anger testdata går det inte att läsa in Correspondence Management-brev i agentens användargränssnitt. (CQ-4348702)
* När en användare tillämpar AEM Forms Service Pack 14 (SP14) från AEM Forms som distribuerats med IBM® WebSphere® misslyckas startkomponenten när en databas initieras och `java.lang.NoClassDefFoundError:org/apache/log4j/Logger` fel inträffar.(NPR-39414)
* När du använder API:t för Document Service för att certifiera PDF misslyckas det på ett AEM formulär på OSGi-servern med följande fel: com.adobe.fd.signatures.truststore.errors.exception.CredentialRetrievalException: AEM-DSS-311-003. (NPR-38855)
* När användaren försöker använda wrapper-tjänsten för att återge bokstäver med AEM 6.3 Forms `java.lang.reflect.UndeclaredThrowableException` fel inträffar. (CQ-4347259)
* När en XDP återges som HTML5-formulär återges innehållet på den överordnad sidan först oavsett var objekten finns i ett anpassat formulär. (CQ-4345218)
* Konfigurationen av programmet på målservern ändras till de inställningar som definierats på källservern även om **Skriv över konfigurationen när importen är klar** alternativet är inte markerat när programmet importeras. (NPR-39044)
* När en användare försöker uppdatera kopplingskonfigurationen med Configuration Manager misslyckas det.(CQ-4347077)
* När en användare försöker köra ett AEM formulär på en JEE-korrigering efter att administratörsanvändarens standardlösenord ändrats, uppstår ett undantag `com.adobe.livecycle.lcm.core.LCMException[ALC-LCM-200-003]: Failed to whitelist the classes` inträffar. (CQ-4348277)
* I AEM Designer placeras formulärfält utan bildtexter i tabellceller, inklusive kryssrutor.(LC-3920410)
* När användaren försöker öppna hjälpen i AEM Forms Designer visas den inte korrekt. (CQ-4341996)

## [!DNL Sites] {#sites-6515}

* Experience Manager Sites Launches console was getting up blank. (NPR-39188)
* Referenserna justerades inte när sidan som hade referensen också behövde aktiveras när sidan flyttades. (NPR-39061)
* När en layoutbehållare inte döljs med den överordnade behållaren tillämpas inte layoutändringar på alla komponenter i den kapslade behållaren. (NPR-39041)
* Innehållet överlappar nu inte längre annat innehåll med en bredd på 320 pixlar. (SITES-8885)
* Fokus har lagts till efter att en dialogruta stängts. (SITES-8885)

### Tillgänglighet {#access-6515}

<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The scrollable region of the Page Editor did not have keyboard access. (SITES-2936) -->
<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The color input field of the Page Editor is not labeled or visible on the screen. (SITES-2925) -->
<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The iframe in the Page Editor is missing a title attribute; it must have an accessible name. (SITES-2894) -->
* The **[!UICONTROL Annotation]** knappens hjälpmedelsnamn saknas. (SITES-2892)
* Status för en ACTIVE-användargränssnittskomponent (**[!UICONTROL Cut]**, **[!UICONTROL Copy]**, **[!UICONTROL Paste]**, **[!UICONTROL Insert Components]**, **[!UICONTROL Group]** och så vidare) har inte minst tre till ett luminiscensförhållande med antingen den inre eller yttre intilliggande bakgrunden. (SITES-8889, SITES-8756, SITES-8885)
* Statusmeddelandet har inte annonserats automatiskt. (SITES-8889, SITES-8756, SITES-8885)
* Textinnehållet saknar kontrastförhållande på 4,5:1. (SITES-8756, SITES-8885)
* Länk- eller knapptext saknar kontrastförhållande på 4,5:1 vid hovring eller fokus. (SITES-8756, SITES-8885)

### [!DNL Content Fragments] {#sites-contentfragments-6515}

* GraphQL genererar ett undantag. Du kan till exempel inte hämta varianttaggar från ett innehållsfragment. Det finns ingen variation med namnet&quot;elektrisk&quot;. Problemet beror på att du ringer `getVariationTags` för en icke-befintlig variation som ger upphov till ett undantag. (SITES-8898)
* Sortera titelordning i listvyn, både stigande och fallande, och hur rubrikerna med ordningen A, C och B ska se ut. (SITES-7585)
* Taggningsstöd för varianter av innehållsfragment har lagts till. (SITES-8168)
* Identifierade och tog bort Odin-specifik kod från Experience Manager 6.5 som inte behövdes. (SITES-3574)
* När du publicerade ett fragment av en språkkopia från användargränssnittet i Content Fragment Editor publicerades de associerade referenserna i mappen English. (NPR-39182)
* Datumfält fylls i med ett datum. (NPR-39124)
* Taggar försvann den andra gången du markerar alternativknappsalternativet. (NPR-39071)

### Fluid XP {#sites-fluidxp-6515}

* Aktivera stöd för ES6-kompilering för klientbiblioteket `/libs/cq/gui/components/siteadmin/admin/restoretree/clientlibs/restoretree.js`. (NPR-39067)
* Multifältet i en innehållsfragmentmodell kan inte tömmas och sparas eftersom valideringen sker även om **[!UICONTROL Required]** är inte markerat. (NPR-39063)
* I antingen **[!UICONTROL Copy]** eller **[!UICONTROL Livecopy]** uppgifter, `cq:targetMetadata` informationen duplicerades felaktigt. Den här funktionen gjorde att två eller flera Experience Fragments i Experience Manager pekade på samma erbjudande som exporterades som mål. (NPR-38970)
* Efter en åtgärd av typen Återställ träd visas meddelandet `Un-publication pending. #0 in the queue` visas i användargränssnittet för en sida som inte har publicerats alls. (NPR-38847)

### Page Editor {#sites-pageeditor-6515}

* Ångra tog inte bort den senaste ändringen av text som lades till i komponenten. När sidan uppdaterades togs i stället hela komponenten bort. (SITES-8597)
* Uppgraderar `jquery-ui` till den senaste versionen resulterade i att sidredigeraren inte fungerade korrekt. (NPR-38596)
* Innehållet överlappar nu inte längre annat innehåll med en bredd på 320 pixlar. (SITES-8756)
* lade till fokus efter att dialogrutan stängts (SITES-8756)

## Sling {#sling-6515}

* `Repoinit` stöder inte skapande eller hantering av grupper med tomt utrymme i huvudnamnet eftersom gruppnamnet behandlades som en sträng och det gick inte att citera. (SLING-10952)
* Loggar fylls av misstag med felmeddelanden och undantag. (NPR-39024)

## Översättningsprojekt {#translation-6515}

* Målsidan lades till i översättningsjobbet för uppdaterade språkkopior via projektpanelen. källsidan uppdaterades inte. (NPR-39278)
* Översättningsprocessen misslyckades när en förhandsgranskning genererades för alla sidor i ett översättningsprojekt. (NPR-39059)
* Om språkinställningen inte finns skapas den fortfarande i en språkområdesmapp när referensregler har konfigurerats för en händelse. (NPR-39054)

## Användargränssnitt {#ui-6515}

* JavaScript-fel inträffar i filen `multifield.js` för vissa fält i modellen för innehållsfragment i modellredigeraren för innehållsfragment och även i redigeraren för innehållsfragment. (NPR-39350)

## Arbetsflöde {#workflow-6515}

* Arbetsflödena som gick bra på Experience Manager 6.5.11 kördes inte enhetligt på 6.5.13 i Experience Manager. (NPR-39023)

## Installera [!DNL Experience Manager] 6.5.15.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.15.0 kräver [!DNL Experience Manager] 6.5. Se [uppgraderingsdokumentation](/help/sites-deploying/upgrade.md) för detaljerade anvisningar. <!-- UPDATE FOR EACH NEW RELEASE -->
* Service Pack-nedladdning finns på Adobe [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* På en distribution med MongoDB och flera instanser installerar du [!DNL Experience Manager] 6.5.15.0 på en av författarinstanserna med hjälp av Package Manager.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
>Adobe rekommenderar inte att du tar bort eller avinstallerar [!DNL Experience Manager] 6.5.15.0-paket. Innan du installerar paketet bör du skapa en säkerhetskopia av `crx-repository` om du behöver rulla tillbaka den. <!-- UPDATE FOR EACH NEW RELEASE -->

### Installera Service Pack på [!DNL Experience Manager] 6.5 {#install-service-pack}

1. Starta om instansen innan installationen om instansen är i uppdateringsläge (när instansen uppdaterades från en tidigare version). Adobe rekommenderar att du startar om om den aktuella upptiden för en instans är hög.

1. Ta en ögonblicksbild eller en ny säkerhetskopia av din [!DNL Experience Manager] -instans.

1. Hämta Service Pack från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Öppna Pakethanteraren och välj **[!UICONTROL Upload Package]** för att överföra paketet. Mer information finns på [Pakethanteraren](/help/sites-administering/package-manager.md).

1. Markera paketet och välj **[!UICONTROL Install]**.

1. Om du vill uppdatera S3-anslutningen stoppar du instansen efter installationen av Service Pack, byter ut den befintliga kopplingen mot en ny binär fil som finns i installationsmappen och startar om instansen. Se [Amazon S3 - datalager](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Dialogrutan för pakethanterarens gränssnitt avslutas ibland när Service Pack installeras. Adobe rekommenderar att du väntar på att felloggarna ska stabiliseras innan du får åtkomst till distributionen. Vänta på de specifika loggarna för avinstallationen av uppdateringspaketet innan du försäkrar dig om att installationen lyckas. Vanligtvis inträffar detta problem i [!DNL Safari] webbläsare, men kan ibland inträffa i vilken webbläsare som helst.

**Automatisk installation**

Det finns två olika metoder som du kan använda för att installera automatiskt [!DNL Experience Manager] 6.5.15.0<!-- UPDATE FOR EACH NEW RELEASE -->

* Placera paketet i `../crx-quickstart/install` när servern är tillgänglig online. Paketet installeras automatiskt.
* Använd [HTTP-API från Package Manager](/help/sites-administering/package-manager.md#package-share). Använd `cmd=install&recursive=true` så att de kapslade paketen installeras.

>[!NOTE]
>
>Experience Manager 6.5.15.0 stöder inte installation av Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validera installationen**

Om du vill veta vilka plattformar som är certifierade för att fungera med den här versionen kan du läsa [tekniska krav](/help/sites-deploying/technical-requirements.md).

1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience Manager (6.5.15.0)` under [!UICONTROL Installed Products]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Alla OSGi-paket är antingen **[!UICONTROL ACTIVE]** eller **[!UICONTROL FRAGMENT]** i OSGi Console (Use Web Console: `/system/console/bundles`).

1. OSGi-paketet `org.apache.jackrabbit.oak-core` är version 1.2.2.13 eller senare (Använd webbkonsol: `/system/console/bundles`). <!-- NPR-39436 for 6.5.15.0 --> <!-- OAK VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installera [!DNL Experience Manager] Forms tilläggspaket {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Hoppa över om du inte använder [!DNL Experience Manager] Forms.

<!-- 
Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.
-->

1. Kontrollera att du har installerat [!DNL Experience Manager] Service Pack.
1. Ladda ned motsvarande tilläggspaket från Forms på [AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) för ditt operativsystem.
1. Installera Forms tilläggspaket enligt beskrivningen i [Installera AEM Forms tilläggspaket](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).
1. Om du använder bokstäver i Experience Manager 6.5 Forms installerar du [senaste AEMFD-kompatibilitetspaket](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates).

### Installera [!DNL Experience Manager] Forms på JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Hoppa över om du inte använder AEM Forms på JEE. Korrigeringar i [!DNL Experience Manager] Forms på JEE levereras via ett separat installationsprogram.

Utför följande steg för alla AEM Forms i JEE-miljöer med andra programservrar än JBoss EAP 7.4.0.
1. Installera [AEM Forms JEE Patch](jee-patch-installer-65.md). Den innehåller alla åtgärdade fel för alla komponenter i AEM 6.5 Forms på JEE.
1. Installera [Fragment för AEM 6.5 Forms för JEE Service Pack 15](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar). Fragmentet lägger till de beroenden som krävs för att installera AEM Service Pack 15 (6.5.15.0).
1. När du har installerat fragmentet väntar du tills programservern har stabiliserats.
1. [Installera Service Pack på Experience Manager 6.5](#install-service-pack).

   >[!NOTE]
   >
   >Om du installerar den senaste [AEM Service Pack (6.5.15.0)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)innan du installerar [Fragment för AEM 6.5 Forms för JEE Service Pack 15](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) på din AEM 6.5 Forms i JEE-miljö kan CRX/bundle och startsidan sluta fungera och du får ett fel om att tjänsten inte är tillgänglig. Utför åtgärderna för att lösa problemet [listas här](/help/forms/using/aem-service-pack-installation-solution.md).
1. Installera [senaste Forms-tilläggspaketet](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html), tar du bort Forms-tilläggspaketet från `crx-repository\install` och starta om servern.

### UberJar {#uber-jar}

UberJar för [!DNL Experience Manager] 6.5.15.0 finns i [Maven Central-arkivet](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.15/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Information om hur du använder UberJar i ett Maven-projekt finns i [använda UberJar](/help/sites-developing/ht-projects-maven.md) och inkludera följande beroende i projektens POM: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.15</version>
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
| Integreringar | The **[!UICONTROL AEM Cloud Services Opt-In]** skärmen är föråldrad sedan [!DNL Experience Manager] och [!DNL Adobe Target] integreringen uppdateras i [!DNL Experience Manager] 6.5. Integreringen stöder Adobe Target Standard API. API:t använder autentisering via Adobe IMS och [!DNL Adobe I/O Runtime]. Det stöder den växande rollen för Adobe Launch till instrument [!DNL Experience Manager] för analys och personalisering är anmälningsguiden funktionellt irrelevant. | Konfigurera systemanslutningar, Adobe IMS-autentisering och [!DNL Adobe I/O Runtime] integreringar via respektive [!DNL Experience Manager] molntjänster. |
| Anslutningar | Adobe JCR Connector för Microsoft® SharePoint 2010 och Microsoft® SharePoint 2013 är föråldrad för [!DNL Experience Manager] 6.5. | Ej tillämpligt |

## Kända fel {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->

* [AEM innehållsfragment med GraphQL indexpaket 1.0.5](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip)
Det här paketet behövs för kunder som använder GraphQL. på så sätt kan de lägga till den indexdefinition som behövs baserat på de funktioner de faktiskt använder.

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
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tidsgränsen överskreds i väntan på att registerändringen skulle slutföras utan registrering.

* När du försöker flytta/ta bort/publicera antingen innehållsfragment eller webbplatser/sidor uppstår ett problem när referenser till innehållsfragment hämtas, eftersom bakgrundsfrågan misslyckas. d.v.s. funktionen fungerar inte.
Du måste lägga till följande egenskaper i indexdefinitionsnoden för att få en korrekt åtgärd `/oak:index/damAssetLucene` (ingen omindexering krävs):

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## OSGi-paket och innehållspaket som ingår {#osgi-bundles-and-content-packages-included}

Följande textdokument listar de OSGi-paket och innehållspaket som ingår i [!DNL Experience Manager] 6.5.15.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Förteckning över OSGi-paket som ingår i Experience Manager 6.5.15.0](/help/release-notes/assets/65150_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Förteckning över innehållspaket som ingår i Experience Manager 6.5.15.0](/help/release-notes/assets/65150_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Begränsade webbplatser {#restricted-sites}

Dessa webbplatser är bara tillgängliga för kunder. Om du är kund och behöver åtkomst kontaktar du din kontoansvarige på Adobe.

* [Nedladdning av produkt på licensing.adobe.com](https://licensing.adobe.com/)
* [Kontakta Adobe kundsupport](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] produktsida](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* [Prenumerera på produktuppdateringar med Adobe prioritet](https://www.adobe.com/subscription/priority-product-update.html)

