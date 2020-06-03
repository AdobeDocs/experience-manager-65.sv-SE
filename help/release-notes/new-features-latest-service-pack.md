---
title: Nyheter i Adobe Experience Manager 6.5 Service Pack 5
description: Nyheter i Adobe Experience Manager 6.5 Service Pack 5
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: cc423a199e860429e85895690f6c1a81c20d1a19
workflow-type: tm+mt
source-wordcount: '1845'
ht-degree: 2%

---


# Nyheter i AEM 6.5 Service Pack 5 {#aem-whats-new-service-pack-5}

Service Pack för Adobe Experience Manager 6.5 innehåller nya funktioner, förbättringar som kunderna efterfrågat, prestanda och stabilitet. Förbättringarna görs kvartalsvis. Leveransmodellen varje kvartal gör det enklare att komma åt och använda nya funktioner och innovationer.

I den här artikeln beskrivs de funktioner som ingår i det senaste 6.5 Service Pack-versionen, [de viktigaste funktionerna i det tidigare 6.5 Service Pack-paketet](#key-features-previous-service-packs)och några av de [viktigaste versionerna sedan Experience Manager 6.5.4.0](#key-features-sice-sp3) -versionen.

## AEM Sites {#aem-sites}

### Förbättringar av hjälpmedel {#accessibility-sites}

* Förbättrad felrapportering genom att lägga till textinformation

* Förbättrat gränssnittsfokus under tangentbordsnavigering

* Förbättrad textkontrast (luminiscens)

* Förbättrad konsekvens för alt-attribut för sidbilder

* Förbättrad enhetlighet i ARIA-etiketter (Accessible Rich Internet Applications)

* Förbättrade NVDA-funktioner (Non-Visual Desktop Access)

* Förbättrat stöd för skärmläsare

### Andra viktiga förbättringar {#other-enhancements-sites}

* När du kopierar eller klistrar in ett sidträd kan du nu välja att antingen klistra in rotsidan eller klistra in rotsidan med undersidorna i trädet.

* AEM Experience Fragments som exporteras till Adobe Target-arbetsytor visas nu som unika erbjudandetyper och erbjudandekällor i [!DNL Target].

* Multi Site Manager - Publiceringsutlösaren tar nu bort en komponent från den publicerade sidan om en komponent tas bort från källsidan.

* Multi Site Manager - När namnet på en lokal komponent i en LiveCopy är identiskt med namnet på en komponent i utkastet och komponenten rullas ut från utkast, läggs termen _msm_move till i namnet på den lokala komponenten.

## AEM Assets {#aem-assets}

### Tillgänglighetsförbättringar i resurser {#assets-accessibility}

[!DNL Adobe Experience Manager] Resursfunktionerna är nu mer tillgängliga i enlighet med Web Content Accessibility Guidelines (WCAG). Tillgängligheten har förbättrats inom följande områden:

* Element, kontroller, sidor och dialogrutor i användargränssnittet är anpassade för skärmläsare.

* Element, kontroller och inmatningsfält i användargränssnittet är tillgängliga via tangentbordet.

* Färgändring och kontrast för vissa bilder som ska kunna urskiljas av användare med begränsad syn och utan att de uppfattas av färger. Färgen på stjärngraderingsikonerna (t.ex. i [!UICONTROL Rating] avsnittet på [!UICONTROL Advanced] fliken i resursen [!UICONTROL Properties] eller i kortvyn) ändras för lämplig kontrast.

![stjärngraderingsikonernas färg har ändrats för att förbättra kontrasten](assets/star-rating-icons.png)

### Förbättrad undantagshantering {#exception-handling}

Resursens användargränssnittsflöde har bättre undantagshantering. Tidigare, om en tillgång inte hade rätt typ för sin dimension, observerades ett undantag som fångades utan spår i loggar. Detta beteende har ändrats och alla undantag fångas i loggar.

## [!DNL Dynamic Media] {#dynamic-media}

### Stöd för 3D i [!DNL Dynamic Media] {#support-for-3d}

Med 3D-stödet i kan kunder [!DNL Dynamic Media] nu publicera och lägga till 3D-innehåll på webbsidor och i tillämpningar. Den innehåller följande uppgifter:

* Publicering av vanliga 3D-resursformat för att generera en resurs-URL.

* Interaktiv visning av publicerade 3D-resurser med ett nytt 3D Web Viewer som finns i [!DNL Dynamic Media] visningsbiblioteket, som drivs av Adobe Dimension.

* 3D-publicering och -visning på [!DNL Experience Manager Sites] sidor med [!DNL Sites] WCM-komponenten.

## AEM Forms {#aem-forms}

### Anpassa kolumnerna i AEM Inbox {#customize-aem-inbox-columns}

Du kan anpassa en AEM-inkorg om du vill ändra standardtiteln för en kolumn, ändra ordning på en kolumns position och visa ytterligare kolumner baserat på data i ett arbetsflöde. Du ska vara medlem av `administrators` eller `workflow-administrators` grupp för att anpassa kolumnerna.

![Anpassa AEM Inbox-kolumner](assets/customize-columns.gif)

### Spara interaktiv kommunikation som utkast {#save-as-draft}

Du kan använda agentgränssnittet för att spara ett eller flera utkast för varje interaktiv kommunikation och hämta utkastet senare för att fortsätta arbeta med det. Du kan ange olika namn för varje utkast för enklare identifiering.

![Spara som utkast](assets/save-as-draft.gif)

### [!DNL Oracle WebLogic] programserverstöd {#weblogic-support}

AEM Forms har lagt till stöd för AEM Forms [!DNL Oracle WebLogic 12] på JEE. Du kan uppgradera från en tidigare version eller konfigurera nya AEM 6.5-formulär på JEE-servern den [!DNL Oracle WebLogic] 12.2.1.4 och senare. Senare motsvarar de mindre versionsändringarna, där x i 12.2.1.x ersätts med ett versionsnummer.

### Förbättringar av hjälpmedel {#accessibility-improvements}

AEM Forms innehåller följande tillgänglighetsförbättringar:

* När en användare förhandsgranskar ett anpassat formulär som ett HTML-formulär behåller [!UICONTROL Scribble Signature] fältet tabbfokus.

* Felmeddelandena som visas när du skickar ett anpassat formulär innehåller nu `aria-describedBy` attributet . Attributet är kopplat till fälten som refereras i felmeddelandet. Attributet `aria-describedby` anger ID:n för elementen som beskriver objektet. Det hjälper till att skapa en relation mellan widgetar eller grupper och text som beskriver dem.

* Om ett anpassningsbart formulär har obligatoriska fält ställs det obligatoriska attributet in på `True` för sådana fält i ARIA-hjälpmedelsschemat.

### X-509 certifikatbaserad autentisering för SOAP-baserade webbtjänster i formulärdatamodell {#x509-based-authentication-soap}

Formulärdatamodellen har nu stöd för X-509-certifikatbaserad autentisering när SOAP-webbtjänster används som datakälla.

### Andra viktiga förbättringar {#other-improvements}

* AEM 6.5 Forms on JEE Document Security baseras nu på [!DNL Apache Struts 2].

* Stöd för [!DNL Oracle Real Applications Cluster (RAC) 19c].

## Viktiga funktioner i tidigare AEM 6.5 Service Packs {#key-features-previous-service-packs}

### AEM Sites {#aem-sites-previous-service-packs}

#### Förbättringar av formatsystemet (6.5.4.0) {#style-system-enhancements}

Nu kan du välja format i komponentdialogrutan med det förbättrade formatsystemet.

#### Prestandaförbättringar inom olika områden (6.5.4.0) {#performance-improvements}

* Minskad tid för inläsning och initiering av ContextHub inom en plats (`contexthub.kernel.js`). Det ger snabbare sidinläsning under ett webbplatsbesök.

* Förkorta tiden för uppdatering av en sida efter att Experience Fragments har dragits till sidredigeraren Platser.

* Ökade inläsningstiden för poster på en Sites-sida med mer än 200 live-kopior i **[!UICONTROL Live Copy Overview]**.

* Förbättrad hantering av ofullständiga eller ogiltiga URL:er. Sådana URL-adresser kan göra mallredigeraren långsammare.

### AEM Assets {#aem-assets-previous-service-packs}

#### Configure AEM Assets with Brand Portal (6.5.4.0) {#configure-assets-bp}

Auktoriseringskanalen mellan AEM Assets och Brand Portal har ändrats. Tidigare konfigurerades varumärkesportalen i Classic UI via äldre OAuth Gateway, som använder JWT-tokenutbyte för att erhålla en IMS Access-token för auktorisering. AEM Assets har nu konfigurerats med Brand Portal via Adobe I/O, som anskaffar en IMS-token för auktorisering av din klient för varumärkesportalen.

Stegen för att konfigurera AEM Assets med Brand Portal är olika beroende på din AEM-version, om du konfigurerar för första gången eller uppgraderar befintliga konfigurationer. Mer information finns i [Konfigurera AEM-resurser med varumärkesportalen](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) .

#### Tillgänglighetsförbättringar (6.5.4.0) {#accessibility-enhancements}

Experience Manager Assets innehåller följande tillgänglighetsförbättringar:

* Piltangenter på tangentbordet kan användas för att flytta och panorera områden i zoomade bilder. Mer information finns i [Förhandsgranska resurser endast](../assets/managing-assets-touch-ui.md#previewing-assets)med tangentbordstangenter.

* Kryssrutorna för blandat läge (där kryssrutorna på första nivån inte markeras och genomstrykas) på panelen Filter kan läsas av skärmläsare om du inte markerar alla kapslade alternativ.

* Begränsningar för datum- och tidsformat finns i fältetiketter för datumfält, så att användarna kan ange datumet i korrekt format med tangentbordet.

   Till exempel, `On Time (MM-DD-YYYY HH:mm)`. Här är MM månad i tvåsiffrigt format, YYYY är år, DD är dag i tvåsiffrigt format, HH är timme i 24-timmars militärt format och mm är minut.

* Symbolen på knappen för att ta bort de markerade taggarna visas nu för skärmläsare tillsammans med antalet markerade taggar. `X`

#### Visuell sökning efter AEM Assets (6.5.2.0) {#visual-search}

Resurser som användare kan söka efter visuellt liknande bilder. AEM visar smarta taggade bilder från DAM-databasen som liknar den användarvalda bilden. Se [Visuell sökning](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

#### Smart Imaging for Dynamic Media {#smart-imaging}

Smart bildbehandling använder varje användares unika visningsegenskaper för att automatiskt leverera rätt bilder som är optimerade för sin upplevelse, vilket ger bättre prestanda och engagemang. Smart bildbehandling fungerar med befintliga bildförinställningar och använder intelligens under de sista millisekunderna i leveransen för att ytterligare minska bildfilens storlek baserat på webbläsarens eller nätverkets anslutningshastighet. Se [Smart bildbehandling](../assets/imaging-faq.md).

#### Smart beskärning i videoprofiler för Dynamic Media (6.5.3.0) {#smart-crop-video}

Smart beskärning för video - en valfri funktion i videoprofiler - är ett verktyg som använder kraften i artificiell intelligens i Adobe Sensei för att automatiskt upptäcka och beskära fokalpunkten i alla adaptiva videoklipp och progressiva videoklipp som du har överfört, oavsett storlek. Se [Använda smart beskärning i videoprofiler](../assets/video-profiles.md).

### AEM Forms {#aem-forms-previous-service-packs}

#### Generera utskrifter i arbetsflöden för AEM Forms (6.5.4.0) {#generate-printable-output}

Med arbetsflödessteget Generera utskrift kan du integrera en källmallsfil med en datafil. Tack vare den här integreringen kan du skriva ut eller spara olika kopior av mallfilen. Steget genererar PCL-, PostScript-, ZPL-, IPL-, TPCL- eller DPL-utdata. Mer information om den här funktionen finns i [Formulärcentrerat arbetsflöde i OSGi - stegreferens](../forms/using/aem-forms-workflow-step-reference.md).

![Generera utdata för utskrift](assets/generate-print-output-step.gif)

#### Stöd för flera kolumner för adaptiva formulär och interaktiv kommunikation i layoutläge (6.5.4.0) {#multi-column-adaptive-forms}

Nu kan du definiera antalet kolumner för en panel i adaptiva formulär och interaktiv kommunikation. Växla till layoutläge om du vill använda det nya alternativet med flera kolumner. Mer information finns i [Använda layoutläget för att ändra storlek på komponenter](../forms/using/resize-using-layout-mode.md).

![Flerspaltig layout](assets/multi-column-layout.gif)

#### Anpassningar av AEM Inbox (6.5.4.0) {#aem-inbox}

Med det nya alternativet Admin Control kan administratörer:

* Anpassa rubriktext och logotyp

* Styra visningen av navigeringslänkar i sidhuvudet

Alternativet Administratörskontroll är bara synligt för medlemmarna i gruppen Administratörer eller Arbetsflödesadministratörer. Mer information om den här funktionen finns i [Inkorgen](../sites-authoring/inbox.md).

#### RTF-stöd i HTML5-formulär (6.5.4.0) {#rich-text-support}

Konvertera ett textfält i ett XFA-formulär till ett RTF-fält i ett HTML5-formulär. Mer information finns i [Utforma formulärmallar för HTML5-formulär](../forms/using/designing-form-template.md).

#### Tillgänglighetsförbättringar (6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience Manager Forms innehåller följande tillgänglighetsförbättringar:

* Skärmläsarna meddelar kryssrutor, länkar, datumväljare och datuminmatningsfält korrekt i ett anpassat formulär.

* Varje sida i ett adaptivt formulär innehåller nu en rubrik och en huvudlandmärkesetikett.

#### Dela och begära åtkomst till inkorgsobjekt som tillhör en AEM Forms-användare (6.5.3.0) {#share-request-access}

Du kan dela dina inkorgsobjekt med en annan användare. När en annan användare får tillgång till dina inkorgsobjekt kan användaren göra anspråk på och vidta lämpliga åtgärder för delade objekt. På samma sätt kan du begära åtkomst till inkorgsobjekt från andra användare. Se [Dela och begära åtkomst till inkorgsobjekt för en användare](../forms/using/configure-shared-queues-osgi.md).

#### Konfigurera inställningar utanför kontoret för inkorgsobjekt för en AEM Forms-användare (6.5.3.0) {#configure-out-of-office}

Om du tänker vara utanför kontoret kan du ange vad som ska hända med artiklar som har tilldelats dig för den perioden.
Du kan ange startdatum och -tid och slutdatum och sluttid så att dina inställningar som inte är på kontoret börjar gälla. Du kan ange en standardperson som alla dina objekt skickas till. Se [Konfigurera inställningar](../forms/using/configure-out-of-office-settings.md)för frånvaro.

#### Generera flera interaktiva dokument med Batch API för AEM Forms (6.5.3.0) {#generate-multiple-ic}

Du kan använda batch-API:t för att skapa flera interaktiva dokument från en mall. Mallen är en interaktiv kommunikation utan data. Batch-API:t kombinerar data med en mall för att skapa en interaktiv kommunikation. API:t är användbart vid massproduktion av interaktiv kommunikation. Till exempel telefonräkningar, kreditkortsutdrag för flera kunder. Se [Generera flera interaktiva dokument med hjälp av API:t](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)för gruppbearbetning.

## Viktiga versioner sedan AEM 6.5 SP4 {#key-releases-since-last-sp}

Mellan 5 mars 2020 och 4 juni 2020 släppte Adobe följande funktioner som ligger utanför AEM-leveranserna:

* AEM Cloud Manager [2020.3.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-3-0.html), [20.4.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-4-0.html)och [2020.5.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-current.html)

* [AEM Assets: Desktop App 2.0.2.0](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html)

* [AEM-skärmar: Funktionspaket 2004](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202004.html)

## Användbara resurser

* [Användarhandböcker för AEM 6.5](../user-guide/home.md)

* [Allmän versionsinformation om Adobe Experience Manager 6.5](release-notes.md)

* [Versionsinformation om Service Pack för Adobe Experience Manager 6.5](sp-release-notes.md)
