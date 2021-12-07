---
title: '[!DNL Adobe Experience Manager] 6.5 Versionsinformation för föregående Service Pack'
description: Versionsinformation för [!DNL Adobe Experience Manager] 6.5 service packs
contentOwner: AK
mini-toc-levels: 2
exl-id: aeed49a0-c7c2-44da-b0b8-ba9f6b6f7101
source-git-commit: 80f4e8c857fe9e0dfe344042fc1db81dde721e18
workflow-type: tm+mt
source-wordcount: '26073'
ht-degree: 0%

---

# Programfixar och funktionspaket som ingår i de tidigare servicepaketen {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## [!DNL Adobe Experience Manager] 6.5.10.0 {#experience-manager-65100}

[!DNL Adobe Experience Manager] 6.5.10.0 innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat samt prestanda, stabilitet och säkerhetsförbättringar som släppts sedan 6.5-utgåvan släpptes i april 2019. Service Pack är installerat på [!DNL Adobe Experience Manager] 6.5.

De viktigaste funktionerna och förbättringarna i [!DNL Adobe Experience Manager] 6.5.10.0 är:

* **Förbättrat [!DNL Content Fragment] Modeller och redigerare**: Nu kan du skapa komplexa och anpassade modeller för strukturerat innehåll med hjälp av kapslade [!DNL Content Fragment] modeller. Innehållsstrukturer modulariseras till grundläggande element som modelleras som underfragment. Fragment på högre nivå refererar till dessa delfragment. Fler datatypsförbättringar som avancerade valideringsregler ger större flexibilitet vid innehållsmodellering med [!DNL Content Fragments]. The [!DNL Experience Manager] [!DNL Content Fragment] redigeraren stöder kapslade fragmentstrukturer i en gemensam redigeringssession, med förbättringar som strukturträdvyn och tabbad breadcrumb-navigering via fragmenthierarkier.

* **GraphQL API for[!DNL Content Fragments]**: Det nya GraphQL API:t är standardmetoden för att leverera strukturerat innehåll i JSON-format. GraphQL-frågor gör att klienter bara kan begära relevanta innehållsobjekt för att återge en upplevelse. En sådan markering eliminerar överleverans av innehåll (möjlig med HTTP REST API:er) som kräver att innehåll analyseras på klientsidan. GraphQL-scheman är härledda från [!DNL Content Fragment] modeller och API-svar görs i JSON-format. I [!DNL Experience Manager] som [!DNL Cloud Service], [GraphQL-frågor finns kvar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-api-content-fragments.html#persisted-queries-caching) och bearbeta cacheanpassade GETTER. Det är ännu inte möjligt i [!DNL Experience Manager] 6.5.10.0

* **GraphQL API for[!DNL Content Fragments]**: Bindestreck tillåts inte längre i egenskapsfältet för innehållsfragmentmodellen för att ge stöd för GraphQL API. GraphQL-frågor kan returnera oönskade resultat om det finns ett bindestreck i något av egenskapsnamnen för Content Fragment Model.
Endast följande tecken tillåts för egenskapsnamn: A-Za-z0-9_. En siffra kan inte vara på den första positionen.

* **Hierarkihantering och framtida förhandsgranskning**: Användarna har nu ett gränssnitt för att komma åt innehållsstrukturerna i [!DNL Experience Manager] startar, inklusive möjligheten att lägga till och ta bort sidor vid en start. Den här funktionen gör att [!DNL Experience Manager] startar för att skapa innehållsversioner för framtida publicering. [Funktion för tidsförvrängning](/help/sites-authoring/working-with-page-versions.md#timewarp) gör att användarna kan förhandsgranska när framtida innehåll visas.

* **Anslutna resurser**: [!DNL Experience Manager] utökar [!DNL Connected Assets] funktionalitet för användning av [!DNL Dynamic Media] bilder i de tillämpliga kärnkomponenterna. Se [använd anslutna resurser](/help/assets/use-assets-across-connected-assets-instances.md).

* **Länka delningsalternativ för att hämta resurser eller återgivningar**: När du delar resurser och samlingar som länkar kan användarna välja om de vill tillåta hämtning av originalresurser, deras återgivningar eller båda med hjälp av den delade länken. Dessutom kan användare som hämtar resurser som delas med dem via länken välja att bara hämta de ursprungliga resurserna, endast återgivningarna eller båda.

* **Begränsa genererade delresurser**: Administratörer kan begränsa antalet underresurser som [!DNL Experience Manager] genererar för sammansatta resurser som PDF, PowerPoint, InDesign och Keynote-filer. Se [Hantera sammansatta resurser](/help/assets/managing-linked-subassets.md#generate-subassets).

* **Camera Raw stöd**: En ny [!DNL Camera Raw] paket som stöder [!DNL Adobe Camera Raw] v10.4. Se [bearbeta bilder med [!DNL Camera Raw]](/help/assets/camera-raw.md).

* Den inbyggda databasen (Apache Jackrabbit Oak) uppdateras till 1.22.8.

* **Förbättrad tillgänglighet**:

   * [!DNL Dynamic Media] innehåller många tillgänglighetsförbättringar för visningsprogram. Se [[!DNL Dynamic Media] uppdateringar](#dynamic-media-65100).

   * Platform har några tillgänglighetsförbättringar. Se [Plattformsuppdateringar](#platform-65100).

* **Förbättringar av användarupplevelsen**:

   * [!DNL Experience Manager] visar direkt en lista över alla innehållsmodeller under en mapp utan att innehållsförfattare behöver navigera i filstrukturen. Funktionen kräver nu färre klick och förbättrar redigeringseffektiviteten.

   * Banfält i [!DNL Sites] redigeraren låter författare dra resurser från [!DNL Content Finder].

* Stöd för `GuideBridge#getGuidePath` API in [!DNL AEM Forms].

* Du kan nu använda tjänsten Automated forms conversion för att [konvertera PDF forms på franska, tyska, spanska, italienska och portugisiska](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html#language-specific-meta-model) till anpassningsbara formulär.

* **Felmeddelanden i egenskapsbläddraren**: Felmeddelanden för varje egenskap i webbläsaren Adaptive Forms Properties har lagts till. Dessa meddelanden hjälper till att förstå tillåtna värden för ett fält.

* **Stöd för att använda det literala alternativet för att ange ett värde för en JSON-typvariabel**: Du kan använda det literala alternativet för att ange ett värde för en JSON-typvariabel i det angivna variabelsteget i ett AEM arbetsflöde. Med det literala alternativet kan du ange en JSON i form av en sträng.

* [Plattformsuppdateringar](../forms/using/aem-forms-jee-supported-platforms.md): [!DNL Adobe Experience Manager Forms] på JEE har lagt till stöd för följande plattformar:
   * [!DNL Adobe Acrobat 2020]
   * [!DNL Ubuntu 20.04]
   * [!DNL Open Office 4.1.10]
   * [!DNL Microsoft Office 2019]
   * [!DNL Microsoft Windows Server 2019]
   * [!DNL RHEL8]

En lista över alla funktioner och förbättringar som ingår i [!DNL Experience Manager] 6.5.10.0, se [nyheter i [!DNL Adobe Experience Manager] 6.5 Service Pack 10](new-features-latest-service-pack.md).

Nedan följer en lista över korrigeringar i [!DNL Experience Manager] 6.5.10.0.

### [!DNL Sites] {#sites-65100}

* Fokuseringen flyttas till ett annat fält när du skriver i **[!UICONTROL Default Value]** fält under **[!UICONTROL Properties]** i Content Fragment Editor (NPR-36992).

* Vid filtrering [!DNL Content Fragment] modeller under en angiven sökväg, [!DNL Experience Manager] sökningen returnerar alla noder med `cq:Template` i stället för att bara returnera banor och noder för [!DNL Content Fragment] modell (SITES-1453).
* [!DNL Content Fragments] return `null` som status för mappar (SITES-1157).
* [!DNL Experience Manager] tillåter inte användare att inaktivera och aktivera [!DNL Content Fragment] Modeller (SITES-1088).
* När en användare flyttar, byter namn på eller tar bort [!DNL Content Fragments] eller medieresurser, refererade [!DNL Content Fragments] uppdateras inte automatiskt (SITES-196).
* När du klistrar in komponenter från en sida till en annan skapas JavaScript-fel (NPR-37030).
* När sidegenskaper visas snabbt öppnas Sidegenskaper för en annan sida (NPR-37025).
* Med innehållsfragmentet kan innehållsfragmentet referera till sig självt. Väljaren stöder inte åtgärden (NPR-36993).
* Efter uppgradering till Service Pack 9 kan vissa användare inte flytta mappar i Experience Manager och se fel i loggarna (SITES-1481).
* När du justerar bredden på komponenten i layoutbehållaren i redigeringsläge, observeras en flimmer (NPR-36961).
* När du befordrar en programstart kommer ändringarna i den befordrade programstarten att introduceras till andra programstarter. Om en användare befordrar den dubbla lanseringen återspeglas det fördubblade innehållet på källsidan (NPR-36893).
* [!DNL Experience Manager] lägger till en grå kant i vissa PNG-bilder med genomskinlighet om du lägger till bilderna på en sida med Image Core-komponenten eller om du ändrar storlek med Foundation Image-komponenten (NPR-36879).
* [!DNL Experience Manager Sites] Administratörsgränssnitt med ett stort antal mallar resulterar i långsam navigering (NPR-36870).
* Uppgradera till Service Pack 9 så går det inte att skapa ett fåtal komponenter. Problemet tillåter inte [!DNL Sites] användare för att skapa nya sidor (NPR-36857).
* The `ContextHubImpl` metod skapar en `ResourceResolver` som inte är stängd. Det leder till varningsmeddelanden om långvarig körning `ResourceResolver` och tjänsten returnerar oväntade resultat vid tidpunkter (NPR-36853).
* Vid synkronisering av en enda live-kopia från egenskaperna för en ritningssida synkroniseras även alla andra live-kopior (NPR-36829, NPR-36522).
* När bara XLS MIME-typen används fungerar inte filöverföringsfunktionen som förväntat (NPR-36785).
* Nya taggar med skiftläge och ord med versaler visas inte i taggfältet i [!DNL Content Fragments] (NPR-36742).
* Alternativet Enstaka textelement när du lägger till ett [!DNL Content Fragment] gör att text saknas och skapar oformaterad formatering som hör till listor och kapslade listor (NPR-36565).
* När en författare kommenterar en komponent på en sida, tar bort komponenten och utför en ångra-åtgärd, uppstår ett fel när sidans tidslinjedata ska visas i platskonsolen (NPR-36528).
* Page properties Bulk Editor&#39;s [!UICONTROL Save & Close] sparar ändringarna men stänger inte redigeraren (NPR-36527).
* När en användare försöker dra och släppa en ny textkomponent på en sida, försvinner komponenten omedelbart (NPR-36442).
* När en användare skriver i en on demand-tagg som innehåller utrymme (taggen som inte finns i systemet) och trycker på Retur, visas taggen under fältet. När [!DNL Content Fragment] sparas och öppnas igen, visas inte taggen on-demand (NPR-36441).
* Mallen kan inte tas bort när instansen nås via Dispatcher (NPR-36385).
* När en sida flyttas krävs en manuell uppdatering av webbläsaren för att återge ändringarna (NPR-36381).
* När du markerar en komponent kan du klippa ut eller kopiera den med Ctrl+X eller Ctrl+C (och Kommando+X eller Kommando+C i Mac). När du klickar på en annan komponent kan du klistra in med verktygsfältet, men inte med tangentbordet (Ctrl+V eller Kommando+V) (NPR-36379).
* När en användare försöker klippa ut komponenter med saxikonen för att flytta dem någon annanstans inträffar ett konsolfel. När du klistrar in flyttas dessutom bara en komponent (NPR-36378).
* [!DNL Experience Manager] har en fråga utan index på WCM eller meddelanden, vilket saktar ned prestanda (NPR-36303).
* När en författare återställer arvet för den borttagna ärvda komponenten är det tillgängliga alternativet att synkronisera allt sidinnehåll. Innehållsförfattarna måste synkronisera hela sidan även om arvet bara återställs på en komponent. En fullständig synkronisering kan leda till att oönskat innehåll synkroniseras (NPR-34456, CQ-4310183).
* Live-användning av en komponent på Author-instansen visar inte alla förekomster. Vissa komponenter används på fler än 1 000 sidor, men rapporten visar endast cirka 40 sidor (CQ-4323724).
* När det finns en webbplatsstruktur med många undersidor tar det längre tid att läsa in undersidorna i kolumnvyn i Experience Manager 6.5.8 jämfört med Experience Manager 6.4.8.2 (CQ-4322766).
* Avmarkera Alla fungerar inte med alternativet Rollout Page (NPR-37070).
* När du öppnar en befintlig version av en v3-komponent på en sida öppnas inte dialogrutan för sidegenskaper och en `NullPointerException` loggas (SITES-1830).

### [!DNL Assets] {#assets-65100}

Följande problem har åtgärdats i [!DNL Assets]:

* Egenskapens värde `jcr:title` uppdateras inte på Publish-instansen när en mapp har flyttats. Att byta namn på och publicera om en mapp i författaren innebär inte att `jcr:title` egenskapsvärdet för samma i Publish-instansen (NPR-36369).

* Om två eller flera resurser är markerade och ett eller flera metadatafält redigeras misslyckas sparåtgärden. Felkod 500 i webbläsaren Safari (NPR-36413).

* Import av massmetadata misslyckas på grund av felaktigt datumformat (NPR-36428).

* När du har gjort en markering i [!UICONTROL Properties] sida för uppdatering av metadata, så är gränssnittet långsamt att svara när det finns många alternativ i schemat (NPR-36430).

* Sök efter filter med [!UICONTROL Expiry Status] predikatet fungerar inte (NPR-36436).

* Snabbmenyn för olika fält i [!UICONTROL Folder Metadata] inte visar de senast valda värdena (NPR-36937, CQ-4314429).

* Om användaren använder ett filter och väljer när han/hon söker efter filer och mappar [!UICONTROL Files & Folders], visas bara filerna men inte mappen (CQ-4319543, NPR-36627).

* Alternativen i verktygsfältet är olika när samma samling väljs inifrån en mapp och när den väljs från ett sökresultat (NPR-36620).

* The [!UICONTROL Quick Publish] är inte tillgängligt på sökresultatsidan (NPR-36904, CQ-4317748).

* När användare skapar en live-kopia av en resurs utan att ange filnamnstillägget, går det inte att använda direktkopieringsfilen efter hämtningen (NPR-36903, CQ-4326305).

* När en användare läggs till som ägare till en underordnad mapp får användaren ägarbehörighet till den överordnade mappen, och därmed även till den överordnade mappens övriga undermappar. Användaren tas inte heller bort som ägare till den överordnade mappen när den försöker ta bort den. (NPR-36801, CQ-4323737).

* [!DNL Experience Manager] genererar ett undantagsfel när minnet är slut när du försöker skapa underresurser för sammansatta resurser, till exempel en PowerPoint-presentation (NPR-36668).

* När användare flyttar en resurs som redan används på en publicerad webbplatssida publiceras webbplatssidan igen även om alternativet att publicera inte har valts (NPR-36636, CQ-4323500).

* När du använder typidentifieringsfunktionen i Apache Tika MIME överfördes resurserna med `AssetManager.createAsset` metoden lämnar en temporär fil med namnet `apache-tika-*.tmp` i den tillfälliga katalogen. Den här tillfälliga filen använder allt tillgängligt ledigt diskutrymme (NPR-36545).

* Alla DRM-skyddade resurser hämtas och användaren väljer att hämta en viss resurs följs inte (CQ-4327422).

* Kan inte dra resurser till `pathfield` i användargränssnittet (NPR-36849).

* När du markerar en resurs i kolumnvyn försvinner panelen med resursinformation (NPR-36667).

### [!DNL Dynamic Media] {#dynamic-media-65100}

**Förbättrad tillgänglighet**

Följande tillgänglighetsförbättringar är tillgängliga i [!DNL Dynamic Media Viewers].

* Skärmläsare lägger nu till en berättarröst i platshållartexten för att söka efter och lägga till e-postadress som ett obligatoriskt fält i Dela resurser som en länkdialogruta, och meddelar även [!UICONTROL Please fill out this field] tooltip (CQ-4327761).

* Skärmläsare lägger nu in en korrekt berättarröst i namn och syften för olika fält i [!UICONTROL Image Preset Editor] om hur du får åtkomst till gränssnittsfält med tangentbordet (CQ-4325677).

* Tangentbordsfokus flyttas nu korrekt till sökfliken i [!UICONTROL Viewer Presets] från resursväljaren i [!UICONTROL Rich Media Type] option (CQ-4324736).

* När du navigerar i formulärläge med hjälp av tangentbordstangenter lägger skärmläsarna till de etiketter som motsvarar alternativen för ökning och minskning på [!UICONTROL Create] flik för [!UICONTROL Image Presets] (CQ-4323900).

* Skärmläsare meddelar nu [!UICONTROL Search and Add Email Address] alternativ för att dela resurser som en länkdialogruta (CQ-4323352).

* Tangentbordsfokus behålls i verktygsfältet när du navigerar resurser med tangentbordstangenter (CQ-4322037).

* Skärmläsare lägger nu till en berättarröst [!UICONTROL Edit] fältinformation efter att du har valt [!UICONTROL Add Crop] i [!UICONTROL Responsive Image Crop] på [!UICONTROL Edit Image Processing Profile] (CQ-4290734).

* På [!UICONTROL Edit Image Preset] och [!UICONTROL Create Interactive Video] på webbsidor kan skärmläsare nu meddela sidrubriken korrekt när de navigerar på sidorna med hjälp av kortkommandon för rubriker (CQ-4290730) (CQ-4290701).

* Skärmläsare kan nu identifiera olika delar av skärmen (t.ex. höger panelregion, vänster panel, verktygsfältet Åtgärd, markering i visningsprogrammets verktygsfält och inzoombar bildlandmärke) med hjälp av kortkommandon för landmärken och regioner när de navigerar på följande sidor.

   * [!UICONTROL Viewer Preset Editor] (CQ-4290729)

   * [!UICONTROL Image Set Editor] (CQ-4290710)

   * [!UICONTROL Create Interactive Video] (CQ-4290702).

* Skärmläsare anger nu namnet på delningsalternativet i videobildrutan när de navigerar med nedpiltangenten (CQ-4290728).

* Skärmläsare lägger nu till en berättarröst för olika alternativ i [!UICONTROL Sprite] och [!UICONTROL Background] tabbar i [!UICONTROL Appearance] tabba in [!UICONTROL Viewer Preset Editor] (CQ-4290727).

* Obligatoriska fält, som fältet som ska redigeras [!UICONTROL Width], i [!UICONTROL Basic] flik för [!UICONTROL Edit Video Encoding] sidan har nu en asterisk (*) (CQ-4290725).

* Skärmläsare meddelar nu etiketten för alternativen på [!UICONTROL Image Profiles] (CQ-4290723).

* Windows-användare kan nu navigera ut ur den utökade CSS-redigeraren på [!UICONTROL Viewer Preset Editor] när fokus ligger på CSS Editor (CQ-4290720).

* På [!UICONTROL Basic] flik för [!UICONTROL Edit Image Preset] När skärmläsarna navigerar i formulärläge lägger de nu till en berättarröst för etiketter för olika redigeringsfält och alternativ (CQ-4290717).

* Skärmläsare lägger nu till en berättarröst för rollen och läget (markerat eller inte markerat) för alternativ i användargränssnittet i den vänstra navigeringen på informationssidan för resurser (CQ-4290709).

* Skärmläsare lägger nu in en korrekt berättarröst i läget (markerat eller inte markerat) och länkar för bildväxlingarna i [!UICONTROL Content] flik för [!UICONTROL Create Interactive Video] (CQ-4290707).

* Skärmläsare lägger nu korrekt till en berättarröst för namn, roll och tillstånd för olika segment i videons tidslinjeskala när de navigerar med nedpilen på [!UICONTROL Create Interactive Video] (CQ-4290706).

* Skärmläsare lägger nu till en berättarröst för namn, roll och standardläge (markerat eller inte markerat) och egenskap när du navigerar bland alternativen i [!UICONTROL Create Interactive Video] (CQ-4290704).

* Skärmläsare lägger nu till en berättarröst för namn, roll och standardläge (markerat eller inte markerat) för alternativen i [!UICONTROL All Assets] och [!UICONTROL All Collections] alternativ vid navigering i [!UICONTROL Publish] (CQ-4290705).

* När du överför ett videoformat som inte stöds (annat än MP4) på [!UICONTROL Create Interactive Video] visas och visas felmeddelanden på Experience Manager (CQ-4290700).

* Kontrasten för siffrorna (tid i sekunder) i tidslinjen skalas på [!UICONTROL Create Interactive Video] sidan uppfyller nu minimikravet på luminiscens, så att användare med begränsad färguppfattning enkelt kan läsa den (CQ-4290699).

* Skärmläsare meddelar nu etiketten för [!UICONTROL Product Name] fält vid navigering i [!UICONTROL Create Interactive Video] (CQ-4290697).

**Åtgärdade problem**

Följande felkorrigeringar är tillgängliga i [!DNL Dynamic Media].

* Överförda videoklipp till [!DNL Experience Manager] visa `Process failed` efter `dynamicmedia_scene7` Runmode är aktiverat och synkronisering är inaktiverat (CQ-4327791).

### Plattform {#platform-65100}

Följande förbättringar har levererats i detta Service Pack:

* När en användare markerar ett objekt i trädvyn visas det som markerats och de verktygsfältsalternativ som visas högst upp (NPR-36504).
* Vissa text- och kontrollnamn är lättare att läsa för användare med synproblem eftersom luminiscensförhållandet uppfyller det lägsta tillåtna förhållandet på 4,5:1 (NPR-36503).
* När en användare använder kalenderkontrollerna visar skärmläsaren information om beskrivande datum, månad och veckodag. När en användare använder kalenderkortkommandon visar skärmläsaren ändringen av datum, månad och år (NPR-36498).
* Stöd för att köra JavaScript `Clientlibs` med ECMAScript 6-funktioner utan att följa strikt läge. I synnerhet `emitUseStrict` flaggan läggs till i `GCCScriptProcessor` (NPR-36411).

Följande felkorrigeringar ingår i detta Service Pack:

* Anpassade hälsokontroller utförs oftare än schemalagt (NPR-36985).
* The `Resourceresolver map` metoden returnerar ett felaktigt resultat för aliassidor (NPR-36767).
* [!DNL Experience Manager] starten fördröjs på grund av inläsningsarbetsflöden (NPR-36615).

### Integreringar {#integrations-65100}

* Experience Manager slutar att svara när den primära MongoDB-noden växlar till en annan nod (NPR-36566).
* [!DNL Sling content distribution] misslyckas vid borttagning av samlingsmedlem (NPR-36521, CQ-4323578).

### Användargränssnitt {#user-interface-65100}

* The **[!UICONTROL References]** På sidopanelen visas inte resurs- och platsreferenser (GRANITE-35078, GRANITE-34892).

### Översättningsprojekt {#translation-65100}

* Extra undersidor i en språkkopia av ett fleröversättningsprojekt raderas (NPR-36622).

### Arbetsflöde {#workflow-65100}

* Om servern får ett meddelande om att den inte är på kontoret rapporterar den minnesvarningar och slutar svara (NPR-36768).

### [!DNL Communities] {#communities-65100}

* Community-webbsidor öppnas i `LoggedIn` för anonyma gästanvändare (NPR-36908).

* När det finns mer än en sida i **[!UICONTROL Community]** > **[!UICONTROL Ideas]** > **[!UICONTROL Comments]** sidnavigeringen fungerar inte (NPR-36541).

<!--
Need to verify with Engineering, the status is currently showing as Resolved
-->


<!--
### [!DNL Brand Portal] {#brandportal-65100}

*
-->

### [!DNL Forms] {#forms-65100}


>[!NOTE]
>
>* [!DNL Experience Manager Forms] släpper tilläggspaketen en vecka efter den schemalagda [!DNL Experience Manager] Lanseringsdatum för Service Pack.


[!DNL AEM 6.5.10.0 Forms] innehåller följande felkorrigeringar:

* När du installerar [!DNL AEM 6.5 Forms], installeras följande tredjepartsbibliotek automatiskt (CQDOC-18373):
   * [!DNL Microsoft Visual C++ 2008 Service Pack 1 (x86)]
   * [!DNL Microsoft Visual C++ 2010 Service Pack 1 (x86)]

**Adaptiv Forms**

* Om valideringen av fältvärdena i ett adaptivt formulär lyckas, [!DNL AEM Forms] kan inte anropa formulärdatamodellen (CQ-4325491).

* När du lägger till en språkordlista i ett översättningsprojekt och sedan öppnar projektet, [!DNL AEM Forms] visar ett felmeddelande (CQ-4324933):

   ```TXT
   Uncaught TypeError: Cannot read property 'PROJECT_LISTING_PATH' of undefined
   at openButtonClickHandler (clientlibs.js:245)
   at HTMLButtonElement.onclick (clientlibs.js:258)
   ```

* Prestandaproblem efter installation [!DNL AEM Forms] Service Pack 7 (CQ-4326828).

**Korrespondenshantering**

* Fördröjning av visning av tecken i [!UICONTROL Data] och i förhandsgranskningen av HTML-bokstaven (NPR-37020).

* När du redigerar ett textdokumentfragment visas de nya orden som HTML-taggar efter att fragmentet har sparats (NPR-36837).

* Det går inte att visa bokstäverna som har sparats som utkast (NPR-36816).

* När du redigerar ett textdokumentfragment och sedan förhandsgranskar brevet, visar AEM Forms uttrycksspråket i förhandsgranskningen av HTML-bokstaven (CQ-4322331).

* Problem vid återgivning av data med en mall för självbetjäningsbrev (NPR-37161).


**Interaktiv kommunikation**

* Ett tabbtecken dupliceras mellan två ord varje gång du förhandsgranskar ett interaktivt meddelande efter att ha redigerat ett textdokumentfragment (NPR-37021).

* [!DNL AEM Forms] visar ett fel när du sparar ett textdokumentfragment som överskrider den maximala storleksgränsen (NPR-36874).

* När du lägger till en bild i ett interaktivt meddelande visas ytterligare ett tomt block efter bilden (NPR-36659).

* När du markerar all text i en redigerare kan du inte ändra teckensnittstexten till Arial (NPR-36646).

* När du skapar en URL i en redigerare och förhandsgranskar ändringarna visas en svart bakgrund i stället för URL-texten (NPR-36640).

* När du kopierar och klistrar in text i en redigerare finns det problem med att ändra teckensnittet till Arial för punkter som är tillgängliga i dokumentet (NPR-36628).

* Problem med indrag för punkter i textredigeraren (NPR-36513).

**Designer**

* Skärmen Reader kan inte läsa flytande fältdata som placerats i textetiketten på den Överordnad sidan eller på delformulärssidor i ett dynamiskt PDF (CQ-4321587).

**Dokumenttjänster**

* När du konverterar XDP-filer till PDF-filer och sedan sätter ihop det resulterande PDF misslyckas PDF-generationen och följande felmeddelande visas:

   ```TXT
   Caused by: com.adobe.fd.assembler.client.AssemblerException$ClientException: Document is in a disposed state!
   ```

**Forms Workflow**

* Det går inte att skicka ett formulär till en Workbench-process efter uppgradering till AEM Forms Service Pack 8 (CQ-4325846).

**HTML5 Forms**

* När du anger värdet för `mfAllowAttachments` egenskap som `True` i CRX DE-databasen `dataXml` skadas när formuläret HTML5 skickas (NPR-37035).

* När du återger en XDP som HTML med `dataXml`, [!DNL AEM Forms] visar en `Page Unresponsive` fel (NPR-36631).

### Handel {#commerce-65100}

* Värdet i **[!UICONTROL Published By]** fältet som visas är felaktigt i kolumnvyn (NPR-36902).
* När en katalog introduceras markeras nya produkter felaktigt som ändrade produkter (NPR-36666).
* När du återskapar en borttagen produkt återskapas inte produktsidan (NPR-36665).
* Ändrade sidor uppdateras men motsvarande länkade produkter uppdateras inte vid kataloglansering (CQ-4321409, NPR-36422).
* The **[!UICONTROL Publish later]** och **[!UICONTROL Unpublish later]** arbetsflöden fungerar inte (CQ-4327679).

Mer information om säkerhetsuppdateringar finns i [[!DNL Experience Manager] säkerhetsbulletinsida](https://helpx.adobe.com/security/products/experience-manager.html).

## Kända fel i Experience Manager 6.5.10.0 {#known-issues}

* Som [!DNL Microsoft Windows Server 2019] stöder inte [!DNL MySQL 5.7] och [!DNL JBoss EAP 7.1], [!DNL Microsoft Windows Server 2019] stöder inte körklara installationer för [!DNL AEM Forms 6.5.10.0].

* Om du uppgraderar dina [!DNL Experience Manager] från version 6.5 till 6.5.10.0 kan du visa `RRD4JReporter` undantag i `error.log` -fil. Starta om instansen för att lösa problemet.

* Om du installerar [!DNL Experience Manager] 6.5 Service Pack 10 eller ett tidigare Service Pack på [!DNL Experience Manager] 6.5, runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) tas bort.
Om du vill hämta körtidskopian rekommenderar Adobe att du synkroniserar designtidskopian av den anpassade arbetsflödesmodellen med körtidskopian med hjälp av HTTP API:
   `<designModelPath>/jcr:content.generate.json`.

* Användare kan byta namn på en mapp i en hierarki i [!DNL Assets] och publicera en kapslad mapp i [!DNL Brand Portal]. Mappens namn uppdateras dock inte i [!DNL Brand Portal] tills rotmappen publiceras på nytt.

* När en användare väljer att konfigurera ett fält för första gången i ett adaptivt formulär visas inte alternativet att spara en konfiguration i egenskapsläsaren. Om du väljer att konfigurera ett annat fält i det adaptiva formuläret i samma redigerare åtgärdas problemet.

* Följande fel och varningsmeddelanden kan visas under installationen av Experience Manager 6.5.x.x:
   * &quot;När Adobe Target-integreringen har konfigurerats i Experience Manager med Target Standard API (IMS-autentisering) skapas felaktiga erbjudandetyper när Experience Fragments exporteras till Target. I stället för att skriva&quot;Experience Fragment&quot;/källa&quot;Adobe Experience Manager&quot; skapar Target flera erbjudanden med typen&quot;HTML&quot;/källa&quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Validering på serversidan av adaptiva formulär misslyckas när sammanställningsfunktioner som SUM, MAX och MIN används (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Aktiveringspunkten i en interaktiv Dynamic Media-bild syns inte när du förhandsvisar mediefilen via Shoppable Banner Viewer.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tidsgränsen överskreds i väntan på att reg.ändringen skulle slutföras utan registrering.

## [!DNL Adobe Experience Manager] 6.5.9.0 {#experience-manager-6590}

[!DNL Adobe Experience Manager] 6.5.9.0 innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat samt prestanda-, stabilitets- och säkerhetsförbättringar som släppts sedan 6.5-versionen släpptes i april 2019. Service Pack är installerat på [!DNL Adobe Experience Manager] 6.5.

De viktigaste funktionerna och förbättringarna i [!DNL Adobe Experience Manager] 6.5.9.0 är:

* [!DNL Experience Manager Sites] Med Dynamic Media Foundation-komponenten kan du nu aktivera eller inaktivera optimering för enheter med högre upplösning när du använder responsiv bildförinställning eller smart beskärning.

* För att förbättra prestandan `hidden=false` villkoret har flyttats från JCR-fråga till [!UICONTROL QueryBuilder] utvärderare. För att verifiera att ett dolt predikat fungerar efter ändringen, [!DNL Experience Manager] kontrollerar att dolda mappar inte visas.

* Möjlighet att återställa borttagna sidor och träd på en [!DNL Experience Manager Sites] sida.

* Stöd för en ny användare att uppdatera åtkomsttoken med hjälp av en uppdateringstoken för konfigurationstjänsten för postlådor.

* [Stöd för SMTP XOAUTH2](/help/sites-administering/notification.md#setting-up-oauth) mekanism för e-postkonfigurationstjänsten.

* Stöd för [!DNL MongoDB] version 4.2 och 4.4.

* Förekomster av namn relaterade till Hong Kong, Macau och Taiwan uppdateras enligt de nya namngivningskonventionerna för kinesiska språk och regioner.

* Tillgänglighetsförbättringar i [!DNL Experience Manager] [[!DNL Assets]](#assets-accessibility-6590) och [[!DNL Dynamic Media]](#accessibility-dm-6590).

* Smart Imaging DPR (Device Pixel Ratio) och optimering av nätverksbandbredd gör att du kan leverera bilder av högsta kvalitet effektivt; på enheter med högupplösta skärmar och begränsad nätverksbandbredd. Mer information och tidslinjen finns i [vanliga frågor om smart bildbehandling](/help/assets/imaging-faq.md).

* [!DNL Dynamic Media] leverans (`fmt` URL-modifierare) stöder nästa generationens AVIF-bildformat (AV1-bildformat). Mer information och tidslinjen finns i [API-format för bildvisning och återgivning](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html).

* Skicka ett e-postmeddelande till en grupp med [!UICONTROL Assign Task] arbetsflödessteg.

* Möjlighet att hämta ett utkast till interaktiv kommunikation efter att källan för interaktiv kommunikation har ändrats.

* Ange ett anpassat domännamn för inläsning, återgivning och validering av reCAPTCHA-tjänsten i [!DNL Experience Manager Forms].

* Förbättrade indata för [!UICONTROL Invoke Form Data Model Service] arbetsflödessteg.

* Möjlighet att använda flera överordnad sidor i en dokumentmall i [!DNL Experience Manager Forms].

* Sidbrytningar i Dokument för post i [!DNL Experience Manager Forms].

* Den inbyggda databasen (Apache Jackrabbit Oak) uppdateras till 1.22.7.

En fullständig lista över funktioner och förbättringar som ingår i [!DNL Experience Manager] 6.5.9.0, se [nyheter i [!DNL Adobe Experience Manager] 6.5 Service Pack 9](new-features-latest-service-pack.md).

>[!NOTE]
>
>Från och med Service Pack 9, [!DNL Experience Manager] kunder kan utveckla och driva sina [!DNL Experience Manager] program med distributioner av [!DNL Azul Zulu] bygger OpenJDK, som följer Java™ SE.
>Stöd för [!DNL Azul Zulu] JDK tillhandahålls också av Adobe till [!DNL Experience Manager] kunder.
>Du kan hämta relevanta versioner av [!DNL Azul Zulu] JDK från [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
>Användarrättigheterna för Oraclet Java™-tekniken, som distribuerats av Adobe, upphör att gälla i slutet av december 2022. [!DNL Experience Manager] Vi rekommenderar att man planerar och implementerar [!DNL Azul Zulu] JDK är senaste detta datum. Mer information om hur du använder [!DNL Oracle Java™] teknik och [!DNL Azul Zulu] teknik, se [Vanliga frågor](https://experienceleague.adobe.com/docs/experience-manager-65/assets/adobe-azul-openjdk-license-agreement.pdf).

Nedan följer en lista över korrigeringar i [!DNL Experience Manager] 6.5.9.0-versionen.

### [!DNL Sites] {#sites-6590}

* Publicerade sidor med egenskapen Autentiseringskrav aktiverad dirigeras inte om till inloggningssidan och returnerar 404-felmeddelande (NPR-36354).

* När du skapar en hyperlänk fungerar inte alternativet att söka efter en länk i textkomponenten (NPR-35849).

* En genomgångsfråga aktiveras när `com.day.cq.wcm.commons.ReferenceSearch` API. Det påverkar prestandan hos [!DNL Experience Manager] server (NPR-36407).

* Kapslad layoutbehållare i en annan storleksändrad layoutbehållare visar ett felaktigt antal kolumner för sina underordnade komponenter, vilket gör att dessa komponenter inte justeras mot rutnätet (NPR-36359).

* Extern länkkontroll visar giltiga externa länkar som ogiltiga länkar (NPR-36289).

* När du har visat referenser ett tag visas ett felmeddelande på referenspanelen (NPR-36167).

* När en komponent flyttas har den automatiskt skapade parsysen inte `sling:resourceType` nod (NPR-36165).

* När du försöker synkronisera en livecopy (när du använder rollout-konfigurationer) [!UICONTROL Activate on Blueprint activation] och [!UICONTROL De-activate on Blueprint activation]) om en komponent tas bort i livecopy-överordnad misslyckas synkroniseringen och en `NullPointerException` loggas (NPR-36127).

* När en användare skriver i improviserad text för tagg (tagg som inte finns i systemet) och trycker på Retur, visas taggen under fältet, men när innehållsfragmentet sparas och öppnas igen försvinner den improviserade taggen (NPR-36132).

* Det finns inget alternativ för att visa status för asynkrona åtgärder (NPR-36104).

* En dubblettkomponent skapas efter återställning av arv (NPR-36000).

* När du använder `RemoteContentRenderingService`, begäran till `RemoteContentRendererRequestHandler.getRequest` innehåller alltid rotsidan för  `ComponentExporter`, men inkluderar inte den begärda sidan om den inte ingår i rotmodellen baserat på alternativen för genomströmningsdjup och filtrering. Begäran måste alltid innehålla den begärda sidan så att SPA har tillräckligt med information för att återge ett svar (NPR-35961).

* onTime/offTime-objekt aktiveras/inaktiveras inte för förväntad onTime/offTime (NPR-35936).

* När du publicerar en sida som innehåller ett Experience Fragment som inte har `cq:lastModified` egenskap, en `NullPointerException` inträffar (NPR-35914).

* När du försöker ändra storlek på en komponent i en behållare går det inte att ändra tillbaka till den ursprungliga storleken. När komponentbehållarens storlek minskas går det inte att återställa storleken till originalstorleken (NPR-35809).

* Statusikonerna för frånkopplade, pausade eller inte skapade sidor är felaktiga i dialogrutan som aktiveras i redigeraren eller från Live Copy-översikten (NPR-35691).

* Flersidig körning av sidegenskaper för överordnad ignorering av kryssrutan för utrullningssida och undersidor (NPR-35634).

* Funktioner för återställning av träd som finns i det klassiska användargränssnittet saknas i Touch-gränssnittet (CQ-4315352, CQ-4309415).

* Problem vid återställning av arv och utrullning av sida på en [!DNL Experience Manager Sites] sidan (NPR-36033).

### [!DNL Assets] {#assets-6590}

Följande förbättringar av användarupplevelsen görs i [!DNL Assets]:

* Så här visar du resurser som inte är sorterade baserat på någon av [!UICONTROL Create], [!UICONTROL Modify], eller [!UICONTROL Name] parametrar, [!DNL Adobe Experience Manager] erbjuder [!UICONTROL None] inom [!UICONTROL Sort by] alternativ. The [!UICONTROL None] gör att resurserna i Assets-användargränssnittet (i vyn Card, Column och Insights) är i samma ordning som de finns i JCR-noden (NPR-36356).

* Gör e-post-ID till gemener i AVS-API-svar från [!DNL Adobe Experience Manager] en valfri inställning införs, som [!DNL Adobe Asset Link] användare kunde inte checka in resurser om deras ID inte hade alla tecken i gemener. The [!DNL Adobe Asset Link] -panelen använder AVS API-svaret från [!DNL Adobe Experience Manager] (CQ-4317704).

Följande tillgänglighetsförbättringar är tillgängliga i [!DNL Assets] som en del av Service Pack 9:

Kontrasten (med bakgrund) för följande text och ikoner har förbättrats så att användare med begränsad syn och uppfattning om färger kan förstå:

* Resursrubrik på [!UICONTROL Properties] (NPR-35967).
* Stjärngraderingsikoner i [!UICONTROL Rating] sektioner på olika platser (NPR-36009).
* Text på resursvyn och mappkortsvyn (NPR-35966).
* Platshållartext på [!UICONTROL Timeline] vy (NPR-35965).
* Resursnamn på resurssökningsresultaten (NPR-35964).
* Platshållartext på [!UICONTROL Link Sharing] dialogrutan (NPR-35963).
* [!UICONTROL Metadata], [!UICONTROL Status]och [!UICONTROL Other] text in [!UICONTROL List] i [!UICONTROL View Settings] dialogrutan (NPR-35910).
* [!UICONTROL Location] och [!UICONTROL Type to search] platshållartexter vid global sökning (NPR-35909).
* Expandera och komprimera ikoner under [!UICONTROL Content Tree] (NPR-35908).
* The [!UICONTROL Assets] text på sidan där resursmappar visas (NPR-35905).
* Text in [!UICONTROL Asset Metadata], [!UICONTROL Usage Statistics] inom [!UICONTROL Overview] option in asset details page (NPR-35904).
* Text för kortkommandon för [!UICONTROL properties] och [!UICONTROL edit] optioner på sidan med tillgångsinformation (NPR-35904).

Följande felkorrigeringar är tillgängliga i [!DNL Assets] som en del av Service Pack 9:

* De taggar som skapas i ett taggrevalselement i en [!UICONTROL Folder Metadata Schema] formuläret sparas inte (NPR-36119).

* När en liten ellips används för att anteckna resurser överlappar ellipsen numret på anteckningen i utskriftsversionen (NPR-36114).

* Ibland i kolumnvyn, [!DNL Experience Manager] frågar inte efter en dubblettresurskonflikt när en dubblettresurs överförs (NPR-36048).

* Dialogrutan Dela länk stängs inte genom att klicka på stängningsknappen om den är öppen och inga ändringar görs (NPR-36030).

* När flera resurser har valts för att uppdatera egenskaperna inträffar ibland ett fel eller egenskaperna för en avmarkerad resurs uppdateras (NPR-36002).

* När blanktecken för överföring av resurser läggs till i början eller slutet av filnamnen, med återstående tecken som är samma som namnet på en befintlig resurs i databasen, ersätts den befintliga resursen utan att något fel loggas (NPR-36001).

* När video spelas upp på sidan med resursinformation fungerar inte alternativen för uppspelning och paus (NPR-35999).

* När resurser avpubliceras i grupp genererar Brand Portal ett fel som anger att URI:n för begäran är för lång (NPR-35954).

* När en resurs med lång anteckningstext skrivs ut trimmas anteckningstexten, även om det finns utrymme (NPR-35948).

* Alternativet att gå till nästa sida är inaktiverat när du väljer sidan i mallvyn på sidan Skapa katalog (CQ-4315462).

* När arbetsflödet för att uppdatera resurser startas på videoresursen uppdateras sidan upprepade gånger (CQ-4313375).

* DAM-mappar kan inte tas bort eller flyttas och ett undantag loggas (NPR-35942).

### [!DNL Dynamic Media] {#dynamic-media-6590}

I [!DNL Adobe Experience Manager] 6.5.9.0, följande tillgänglighetsförbättringar är tillgängliga i [!DNL Dynamic Media]:

* När du öppnar dialogrutan för att lägga till resurser med hjälp av tangentbordstangenter i [!UICONTROL Image Set] redigerare:
   * Skärmläsare anger att dialogrutan är öppen.
   * Tangentbordsfokus flyttas till dialogrutan när den öppnas.
   * Tangentbordsfokus flyttas tillbaka till alternativet Lägg till resurs när dialogrutan stängs (CQ-4312134).

* Nu kan du lägga till och redigera aktiveringspunkter för resurser med hjälp av tangentbordstangenter i Hotspot-redigeraren (CQ-4305965).

* Nu kan du lägga hyperlänken på hotspot-områden via hotspot-hantering med hjälp av tangentbordstangenter. Skärmläsarens fokus flyttas nu till fältet för att redigera URL-sökväg och alternativet Öppna markeringsdialogruta (CQ-4290735).

* Kontrasten (med bakgrunden) för text och kontroller på sidan i redigeringsprogrammet för bilduppsättningar har förbättrats så att användare med begränsad syn och uppfattning om färger kan förstå (CQ-4290733).

* Nu kan du navigera till resursdelningsalternativ i redigeraren för visningsförinställningar och komprimera det utökade delningsalternativet med hjälp av tangentbordstangenter (CQ-4290724).

* Nu kan du navigera och visa verktygstips på informationsikonerna och varningsikonerna på flikarna Grundläggande och Avancerat på sidan Redigera videokodning med hjälp av tangentbordstangenter (CQ-4290722).

* Skärmläsare lägger nu till en berättarröst för de olika fälten på fliken Utseende och på fliken Beteende i redigeraren för visningsförinställningar (CQ-4290721).

* När du navigerar på sidan Redigera bildförinställning i formulärläge lägger skärmläsaren till en berättarröst för syftet och namnen på olika fält och kontroller (CQ-4290717).

* När du navigerar på detaljsidan för resurser beskriver skärmläsare nu syftet med olika alternativ i visningsprogram (CQ-4290716).

* Kontrasten (med bakgrund) för platshållartexten Alla återgivningar i återgivningar på sidan med resursinformation har förbättrats så att användare med begränsad syn och uppfattning om färg kan förstå (CQ-4290713).

* Visuell asterisk för att ange obligatoriskt fält finns nu i tillgångsfältet Rubrik i bilduppsättningsredigeraren, och skärmläsare meddelar den obligatoriska informationen för fältet (CQ-4290712).

* Skärmläsare kan nu komma åt och lägga till en berättarröst för olika interaktiva alternativ i visningsprogram på sidan med tillgångsinformation (CQ-4290708).

Adobe Experience Manager 6.5.9.0 Assets åtgärdar följande problem i [!DNL Dynamic Media]:

* Anpassade visningsprogramförinställningar och CSS replikeras inte till [!DNL Dynamic Media] när [!DNL Dynamic Media] aktiveras selektivt och inaktiveras av [standard](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/dynamicmedia/config-dm.html#troubleshoot-dm-config) (NPR-36232).

* När du försöker förhandsgranska videoåtergivningar på sidan med resursinformation går det långsamt att läsa in videoklippen (CQ-4320122).

* Webbläsarsidan slutar svara och blir långsammare när över 200 resurser överförs med funktionen Duplicera resursidentifierare aktiverad (CQ-4319633).

* När en panoramabild läggs till på panoramamakomponenten på en sida loggas ett ej infångat referensfel (CQ-4317666).

* När en interaktiv mediavisare implementeras med Experience Fragment öppnas inte Experience Fragment från utgivaren och ett fel loggas (CQ-4317655).

* [!UICONTROL Publish to Dynamic Media] alternativet är inte tillgängligt i [!UICONTROL Quick Publish] alternativ i [!UICONTROL Properties] (CQ-4317199).

* Webbplatsförfattare med skrivskyddad behörighet kan använda smarta beskärningsfunktioner för resurser och redigera smarta beskurna återgivningar (CQ-4316450).

* Videoanteckningar fungerar inte för mappsökvägar där [!DNL Dynamic Media] -konfigurationen är inte aktiverad, även om [!DNL Experience Manager] instansen har konfigurerats i [!DNL Dynamic Media] mode (CQ-4314950).

* När resurstiteln har tecken för dubbelbyte, multibyte, högt ASCII, kyrilliskt, surrogatpar, hebreiska, arabiska och GB18030 får resurstiteln ett frågetecken (?) vid publicering till Dynamic Media. (CQ-4311872).

>Kända problem med videouppspelning i Dynamic Media *endast på Experience Manager 6.5.9.0*:
>
>* 

   <!-- CQDOC-18116 -->You cannot play video renditions from the asset's Details page on Experience Manager - Dynamic Media running in hybrid mode.
>* 

   <!-- CQDOC-18116 -->You cannot stream videos on Experience Manager - Dynamic Media running in hybrid mode.


### Plattform {#platform-6590}

* När du genererar en miniatyrbild för en ritning och sparar ändringarna i den aktiva kopian fungerar inte arvet för vissa fält (CQ-4319517).

* När du skapar en mapp väljer du egenskapen Ordningsbar och lägger till mer än 20 resurser i mappen. Om du väljer alla resurser i mappen visas fel antal (CQ-4316243).

* När du uppdaterar en sida visas inte rätt resultat vid sorteringen av mappar eller resurser (CQ-4316200).

* Hanteringsfält JavaScript-biblioteket uppgraderas till v4.7.7 (NPR-36375).

* Anpassade paket uppdateras inte när du installerar ett nytt kodpaket med Package Manager (NPR-35949).

* A `resourceresolver` Sling bundle orsakar `Sling:alias` fråga som ska misslyckas (NPR-35335).

* Kontextsökvägen tas bort när SSL konfigureras i Experience Manager (NPR-35294).

* The `SegmentNotFound` Undantaget returneras efter en session som körs länge (NPR-36405).

### Integreringar {#integrations-6590}

* Det går inte att spara sidegenskaper med arv aktiverat för Cloud Services med Experience Fragments (NPR-36107).

* Sidnumrering och lazy loading av IMS-användargränssnitt ger inte rätt resultat (NPR-36046).

* När du skapar en A4T-målkonfiguration och väljer rapportkällan som [!DNL Adobe Analytics], finns det inga rapportsviter med Adobe Target-funktioner tillgängliga i listrutan (NPR-36006).

### Projekt {#projects-6590}

* Det går inte att spara egenskaperna för ett projekt eftersom JCR-sökvägen till projektet inte har matchats på grund av ett extra snedstreck (`/`) som lagts till i projektsökvägen (NPR-36191).

### Skärmar {#screens-6590}

* [!DNL Experience Manager Screens] Det går inte att autentisera om en anpassad tvåfaktorsautentiseringshanterare används (NPR-35854).

### Handel {#commerce-6590}

* The [!UICONTROL Commerce Catalog] kan inte läsa in mer än 40 objekt i kolumnvyn (CQ-4318379).

### Översättningsprojekt {#translation-6590}

* Uppdaterings- eller överskrivningsalternativen visas inte när en `es` till `es_es` sidan (NPR-36170).

* När alternativet för automatiskt godkännande har valts för ett projekt med mänsklig översättning visas jobbstatusen som `Unknown` (NPR-35981).

* När du översätter en sida är referenssökvägen för [!DNL Experience Fragments] uppdaterar inte till målet [!DNL Experience Fragment] referenssökväg (NPR-35911).

* När du gör ändringar på de överordnade och underordnade sidorna och skickar den överordnade sidan för översättning, översätts även de underordnade sidorna felaktigt (NPR-35896).

* När det finns flera samtidiga översättningsprojekt för en markerad sida visas [!UICONTROL Go To Projects] Alternativet länkar inte till det senaste översättningsprojektet (NPR-35454).

* När du publicerar resurser på [!DNL Dynamic Media], [!DNL Experience Manager] visar ett felaktigt meddelande för opublicerade taggar (CQ-4315914, CQ-4315913).

* När du öppnar ett borttaget jobb [!DNL Experience Manager] visar ett felaktigt meddelande (CQ-4315910).

### Arbetsflöde {#workflow-6590}

* När du klickar på Complete (Fullständig), Delegate (Delegera) eller Open (Öppna) för objekt som är tillgängliga i Inbox finns ingen visuell ledtråd för att slutföra dessa åtgärder (NPR-36317).

### [!DNL Communities] {#communities-6590}

* Vid skräppostfiltrering förbrukar systemet 100 % av Java™-heap-utrymmet, vilket gör att Experience Manager-servern inte svarar (NPR-36316, NPR-36493).
* I forumen läser JCR in data från `SearchCommentSocialComponentListProvider` har läckt (NPR-36235).
* När du öppnar ett specifikt inkorgsmeddelande visas alla meddelanden med felaktig sidnumrering och andra problem (NPR-35917).

### [!DNL Brand Portal] {#brandportal-6590}

* Funktionsflaggan Resurser aktiveras automatiskt vid konfigurering [!DNL Experience Manager Assets] med [!DNL Brand Portal] (NPR-36010).

### [!DNL Forms] {#forms-6590}

>[!NOTE]
>
>* [!DNL Experience Manager Forms] släpper tilläggspaketen en vecka efter den schemalagda [!DNL Experience Manager] Lanseringsdatum för Service Pack.


**Adaptiv Forms**

* Problem med språkinitiering i [!DNL Experience Manager Forms] 6.5.7.0 när flera översättningsordlistor genereras (NPR-36439).
* När du lägger till en bifogad fil i ett adaptivt formulärfragment och skickar formuläret, [!DNL Experience Manager Forms] visar följande felmeddelande (NPR-36195):

   ```TXT
    POST /content/forms/af/attachmentissue/jcr:content/guideContainer.af.submit.jsp HTTP/1.1] com.adobe.aemds.guide.servlet.GuideSubmitServlet [AF] Invalid file name or mime type for file resulted in submission failure
   ```

* När du använder mänsklig översättning för att uppdatera ett lexikon och sedan förhandsgranska ett anpassat formulär visas inte ändringarna (NPR-36035).

**Interaktiv kommunikation**

* När du överför en bild med Interactive Communications Print-kanalen och redigerar den är bilden inte längre synlig (NPR-36518).

* När du redigerar en textresurs och fyller i en platshållare tas alla interaktiva element bort från navigeringsrutan (NPR-35991).

**Arbetsflöde**

* När du anropar REST-slutpunkten för en [!DNL Experience Manager Forms] på JBoss®, [!DNL Experience Manager] visar följande felmeddelande (NPR-36305):

   ```TXT
   Invalid input. The maximum length of 2000 characters was exceeded.
   ```

**BackendIntegration**

* Det går inte att spara en formulärdatamodell när Lästjänstargumentet binds till ett literalt värde som innehåller ett bindestreck (NPR-36366).

**Dokumentsäkerhet**

* När du anger certifiering och HSM för GlobalSign, [!DNL Experience Manager Forms] visar `Unsuported Algorithm` och `Invalid TSA Certificate` felmeddelanden när en tidsstämpel läggs till i LTV (NPR-36026, NPR-36025).

**Dokumenttjänster**

* Uppdateringar till [!DNL Gibson] för integrering med [!DNL Experience Manager Forms] (NPR-36211).

**Foundation JEE**

* När du väljer Endpoint Management i AdminUI, [!DNL Experience Manager Forms] visar `endpoint registry failure` felmeddelande (CQ-4320249).

Mer information om säkerhetsuppdateringar finns i [[!DNL Experience Manager] säkerhetsbulletinsida](https://helpx.adobe.com/security/products/experience-manager.html).

### Kända fel i Experience Manager 6.5.9.0 {#known-issues-6590}

* Om du uppgraderar dina [!DNL Experience Manager] från version 6.5 till 6.5.10.0 kan du visa `RRD4JReporter` undantag i `error.log` -fil. Starta om instansen för att lösa problemet.

* Om du installerar [!DNL Experience Manager] 6.5 Service Pack 5 eller ett tidigare Service Pack på [!DNL Experience Manager] 6.5, runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) tas bort.
Om du vill hämta körtidskopian rekommenderar Adobe att du synkroniserar designtidskopian av den anpassade arbetsflödesmodellen med körtidskopian med hjälp av HTTP API:
   `<designModelPath>/jcr:content.generate.json`.

* Användare kan byta namn på en mapp i en hierarki i [!DNL Assets] och publicera en kapslad mapp i [!DNL Brand Portal]. Mappens namn uppdateras dock inte i [!DNL Brand Portal] tills rotmappen publiceras på nytt.

* När en användare väljer att konfigurera ett fält för första gången i ett adaptivt formulär visas inte alternativet att spara en konfiguration i egenskapsläsaren. Om du väljer att konfigurera ett annat fält i det adaptiva formuläret i samma redigerare åtgärdas problemet.

* Följande fel och varningsmeddelanden kan visas under installationen av Experience Manager 6.5.x.x:
   * &quot;När Adobe Target-integreringen har konfigurerats i Experience Manager med Target Standard API (IMS-autentisering) skapas felaktiga erbjudandetyper när Experience Fragments exporteras till Target. I stället för att skriva&quot;Experience Fragment&quot;/källa&quot;Adobe Experience Manager&quot; skapar Target flera erbjudanden med typen&quot;HTML&quot;/källa&quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Validering på serversidan av adaptiva formulär misslyckas när sammanställningsfunktioner som SUM, MAX och MIN används (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Aktiveringspunkten i en interaktiv Dynamic Media-bild syns inte när du förhandsvisar mediefilen via Shoppable Banner Viewer.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tidsgränsen överskreds i väntan på att reg.ändringen skulle slutföras utan registrering.

## [!DNL Adobe Experience Manager] 6.5.8.0 {#experience-manager-6580}

[!DNL Adobe Experience Manager] 6.5.8.0 innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat samt prestanda-, stabilitets- och säkerhetsförbättringar som släppts sedan 6.5-versionen släpptes i april 2019. Service Pack är installerat på [!DNL Adobe Experience Manager] 6.5.

De viktigaste funktionerna och förbättringarna i [!DNL Adobe Experience Manager] 6.5.8.0 är:

<!-- TBD:
* Using the Connected Assets functionality, it is now possible to connect up to 3 [!DNL Sites] instances with 1 [!DNL Assets] instances. The configuration user interface now allows the administrators to provide the details of these [!DNL Sites] instances. -->

* När du använder [Funktioner för anslutna resurser](/help/assets/use-assets-across-connected-assets-instances.md)kan du nu visa en lista över alla [!DNL Sites] sidor som använder resursen. Dessa referenser till en resurs är tillgängliga i en tillgångs [!UICONTROL Properties] sida. På så sätt kan administratörer, marknadsförare och bibliotekarier få en komplett bild av medieanvändningen, vilket ger bättre spårning, hantering och enhetlighet för varumärken.

* När du tar bort en resurs som refereras på en webbsida, [!DNL Experience Manager] [visar en varning](/help/assets/use-assets-across-connected-assets-instances.md#asset-usage-references). Du kan framtvinga borttagning av en refererad resurs eller kontrollera och ändra referenserna som visas i [!DNL Properties] sidan för resursen. När du klickar på referenserna öppnas den lokala datorn och fjärrkontrollen [!DNL Sites] sidor.

* Sortera de Live Copy-sidor som är tillgängliga för utrullning med [!UICONTROL Name], [!UICONTROL Last modified date,] och [!UICONTROL Last rollout date] egenskaper.

* Den inbyggda databasen (Apache Jackrabbit Oak) uppdateras till 1.22.6. <!-- TBD: Mention the version -->

En fullständig lista över funktioner och förbättringar som ingår i [!DNL Experience Manager] 6.5.8.0, se [nyheter i [!DNL Adobe Experience Manager] 6.5 Service Pack 8](new-features-latest-service-pack.md).

Nedan följer en lista över korrigeringar i [!DNL Experience Manager] 6.5.8.0.

### [!DNL Sites] {#sites-6580}

* När en sida flyttas till utkast uppdateras inte länkarnas mål (NPR-35724).
* Tizen-baserad spelare kan inte autentiseras i vissa webbläsare. Problemet inträffar med webbläsare som inte har stöd för attributet sameSite=none (NPR-35589).
* En olåst responsiv behållare visar inte tillåtna komponenter (NPR-35565).
* När du skapar en live-kopia av en nyligen tillagd sida skapar överordnad två kopior för varje domän (NPR-35545).
* Deadlock i registret över SCR-komponenter när många trådar blockeras på grund av `org.apache.felix.scr.impl.ComponentRegistry` timer. Som en följd av detta [!DNL Experience Manager] slutar svara på obestämd tid (GRANITE-33125,FELIX-6252).
* När du söker efter en viss resurs i sidofältet innehåller resultatet vissa resurser som inte sökts (NPR-35524).
* När du aktiverar SSL för en Experience Manager-instans tas kontextsökvägen bort (NPR-35477).
* När du skapar en lista lägger till text som det första elementet, lägger till en tabell som det andra elementet och lägger till en lista inuti tabellen, förvrängs den överordnade listan (NPR-35465).
* När du använder olika plugin-program för efterföljande listobjekt, en extra <br> -taggen läggs till i listobjekten (NPR-35464).
* När en lista placeras mellan två stycken kan du inte lägga till en tabell i listan (NPR-35356).
* När du startar en uppgradering av en AEM instans från AEM 6.3 till AEM 6.5 tar det längre tid att starta uppgraderingsinstansen (NPR-35323).
* När du replikerar en AEM som innehåller en hakparentes (). i namnet misslyckas replikeringen (GRANITE-27004, NPR-35315).
* När du lägger till rubriker i en textredigerare inaktiveras styckeknappen (NPR-35256).
* När du lägger till ett objekt i en befintlig lista tas efterföljande komprimeringsbar lista eller växlingslista bort (NPR-35206).
* När alternativet Utrullningssida är markerat visas en dialogruta med alla tillgängliga live-kopior och automatisk utrullning sker. De publicerade kopiorna av sidorna distribueras till alla platser utan användaråtgärd (NPR-35138).
* När du använder alternativet Inkludera underordnade visas inte alla sidor med alternativet Hantera publikation. Endast 22 sidor listas (NPR-35086).
* När en profil redigeras behåller textkomponenten inte policyändringarna (NPR-35070).
* När du drar in vissa objekt i en numrerad lista behåller alla objekt samma nummer, men numreringen ska börja från 1 för objekt med samma indrag (CQ-4313011).
* När miniatyrbilder är aktiverade kan du inte redigera någon sida eller komponent. Problemet uppstod efter installation av AEM 6.5 Service Pack 7 (CQ-431133).
* Omni sök- och resursfilter returnerar irrelevanta eller inga resultat (CQ-4312322, NPR-35793).
* När flera sidor samtidigt kommer åt ett klientbibliotek kan bibliotekshanteraren i HTML inte läsa in klientbiblioteket. Det leder till felaktig återgivning av sidor (NPR-35538).
* Kontextsökvägen tas bort automatiskt när du konfigurerar en SSL i [!DNL Experience Manager] (NPR-35294).
* Pakethanteraren loggar inte ut användare efter att ha klickat på alternativet Logout (NPR-35160).

### [!DNL Assets] {#assets-6580}

[!DNL Adobe Experience Manager] 6.5.8.0 [!DNL Assets] åtgärdar följande problem och ger följande förbättringar.

* När en tidigare version av en resurs återställs aktiveras inte händelsen DamEvent.Type RESTORED i OSGi-konsolen (NPR-35789).
* `IndexWriter.merge` orsaker `OutOfMemoryError` fel när funktionen för smart taggning skapar stora `/oak:index/lucene` och `/oak:index/ntBaseLucene` index (NPR-35651).
* Ett felmeddelande visas när du försöker spara ett [!UICONTROL Asset Contribution] typmapp med flerbytetecken i namnet (NPR-35605).
* När överlappande metadataundertypsfält används inträffar ett felaktigt &#39;Fyll i det här fältet&#39;-fel (NPR-35643).
* När en befintlig resurs dras på [!DNL Assets] användargränssnittet och en ny version skapas är ändringarna i metadata inte beständiga (NPR-34940).
* När du skapar regler i metadatamodeditorn för en överlappande meny, [!UICONTROL Dependant On] Alternativet upprepas med samma namn (NPR-35596).
* Likhetssökning fungerar inte efter redigering [!UICONTROL Assets Admin Search Rail] (NPR-35588).
* Om du öppnar resurssökningen i den vänstra listen genom att klicka i en mapp [!UICONTROL Filter], filtret i [!UICONTROL Status] > [!UICONTROL Checkout] > [!UICONTROL Checked out] fungerar inte (NPR-35530).
* Om du försöker ta bort alla smarta taggar för en resurs och spara ändringarna tas de inte bort. Användargränssnittet anger dock att ändringarna sparas (NPR-35519).
* Användare kan inte ordna om eller sortera resurser i listvyn i en ordningsbar mapp (NPR-35516).
* Om du redigerar standardmetadataschemat finns taggfältet i resursens [!UICONTROL Properties] sidan ändras till ett textfält. Ändringen gör att okända användare kan lägga till taggar på begäran och taggarna lagras som en sträng i databasen (NPR-35478).
* Om du anger ett namn som inte har en giltig e-postadress när du hämtar en resurs är nedladdningsalternativet inte tillgängligt. Om ett annat alternativ i hämtningsdialogrutan väljs aktiveras knappen, men inget e-postmeddelande skickas (NPR-35365).
* Användare kan inte checka in resurser efter att de har redigerats i [!DNL Adobe InDesign] och få felmeddelanden om behörighetsbrist (NPR-35341).
* Hanteringsfält JavaScript-biblioteket uppgraderas till v4.7.6 (NPR-35333).
* Gränssnittet för metadataredigeraren slutar fungera som förväntat när du startar från redigering av massmetadata och avmarkerar objekt tills ett enda objekt förblir markerat (NPR-35144).
* Global navigering öppnar inte rätt konsol när användaren klickar i den `assets.html` (CQ-4312311).
* [!DNL Assets] visar inte RGB-återgivning för en resurs som har RGB (CQ-4310190).
* The [!UICONTROL Relate] alternativet på menyn visas inte korrekt i [!UICONTROL Properties] (CQ-4310188).
* Om filtypsfilter för dokument används för att söka efter resurser och skapa en smart samling används inte filtret när samlingen används. I stället visas alla typer av resurser i sökningen (NPR-35759).
* Du kan inte dra och lägga till resurser i en ljuslåda från [!DNL Assets] användargränssnitt (NPR-35901).
* När en ny version av en befintlig resurs skapas efter att namnkonflikten har lösts, skrivs metadata för den ursprungliga resursen över (CQ-4313594).
* När du filtrerar resurssökningen med ett sökfilter eller predikat, öppnar en resurs för att visa eller redigera den och går tillbaka till sökresultatsidan fungerar inte filtret. Alla sökda resurser listas ofiltrerade (NPR-35913).

#### [!DNL Dynamic Media] {#dynamic-media-6580}

* Alternativet URL för RESS-bildförinställning är aktiverat på sidan med resursinformation. Nu är både URL- och RESS-alternativen tillgängliga på sidan med resursinformation när RESS-bildförinställningen har valts i avsnittet med dynamiska återgivningar. (CQ-4311241)
* Interaktiv mediekomponent - interaktiv video fungerar inte om användaren har [!DNL Experience Manager] med selektiv publiceringskonfiguration (CQ-4311054).
* Om du flyttar resurser mellan mappar synkroniseras de mellan [!DNL Experience Manager] och [!DNL Dynamic Media–Scene7] via-API är mycket långsamt (CQ-4310001).
* När Omnisearch används ökar loggarnas storlek avsevärt (CQ-4309153).
* När selektiv synkronisering är aktiverat och en resurs kopieras (inte flyttas) till en synkroniseringsmapp synkroniseras den inte som förväntat (CQ-4307122).
* För överförda resurser som automatiskt publiceras till DM visas inte statusen Publicerad på AEM. Dessutom visas inte rätt publiceringsstatus i statuskolumnen för Dynamic Media Publish (CQ-4306415).
* Om en resurs publiceras på [!DNL Experience Manager] och är inställd på att publicera till [!DNL Dynamic Media] vid aktiveringen, `scene7FileStatus` metadatavärdet uppdateras inte som förväntat (CQ-4308269).
* När du redigerar videoprofilen [!DNL Experience Manager] visar inte de höjd- och bithastighetsvärden som angetts för videoförinställningen. Fälten visas tomma (CQ-4311828).

### [!DNL Commerce] {#commerce-6580}

* Det går inte att skapa en anpassad tagg för alla produkter i Commerce (CQ-4310682).

* Referensuppdatering av produktresurs gör att replikeringstrådar är i vänteläge tills ProductAssetListener-tråden slutför sina implementeringar av JCR (NPR-35269).

### Plattform {#platform-6580}

* När du använder en Coral Tab View-komponent utan flikar och sedan utlöser en Foundation-validerare inträffar följande fel (NPR-35636):

   ```TXT
    Uncaught TypeError: Cannot set property 'invalid' of undefined
     at enable (foundation.js:10703)
     at foundation.js:10710
   ```

* SCD-framåtreplikering misslyckas för Delete-händelser för noder som innehåller kommatecken i namnet (NPR-35191).

* När du har uppgraderat till AEM 6.5.7 misslyckas byggnaderna. Orsaken är att en gammal version eller ingen jackson-core är inbäddad i uber-jar (GRANITE-33006).

### Användargränssnitt {#ui-6580}

* När du växlar från kortvyn till listvyn för dokument i en mapp i resurskonsolen fungerar inte sorteringen korrekt (NPR-35842).

* När du hyperlänkar text i en textkomponent visas inte rätt resultat i sökfunktionen (NPR-35849).

* När ett värde inte anges för ett dolt fält som är markerat som obligatoriskt, blockerar det dig från att spara en komponent (NPR-35219).

### Integreringar {#integrations-6580}

* När du använder olika värden för IMS-klient-ID och målklientkod, [!DNL Experience Manager] inte kan integreras med [!DNL Adobe Target] (NPR-35342).

### Översättningsprojekt {#translation-6580}

* Problem vid export eller import av ett översättningsjobb i [!DNL Experience Manager] (NPR-35259).

### Campaign {#campaign-6580}

* När du skapar en kampanjsida med hjälp av en färdig mall i Touch-gränssnittet och öppnar fliken E-post i dialogrutan för sidegenskaper, är personaliseringsvariabeln för ämnes- och brödfälten fortfarande inaktiverad (CQ-4312388).

### [!DNL Communities] {#communities-6580}

* När du lägger till en sidstruktur i en community-grupp [!UICONTROL Group] titeln i den synliga sökvägen ändras till den första [!UICONTROL Page] (NPR-35803).
* Till skillnad från moderatorer kan en standardmedlem i communityn inte komma åt och redigera utkast (NPR-35339).
* Åtkomstkontroll och denial-of-service med `DSRPReindexServlet` som gör att communitysajten hamnar nere tills indexeringen är klar (NPR-35591).
* Tar bort [!UICONTROL All Users] från [!UICONTROL Administrators] fält verkligen inte tar bort dem från back-end (NPR-35592, NPR-35611).
* The [!UICONTROL Compose Message] returnerar inte något resultat när den angivna texten är en delmatchning (NPR-35666).

* Om du försöker lägga till taggar i en ny blogg kan du märka en viss prestandapåverkan och långsamhet genom att välja **[!UICONTROL Add Tags]**. Installera [cqTagLucene-0.0.1.zip hotfix](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/cqTagLucene-0.0.1.zip).

### [!DNL Brand Portal] {#brandportal-6580}

* Lägga till en medlem i en [!UICONTROL Asset Contribution] typmappvisa [!UICONTROL Add User or Group] bildtext i användargränssnittet, men bara aktiva Brand Portal-användare stöds och inte grupper (NPR-35332).

### [!DNL Forms] {#forms-6580}

>[!NOTE]
>
>[!DNL Experience Manager Forms] släpper tilläggspaketen en vecka efter den schemalagda [!DNL Experience Manager] Lanseringsdatum för Service Pack.

**Adaptiv Forms**

* När du infogar en tabell med en repeterbar rad på en repeterbar panel som har flera instanser i en adaptiv form, läggs tabellen alltid till i den första instansen av panelen (NPR-35635).

* När tabbfokus når CAPTCHA-komponenten igen efter att ha verifierat den en gång i ett adaptivt formulär, [!DNL Experience Manager Forms] visar `Provide Captcha phrase to proceed` felmeddelande (NPR-35539).

**Interaktiv kommunikation**

* När du skickar in ett översatt formulär visas inskickningsmeddelandena på engelska och översätts inte till rätt språk (NPR-35808).

* När du inkluderar ett dolt villkor i bifogade XDP-dokument eller dokumentfragment, läses inte den interaktiva kommunikationen in (NPR-35745).

**Korrespondenshantering**

* När du redigerar ett brev tar det längre tid att läsa in moduler med villkor (NPR-35325).

* När du väljer en resurs i den vänstra navigeringsrutan som inte ingår i en bokstav och sedan väljer nästa resurs, tas inte den blå markeringen bort från den tidigare valda resursen (NPR-35851).

* När du redigerar textfält i en bokstav [!DNL Experience Manager Forms] visar `Text Edit Failed` felmeddelande (CQ-4313770).

**Arbetsflöde**

* När du försöker öppna ett anpassat formulär på en [!DNL Experience Manager Forms] mobilprogram för iOS svarar programmet inte (CQ-4314825).

* The [!UICONTROL To-do] på arbetsytan i HTML visas HTML-tecken (NPR-35298).

**XMLFM**

* När du genererar ett XML-dokument med hjälp av utdatatjänsten visas `OutputServiceException` fel inträffar för vissa av XML-filerna (CQ-4311341, CQ-4313893).

* När du använder upphöjd egenskap på det första tecknet i en punkt blir punktstorleken mindre (CQ-4306476).

* PDF forms som genereras med Output Service innehåller inga kantlinjer (CQ-4312564).

**Designer**

* När du öppnar en XDP-fil i [!DNL Experience Manager Forms] Designer, en designer.log-fil genereras i samma mapp som XDP-filen (CQ-4309427, CQ-4310865).

**HTML5 Forms**

* När du markerar en kryssruta i ett anpassat formulär i [!DNL Safari] webbläsare för [!DNL iOS 14.1 or 14.2]visas inte ytterligare fält (NPR-35652).

**Forms Management**

* Inget bekräftelsemeddelande som indikerar slutförd massöverföring av XDP-filer till CRX-databasen (NPR-35546).

**Dokumentsäkerhet**

* Flera problem har rapporterats för [!UICONTROL Edit Policy] i AdminUI (NPR-35747).

### Kända fel i Experience Manager 6.5.8.0 {#known-issues-6580}

* Om du uppgraderar dina [!DNL Experience Manager] från version 6.5 till 6.5.8.0 kan du visa `RRD4JReporter` undantag i `error.log` -fil. Starta om instansen för att lösa problemet.

* Om du installerar [!DNL Experience Manager] 6.5 Service Pack 5 eller ett tidigare Service Pack på [!DNL Experience Manager] 6.5, runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) tas bort.
Om du vill hämta körtidskopian rekommenderar Adobe att du synkroniserar designtidskopian av den anpassade arbetsflödesmodellen med körtidskopian med hjälp av HTTP API:
   `<designModelPath>/jcr:content.generate.json`.

* Kontakta Adobe kundsupport om du stöter på problem när du redigerar och skapar överlappande regler i [!UICONTROL Folder Metadata Schema Forms Editor] och [!UICONTROL Metadata Schema Forms Editor] använda [!UICONTROL Define Rule] -dialogrutan. Reglerna som redan har skapats och sparats fungerar som förväntat.

* Om en mapp i hierarkin byter namn [!DNL Experience Manager Assets] och den kapslade mappen som innehåller en resurs publiceras i [!DNL Brand Portal], uppdateras inte mappens namn i [!DNL Brand Portal] tills rotmappen publiceras igen.

* När en användare väljer att konfigurera ett fält för första gången i ett adaptivt formulär visas inte alternativet att spara en konfiguration i egenskapsläsaren. Om du väljer att konfigurera ett annat fält i det adaptiva formuläret i samma redigerare åtgärdas problemet.

* If [!UICONTROL Connected assets configuration] guiden returnerar ett 404-felmeddelande efter installationen. Installera om `cq-remotedam-client-ui-content` och `cq-remotedam-client-ui-components` paket med pakethanteraren.

* Följande fel och varningsmeddelanden kan visas under installationen av Experience Manager 6.5.x.x:
   * &quot;När Adobe Target-integreringen har konfigurerats i Experience Manager med Target Standard API (IMS-autentisering) skapas felaktiga erbjudandetyper när Experience Fragments exporteras till Target. I stället för att skriva&quot;Experience Fragment&quot;/källa&quot;Adobe Experience Manager&quot; skapar Target flera erbjudanden med typen&quot;HTML&quot;/källa&quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Validering på serversidan av adaptiva formulär misslyckas när sammanställningsfunktioner som SUM, MAX och MIN används (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Aktiveringspunkten i en interaktiv Dynamic Media-bild syns inte när du förhandsvisar mediefilen via Shoppable Banner Viewer.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tidsgränsen överskreds i väntan på att reg.ändringen skulle slutföras utan registrering.

## [!DNL Adobe Experience Manager] 6.5.7.0 {#experience-manager-6570}

[!DNL Adobe Experience Manager] 6.5.7.0 är en viktig uppdatering som innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat samt prestanda, stabilitet och säkerhetsförbättringar som släppts sedan 6.5-utgåvan släpptes i april 2019. Service Pack är installerat på [!DNL Adobe Experience Manager] 6.5.

De viktigaste funktionerna och förbättringarna i [!DNL Adobe Experience Manager] 6.5.7.0 innehåller följande:

* Utföra sidflyttningar och MSM-utrullningar som asynkrona åtgärder för att minska deras påverkan på körningsprestanda.

* Användare kan sortera digitala resurser i kort- och kolumnvyn.

* [!DNL Assets] och [!DNL Dynamic Media] erbjuder flera tillgänglighetsförbättringar. Förbättringarna rör tangentbordsnavigering, användning av skärmläsare och möjlighet för användare att använda liknande hjälpmedelsteknik (AT). Se [[!DNL Assets] förbättringar](#assets-6570) och [[!DNL Dynamic Media] förbättringar](#dynamic-media-6570).

* [HTTP-klientkonfiguration för formulärdatamodell](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration) för att optimera prestanda.

* [Tillgänglighet för alternativet Återställ för varje komponent](../../help/forms/using/resize-using-layout-mode.md#resize-components) i layoutläget

* [!DNL Experience Manager] 6.5 Service Pack 7 Forms förbättrar prestandan för:

   * Validerar fältvärdena på servern när du skickar ett anpassat formulär.

   * Konvertera ett PDF-formulär till ett anpassningsbart formulär med [!DNL Automated Forms Conversion service].

* Stöd för [!DNL Microsoft SQL Server] 2019 i [!DNL Experience Manager Forms].

* Stöd för [!DNL Microsoft] SQL Server 2016 Always On-tillgänglighetsgrupper för OSGi-distributioner.

* Den inbyggda databasen (Apache Jackrabbit Oak) uppdateras till version 1.2.5.

En fullständig lista över funktioner och förbättringar som ingår i [!DNL Experience Manager] 6.5.7.0, se [Nyheter i [!DNL Adobe Experience Manager] 6.5 Service Pack 7](new-features-latest-service-pack.md).

Nedan följer en lista över korrigeringar i [!DNL Experience Manager] 6.5.7.0-versionen.

### [!DNL Sites] {#sites-6570}

* När du öppnar [!UICONTROL Timewrap] för en sida, låta alternativet Sidospår i tidslinjen vara öppet och navigera till [!UICONTROL Sites] konsol, `Failed to Load` fel inträffar (NPR-34951).

* The [!UICONTROL Timewrap] visar inte bilder för det valda datumet och tidsintervallet (NPR-34951).

* När ett filter anropar `getHeader()` från en sida som innehåller ett innehållsfragment, `java.lang.AbstractMethodError` fel inträffar (NPR-34942).

* När sökvägen till en sida innehåller flera innehållsdelsträngar kan förhandsgranskningarna inte återges och funktionen för versionsjämförelse misslyckas också (NPR-34740).

* När du anger ett numeriskt värde för `String` type label-egenskap för en komponent kan du ta bort komponenten och ångra borttagningsåtgärden. När du har ångrat borttagningen ändras etikettegenskapen från `String` till `Long` (NPR-34739).

* Följande undantag inträffar när ett Experience Fragment läggs till som är baserat på en mall med en låst layout på en sida (NPR-34632):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.mozilla.javascript.EcmaError: TypeError: Cannot call method "getChildren" of null
   ```

* När du flyttar en mapp uppstår problem med genomgången och följande fel inträffar (NPR-34554):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript. org.apache.jackrabbit.oak.query.RuntimeNodeTraversalException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped
   ```

* När nya resurser skapas, publiceras och flyttas till en ny plats visas `Request to complete move operation` arbetsflödet skapas och resultatet avbryts. Överföra en ny resurs och köra en `move` operationsresultat när `Request to complete move operation` arbetsflöde i väntande tillstånd (NPR-34543).

* När du exporterar ett Experience Fragment från [!DNL Experience Manager] 6.5.2 miljö till [!DNL Target] Standard: API-anropet misslyckas eftersom arbetsyteegenskapen inte är tillgänglig för [!DNL Target] Standard (NPR-34557).

* Användarna kan inte publicera sidor via [!UICONTROL manage publication] eftersom [!UICONTROL Publish] Alternativet försvinner (NPR-34542).

* När du lägger till vissa format i texten kan du `<div>` -taggen läggs till i texten och formatet kan inte användas på texten längre (NPR-34531).

* När du markerar ett alternativ på en snabbmeny och uppdaterar de filer som krävs, går det inte att spara dialogvärden eftersom den andra menyn har ett tomt obligatoriskt fält (NPR-34529).

* När du skapar en sida från en anpassad mall och flyttar den inom hierarkin för utkast, visas komponenter som togs bort tidigare från sidan på sidan i den aktiva kopieringshierarkin (NPR-34527).

* När ett artikelformat har tillämpats på ett innehåll kan det inte tas bort (NPR-34486).

* Alla live-kopior och kopior av en Experience Fragment pekar på samma [!DNL Adobe Target] erbjudande-ID (NPR-34469).

* Punkter i punktlistor visas utöver den numrerade listan (NPR-34455).

* Alternativet Jämför med källa kan inte visa skillnaden mellan källsidan och den redigerade versionen av en sida (NPR-34285).

* När du tar bort en sida går det inte att konfigurera versionsinformationen (NPR-34159).

* När en användare väljer [!UICONTROL Open Selection] går tangentbordsfokus till den dolda kontrollen på sidan (CQ-4307779, CQ-4293601).

* När du flyttar en publicerad mapp på författaren uppdateras inte mappsökvägarna i enlighet med detta på publiceringsinstansen (CQ-4305144).

* När en användare väljer `Enter` på [!UICONTROL Select All] går tangentbordsfokus inte till [!UICONTROL Create Control] option (CQ-4293599).

* När du väljer `Esc` -tangenten återställs inte fokus till den överordnade kontrollen (CQ-4293593, CQ-4293590).

* Förbättrad WCAG-kompatibilitet för [!DNL Sites] UI- och Core-komponenter (CQ-4293448).

* [!UICONTROL Zoom] och [!UICONTROL Scale] funktioner är inaktiverade för [!DNL Sites Editor] (CQ-4282353).

* När du har använt alternativet Rotera höger avbryts berättarrösten för den aktuella rotationen eller det aktuella vändläget (CQ-4282128).

* Dialogruteknapparna Klar och Avbryt konfigurering har många tabbstopp (CQ-4274601).

* Det är inte tillåtet att flytta sidor med liknande namn på samma nivå (NPR-35041).

* När du har valt alternativet Radera (x) flyttas tangentbordsfokus inte till [!UICONTROL Filter] fält (CQ-4293581).

* När du uppgraderar till [!DNL Experience Manager] 6.5.6.0, beteendet hos det ärvda styckesystemet ändras och fungerar inte korrekt (NPR-35117).

* Tangentbordsanvändare kan inte ändra tabbfokus i lämplig ordning efter att de har valt [!UICONTROL Action] på en [!DNL AEM Sites] (CQ-4307786).

* När du har valt ett alternativ i listan med länkmål i verktygsfältet för textredigering när du redigerar ett innehållsfragment, börjar dialogrutan för författare av innehållsfragment flimra (CQ-4305532).

* Tangentbordsanvändare kan inte välja alternativen i [!UICONTROL Add Component] nedrullningsbar lista med nedpilstangenten (CQ-4295097).

* Flikfokus flyttas inte i rätt ordning när du väljer ett datum på menyn Kalender i dialogrutan [!UICONTROL Assets] -flik i en [!DNL Sites] (CQ-4293600).

* Flikfokus flyttas inte till nästa eller föregående alternativ för tangentbordsanvändare efter att alternativen Länk eller Text som är tillgängliga vid redigering av en platssida har tagits bort (CQ-4293597).

* Tangentbordsanvändare kan inte ändra tabbfokus tillbaka till Fler alternativ i [!UICONTROL Actions] när du har visat de tillgängliga alternativen och trycker på `Esc` key (CQ-4293592).

* När du aktiverar [!UICONTROL Rotate] för en bild i [!UICONTROL Edit] tabbfokus, i stället för att vara kvar vid Rotera, flyttas till [!UICONTROL Redo] för tangentbordsanvändare (CQ-4293587).

* I [!UICONTROL Open Selection] är tillgänglig på [!UICONTROL Link and Actions] tabbfokus ändras till dolda element på sidan efter [!UICONTROL Cancel] option (CQ-4293579).

* Navigera till [!UICONTROL Finish] och trycker på Retur. Skärmläsarna meddelar inte om att de är klara (CQ-4282351).

* Alternativen Flytta uppåt och Flytta nedåt finns på [!UICONTROL Link and Actions] -dialogrutan är inte tillgänglig för skärmläsare och tangentbordsanvändare (CQ-4281120).

* Tangentbordsanvändare kan inte återställa tabbfokus efter att de har navigerat till alternativet Stäng (X) på [!UICONTROL Properties] (CQ-4293581, NPR-34653).

### [!DNL Assets] {#assets-6570}

[!DNL Adobe Experience Manager] 6.5.7.0 [!DNL Assets] åtgärdar följande problem och ger följande förbättringar.

* Följande förbättringar har gjorts för tillgänglighet i [!DNL Experience Manager Assets] i den här versionen. Mer information finns i [tillgänglighetsfunktioner i [!DNL Assets]](/help/assets/accessibility.md).

   * När du navigerar på tidslinjen med ett tangentbord visas `Esc` kan dölja [!UICONTROL Show All] utan att förlora fokus (CQ-4293598).
   * När du navigerar med tangentbordets tabbtangent behålls fokus i taggfältet (NPR-35109) när du har tagit bort den sista taggen från de tillagda taggarna.
   * [!DNL Experience Manager] innehåller nu lämplig information för namn, roll och värde som ska användas av skärmläsare (NPR-34255).
   * När du har tagit bort kombinationsrutan Typ/storlek, kombinationsrutan Länk, Kombinationsrutan Språk eller textredigeringsrutan, återgår tangentbordsfokus till nästa eller föregående element i användargränssnittet eller till ett mer relevant element i användargränssnittet (CQ-4293585).
   * När du håller pekaren över alternativ visas tips som Markera och Hämta. Användare som använder en skärmförstorare kanske inte ser filminiatyrbilderna på grund av dessa tips. Nu går det att behålla fokus när du har tagit bort alternativet med `Escape` nyckel. (CQ-4293554).
   * När du väljer en stödrastercell från det stödraster som finns på sidan flyttas fokus till det åtgärdsfält som visas på skärmen (CQ-4282127).
   * Visuella användare kan skilja mellan normal text och en länk, eftersom visuella ledtrådar (underline- och chevron-ikoner) visas för länkar till alla lösningar i [!DNL Experience Manager] hemsida (CQ-4282072).

* Följande förbättringar av användarupplevelsen görs i [!DNL Assets]:

   * Möjliggör sortering av resurser i kortvyn och kolumnvyn (NPR-35097).

* Om en JSON-fil genereras med Assets HTTP API efter uppgraderingen till 6.5, uppstår problem med den kodning som används i filen (NPR-35129).

* Användare av en grupp som inte har behörighet att skapa samlingar (alternativet Skapa samling är inte tillgängligt) kan fortfarande skapa samlingar genom direktåtkomst till URL:en `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/collections/createcollectionwizard.html/content/dam/collections?contentPath=/content/dam/collections` (NPR-35115).

* När de sökda resurserna sorteras efter namn sorteras de efter skiftlägeskänsliga inställningar. Detta skapar två separata sorterade listor baserade på skiftläget som visas på rätt sätt i sökresultaten (NPR-35068).

* När ett innehållsfragment öppnas i redigeraren visas varningsmeddelanden (`Invalid value specified for a metadata property`) loggas i felloggarna (NPR-35012).

* Användare utan administratörsbehörighet kan redigera utgångna resurser med [Experience Manager] datorprogram. (NPR-34993).

* När samma resurs dras i Assets-användargränssnittet och en ny version skapas blir ändringarna i metadata inte beständiga (NPR-34940).

* När du redigerar samlingar kan användaren ta bort titeln på samlingen och spara ändringarna (NPR-34889).

* När du överför en duplicerad bild visas ett borttagningsalternativ. Om du väljer Ta bort kan bilderna överföras. Arbetsflödet för DAM-uppdatering av tillgångar aktiveras också (NPR-34744).

* När du använder [!DNL Adobe Asset Link] med [!DNL Adobe InDesign], innehåller sökresultaten inte mappar och samlingar, men bara resurser (NPR-34699, CQ-4303666).

* Pekaren placeras på kortvyn och skärmen rullas som ett resultat av (automatisk) fokus på de snabbåtgärder som är tillgängliga på kortet (NPR-34514).

* När du redigerar egenskaperna för flera resurser samtidigt, väljer du [!UICONTROL Save] stänger gruppredigeringsvyn och dirigerar om till huvudvyn [!DNL Assets] sida. Detta beteende är detsamma som beteendet för [!UICONTROL Save & Close] option och is not expected (NPR-34546).

* Den smarta samlingen visar inte rätt inställning för användargränssnitt när den har sparats. Frågan sparas korrekt, men gränssnittet visar alltid det senast tillagda Option-predikatet (NPR-34539).

* När resurser läggs till i [!DNL Experience Manager]importeras inte metadata utan namnutrymme (NPR-34530).

* När du drar en resurs till en mapp för att flytta den visas även alternativet att [!UICONTROL Drop in Lightbox] och [!UICONTROL Drop in Collection]. Även om flyttåtgärden avbryts fortsätter användargränssnittet att visa de senare två alternativen (NPR-34526).

* Symbolen `%>` visas på sidan för samlingar (NPR-34499).

* I kolumnvyn [!DNL Assets] visar duplicerade mapp- och resursnamn när du bläddrar uppåt och nedåt innan alla resurser visas (NPR-34464).

* Om du skapar en privat mapp omedelbart efter att du har skapat en gemensam mapp används inställningarna för den privata mappen (NPR-34415) för den gemensamma mappen.

* I kortvyn visas korten inte i alfabetisk ordning och korten kan inte sorteras i alfabetisk ordning (NPR-34234).

* När överlappningsregler öppnas igen behålls inte alternativen i användargränssnittet (CQ-4301452).

#### [!DNL Dynamic Media] {#dynamic-media-6570}

* Följande förbättringar har gjorts för tillgänglighet i [!DNL Dynamic Media] (CQ-4290306). Mer information finns i [tillgänglighetsfunktioner i [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).

   * Skärmläsare (JAWS, Skärmläsaren) lägger till en berättarröst för menyalternativens namn, roll och tillstånd på menyn Bädda in storlek (CQ-4290927).
   * Användare kan navigera i dialogrutan E-postlänk med `Tab` key (CQ-4290926).
   * Arbetsflödet för att skapa videokodningsprofiler är mer användarvänligt med tanke på skärmläsarförbättringarna (CQ-4290623, CQ-4290622).
   * Vid navigering med `Tab` flyttar fokus till lämpliga element i användargränssnittet i arbetsflödet för att skapa en interaktiv video (CQ-4290621, CQ-4290620, CQ-4290619).
   * Sidan Publicera, Redigera resurs, sidan Redigera smarta beskärningar och sidan Redigera bilduppsättning har förbättrats så att de uppfyller webbstandarderna. Användare av hjälpfunktioner (AT) kan nu enkelt navigera på dessa sidor och vidta åtgärder som beskärningsbilder (CQ-4290617, CQ-4290616, CQ-4290613, CQ-4290612, CQ-429 (CQ-4290614).
   * Visningsprogrammen har förbättrats så att användarna kan navigera med tangentbordet (CQ-4290615).
   * Användare av tangentbord och skärmläsare kan använda beskärningsfunktionen (CQ-4290609).
   * Tangentbordsanvändarna kan hantera de aktiveringspunkter som behövs bättre (CQ-4290604, CQ-4290603).

* Fjärrbildsuppsättningar kan inte redigeras i [!DNL Experience Manager] om företagsnamnet och mappnamnet är samma (NPR-31340).

* z-indexordningen är felaktig när du försöker förhandsgranska utdata efter att ha lagt till en aktiveringspunkt i en [!DNL Dynamic Media] eller efter redigering av en [!DNL Dynamic Media] video eller [!DNL Experience Fragment] med en bild (CQ-4307267).

* [!DNL Dynamic Media] synkroniseringen misslyckas när blandade medieuppsättningar bearbetas på nytt (CQ-4307184).

* Om en resurs flyttas till en mapp där automatisk synkronisering sker till [!DNL Dynamic Media] är konfigurerat synkroniseras inte resursen (CQ-4307122).

* [!DNL Dynamic Media] video spelas inte upp på iOS-enheter med inbyggda HTML5-videokontroller (CQ-4306977, CQ-4306727).

* Det går inte att hämta bilder som SmartCrop används på (CQ-4304558).

* Det går inte att selektivt publicera mappar till Dynamic Media (CQ-4304526).

* Avpublicera en videofil från [!DNL Experience Manager] avpublicera inte den adaptiva videouppsättningen från en konfigurerad Scene7-distribution (CQ-4304405).

* Om du lägger till en panoramabild i en panoramamakomponent och uppdaterar sidan resulterar det i `Uncaught ReferenceError: $ is not defined` fel (CQ-4302810).

* I [!UICONTROL Viewer Presets Editor], vid redigering [!UICONTROL PanoramicImage/PanoramicImage_VR] förinställning i `PanoramicView` -komponenten, `PANORAMICVIEW_AUTOROTATE` modifieringsetiketten är inte tillgänglig (CQ-4302443).

* Bildtexter visas inte om videon inte är den första i en MixedMediaSet (CQ-4298161).

* HTML5 eCatalog Viewer på iPhone-mobilenheter kan inte vända på sidorna eller vända på sidorna (CQ-4296611).

* När du rullar färgrutor på en mobil enhet rullas färgrutorna till höger och ut ur det synliga området några sekunder innan du bläddrar tillbaka till vyn (CQ-4296439).

* När en Överordnad post för visningsförinställning skapas publiceras inte CSS och teckningen och bara visningsförinställningen publiceras (CQ-4262205).

* När du försöker länka ett Experience Fragment för en viss hotspot i [!UICONTROL Interactive Video/Images] visas inte den valda Experience Fragment-sökvägen. I stället returneras ett tomt värde från sökvägsfältet (NPR-35146, CQ-4298136).

* Det går inte att förhandsgranska ett Experience Fragment i IVV Editor (CQ-4308560).

* När du lägger till en hotspot i en bild och väljer ett Experience Fragment går det inte att välja undermapparna och varianterna för Experience Fragment (CQ-4307455).

* Resurserna som inte är bilder visas inte som publicerade efter överföring (CQ-4306415).

#### [!DNL Experience Manager] 3D-resurser {#three-d-assets-6570}

* `DAM CQ MIME Type` använder felaktiga MIME-typer på 3D-resurser, vilket leder till felaktig återgivning (NPR-34731).

### [!DNL Commerce] {#commerce-6570}

* Användargränssnittet för Commerce-produktsamlingen innehåller inte fler än 15 produkter i en samling (NPR-34502).

### Plattform {#platform-6570}

* En HTTP-session över HTTPS är inte ogiltig (NPR-35083).
* A `NullPointerException` returneras vid start av dagliga eller veckovisa underhållsuppgifter från användargränssnittet (NPR-34953).
* W3C-valideraren rapporterar varningar för kompatibla JavaScript-filer för klientbibliotek (NPR-34898).
* The `AudienceOmniSearchHandler` funktionen använder ett inaktuellt index (NPR-34870).
* Om du loggar ut från Experience Manager rensas inte cookies (NPR-34743).
* The `findByTitle` funktionen i `TagManager` API fungerar inte om taggnamnet innehåller ett specialtecken (NPR-34357).
* Processen att importera användarsynkroniseringspaketet misslyckades (NPR-34399).
* Stöd för `ariaLabel` och `ariaLabelledby` egenskaper för `Coral.Masonry` komponent (GRANITE-29962).
* Dispatcher-cachen uppdateras inte för sidor med innehållsfragment efter installation av de senaste kärnkomponentpaketen (CQ-4306788).
* Lokaliserade märkordsnamn med citattecken (`"`) visas inte korrekt i användargränssnittet (CQ-4305439).

### Användargränssnitt {#ui-6570}

* The [!UICONTROL Link to] fält i komponentegenskaper visar förslag på automatisk komplettering som inte matchar den angivna strängen (NPR-34865).

* AEM visar följande felmeddelande när du schemalägger ett dagligt underhållsfönster som är fördelat mellan 2 dagar (NPR-35280):

   ```TXT
   ERROR The start time must precede (be less than) the end time
   ```

### Integreringar {#integrations-6570}

* Redigera en befintlig [!DNL Adobe Launch] konfigurationen misslyckas (NPR-35045).
* Kan inte exportera [!DNL Experience Fragments] till [!DNL Adobe Target] om IMS-konfiguration används och [!DNL Adobe Target Standard] miljö (NPR-34555).
* The [!UICONTROL Create] finns på [!UICONTROL Audiences] sida vid navigering från en mapp till [!UICONTROL Audiences] sidan (NPR-35151).

### Sling {#sling-6570}

* Standardhälsokontrollen vid inloggning validerar inloggningsuppgifterna för en användare som inte finns (NPR-34686).

### Översättningsprojekt {#translation-6570}

* Om du avbryter ett översättningsprojekt i [!DNL Experience Manager], begäran om att avbryta den inte skickas till översättningsleverantören (NPR-34433).

### [!DNL Communities] {#communities-6570}

* Alla fall av orättvis terminologi i produkten ska ersättas med vedertagna motsvarigheter (NPR-34311).
* [!DNL Google+] tas bort från listan över alternativ för delning via sociala medier (NPR-33877).

### [!DNL Brand Portal] {#brandportal-6570}

* Användargränssnittet svarar inte när resurserna väljs i [!UICONTROL List View] (NPR-34728).

### [!DNL Forms] {#forms-6570}

>[!NOTE]
>
>[!DNL Experience Manager Forms] släpper tilläggspaketen en vecka efter den schemalagda [!DNL Experience Manager] Lanseringsdatum för Service Pack.

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack innehåller inte korrigeringar för [!DNL Forms]. De levereras med en separat [!DNL Forms] tilläggspaket. Dessutom släpps ett kumulativt installationsprogram med korrigeringar för [!DNL Experience Manager Forms] på JEE. Mer information finns i [Installera AEM Forms-tillägg](#install-aem-forms-add-on-package) och [Installera AEM Forms i JEE](#install-aem-forms-jee-installer).

**Adaptiv Forms**

* Det går inte att redigera ett anpassat formulär med det klassiska användargränssnittet efter användning [!DNL Experience Manager] Service Pack 6 (NPR-35126).

* När du konverterar ett PDF till ett anpassat formulär kan du inte ange ett värde för en kapslad panel med hjälp av en formulärdatamodell i fliklayouten. Det finns dessutom problem när du ställer in ett värde för alternativknappsgrupper dynamiskt med en statisk array med kodredigeraren (NPR-35062).

* När du anger japanska tecken i en textfältskomponent i ett anpassat format kan du ange fler tecken än maxgränsen på 35 tecken (NPR-35039).

* Det adaptiva formuläret innehåller oönskade parametrar, till exempel `owner` och `status`, på **[!UICONTROL Thank you]** sida som visas när formuläret har skickats (NPR-34989).

* The [!UICONTROL File Selection] för [!UICONTROL Attachment] -komponenten visar även filtyper som inte stöds för markering, vilket resulterar i fel vid sändning av anpassningsbara formulär (NPR-34970).

* När du infogar ett adaptivt formulär i en [!DNL Experience Manager Sites] sida som innehåller text före formuläret flyttas markörens fokus direkt till formuläret i stället för texten före formuläret (NPR-34947).

* [!UICONTROL Preview with Data] möjlighet att förifylla ett adaptivt formulär med en [!DNL Experience Manager] 6.2 data-XML-filen fungerar inte korrekt (NPR-35087).

* När du uppdaterar dataordlistan för ett anpassat formulär, översätts inte formuläret eftersom det anpassningsbara formuläret returnerar cachelagrade värden (NPR-34845).

* Fragment tar längre tid att läsa in i en adaptiv form på grund av cacheogiltigförklaring (NPR-34567).

* Tabbnavigering fungerar inte korrekt för skärmläsare i anpassad form (NPR-34544).

**Korrespondenshantering**

* Det går inte att spara värden för XML-taggar med numeriska data, som innehåller flyttalstyp, som ett utkast (NPR-35050).

* När du migrerar resurserna från ES3 innehåller resurserna två icke-redigerbara standardvillkor (NPR-34972).

* När du redigerar en dataordlista i en bokstav visas [!UICONTROL Lent Content] I visas snurrande rektanglar i stället för användbar information (NPR-34853).

**Interaktiv kommunikation**

* Konfigurationsnamnet för interaktiv kommunikation som är tillgängligt när du har installerat [!DNL Forms] tilläggspaket, duplicerar standardkonfigurationsnamnet för utrullning (NPR-34976).

**Dokumentsäkerhet**

* När du sparar en ny dokumentskyddsprofil visas följande i Experience Manager Forms `Relative validity period is required` felmeddelande (NPR-34679).

* Dokumentsäkerhet kan inte skydda dokument från PDF 2.0 (CQ-4305851).

Mer information om säkerhetsuppdateringar finns i [Experience Manager säkerhetsbulletiner](https://helpx.adobe.com/security/products/experience-manager.html).

## [!DNL Adobe Experience Manager] 6.5.6.0 {#experience-manager-6560}

Adobe Experience Manager 6.5.6.0 är en viktig uppdatering som innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat samt prestanda, stabilitet och säkerhetsförbättringar som släppts sedan den allmänna tillgängligheten av 6.5-versionen i **April 2019**. Den kan installeras ovanpå Adobe Experience Manager 6.5.

De viktigaste funktionerna och förbättringarna i Adobe Experience Manager 6.5.6.0 är:

* Publicera eller avpublicera resurser selektivt på [!DNL Experience Manager] eller [!DNL Dynamic Media] använda [!UICONTROL Quick Publish] eller [!UICONTROL Manage Publication] guide.

* Använd [!DNL Dynamic Media] -användargränssnittet för att göra Cachelagrat innehåll i Content Delivery Network (CDN) ogiltigt.

* Publicering av resursavgiftsmappar från Brand Portal till Experience Manager Assets stöds nu även via proxyservern.

* De automatiskt genererade grupperna med privata mappar rensas nu bort när den privata mappen tas bort i [!DNL Experience Manager Assets].

* Beskrivningar av modifierare i video [!UICONTROL Viewer] förinställningsredigeraren har uppdaterats i [!DNL Dynamic Media].

* En ny företagsinställning tillhandahålls för att återspegla statusen för [!DNL Dynamic Media] koppling.

* Standardalternativen för `test` och `aiprocess` uppdateras till `Thumbnail`, från `Rasterize` tidigare i Dynamic Media, för att säkerställa att användarna bara behöver skapa miniatyrbilder och hoppa över sidextraheringen och extraheringen av nyckelord.

* [Fyll i ett anpassat formulär i förväg på klienten](../../help/forms/using/prepopulate-adaptive-form-fields.md#prefill-at-client).

* [Integrering av formulärdatamodell med RESTful API:er på en server med tvåvägs SSL-implementering](../../help/forms/using/configure-data-sources.md).

* [Förbättrad cachning för översatta adaptiva formulärsidor](../../help/forms/using/configure-adaptive-forms-cache.md).

* Stöd för [Adobe Sign texttaggar i tjänsten Automated forms conversion](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html).

* Stöd för [konvertera färgade formulär till anpassningsbara formulär](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html) använda [!DNL Automated Forms Conversion service].

* Stöd för SMB 2- och SMB 3-protokoll.

* Den inbyggda databasen (Apache Jackrabbit Oak) uppdateras till version 1.22.4.

En fullständig lista över funktioner och förbättringar som introducerats i Experience Manager 6.5.6.0 finns på [Nyheter i Adobe Experience Manager 6.5 Service Pack 6](new-features-latest-service-pack.md).

Nedan följer en lista över korrigeringar i [!DNL Experience Manager] 6.5.6.0.

### [!DNL Sites] {#sites-6560}

* I [!DNL Sites] eller [!DNL Screens], väljer ett projekt och klickar på [!UICONTROL Management Publications]. Användarna kan inte gå vidare i [!UICONTROL Manage Publication] guide på grund av gränssnittsfel. I synnerhet [!UICONTROL Publish] fungerar inte (NPR-34099).
* Positionen för iParsys (ärvt styckesystem) återställs inte till den ursprungliga standardpositionen efter avmarkering [!UICONTROL Cancel Inheritance] eller [!UICONTROL Disable Inheritance] optioner (NPR-34097).
* Om `RolloutConfigManagerFactoryImpl` kan inte läsa in en rollout-konfiguration, den försöker inte läsa in de saknade konfigurationerna. Den returnerar de cachelagrade konfigurationerna (NPR-34092).
* I huvudkomponenten för Text, efter att du har använt redigeringsalternativet för HTML, klassen från `em` -taggen tas bort (NPR-34081).
* Efter uppgradering från Experience Manager 6.3.3 till Experience Manager 6.5.3 tar utrullningsprocessen mycket längre tid och utrullningen misslyckas med ett timeoutfel (NPR-34049).
* The `htmlwriter` kodar inte tillbaka attributvärdena. Den kod som finns i XF-koden exporteras med avkodade attributvärden (d.v.s. `"` i stället för `&#34`). Det orsakar problem på målsidan med Visual Experience Composer som använder den exporterade XF-filen (NPR-34048).
* När sidor flyttas in [!DNL Experience Manager Sites], förbättra loggningen för att fånga upp det fel som uppstod när versionen skapades (NPR-34014).
* I [!DNL Rich Text Editor] Om all text tas bort tas även stycketaggen bort (NPR-33976).
* När `siteadmin` (i Classic UI) öppnas eller uppdateras alternativen i `New` -menyn är inaktiverad (NPR-33949).

   ![Skärmbild som illustrerar problemet med saknade menyer i Classic UI](assets/33949_missing_menu.png)

* A [!DNL Content Fragment] kan inte användas som `TemplatedResource` när det inte går att `ContentFragmentUsePojo` (NPR-33911).
* Synkrona och asynkrona flyttningsåtgärder kan leda till fel på grund av samtidiga överföringar. Åtgärder för att flytta sidor är begränsade till asynkron förflyttning. Den förhindrar samtidig flyttning av sidor (NPR-33875).
* [!UICONTROL Manage Publication] åtgärden att replikera innehåll från författare till publiceringsinstans misslyckas och genererar ett JavaScript-fel (NPR-33872).
* När flera sidor eller resurser har valts för att skapa versioner skapas den nya versionen endast för den senast valda sidan eller resursen (NPR-33866).
* Flytta en ritningssida med live-kopior till en annan mapp. När du flyttar den till den ursprungliga mappen misslyckas flyttåtgärden utan något fel (NPR-33864).
* När flyttningsåtgärden används för att byta namn på en webbsida i [!DNL Sites] På konsolen visas två överlappande dialogrutor i det sista steget i guiden (NPR-33831).

   ![Skärmbild som illustrerar NPR-33831-utgåvan av dialogrutan för överlappande flyttning](assets/33831_rename_dialog.png)

* The `cq:acLinks` och `cq:acUUID` egenskaper för [!DNL Adobe Campaign] på kopian tas bort under kopierings- och inklistringsåtgärden (NPR-33794).
* När du försöker distribuera en underordnad sida till en frånkopplad överordnad live-kopia, [!DNL Experience Manager] genererar ett null-pekarundantag (NPR-33676).
* The [!DNL RTE] -komponenter i en layoutbehållare visas inte när layoutbehållaren kopieras och klistras in igen på sidan. The [!DNL RTE] -komponenter går inte att redigera, men visas vid uppdatering av sidor (NPR-33662).
* När du ändrar storlek på en layoutkomponent för olika brytpunkter (mellanstora och stora) fungerar inte layouten som förväntat (NPR-33608).
* I infogat redigeringsläge i [!DNL RTE]fungerar inte det att dra en bild för textkomponenten (NPR-33602).
* Det går att skapa en komponent på en ritningssida med samma namn som sidnamnet. Under utrullning `_msm_moved` har suffix för att byta namn på komponenten. Komponenten flyttas till slutet av [!UICONTROL Paragraph System] (NPR-33535).
* När offTime eller onTime är inställt på många sidor eller resurser är det resurskrävande och gör systemet långsammare vid start och avstängning (NPR-33482).
* En användare med CRUD-behörighet för `/content/experience-fragment` kan inte ta bort en mapp (NPR-33436).
* Du kan välja [!UICONTROL HTML & JSON] som alternativ för [!UICONTROL Adobe Target export format] på en överordnad mapp i [!DNL Experience Fragments] -avsnitt. Samma egenskaper visas i det Touch-aktiverade användargränssnittet för undermapparna i den här överordnade mappen. I CRXDE, för `cq:adobeTargetExportFormat`visas bara HTML i stället för att visas `html,json` (NPR-33423).
* Publicera eller Avpublicera från ett sidalias stöds inte. Ta bort alternativet som verkar göra anspråk på något annat (NPR-33415).
* En viss tagg kan flyttas från en plats till en annan i [!DNL Experience Manager]. Den kan även tillämpas på olika sidor före och efter att den flyttas. När du redigerar egenskaperna för sidorna visas inte taggen för redigering även om taggen är densamma (NPR-33353).
* En sidmall återges inte korrekt när en layoutbehållare tas bort från en mall som innehåller flera layoutbehållare (NPR-33347).
* I mallredigeraren kan du försöka ta bort en mall som används av mer än 100000 sidor under `/content/`. Ett fel visas utan något felmeddelande (NPR-33312).
* Omdirigering till [!DNL Experience Manager] sida med ankarpunkt fungerar inte på författarinstans som `PageRedirectServlets` skickar frågesträngen efter ett URL-fragment eller ett ankare (NPR-34288).
* Skapa ett varumärke under `/content/campaign` resulterar i en struktur som inte tillåter att kampanjer skapas. [!UICONTROL Create Brand] lämnar det nyskapade varumärket utan möjlighet att skapa [!UICONTROL Offers and Activities] eftersom det inte finns något [!UICONTROL Create] option (NPR-34113).
* Du kan göra uppehåll i [!DNL Live Copy] för en sida och arv bryts i som de visas i redigeringsläget. I sidegenskaperna indikerar ikonen som representerar arv felaktigt att arvet finns och inte är brutet (NPR-34017).
* Sidor med många referenser kan inte flyttas asynkront och ibland misslyckas flyttåtgärden (CQ-4297969).
* En webbsida med `/` i URL:en slutar svara vid redigering. När en komponent läggs till under utvecklingen ökar processoranvändningen och webbläsaren slutar svara (CQ-4295749).
* I bläddringsläget lägger inte NVDA till en berättarröst för ett värde som är valt på menyalternativet Typ/Storlek. Det visuella fokus ligger inte på det markerade elementet. Användare som förlitar sig på en skärmläsare kan inte använda bläddringsläget (CQ-4294993).
* När du skapar en webbsida kan användarna välja [!UICONTROL Content Page] mall. I [!UICONTROL Social Media] -flik, användare välja [!UICONTROL Preferred XF variation]. Användarna kan inte använda tangentbordstangenter för att välja ett Experience Fragment i NVDA-bläddringsläge (CQ-4292669).
* Hanteringsbiblioteket uppdaterades till den säkrare versionen v4.7.3 (NPR-34484).
* Flera serveröverskridande skriptinstanser i [!DNL Experience Manager Sites] komponenter (NPR-33925).
* Mappnamnsfältet när du skapar en ny mapp kan användas med korsskriptning mellan webbplatser (GRANITE-30094).
* Sökresultaten på[!UICONTROL  Welcome] sidan och mallen för komplettering av sökväg är sårbara för serveröverskridande skriptning (NPR-33719, NPR-33718).
* Om du skapar en binär egenskap på en ostrukturerad nod får du serveröverskridande skriptning (cross-site scripting) i dialogrutan för binär egenskap (NPR-33717).
* Serveröverskridande skript vid användning [!UICONTROL Access Control Test] i CRX DE-gränssnittet (NPR-33716).
* Användarindata är inte korrekt kodade för olika komponenter när information skickas till klienten (NPR-33695).
* Serveröverskridande skriptning (cross site scripting) i kalendervyn för Experience Manager Inbox (NPR-33545).
* En URL som slutar med `childrenlist.html` visar en HTML-sida i stället för ett 404-svar. Sådana URL:er är sårbara för serveröverskridande skriptning (NPR-33441).


### [!DNL Assets] {#assets-6560}

**Tillgänglighetsförbättringar i Experience Manager Assets**

* Med tangentbordstangenterna kan användarna nu komma åt och fokusera på de interaktiva gränssnittsalternativen i [!UICONTROL References] Förteckning över tillgångar (NPR-34115).

* Skärmläsaren presenterar nu avsedd åtgärd för predikaten på söksidan (NPR-34104).

* Söksidan och sökresultatsidan har nu mer informativa titlar för att förstå skärmläsaranvändare bättre (NPR-34093).

* Skärmläsare meddelar nu vilka alternativ som finns för att ta bort de markerade taggarna i [!UICONTROL Basic] tillgångsflik [!UICONTROL Properties] sidan (NPR-33972).

* Elementen i varje rad i listvyn presenteras nu som element i samma rad av skärmläsare (NPR-33932).

* Användarfokus vid navigering med `Tab` går nu till stängningsalternativet i förhandsgranskning av version (NPR-33863).

* Användarfokus flyttas nu till sökikonen när Omnissearch har stängts (NPR-33705).

* Alternativen i det användbara gränssnittet har nu ett mer framträdande visuellt fokus med förbättrad kontrast när du navigerar med tangentbordstangenter. Tangentbordsanvändare kan identifiera de fokuserade områdena (NPR-33542).

* Dragningsfunktionen med tangentbordet fungerar nu i [!UICONTROL Metadata Schema Editor] i bläddringsläge för skärmläsare (CQ-4296326).

* När du navigerar i bläddringsläge i dialogrutan för länkdelning visas en skärmläsare,

   * Berättar inte tabellinformationen så fort dialogrutan har lästs in.

   * Kan navigera till alla automatiska förslag som visas.

   * Lägger till en berättarröst för de automatiska förslag som visas för [!UICONTROL Add Email Address/Search] (CQ-4294232).

* Användning av `Esc` tangenten för att ta bort snabbredigeringsikonerna från kortvyn tar inte längre bort tangentbordsfokus från det senast fokuserade objektet (CQ-4293554).

* För interaktiva alternativ i användargränssnittet meddelar skärmläsaren nu vad de är avsedda för och inte vad ikonerna har för litteralnamn (CQ-4272943).

* Tangentbordsfokus flyttas nu till [!UICONTROL Flyout], [!UICONTROL InlineZoom], [!UICONTROL Shoppable_Banner], [!UICONTROL Zoom_dark], [!UICONTROL Zoom_light], [!UICONTROL ZoomVertical_dark]och [!UICONTROL ZoomVertical_light] alternativ vid navigering med tangentbordsfliktangenten i resursinformationen [!UICONTROL Viewers] in [!DNL Dynamic Media] (CQ-4290605).

* [!UICONTROL Save & Close] option on asset [!UICONTROL Properties] sidan kan nu öppnas med tangentbordstangenter (NPR-34107).

* Felmeddelanden på grund av felaktiga kombinationer av användarnamn och lösenord på inloggningssidan meddelas nu av skärmläsare varje gång felet inträffar (NPR-33722).

* I [!DNL Experience Manager] sidhuvudsavsnittet, när du navigerar i bläddringsläge, visas nu meddelanden i skärmläsaren,

   * Automatiskt redigerade förslag i [!UICONTROL Type to search] i Omnisearch.

   * Läget som expanderat eller komprimerat för [!UICONTROL Solutions], [!UICONTROL Help], [!UICONTROL Inbox]och [!UICONTROL User] alternativ.

   * The [!UICONTROL Searching Help] statusmeddelande som visas när användaren anger en söksträng i [!UICONTROL Search for Help] fält under [!UICONTROL Help] alternativ.

   ![Hjälpmenyn i sidhuvudet](assets/Help_aem_header.png)

   *Bild: [!UICONTROL Search for Help] in [!UICONTROL Help] -menyn.*

   * Felmeddelandet om ett felaktigt värde anges i [!UICONTROL Impersonate as] fält under [!UICONTROL User] och fokus flyttas korrekt till textfältet (NPR-33804).

   ![Användarmeny i sidhuvud](assets/User_aem_header.png)

   *Bild: [!UICONTROL Impersonate as] fält i [!UICONTROL User] meny i sidhuvud.*

* Användaren kan nu ändra fokus med tangentbordet i:

   * [!UICONTROL Search/Add Email Address] i [!UICONTROL Link Sharing] -dialogrutan.

   * [!UICONTROL Add User or Group] fält under [!UICONTROL Closed User Group] i [!UICONTROL Permissions] mappflik [!UICONTROL Properties] (NPR-34452).

**Problem som har korrigerats i Experience Manager Assets**

[!DNL Adobe Experience Manager] 6.5.6.0 [!DNL Assets] innehåller korrigeringar av följande problem:

* Anteckningar markeras inte när de väljs från resursens tidslinje (CQ-4302422).

* Förhandsgranskning av marknadsmaterial (t.ex. broschyr, flygblad och visitkort) som skapats med [!DNL Adobe InDesign] mallen visar inte radbrytningar och styckebrytningar (NPR-34268).

* Textextrahering och därmed textsökning för överförda PDF-filer fungerar inte (NPR-34164). Åtgärda problemet genom att starta om [!DNL sAdobe Experience Manager] efter installation av Service Pack 6.

* På tidslinjen för flersidiga resurser visas anteckningar som används för alla underresurser när du bläddrar bland resursen i tidslinjevyn i stället för att anteckningarna som är specifika för de specifika underresurserna visas (NPR-34100).

* Resursmappar publiceras inte med [!UICONTROL Manage Publication] om mapparna innehåller resurser i JavaScript-, CSS- eller JSON-filformat (NPR-34090).

* Om du avmarkerar eller tar bort de tillämpade taggarna eller filtren i Omnissearch körs sökfrågan flera gånger, vilket leder till att söktiden ökar (NPR-34078).

* I kortvyn när ett arbetsflöde (för en resurs i en mapp) pågår eller väntar, läses sidan in igen tills arbetsflödet har slutförts eller avslutats. Därför kan författare inte arbeta med de resurserna i den mapp som de måste rulla nedåt för (NPR-33986).

* Om användaren flyttar en publicerad resurs till en ny plats publiceras resursen om, även om [!UICONTROL Republish] alternativet är avmarkerat. Detta leder till att många överblivna resurser ligger i publiceringsinstansen. Standardbeteendet är dock att om du flyttar en åtgärd på en publicerad resurs återpubliceras den automatiskt. den här resursen publiceras på nytt om författaren väljer [!UICONTROL Republish] option when moving the asset (NPR-33934).

* The [!UICONTROL Move Assets] sidan för resurser i samlingar inte läser in allt innehåll i HTML, till exempel [!UICONTROL Adjust/ Republish] alternativ. Därför kan användare inte slutföra flyttåtgärden (NPR-33860).

* Om du flyttar en resurs och lägger till specialtecken i namnet och titeln på de flyttade resurserna skapas en extra mapp (med samma namn) på den nya platsen för resursen (NPR-33826).

* [!UICONTROL Download] knappen för en resurs inaktiveras när [!UICONTROL Email] alternativet är markerat på [!UICONTROL Download] dialogrutan (NPR-33730).

* Felet&quot;Begär-URI för lång&quot; visas vid gruppåtgärder för resurser, t.ex. redigering av massmetadata (NPR-33723).

* JavaScript-fel observeras och användare kan inte markera eller ta bort de alternativ som genererats i [!UICONTROL Dropdown] fält efter [!UICONTROL Add through JSON path] i [!UICONTROL Folder Metadata Schema Form Editor], om den överförda JSON-filen har blanksteg eller specialtecken i värde (NPR-33712).

* De statiska återgivningarna av resurser uppdateras inte när resursen uppdateras med [!UICONTROL Open] alternativ i [!DNL desktop app] eller [!DNL Adobe Asset Link] och synkroniseras tillbaka till [!DNL Adobe Experience Manager] (CQ-4296279).

* I kolumnvyn flyttar flyttåtgärden för en uppsättning resurser även de resurser som markerades innan de användes [!UICONTROL Filter] för dem. Observera att [!UICONTROL Filter] avmarkerar föregående markering (NPR-34018).

* Omvända snedstreck läggs till före specialtecken i sökförslag för resurser, som har specialtecken i sitt namn (NPR-33834).

* När regler för listrutor skapas i [!UICONTROL Folder Metadata Schema Form], användaren kan inte välja värden från [!UICONTROL Field Choices] kolumn (CQ-4297530).

* Körningskopian av resurser, anpassad arbetsflödesmodell (skapad i `/var/workflow/models/dam`) tas bort när du installerar [!DNL Experience Manager] 6.5 Service Pack 5 eller en tidigare version på [!DNL Experience Manager] 6.5 (NPR-34532). Om du vill hämta körtidskopian synkroniserar du designtidskopian av arbetsflödesmodellen med körtidskopian med HTTP API:
   `<designModelPath>/jcr:content.generate.json`.

**Problem som har korrigerats i Dynamic Media**

* Om användaren definierar kodningsinställningarna i redigeringar efter att videoprofilen har skapats, tas inställningarna för smart beskärning bort från videoprofiler (CQ-4299177).

* Resurser flimmer vid sidinläsning när användaren växlar mellan alternativ för sidospår (till exempel [!UICONTROL Overview], [!UICONTROL Timeline], [!UICONTROL Viewers]) på sidan med tillgångsinformation (NPR-34235).

* Följande problem har observerats med omprocessjobb:

   * Jobb-ID saknas i jobbreferensen som returnerades av ombearbetningsjobbet.

   * Bearbeta om jobb för enbart videologgar med filnamn och inte fullständig sökväg.

   * Återbearbetningsjobbet har inte möjlighet att ange resurstypen som statisk.

   * `ExcludeFromAVS` finns inte (CQ-4298401).

* Funktionen för smart beskärning misslyckas med fel när en bildprofil läggs till i en mapp med flera (till exempel 11) proportioner (NPR-34082).

* Arbetsflödet för DAM-uppdateringsresurser aktiveras när användaren rullar nedåt [!UICONTROL Workflow Archive] sida på [!UICONTROL Workflow] tabba i [!UICONTROL Tools] in [!DNL Adobe Experience Manager] konfigurerat med Dynamic Media Scene7 (CQ-4299727).

* Symboler i [!UICONTROL Behavior] flik för [!UICONTROL Viewer Preset Editor] är inte lokaliserade (CQ-4299026).

* I huvudvyn visas bilden i en felaktig layout som inte får plats i visningsprogrammet, om visningsprogrammet är i svarsläge (CQ-4298293).

* Ändringar av bildförinställningar i [!UICONTROL Adobe Experience Manager] synkronisera inte med Scene7 Publishing System (CQ-4299713).

### [!DNL Commerce] {#commerce-6560}

* Länkar till resurser från produkter ändras inte när resurser flyttas (NPR-34098).

### Plattform {#platform-6560}

* Det går inte att hämta loggar med diagnosverktyget på en uppgraderad Experience Manager-instans (NPR-34336).
* Uppgraderingen misslyckas med ett fel på grund av beroenden till en viss version av `cq-wcm-api` Foundation package (CQ-4300520).
* Standardvärdena för **[!UICONTROL Connect Timeout]** och **[!UICONTROL Socket Timeout]** inställningarna för standardagentkonfigurationen (publicering) har inte angetts (NPR-33707).
* Uppdateringar av mappningskonfigurationen under `/etc/map.publish` återspeglas inte på webbplatssidorna (NPR-34015).
* [API-referensdokumentation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html) innehåller inte dokumentation för `com.day.cq.tagging` paket (CQ-4295864).

### Användargränssnitt {#ui-6560}

* Gränssnittet för avlastningsläsaren visar inte alla jobbämnen (NPR-34308).
* The [Konfigurationsläsaren](/help/sites-administering/configurations.md) gränssnittet visar inte alla konfigurationer (NPR-33644).
* Tryck på `Esc` när du söker efter användare att personifiera, **[!UICONTROL User]** stängs i stället för användarlistan (NPR-34084).

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

* Foundation Components - När du lägger till en grundläggande bildkomponent på en sida och refererar till en bild, `Undo` åtgärden fungerar inte (NPR-34516).

* Det går inte att använda åtgärden Sidflyttning (CQ-4303028).

### [!DNL Communities] {#communities-6560}

* Att dela ett inlägg på sociala medier visar ett föråldrat alternativ, Google+ (NPR-33877).

* Community-medlemmen kan inte ändra gruppmallen eller andra gruppfunktionsinställningar (NPR-33530).

* Hyperlänkstaggar i bilder genereras inte korrekt i ett foruminlägg (NPR-33464).

* Tillgänglighetsfel identifieras i funktionen för communitytilldelning (NPR-33442).

* Befintliga användare i en community-grupp som lagts till via Admin Console tas bort från användarlistan vid ändringar i community-gruppkonsolen (NPR-34315).

* The `TagFilterServlet` läckage av potentiellt känsliga data (NPR-33868).

<!--
* Tag filters are vulnerable to sensitive information disclosure (NPR-33868).
-->

### [!DNL Forms] {#forms-6560}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack innehåller inte korrigeringar för [!DNL Forms]. De levereras med en separat [!DNL Forms] tilläggspaket. Dessutom släpps ett kumulativt installationsprogram med korrigeringar för [!DNL Experience Manager Forms] på JEE. Mer information finns i [Installera AEM Forms-tillägg](#install-aem-forms-add-on-package) och [Installera AEM Forms i JEE](#install-aem-forms-jee-installer).

När du har installerat [!DNL Experience Manager Forms] 6.5.6.0-tilläggspaket:

* Stoppa [!DNL Experience Manager Forms] -instans.

* Ta bort `bcpkix-1.51`, `bcmail-1.51`och `bcprov-1.51` JAR-filer från `crx-repository\launchpad\ext` katalog.

* Ta bort` sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider` -egenskapen från `sling.properties` -fil.

* Starta om [!DNL Experience Manager Forms] -instans.

**Adaptiv Forms**

* Om det saknas ett adaptivt formulärfragment återges inte det adaptiva formuläret (NPR-34302).

* Hjälpinnehållsbeskrivningen för adaptiva formulärfält visar taggen HTML (NPR-34116).

* När du väljer **[!UICONTROL Revalidate on Server]** egenskapen, det adaptiva formuläret inte kan skickas (NPR-33876).

* The **[!UICONTROL Submit to REST endpoint]** Skicka-åtgärden fungerar inte för anpassningsbara formulär (CQ-4299044).

* Tillgänglighet: När du försöker skicka ett anpassat formulär utan att överföra en bilaga för ett obligatoriskt fält flyttas fokus inte automatiskt till bilagefältet (CQ-4298065).

* När du lägger till rader i en tabell i ett anpassat formulär visas **[!UICONTROL Add to top]** och **[!UICONTROL Add to bottom]** alternativ inte visar lämpliga resultat (CQ-4297511).

* The [!UICONTROL Value Commit] skriptet aktiveras felaktigt, vilket resulterar i dataförlust i en adaptiv form (CQ-4296874).

* Datumväljaren fungerar inte korrekt för lokaliserade adaptiva formulär (NPR-34333).

* När det finns ett understreck eller blanksteg i filnamnet kan du inte bifoga filen till ett anpassat formulär (CQ-4301001).

* När en kapslad upprepningsbar panel har fler förekomster än den överordnade panelen, kan inte alla förekomster av den kapslade upprepningsbara panelen fyllas i i förväg (NPR-33666).

* Adaptiva formulär har vissa öppna resurslösningar. Detta leder till att det inte går att skicka in. Problemet inträffar då och då (CQ-4299407).

* När du öppnar fältkonfigurationen för första gången visas inte egenskapsikonen (CQ-4296284).

* Användare kan redigera inskickningsmetadata, t.ex. `afPath`, `afSubmissionTime` och `signers`när du skickar in ett anpassat formulär. För att lösa problemet tas metadatavärdena bort från informationen om att skicka formulär på klientsidan. Användarna kan använda `FormSubmitInfo` -objekt för att hämta dessa värden från servern (NPR-33654).

* Användarindata är inte korrekt kodade för [!DNL Forms] komponenter när information skickas till klienten (NPR-33611).

**Arbetsflöde**

* När en arbetsflödesgodkännare överför en bifogad fil får den bilagan ett nytt namn `undefined` (NPR-33699).

* [!DNL Experience Manager] Åtgärd för tömning av arbetsflöde misslyckas och följande felmeddelande visas (NPR-33575):

   `java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory`

* [!DNL Experience Manager Forms] app för [!DNL Windows] slutar svara efter att ett formulär har skickats (NPR-34409).

* När du installerar AEM Service Pack **Att göra** objektlistan visas inte som länkar. Texten för **Att göra** -objekt omfattar HTML-taggar (NPR-34317).

**Interaktiv kommunikation**

* När du inkluderar ett textdokumentfragment med kapslade repeterbara komponenter, sparas inte det interaktiva meddelandet (NPR-34095).

**Korrespondenshantering**

* När du ändrar ett textdokumentfragment som innehåller data dictionary-värden slutar agentens användargränssnitt svara (NPR-33930).

* Kopiera och klistra in innehåll från en [!DNL Microsoft Word] dokument till ett textdokumentfragment i en bokstav resulterar i formateringsproblem (NPR-33536).

**Dokumenttjänster**

* När du genererar en PDF-fil från en XDP-fil med hjälp av utdata och Forms-tjänster, leder det till att text saknas och överlappar (NPR-34237, CQ-4299331).

* När du konverterar en HTML-fil till PDF `MaxReuseCount` är inte konfigurerbart (NPR-33470).

* När du hämtar en PDF-fil med interaktiva funktioner för Reader Extensions kan du inte lägga till en bifogad fil i PDF med [!DNL Adobe Reader] (NPR-33729).

**Dokumentsäkerhet**

* Det går inte att utföra signeringsåtgärden med HSM-baserade certifikat i en PDF-fil efter installation [!DNL Experience Manager] Service Pack (NPR-34310).

**Designer**

* Det går inte att öppna Xformuläri Designer version 6.5.x (CQ-4295322).

* När du öppnar Designer visas ett felaktigt år på välkomstskärmen (CQ-4295289).

* När du installerar [!DNL Acrobat DC] på servern, **[!UICONTROL Distribute Form]** är inaktivt (CQ-4296304).

Mer information om säkerhetsuppdateringar finns i [Experience Manager säkerhetsbulletiner](https://helpx.adobe.com/security/products/experience-manager.html).

## [!DNL Adobe Experience Manager] 6.5.5.0 {#experience-manager-6550}

Adobe Experience Manager 6.5.5.0 är en viktig uppdatering som innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat samt prestanda, stabilitet och säkerhetsförbättringar som släppts sedan den allmänna tillgängligheten av 6.5-versionen i **April 2019**. Den kan installeras ovanpå Adobe Experience Manager 6.5.

Några viktiga funktioner och förbättringar i [!DNL Adobe Experience Manager] 6.5.5.0 innehåller följande:

* Anonym åtkomst till CRXDE Lite är inte tillåten. I stället dirigeras användarna till inloggningsskärmen. Se [Utveckla med CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

* Anpassa kolumnnamnen som visas i [!DNL Adobe Experience Manager] Inkorgen.

* Förbättrad tillgänglighet inom olika områden i Experience Manager Web Content Management (WCM), t.ex. sidredigeraren, Core Components, RTE och administratörsgränssnittet.

* Spara en [!DNL Interactive Communication] som ett utkast.

* Stöd för [!DNL Oracle WebLogic 12] för Experience Manager Forms på JEE.

* Förbättrad undantagshantering i [!DNL Adobe Experience Manager Assets] användargränssnittsflöde.

* En ny metod för att hämta publicerings-URL för Dynamic Media Scene7 `getRemoteAssetPublishURL` läggs till i `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi` gränssnitt.

* [Förbättrad tillgänglighet](#assets-6550) in [!DNL Adobe Experience Manager Assets] i enlighet med Web Content Accessibility Guidelines (WCAG).

* Paketdelningsintegrering har tagits bort från Adobe Experience Manager.

* Den inbyggda databasen (Apache Jackrabbit Oak) uppdateras till version 1.2.3.

En fullständig lista över funktioner, viktiga högdagrar, viktiga funktioner som introducerades i Experience Manager 6.5 Service Pack 5 finns på [Nyheter i Adobe Experience Manager 6.5 Service Pack 5](new-features-latest-service-pack.md) .

Nedan följer en lista över korrigeringar i [!DNL Experience Manager] 6.5.5.0-versionen.

### [!DNL Sites] {#sites-6550}

* Experience Manager Sites erbjuder ett alternativ för att publicera eller avpublicera en sida från dess alias. Alternativet fungerar inte (NPR-33415).
* När en layoutbehållare tas bort från en mall som innehåller flera mallar återges inte mallen korrekt (NPR-33347).
* När en Experience Manager Sites-sida är en del av en stor innehållsuppsättning med flera live-kopior går det inte att läsa in förhandsgranskningen av sidversionshistoriken (NPR-33311).
* När du använder kommandot Flytta för att byta namn på en Experience Manager Sites-sida uppdateras inte sidtiteln (NPR-33264).
* När du flyttar sidor genom kolumnvyn försvinner kolumnerna (NPR-33216).
* När namnet på en lokal komponent i en språkkopia är identiskt med namnet på en komponent i utkastet och komponenten rullas ut från utkast, term `_msm_moved` läggs inte till namnet på den lokala komponenten (NPR-33208).
* Servern för omdirigering av sidor lägger till .html till en Experience Manager Sites-URL där ResourceType inte är `cq:Page` (NPR-33176).
* När du klistrar in ett underträd finns det inget alternativ för att bestämma om motsvarande undersidor ska klistras in eller inte (NPR-33149).
* Antalet resultat i direktanvändning av en komponent är begränsat till nummer 49 (NPR-33058).
* När du baserar ett innehållsfragment på ett schema och det innehåller ett obligatoriskt textområde eller ett sökvägsfält, kan innehållsfragmentet inte sparas (NPR-33007).
* När du skapar en anpassad komponent med standardkomponenten för Experience Fragment och använder den på Experience Manager Sites-sidor, visar inte Experience Manager referenser (användning) för den anpassade komponenten (NPR-32852).
* När du byter namn på en mapp med ett stort antal referenser uppdateras inte många referenser till mappen (NPR-32765).
* När du aktiverar källredigeringsalternativet blir det tillgängligt för alternativ för helskärmsvisning, men saknas för redigeringsdialogruta och alternativ för helskärmsvisning i textredigeraren (NPR-32763).
* Om du har ett flerfält och det innehåller ett obligatoriskt fält (till exempel en listruta eller ett sökvägsfält) i sidegenskaperna för en plan, sparas inte sidegenskaperna för live-kopian när en sida som innehåller ett sådant flerfält öppnas (NPR-32751).
* Skärmläsare kan inte använda rubrikstrukturen för att navigera på en sida. Dessutom har fliken Komponenter fel etikett (NPR-32648).
* När sidnumreringen startar läses inte Experience Fragments Picker in alla objekt (NPR-32605).
* Författarbehörigheter för att läsa, ändra, skapa och ta bort live-kopior återkallas. Varje författare måste uttryckligen ange läs- och ändringsbehörigheter för att kunna flytta sidor i en utkast (NPR-32550).
* Innehållsförfattare kan inte skapa Launch för en sida som är integrerad med Adobe Analytics (NPR-32548).
* När en användare återupptar arv med synkronisering synkroniseras inte den överordnade sidans live-kopia med ritningen och visar en felaktig status (NPR-32500).
* Det tar mer än 15 sekunder att läsa in Experience Manager Sites redigeringssida (NPR-32413).
* I vissa fält visas inte alternativet Avbryt arv (NPR-32362).
* När du markerar en sökväg för en Experience Fragment-komponent och markerar kryssrutan Öppna dialogrutan Markering, navigeras du inte till den valda sökvägen i sökvägsläsaren (NPR-32308).
* När du uppgraderar från Experience Manager 6.2 till Experience Manager 6.5 visas inte Parsys-komponenten för statiska mallar korrekt. Parsys-komponentens höjd anges till 0 och komponenterna i den är inte synliga (NPR-33663).
* När en användare kopierar och klistrar in en layoutbehållare på samma sida visas inte komponenterna i en layoutbehållare (NPR-33648).
* Dispatcher-hälsokontroller visas `Invalid cookie header` varningsmeddelande i loggfilerna (NPR-33629).
* Speglad XSS i PreferencesServlet (NPR-33438).
* Anonyma användare har tillgång till CRXDE Lite-funktioner (GRANITE-27790).

### [!DNL Assets] {#assets-6550}

>[!IMPORTANT]
>
>Windowsanvändare av [!DNL Experience Manager desktop app] rekommenderar vi att du uppgraderar till [datorprogram version 2.0.3.2](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html#what-is-new) för att komma åt DAM-databasen på [!DNL Adobe Experience Manager 6.5.5.0] -instans. Eftersom de kan stöta på problem vid åtkomst till DAM-databasen på [!DNL Adobe Experience Manager] 6.5.5.0-instans som använder datorprogrammet version 2.0.2.

**Tillgänglighetsförbättringar i Experience Manager Assets**

* Nu går det att fokusera på tangentbordet [!UICONTROL Comments] lista och klickbart alternativ till [!UICONTROL Create] versionskommentarer under [!UICONTROL Create new version] in [!UICONTROL Timeline] tillgångspanel (NPR-33424).

* Nu är det möjligt att nå [!UICONTROL View Settings] alternativ för resurser och ändra inställningar i [!UICONTROL View Settings] dialogruta med tangentbordstangenter (NPR-33420).

* Listrutans popup-meny för kombinationsrutan (i olika fält på olika sidor) visar nu poster som en lista med alternativ som kan tillkännages av skärmläsare (NPR-33516).

* Sorteringsfunktionen för sorterbara rubriker (i listvyn, [!UICONTROL Timeline] visa och [!UICONTROL Manage Publication] sida) presenteras nu av skärmläsare och sorteringskontroller för kolumnrubriker som är tillgängliga via tangentbordet (NPR-32979).

* Klickbara element som kommentarkort, versionsuppdateringar, kombinationsrutor och ikoner för menyerna kan nu fokuseras och interagera med tangentbordet (NPR-33514).

* Funktionalitet (eller syfte) för insikter, ikoner (för användning, visningar och klickningar) på [!UICONTROL Insights View] presenteras nu korrekt av skärmläsare (NPR-33513).

* Skrivskyddade formulärfält (t.ex. inaktiverade fält på [!UICONTROL Basic tab] av tillgång [!UICONTROL Properties]) kan nu fokuseras med tangentbordet (NPR-33493, CQ-4273031).

* Etiketter i olika indatafält är nu permanenta etiketter (så att de är tillgängliga) och inte bara platshållaretiketter, som försvinner när texten skrivs (NPR-33475).

* Olika rubriknivåer (t.ex. sidrubriker och avsnittsrubriker) uppfattas nu som rubriker med olika nivåer för skärmläsaranvändare (NPR-33471).

* Interaktiva element i användargränssnittet, t.ex. länkar och alternativ (för rubrik- och zoomalternativ på tillgångssidan, mappnavigering), är nu tillgängliga via ett tangentbord (NPR-33468, CQ-4271412).

* The [!UICONTROL Options], [!UICONTROL Scope]och [!UICONTROL Workflows] förloppsindikatorer för [!UICONTROL Manage Publication] sidan läses nu ut korrekt av skärmläsare som förloppsindikatorer i stället för som flikar (NPR-33416).

* Färgen på stjärngraderingsikoner (t.ex. i [!UICONTROL Rating] avsnitt i [!UICONTROL Advanced] flik i resurs [!UICONTROL Properties] eller i kortvyn) ändras så att lämplig kontrast blir synlig för användare med begränsad syn och utan att färgerna uppfattas (NPR-33414).

* Sparruppil bredvid [!UICONTROL Comment] fält på tillgångsinformationssidan kan nu öppnas med hjälp av tangentbordstangenter (NPR-33397).

* De utökade och komprimerade lägena för [!UICONTROL Tags] dialogruta för resurs [!UICONTROL Properties] och navigering till vänster (i tillgångsanvändargränssnittet) annonseras nu korrekt av skärmläsare (NPR-33396).

* Titlar på alla bläddrade sidor på [!DNL Adobe Experience Manager] Resurserna är nu unika (NPR-33343).

* När du navigerar i trädstrukturen visas nu olika element i trädvykontrollen korrekt av skärmläsare (NPR-33304).

* Olika versioner av resurser i [!UICONTROL Timeline] sidan med tillgångsinformation är nu tillgänglig med tangentbordstangenter (NPR-33283).

* Namn på sökförslag som visas i kombinationsrutan Omnissearch meddelas nu av skärmläsare när sökfunktionen används (NPR-33280).

* Klickbara element och [!UICONTROL Go to link] in [!UICONTROL References rail] presenteras nu som klickbara element av skärmläsare (NPR-33278).

* Tabellstrukturinformation (t.ex. rad 1, cell 1, tabell) för [!UICONTROL Share Link] dialogrutan visas inte längre av skärmläsare när dialogrutan öppnas (NPR-33268).

* Syftet med olika kombinationsruteelement (t.ex. fältet Sökväg och alternativet att öppna dialogrutan Markering på fliken Grundläggande i resursegenskaper) har nu annonserats korrekt av skärmläsare (NPR-33235).

* Information om att raderna i listvytabellen kan markeras skickas nu till skärmläsaranvändare när tangentbordsfokus är på dem. När en pekare placeras på raderna visas informationen (NPR-33234).

* Alternativ (med [!UICONTROL x]) för att ta bort alla markerade taggar under [!UICONTROL Tags] fält i [!UICONTROL Basic] flik för [!UICONTROL Properties] är nu tillgängliga för skärmläsare (NPR-33206).

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

* Syftet med nedre gräns ([!UICONTROL From]) och övre gräns ([!UICONTROL To]) indatafält för filstorleksfiltret visas nu för användare som inte har en synkad skärmläsare (NPR-32064).

* The [!UICONTROL Languages] menyn i [!UICONTROL Create and Translate] -formuläret är nu tillgängligt för skärmläsare i bläddringsläge (CQ-4293906).

* The [!UICONTROL References] Panelen är nu tillgänglig med följande förbättringar (NPR-33261, CQ-4293798):

   * I bläddringsläge flyttas skärmläsarens fokus inte längre till dolda redigeringsfält med flera rader under [!UICONTROL Site References], [!UICONTROL Asset References], [!UICONTROL Copies]och [!UICONTROL Form References] -avsnitt.

   * Skärmläsare presenterar nu rollen som [!UICONTROL Site References] och [!UICONTROL Language Copies] -element.

   * Skärmläsarnas fokus i bläddringsläge ändras i en meningsfull sekvens till olika element.

* [!UICONTROL Metadata Schema Editor] sidan och dess element är nu tillgängliga via tangentbordet och är skärmläsarvänliga (CQ-4290962, CQ-4272953).

* Syftet med `X` symbolen för att ta bort de markerade taggarna visas nu av skärmläsare tillsammans med antalet markerade taggar (CQ-4273017).

* För att undvika förvirring för användare som inte är synkade med skärmläsare ignoreras nu dekorativa ikoner och bilder av skärmläsare (CQ-4272944).

**Problem som har korrigerats i Experience Manager Assets**

[!DNL Adobe Experience Manager] 6.5.5.0 Resurser innehåller korrigeringar av följande:

* [!UICONTROL Start] alternativ på [!UICONTROL Create Workflow] dialogrutan för resurser i en samling är inaktiverad, vilket förhindrar att arbetsflödet aktiveras (NPR-32471).

* När du använder överlappande popup-fönster i metadatascheman försvinner det valda alternativet för apostrof när du väljer och sparar ett nedrullningsbart alternativ som innehåller en apostrof (från den underordnade listrutan) efter att resursen öppnats på nytt [!UICONTROL Properties] (NPR-32649).

* [!UICONTROL Assets Insights Sync Job] stoppar och misslyckas om ogiltiga poster påträffas (på analyssidan) i stället för att nästa post (NPR-32674) flyttas.

* Gyroscope fungerar inte eftersom rörelsesensorerna är inaktiverade som standard i mobilwebbläsare i panoramavisare (CQ-4272937).

* [!UICONTROL Connected Assets Configuration] guide fungerar inte med 404-fel vid installation av 6.5.3 i 6.5.1 (NPR-32730).

* Under XMP tillbakaskrivning ändrar alla anpassade namnutrymmesmetadataegenskaper det anpassade namnområdesprefixet till ns2 i motsats till det namnområdesprefix som har konfigurerats (NPR-32748).

* Lazy-inläsning aktiveras inte och endast 100 resurser visas när du väljer att granska uppgifter från meddelandeinkorgen (NPR-32750).

* `NullPointerException` observeras på grund av att nodinställningar saknas i den nyligen skapade användarprofilen (SAML/SSO). Detta fel förhindrar att nyinloggade användare använder [!DNL Adobe Experience Manager Stock] integrering (NPR-32777).

* Traversal-varningar observeras i loggar när en smart samling som innehåller mer än 10 000 resurser öppnas (NPR-32980).

* Resursnamn ändras till gemener när resurser flyttas från en mapp till en annan i [!DNL Adobe Experience Manager] som arbetar med Dynamic Media Scene7 runmode (NPR-32995).

* Det går inte att ta bort en sökresurs efter att ha navigerat till dess egenskaper från sökresultaten och sedan gå tillbaka till sökresultaten för att ta bort den (NPR-32998).

* [!UICONTROL Next] alternativet är inaktiverat när målmapp väljs i [!UICONTROL Move Assets] gränssnitt (NPR-33356).

* [!UICONTROL Next] är inte aktiverat när du väljer överordnad nod (där en underordnad mapp är synlig) och sedan väljer underordnad mapp (NPR-33275).

* Inchecknings- och utcheckningsbehörigheter är inaktiverade på Adobe Asset Link (AAL) för användare med borttagningsbehörighet, även om andra behörigheter som läsning, skapande eller ändring beviljas (NPR-33272).

* Smart Crop-renderingar är inte tillgängliga i dialogrutan för hämtning av resurser (NPR-33167).

* Undantag observeras i loggar vid öppning av renderingsspår för en PDF under en mapp med en smart beskärningsprofil (CQ-4294201).

* Bildförinställningar publiceras inte om [!UICONTROL Dynamic Media sync mode] är inaktiverat som standard på Experience Manager med Dynamic Media Scene7 runmode (CQ-4294200).

* Resursbearbetning när massöverföring fastnar och arbetsflödesinstansen visar fasta instanser av DAM-uppdateringsresurs (CQ-4293916).

* Det går att skapa en Dynamic Media-konfiguration i Experience Manager, men i användargränssnittet händer inget när du väljer Spara (CQ-4292442).

* Förhandsgranskning av F4V-videomaterial fungerar inte i progressiv uppspelning i Safari/Mac (CQ-4289844).

* En extra mapp skapas vid smart beskärning av en resurs som finns i en överordnad mapp med en punkt `.` i namnet (CQ-4289337).

* Miniatyrbilden är trasig och videobearbetningsbanderollen visas inte när en video kopieras (CQ-4284125).

* Dimensionella visningsprogram visar felaktigt tomma miniatyrbilder i Firefox för vissa modeller med tomma kameravinklar (CQ-4283447).

* Prestandaproblem som åtgärdas i 6.5.5.0 är (CQ-4279206):

   * Det tar för lång tid att överföra stora binära filer till Dynamic Media bildbehandlingsservrar.

   * Genereringstiden för miniatyrbilder på Experience Manager ökar på grund av Dynamic Media Scene7-arkitekturen.

* Migreringsproblem med Dynamic Media Scene7 misslyckas för kunder med ett stort antal mediefiler (CQ-4279206).

* Layouten för visningsprogrammet för video 360 fungerar inte om `setVideo` används, och videon ändras till `video= modifier` (CQ-4263201).

* Ett felmeddelande visas när Experience Manager SDL-paketet (NPR-33175) installeras.

* SSRF-sårbarhet i Experience Manager (NPR-33435).

### Plattform {#platform-6550}

* The [!DNL Sling] filtret anropas inte om `sling:match` kartpost skapas under `/etc/maps` (NPR-33362).
* Experience Manager kraschar på grund av segmenteringsfel med [!DNL Apache Lucene] (NPR-32988).
* [!DNL Jackson] kärnpaket saknas i filen Experience Manager uberjar (NPR-32848).
* CRXDE Lite läser inte in innehåll för användare utan läsbehörighet för `jcr:primaryType` för en nod (NPR-32611).
* [!DNL Granite] Schemaläggaren för underhållsaktiviteter initieras om för ofta under distributioner av Experience Manager (CQ-4294627).
* När en SQL-fråga körs länge, till exempel 7 timmar, slutar Experience Manager svara (NPR-33044).

### Användargränssnitt {#ui-6550}

* Alternativknappsmarkeringen finns inte kvar i ett multifält (NPR-33309).
* Lazy-inläsningsgränsen fungerar inte för listvyn (NPR-33124).
* Sidan med omsökningsresultat visar inget meddelande om det inte finns några matchningar (NPR-32974).
* Omsökningsfiltret returnerar alla matchningar under `/content` noden ignorerar den valda platsen (NPR-32849).

### Integreringar {#integrations-6550}

* Intern cache rensas när en sida med en Adobe Target-komponent publiceras (NPR-33162).
* Integrering med Adobe Target fungerar inte på [!DNL Windows Internet Explorer] 11 (NPR-33111).
* När du konfigurerar Adobe Target [!UICONTROL Company] och [!UICONTROL Report Suite] fält visas inte när du väljer en rapportkälla (NPR-32502).
* Vid export [!DNL Experience Fragments] använda [!DNL Adobe I/O], exporteras inte metadata som Source Product till Adobe Target (NPR-32159).
* Auktoriserade IMS-användare i den lokala Experience Manager-administratörsgruppen kan inte skapa eller ändra IMS-konfigurationer (NPR-33045).
* Konfigurationssidan för Adobe Launch visar inte alla poster (NPR-33011).
* Användare i gruppen content-authors kan inte redigera egenskaper för en Adobe Target-komponent på grund av ett JavaScript-fel (NPR-32996).
* Serveröverskridande skriptning för JSON (NPR-32744).

### Översättningsprojekt {#translation-6550}

* Översatta taggar importeras inte till Experience Manager från översättningstjänster från tredje part (NPR-33154).
* Översättningskonfigurationssidan visar en felaktig översättningsprovider än den som används för översättningen (NPR-32971).
* Om du lägger till en upplevelsefragmentmapp i ett befintligt översättningsprojekt skapas ett nytt projekt (NPR-32843).
* A `NullPointerException` fel visas i loggarna när ett översättningsjobb körs (NPR-32628).

### WCM {#wcm-6550}

* Page Editor - [!DNL Sites] Page Editor tillåter inte att användare med endast tangentbord hoppar över huvudinnehållet i stället för att växla tabbfokus mellan alla alternativ som är tillgängliga i sidhuvudet (CQ-4293883).
* Sidredigeraren - paneler som använder Well-komponenten och inkluderar sparade data visas inte på grund av uppdateringar i [!DNL Chrome] och [!DNL Firefox] versioner (CQ-4292995).
* MSM - Om du tar bort en komponent från sidan tas inte komponenten bort från den publicerade versionen av sidan (CQ-4292360).

### [!DNL Brand Portal] {#assets-brand-portal-6550}

* Ta bort ett publicerat metadataschema från [!DNL Brand Portal] resulterar i ett fel (CQ-4292063).
* Om en administratör konfigurerar [!DNL Experience Manager Assets] 6.5.4 med Brand Portal via Adobe Developer Console, [!DNL Brand Portal] användaren inte kan publicera en resurs i en bidragsmapp från [!DNL Brand Portal] till [!DNL Experience Manager] (NPR-33046).
* Duplicerad replikering av de överordnade mapparna som orsakar konflikter (NPR-33001).

### [!DNL Communities] {#communities-6550}

* Det går inte att ta bort ett kort i en moderationskonsol med hjälp av snabbredigeringsmenyalternativet (NPR-33117).
* Ett fel inträffar vid åtkomst av [!UICONTROL Activity Stream] sidan (NPR-33146).
* Grupper som tas bort från författarinstansen tas inte bort från alla publiceringsinstanser (NPR-33199).
* Författare som har skapat en ny grupp omdirigeras inte till [!UICONTROL Community Group] avsnitt på [!DNL Internet Explorer] 11 (NPR-33205).
* Om du öppnar ett meddelande i Inkorgen i Experience Manager ändras inte meddelandets status till Läs (NPR-32764).
* Redigera en [!DNL Communities] gruppen och ändringen av miniatyrbilden uppdaterar inte gruppens miniatyrbild (NPR-32599).
* En användare kan inte skicka ett e-postmeddelande till en annan användare i en community (NPR-32598).
* En skickad blogg visas inte förrän användaren uppdaterar sidan (NPR-32391).
* När du skapar en version av meddelanden och prenumerationer på användargenererat innehåll (UGC) lagras ett felaktigt ID för källsidan (CQ-4279355, CQ-4289703).
* Serveröverskridande skriptproblem (NPR-33203).

### Arbetsflöde {#workflow-6550}

* The [!UICONTROL Timeline] i den vänstra listen tar längre tid att ladda än väntat (NPR-32851).
* När du har startat om en Experience Manager-instans innehåller e-postmeddelandet för granskningsaktiviteten för en samling en felaktig nyttolastlänk (NPR-32774).

### [!DNL Forms] {#forms-6550}

>[!NOTE]
>
>Experience Manager Service Pack innehåller inga korrigeringar för [!DNL Forms]. De levereras med ett separat Forms-tilläggspaket. Dessutom släpps ett kumulativt installationsprogram med korrigeringar för AEM Forms på JEE. Mer information finns i [Installera Experience Manager Forms-tillägg](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) och [Installera Experience Manager Forms i JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

* Korrespondenshantering: Ordningen på tillgångarna i ett målområde blandas efter att en skrivelse har lämnats in (NPR-33359, NPR-33153).
* Adaptiv Forms: När en användare redigerar ett anpassat formulär [!UICONTROL Start Workflow] finns i [!UICONTROL Page Information] fungerar inte (NPR-33004).
* Adaptiv Forms: Användaren kan inte spara ett anpassat formulär med mer än en bifogad fil (NPR-32997).
* Adaptiv Forms: Om du ändrar panellayouten i ett adaptivt formulär uppstår ett fel (CQ-4293880).
* Adaptiv Forms: En ny rad i en sträng i en ordlista för anpassade formulär läggs till `&#xa;` till ordlistan (NPR-33266).
* Adaptiv tillgänglighet för Forms: När en användare förhandsgranskar ett adaptivt formulär som ett HTML-formulär visas [!UICONTROL Scribble Signature] kan inte behålla tabbfokus (NPR-33159).
* Adaptiv tillgänglighet för Forms: Felmeddelandena som visas när ett anpassat formulär skickas länkar inte till ett `aria-describedBy` attribute (NPR-33071).
* Adaptiv tillgänglighet för Forms: Fält som markerats som obligatoriska i en adaptiv form har inte det obligatoriska attributet inställt på True i ARIA-hjälpmedelsschemat (NPR-33070).
* PDFG-tjänst: När en användare konverterar en textfil till PDF återges inte japanska tecken korrekt (NPR-33238).
* PDFG-tjänst: `CreatePDF` åtgärden kan inte konvertera en PDF-fil till PDF OCR-format (NPR-32994).
* PDFG-tjänst: PDF-konverteringen misslyckas för den 200:e instansen av en [!DNL OpenOffice] dokument (NPR-32766).
* BackendIntegration: Begäranden från formulärdatamodellen misslyckas eftersom uppdateringstoken förfaller på grund av ett inaktivt tillstånd (NPR-33169).
* Designer: Skärmläsare kör tabbordningen baserat på den geografiska standardordningen i stället för den anpassade tabbordningen som definieras i XDP-filen (NPR-32160).
* Designer: Om taggningsalternativet är aktiverat försvinner delformulärens kantlinje i utdata från PDF (NPR-32778).
* Lagrade XSS med GuideSOMProviderServlet (NPR-32700).

## Adobe Experience Manager 6.5.4.0 {#experience-manager-6540}

Adobe Experience Manager 6.5.4.0 är en viktig uppdatering som innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat och prestanda, stabilitet, säkerhetsförbättringar som släppts sedan den allmänna tillgängligheten av version 6.5 i **April 2019**. Den kan installeras ovanpå Adobe Experience Manager 6.5.

Några viktiga funktioner och förbättringar i Adobe Experience Manager 6.5.4.0:

* Adobe Experience Manager Assets har nu konfigurerats med Brand Portal via [!DNL Adobe I/O] Konsol.

* En ny [Generera utdata för utskrift](../forms/using/aem-forms-workflow-step-reference.md) finns nu för Adobe Experience Manager Forms arbetsflöden.

* [Stöd för flera kolumner](../forms/using/resize-using-layout-mode.md) för layoutläge för adaptiva formulär och interaktiv kommunikation.

* Stöd för [RTF](../forms/using/designing-form-template.md) i HTML5-formulär.

* [Förbättrad tillgänglighet](new-features-latest-service-pack.md#accessibility-enhancements) i Experience Manager Assets.

* Den inbyggda databasen (Apache Jackrabbit Oak) uppdateras till version 1.10.8.

* Nu kan du synkronisera delträd med selektivt innehåll till *Dynamic Media - Scene7-läge* istället för alla tillgängliga på `content/dam`.

* Integrering av formulärdatamodell med SOAP-webbtjänst har nu stöd för urvalsgrupper eller attribut för element.

* SOAP-indata eller -utdata och komplexa datastrukturer har nu stöd för dynamisk gruppersättning.

En fullständig lista över funktioner och viktiga högdagrar som introducerats i de senaste Service Packs finns på [Nyheter i Adobe Experience Manager 6.5 Service Pack](new-features-latest-service-pack.md).

### Sites {#sites-fixes}

* När en URL för en Adobe Experience Manager Sites-sida innehåller ett kolon (`:`) eller procentsymbol (`%`) slutar webbläsaren att svara och CPU-användningstoppar (NPR-32369, NPR-31918).

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

* Experience Manager Assets-användargränssnitt visar trunkerade filnamn när resurser med fler än 50 tecken i filnamnet överförs (NPR-32054).

* Alla kryssrutor på panelen Filter avmarkeras när den första och den andra kryssrutan avmarkeras när du har markerat två kryssrutor i kryssruteträdet i Adobe Stock (NPR-31919).

* Filer- och mappsökning med Omnisearch-ansikten ger undantag (NPR-31872).

* Fältmarkering för obligatoriskt fältval i metadataredigeraren tas inte bort även efter att det obligatoriska fältet har markerats, när beroendereglerna har angetts i motsvarande metadatamatchformulär (NPR-31834).

* Fullständiga namn på taggar på lövnivå (från tagghierarkin) visas inte på egenskapssidan för resurser (NPR-31820).

* Om du använder kommandot back från objektets egenskapssida i webbläsaren Safari uppstår ett fel (NPR-31753).

* Touch UI-sökning (utförd via Omnissearch)-resultatsidan rullar automatiskt upp och förlorar användarens rullningsposition (NPR-31307).

* Assets detail page of PDF assets does not show action buttons except To Collection and Add Rendition buttons in Experience Manager running on Dynamic Media Scene7 run mode (CQ-4286705).

* Resurserna tar för lång tid att bearbeta genom batchöverföringen i Scene7 (CQ-4286445).

* Knappen Spara importerar inte fjärruppsättningen när användaren inte har gjort några ändringar i uppsättningsredigeraren i Dynamic Media Client (CQ-4285690).

* Miniatyrbilden av 3D-resursen är inte informativ när en 3D-modell som stöds har importerats till Experience Manager (CQ-4283701).

* Den obearbetade statusen för visningsförinställningen för smart beskärning visas två gånger på banderolltexten bredvid förinställningsnamnet (CQ-4283517).

* Felaktig behållarhöjd för en överförd 3D-modell som förhandsvisats i 3D-visningsprogrammet visas på objektets informationssida (CQ-4283309).

* Carousel Editor öppnas inte i IE 11 i Experience Manager Dynamic Media Hybrid-läge (CQ-425590). **För kunder i Adobe Dynamic Media - hybridläge:** Adobe upphör med stödet för Internet Explorer 11 i Dynamic Media - hybridläge, efter maj 2022.

* Tangentbordsfokus fastnar i den nedrullningsbara menyn E-post i hämtningsdialogrutan i webbläsarna Chrome och Safari (NPR-32067).

* Kryssrutan Synkronisera allt innehåll är inte aktiverad som standard när du försöker lägga till DM-molnkonfiguration på Experience Manager (CQ-4288533).

### Foundation UI {#foundation-ui-6540}

* Muskontrollen flyttas till föregående filterfält i stället för att finnas kvar i det befintliga filterfältet när resurser söks med hjälp av filterpanelen (NPR-32538).

* Plattformstaggning: Sök efter taggar genom att skriva i taggfälten visas taggar utanför rotgränserna och uppfyller inte `rootPath` egenskap för taggfält (NPR-31895).

* Plattformsgränssnitt: Webbläsaren för sökvägen bryts om en ogiltig sökväg läggs till i textfältet (NPR-31884).

* Meddelande döljs bakom en klistermeny vid sidval (NPR-31628).

### Plattform {#platform-sling-6540}

* (HTL) Understrykningar ersätter kolon i sökvägsavsnittet i URL (NPR-32231).

### Projekt {#projects-6540}

* Knappen Skapa är inte synlig för användaren även om användaren har behörighet att skapa projekt i undermappen (NPR-31832).

### Projektöversättning {#projects-translation-6540}

* När ett översättningsprojekt skapas bryts gränssnittet när alternativet Trimma mellanslag aktiveras i `Apache Sling JSP Script Handler` (NPR-32154).

* Fel i användargränssnitt och Null-punktsundantag i felloggar observeras när en tagg, som ska översättas, läggs till i ett översättningsprojekt (NPR-31896).

### Integreringar {#integrations-6540}

* Generering av biblioteks-URL baseras endast på `path` och `library_name` värden från Launch-API:t, som inte baseras på `library_path` värde (NPR-31550).

* Ett felmeddelande visas när LiveFyre-relaterade objekt bearbetas (FYR-12420).

* ReportSuitesServlet är sårbart för SSRF (NPR-32156).

### WCM-mallredigerare {#wcm-template-editor-6540}

* I redigerbart mallstrukturläge visas inte länkknappskomponenten i listan över tillåtna komponenter i layoutbehållaren (CQ-4282099).

### WCM Page Editor {#wcm-page-editor-6540}

* Det uppstod ett fel när en övertäckning skulle markeras och därefter när responsiva rutnätskomponenter skulle markeras här (CQ-4283342).

### Kampanjanpassning {#campaign-targeting-6540}

* Målmolnkonfigurationen misslyckades med felet när mbox-begäran skulle hämtas (CQ-4279880).

### Brand Portal {#assets-brand-portal-6540}

* Brand Portal-användare kan inte publicera resurser i mappen för bidrag till [!DNL Assets] uppgradera till [!DNL Adobe I/O] på Experience Manager 6.5.4 (CQDOC-15655). För en omedelbar fix på Experience Manager 6.5.4 rekommenderas att [ladda ned snabbkorrigeringen](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041) och installera på din författarinstans.

* Popup-värden för metadataschemat visas inte i resursegenskaper (CQ-4283287).

* Delschemat Metadata visar inte flikar baserade på MIME-typer i resursegenskaper (CQ-4283288).

* Ett felmeddelande fylls i när metadatamatchemat avpubliceras, även om schemat tas bort vid backend.

* Förhandsvisningsbilden visas inte för en publicerad resurs (CQ-4285886).

* Användaren kan inte publicera eller avpublicera resurser som innehåller ett enkelt citattecken i namnet (CQ-4272686).

* Villkoren visas inte vid hämtning av flera resurser (CQ-4281224).

* Mindre säkerhetsluckor har åtgärdats.

### Communities {#communities-6540}

* Formuläret Skapa medlem visas som en tom sida (NPR-31997).

* Användaren kan inte visa Analytics-rapporten för författarinstansen (NPR-30913).

### Oak-indexering och frågor {#oak-indexing-6540}

* MS Word- och MS Excel-dokument som innehåller JPEG-bilder kan inte tolkas när de tolkas med Tika-tolken, och ett klassfel som inte hittas observeras (NPR-31952).

### Forms {#forms-6540}

>[!NOTE]
>
>Experience Manager Service Pack innehåller inga korrigeringar för Experience Manager Forms. De levereras med ett separat Forms-tilläggspaket. Dessutom släpps ett kumulativt installationsprogram med korrigeringar för Adobe Experience Manager Forms på JEE. Mer information finns i [Installera Experience Manager Forms-tillägg](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) och [Installera Experience Manager Forms i JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

* Korrespondenshantering: Bokstäverna visar extra tecken efter överföring för att bokföra processarbetsflöden (NPR-32626).

* Korrespondenshantering: Bokstäverna visar en nedrullningsbar platshållare som en textkomponent efter att de skickats in till arbetsflöden efter bearbetning (NPR-32539).

* Korrespondenshantering: Standardvärdena som definieras i brevmallen visas inte i förhandsvisningsläget (NPR-32511).

* Mobile Forms: Skicka-knappen visas som utökad när ett XDP-formulär återges i en HTML-version (NPR-32514).

* Dokumenttjänster: Problem med URL-åtkomst för brev och vissa andra sidor efter att Service Pack 2 har tillämpats (NPR-32508, NPR-32509).

* Dokumenttjänster: Om antalet transaktioner på en server överstiger en viss gräns misslyckas konverteringen från HTML till PDF och filtypsinställningarna tas bort från [!DNL Forms] server (NPR-32204).

* Adaptiv Forms: Verktyget Webbläsartillgänglighet rapporterar fel i adaptiva formulär enligt riktlinjerna för WCAG2 Level AA (NPR-32312, NPR-32309, CQ-4285439).

* Adaptiv Forms: Webbläsarhjälpmedelsverktyget i Chrome rapporterar ett fel med bästa praxis (NPR-32310).

* Adaptiv Forms: Översättningsproblem vid konfiguration av ett adaptivt formulär inbäddat på en Experience Manager Sites-sida (NPR-32168).

* Workbench: Ett felmeddelande visas när åtgärden Hämta PDF-egenskaper används för tjänsten PDF Utilities (NPR-32150).

* Dokumentsäkerhet: En skyddad PDF-fil kan inte öppnas offline med alternativet DisableGlobalOfflineSynchronizationData inställt på True (NPR-32078).

* Designer: Om taggningsalternativet är aktiverat försvinner delformulärsramen i utdata från PDF (NPR-32547, NPR-31983, NPR-31950).

* Designer: Om det finns sammanfogade celler i en tabell misslyckas hjälpmedelstestet för utdatafilen som konverterats från ett XDP-formulär med hjälp av utdatatjänsten (CQ-4285372).

* Foundation JEE: Om en Experience Manager Forms-server är frånkopplad från ett kluster kan cachelagring förhindra att den återansluter till servern (NPR-32412).

## Adobe Experience Manager 6.5.3.0 {#experience-manager-6530}

[!DNL Adobe Experience Manager] 6.5.3.0 är en viktig version som innehåller prestanda, stabilitet, säkerhet och viktiga kundkorrigeringar och förbättringar som släppts sedan den allmänna tillgängligheten av 6.5-versionen i **April 2019**. Den kan installeras ovanpå [!DNL Adobe Experience Manager] 6.5.

Några viktiga höjdpunkter i den här Service Pack-versionen är:

* Den inbyggda databasen (Apache Jackrabbit Oak) uppdateras till version 1.10.6.

* [!DNL Experience Manager Assets] har nu stöd för ZIP-arkiv som skapats med algoritmen Deflate64.

* Ny kolumn för skapat datum, som är sorterbar, har lagts till i DAM-listvyn och i resurssökningsresultat i listvyn.

* Resurssortering baserad på namnkolumnen har aktiverats i listvyn.

* [!DNL Dynamic Media] har nu stöd för videomaterial för Smart Crop. Smart Crop är en maskininlärningsdriven funktion som återbeskär en video medan bildrutan flyttas för att följa scenens fokuspunkt.

* [!DNL Dynamic Media] har stöd för Smart Imaging.

* Möjlighet att [ange frånvaro](../forms/using/configure-out-of-office-settings.md) inställningar i [!DNL Experience Manager] arbetsflöden.

* Möjlighet att [dela inkorgs- eller inkorgsobjekt](../forms/using/configure-shared-queues-osgi.md) med andra användare i [!DNL Experience Manager] arbetsflöden.

* Möjlighet att [generera interaktiv kommunikation i gruppläge](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

* Uppdaterad version av jQuery som paketerats i ContextHub till 3.4.1.

### Resurser {#assets-6530-enhancements}

**Produktförbättringar**

* [!DNL Experience Manager Assets] har nu stöd för ZIP-arkiv som skapats med algoritmen Deflate64 (NPR-27573).

* Ny kolumn för skapat datum, som är sorterbar, läggs till i DAM-listvyn och i resurssökningsresultat i listvyn (NPR-31312).

* I listvyn kan användarna sortera listan med resurser med [!UICONTROL Name] kolumn (NPR-31299).

* GLB-, GLTF-, OBJ- och STL-filer kan förhandsgranskas i [!UICONTROL Asset Details] sida i DAM (CQ-4282277).

* `ReplicationOnModifyListener` -händelsen utlöses för segmentnoder under segmentöverföring i [!DNL Dynamic Media] (CQ-4281279).

* [!DNL Dynamic Media] har nu stöd för videomaterial för Smart Crop. Smart Crop är en maskininlärningsdriven funktion som återbeskär en video samtidigt som bildrutan flyttas för att följa scenens fokuspunkt (CQ-4278995).

* [!DNL Dynamic Media] har stöd för Smart Imaging (CQ-422249).

* Vyn Sök eller Bläddra anges som standardvy i Foundation-väljaren om frågeparametrar skickas i begäran (NPR-31601).

**Korrigeringar**

* Metadata för vissa PDF-dokument uppdateras inte och sparas i PDF när titeln ändras (NPR-31629).

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

* Mappval Skapa > FileUpload-åtgärdsobjekt saknas när ACL för Neka `jcr:removeChildNodes` och `jcr:removeNode` på bana tillämpas för en användare (NPR-30840).

* DAM-arbetsflöden försätts i viloläge när vissa mp4-resurser överförs, vilket gör att alla återstående arbetsflöden försätts i viloläge (NPR-30662).

* Slut på minnesfel uppstår när stora PDF-filer (av flera gigabyte) överförs till DAM och dess underresurser bearbetas (NPR-30614).

* Massförflyttning av resurser misslyckas och ett varningsmeddelande visas (NPR-30610).

* Resursnamn ändras till gemener när resurser flyttas från en mapp till en annan i [!DNL Experience Manager] kör [!DNL Dynamic Media]-Scene7 mode (NPR-31630).

* Ett fel uppstod när en fjärrbilduppsättning redigerades för bilden i mappen som heter samma som Scene7 företagsnamn (NPR-31340).

* [!DNL Dynamic Media] resurser som innehåller referenser publiceras inte (NPR-31180).

* Överför från [!DNL Dynamic Media]7-Scene7-läge till [!DNL Dynamic Media Classic] tar för lång tid att slutföra (NPR-31048).

* Aktiveringspunkten som läggs till i en bildresurs är inte synlig via Interactive Image Viewer på sidan med resursinformation (NPR-30979).

* Enorma snedningsjobb skapas och Bearbetningsbanderollen visas igen när åtgärder utförs på resurser i [!DNL Experience manager Assets] skickas till Scene7 (NPR-30947).

* En konflikt uppstår när språkkopia av resurser skapas och resurser inte överförs till Scene7 (NPR-30932).

* Dynamiska återgivningar hämtade från [!DNL Experience Manager] kör [!DNL Dynamic Media]-Hybridläget är brutet (de är av texttyp med innehållet&quot;det går inte att hitta bilden&quot; i stället för bildinnehållstypen) (NPR-30876).

* [!DNL Dynamic Media] Arbetsflödet för kodning av video kan inte generera miniatyrbilder för videon som migreras från [!DNL Dynamic Media Classic] till [!DNL Dynamic Media]-Scene7-läge i Adobe Experience Manager (CQ-4282011).

* IpsApiException observerades när resurser migrerades från en instans till en annan med olika Scene7-företags-ID:n (CQ-4280548).

* Miniatyrbilden av 3D-resursen är inte informativ när en 3D-modell som stöds hämtas till [!DNL Experience Manager] (CQ-4283701).

* Rullningsknappar visas i visningsprogrammet om en 3D-resurs har få kameravinklar (CQ-4283322).

* Felaktig behållarhöjd för en överförd 3D-modell som förhandsvisats i DimensionalViewer på sidan Resursinformation (CQ-4283309).

* Videor kan inte spelas upp med SmartCropVideoViewer i Internet Explorer 11 och Safari (CQ-4281422).

* Om du använder knappen Flytta för att flytta flera resurser, från en mapp till en annan, misslyckas åtgärden i [!DNL Experience Manager] körs [!DNL Dynamic Media]-Scene7 runmode (CQ-4280384).

* Förvrängd video visas i resursinformation när MIME-typen är en annan än MP4 (CQ-4279704).

* Videoklipp som nyligen har infogats i mappar med en videoprofil är fortfarande i bearbetningstillstånd även när kodens procenttal har slutförts till 100 % (CQ-4279389).

* När du flyttar resurser från en mapp skapas ett stort antal snedstreck (Scene7 API-anrop) än vad som helst krävs (CQ-4278664).

* Namn på bilduppsättningen ändras till gemener i Scene7 när bilduppsättning (eller mediaset) skapas och namnges med lämplig namnkonvention i DAM (CQ-4281112).

* Scene7 Migrator anger felaktigt publiceringstillstånd (CQ-4263492).

* Touch UI-sökning (utförd via Omnissearch)-resultatsidan rullar automatiskt upp och förlorar användarens rullningsposition i innehållsfragment (CQ-4282898).

* PDF-filer är inte indexerade och innehåll i är inte sökbart (CQ-4278916).

* Felmeddelandet&quot;Grupp visas inte av användarväljaren: false förväntas vara lika med true&quot; visas när en stängd användargrupp med olika `principalName` och `authorizableId` (CQ-4278177).

* Resursens gränssnittskolumnvy visar alla sökvägar oavsett vilken sökväg en klientorganisation har (CQ-4278175).

* Resursväljarens sökning fungerar inte som förväntat (CQ-4275886).

* Återgivningsarbetsflöden misslyckas (CQ-4271928).

* DAM-händelse - tömning tar bort den senaste (`maxSavedActivities`) händelsedata och innehåller data som skapats tidigare (NPR-31336).

* Touch UI-sökning (utförd via Omnissearch)-resultatsidan rullar automatiskt upp och förlorar användarens rullningsposition (NPR-31307).

* Åtgärdsfältet och antalet resurser uppdateras inte när du markerar alla och sedan avmarkerar vissa objekt (mappar/enskilda resurser) i Touch UI (NPR-3118).

* Ett undantag visas i [!DNL Experience Manager] vid avsökning efter jobbdetaljer för en resurs (CQ-4283569).

### Webbplatser

* Om LiveCopy-arvet bryts visas länkar för språkkopiering i stället för länkar för LiveCopy (NPR-30980).
* Om antalet poster är fler än 40 visas bara de första 40 posterna för en ny utkast. I utkast visas tomma rader för resten av posterna (NPR-31182).
* När en användare lägger till japanska eller koreanska tecken i egenskapen description på en meny visas förvrängda tecken för japansk och koreansk text på menyn (NPR-31331).
* Det går inte att infoga en inbäddad tabell som listobjekt (NPR-30879) i RTF-redigeraren.
* När du har gjort en avskalning av RTF-redigerare (Rich Text Editor). använder textbunden teckensnittsstorlek för element, oväntat (NPR-31284).
* När en användare fokuserar på fält med vänster stödlinje och använder ett kortkommando för att klistra in innehåll, klistras innehållet i sidredigerarens urklipp in i stället för innehållet som kopieras från de vänstra fältspåren (NPR-31172).
* När en användare lägger till ett filöverföringsfält i ett flerfält lagras bildsökvägen i komponentnoden i stället för i flerfältsnoden (NPR-30882).
* The `ResponsiveGridExporter` API returnerar inte `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` gränssnitt. The `com.day.cq.wcm.foundation.model.impl` paketet deklareras som ett privat paket (NPR-31398).

<!-- Review: NPR-31398 has fixVersion as 6530. However, it is mentioned twice in 6530 and 6520 as fixed. 
Remove one mention of this fix.
-->

* När en sida som innehåller vissa Experience Fragments öppnas i icke-redigeringsläge (antingen i redigeringsläget utan `editor.html` prefix och `wcmmode=disabled`, eller i Publisher). avslutas begäran med HTTP-statusfelkod `500` (NPR-30743).
* Användare kan inte ändra sitt lösenord och komma åt sin profilsida (NPR-31161).

### Sök- och användargränssnitt {#ui-interface-and-search}

* När du växlar från kortvyn till listvyn på en sökresultatsida uppstår en fördröjning innan sidan kan rullas (NPR-31286).

* The [!UICONTROL Select All] kryssrutan är dold i listvyn på [!DNL Sites] användargränssnitt (NPR-31614).

* The [!UICONTROL Select All] räknaren för en sökresultatsida är felaktig (NPR-31120).

* I metadataredigeraren visas taggar som inte finns (NPR-31119).

### Översättning {#translation}

* Två popup-fönster visas när du väljer alternativet Förfallodatum i ett översättningsjobb (NPR-31270).

### Plattform

* Alternativet Mime-typ i webbkonsolen fungerar inte (NPR-31108).

* Klientcertifikatet accepteras inte när enkel inloggning konfigureras (NPR-31165).

* Uppdateringar i buffertstorlekskonfigurationen för Jetty-baserad HTTP-tjänst sparas inte (NPR-30925).

* QueryBuilder har nu stöd för orderby `fn:name()` in xpath queries (NPR-31322).

* Dubblettaktiveringsträdet skapas vid uppgradering från [!DNL Experience Manager] 6.3 (NPR-31513).

* Vidarebefordrade begäranden bevarar inte svarshuvuden som ställs in vid slingautentisering (NPR-30013).

* Det går inte att söka i väljarkomponenterna (NPR-31692).

* Ett fel visas när en ZIP-fil bifogas till en [!DNL Experience Manager Communities] inlägg på grund av olika versioner av Apache POI och Apache Tika bundle (NPR-31018).

* The `org.apache.sling.distribution.api` Paketet är dolt i konfigurationshanteraren och därför inte tillgängligt för anpassade paket (NPR-31720).

### Projekt

* Det går inte att växla kalendervyer (NPR-31271).

### Brand Portal {#assets-brand-portal-6530}

**Produktförbättringar**

* Arbetsflöde för import av resurskälla i [!DNL Experience Manager Assets] har ändrats så att endast de nyskapade resurserna från hämtas [!DNL Brand Portal] till [!DNL Experience Manager]och hoppa över de resurser som redan finns i den NYA mappen för att undvika replikering (CQ-4278527).

**Korrigeringar**

* En felaktig ikon visas när en ny Contribute-mapp skapas i funktionen Resurser (CQ-4282825).
* När du skapar en ny Contribute-mapp visas inte en eller båda undermapparna (NYTT och DELAT) i Contribute-mappen (CQ-4282424).
* Ett undantag genereras om användaren försöker publicera om Contribute-mappen från [!DNL Experience Manager] till [!DNL Brand Portal] efter att nya resurser har tagits emot i Contribute-mappen från [!DNL Brand Portal] end (CQ-4279740).
* Det är inte tillåtet att skapa en Contribute-mapp i en Contribute-mapp (kapslad mapp) för att undvika komplexitet (CQ-4278391).
* Ett undantag genereras när systemet överför [!DNL Brand Portal] användarlista (.csv-fil) importerad från [!DNL Experience Manager] Admin Console. Endast fälten Email, FirstName och LastName i CSV-filen är obligatoriska (CQ-4278390).

### Communities {#communities-6530}

**Korrigeringar**

* Snabblänkar för att hantera grupper (Öppna/Redigera/Publicera/Ta bort grupper) är inte synliga för communityadministratörer (Gruppadministratör/Webbplatsadministratör) (NPR-31627).
* En inskickad blogg visas bara om sidan uppdateras/läses in manuellt (NPR-31599).
* JCR-frågan som används av funktionen &quot;Mentions&quot; är skiftlägeskänslig och tar för lång tid att returnera resultaten (NPR-31475).
* [!DNL Experience Manager] 6.5 Filen UberJar genererar ett undantag, `cq-social-translation` paket saknas från [!DNL Experience Manager] 6.5 filen UberJar (NPR-31186).
* Jackson Database-bibliotek uppdaterade till version 2.9.9.3 för att åtgärda nya säkerhetsluckor (NPR-30967).
* Aktiviteter och meddelandetitlar är inkonsekventa (NPR-30941).
* Sidindelningen fungerar inte korrekt i [!DNL Communities] Bloggar (NPR-30914).
* Analysrapporter fylls inte i i [!DNL Experience Manager] författarmiljö, tom sida visas (NPR-30913).

### Oak {#oak}

* Uppdateringar av Lucene-index gör att författarservern sinkas (NPR-31548).

### Forms {#forms-6530}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack innehåller inte korrigeringar för [!DNL Experience Manager Forms]. De levereras med ett separat Forms-tilläggspaket. Dessutom släpps ett kumulativt installationsprogram med korrigeringar för [!DNL Experience Manager Forms] på JEE. Mer information finns i [Installera Experience Manager Forms-tillägg](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) och [Installera Experience Manager Forms i JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

#### Forms tilläggspaket {#forms-add-on-package-6530}

**Adaptiv Forms**

* Strängar innehåller ordlistenyckeln när adaptiva former lokaliseras (NPR-31110).

**Interaktiv kommunikation**

* **MissingNode.toString()** returnerar felaktiga resultat efter uppgradering av Jackson-bibliotek till 2.10.0 (NPR-31549).

* Textredigeraren tar slumpmässigt bort blankstegstecken från text som kopieras från Microsoft Word (NPR-31113).

**Korrespondenshantering**

* Bildtexter och verktygstips visas inte när bokstäver migreras från LiveCycle ES4SP1 till [!DNL Experience Manager] 6.5 (NPR-31615).

* **Textflödesformatering stöds inte längre** felmeddelandet visas när bokstäver sparas som utkast (NPR-30463).

**Arbetsflöde**

* OSGi-arbetsflödet misslyckas på grund av 100 % processoranvändning (NPR-31233).

**HTML5 Forms**

* När du genererar HTML5-förhandsgranskning av ett XDP-formulär visas ett flimmer medan instanser av ett delformulär läggs till (NPR-30909).

#### Forms på JEE-installationsprogram {#forms-jee-installer-6530}

**Forms - dokumenttjänster**

* SOAP-webbtjänst som använder MTOM i ett .NET-projekt visar undantag för AssemblerServiceClient-anrop och HTMLToPDF2-metoder (NPR-4281771).

* Säkerhetsluckan 2012-5784 och 2014-3596 hittades med AXIS 1.4 jar och korrigeringen medföljer [AXIS1.4.1 jar](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0014.html) (NPR-31015).

**Foundation JEE**

* Åtgärdskonfigurationen läser inte in processnamnen för åtgärden Anropa en Forms Workflow skicka (NPR-31478).

### Funktionspaket ingår {#feature-packs-included-6530}

>[!NOTE]
>
>För [!DNL Experience Manager Forms] -kunder, det är viktigt att installera [!DNL Experience Manager Forms] tilläggspaket efter installation av [!DNL Experience Manager] Service Pack, Cumulative Fix Pack eller Feature Pack.

#### Forms - Foundation JEE {#forms-foundation-jee-feature}

* [!DNL Experience Manager] Forms-stöd för Oracle 18c (NPR-29155).

## Adobe Experience Manager 6.5.2.0 {#experience-manager-6520}

[!DNL Adobe Experience Manager] 6.5.2.0 är en viktig version som innehåller prestanda, stabilitet, säkerhet samt viktiga korrigeringar och förbättringar som gjorts sedan den allmänna tillgängligheten för [!DNL Adobe Experience Manager] 6,5 tum **April 2019**. Den kan installeras ovanpå [!DNL Experience Manager] 6.5.

Några viktiga höjdpunkter i den här Service Pack-versionen är:

* Den inbyggda databasen (Apache Jackrabbit Oak) uppdateras till version 1.10.3.
* En konfigurationsegenskap som tillåter export av Experience Fragments direkt till användardefinierade arbetsytor för [!DNL Adobe Target].
* Resurser som användare kan söka efter visuellt liknande bilder. [!DNL Experience Manager] visar smarta taggade bilder från DAM-databasen som liknar den användarvalda bilden. Se [visuell sökning](../assets/search-assets.md#visualsearch).

* Förbättrade funktionerna för anslutna resurser för att lägga till stöd för att hämta dokument från DAM-fjärrdistributioner. Webbplatsförfattare kan nu söka efter och filtrera dokumenttyper som stöds i Content Finder. Fjärrdokumenten kan läggas till i komponenten Download på webbsidor. Se [använda anslutna resurser](../assets/use-assets-across-connected-assets-instances.md).

* Förbättra dokumenttypsfilter med fler MIME-typer som stöder flervärdesalternativ.
* Ett externt arbetsflöde för ombearbetning har introducerats för stöd för flera resurser.
* Optimerad [!DNL Dynamic Media] prestanda genom att använda standardresursfilter för replikering.
* Återställt redigeringsalternativ för beskärning/rotering av resurser för DMS7.
* Implementerade ett alternativ för att stänga av ljudet för en video vid inläsning i VideoPlayer.
* Åtgärda problemet så att kolumnvyn i resursanvändargränssnittet bara visar innehåll som är specifikt för innehavaren.
* Korrigera så att formatdragspelsändringar återspeglas i sökresultaten.

### Resurser

**Produktförbättringar**

* Förbättrade funktionerna för anslutna resurser för att lägga till stöd för att hämta dokument från DAM-fjärrdistributioner. Webbplatsförfattare kan nu söka efter och filtrera dokumenttyper som stöds i Content Finder. Fjärrdokumenten kan läggas till i komponenten Download på webbsidor. Programfix för CQ-4270245. Se [använda anslutna resurser](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Experience Manager Assets] -användare kan söka visuellt liknande bilder. [!DNL Experience Manager] visar smarta taggade bilder från DAM-databasen som liknar den användarvalda bilden. Se [visuell sökning](../assets/search-assets.md#visualsearch).

**Korrigeringar**

* Resurssökvägar i URL:er och mappmetadata som genereras av AVS-API:t är inte URL-kodade. GRANITE-26198: Programfix för CQ-4271814
* Det går inte att öppna ett arkiv med ett procenttecken (%) i namnet med hjälp av [!DNL Experience Manager Assets] gränssnitt. NPR-29989: Programfix för CQ-4270467
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
* Funktionen Dela länk fungerar inte på [!DNL Experience Manager] -instans med DMS7-konfiguration. NPR-30080, NPR-30492: Programfix för CQ-4273651
* Lägga till [!DNL Dynamic Media]-Scene7-komponenten till sidan och sedan publicera sidan utlöser inte dmscene7-konfigurationen varje gång. NPR-30641: Programfix för CQ-4275962
* En IPSJobJournal har lagts till i [!DNL Experience Manager] för att skapa endast ett IPS-jobb (Intrusion Prevention Systems) per bearbetningsprofil. NPR-30490: Programfix för CQ-4273614
* [!DNL Dynamic Media]: Lagt till standardfilter för att exkludera resurser från att replikeras till [!DNL Experience Manager] publiceringsnod. NPR-30538: Programfix för CQ-4274678
* Ett externt arbetsflöde för ombearbetning har introducerats för stöd för flera resurser så att mappen kan användas som nyttolast. Arbetsflödet består av två steg: ombearbetar resurser utan handtag via metadatamappning till nästa steg och överför alla resurser utan resurshandtag till S7 i ett enda IPS-jobb. Mer information finns i Konfigurera [!DNL Dynamic Media] Cloud Services. NPR-30489: Programfix för CQ-4272903
* När du laddar upp en felaktig CSV-fil efter att du korrigerat CSV-filen raderas den korrekta CSV-filen. Programfix för CQ-4277694, CQ-4277814
* Den felaktiga ikonen som är specifik för de bidragsmappar som ska tas bort. Programfix för CQ-4277580
* När du väljer en användare i användarväljaren på fliken Resursbidrag visas inte användarens namn i tabellen och dialogrutan Ta bort användare på egenskapssidan visar fel text. Programfix för CQ-4277875
* Medarbetare kan inte läggas till i resursavgiftsmappen från användarväljaren genom att markera användare och klicka på Lägg till. Programfix för CQ-4277824, CQ-4278087
* Det går inte att söka efter användarnamn med gemener i användarväljaren. Programfix för CQ-4277958, CQ-4277930
* Icke-administratörer kan publicera resurser i en ny mapp i en resursavgiftsmapp. Programfix för CQ-4278200
* dam-user (icke-admin) har inte möjlighet att lägga till medarbetare i resursavgiftsmappen. Programfix för CQ-4278192
* Knappen&quot;Skapa&quot; visas i mappen Resursbidrag. Programfix för CQ-4277560
* Sortera sökfrågan efter relevansreturer [!DNL InDesign] dokument tillsammans med [!DNL InDesign] -mallar. Programfix för CQ-4273864
* Om användaren har ett e-post-ID med versaler kan användarna inte checka in de resurser som tidigare har checkats ut. Programfix för CQ-4276575
* Åtgärden Ta bort gäller bara för de förinställningar som är markerade, och om skärmen automatiskt uppdaterar listan efter åtgärden visas andra förinställningar som redan har uppdaterats. Programfix för CQ-4261461
* Konfigurerar [!DNL Dynamic Media] Cloud Services i [!DNL Dynamic Media]-Hybrid-läget resulterar i flera tomma rapportsviter skapade i [!DNL Analytics]och utan något rapportpaket-ID som lagras i [!DNL Experience Manager], vilket resulterar i dubbletter av rapportsviten. Programfix för CQ-4249780
* Byt namn på åtgärd i [!DNL Experience Manager] resurs till duplicerat namn kan inte synkroniseras med Scene7. Programfix för CQ-4276763
* Användargenererat innehåll visas felaktigt på sökfilterpanelen. Programfix för CQ-4273875
* Alternativet Sök efter liknande är inte tillgängligt för bilder i TIFF. Programfix för CQ-4278238
* Implementerat alternativ för att stänga av video vid inläsning i VideoPlayer. Programfix för CQ-4266465
* Visare - VideoViewer: affisch=none fungerar inte korrekt om en extern video används. Programfix för CQ-4265536
* Vänteikonen visas när videon spelas upp i IE11- och MS Edge-webbläsare. Programfix för CQ-4251539
* 3.8 SDK- och 5.13-visningsprogram - README-filer uppdateras inte och innehåller information från tidigare versioner. Programfix för CQ-4273737
* Innehållsfragment får versionsnummer även innan ändringarna sparas. NPR-30616: Programfix för CQ-4273088
* Ersätt Asset#getMetadata(String) med Asset#getMetadataValueFromJcr(String) i en miniatyrprocess. NPR-30491: Programfix för CQ-4273067
* Om du överför jpg uppstår flera instanser av meddelandet: &quot;ReplicateOnModifyWorker Replicating UPDATED&quot; för varje resurs, vilket ger sämre prestanda.
* Uppackning av zip-arkiv med funktionen Extrahera arkiv orsakar problem med mappar vars namn innehåller procent (%) i titeln. NPR-29990: Programfix för CQ-4270467

### Webbplatser {#sites-6520}

* Om LiveCopy-arvet bryts visas länkar för språkkopiering i stället för länkar för LiveCopy (NPR-30980).
* Om antalet poster är fler än 40 visas endast de första 40 posterna för en ny utkast. I utkast visas tomma rader för resten av posterna (NPR-31182).
* Plugin-programmet RTE (Rich Text Editor) för textkomponenten visar förvrängda tecken för japansk och koreansk text (NPR-31331).
* Det går inte att infoga en inbäddad tabell som listobjekt (NPR-30879) i RTF-redigeraren.
* Vid skalning av RTF-redigerare (Rich Text Editor) används teckensnittsstorleken för element, oväntat (NPR-31284).
* När en användare fokuserar på fält med vänster stödlinje och använder kortkommando för att klistra in innehåll, klistras innehållet i sidredigerarens urklipp in i stället för innehållet som kopieras från fält med vänster stödlinje (NPR-31172).
* När en användare lägger till ett filöverföringsfält i ett flerfält lagras bildsökvägen i komponentnoden i stället för i flerfältsnoden (NPR-30882).
* The `ResponsiveGridExporter` API returnerar inte `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` gränssnitt. The `com.day.cq.wcm.foundation.model.impl` paketet deklareras som ett privat paket (NPR-31398).
* När en sida som innehåller vissa Experience Fragments öppnas i icke-redigeringsläge (antingen i redigeringsläget utan `editor.html` prefix och `wcmmode=disabled`, eller i Publisher), avslutas begäran med HTTP-statusfelkod 500 (NPR-30743).

### WCM - sidredigeraren {#wcm-page-editor-6520}

**Produktförbättringar**

* `EnhanceDocument` typfilter med fler MIME-typer som stöder flervärdesalternativ. Programfix för CQ-4270694

### Hantering av innehållsfragment {#content-fragment-management-6520}

* Frågan som används av gränssnittet för modeller för innehållsfragment är mycket långsam och resulterar till slut i ett fel. Programfix för CQ-4270807

### UI - Foundation {#ui-foundation}

* Kortkommandon som utlöser ett fel som gör att användaren inte kan använda &#39;m,&#39; &#39;p,&#39; &#39;e&#39; i ett visst användargränssnitt. NPR-30355: Programfix för GRANITE-26346
* Stänger [!DNL Experience Manager Assets] Sökgränssnittet återställer inte den vänstra listen till Innehållsval, vilket förhindrar användaren från att öppna filterfältet andra gången. NPR-30509: Programfix för CQ-4274716
* Flerklientmiljö: [!DNL Experience Manager Assets] Gränssnittets övre navigering är inte tillgänglig och orsakar JavaScript-fel. NPR-30104: Programfix för GRANITE-26344

### Översättning {#translation-6520}

* Översättningsproblem - Endast ett fåtal komponenter översätts med maskinöversättning. NPR-30079: Programfix för CQ-4273764

### Plattform {#platform-6520}

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
>[!DNL Experience Manager] Service Pack innehåller inte korrigeringar för [!DNL Experience Manager Forms]. De levereras med en separat [!DNL Forms] tilläggspaket. Dessutom släpps ett kumulativt installationsprogram med korrigeringar för [!DNL Experience Manager Forms] på JEE. Mer information finns i [Installera Experience Manager Forms-tillägg](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) och [Installera Experience Manager Forms i JEE](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer).

De viktigaste nyheterna för [!DNL Experience Manager] 6.5.2.0-blanketter:

* Inställningen Auto har lagts till i `RenderAtClient` in `PDFFormRenderOptions` API för [!DNL Experience Manager] Forms OSGi.

#### Forms tilläggspaket

**Integrering med back end**

* Det går inte att konfigurera formulärdatamodellen med en AWS-värdbaserad belastningsutjämnad URL. NPR-30123: Programfix för CQ-4273359
* Felmeddelandet visas när formulärdatamodellen (FDM) skapas med WSDL (Web Service Definition Language) `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type` returneras: NPR-30477: Programfix för CQ-4272921

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

* Om &quot;SubmitURL&quot; innehåller ett et-tecken (&amp;), visas tolkningsfel i loggen när en POST begär det `renderpdf` servlet. NPR-30865: Programfix för CQ-4278232

**Forms - Foundation JEE**

* HTMLtoPDF-tjänsten visar inte maxReuseCount i JMX-konsolen. NPR-30134, NPR-30304: Programfix för CQ-4273763
* Lägga till eller redigera en webbtjänstanslutning genom att anropa webbtjänster från [!DNL Experience Manager Forms] Workbench genererar ett fel: ClassNotFoundException org.apache.axis.message.SOAPBodyElement. NPR-30105: Programfix för CQ-4273217

### Funktionspaket ingår

>[!NOTE]
>
>För [!DNL Experience Manager Forms] -kunder, det är viktigt att installera [!DNL Experience Manager Forms] tilläggspaket efter installation av [!DNL Experience Manager] Service Pack, Cumulative Fix Pack eller Feature Pack.

#### Webbplatser {#sites-feature-packs-included}

* En konfigurationsegenskap som tillåter export av Experience Fragments direkt till användardefinierade arbetsytor för [!DNL Adobe Target]. NPR-29189: Programfix för CQ-4249782

#### Forms - dokumenttjänster {#forms-document-services-1}

* Inställningen Auto har lagts till i `RenderAtClient` in `PDFFormRenderOptions` API för [!DNL Experience Manager Forms] OSGi. NPR-30759: Programfix för CQ-4278193

## Adobe Experience Manager 6.5.1.0 {#experience-manager-6510}

[!DNL Adobe Experience Manager] 6.5.1.0 är en viktig version som innehåller prestanda, stabilitet, säkerhet samt viktiga korrigeringar och förbättringar som gjorts sedan den allmänna tillgängligheten för [!DNL Adobe Experience Manager] 6,5 tum *April 2019.* Den kan installeras ovanpå [!DNL Experience Manager] 6.5.

Några viktiga höjdpunkter i den här Service Pack-versionen är:

* Aktiverade inkludering av dynamiskt gränssnittsläge i spårningshändelser som anpassade attribut.
* Inkluderat stöd för leverans av 360-graders videomaterial i [!DNL Dynamic Media]-Scene7.
* Aktiverad *Japansk radbrytning* via stilplugin-programmet i RTF-redigeraren. Mer information finns i [Konfigurera japansk radbrytning](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### Resurser

* DAM DMGGateway-gränssnittet för S3-multipart-stöd har uppdaterats. NPR-29740: Programfix för CQ-4226303
* Förhandsgranskning av återgivningar genererar `Only empty tenantId is currently supported` fel efter uppgradering till [!DNL Experience Manager] 6.5. NPR-29986: Programfix för CQ-4272353
* Dialogrutan Ta bort är inte synlig så att du kan ta bort jobb. NPR-29720: Programfix för CQ-4271074
* När en användare har lagt till en objekttitel på egenskapssidan och försöker stänga sidan, [!DNL Experience Manager] öppnar egenskapssidan igen. NPR-29627: Programfix för CQ-4264929
* VersioningTimelineEventProvider ska tillhandahålla rotversionen tillsammans med noden av typen nt: version. Programfix för GRANITE-26063
* Implementerade möjligheten att ladda upp och spela upp 360 sfäriska videor i [!DNL Experience Manager] DM-Scene7-läge. Programfix för CQ-4265131
* Live-kopian hämtar felaktig status om källan redigeras. Programfix för CQ-4265451
* Aktiverat stöd för Multi-Site Manager för [!DNL Experience Manager Assets]. Programfix för CQ-4271453, CQ-4268621, CQ-4257491
* [!DNL Experience Manager] gränssnittet bör visa ytterligare en post för den aktuella versionen av resursen i tidslinjehistoriken och visa den senaste incheckningskommentaren från [!DNL Adobe Asset Link]. Programfix för CQ-4262864
* Tidslinjen för innehållsfragment visar ett felmeddelande när egenskaper saknas. Programfix för CQ-4272560
* Ett problem med Scene7 videospelare när den expanderar till helskärm. Programfix för CQ-4266700
* ZoomVerticalViewer: Panoreringsknappar ska inte visas om en enda bildresurs används. Programfix för CQ-4264795
* Om du tar bort en underordnad nod i live-kopian bör liveRelationship frigöras. Programfix för CQ-4270395
* Metadataschemat innehåller bara objekt från den globala konfigurationen och saknar dem från den aktiva klientorganisationen. URL-värdet för formPath återställs till standard även om det ändras. NPR-29945: Programfix för CQ-4262898
* Publicera bildförinställningar till [!DNL Brand Portal] misslyckas med 500-felkod. NPR-29510: Programfix för CQ-4268659

### Webbplatser

* Tomma egenskaper och flera egenskaper sprids inte från utkast under utrullning. Det går inte att återställa live-kopia med utkast för komponenter. NPR-29253: Programfix för CQ-4264928, CQ-4264926, CQ-4267722
* CoralUI, vid användning med `Multifield`, sparar `fileReferenceParameter` på komponentnivå i stället för på multifältnivå. NPR-29537: Programfix för CQ-4266129
* Förbättring av [!DNL Experience Manager] textkomponent och textredigerare till japanska. NPR-29785: Programfix för CQ-4265090
* Sidan som återställs med Timewarp ska referera till rätt bild vid versionshanteringen. NPR-29431: Programfix för CQ-4262638
* Ett problem med arv av Style System-noder från överordnad till underordnad. NPR-29516: Programfix för CQ-4270330
* Ett felmeddelande när social bokföring konfigureras till [!DNL Facebook] autentisering. NPR-29211: Programfix för CQ-4266630
* Den återgivna miniatyrbilden för innehållsfragment visar intern kalenderrepresentation för fältet Datum och Tid. NPR-29531: Programfix för CQ-4269362
* Knapparna visas inte när du öppnar fliken Behörigheter i Coral2-implementeringen. Programfix för CQ-4269419

### Handel

* ConstraintViolationException, när lat innehåll migreras för e-handel. NPR-29247: Programfix för CQ-4264383

### Hantering av innehållsfragment

* Tolkningsfel vid öppning av ett innehållsfragment som har tecken i dollartecken `($)` och öppen klammerparentes `({)`. Programfix för CQ-4270266

### Experience Fragments

* Exportera [!DNL Experience Manager] Upplev fragment till [!DNL Adobe Target]. Programfix för CQ-4265469
* Experience Fragments export till target misslyckas med smarta bilder. Programfix för CQ-4269606

* Användaren stöter på en återvändsgränd när försöker flytta Experience Fragments via Omnissearch i kortvyn. Programfix för CQ-4263848

### WCM - sidredigeraren

* XSS (Cross-site scripting) speglades när en ogiltig väljare användes. Programfix för CQ-4270397

### Replikering

* Data som tillhandahålls av användaren kan inte utelämnas vid utdata i `cq/replication/components/agent` -komponent, vilket resulterar i en lagrad XSS-säkerhetslucka (Cross-site scripting). Programfix för CQ-4266263

### Arbetsflöde

* Dialogdeltagarens kalenderväljarfält har brutits. NPR-29727: Programfix för CQ-4270423

### WCM - SPA

* Aktiverat hämtning av föråtergivet innehåll från en fjärrslutpunkt. Programfix för CQ-4270238
* Varningar i loggar när en SPA mallsida öppnas på serversidan. Programfix för CQ-4270238

### WCM - MSM

* Uppgradera till [!DNL Experience Manager] 6.4.3 gör att det tar lång tid att implementera Multi-Site Manager. Programfix för CQ-4271410

### Integrering

* BrightEdge-autentiseringsuppgifter misslyckas med anslutningsfel. NPR-29168: Programfix för CQ-4265872

* Ett undantagsmeddelande visas när du försöker redigera och spara [!DNL Experience Manager] starta konfigurationen. NPR-29176: Programfix för CQ-4265782/CQ-4266153

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

* Publicera [!DNL Experience Manager Assets] från [!DNL Experience Manager] Skapa /content/dam/mac-mappen till [!DNL Brand Portal] fungerar inte. NPR-29819: Programfix för CQ-4271118

### Plattform

* HtmlLibraryManager tar bort allt innehåll i crx-quickstart vid cacheogiltigförklaring. NPR-29863: Programfix för GRANITE-26197

### Felix

* Information om minnesanvändning visas inte i systemkonsolen när Java11 används. NPR-29669

### Forms

De viktigaste nyheterna för [!DNL Experience Manager Forms] 6.5.1.0 är:

* Endast OSGi: Ett nytt attribut har lagts till `PAGECOUNT` i Output och Forms Service.

* Endast OSGI: Stöd för att skapa statiska PDF-filer med Forms Service.
* Behörigheter för XMLForm.exe har aktiverats för administratör och rotanvändare.
* Aktiverat stöd för ADFS v3.0 för Dynamics lokal integrering.

#### Forms tilläggspaket

**Integrering med backend**

* Det gick inte att hämta WSDL (Protected Web Service Definition Language). NPR-29944: Programfix för CQ-4270777
* När [!DNL Experience Manager Forms] är installerat på IBM WebSphere och det går inte att skapa en formulärdatamodell baserad på SOAP. Programfix för CQ-4251134
* Aktiverat stöd för ADFS (Active Directory Federation Services) v3.0 för integrering på plats i Microsoft Dynamics. Programfix för CQ-4270586
* När en datakällas titel ändras visas inte den uppdaterade titeln i formulärdatamodellen. Programfix för CQ-4265599
* Om namnet på en entitet eller ett attribut innehåller bindestreck eller blanksteg, kan uttrycken inte utvärdera sådana entiteter och attribut. Programfix för CQ-4225129

* Felaktiga utdata visas när ett kolon finns i den primitiva strängutdata. Programfix för CQ-4260825

* Även om inget innehåll förväntas från REST API-utdata genereras ett fel av formulärdatamodellens invoke-åtgärd. Programfix för CQ-4268828

**Adaptiv Forms**

* Det gick inte att lägga till en ny instans i adaptivt formulärfragment under en lat inläsning. NPR-29818: Programfix för CQ-4269875
* Verifiera att komponenten inte loggar eller visar något fel för dokumentmallar. Programfix för CQ-4272999
* Stöd har lagts till för att inaktivera layoutredigeraren för Adaptive Forms. Programfix för CQ-4270810
* Verifieringssteget för Adaptive Forms har återställts i [!DNL Experience Manager] 6.5. Programfix för CQ-4269583

* Fel vid validering av adaptiva formulärfält [!DNL Adobe Sign]. Programfix för CQ-4269463
* När en [!DNL Experience Manager Forms] -instansen har fler än 20 adaptiva formulärfragment och namnet på alla formulärfragment börjar med samma sträng. Sökningen returnerar inga eller endast de 20 senast skapade fragmenten. Programfix för CQ-4264414, CQ-4264914

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
* När en bild på mer än 2 MB bifogas som en bifogad fil på fältnivå till ett formulär i Android-versionen av [!DNL Experience Manager Forms] programmet kraschar. Programfix för CQ-4265578

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

* När en fullständig tillgänglighetskontroll utförs på det statiska PDF som skapats med [!DNL Experience Manager Forms Designer], misslyckas kontrollen av primärt språk på grund av att språkattribut saknas. Programfix för CQ-4272923, CQ-4271002

**Forms - dokumentsäkerhet**

* Digital signatur med HSM (Hardware Security Module) fungerar inte med OSGi Linux på Java 11 och Java 8\. NPR-29838: Programfix för CQ-4270441
* Digital signatur med HSM (Hardware Security Module) fungerar inte med JEE Linux och alla appservrar som stöds, dvs. JBoss och Websphere. NPR-29839: Programfix för CQ-4266721
* Verifiering av signaturer i PDF med PDF Advanced Electronic Signatures (PAdES) genererar InvalidOperationException. NPR-29842: Programfix för CQ-4244837
* Utökat stöd för Document Security Extension för Office 2019\. Programfix för CQ-4254369, CQ-4259764

**Forms - dokumenttjänster**

* PDF kan inte konvertera till PDF/A-1b med formulärfältet har ingen utseendeordlista. NPR-29940: Programfix för CQ-4269618

* OSGi: Det går inte att avgöra antalet sidor som genereras under återgivningen. NPR-28922: Programfix för CQ-4270870
* Aktiverat stöd för statiska PDF-filer med Forms-tjänsten i [!DNL Experience Manager Forms OSGi]. NPR-28572: Programfix för CQ-4270869
* Det går inte att ändra behörigheten för XMLForm.exe. NPR-29828, NPR-29237: Programfix för Q-4267080
* Det statiska PDF som skapas av [!DNL Experience Manager Forms] serverns utdatamoddul fyller inte i attributet/taggen language med språket i det dokument som skapas. NPR-27332: Programfix för CQ-4271002

**Forms - Foundation JEE**

* Om pdfg_srt inte är tillgänglig i de sista artefakterna misslyckas installationsprogrammet. NPR-29854: Programfix för CQ-4270137
* LCBackupMode.sh fungerar inte. NPR-29840: Programfix för CQ-4269424
* UDP-portreferens ska tas bort från användargränssnittet för WebSphere. Programfix för CQ-4264782

### Funktionspaket ingår

#### Resurser - inkluderade

* Aktiverat stöd för Multi-Site Manager för [!DNL Experience Manager Assets]. Mer information finns i [Återanvänd resurser med MSM för Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/reuse-assets-using-msm.html). NPR-29199: Programfix för CQ-4259922

#### Webbplatser - ingår

* Exportera [!DNL Experience Manager] Upplev fragment till [!DNL Adobe Target]. Mer information finns i [Experience Fragment Link Rewriter Provider - HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML). Programfix för CQ-4265469

#### Forms - dokumenttjänster - ingår

* Endast OSGi: Ett nytt attribut, PAGECOUNT, har lagts till i Output och Forms Service. NPR-28922: Programfix för CQ-4270870
* Endast OSGi: Stöd för att skapa statiska PDF-filer med Forms Service. NPR-28572: Programfix för CQ-4270869
* Behörigheter för XMLForm.exe har aktiverats för administratör och rotanvändare. NPR-29237: Programfix för CQ-4267080

### OSGi-paket och innehållspaket

Följande textdokument listar de OSGi-paket och innehållspaket som ingår i [!DNL Experience Manager] 6.5.1.0

Lista över OSGi-paket som ingår i [!DNL Experience Manager] 6.5.1.0

[Hämta fil](assets/6_5-bundle-list.txt)

Lista över innehållspaket som ingår i [!DNL Experience Manager] 6.5.1.0

[Hämta fil](assets/6_5-content-package-list.txt)
