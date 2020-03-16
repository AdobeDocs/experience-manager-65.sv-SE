---
title: Nyheter i Adobe Experience Manager 6.5 Service Pack 4
description: Nyheter i Adobe Experience Manager 6.5 Service Pack 4
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: ed756d785864131c2e031aec4331388bc057576b

---


# Nyheter i Adobe Experience Manager 6.5 Service Pack 4 {#aem-whats-new-service-pack-4}

Adobe Experience Manager (AEM) 6.5 ger funktioner och kontinuerliga förbättringar genom kvartalsvisa Service Packs i år. Det nya sättet är till fördel för våra kunder när de börjar använda innovationerna snabbare.

Den senaste versionen av AEM Service Pack 4 (6.5.4.0) släpptes 5 **mars 2020**. I den här artikeln beskrivs de funktioner som den senaste Service Pack-versionen erbjuder för att göra din AEM-resa mer tilltalande.

## AEM Sites {#aem-sites}

### Prestandaförbättringar inom olika områden {#performance-improvements}

* Minskad tid för inläsning och initiering av ContextHub inom en plats (contexthub.kernel.js). Det ger snabbare sidinläsning under ett webbplatsbesök.

* Förkorta tiden för uppdatering av en sida efter att Experience Fragments har dragits och släppts till sidredigeraren Webbplatser.

* Förkortade tiden för inläsning av poster för en Sites-sida med över 200 live-kopior i Live Copy Overview.

* Förbättrad hantering av ofullständiga eller ogiltiga URL:er. Sådana URL-adresser kan göra mallredigeraren långsammare.

Dessutom innehåller AEM 6.5.4.0 förbättringar i formatsystemet. Nu kan du välja format i komponentdialogrutan.

## AEM Assets {#aem-assets}

### Integrering med varumärkesportalen via Adobe I/O Console {#assets-integration-bp}

Nu kan du konfigurera AEM Assets med Brand Portal via Adobe I/O Console. Adobe I/O Console anskaffar en IMS-token för godkännande av innehavaren av varumärkesportalen. Tidigare konfigurerades AEM Assets med varumärkesportalen i det klassiska användargränssnittet via äldre OAuth-gateway. Konfigurationerna som använder äldre OAuth Gateway stöds till 6 april 2020. Om du inte ändrar integreringen fortsätter de befintliga konfigurationerna att fungera.

Du kan antingen skapa en ny integrering eller uppgradera integreringsinställningarna till Adobe I/O Console.

### Förbättrad tillgänglighet {#accessibility-enhancements}

Experience Manager Assets innehåller följande tillgänglighetsförbättringar:

* Piltangenter på tangentbordet kan användas för att flytta och panorera områden i zoomade bilder. Mer information finns i [Förhandsgranska resurser endast](../assets/managing-assets-touch-ui.md#previewing-assets)med tangentbordstangenter.

* Kryssrutorna för blandat läge (där kryssrutorna på första nivån inte markeras och genomstrykas) på panelen Filter kan läsas av skärmläsare om du inte markerar alla kapslade alternativ.

* Begränsningar för datum- och tidsformat finns i fältetiketter för datumfält, så att användarna kan ange datumet i korrekt format med tangentbordet.

   Exempel, `On Time (MM-DD-YYYY HH:mm)`. Här är MM månad i tvåsiffrigt format, YYYY är år, DD är dag i tvåsiffrigt format, HH är timme i 24-timmars militärt format och mm är minut.

* Symbolen på knappen för att ta bort de markerade taggarna visas nu för skärmläsare tillsammans med antalet markerade taggar. `X`

## AEM Forms {#aem-forms}

### Generera utskrifter i arbetsflöden för AEM Forms {#generate-printable-output}

Om du vill ha en lösning för att skriva ut eller spara flera kopior av en källmallfil och integrera den med en datafil med flera poster, finns ett nytt arbetsflödessteg för att generera utskrift i AEM Forms. Om du till exempel vill skriva ut ett källformulär med ett annat namn varje gång det skrivs ut, kan du ha dessa namn i datafilen och integrera dem med en standardmallfil.

Utnyttja den här funktionen med **Verktyg** > **[!UICONTROL Arbetsflöde]** > **[!UICONTROL Modeller]** > **[!UICONTROL Skapa]** och sök sedan efter arbetsflödessteget **[!UICONTROL Generera utskrift]** .

![Generera utdata för utskrift](assets/generate-print-output-demo.gif)

Mer information om den här funktionen finns i [Formulärcentrerat arbetsflöde i OSGi - stegreferens](../forms/using/aem-forms-workflow-step-reference.md).

### Stöd för flera kolumner för adaptiva formulär och interaktiv kommunikation i layoutläge {#multi-column-adaptive-forms}

Nu kan du definiera antalet kolumner för en panel i adaptiva formulär och interaktiv kommunikation.

Du hittar det nya alternativet genom att växla till layoutläget. Tryck på panelen som du vill konvertera till ett flerkolumnsformat, markera dess överordnade panel och tryck på ikonen för flera kolumner för att definiera antalet kolumner för panelen.

![Flerspaltig layout](assets/multi-column-layout.gif)

Mer information finns i [Använda layoutläget för att ändra storlek på komponenter](../forms/using/resize-using-layout-mode.md).

### Anpassningar av AEM Inbox {#aem-inbox}

Känner du någonsin att du behöver anpassa alternativen i AEM-huvudet? Det är nu möjligt med vår nya Service Pack-version med introduktionen av ett alternativ för **[!UICONTROL administratörskontroll]** .

**Anpassa rubriktext**

Arbetsflödesadministratörer kan nu ange vilken rubriktext du vill ha.

Du hittar det nya alternativet **[!UICONTROL Anpassa rubriktext]** under vyväljaren (som finns längst upp till höger i verktygsfältet) > **[!UICONTROL Administratörskontroll]**.

**Anpassa logotyp**

På samma sätt som när du anpassar rubriktext kan arbetsflödesadministratörer nu ange rubriklogotyp efter eget val.

Du hittar det nya alternativet **[!UICONTROL Anpassa logotyp]** under vyväljaren > **[!UICONTROL Administratörskontroll]**.

Mer information om den här funktionen finns i [Inkorgen](../sites-authoring/inbox.md).

### Användarnavigeringskontroll {#user-navigation-control}

Arbetsflödesadministratörer kan nu välja att få användarna att arbeta i AEM i ett begränsat läge baserat på sin roll. Administratörerna kan styra visningen av de navigeringsalternativ som är tillgängliga i sidhuvudet för att begränsa användarnas möjlighet att växla till arbetsflödets redigeringsläge eller andra lösningslänkar.

Kolla in de nya **[!UICONTROL Dölj-navigeringsalternativen]** under vyväljaren > **[!UICONTROL Administratörskontroll]**.

Mer information om den här funktionen finns i [Inkorgen](../sites-authoring/inbox.md).

### RTF-stöd i HTML5-formulär {#rich-text-support}

Textfältet kan nu visa en lista med formateringsalternativ i det återgivna HTML5-formuläret. Du måste definiera ett format för textfältet i Forms Designer för att kunna använda lämpliga inställningar för fältet.

Om du vill använda den här funktionen trycker du på textfältet i **[!UICONTROL designvyn]** i Forms Designer. Använd inställningarna genom att välja **[!UICONTROL RTF]** i listrutan **[!UICONTROL Fältformat]** på fliken **[!UICONTROL Fält]** .

Mer information finns i [Utforma formulärmallar för HTML5-formulär](../forms/using/designing-form-template.md).

## Viktiga högdagrar

Förutom nya funktioner innehåller AEM 6.5 Service Pack 4 följande viktiga funktioner:

* Nu kan du synkronisera selektiva underträd till *Dynamic Media - Scene7-läge* i stället för alla tillgängliga på `content/dam`.

* Integrering av formulärdatamodell med SOAP-webbtjänst har nu stöd för urvalsgrupper eller attribut för element.

* SOAP-indata eller -utdata och komplexa datastrukturer har nu stöd för dynamisk gruppersättning.

## Viktiga funktioner i tidigare AEM 6.5 Service Packs

### Smart Imaging for Dynamic Media {#smart-imaging}

Smart bildbehandling utnyttjar varje användares unika visningsegenskaper för att automatiskt leverera rätt bilder som är optimerade för sin upplevelse, vilket ger bättre prestanda och engagemang. Smart bildbehandling fungerar med befintliga bildförinställningar och använder intelligens under de sista millisekunderna i leveransen för att ytterligare minska bildfilens storlek baserat på webbläsarens eller nätverkets anslutningshastighet. Se [Smart bildbehandling](../assets/imaging-faq.md).

### Visuell sökning efter AEM Assets {#visual-search}

Resurser som användare kan söka efter visuellt liknande bilder. AEM visar smarta taggade bilder från DAM-databasen som liknar den användarvalda bilden. Se [Visuell sökning](../assets/search-assets.md).

### Dela och begära åtkomst till inkorgsobjekt från en användare {#share-request-access}

Du kan dela dina inkorgsobjekt med en annan användare. När en annan användare har åtkomst till dina inkorgsobjekt kan användaren göra anspråk på och vidta lämpliga åtgärder för delade objekt. På samma sätt kan du begära åtkomst till inkorgsobjekt från andra användare. Se [Dela och begära åtkomst till inkorgsobjekt för en användare](../forms/using/configure-shared-queues-osgi.md).

### Konfigurera frånvaroinställningar för inkorgsobjekt {#configure-out-of-office}

Om du tänker vara utanför kontoret kan du ange vad som ska hända med artiklar som har tilldelats dig för den perioden.
Du kan ange startdatum och -tid och slutdatum och sluttid så att dina inställningar som inte är på kontoret börjar gälla. Du kan ange en standardperson som alla dina objekt skickas till. Se [Konfigurera inställningar](../forms/using/configure-out-of-office-settings.md)för frånvaro.

### Generera flera interaktiva dokument med Batch API {#generate-multiple-ic}

Du kan använda batch-API:t för att skapa flera interaktiva dokument från en mall. Mallen är en interaktiv kommunikation utan data. Batch-API:t kombinerar data med en mall för att skapa en interaktiv kommunikation. API:t är användbart vid massproduktion av interaktiv kommunikation. Till exempel telefonräkningar, kreditkortsutdrag för flera kunder. Se [Generera flera interaktiva dokument med hjälp av API:t](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)för gruppbearbetning.

### Standardvalideringsfelmeddelanden för anpassade formulär {#standard-validation}

Anpassningsbara formulär kan nu integreras med anpassade tjänster för datavalidering. Om indatavärdena inte uppfyller valideringskriterierna och det valideringsfelmeddelande som servern returnerar har standardmeddelandeformatet, visas felmeddelandena på fältnivå i formuläret. Om indatavärdena inte uppfyller valideringskriterierna och servervalideringsfelmeddelandet inte har standardmeddelandeformatet, erbjuder adaptiva formulär en mekanism för att omvandla valideringsfelmeddelandena till ett standardformat så att de visas på fältnivå i formuläret. Se [Standardvalideringsfelmeddelanden för adaptiva formulär](../forms/using/standard-validation-error-messages-adaptive-forms.md).

## Viktiga versioner sedan AEM 6.5 SP3

Mellan 12 december 2019 och 5 mars 2020 släppte Adobe följande funktioner som ligger utanför AEM-leverantörens kärnprogram:

* AEM Cloud Manager 2020.1.0 och 2020.2.0Månadsförbättringar av Cloud Manager, de senaste två versionerna med fokus på att förbättra pipeline-statusen och möjligheten att hämta loggar för de olika stegen. Läs den fullständiga versionsinformationen här:
   * [Cloud Manager 2020.1.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-1-0.html)

   * [Cloud Manager 2020.2.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-current.html)

* CLI-uppdateringar för AEM Cloud ManagerAutomatisera molnhanteraruppgifter med kommandoradsverktyget. Vi utökar CLI kontinuerligt - gå med i [GitHub](https://github.com/adobe/aio-cli-plugin-cloudmanager/releases).

* AEM Sites: Project Archetype 23Det bästa sättet att starta ett nytt AEM-projekt. Med Arketype 23 [sammanfogar vi Project Archetype för SPA och vanliga webbplatser till en](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-23), vilket ger dig ett standardtema som hjälper dig att komma igång direkt med utvecklingen.

* AEM Sites: WKND Reference SiteAlla [nya referensprojekt](https://www.wknd.site/) är fullmatade med bästa praxis för hur man bygger webbplatser med AEM. Lär dig mer genom att läsa den helt uppdaterade [WKND-självstudiekursen](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html) och hämta koden från [GitHub](https://github.com/adobe/aem-guides-wknd/releases).

* AEM Sites: Commerce CIF Core Components 0.7.0 och 0.9.0Integrating AEM Sites and Magento Commerce. Vi [utökar kontinuerligt dedikerade kärnkomponenter och en projekttyp med fokus på Commerce](https://github.com/adobe/aem-core-cif-components/releases).

* AEM Assets: Desktop App 2.0.1.1
   [Få åtkomst till resurserna på datorn](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html)

* AEM-skärmar: Feature Pack 202001Digital signage direkt från AEM. Ta del av de senaste förbättringarna med det senaste funktionspaketet, den här gången [aktiverar vi synkron uppspelning över flera mediespelare](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202001.html).

## Användbara resurser

* [Användarhandböcker för AEM 6.5](../user-guide/capabilities.md)

* [Allmän versionsinformation om Adobe Experience Manager 6.5](release-notes.md)

* [Versionsinformation om Service Pack för Adobe Experience Manager 6.5](sp-release-notes.md)
