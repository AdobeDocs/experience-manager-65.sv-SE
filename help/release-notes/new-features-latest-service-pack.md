---
title: Nyheter i Adobe Experience Manager 6.5 Service Pack 4
description: Nyheter i Adobe Experience Manager 6.5 Service Pack 4
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: f50369f269040bf7f1a30b018acbc1b441abdb15

---


# Nyheter i Adobe Experience Manager 6.5 Service Pack 4 {#aem-whats-new-service-pack-4}

Adobe Experience Manager (AEM) 6.5 ger funktioner och kontinuerliga förbättringar genom kvartalsvisa Service Pack. Det nya sättet är till fördel för våra kunder när de börjar använda innovationerna snabbare.

Den senaste versionen av AEM Service Pack 4 (6.5.4.0) släpptes 5 **mars 2020**. I den här artikeln beskrivs de funktioner som den senaste Service Pack-versionen erbjuder för att göra din AEM-resa mer tilltalande.

## AEM Sites {#aem-sites}

### Prestandaförbättringar inom olika områden {#performance-improvements}

* Minskad tid för inläsning och initiering av ContextHub inom en plats (`contexthub.kernel.js`). Det ger snabbare sidinläsning under ett webbplatsbesök.

* Förkorta tiden för uppdatering av en sida efter att Experience Fragments har dragits till sidredigeraren Platser.

* Ökade inläsningstiden för inlägg på en Sites-sida med över 200 live-kopior i **[!UICONTROL Live Copy Overview]**.

* Förbättrad hantering av ofullständiga eller ogiltiga URL:er. Sådana URL-adresser kan göra mallredigeraren långsammare.

Dessutom innehåller AEM 6.5.4.0 förbättringar i formatsystemet. Nu kan du välja format i komponentdialogrutan.

## AEM Assets {#aem-assets}

### Konfigurera AEM-resurser med varumärkesportalen {#configure-assets-bp}

Auktoriseringskanalen mellan AEM Assets och Brand Portal har ändrats. Tidigare konfigurerades varumärkesportalen i Classic UI via äldre OAuth Gateway, som använder JWT-tokenutbyte för att erhålla en IMS Access-token för auktorisering. AEM Assets har nu konfigurerats med Brand Portal via Adobe I/O, som anskaffar en IMS-token för auktorisering av din klient för varumärkesportalen.

Stegen för att konfigurera AEM Assets med Brand Portal är olika beroende på din AEM-version, om du konfigurerar för första gången eller uppgraderar befintliga konfigurationer. Mer information finns i [Konfigurera AEM-resurser med varumärkesportalen](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) .


### Förbättrad tillgänglighet {#accessibility-enhancements}

Experience Manager Assets innehåller följande tillgänglighetsförbättringar:

* Piltangenter på tangentbordet kan användas för att flytta och panorera områden i zoomade bilder. Mer information finns i [Förhandsgranska resurser endast](../assets/managing-assets-touch-ui.md#previewing-assets)med tangentbordstangenter.

* Kryssrutorna för blandat läge (där kryssrutorna på första nivån inte markeras och genomstrykas) på panelen Filter kan läsas av skärmläsare om du inte markerar alla kapslade alternativ.

* Begränsningar för datum- och tidsformat finns i fältetiketter för datumfält, så att användarna kan ange datumet i korrekt format med tangentbordet.

   Exempel, `On Time (MM-DD-YYYY HH:mm)`. Här är MM månad i tvåsiffrigt format, YYYY är år, DD är dag i tvåsiffrigt format, HH är timme i 24-timmars militärt format och mm är minut.

* Symbolen på knappen för att ta bort de markerade taggarna visas nu för skärmläsare tillsammans med antalet markerade taggar. `X`

## AEM Forms {#aem-forms}

### Generera utskrifter i arbetsflöden för AEM Forms {#generate-printable-output}

Med det nya arbetsflödessteget Generera utskrift kan du integrera en källmallfil med en datafil. Tack vare den här integreringen kan du skriva ut eller spara olika kopior av mallfilen. Du kan till exempel skriva ut ett källformulär med ett annat namn varje gång det skrivs ut. Spara namnen i datafilen och integrera datafilen med en standardmallfil. Mer information om den här funktionen finns i [Formulärcentrerat arbetsflöde i OSGi - stegreferens](../forms/using/aem-forms-workflow-step-reference.md).

![Generera utdata för utskrift](assets/generate-print-output-demo.gif)

### Stöd för flera kolumner för adaptiva formulär och interaktiv kommunikation i layoutläget {#multi-column-adaptive-forms}

Nu kan du definiera antalet kolumner för en panel i adaptiva formulär och interaktiv kommunikation. Växla till layoutläge om du vill använda det nya alternativet med flera kolumner. Mer information finns i [Använda layoutläget för att ändra storlek på komponenter](../forms/using/resize-using-layout-mode.md).


![Flerspaltig layout](assets/multi-column-layout.gif)



### Anpassningar av AEM Inbox {#aem-inbox}

Med det nya alternativet Admin Control kan administratörer:

* Anpassa rubriktext och logotyp

* Styra visningen av navigeringslänkar i sidhuvudet

Alternativet Administratörskontroll är bara synligt för medlemmarna i gruppen Administratörer eller Arbetsflödesadministratörer. Mer information om den här funktionen finns i [Inkorgen](../sites-authoring/inbox.md).

### RTF-stöd i HTML5-formulär {#rich-text-support}

Du kan nu konvertera ett textfält i ett XFA-formulär till ett RTF-fält när det återges i ett HTML5-formulär. Det innebär att textfältet innehåller en lista med andra formateringsalternativ i ett HTML5-formulär. Mer information finns i [Utforma formulärmallar för HTML5-formulär](../forms/using/designing-form-template.md).

### Förbättrad tillgänglighet {#forms-accessibility-enhancements-6540}

Experience Manager Forms innehåller följande tillgänglighetsförbättringar:

* Man kan flytta tabbfokus utan problem för det Ultramarine-Accessible-referenstemat i ett adaptivt formulär.

* Skärmläsarna meddelar kryssrutor, länkar, datumväljare och datuminmatningsfält korrekt i ett anpassat formulär.

* Varje sida i ett adaptivt formulär innehåller nu en rubrik och en huvudlandmärkesetikett.

## Viktiga funktioner i tidigare AEM 6.5 Service Packs

### Smart Imaging for Dynamic Media (6.5.3.0) {#smart-imaging}

Smart bildbehandling använder varje användares unika visningsegenskaper för att automatiskt leverera rätt bilder som är optimerade för sin upplevelse, vilket ger bättre prestanda och engagemang. Smart bildbehandling fungerar med befintliga bildförinställningar och använder intelligens under de sista millisekunderna i leveransen för att ytterligare minska bildfilens storlek baserat på webbläsarens eller nätverkets anslutningshastighet. Se [Smart bildbehandling](../assets/imaging-faq.md).

### Visuell sökning efter AEM Assets (6.5.2.0) {#visual-search}

Resurser som användare kan söka efter visuellt liknande bilder. AEM visar smarta taggade bilder från DAM-databasen som liknar den användarvalda bilden. Se [Visuell sökning](../assets/search-assets.md).

### Dela och begära åtkomst till inkorgsobjekt för en användare (6.5.3.0) {#share-request-access}

Du kan dela dina inkorgsobjekt med en annan användare. När en annan användare får tillgång till dina inkorgsobjekt kan användaren göra anspråk på och vidta lämpliga åtgärder för delade objekt. På samma sätt kan du begära åtkomst till inkorgsobjekt från andra användare. Se [Dela och begära åtkomst till inkorgsobjekt för en användare](../forms/using/configure-shared-queues-osgi.md).

### Konfigurera inställningen för frånvaro av inkorgsobjekt (6.5.3.0) {#configure-out-of-office}

Om du tänker vara utanför kontoret kan du ange vad som ska hända med artiklar som har tilldelats dig för den perioden.
Du kan ange startdatum och -tid och slutdatum och sluttid så att dina inställningar som inte är på kontoret börjar gälla. Du kan ange en standardperson som alla dina objekt skickas till. Se [Konfigurera inställningar](../forms/using/configure-out-of-office-settings.md)för frånvaro.

### Generera flera interaktiva dokument med Batch API (6.5.3.0) {#generate-multiple-ic}

Du kan använda batch-API:t för att skapa flera interaktiva dokument från en mall. Mallen är en interaktiv kommunikation utan data. Batch-API:t kombinerar data med en mall för att skapa en interaktiv kommunikation. API:t är användbart vid massproduktion av interaktiv kommunikation. Till exempel telefonräkningar, kreditkortsutdrag för flera kunder. Se [Generera flera interaktiva dokument med hjälp av API:t](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)för gruppbearbetning.



## Viktiga versioner sedan AEM 6.5 SP3

Mellan 12 december 2019 och 5 mars 2020 släppte Adobe följande funktioner som ligger utanför AEM-leverantörens kärnprogram:

* AEM Cloud Manager 2020.1.0 och 2020.2.0Versionsuppdateringarna förbättrar pipeline-statusen och möjligheten att hämta loggar för olika steg. Mer information finns i:
   * [Cloud Manager 2020.1.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-1-0.html)

   * [Cloud Manager 2020.2.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-current.html)

* CLI-uppdateringar för AEM Cloud Manager

   Versionsuppdateringarna inkluderar automatisering av Cloud Manager-åtgärder med kommandoradsverktyget. Se [GitHub](https://github.com/adobe/aio-cli-plugin-cloudmanager/releases).

* AEM Sites: Project Archetype 23

   Det bästa sättet att starta ett nytt AEM-projekt. Arketyp 23 sammanfogar [Project Archetype för SPA och vanliga webbplatser till en och samma](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-23) webbplats och tillhandahåller ett standardtema för att komma igång snabbt med utvecklingen.

* AEM Sites: WKND-referensplats

   [Nytt referensprojekt](https://www.wknd.site/) fullmatat med bästa praxis för hur man bygger webbplatser med AEM. Läs mer i den uppdaterade [WKND-självstudiekursen](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html). Du kan hämta den senaste koden från [GitHub](https://github.com/adobe/aem-guides-wknd/releases).

* AEM Sites: Commerce CIF Core Components 0.7.0 och 0.9.0

   Integrera AEM Sites med Magento Commerce. Se [hur du utökar dedikerade kärnkomponenter och Project Archetype med fokus på Commerce](https://github.com/adobe/aem-core-cif-components/releases).

* AEM Assets: Desktop App 2.0.1.1

   Mer information finns i [Få åtkomst till resurserna](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html)på skrivbordet.

* AEM-skärmar: Feature Pack 202001

   Digital skylt direkt från AEM. Installera förbättringarna med det senaste funktionspaketet för att [aktivera synkron uppspelning över flera mediespelare](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202001.html).

## Användbara resurser

* [Användarhandböcker för AEM 6.5](../user-guide/home.md)

* [Allmän versionsinformation om Adobe Experience Manager 6.5](release-notes.md)

* [Versionsinformation om Service Pack för Adobe Experience Manager 6.5](sp-release-notes.md)
