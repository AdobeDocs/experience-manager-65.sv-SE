---
title: Nyheter i [!DNL Experience Manager] 6.5 Service Pack 11
description: Nyheter i [!DNL Experience Manager] 6.5 Service Pack 11
contentOwner: AK
mini-toc-levels: 1
exl-id: 32470e6e-8a66-4670-82da-2259f6e001c3
source-git-commit: 35260325b583bd047f22ffa88afb9469b2023e60
workflow-type: tm+mt
source-wordcount: '4330'
ht-degree: 0%

---

# Nyheter i [!DNL Adobe Experience Manager] 6.5 Service Pack 11 {#aem-whats-new-service-pack}

<!-- TBD: Downsample this image. We do not need as big an image since customers don't use as big a screen to view. Also, having a 700+ KB decorative image is bad for page load time.
-->

![Nyheter](assets/whatsnew.jpeg)

[!DNL Adobe Experience Manager] 6.5 Service Packs innehåller nya funktioner, förbättringar som kunderna efterfrågat samt prestanda-, stabilitets- och säkerhetsförbättringar med kvartalsvisa intervall. Den kvartalsvisa tillgängligheten gör det enkelt att komma åt och anta nya funktioner och innovationer.

I den här artikeln beskrivs funktionerna som ingår i det senaste Service Pack-meddelandet [de viktigaste funktionerna i de tidigare 6.5 Service Pack-paketen](#key-features-previous-service-packs)och [nyckelversioner sedan senaste Service Pack](#key-releases-since-last-sp) release.

## [!DNL Adobe Experience Manager Sites] {#aem-sites}

* Automatisk generering av webbplatskartan för SEO-syften är möjlig med [SEO-indexpaket](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/sites-seo-index-content-1.0.0.zip). Det har stöd för platskartor, alternativa URL:er, metataggar för robot med mera i [!DNL Core Components].

* Stöd för flera fält har lagts till för datatypen flerradig text.

* Förbättring som gör användare medvetna om det asynkrona jobb som körs i bakgrunden för att förhindra att de utlöser flera asynkrona åtgärder på samma sökväg.

## [!DNL Adobe Experience Manager Assets] {#aem-assets}

* En förbättring av användarupplevelsen visar antalet resurser i en mapp. För mer än 1000 resurser i en mapp, [!DNL Assets] visar 1000+.

   ![Antal resurser i en mapp](/help/assets/assets/browse-folder-number-of-assets.png)

* Följande tillgänglighetsförbättringar är tillgängliga:

   * I kortvyn i [!DNL Assets] databas, när `Tab` för att flytta fokus till det första objektet som öppnar snabbåtgärder i fokus, kommer skärmläsaren att meddela namnet på det objekt som är i fokus.
   * I [!DNL Dynamic Media] [!UICONTROL Viewer Preset Editor]när det inte finns någon skuggfärg eller kantfärg inaktiveras indata med egenskapen disabled. Tangentbordsanvändare kan inte fokusera indata och skärmläsare meddelar inte att kontrollen är inaktiverad.
   * I [!DNL Dynamic Media], i gränssnittet för att skapa en ny videokodningsprofil, [!UICONTROL Smart Crop Ratio] -alternativet har en tillgänglighetsetikett så att skärmläsare kan meddela det på rätt sätt.

### [!DNL Dynamic Media] {#dynamic-media}

* Du kan nu använda [!DNL Dynamic Media] för att konfigurera allmänna inställningar i stället för att behöva gå igenom [!DNL Dynamic Media Classic] datorprogram. Se [Konfigurera allmänna inställningar för Dynamic Media](/help/assets/dm-general-settings.md).

   ![Allmänna inställningar för DM](/help/assets/assets-dm/dm-general-settings.png)

* Du kan nu använda [!DNL Dynamic Media] för att konfigurera publiceringsinställningar i stället för att behöva gå igenom [!DNL Dynamic Media Classic] datorprogram. Se [Konfigurera Dynamic Media Publish Setup](/help/assets/dm-publish-settings.md).

   ![DM-publiceringsinställningar](/help/assets/assets-dm/dm-publish-setup.png)

## [!DNL Adobe Experience Manager Forms] {#aem-forms}

>[!NOTE]
>
>* [!DNL Experience Manager Forms] släpper tilläggspaketen en vecka efter den schemalagda [!DNL Experience Manager] Lanseringsdatum för Service Pack.


## Viktiga funktioner i tidigare versioner [!DNL Experience Manager] 6.5 Service Pack {#key-features-previous-service-packs}

### [!DNL Experience Manager Sites] {#aem-sites-previous-service-packs}

#### Funktioner i AEM 6.5.10.0 {#features-sites-65100}

* **Förbättrat [!DNL Content Fragment] Modeller och redigerare**: Nu kan du skapa komplexa och anpassade modeller för strukturerat innehåll med hjälp av kapslade [!DNL Content Fragment] modeller. Innehållsstrukturer modulariseras till grundläggande element som modelleras som underfragment. Fragment på högre nivå refererar till dessa delfragment. Fler datatypsförbättringar som avancerade valideringsregler ger större flexibilitet vid innehållsmodellering med [!DNL Content Fragments]. The [!DNL Experience Manager] [!DNL Content Fragment] redigeraren stöder kapslade fragmentstrukturer i en gemensam redigeringssession, med förbättringar som strukturträdvyn och tabbad breadcrumb-navigering via fragmenthierarkier.

* **GraphQL API for[!DNL Content Fragments]**: Det nya GraphQL API:t är standardmetoden för att leverera strukturerat innehåll i JSON-format. GraphQL-frågor gör att klienter bara kan begära relevanta innehållsobjekt för att återge en upplevelse. En sådan markering eliminerar överleverans av innehåll (möjlig med HTTP REST API:er) som kräver att innehåll analyseras på klientsidan. GraphQL-scheman är härledda från [!DNL Content Fragment] modeller och API-svar görs i JSON-format. I [!DNL Experience Manager] som [!DNL Cloud Service], [GraphQL-frågor finns kvar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-api-content-fragments.html#persisted-queries-caching) och bearbeta cacheanpassade GETTER. Det är ännu inte möjligt i [!DNL Experience Manager] 6.5.

* **Hierarkihantering och framtida förhandsgranskning**: Användarna har nu ett gränssnitt för att komma åt innehållsstrukturerna i [!DNL Experience Manager] startar, inklusive möjligheten att lägga till och ta bort sidor vid en start. Den här funktionen gör att [!DNL Experience Manager] startar för att skapa innehållsversioner för framtida publicering. [Funktion för tidsförvrängning](/help/sites-authoring/working-with-page-versions.md#timewarp) gör att användarna kan förhandsgranska när framtida innehåll visas.

* [!DNL Experience Manager] visar direkt en lista över alla innehållsmodeller under en mapp utan att innehållsförfattare behöver navigera i filstrukturen. Funktionen kräver nu färre klick och förbättrar redigeringseffektiviteten.

* Banfält i [!DNL Sites] redigeraren låter författare dra resurser från [!DNL Content Finder].

* Platform har några tillgänglighetsförbättringar. Se [Plattformsuppdateringar](/help/release-notes/sp-release-notes.md#platform-65100).

#### Möjlighet att återställa borttagna sidor och träd (6.5.9.0) {#ability-to-restore-pages-tree}

Nu kan du återställa de borttagna sidorna och hela trädvyn på en [!DNL Experience Manager Sites] sida.

#### Sortera de Live Copy-sidor som är tillgängliga för utrullning (6.5.8.0) {#sort-livecopy-pages}

Nu kan du sortera de Live Copy-sidor som är tillgängliga för utrullning med [!UICONTROL Name], [!UICONTROL Last modified date]och [!UICONTROL Last rollout date] egenskaper. The [!UICONTROL Last rollout date] för en sida är en ny egenskap som introducerades i den här versionen.

#### Tillgänglighet för sidförflyttning och MSM-rollouter som asynkrona åtgärder (6.5.7.0) {#page-moves-msm-asynchronous}

Nu kan du utföra sidflyttningar och MSM-rollouter som asynkrona åtgärder för att minska deras påverkan på körningsprestanda. Du kan schemalägga åtgärderna för omedelbar eller senare körning. Statusen för associerade jobb och processsteg visas i en konsol, vilket är användbart för övervakning av storskaliga MSM-utrullningar.

#### Tillgänglighet för åtgärden Sidflyttning i asynkront läge (6.5.6.0) {#page-move-asynchronous}

Åtgärden Flytta sida är nu tillgänglig i asynkront läge. Förutom omedelbar körning kan du schemalägga åtgärden Sidflyttning för senare körning.

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

* [!DNL Adobe Experience Manager Experience Fragments] exporterat till [!DNL Adobe Target] arbetsytorna visas nu som unika erbjudandetyper och erbjuder källor i [!DNL Target].

* Multi Site Manager - Publiceringsutlösaren tar nu bort en komponent från den publicerade sidan om en komponent tas bort från källsidan.

* Multi Site Manager - När namnet på en lokal komponent i en [!UICONTROL Live Copy] är identiskt med namnet på en komponent i ritningen och komponenten rullas ut från ritytan, sedan termen `_msm_moved` läggs nu till i namnet på den lokala komponenten.

#### Förbättringar av formatsystemet (6.5.4.0) {#style-system-enhancements}

Nu kan du välja format i komponentdialogrutan med det förbättrade formatsystemet.

#### Prestandaförbättringar inom olika områden (6.5.4.0) {#performance-improvements}

* Minskad tid för att läsa in och initiera ContextHub på en plats (`contexthub.kernel.js`). Det ger snabbare sidinläsning under ett webbplatsbesök.

* Förkorta tiden för uppdatering av en sida efter att du dragit [!DNL Experience Fragments] till [!DNL Sites] Sidredigeraren.

* Förkorta inläsningstiden för poster på en [!DNL Sites] sida med mer än 200 live-kopior i **[!UICONTROL Live Copy Overview]**.

* Förbättrad hantering av ofullständiga eller ogiltiga URL:er. Sådana URL-adresser kan göra mallredigeraren långsam.

### [!DNL Adobe Experience Manager Assets] {#aem-assets-previous-service-packs}

#### Funktioner i AEM 6.5.10.0 {#features-assets-65100}

* [!DNL Experience Manager] utökar funktionerna för anslutna resurser till att använda [!DNL Dynamic Media] bilder i de tillämpliga kärnkomponenterna. Se [använd anslutna resurser](/help/assets/use-assets-across-connected-assets-instances.md).

* När du delar enskilda resurser och samlingar som en länk (med [!UICONTROL Link Sharing] kan användarna välja om de vill att mottagaren ska kunna hämta de ursprungliga resurserna, sina återgivningar eller båda. Se [Dela resurser via länk](/help/assets/link-sharing.md).

   ![möjlighet att endast tillåta hämtning av ursprungliga resurser, endast återgivningar, eller båda](/help/release-notes/assets/share-assets-as-link.png)

* När användare hämtar resurser som delas med dem som en länk kan de välja att hämta de ursprungliga resurserna, återgivningarna eller båda.

* **Begränsa genererade delresurser**: Administratörer kan begränsa antalet underresurser som [!DNL Experience Manager] genererar för sammansatta resurser som PDF, PowerPoint, InDesign och Keynote-filer.

   ![begränsa produktionen av undertillgångar](/help/assets/assets/sub-asset-limit.png)

* En ny [!DNL Camera Raw] paket som stöder [!DNL Adobe Camera Raw] v10.4. Se [bearbeta bilder med [!DNL Camera Raw]](/help/assets/camera-raw.md).

#### Tidigare versioner {#previous-releases-assets}

* Namnet på kinesiska språk och regioner i Hongkong, Macau och Taiwan har uppdaterats så att de överensstämmer med kinesiska sociala och politiska åsikter (6.5.9.0).

* En valfri konfiguration introduceras för att ändra placering i e-post-ID:n i AVS-API-svar från [!DNL Adobe Experience Manager] (6.5.9.0).

   ![konfiguration för att ändra e-post-ID till gemener i AVS-svar från [!DNL Experience Manager]](assets/email-lowcase-config.png)

* Kontrasten mellan text och ikoner mot bakgrunden har förbättrats för olika funktioner. Den här implementeringen av riktlinjerna för hjälpmedel för webbinnehåll (WCAG) gör att [!DNL Assets] tillgängligare för användare med begränsad syn på och uppfattning om färger. Se [tillgänglighetsförbättringar i [!DNL Assets]](sp-release-notes.md#assets-accessibility-6590) (6.5.9.0).
* När du använder [Funktioner för anslutna resurser](/help/assets/use-assets-across-connected-assets-instances.md)kan du nu visa en lista över alla [!DNL Sites] sidor som använder resursen. Dessa referenser till en resurs är tillgängliga i en tillgångs [!UICONTROL Properties] sida. På så sätt kan administratörer, marknadsförare och bibliotekarier få en komplett bild av medieanvändningen, vilket ger bättre spårning, hantering och varumärkestrohet (6.5.8.0).

* När du tar bort en resurs som refereras på en webbsida, [!DNL Experience Manager] visar en varning. Du kan framtvinga borttagning av en refererad resurs eller kontrollera och ändra referenserna som visas i [!DNL Properties] sidan för resursen. När du klickar på referenserna öppnas den lokala datorn och fjärrkontrollen [!DNL Sites] sidor (6.5.8.0).

* [!DNL Assets] och [!DNL Dynamic Media] erbjuder flera tillgänglighetsförbättringar. Förbättringarna är relaterade till tangentbordsnavigering, användning av skärmläsare och liknande förbättringar som möjliggör användning av hjälpmedelstekniker (AT). Se [[!DNL Assets] förbättringar](/help/release-notes/sp-release-notes.md#assets-6570) och [[!DNL Dynamic Media] förbättringar](/help/release-notes/sp-release-notes.md#dynamic-media-6570) (6.5.7.0)

* Användare kan sortera digitala resurser i kort- och kolumnvyerna (6.5.7.0).

#### Tillgänglighetsförbättringar (6.5.6.0) {#accessibility-assets-6560}

* **Förbättrat fokus på användargränssnittet vid tangentbordsnavigering**, t.ex. fokus på:

   * `x` ikon in [!UICONTROL Version Preview] dialogrutan för en resurs i [!UICONTROL Timeline].

   * Alternativ för användargränssnitt som kan användas.

   * E-postfält på [!UICONTROL Share Link] dialogruta och fält för att lägga till sluten användargrupp i [!UICONTROL Permission] mappflik [!UICONTROL Properties].

* **Förbättrade funktioner med tangentbordstangenter**

   Användare kan använda tangentbordstangenter för att dra kontroller i Formulärredigeraren för metadata i bläddringsläge för skärmläsare.

* **Förbättrad användbarhet för skärmläsaranvändare**, på grund av följande:

   * Skärmläsare berättar syftet med video- och ljudspelare.

   * Skärmläsare meddelar syftet med alternativen i användargränssnittet att ta bort de taggar som har markerats med [!UICONTROL Tags selection dialog] on asset [!UICONTROL Properties].

   * Skärmläsare meddelar radrubrikerna och radobjekten i tabeller så att användarna vet vilka poster som tillhör samma rad.

   * Beskrivande och meningsfull sidrubrik för söksidan.

   * Skärmläsare meddelar alternativen på sökfilterpanelen som expanderbara dragspelspaneler.

#### Andra förbättringar i [!DNL Assets] (6.5.6.0) {#other-enhancements-assets-6560}

* Användargrupper som är associerade med mappar (privata och icke-privata) tas nu bort från databasen på [borttagning av dessa mappar](/help/assets/private-folder.md#delete-private-folder). De befintliga överflödiga, överblivna, oanvända och automatiskt genererade användargrupperna kan tas bort från databasen med JMX.

#### Tillgänglighetsförbättringar i [!DNL Assets] (6.5.5.0) {#assets-accessibility}

[!DNL Experience Manager Assets] är nu mer tillgängligt i enlighet med Web Content Accessibility Guidelines (WCAG). Tillgängligheten har förbättrats på grund av följande förbättringar:

* Många gränssnittselement, kontroller, sidor och dialogrutor är anpassade för skärmläsare.

* Många gränssnittselement, kontroller och inmatningsfält är tillgängliga via tangentbordet.

* Färgen och kontrasten i vissa element i användargränssnittet uppdateras så att användare med begränsad syn eller användare utan att uppfatta färger kan särskilja dessa element i användargränssnittet. Färgen på stjärngraderingsikonerna (som i [!UICONTROL Rating] avsnitt i [!UICONTROL Advanced] flik i resurs [!UICONTROL Properties] eller i kortvyn) ändras för att ge rätt kontrast.

   ![Klassificeringsikoner med förbättrad kontrast](assets/star-rating-icons.png)

#### Förbättrad undantagshantering (6.5.5.0) {#exception-handling}

[!DNL Assets] användargränssnittets flöde har bättre undantagshantering. Om en resurs inte har någon typ för sin dimension registreras det observerade undantaget i loggfilerna.

#### Konfigurera [!DNL Experience Manager Assets] med [!DNL Brand Portal] (6.5.4.0) {#configure-assets-bp}

Auktoriseringskanalen mellan [!DNL Experience Manager Assets] och [!DNL Brand Portal] ändras. Tidigare [!DNL Brand Portal] konfigurerades i Classic UI via äldre OAuth Gateway, som använder JWT-tokenutbyte för att erhålla en IMS Access-token för auktorisering. [!DNL Experience Manager Assets] har nu konfigurerats med [!DNL Brand Portal] via [!DNL Adobe I/O], som köper en IMS-token för att godkänna din [!DNL Brand Portal] tenant.

Vilka steg som ska konfigureras [!DNL Experience Manager Assets] med [!DNL Brand Portal] är olika beroende på din [!DNL Experience Manager] version och om du konfigurerar för första gången eller uppgraderar befintliga konfigurationer. Se [Konfigurera Experience Manager Assets med Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) för mer information.

#### Tillgänglighetsförbättringar (6.5.4.0) {#accessibility-enhancements-6540}

[!DNL Experience Manager Assets] innehåller följande tillgänglighetsförbättringar:

* Piltangenter på tangentbordet kan användas för att flytta och panorera områden i zoomade bilder. Mer information finns i [förhandsvisa resurser endast med tangentbordstangenter](../assets/manage-assets.md#previewing-assets).

* Kryssrutorna för blandat läge (där kryssrutorna på första nivån inte markeras och genomstrykas) på panelen Filter kan läsas av skärmläsare om du inte markerar alla kapslade alternativ.

* Begränsningar för datum- och tidsformat finns i fältetiketter för datumfält, så att användarna kan ange datumet i korrekt format med tangentbordet.
Till exempel, `On Time (MM-DD-YYYY HH:mm)`. Här är MM månad i tvåsiffrigt format, YYYY är år, DD är dag i tvåsiffrigt format, HH är timme i 24-timmars militärt format och mm är minut.

* Skärmläsare meddelar alternativet att ta bort markerade taggar (`X` symbol) och antalet markerade taggar.

#### Sorterbar kolumn för Skapat datum för resurser i listvyn (6.5.3.0) {#sortable-date-created-column}

En ny sorterbar kolumn för skapat datum för resurser läggs till i DAM-listvyn och i resurssökningsresultat i listvyn.

![Sorterbar kolumn för skapat datum](assets/asset-created-date.png)

#### Visuell sökning efter [!DNL Adobe Experience Manager Assets] (6.5.2.0) {#visual-search}

[!DNL Assets] -användare kan söka visuellt liknande bilder. Experience Manager visar de smarta taggade bilder från DAM-databasen som liknar den bild som användaren har valt. Se [Visuell sökning](../assets/search-assets.md).

### Dynamic Media {#dynamic-media-previous-service-packs}

* Många tillgänglighetsförbättringar har gjorts i [!DNL Dynamic Media] så att en skärmläsare kan ge en mer lämplig och användbar beskrivning av åtgärden eller användargränssnittet. Se [[!DNL Dynamic Media] uppdateringar](/help/release-notes/sp-release-notes.md#dynamic-media-65100) (6.5.10.0).

* [[!DNL Dynamic Media] är mer tillgänglig](sp-release-notes.md#assets-accessibility-6590) när det gäller

   * Enkel användning med tangentbordstangenter.
   * Kontrast (med bakgrund) för text, platshållartext och kontroller i olika redigerare.
   * Skärmläsarnas tillgänglighet och berättarröst.

* Leverera bilder av högsta kvalitet effektivt på enheter med högupplösta skärmar och begränsad nätverksbandbredd med Smart Imaging DPR (Device Pixel Ratio) och optimering av nätverksbandbredd. Se [Vanliga frågor om smart bildbehandling](/help/assets/imaging-faq.md) (6.5.9.0).

* [!DNL Dynamic Media] leverans (`fmt` URL-modifierare) har nu stöd för nästa generationens AVIF-bildformat (AV1-bildformat). Mer information och tidslinjen finns i [API-format för bildvisning och återgivning](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html) (6.5.9.0).

#### Stöd för 3D-resurser i [!DNL Dynamic Media] (6.5.5.0) {#support-for-3d}

Stöd för 3D-bilder i [!DNL Dynamic Media] gör att kunder kan publicera och lägga till 3D-innehåll på webbsidor och i tillämpningar. Supporten omfattar:

* Publicera vanliga 3D-resursformat och generera en resurs-URL som kan användas på webbsidor och andra program.

* Ett 3D Web Viewer med [!DNL Adobe Dimension], för att interaktivt visa de publicerade 3D-resurserna.

* Publicera och visa vanliga 3D-resurser på [!DNL Experience Manager Sites] sidor med [!DNL Sites] WCM-komponent.

#### Invalidera cachelagrat CDN-innehåll (6.5.6.0) {#invalidate-cdn-cached-content}

Nu kan du använda [!DNL Dynamic Media] -användargränssnittet för att göra Cachelagrat innehåll i Content Delivery Network (CDN) ogiltigt. Därför är de uppdaterade resurserna tillgängliga direkt i stället för att vänta på att cachen ska upphöra att gälla. Du kan göra CDN ogiltig genom att:

* Skapa en CDN-invalideringsmall: Välja resurser och formulärassocierade mallbaserade URL:er

* Välja resurser och tillhörande förinställningar med resursväljaren

* Lägga till fullständiga resurs-URL:er

#### Selektiv publicering av material till [!DNL Experience Manager] och [!DNL Dynamic Media] (6.5.6.0) {#selective-publishing}

Du kan nu välja att publicera eller avpublicera resurser till antingen [!DNL Experience Manager] eller [!DNL Dynamic Media] använda [!UICONTROL Quick Publish] eller [!UICONTROL Manage Publication] guide. Du kan också ange `Publish` eller `Unpublish` läge på mappnivå.

#### Smart Imaging för Dynamic Media {#smart-imaging}

Smart bildbehandling använder varje användares unika visningsegenskaper för att automatiskt leverera rätt bilder som är optimerade för sin upplevelse, vilket ger bättre prestanda och engagemang. Smart bildbehandling fungerar med befintliga bildförinställningar och använder intelligens under de sista millisekunderna i leveransen för att ytterligare minska bildfilens storlek baserat på webbläsarens eller nätverkets anslutningshastighet. Se [Smart bildbehandling](../assets/imaging-faq.md).

#### Smart beskärning i videoprofiler för Dynamic Media (6.5.3.0) {#smart-crop-video}

Smart beskärning för video - en valfri funktion i videoprofiler - använder Adobe Sensei för att automatiskt identifiera och beskära fokalpunkten i adaptiv video eller progressiv video, oavsett storlek. Se [om hur du använder smart beskärning i videoprofiler](../assets/video-profiles.md).

### Experience Manager Forms {#aem-forms-previous-service-packs}

#### Funktioner i AEM 6.5.10.0 {#features-forms-65100}

>[!NOTE]
>
>Tilläggspaketet för [!DNL Experience Manager Forms] görs tillgänglig en vecka efter den schemalagda [!DNL Experience Manager] Service Pack-version.

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

* Stöd för `GuideBridge#getGuidePath` API in [!DNL AEM Forms].

#### Stöd för [!DNL Azul Zulu OpenJDK] (6.5.9.0) {#support-azul-zulu}

Nu kan du utveckla och använda program med [!DNL Azul Zulu] byggen av [!DNL OpenJDK] for [!DNL Experience Manager Forms] på OSGi-distributioner. Mer information finns i [Versionsinformation om Experience Manager 6.5 Service Pack 9](sp-release-notes.md) och [Tekniska krav](../sites-deploying/technical-requirements.md).

#### Skicka ett e-postmeddelande till en grupp med [!UICONTROL Assign Task] (6.5.9.0) {#group-notification-email}

Du kan nu skicka ett e-postmeddelande till en grupp-e-postadress med hjälp av arbetsflödessteget Tilldela uppgift.

#### Möjlighet att hämta ett utkast till interaktiv kommunikation efter ändring av källan för interaktiv kommunikation (6.5.9.0) {#retrieve-draft-after-source-modifications}

Du kan nu hämta en interaktiv kommunikation som sparats som ett utkast när du har ändrat källan för interaktiv kommunikation.

#### Ange ett anpassat domännamn för inläsning, återgivning och validering av tjänsten reCAPTCHA (6.5.9.0) {#set-custom-domain-name-recaptcha}

reCAPTCHA-tjänsten använder `https://www.recaptcha.net/` som standarddomän. Du kan nu ändra inställningarna för att ange `https://www.google.com/` eller ett anpassat domännamn för att läsa in, rendera och validera reCAPTCHA-tjänsten.

#### Förbättrade indata för [!UICONTROL Invoke Form Data Model Service] arbetsflödessteg (6.5.9.0) {#input-data-enhancements-fdm}

När du väljer en formulärdatamodell och en tjänst i [!UICONTROL Invoke Form Data Model Service] arbetsflödessteg anger du tjänstargument för indata.

Om du väljer [!UICONTROL Relative to Payload] om du vill bifoga en fil som ett tjänstargument kan du nu ange den mappsökväg som innehåller filen i stället för det faktiska filnamnet. Om du definierar mappnamnet i stället för namnet på den bifogade filen kan du återanvända arbetsflödesmodeller. Du begränsar inte arbetsflödesmodellen till ett namn på en bifogad fil.

#### Möjlighet att använda flera överordnad sidor i en dokumentmall (6.5.9.0) {#use-multiple-master-pages-dor-template}

Nu kan du använda flera överordnad sidor i en dokumentmall. Därför kan du nu ha olika sidhuvuden, sidfötter, teckensnitt, logotypinformation på titelsidan och andra sidor i mallen.

#### Supportsidbrytningar i Dokumentformat (6.5.9.0) {#support-page-breaks-dor}

Nu kan du lägga till sidbrytningar i ett postdokument. Om en panel bryts på sidor kan du därför lägga till en sidbrytning för att flytta panelen till en ny sida i ett postdokument.

#### Visa eller dölj CAPTCHA-komponenten i ett anpassat formulär baserat på regler (6.5.8.0) {#show-hide-captcha}

Du kan nu validera CAPTCHA antingen när du skickar in formulär med adaptiv form eller när användaren gör något. Du kan också lägga till villkor för att validera CAPTCHA på en användaråtgärd och visa eller dölja CAPTCHA-komponenten i ett anpassat formulär baserat på regler.

#### Lägg till anpassade CAPTCHA-tjänster (6.5.8.0) {#add-custom-captcha-services}

[!DNL Experience Manager Forms] har direkt stöd för att använda Google reCAPTCHA (en separat licens av Google reCAPTCHA API:er krävs) som en CAPTCHA-valideringstjänst. Du kan också använda en anpassad CAPTCHA-tjänst för att validera CAPTCHA.

#### Andra förbättringar (6.5.8.0) {#other-enhancements-forms-6580}

* Förbättrad tillgänglighet för [!DNL Experience Manager Forms] Datumväljarkomponent.

* Stöd har lagts till för att generera en interaktiv kommunikation i PCL-format med hjälp av API:t PrintChannel.

* När du utför en PDFG-konvertering kan du nu aktivera eller inaktivera [!DNL Experience Manager Forms] registerändringar för generering av anpassade bokmärken.

#### Prestandaförbättringar (6.5.7.0) {#performance-improvements-forms}

[!DNL Experience Manager] 6.5 Service Pack 7 Forms förbättrar prestandan för:

* Validerar fältvärdena på servern när du skickar ett anpassat formulär.

* Konvertera ett PDF-formulär till ett anpassningsbart formulär med [!DNL Automated Forms Conversion service].

#### Stöd för tillgänglighetsgrupper med Alltid på i Microsoft SQL Server 2016 för hög tillgänglighet (6.5.7.0) {#always-on-availability-groups}

[!DNL Experience Manager Forms] nu har stöd för [!DNL Microsoft] SQL Server 2016 Always On-tillgänglighetsgrupper för OSGi-distributioner.

#### HTTP-klientkonfiguration för formulärdatamodell för optimering av prestanda (6.5.7.0) {#fdm-http-client-config}

[!DNL Experience Manager Forms] när du integrerar med RESTful-webbtjänster som datakälla inkluderar nu HTTP-klientkonfigurationer för prestandaoptimering. Se [Konfigurera datakällor](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration).

#### Tillgänglighet för alternativet Återställ för varje komponent i layoutläget (6.5.7.0) {#reset-option-layout-mode}

Du kan nu använda återställningsalternativet för varje komponent i layoutläget i ett anpassat formulär. När du definierar en layout med flera kolumner för en panel kan du använda den här funktionen för att återställa enskilda komponenter på panelen. Se [Använd layoutläget för att ändra storlek på komponenter](../../help/forms/using/resize-using-layout-mode.md#resize-components).

#### Förifyll ett adaptivt formulär på klienten (6.5.6.0) {#prefill-merge-data-at-client}

När du fyller i ett anpassat formulär i förväg visas [!DNL Experience Manager Forms] servern sammanfogar data med ett adaptivt formulär och skickar det ifyllda formuläret till dig. Som standard utförs datasammanfogningsåtgärden på servern.
Nu kan du konfigurera [!DNL Experience Manager Forms] server till [utföra datasammanfogningsåtgärden på klienten](../../help/forms/using/prepopulate-adaptive-form-fields.md) i stället för servern. Det minskar avsevärt den tid som krävs för att förifylla och återge anpassningsbara formulär.

#### Integrering av formulärdatamodell med RESTful API:er på en server med tvåvägs SSL-implementering (6.5.6.0) {#fdm-integration-rest-apis-two-way-ssl}

[!DNL Experience Manager Forms] formulärdatamodellen kan nu [integrera med RESTful-API:er på en server som har en tvåvägs SSL implementerad på den](../../help/forms/using/configure-data-sources.md).

#### Stöd för [!DNL Adobe Sign] Texttaggar i tjänsten Automated forms conversion (6.5.6.0) {#sign-integration-acroform-afcs}

Om ett AcroForm innehåller [!DNL Adobe Sign] Texttaggar, dessa fält känns nu igen och representeras som [!DNL Adobe Sign] fält i det adaptiva formuläret har konverterats med [!DNL Automated Forms Conversion service]. En signerare kan fylla i sådana fält medan han/hon signerar det anpassade formuläret.

#### Stöd för konvertering av färgat PDF forms till adaptiva formulär (6.5.6.0) {#colored-PDF-forms}

Du kan använda [!DNL Automated Forms Conversion service] för att konvertera färgat PDF forms till anpassningsbara formulär.

#### Stöd för SMB 2- och SMB 3-protokoll (6.5.6.0) {#smb-support}

[!DNL Experience Manager Forms] har nu stöd för SMB 2- och SMB 3-protokoll.

#### Förbättrad cachning för översatta adaptiva formulärsidor (6.5.6.0) {#enhanced-caching-translated-adaptive-forms}

Nu kan du ange [språkinställning som väljare i URL:en för anpassningsbara formulär i stället för ett argument i URL:en för anpassningsbara formulär](../../help/forms/using/supporting-new-language-localization.md). Det hjälper till att cachelagra översatta adaptiva formulär på [!DNL Experience Manager Dispatcher]. Det gick inte att cachelagra översatt adaptiv form i tidigare versioner. Mer information om hur du konfigurerar cachning för att använda språkområdet som väljare i URL:en för anpassningsbara formulär finns i [Konfigurera cacheminne för anpassningsbara formulär vid dispatcher](../../help/forms/using/configure-adaptive-forms-cache.md).

#### Spara utdata från formulärdatamodelltjänst till en variabel (6.5.6.0) {#save-fdm-service-to-variable}

Med formulärdatamodellen kan du spara utdata från en formulärdatamodelltjänst till en variabel. [!DNL Experience Manager Forms] mappar nu automatiskt typen av formulärdatamodelltjänst till variabeltypen.

#### Bifoga flera filer för komponenten Bifogad fil (6.5.6.0) {#attach-multiple-files}

Nu kan du [bifoga flera filer](../../help/forms/using/introduction-forms-authoring.md) till [!UICONTROL File Attachment] i adaptiva former.

#### Anpassa Adobe Experience Manager Inbox-kolumnerna (6.5.5.0) {#customize-aem-inbox-columns}

Du kan anpassa en [!DNL Experience Manager] Inkorg om du vill ändra standardrubriken för en kolumn, ändra ordning på en kolumns position och visa ytterligare kolumner baserat på data i ett arbetsflöde. Ledamöter av `administrators` eller `workflow-administrators` kan anpassa kolumnerna. Mer information finns i [Administratörskontroll](../sites-authoring/inbox.md#inbox-admin-control).

![Anpassa Experience Manager-inkorgskolumner](assets/customize-columns.gif)

#### Spara interaktiv kommunikation som ett utkast (6.5.5.0) {#save-as-draft}

Du kan använda agentgränssnittet för att spara ett eller flera utkast för varje interaktiv kommunikation och hämta utkastet senare för att fortsätta arbeta med det. Du kan ange olika namn för varje utkast för att identifiera det. Mer information finns i [Spara interaktiv kommunikation som utkast](../forms/using/prepare-send-interactive-communication.md#save-as-draft).

![Spara som utkast](assets/save-as-draft.gif)

#### [!DNL Oracle WebLogic] stöd för programservrar (6.5.5.0) {#weblogic-support}

Adobe Experience Manager Forms har lagt till stöd för [!DNL Oracle WebLogic 12] för Adobe Experience Manager Forms på JEE. Du kan uppgradera från en tidigare version eller konfigurera en ny Experience Manager 6.5 Forms på JEE-servern på [!DNL Oracle WebLogic] 12.2.1.4 och senare. Senare motsvarar de mindre versionsändringarna, där x i 12.2.1.x ersätts med ett versionsnummer.

#### Förbättringar av hjälpmedel (6.5.5.0) {#accessibility-improvements}

Adobe Experience Manager Forms innehåller följande tillgänglighetsförbättringar:

* När en användare förhandsgranskar ett adaptivt formulär som ett HTML-formulär visas [!UICONTROL Scribble Signature] fältet behåller tabbfokus.

* Felmeddelandena som visas när du skickar ett anpassat formulär innehåller nu `aria-describedBy` -attribut. Attributet är kopplat till fälten som refereras i felmeddelandet. The `aria-describedby` -attribut anger ID:n för elementen som beskriver objektet. Det hjälper till att skapa en relation mellan widgetar eller grupper och text som beskriver dem.

* Om ett anpassningsbart formulär har obligatoriska fält anges det obligatoriska attributet till `True` för sådana fält i hjälpmedelsschemat för ARIA.

#### X-509 certifikatbaserad autentisering för SOAP-baserade webbtjänster i formulärdatamodell (6.5.5.0) {#x509-based-authentication-soap}

Formulärdatamodellen har nu stöd för X-509-certifikatbaserad autentisering när SOAP-webbtjänster används som datakälla. Mer information finns i [Konfigurera SOAP-webbtjänster](../forms/using/configure-data-sources.md#configure-soap-web-services).

#### Andra viktiga förbättringar (6.5.5.0) {#other-improvements}

* Experience Manager 6.5 Forms on JEE Document Security är nu baserat på [!DNL Apache Struts 2].

* Stöd för [!DNL Oracle Real Applications Cluster (RAC) 19c].

#### Generera utskrift i Experience Manager Forms-arbetsflöden (6.5.4.0) {#generate-printable-output}

Med arbetsflödessteget Generera utskrift kan du integrera en källmallsfil med en datafil. Tack vare den här integreringen kan du skriva ut eller spara olika kopior av mallfilen. Steget genererar PCL-, PostScript-, ZPL-, IPL-, TPCL- eller DPL-utdata. Mer information om den här funktionen finns i [Forms-centrerat arbetsflöde i OSGi - stegreferens](../forms/using/aem-forms-workflow-step-reference.md).

![Generera utdata för utskrift](assets/generate-print-output-step.gif)

#### Stöd för flera kolumner för adaptiva formulär och interaktiv kommunikation i layoutläge (6.5.4.0) {#multi-column-adaptive-forms}

Nu kan du definiera antalet kolumner för en panel i adaptiva formulär och interaktiv kommunikation. Växla till layoutläge om du vill använda det nya alternativet med flera kolumner. Mer information finns i [Använd layoutläget för att ändra storlek på komponenter](../forms/using/resize-using-layout-mode.md).

![Flerspaltig layout](assets/multi-column-layout.gif)

#### Anpassningar av Inkorgen för Experience Manager (6.5.4.0) {#aem-inbox}

Med det nya alternativet Admin Control kan administratörer:

* Anpassa rubriktext och logotyp.

* Styr visningen av navigeringslänkar i sidhuvudet.

Alternativet Admin Control är bara synligt för medlemmarna i `administrators` eller `workflow-administrators` grupp. Mer information om den här funktionen finns i [Din inkorg](../sites-authoring/inbox.md).

#### Stöd för RTF i HTML5-formulär (6.5.4.0) {#rich-text-support}

Konvertera ett textfält i ett XFA-formulär till ett RTF-fält i ett HTML5-formulär. Mer information finns i [Utforma formulärmallar för HTML5-formulär](../forms/using/designing-form-template.md).

#### Tillgänglighetsförbättringar (6.5.4.0) {#forms-accessibility-enhancements-6540}

Experience Manager Forms innehåller följande tillgänglighetsförbättringar:

* Skärmläsarna meddelar kryssrutor, länkar, datumväljare och datuminmatningsfält korrekt i ett anpassat formulär.

* Varje sida i ett adaptivt formulär innehåller nu en rubrik och en huvudlandmärkesetikett.

#### Dela och begära åtkomst till inkorgsobjekt som tillhör en Experience Manager Forms-användare (6.5.3.0) {#share-request-access}

Du kan dela dina inkorgsobjekt med en annan användare. När en annan användare får tillgång till dina inkorgsobjekt kan användaren göra anspråk på och vidta lämpliga åtgärder för delade objekt. På samma sätt kan du begära åtkomst till inkorgsobjekt från andra användare. Se [Dela och begära åtkomst till inkorgsobjekt från en användare](../forms/using/configure-shared-queues-osgi.md).

#### Konfigurera inställningar utanför kontoret för inkorgsobjekt för en Experience Manager Forms-användare (6.5.3.0) {#configure-out-of-office}

Om du tänker vara utanför kontoret kan du ange vad som ska hända med artiklar som har tilldelats dig för den perioden.
Du kan ange startdatum och -tid och slutdatum och sluttid så att dina inställningar som inte är på kontoret börjar gälla. Du kan ange en standardperson som alla dina objekt skickas till. Se [Konfigurera inställningar för frånvaro](../forms/using/configure-out-of-office-settings.md).

#### Generera flera interaktiva dokument med Batch API för Experience Manager Forms (6.5.3.0) {#generate-multiple-ic}

Du kan använda batch-API:t för att skapa flera interaktiva dokument från en mall. Mallen är en interaktiv kommunikation utan data. Batch-API:t kombinerar data med en mall för att skapa en interaktiv kommunikation. API:t är användbart vid massproduktion av interaktiv kommunikation. Till exempel telefonräkningar, kreditkortsutdrag för flera kunder. Se [Generera flera interaktiva dokument med Batch API](../forms/using/generate-multiple-interactive-communication-using-batch-api.md).

<!-- TBD: Check if the wider team released anything in FY21.
-->

## Viktiga releaser sedan [!DNL Adobe Experience Manager] 6.5 SP10{#key-releases-since-last-sp}

Mellan den 26 augusti 2021 och den 25 november 2021 släppte Adobe följande, förutom Service Packs:

* [!DNL Adobe Experience Manager] as a Cloud Service [2021.9.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2021/release-notes-2021-9-0.html) och [2021.10.0](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

* [[!DNL Experience Manager] datorprogram 2.1 (2.1.3.4)](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

* [Experience Manager Screens: Feature Pack 202109](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/release-notes/release-notes-fp-202109.html)

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* [Allmän information om tillgänglighetsrelease för [!DNL Experience Manager] 6.5](release-notes.md)
>* [Versionsinformation för Service Pack för [!DNL Experience Manager] 6.5](sp-release-notes.md)

