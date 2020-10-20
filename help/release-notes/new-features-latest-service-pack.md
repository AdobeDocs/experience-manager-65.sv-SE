---
title: Nyheter i Adobe Experience Manager 6.5 Service Pack 6
description: Nyheter i Adobe Experience Manager 6.5 Service Pack 6
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 750e3729a33718d54dca8b2514468d4a40910d4c
workflow-type: tm+mt
source-wordcount: '2534'
ht-degree: 0%

---


# Nyheter i Adobe Experience Manager 6.5 Service Pack 6 {#aem-whats-new-service-pack-6}

Adobe Experience Manager 6.5 Service Pack innehåller nya funktioner, förbättringar som kunden efterfrågat samt prestanda-, stabilitets- och säkerhetsförbättringar varje kvartal. Den kvartalsvisa tillgängligheten gör det enkelt att komma åt och anta nya funktioner och innovationer.

I den här artikeln beskrivs de funktioner som ingår i det senaste 6.5 Service Pack-versionen, [de viktigaste funktionerna i det tidigare 6.5 Service Pack-](#key-features-previous-service-packs)paketet [och några av de](#key-releases-since-last-sp) viktigaste versionerna sedan Experience Manager 6.5.5.0-versionen.

## Adobe [!DNL Experience Manager] Sites {#aem-sites}

### Tillgänglighet för åtgärden Sidflyttning i asynkront läge {#page-move-asynchronous}

Åtgärden Flytta sida är nu tillgänglig i asynkront läge. Förutom omedelbar körning kan du schemalägga åtgärden Sidflyttning för senare körning.

## [!DNL Dynamic Media] {#dynamic-media}

### Invalidera cachelagrat CDN-innehåll {#invalidate-cdn-cached-content}

Du kan nu använda [!DNL Dynamic Media] användargränssnittet för att göra Cachelagrat innehåll i Content Delivery Network (CDN) ogiltigt. Därför är de uppdaterade resurserna tillgängliga direkt i stället för att vänta på att cachen ska upphöra att gälla. Du kan göra CDN ogiltig genom att:

* Skapa en CDN-invalideringsmall: Välja resurser och formulärassocierade mallbaserade URL:er

* Välja resurser och tillhörande förinställningar med resursväljaren

* Lägga till fullständiga resurs-URL:er

### Selektiv publicering av resurser till [!DNL Experience Manager] och [!DNL Dynamic Media] {#selective-publishing}

Du kan nu välja att selektivt publicera eller avpublicera resurser till antingen [!DNL Experience Manager] eller [!DNL Dynamic Media] med hjälp av [!UICONTROL Quick Publish] eller [!UICONTROL Manage Publication] guide. Du kan också ange `Publish` - eller `Unpublish` -läge på mappnivå.

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

### Förbättrad tillgänglighet {#accessibility-assets-6560}

* **Förbättrat fokus på användargränssnittet vid tangentbordsnavigering**, till exempel med fokus på:

   * `x` i [!UICONTROL Version Preview] dialogruta för en resurs i [!UICONTROL Timeline].

   * Alternativ för användargränssnitt som kan användas.

   * E-postfält i [!UICONTROL Share Link] dialogrutan och fält för att lägga till stängd användargrupp på [!UICONTROL Permission] mappfliken [!UICONTROL Properties].

* **Förbättrade funktioner med tangentbordstangenter**

   Användare kan använda tangentbordstangenter för att dra kontroller i Formulärredigeraren för metadata i bläddringsläge för skärmläsare.

* **Förbättrad användbarhet för skärmläsaranvändare** på grund av följande:

   * Skärmläsare berättar syftet med video- och ljudspelare.

   * Skärmläsare meddelar syftet med alternativen i användargränssnittet att ta bort de taggar som har valts med [!UICONTROL Tags selection dialog] en resurs [!UICONTROL Properties].

   * Skärmläsare meddelar radrubrikerna och radobjekten i tabeller så att användarna vet vilka poster som tillhör samma rad.

   * Beskrivande och meningsfull sidrubrik för söksidan.

   * Skärmläsare meddelar alternativen på sökfilterpanelen som expanderbara dragspelspaneler.

### Andra förbättringar i Assets {#other-enhancements-assets-6560}

* Användargrupper som är associerade med mappar (privata och icke-privata) tas nu bort från databasen när mapparna [tas](/help/assets/private-folder.md#delete-private-folder)bort. Befintliga redundanta, överblivna, oanvända och autogenererade användargrupper kan rensas bort från databasen med JMX.

## [!DNL Adobe Experience Manager Forms] {#aem-forms}

### Fyll i ett anpassat formulär i förväg på klienten {#prefill-merge-data-at-client}

När du fyller i ett adaptivt formulär i förväg sammanfogar servern data med ett adaptivt formulär och skickar det ifyllda formuläret till dig. [!DNL Experience Manager Forms] Som standard utförs datasammanfogningsåtgärden på servern.
Nu kan du konfigurera [!DNL Experience Manager Forms] servern så att den [utför datasammanfogningsåtgärden på klienten](../../help/forms/using/prepopulate-adaptive-form-fields.md) i stället för på servern. Det minskar avsevärt den tid som krävs för att förifylla och återge anpassningsbara formulär.

### Integrering av formulärdatamodell med RESTful API:er på en server med tvåvägs SSL-implementering {#fdm-integration-rest-apis-two-way-ssl}

[!DNL Experience Manager Forms] formulärdatamodellen kan nu [integreras med RESTful-API:er på en server som har en tvåvägs SSL implementerad på den](../../help/forms/using/configure-data-sources.md).


### Stöd för [!DNL Adobe Sign] texttaggar har lagts till i den automatiserade Forms Conversion Service {#sign-integration-acroform-afcs}

Om ett AcroForm innehåller [!DNL Adobe Sign] texttaggar identifieras och representeras dessa fält som [!DNL Adobe Sign] fält i det adaptiva formuläret som konverterats med [!DNL Automated Forms Conversion service]. En signerare kan fylla i sådana fält medan han/hon signerar det anpassade formuläret.

### Support to convert colored PDF forms to adaptive forms {#colored-PDF-forms}

Du kan använda [!DNL Automated Forms Conversion service] för att konvertera färgad PDF forms till adaptiva formulär.

### Stöd för SMB 2- och SMB 3-protokoll {#smb-support}

[!DNL Experience Manager Forms] har nu stöd för SMB 2- och SMB 3-protokoll.

### Förbättrad cachning för översatta adaptiva formulärsidor {#enhanced-caching-translated-adaptive-forms}

Du kan nu ange [språkområde som en väljare i den anpassningsbara formulärets URL i stället för ett argument i en anpassad formulär-URL](../../help/forms/using/supporting-new-language-localization.md). Det hjälper till att cachelagra översatta adaptiva formulär på [!DNL Experience Manager Dispatcher]. Det gick inte att cachelagra översatt adaptiv form i tidigare versioner. Mer information om hur du konfigurerar cachning för att använda språkområdet som väljare i URL:en för anpassningsbara formulär finns i [Konfigurera cacheminne för anpassningsbara formulär vid dispatcher](../../help/forms/using/configure-adaptive-forms-cache.md).

### Spara utdata från formulärdatamodelltjänst till en variabel {#save-fdm-service-to-variable}

Med formulärdatamodellen kan du spara utdata från en formulärdatamodelltjänst till en variabel. [!DNL Experience Manager Forms] mappar nu automatiskt typen av formulärdatamodelltjänst till variabeltypen.

### Bifoga flera filer för komponenten Bifogad fil {#attach-multiple-files}

Nu kan du [bifoga flera filer](../../help/forms/using/introduction-forms-authoring.md) till [!UICONTROL File Attachment] komponenten i adaptiva formulär.



## Viktiga funktioner i tidigare Experience Manager 6.5 Service Packs {#key-features-previous-service-packs}

### Experience Manager Sites {#aem-sites-previous-service-packs}

#### Förbättringar av hjälpmedel (6.5.5.0) {#accessibility-sites}

* Förbättrad felrapportering genom att lägga till textinformation.

* Förbättrat fokus på användargränssnittet vid tangentbordsnavigering.

* Förbättrat kontrastförhållande för olika element i användargränssnittet.

* Förbättrad konsekvens för alt-attribut för sidbilder.

* Förbättrad enhetlighet i ARIA-etiketter (Accessible Rich Internet Applications).

* Förbättrade NVDA-funktioner (Non-Visual Desktop Access).

* Förbättrat stöd för skärmläsare.

#### Andra viktiga förbättringar (6.5.5.0) {#other-enhancements-sites}

* Anonym åtkomst till CRXDE Lite är inte tillåten för att öka säkerheten. I stället dirigeras användarna till inloggningsskärmen. Se [Utveckla med CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

* När du kopierar eller klistrar in ett sidträd kan du nu välja att antingen klistra in rotsidan eller klistra in rotsidan med undersidorna i trädet.

* [!DNL Adobe Experience Manager Experience Fragments] som exporteras till [!DNL Adobe Target] arbetsytor visas nu som unika erbjudandetyper och erbjudandekällor i [!DNL Target].

* Multi Site Manager - Publiceringsutlösaren tar nu bort en komponent från den publicerade sidan om en komponent tas bort från källsidan.

* Multi Site Manager - När namnet på en lokal komponent i en [!UICONTROL Live Copy] är identiskt med namnet på en komponent i en plan och komponenten rullas ut från planen, `_msm_moved` läggs nu termen till i namnet på den lokala komponenten.

#### Förbättringar av formatsystemet (6.5.4.0) {#style-system-enhancements}

Nu kan du välja format i komponentdialogrutan med det förbättrade formatsystemet.

#### Prestandaförbättringar inom olika områden (6.5.4.0) {#performance-improvements}

* Minskad tid för att läsa in och initiera ContextHub inom en plats (`contexthub.kernel.js`). Det ger snabbare sidinläsning under ett webbplatsbesök.

* Förkorta tiden för uppdatering av en sida efter att du dragit [!DNL Experience Fragments] till [!DNL Sites] sidredigeraren.

* Förkorta inläsningstiden för poster på en [!DNL Sites] sida med fler än 200 live-kopior i **[!UICONTROL Live Copy Overview]**.

* Förbättrad hantering av ofullständiga eller ogiltiga URL:er. Sådana URL-adresser kan göra mallredigeraren långsam.

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}

#### Tillgänglighetsförbättringar i [!DNL Assets] (6.5.5.0) {#assets-accessibility}

[!DNL Experience Manager Assets] är nu mer tillgängligt i enlighet med Web Content Accessibility Guidelines (WCAG). Tillgängligheten har förbättrats på grund av följande förbättringar:

* Många gränssnittselement, kontroller, sidor och dialogrutor är anpassade för skärmläsare.

* Många gränssnittselement, kontroller och inmatningsfält är tillgängliga via tangentbordet.

* Färgen och kontrasten i vissa element i användargränssnittet uppdateras så att användare med begränsad syn eller användare utan att uppfatta färger kan särskilja dessa element i användargränssnittet. Färgen på stjärngraderingsikonerna (t.ex. i [!UICONTROL Rating] avsnittet på [!UICONTROL Advanced] fliken i resursen [!UICONTROL Properties] eller i kortvyn) ändras för lämplig kontrast.

   ![Klassificeringsikoner med förbättrad kontrast](assets/star-rating-icons.png)

#### Förbättrad undantagshantering (6.5.5.0) {#exception-handling}

[!DNL Assets] användargränssnittets flöde har bättre undantagshantering. Om en resurs inte har någon typ för sin dimension registreras det observerade undantaget i loggfilerna.

#### Stöd för 3D-resurser i [!DNL Dynamic Media] (6.5.5.0) {#support-for-3d}

Stöd för 3D-bilder i [!DNL Dynamic Media] gör att man kan publicera och lägga in 3D-material på webbsidor och i tillämpningar. Supporten omfattar:

* Publicera vanliga 3D-resursformat och generera en resurs-URL som kan användas på webbsidor och andra program.

* Ett 3D Web Viewer från [!DNL Adobe Dimension]vilken du interaktivt kan visa publicerade 3D-resurser.

* Publicera och visa vanliga 3D-resurser på [!DNL Experience Manager Sites] sidor med [!DNL Sites] WCM-komponenten.

#### Konfigurera [!DNL Experience Manager Assets] med [!DNL Brand Portal] (6.5.4.0) {#configure-assets-bp}

Auktoriseringskanalen mellan [!DNL Experience Manager Assets] och [!DNL Brand Portal] ändras. Tidigare [!DNL Brand Portal] konfigurerades i Classic UI via äldre OAuth-gateway, som använder JWT-tokenutbyte för att erhålla en IMS-åtkomsttoken för auktorisering. [!DNL Experience Manager Assets] har nu konfigurerats med [!DNL Brand Portal] via Adobe I/O, som anskaffar en IMS-token för auktorisering av din [!DNL Brand Portal] klientorganisation.

Vilka steg som ska konfigureras [!DNL Experience Manager Assets] med [!DNL Brand Portal] varierar beroende på [!DNL Experience Manager] version, om du konfigurerar för första gången eller om du uppgraderar befintliga konfigurationer. Mer information finns i [Konfigurera Experience Manager Assets with Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) .

#### Tillgänglighetsförbättringar (6.5.4.0) {#accessibility-enhancements}

[!DNL Experience Manager Assets] innehåller följande tillgänglighetsförbättringar:

* Piltangenter på tangentbordet kan användas för att flytta och panorera områden i zoomade bilder. Mer information finns i [Förhandsgranska resurser endast](../assets/managing-assets-touch-ui.md#previewing-assets)med tangentbordstangenter.

* Kryssrutorna för blandat läge (där kryssrutorna på första nivån inte markeras och genomstrykas) på panelen Filter kan läsas av skärmläsare om du inte markerar alla kapslade alternativ.

* Begränsningar för datum- och tidsformat finns i fältetiketter för datumfält, så att användarna kan ange datumet i korrekt format med tangentbordet.
Till exempel, `On Time (MM-DD-YYYY HH:mm)`. Här är MM månad i tvåsiffrigt format, YYYY är år, DD är dag i tvåsiffrigt format, HH är timme i 24-timmars militärt format och mm är minut.

* Skärmläsare meddelar nu att `X` symbolen tar bort de markerade taggarna tillsammans med antalet markerade taggar.

#### Sorterbar kolumn för Skapat datum för resurser i listvyn (6.5.3.0) {#sortable-date-created-column}

En ny sorterbar kolumn för skapat datum för resurser läggs till i DAM-listvyn och i resurssökningsresultat i listvyn.

![Sorterbar kolumn för skapat datum](assets/asset-created-date.png)

#### Visuell sökning efter [!DNL Adobe Experience Manager Assets] (6.5.2.0) {#visual-search}

[!DNL Assets] -användare kan söka visuellt liknande bilder. Experience Manager visar de smarta taggade bilder från DAM-databasen som liknar den bild som användaren har valt. Se [Visuell sökning](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

#### Smart Imaging for Dynamic Media {#smart-imaging}

Smart bildbehandling använder varje användares unika visningsegenskaper för att automatiskt leverera rätt bilder som är optimerade för sin upplevelse, vilket ger bättre prestanda och engagemang. Smart bildbehandling fungerar med befintliga bildförinställningar och använder intelligens under de sista millisekunderna i leveransen för att ytterligare minska bildfilens storlek baserat på webbläsarens eller nätverkets anslutningshastighet. Se [Smart bildbehandling](../assets/imaging-faq.md).

#### Smart beskärning i videoprofiler för Dynamic Media (6.5.3.0) {#smart-crop-video}

Smart beskärning för video - en valfri funktion i videoprofiler - är ett verktyg som använder kraften i artificiell intelligens i Adobe Sensei för att automatiskt upptäcka och beskära fokalpunkten i adaptiv video eller progressiv video som du har överfört, oavsett storlek. Se [Använda smart beskärning i videoprofiler](../assets/video-profiles.md).

### Experience Manager Forms {#aem-forms-previous-service-packs}

#### Anpassa Adobe Experience Manager Inbox-kolumnerna (6.5.5.0){#customize-aem-inbox-columns}

Du kan anpassa en [!DNL Experience Manager] inkorg om du vill ändra standardtiteln för en kolumn, ändra ordningen på en kolumns position och visa ytterligare kolumner baserat på data i ett arbetsflöde. Medlemmar i `administrators` eller `workflow-administrators` grupper kan anpassa kolumnerna. Mer information finns i [Administratörskontroll](../sites-authoring/inbox.md#inbox-admin-control).

![Anpassa Experience Manager-inkorgskolumner](assets/customize-columns.gif)

#### Spara interaktiv kommunikation som ett utkast (6.5.5.0) {#save-as-draft}

Du kan använda agentgränssnittet för att spara ett eller flera utkast för varje interaktiv kommunikation och hämta utkastet senare för att fortsätta arbeta med det. Du kan ange olika namn för varje utkast för att identifiera det. Mer information finns i [Spara interaktiv kommunikation som ett utkast](../forms/using/prepare-send-interactive-communication.md#save-as-draft).

![Spara som utkast](assets/save-as-draft.gif)

#### [!DNL Oracle WebLogic] stöd för programservrar (6.5.5.0) {#weblogic-support}

Adobe Experience Manager Forms har lagt till stöd [!DNL Oracle WebLogic 12] för Adobe Experience Manager Forms på JEE. Du kan uppgradera från en tidigare version eller konfigurera en ny Experience Manager 6.5 Forms på JEE-servern på [!DNL Oracle WebLogic] 12.2.1.4 och senare. Senare motsvarar de mindre versionsändringarna, där x i 12.2.1.x ersätts med ett versionsnummer.

#### Förbättringar av hjälpmedel (6.5.5.0) {#accessibility-improvements}

Adobe Experience Manager Forms innehåller följande tillgänglighetsförbättringar:

* När en användare förhandsgranskar ett anpassat formulär som ett HTML-formulär behåller [!UICONTROL Scribble Signature] fältet tabbfokus.

* Felmeddelandena som visas när du skickar ett anpassat formulär innehåller nu `aria-describedBy` attributet . Attributet är kopplat till fälten som refereras i felmeddelandet. Attributet `aria-describedby` anger ID:n för elementen som beskriver objektet. Det hjälper till att skapa en relation mellan widgetar eller grupper och text som beskriver dem.

* Om ett anpassningsbart formulär har obligatoriska fält ställs det obligatoriska attributet in på `True` för sådana fält i ARIA-hjälpmedelsschemat.

#### X-509 certifikatbaserad autentisering för SOAP-baserade webbtjänster i formulärdatamodell (6.5.5.0) {#x509-based-authentication-soap}

Formulärdatamodellen har nu stöd för X-509-certifikatbaserad autentisering när SOAP-webbtjänster används som datakälla. Mer information finns i [Konfigurera SOAP-webbtjänster](../forms/using/configure-data-sources.md#configure-soap-web-services).

#### Andra viktiga förbättringar (6.5.5.0) {#other-improvements}

* Experience Manager 6.5 Forms on JEE Document Security baseras nu på [!DNL Apache Struts 2].

* Stöd för [!DNL Oracle Real Applications Cluster (RAC) 19c].

#### Generera utskrifter i Experience Manager Forms-arbetsflöden (6.5.4.0) {#generate-printable-output}

Med arbetsflödessteget Generera utskrift kan du integrera en källmallsfil med en datafil. Tack vare den här integreringen kan du skriva ut eller spara olika kopior av mallfilen. Steget genererar PCL-, PostScript-, ZPL-, IPL-, TPCL- eller DPL-utdata. Mer information om den här funktionen finns i [Forms-centrerat arbetsflöde i OSGi - Step Reference](../forms/using/aem-forms-workflow-step-reference.md).

![Generera utdata för utskrift](assets/generate-print-output-step.gif)

#### Stöd för flera kolumner för adaptiva formulär och interaktiv kommunikation i layoutläge (6.5.4.0) {#multi-column-adaptive-forms}

Nu kan du definiera antalet kolumner för en panel i adaptiva formulär och interaktiv kommunikation. Växla till layoutläge om du vill använda det nya alternativet med flera kolumner. Mer information finns i [Använda layoutläget för att ändra storlek på komponenter](../forms/using/resize-using-layout-mode.md).

![Flerspaltig layout](assets/multi-column-layout.gif)

#### Anpassningar av Inkorgen för Experience Manager (6.5.4.0) {#aem-inbox}

Med det nya alternativet Admin Control kan administratörer:

* Anpassa rubriktext och logotyp.

* Styr visningen av navigeringslänkar i sidhuvudet.

Alternativet Administratörskontroll är bara synligt för medlemmarna i `administrators` eller `workflow-administrators` gruppen. Mer information om den här funktionen finns i [Inkorgen](../sites-authoring/inbox.md).

#### RTF-stöd i HTML5-formulär (6.5.4.0) {#rich-text-support}

Konvertera ett textfält i ett XFA-formulär till ett RTF-fält i ett HTML5-formulär. Mer information finns i [Utforma formulärmallar för HTML5-formulär](../forms/using/designing-form-template.md).

#### Tillgänglighetsförbättringar (6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience Manager Forms innehåller följande tillgänglighetsförbättringar:

* Skärmläsarna meddelar kryssrutor, länkar, datumväljare och datuminmatningsfält korrekt i ett anpassat formulär.

* Varje sida i ett adaptivt formulär innehåller nu en rubrik och en huvudlandmärkesetikett.

#### Dela och begär åtkomst till inkorgsobjekt från användare av Experience Manager Forms (6.5.3.0) {#share-request-access}

Du kan dela dina inkorgsobjekt med en annan användare. När en annan användare får tillgång till dina inkorgsobjekt kan användaren göra anspråk på och vidta lämpliga åtgärder för delade objekt. På samma sätt kan du begära åtkomst till inkorgsobjekt från andra användare. Se [Dela och begära åtkomst till inkorgsobjekt för en användare](../forms/using/configure-shared-queues-osgi.md).

#### Konfigurera inställningar utanför kontoret för inkorgsobjekt för användare av Experience Manager Forms (6.5.3.0) {#configure-out-of-office}

Om du tänker vara utanför kontoret kan du ange vad som ska hända med artiklar som har tilldelats dig för den perioden.
Du kan ange startdatum och -tid och slutdatum och sluttid så att dina inställningar som inte är på kontoret börjar gälla. Du kan ange en standardperson som alla dina objekt skickas till. Se [Konfigurera inställningar](../forms/using/configure-out-of-office-settings.md)för frånvaro.

#### Generera flera interaktiva dokument med Batch API för Experience Manager Forms (6.5.3.0) {#generate-multiple-ic}

Du kan använda batch-API:t för att skapa flera interaktiva dokument från en mall. Mallen är en interaktiv kommunikation utan data. Batch-API:t kombinerar data med en mall för att skapa en interaktiv kommunikation. API:t är användbart vid massproduktion av interaktiv kommunikation. Till exempel telefonräkningar, kreditkortsutdrag för flera kunder. Se [Generera flera interaktiva dokument med hjälp av API:t](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)för gruppbearbetning.

## Viktiga versioner sedan Adobe Experience Manager 6.5 SP5 {#key-releases-since-last-sp}

Mellan 4 juni 2020 och 3 september 2020 släppte Adobe följande, förutom servicepaket och kumulativa korrigeringspaket:

* [Programdistributionsportalen](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) är tillgänglig för nedladdning av Experience Manager Service Pack, kumulativa korrigeringspaket, snabbkorrigeringar och funktionspaket.

* [!DNL Adobe Experience Manager as a cloud service] [2020.7.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/release-notes/release-notes-2020-7-0.html) och [2020.8.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

* [Experience Manager desktop app 2.0 (2.0.3.2)](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html).

* [Experience Manager Screens: Feature Pack 20208](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202008.html)

>[!MORELIKETHIS]
>
>* [Adobe Experience Manager 6.5 - dokumentation](../user-guide/home.md)
>* [Allmän versionsinformation om Adobe Experience Manager 6.5](release-notes.md)
>* [Versionsinformation om Service Pack för Adobe Experience Manager 6.5](sp-release-notes.md)

