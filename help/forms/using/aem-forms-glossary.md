---
title: AEM Forms-ordlista
description: AEM Forms Glossary innehåller en omfattande lista med termer, definitioner och koncept som används i Adobe Experience Manager Forms (AEM Forms), vilket gör det enklare för användare att förstå och arbeta med adaptiva formulär och relaterade funktioner.
feature: Adaptive Forms
role: Admin, User, Developer
hidefromtoc: true
hide: true
source-git-commit: 37f471e09c13b7ab036ab1043d11dfed98da1d97
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 0%

---

# AEM Forms-ordlista

## [Adaptiv Forms](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form)

Dynamiska, responsiva formulär som anpassar layout och presentation utifrån användarens enhet och indata, vilket förbättrar användarupplevelsen på olika plattformar. Innehåller villkorsstyrd logik, dynamisk databindning och regelbaserat beteende.

## [Anpassa formulärversionshantering](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/add-versioning-reviews-comments)

Möjlighet att hantera flera versioner av ett formulär i databasen med JCR-nodversionshantering. Säkerställer spårbarhet och enkel återställning för anpassningsbara formulär.

## [Adobe Analytics Forms Integration](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation)

Ger detaljerade insikter om användarinteraktioner (t.ex. när man lämnar fält, hur lång tid man lägger på varje avsnitt) med Adobe Analytics, vilket möjliggör datadriven optimering av formulärdesignen.

## [AEM Forms-tilläggspaket](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi)

Ett program som distribueras till Adobe Experience Manager (AEM) som ett paket, som innehåller tjänster (API-providers) och -servrar eller JSP:er som hanteras av AEM Sling-ramverket.

## [AEM Forms på JEE](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms)

Ett driftsättningsalternativ för AEM Forms som utnyttjar Java Enterprise Edition-servrar (JEE) och ger skalbarhet på företagsnivå, transaktionshantering och stöd för komplexa företagsarbetsflöden.

## [AEM Forms på OSGi](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/deploying/introduction/technical-requirements)

AEM Forms i OSGi-miljön är AEM författare eller AEM Publish med AEM Forms-paket som distribueras på det. Du kan köra AEM Forms på OSGi i en enda servermiljö, Farm och grupperade konfigurationer. Klusterinställningar är bara tillgängliga för AEM Author-instanser.

## [Adobe Sign i AEM Forms](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-advanced-authoring/adobe-sign-integration-adaptive-forms)

En RESTful-tjänst för säkra och sömlösa arbetsflöden för digitala signaturer. Den kan integreras med AEM Forms med OAuth-baserad autentisering, vilket möjliggör automatiska signatursamlingar och realtidsspårning.

## [AEM Forms Document Services 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/overview-aem-document-services)

API:er från AEM Forms webblager för fjärrkonsumtion av HTTP-baserade klienter, som t.ex. SDK mobilformulär.Funktioner i AEM Forms som gör det möjligt att skapa, sammanställa, distribuera och arkivera PDF-dokument, lägga till digitala signaturer och avkoda Barcoded Forms.

| **Tjänstnamn** | **Beskrivning** | **Dokumentationslänk** |
|------------------------------|---------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| **Forms-tjänst** | Rendera PDF forms med mallar och XML, integrera formulärdata för import/export och hantera fragmentbaserad återgivning. | [Forms tjänstdokumentation](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/output-service) |
| **Utdatatjänst** | Skapar dokument genom att sammanfoga data med mallar i format som PDF, PCL eller PostScript. | [Utdatatjänstens dokumentation](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/output-service) |
| **Assembler Service** | Innehåller, ordnar om, validerar och utökar dokument i PDF och XDP. | [Resursdokumentation](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/assembler-service) |
| **ConvertPDF-tjänst** | Konverterar PDF-dokument till PostScript eller bildformat som PNG, JPEG eller TIFF. | [ConvertPDF-tjänstdokumentation](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/using-convertpdf-service) |
| **Streckkodad Forms-tjänst** | Extraherar data från streckkoder i TIFF och PDF för att automatisera datainhämtningsprocesserna. | [Barcoded Forms Service documentation](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/using-barcoded-forms-service) |
| **DocAssurance-tjänst** | Krypterar, dekrypterar, signerar digitalt och tillämpar säkerhetsprofiler på PDF. | [DocAssurance-tjänstdokumentation](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/overview-aem-document-services#doc-assurance-service) |
| **Tjänsten PDF Generator** | Konverterar inbyggda filformat (t.ex. Microsoft Word, Excel) till PDF-dokument. | [PDF Generator Service-dokumentation](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/aem-document-services-programmatically#pdfgeneratorservice) |

## [Forms as a Cloud Service kommunikations-API:er](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction)

AEM Forms as a Cloud Service har avancerade verktyg för att hantera blanketter och arbetsflöden för kommunikation, med stöd för smidig digital blankettkonstruktion, datainhämtning och skräddarsydd kommunikation. Med API:er för molnkommunikation får du säker dokumentgenerering on demand och batchvis, hantering, validering och integrering med externa system via HTTP, vilket ger smidig och säker drift.

| **Tjänstnamn** | **Beskrivning** | **Dokumentationslänk** |
|-------------------------------|------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| **Dokumentgenerering** | Kombinera en mall (XFA eller PDF) med XML-data för att generera dokument i PDF och utskriftsformat som PS, PCL, DPL, IPL och ZPL. | [Dokumentation för dokumentgenerering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html#document-generation) |
| **Dokumentmanipulering** | Kombinera och ordna om dokument i PDF. | [Dokumentation för dokumentredigering](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-manipulation) |
| **Dokumentkonvertering** | Konvertera PDF till PDF/A och kontrollera att PDF/A-reglerna följs. | [Dokumentation för dokumentkonvertering](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-conversion) |
| **Document Assurance** | Lägg till eller ta bort signaturfält, signera, certifiera, kryptera, dekryptera och lägg in användningsrättigheter i PDF-dokument. | [Dokumentation för Assurance](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#doc-assurance) |
| **Digitala signaturer** | Integrerar Adobe Sign för säker e-signering av formulär och dokument. | [Dokumentation för digitala signaturer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html#digital-signatures) |


## [AEM Forms Workbench](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/install-workbench)

Ett skrivbordsprogram för att skapa, redigera och distribuera arbetsflöden samt för att hantera formulärcentrerade affärsprocesser. Det är integrerat med backend-tjänster och -system.

## [Arketyp](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/developing/archetype/overview)

En mall eller ett mönster i AEM som används för att generera ett nytt projekt med en fördefinierad struktur, vilket underlättar standardisering, snabbinstallation och efterlevnad AEM bästa praxis för utveckling.

## [Författarinstans](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/publish-process-aem-forms/publishing-unpublishing-forms)

Miljön där skribenter och administratörer utformar, skapar och hanterar innehåll innan de publicerar det. Stöder versionshantering, förhandsgranskning och testning.

## [Redigerar klientdel](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

Ett användargränssnitt för att skapa och hantera formulär i AEM Forms.

## [Adaptivt formulärblock](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/forms-references/form-components)

En inkapslingsenhet som logiskt grupperar relaterade komponenter och metadata, vilket möjliggör dynamisk datahantering och enkel skalbarhet i flerstegsformulär.

## [Kärnkomponenter](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction)

Enkelt att återanvända byggstenar för att skapa formulär, inklusive formulärfält, layoutbehållare, knappar och andra interaktiva element.

## [Korrespondenshantering](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/letters-correspondences/cm-overview)

En modul som möjliggör för företag att skapa, hantera och leverera personaliserad korrespondens med hjälp av fördefinierade mallar, regler och datakällor. Innehåller brevmallar, kundkommunikation och batchgenerering.

## [CRX (Content repository extreme)](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-aem-forms-workspace/html-workspace-architecture)

Den inbyggda Java Content Repository (JCR) i AEM som lagrar strukturerade och ostrukturerade data, vilket möjliggör hierarkisk lagring av innehåll, mallar och konfigurationer.

## [Egen komponent](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/customize-adaptive-forms-core-components)

En skräddarsydd komponent som utökar funktionaliteten i AEM Forms, som utvecklats med Sling Models, Sightly (HTL) och Java. Används vanligtvis för unik affärslogik eller avancerad interaktivitet på klientsidan.

## [Anpassad XCI (XML-konfigurationsinformation)](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/administrator-help/configure-forms/specifying-xci-configuration-options)

I Adobe Experience Manager (AEM) Forms kan administratörer med hjälp av en anpassad XCI-fil (XML Configuration Information) definiera specifika återgivningsegenskaper för formulär och dokument. Genom att konfigurera XCI-inställningar i administrationskonsolen kan du åsidosätta systemstandardinställningar med anpassade alternativ, vilket säkerställer skräddarsydd bearbetning och presentation av formulär.

## [Dataintegrering](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/form-data-model/data-integration)

Smidig integrering av externa datakällor, som databaser, webbtjänster eller REST API:er, i formulär och arbetsflöden för att möjliggöra dynamiska och personaliserade användarupplevelser.

## [Datakällor](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/form-data-model/configure-data-sources)

Gränssnitt för att integrera externa data i formulär, inklusive JDBC för relationsdatabaser, REST-slutpunkter för webbtjänster och OData för SAP-system. Hanteras via AEM Forms ramverk för dataintegrering.

## [Dokumentfragment](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/letters-correspondences/lists)

Återanvändbara dokumentkomponenter, t.ex. sidhuvuden, sidfötter, ansvarsfriskrivning eller klausuler, som kan inkluderas dynamiskt i formulär eller korrespondens för att säkerställa enhetlighet.

## [Postdokument (DoR)](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms)

En funktion i AEM Forms som genererar en icke-redigerbar, arkiveringsversion av ett inskickat formulär, vanligtvis i PDF-format, som bevarar det exakta innehållet och layouten som ett kvitto på transaktionen.

## [Edge Delivery Services](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/overview)

Optimerad innehållsleverans för AEM Forms, vilket ger kortare latens för resurser som formulär, teman och klientbibliotek där författare snabbt kan uppdatera och publicera innehåll.

## [Forms-integrering](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/form-data-model/data-integration)

Inkluderar att ansluta AEM Forms till företagssystem (t.ex. SAP, Salesforce) med hjälp av OSGi-paket och anslutningar, som stöder dubbelriktade dataflöden och realtidsuppdateringar.

## [Formulärgranskning](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-reviews-forms)

En arbetsflödesstyrd funktion som gör att intressenter kan granska anpassade formulär, lägga till kommentarer och godkänna ändringar innan de publicerar. Använder AEM Inkorgen och Aktivitetshantering.

## [Formulärdatamodell (FDM)](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/using-form-data-model)

Ett representationslager som kopplar samman adaptiva formulär med backend-datakällor, vilket möjliggör integrering med RESTful-webbtjänster, SOAP och OData. Med FDM kan formulärförfattare mappa formulärfält direkt till backend-datastrukturer, vilket säkerställer smidig synkronisering av användarindata med externa system.

## [Formulärlokalisering](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/supporting-new-language-localization)

En process med anpassningsbara formulär som kan hantera flera språk och nationella inställningar, vilket säkerställer att formulären är tillgängliga och användarvänliga för en mångfaldig publik.

## [Formulärportal](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-forms-portal/creating-form-portal-page)

Forms Portal-komponenter förser webbutvecklare med komponenter för att skapa och anpassa en Forms Portal på webbplatser som skapats med Adobe Experience Manager (AEM). Det gör det möjligt för användarna att effektivt hitta, få tillgång till och skicka in formulär på webben och mobila plattformar.

## [Formuläråtergivning och skicka från början](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

Ett användargränssnitt i AEM Forms som gör att användare kan visa och skicka formulär via en webbläsare.

## [Formuläruppsättningar](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/html5-forms/formset-in-aem-forms)

En samling relaterade formulär som grupperats tillsammans för att presenteras som en enda enhet för användarna, vilket gör att komplexa datainsamlingsprocesser kan delas upp i hanterbara avsnitt.

## [Forms Designer](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/installing-configuring-designer)

Ett fristående program som används för att utforma formulärmallar i XDP-formulär och använda det i din AEM Forms för att generera en dokumentmall.

## [Forms-centrerat arbetsflöde](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/workflows/aem-forms-workflow)

En uppsättning automatiska eller manuella steg i AEM Forms som hanterar affärsprocesser, som dokumentgodkännande, innehållspublicering eller användarmeddelanden.

## [Interaktiv kommunikation](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/getting-started/interactive-communications-overview)

En anpassad implementering för hantering av personaliserad kommunikation i flera kanaler. Den kombinerar data från olika källor, som CRM- och ERP-system, för att leverera kommunikation i format som webben, mobiler, e-post och tryck.

## [JCR (Java Content Repository)](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-jcr)

En hierarkisk, standardbaserad databas för lagring av innehåll, konfigurationer och metadata i AEM, som stöder strukturerad och ostrukturerad datalagring.

## [Bokstäver](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/letters-correspondences/create-letter#create-a-letter-template)

Genererad kundkommunikation med hjälp av AEM Forms Document Services. Bokstäverna skapas med en kombination av XDP-mallar, datamodeller och återanvändbara fragment, vilket garanterar skalbarhet i scenarier med stora volymer.

## [Metadata i AEM Forms](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/manage-administer-aem-forms/manage-form-metadata)

Metadata möjliggör effektiv kategorisering och hämtning av resurser. AEM Forms innehåller fördefinierade metadata för varje resurstyp och möjliggör anpassning. Det innehåller även verktyg för att skapa, hantera och utbyta metadata sömlöst.

## [PDF Generator](https://experienceleague.adobe.com/en/docs/experience-manager-learn/forms/document-services/using-pdfg-in-aem-forms)

Ett verktyg i AEM Forms som konverterar olika filformat (t.ex. Word, Excel, PowerPoint) till PDF-dokument och innehåller funktioner som kryptering, vattenstämplar och sammanslagning.

## [Publish Instance](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/publish-process-aem-forms/publishing-unpublishing-forms)

Den miljö i AEM som levererar direktsänt innehåll till slutanvändare. Den levererar formulär, sidor och andra digitala upplevelser med optimerade prestanda.

## [Regelredigeraren](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/rule-editor-core-components/rule-editor-core-components)

Ett visuellt verktyg i Adaptive Forms som gör att författare kan definiera anpassade regler och logik för formulärfält, som synlighet, validering och förifyllning av data, utan att behöva ha någon kodningsexpertis.

## [Skriptsignaturer](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/signing-forms-using-scribble)

En funktion i AEM Forms som gör att användare kan signera formulär elektroniskt genom att rita sin signatur direkt i formuläret med en mus- eller pekskärm.

## [Skicka åtgärd i AEM Forms](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/configuring-submit-actions)

Åtgärder på serversidan eller klientsidan som utförs när formulär skickas. Exempel är REST API-anrop, anrop av ett arbetsflöde eller skrivning av data till en JCR (Java Content Repository).

## [Teman](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components)

CSS-styrda formateringsramverk som tillämpas på adaptiva formulär och använder LESS/SASS för preprocessorer. Temana säkerställer överensstämmelse med riktlinjer för branding och tillgänglighetsstandarder, du kan anpassa ett tema, ändra dess designelement, layout, färger, typografi och ibland den underliggande koden.

## [Mall](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components)

Du kan skapa och anpassa nya mallar eller använda befintliga färdiga mallar för att skapa utkast för adaptiva formulär, som innehåller strukturella element (fält, layouter) och förkonfigurerade skript.

## [Webblager](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

Omfattar JSP:er eller serverlets som byggts över vanliga tjänster och formulärtjänster, med funktioner som framtagning av front-end, formuläråtergivning och inskickning av front-end samt REST API:er.

## [XDP (XML-datapaket)](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/manage-administer-aem-forms/get-xdp-pdf-documents-aem)

Ett filformat som används i AEM Forms för att utforma och strukturera formulär, vilket möjliggör återgivning i PDF eller HTML med stöd för dynamiskt innehåll och interaktivitet.

## [XFA (XML Forms-arkitektur)](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/creating-adaptive-form#create-an-adaptive-form-based-on-an-xfa-form-template)

En äldre teknik för att skapa interaktivt och dynamiskt PDF forms. XFA-formulär möjliggör avancerade funktioner, t.ex. dynamiska layoutjusteringar, skript och smidig integrering med backend-system.

## [XML- eller JSON-schema](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/creating-adaptive-form#create-an-adaptive-form-based-on-xml-or-json-schema)

En standardiserad struktur som används för att definiera format och organisation för XML- eller JSON-data i formulär och arbetsflöden. Dessa scheman säkerställer enhetlig datahantering och möjliggör interoperabilitet med externa system.

<!--

## **Custom Properties**  

Developer-defined metadata attributes added to components or forms for advanced behaviors, accessed via Sling APIs or Groovy scripts for dynamic processing.

## **Embedding** 

Integrating adaptive forms into AEM Sites or external web pages using `<iframe>` or SPA (Single Page Application) models. Embedding supports seamless session handling and cross-origin resource sharing (CORS).

## **CDN (Content Delivery Network)**  

Distributed networks (e.g., Akamai) used for caching and delivering forms-related resources, ensuring high availability and faster load times for geographically distributed users.


## **Dispatcher**  

An AEM caching and load balancing tool configured to optimize delivery of adaptive forms. Its filter rules ensure secure access control while caching frequently accessed forms and assets.

## **Editors**  

Tools like the Adaptive Forms Editor, Theme Editor, and Rule Editor, enabling developers and content authors to customize forms and their behavior without extensive coding.

## **Responsive UI**  

An implementation of media queries and flexible grids, ensuring adaptive forms render seamlessly across various screen sizes and devices.

## **Custom Functions**  

JavaScript-based utilities or REST microservices that provide additional logic (e.g., complex field validation or data pre-population), extending the out-of-the-box capabilities of AEM Forms.

## **Package Manager**  

AEM's CRX Package Manager facilitates importing/exporting adaptive forms, data schemas, or configurations as .zip files, enabling modular deployment in distributed environments.

## **UE (User Experience)**  

Design principles and optimizations applied in AEM Forms to enhance usability, including accessibility features (ARIA roles, tab navigation) and intuitive layouts.

## **Forms Submission Services**

Back-end services for handling form submissions, integrating with the AEM Workflow engine, third-party APIs, or direct JCR persistence.


Foundation components
e-signing
adobe sign
letters
submit action
data sources
adaptive form block
edge delivery services
forms integration
custom component 
themes
template 
custom properties
embedding
CDN
Dispatcher
editors
responsive UI
custom functions
package manager
communication APIs
UE
Forms submission services
Form review
Forms Versioning
Adobe analytics forms integration specific

## **AEM Forms Foundation Components**  
Core reusable elements within AEM Forms, built on Granite UI, enabling developers to create complex forms. They provide robust features like data bindings, field validations, and support for multilingual content.


## **e-Signing**  
An implementation of digital signature standards (e.g., PKCS #7) within AEM Forms, integrated with Adobe Sign APIs to ensure secure and legally binding electronic signatures.

## Workspace

A browser-based interface for users to interact with AEM Forms workflows, tasks, and approvals.

## Sling

A REST-based web framework used in AEM to map request URLs to content resources, enabling efficient content rendering and delivery.

-->