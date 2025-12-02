---
title: Versionsinformation för  [!DNL Adobe Experience Manager] 6.5
description: Hitta versionsinformation, nyheter, installationsguider och en detaljerad ändringslista för  [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 6eccdab5cd492686dda2aca3fee4df171a2d9011
workflow-type: tm+mt
source-wordcount: '8925'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] 6.5 Versionsinformation om senaste Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Versionsinformation {#release-information}

| Produkt | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.24.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Typ | Service Pack-version |
| Datum | 26 november 2025 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Hämta URL | [Programdistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.24.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

<!-- OLD DOWNLOAD URL
(https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip) -->

## Vad ingår i [!DNL Experience Manager] 6.5.24.0 {#what-is-included-in-aem-6524}

[!DNL Experience Manager] 6.5.24.0 innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat samt felkorrigeringar. Det innehåller även förbättringar av prestanda, stabilitet och säkerhet som släppts sedan den första tillgängligheten av 6.5 i april 2019. [Installera detta Service Pack](#install) på [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

<!--
## Key features and enhancements
-->




## Åtgärdade problem i Service Pack 24 {#fixed-issues}

<!-- 6.5.24.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Assets] {#assets-sp24}

* Efter uppdatering till version 6.5.23.0 orsakade sortering av mappar efter ändringsdatum i kortvyn svårigheter med att hitta nyligen ändrade resurser för anläggningsdistributioner. (ASSETS-56946)
* Upprepade varningsloggposter genereras vid körning av schemaläggare. (ASSETS-5254)
* Titelsortering fungerar inte i listvyn. (ASSETS-50716)
* Fönstret Samlingsegenskaper stängs inte ens när du klickat på Avbryt. (ASSETS-48504)

* Ett *ogiltigt URL*-fel inträffar vid försök att kommentera resurser i AEM 6.5.22. (NPR-42684)
* Formuläret för Assets-metadataredigeraren initieras inte om efter att relaterade eller orelaterade åtgärder har utförts. (ASSETS-5207)
* När resurser från fjärr-DAM synkroniseras om till platsens lokala plats, uppdateras resursernas publiceringsstatus felaktigt till `Not published`. (ASSETS-48958)
* Problem uppstod vid uppgradering från SP23 till 6.5 LTS-versionen. (ASSETS-50541)

### [!DNL Sites]{#sites-6524}

#### Tillgänglighet {#sites-accessibility-6524}

* Dialogrutan **Växla visningsformat** har nu stöd för en fullständig tangentbordsåtgärd. Fokus hoppar inte längre över knappen **Visa inställningar** och standardtangenterna (`Tab`, `Enter`, `Space`) fungerar konsekvent. (SITES-24306)
* Tangentbordsanvändare kan ta bort de publicerade statustaggarna utan en mus. Fokusmarkeringar på varje tagg och aktivering fungerar med `Enter`/`Space` och Backsteg/Delete. Taggkontrollen fungerar nu som en knapp som förbättrar skärmläsarfeedback och uppfyller WCAG 2.1.1-tangentbordet. (SITES-24491)
* Filterfältet flödar om snabbt i smala visningsrutor. Markeringskontroller och resultat ligger kvar i visningsrutan med 400 % zoom, vilket eliminerar vågrät rullning och innehållets skärpa. (SITES-24708)
* AEM återställer fullständig tangentbordsåtkomst till knapparna ContextHub Reset, Persona och Device. Tabb- och piltangenterna når varje kontroll, visar en synlig fokusindikator och aktiverar åtgärder med `Enter` eller `Space`. Skärmläsare meddelar tydliga etiketter. (SITES-24939)
* Datumindata och väljaren är helt synliga vid 320 px. Den modala förvrängningen för Timewarp använder responsiv storlek, vilket innebär att kontrollen inte längre försvinner eller försvinner på den minsta visningsrutan. (SITES-24962)
* Referenslisten har nu stöd för 400 % webbläsarzoom utan att förlora åtkomsten till innehållet. Rälen använder responsiv storlek i stället för en fast bredd, så objekten förblir synliga och kan markeras med 1280 × 1024. (SITES-24972)
* Filters Rail fungerar nu med 400 % zoom. Rälens storlek ändras med relativa enheter och varken blockerar eller döljer filterkontroller. Användarna kan visa och välja alla filteralternativ utan vågrät rullning eller bortfallsmål. (SITES-24981)
* Tangentbordsanvändare kan använda formateringsmenyer i det modala Teaser-läget. Om du trycker på `Enter` eller `Space` på **List** eller **Paragraph Format** öppnas popup-fönstret, piltangenterna navigerar och `Enter` tillämpar markeringen. `Escape` stänger menyn och återställer fokus till den utlösande kontrollen, vilket ger ett konsekvent verktygsfältsarbetsflöde. (SITES-25235)
* Färgväljaren för färgrutor ligger nu kvar i visningsrutan vid 320 px. I pekaren visas alla färgrader och det finns stöd för bläddring, så att författare kan välja en färgruta på små skärmar. (SITES-25274)
* Demografiska verktygsfältets listrutor fungerar nu helt med tangentbordet. När du öppnar en meny flyttas fokus till det första alternativet, piltangenterna navigerar i listan och Esc/Tabb stängs eller flyttas framåt utan att dumpa fokus till verktygsfältet. Interaktiva objekt använder rätt semantik så att NVDA och andra läsare kan meddela alternativ korrekt. (SITES-25310)
* Add Component in the Content tree works as DESIGN on AEM 6.5 SP24. Det första felet uppstod när författarbehörigheter saknades i en lokal konfiguration, inte från AEM. Författare med redigeringsbehörighet kan aktivera knappen och lägga till komponenter via tangentbordet eller musen. (SITES-25312)
* Tangentbords- och skärmläsaråtkomst i det demografiska verktygsfältet fungerar nu tillförlitligt. Författare som använder NVDA kan gå igenom **Commerce**, **Persona** och 88 med pilar, följa tydlig fokusfeedback och förstå vilken flik som är aktiv. (SITES-25326)

* Länken **Hoppa till innehåll** flyttar nu tangentbordsfokus till rubriken för huvudinnehållet. Fokus förblir synligt på ett unikt identifierat mål, så skärmläsare kan presentera rätt avsnitt. Ändringen uppfyller WCAG 2.4.1 och 2.4.3. (SITES-24061)
* Tangentbordsnavigering i trädet för webbplatsens hemsida följer en logisk sekvens när **Markera alla** har använts. Fokuset flyttas från **Markera allt** till nästa kontroll (vänster rälsknapp) i stället för att hoppa tillbaka till början av sidan. (SITES-24307)
* Avsnittsrubriker och redigeringskontroller i Sites editor svarar på tangentbordsfokus och aktivering. Tangentbordsanvändare visar samma titel och åtgärder som tidigare bara visades vid hovring. (SITES-24479)
* Knappar i Sites Editor visar beskrivande namn i stället för generiska eller saknade etiketter. Hjälpmedelstekniker lanserar rätt åtgärd, vilket ökar klarheten och minskar antalet felklick. (SITES-24480)
* Skärmläsare får ett tal om att&quot;läsa in&quot; medan platsvyn uppdateras. Uppdateringen lägger till en dedikerad statusregion och skriver meddelandet i den programmatiskt, vilket bekräftar förloppet utan att flytta fokus. (SITES-24481)
* Assets sidospår har nu en rensad **Close**-kontroll och återgår till växlingsknappen. Användare av tangentbord och skärmläsare stänger av panelen direkt i stället för att tabba igenom alla kontroller. Ändringen minskar antalet tangenttryckningar och matchar det förväntade panelbeteendet. (SITES-24489)
* Fliklistan ARIA i Sites Page Editor innehåller ett beskrivande namn. Skärmläsare identifierar nu kontrollen som en fliklista och läser rätt etikett, så att användarna kan hitta rätt uppsättning flikar och flytta mellan dem på ett tillförlitligt sätt. (SITES-24492)
* Sökfunktionen i redigeraren visar nu resultat för skärmläsare. När användare skriver rapporterar ett live-statusmeddelande antalet träffar och uppdateringar utan att flytta fokus. Tangentbordsanvändare upptäcker resultatet direkt. (SITES-24506)
* Val av rader i listvyn förbättras för användare med hjälpfunktioner. Kryssrutan visar ett beskrivande namn som härleds från radrubriken, så meddelandena är korta och beskriver åtgärden korrekt. (SITES-24514)
* Korrigerade tillgänglighetsnamn för listvyn. Tabellen tar bort `aria-label` från icke-interaktiva element och tilldelar etiketten till den användbara länken eller knappen. Nu kan skärmläsaranvändare höra korrekta, icke-duplicerade etiketter i hela kolumnen. (SITES-24515)
* Den klibbiga rubriken dolde inte dialogrutan för teaser vid användning med hög zoom. Innehållet förblir läsbart och kan användas vid zoomning i 200 % och 400 %, med lodrätt flöde och utan bortfall. (SITES-24523)
* När du skriver i sökfältet aktiveras inte längre ett för tidigt meddelande om det första resultatet eller en oavsiktlig aktivering. Nu visas ett kort statusmeddelande med resultatantal, medan fokus ligger kvar i fältet tills användaren navigerar till listan. (SITES-24658)
* Alternativtextfältet i textredigerarens hyperlänksdialogruta visar nu en programmatisk etikett. Skärmläsare meddelar &quot;Alternativ text&quot; för fältet och fokus hamnar på den namngivna kontrollen. Den här korrigeringen förbättrar navigeringen för tangentbords- och talanvändare. (SITES-24675)
* Ett live-statusmeddelande har lagts till i referensfältet så att hjälpmedelstekniken omedelbart kan meddela ändringar. Om du markerar flera objekt visas ett tydligt meddelande om referenstillgänglighet, vilket förhindrar tysta lägesändringar och minskar antalet upprepade åtgärder. (SITES-24678)
* Dialogrutan Bild meddelar nu inläsningsstatus via en ARIA-region. Skärmläsare hör meddelandet&quot;Läser in, vänta&quot; medan rotationsrutan visas. Och en klar uppdatering när innehållet är klart, så att användarna vet när de kan interagera. (SITES-24697)
* Dialogrutan Länkval visar nu en aktiv region med sökresultat. Skärmläsare hör statusen&quot;resultaten har uppdaterats&quot; efter varje sökning utan att flytta fokus, så användarna får en tydlig bekräftelse på att sökningen har slutförts. (SITES-24700)
* Dialogrutan Länkval omformas nu till 320 px. Alla fält och åtgärder förblir synliga och användbara, och den vågräta rullningslisten visas inte längre. (SITES-24709)
* Dialogrutan Länkmarkering använder nu samma etikett för både texten på skärmen och hjälpmedelsnamnet för varje trädobjekt. Skärmläsare meddelar varje objekt medan de flyttar med piltangenterna, inklusive den sista nivån, så att tysta noder och felmatchade namn tas bort. (SITES-24710)
* Ändra filter rapporterar nu status som expanderat eller komprimerat. Knappen växlar `aria-expanded` synkroniserat med filterpanelen och visar ett enda tydligt namn (&quot;Ändra filter&quot;), vilket tar bort det förvirrande&quot;filtret?&quot; meddelande. Skärmläsaranvändare kan förutsäga resultatet av att aktivera kontrollen. (SITES-24713)
* Modala sidhuvuden täcker inte längre innehåll med bredden 320 px. Rubriken frigörs från sitt klisterläge och dialogrutans brödtext rullas så att alla fält och åtgärdsknappar förblir synliga och användbara. Tangentbordsanvändare kan nå alla kontroller utan att förlora fokus. (SITES-24718)
* Länkarna för appnavigering visar nu rätt länksemantik. Skärmläsare annonserar varje objekt som en länk i stället för som ett listobjekt, vilket förbättrar tangentbordsnavigering och röstkontroll. Listbehållaren innehåller semantik för listor, medan länkar fortfarande är de mål som kan fokuseras. (SITES-24719)
* Resultatstatusen visas nu för skärmläsare när filtren ändras. NVDA läser både antalet &quot;X av Y-resultat&quot; och meddelandet &quot;inga resultat&quot;. Sidindelningsstatusen använder en aktiv region som uppdateras på plats, så att användarna får en bekräftelse utan att flytta fokus. (SITES-24720)
* Rotationsknappen i Carousel-dialogrutan meddelar nu ett enda kortfattat namn för skärmläsare. Kontrollen upprepas inte längre både gruppetiketten och indataetiketten, vilket minskar komplexiteten och förvirringen för NVDA-användare. (SITES-24725)
* Söklistan på hjälpmenyn innehåller rätt semantik. Behållaren visar en lista och varje resultat behåller en länk utan att rollen är i konflikt. NVDA och JAWS meddelar länkar korrekt och navigeringen är konsekvent. (SITES-24729)
* Adobe har korrigerat popup-fönstret för färgrutor i användarinställningarna så att NVDA meddelar färgrutan som är i fokus, inte den tidigare markerade färgrutan. Tangentbordsanvändare får korrekta färgnamn när de går igenom listan och kan bekräfta att du valt rätt färg. (SITES-24739)
* NVDA läser nu den fullständiga beskrivningen i trädkatalogen. På informationspanelen visas text med flera rader som ett värde och den länkas till fältetiketten. Tangentbordsanvändare hör hela texten när de tabbar sig igenom skrivskyddade fält. (SITES-24780)
* Trädkatalogen meddelar nu datumet Ändrat. NVDA läser det datum då fokus flyttas till kolumnen Ändrad. Rutnätet kopplar varje datum till objektnamnet så att användarna kan höra både filen och den senaste uppdateringen. (SITES-24782)
* Förhandsgranskningsläget följer nu inställningarna för textavstånd. Arbetsytan återspeglar ändringar av bokstaven, ordet och radhöjden i allt förhandsgranskat innehåll. Texten förblir inte längre fast eller klippen när mellanrummet ökar. Tangentbordsanvändare och användare med nedsatt syn kan läsa innehåll utan layoutbrytningar. (SITES-24936)
* AEM korrigerar tabbordningen på Assets Editor-sidorna. Tabbningen går nu från rubrikkontrollerna till kontaktnavknapparna och slutligen in på arbetsytans verktyg i en tydlig sekvens. Skärmläsare följer samma ordning, vilket tar bort förvirring och snabbar upp tangentbordsnavigeringen. (SITES-24937)
* AEM lägger till ett programmatiskt namn i menyraden för kortåtgärder. Skärmläsare meddelar kontrollen korrekt och talanvändare kan ange den som namn. Tangentbordsnavigering och fokus ändras inte. (SITES-24938)
* Kortvymenyerna har bättre textavstånd. Objektet Fler åtgärder växer och trunkerar inte längre etiketter, inklusive Snabbpublicering. Användare som höjer bokstaven, ordet eller radavståndet har full etikett och tangentbordsåtkomst. (SITES-24941)
* Den presentationsroll som dolde tabellen för webbplatsens hemsida har tagits bort från hjälpmedelsträdet. Tabellen läses korrekt igen. NVDA och JAWS identifierar tabellen, känner igen rubriker och meddelar rubrikrelationer under rad- och kolumnnavigering. (SITES-24942)
* Sortering av feedback i listvyn är explicit och konsekvent. Efter en sortering visar rubriken ordningen via `aria-sort`. Ändringen tillkännages, medan osorterade rubriker inte längre gör anspråk på ett läge, vilket hjälper skärmläsaranvändare att spåra vilka kolumner som styr sorteringen. (SITES-24943)
* Sidhuvudet Redigera layout visar inte längre en **Redigera**-knapp som inte fungerar. Kontrollen fungerar nu som en statisk statusetikett och ligger utanför tabbordningen, så att tangentbordsanvändare inte slösar bort en tangenttryckning. Använd **Välj ett annat läge** om du vill ändra läge, med tydlig skärmläsarfeedback. (SITES-24950)
* Emulatorverktygsfältet visar fullständiga enhetsnamn som standard. Etiketten trunkeras inte längre vid inläsning, så användare kan läsa och välja enheter utan att gissa. Texten skalas jämnt över zoomnivåer och smala bredder. (SITES-24952)
* Emulatorverktygsfältet passar för små visningsrutor. Vid 320 pixlar visas enhetslistan och skärmen kontrolleras utan urklipp, så att användare kan välja Galaxy S7 och nyare modeller. Layouten skalas och bryts för att undvika vågrät rullning även vid 400 % zoom. (SITES-24953)
* Skärmläsare meddelar den valda enheten och dess mått i emulatorn. NVDA stoppar läsningen av linjalströmmen. Enhetsknappen använder en bifogad beskrivning för verktygstipstexten, vilket minskar brus och navigering i stödlinjer. (SITES-24955)
* Filterfältet hanterar nu varje markerad tagg som en åtgärdsknapp. Rensa tillgängliga namn och fokushantering förbättrar meddelanden och tangentbordskontroll. (SITES-24980)
* Statusuppdateringar i filtret Platsadministratörer meddelar skärmläsare. När användare byter kort/lista medan objekt läses in talar NVDA nu meddelandet&quot;Vänta&quot; via en aktiv region. Den här vägledningen förhindrar extra klick och förvirring. (SITES-24992)
* Tangentbordsfokus flyttas nu i en logisk ordning när användaren expanderar den vänstra listen. Fokuseringen växlar direkt från den vänstra knappen till det utökade innehållet, vilket eliminerar behovet av att bakåt spåra eller hoppa över element. Den här ändringen förbättrar tillgängligheten för skärmläsare och tangentbordsanvändare. (SITES-24998)
* Skärmläsarfeedback för knappen **Redigera** matchar nu kontrollen. När du aktiverar knappen meddelas redigeringsåtgärden i stället för ett förhandsgranskningsmeddelande, vilket förbättrar klarheten och minskar indatafel för användare som inte använder musen. (SITES-25208)
* Åtgärden för att bekräfta i dialogrutan Teaser meddelar skärmläsare korrekt. Kontrollen rapporterar&quot;Bekräfta&quot;, inte ikonbeskrivningen, vilket ger användare av tangentbord och skärmläsare tydliga riktlinjer. (SITES-25223)
* Hjälpknappen visar nu ett tydligt namn. Skärmläsare skriver &quot;Help&quot; i stället för en detaljerad beskrivning. Användarna förstår åtgärden och kan få hjälp snabbare. (SITES-25224)
* Den spärrade funktionen för Timewarp visar en tydlig fokusring på länkarna **`Set Date`** och **Avsluta Timewarp**. Användare som ser exakt var fokus hamnar och undviker oavsiktliga åtgärder. Ringen bibehåller minst 3:1 kontrast mot bakgrunden. (SITES-25232)
* Skärmläsare meddelar nu kontrollerna Anteckna och Stäng anteckningar korrekt i verktygsfältet Anteckningar. NVDA säger inte längre &quot;Förhandsgranskningsknappen trycktes ned&quot;, som vilseleda författare och föreslog fel åtgärd. Meddelandet matchar knappen som trycktes ned och håller arbetsflödet tydligt. (SITES-25234)
* Tangentbordsnavigeringen i verktygsfältet för anteckningar fungerar på ett enhetligt sätt. Fokus hoppar inte längre till Avsluta när du öppnar läget utan flyttas till startkontrollen för att lägga till anteckningar. Användarna navigerar i kontrollerna sekventiellt utan omvänd tabbning. (SITES-25241)
* Liten skärmvisning fungerar som väntat i Teaser modal. Dialogrutan skapar inte längre en vågrät rullningslist med 320 px, och verktygsfältet förblir tillgängligt utan att panorera åt sidan. Uppdateringen hjälper synskadade användare som zoomar sidan. (SITES-25242)
* Liten skärmvisning fungerar som väntat i det modala bildläget. Dialogrutan skapar inte längre en vågrät rullningslist med 320 px, och bildverktygen är fortfarande tillgängliga utan panorering åt sidan. Den här uppdateringen förbättrar navigeringen för användare med nedsatt syn som zoomar sidan. (SITES-25244)
* Sökning spärrar inställningarna för användartextavstånd. Om du ökar radhöjden, styckeavståndet, bokstavsmellanrummet eller ordmellanrummet klipps inte längre texten bort eller överlappar trädet. Innehållet flödar om vid WCAG 1.4.12-värden och förblir fullt läsbart. (SITES-25245)
* Sökning modal passar nu in på små skärmar utan att överlappa trädkatalogen vid 320 px. Innehållet flödar om inuti dialogrutan, behåller endast lodrät rullning och gör kontrollerna synliga. Den här korrigeringen förbättrar läsbarheten och tangentbordsnavigeringen och anpassar sig till WCAG-flödesomformningen. (SITES-25246)
* Carousel modal overflow medför inte längre vågrät rullning vid telefonbredder. Komponenten anpassas till 320 px, bevarar det lodräta flödet och ger kontroll synlig. Ändringen förbättrar läsbarheten och tangentbordsåtkomsten vid redigering. (SITES-25254)
* Anteckningsarbetsflöden förlorar inte längre fokus. Den modala placerar det inledande fokus på en meningsfull rubrik, förhindrar att fokus hoppar utanför dialogrutan och återställer fokus till utlösaren efter stängningen. Skärmläsarutdata förblir koncisa och relevanta. (SITES-25257)
* Dialogrutan **Ta bort anteckning** hanterar nu tangentbordsfokus korrekt. Om du öppnar dialogrutan flyttas fokus till rubriken för skärmläsarkontext och om du stänger den flyttas fokus tillbaka till knappen **Ta bort anteckning** som startade den. Användare landar inte längre på icke-relaterade kontroller eller bakom modala kontroller. (SITES-25258)
* Tidsförvrängningsdatumväljaren hanterar nu fokus korrekt. Om du trycker på `Esc` återgår fokus till knappen **Datumväljaren** och om du väljer ett datum flyttas fokus till det länkade inmatningsfältet. Tangentbords- och skärmläsaranvändare behåller sitt sammanhang och hamnar inte bakom det modala. (SITES-25264)
* Skärmläsare meddelar de rätta åtgärderna för knapparna **Anteckning** och **Stäng anteckning**. NVDA säger inte längre &quot;Förhandsgranskningsknappen trycks ned&quot;. Det meddelar knappnamnet så att användarna vet när anteckningsläget startar eller avslutas. (SITES-25268)
* Anteckningens modala visar nu en tydlig **Skicka**-åtgärd. Författare kan lägga till en kommentar och skicka den med pennikonknappen eller stänga spärren med `Esc`, utan att gissa flödet. (SITES-25269)
* Anteckningsposten innehåller explicita åtgärdsknappar. I dialogrutan visas **Skicka** för att spara anteckningen och **Avbryt** för att stänga den. Både tangentbordet är tillgängligt och hjälpmedlet har meddelat dig. Författare behöver inte längre förlita sig på att du klickar utanför dialogrutan eller bara trycker på `Esc` för att slutföra. (SITES-25281)
* Anteckningsläget behåller nu tangentbordsfokus på övertäckningen och dess verktygsfält. Sidan bakom övertäckningen får inte längre fokus när författare trycker på Tabb, så användarna behåller sin orientering och kan navigera i anteckningar utan att hoppa till underliggande innehåll. (SITES-25282)
* Enhetsväljaren i Redigera layout fungerar som den ska. När två enhetsalternativ har liknande bredd (t.ex. iPhone 8 Plus bredvid Galaxy 7) visar den markerade knappen ett verktygstips som visar hela etiketten medan båda knapparna är synliga och tillgängliga. (SITES-25285)
* Vid 200 % zoomning kommer Redigera layout inte längre att åsidosätta sidan. Verktygsfältet återger helt och visar vågrät rullning vid behov, vilket återställer åtkomst till tidigare dolda kontroller för användare med nedsatt syn. (SITES-25288)
* Tabbordningen i förhandsvisningen av layout går nu direkt från det primära verktygsfältet till det demografiska verktygsfältet. Användare av tangentbord och skärmläsare kan gå igenom kontrollerna i en förutsägbar sekvens i stället för att hoppa till det sekundära verktygsfältet. Ändringen överensstämmer med WCAG 2.4.3 Fokusordning. (SITES-25305)
* När du zoomar sidan till 200 % döljs inte längre en del av det demografiska verktygsfältet. Verktygsfältsavsnittet hanterar spill och ger rullning i sitt eget område, vilket gör att alla kontroller är synliga och kan användas med hög förstoring. (SITES-25309)
* Textinmatningar i verktygsfältet Demografi visar nu tillgängliga namn. Varje fält innehåller ett unikt ID med en programmatisk etikett, så skärmläsare meddelar syftet med fältet och användarna kan navigera efter etikett. Den synliga etiketten sitter nära kontrollen för att förbättra läsbarheten vid låga visioner. (SITES-25316)
* Knappen Redigera meddelar nu skärmläsare i det sekundära verktygsfältet rätt åtgärd. När du aktiverar den läses&quot;Redigera&quot; i stället för den orelaterade&quot;Förhandsgranska&quot;-knappen som trycks ned, vilket tar bort förvirring vid tangentbordsnavigering. (SITES-25320)
* Nu visas ett lämpligt namn i diagramreglaget för demografi. Skärmläsare meddelar&quot;Summa av kundvagn&quot; och inmatningsverktyg kan rikta kontrollen efter namn, vilket förbättrar kompatibiliteten med WCAG 4.1.2 (Namn, Roll, Värde). (SITES-25322)
* Verktygsfältets skjutreglage för demografiska data behåller nu fokus när författare ändrar värdet med piltangenterna. Fokus hoppar inte längre till knappen Cart, så kortkommandoanvändare justerar värdet kontinuerligt och skärmläsare meddelar varje ändring. (SITES-25324)
* Sök efter Assets Reflow jämnt i 320 pixlar (cirka 400 % zoom). Den spärrade funktionen gör att rubriker, fält och åtgärder kan läsas och inte överlappas, så att författare kan söka utan vågrät rullning. (SITES-25330)
* Assets-panelen i redigeraren följer en sekvens med logiskt fokus. Tangentbordsanvändare har flikar över varje miniatyrbild och kan komma åt panelens avslutningskontroller. Ändringen tar bort hopp och förbättrar efterlevnaden av WCAG 2.4.3. (SITES-25360)
* AEM uppdaterar knapparna **Listor** och **Stycken** i Teaser modal textredigerare för att visa deras utökade och komprimerade läge. Knapparna växlar nu `aria-expanded` och meddelar skärmläsarna om statusändringen. Författare får tydlig feedback och slipper gissa innan de öppnar eller stänger formatmenyerna. (SITES-25365)
* AEM presenterar inläsningsstatus i Teaser modal. modal visar nu ett live-statusmeddelande medan innehållet läses in, så NVDA och JAWS talar&quot;Loading, please wait.&quot; Författare bör få tydlig feedback och undvika att interagera med dialogrutan innan den är klar. (SITES-25366)
* Förbättrar statusmeddelanden på fliken Resurser i dialogrutan Länkval. När ett fel inträffar injicerar komponenten en läsbar statusuppdatering och håller tangentbordsfokus stabilt, vilket gör att NVDA/JAWS informerar användarna direkt. (SITES-25368)
* Ett korrigerat gränssnittsbeteende på anteckningspanelen för mycket smala visningsrutor. Vid 320 px formas rubriken och Lägg till-kontrollen tidigare. Verktygsfältet flödar nu om och behåller tydlig separation mellan elementen. Författare kan använda kontrollerna utan att förlora information eller funktion. (SITES-25376)
* Korrigerade ett kvarvarande feltillstånd på fliken **Länkar och åtgärder** i dialogrutan **Teaser** . När författarna har aktiverat **Call to action** och korrigerat tomma eller ogiltiga fält rensas felformateringen och ikonen på fliken och `aria-invalid` tas bort. Skärmläsare meddelar inte längre något fel när fälten har validerats. (SITES-25527)
* Felhanteringen i webbplatsadministratörsformulär uppfyller nu förväntningarna på tillgänglighet. När valideringen misslyckas visas felet omedelbart på sidan, fokus flyttas till ett användbart meddelandemål och texten visas för skärmläsare som JAWS. (SITES-27138)
* När du skapar en mapp i Sites visas nu en tydlig bekräftelsetagg. JAWS presenterar budskapet i hela regionen, så författarna får direkt och åtkomlig feedback efter åtgärden. (SITES-27141)
* Korrigerade ett hjälpmedelsgap där bilder i redigeringsdialogrutor återges utan Alt-text. Dialogrutan innehåller nu beskrivande alternativ text vid behov och tomt alt för enbart visuella element, vilket återställer kompatibelt beteende för JAWS och andra skärmläsare. (SITES-27153)
* Förbättrad felhantering i redigeringsdialogrutor. När ett konfigurationsfel inträffar visar gränssnittet explicit text och utlöser ett skärmläsarmeddelande via ett varningsområde. Författarna får direkt feedback och kan åtgärda problemet utan att tappa sitt sammanhang. (SITES-27155)
* Korrigerade ett fel i flödesomformningstillgänglighet i Platsadministratör. Vid zoomning med 400 % webbläsare kontrollerar verktygsfältet och rutnätet överlappande och push-knappar utanför skärmen, vilket blockerar tangentbordsnavigering och skärmläsaranvändning. Layouten flödar nu korrekt så att sök-, filter- och åtgärdsknapparna förblir synliga och kan användas med 400 % zoomning. (SITES-27238)
* Låg kontrast i låsstatusmeddelandet som visas i arbetsflödet Lås/Lås upp sida har korrigerats. Meddelandet uppfyller nu 4,5 :1-kvoten, vilket förbättrar läsbarheten och ADA-kompatibiliteten för författare. (SITES-27270)
* Tillgängliga namn har lagts till i bockmarkeringsikonerna i dialogrutan **Effektiva behörigheter**. JAWS presenterar nu ikonerna och deras innebörd, vilket förbättrar tangentbordsnavigering och ADA-kompatibilitet. (SITES-27272)
* Navigering med dolda rubriker accepterade fokus och förvirrade användare med både synkning och skärmläsare. Uppdateringen inaktiverar fokus på komprimerade kontroller och visar endast synliga objekt. Navigeringen är förutsägbar och uppfyller WCAG 2.4.3. (SITES-35224)

* Mappens miniatyrbildikoner i Sites Admin har åtgärdats så att de fungerar som dekorativa bilder. Uppdateringen tar bort bildrollen och använder tom alternativ text, så hjälpmedelstekniken ignorerar ikonerna och läser bara meningsfulla etiketter. (SITES-2852)
* Adobe ökade färgkontrasten för referenstexten på webbplatsens hemsida. Texten uppfyller nu WCAG 2.1 AA med en kvot på minst 4,5:1 och kan läsas tydligt på ljusa teman och ljusa skärmar. (SITES-24755)
* Med referensmarkeringen för järnväg visas nu namnet för skärmläsare. Regionen visar en unik `aria-label` (&quot;Reference rail&quot;), som förbättrar navigeringen för landmärken och särskiljer den från andra regioner. (SITES-24973)
* Beskrivningshastigheten blockerade navigering på fliken framåt och bröt dialogflödet. Korrigeringen återställer standardtangentbordsrörelsen. Författare fortsätter förbi fältet med en enda tabb och behåller markeringsordningen förutsägbar. (SITES-35228)
* Redigeringskontrollerna saknade hjälpmedelsnamn och exponerad Raw-ikontext, vilket förvirrade JAWS. Korrigeringen lägger till explicita ARIA-etiketter och standardroller. Meddelandena låter korrekta och överensstämmer med förväntningarna på tillgänglighet. (SITES-35227)
* Listrutan Kategorier saknade en specifik etikett, så JAWS talade om en allmän&quot;bildknappsmeny&quot;. Uppdateringen namnger kontrollen &quot;Kategorier&quot; och definierar dess roll. Skärmläsaranvändare hör en korrekt etikett och förstår vilka alternativ som är tillgängliga. (SITES-35226)
* I dialogrutan Egenskaper visas ett datarutnät som skärmläsare behandlas som oformaterad text. JAWS och NVDA missade fokus och kunde inte meddela rader och kolumner. Korrigeringen lägger till riktiga tabellsemantik och ARIA-roller. Skärmläsare känner nu igen tabellen och spårar fokus korrekt. (SITES-35225)
* Textredigeraren för innehållsfragment som läses in med ett trunkerat åtgärdsfält. Ikonerna klipptes av och det gick inte att komma åt spillmenyn. Uppdateringen åtgärdar layouten så att hela verktygsfältet förblir synligt och tillgängligt. (SITES-33005)
* Formulärfält på fliken Grundläggande kunde inte visa användbar feltext. Formuläret visar nu tydliga, textbundna meddelanden och länkar dem till fältet för skärmläsare. Användare av tangentbord och hjälpmedel får omedelbar vägledning för att åtgärda inmatningar. (SITES-32480)
* Det multifält som används i en anpassad komponent som visas med ikonknappar utan etikett och med inkonsekvent tabbordning. JAWS/NVDA meddelade endast att det fanns&quot;knappar&quot; eller överhoppade kontroller som blockerade tangentbordsåtgärder. Uppdateringen innehåller beskrivande namn för Lägg till, Ta bort och Flytta, normaliserar tabbstopp och meddelar listuppdateringar för att uppfylla ADA:s förväntningar. (SITES-30660)
* Snabbpublicering returnerar nu ett tydligt meddelande om att åtgärden lyckades. Dialogrutan stängs, en popup-bild bekräftar åtgärden och skärmläsarna meddelar meddelandet så att författarna inte missar resultatet. (SITES-26912)
* Ingen ändring krävs. Adobe granskade påståendet att sökikonen överlappar närliggande text. Rubriken innehöll en etikett som kunden lagt till. Vanilla AEM återger bara ikonen. En ren instans visar den korrekta layouten vid 100 % zoom, så felet stängdes som utanför omfånget. (SITES-26910)
* Skapa sidteman döljer inte längre fokusläget. Akvatiska format och designformat återger en konsekvent markering på fliken **Grundläggande** och intilliggande flikar under tangentbordsnavigering. Den här ändringen återställer förutsägbar och förutsägbar fokusåterkoppling för användare med nedsatt syn. (SITES-26907)



#### Administratörsgränssnitt{#sites-adminui-6524}

Skärmläsaranvändare fick ingen navigeringshjälp i rutnätet **Catalog System Blueprint** . JAWS meddelade bara cellpositionen och blev sedan tyst. I den här versionen läggs hjälpmedelsförberedda riktlinjer och roller till, vilket gör att JAWS kan läsa listkontexten, det markerade objektet och de obligatoriska pil-/mellanrumskontrollerna. (SITES-30661)

#### Klassiskt användargränssnitt{#sites-classicui-6524}

Klassiskt användargränssnitt förlorade etiketter och visade tomma alternativ. Dialogrutor visas även med kodade HTML-filer, t.ex. `<br>`. Uppdateringen återställer kryssruteetiketter och avkodningskoder, så att dialogrutorna läses korrekt. (SITES-31822)

<!--
#### [!DNL Content Fragments]{#sites-contentfragments-6524}
-->

#### [!DNL Content Fragments] - Admin{#sites-admin-6524}

Parenteser i ett innehållets fragmentnamn orsakade att referenspanelen felaktigt rapporterade användningen. Författare såg 0 även när andra fragment refererade till det. Med korrigeringen korrigeras sökvägsparsningen för&quot;(&quot; och&quot;)&quot; och rätt antal och poster som inte är noll visas. (SITES-35078)


#### [!DNL Content Fragments] - Fragmentredigeraren{#sites-fragments-editor-6524}

* Avpubliceringen misslyckades för innehållsfragment vars DAM-sökväg innehöll parenteser. Guiden Hantera publikation skrev om &quot;(&quot; och &quot;)&quot; och bröt resurssökvägen. Korrigeringen bevarar tecknen och åtgärdar rätt objekt, så avpubliceringsåtgärden slutförs. (SITES-35077)
* När du redigerar ett innehållsfragment och går tillbaka till Assets-listan doldes fragmentet eller hela mappen. Det gick inte att uppdatera listan efter att redigeraren stängts. Korrigeringen uppdaterar nu listan på ett tillförlitligt sätt och gör det redigerade fragmentet synligt utan att behöva läsas in på nytt. (SITES-35374)

* Det gick inte att öppna väljaren för polarisresurser eftersom nödvändiga IMS-omfattningar har tagits bort. Med korrigeringen återställs minimala scope och leveransanslutningen återupprättas. Bläddra efter resurser och markera objekt igen, utan HTTP 500-fel. (SITES-35837)

#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6524}

Efter varje distribution har giltiga GraphQL-frågor börjat returnera `GraphQL_QueryValidationError`. Slutpunkten behöll ett inaktuellt schema tills teamen tömde caches eller startade om. Korrigeringen uppdaterar GraphQL-schemat och registret för beständiga frågor under distributionen och återställer normala svar omedelbart. (SITES-34301)

<!--
#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6524}


#### [!DNL Content Fragments] - REST API{#sites-restapi-6524}


#### Component Console{#sites-component-console-6524}


#### Core Backend{#sites-core-backend-6524}


#### Core Components{#sites-core-components-6524}


#### Campaign integration{#sites-campaign-integration-6524}
-->


#### ContentHub {#sites-contenthub-6524}

ContextHub injicerar inte längre en andra jQuery-kopia på publiceringssidor. Klientbiblioteket för segmentmotorn tar bort cq.shared-beroendet som tog jQuery 1.12.4, så att webbplatser läser in en konsekvent jQuery- och front-end-kod fungerar tillförlitligt. (SITES-30404)

#### Upplevelsefragment{#sites-experiencefragments-6524}

* Experience Fragments lokaliserar nu varningen som visas när det inte finns någon Adobe Target-konfiguration. Meddelandet visas på författarens språkområde i stället för på engelska, så export- och aktiveringsstegen läses korrekt för globala team. (SITES-11868)
* När du publicerar en Experience Fragment-variant visas nu ett lokaliserat felmeddelande när ingen molntjänst är kopplad till variationen. Meddelandet visas i användargränssnittet på användarens språk i stället för i en sträng som bara är för engelska. (SITES-20293)
* Exporteringen av en Experience Fragment till Target kraschade med `Attempt to modify attribute at illegal index: -1`. Instrumentationen för webbinspiraler är i konflikt med exporteraren och attributhanteringen är skadad. Korrigeringen gör att attributbearbetning blir svårare och den konflikten tas bort. Exporten lyckades och fragmentet återges i Target. (SITES-31891)

* Experience Fragment-egenskaper översätter nu fliken **Referenser**. Etiketter och kolumnrubriker som &quot;Sida&quot;, &quot;Sidsökväg&quot; och &quot;Varianttitel&quot; visas på författarens språk. Den här ändringen tar bort strängar som bara är för engelska och gör egenskapsvyn konsekvent för globala team. (SITES-11203)
* **Variationer** > **Skapa arbetsflöde** visar nu fullständig översättningstext. I dialogrutan hanteras långa språksträngar genom att innehållet radbryts och storleksändras på rätt sätt, vilket eliminerar urklipps- eller brytningsetiketter. (SITES-19304)
* Experience Fragment-egenskaper översätter nu statusetiketterna för sociala medier. Författare ser statusvärden som Bokfört och Inte bokfört på det valda språket för alla språk. Den här ändringen tar bort strängar som bara är för engelska och som orsakade förvirring under granskningen. (SITES-2014)

<!--
#### Foundation Components (Legacy){#sites-foundation-components-legacy-6524}
-->

#### Launches{#sites-launches-6524}

* Om du tar bort en mycket stor Launch låstes databasen. Jobbet köade för många borttagningar och utlöste andra begäranden. Korrigeringen tar nu bort batchar och ger upphov till genvägar mellan segment, så rensningen slutförs medan systemet förblir responsivt. (SITES-32004)

* Öppna Konfiguration > Egenskaper visar listrutorna Företag och Egenskap. **Spara** och **Stäng** bevarar slutförda fält, och verifieringen av titeln utlöser inte längre fel på företag eller egenskap. (CQ-4359853)
* Nödvändiga kontroller i IMS-konfigurationen körs vid uppdatering, inte bara när den skapas. Tomma värden i fält som klient-ID eller Klienthemlighet visar ett fel och stoppar sparandet tills ett giltigt värde anges, vilket förhindrar återanvändning av det tidigare värdet. (CQ-4359938)
* När du startar projektet visas översatta validerings- och felsträngar. Meddelanden som bara innehåller engelska för fel vid skapande och saknade källsidor visas inte längre. Författarna ser tydlig och språklig feedback under installationen av Launch. (SITES-13085)
* Starta kampanj uppdaterar sidegenskaperna `jcr:title`, `jcr:description` och `cq:redirectTarget` på källsidan. Ändringen tar bort egenskapsundantag i MSM-utrullningskonfigurationen och arbetsflödeslogiken. Kampanjer, översättningar och SEO håller enhetliga titlar, beskrivningar och omdirigeringar. (SITES-34509)
* Launch-åtgärden ignorerade omfånget och inkluderade sidor som delade samma överordnade som målavsnittet. Uppdateringen tvingar underträdets gränser och befordrar bara den valda sidan och dess underordnade sidor. Ej relaterade sidor behåller sitt befintliga innehåll. (SITES-34344)
* En automatisk befordran för kapslad start som stoppades vid författaren och hoppade över publiceringsnivån har åtgärdats. Den automatiska kampanjen för en underordnad start publicerar de uppdaterade sidorna till de konfigurerade utgivarna och slutför den fullständiga starten enligt schemat. (SITES-30420)

<!--
#### Link Checker{#sites-link-checker-6524}
-->

#### MSM - Live-kopior{#sites-msm-live-copies-6524}

* En utrullning på mappnivå kunde inte skapa live-kopior för Experience Fragments under den mappen. Enskilda rollouts fungerade, vilket bröt arbetsflödena. Ändringen justerar mapplanseringen med sidbeteendet och sprider relationer och referenser i underträdet. (SITES-35161)
* När du har tagit bort en komponent i en Live-kopia gick **Aktivera arv** sönder med ett JavaScript-fel och komponenten saknades tills ett andra försök gjordes. Uppdateringen åtgärdar den efterborttagna inläsningen så att den innehåller rätt parametrar och ersätter det föråldrade varningsanropet. Dialogrutan öppnas korrekt och arv återställs vid det första försöket. (SITES-31387)
* Utrullningsguiden accepterade **senare** utan datum. Författare utvecklade och skapade en utrullning utan schema. Uppdateringen framtvingar datumval och visar en tydlig uppmaning. Åtgärden **Fortsätt** är inaktiverad tills ett datum finns. (SITES-31374)


#### Page Editor{#sites-pageeditor-6524}

* När innehållsträdet öppnades på en sida med en Personalization-behållare returnerades en tom panel och ett null-referensfel för konsolen. Författare kunde inte välja eller konfigurera komponenter. Uppdateringen tar bort felet och aktiverar samspelet mellan träd och komponenter på nytt. (SITES-34336)
* AEM 6.5 SP23, växling till paus i sidredigeraren. Om du klickar på **Layout**, **Utvecklare** eller **Mål** låstes redigeraren i läget **Redigera** och en konsol `TypeError` utlöstes. Uppdateringen återställer ändringar i verktygsfältsläget och rensar felet. (SITES-34536)
* Sidredigeraren hoppade bort från insättningspunkten när författare lade till komponenter i långa behållare. Uppdateringen justerar övertäckningstidpunkten och rullningshanteringen. Vyn behåller sin plats och den nya komponenten är synlig och klar att konfigureras. (SITES-32621)
* Anpassade taggetiketter misslyckades i sidredigeraren och användargränssnittet visade alltid&quot;taggar&quot;. Predikatet utvärderar nu `fieldLabel` först och `labelText` sekund, och sedan används standardvärdet. Författare ser etiketten som de anger. (SITES-32278)
* Om du avbryter platsfiltret i Platser har OmniSearch-ikonen felaktigt justerats och överlappat den med platshållartexten. Ikonen blev oklickbar. Korrigeringen justerar ikonen och återställer träffområdet så att både musen och tangentbordet aktiverar sökningen. (SITES-30946)
* När du valde Utvecklare befann du sidan i ett felaktigt läge och blockerade redigering på den sidan. Panelen stängdes och gränssnittet slutade svara. Uppdateringen reparerar logiken för växling mellan lägen och hantering av cache, vilket gör sidan redigerbar och visar utvecklardata direkt. (SITES-30922)
* Sökfrågan togs inte bort när du klickade på **Rensa** i **Infoga ny komponent** och listan lämnades filtrerad till ett enskilt objekt (dragspel). Korrigeringen återställer frågan och uppdaterar listan. Alla tillåtna komponenter visas igen. (SITES-30921)

<!--
#### Replication{#sites-replication-6524}
-->

#### RTF-redigerare{#sites-rte-6524}

* I helskärmsläge dolde textredigeraren resultatet av stavningskontrollen bakom dialogrutan när det inte fanns några fel. Uppdateringen placerar resultatpanelen längst fram och håller meddelanden och förslag synliga. Författare granskar och godkänner korrigeringar utan att behöva lämna helskärmsläget. (SITES-32366)
* RTF-redigeringsbilder följer nu den valda justeringen. Författare anger vänster, mitten eller höger i bilddialogrutan så använder redigeraren det alternativet konsekvent i utdata. Ändringen stabiliserar även dialogrutan Alt-text så att Alt-text och justering sparas och behålls vid redigering. (SITES-30634)

#### Universell redigerare {#sites-universal-editor-6524}

När autentiseringshanteraren för frågetoken konfigurerades blandades användarna eftersom etiketterna inte matchade fälten. Gränssnittet tog bort text från sökvägen och visade fel namn. Korrigeringen återställer tydliga och korrekta etiketter för tjänstrankning och frågetokenalternativ. (SITES-31305)


### [!DNL Assets]{#assets-6524}


#### [!DNL Dynamic Media]{#assets-dm-6524}

* Alternativet **Välj miniatyrbild** för videofilmer fungerar nu korrekt i AEM Assets - Dynamic Media. När du klickar öppnas dialogrutan där du kan välja en miniatyrbild från Assets, vilket eliminerar beteendet att klickningen inte fungerade tidigare och endast tar bort begränsningen till extrahering av videobildrutor. (ASSETS-58926)


### [!DNL Forms]{#forms-6524}

>[!NOTE]
>
>Korrigeringar i [!DNL Experience Manager] Forms levereras via ett separat tilläggspaket en vecka efter den schemalagda versionen av [!DNL Experience Manager] Service Pack. I detta fall kommer tilläggspaketen att släppas torsdagen den 4 december 2025. Dessutom har en lista med korrigeringar och förbättringar för Forms lagts till i det här avsnittet.

<!--
#### Forms Designer 

#### Forms

#### Forms JEE 

#### Forms Captcha {#forms-captcha-6524} 

#### XMLFM {#forms-xmlfm-6524}

#### [!DNL Forms Designer] {#forms-designer-6524}

-->


### Foundation {#foundation-6524}


#### Apache Felix {#foundation-apachefelix-6524}

Felix Web Console-paketet med FELIX-6747 har uppdaterats. Den här korrigeringen åtgärdar svarshantering som tidigare har brutit sidåtergivning och autentisering i OSGi Web Console. Konsolen läses in konsekvent och genererar inte längre IllegalStateException-poster i loggarna. (NPR-42730)

<!--
#### Campaign{#foundation-campaign-6524}

#### Cloud Services{#foundation-cloudservices-6524}

#### Communities {#foundation-communities-6524}

#### Content distribution{#foundation-content-distribution-6524}

#### CRX {#foundation-crx-6524}
-->

#### Granit{#foundation-granite-6524}

* Raw- eller engelskskrivna strängar visas inte längre i dialogrutan **Ta bort åtkomstkontroll** . I dialogrutan visas helt lokaliserat innehåll för olika språk som stöds, vilket ger en konsekvent tillgänglighet. (GRANITE-48479)
* Hjälpikonen visar nu en kortfattad etikett för hjälpmedelstekniker. JAWS läser&quot;hjälpknapp&quot; och lägger inte längre till överflödiga&quot;menyord&quot;. Den här uppdateringen gör att kontrollen överensstämmer med WCAG 4.1.2 och förenklar användningen av tangentbord och skärmläsare. GRANITE-55360
* Återställ HTL-skriptmotorfabriken efter att ha eliminerat en beroendeloop i OSGi-tjänster. Miljöerna börjar som de ska, HTML-återgivning fungerar över alla redigeringspunkter och administratörer stöter inte längre på startfel eller saknade skripttjänster. (GRANITE-58276)

* Rutan Sök i sidhuvudet täcker inte längre förstoringsglaset på platshållartexten. Platshållaren visas med rätt utfyllnad och är fortfarande fullt läsbar i olika webbläsare. (GRANITE-54391)
* Författare ser läsbara etiketter i fält för automatisk komplettering i stället för råvärden i dialogrutan. Implementeringen bevarar värdet i JCR och förbättrar klarheten för en- och flervalskonfigurationer som källalternativ dynamiskt. (GRANITE-57615)
* Redigeringsläget fungerar inte när htmlLibraryManager.debug är inställt på true. Ändringen återställer korrekt klientlibbupplösning och inläsning, vilket gör att utvecklare kan använda felsökningsverktygen i HTML Library Manager vid redigeringen. GRANITE-58002
* Redigeringssidan för replikeringsagenten genererar inte längre ett JavaScript-fel i det klassiska användargränssnittet. Sidan öppnas, visar alla flikar och sparar agentinställningar utan konsolfel. GRANITE-58302
* Hälsostatusaggregering har korrigerats i Systemöversikt. Vyn uppdateras nu när enskilda kontroller har körts och rätt antal visas. Operatörerna ser&quot;OK&quot; när säkerhets- och underhållskontroller godkänns, i stället för en felaktig banderoll med&quot;2 fel&quot;. GRANITE-61482
* `CodeUpgradeTasks` har stoppats från att köras under uppgraderingar av AEM 6.5 LTS (Long Term Support). Uppgraderingen fortsätter nu utan uppgiftsutlösta databasändringar eller omkonfigurationer. Med den här programfixen minskas uppgraderingsriskerna och driftstopp undviks. GRANITE-61486
* I redigeringsdialogrutor visas nu ett enda exakt valideringsfel i obligatoriska fält. Meddelandet använder fältets egen etikett när det finns, och återgår till en allmän fråga när det inte finns någon etikett. Dubblerade och felmatchade meddelanden i olika fält visas inte längre. (GRANITE-59531)
* Dialogrutan för att skapa sidor verifierar nu obligatoriska fält på nytt vid varje interaktion, inklusive tabbändringar och redigering av flera fält. Knappen **Skapa** är inaktiverad tills författarna har slutfört alla nödvändiga indata och guiden visar infogade fel för saknade värden. GRANITE-58826

#### Integreringar{#foundation-integrations-6524}

Publicering av AEM Target-aktiviteter misslyckas inte längre när författare anger start- och slutdatum. Integreringen skickar standardkompatibla tidsstämplar som innehåller tidszonen, så Target bearbetar aktivitetens nyttolast och slutför synkroniseringen som förväntat. (CQ-4360733)

<!--
#### Jetty{#foundation-jetty-6524}
-->

#### Lokalisering{#foundation-localization-6524}

* Lokalisering i zh-CN tar bort en tvetydig fras i referensinsamlingsstatusen som visas vid tillgångsåtgärder som Flytta. Gränssnittet visar nu `正在获取对 [[0]] 项的引用`, vilket ger korrekt innebörd och konsekvent terminologi. (CQ-4354648)
* När du skapar en smart samling översätts inte längre sparade söknyckelord vid uppdatering. Författare som anger engelska termer ser att samma termer behålls och att samlingen fortsätter att returnera konsekventa resultat. (NPR-43158)
* Korrigerad trunkerad knappbeskrivningstext på panelen Bild. Beskrivningen &quot;Visa bildtext som popup-fönster&quot; återges fullständigt på alla språk som stöds, vilket förbättrar vägledningen för författare som inte är engelska. (SITES-10490)
* Spaltvyn Webbplatsadministration trunkerade lokaliserade etiketter på franska och spanska. &quot;Sluttid&quot; och &quot;Inte tid&quot; verkade trunkerade och visade inget verktygstips. Adobe korrigerade översättningarna och återställde verktygstipset vid hovring, så etiketterna lästes in fullständigt. (SITES-31318)
* Dialogrutan **Flytta** på platser visade i18n-nycklar i Raw-format i stället för läsbara etiketter. Objekt som &quot;Refererande sidor&quot;, &quot;Skapad den&quot;, &quot;Skapad av&quot; och &quot;Sökväg&quot; förvanskades. Korrigeringen kopplar dialogrutan till rätt ordlistor och förser översättningarna med en engelsk reservtext. (SITES-30881)

<!--
#### Oak {#foundation-oak-6524}
-->

#### Plattform{#foundation-platform-6524}

* Valideringsfel visar nu tydlig och beskrivande text i stället för bara en ikon. Skärmläsarna meddelar meddelandet automatiskt när det visas, så att användarna inte behöver navigera till en ikon för att ta reda på vad som gick fel. (CQ-4359152)


* Hovringsetiketter i navigeringsfältet finns inte längre kvar på skärmen när markören flyttas bort från kontrollen. Gränssnittet döljer dessa verktygstips omedelbart när du gör oskärpa eller klickar med musen, vilket förhindrar att det blir rörigt och att användaren klickar fel. (CQ-4360030)
* I Platser slutar verktygsfältåtgärder att skapa ett andra popup-fönster när användaren upprepar klickningar. Den andra klickningen stänger det befintliga popup-fönstret och lämnar bara en instans synlig, vilket eliminerar överlappning och störning. (CQ-4360038)
* Den gamla copyrighttexten för 2024 visas inte längre. Inloggningssidan och **Hjälp** > **Om AEM** 2025-popup-programmet, och AEM läser året programmatiskt för att undvika manuella redigeringar. (CQ-4360042)
* När du klickar på ett verktygstips i AEM rubrikfält aktiveras inte längre den underliggande åtgärden. Popup-fönster öppnas bara när användaren klickar på den faktiska knappen, vilket förhindrar att dialogrutor av misstag visas när användaren interagerar med verktygstipstexten. (CQ-4360105)
* Årets överrullning lämnar inte längre föråldrad copyrighttext. Inloggningsskärmen och dialogrutan **Hjälp** > **Om AEM** hämtar året från systemklockan och återger det aktuella värdet varje gång användargränssnittet läses in. (CQ-4360173)
* Popup-fönster för rubrikfält visas nu korrekt. Om du klickar på samma åtgärd (till exempel **Sök** eller **Filter**) stängs popup-fönstret som är öppet i stället för att något annat överlägg öppnas. Ändringen förhindrar staplade popup-fönster och återställer fokus till rubrikkontrollen. (NPR-42891)
* Projekt och kalendervyn i Inkorgen återges korrekt. När du växlar vy blir sidan inte längre tom. Kalendern läses in och visar schemalagda objekt. (NPR-42968)

<!--
#### Security{#foundation-security-6524}
-->


#### Sling{#foundation-sling-6524}

* Cachelagring på SAML-skyddade sidor har korrigerats. AEM lägger till rätt cachekontroll och varierar metadata för autentiserade sessioner, så proxies och Dispatcher hoppar över cachelagring av personaliserade svar. Anonymt innehåll cachelagras fortfarande normalt medan inloggade vyer är användarspecifika. (NPR-42640)

* Plattformen uppgraderar kärnmotorn från 2.16.2 till 2.16.6. Den nyare motorn härdar indatavalideringen och stabiliserar bearbetningen av begäranden under belastning. (NPR-43105)

#### SPA-redigerare {#foundation-spa-editor-6524}

Aktiverar Sling Main Servlet **Check Content-Type** åsidosätter brutna `.model.json` exporter i AEM 6.5 SP21/22. Begäranden returnerade HTML eller fel eftersom exporteraren bytte typ efter mittkedjan. Korrigeringen genererar JSON med rätt typ från början, så `.model.json` fungerar i redigerings- och publiceringsmiljöer. (SITES-32634)


#### Översättning{#foundation-translation-6524}

* En omindexeringsåtgärd för översättningsprojektstatus har lagts till. Administratörer kan återskapa säkerhetskopieringsindexet när statusvyn inte är synkroniserad, återställa resultat och eliminera Oak traversal-varningar. Sidan läses in snabbare och visar aktuella jobbtillstånd. (NPR-42699)
* Korrigerade en regression där XLIFF-import rapporterade att det lyckades men lämnade JSON-ordlistefilerna oförändrade. Importerna har nu rätt i18n-sökväg som mål och beständiga översättningar så att lokaliseringsrundorna är slutförda utan manuella redigeringar. (NPR-42989)


* XML för översättningsregler fungerar nu som konfigurerats. Översättningsramverket följer undantagsreglerna och gäller för `include`- och `exclude`-mönster korrekt när jobb skapas. Översättningsbegäranden skickar inte längre utelämnat innehåll. (NPR-42761)



#### Användargränssnitt{#foundation-ui-6524}

* Korrigerade en gränssnittsregression som inaktiverade indata i dialogrutan Adobe Stock License. Dialogrutan fungerar nu som den ska, accepterar text i obligatoriska fält och slutför licensieringsflödet för Stock-mediefiler från vyn Resursinformation. (NPR-42748)

* Korrigerad gruppsynlighet i författarmiljön. Grupper-konsolen slutar inte längre med cirka 41 resultat och returnerar alla medlemskap för varje användare. Med den här korrigeringen återställs konsekvent beteende efter kumulativa korrigeringar och den aktuella säkerhetshärdningen behålls. (NPR-42749)


<!--
#### WCM{#foundation-wcm-6524}



#### Workflow{#foundation-workflow-6524}
-->




## Installera [!DNL Experience Manager] 6.5.24.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.24.0 kräver [!DNL Experience Manager] 6.5. Mer information finns i [&#x200B; uppgraderingsdokumentationen &#x200B;](/help/sites-deploying/upgrade.md) . <!-- UPDATE FOR EACH NEW RELEASE -->
* Hämtningen av Service Pack är tillgänglig på Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.24.0.zip).
* Installera [!DNL Experience Manager] 6.5.24.0 på en av författarinstanserna med Package Manager på en distribution med MongoDB och flera instanser.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe rekommenderar inte att du tar bort eller avinstallerar paketet [!DNL Experience Manager] 6.5.24.0. Därför bör du skapa en säkerhetskopia av `crx-repository` innan du installerar paketet, ifall du måste återställa det. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### Installera Service Pack på [!DNL Experience Manager] 6.5{#install-service-pack}

1. Starta om instansen innan installationen om instansen är i uppdateringsläge (när instansen uppdaterades från en tidigare version). Adobe rekommenderar att du startar om om den aktuella upptiden för en instans är hög.

1. Ta en ögonblicksbild eller en ny säkerhetskopia av din [!DNL Experience Manager]-instans innan du installerar.

1. Hämta Service Sack från [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.24.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Öppna Pakethanteraren och välj sedan **[!UICONTROL Upload Package]** för att överföra paketet. Mer information finns i [Pakethanteraren](/help/sites-administering/package-manager.md).

1. Markera paketet och välj sedan **[!UICONTROL Install]**.

1. Om du vill uppdatera S3-anslutningen stoppar du instansen efter installationen av Service Pack, byter ut den befintliga kopplingen mot en ny binär fil som finns i installationsmappen och startar om instansen. Se [Amazon S3-datalager](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Dialogrutan i pakethanterarens gränssnitt stängs ibland under installationen av Service Pack. Adobe rekommenderar att du väntar på att felloggarna ska stabiliseras innan du får åtkomst till distributionen. Vänta på de specifika loggarna för avinstallationen av uppdateringspaketet innan du försäkrar dig om att installationen lyckas. Vanligtvis inträffar det här problemet i webbläsaren [!DNL Safari], men kan inträffa i alla webbläsare.

**Automatisk installation**

Det finns två olika metoder att använda för att installera [!DNL Experience Manager] 6.5.24.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Placera paketet i mappen `../crx-quickstart/install` när servern är tillgänglig online. Paketet installeras automatiskt.
* Använd [HTTP-API:t från Package Manager](/help/sites-administering/package-manager.md#package-share). Använd `cmd=install&recursive=true` så att kapslade paket installeras.

>[!NOTE]
>
>Experience Manager 6.5.24.0 stöder inte installation av Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Verifiera installationen**

Information om vilka plattformar som är certifierade för att fungera med den här versionen finns i [tekniska krav](/help/sites-deploying/technical-requirements.md).

1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience Manager (6.5.24.0)` under [!UICONTROL Installed Products]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Alla OSGi-paket är antingen **[!UICONTROL ACTIVE]** eller **[!UICONTROL FRAGMENT]** i OSGi-konsolen (använd webbkonsol: `/system/console/bundles`).

1. OSGi-paketet `org.apache.jackrabbit.oak-core` är version 1.2.20 eller senare (Använd webbkonsol: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### Installera Service Pack för [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Instruktioner om hur du installerar Service Pack på Experience Manager Forms finns i [Installationsanvisningar för Experience Manager Forms Service Pack](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>Den adaptiva Forms-funktionen, som finns i [AEM 6.5 QuickStart](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/deploying/deploying/deploy), är endast avsedd för utforsknings- och utvärderingsändamål. För produktion krävs en giltig licens för AEM Forms, eftersom Adaptive Forms-funktionaliteten kräver rätt licensiering.

### Installera GraphQL Index Package för Experience Manager Content Fragments{#install-aem-graphql-index-add-on-package}

Kunder som använder GraphQL måste installera [Experience Manager Content Fragment med GraphQL Index Package 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

På så sätt kan du lägga till den indexdefinition som krävs baserat på de funktioner som de faktiskt använder.

Om du inte installerar det här paketet kan GraphQL-frågor bli långsamma eller misslyckas.

>[!NOTE]
>
>Installera bara det här paketet en gång per instans. Det behöver inte installeras om med varje Service Pack.

### UberJar{#uber-jar}

UberJar för [!DNL Experience Manager] 6.5.24.0 är tillgänglig i [Maven Central-databasen](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.24/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Om du vill använda UberJar i ett Maven-projekt ska du läsa [Använda UberJar](/help/sites-developing/ht-projects-maven.md) och inkludera följande beroende i projektstrukturen: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.24</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar och andra relaterade artefakter är tillgängliga i Maven Central Repository i stället för i Adobe Public Maven-databasen (`repo.adobe.com`). Huvudfilen för UberJar har bytt namn till `uber-jar-<version>.jar`. Det finns alltså ingen `classifier`, med `apis` som värde, för taggen `dependency`.



## Föråldrade och borttagna funktioner{#removed-deprecated-features}

Se [Inaktuella och borttagna funktioner](/help/release-notes/deprecated-removed-features.md) för en detaljerad lista över alla funktioner som har tagits bort eller tagits bort för AEM 6.5.

### SPA Editor {#spa-editor}

[SPA-redigeraren](/help/sites-developing/spa-overview.md) har tagits bort för nya projekt från och med version 6.5.24 av AEM 6.5. SPA-redigeraren stöds fortfarande för befintliga projekt, men bör inte användas för nya projekt.

De redigerare som rekommenderas för hantering av headless-innehåll i AEM är nu:

* [Den universella redigeraren](/help/sites-developing/universal-editor/introduction.md) för visuell redigering.
* [Innehållsfragmentsredigeraren](/help/sites-developing/universal-editor/introduction.md) för formulärbaserad redigering.

## Kända fel{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **Problem med JSP-skriptpaket i AEM 6.5.21-6.5.24 och AEM 6.5 LTS GA**
AEM 6.5.21 till 6.5.24 och AEM 6.5 LTS GA levereras tillsammans med `org.apache.sling.scripting.jsp:2.6.0` -paketet, som innehåller ett känt fel. Problemet är vanligtvis under hög belastning när AEM-instansen hanterar många samtidiga begäranden.

  När det här problemet inträffar kan ett av följande undantag visas i felloggarna tillsammans med referenser till `org.apache.sling.scripting.jsp:2.6.0`:

   * `java.io.IOException: classFile.delete() failed`
   * `java.io.IOException: tmpFile.renameTo(classFile) failed`
   * `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
   * `java.io.FileNotFoundException`

  När det här felet inträffar är den enda återställningsmetoden att starta om AEM-instansen.

  Kontakta kundsupporten på Adobe och läs den här versionsinformationen för en lösning.

* **Relaterat till Oak**
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
Nya mappar i `cache` och `diff-cache` skapas automatiskt och du får inte längre något undantag relaterat till `mvstore` i `error.log`.

* Uppdatera dina GraphQL-frågor som kan ha använt ett anpassat API-namn för innehållsmodellen så att standardnamnet för innehållsmodellen används i stället.

* En GraphQL-fråga kan använda indexvärdet `damAssetLucene` i stället för indexvärdet `fragments`. Den här åtgärden kan leda till att GraphQL-frågor misslyckas eller tar lång tid att köra.

  För att åtgärda problemet måste `damAssetLucene` konfigureras att inkludera följande två egenskaper under `/indexRules/dam:Asset/properties`:

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

* När du försöker flytta, ta bort eller publicera antingen innehållsfragment, webbplatser eller sidor, uppstår ett problem när referenser till innehållsfragment hämtas. Bakgrundsfrågan misslyckas. Funktionen fungerar alltså inte.
För att säkerställa korrekt åtgärd måste du lägga till följande egenskaper i indexdefinitionsnoden `/oak:index/damAssetLucene` (ingen omindexering krävs):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Om du uppgraderar din [!DNL Experience Manager]-instans från 6.5.0 till 6.5.4 till den senaste Service Pack-versionen av Java™ 11 visas `RRD4JReporter` undantag i `error.log` -filen. Starta om instansen av [!DNL Experience Manager] om du vill stoppa undantagen. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Användare kan byta namn på en mapp i en hierarki i [!DNL Assets] och publicera en kapslad mapp till [!DNL Brand Portal]. Mappens namn uppdateras dock inte i [!DNL Brand Portal] förrän rotmappen publiceras på nytt.

* Följande fel och varningsmeddelanden kan visas under installationen av [!DNL Experience Manager] 6.5.x.x:
   * &quot;När Adobe Target-integreringen har konfigurerats i [!DNL Experience Manager] med hjälp av Target Standard API (IMS-autentisering) skapas felaktiga erbjudandetyper när Experience Fragments exporteras till Target. I stället för att skriva&quot;Experience Fragment&quot;/källa&quot;Adobe Experience Manager&quot; skapar Target flera erbjudanden med typen&quot;HTML&quot;/källa&quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Inga underhållsfönster hittades på `granite/operations/maintenance`.
   * Validering på serversidan av adaptiva formulär misslyckas när sammanställningsfunktioner som SUM, MAX och MIN används (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : Inga underhållsfönster hittades på `granite/operations/maintenance`.
   * Den aktiva punkten i en interaktiv Dynamic Media-bild visas inte när du förhandsgranskar resursen via visningsprogrammet för den köpbara kanalen.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Timeout uppstod i väntan på att registerändringen skulle slutföras utan registrering.

* Från och med AEM 6.5.15 har den Rhino JavaScript-motor som tillhandahålls av paketet ```org.apache.servicemix.bundles.rhino``` ett nytt värdbeteende. Skript som använder strikt läge (```use strict;```) måste deklarera sina korrekta variabler. Annars körs de inte, vilket resulterar i ett körningsfel.

* Om du installerar taggning av relaterat innehåll som inte finns i kartongen med hjälp av ett officiellt uppdateringspaket återställs språkegenskapen för noden `/content/cq:tags` till standardvärdet. Den här åtgärden gäller för Service Packs, Security Service Pack, Extended Feature Packs, Cumulative Feature Packs, Patches osv. Det är därför nödvändigt att lägga till den från egenskaperna före installationen.

### Känt problem för AEM Sites {#known-issues-aem-sites-6524}

Content Fragments-Preview misslyckas på grund av DoS-skydd för ett stort träd med fragment. Se artikeln [KB om standardkonfigurationsalternativ för GraphQL Query Executor](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934)

### Kända fel för AEM Forms {#known-issues-aem-forms-6524}

>[!NOTE]
>
>Undvik att uppgradera till Service Pack 6.5.24.0 för problem utan en tillgänglig snabbkorrigering. Det kan leda till oväntade fel. Uppgradera till Service Pack 6.5.24.0 först när de nödvändiga snabbkorrigeringarna har släppts.

#### Problem med tillgängliga snabbkorrigeringar {#aem-forms-issues-with-hotfixes}

Följande problem har en hotfix som kan hämtas och installeras. Du kan [hämta och installera programfixen](/help/release-notes/aem-forms-hotfix.md) för att lösa dessa problem:

* **FORMS-20203**: När en användare uppgraderar Struts-ramverket från version 2.5.x till 6.x, visas inte alla konfigurationer i principgränssnittet i AEM Forms, t.ex. alternativet att lägga till en vattenstämpel.

* **FORMS-20360**: Efter uppgradering till AEM Forms Service Pack 6.5.24.0 misslyckas ImageToPDF-konverteringstjänsten med följande fel:
  ```17:15:44,468 ERROR [com.adobe.pdfg.GeneratePDFImpl] (default task-49) ALC-PDG-001-000-ALC-PDG-011-028-Error occurred while converting the input image file to PDF. com/adobe/internal/pdftoolkit/core/encryption/EncryptionImp```

* **FORMS-20478**: När du försöker konvertera TIFF-filer av typen 7/8 till PDF misslyckas konverteringsprocessen. Felkod:&quot;ALC-PDG-001-000-Image2Pdf-konverteringen misslyckades. Orsaken är: com/sun/image/codec/jpeg/JPEGCodec&quot; och&quot;ALC-PDG-0 16-003-Ett okänt/oväntat fel uppstod under efterbearbetningen av PDF.&quot; Systemet försöker att försöka igen med att använda TM ImageIO TIFF-avkodare, men misslyckas i slutändan med att slutföra jobbet.

* **FORMS-14521**: Om en användare försöker förhandsgranska ett utkast med sparade XML-data fastnar den i läget `Loading` för vissa specifika bokstäver.

* AEM Forms innehåller nu en uppgradering av Struts-versionen från 2.5.33 till 6.x för formulärkomponenten. Uppgraderingen innehåller tidigare missade strängändringar som inte ingick i SP24. Stödet lades till via en [hotfix](/help/release-notes/aem-forms-hotfix.md) som du kan hämta och installera för att lägga till stöd för den senaste versionen av Struts.

#### Andra kända fel {#aem-forms-other-known-issues}

* När du har installerat AEM Forms JEE Service Pack 21 (6.5.21.0) utför du följande steg för att lösa problemet om du hittar dubblettposter för Geode jars `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` i mappen `<AEM_Forms_Installation>/lib/caching/lib` (FORMS-14926):

   1. Stoppa positionerarna om de är igång.
   2. Stoppa AEM Server.
   3. Gå till `<AEM_Forms_Installation>/lib/caching/lib`.
   4. Ta bort alla Geode-korrigeringsfiler utom `geode-*-1.15.1.2.jar`. Bekräfta att det bara finns Geode-burkar med `version 1.15.1.2`.
   5. Öppna kommandotolken i administratörsläge.
   6. Installera Geode-korrigeringen med filen `geode-*-1.15.1.2.jar`.

* När användare uppgraderade från AEM 6.5 Forms Service Pack 18 eller 19 till Service Pack 20 eller 21 uppstod ett JSP-kompileringsfel. Det här felet hindrade dem från att öppna eller skapa anpassade formulär. Den orsakade även problem med andra AEM-gränssnitt. Gränssnitten innehåller sidredigeraren, användargränssnittet i AEM Forms, arbetsflödesredigeraren och användargränssnittet för systemöversikt. (FORMS-1256)

  Om du råkar ut för ett sådant problem följer du de här stegen för att lösa det:
   1. Navigera till katalogen `/libs/fd/aemforms/install/` i CRXDE.
   2. Ta bort paketet med namnet `com.adobe.granite.ui.commons-5.10.26.jar`.
   3. Starta om AEM Server.

* I förhandsgranskningen av gränssnittet för Interactive Communications Agent visas valutasymbolen (till exempel dollartecknet $) inkonsekvent för alla fältvärden. Den visas för värden upp till 999 men saknas för värden över 1 000. (FORMS-1657)
* Eventuella ändringar av det kapslade layoutfragmentets XDP i en interaktiv kommunikation återspeglas inte i IC-redigeraren. (FORMS-16575)
* I förhandsgranskningen av gränssnittet för den interaktiva kommunikationsagenten visas vissa beräknade värden inte korrekt. (FORMS-16603)
* När brevet visas i Förhandsgranska utskrift ändras innehållet. Vissa blanksteg försvinner och vissa bokstäver ersätts med `x`. (FORMS-15681)
* **FORMS-15428**: Efter uppdatering till AEM Forms Service Pack 20 (6.5.20.0) med Forms Add-On slutar konfigurationer som är beroende av den äldre Adobe Analytics Cloud-tjänsten med inloggningsbaserad autentisering att fungera. Det här problemet förhindrade att analysreglerna kördes korrekt.

* När en användare konfigurerar en WebLogic 14c-instans misslyckas PDFG-tjänsten i AEM Forms Service Pack 21 (6.5.21.0) på JEE som körs på JBoss® på grund av klassinläsarkonflikter i SLF4J-biblioteket. Felet visas enligt följande (CQDOC-22178):

  ```java
  Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
  the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
  @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
  (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
  have different Class objects for the type org/slf4j/ILoggerFactory used in the signature.
  ```

* FORMS-21378: När serversidesvalidering (SSV) är aktiverat kan det hända att formulärskickning misslyckas. Kontakta Adobe Support om du råkar ut för problemet.



## OSGi-paket och innehållspaket som ingår{#osgi-bundles-and-content-packages-included}

Följande textdokument innehåller en lista över de OSGi-paket och innehållspaket som ingår i den här versionen av [!DNL Experience Manager] 6.5 Service Pack:

* [Lista över OSGi-paket som ingår i Experience Manager 6.5.24.0](/help/release-notes/assets/65240-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista över innehållspaket som ingår i Experience Manager 6.5.24.0](/help/release-notes/assets/65240-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Begränsade webbplatser{#restricted-sites}

Dessa webbplatser är endast tillgängliga för kunder. Kontakta din kontoansvarige på Adobe om du är kund och behöver åtkomst.

* [Nedladdning av produkt på licensing.adobe.com](https://licensing.adobe.com/)
* [Kontakta Adobe kundsupport](https://experienceleague.adobe.com/en/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] produktsida](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5-dokumentation](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [Prenumerera på Adobe Priority-produktuppdateringar](https://www.adobe.com/subscription/priority-product-update.html)
