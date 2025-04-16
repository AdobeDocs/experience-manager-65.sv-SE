---
title: Versionsinformation för  [!DNL Adobe Experience Manager] 6.5
description: Hitta versionsinformation, nyheter, installationsguider och en detaljerad ändringslista för  [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 461ec6a48bc41d46338c2c0162869525e49de97f
workflow-type: tm+mt
source-wordcount: '6127'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] 6.5 Versionsinformation om senaste Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Versionsinformation {#release-information}

| Produkt | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.22.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Typ | Service Pack-version |
| Datum | Torsdag den 21 november 2024 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Hämta URL | [Programdistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Vad ingår i [!DNL Experience Manager] 6.5.22.0 {#what-is-included-in-aem-6522}

[!DNL Experience Manager] 6.5.22.0 innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat samt felkorrigeringar. Det innehåller även förbättringar av prestanda, stabilitet och säkerhet som släppts sedan den första tillgängligheten av 6.5 i april 2019. [Installera detta Service Pack](#install) på [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## Viktiga funktioner och förbättringar

### Forms {#forms-sp22}

Bland huvudfunktionerna och förbättringarna i den här versionen finns följande:

#### Nya GA-funktioner i AEM Forms {#ga-aem-forms-sp22}

* Stöd har lagts till för att aktivera teckensnittsinbäddning i [API:er för Interactive Communications Batch](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/interactive-communications/create-interactive-communication#output-format-print-channel) - Interactive Communications har nu stöd för inbäddning av Adobe Ming- och Adobe Myungjo-teckensnitt i PDF-filer som genererats via Batch API. Den här förbättringen säkerställer korrekt textåtergivning i genererade dokument, även när deluppsättningar av teckensnitt används, vilket ger bättre stöd för flerspråkigt innehåll i PDF-utdata.

* [Tabell över innehåll-API för PDF Accessibility](/help/forms/using/aem-document-services-programmatically.md#auto-tag-pdf-documents-auto-tag-api) - AEM Forms på OSGi har nu stöd för det nya TOC Tag API:t för att förbättra PDF för tillgänglighetsstandarder. Det gör PDF-filer mer tillgängliga för användare med hjälpmedel.

* [Fragment-XDP-upplösning](/help/forms/using/assembler-service.md#resolve-references-on-crx-repository-resolve-references-on-crx-repository) - AEM Forms på OSGi löser nu fragment-XDP:er som refereras i primära XDP:er och lagras i AEM CRX-databasen.

* [Kompatibilitetsförbättringar för PDF/A](/help/forms/developing/pdf-a-documents.md#converting-documents-to-pdfa-documents-converting-documents-to-pdf-a-documents) - Nu kan användare konvertera PDF-filer till PDF/A-format (1a, 2a, 3a) i arkiveringssyfte samtidigt som de säkerställer tillgänglighet och verifierar överensstämmelse med dessa standarder.

* **Stöd för automatisk storleksändring av teckensnitt för statiska PDF-dokument** - AEM Forms Designer, OutputService och FormsService har nu stöd för automatisk storleksändring av teckensnitt för statiska PDF-filer. Om användaren anger teckenstorleken 0 för text-, numeriska fält, lösenordsfält eller datumtidsfält justeras teckensnittsstorleken automatiskt i dessa fält utan att ändra fältets totala storlek. Användarna skickar en flagga i den anpassade XCI:n `<behaviorOverride>patch-LC-3921991:1</behaviorOverride>` för att använda funktionen.

#### Nya Beta-funktioner i AEM Forms {#beta-aem-forms-sp22}

Betafunktionen ger dig en unik möjlighet att få exklusiv tillgång till de senaste innovationerna och hjälper dig att utveckla dem. Vill du aktivera en betafunktion för dina miljöer? Skicka ett e-postmeddelande från din officiella adress till aem-forms-ea@adobe.com med en lista över funktioner som du är intresserad av.

* [hCaptcha](/help/forms/using/integrate-adaptive-forms-hcaptcha.md) och [Cloudflare Turnstile CAPTCHA-tjänster](/help/forms/using/integrate-adaptive-forms-turnstile.md): AEM Forms stöder följande Captcha-tjänster:
   * Captcha skyddar formulär från stötar, skräppost och automatiskt missbruk genom att utmana användare med en kryssrutewidget. Det säkerställer att endast mänskliga användare går vidare och förbättrar säkerheten vid onlinetransaktioner.
   * Cloudflare Turnstile erbjuder en säkerhetsåtgärd som syftar till att skydda formulär från automatiserade robotar, skadliga attacker, skräppost och oönskad automatiserad trafik. Den visar en kryssruta när formuläret skickas in för att verifiera att det är humant, innan det går att skicka in formuläret.

* Versionshantering för adaptiva formulär:
   * [Skapa flera versioner av ett adaptivt formulär](/help/forms/using/add-versioning-reviews-comments.md) - Nu kan användare enkelt hantera varianter av befintliga formulär. Denna process förenklar versionskontrollen och underlättar jämförelse för formuläroptimering, allt i ett enda smidigt arbetsflöde.
   * [Jämför adaptiv Forms](/help/forms/using/compare-forms-core-components.md): Nu kan användare enkelt jämföra två formulär för att identifiera skillnader. Det underlättar smidigt samarbete genom att teammedlemmarna kan jämföra revisioner och diskutera ändringar effektivt.

<!-- * _6.5.21.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

### Sites {#sites}

[Den universella redigeraren](/help/sites-developing/universal-editor/introduction.md) finns nu i AEM 6.5 för headless-användning med ett funktionspaket.

### [!DNL Assets]

IPTC-fliken har nu stöd för textfälten [!UICONTROL Alt Text] och [!UICONTROL Extended Description]. (ASSETS-34918)

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Åtgärdade problem i Service Pack 22 {#fixed-issues}


### [!DNL Sites]{#sites-6522}


#### Tillgänglighet {#sites-accessibility-6522}

* Det saknades ett hjälpmedelsnamn för knappen för val av anteckningsfärgruta. Det vill säga att det inte finns något namn på knappen som kan tolkas av användaren när ett nytt hexvärde har angetts. (SITES-11992)
* Följande element på menyn för den vänstra listen visas som en lista men markeras inte som sådana i skärmläsaren:

   * Plats
   * Live copy
   * Starta
   * Språkkopia
   * Mapp
   * CSV-rapport (SITES-2874)

* AEM Core Web Content Management kräver en hjälpmedelsetikett för hyperlänkar i RTF-redigeraren. När en hyperlänk används i textkomponenten bör ankartaggen innehålla attributet `aria-label` för att säkerställa att skärmläsare kan läsa och förmedla länktexten korrekt i hjälpmedelssyfte. (SITES-11511)
* I AEM har de interaktiva elementen i tabellrubriken i listvyn inte den knapproll som krävs. Skärmläsaren NVDA meddelar därför inte de förväntade knapprollerna för följande tabellrubriker: Rubrik, Namn, Ändrad, Publicerad, Förhandsgranska, Mall, Åtgärd, Arbetsflöde. Varje interaktivt element i tabellhuvudet ska tilldelas en&quot;knapproll&quot; för att säkerställa kompatibilitet med hjälpmedelstekniker som NVDA. (SITES-10962)


#### Administratörsgränssnitt{#sites-adminui-6522}

* I vissa fall av AEM fungerade inte funktionerna för förhandsgranskning och jämförelse som förväntat på flera sidor. Mer specifikt:

   * **Förhandsgranskningsproblem:** Ett fel visas från början när du försöker förhandsgranska en sidversion. När du har försökt igen blir förhandsgranskningen en tom sida.
   * **Versionsjämförelseproblem:** Funktionen Jämför med aktuell visade bara den aktuella versionen, utan att markera några skillnader mellan versionerna. (SITES-23988)

* En oväntad `<br>`-tagg visas i RTE-fältet (Rich Text Editor) när `defaultPasteMode` inställd på `plaintext` används under en kopiera- och klistra in-åtgärd. Det här problemet resulterar i olika markeringar för samma innehåll, vilket resulterar i att samma textinnehåll översätts två gånger i kundens översättningsminne. (SITES-23606)
* I AEM 6.5.20.0 påträffades ett funktionsfel med funktionen **Hantera publikation**. När du väljer en nod och schemalägger den för framtida publicering kan ett felmeddelande,&quot;Det gick inte att hämta underordnade resurser för valda objekt&quot;, visas när underordnade noder ska inkluderas. Det här problemet blockerade användningen av alternativet **Inkludera underordnade**, vilket förhindrar att den avsedda innehållshierarkin publiceras fullständigt. (SITES-23000)
* En malls&quot;publicerade&quot; tidsstämpel uppdaterades inte i författarmiljön, även om mallen replikerades till publiceringsinstanserna. Det förväntade beteendet var att tidsstämpeln på författarinstansen skulle återspegla den senaste publikationen, men den här uppdateringen gjordes inte som förväntat. (SITES-21585)
* Antalet inkommande länkar i AEM-redigeringsmiljön stämmer inte överens. Den vänstra listen visade färre länkar jämfört med det klassiska användargränssnittet. Vissa inkommande länkar som var berättigade fungerar inte heller. (SITES-24837)
* Extremt långa inläsningstider rapporterades när sidversioner visades i tidslinjevyn i AEM. Det tog upp till 19 minuter att visa versioner. Problemet har pågått sedan uppgraderingen från AEM 6.4.8 till 6.5.18, vilket avsevärt har påverkat arbetsflödets effektivitet. (SITES-22468 &amp; SITES-22467)

<!-- #### Classic UI{#sites-classicui-6522} 

* A -->


#### [!DNL Content Fragments]{#sites-contentfragments-6522}

* Om du sparar innehållsfragment i den uppgraderade AEM 6.5.17 uppstod följande fel: *FEL: Det gick inte att spara innehållsfragment.* (SITES-22993)
* Ett problem identifierades med en icke stängd resurslösare i `ContentFragmentModelOmniSearchHandler` på utgivaren i AEM. (SITES-24903)


#### [!DNL Content Fragments] - Admin{#sites-admin-6522}

Om du klickar på länken i e-postmeddelandet dirigeras användaren till standardresursläsaren eller -redigeraren. Det gör det i stället för innehållsfragmentsredigeraren, även när resursen i arbetsflödet bedöms vara ett innehållsfragment. (SITES-24338)


#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6522}

När du använder innehållsfragment med flerradiga textfältsobjekt, bibehölls inte formateringen som angetts i HTML för den kod som genererades när du frågade med GraphQL. En ny rad saknades till exempel efter listan. Följden blev att det sista stycket blev en del av listan. (SITES-23233)


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6522}

* A


#### [!DNL Content Fragments] - REST API{#sites-restapi-6522}

* A -->

#### Core Backend{#sites-core-backend-6522}

* Återkommande `SegmentNotFoundException` fel rapporterades för en AEM-författarinstans. Problemet löstes tillfälligt när författaren startades om, men en långsiktig korrigering krävdes för att förhindra ytterligare händelser. (SITES-22573)
* Ett problem uppstod med tidslinjefunktionen i AEM Sites, särskilt när `cq:lastModified`-egenskaper hanterades i anteckningar. När AEM 6.5.20 har tillämpats var det osäkert om befintligt innehåll behövde åtgärdas för den saknade egenskapen eller om tidslinjen uppdaterades för att fungera korrekt utan den. (SITES-21861)


#### Kärnkomponenter{#sites-core-components-6522}

* Efter en uppgradering från AEM 6.5.18 till 6.5.21 identifierades ett problem med funktionen som kontrollerar komponenternas användning i realtid. När du försökte bläddra efter ytterligare objekt på sidan Live-användning kunde tabellen inte läsa in fler resultat trots att&quot;Läsa in fler objekt&quot; visades i användargränssnittet. (SITES-23919)
* Ett problem med valideringen av obligatoriska fält i en AEM-komponentdialogruta med två flikar rapporterades. Fliken 1 innehöll en textredigerare (RTE) och textfält, medan Flik 2 hade sökvägsfält och textfält. Även om alla fält har markerats som obligatoriska (`required=true`) kvarstår felmeddelanden felaktigt i flik 1, även efter att alla obligatoriska fält har fyllts i. Fel i tabb 2 rensas däremot som förväntat. (SITES-23243)
* Efter migrering till AEM 6.5.21 fungerar inte längre programsatsen HTML Template Language `data-sly-include` som förväntat, vilket innebär att `appendPath`- och `prependPath`-uttryck inte stöds. Resultatet blev att den inkluderade resursens utdata inte renderades korrekt, även om den fungerade korrekt före migreringen. Det här problemet orsakade återgivningsfel för resurser som är beroende av dessa uttryck för sökvägsändring. (GRANITE-52970)


<!-- #### Campaign integration{#sites-campaign-integration-6522}

* A -->


#### Upplevelsefragment{#sites-experiencefragments-6522}

* Experience Fragments sorterar inte efter rubrik som förväntat när du klickar på kolumnrubriken **Title** i listvyn. En snabb flimmer av skärmen visas, men den sorteras inte. (SITES-23706)

* I AEM 6.5.17 påträffades ett fel när en sidkomponent konverterades till ett Experience Fragment med hjälp av funktionen som finns i kartongen. Efter konverteringen verkade Experience Fragment tomt under redigeringen, trots att det visades korrekt på sidan där det användes. Problemet uppstod när en felaktig nod skapades: komponentnoden placerades utanför rot-/behållarnoden, vilket bröt mot mallens struktur. Du måste flytta komponentnoden manuellt till rätt rot-/behållarnod för att kunna återställa fragmentets redigerbarhet. (SITES-22974)

* Efter migrering från AEM 6.5.11 till 6.5.20 sparades inte molnkonfigurationer på Experience Fragments korrekt. Även om konfigurationerna verkade ha sparats i `crx/de`, visas de inte när konfigurationskonsolen öppnas igen, vilket tyder på ett problem med beständighet. (SITES-22287)


<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6522}

* A -->


#### Launches{#sites-launches-6522}

När användaren lägger till Experience Fragment-resurser med taggningsfiltret i AEM-produktionen, kunde han eller hon markera det, men ett fel uppstod när **Skapa språkkopia** valdes. Det förväntade beteendet var att Experience Fragment-resursen som valdes från taggningsfiltret skulle läggas till i översättningsprojektet. (SITES-24152)

#### Länkkontroll{#sites-link-checker-6522}

LinkCheckerTask kan inte autentiseras eftersom HTTP-klienten försöker med NTLM före grundläggande autentisering, vilket gör att proxyn blockerar användare efter flera misslyckade försök. Systemet bör i stället använda grundläggande autentisering för att autentisera mot proxyn, så att LinkCheckerTask-tjänsterna fungerar korrekt. (SITES-25034)


#### MSM - Live-kopior{#sites-msm-live-copies-6522}

* När SEO Robots-taggar används på den primära kopian och distribueras till Live Copy-sidor, visades värdena korrekt i `crx/de`. Värdena speglades emellertid inte i användargränssnittet under Sidegenskaper på Live Copy-sidorna. (SITES-23475)
* Fel som rör startprogram uppstod när ett försök gjordes att befordra en startsida via användargränssnittet. Guiden för att starta upp kampanjen förblev tom, vilket förhindrar att kampanjprocessen slutförs. (SITES-19718)
* Problem uppstod med Experience Fragments i AEM efter försök att skapa Live-kopior och utföra rollouts. Problemet uppstod när användare påträffade ett `NotFound`-fel när de försökte navigera tillbaka till hanteringsskärmen för Experience Fragments från utrullningsskärmen. (SITES-21933)


#### Page Editor{#sites-pageeditor-6522}

* Knappen Ångra ändrade komponentens position förutom att ändra texten till den senaste versionen. (SITES-17465)
* När en kopierad behållarkomponent klistrades in visuellt visuellt två gånger, vilket resulterar i tre instanser på sidan. När sidan har uppdaterats försvann dock dubbletten, vilket tyder på att problemet troligen var ett tillfälligt visuellt fel. (SITES-21890)
* När du navigerade i den vänstra rutan Komponenter med tangenterna Tabb eller Skift+Tabb på tangentbordet var flera textelement inte tydliga, både visuellt och i tabbläge. Det här problemet påverkade tillgängligheten, vilket gjorde det svårt att identifiera eller interagera med dessa komponenter under tangentbordsnavigeringen. (SITES-2266)

#### Replikering{#sites-replication-6522}

I AEM 6.5.18 och 6.5.19 genererades flera inaktiveringsbegäranden för varje underordnad sida när en överordnad sida inaktiverades. Detta gjorde också att huvuddelen av GraphQL-slutpunkterna inte kunde publiceras. (NPR-42075 &amp; NPR42010)


### [!DNL Assets]{#assets-6522}

* När du använder funktionen för uppkopplade Assets återspeglas inte uppdateringarna i AEM Assets i AEM Sites-miljön. (ASSETS-42344)
* Problem med publiceringsstatusen för resurser när du flyttar resurser från en plats till en annan inom Experience Manager. (ASSETS-41158)
* Om du överför resurser med API visas ett felmeddelande om `unclosed resource resolver`. (ASSETS-41049)
* Problem med `AssetReferenceResolverImpl`-referensfrågan efter uppgradering till Adobe Experience Manager, Service Pack 21. (ASSETS-40384)
* I AEM version 6.5.19 avmarkeras även alla andra tillgängliga kryssrutor när du tar bort ett alternativ från sökpanelsresultatet. (ASSETS-37335)
* Skräppostvärden visas i Excel-utdata när gruppmetadataexporten utförs. (ASSETS-37260)
* I AEM version 6.5.19 blir utdata oskarpa när du överför en SVG-fil i UTF-8-format. (ASSETS-36616)
* Alternativet `Fetch original rendition for Dynamic Media Connected Assets` saknas i den anslutna Assets-konfigurationen. (ASSETS-41726)
* Resursegenskaper sparas även om du inte definierar ett värde för obligatoriska fält. (ASSETS-37914)
* Om bearbetningsstatusen för en resurs är Misslyckad eller Metadata misslyckades fungerar inte beskrivningarna och ljudspårens användargränssnitt korrekt. (ASSETS-37281)
* När du sparar metadata för en resurs och försöker redigera den visas inte språknamnet. (ASSETS-37281)

#### [!DNL Dynamic Media]{#assets-dm-6522}

Ett produktionsproblem stör migreringsprocessen när en videoöverföring till Dynamic Media misslyckades och ett processfel visas i användargränssnittet. (ASSETS-36038)

<!--

### [!DNL Forms]{#forms-6522}

Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.22.0 Forms add-on package release is scheduled for Thursday, November 28, 2024. A list of Forms fixes and enhancements is added to this section post the release.

-->

### Forms {#forms-bug-fixes-sp22}

* De URL:er som genereras för bifogade filer i sparade utkast i AEM Forms återspeglar inte de konfigurerade mappningarna för Apache Sling Resource Resolver Factory. (FORMS-16949)
* När en användare på AEM Forms Service Pack 19 (6.5.19.0) förhandsgranskar en bokstav justeras inte innehållet korrekt, eftersom blanksteg verkar saknas och tecknet `x` visas på vissa platser. (FORMS-1670)
* När en användare använder AEM Forms Service Pack 18 (6.5.18.0) försöker skriva ut filerna med CIFS-protokoll misslyckas den med följande fel: (FORMS-16629)
  `ALC-OUT-001-401: Unknown error while printing using CIFS on the Printer: \\\\\\\\NSMVPLUETEST01\\\\TH_Test`.
* När en användare uppgraderar från AEM Forms Service Pack 17 (6.5.17.0) till AEM Forms Service Pack 20 (6.5.20.0) visas inte ikonen för regelredigeraren på formulärbehållarnivå. (FORMS-16430)
* När en användare uppgraderar från AEM Forms Service Pack 17 (6.5.17.0) till AEM Forms Service Pack 21 (6.5.21.0) fungerar inte den ändrade URL-sökvägen för adaptiv formulärsändning. (FORMS15894)
* I AEM Forms Service Pack 19 (6.5.19.0) misslyckas AEM Forms 6.5 PDF/A-verifieringen för vissa filer med felet `creation date and modification date mismatch with timezone`, medan den körs utan problem i Acrobat Pro PDF/A-verifieringen för en kompatibilitetskontroll. (FORMS-15840)
* När en användare tar bort formulärutkast med komponenten &quot;Utkast och överföringar&quot; på en webbplatssida i AEM Forms Service Pack 15 (6.5.15.0) i OSGi misslyckas borttagningen. (FORMS-1575)
* När en användare har en SharePoint-lista med fler än 999 poster och formuläret innehåller en bifogad fil, misslyckas överföringen av formuläret. (FORMS-15057)
* En valideringsregel läggs till för att säkerställa att slutdatumet inte är tidigare än startdatumet, tillsammans med ett anpassat skript för valideringsmeddelandet. Valideringen utlöses emellertid inte när slutdatumet är tidigare än startdatumet. (FORMS-14757)
* När en användare använder funktionerna för att visa/dölja i en tabell i ett adaptivt format krymper fältstorleken. Fältstorleken rättas till när du lägger till och tar bort en rad. (FORMS-14756)
* När en användare skriver ut formulär på AEM Forms Service Pack 19 (6.5.19.0) återges vissa formulär inte korrekt på servern, vilket orsakar fel under utskriftsprocessen. (FORMS14734)
* När en användare uppdaterar från AEM Forms Service Pack 15 (6.5.15.0) till Service Pack 19 (6.5.19.0) uppstår ett problem. Ett anpassat visningsmönster inställt på `num{$zzz,zz9.99}` återges inte korrekt i förhandsgransknings- och agentgränssnittet. (FORMS-14694)
* När en användare förhandsgranskar en bokstav i ett interaktivt dokument med sparad data-xml fastnar bokstaven i inläsningsläget i AEM-gränssnittet. Det går bra att förhandsgranska brevet igen med samma XML. (FORMS-14521)
* I AEM Forms Service Pack 20 (6.5.20.0) varnar användare som skickar e-post med bilagor med knappen &quot;Skicka e-post&quot; i anpassningsbara formulär ett problem. Namnet på den bifogade filen visas på nästa rad i stället för på raden. (FORMS-1426)
* När en användare skapar en PDF i AEM Forms med punktlistor inställda på standardformatet Skiva misslyckas PDF tillgänglighetskontrollen i Adobe Acrobat hjälpmedelsverktyg. Lista med punkttecken- och fyrkantsformat godkänns vid tillgänglighetskontrollen. (FORMS-13802, LC-3922179)
* När en användare uppgraderar från AEMForms-6.5.0-0065 till AEMForms-6.5.0-0087 på en fristående konfiguration av RHEL8 JBoss® kan den inte ansluta till LiveCycle-tjänstbehållaren. (FORMS-15907) *
* I AEM Forms på JEE, i AEM Workspace, uppstår ett problem om du väljer ett tidigare skickat formulär för att starta en ny formulärprocess. Forms med förifyllda data skriver över alla tidigare inskickade data och tar bort manuellt ifyllda fält. (FORMS-15376)
* I AEM Forms Service Pack 20 (6.5.20.0) när en användare konverterar Tiff-filen till PDF med PDFG-tjänsten misslyckas den med följande fel: (FORMS-14879) ALC-PDG-011-028-Error inträffade när indatabildfilen konverterades till PDF. com/sun/image/codec/jpeg/JPEGCodec
* Uppgradera i AEM Forms med JEE jar-filer: Biblioteket `commons-collections:commons-collections:jar` ingår nu för att förbättra beroendeupplösningen och funktionaliteten i olika AEM Forms JEE-jobb som:
   * Förbättrade jobb för att förbättra jobbbearbetning och felhantering.
   * PDF Generator (PDFG) Jobbförbättring ger smidigare dokumentgenerering och konvertering.
   * LC-Upgrade Job enhancement förbättrar uppgraderingsprocessen samtidigt som man säkerställer en stabil övergång mellan versionerna.
   * Rights Management Job enhancement för säker dokumenthantering och förbättrade Rights Management-funktioner.
   * Förbättrade processhanteringsjobb för tillförlitligare jobbbearbetning och systemhantering.
* Med början från AEM Forms OSGi 6.5.22 kommer Forms-tjänstens renderPDFForm-åtgärd inte att köra skript som bara innehåller klient (runAt=client) på servern. Endast de som är märkta runAt=server eller runAt=båda kommer att köras enligt beskrivningen i tabellen nedan. (FORMS-16564)

  | Skript markerat som runAt | Kördes på servern |
  |---------------------|-------------------------|
  | server | ja |
  | båda | ja |
  | klient | no |

#### XML FM {#forms-xmlfm-sp22}

* I AEM Forms Service Pack 21 (6.5.21.0) när en användare lägger till taggar som inte är standard i PDF-filer med hjälp av XMLFM, uppfyller dokumentet inte PDF specifikationer. (LC-3922484)
* När en användare genererar en PDF med hjälp av utdatatjänsten i AEM Forms Service Pack 20 (6.5.20.0) misslyckas den med CORBA.COMM_FAILURE och visar felet: `15:04:35,973 ERROR [com.adobe.formServer.PA.XMLFormAgentWrapper] (default task-14) ALCOUT-002-013: XMLFormFactory, PAexecute failure: "org.omg.CORBA.COMM_FAILURE"`. Tjänsten godkänns när tillgänglighetsrollen &quot;Referens&quot; exkluderas från XDP-mallens delformulär. Denna roll behövs dock för att 508 regler ska uppfyllas. (LC-3922402)
* När en användare konverterar ett XFA-formulär till ett AcroForm PDF misslyckas det. (LC-3922363)
* I AEM Forms Service Pack 19 (6.5.19.0) visas FS_DATA_SOM tomt för namnlösa delformulär när en användare skapar en XDP med namnlösa delformulär. (LC-3922034)

#### Forms Designer {#forms-designer-sp22}

* När en användare öppnar ett fragmentbibliotek genom att markera en fragmentmapp i AEM Forms Designer version 6.5.21.0 kraschar det. (LC-3922439)
* När en användare avinstallerar 32-bitarsversionen av AEM Forms Designer 6.5.20.0 och installerar AEM Forms Designer version 6.5.21.0 startar inte Forms Designer. Felloggarna visar att det inte finns tillräckligt med minne för JRE (Java Runtime Environment). (LC-3922404)
* När en användare har installerat AEM Forms Designer version 6.5.20.0 visas inte makroalternativet Makron på menyn. Endast standardmakrot &#39;Tillgänglighetskontroll&#39; visas och kan inte köras. (LC-3922321)
* När en användare lägger till en ny mallplats för att skapa XDP-filer i AEM Forms Designer version 6.5.20.0 kraschar Forms Designer. (LC-3922316)
* När en användare genererar utdata med metoden ExportData i AEM Forms 6.5 Service Pack 15 (6.5.15.0) OSGI, skapas ofullständiga och felaktiga data. (LC-3922340)


<!-- #### [!DNL Adaptive Forms] {#forms-6522}

* A


#### [!DNL Forms Designer] {#forms-designer-6522}

* A -->


### Foundation {#foundation-6522}

Ett fel uppstod i AEM Assets Console när DITA-dokument skulle sorteras om. Det synliga spåret högst upp i dialogrutan för sökvägsläsaren visar felaktigt nodnamnet i stället för nodrubriken för rotens överordnade nod. Korrekt nodtitel visas bara när du har markerat ett objekt i den synliga sökvägen, vilket anger ett tillfälligt visningsfel. (NPR-42106)


<!-- #### Apache Felix {#foundation-apachefelix-6522}


* A

#### Campaign{#foundation-campaign-6522}

* A


#### Cloud Services{#foundation-cloudservices-6522}

* A -->


#### Communities {#foundation-communities-6522}

Efter uppgradering från AEM 6.5.19 till 6.5.20 uppstod ett fel där `Connection evic` trådar inte kunde stängas korrekt efter anrop till `UgcSearch`. Detta problem, som observerats i produktionsmiljön, gör att dessa trådar kvarstår och ackumuleras över tid, vilket kan påverka prestandan. (NPR-42019)


<!-- #### Content distribution{#foundation-content-distribution-6522}

* A -->


#### CRX {#foundation-crx-6522}

* Sorteringen fungerade inte enligt **grupper** på den vänstra menyn i CRX Package Manager. (GRANITE-53277)
* Pakethanteraren i AEM begränsar installation av äldre versioner som standard, men tillåter att äldre versioner installeras med tvång. Om du använder kraftinstallationsalternativet kan det dock störa framtida installationer genom standardförloppet. Om till exempel version 1.21 installeras och version 1.24 läggs till, slutförs installationen och båda versionerna listas. Det går emellertid inte att installera version 1.22 över 1.24 i pipeline, men det fungerar om versionen är installerad med tvång, så att alla versioner listas. På samma sätt blockeras installation av version 1.23 om version 1.24 redan finns, eftersom pipeline inte tillåter nedgraderingar. GRANITE-53263


#### Granit{#foundation-granite-6522}

* Fixeringspaket installeras i AEM med CURL-kommandon. Under installationen skannade JCR-installationsprogrammet paketen med OSGI Installer för att säkerställa att inga ytterligare OSGI-paket eller konfigurationer krävs. Om en paketversion innehöll &quot;SNAPSHOT&quot; utlöste OSGI-installationsprogrammet VLT för att skapa ett motsvarande ögonblickspaket. Eftersom varje instans av AEM-författaren kör ett eget OSGI-installationsprogram kan båda instanserna försöka generera ögonblicksbilden samtidigt, vilket leder till sessionskonflikter i databasen. (NPR-42003)
* Det fanns en låskonflikt i `ScriptDependencyResolver` med AEM 6.5.21. (GRANITE-53181)
* Efter uppgraderingen av AEM till 6.5.21 uppstod problem när relativa sökvägar användes i syntaxen Sightly (HTL), till exempel `data-sly-use`. (GRANITE-53080)


#### Integreringar{#foundation-integrations-6522}

* Lagt till behörighetsförklaring för användargränssnittet i molntjänster. (FORMS-16373)
* Läsbehörighet har lagts till för användaren **fd-cloudService** som kan komma åt hCaptcha- och Turnstile-konfigurationer, vilket gör att klienten kan hämta klient-ID och klienthemlighet som krävs för captcha-återgivning och validering. Dessutom implementerades en åtkomstkontrollistmodell för att hantera åtkomsten till dessa konfigurationer. (FORMS-16360)


#### Lokalisering{#foundation-localization-6522}

I ![Hammer-ikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) Verktyg > **Säkerhet** > ![Användarikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_User_18_N.svg) **Användare** på sidan Användarhantering visades data i kolumnen **Status** i tabellen lodrätt. GRANITE-48304


<!-- #### Oak {#foundation-oak-6522}

* A -->


#### Plattform{#foundation-platform-6522}

* Spåra företagsinformation som introducerades i AEM 6.5.18 orsakade avvikelser vid beräkningen av poängen för produktanvändning. Adobe Metrics Library orsakade problemet genom att skriva över användardata från Omega tracking-biblioteket. Därför sjönk antalet användare för många av AEM Sites- och AEM Assets-kunderna till noll från och med februari 2024. (CQ-4358438)
* Ett kritiskt problem har identifierats i produktionsmiljön där skräpinsamlaren felaktigt hanterade taggar. När en tagg flyttades eller fick ett nytt namn kunde inte skräpinsamlaren uppdatera egenskapen `cq:MovedTo`, vilket gjorde att taggen försvann från sidorna. (CQ-4358293)
* Ett problem med ContextHub i AEM 6.5.19 gjorde att segment inte löstes korrekt när en kontextsökväg lades till i en AEM-instans. Problemet påverkade specifikt URL-fältet i JavaScript-objekten som genererades av sidkomponenten, där det nödvändiga kontextsökvägsprefixet saknades. Detta förhindrade att segment fungerade som förväntat. (SITES-21852)
* AEM Quickstart har uppdaterats för att använda biblioteket `commons-collections-3.2.2-adobe-2`. Uppdateringen ser till att programmet kan fortsätta att köras utan problem. (NPR-42150)
* SMTP OAuth2-konfigurationen i AEM 6.5 skiljer sig avsevärt från vad som används i AEM as a Cloud Service. För att effektivisera konfigurationen och säkerställa enhetlighet måste konfigurationen i AEM 6.5 anpassas till de standarder som används i AEM as a Cloud Service. (GRANITE-53273)
* Ett fel uppstod när du klickade på ikonen ![Komprimera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Compass_18_N.svg) > ![Projektikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Project_18_N.svg) Projekt och sedan placerade muspekaren över ikonen ![Rail till vänster](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RailLeft_18_N.svg) ![Sparron nedåt](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) , som visas framför verktygstipstexten&quot;Endast innehåll&quot;. (CQ-4356633)

#### Dokumentskydd{#foundation-security-6522}

* Problem uppstod med ett inaktuellt JSAFE-kryptografiskt bibliotek (version 6.0.0) i AEM. Ett programpaket med JSAFE version 6.2.5 ingår i AEM 6.5.22. (NPR-42006)
* Vid validering av tillåtna protokoll vid XSS-kontroller jämförs hanterare med&quot;http&quot; och&quot;https&quot;. Egenskapen `protocol` för ett URL-objekt returnerade emellertid dessa värden med ett efterföljande kolon, till exempel `http:` och `https:`. Felmatchningen orsakade valideringsproblem. För att säkerställa korrekt parsning krävs en protokollkontroll för att ta hänsyn till kolonet eller för att justera jämförelselogiken i enlighet med detta.  (NPR-42119)
* När du har installerat AEM 6.5.21 (tidigare version var AEM 6.5.19) på IBM® WebSphere® Liberty Profile och Semeru Java 8.0 gick det inte att öppna några sidor. Felloggarna indikerade problem relaterade till serverversioner som olika paket kräver. För att åtgärda det här problemet måste beroendet av `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar` återställas eftersom det var relaterat till problemet. (NPR-42116)
* Flera webbläsare håller på att fasa ut stödet för **SameSite=None**-cookies, som används för att tillåta åtkomst till cookies mellan webbplatser. Som ett alternativ introduceras **partitionerade cookies**. Dessa cookies isolerar lagring efter i vilket sammanhang de används, vilket förbättrar sekretess och säkerhet genom att förhindra spårning mellan webbplatser samtidigt som cookies fortfarande fungerar inom specifika partitioner, till exempel inbäddat innehåll från tredje part. GRANITE-51953


<!-- #### Sling{#foundation-sling-6522}

* A -->


#### Översättning{#foundation-translation-6522}

* Stöd för de senaste ändringarna i kärnkomponenter har lagts till i standardöversättningsreglerna. (NPR-42029)
* Ett problem uppstod vid export av XLIFF-filer i AEM Forms. När du använder alternativet **Exportera markering som XLIFF (endast strängar)** bibehölls inte komponentsekvensen konsekvent. Däremot förblir sekvensen korrekt när du exporterar XLIFF för ett visst språk. Två filer tillhandahölls för att demonstrera problemet: **DE-CH_Export.xliff** (korrekt sekvens) och **String_Export.xliff** (felaktig sekvens). (NPR-42118)


#### Användargränssnitt{#foundation-ui-6522}

* `coralui-component-dialog` ändrade placeringen av `cq-dialog-actions`, vilket eventuellt kunde påverka layout eller beteende för åtgärdsknappar i dialogrutor i AEM. (NPR-42294)
* Färgväljarfunktionen i AEM fungerade inte som den ska. När den används visas en tom modal bild, vilket förhindrar färgmarkering. Problemet uppstod när AEM 6.5.20 installerades i scenmiljön. Färgväljaren fungerade korrekt *före* för uppdateringen. (NPR-42163)
* I ikonen ![Hammer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) **Verktyg** > **Arbetsflöde** > **Modeller** > välj en modell > **Starta arbetsflöde** saknades ikonen Bläddra i fältet Nyttolast i dialogrutan **Kör arbetsflöde** . (NPR-42162)


<!-- #### WCM{#foundation-wcm-6522}

* A


#### Workflow{#foundation-workflow-6522}

* A -->


## Installera [!DNL Experience Manager] 6.5.22.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.22.0 kräver [!DNL Experience Manager] 6.5. Mer information finns i [ uppgraderingsdokumentationen ](/help/sites-deploying/upgrade.md) . <!-- UPDATE FOR EACH NEW RELEASE -->
* Hämtningen av Service Pack är tillgänglig på Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip).
* Installera [!DNL Experience Manager] 6.5.22.0 på en av författarinstanserna med Package Manager på en distribution med MongoDB och flera instanser.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe rekommenderar inte att du tar bort eller avinstallerar paketet [!DNL Experience Manager] 6.5.22.0. Därför bör du skapa en säkerhetskopia av `crx-repository` innan du installerar paketet, ifall du måste återställa det. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Installera Service Pack på [!DNL Experience Manager] 6.5{#install-service-pack}

1. Starta om instansen innan installationen om instansen är i uppdateringsläge (när instansen uppdaterades från en tidigare version). Adobe rekommenderar att du startar om om den aktuella upptiden för en instans är hög.

1. Ta en ögonblicksbild eller en ny säkerhetskopia av din [!DNL Experience Manager]-instans innan du installerar.

1. Hämta Service Sack från [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Öppna Pakethanteraren och välj sedan **[!UICONTROL Upload Package]** för att överföra paketet. Mer information finns i [Pakethanteraren](/help/sites-administering/package-manager.md).

1. Markera paketet och välj sedan **[!UICONTROL Install]**.

1. Om du vill uppdatera S3-anslutningen stoppar du instansen efter installationen av Service Pack, byter ut den befintliga kopplingen mot en ny binär fil som finns i installationsmappen och startar om instansen. Se [Amazon S3-datalager](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Dialogrutan i pakethanterarens gränssnitt stängs ibland under installationen av Service Pack. Adobe rekommenderar att du väntar på att felloggarna ska stabiliseras innan du får åtkomst till distributionen. Vänta på de specifika loggarna för avinstallationen av uppdateringspaketet innan du försäkrar dig om att installationen lyckas. Vanligtvis inträffar det här problemet i webbläsaren [!DNL Safari], men kan inträffa i alla webbläsare.

**Automatisk installation**

Det finns två olika metoder att använda för att installera [!DNL Experience Manager] 6.5.22.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Placera paketet i mappen `../crx-quickstart/install` när servern är tillgänglig online. Paketet installeras automatiskt.
* Använd [HTTP-API:t från Package Manager](/help/sites-administering/package-manager.md#package-share). Använd `cmd=install&recursive=true` så att kapslade paket installeras.

>[!NOTE]
>
>Experience Manager 6.5.22.0 stöder inte installation av Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Verifiera installationen**

Information om vilka plattformar som är certifierade för att fungera med den här versionen finns i [tekniska krav](/help/sites-deploying/technical-requirements.md).

1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience Manager (6.5.22.0)` under [!UICONTROL Installed Products]. <!-- UPDATE FOR EACH NEW RELEASE -->

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

UberJar för [!DNL Experience Manager] 6.5.22.0 är tillgänglig i [Maven Central-databasen](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.22/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Om du vill använda UberJar i ett Maven-projekt ska du läsa [Använda UberJar](/help/sites-developing/ht-projects-maven.md) och inkludera följande beroende i projektstrukturen: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.22</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar och andra relaterade artefakter är tillgängliga i Maven Central Repository i stället för i Adobe Public Maven-databasen (`repo.adobe.com`). Huvudfilen för UberJar har bytt namn till `uber-jar-<version>.jar`. Det finns alltså ingen `classifier`, med `apis` som värde, för taggen `dependency`.


## Föråldrade och borttagna funktioner{#removed-deprecated-features}

Se [Inaktuella och borttagna funktioner](/help/release-notes/deprecated-removed-features.md/).

## Kända fel{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.-->

<!-- * **Page publishing not working in Page Editor after upgrading to Service Pack 18 (6.5.18.0)** -->

<!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0 -->
<!-- After you upgrade an instance of AEM 6.5.0.0&mdash;6.5.17.0 to AEM 6.5.19.0, when you click **Publish Page** inside the Page Editor, you are redirected to a URL that does not exist.

  To work around this issue, do one of the following:

  * Remove the following "path" property.

       `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

  * Paste the correct URL directly into the browser.

       `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html` -->


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

### Känt problem för AEM Sites {#known-issues-aem-sites-6522}

* Content Fragments-Preview misslyckas på grund av DoS-skydd för ett stort träd med fragment. Se artikeln [KB om standardkonfigurationsalternativ för GraphQL Query Executor](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934)


### Kända fel för AEM Forms {#known-issues-aem-forms-6522}

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

* När användare uppgraderade från AEM 6.5 Forms Service Pack 18 eller 19 till Service Pack 20 eller 21 uppstod ett JSP-kompileringsfel. Det här felet hindrade dem från att öppna eller skapa anpassade formulär. Den orsakade även problem med andra AEM-gränssnitt. Gränssnitten innehåller sidredigeraren, AEM Forms-gränssnittet, arbetsflödesredigeraren och användargränssnittet för systemöversikt. (FORMS-1256)

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
* När brevet visas i Förhandsgranska utskrift ändras innehållet. Vissa blanksteg försvinner och vissa bokstäver ersätts med &quot;x&quot;. (FORMS-15681)
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

* [Lista över OSGi-paket som ingår i Experience Manager 6.5.22.0](/help/release-notes/assets/65220-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista över innehållspaket som ingår i Experience Manager 6.5.22.0](/help/release-notes/assets/65220-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Begränsade webbplatser{#restricted-sites}

Dessa webbplatser är bara tillgängliga för kunder. Kontakta din kontoansvarige på Adobe om du är kund och behöver åtkomst.

* [Nedladdning av produkt på licensing.adobe.com](https://licensing.adobe.com/)
* [Kontakta Adobe kundsupport](https://experienceleague.adobe.com/en/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] produktsida](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5-dokumentation](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [Prenumerera på Adobe Priority-produktuppdateringar](https://www.adobe.com/subscription/priority-product-update.html)
