---
title: Versionsinformation för  [!DNL Adobe Experience Manager] 6.5
description: Hitta versionsinformation, nyheter, installationsguider och en detaljerad ändringslista för  [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: d66d1a535ed4b1b8964139ffc5b110a5b52e32f1
workflow-type: tm+mt
source-wordcount: '5287'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] 6.5 Versionsinformation om senaste Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Versionsinformation {#release-information}

| Produkt | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.23.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Typ | Service Pack-version |
| Datum | Torsdag den 22 maj 2025 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Hämta URL | [Programdistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Vad ingår i [!DNL Experience Manager] 6.5.23.0 {#what-is-included-in-aem-6523}

[!DNL Experience Manager] 6.5.23.0 innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat samt felkorrigeringar. Det innehåller även förbättringar av prestanda, stabilitet och säkerhet som släppts sedan den första tillgängligheten av 6.5 i april 2019. [Installera detta Service Pack](#install) på [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

<!--
## Key features and enhancements

### Sites {#sites}

* A () -->

<!--
### [!DNL Assets]

* A ()
-->

<!--
### Forms {#forms-sp23}

Key features and enhancements in this release include the following:

#### New GA features in AEM Forms {#ga-aem-forms-sp23}

* A ()

#### New Beta features in AEM Forms {#beta-aem-forms-sp23}
-->

## Åtgärdade problem i Service Pack 23 {#fixed-issues}

<!-- 6.5.23.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-6523}

#### Tillgänglighet {#sites-accessibility-6523}

* Avsnitten på arbetsytan på AEM Editor har nu stöd för fullständig tangentbordstillgänglighet. Användarna kan bara aktivera avsnittsrubriker och redigera knappar med hjälp av tangentbordet, utan att behöva använda muspekaren. Uppdateringen säkerställer överensstämmelse med WCAG 2.1.1 och förbättrar användbarheten i komponenter som Teaser, Image, Carousel, Layout, Time Warp och Annotation. (SITES-25256) <!-- 6.5 LTS SP1 -->
* Korrigerade ett tillgänglighetsproblem i AEM Page Editor där tangentbordsfokus oväntat återställs till början av det demografiska verktygsfältet efter att knappar som Persona, Kundvagn eller Borttagen har aktiverats. Fokus ligger nu kvar på den aktiverade knappen för att ge stöd för enhetlig tangentbordsnavigering och arbetsflöden för skärmläsare. (SITES-25306)
* Korrigerade ett kritiskt hjälpmedelsproblem i AEM Page Editor där Canvas-element i flera dialogrutor och moduler (t.ex. Resursrand eller Layoutförhandsvisning) inte kunde användas med bara ett tangentbord. Alla interaktiva element på arbetsytan har nu stöd för navigering endast via tangentbordet, vilket säkerställer överensstämmelse med WCAG 2.1.1 (SITE-25256)
* Korrigerade ett tillgänglighetsproblem i användargränssnittet för Sites Admin där interaktiva listobjekt i popup-fönstret Skapa använde felaktiga ARIA-roller. Element som betedde sig som länkar tilldelades `role="listitem"` i stället för `role="menuitem"`, bröt mot ARIA-designmönstren och förvirrade skärmläsare. Uppdateringarna ser till att alla listkomponenter har rätt semantiska roller för förbättrat stöd för tangentbords- och hjälpfunktioner. (SITES-24493)
* Ett problem med associationen för hjälpmedelsetiketter för sidrubrik- och taggfält har åtgärdats. AEM-gränssnittet kopplar nu hjälpmedelsetiketter korrekt till fälten Rubrik och Sidtitel när du använder skärmläsare som JAWS. Korrigeringen säkerställer korrekt läsning av etiketter och förbättrar ADA-kompatibiliteten för sidgenerering, egenskaper och arbetsflöden. (SITES-27149)
* Korrigerade ett tillgänglighetsproblem med tabellidentifiering i dialogrutan för behörigheter. Behörighetstabellen i AEM använder nu korrekta ARIA-roller och -attribut för att säkerställa att skärmläsare som JAWS identifierar den som en tabell. Korrigeringen förbättrar tillgängligheten och säkerställer att användarna får rätt navigerings- och innehållsinformation. (SITES-27140)
* Korrigerat saknad visuell etikett för kommentarinmatningsfält på tidslinjen. Korrigerade saknade visuella etiketter för inmatningsfält för kommentarer under tidslinjen för att förbättra tillgängligheten. Uppdateringen ser till att skärmläsare kan meddela fältetiketterna korrekt. Den här upplevelsen förbättrar formulärnavigering och överföring för alla användare, särskilt de som använder hjälpmedelstekniker. (SITES-26903)
* Korrigerad tangentbordstillgänglighet för ellipsknappen i tidslinjekommentarer. Aktiverad tangentbordsnavigering för ellipsknappen (tre punkter) bredvid kommentarer under tidslinjeavsnittet. Användarna kan nu komma åt och interagera med knappen med tabbtangenten, vilket förbättrar tillgängligheten för användare som bara använder tangentbordsnavigering. (SITES-26891)
* Förbättrade NVDA-/Skärmläsarmeddelanden för sökresultat i urvalsdialogrutor. Uppdaterade dialogrutan Öppna markering för att meddela om sökresultat hittas eller inte när du använder skärmläsare, t.ex. NVDA eller Skärmläsaren. Denna förbättring hjälper användare som förlitar sig på hjälpmedelstekniker att förstå resultatet av sina sökåtgärder utan att behöva någon visuell bekräftelse. (SITES-26883)
* ARIA-rollen för ellipsikonen har korrigerats bredvid kommentarinmatningsfältet. Ellipsikonen (tre punkter) bredvid kommentarinmatningsfältet har uppdaterats så att rätt ARIA-roll används, vilket gör att skärmläsare kan identifiera elementet korrekt. Den här förbättringen förbättrar tillgängligheten och förbättrar upplevelsen för användare som använder hjälpmedelstekniker. (SITES-26881)
* Ogiltiga ARIA-attribut i Coral UI-komponenter har korrigerats. Uppdaterade Coral UI-komponenter för att säkerställa att alla ARIA-attribut använder giltiga värden, vilket förbättrar tillgängligheten. I synnerhet har fall där ogiltiga värden som `aria-modal="dialog"` har tilldelats felaktigt åtgärdats. Den här förbättringen gör att skärmläsare kan tolka element i dialogrutor korrekt, vilket förbättrar tillgängligheten för användare som använder hjälpmedelstekniker. (SITES-26873)
* Förbättrad synlighet och verktygstips för ikoner i flödesomformningsscenarier. Förbättrat flödesomformningsbeteende för att verktygstipsen ska visas korrekt för ikonerna **Hämta**, **Bearbeta resurser** och **Checka ut**. Fokuseras på ett hjälpmedelsproblem där ikoner och deras etiketter blev osynliga när visningsrutans storlek ändrades eller webbläsarens zoominställningar ändrades. Den här korrigeringen stöder användare med nedsatt syn genom att bibehålla synligheten och tillhandahålla korrekta ikonbeskrivningar under flödesomformningen. (SITES-26871)

#### Administratörsgränssnitt{#sites-adminui-6523}

Ett undantagsfel i URL-tjänsten för Universal Editor har korrigerats och Externalizer-slutpunkter saknas. URL-tjänsten för Universal Editor hanterar nu saknade författare, publiceringspunkter eller lokala Externalizer-slutpunkter utan att ge några undantag. Administratörsanvändare kan öppna sidredigeraren även när vissa Externalizer-konfigurationer är ofullständiga. (SITES-28877) <!-- LTS -->

#### Klassiskt användargränssnitt{#sites-classicui-6523}

* Ett problem i dialogrutor för klassiskt användargränssnitt där en knapp skulle dölja ett textområde och inte visas igen vid efterföljande klick. Med korrigeringen ser du till att textområdet visas igen när du växlar, vilket återställer förväntat beteende och förhindrar avbrott i dynamiska dialogrutearbetsflöden. (SITES-30230)
* Korrigerad funktion för avbildning av trasiga Classic UI-bilder efter uppgradering av Service Pack 2. I den klassiska sökaren för användargränssnittsbildresurser hanteras nu resursnamn som innehåller mellanslag eller specialtecken korrekt. Den här uppdateringen ser till att filnamnen kodas korrekt i resurssökaren, vilket förhindrar sökfel och gör att författare kan hitta och välja bildresurser utan fel. (SITES-29151)

#### [!DNL Content Fragments]{#sites-contentfragments-6523}

* Ett valideringstestfel för `DeleteVariationIT.testUpdateBasic` har korrigerats. `DeleteVariationIT.testUpdateBasic`-testet misslyckas inte längre när Service Pack-valideringen körs. Korrigeringen åtgärdar ett textmappningsfel som saknas i JSON-hanteringslogiken, vilket säkerställer teststabilitet och undviker onödiga testavbrott. (SITES-28022)
* AEM förhindrar nu prestandaförsämring på grund av felaktiga XMP-metadata i bildresurser. Assets som innehåller ogiltiga eller icke-kompatibla egenskapsnamn för XMP, t.ex. de med numeriska segment eller okvalificerade strukturer, utlöser inte längre upprepade varningsloggar under bearbetningen. Systemet filtrerar bort problematiska metadata för att säkerställa att inmatning och validering av resurser slutförs utan fel. (SITES-30683) <!-- AEM 6.5 LTS SP1 -->


<!-- #### [!DNL Content Fragments] - Admin{#sites-admin-6523}

* A () -->


#### [!DNL Content Fragments] - Fragmentredigeraren{#sites-fragments-editor-6523}

Andra författare kan fortfarande publicera innehållsfragment även när en annan författare checkar ut dem, vilket strider mot det avsedda beteendet för utcheckningsfunktionen. Den här korrigeringen förhindrar att andra användare ser eller använder publiceringsknapparna i redigeringsgränssnittet när ett innehållsfragment är utcheckat. (SITES-30578) <!-- LTS -->

#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6523}

Korrigerat GraphQL QueryValidationError med Content Fragment-scheman. Uppdatering av paketet `cq-dam-cfm-graphql` åtgärdar schemavalideringsfel när Content Fragment-referenser används. Korrigeringen ser till att GraphQL-frågor fungerar korrekt utan manuell schemajustering eller ompublicering efter paketdistributioner. (SITES-27001) <!-- LTS -->


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6523}

* A () -->

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6523}

* A () -->


#### Komponentkonsol{#sites-component-console-6523}

Förbättringar av sidinläsning för&quot;Component Live Usage&quot;. Optimerar sidan&quot;Använda komponenter direkt&quot; i AEM för att förhindra att tomma rader visas när du bläddrar igenom stora datauppsättningar. Användare som läser in komponenter med omfattande användningsreferenser kan nu få kontinuerlig datainläsning utan onödiga luckor eller tomma poster. Den här upplevelsen förbättrar sidnavigering, noggrannhet i spårningen och effektiviteten i hanteringen av rapporter om komponentanvändning. (SITES-26454)

#### Core Backend{#sites-core-backend-6523}

* Det gick inte att visa objekt i Finder för fast innehåll på grund av ogiltiga resursnamn. Innehållssökaren hanterar nu resursnamn med icke-kodade tecken korrekt. Resurslista i sidredigeraren misslyckas inte längre eller utlöser undantag när resurser med problematiska namn påträffas. (SITES-28722)
* Ett problem där komponenten `SearchPathLimiter` genererade för stora loggposter genom att skriva ut meddelanden på FEL-nivå för varje anrop. Detta beteende började efter Service Pack 17 och ledde till prestandaproblem på grund av extremt stora loggvolymer. Med korrigeringen nedgraderas loggnivån till DEBUG, vilket avsevärt minskar loggbruset och förbättrar systemövervakning och diagnostikeffektivitet. (SITES-29835)
* Felaktigt formaterade XMP-metadata utlöste ett fel vid bearbetning av bildresurser i `ValidationDataServlet`. Korrigeringen säkerställer kompatibel metadatahantering och undviker redundant parsning av ogiltiga egenskaper. (SITE-30683) <!-- LTS -->


<!-- #### Core Components{#sites-core-components-6523}

* A () -->

<!-- #### Campaign integration{#sites-campaign-integration-6523}

* A () -->

<!-- #### Experience Fragments{#sites-experiencefragments-6523}

* A () -->

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6523}

* A () -->


#### Launches{#sites-launches-6523}

* Korrigerat felaktigt startdatum mellan 25 december och 31 december. Startgränssnittet visar nu datum mellan 25 december och 31 december med rätt år. Programfixen säkerställer att datum inte längre visas felaktigt nästa år, vilket undviker förvirring under kampanjplanering och schemaläggning. (SITES-28706)
* Åtgärdade brutna AEM Launch-mallar efter uppgraderingen av Service Pack 2. AEM Launch-mallar läses nu in korrekt efter en uppgradering av Service Pack 2. Korrigeringen åtgärdar ogiltiga data i interna startkonfigurationer, vilket gör att användare kan visa, redigera och skapa startprogram utan fel eller fält som saknas. (SITES-28504)


<!-- #### Link Checker{#sites-link-checker-6523}

* A () -->

<!-- #### MSM - Live Copies{#sites-msm-live-copies-6523}

* A () -->


#### Page Editor{#sites-pageeditor-6523}

* Ett problem med att läsa in AssetPicker med lägre skärmupplösning har åtgärdats. AssetPicker läser nu in resurser korrekt när användare rullar med lägre skärmupplösning (1 728 × 1 117 eller lägre). Användarna upplever inte längre att resurser saknas vid bläddring, vilket förbättrar resurshanteringen över olika brytpunkter på enheten. (SITES-28065)
* Ett meddelande om att skärmläsaren saknas för åtgärder för att låsa och låsa upp sidor har åtgärdats. Sidredigeraren meddelar nu meddelandet&quot;Info: Sidan har låsts/låsts upp&quot; korrekt när användaren aktiverar knappen för lås/lås upp. Korrigeringen förbättrar tillgängligheten och ser till att skärmläsaranvändare får dynamiska uppdateringar under sidredigering. (SITES-27143)
* Förbättrat tangentbordsfokus för komponentåtgärder i AEM Authoring. Förbättrad tangentbordsnavigering i AEM Author-verktyget för att säkerställa att fokus ligger kvar på den nyskapade eller markerade komponenten efter åtgärder som Konfigurera, Ta bort eller Konvertera. Tidigare flyttades fokus till sidans överkant, vilket orsakade problem med kompatibiliteten. Den här uppdateringen förbättrar användarupplevelsen för användare av tangentbord och hjälpmedel. Det gör det genom att bibehålla det logiska fokusets förlopp i redigeringsarbetsflödet. (SITES-26549)
* Förbättrad tabbnavigering i redigeringsdialogrutor. Förbättrar tangentbordsnavigeringen i dialogrutorna för AEM Author genom att låta användare fortsätta att tabba framåt när redigeringsrutan Beskrivning har nåtts. Tidigare blockerade fokussvällning i fältet Beskrivning ytterligare navigering utan specialtangentkombinationer. Uppdateringen ser till att användarna smidigt kan navigera i fälten med bara tabbtangenten, vilket förbättrar tillgängligheten och användarupplevelsen. (SITES-26524)
* En regression introducerades i AEM 6.5 Service Pack 2 som förhindrade användare från att inkludera mellanslag i Launch-titlar. Med korrigeringen återställs möjligheten att använda blanksteg så att team kan definiera och organisera startnamnen mer flexibelt, i linje med förväntat beteende. (SITES-29414)
* Ett problem med storleksändring för komponenter i layoutbehållare har korrigerats efter dolda/visade åtgärder. Page Editor beräknar nu kolumnvärden korrekt efter att en layoutbehållare har dolts och tagits bort. Användare kan ändra storlek på komponenter utan fel, och kolumner visas korrekt vid storleksändring. (SITES-28463)
* Knappfel för fast innehållsträd i sidredigeraren. Sidredigeraren placerar nu konfigurationsknappen för innehållsträdet korrekt under den avsedda dialogrutan &quot;Head Teaser&quot; i stället för i fel avsnitt. Korrigeringen uppdaterar CSS för dialogrutan Innehållsträd så att den använder `top:0` i stället för `bottom:0`, vilket säkerställer korrekt placering av knapparna. (SITES-28448)


<!-- #### Replication{#sites-replication-6523}

* A () -->


#### RTF-redigerare{#sites-rte-6523}

Åtgärda oväntade `<br>`-taggar i RTF-redigeraren med inklistringsläge. RTF-redigeraren hanterar nu klipp ut och klistra in-åtgärder korrekt när du använder klartext `defaultPasteMode`. Korrigeringen förhindrar infogning av oväntade `<br>`-taggar när användare klipper ut och klistrar in text i RTE-fält, vilket ger en ren formatering vid redigering av innehåll. (SITES-27780)

#### Universell redigerare {#sites-universal-editor-6523}

* När flera begäranden som innehåller frågeparametern skickas till AEM, kan cookie-filen för inloggningstoken inte returneras i tid, vilket kan leda till en misslyckad inloggning. (SITES-30659) <!-- LTS -->
* För att säkerställa kompatibilitet och stöd med SAML-hanterare måste du konfigurera egenskapen `service.ranking` så att `Query Token Auth`-hanteraren kör *före* `SAML Auth`-hanteraren. (SITES-29684)

### [!DNL Assets]{#assets-6523}

* Följande problem kan uppstå på navigeringssidan [!DNL AEM] lokalt (6.5.22.0) när du har valt ![Assets ](/help/assets/assets/Smock_Asset_18_N.svg)**[!UICONTROL Assets]**, navigerat till mappen **[!UICONTROL Search Adobe Stock]**&#x200B;och valt en stockbild:
   * Den valda stockbilden kan inte licensieras och sparas eftersom en tom listruta visas när du klickar på **[!UICONTROL License & Save]**.
   * Om du väljer Stock-bilden eller anger URL:en för Stock-sidan igen dirigeras den till hemsidan [!DNL AEM], vilket förhindrar åtkomst till Adobe Stock-bilden. (ASSETS-48687)
* Problem vid hantering av mappar om namnet på mappen innehåller `/` i namnet på navigeringssidan [!DNL AEM] On-Premise (6.5.22.0). (ASSETS-46740)
* På [!DNL AEM] 6.5 läses sidan med resursinformation inte in från vyn ![ Samling ](/help/assets/assets/Smock_Collection_18_N.svg)**[!UICONTROL Collections]**&#x200B;på grund av hög minnesanvändning. (ASSETS-46738)
* Integrationsproblem med [!DNL InDesign] som `Day CQ DAM Mime Type OSGI`-tjänst identifierar felaktigt [!DNL InDesign]-filer som `x-adobe-indesign` i stället för `x-indesign`. (ASSETS-4953)
* Sessionsläckan [!DNL AEM 6.5.21] spårade till det körklara **[!UICONTROL Scheduled publish to Brand Portal]**-arbetsflödessteget. (ASSETS-44104)
* **[!UICONTROL Out of Memory (OOM)]** fel visas i [!DNL AEM] vid bearbetning och publicering av bilder. Det här problemet berodde på föråldrade metoder i arbetsflöden, som **[!DNL Dam Asset update]** och **[!DNL Dynamic Media: Reprocess assets]**. (ASSETS-4343)
* När du har gjort en mindre ändring, till exempel uppdaterat titeln, öppnar du **[!DNL Connected Assets configuration]** igen och sparar om den på den lokala platsinstansen. Fjärrinstansen förlorar sedan anslutningen till den lokala instansen. Det innebär att det inte går att upprätta kommunikation med den lokala platsinstansen. (ASSETS-4484)
* I [!DNL AEM 6.5.21] visas ett **[!UICONTROL 0 of NaN assets uploaded]**-fel när en överföring av en resurs i listvyn avbryts och en andra överföring utförs. [!DNL AEM] (ASSETS-44124)

#### [!DNL Dynamic Media]{#assets-dm-6523}

En metadataegenskap (`jcr:content/metadata/dam:scene7SmartCropStatus`) har lagts till i resurser för identifiering av misslyckade Smart Crop-generationer. Möjliggör effektiv sökning, filtrering och ombearbetning av resurser med problem med Smart Crop via manuella eller automatiserade arbetsflöden. (ASSETS-46237)

#### [!DNL Dynamic Media] - hybridläge {#assets-dm-hybrid-6523}

##### Dynamic Media - tilläggspaket för hybrid (AEM 6.5.23 och senare)

Från och med AEM 6.5 Service Pack 23 finns ett nytt tilläggspaket för Dynamic Media - hybrid-läge. Det här paketet innehåller paketet `cq-scene7-imaging` som är specifikt kompatibelt med körningsläget Dynamic Media - Hybrid.

**Nyckelkorrigering ingår**

Korrigerade ett problem i Dynamic Media - Hybrid-distributioner där uppdateringar av parametern `catalog.expiration` under `/conf/global/settings/dam/dm/imageserver` inte reflekterades på server- eller författarens URL:er, trots att replikeringen lyckades utan fel. Uppdateringen säkerställer enhetliga utgångsvärden mellan CRX/DE, serversvar och URL:er för offentlig leverans. I sin tur förbättras funktionen för cache-lagring och tillförlitligheten i bildomvandlingar. (ASSETS-4837)

**Viktiga överväganden**

* Paketet `cq-scene7-imaging` i den grundläggande AEM 6.5.23-installationen (och senare) är *inte kompatibelt* med körläget Dynamic Media - Hybrid.
* Endast installation av Service Pack 23 (och senare) uppdaterar *inte automatiskt* befintligt `cq-scene7-imaging`-paket på AEM-instanser som konfigurerats för Dynamic Media - Hybrid (`-r dynamicmedia` körningsläge).

**När tilläggspaketet Hybrid ska installeras**

* Vid uppgradering direkt till AEM 6.5.23 (och senare) från AEM 6.5.19 eller tidigare.
* När du behöver korrigeringar som är specifika för Dynamic Media - Hybrid-funktionen.
* Vid driftsättning av nya Dynamic Media - Hybrid-instanser direkt från AEM 6.5 GA (General Availability) till Service Pack 23 (och senare).

**Hämta tilläggspaket för hybrid**

Tilläggspaketet Hybrid är öppet för distribution av Adobe-program från och med torsdagen den 22 maj 2025, med den officiella versionen av AEM 6.5.23. Användare kan hitta det genom att söka efter **AEM 6.5 Dynamic Media Hybrid Add-on Package** i Software Distribution.


### [!DNL Forms]{#forms-6523}

Korrigeringar i [!DNL Experience Manager] Forms levereras via ett separat tilläggspaket en vecka efter den schemalagda versionen av [!DNL Experience Manager] Service Pack. I det här fallet planeras AEM 6.5.23.0 Forms-tilläggspaketets release för torsdagen den 29 maj 2025. En lista över Forms-korrigeringar och förbättringar har lagts till i det här avsnittet när utgåvan släppts.

#### Forms Captcha {#forms-captcha-6523}

* Förbättrade reCAPTCHA-varningar i Adaptive Forms genom att uppdatera skicka-felkoder till 400. Du kan även förfina loggvarningar för att skilja mellan tidsgränser, förfallodatum och fel vid robotidentifiering, vilket förbättrar felsökningsnoggrannheten och systemobserverbarheten. (FORMS-19240)
* En oavslutad `ResourceResolver`-instans i `ReCaptchaConfigurationServiceImpl` stängdes för att förhindra potentiella resursläckor och förbättra systemstabiliteten när du använder reCAPTCHA-integreringar i AEM Forms. (FORMS-1924)
* Förbättrad CAPTCHA-konfigurationshantering för AEM Forms genom att se till att rätt konfigurations-binder till varje formulär när det finns flera poster i mappen `/conf/global`. Förhindrar oavsiktlig användning av felaktiga CAPTCHA-inställningar när konfigurationsbehållaren inte uttryckligen har valts. (FORMS-19239)


<!--
#### XMLFM {#forms-xmlfm-6523}

* A () -->

<!--
#### [!DNL Adaptive Forms] {#adaptive-forms-6523}

* A () -->

<!--
#### [!DNL Forms Designer] {#forms-designer-6523}

* A () -->


### Foundation {#foundation-6523}

* Korrigerade ett fel i Coral Alert Banners där textfärgen ser vit ut i stället för svart efter uppgradering till Service Pack 21. Ser till att rätt formatering används för att upprätthålla korrekt kontrast och läsbarhet för varningsmeddelanden i hela gränssnittet. (NPR-42359)
* Stöd för OAuth-integrering i konfigurationen av smarta taggar har lagts till för anpassning till borttagningen av JWT (JSON Web Token). Säkerställer fortsatt funktionalitet för smarta taggar med uppdaterade autentiseringsmetoder. (NPR-42296)

#### Apache Felix {#foundation-apachefelix-6523}

Korrigerade ett NullPointerException som inträffade när privata nyckelfiler överfördes till ett egenskapsfält av binär typ i CRX, vilket återställde kompatibiliteten som fanns i Service Pack 16. Möjliggör säkra arbetsflöden för överföring av nyckelfiler i AEM Managed Services utan serverfel eller avbrott i certifikatförnyelseprocessen. (CQ-4359178)


<!--
#### Campaign{#foundation-campaign-6523}

* A () -->

<!--
#### Cloud Services{#foundation-cloudservices-6523}

* A () -->

<!--
#### Communities {#foundation-communities-6523}

* A () -->

<!--
#### Content distribution{#foundation-content-distribution-6523}

* A () -->

<!--
#### CRX {#foundation-crx-6523}

* A () -->


#### Granit{#foundation-granite-6523}

* Löste OSGi-beroendecykler mellan Apache Sling-skripttjänster som orsakade fördröjningar eller fel vid inläsning av HTML-sidor efter uppgradering till Service Pack 21. Uppdaterade interna tjänstreferenser för att ta bort cykliska beroenden som inbegriper `SightlyScriptingEngineFactory` och relaterade komponenter, vilket förbättrar skriptmotorns tillförlitlighet och startbeteende. GRANITE-56808
* Uppdaterade JS använder skript i Apache Sling för att endast läsa in on-demand i stället för att snabbt starta, vilket eliminerar trådproblem och minskar risken för att publiceringsservrar inte svarar vid inläsning. Den här ändringen förbättrar serverstabiliteten och svarstiderna under högtrafikscenarier genom att förhindra resurslås som orsakas av tidig skriptupplösning. (GRANITE-56611)
* Ett problem har korrigerats i AEM Omnissearch där platshållare för inmatningsfält felaktigt visas som etiketter, vilket leder till visuell förvirring. Säkerställer korrekt återgivning av platshållare över filterfält, vilket ger ett konsekvent och tillgängligt formulärbeteende. (GRANITE-51791)
* Löste ett serverfel som utlöstes när fler än 30 CFM:er (Content Fragment Models) valdes med multifältsreferenser i modellredigeraren för innehållsfragment. Förbättrade filterförslagskomponenten som stöder POST-åtgärder. Denna funktion gör att stora referensuppsättningar kan hanteras på rätt sätt när innehållsfragment skapas och att stabiliteten för modellkonfigurationer med stora volymer förbättras. (GRANITE-57164)
* Löste ett problem i CFM:er där användaren oavsiktligt växlade läget genom att klicka nära en kryssruta. Uppdaterade format som begränsar klickaktiveringen till kryssruteelementet, förhindrar oavsiktliga användarinteraktioner och förbättrar formuläranvändbarheten och tillgängligheten. GRANITE-52384


<!--
#### Integrations{#foundation-integrations-6523}

* A () -->


#### Jetty{#foundation-jetty-6523}

Löste ett problem där SNI-validering blockerade API-anrop via HTTPS för AEM-kunder som använder Dispatcher SSL-konfigurationer med anpassade värdhuvuden. Introducerar ett alternativ för att inaktivera SNI-validering som en del av Jetty-konfigurationen, vilket möjliggör kompatibilitet med specifika omvända proxyinställningar där `mod_proxy` inte är möjligt. (NPR-42614)


<!--
#### Localization{#foundation-localization-6523}

* A () -->

<!--
#### Oak {#foundation-oak-6523}

* A () -->


#### Plattform{#foundation-platform-6523}

* Ett inkonsekvent beteende för taggsammanfogning har åtgärdats genom att det sammanslagna taggvärdet alltid visas korrekt i alla resurser, oavsett om taggarna skapas inline eller med standardmetoden för att skapa taggar. Förhindrar att restvärden från `EN:title`-fält åsidosätter visningen av sammanfogade taggar. (CQ-4358812)
* Korrigerad upprepad kodning av et-tecken i taggvärden i dialogrutan för taggredigering. Förhindrar att extra &quot;&amp;&quot;-entiteter läggs till varje gång du sparar, vilket säkerställer att taggvärdena förblir rena och konsekventa vid redigeringar och att fel i det redigerade innehållet undviks. (CQ-4359048)
* Ett `ClassCastException`-fel som förhindrar e-postleverans vid sändning av adaptiva formulär i AEM 6.5 som körs på WebSphere® har åtgärdats. Korrigeringen möjliggör e-postöverföring genom att säkerställa kompatibilitet mellan `com.sun.mail.handlers.text_plain` och `java.activation.DataContentHandler`, i enlighet med den e-posthanterarkonfiguration som förväntas av WebSphere®-miljöer. (NPR-42500)
* Förbättrad felhantering i Package Manager genom att säkerställa att AEM får ett tydligt meddelande när installationen misslyckas och att felsvaret annars är tomt. Den här korrigeringen förhindrar tysta fel och hjälper till att felsöka snabbare vid paketdistribution. (NPR-42375)

<!--
#### Security{#foundation-security-6523}

* A -->

<!--
#### Sling{#foundation-sling-6523}

* A () -->


#### Översättning{#foundation-translation-6523}

Korrigerade ett NullPointerException-problem (NPE) som utlöstes vid uppdatering av innehållsfragment i arbetsflöden med **Uppdatera språkkopia**. Med den här korrigeringen kan du säkerställa att arbetsflöden inte försätts i ett feltillstånd eller fastnar i ett körningsläge när du redigerar innehåll som är kopplat till översättningsreferenser. (NPR-42115)

#### Användargränssnitt{#foundation-ui-6523}

Lägger till saknade `title`-attribut i dialogruteknappar för korallgränssnitt, till exempel **Klar** och **Avbryt**, i dialogrutorna för komponentredigering för att förbättra tillgängligheten och aktivera automatisk validering. Ser till att knappar behåller förväntade attribut vid markeringsåtergivning och förhindrar fel i självbaserade gränssnittstester. (NPR-42412)

#### WCM{#foundation-wcm-6523}

Korrigerade ett problem som förhindrar att sidor läggs till i översättningsjobb när **Uppdatera språkkopia** används i miljöer med Service Pack 19 eller senare. Ser till att översättningsarbetsflöden fortsätter som förväntat, vilket möjliggör korrekt sidöverföring mellan språkkopior utan manuell åtgärd. (CQ-4357929)

#### Arbetsflöde{#foundation-workflow-6523}

Löste ett problem i `EmailNotificationServiceProcessor` där metoden `getSegmentId` returnerar `null` efter snabbkorrigeringsdistributionen, vilket medförde att e-postutlösare misslyckades under arbetsflödesbearbetningen. Återställer korrekt logik för segment-ID-matchning genom att se till att processorn hämtar de `SegmentInfo` värden som krävs för att stödja arbetsflöden för e-postmeddelanden i alla AEM-instanser. (CQ-4359755)


## Installera [!DNL Experience Manager] 6.5.23.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.23.0 kräver [!DNL Experience Manager] 6.5. Mer information finns i [ uppgraderingsdokumentationen ](/help/sites-deploying/upgrade.md) . <!-- UPDATE FOR EACH NEW RELEASE -->
* Hämtningen av Service Pack är tillgänglig på Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip).
* Installera [!DNL Experience Manager] 6.5.23.0 på en av författarinstanserna med Package Manager på en distribution med MongoDB och flera instanser.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe rekommenderar inte att du tar bort eller avinstallerar paketet [!DNL Experience Manager] 6.5.23.0. Därför bör du skapa en säkerhetskopia av `crx-repository` innan du installerar paketet, ifall du måste återställa det. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### Installera Service Pack på [!DNL Experience Manager] 6.5{#install-service-pack}

1. Starta om instansen innan installationen om instansen är i uppdateringsläge (när instansen uppdaterades från en tidigare version). Adobe rekommenderar att du startar om om den aktuella upptiden för en instans är hög.

1. Ta en ögonblicksbild eller en ny säkerhetskopia av din [!DNL Experience Manager]-instans innan du installerar.

1. Hämta Service Sack från [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Öppna Pakethanteraren och välj sedan **[!UICONTROL Upload Package]** för att överföra paketet. Mer information finns i [Pakethanteraren](/help/sites-administering/package-manager.md).

1. Markera paketet och välj sedan **[!UICONTROL Install]**.

1. Om du vill uppdatera S3-anslutningen stoppar du instansen efter installationen av Service Pack, byter ut den befintliga kopplingen mot en ny binär fil som finns i installationsmappen och startar om instansen. Se [Amazon S3-datalager](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Dialogrutan i pakethanterarens gränssnitt stängs ibland under installationen av Service Pack. Adobe rekommenderar att du väntar på att felloggarna ska stabiliseras innan du får åtkomst till distributionen. Vänta på de specifika loggarna för avinstallationen av uppdateringspaketet innan du försäkrar dig om att installationen lyckas. Vanligtvis inträffar det här problemet i webbläsaren [!DNL Safari], men kan inträffa i alla webbläsare.

**Automatisk installation**

Det finns två olika metoder att använda för att installera [!DNL Experience Manager] 6.5.23.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Placera paketet i mappen `../crx-quickstart/install` när servern är tillgänglig online. Paketet installeras automatiskt.
* Använd [HTTP-API:t från Package Manager](/help/sites-administering/package-manager.md#package-share). Använd `cmd=install&recursive=true` så att kapslade paket installeras.

>[!NOTE]
>
>Experience Manager 6.5.23.0 stöder inte installation av Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Verifiera installationen**

Information om vilka plattformar som är certifierade för att fungera med den här versionen finns i [tekniska krav](/help/sites-deploying/technical-requirements.md).

1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience Manager (6.5.23.0)` under [!UICONTROL Installed Products]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Alla OSGi-paket är antingen **[!UICONTROL ACTIVE]** eller **[!UICONTROL FRAGMENT]** i OSGi-konsolen (använd webbkonsol: `/system/console/bundles`).

1. OSGi-paketet `org.apache.jackrabbit.oak-core` är version 1.2.20 eller senare (Använd webbkonsol: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### Installera Service Pack för [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Instruktioner om hur du installerar Service Pack på Experience Manager Forms finns i [Installationsanvisningar för Experience Manager Forms Service Pack](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>Den adaptiva Forms-funktionen, som finns i [AEM 6.5 QuickStart](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/deploying/deploying/deploy), är endast avsedd för utforsknings- och utvärderingsändamål. För produktion krävs en giltig licens för AEM Forms, eftersom Adaptive Forms-funktionaliteten kräver rätt licensiering.

### Installera GraphQL Index Package för Experience Manager Content Fragments{#install-aem-graphql-index-add-on-package}

Kunder som använder GraphQL måste installera [Experience Manager Content Fragment med GraphQL Index Package 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

På så sätt kan du lägga till den indexdefinition som krävs baserat på de funktioner som de faktiskt använder.

Om du inte installerar det här paketet kan GraphQL-frågor bli långsamma eller misslyckas.

>[!NOTE]
>
>Installera bara det här paketet en gång per instans. Det behöver inte installeras om med varje Service Pack.

### UberJar{#uber-jar}

UberJar för [!DNL Experience Manager] 6.5.23.0 är tillgänglig i [Maven Central-databasen](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.22/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Om du vill använda UberJar i ett Maven-projekt ska du läsa [Använda UberJar](/help/sites-developing/ht-projects-maven.md) och inkludera följande beroende i projektstrukturen: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.23</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar och andra relaterade artefakter är tillgängliga i Maven Central Repository i stället för i Adobe Public Maven-databasen (`repo.adobe.com`). Huvudfilen för UberJar har bytt namn till `uber-jar-<version>.jar`. Det finns alltså ingen `classifier`, med `apis` som värde, för taggen `dependency`.



## Föråldrade och borttagna funktioner{#removed-deprecated-features}

Se [Inaktuella och borttagna funktioner](/help/release-notes/deprecated-removed-features.md/) för en detaljerad lista över alla funktioner som har tagits bort eller tagits bort för AEM 6.5.

### SPA Editor {#spa-editor}

[SPA-redigeraren](/help/sites-developing/spa-overview.md) har tagits bort för nya projekt från och med version 6.5.23 av AEM 6.5. SPA-redigeraren stöds fortfarande för befintliga projekt, men bör inte användas för nya projekt.

De redigerare som rekommenderas för hantering av headless-innehåll i AEM är nu:

* [Den universella redigeraren](/help/sites-developing/universal-editor/introduction.md) för visuell redigering.
* [Innehållsfragmentsredigeraren](/help/sites-developing/universal-editor/introduction.md) för formulärbaserad redigering.

## Kända fel{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **Problem med JSP-skriptpaket i AEM 6.5.21-6.5.23 och AEM 6.5 LTS GA**
AEM 6.5.21, 6.5.22, 6.5.23 och AEM 6.5 LTS GA innehåller paketet `org.apache.sling.scripting.jsp:2.6.0` som påverkas av ett känt fel. Detta problem uppstår oftast under höga inläsningsförhållanden när många samtidiga begäranden bearbetas av AEM-instansen.

När det här problemet inträffar kan ett av följande undantag visas i felloggarna tillsammans med referenser till `org.apache.sling.scripting.jsp:2.6.0`:

* `java.io.IOException: classFile.delete() failed`
* `java.io.IOException: tmpFile.renameTo(classFile) failed`
* `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
* `java.io.FileNotFoundException`

När det här felet inträffar är den enda återställningsmetoden att starta om AEM-instansen.

Kontakta Adobe kundsupport och läs den här versionsinformationen för att få en lösning.

* **Relaterat till Oak**
Från Service Pack 13 och senare har följande fellogg börjat visas som påverkar persistence-cachen:

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  eller

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  Så här löser du det här undantaget:

   1. Ta bort följande två mappar från `crx-quickstart/repository/`

      * `cache`
      * `diff-cache`

   1. Installera Service Pack eller starta om Experience Manager as a Cloud Service.
Nya mappar i `cache` och `diff-cache` skapas automatiskt och du får inte längre något undantag relaterat till `mvstore` i `error.log`.

* Uppdatera dina GraphQL-frågor som kan ha använt ett anpassat API-namn för innehållsmodellen så att standardnamnet för innehållsmodellen används i stället.

* En GraphQL-fråga kan använda indexvärdet `damAssetLucene` i stället för indexvärdet `fragments`. Den här åtgärden kan leda till att GraphQL-frågor misslyckas eller tar lång tid att köra.

  För att åtgärda problemet måste `damAssetLucene` konfigureras att inkludera följande två egenskaper under `/indexRules/dam:Asset/properties`:

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  När indexdefinitionen har ändrats krävs en omindexering (`reindex` = `true`).

  Efter dessa steg bör GraphQL-frågorna gå snabbare.

* När du försöker flytta, ta bort eller publicera antingen innehållsfragment, webbplatser eller sidor, uppstår ett problem när referenser till innehållsfragment hämtas. Bakgrundsfrågan misslyckas. Funktionen fungerar alltså inte.
För att säkerställa korrekt åtgärd måste du lägga till följande egenskaper i indexdefinitionsnoden `/oak:index/damAssetLucene` (ingen omindexering krävs):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Om du uppgraderar din [!DNL Experience Manager]-instans från 6.5.0 till 6.5.4 till den senaste Service Pack-versionen av Java™ 11 visas `RRD4JReporter` undantag i `error.log` -filen. Starta om instansen av [!DNL Experience Manager] om du vill stoppa undantagen. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Användare kan byta namn på en mapp i en hierarki i [!DNL Assets] och publicera en kapslad mapp till [!DNL Brand Portal]. Mappens namn uppdateras dock inte i [!DNL Brand Portal] förrän rotmappen publiceras på nytt.

* Följande fel och varningsmeddelanden kan visas under installationen av [!DNL Experience Manager] 6.5.x.x:
   * &quot;När Adobe Target-integreringen har konfigurerats i [!DNL Experience Manager] med hjälp av Target Standard API (IMS-autentisering) skapas felaktiga erbjudandetyper när Experience Fragments exporteras till Target. I stället för att skriva&quot;Experience Fragment&quot;/källa&quot;Adobe Experience Manager&quot; skapar Target flera erbjudanden med typen&quot;HTML&quot;/källa&quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Inga underhållsfönster hittades på `granite/operations/maintenance`.
   * Validering på serversidan av adaptiva formulär misslyckas när sammanställningsfunktioner som SUM, MAX och MIN används (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : Inga underhållsfönster hittades på `granite/operations/maintenance`.
   * Den aktiva punkten i en interaktiv Dynamic Media-bild visas inte när du förhandsgranskar resursen via visningsprogrammet för den köpbara kanalen.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Timeout uppstod i väntan på att registerändringen skulle slutföras utan registrering.

* Från och med AEM 6.5.15 har den Rhino JavaScript-motor som tillhandahålls av paketet ```org.apache.servicemix.bundles.rhino``` ett nytt värdbeteende. Skript som använder strikt läge (```use strict;```) måste deklarera sina korrekta variabler. Annars körs de inte, vilket resulterar i ett körningsfel.

* Om du installerar taggning av relaterat innehåll som inte finns i kartongen med hjälp av ett officiellt uppdateringspaket återställs språkegenskapen för noden `/content/cq:tags` till standardvärdet. Den här åtgärden gäller för Service Packs, Security Service Pack, Extended Feature Packs, Cumulative Feature Packs, Patches osv. Det är därför nödvändigt att lägga till den från egenskaperna före installationen.

### Känt problem för AEM Sites {#known-issues-aem-sites-6523}

* Content Fragments-Preview misslyckas på grund av DoS-skydd för ett stort träd med fragment. Se artikeln [KB om standardkonfigurationsalternativ för GraphQL Query Executor](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934)



### Kända fel för AEM Forms {#known-issues-aem-forms-6523}

* Om konverteringen från HTML till PDF misslyckas på en SUSE® Linux®-server (SLES 15 SP6 och senare) med följande fel:

  ```Auto configuration failed 4143511872:error:0E079065:configuration file routines:DEF_LOAD_BIO:missing equal sign:conf_def.c:362:line 57```
Ange sedan följande miljövariabel och starta om servern:
  `OPENSSL_CONF=/etc/ssl`

* När du har installerat AEM Forms JEE Service Pack 21 (6.5.21.0) utför du följande steg för att lösa problemet om du hittar dubblettposter för Geode jars `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` i mappen `<AEM_Forms_Installation>/lib/caching/lib` (FORMS-14926):

   1. Stoppa positionerarna om de är igång.
   1. Stoppa AEM Server.
   1. Gå till `<AEM_Forms_Installation>/lib/caching/lib`.
   1. Ta bort alla Geode-korrigeringsfiler utom `geode-*-1.15.1.2.jar`. Bekräfta att det bara finns Geode-burkar med `version 1.15.1.2`.
   1. Öppna kommandotolken i administratörsläge.
   1. Installera Geode-korrigeringen med filen `geode-*-1.15.1.2.jar`.

* Om en användare försöker förhandsgranska ett utkast med sparade XML-data fastnar den i läget `Loading` för vissa specifika bokstäver. Läs artikeln [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) om du vill hämta och installera snabbkorrigeringen. (FORMS-14521)

* När du har uppgraderat till AEM Forms Service Pack 6.5.21.0 misslyckas tjänsten `PaperCapture` med att utföra OCR-åtgärder (Optical Character Recognition) på PDF-filer. Tjänsten genererar inte utdata i form av en PDF- eller loggfil. Läs artikeln [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) om du vill hämta och installera snabbkorrigeringen. (CQDOC-21680)

* När användare uppgraderade från AEM 6.5 Forms Service Pack 18 eller 19 till Service Pack 20 eller 21 uppstod ett JSP-kompileringsfel. Det här felet hindrade dem från att öppna eller skapa anpassade formulär. Den orsakade även problem med andra AEM-gränssnitt. Gränssnitten innehåller sidredigeraren, användargränssnittet i AEM Forms, arbetsflödesredigeraren och användargränssnittet för systemöversikt. (FORMS-1256)

  Om du råkar ut för ett sådant problem följer du de här stegen för att lösa det:
   1. Navigera till katalogen `/libs/fd/aemforms/install/` i CRXDE.
   1. Ta bort paketet med namnet `com.adobe.granite.ui.commons-5.10.26.jar`.
   1. Starta om AEM Server.

* Efter uppdatering till AEM Forms Service Pack 20 (6.5.20.0) med Forms Add-On slutar konfigurationer som är beroende av den äldre Adobe Analytics Cloud-tjänsten med hjälp av autentiseringsbaserad autentisering att fungera. Det här problemet förhindrade att analysreglerna kördes korrekt. Läs artikeln [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) om du vill hämta och installera snabbkorrigeringen. (FORMS-15428)

* När en användare uppdaterar till AEM Forms Service Pack 20 (6.5.20.0) på JEE-servern och genererar PDF-filer med hjälp av utdatatjänster, återges PDF-filerna med tillgänglighetsproblem. Läs artikeln [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) om du vill hämta och installera snabbkorrigeringen. (LC-3922112)
* När en användare genererar taggade PDF-filer med hjälp av utdatatjänsten för JEE visas&quot;Olämplig strukturvarning&quot;. Läs artikeln [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) om du vill hämta och installera snabbkorrigeringen. (LC-3922038)
* När ett formulär skickas i AEM Forms JEE tas instanser av ett upprepat XML-element bort från data. Läs artikeln [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) om du vill hämta och installera snabbkorrigeringen. (LC-3922017)
* När en användare i en Linux®-miljö återger ett adaptivt formulär (i JEE) i HTML återges det inte korrekt. Läs artikeln [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) om du vill hämta och installera snabbkorrigeringen. (LC-3921957)
* När en användare konverterar en XTG-fil till PostScript-format med hjälp av utdatatjänsten i AEM Forms JEE misslyckas den med följande fel: `AEM_OUT_001_003: Unexpected Exception: PAExecute Failure: XFA_RENDER_FAILURE`. Läs artikeln [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) om du vill hämta och installera snabbkorrigeringen. (LC-3921720)
* När en användare har uppgraderat till AEM Forms Service Pack 18 (6.5.18.0) på JEE-servern kan den inte återge HTML5 eller PDF forms och XMLFM när ett formulär skickas. Läs artikeln [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) om du vill hämta och installera snabbkorrigeringen. (LC-3921718)
* I förhandsgranskningen av gränssnittet för Interactive Communications Agent visas valutasymbolen (till exempel dollartecknet $) inkonsekvent för alla fältvärden. Den visas för värden upp till 999 men saknas för värden över 1 000. (FORMS-1657)
* Eventuella ändringar av det kapslade layoutfragmentets XDP i en interaktiv kommunikation återspeglas inte i IC-redigeraren. (FORMS-16575)
* I förhandsgranskningen av gränssnittet för den interaktiva kommunikationsagenten visas vissa beräknade värden inte korrekt. (FORMS-16603)
* När brevet visas i Förhandsgranska utskrift ändras innehållet. Vissa blanksteg försvinner och vissa bokstäver ersätts med `x`. (FORMS-15681)
* När en användare konfigurerar en WebLogic 14c-instans misslyckas PDFG-tjänsten i AEM Forms Service Pack 21 (6.5.21.0) på JEE som körs på JBoss® på grund av klassinläsarkonflikter i SLF4J-biblioteket. Felet visas enligt följande (CQDOC-22178):

  ```java
  Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
  the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
  @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
  (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
  have different Class objects for the type org/slf4j/ILoggerFactory used in the signature
  ```



## OSGi-paket och innehållspaket som ingår{#osgi-bundles-and-content-packages-included}

Följande textdokument innehåller en lista över de OSGi-paket och innehållspaket som ingår i den här versionen av [!DNL Experience Manager] 6.5 Service Pack:

* [Lista över OSGi-paket som ingår i Experience Manager 6.5.23.0](/help/release-notes/assets/65230-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista över innehållspaket som ingår i Experience Manager 6.5.23.0](/help/release-notes/assets/65230-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->



## Begränsade webbplatser{#restricted-sites}

Dessa webbplatser är endast tillgängliga för kunder. Kontakta din kontoansvarige på Adobe om du är kund och behöver åtkomst.

* [Nedladdning av produkt på licensing.adobe.com](https://licensing.adobe.com/)
* [Kontakta Adobe kundsupport](https://experienceleague.adobe.com/en/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] produktsida](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5-dokumentation](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [Prenumerera på Adobe Priority-produktuppdateringar](https://www.adobe.com/subscription/priority-product-update.html)
