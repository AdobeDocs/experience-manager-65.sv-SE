---
title: '[!DNL Adobe Experience Manager] 6.5 Service Pack versionsinformation'
description: Versionsinformation för  [!DNL Adobe Experience Manager] 6.5 Service Pack 7
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: ed8299662139c2c2ab2fa304c9fa3448b0fce223
workflow-type: tm+mt
source-wordcount: '3696'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager] 6.5 Service Pack versionsinformation  {#aem-service-pack-release-notes}

## Versionsinformation {#release-information}

| Produkter | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.7.0 |
| Typ | Service Pack-version |
| Date | 26 november 2020 |
| Hämta URL | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.7.zip) |

<!-- TBD: Update the SD link when SP7 is available. -->

## Vad ingår i [!DNL Adobe Experience Manager] 6.5.7.0 {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.7.0 är en viktig uppdatering som innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat samt prestanda, stabilitet och säkerhetsförbättringar som släppts sedan 6.5-utgåvan släpptes i april 2019. Service Pack är installerat på [!DNL Adobe Experience Manager] 6.5.

De viktigaste funktionerna och förbättringarna i [!DNL Adobe Experience Manager] 6.5.7.0 är:

* Sortera de Live Copy-sidor som är tillgängliga för utrullning med hjälp av egenskaperna [!UICONTROL Name], [!UICONTROL Last modified date,] och [!UICONTROL Last rollout date].

* Utföra sidflyttningar och MSM-utrullningar som asynkrona åtgärder för att minska deras påverkan på körningsprestanda.

* Användare kan sortera digitala resurser i kort- och kolumnvyn.

* [!DNL Assets] och  [!DNL Dynamic Media] erbjuder flera tillgänglighetsförbättringar. Förbättringarna rör tangentbordsnavigering, användning av skärmläsare och möjlighet för användare att använda liknande hjälpmedelsteknik (AT). Se [[!DNL Assets] förbättringar](#assets-6570) och [[!DNL Dynamic Media] förbättringar](#dynamic-media-6570).

* Den inbyggda databasen (Apache Jackrabbit Oak) uppdateras till version 1.2.5.

En fullständig lista över funktioner och förbättringar som introducerats i [!DNL Experience Manager] 6.5.7.0 finns i [Nyheter i [!DNL Adobe Experience Manager] 6.5 Service Pack 7](new-features-latest-service-pack.md).

Nedan följer en lista över korrigeringar i [!DNL Experience Manager] 6.5.7.0-versionen.

### [!DNL Sites] {#sites-6570}

* När du öppnar alternativet [!UICONTROL Timewrap] för en sida, låter alternativet Sidospår i tidslinjen vara öppet och navigerar till konsolen [!UICONTROL Sites] inträffar felet `Failed to Load` (NPR-34951).

* Alternativet [!UICONTROL Timewrap] visar inte bilder för det valda datumet och tidsintervallet (NPR-34951).

* När ett filter anropar `getHeader()` från en sida som innehåller ett innehållsfragment inträffar felet `java.lang.AbstractMethodError` (NPR-34942).

* När sökvägen till en sida innehåller flera innehållsdelsträngar kan förhandsgranskningarna inte återges och funktionen för versionsjämförelse misslyckas också (NPR-34740).

* När du anger ett numeriskt värde för egenskapen `String` type label för en komponent kan du ta bort komponenten och ångra borttagningsåtgärden. När du har ångrat borttagningen ändras etikettegenskapen från `String` till `Long` (NPR-34739).

* Följande undantag inträffar när ett Experience Fragment läggs till som är baserat på en mall med en låst layout på en sida (NPR-34632):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.mozilla.javascript.EcmaError: TypeError: Cannot call method "getChildren" of null
   ```

* När du flyttar en mapp uppstår problem med genomgången och följande fel inträffar (NPR-34554):

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript. org.apache.jackrabbit.oak.query.RuntimeNodeTraversalException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped
   ```

* När nya resurser skapas, publiceras och flyttas till en ny plats skapas arbetsflödet `Request to complete move operation` och resultatet blir ett avbrutet tillstånd. Om du överför en ny resurs och kör en `move`-åtgärd skapas arbetsflödet `Request to complete move operation` i väntande läge (NPR-34543).

* När du exporterar ett Experience Fragment från [!DNL Experience Manager] 6.5.2-miljö till [!DNL Target] Standard misslyckas API-anropet eftersom arbetsyteegenskapen inte är tillgänglig för [!DNL Target] Standard (NPR-34557).

* Användare kan inte publicera sidor med alternativet [!UICONTROL manage publication] eftersom alternativet [!UICONTROL Publish] försvinner (NPR-34542).

* När du lägger till vissa format i texten läggs en `<div>`-tagg till i texten och formatet kan inte längre användas på texten (NPR-34531).

* När du markerar ett alternativ på en snabbmeny och uppdaterar de filer som krävs, går det inte att spara dialogvärden eftersom den andra menyn har ett tomt obligatoriskt fält (NPR-34529).

* När du skapar en sida från en anpassad mall och flyttar den inom hierarkin för utkast, visas komponenter som togs bort tidigare från sidan på sidan i den aktiva kopieringshierarkin (NPR-34527).

* När ett artikelformat har tillämpats på ett innehåll kan det inte tas bort (NPR-34486).

* Alla live-kopior och kopior av en Experience Fragment pekar på samma [!DNL Adobe Target] erbjudande-ID (NPR-34469).

* Punkter i punktlistor visas utöver den numrerade listan (NPR-34455).

* Alternativet Jämför med källa kan inte visa skillnaden mellan källsidan och den redigerade versionen av en sida (NPR-34285).

* När du tar bort en sida går det inte att konfigurera versionsinformationen (NPR-34159).

* När en användare väljer alternativet [!UICONTROL Open Selection] går tangentbordsfokus till den dolda kontrollen på sidan (CQ-4307779, CQ-4293601).

* När du flyttar en publicerad mapp på författaren uppdateras inte mappsökvägarna i enlighet med detta på publiceringsinstansen (CQ-4305144).

* När en användare väljer `Enter`-tangenten för alternativet [!UICONTROL Select All] flyttas tangentbordsfokus inte till alternativet [!UICONTROL Create Control] (CQ-4293599).

* När du väljer `Esc`-tangenten återställs inte fokus till den överordnade kontrollen (CQ-4293593, CQ-4293590).

* Förbättrad WCAG-kompatibilitet för [!DNL Sites] UI- och Core-komponenter (CQ-4293448).

* [!UICONTROL Zoom] och  [!UICONTROL Scale] funktioner är inaktiverade för  [!DNL Sites Editor] sidan (CQ-4282353).

* När du har använt alternativet Rotera höger avbryts berättarrösten för den aktuella rotationen eller det aktuella vändläget (CQ-4282128).

* Dialogruteknapparna Klar och Avbryt konfigurering har fler än ett tabbstopp (CQ-4274601).

* Det är inte tillåtet att flytta sidor med liknande namn på samma nivå (NPR-35041).

* När du har valt alternativet Radera (x) flyttas tangentbordsfokus inte till fältet [!UICONTROL Filter] (CQ-4293581).

* När du uppgraderar till [!DNL Experience Manager] 6.5.6.0 ändras det ärvda styckesystemets beteende och fungerar inte korrekt (NPR-35117).

* Tangentbordsanvändare kan inte ändra tabbfokus i lämplig ordning efter att ha valt [!UICONTROL Action]-avsnittet på en [!DNL AEM Sites]-sida (CQ-4307786).

* När du har valt ett alternativ i listan med länkmål i verktygsfältet för textredigering när du redigerar ett innehållsfragment, börjar dialogrutan för författare av innehållsfragment flimra (CQ-4305532).

* Tangentbordsanvändare kan inte välja alternativen i listrutan [!UICONTROL Add Component] med nedpilstangenten (CQ-4295097).

* Flikfokus flyttas inte i lämplig ordning när du väljer ett datum på menyn Kalender på fliken [!UICONTROL Assets] på en [!DNL Sites]-sida (CQ-4293600).

* Flikfokus flyttas inte till nästa eller föregående alternativ för tangentbordsanvändare efter att alternativen Länk eller Text som är tillgängliga vid redigering av en platssida har tagits bort (CQ-4293597).

* Tangentbordsanvändare kan inte ändra tillbaka tabbfokus till Fler alternativ i [!UICONTROL Actions]-avsnittet efter att ha visat de tillgängliga alternativen och tryckt på `Esc`-tangenten (CQ-4293592).

* När du aktiverar alternativet [!UICONTROL Rotate] för en bild i [!UICONTROL Edit]-läget växlar tabbfokus, i stället för att vara kvar på Rotera, till alternativet [!UICONTROL Redo] för tangentbordsanvändare (CQ-4293587).

* I dialogrutan [!UICONTROL Open Selection] som finns på fliken [!UICONTROL Link and Actions] flyttas tabbfokus till dolda element på sidan efter alternativet [!UICONTROL Cancel] (CQ-4293579).

* När kortkommandoanvändare redigerar en bild, navigerar till alternativet [!UICONTROL Finish] och trycker på Retur, kommer skärmläsarna inte att meddela att de är klara (CQ-4282351).

* Alternativen Flytta uppåt och Flytta nedåt som är tillgängliga i dialogrutan [!UICONTROL Link and Actions] är inte tillgängliga för skärmläsare och kortkommandoanvändare (CQ-4281120).

* Tangentbordsanvändare kan inte återställa tabbfokus efter att de navigerat till alternativet Stäng (X) på sidan [!UICONTROL Properties] (CQ-4293581, NPR-34653).

### [!DNL Assets] {#assets-6570}

[!DNL Adobe Experience Manager] 6.5.7.0  [!DNL Assets] åtgärdar följande och ger följande förbättringar.

* Följande förbättringar har gjorts för tillgänglighet i [!DNL Experience Manager Assets] i den här versionen. Mer information finns i [tillgänglighetsfunktioner i [!DNL Assets]](/help/assets/accessibility.md).

   * När du navigerar på tidslinjen med ett tangentbord kan `Esc`-tangenten komprimera [!UICONTROL Show All]-alternativet utan att förlora fokus (CQ-4293598).
   * När du navigerar med tangentbordets tabbtangent behålls fokus i taggfältet (NPR-35109) när du har tagit bort den sista taggen från de tillagda taggarna.
   * [!DNL Experience Manager] innehåller nu lämplig information för namn, roll och värde som ska användas av skärmläsare (NPR-34255).
   * När du har tagit bort kombinationsrutan Typ/storlek, kombinationsrutan Länk, Kombinationsrutan Språk eller textredigeringsrutan, återgår tangentbordsfokus till nästa eller föregående element i användargränssnittet eller till ett mer relevant element i användargränssnittet (CQ-4293585).
   * När du håller pekaren över alternativ visas tips som Markera och Hämta. Användare som använder en skärmförstorare kanske inte ser filminiatyrbilderna på grund av dessa tips. Nu är det möjligt att behålla fokus när du har tagit bort alternativet med `Escape`-tangenten. (CQ-4293554).
   * När du väljer en stödrastercell från det stödraster som finns på sidan flyttas fokus till det åtgärdsfält som visas på skärmen (CQ-4282127).
   * Visuella användare kan skilja mellan normal text och en länk, eftersom visuella ledtrådar (underline- och chevron-ikoner) visas för länkar till alla lösningar på startsidan för [!DNL Experience Manager] (CQ-4282072).

* Följande förbättringar av användarupplevelsen görs i [!DNL Assets]:

   * Möjliggör sortering av resurser i kortvyn och kolumnvyn (NPR-35097).

* Om en JSON-fil genereras med Assets HTTP API efter uppgraderingen till 6.5, uppstår problem med den kodning som används i filen (NPR-35129).

* Användare av en grupp som inte har behörighet att skapa samlingar (alternativet Skapa samling är inte tillgängligt) kan fortfarande skapa samlingar genom direktåtkomst till URL:en `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/collections/createcollectionwizard.html/content/dam/collections?contentPath=/content/dam/collections` (NPR-35115).

* När de sökda resurserna sorteras efter namn sorteras de efter skiftlägeskänsliga inställningar. Detta skapar två separata sorterade listor baserade på skiftläget som visas på rätt sätt i sökresultaten (NPR-35068).

* När ett innehållsfragment öppnas i redigeraren loggas varningsmeddelanden (`Invalid value specified for a metadata property`) i felloggarna (NPR-35012).

* Användare utan administratörsbehörighet kan redigera utgångna resurser med [Experience Manager]-datorprogrammet. (NPR-34993).

* När samma resurs dras i Assets-användargränssnittet och en ny version skapas blir ändringarna i metadata inte beständiga (NPR-34940).

* När du redigerar samlingar kan användaren ta bort titeln på samlingen och spara ändringarna (NPR-34889).

* När du överför en duplicerad bild visas ett borttagningsalternativ. Om du väljer Ta bort kan bilderna överföras. Arbetsflödet för DAM-uppdatering av tillgångar aktiveras också (NPR-34744).

* När du använder [!DNL Adobe Asset Link] med [!DNL Adobe InDesign] innehåller sökresultaten inte mappar och samlingar, utan bara resurser (NPR-34699, CQ-4303666).

* Pekaren placeras på kortvyn och skärmen rullas som ett resultat av (automatisk) fokus på de snabbåtgärder som är tillgängliga på kortet (NPR-34514).

* När du redigerar egenskaperna för flera resurser samtidigt stängs gruppredigeringsvyn och omdirigeras till huvudsidan [!DNL Assets] när du väljer alternativet [!UICONTROL Save]. Detta beteende är detsamma som beteendet för alternativet [!UICONTROL Save & Close] och förväntas inte (NPR-34546).

* Den smarta samlingen visar inte rätt inställning för användargränssnitt när den har sparats. Frågan sparas korrekt, men gränssnittet visar alltid det senast tillagda Option-predikatet (NPR-34539).

* När du lägger till resurser i [!DNL Experience Manager] importeras inte metadata utan namnutrymme (NPR-34530).

* När du drar en resurs till en mapp för att flytta den visas även alternativet [!UICONTROL Drop in Lightbox] och [!UICONTROL Drop in Collection] i användargränssnittet. Även om flyttåtgärden avbryts fortsätter användargränssnittet att visa de senare två alternativen (NPR-34526).

* Symbolen `%>` visas på sidan för samlingar (NPR-34499).

* I kolumnvyn visar [!DNL Assets] duplicerade mapp- och resursnamn när du bläddrar uppåt och nedåt innan alla resurser visas (NPR-34464).

* Om du skapar en privat mapp omedelbart efter att du har skapat en gemensam mapp används inställningarna för den privata mappen (NPR-34415) för den gemensamma mappen.

* I kortvyn visas korten inte i alfabetisk ordning och korten kan inte sorteras i alfabetisk ordning (NPR-34234).

* När överlappningsregler öppnas igen behålls inte alternativen i användargränssnittet (CQ-4301452).

#### [!DNL Dynamic Media] {#dynamic-media-6570}

* Följande förbättringar har gjorts för hjälpmedel i [!DNL Dynamic Media] (CQ-4290306). Mer information finns i [tillgänglighetsfunktioner i [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).

   * Skärmläsare (JAWS, Skärmläsaren) lägger till en berättarröst för menyalternativens namn, roll och tillstånd på menyn Bädda in storlek (CQ-4290927).
   * Användare kan navigera i dialogrutan E-postlänk med `Tab`-tangenten (CQ-4290926).
   * Arbetsflödet för att skapa videokodningsprofiler är mer användarvänligt med tanke på skärmläsarförbättringarna (CQ-4290623, CQ-4290622).
   * När du navigerar med `Tab`-tangenten flyttas fokus till lämpliga element i användargränssnittet i arbetsflödet för att skapa en interaktiv video (CQ-4290621, CQ-4290620, CQ-4290619).
   * Sidan Publicera, Redigera resurs, sidan Redigera smarta beskärningar och sidan Redigera bilduppsättning har förbättrats så att de uppfyller webbstandarderna. Användare av hjälpfunktioner (AT) kan nu enkelt navigera på dessa sidor och vidta åtgärder som beskärningsbilder (CQ-4290617, CQ-4290616, CQ-4290613, CQ-4290612, CQ-429 (CQ-4290614).
   * Visningsprogrammen har förbättrats så att användarna kan navigera med tangentbordet (CQ-4290615).
   * Användare av tangentbord och skärmläsare kan använda beskärningsfunktionen (CQ-4290609).
   * Tangentbordsanvändarna kan hantera de aktiveringspunkter som behövs bättre (CQ-4290604, CQ-4290603).

* Remote Imagesets kan inte redigeras i [!DNL Experience Manager] om företagsnamnet och mappnamnet är samma (NPR-31340).

* z-indexordningen är felaktig när du försöker förhandsgranska utdata efter att ha lagt till en aktiveringspunkt i en [!DNL Dynamic Media]-bild eller efter att ha redigerat en [!DNL Dynamic Media]-video eller en [!DNL Experience Fragment]-bild (CQ-4307267).

* [!DNL Dynamic Media] synkroniseringen misslyckas när blandade medieuppsättningar bearbetas på nytt (CQ-4307184).

* Om en resurs flyttas till en mapp där automatisk synkronisering till [!DNL Dynamic Media] är konfigurerad synkroniseras inte resursen (CQ-4307122).

* [!DNL Dynamic Media] video spelas inte upp på iOS-enheter med de inbyggda HTML5-videokontrollerna (CQ-4306977, CQ-4306727).

* Det går inte att hämta bilder som SmartCrop används på (CQ-4304558).

* Det går inte att selektivt publicera mappar till dynamiska media (CQ-4304526).

* Om du avpublicerar en videofil från [!DNL Experience Manager] avpubliceras inte den adaptiva videouppsättningen från en konfigurerad Scene7-distribution (CQ-4304405).

* Om du lägger till en panoramabild i en panoramamakomponent och uppdaterar sidan uppstår ett `Uncaught ReferenceError: $ is not defined`-fel (CQ-4302810).

* I [!UICONTROL Viewer Presets Editor] är modifieringsetiketten `PANORAMICVIEW_AUTOROTATE` inte tillgänglig när du redigerar [!UICONTROL PanoramicImage/PanoramicImage_VR]-förinställningen i `PanoramicView`-komponenten (CQ-4302443).

* Bildtexter visas inte om videon inte är den första i en MixedMediaSet (CQ-4298161).

* HTML5 eCatalog Viewer på iPhone-mobilenheter kan inte vända på sidorna eller vända på sidorna (CQ-4296611).

* När du rullar färgrutor på en mobil enhet rullas färgrutorna till höger och ut ur det synliga området några sekunder innan du bläddrar tillbaka till vyn (CQ-4296439).

* När en Överordnad post för visningsförinställning skapas publiceras inte CSS och teckningen och bara visningsförinställningen publiceras (CQ-4262205).

* När du försöker länka ett Experience Fragment för en viss hotspot i [!UICONTROL Interactive Video/Images]-komponenten visas inte den valda Experience Fragment-sökvägen. I stället returneras ett tomt värde från sökvägsfältet (NPR-35146, CQ-4298136).

* Det går inte att förhandsgranska ett Experience Fragment i IVV Editor (CQ-4308560).

* När du lägger till en hotspot i en bild och väljer ett Experience Fragment går det inte att välja undermapparna och varianterna för Experience Fragment (CQ-4307455).

* Resurserna som inte är bilder visas inte som publicerade efter överföring (CQ-4306415).

#### [!DNL Experience Manager] 3D-resurser  {#three-d-assets-6570}

* `DAM CQ MIME Type` använder felaktiga MIME-typer på 3D-resurser, vilket leder till felaktig återgivning (NPR-34731).

### [!DNL Commerce] {#commerce-6570}

* Användargränssnittet för Commerce-produktsamlingen innehåller inte fler än 15 produkter i en samling (NPR-34502).

### Plattform {#platform-6570}

* En HTTP-session över HTTPS är inte ogiltig (NPR-35083).
* En `NullPointerException` returneras när underhållsaktiviteter startas dagligen eller veckovis från användargränssnittet (NPR-34953).
* W3C-valideraren rapporterar varningar för kompatibla JavaScript-filer för klientbibliotek (NPR-34898).
* Funktionen `AudienceOmniSearchHandler` använder ett inaktuellt index (NPR-34870).
* Om du loggar ut från Experience Manager rensas inte cookies (NPR-34743).
* Funktionen `findByTitle` i API:t `TagManager` fungerar inte om taggnamnet innehåller ett specialtecken (NPR-34357).
* Processen att importera användarsynkroniseringspaketet misslyckades (NPR-34399).
* Stöd för egenskaperna `ariaLabel` och `ariaLabelledby` har lagts till i komponenten `Coral.Masonry` (GRANITE-29962).
* Dispatcher-cachen uppdateras inte för sidor med innehållsfragment efter installation av de senaste kärnkomponentpaketen (CQ-4306788).
* Lokaliserade taggnamn med citattecken (`"`) visas inte korrekt i användargränssnittet (CQ-4305439).

### Användargränssnitt {#ui-6570}

* Fältet [!UICONTROL Link to] i komponentegenskaperna visar förslag för automatisk komplettering som inte matchar den angivna strängen (NPR-34865).

* AEM visar följande felmeddelande när du schemalägger ett dagligt underhållsfönster som är fördelat mellan 2 dagar (NPR-35280):

   ```TXT
   ERROR The start time must precede (be less than) the end time
   ```

### Integreringar {#integrations-6570}

* Redigering av en befintlig [!DNL Adobe Launch]-konfiguration misslyckas (NPR-35045).
* Det går inte att exportera [!DNL Experience Fragments] till [!DNL Adobe Target] om IMS-konfigurationen och miljön [!DNL Adobe Target Standard] används (NPR-34555).
* Alternativet [!UICONTROL Create] visas på sidan [!UICONTROL Audiences] när du navigerar från en mapp till sidan [!UICONTROL Audiences] (NPR-35151).

### Sling {#sling-6570}

* Standardhälsokontrollen vid inloggning validerar inloggningsuppgifterna för en användare som inte finns (NPR-34686).

### Översättningsprojekt {#translation-6570}

* Om du avbryter ett översättningsprojekt i [!DNL Experience Manager] skickas ingen begäran om att avbryta det till översättningsprovidern (NPR-34433).

### [!DNL Communities] {#communities-6570}

* Alla fall av orättvis terminologi i produkten ska ersättas med vedertagna motsvarigheter (NPR-34311).
* [!DNL Google+] tas bort från listan över alternativ för delning via sociala medier (NPR-33877).

### [!DNL Brand Portal] {#brandportal-6570}

* Användargränssnittet svarar inte när resurserna väljs i [!UICONTROL List View] (NPR-34728).

### [!DNL Forms] {#forms-6570}

>[!NOTE]
>
>[!DNL Experience Manager Forms] släpper tilläggspaketen en vecka efter det schemalagda datumet för  [!DNL Experience Manager] Service Pack.

Mer information om säkerhetsuppdateringar finns på [Experience Manager-säkerhetsbulletinsidan](https://helpx.adobe.com/security/products/experience-manager.html).

## Installera 6.5.7.0 {#install}

**Installationskrav och mer information**

* AEM 6.5.7.0 kräver AEM 6.5. Mer information finns i [uppgraderingsdokumentationen](/help/sites-deploying/upgrade.md).
* Service Pack-nedladdningen finns på Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* Installera AEM 6.5.7.0 på en av Author-instanserna med Package Manager på en distribution med MongoDB och flera instanser.

>[!NOTE]
>
>Adobe rekommenderar inte att du tar bort eller avinstallerar paketet [!DNL Adobe Experience Manager] 6.5.7.0.

### Installera Service Pack {#install-service-pack}

Så här installerar du Service Pack på en befintlig Adobe Experience Manager 6.5-instans:

1. Starta om instansen innan installationen om instansen är i uppdateringsläge (och så är fallet när instansen uppdaterades från en tidigare version). Adobe rekommenderar också en omstart om den aktuella upptiden för en instans är hög.

1. Ta en ögonblicksbild eller en ny säkerhetskopia av din [Experience Manager]-instans innan du installerar.

1. Hämta Service Pack från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.7.zip).

1. Öppna Pakethanteraren och klicka på **[!UICONTROL Upload Package]** för att överföra paketet. Mer information finns i [Pakethanteraren](/help/sites-administering/package-manager.md).

1. Markera paketet och klicka på **[!UICONTROL Install]**.

1. Om du vill uppdatera S3-anslutningen stoppar du instansen efter installationen av Service Pack, byter ut den befintliga kopplingen mot en ny binär fil som finns i installationsmappen och startar om instansen. Se [Amazon S3-datalager](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Dialogrutan för pakethanterarens gränssnitt avslutas ibland när Service Pack installeras. Adobe rekommenderar att du väntar på att felloggarna ska stabiliseras innan du får åtkomst till distributionen. Vänta på de specifika loggarna för avinstallationen av uppdateringspaketet innan du försäkrar dig om att installationen lyckas. Vanligtvis inträffar detta på [!DNL Safari], men kan inträffa i alla webbläsare.

**Automatisk installation**

Det finns två sätt att installera Adobe Experience Manager 6.5.7.0 automatiskt på en fungerande instans:

S. Placera paketet i mappen `../crx-quickstart/install` när servern är tillgänglig online. Paketet installeras automatiskt.

B. Använd [HTTP-API:t från Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html). Använd `cmd=install&recursive=true` så att kapslade paket installeras.

>[!NOTE]
>
>Adobe Experience Manager 6.5.7.0 stöder inte installation av Bootstrap.

**Validera installation**

1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience Manager (6.5.7.0)` under [!UICONTROL Installed Products].

1. Alla OSGi-paket är antingen **[!UICONTROL ACTIVE]** eller **[!UICONTROL FRAGMENT]** i OSGi Console (Använd webbkonsol: `/system/console/bundles`).

1. OSGi-paketet `org.apache.jackrabbit.oak-core` är version 1.2.3 eller senare (Använd webbkonsol: `/system/console/bundles`).

Information om vilka plattformar som är certifierade för att fungera med den här versionen finns i [tekniska krav](/help/sites-deploying/technical-requirements.md).

### Installera Adobe Experience Manager Forms tilläggspaket {#install-aem-forms-add-on-package}

>[!NOTE]
>
>[!DNL Experience Manager Forms] släpper tilläggspaketen en vecka efter det schemalagda datumet för  [!DNL Experience Manager] Service Pack.

>[!NOTE]
>
>Hoppa över om du inte använder AEM Forms. Korrigeringar i Adobe Experience Manager Forms levereras via ett separat tilläggspaket.

1. Kontrollera att du har installerat Adobe Experience Manager Service Pack.
1. Ladda ned motsvarande tilläggspaket från Forms som finns på [AEM Forms releases](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) för ditt operativsystem.
1. Installera Forms tilläggspaket enligt beskrivningen i [Installera AEM Forms tilläggspaket](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Installera Adobe Experience Manager Forms på JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Hoppa över om du inte använder AEM Forms på JEE. Korrigeringar i Adobe Experience Manager Forms på JEE levereras via ett separat installationsprogram.

Information om hur du installerar det kumulativa installationsprogrammet för Experience Manager Forms på JEE och konfigurationen efter distributionen finns i [versionsinformationen](jee-patch-installer-65.md).

### UberJar {#uber-jar}

UberJar för Experience Manager 6.5.7.0 finns i [Maven Central-databasen](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.7/).

Om du vill använda UberJar i ett Maven-projekt läser du [hur du använder UberJar](/help/sites-developing/ht-projects-maven.md) och inkluderar följande beroende i projektstrukturen:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.7</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar och andra relaterade artefakter finns tillgängliga i Maven Central Repository i stället för i Adobe Public Maven-databasen (`repo.adobe.com`). Huvudfilen för UberJar har bytt namn till `uber-jar-<version>.jar`. Det finns alltså inget `classifier`, med `apis` som värde, för taggen `dependency`.

## Inaktuella funktioner {#removed-deprecated-features}

Nedan finns en lista över funktioner som är markerade som borttagna med [!DNL Experience Manager] 6.5.7.0. Funktioner markeras som borttagna från början och senare i en framtida version. Ett alternativt alternativ brukar anges.

Granska om du använder en funktion eller en funktion i en distribution. Planera också att ändra implementeringen så att ett alternativt alternativ används.

| Yta | Funktion | Ersättning |
|---|---|---|
| Integreringar | Skärmen **[!UICONTROL AEM Cloud Services Opt-In]** är föråldrad. Med integreringen av AEM och Target uppdaterades i AEM 6.5 för att stödja Target Standard API, som använder autentisering via Adobe IMS och I/O, och den växande rollen hos Adobe Launch för att instrumentera AEM sidor för analys och personalisering, har guiden för att välja In blivit funktionellt irrelevant. | Konfigurera systemanslutningar, Adobe IMS-autentisering och Adobe I/O-integreringar via respektive AEM-molntjänster. |
| Anslutningar | Adobe JCR Connector för Microsoft SharePoint 2010 och Microsoft SharePoint 2013 är borttagen för AEM 6.5. | Ej tillämpligt |

## Kända fel {#known-issues}

* Ignorera följande fel i `error.log`-filen under installationen av Experience Manager 6.5.7.0:

   ```TXT
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy(1314)] : Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy(1316)] : Could not load implementation object class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy(1315)] : Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy)
   ```

* Om du uppgraderar din [!DNL Experience Manager]-instans från version 6.5 till version 6.5.7.0 kan du visa `RRD4JReporter`-undantag i `error.log`-filen. Starta om instansen för att lösa problemet.

* Om du installerar [!DNL Experience Manager] 6.5 Service Pack 5 eller ett tidigare Service Pack på [!DNL Experience Manager] 6.5 tas körtidskopian av din resurskräddarsydda arbetsflödesmodell (skapad i `/var/workflow/models/dam`) bort.
Om du vill hämta körtidskopian rekommenderar Adobe att du synkroniserar designtidskopian av den anpassade arbetsflödesmodellen med körtidskopian med hjälp av HTTP API:
   `<designModelPath>/jcr:content.generate.json`.

* Kontakta Adobe kundtjänst om du stöter på problem när du redigerar och skapar överlappande regler i [!UICONTROL Folder Metadata Schema Forms Editor] och [!UICONTROL Metadata Schema Forms Editor] med hjälp av dialogrutan [!UICONTROL Define Rule]. Reglerna som redan har skapats och sparats fungerar som förväntat.

* Om en mapp i hierarkin byter namn i [!DNL Experience Manager Assets] och den kapslade mappen som innehåller en resurs publiceras i [!DNL Brand Portal], uppdateras inte mappens namn i [!DNL Brand Portal] förrän rotmappen publiceras igen.

* När en användare väljer att konfigurera ett fält för första gången i ett adaptivt formulär visas inte alternativet att spara en konfiguration i egenskapsläsaren. Om du väljer att konfigurera ett annat fält i det adaptiva formuläret i samma redigerare åtgärdas problemet.

* Om [!UICONTROL Connected assets configuration]-guiden returnerar ett 404-felmeddelande efter installationen måste du installera om paketen `cq-remotedam-client-ui-content` och `cq-remotedam-client-ui-components` manuellt med hjälp av pakethanteraren.

* Följande fel och varningsmeddelanden kan visas under installationen av AEM 6.5.x.x:
   * &quot;När Target-integrationen har konfigurerats i AEM med Target Standard API (IMS-autentisering) skapas felaktiga erbjudandetyper när Experience Fragments exporteras till Target. I stället för att skriva&quot;Experience Fragment&quot;/källa&quot;Adobe Experience Manager&quot; skapar Target flera erbjudanden med typen&quot;HTML&quot;/källa&quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Validering på serversidan av adaptiva formulär misslyckas när sammanställningsfunktioner som SUM, MAX och MIN används. CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Aktiveringspunkten i en interaktiv bild i Dynamic Media är inte synlig när du förhandsgranskar resursen via visningsprogrammet för den köpbara kanalen.

## OSGi-paket och innehållspaket som ingår {#osgi-bundles-and-content-packages-included}

Följande textdokument innehåller en lista över de OSGi-paket och innehållspaket som ingår i AEM 6.5.7.0:

* [Förteckning över OSGi-paket som ingår i AEM 6.5.7.0](assets/6570_bundles.txt)

* [Förteckning över innehållspaket som ingår i AEM 6.5.7.0](assets/6570_packages.txt)

## Begränsade webbplatser {#restricted-sites}

Dessa webbplatser är bara tillgängliga för kunder. Om du är kund och behöver åtkomst kontaktar du din kontoansvarige på Adobe.

* [Nedladdning av produkt på licensing.adobe.com](https://licensing.adobe.com/)
* Se [hur du kontaktar kundsupport](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5 Versionsinformation](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] produktsida](https://www.adobe.com/marketing/experience-manager.html)
>* [[!DNL Experience Manager] 6.5-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* Prenumerera på [produktuppdateringar med Adobe prioritet](https://www.adobe.com/subscription/priority-product-update.html)

