---
title: Cumulative Key Features and Enhancements in Adobe Experience Manager 6.5.
description: En kumulativ lista över viktiga funktioner och förbättringar som gjorts i Adobe Experience Manager 6.5 från de tidigare åtta Service Pack-versionerna.
content-type: reference
docset: aem65
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 01fe5b53-2244-445f-a4d0-bd58ea38b611
solution: Experience Manager
source-git-commit: 03c070f7bba1d66ce2a5309d2ab79567dbef3264
workflow-type: tm+mt
source-wordcount: '3531'
ht-degree: 0%

---

# Kumulativa nyckelfunktioner och förbättringar

En kumulativ lista med viktiga funktioner och förbättringar i Adobe Experience Manager 6.5 för tidigare Service Pack-versioner.

Se även [Versionsinformation om Adobe Experience Manager 6.5 Senaste Service Pack](/help/release-notes/release-notes.md).


## AEM 6.5, Service Pack 23 - 22 maj 2025

### Forms {#forms-sp23}

* [Tillgängliga hyperlänkar med blandad textformatering i statiska PDF-filer](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf): Hyperlänkar som innehåller blandade textformat i statiska PDF-filer är nu taggade som ett enda tillgängligt element. Den här förbättringen förenklar taggträdets struktur, förbättrar skärmläsarnavigeringen och stöder bättre tillgänglighet.

* [Uppdaterad plattformsmatris som stöds](/help/forms/using/aem-forms-jee-supported-platforms.md)

  Den senaste versionen innehåller uppdateringar av den plattformsmatris som stöds, vilket säkerställer kompatibilitet med nyare tekniker.

   * IBM® Content Manager Client 8.7

   * MongoDB Enterprise 7.0

   * MySQL 8.4

   * Microsoft® SQL Server 2022

   * Microsoft® SQL Server JDBC Driver 12.8

   * Red Hat® Enterprise Linux® 9 (Kernel 4.x, 64 bitar)

* [Komponenten för bifogad fil ](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment) med hög densitet: Komponenten förhindrar nu att filer skickas med ändrade tillägg som försöker kringgå tillåtna filtypskontroller. Sådana filer blockeras under överföringen för att säkerställa att endast giltiga filtyper accepteras.

## AEM 6.5, Service Pack 22 - 21 november 2024

### Sites {#sites}

[Den universella redigeraren](/help/sites-developing/universal-editor/introduction.md) finns nu i AEM 6.5 för headless-användning med ett funktionspaket.

### [!DNL Assets]

IPTC-fliken har nu stöd för textfälten [!UICONTROL Alt Text] och [!UICONTROL Extended Description]. (Assets-34918)

### Forms {#forms-sp22}

#### Nya GA-funktioner i AEM Forms {#ga-aem-forms-sp22}

* Stöd har lagts till för att aktivera teckensnittsinbäddning i [API:er för Interactive Communications Batch](https://experienceleague.adobe.com/sv/docs/experience-manager-65/content/forms/interactive-communications/create-interactive-communication#output-format-print-channel) - Interactive Communications har nu stöd för inbäddning av Adobe Ming- och Adobe Myungjo-teckensnitt i PDF-filer som genererats via Batch API. Den här förbättringen säkerställer korrekt textåtergivning i genererade dokument, även när deluppsättningar av teckensnitt används, vilket ger bättre stöd för flerspråkigt innehåll i PDF-utdata.

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

## AEM 6.5, Service Pack 21-6 juni 2024

### [!DNL Assets]

#### Förbättringar

IPTC-fliken har nu stöd för textfälten [!UICONTROL Alt Text] och [!UICONTROL Extended Description]. (Assets-34918)

#### Tillgänglighet

* Om bearbetningsstatusen för en resurs är Misslyckad eller Metadata misslyckades fungerar bildtexterna och ljudspåren nu korrekt. (Assets-37281)
* När du sparar metadata för en resurs och försöker redigera den visas språknamnet. (Assets-37281)

### [!DNL Forms]

Några av de viktigaste funktionerna och förbättringarna i den här versionen är följande:

* **Stöd för OAuth-autentiseringsuppgifter**: En ny och enklare att använda autentiseringsuppgifter för server-till-server-autentisering och ersätter den befintliga JWT-autentiseringsuppgiften (Service Account). (NPR-41994)
* [Förbättringar av regelredigeraren i AEM Forms](/help/forms/using/rule-editor-core-components.md):
   * Stöd för implementering av kapslade villkor med funktionen `When-then-else`.
   * Validera eller återställ paneler och formulär, inklusive fält.
   * Stöd för moderna JavaScript-funktioner, t.ex. låt- och pilfunktioner (ES10-stöd) i de anpassade funktionerna.
* [AutoTag API för PDF Accessibility](/help/forms/using/aem-document-services-programmatically.md#doc-utility-services-doc-utility-services): AEM Forms på OSGi har nu stöd för det nya AutoTag API:t för att förbättra PDF för tillgänglighetsstandarder genom att lägga till taggar: stycken och listor. Det gör PDF-filer mer tillgängliga för användare med hjälpmedel.
* **Stöd för 16-bitars PNG**: PDF Generator ImageToPdf-tjänst stöder nu konvertering av PNG-filer med 16-bitars färgdjup.
* **Tillämpa artefakter på enskilda textblock i XDP-filer**: I Forms Designer kan användare nu konfigurera inställningar för enskilda textblock i XDP-filer. Med den här funktionen kan du styra elementen som behandlas som artefakter i de resulterande PDF-filerna. Dessa element, som sidhuvuden och sidfötter, är tillgängliga för hjälpmedelstekniker. De viktigaste funktionerna är att markera textblock som artefakter och att bädda in dessa inställningar i XDP-metadata. Forms Output-tjänsten tillämpar dessa inställningar under PDF-genereringen och ser till att PDF/UA-taggningen är korrekt.
* **AEM Forms Designer är certifierat med `GB18030:2022` standard**: Med `GB18030:2022`-certifieringen stöder nu Forms Designer den kinesiska Unicode-teckenuppsättningen som gör att du kan mata in kinesiska tecken i alla redigerbara fält och dialogrutor.
* [Stöd för WebToPDF-flöde i JEE Server](/help/forms/using/admin-help/configure-service-settings.md#generate-pdf-service-settings-generate-pdf-service-settings) som använder PDF Generator-tjänsten har nu stöd för WebToPDF-vägen för konvertering av HTML-filer till PDF-dokument på JEE. Detta stöd finns utöver befintliga WebKit- och WebCapture-vägar (endast Windows). Vägen WebToPDF är redan tillgänglig i OSGi och utökas till JEE. På både JEE- och OSGi-plattformarna har PDF Generator-tjänsten nu stöd för följande vägar i olika operativsystem:
   * **Windows**: Webkit, WebCapture, WebToPDF
   * **Linux®**: Webkit, WebToPDF


## AEM 6.5, Service Pack 20 - 22 februari 2024

### [!DNL Assets]

* Dynamic Media stöder nu förlustfritt HEIC-bildformat för Apple iOS/iPadOS. Se [fmt](https://experienceleague.adobe.com/sv/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt) i API:t för dynamisk mediabildsserver och återgivning.
* Multisite Manager (MSM) har nu stöd för Experience Fragment-strukturer, inklusive mappar och undermappar, för effektiv gruppdistribution av Experience Fragments till Live Copies.

### [!DNL Forms]

* **Transaktionsrapportering i AEM Forms på JEE**: Transaktionsrapportering har introducerats för AEM Forms på JEE. Det möjliggör omfattande inspelning av dokumenttransaktioner som konverteringar, återgivningar och inskickade dokument. Den här förbättringen ökar effektiviteten och underlättar bättre registrering. Funktionen är inaktiverad som standard. Du kan aktivera det från administratörsgränssnittet.
* **Förbättrat skydd med ECDSA-stöd**: AEM Forms erbjuder nu robust stöd för ECDSA (Elliptic Curve Digital Signature Algorithm) för både JEE- och OSGi-stackar. Användare kan nu signera, certifiera och verifiera PDF-dokument med ökad säkerhet. Följande algoritmer för EC-kurvor stöds:
   * ECDSA-elliptisk kurva P256 med SHA256-sammandragsalgoritm
   * ECDSA-elliptisk kurva P384 med SHA384-sammandragsalgoritm
   * ECDSA elliptisk kurva P512 med SHA512-algoritm
* **Sömlös kompatibilitet med Windows 11 för Forms Designer**: AEM Forms Designer har nu stöd för Windows 11, vilket ger smidig installation och drift. Användare kan tryggt uppgradera till Windows 11 utan att behöva installera om Forms Designer eller oroa sig för kompatibilitetsproblem, vilket ger ett avbrottsfritt arbetsflöde.
* **Förbättrad tillgänglighet med den anpassade rollen Bildtext i AEM Forms Designer**: AEM Forms Designer har nu en anpassad tillgänglighetsroll som kallas Bildtext, som gör att användare kan skapa XDP-filer med anpassade bildtextelement. Den här funktionen förbättrar tillgängligheten genom att användarna kan integrera anpassade bildtexter i sina dokumentdesigner så att de kan förbättra integriteten och användarupplevelsen.

## AEM 6.5, Service Pack 19 - 7 december 2023

* Användare av sidredigeraren/bildkomponenten har aktiverat Sites för att referera till resurser från Assets Cloud Service. (SITES-13448, SITES-13433)
* AEM har nu stöd för sortering på serversidan för snabbare projektnavigering i listvyn. Projektnoder sorteras baserat på den användarvalda kolumnen innan de visas i gränssnittet.

### [!DNL Forms]

* **Nya kärnkomponenter för adaptiva formulär**: Lodräta flikar, villkor och kryssruta läggs till för att öka formulärens skalbarhet.
   * **[Kryssrutekomponent](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox)**: Adaptiv Forms baserad på kärnkomponenter kan nu innehålla en kryssrutekomponent. Det gör att användare kan göra binära val, markera eller avmarkera ett visst alternativ. Det visas vanligtvis som en liten ruta som du kan klicka på eller peka på för att växla mellan två lägen: markerad och avmarkerad. Kryssrutan är ett vanligt formulärelement som används för att ange ett ja/nej- eller sant/falskt-val.

   * **[Villkorskomponent](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions)**: Core Component-based Adaptive Forms innehåller nu en Terms and Conditions-komponent. Formulärförfattare lägger till det här avsnittet för att visa användare villkoren eller juridiska avtal för tjänsten, produkten eller plattformen. Den här komponenten är utformad för att informera användare om de regler, bestämmelser och skyldigheter som de godkänner genom att skicka in formuläret.

     ![Lodräta flikar, villkor och kryssrutekomponenter](/help/forms/using/assets/forms-components.png)

   * **[Komponent för lodräta flikar](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs)**: Adaptiv Forms baserad på kärnkomponenter kan nu ordna formulärinnehåll i en lodrät lista med flikar, vilket ger en strukturerad och navigeringsbar layout. Lodräta flikar i ett formulär förbättrar användarupplevelsen genom att förenkla navigering och organisera innehållet. De är särskilt användbara när formuläret innehåller flera avsnitt eller komplex information.

* **[64-bitarsversionen av AEM Forms Designer](/help/forms/using/installing-configuring-designer.md)**: 64-bitarsversionen av AEM Forms Designer ger bättre prestanda, skalbarhet och minneshantering så att du kan skapa formulär. Med 64-bitarsarkitekturen kan du enkelt hantera ännu större och mer komplexa projekt, vilket ger smidiga designarbetsflöden och optimerad effektivitet. Förbättra dina formulärdesignmöjligheter och ta till vara framtiden för AEM Forms Designer med denna banbrytande release.

* **[Anslut en adaptiv Forms med Microsoft® SharePoint List](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)**: AEM Forms erbjuder en körklar integrering för att skicka formulärdata direkt till SharePoint List, så att du kan använda funktionerna i SharePoint Lists. Du kan konfigurera Microsoft® SharePoint List som en datakälla för en formulärdatamodell och använda Skicka med formulärdatamodellen för att ansluta ett anpassat formulär med SharePoint List.

* **[Stöd för att konfigurera dokumentegenskaper för adaptiva formulärfragment](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)**: Nu kan du enkelt anpassa dina adaptiva formulärfragment och dess fält i den adaptiva formulärredigeraren.

* **64-bitars XMLFM**: Med 64-bitarsitereringen av XMLFM får du bättre prestanda, skalbarhet och förbättrad minneshantering. Det är den första inbyggda 64-bitarstjänsten som körs på serversidan. Genom att utnyttja sin inneboende förmåga att få tillgång till större minnesresurser jämfört med sin 32-bitars motsvarighet, ger XMLFM 64-bitars smidig hantering av större återgivningsarbetsbelastningar. Denna milstolpe innebär inte bara ett prestandasprång utan även viktiga förbättringar av det systemspecifika tjänstramverket i AEM Forms Server. Den här uppdateringen gör att AEM Forms Server stöder alla 64-bitars inbyggda tjänster sömlöst.

## AEM 6.5, Service Pack 18-24 augusti 2023

* Assets, Dynamic Media - [Stöd för flera bildtexter och ljudspår för videofilmer i Dynamic Media](/help/assets/video.md#about-msma) - Nu kan du enkelt lägga till flera undertexter och flera ljudspår i en primär video. Detta innebär att videoklippen är tillgängliga för en global publik. Du kan anpassa en enda publicerad primär video till en global publik på flera språk och följa riktlinjer för tillgänglighet för olika geografiska regioner. Författare kan också hantera undertexter och ljudspår från en enda flik i användargränssnittet.
* Assets - Från sökresultaten kan du nu navigera till den mapplats som innehåller en resurs så att du kan utföra olika resurshanteringsåtgärder.
* Sites Polaris Picker i Content Fragments har förbättrat prestandan.
* Användare av sidredigeraren/bildkomponenten har aktiverat Sites för att referera till resurser från Assets Cloud Service.
* Om du snabbt vill hitta ett projekt i listvyn, där du kan ha många projekt i systemet, har Adobe nu stöd för sortering på serversidan. Projektnoder sorteras på serverdelen baserat på den kolumn som valts av användaren innan de återges i användargränssnittet.
* AEM 6.5.18.0 stöder MongoDB 5.0 till 6.0.

### [!DNL Forms]

* **[Förbättrad felhantering med anpassade felhanterare i regelredigeraren](https://experienceleague.adobe.com/sv/docs/experience-manager-65/content/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms)** - Du kan nu anropa en anpassad funktion (med klientbibliotek) som svar på ett fel som returnerats av en extern tjänst. Och ni kan ge slutanvändarna ett skräddarsytt svar. Du kan också vidta specifika åtgärder för fel som returneras av en tjänst. Du kan till exempel anropa ett anpassat arbetsflöde i serverdelen för specifika felkoder eller informera kunden om att tjänsten är nere

* **[Förbättrat arbetsflödessteg i Adobe Sign](https://experienceleague.adobe.com/sv/docs/experience-manager-65/content/forms/workflows/aem-forms-workflow-step-reference#sign-document-step)** - Arbetsflödessteget i Adobe Sign i AEM-arbetsflöden är tillgängligt med följande förbättringar.

   * **Förbättrad säkerhet med myndighets-ID-baserad autentisering för Adobe Sign** - Adobe Acrobat Sign myndighets-ID-baserad autentisering erbjuder ytterligare verifieringslager. Det gör det möjligt för användare att autentisera sin identitet med hjälp av ett foto-ID (körkort, nationellt ID, pass). Genom att använda pålitliga identifieringsdokument ger den här förbättringen ytterligare tillförlitlighet i signeringsprocessen, vilket gör den idealisk för scenarier som kräver högre säkerhet, regelefterlevnad och användarvalidering.

   * **Förbättrad genomskinlighet med granskningsspår för Adobe Sign-dokument** - Använd funktionen Granskningsspår för att få detaljerade insikter om livscykeln för dina Adobe Sign-dokument. Med granskningsspåret kan du nu arkivera alla åtgärder och interaktioner som rör dina dokument. Dessa åtgärder och interaktioner omfattar vem som visade, redigerade eller signerade dokumentet tillsammans med tidsstämplar för varje händelse. Den här förbättringen är avgörande för att upprätthålla regelefterlevnaden, lösa tvister och säkerställa integriteten för dina digitala avtal.


   * **Utökade roller för avtalsmottagare utöver bara signeraren** - Med Adobe Acrobat Sign kan du utöka rollerna för avtalsmottagare till andra än bara signeraren för att bättre matcha deras arbetsflödesbehov. När det här alternativet är aktiverat kan varje mottagare i ett avtal konfigureras individuellt, med signerare som standard.


* **[AEM Forms i JEE med fullständigt installationsprogram](https://experienceleague.adobe.com/sv/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms)** - Service Pack har ett fullständigt installationsprogram för AEM Forms i JEE som har stöd för flera nya programkombinationer, inklusive:
   * Microsoft® Windows Server 2022
   * Microsoft® Active Directory 2022
   * Oracle WebLogic 14C i Windows Server 2022
   * Red Hat® JBoss® 7.4.10
   * MongoDB 6.0 <!-- it was previously MongoDB 4.4 -->
   * MySQL JDBC Connector 8

Om du installerar eller planerar att använda den senaste programvaran för din AEM 6.5 Forms i JEE-miljö rekommenderar Adobe att du använder AEM 6.5.18.0 Forms i JEE-fullversionen. En fullständig lista över nyligen tillagda och ersatta program finns i dokumentationen för AEM Forms on JEE eller AEM Forms on OSGi.

## AEM 6.5, Service Pack 17 - 25 maj 2023

* **Förbättringar av sökupplevelsen** - Nu kan du snabbt utföra följande åtgärder på resurserna som visas i sökresultaten:
   * Skapa ett arbetsflöde
   * Skapa en version
   * Relatera eller inte relatera tillgångar

  Du behöver inte navigera till resursplatsen och visa dess egenskaper för att utföra dessa åtgärder.

* Med **Dynamic Media _Snapshot_**&#x200B;kan du förhandsgranska bildmodifierare och optimering av smarta bilder - som WebP- eller AVIF-utdata, bandbreddsmedveten komprimering och skalning av enhetspixelproportioner - med testbilder eller dynamiska medie-URL:er. Du kan sedan omedelbart jämföra hur varje inställning påverkar kvalitet och filstorlek.
Se [Dynamisk medieögonblicksbild](https://experienceleague.adobe.com/sv/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot).
* **DASH-direktuppspelning med Dynamic Media** - Nytt protokoll (DASH - Dynamic Adaptive Streaming over HTTP) startades för Adaptive Streaming i Dynamic Media-leverans (med CMAF aktiverat). Finns nu för alla regioner.
* **Integrering av Experience Manager Sites- och innehållsfragment med Assets nästa generations dynamiska media** - Användare kan nu använda sina molnbaserade resurser i Experience Manager Sites 6.5. De kan skapa och leverera dessa resurser lokalt eller i Managed Services-instanser.

### [!DNL Forms]

* **[Adaptiv Forms i AEM Page Editor](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)** - Nu kan du använda AEM Page Editor för att snabbt skapa och lägga till flera formulär på webbplatserna. Med den här funktionen kan skribenter skapa sömlösa datainhämtningsmöjligheter på webbplatssidor med hjälp av kraften i adaptiva formulärkomponenter, inklusive dynamiskt beteende, validering, dataintegrering, generering av dokument för post- och affärsprocessautomatisering. Du kan:
   * Skapa ett anpassat formulär genom att dra och släppa formulärkomponenter till den adaptiva Forms-behållarkomponenten i AEM Sites Editor eller Experience Fragments.
   * Använd Adaptive Forms Wizard i AEM Sites Editor för att skapa formulär oberoende av sajtsidor, vilket ger dig frihet att återanvända sådana formulär på flera sidor.
   * Lägg till flera formulär på en webbplatssida, effektivisera användarupplevelsen och ge större flexibilitet.
* **[Stöd för reCAPTCHA Enterprise i Experience Manager Forms](/help/forms/using/captcha-adaptive-forms.md)** - har lagts till för reCAPTCHA Enterprise i Experience Manager Forms. Detta ger ett bättre skydd mot bedräglig aktivitet och skräppost, utöver det befintliga stödet för Google reCAPTCHA v2.
* **[Stöd för Adobe Acrobat Sign för offentlig sektor har lagts till med Experience Manager Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md)** - AEM Forms är nu integrerat med Adobe Acrobat Sign för offentlig sektor (FedRAMP-kompatibelt). Integreringen ger en avancerad nivå av regelefterlevnad och säkerhet för e-signaturer med inskickade adaptiva formulär för myndighetskonton (myndigheter och myndigheter). Tack vare integreringen med Adobe Acrobat Sign för offentlig sektor kan Adobe partners och myndighetskunder använda elektroniska signaturer i Adaptive Forms för några av de mest verksamhetskritiska och känsliga affärsområdena. Detta extra säkerhetsskikt säkerställer att alla e-signaturer är helt kompatibla med FedRAMP Moderate och ger Adobe myndighetskunder sinnesro.
* **Aktivera Salesforce-integrering med Experience Manager Forms för datautbyte** - Konfigurera integreringen mellan Experience Manager Forms och Salesforce-programmet med hjälp av inloggningsflödet för OAuth 2.0-klienten. Den här funktionen möjliggör säker och direkt autentisering och behörighet av programmet och möjliggör smidig kommunikation utan användarinblandning.
* **Optimering och förbättrad funktionalitet för arbetsflödesmotorn**: Öka arbetsflödesmotorernas prestanda genom att minimera antalet arbetsflödesinstanser. Förutom statusvärdena `COMPLETED` och `RUNNING` stöder arbetsflödet även tre nya statusvärden: `ABORTED`, `SUSPENDED` och `FAILED`.

## AEM 6.5, Service Pack 16 - 23 februari 2023

Det nya protokollet DASH (Dynamic Adaptive Streaming over HTTP) startades för strömning med adaptiv bithastighet i Dynamic Media Video-leverans (med CMAF [Common Media Application Format] aktiverat).

* Adaptiv direktuppspelning (DASH/HLS) ger en bättre tittarupplevelse för videor.
* DASH är det internationella standardprotokollet för strömning av adaptiv video och är en vida spridd bransch.
* Finns nu i Asien-Stillahavsområdet och Nordamerika och kommer snart i Europa-Mellanöstern-Afrika.

### [!DNL Forms]

* Med [Headless Adaptive Forms](https://experienceleague.adobe.com/sv/docs/experience-manager-headless-adaptive-forms/using/overview) kan dina utvecklare skapa, publicera och hantera interaktiva formulär som kan nås och interagera med via API:er, i stället för via ett traditionellt grafiskt användargränssnitt.

* [Adaptiva Forms Core-komponenter](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/introduction#features) är en uppsättning med 24 BEM-kompatibla komponenter med öppen källkod som bygger på grundvalen för Adobe Experience Manager WCM Core-komponenter. Dessa komponenter har öppen källkod och ger utvecklare möjlighet att enkelt anpassa och utöka komponenterna så att de passar organisationens specifika behov. Alla som har befintliga kunskaper för att anpassa [WCM Core-komponenter](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/get-started/authoring) kan enkelt anpassa och formatera de här komponenterna.

* Reader Extension-tjänsten på OSGi har nu olika alternativ för att aktivera import- och exportanvändningsrättigheter för en PDF för import eller export av data i Adobe Acrobat Reader.

## AEM 6.5, Service Pack 15 - 24 november 2022

### [!DNL Forms]

* AEM Forms Designer finns nu på [spanska](https://experienceleague.adobe.com/sv/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases).
* Du kan nu använda [OAuth2 för att autentisera med e-postserverprotokoll för Microsoft® Office 365 (SMTP och IMAP)](/help/forms/using/oauth2-support-for-mail-service.md).
* Du kan ställa in egenskapen [Revalidate på server](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#enabling-server-side-validation-br) på true om du vill identifiera dolda fält som ska uteslutas från ett postdokument på serversidan.
* AEM Forms Designer kräver en 32-bitarsversion av Visual C++ 2019 Redistributable (x86).

## AEM 6.5, Service Pack 14-25 augusti 2022

Endast felkorrigeringar.

## AEM 6.5, Service Pack 13 - 26 maj 2022

* Använd osynlig CAPTCHA i en adaptiv form: nu kan du använda en osynlig CAPTCHA för att visa CAPTCHA-utmaningen endast om det finns misstänkt aktivitet. Om ingen misstänkt aktivitet hittas visas inte CAPTCHA-utmaningen. Det gör det lättare att bedöma om formulär ska fyllas i av människor utan att det behövs kryssrutor, minska anpassningsarbetet och förbättra slutanvändarens upplevelse.

* Stöd har lagts till för att hämta svarshuvuden i efterbearbetningen av formulärdatamodellen för REST-slutpunkter.

* När du genererar en adaptiv formuläröversättningsfil är nu samma textsekvens i den genererade XLIFF-filen identisk med komponentsekvensen i motsvarande adaptiva formulär.

* När du lokaliserar ett adaptivt formulär och gör en liten ändring av texten i basspråket, saknas den fullständiga översättningen för alla andra språk. Problemet har åtgärdats i [!DNL Experience Manager] 6.5.13.0.

* Tillgänglighetsförbättringar för Forms:

   * Stöd för skärmläsare har lagts till för att identifiera tabellens rubrik och brödtext som fortsätter och anslutna enheter. Det hjälper skärmläsare att navigera i tabellerna på rätt sätt. (NPR-37139)
   * Stöd för att skärmläsare ska sluta navigera på HTML-arbetsytan tills en dialogruta är öppen har lagts till.

## AEM 6.5, Service Pack 12 - 24 februari 2022

* När du har konfigurerat en anslutning mellan distributioner av fjärr-DAM och platser, blir resurserna på fjärr-DAM tillgängliga i Sites-distributionen. Nu kan du uppdatera, ta bort, byta namn på och flytta resurser eller mappar i fjärr-DAM. Uppdateringarna, med viss fördröjning, är automatiskt tillgängliga i Sites-distributionen.
* Det går nu som standard att överföra en live-kopia av en källa till flera Live-kopior, utan att en ritningskonfiguration krävs.
* Status för pågående asynkrona åtgärder visas nu i användargränssnittet för att förhindra att användare av misstag utlöser flera asynkrona åtgärder på samma sökväg.
* Stöd för IMS-baserad autentisering finns för API:er i Analytics 2.0.
* API-stöd för JSON-erbjudandetypen Experience Fragment.
* Erbjudandet gäller nu för Delete-erbjudandet (Experience Fragment API) i IMS.
* Den inbyggda databasen (Apache Jackrabbit Oak) är fortfarande 1.22.9.
