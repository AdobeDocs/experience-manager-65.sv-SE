---
title: '[!DNL Experience Manager] 6.5 Versionsinformation för Service Pack'
description: Versionsinformation som är specifik för  [!DNL Adobe Experience Manager] 6.5 Service Pack 10
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: a3d52ecf9284ba22cac3739ba543e5dd5c855331
workflow-type: tm+mt
source-wordcount: '4077'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] 6.5 Versionsinformation för Service Pack {#aem-service-pack-release-notes}

## Versionsinformation {#release-information}

| Produkter | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.10.0 |
| Typ | Service Pack-version |
| Date | 26 augusti 2021 |
| Hämta URL | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip) |

## Vad ingår i [!DNL Adobe Experience Manager] 6.5.10.0 {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.10.0 innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat samt prestanda, stabilitet och säkerhetsförbättringar som släppts sedan 6.5-utgåvan släpptes i april 2019. Service Pack är installerat på [!DNL Adobe Experience Manager] 6.5.

De viktigaste funktionerna och förbättringarna i [!DNL Adobe Experience Manager] 6.5.10.0 är:

* **Förbättrade  [!DNL Content Fragment] modeller och redigerare**: Nu kan du skapa komplexa och anpassade modeller för strukturerat innehåll med hjälp av kapslade  [!DNL Content Fragment] modeller. Innehållsstrukturer modulariseras till grundläggande element som modelleras som underfragment. Fragment på högre nivå refererar till dessa delfragment. Fler datatypsförbättringar som avancerade valideringsregler ger större flexibilitet vid innehållsmodellering med [!DNL Content Fragments]. Redigeraren [!DNL Experience Manager] [!DNL Content Fragment] har stöd för kapslade fragmentstrukturer i en gemensam redigeringssession, med förbättringar som strukturträdvyn och tabbad kolumnnavigering via fragmenthierarkier.

* **GraphQL API för[!DNL Content Fragments]**: Det nya GraphQL API:t är standardmetoden för att leverera strukturerat innehåll i JSON-format. GraphQL-frågor gör att klienter bara kan begära relevanta innehållsobjekt för att återge en upplevelse. En sådan markering eliminerar överleverans av innehåll (möjlig med HTTP REST API:er) som kräver att innehåll analyseras på klientsidan. GraphQL-scheman härleds från [!DNL Content Fragment]-modeller, och API-svar görs i JSON-format. I [!DNL Experience Manager] som [!DNL Cloud Service] finns [GraphQL-frågor kvar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-api-content-fragments.html#persisted-queries-caching) och processcacheanpassade GET-begäranden. Det är ännu inte möjligt i [!DNL Experience Manager] 6.5.10.0.

* **Hierarkihantering och framtida förhandsgranskning**: Användarna har nu ett gränssnitt för att komma åt innehållsstrukturerna när de  [!DNL Experience Manager] startar, inklusive möjligheten att lägga till och ta bort sidor vid en start. Den här funktionen förbättrar flexibiliteten i [!DNL Experience Manager]-lanseringar att skapa innehållsversioner för framtida publicering. [Funktionerna för ](/help/sites-authoring/working-with-page-versions.md#timewarp) tidsförvrängning gör att användarna kan förhandsgranska när framtida innehållslägen visas.

* **Anslutna resurser**:  [!DNL Experience Manager] utökar  [!DNL Connected Assets] funktionaliteten till att även använda  [!DNL Dynamic Media] bilder i de tillämpliga kärnkomponenterna. Se [använd anslutna resurser](/help/assets/use-assets-across-connected-assets-instances.md).

* **Alternativ för länkdelning för att hämta resurser eller återgivningar**: När du delar resurser och samlingar som länkar kan användarna välja om de vill tillåta hämtning av originalresurser, deras återgivningar eller båda med hjälp av den delade länken. Dessutom kan användare som hämtar resurser som delas med dem via länken välja att bara hämta de ursprungliga resurserna, endast återgivningarna eller båda.

* **Begränsa genererade** delresurser: Administratörer kan begränsa antalet underresurser som  [!DNL Experience Manager] genereras för sammansatta resurser som PDF-, PowerPoint-, InDesign och Keynote-filer. Se [Hantera sammansatta resurser](/help/assets/managing-linked-subassets.md#generate-subassets).

* **Camera Raw stöd**: Det finns ett nytt  [!DNL Camera Raw] paket med stöd för  [!DNL Adobe Camera Raw] v10.4. Se  [Bearbeta bilder med [!DNL Camera Raw]](/help/assets/camera-raw.md).

* Den inbyggda databasen (Apache Jackrabbit Oak) uppdateras till 1.22.8.

* **Tillgänglighetsförbättringar**:

   * [!DNL Dynamic Media] innehåller många tillgänglighetsförbättringar för visningsprogram. Se [[!DNL Dynamic Media] uppdateringar](#dynamic-media-65100).

   * Platform har några tillgänglighetsförbättringar. Se [Plattformsuppdateringar](#platform-65100).

* **Förbättringar** av användarupplevelsen:

   * [!DNL Experience Manager] visar direkt en lista över alla innehållsmodeller under en mapp utan att innehållsförfattare behöver navigera i filstrukturen. Funktionen kräver nu färre klick och förbättrar redigeringseffektiviteten.

   * Med Banfältet i redigeraren [!DNL Sites] kan författare dra resurser från [!DNL Content Finder].

* Stöd för `GuideBridge#getGuidePath` API har lagts till i [!DNL AEM Forms].

* Du kan nu använda tjänsten Automated forms conversion för att [konvertera PDF forms på franska, tyska och spanska ](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#language-specific-meta-model) till anpassningsbara formulär.

* **Felmeddelanden i egenskapsläsaren**: Felmeddelanden för varje egenskap i webbläsaren Adaptive Forms Properties har lagts till. Dessa meddelanden hjälper till att förstå tillåtna värden för ett fält.

* **Stöd för att använda det literala alternativet för att ange ett värde för en JSON-typvariabel**: Du kan använda det literala alternativet för att ange ett värde för en JSON-typvariabel i det angivna variabelsteget i ett AEM arbetsflöde. Med det literala alternativet kan du ange en JSON i form av en sträng.

<!--

* [Platform Updates](../forms/using/aem-forms-jee-supported-platforms.md): [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platforms:
  * [!DNL Adobe Acrobat 2020]
  * [!DNL Ubuntu 20.04]
  * [!DNL Open Office 4.1.10]
  * [!DNL Microsoft Office 2019]
  * [!DNL Microsoft Windows Server 2019]
  * [!DNL RHEL8]

  -->

En lista över alla funktioner och förbättringar som introducerats i [!DNL Experience Manager] 6.5.10.0 finns i [vad som är nytt i [!DNL Adobe Experience Manager] 6.5 Service Pack 10](new-features-latest-service-pack.md).

Nedan följer en lista över korrigeringar i [!DNL Experience Manager] 6.5.10.0-versionen.

### [!DNL Sites] {#sites-65100}

* Fokuseringen flyttas till ett annat fält när du skriver i fältet **[!UICONTROL Default Value]** under fliken **[!UICONTROL Properties]** i redigeraren för innehållsfragment (NPR-36992).

* När du filtrerar [!DNL Content Fragment]-modeller under en angiven sökväg returnerar [!DNL Experience Manager]-sökningen alla noder med `cq:Template` i stället för att bara returnera sökvägar och noder för [!DNL Content Fragment]-modellen (SITES-1453).
* [!DNL Content Fragments] returneras  `null` som mappstatus (SITES-1157).
* [!DNL Experience Manager] tillåter inte användare att inaktivera och aktivera  [!DNL Content Fragment] modeller (SITES-1088).
* När en användare flyttar, byter namn på eller tar bort [!DNL Content Fragments] eller medieresurser uppdateras inte det refererade [!DNL Content Fragments] automatiskt (SITES-196).
* När du klistrar in komponenter från en sida till en annan skapas JavaScript-fel (NPR-37030).
* När sidegenskaper visas snabbt öppnas Sidegenskaper för en annan sida (NPR-37025).
* Med innehållsfragmentet kan innehållsfragmentet referera till sig självt. Väljaren stöder inte åtgärden (NPR-36993).
* Efter uppgradering till Service Pack 9 kan vissa användare inte flytta mappar i Experience Manager och se fel i loggarna (SITES-1481).
* När du justerar bredden på komponenten i layoutbehållaren i redigeringsläge, observeras en flimmer (NPR-36961).
* När du befordrar en programstart kommer ändringarna i den befordrade programstarten att introduceras till andra programstarter. Om en användare befordrar den dubbla lanseringen återspeglas det fördubblade innehållet på källsidan (NPR-36893).
* [!DNL Experience Manager] lägger till en grå kant i vissa PNG-bilder med genomskinlighet om du lägger till bilderna på en sida med Image Core-komponenten eller om du ändrar storlek med Foundation Image-komponenten (NPR-36879).
* [!DNL Experience Manager Sites] Administratörsgränssnitt med ett stort antal mallar resulterar i långsam navigering (NPR-36870).
* Uppgradera till Service Pack 9 så går det inte att skapa ett fåtal komponenter. Det här problemet tillåter inte att [!DNL Sites]-användare skapar nya sidor (NPR-36857).
* Metoden `ContextHubImpl` skapar en `ResourceResolver` som inte är stängd. Det leder till varningsmeddelanden om `ResourceResolver` som körs länge och tjänsten returnerar oväntade resultat vid olika tidpunkter (NPR-36853).
* Vid synkronisering av en enda live-kopia från egenskaperna för en ritningssida synkroniseras även alla andra live-kopior (NPR-36829, NPR-36522).
* När bara XLS MIME-typen används fungerar inte filöverföringsfunktionen som förväntat (NPR-36785).
* Nya taggar med inledande versal och alla versala ord visas inte i taggfältet i [!DNL Content Fragments] (NPR-36742).
* Alternativet Enkelt textelement när du lägger till [!DNL Content Fragment] saknas text och skapar oregelbunden formatering som hör till listor och kapslade listor (NPR-36565).
* När en författare kommenterar en komponent på en sida, tar bort komponenten och utför en ångra-åtgärd, uppstår ett fel när sidans tidslinjedata ska visas i platskonsolen (NPR-36528).
* Sidegenskaper Med alternativet [!UICONTROL Save & Close] i gruppredigeraren sparas ändringarna men redigeraren stängs inte (NPR-36527).
* När en användare försöker dra och släppa en ny textkomponent på en sida, försvinner komponenten omedelbart (NPR-36442).
* När en användare skriver i en on demand-tagg som innehåller utrymme (taggen som inte finns i systemet) och trycker på Retur, visas taggen under fältet. Men när [!DNL Content Fragment] sparas och öppnas igen visas inte on-demand-taggen (NPR-36441).
* Mallen kan inte tas bort när instansen nås via Dispatcher (NPR-36385).
* När en sida flyttas krävs en manuell uppdatering av webbläsaren för att återge ändringarna (NPR-36381).
* När du markerar en komponent kan du klippa ut eller kopiera den med Ctrl+X eller Ctrl+C (och Kommando+X eller Kommando+C på Mac). När du klickar på en annan komponent kan du klistra in med verktygsfältet, men inte med tangentbordet (Ctrl+V eller Kommando+V) (NPR-36379).
* När en användare försöker klippa ut komponenter med saxikonen för att flytta dem någon annanstans inträffar ett konsolfel. När du klistrar in flyttas dessutom bara en komponent (NPR-36378).
* [!DNL Experience Manager] har en fråga utan index på WCM eller meddelanden, vilket saktar ned prestanda (NPR-36303).
* När en författare återställer arvet för den borttagna ärvda komponenten är det tillgängliga alternativet att synkronisera allt sidinnehåll. Innehållsförfattarna måste synkronisera hela sidan även om arvet bara återställs på en komponent. En fullständig synkronisering kan leda till att oönskat innehåll synkroniseras (NPR-34456, CQ-4310183).
* Live-användning av en komponent på Author-instansen visar inte alla förekomster. Vissa komponenter används på fler än 1 000 sidor, men rapporten visar endast cirka 40 sidor (CQ-4323724).
* När det finns en webbplatsstruktur med många undersidor tar det längre tid att läsa in undersidorna i kolumnvyn i Experience Manager 6.5.8 jämfört med Experience Manager 6.4.8.2 (CQ-4322766).
* Avmarkera Alla fungerar inte med alternativet Rollout Page (NPR-37070).
* När du öppnar en befintlig version av en v3-komponent på en sida öppnas inte dialogrutan för sidegenskaper och en `NullPointerException` loggas (SITES-1830).

### [!DNL Assets] {#assets-65100}

Följande problem har korrigerats i [!DNL Assets]:

* Värdet för egenskapen `jcr:title` uppdateras inte på publiceringsinstansen när en mapp har flyttats. Om du ändrar namn på och publicerar om en mapp i författaren uppdateras inte `jcr:title`-egenskapsvärdet för samma i publiceringsinstansen (NPR-36369).

* Om två eller flera resurser är markerade och ett eller flera metadatafält redigeras misslyckas sparåtgärden. Felkod 500 i webbläsaren Safari (NPR-36413).

* Import av massmetadata misslyckas på grund av felaktigt datumformat (NPR-36428).

* När du har valt att uppdatera metadata på [!UICONTROL Properties]-sidan tar det lång tid för gränssnittet att svara när det finns många alternativ i schemat (NPR-36430).

* Sökfilter som använder predikatet [!UICONTROL Expiry Status] fungerar inte (NPR-36436).

* Popup-menyn för olika fält i [!UICONTROL Folder Metadata]-egenskaper visar inte de senast valda värdena (NPR-36937, CQ-4314429).

* När användaren söker efter filer och mappar och väljer [!UICONTROL Files & Folders] visas bara filerna, men inte mappen (CQ-4319543, NPR-36627).

* Alternativen i verktygsfältet är olika när samma samling väljs inifrån en mapp och när den väljs från ett sökresultat (NPR-36620).

* Alternativet [!UICONTROL Quick Publish] är inte tillgängligt på sökresultatsidan (NPR-36904, CQ-4317748).

* När användare skapar en live-kopia av en resurs utan att ange filnamnstillägget, går det inte att använda direktkopieringsfilen efter hämtningen (NPR-36903, CQ-4326305).

* När en användare läggs till som ägare till en underordnad mapp får användaren ägarbehörighet till den överordnade mappen, och därmed även till den överordnade mappens övriga undermappar. Användaren tas inte heller bort som ägare till den överordnade mappen när den försöker ta bort den. (NPR-36801, CQ-4323737).

* [!DNL Experience Manager] genererar ett undantagsfel när minnet är slut när du försöker skapa underresurser för sammansatta resurser, till exempel en PowerPoint-presentation (NPR-36668).

* När användare flyttar en resurs som redan används på en publicerad webbplatssida publiceras webbplatssidan igen även om alternativet att publicera inte har valts (NPR-36636, CQ-4323500).

* När du använder typidentifieringsfunktionen för Apache Tika MIME lämnar resurser som överförts med metoden `AssetManager.createAsset` en temporär fil med namnet `apache-tika-*.tmp` i den temporära katalogen. Den här tillfälliga filen använder allt tillgängligt ledigt diskutrymme (NPR-36545).

* Alla DRM-skyddade resurser hämtas och användaren väljer att hämta en viss resurs följs inte (CQ-4327422).

* Det går inte att dra resurser till `pathfield` i användargränssnittet (NPR-36849).

* När du markerar en resurs i kolumnvyn försvinner panelen med resursinformation (NPR-36667).

### [!DNL Dynamic Media] {#dynamic-media-65100}

**Förbättrad tillgänglighet**

Följande tillgänglighetsförbättringar är tillgängliga i [!DNL Dynamic Media Viewers].

* Skärmläsare lägger nu till en berättarröst i platshållartexten för att söka efter och lägga till e-postadress som ett obligatoriskt fält i Dela resurser som en länkdialogruta och meddelar även [!UICONTROL Please fill out this field]-verktygstipset (CQ-4327761).

* Skärmläsare lägger nu in en korrekt berättarröst i namnen och syftet med olika fält i [!UICONTROL Image Preset Editor] när användaren öppnar gränssnittsfälten med tangentbordet (CQ-4325677).

* Tangentbordsfokus flyttas nu korrekt till sökfliken i dialogrutan [!UICONTROL Viewer Presets] från resursväljaren för alternativet [!UICONTROL Rich Media Type] (CQ-4324736).

* När du navigerar i formulärläge med hjälp av tangentbordstangenter lägger skärmläsarna till de etiketter som motsvarar alternativen för ökning och minskning på fliken [!UICONTROL Create] på [!UICONTROL Image Presets] (CQ-4323900).

* Skärmläsare meddelar nu alternativet [!UICONTROL Search and Add Email Address] för att dela resurser som en länkdialogruta (CQ-4323352).

* Tangentbordsfokus behålls i verktygsfältet när du navigerar resurser med tangentbordstangenter (CQ-4322037).

* Skärmläsare lägger nu till en berättarröst för den nya fältinformationen [!UICONTROL Edit] efter att ha valt alternativet [!UICONTROL Add Crop] på [!UICONTROL Responsive Image Crop]-sidan på [!UICONTROL Edit Image Processing Profile] (CQ-4290734).

* På [!UICONTROL Edit Image Preset]- och [!UICONTROL Create Interactive Video]-sidor kan skärmläsare nu meddela sidrubriken korrekt när de navigerar på sidorna med hjälp av rubrikkortkommandon (CQ-4290730) (CQ-4290701).

* Skärmläsare kan nu identifiera olika delar av skärmen (t.ex. höger panelregion, vänster panel, verktygsfältet Åtgärd, markering i visningsprogrammets verktygsfält och inzoombar bildlandmärke) med hjälp av kortkommandon för landmärken och regioner när de navigerar på följande sidor.

   * [!UICONTROL Viewer Preset Editor] (CQ-4290729)

   * [!UICONTROL Image Set Editor] (CQ-4290710)

   * [!UICONTROL Create Interactive Video] (CQ-4290702).

* Skärmläsare anger nu namnet på delningsalternativet i videobildrutan när de navigerar med nedpiltangenten (CQ-4290728).

* Skärmläsare lägger nu till en berättarröst för olika alternativ på flikarna [!UICONTROL Sprite] och [!UICONTROL Background] på fliken [!UICONTROL Appearance] i [!UICONTROL Viewer Preset Editor] (CQ-4290727).

* Obligatoriska fält, som det fält som ska redigeras [!UICONTROL Width], på fliken [!UICONTROL Basic] på sidan [!UICONTROL Edit Video Encoding] har nu en asterisk (*) (CQ-4290725).

* Skärmläsare meddelar nu etiketten för alternativen på [!UICONTROL Image Profiles]-sidan (CQ-4290723).

* Windows-användare kan nu navigera ut ur den utökade CSS-redigeraren på [!UICONTROL Viewer Preset Editor] när CSS Editor är i fokus (CQ-4290720).

* Skärmläsarna visar nu etiketterna för olika redigeringsfält och alternativ på fliken [!UICONTROL Edit Image Preset] när de navigerar i formulärläge (CQ-4290717).[!UICONTROL Basic]

* Skärmläsare lägger nu till en berättarröst för rollen och läget (markerat eller inte markerat) för alternativ i användargränssnittet i den vänstra navigeringen på informationssidan för resurser (CQ-4290709).

* Skärmläsare kommenterar nu korrekt läget (markerat eller inte markerat) och länken för bildväxlingarna på fliken [!UICONTROL Content] på sidan [!UICONTROL Create Interactive Video] (CQ-4290707).

* Skärmläsare lägger nu korrekt till en berättarröst för namn, roll och tillstånd för olika segment i videons tidslinjeskala när de navigerar med nedpiltangenten på [!UICONTROL Create Interactive Video]-sidan (CQ-4290706).

* Skärmläsare lägger nu till en berättarröst för namn, roll och standardläge (markerat eller inte markerat) och egenskap när du navigerar bland alternativen på sidan [!UICONTROL Create Interactive Video] (CQ-4290704).

* Skärmläsare lägger nu till en berättarröst för namn, roll och standardläge (markerat eller inte markerat) för alternativen [!UICONTROL All Assets] och [!UICONTROL All Collections] när sidan [!UICONTROL Publish] navigeras (CQ-4290705).

* När du överför ett videoformat som inte stöds (annat än MP4) på [!UICONTROL Create Interactive Video]-sidan, visas och meddelas felmeddelanden i Experience Manager (CQ-4290700).

* Kontrasten för siffrorna (tid i sekunder) i tidslinjeskalan på [!UICONTROL Create Interactive Video]-sidan uppfyller nu minimikravet på luminiscens, så att användare med begränsad färguppfattning enkelt kan läsa (CQ-4290699).

* Skärmläsare meddelar nu etiketten för fältet [!UICONTROL Product Name] vid navigering på sidan [!UICONTROL Create Interactive Video] (CQ-4290697).

**Åtgärdade problem**

Följande felkorrigeringar är tillgängliga i [!DNL Dynamic Media].

* Överförda videoklipp till [!DNL Experience Manager]-skärmen `Process failed` när `dynamicmedia_scene7`-körningsläget är aktiverat och synkronisering är inaktiverat (CQ-4327791).

### Plattform {#platform-65100}

Följande förbättringar har levererats i detta Service Pack:

* När en användare markerar ett objekt i trädvyn visas det som markerats och de verktygsfältsalternativ som visas högst upp (NPR-36504).
* Vissa text- och kontrollnamn är lättare att läsa för användare med synproblem eftersom luminiscensförhållandet uppfyller det lägsta tillåtna förhållandet på 4,5:1 (NPR-36503).
* När en användare använder kalenderkontrollerna visar skärmläsaren information om beskrivande datum, månad och veckodag. När en användare använder kalenderkortkommandon visar skärmläsaren ändringen av datum, månad och år (NPR-36498).
* Stöd ges för att köra anpassad JavaScript `Clientlibs` med ECMAScript 6-funktioner utan att följa strikt läge. Mer specifikt läggs `emitUseStrict`-flaggan till i `GCCScriptProcessor` (NPR-36411).

Följande felkorrigeringar ingår i detta Service Pack:

* Anpassade hälsokontroller utförs oftare än schemalagt (NPR-36985).
* Metoden `Resourceresolver map` returnerar ett felaktigt resultat för aliassidor (NPR-36767).
* [!DNL Experience Manager] starten fördröjs på grund av inläsningsarbetsflöden (NPR-36615).

### Integreringar {#integrations-65100}

* Experience Manager slutar att svara när den primära MongoDB-noden växlar till en annan nod (NPR-36566).
* [!DNL Sling content distribution] misslyckas vid borttagning av samlingsmedlem (NPR-36521, CQ-4323578).

### Användargränssnitt {#user-interface-65100}

* Sidpanelen **[!UICONTROL References]** visar inte resurs- och platsreferenser (GRANITE-35078, GRANITE-34892).

### Översättningsprojekt {#translation-65100}

* Extra undersidor i en språkkopia av ett fleröversättningsprojekt raderas (NPR-36622).

### Arbetsflöde {#workflow-65100}

* Om servern får ett meddelande om att den inte är på kontoret rapporterar den minnesvarningar och slutar svara (NPR-36768).

### [!DNL Communities] {#communities-65100}

* Webbplatssidor i communityn öppnas i `LoggedIn`-läge för anonyma gästanvändare (NPR-36908).

* Om det finns mer än en sida på sidan **[!UICONTROL Community]** > **[!UICONTROL Ideas]** > **[!UICONTROL Comments]** fungerar inte sidnavigeringen (NPR-36541).

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
>* [!DNL Experience Manager Forms] släpper tilläggspaketen en vecka efter det schemalagda datumet för  [!DNL Experience Manager] Service Pack.


**Adaptiv Forms**

<!--

* When the validations performed on the field values in an adaptive form are successful, [!DNL AEM Forms] fails to invoke the Form Data Model (CQ-4325491).

-->

* När du lägger till en språkordlista i ett översättningsprojekt och sedan öppnar projektet visas ett felmeddelande i [!DNL AEM Forms] (CQ-4324933):

   ```TXT
   Uncaught TypeError: Cannot read property 'PROJECT_LISTING_PATH' of undefined
   at openButtonClickHandler (clientlibs.js:245)
   at HTMLButtonElement.onclick (clientlibs.js:258)
   ```

* Prestandaproblem efter installation av [!DNL AEM Forms] Service Pack 7 (CQ-4326828).

**Korrespondenshantering**

* Fördröjning av visning av tecken på fliken [!UICONTROL Data] och i förhandsvisningen av HTML-bokstav (NPR-37020).

* När du redigerar ett textdokumentfragment visas de nya orden som HTML-taggar efter att fragmentet har sparats (NPR-36837).

* Det går inte att visa bokstäverna som har sparats som utkast (NPR-36816).

* När du redigerar ett textdokumentfragment och sedan förhandsgranskar brevet, visas uttrycksspråket i HTML-förhandsvisningen (CQ-4322331) i AEM Forms.

* Problem vid återgivning av data med en mall för självbetjäningsbrev (NPR-37161).


**Interaktiv kommunikation**

* Ett tabbtecken dupliceras mellan två ord varje gång du förhandsgranskar ett interaktivt meddelande efter att ha redigerat ett textdokumentfragment (NPR-37021).

* [!DNL AEM Forms] visar ett fel när du sparar ett textdokumentfragment som överskrider den maximala storleksgränsen (NPR-36874).

* När du lägger till en bild i ett interaktivt meddelande visas ytterligare ett tomt block efter bilden (NPR-36659).

* När du markerar all text i en redigerare kan du inte ändra teckensnittstexten till Arial (NPR-36646).

<!--

* When you create a URL in an editor and preview the changes, a black background displays instead of the URL text (NPR-36640).

-->

* När du kopierar och klistrar in text i en redigerare finns det problem med att ändra teckensnittet till Arial för punkter som är tillgängliga i dokumentet (NPR-36628).

* Problem med indrag för punkter i textredigeraren (NPR-36513).

<!--
**Designer**

* Screen Reader fails to read floating field data placed inside text label on the Master page or on Subform pages in a dynamic PDF (CQ-4321587).

-->

**Dokumenttjänster**

* När du konverterar XDP-filer till PDF-filer och sedan sätter ihop den resulterande PDF-filen misslyckas PDF-generationen och följande felmeddelande visas (CQ-4328666):

   ```TXT
   Caused by: com.adobe.fd.assembler.client.AssemblerException$ClientException: Document is in a disposed state!
   ```

**Forms Workflow**

* Det går inte att skicka ett formulär till en Workbench-process efter uppgradering till AEM Forms Service Pack 8 (CQ-4325846).

**HTML5 Forms**

* När du anger värdet för egenskapen `mfAllowAttachments` som `True` i CRX DE-databasen skadas `dataXml` när HTML5-formuläret skickas (NPR-37035).

* När du återger en XDP som HTML med `dataXml` visar [!DNL AEM Forms] ett `Page Unresponsive`-fel (NPR-36631).

### Handel {#commerce-65100}

* Värdet i fältet **[!UICONTROL Published By]** som visas är felaktigt i kolumnvyn (NPR-36902).
* När en katalog introduceras markeras nya produkter felaktigt som ändrade produkter (NPR-36666).
* När du återskapar en borttagen produkt återskapas inte produktsidan (NPR-36665).
* Ändrade sidor uppdateras men motsvarande länkade produkter uppdateras inte vid kataloglansering (CQ-4321409, NPR-36422).
* Arbetsflödena **[!UICONTROL Publish later]** och **[!UICONTROL Unpublish later]** fungerar inte (CQ-4327679).

Mer information om säkerhetsuppdateringar finns på [[!DNL Experience Manager] sidan Säkerhetsbulletiner](https://helpx.adobe.com/security/products/experience-manager.html).

## Installera 6.5.10.0 {#install}

**Installationskrav och mer information**

* Experience Manager 6.5.10.0 kräver Experience Manager 6.5. Mer information finns i [uppgraderingsdokumentationen](/help/sites-deploying/upgrade.md).
* Service Pack-nedladdningen finns på Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* Installera Experience Manager 6.5.10.0 på en av författarinstanserna med hjälp av Package Manager på en distribution med MongoDB och flera instanser.

>[!NOTE]
>
>Adobe rekommenderar inte att du tar bort eller avinstallerar paketet [!DNL Adobe Experience Manager] 6.5.10.0.

### Installera Service Pack {#install-service-pack}

Så här installerar du Service Pack på en [!DNL Adobe Experience Manager] 6.5-instans:

1. Starta om instansen innan installationen om instansen är i uppdateringsläge (när instansen uppdaterades från en tidigare version). Adobe rekommenderar att du startar om om den aktuella upptiden för en instans är hög.

1. Ta en ögonblicksbild eller en ny säkerhetskopia av din [!DNL Experience Manager]-instans innan du installerar.

1. Hämta Service Pack från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip).

1. Öppna Pakethanteraren och klicka på **[!UICONTROL Upload Package]** för att överföra paketet. Mer information finns i [Pakethanteraren](/help/sites-administering/package-manager.md).

1. Markera paketet och klicka på **[!UICONTROL Install]**.

1. Om du vill uppdatera S3-anslutningen stoppar du instansen efter installationen av Service Pack, byter ut den befintliga kopplingen mot en ny binär fil som finns i installationsmappen och startar om instansen. Se [Amazon S3-datalager](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Dialogrutan för pakethanterarens gränssnitt avslutas ibland när Service Pack installeras. Adobe rekommenderar att du väntar på att felloggarna ska stabiliseras innan du får åtkomst till distributionen. Vänta på de specifika loggarna för avinstallationen av uppdateringspaketet innan du försäkrar dig om att installationen lyckas. Vanligtvis inträffar det här problemet i [!DNL Safari]-webbläsaren, men det kan inträffa i alla webbläsare.

**Automatisk installation**

Det finns två sätt att automatiskt installera [!DNL Experience Manager] 6.5.10.0 på en fungerande instans:

S. Placera paketet i mappen `../crx-quickstart/install` när servern är tillgänglig online. Paketet installeras automatiskt.

B. Använd [HTTP-API:t från Package Manager](/help/sites-administering/package-manager.md#package-share). Använd `cmd=install&recursive=true` så att kapslade paket installeras.

>[!NOTE]
>
>Adobe Experience Manager 6.5.10.0 stöder inte installation av Bootstrap.

**Validera installationen**

1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience Manager (6.5.10.0)` under [!UICONTROL Installed Products].

1. Alla OSGi-paket är antingen **[!UICONTROL ACTIVE]** eller **[!UICONTROL FRAGMENT]** i OSGi Console (Använd webbkonsol: `/system/console/bundles`).

1. OSGi-paketet `org.apache.jackrabbit.oak-core` är version 1.2.3 eller senare (Använd webbkonsol: `/system/console/bundles`).

Information om vilka plattformar som är certifierade för att fungera med den här versionen finns i [tekniska krav](/help/sites-deploying/technical-requirements.md).

### Installera Adobe Experience Manager Forms tilläggspaket {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Hoppa över om du inte använder Experience Manager Forms. Korrigeringar i Experience Manager Forms levereras via ett separat tilläggspaket en vecka efter den schemalagda versionen av [!DNL Experience Manager] Service Pack.

1. Kontrollera att du har installerat Adobe Experience Manager Service Pack.
1. Ladda ned motsvarande tilläggspaket från Forms som finns på [AEM Forms releases](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) för ditt operativsystem.
1. Installera Forms tilläggspaket enligt beskrivningen i [Installera AEM Forms tilläggspaket](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>Experience Manager 6.5.10.0 innehåller en ny version av [AEM Forms-kompatibilitetspaket](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases). Om du använder en äldre version av AEM Forms Compatibility Package och uppdaterar till Experience Manager 6.5.10.0 installerar du den senaste versionen av paketet efter installationen av Forms Add-On Package.

<!--

### Install Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Skip if you are not using AEM Forms on JEE. Fixes in Adobe Experience Manager Forms on JEE are delivered through a separate installer.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes](jee-patch-installer-65.md).

>[!NOTE]
>
>After installing the cumulative installer for Experience Manager Forms on JEE, install the latest Forms add-on package, delete the Forms add-on package from the `crx-repository\install` folder, and restart the server.

-->

### UberJar {#uber-jar}

UberJar för Experience Manager 6.5.10.0 finns i [Maven Central-databasen](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.10/).

Om du vill använda UberJar i ett Maven-projekt läser du [hur du använder UberJar](/help/sites-developing/ht-projects-maven.md) och inkluderar följande beroende i projektstrukturen:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.10</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar och andra relaterade artefakter finns tillgängliga i Maven Central Repository i stället för i Adobe Public Maven-databasen (`repo.adobe.com`). Huvudfilen för UberJar har bytt namn till `uber-jar-<version>.jar`. Det finns alltså inget `classifier`, med `apis` som värde, för taggen `dependency`.

## Föråldrade funktioner {#removed-deprecated-features}

Nedan finns en lista över funktioner som är markerade som borttagna med [!DNL Experience Manager] 6.5.7.0. Funktioner markeras som borttagna från början och senare i en framtida version. Ett alternativt alternativ anges.

Granska om du använder en funktion eller en funktion i en distribution. Planera också att ändra implementeringen så att ett alternativt alternativ används.

| Yta | Funktion | Ersättning |
|---|---|---|
| Integreringar | Skärmen **[!UICONTROL AEM Cloud Services Opt-In]** är föråldrad eftersom integreringen [!DNL Experience Manager] och [!DNL Adobe Target] har uppdaterats i Experience Manager 6.5. Integreringen stöder Adobe Target Standard API. API:t använder autentisering via Adobe IMS och [!DNL Adobe I/O] och stöder den växande rollen hos Adobe Launch till instrumentets [!DNL Experience Manager]-sidor för analys och personalisering. Anmälningsguiden är funktionellt irrelevant. | Konfigurera systemanslutningar, Adobe IMS-autentisering och [!DNL Adobe I/O]-integreringar via respektive [!DNL Experience Manager]-molntjänster. |
| Anslutningar | Adobe JCR Connector för Microsoft® SharePoint 2010 och Microsoft® SharePoint 2013 är föråldrad för Experience Manager 6.5. | Ej tillämpligt |

## Kända fel {#known-issues}

<!--

* (For JBoss on Microsoft Windows only) To continue using the Create PDF service on [!DNL AEM Forms on JEE], download [omniORB_4.1.1_x86_win32_vc10.zip](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/omniORB_4.1.1_x86_win32_vc10.zip) from Software Distribution, extract and copy the folder available in the Zip file to the following location:
`[AEM Forms Installation]\Adobe\Adobe_Experience_Manager_Forms\jboss\standalone\svcnative\CommonNatives\lib`

* As [!DNL Microsoft Windows Server 2019] does not support [!DNL MySQL 5.7] and [!DNL JBoss EAP 7.1], [!DNL Microsoft Windows Server 2019] does not support turnkey installations for [!DNL AEM Forms 6.5.10.0].

-->

* Om du uppgraderar din [!DNL Experience Manager]-instans från version 6.5 till version 6.5.10.0 kan du visa `RRD4JReporter`-undantag i `error.log`-filen. Starta om instansen för att lösa problemet.

* Om du installerar [!DNL Experience Manager] 6.5 Service Pack 10 eller ett tidigare Service Pack på [!DNL Experience Manager] 6.5 tas körtidskopian av din resurskräddarsydda arbetsflödesmodell (skapad i `/var/workflow/models/dam`) bort.
Om du vill hämta körtidskopian rekommenderar Adobe att du synkroniserar designtidskopian av den anpassade arbetsflödesmodellen med körtidskopian med hjälp av HTTP API:
   `<designModelPath>/jcr:content.generate.json`.

* Användare kan byta namn på en mapp i en hierarki i [!DNL Assets] och publicera en kapslad mapp till [!DNL Brand Portal]. Mappens namn uppdateras dock inte i [!DNL Brand Portal] förrän rotmappen publiceras på nytt.

* När en användare väljer att konfigurera ett fält för första gången i ett adaptivt formulär visas inte alternativet att spara en konfiguration i egenskapsläsaren. Om du väljer att konfigurera ett annat fält i det adaptiva formuläret i samma redigerare åtgärdas problemet.

* Följande fel och varningsmeddelanden kan visas under installationen av Experience Manager 6.5.x.x:
   * &quot;När Adobe Target-integreringen har konfigurerats i Experience Manager med Target Standard API (IMS-autentisering) skapas felaktiga erbjudandetyper när Experience Fragments exporteras till Target. I stället för att skriva&quot;Experience Fragment&quot;/källa&quot;Adobe Experience Manager&quot; skapar Target flera erbjudanden med typen&quot;HTML&quot;/källa&quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Validering på serversidan av adaptiva formulär misslyckas när sammanställningsfunktioner som SUM, MAX och MIN används (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Aktiveringspunkten i en interaktiv Dynamic Media-bild syns inte när du förhandsvisar mediefilen via Shoppable Banner Viewer.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tidsgränsen överskreds i väntan på att reg.ändringen skulle slutföras utan registrering.

## OSGi-paket och innehållspaket som ingår {#osgi-bundles-and-content-packages-included}

Följande textdokument innehåller en lista över de OSGi-paket och innehållspaket som ingår i [!DNL Experience Manager] 6.5.10.0:

* [Förteckning över OSGi-paket som ingår i Experience Manager 6.5.10.0](assets/65100_bundles.txt)

* [Förteckning över innehållspaket som ingår i Experience Manager 6.5.10.0](assets/65100_packages.txt)

## Begränsade webbplatser {#restricted-sites}

Dessa webbplatser är bara tillgängliga för kunder. Om du är kund och behöver åtkomst kontaktar du din kontoansvarige på Adobe.

* [Nedladdning av produkt på licensing.adobe.com](https://licensing.adobe.com/)
* Se [hur du kontaktar Adobe kundtjänst](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5 Versionsinformation](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] produktsida](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* [Prenumerera på produktuppdateringar med Adobe prioritet](https://www.adobe.com/subscription/priority-product-update.html)

