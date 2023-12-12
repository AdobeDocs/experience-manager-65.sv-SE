---
title: Versionsinformation för [!DNL Adobe Experience Manager] 6.5
description: Hitta versionsinformation, nyheter, installationsanvisningar och en detaljerad ändringslista för [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
exl-id: cac14ac1-9cda-46ae-8aa3-94674bb79157
source-git-commit: 9b18d92ffabc141e83ba9a7c3694257d3dee1ea1
workflow-type: tm+mt
source-wordcount: '4204'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] 6.5 Versionsinformation om senaste Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Versionsinformation {#release-information}

| Produkt | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.19.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Typ | Service Pack-version |
| Datum | Torsdagen den 7 december 2023 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Hämta URL | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.19.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Vad ingår i [!DNL Experience Manager] 6.5.19.0 {#what-is-included-in-aem-6519}

[!DNL Experience Manager] 6.5.19.0 innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat, felkorrigeringar, prestanda, stabilitet och säkerhetsförbättringar som har släppts sedan den första tillgängligheten av 6.5 i april 2019. [Installera detta Service Pack](#install) på [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

## Viktiga funktioner och förbättringar

Några av de viktigaste funktionerna och förbättringarna i den här versionen är följande:

* Användare av sidredigeraren/bildkomponenten har aktiverat platser för att referera till resurser från Cloud Servicen Fjärrresurser. (SITES-13448, SITES-13433)
* AEM har nu stöd för sortering på serversidan för snabbare projektnavigering i listvyn. Projektnoder sorteras baserat på den användarvalda kolumnen innan de visas i gränssnittet.

### [!DNL Forms]

* **Nya adaptiva kärnkomponenter i formulär**: Lodräta flikar, villkor och kryssruta läggs till för att öka formulärens skalbarhet.
   * **[Kryssrutekomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html)**: Adaptiv Forms baserad på kärnkomponenter kan nu innehålla en kryssrutekomponent. Det gör att användare kan göra binära val, markera eller avmarkera ett visst alternativ. Det visas vanligtvis som en liten ruta som du kan klicka på eller peka på för att växla mellan två lägen: markerad och avmarkerad. Kryssrutan är ett vanligt formulärelement som används för att ange ett ja/nej- eller sant/falskt-val.

   * **[Villkorskomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html)**: Adaptiv Forms baserad på kärnkomponenter kan nu innehålla en villkorskomponent. Det gör det möjligt för formulärförfattare att infoga ett specifikt avsnitt i formuläret där användarna presenteras med de villkor eller juridiska avtal som är kopplade till användningen av en tjänst, produkt eller plattform. Den här komponenten är utformad för att informera användare om de regler, bestämmelser och skyldigheter som de godkänner genom att skicka in formuläret.

     ![Vertikala flikar, villkor och kryssrutekomponenter](/help/forms/using/assets/forms-components.png)

   * **[Lodräta flikar, komponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html)**: Adaptiv Forms baserad på kärnkomponenter kan nu ordna formulärinnehåll i en lodrät lista med flikar, vilket ger en strukturerad och navigeringsbar layout. Om du använder vertikala flikar i ett formulär kan det förbättra användarupplevelsen genom att förenkla navigeringen och förbättra organisationen av formulärinnehållet, särskilt i situationer där ett formulär innehåller flera avsnitt eller komplex information.

* **[64-bitarsversionen av AEM Forms Designer](/help/forms/using/installing-configuring-designer.md)**: 64-bitarsversionen av AEM Forms Designer ger bättre prestanda, skalbarhet och minneshantering så att du kan skapa formulär. Med 64-bitarsarkitekturen kan du enkelt hantera ännu större och mer komplexa projekt, vilket ger smidiga designarbetsflöden och optimerad effektivitet. Utöka dina formulärdesignmöjligheter och ta till vara framtiden för AEM Forms Designer med den här banbrytande releasen.

* **[Ansluta en adaptiv Forms med Microsoft® SharePoint List](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)**: AEM Forms erbjuder en OOTB-integrering för att skicka formulärdata direkt till SharePoint List, så att du kan använda funktionerna i SharePoint Lists. Du kan konfigurera Microsoft SharePoint List som en datakälla för en formulärdatamodell och använda Skicka med formulärdatamodellen för att ansluta ett anpassat formulär med SharePoint List.

* **[Stöd för att konfigurera Document of Record-egenskaper för adaptiva formulärfragment](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)**: Nu kan du enkelt anpassa dina adaptiva formulärfragment och fälten i den adaptiva formulärredigeraren.

* **64-bitars XMLFM**: 64-bitarsitereringen av XMLFM ger bättre prestanda, skalbarhet och förbättrad minneshantering. Det är den första inbyggda 64-bitarstjänsten som körs på serversidan. Genom att utnyttja sin inneboende förmåga att komma åt betydligt större minnesresurser jämfört med sin 32-bitars motsvarighet, ger XMLFM 64-bitars smidig hantering av större arbetsbelastningar för återgivning. Denna milstolpe innebär inte bara ett prestandasprång utan även viktiga förbättringar av det systemspecifika tjänstramverket i AEM Forms-servern. Den här uppdateringen gör att AEM Forms-servern sömlöst stöder alla 64-bitars inbyggda tjänster.

**Inaktuell funktion**

* ActiveMQ i AEM är föråldrat. ActiveMQ användes för kommunikation mellan två AEM publiceringsinstanser. Adobe rekommenderar att man nu använder en belastningsutjämnare.

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Åtgärdade problem i Service Pack 19 {#fixed-issues}

### [!DNL Sites]{#sites-6519}

#### Tillgänglighet{#sites-accessibility-6519}

* På en AEM Sites-sida visas länkarna när du zoomar in 200 % på sidan **[!UICONTROL Language Copy]** och **[!UICONTROL CSV Report]** i referensfältet försvinner. (SITES-11011)

#### Administratörsgränssnitt{#sites-adminui-6519}

* AEM Screens Channel **[!UICONTROL Preview]** funktionen fungerar inte och visas inte på kontrollpanelen. (SITES-15730)
* Om användargränssnittet inte kan visa referenserna under en sidförflyttning, men om de publiceras automatiskt, kommer de att *not* publicerad på nytt. (SITES-16435)
* I AEM 6.5 med Service Pack 16 eller 17 kan du inte sortera listan baserat på objekten i den kolumnen när webbplatser i listvyn med kolumnen &quot;Arbetsflöde&quot; är aktiverad. Ingen sortering sker. (SITES-15385)
* Omdirigeringsfältet har gjorts obligatoriskt för en omdirigeringssidmall. Valideringen för det obligatoriska fältet tillämpas inte och fungerar inte i dessa två scenarier: när en sida skapas utan ett obligatoriskt omdirigeringsvärde kan inte en omdirigeringssida skapas. Valideringen fungerar inte när du navigerar med kortkommandon och när fältet är markerat som ogiltigt fortsätter det inte. (SITES-15903)
* Några **Inkommande länkar** togs inte med i det visade antalet i **Referenser** -panelen. Panelen visades till exempel **Inkommande länkar (6)** men det fanns faktiskt nio inkommande länkar. (SITES-14816)

#### Klassiskt användargränssnitt{#sites-classicui-6519}

* Efter installation av snabbkorrigering i SITES-15827 ersattes dialogrutans rubriker med mellanrum mellan ord med `" "`. Radbrytningar togs också bort. (SITES-16089)
* Kodade dialogrutetitlar ger nu en dubbel kodning av titeln. (SITES-15841)
* Uppdateringen av AEM servrar från Service Pack 6.5.16 till 6.5.17 resulterade i en dubbel kodning av klassiska gränssnittsdialogrutor. (SITES-15634)

#### [!DNL Content Fragments]{#sites-contentfragments-6519}

* Ett internt serverfelmeddelande visas i Content Fragment Editor. (SITES-13550)
* Uppdateringen av `org.json` biblioteket via NPR-41291 orsakade datafel i `DefaultDataTypeConverter` i `cfm-impl` paket. Datatypskonverteringen måste vara mer flexibel. (SITES-16473)
* Hämtar felmeddelandet &quot;This content fragment version cannot be Comparing to the current version because of compatible content.&quot; Innehållsfragment bör vara jämförbara, men det är det inte. (SITES-16317)
* Ändrad JS-URL för resursväljaren från
  `https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js`
till
  `https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js` (SITES-16068)
* Anpassa det nya svarsschemat för Polaris-metadata-API:t för integrering av CFM-Polaris. (SITES-15166)
* Alla innehållsfragment ska listas där det valda innehållsfragmentet refereras. I stället visar resursreferenserna på innehållets fragmentreferenspanel 0(noll)-referenser. (SITES-15036)

#### Core Backend{#sites-core-backend-6519}

* Förbättra `StyleImpl`. (SITES-15164)
* Förbättra releasen/650-grenen av WCM-pipeline för att kunna köra integreringstester för dess moduler. (SITES-12938)

<!--#### Core Components{#sites-core-components-6519}

* A -->

#### Kampanjintegrering{#sites-campaign-integration-6519}

* I signaturkomponenten (`/apps/fpl/components/campaign/signature`) fungerade inte länkens Externalizer. Domänen lades inte till i bildkällan om HTML-kommentaren ovanför bildtaggen togs bort. Problemet hittades bara med signaturkomponenten i produktionsmiljön, inte med mellanlagringsmiljön. (SITES-16120)

<!--#### Experience Fragments{#sites-experiencefragments-6519}

* A -->

#### Foundation Components (Legacy){#sites-foundation-components-legacy-6519}

* Adobe Experience Manager (AEM) Sites Search-komponenten bryter användargränssnittet. (SITES-15087)

#### GraphQL Query Editor{#sites-graphql-query-editor-6519}

* I användargränssnittet i GraphQL Editor kan du inte bläddra igenom alla beständiga frågor när det finns ett stort antal frågor (till exempel fler än 25). (SITES-16008)
* Publiceringsstatusen för beständiga frågor sparas inte i GraphQL Editor. Knappen för att avpublicera visas i GraphQL Editor, men ikonen som anger att den beständiga frågan är publicerad visas inte. När du uppdaterar sidan visas att den beständiga frågan inte ens är publicerad. (SITES-15858)

#### Launches{#sites-launches-6519}

* Ändringar i databasen sparas inte på grund av `Oak0001` är i konflikt när flera sidor redigeras eller när innehåll redigeras. Det är normalt att göra ett nytt försök i en sådan händelse, men detta inträffar inte. (SITES-14840)

#### MSM - Live-kopior{#sites-msm-live-copies-6519}

* MSM Rollout Button fungerar inte i det grafiska användargränssnittet för pekfunktioner. (SITES-16991)
* Länkreferens uppdateras inte i Experience Fragment när en live-kopia skapas eller när ett Experience Fragment distribueras. (SITES-15460)

#### Page Editor{#sites-pageeditor-6519}

* Om du öppnade ett tema i temoredigeraren i Forms > Teman och gjorde några ändringar och sparade, och sedan klickade på Förhandsgranska, visas en inläsningsikon, men förhandsvisningen läses inte in. (SITES-17164)
* Markering av flera dokumentfiltyper i filtret för resurstyp fungerar inte på sidkonsolen. Inga resultat hittas även om resultaten för en viss filtyp är tillgängliga. Därför kan man inte filtrera flera dokument. De måste använda flera dokumenttyper och måste filtrera en åt gången. (SITES-14047)
* När du har uppgraderat en instans från AEM 6.5.17 och AEM 6.5.18, inifrån sidredigeraren, om du har valt **[!UICONTROL Publish Page]**, omdirigeras du till en URL som inte finns. Användaren bör omdirigeras till publiceringsguiden. (SITES-15856)
* Överflödig kopiering från AEM Urklipp under en inklistring från operativsystemets Urklipp. (SITES-15704)
* I Resurser, välja **[!UICONTROL Documents]**, sedan under **[!UICONTROL Filtertype]**, markera **[!UICONTROL Microsoft® Word]** eller **[!UICONTROL Microsoft® Excel]** visar inga resultat trots att det finns filer av båda typerna. (SITES-14837)

### [!DNL Assets]{#assets-6519}

* När du skapar eller sparar en gemensam mapp skapas tre grupper i en admin-kontrollpanel. (ASSETS-26700)
* Det går inte att skilja publiceringsresurser åt Experience Manager eller Brand Portal. (NPR-41320)
* När du markerar kryssrutor på sökpanelen och avmarkerar någon av dem avmarkeras alla kryssrutor. (ASSETS-26377)

#### [!DNL Dynamic Media]{#assets-dm-6519}

* När en resurs har överförts till AEM `update_asset` arbetsflödet aktiveras. Arbetsflödet avslutas aldrig. Om du tittar på arbetsflödesinstanserna avslutas arbetsflödet upp till produktöverföringssteget. Nästa steg är batchöverföring från Scene7. Användaren kan se att resursen finns i Scene7 från Dynamic Media Classic-appen. (ASSETS-30443)
* En anpassad serverdel (API-slutpunkt) returnerar ett felaktigt Dynamic Media-filnamn (Scene7). Det inträffar när en resurs tas bort och ersätts med en tillgång med samma namn. Den anpassade servern returnerar det gamla Dynamic Media-filnamnet (Scene7), medan ett jcr-API-anrop returnerar rätt filnamn. (ASSETS-29476)
* Även efter att Synkronisering har inaktiverats på mappnivå visar loggarna utlösaren Scene7 ReplicateOnModifyListener. The `ReplicateOnModifyListener/Worker` bör inte bearbeta mappresurser och innehållsfragment som inte finns i Dynamic Media. (ASSETS-26705)
* Personer med nedsatt syn påverkas om fokus inte syns i listruteelement (Endast innehåll, Visa, Fler alternativ) i svart- och vitt-läge med hög kontrast. (ASSETS-25759)
* Personer med nedsatt syn påverkas om kontrastförhållandet för luminiscens för text på en sida är mindre än 4,5:1. (ASSETS-25756)
* Skärmläsare lägger inte till någon berättarröst i det visade popup-meddelandet när data har skickats. (ASSETS-25755)
* Skärmläsare känner inte igen landmärken på sidan (Dynamic Media; skapar en videokodningsprofil) när de navigerar med hjälp av kortkommandon för landmärke/region `D/R`. (ASSETS-25752)
* Skärmläsare känner inte igen flera landmärken på sidan (Dynamic Media; skapar interaktiv video) när de navigerar med kortkommandon för landmärke/region `D/R`. (ASSETS-25750)
* Skärmläsare (NVDA/JAWS/Skärmläsaren) känner inte igen landmärkena i **Redigera resurs** sida vid navigering med kortkommandon `D/R`. (ASSETS-25744)
* Användaren får ett tomt/falskt asynkront jobbmeddelande, men den anslutna resursen har publicerats. (ASSETS-29342)

### [!DNL Forms]{#forms-6519}

#### [!DNL Adaptive Forms]

<!-- Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.19.0 Forms add-on package release is scheduled for Thursday, November 30, 2023. A list of Forms fixes and enhancements would be added to this section post the release.-->

<!--* Adding Access Control List for `fd-cloudservice` user to be able to read or update the Microsoft&reg; configurations under `cloudconfigs/microsoftoffice`. (FORMS-11142) -->

<!--LEFT BULLET LIST HERE IN CASE OF REUSE BY FORMS IN THE FUTURE 
* **Document Services**
  * text
* **Adaptive Forms** 
  * text
* **Accessibility**
  * text
* **Interactive Communications**
  * text -->

<!--### Commerce{#commerce-6519}

* A -->

* När en användare lägger till ett verktygsfält i ett anpassat formulär, visar behållaretiketten felaktigt beteende eftersom den inte ändras till det språk som författaren valt för Forms. (FORMS-1371)
* I AEM Forms Workspace väljer listrutan det första alternativet som standard i användargränssnittet. (FORMS-1346)
* Språkkonfigurationen i AEM har ingen effekt om du använder språkområden med fem tecken och decimalavgränsaren inte återges korrekt i bokstaven. (FORMS-1344)
* När en användare genererar XML-utdata med Workbench-processen misslyckas detta för några av filerna. (FORMS-1314)
* När en användare genererar en förhandsgranskning för DOR (Document of record) på andra språk än engelska fungerar den inte. (FORMS-11106)
* När en användare konverterar vissa bildfiler med PDFG i en OSGI-instans som är baserad på Linux med JDK11, konverteras den inte. (FORMS-11105)
* När användare installerar AEM Forms-tillägget bryts innehållsträdspanelen i AEM Sites. (FORMS-10912)
* När en användare kopierar datum med NVDA-skärmläsare från datumväljarkomponenten läses det inte korrekt. (FORMS-10805) 
* I Forms regelredigerare kan användaren inte ange värdet för alternativknappen/kryssrutan när datavärdestypen är Boolean. (FORMS-10713)
* När en användare lägger till objekt i ett adaptivt formulär läggs det till i omvänd ordning i en nedrullningsbar lista. (FORMS-10456)
* När en listruta har rensats med regelredigeraren visas det första angivna värdet fortfarande, även om värdet har rensats. (FORMS-9963) 
* Användarna kan inte komma åt formulärtiteln med skärmläsare som NVDA. (FORMS-8815) 
* Användare kan inte komma åt underrubriken i ett formulär med skärmläsare som NVDA. (FORMS-8814) 
* I HTML-formulärets sidkälla är åtkomstnyckelattributet tomt och fungerar inte. (FORMS-5753) 
* I dialogrutan Om arbetsyta visas texten&quot;Adobe Experience Manager - Forms&quot; som text. (FORMS-5748)

#### [!DNL Forms Designer]{#forms-designer-6519}

* När en användare försöker läsa icke-interaktiv PDF forms via skärmläsare, läses eller hoppas vissa listobjekt över. (LC-3921645) 
* När en användare går igenom de redigerbara fälten går det inte till alla PDF formulärfält på ett konsekvent sätt. (LC-3921631) 
* Ordningen på taggarna ändras slumpmässigt i PDF, även om taggningen i Forms Designer är korrekt. (LC-3921313) 
* En lista visas inte korrekt i taggarna i Adobe Acrobat Reader eller Adobe Acrobat DC. (LC-3921306)
* Rubriknivåer som tilldelas korrekt i Forms Designer ändras slumpmässigt till `<P>` i Adobe Acrobat. (LC-3921305) 
* I en tabell kan ID:t för ett objekt inte ändras när det har tilldelats. (LC-3921134) 
* Om det finns sammanfogade celler i tabellen är inget GUI tillgängligt för att ange omfånget (rad och kolumn) och omfånget i en komplex tabell i AEM Forms Designer. (LC-3919532) 

### Foundation{#foundation-6519}

* När du skapar en språkkopia på språkets rotnivå justeras inte sökvägarna på sidan. Om språkkopian skapades, inte för språkroten utan för sidorna under den, ändrades sökvägen korrekt. (NPR-41364)
* Verktygstipset &quot;Relativ datumpresentation&quot; kan bara stängas genom att trycka på Esc på tangentbordet. Verktygstipset bör stängas när användaren väljer någon del av användargränssnittet. (NPR-41394)
* Olokaliserad sträng `Something went wrong while adding the private key.` när fel privata nyckelfil läggs till i **Redigera användare** > **Nyckelbehållare**. (NPR-41366)
* Ikoner krävs för Microsoft® SharePoint och Microsoft® One Drive i AEM 6.5-miljön. (NPR-41354)
* Olokaliserad &quot;UserId/Password mismatch&quot;. sträng i **Säkerhet** > **Användare** > **Skapa** -dialogrutan. (NPR-41245)
* Leveranskod och händelsehanterare läses in två gånger, vilket bryter de Coral3-baserade användargränssnitten som användaren skapat. (NPR-41171)
* Avmarkeringen fungerar inte korrekt när du har använt Markera allt i AEM Sites-konsolen. (NPR-41304)

<!--#### Content distribution{#foundation-content-distribution-6519}

* T -->

#### Integreringar{#integrations-6519}

* SMS-länkar i en AEM e-postkampanj skrivs inte korrekt. De innehåller ett ankarelement i HTML. (NPR-41211)
* Inspelning som används på kontokonfigurationsskärmen ska inte använda den nya autentiseringstypen. (NPR-41210)
* Flyttar importschemaläggare för analysrapport från `ManagedPollConfig` till att sälja jobb. När två olika analysramverk bifogades med olika rapportsviter till två olika webbplatser, `ManagedPollConfig` avfrågar bara en av dem. (NPR-41209)
* När värdet återställs till standardvärdet förblir den tidigare markerade knappen för tidsram aktiverad. På kontrollpanelen för innehållsinsikter i AEM är tidsramen inställd på veckan som standard och innehållsinsikter visas som veckodata. Om användaren nu väljer andra alternativ för tidsramar, som timme, dag, månad och år, ändras data enligt det valda värdet. Om värdena återställs är emellertid den synliga tidsramen som standard vecka, men fortfarande det tidigare markerade tidsbildrutealternativet. (NPR-41246)

#### Oak{#oak-6519}

* Bakåtportverktyget för att hastighetsbegränsa skrivningar till AEM om asynkron indexering är fördröjd. (NPR-40985)

#### Plattform{#foundation-platform-6519}

* QueryBuilder-frågor med hakparenteser översätts felaktigt till xpath. (NPR-41298)

<!--#### Replication{#foundation-replication-6519}

* R -->

<!--#### Sling{#foundation-sling-6519}

* W -->

#### Översättningsprojekt{#foundation-translation-6519}

* När språkkopian av sidan&quot;A&quot; skapas bör den automatiskt skapa språkkopiorna av de refererade sidorna, upplevelsefragment, innehållsfragment och resurser. Dessutom bör den nya språkkopian av sida A i den nya sökvägen ha sina referenser uppdaterade till de nya språkkopiorna av sidorna, upplevelsefragment, innehållsfragment och resurser. (NPR-41076)

<!--#### User interface{#foundation-ui-6519}

* A -->

<!--#### WCM{#wcm-6519}

* A -->

#### Arbetsflöde{#foundation-workflow-6519}

* Det går inte att slutföra en åtgärd i Inkorgen. Endast ett odefinierat värde visas i listrutan när du försöker slutföra uppgiften och välja en åtgärd. Det innebär att användare inte kan använda AEM 6.5.18-Service Pack. (NPR-41402 och NPR-41473)
* Det går inte att slutföra uppgifter i Inkorgen. Det finns inget värde (endast&quot;undefined&quot;) i listrutan när du försöker slutföra åtgärden för zip-filer, tillgångsrapporter, flytt (om åtgärden lyckades eller misslyckades) eller när resursen förfaller. (NPR-41305)
* När en användare väljer **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > instanser, väljer arbetsflödet som körs och väljer **[!UICONTROL View Payload]** resulterar det i en felsida på 500. (NPR-41325)

## Installera [!DNL Experience Manager] 6.5.19.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.19.0 kräver [!DNL Experience Manager] 6.5. Se [uppgraderingsdokumentation](/help/sites-deploying/upgrade.md) för detaljerade anvisningar. <!-- UPDATE FOR EACH NEW RELEASE -->
* Service Pack-nedladdning finns på Adobe [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.19.0.zip).
* På en distribution med MongoDB och flera instanser installerar du [!DNL Experience Manager] 6.5.19.0 på en av författarinstanserna med hjälp av Package Manager.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe rekommenderar inte att du tar bort eller avinstallerar [!DNL Experience Manager] 6.5.19.0-paket. Innan du installerar paketet bör du skapa en säkerhetskopia av `crx-repository` om du måste rulla tillbaka den. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Installera Service Pack på [!DNL Experience Manager] 6.5{#install-service-pack}

1. Starta om instansen innan installationen om instansen är i uppdateringsläge (när instansen uppdaterades från en tidigare version). Adobe rekommenderar att du startar om om den aktuella upptiden för en instans är hög.

1. Ta en ögonblicksbild eller en ny säkerhetskopia av din [!DNL Experience Manager] -instans.

1. Hämta Service Pack från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.19.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Öppna Pakethanteraren och välj **[!UICONTROL Upload Package]** för att överföra paketet. Mer information finns på [Pakethanteraren](/help/sites-administering/package-manager.md).

1. Markera paketet och välj **[!UICONTROL Install]**.

1. Om du vill uppdatera S3-anslutningen stoppar du instansen efter installationen av Service Pack, byter ut den befintliga kopplingen mot en ny binär fil som finns i installationsmappen och startar om instansen. Se [Amazon S3 - datalager](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Dialogrutan för pakethanterarens gränssnitt avslutas ibland när Service Pack installeras. Adobe rekommenderar att du väntar på att felloggarna ska stabiliseras innan du får åtkomst till distributionen. Vänta på de specifika loggarna för avinstallationen av uppdateringspaketet innan du försäkrar dig om att installationen lyckas. Vanligtvis inträffar det här problemet i [!DNL Safari] webbläsare, men kan ibland inträffa i vilken webbläsare som helst.

**Automatisk installation**

Det finns två olika metoder som du kan använda för att installera automatiskt [!DNL Experience Manager] 6.5.19.0<!-- UPDATE FOR EACH NEW RELEASE -->

* Placera paketet i `../crx-quickstart/install` när servern är tillgänglig online. Paketet installeras automatiskt.
* Använd [HTTP-API från Package Manager](/help/sites-administering/package-manager.md#package-share). Använd `cmd=install&recursive=true` så att de kapslade paketen installeras.

>[!NOTE]
>
>Experience Manager 6.5.19.0 stöder inte installation av Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validera installationen**

Om du vill veta vilka plattformar som är certifierade för att fungera med den här versionen kan du läsa [tekniska krav](/help/sites-deploying/technical-requirements.md).

1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience Manager (6.5.19.0)` under [!UICONTROL Installed Products]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Alla OSGi-paket är **[!UICONTROL ACTIVE]** eller **[!UICONTROL FRAGMENT]** i OSGi Console (Use Web Console: `/system/console/bundles`).

1. OSGi-paketet `org.apache.jackrabbit.oak-core` är version 1.2.2.17 eller senare (Använd webbkonsol: `/system/console/bundles`). <!-- NPR-41292 for 6.5.19.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installera Service Pack för [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Anvisningar om hur du installerar Service Pack på Experience Manager Forms finns i [Installationsanvisningar för Experience Manager Forms Service Pack](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>Funktionen Adaptive Forms, som finns i [AEM 6.5 QuickStart](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html), är endast avsedd för prospektering och utvärdering. För produktion krävs en giltig licens för AEM Forms, eftersom Adaptive Forms-funktionaliteten kräver rätt licensiering.

### Installera GraphQL Index Package för Experience Manager Content Fragments{#install-aem-graphql-index-add-on-package}

Kunder som använder GraphQL måste installera [Experience Manager Content Fragment with GraphQL Index Package 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

På så sätt kan du lägga till den indexdefinition som krävs baserat på de funktioner som de faktiskt använder.

Om du inte installerar det här paketet kan GraphQL-frågor bli långsamma eller misslyckas.

>[!NOTE]
>
>Installera bara det här paketet en gång per instans. Det behöver inte installeras om med varje Service Pack.

### UberJar{#uber-jar}

UberJar för [!DNL Experience Manager] 6.5.19.0 finns i [Maven Central-arkivet](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.19/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Information om hur du använder UberJar i ett Maven-projekt finns i [använda UberJar](/help/sites-developing/ht-projects-maven.md) och inkludera följande beroende i projektens POM: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.19</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar och andra tillhörande artefakter finns tillgängliga i Maven Central Repository i stället för i Adobe Public Maven-arkivet (`repo.adobe.com`). Huvudfilen för UberJar byter namn till `uber-jar-<version>.jar`. Så det finns ingen `classifier`, med `apis` som värdet, för `dependency` -tagg.

## Föråldrade och borttagna funktioner{#removed-deprecated-features}

Se [Föråldrade och borttagna funktioner](/help/release-notes/deprecated-removed-features.md/).

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



* **Relaterad till eken**
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
Nya mappar med `cache` och `diff-cache` skapas automatiskt och du får inte längre något undantag relaterat till `mvstore` i `error.log`.

* Uppdatera dina GraphQL-frågor som kan ha använt ett anpassat API-namn för innehållsmodellen så att standardnamnet för innehållsmodellen används i stället.

* En GraphQL-fråga kan använda `damAssetLucene` index i stället för `fragments` index. Den här åtgärden kan leda till att GraphQL-frågor misslyckas eller tar lång tid att köra.

  För att åtgärda problemet `damAssetLucene` måste konfigureras så att följande två egenskaper ingår i `/indexRules/dam:Asset/properties`:

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

* När du försöker flytta, ta bort eller publicera antingen innehållsfragment, platser eller sidor uppstår ett problem när referenser till innehållsfragment hämtas, eftersom bakgrundsfrågan misslyckas. Funktionen fungerar alltså inte.
Du måste lägga till följande egenskaper i indexdefinitionsnoden för att få en korrekt åtgärd `/oak:index/damAssetLucene` (ingen omindexering krävs):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Om du uppgraderar [!DNL Experience Manager] från 6.5.0 till 6.5.4 till senaste Service Pack på Java™ 11, se `RRD4JReporter` undantag i `error.log` -fil. Starta om instansen av [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Användare kan byta namn på en mapp i en hierarki i [!DNL Assets] och publicera en kapslad mapp i [!DNL Brand Portal]. Mappens namn uppdateras dock inte i [!DNL Brand Portal] tills rotmappen publiceras på nytt.

* Följande fel och varningsmeddelanden kan visas under installationen av [!DNL Experience Manager] 6.5.x.x:
   * &quot;När Adobe Target-integreringen är konfigurerad i [!DNL Experience Manager] med Target Standard API (IMS-autentisering) och sedan exportera Experience Fragments till Target så att fel erbjudandetyper skapas. I stället för att skriva&quot;Experience Fragment&quot;/källa&quot;Adobe Experience Manager&quot; skapar Target flera erbjudanden med typen&quot;HTML&quot;/källa&quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Validering på serversidan av adaptiva formulär misslyckas när sammanställningsfunktioner som SUM, MAX och MIN används (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Den aktiva punkten i en interaktiv Dynamic Media-bild syns inte när du förhandsgranskar mediefilen via visningsprogrammet för den köpbara kanalen.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Timeout väntar på att registerändringen ska slutföras utan registrering.

* Från och med AEM 6.5.15, JavaScript-motorn i Rhino från ```org.apache.servicemix.bundles.rhino``` paket har ett nytt värdbeteende. Skript som använder strikt läge (```use strict;```) måste deklarera variablerna korrekt, annars körs de inte, utan genererar i stället ett körningsfel.

### Kända fel för AEM Forms

#### Plattformar som stöds

* JDK 11.0.20 stöds inte för installation av AEM Forms i JEE Installer. Endast JDK 11.0.19 och tidigare versioner stöds för installation av AEM Forms i JEE Installer. (FORMS-10659)

#### Installation

* På JBoss® 7.1.4-plattformen när användaren installerar Experience Manager 6.5.16.0 eller senare Service Pack, `adobe-livecycle-jboss.ear` distributionen misslyckas. (CQ-4351522, CQDOC-20159)

<!-- 
* After upgrading to AEM Forms 6.5.18.0 JBoss&reg; Turnkey full installer environment on Windows Server 2022, when compiling Output client application code using Java&trade; 11, the following compilation error may occur:
  
  ```
  error: error reading [AEM_Forms_Installation_dir]\sdk\client-libs\common\adobe-output-client.jar; java.net.URISyntaxException: 
  Illegal character in path at index 70: file:/[AEM_Forms_Installation_dir]/sdk/client-libs/common/${clover.jar.name} 1 error
  
  ```
  
  To resolve the issue, perform the following steps:
    1. Navigate to `[AEM_Forms_Installation_dir]\sdk\client-libs\common\` and unzip `adobe-output-client.jar` to extract the `Manifest.mf` file.
    1. Update the `Manifest.mf` file by removing the entry `${clover.jar.name}` from the class-path attribute. 

        >[!NOTE]
        >
        > You can also use an in-place editing tool, for example, 7-zip, to update the `Manifest.mf` file.  

    1. Save the updated the `Manifest.mf` in the `adobe-output-client.jar` archive. 
    1. Save the modified `adobe-output-client.jar` file and rerun the setup. (CQDOC-20878) -->

* När du har installerat AEM Service Pack 6.5.19.0 med fullständigt installationsprogram misslyckas EAR-distributionen på JEE med JBoss® Turnkey.
Du löser problemet genom att leta reda på `<AEM_Forms_Installation_dir>\jboss\bin\standalone.bat` fil och uppdatera `Adobe_Adobe_JAVA_HOME` till `Adobe_JAVA_HOME` för alla förekomster innan konfigurationshanteraren körs. (CQDOC-20803)

#### Installera serverdelen (AEM Service Pack 6.5.14.0 eller tidigare)

* Om du uppgraderar till AEM Service Pack 6.5.15.0 eller senare, och din AEM körs på Tomcat 8.5.88, är det obligatoriskt att installera serverfragmentet *före* du fortsätter med installationen av Service Pack 6.5.15.0 eller senare.
* Det är obligatoriskt att installera serverdelen för alla programservrar utom de som körs på JBoss® EAP 7.4.0.

**Så här installerar du serletfragmentet:**

1. Hämta serverfragmentet från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).
1. Starta programservern.
1. Vänta tills loggarna har stabiliserats och kontrollera pakettillståndet.
1. Öppna Web Console Bundles. Standardwebbadressen är `http://[Server]:[Port]/system/console/bundles`.
1. Välj **[!UICONTROL Install]** eller **[!UICONTROL Update]**.
1. Välj det hämtade fragmentet
   `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`
1. Välj **[!UICONTROL Install]** eller **[!UICONTROL Update]**.
1. Vänta tills programservern har stabiliserats.
1. Stoppa programservern.

#### Adaptiv Forms

* När ett adaptivt formulär publiceras kommer alla dess beroenden, inklusive profiler, att publiceras på nytt, även om inga ändringar har gjorts i dem. (FORMS-10454)
* När en användare väljer att konfigurera ett fält för första gången i ett adaptivt formulär visas inte alternativet att spara en konfiguration i egenskapsläsaren. Problemet åtgärdas genom att ett annat fält i det adaptiva formuläret konfigureras i samma redigerare.
* När användare utför en sändningsåtgärd misslyckas överföringen med ett fel:
  ` javax.servlet.ServletException: java.lang.NoSuchMethodError`
För att lösa problemet [kompilera om Sling-skript som JSP, Java och Sightly](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16543.html?lang=en#resolution). (FORMS-8542)


## OSGi-paket och innehållspaket som ingår{#osgi-bundles-and-content-packages-included}

Följande textdokument listar de OSGi-paket och innehållspaket som ingår i [!DNL Experience Manager] 6.5.19.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Förteckning över OSGi-paket i Experience Manager 6.5.19.0](/help/release-notes/assets/65190_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Förteckning över innehållspaket i Experience Manager 6.5.19.0](/help/release-notes/assets/65190_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Begränsade webbplatser{#restricted-sites}

Dessa webbplatser är bara tillgängliga för kunder. Om du är kund och behöver åtkomst kontaktar du din kontoansvarige på Adobe.

* [Nedladdning av produkt på licensing.adobe.com](https://licensing.adobe.com/)
* [Kontakta Adobe kundsupport](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] produktsida](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* [Prenumerera på produktuppdateringar med Adobe prioritet](https://www.adobe.com/subscription/priority-product-update.html)
