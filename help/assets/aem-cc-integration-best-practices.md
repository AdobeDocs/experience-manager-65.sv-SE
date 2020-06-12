---
title: Bästa praxis för integrering av Adobe Creative Cloud och [!DNL Adobe Experience Manager].
description: Bästa tillvägagångssätt för att integrera [!DNL Adobe Experience Manager] med [!DNL Adobe Creative Cloud] för att effektivisera resursöverföringsarbetsflöden och uppnå hög innehållshastighet.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 17fa61fd0aff066bd59f4b6384d2d91bb97b749c
workflow-type: tm+mt
source-wordcount: '3262'
ht-degree: 15%

---


# [!DNL Adobe Experience Manager] och [!DNL Creative Cloud] bästa praxis för integrering {#aem-and-creative-cloud-integration-best-practices}

[!DNL Adobe Experience Manager Assets] är en DAM-lösning (Digital Asset Management) som kan integreras med [!DNL Adobe Creative Cloud] för att hjälpa DAM-användare att samarbeta med kreativa team och effektivisera samarbetet när innehåll skapas.

[!DNL Adobe Creative Cloud] ger kreativa team ett ekosystem av lösningar och tjänster som hjälper dem att skapa digitala resurser. Det omfattar dator- och mobilapplikationer, molntjänster som lagring med skrivbordssynkronisering eller webbupplevelse, liksom marknadsplatser som [!DNL Adobe Stock].

Läs vidare för att ta reda på vilka integreringar som du ska välja mellan stationär dator och företagsspecifik DAM baserat på ditt användningsfall och vilka metoder som är associerade med de sammankopplade arbetsflödena.

>[!NOTE]
>
>[!DNL Experience Manager] till- [!DNL Creative Cloud] mappdelning är föråldrat och ingår inte längre i den här guiden. Adobe rekommenderar att du använder nyare funktioner som [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) eller [Experience Manager-datorprogrammet](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/introduction.html) för att ge kreativa användare tillgång till resurser som hanteras i [!DNL Experience Manager].

## Samarbete mellan kreatörer, marknadsförare och DAM-användare {#collaboration-needs-of-creatives-marketers-and-dam-users}

| Krav | Använd skiftläge | Involverade ytor |
|---|---|---|
| Förenkla för kreatörer på datorn | Effektivisera åtkomsten till resurser från en DAM ([!DNL Experience Manager Assets]) för kreatörer, eller mer allmänt, användare på datorer som arbetar i program för att skapa egna resurser. De behöver ett enkelt och enkelt sätt att upptäcka, använda (öppna), redigera och spara ändringar [!DNL Experience Manager]samt överföra nya filer. | Skrivbordet Win eller Mac. [!DNL Creative Cloud] appar |
| Tillhandahåll högkvalitativa, färdiga resurser från [!DNL Adobe Stock] | Marknadsförarna hjälper till att snabba upp processen för att skapa innehåll genom att hjälpa till med materialanskaffning och identifiering. Kreatörer använder det godkända materialet direkt inifrån sina kreativa verktyg. | [!DNL Experience Manager Assets]; [!DNL Adobe Stock] Marknadsplats. metadatafält |
| Distribuera och dela resurser efter organisationer | Interna avdelningar/lokala kontor och externa partners, distributörer och byråer använder det godkända material som delas av huvudorganisationen. Organisationen vill säkert och smidigt dela de skapade resurserna för vidare återanvändning. | Varumärkesportal, Resursdelningskommentarer |

## Adobes lösningar för samverkan {#adobe-offerings-to-support-the-collaboration-need}

| Värdeförslag för berörda personer | Erbjudande | Involverade ytor |
|---|---|---|
| Creative users upptäcker resurser från [!DNL Experience Manager], öppnar och använder dem, redigerar och överför ändringar till [!DNL Experience Manager]samt överför nya filer till [!DNL Experience Manager], utan att lämna [!DNL Creative Cloud] programmen. | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]och [!DNL Adobe InDesign]. |
| Affärsanvändare förenklar öppning och användning av resurser, redigering och överföring av ändringar [!DNL Experience Manager]samt överföring av nya filer till [!DNL Experience Manager] från skrivbordsmiljön. De använder en allmän integrering för att öppna alla resurstyper i det inbyggda datorprogrammet, inklusive sådana som inte kommer från Adobe. | [Experience Manager-datorprogram](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) | [!DNL Experience Manager] datorprogram på Win- och Mac-datorer |
| Marknadsförare och företagsanvändare upptäcker, förhandsgranskar, licensierar och sparar samt hanterar [!DNL Adobe Stock] mediefiler inifrån [!DNL Experience Manager]. Licensierade och sparade resurser ger utvalda [!DNL Adobe Stock] metadata för bättre styrning. | [Integrering av Experience Manager och Adobe Stock](aem-assets-adobe-stock.md) | [!DNL Experience Manager] webbgränssnitt |

Den här artikeln fokuserar främst på de två första aspekterna av samarbetsbehovet. Distribution och anskaffning av resurser i stor skala omnämns kortfattat som ett användningsexempel. Överväg Adobes varumärkesportal eller Assets Share Commons för sådana behov. Alternate solutions such as [Brand Portal](https://helpx.adobe.com/se/experience-manager/brand-portal/user-guide.html), solutions that can be built based on [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) components, [Link Share](/help/assets/link-sharing.md), using [Experience Manager Assets](/help/assets/managing-assets-touch-ui.md) should be reviewed based on specific requirement.

![Creative Cloud-anslutningar för Experience Manager, avgöra vilka funktioner som ska användas](assets/creative-connections-aem.png)

### Mappning av användningsfall och Adobe-lösningar {#mapping-of-use-cases-and-adobe-solutions}

| Användningsfall | [!DNL Adobe Asset Link] | [!DNL Experience Manager] datorprogram | Anmärkningar/andra lösningar |
|---|---|---|---|
| Upptäck - bläddra bland DAM-mappar | Ja | [!DNL Experience Manager] Webbgränssnitt och skrivbordsfunktioner |  |
| Upptäck - få åtkomst till DAM-samlingar | Ja | [!DNL Experience Manager] Webbgränssnitt och skrivbordsfunktioner |  |
| Upptäck - sök efter resurser från DAM | Ja | [!DNL Experience Manager] Webbgränssnitt och skrivbordsfunktioner |  |
| Använd - öppen resurs | Ja | Ja | [Öppna från webbgränssnittet](managing-assets-touch-ui.md#previewing-assets) eller från Finder |
| Använd - placera resurs från DAM i ett dokument | Ja - inbäddning | Ja - länkning eller inbäddning | [!DNL Experience Manager] datorprogrammet ger åtkomst till resurser som filer i det lokala filsystemet. De här länkarna i de ursprungliga programmen representeras av lokala sökvägar. |
| Redigera - öppna för redigering | Ja - utcheckningsåtgärd | Ja - Öppna åtgärd (i nätverksresursen) | [Checka ut i AAL](https://helpx.adobe.com/se/enterprise/using/manage-assets-using-adobe-asset-link.html) sparar resursen i användarens Creative Cloud-lagringskonto (synkroniserat med Creative Cloud-programmet) som standard. |
| Redigera - pågående arbete utanför DAM | Ja - Tillgängliga resurser i användarens Creative Cloud-lagringskonto synkroniserat med skrivbordet. | Ja |  |
| Redigera - ladda upp ändringar | Ja - [incheckningsåtgärd](https://helpx.adobe.com/se/enterprise/using/manage-assets-using-adobe-asset-link.html) med valfri kommentar | Ja |  |
| Överför - en fil | Ja - överför aktuellt aktivt dokument | Ja | [Överför via webbgränssnitt](managing-assets-touch-ui.md#uploading-assets) |
| Överför - flera filer/hierarkiska mappstrukturer | Nej | Ja | [Ladda upp via webbgränssnitt](managing-assets-touch-ui.md#uploading-assets) eller via skript eller verktyg. |
| Diverse - användare och inloggning | Creative Cloud-användare som är inloggad på Creative Cloud-datorprogrammet blir igenkända (SSO) | [!DNL Experience Manager] användare och autentiseringsuppgifter | Användare av båda lösningarna räknas in i [!DNL Experience Manager] användarkvoten. |
| Diverse - nätverk och åtkomst | Kräver åtkomst från användarens skrivbord till [!DNL Experience Manager] distribution via nätverk | Kräver åtkomst från användarens skrivbord till [!DNL Experience Manager] distribution via nätverk | [!DNL Adobe Asset Link] delar inte nätverksproxymiljö. |
| Diverse - Migrera ett stort antal resurser | Nej | Nej | [Guide för resursmigrering](assets-migration-guide.md) |

För att stödja användningsexemplen på resursfördelning bör andra lösningar beaktas:

* [Varumärkesportalen](https://helpx.adobe.com/se/experience-manager/brand-portal/user-guide.html) för ett konfigurerbart SaaS-tillägg för [!DNL Experience Manager Assets] publicering av resurser.
* Anpassade lösningar skapas baserat på kodbasen [Resursdelningskommentarer](https://adobe-marketing-cloud.github.io/asset-share-commons/) .
* [!DNL Experience Manager] [länkdelning](/help/assets/link-sharing.md) för att dela resurser ad hoc med hjälp av länkar.
* [Experience Manager Assets-webbgränssnittet](/help/assets/managing-assets-touch-ui.md) med områden för externa parter som skyddas av [!DNL Experience Manager] åtkomstkontrollinställningar och nödvändiga IT-/nätverkskonfigurationsjusteringar, vilket ger dessa externa användare åtkomst till [!DNL Experience Manager].

## Viktiga begrepp och användningsområden {#key-concepts-and-use-cases}

### Ordlista med vanliga termer {#glossary-of-common-terms}

* **Pågående arbeten eller pågående designarbeten (WIP):** En fas i en resurs livscykel där den genomgår flera ändringar och oftast inte är redo att delas med större team.
* **Kreativa resurser:** [!DNL Assets] som är redo att delas med ett större team, eller som har valts ut/godkänts av det kreativa teamet för att delas med marknadsförings- eller LOB-team.
* **Godkännanden av resurser:** Godkännandeprocessen som körs för resurser som redan har överförts till DAM, som vanligtvis omfattar varumärkesgodkännanden, juridiska godkännanden och så vidare.
* **Slutlig resurs:** En resurs som har genomgått alla godkännanden och all metadatataggning och är klar att användas av teamet. En sådan resurs lagras i DAM och är tillgänglig för alla (intresserade) användare. Den kan användas i marknadsföringskanaler eller av designteam för att skapa material.
* **Mindre uppdatering/ändring av resurs:** En snabb och liten ändring av en digital resurs. Ändringarna är ofta retuscheringar, smärre redigeringar, resursgranskningar eller godkännanden (t.ex. omplacering, ändring av textstorlek, justering av mättnad/intensitet eller färg).
* **Större uppdatering/ändring av resurs:** En arbetskrävande ändring av en digital resurs, som ibland tar lång tid att genomföra. Den omfattar vanligtvis flera ändringar. Resursen måste sparas flera gånger medan den uppdateras. Större resursuppdateringar medför oftast att resursen får statusen pågående arbete.
* **DAM:** Digitalt resurshanteringssystem. In this document, it is synonymous with [!DNL Experience Manager Assets], unless specifically mentioned otherwise.
* **Designanvändare:** En kreatör som skapar digitalt material med Creative Cloud-program och -tjänster. I vissa fall är designanvändaren medlem i ett designteam och kan använda Creative Cloud, men skapar inte digitala resurser (som en designchef eller designteamschef).
* **DAM-användare:** En typisk användare av ett DAM-system. Beroende på organisationen kan en DAM-användare vara en marknadsföringsanvändare eller en icke-marknadsföringsanvändare, till exempel en affärsområdesanvändare, bibliotekarie eller säljare.

### Att tänka på när du använder [!DNL Experience Manager] och [!DNL Creative Cloud] integrerar {#considerations-when-using-aem-and-creative-cloud-integration}

* Se [de effektivaste strategierna för skrivbordsappar](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/troubleshoot.html#best-practices-to-prevent-troubles)
* Se [Adobe Stock-integrering](aem-assets-adobe-stock.md)
* Se [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)

Detta är en kort sammanfattning av bästa praxis för [!DNL Experience Manager] och [!DNL Creative Cloud] integrering. Läs resten av det här dokumentet för att få en mer detaljerad förståelse för dessa.

* **För designanvändare som arbetar i Photoshop, InDesign eller Illustrator:** Adobe Asset Link ger den bästa användarupplevelsen, inklusive ren hantering av pågående arbeten för resurser som checkats ut från [!DNL Experience Manager].
* **För att förenkla åtkomsten till resurser från skrivbordet för alla generiska filformat eller program:** använd [!DNL Experience Manager] datorprogrammet.
* **Förstå varför och när resurser ska lagras i DAM:** Uppdateringar som ska göras tillgängliga för hela teamet i organisationen.
* **Tänk på mängden resurser som delas:** Om ni använder mediedistribution kan styrning och säkerhet vara de viktigaste aspekterna. Överväg att använda verktyg som är byggda för att göra detta i stor skala, som varumärkesportalen.
* **Förstå resursers livscykel:** Ta reda på hur resurser hanteras i organisationen av olika team
* **Var försiktig med ofta sparade resurser:** Adobe Asset Link tar hand om det med PS, AI och ID. För andra program bör du inte utföra pågående arbete i mappade/delade mappar om du behöver alla ändringar i DAM

### Åtkomst till [!DNL Adobe Stock] resurser från [!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}

[Integreringen](/help/assets/aem-assets-adobe-stock.md) med Experience Manager och Adobe Stock ger [!DNL Experience Manager] användarna möjlighet att söka, förhandsgranska, licensiera och spara resurser från [!DNL Adobe Stock] till [!DNL Experience Manager]. Licensierade och sparade [!DNL Stock] resurser har valt [!DNL Stock] metadata som kan användas för att söka efter dem med extra filter.

Några viktiga punkter om den här integreringen:

* När resurser från Adobe Stock sparas i [!DNL Experience Manager]blir de vanliga [!DNL Assets]och binära sparas i [!DNL Experience Manager] databasen. Vissa metadata som är relaterade till [!DNL Adobe Stock] sparas för resursen i, [!DNL Experience Manager]annars ser det ut som för andra filer. Om till exempel smarta taggar är aktiva läggs taggarna till i de här resurserna när de sparas.
* Resursen som sparas i [!DNL Experience Manager] är en kopia, inte en länk tillbaka till [!DNL Adobe Stock].

**Arbeta med resurser som sparats[!DNL Adobe Stock]i[!DNL Experience Manager]In[!DNL Creative Cloud]**. Den här integreringen är oberoende av[!DNL Adobe Asset Link], men[!DNL Adobe Asset Link]känner igen dessa resurser som sparats på[!DNL Stock]det sättet och visar ytterligare metadata och[!DNL Stock]ikoner för dessa resurser i[!DNL Adobe Asset Link]tilläggsgränssnittet i[!DNL Photoshop],[!DNL Illustrator]eller[!DNL InDesign]. Filerna är tillgängliga för att bläddra, öppna och så vidare, eftersom de är vanliga resurser när de sparas i[!DNL Experience Manager].
Creative-användare som arbetar i[!DNL Creative Cloud]program med[!DNL Adobe Asset Link]tillägg kan, förutom att ha tillgång till redan licensierade resurser från[!DNL Adobe Stock]till[!DNL Experience Manager], även använda[!DNL Creative Cloud]Libraries-panelen för att söka efter, förhandsgranska och licensiera[!DNL Adobe Stock]resurser.[!DNL Assets]från[!DNL Adobe Stock]licensierade och sparade i[!DNL Experience Manager]blir tillgängliga för de större team som får tillgång till[!DNL Experience Manager Assets]distributionen, medan kreatörer som licensierar mediefiler från[!DNL Adobe Stock]via[!DNL Creative Cloud]Libraries-panelen endast gör dem tillgängliga för sig själva som standard på sina[!DNL Creative Cloud]konton.

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM article.
-->

## Lagra resurser i ett resurshanteringssystem {#about-storing-assets-in-a-dam}

För att skapa ett effektivt arbetsflöde mellan kreatörer och marknadsförare/branschspecifika team (LOB) och välja de bästa supportfunktionerna är det viktigt att förstå när och varför resurser lagras i DAM.

### Varför resurser lagras i DAM {#why-assets-are-stored-in-dam}

Genom att lagra resurser i DAM blir de enkelt tillgängliga och sökbara. Det ser till att resurserna kan utnyttjas av många användare i organisationen eller ekosystemet, bland annat partners, kunder och så vidare.

De flesta organisationer väljer att endast lagra resurser som är relevanta för marknadsförings-/LOB-processerna längre fram i kedjan (publicera till kanaler som webbkanaler via [!DNL Experience Manager Sites] eller andra kanaler som hanteras av Adobe Experience Cloud - Marketing Cloud, Advertising Cloud, och som mäts av Analytics Cloud, som tillhandahålls användare/partner och så vidare). Dessutom lagrar organisationer resurser som kan bli föremål för en gransknings-/godkännandeprocess i DAM. På så sätt lagrar DAM de flesta resurser som har stora chanser att utnyttjas och undviker att lagra inaktiva resurser.

Lagring av resurser är också beroende av tekniska aspekter och resursutnyttjande. DAM tillhandahåller ytterligare tjänster runt lagrade resurser, inklusive extrahering av metadata, versionshantering, generering av förhandsgranskning/omkodning, hantering av referenser och tillägg av åtkomstkontrollsinformation. Dessa tjänster kräver extra tid och infrastrukturresurser.

Det är ofta inte önskvärt att lagra alla resurser och uppdateringar. Om till exempel uppdateringar av specifika resurser har dålig kvalitet och förbrukar för mycket resurser, kanske resurserna inte lagras i DAM.

#### När resurser lagras i DAM {#when-assets-are-stored-in-dam}

Kreativa team (och organisationer) är vanligtvis inte intresserade av att lagra resurser i varje skede av resursens livscykel. De undviker till exempel att lagra resurser i följande fall:

* Resurser som ännu inte har slutförts eller som är föremål för experimenterande.
* Resurser som inte klarar granskningsprocessen.
* Jämfört med resursen i fråga har teamet bättre kandidater att representera sitt arbete för externa team.

Vanligtvis lagras följande klassresurser i DAM:

* Tillgångar som har nått en viss löptid och anses vara klara att delas.
* Resurser som har valts ut i förväg av det kreativa teamet.
* Specifika resursformat som kan användas eller begäras av marknadsföring, beroende på ett specifikt kontrakt eller avtal (t.ex. JPG-filer som konverterats från RAW-filer, TIFF-filer/bilder från PSD-original).

#### När uppdateringar av resurser lagras i DAM {#when-updates-to-assets-are-stored-in-dam}

I regel ska endast uppdateringar av resurser som är relevanta för den bredare uppsättningen DAM-användare lagras i DAM. Det ser till att användare (marknadsföringsfunktioner och liknande funktioner) bara ser relevanta versioner på tidslinjen för DAM-resurser.

Vanligtvis ändras relaterade till viktiga milstolpar i resursens livscykel. Den initiala marknadsföringsfärdiga resursen eller en officiell uppdatering som baseras på begäran/granskning som tillhandahålls av det kreativa teamet bör till exempel lagras och versionshanteras i DAM.

Det kreativa teamets uppdatering för granskning av marknadsföringsteamet efter en begäran om ändring av befintligt material i DAM är ett exempel på en relevant uppdatering. Den ska lagras och versionshanteras i DAM för vidare referens eller för att återgå till den tidigare versionen.

Nedan följer exempel på uppdateringar som vanligtvis inte är relevanta:

* Tidiga versioner av mediefiler som överförts innan de är klara för marknadsföringsgranskning
* Vanliga kreativa förändringar av resursen i den pågående arbetsfasen innan kreatörer och marknadsförare bestämmer sig för att resursen är klar

### Användaråtkomst till DAM {#user-access-to-dam}

[!DNL Assets] har stöd för två typer av användare baserat på deras åtkomst till [!DNL Assets] distributionen. Vanligtvis har användare i företagsnätverket (brandväggen) direktåtkomst till DAM. Andra användare utanför företagsnätverket skulle inte ha direkt åtkomst. Användartypen avgör vilka integreringar som kan användas ur teknisk synpunkt.

#### Kreativa användare med direkt åtkomst till DAM {#creative-users-with-direct-access-to-dam}

Vanligtvis har interna kreativa team, byråer/kreatörer som är anställda på det interna nätverket tillgång till DAM-instansen, inklusive [!DNL Experience Manager] inloggning. [!DNL Experience Manager] och nätverksinfrastruktur kan konfigureras för att ge direktåtkomst till externa parter - vanligen betrodda organisationer som byråer som arbetar för en klient - för att få åtkomst till [!DNL Experience Manager] via nätverket, till exempel via VPN eller IP-listan.

I sådana fall kan Adobe Asset Link eller [!DNL Experience Manager] skrivbordsappen enkelt ge åtkomst till slutliga/godkända resurser och göra det möjligt att spara kreativa resurser på DAM.

#### Kreativa användare utan åtkomst till DAM {#creative-users-without-access-to-dam}

Externa byråer och frilansare som inte har direkt åtkomst till DAM-instansen kan behöva åtkomst till godkända resurser eller lägga till sina nya designer i DAM.

Använd följande strategier för att ge åtkomst till slutliga/godkända mediefiler:

* Använd skrivbordsappen om Asset Link inte fungerar.
* Använd [Experience Manager Assets Brand Portal](https://helpx.adobe.com/se/experience-manager/brand-portal/user-guide.html) för säker distribution av resurser till externa partner
* Använd en anpassad implementering av en distributions- och källportal baserad på [resursdelningskommentarer](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Använd den åtkomstkontroll som har konfigurerats i [!DNL Experience Manager] och nödvändig nätverksinfrastruktur (till exempel listan över tillåtna VPN- och IP-adresser) för att ge externa parter åtkomst till ett dedikerat innehållsområde i din DAM. De kan använda [!DNL Experience Manager] webbgränssnittet för att hämta resurser och överföra nytt innehåll till din DAM.

#### Pågående arbete med resurser från [!DNL Experience Manager] {#work-in-progress-on-assets-from-aem}

Som beskrivs i det här dokumentet rekommenderar vi att du utför större uppdateringar av resurser, ibland kallat pågående arbete, utan att ha alla redigeringar sparade i den lokala filen överförda till [!DNL Experience Manager] som ändringar. Detta snabbar upp arbetet för en stationär användare, begränsar den nätverksbandbredd som används och håller resursernas tidslinje ren och fokuserad på kontrollerade, viktiga uppdateringar.

Adobe Asset Link har ett bra stöd för detta:

* När användare i [!DNL Photoshop], [!DNL InDesign]eller [!DNL Illustrator] för att redigera en fil utför de en utcheckningsåtgärd för den angivna resursen
* Resursen hämtas i bakgrunden, läggs till användare Creative Cloud-kontot synkroniserat med disken av Creative Cloud-datorprogrammet och utcheckningsflaggan aktiveras [!DNL Experience Manager] på resursen för att minimera redigeringskonflikter
* Därifrån arbetar användaren i en fil som lagras lokalt på den synkroniserade platsen och kan fortsätta att arbeta och spara nödvändiga ändringar med den frekvens som behövs
* Eftersom resursen finns på Creative Cloud-kontot är den dessutom tillgänglig på andra enheter som användaren kan ha (till exempel kan öppnas eller redigeras i en dedikerad Creative Cloud-mobilapp) och kan delas med andra Creative Cloud-användare i samarbetssyfte.
* När den kreativa användaren är klar med ändringarna kan han/hon utföra en incheckningsåtgärd för filen i sitt Creative Cloud-program, med en valfri kommentar. Motsvarande resurs i [!DNL Experience Manager] versionshanteras och uppdateras till med den nya binärfilen. [!DNL Experience Manager] -användare som marknadsförare eller LOB-användare har tillgång till större förändringar av tillgångar, eller milstolpar, via [!DNL Experience Manager] resursens tidslinjegränssnitt.

[!DNL Experience Manager] datorprogrammet har en nätverksresurs för resurser som öppnas i det ursprungliga programmet. Som standard överförs alla ändringar som görs lokalt till [!DNL Experience Manager] automatiskt efter en kort stund. Med en sådan konfiguration överförs ofta sparande under den pågående arbetsfasen till [!DNL Experience Manager] och versionsindelas, vilket skapar en hel del nätverkstrafik och potentiella skalbarhetsproblem - för att inte tala om onödiga versioner i [!DNL Experience Manager].

Det rekommenderade sättet här är att använda ett alternativ i [!DNL Experience Manager] skrivbordsappen för att inaktivera automatiska uppdateringar och överföra ändringar av resurser till [!DNL Experience Manager] manuellt, med hjälp av åtgärden för överföring av ändringar i programmets resursstatusgränssnitt.

#### Massöverföring till DAM {#bulk-upload-to-dam}

Du kan behöva överföra ett större antal filer till DAM samtidigt i vissa scenarier, till exempel:

* Överföra resultat från foton eller större projekt
* Överföra material från reklambyråer
* Överför markerade resurser från en större uppsättning om markeringen görs utanför DAM

Beskrivningen avser att överföra filer operativt (till exempel varje vecka eller med varje fotografering), som en normal del av datoranvändarens arbetsflöde. Stora resursmigreringar beskrivs inte här.

Du kan använda följande överföringsfunktioner:

* Om du vill överföra stora/hierarkiska mappar samtidigt använder du [!DNL Experience Manager] skrivbordsappen som har funktioner för [mappöverföring](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html#bulkupload) . Du kan också överföra hierarkiska mappstrukturer. [!DNL Assets] överförs i bakgrunden och är därför inte knuten till en webbläsarsession
* Om du vill överföra några filer från en enda mapp drar du filerna direkt till webbgränssnittet eller använder alternativet Skapa i [!DNL Assets] webbgränssnittet.
* Beroende på vilka affärskrav du har kan du även använda en anpassad överförare.

#### Hantera digitala resurser direkt från skrivbordet {#managing-digital-assets-directly-from-desktop}

Om du använder Network File Shares för att hantera digitala resurser kan du se att bara den nätverksresurs som mappas av [!DNL Experience Manager] skrivbordsappen används som ett praktiskt alternativ. När du övergår från filresurser i nätverket har webbgränssnittet en mängd funktioner för hantering av digitala resurser som går mycket längre än vad som är möjligt på en nätverksresurs (sökning, samlingar, metadata, samarbete, förhandsvisningar med mera) och [!DNL Experience Manager] [!DNL Experience Manager] skrivbordsappen är en praktisk länk för att ansluta DAM-databasen på serversidan med datorarbetet.

Undvik att använda [!DNL Experience Manager] skrivbordsappen för att hantera resurser direkt i nätverksresursen för [!DNL Assets]. Undvik till exempel att använda [!DNL Experience Manager] skrivbordsappen för att flytta/kopiera flera filer. Använd i stället gränssnittet för att dra mappar från Finder/Utforskaren till nätverksresursen eller använd funktionen [!DNL Assets] [!DNL Assets] Mappöverföring.

#### Resursmigrering {#asset-migration}

Information om hur du planerar och kör resursmigreringar från ett befintligt system till ett nytt system eller migrering av stora volymer resurser som lagras på servrar finns i [migreringshandboken](/help/assets/assets-migration-guide.md). [!DNL Experience Manager] skrivbordsappen och [!DNL Experience Manager] till [!DNL Creative Cloud] integreringar stöder inte sådana migreringar. På grund av de stora volymer resurser som ska importeras och ytterligare krav på metadatamappning, omvandling och förtäring bör migreringar hanteras med olika verktyg och metoder.

>[!MORELIKETHIS]
>
>* [Adobe Asset Link](https://helpx.adobe.com/in/enterprise/using/adobe-asset-link.html)
>* [Bästa praxis för Experience Manager-datorprogram](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Experience Manager Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Integrering av Experience Manager och Adobe Stock](aem-assets-adobe-stock.md)

