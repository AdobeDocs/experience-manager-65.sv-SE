---
title: '[!DNL Experience Manager] 6.5 Versionsinformation för Service Pack'
description: Versionsinformation som är specifik för  [!DNL Adobe Experience Manager] 6.5 Service Pack 9
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: 2e01bb0b16728a8073e5de47deb88de69486d408
workflow-type: tm+mt
source-wordcount: '3817'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] 6.5 Versionsinformation för Service Pack  {#aem-service-pack-release-notes}

## Versionsinformation {#release-information}

| Produkter | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.9.0 |
| Typ | Service Pack-version |
| Date | 27 maj 2021 |
| Hämta URL | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.9.zip) |

<!-- TBD: Update the SD link when SP8 is available. Same link is duplicated below in install -->

## Vad ingår i [!DNL Adobe Experience Manager] 6.5.9.0 {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.9.0 innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat samt prestanda-, stabilitets- och säkerhetsförbättringar som släppts sedan 6.5-versionen släpptes i april 2019. Service Pack är installerat på [!DNL Adobe Experience Manager] 6.5.

De viktigaste funktionerna och förbättringarna i [!DNL Adobe Experience Manager] 6.5.9.0 är:

* Nu kan AEM Sites Dynamic Media Foundation-komponenten aktivera eller inaktivera optimering för enheter med högre upplösning när du använder responsiv bildförinställning eller smart beskärning.

* För att förbättra prestandan flyttas villkoret hidden=false från JCR-frågan till QueryBuilder-utvärderaren. För att verifiera att ett dolt predikat fungerar efter ändringen kontrollerar Adobe Experience Manager att alla dolda mappar inte visas i gränssnittet.

* Möjlighet att återställa borttagna sidor och träd på en [!DNL Experience Manager Sites]-sida.

* Stöd för en ny användare att uppdatera åtkomsttoken med hjälp av en uppdateringstoken för konfigurationstjänsten för postlådor.

* [Stöd för SMTP XOAUTH2-](/help/sites-administering/notification.md#setting-up-oauth) mekanismen för e-postkonfigurationstjänsten.

* Stöd för [!DNL MongoDB] version 4.2 och 4.4.

* Förekomster av namn relaterade till Hong Kong, Macau och Taiwan uppdateras enligt de nya namnkonventionerna för kinesiska språk och regioner.

* Tillgänglighetsförbättringar i [!DNL Experience Manager] [Resurser](#assets-accessibility-6590) och [Dynamic Media](#accessibility-dm-6590).

* Smart Imaging DPR (Device Pixel Ratio) och optimering av nätverksbandbredd gör att du kan leverera bilder av högsta kvalitet effektivt. på enheter med högupplösta skärmar och begränsad nätverksbandbredd. Mer information finns i [Vanliga frågor om smart bildbehandling](/help/assets/imaging-faq.md).

   >[!NOTE]
   >
   >Tidslinjen i releasen för de ovanstående förbättringarna av Smart Imaging är:
   >
   >* Nordamerika 24 maj 2021 i NA,
      >
      >
   * Europa, Mellanöstern och Afrika 25 juni 2021,
      >
      >
   * Asien-Stillahavsområdet 19 juli 2021.


* Introducerat stöd för nästa generationens AVIF-bildformat i Dynamic Media-leverans (fmt URL-modifierare). Mer information finns i [bildvisning och återgivning av api fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html).

   >[!NOTE]
   >
   >Tidslinjen för releasen för AVIF-stöd är:
   >
   >* Nordamerika 10 maj 2021,
      >
      >
   * Europa, Mellanöstern och Afrika 24 maj 2021,
      >
      >
   * Asien-Stillahavsområdet 24 juni 2021.


* Möjlighet att skicka ett e-postmeddelande till en grupp med [!UICONTROL Assign Task]-arbetsflödessteg.

* Möjlighet att hämta ett utkast till interaktiv kommunikation efter att källan för interaktiv kommunikation har ändrats.

* Ange ett anpassat domännamn för inläsning, återgivning och validering av reCAPTCHA-tjänsten i [!DNL Experience Manager Forms].

* Förbättrade indata för arbetsflödessteget [!UICONTROL Invoke Form Data Model Service].

* Möjlighet att använda flera överordnad sidor i en dokumentmall i [!DNL Experience Manager Forms].

* Supportsidbrytningar i Postdokument i [!DNL Experience Manager Forms].

* Den inbyggda databasen (Apache Jackrabbit Oak) uppdateras till 1.22.7.

En fullständig lista över funktioner och förbättringar som introducerats i [!DNL Experience Manager] 6.5.9.0 finns i [vad som är nytt i [!DNL Adobe Experience Manager] 6.5 Service Pack 9](new-features-latest-service-pack.md).

>[!NOTE]
>
>Från och med AEM Service Pack 9 kan [!DNL Experience Manager]-kunder utveckla och använda sina [!DNL Experience Manager]-program med distributioner av [!DNL Azul Zulu]-byggen av OpenJDK, som följer Java SE-standarden.
>Adobe stöder också [!DNL Azul Zulu] JDK:er till [!DNL Experience Manager]-kunder.
>Du kan hämta relevanta versioner av [!DNL Azul Zulu JDKs] från [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
>Användarrättigheterna för Oraclet Java-tekniken, som distribuerats av Adobe, upphör att gälla i slutet av december 2022. [!DNL Experience Manager] Vi rekommenderar att man planerar och implementerar användning för  [!DNL Azul Zulu] JDK senast detta datum. Mer information om användningen av [!DNL Oracle Java]-tekniken och [!DNL Azul Zulu]-tekniken finns i [Frågor och svar](https://experienceleague.adobe.com/docs/experience-manager-65/assets/adobe-azul-openjdk-license-agreement.pdf?lang=en).

Nedan följer en lista över korrigeringar i [!DNL Experience Manager] 6.5.9.0-versionen.

### [!DNL Sites] {#sites-6590}

* Publicerade sidor med egenskapen Autentiseringskrav aktiverad dirigeras inte om till inloggningssidan och returnerar 404-felmeddelande (NPR-36354).

* När du skapar en hyperlänk fungerar inte alternativet att söka efter en länk i textkomponenten (NPR-35849).

* En genomgångsfråga aktiveras när API:t `com.day.cq.wcm.commons.ReferenceSearch` används. Det påverkar prestandan för [!DNL Experience Manager]-servern (NPR-36407).

* Kapslad layoutbehållare i en annan storleksändrad layoutbehållare visar ett felaktigt antal kolumner för sina underordnade komponenter, vilket gör att dessa komponenter inte justeras mot rutnätet (NPR-36359).

* External Link Checker visar giltiga externa länkar som ogiltiga länkar (NPR-36289).

* När du har visat referenser ett tag visas ett felmeddelande på referenspanelen (NPR-36167).

* När en komponent flyttas har den automatiskt skapade parsysen inte noden `sling:resourceType` (NPR-36165).

* När du försöker synkronisera en livecopy (när rollout-konfigurationer används [!UICONTROL Activate on Blueprint activation] och [!UICONTROL De-activate on Blueprint activation]) om en komponent tas bort i livecopy-överordnad misslyckas synkroniseringen och en `NullPointerException` loggas (NPR-36127).

* När en användare skriver ad hoc-text för tagg (tagg som inte finns i systemet) och trycker på Retur, visas taggen under fältet, men när innehållsfragmentet sparas och öppnas igen försvinner ad hoc-taggen (NPR-36132).

* Det finns inget alternativ för att visa status för asynkrona åtgärder (NPR-36104).

* En dubblettkomponent skapas efter återställning av arv (NPR-36000).

* När du använder `RemoteContentRenderingService` innehåller begäran till `RemoteContentRendererRequestHandler.getRequest` alltid rotsidan för `ComponentExporter`, men den begärda sidan tas inte med om den inte ingår i rotmodellen baserat på alternativen för genomströmningsdjup och filtrering. Begäran måste alltid innehålla den begärda sidan så att SPA har tillräckligt med information för att återge ett svar (NPR-35961).

* onTime/offTime-objekt aktiveras/inaktiveras inte för förväntad onTime/offTime (NPR-35936).

* När du publicerar en sida som innehåller ett Experience Fragment som inte har någon `cq:lastModified`-egenskap inträffar en `NullPointerException` (NPR-35914).

* När du försöker ändra storlek på en komponent i en behållare går det inte att ändra tillbaka till den ursprungliga storleken. När komponentbehållarens storlek minskas går det inte att återställa storleken till originalstorleken (NPR-35809).

* Statusikonerna för frånkopplade, pausade eller inte skapade sidor är felaktiga i dialogrutan som utlöses i redigeraren eller i Live Copy-översikten (NPR-35691).

* Flersidig körning av sidegenskaper för överordnad ignorering av kryssrutan för utrullningssida och undersidor (NPR-35634).

* Funktioner för återställning av träd som finns i det klassiska användargränssnittet saknas i Touch-gränssnittet (CQ-4315352, CQ-4309415).

* Problem vid återställning av arv och utrullning av sida på en [!DNL Experience Manager Sites]-sida (NPR-36033).

### [!DNL Assets] {#assets-6590}

[!DNL Adobe Experience Manager] 6.5.9.0  [!DNL Assets] åtgärdar följande problem.

* De taggar som skapas från ett taggrevalselement i ett [!UICONTROL Folder Metadata Schema]-formulär sparas inte (NPR-36119).

* När en liten ellips används för att anteckna resurser överlappar ellipsen numret på anteckningen i utskriftsversionen (NPR-36114).

* I kolumnvyn kan det hända att [!DNL Experience Manager] inte frågar efter en dubblettresurskonflikt när en dubblettresurs överförs (NPR-36048).

* Dialogrutan Dela länk stängs inte genom att klicka på stängningsknappen om den är öppen och inga ändringar görs (NPR-36030).

* När flera resurser har valts för att uppdatera egenskaperna inträffar ibland ett fel eller egenskaperna för en avmarkerad resurs uppdateras (NPR-36002).

* När blanktecken för överföring av resurser läggs till i början eller slutet av filnamnen, med återstående tecken som är samma som namnet på en befintlig resurs i databasen, ersätts den befintliga resursen utan att något fel loggas (NPR-36001).

* När video spelas upp på sidan med resursinformation fungerar inte alternativen för uppspelning och paus (NPR-35999).

* När resurser avpubliceras i grupp genererar Brand Portal ett fel som anger att URI:n för begäran är för lång (NPR-35954).

* När en resurs med lång anteckningstext skrivs ut trimmas anteckningstexten, även om det finns utrymme (NPR-35948).

* Alternativet att gå till nästa sida är inaktiverat när du väljer sidan i mallvyn på sidan Skapa katalog (CQ-4315462).

* När arbetsflödet för att uppdatera resurser startas på videoresursen uppdateras sidan upprepade gånger (CQ-4313375).

* DAM-mappar kan inte tas bort eller flyttas och ett undantag loggas (NPR-35942).

#### Förbättringar i resurser {#assets-enhancements}

* Alternativet [!UICONTROL None] introducerades i vyn kort, kolumn och insikter för att sortera resurser i den ordning som de lagras i JCR-noden (NPR-36356).

* Ett alternativ har lagts till för att lägga till e-post-ID i gemener i API-svar från Adobe Experience Manager (CQ-4317704).

#### Tillgänglighetsförbättringar i resurser {#assets-accessibility-6590}

[!DNL Adobe Experience Manager] 6.5.9.0  [!DNL Assets] innehåller följande tillgänglighetsförbättringar.

Kontrasten (med bakgrund) för följande text och ikoner har förbättrats så att användare med begränsad syn och uppfattning om färger kan förstå:

* tillgångstitel på sidan [!UICONTROL Properties] (NPR-35967).
* stjärngraderingsikoner i [!UICONTROL Rating]-avsnitt på olika platser (NPR-36009).
* text på tillgångs- och mappkortsvyn (NPR-35966).
* platshållartext i vyn [!UICONTROL Timeline] (NPR-35965).
* resursnamn på resurssökningsresultaten (NPR-35964).
* platshållartext i dialogrutan [!UICONTROL Link Sharing] (NPR-35963).
* [!UICONTROL Metadata],  [!UICONTROL Status]och  [!UICONTROL Other] text i  [!UICONTROL List] alternativet i  [!UICONTROL View Settings] dialogrutan (NPR-35910).
* [!UICONTROL Location] och  [!UICONTROL Type to search] platshållartexter vid global sökning (NPR-35909).
* expandera och komprimera ikoner under [!UICONTROL Content Tree] (NPR-35908).
* texten [!UICONTROL Assets] på sidan där resursmappar visas (NPR-35905).
* text i [!UICONTROL Asset Metadata], [!UICONTROL Usage Statistics] inom alternativet [!UICONTROL Overview] på sidan med tillgångsinformation (NPR-35904).
* text för kortkommandon för alternativen [!UICONTROL properties] och [!UICONTROL edit] på sidan med tillgångsinformation (NPR-35904).

### [!DNL Dynamic Media] {#dynamic-media-6590}

Adobe Experience Manager 6.5.9.0 Assets åtgärdar följande problem i [!DNL Dynamic Media]:

* Anpassade visningsprogramförinställningar och CSS replikeras inte till [!DNL Dynamic Media] när [!DNL Dynamic Media] aktiveras selektivt och inaktiveras av [standard](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/dynamicmedia/config-dm.html?lang=en#troubleshoot-dm-config) (NPR-36232).

* När du försöker förhandsgranska videoåtergivningar på sidan med resursinformation går det långsamt att läsa in videoklippen (CQ-4320122).

* Webbläsarsidan slutar svara och blir långsammare när över 200 resurser överförs med funktionen Duplicera resursidentifierare aktiverad (CQ-4319633).

* När en panoramabild läggs till på panoramamakomponenten på en sida loggas ett ej infångat referensfel (CQ-4317666).

* När en interaktiv mediavisare implementeras med Experience Fragment öppnas inte Experience Fragment från utgivaren och ett fel loggas (CQ-4317655).

* Alternativet Publicera till Dynamic Media är inte tillgängligt i snabbpublicering i metadataredigerarvyn (CQ-4317199).

* Webbplatsförfattare med skrivskyddad behörighet kan använda smarta beskärningsfunktioner för resurser och redigera smarta beskurna återgivningar. Användare med skrivskyddad behörighet får dock inte kunna redigera resursegenskaper i Sites Dev-instansen (CQ-4316450).

* Videoanteckningar fungerar inte för mappsökvägar där Dynamic Media-konfigurationen inte är aktiverad, även om AEM är Dynamic Media-läge (CQ-4314950).

* När resurstiteln har tecken för dubbelbyte, multibyte, högt ASCII, kyrilliskt, surrogatpar, hebreiska, arabiska och GB18030 får resurstiteln ett frågetecken (?) vid publicering till Dynamic Media. (CQ-4311872).

#### Tillgänglighetsförbättringar i Dynamic Media {#accessibility-dm-6590}

[!DNL Adobe Experience Manager] 6.5.9.0  [!DNL Assets] innehåller följande tillgänglighetsförbättringar i  [!DNL Dynamic Media].

* När du öppnar dialogrutan för att lägga till resurser med hjälp av tangentbordstangenter i bilduppsättningsredigeraren:
   * skärmläsare anger att dialogrutan öppnas.
   * tangentbordsfokus flyttas till dialogrutan när den öppnas.
   * tangentbordsfokus flyttas tillbaka till alternativet Lägg till resurs när dialogrutan stängs (CQ-4312134).

* Nu kan du lägga till och redigera aktiveringspunkter för resurser med hjälp av tangentbordstangenter i Hotspot-redigeraren (CQ-4305965).

* Nu kan du lägga hyperlänken på hotspot-områden via hotspot-hantering med hjälp av tangentbordstangenter. Skärmläsarens fokus flyttas nu till fältet för att redigera URL-sökväg och alternativet Öppna markeringsdialogruta (CQ-4290735).

* Kontrasten (med bakgrunden) för text och kontroller på sidan i redigeringsprogrammet för bilduppsättningar har förbättrats så att användare med begränsad syn och uppfattning om färger kan förstå (CQ-4290733).

* Nu kan du navigera till resursdelningsalternativ i redigeraren för visningsförinställningar och komprimera det utökade delningsalternativet med hjälp av tangentbordstangenter (CQ-4290724).

* Nu kan du navigera och visa verktygstips på informationsikonerna och varningsikonerna på flikarna Grundläggande och Avancerat på sidan Redigera videokodning med hjälp av tangentbordstangenter (CQ-4290722).

* Skärmläsare lägger nu till en berättarröst för de olika fälten på fliken Utseende och på fliken Beteende i redigeraren för visningsförinställningar (CQ-4290721).

* När du navigerar på sidan Redigera bildförinställning i formulärläge lägger skärmläsaren till en berättarröst för syftet och namnen på olika fält och kontroller (CQ-4290717).

* När du navigerar på detaljsidan för resurser beskriver skärmläsare nu syftet med olika alternativ i visningsprogram (CQ-4290716).

* Kontrasten (med bakgrund) för platshållartexten Alla återgivningar i återgivningar på sidan med resursinformation har förbättrats så att användare med begränsad syn och uppfattning om färg kan förstå (CQ-4290713).

* Visuell asterisk för att ange obligatoriskt fält finns nu i tillgångsfältet Rubrik i bilduppsättningsredigeraren, och skärmläsare meddelar den obligatoriska informationen för fältet (CQ-4290712).

* Skärmläsare kan nu komma åt och lägga till en berättarröst för olika interaktiva alternativ i visningsprogram på sidan med tillgångsinformation (CQ-4290708).

### Plattform {#platform-6590}

* När du genererar en miniatyrbild för en ritning och sparar ändringarna i den aktiva kopian fungerar inte arvet för vissa fält (CQ-4319517).

* När du skapar en mapp väljer du egenskapen Ordningsbar och lägger till mer än 20 resurser i mappen. Om du väljer alla resurser i mappen visas fel antal (CQ-4316243).

* När du uppdaterar en sida visas inte rätt resultat vid sorteringen av mappar eller resurser (CQ-4316200).

* Hanteringsfält JavaScript-biblioteket uppgraderas till v4.7.7 (NPR-36375).

* Anpassade paket uppdateras inte när du installerar ett nytt kodpaket med Package Manager (NPR-35949).

* En `resourceresolver`-delningsbunt gör att `Sling:alias`-frågan misslyckas (NPR-35335).

* Kontextsökvägen tas bort när SSL konfigureras i AEM (NPR-35294).

* Undantaget `SegmentNotFound` returneras efter en session som körs länge (NPR-36405).

### Integreringar {#integrations-6590}

* Det går inte att spara sidegenskaper med arv aktiverat för Cloud Services med Experience Fragments (NPR-36107).

* Sidnumrering och lazy loading av IMS-användargränssnitt ger inte rätt resultat (NPR-36046).

* När du skapar en A4T-målkonfiguration och väljer rapportkällan som [!DNL Adobe Analytics] finns det inga rapportsviter med Adobe Target-stöd tillgängliga i listrutan (NPR-36006).

### Projekt {#projects-6590}

* Det går inte att spara egenskaperna för ett projekt eftersom JCR-sökvägen till projektet inte löses på grund av ett extra snedstreck (/) som läggs till i projektsökvägen (NPR-36191).

### Skärmar {#screens-6590}

* [!DNL Experience Manager Screens] Det går inte att autentisera om en anpassad 2FA-autentiseringshanterare används (NPR-35854).

### Handel {#commerce-6590}

* Guiden [!UICONTROL Commerce Catalog] kan inte läsa in mer än 40 objekt i kolumnvyn (CQ-4318379).

### Översättningsprojekt {#translation-6590}

* Uppdaterings- eller överskrivningsalternativen visas inte när en `es`-sida konverteras till `es_es` (NPR-36170).

* När alternativet för automatiskt godkännande har valts för ett projekt med mänsklig översättning visas jobbstatusen som `Unknown` (NPR-35981).

* När du översätter en sida uppdateras inte referenssökvägen för Experience Fragments till referenssökvägen för Experience Fragment (NPR-35911).

* När du gör ändringar på de överordnade och underordnade sidorna och skickar den överordnade sidan för översättning, översätts även de underordnade sidorna felaktigt (NPR-35896).

* När det finns flera samtidiga översättningsprojekt för en vald sida länkar inte alternativet [!UICONTROL Go To Projects] till det senaste översättningsprojektet (NPR-35454).

* När du publicerar resurser på [!DNL Dynamic Media] visar [!DNL Experience Manager] ett felaktigt meddelande för opublicerade taggar (CQ-4315914, CQ-4315913).

* När du öppnar ett borttaget jobb visar [!DNL Experience Manager] ett felaktigt meddelande (CQ-4315910).

### Arbetsflöde {#workflow-6590}

* När du klickar på Complete (Fullständig), Delegate (Delegera) eller Open (Öppna) för objekt som är tillgängliga i Inbox finns ingen visuell ledtråd som anger att dessa åtgärder har slutförts (NPR-36317).

### [!DNL Communities] {#communities-6590}

* Vid filtrering av skräppost förbrukar systemet 100 % av JAVA-heap-utrymmet, vilket medför att den AEM servern krymper (NPR-36316, NPR-36493).
* I forumen läses JCR-sessionsdata som härstammar från SearchCommentSocialComponentListProvider (NPR-36235).
* När du öppnar ett specifikt inkorgsmeddelande visas alla meddelanden med felaktig sidnumrering och andra problem (NPR-35917).

### [!DNL Brand Portal] {#brandportal-6590}

* Funktionsflaggan Resurser aktiveras automatiskt när [!DNL Experience Manager Assets] konfigureras med [!DNL Brand Portal] (NPR-36010).

### [!DNL Forms] {#forms-6590}

>[!NOTE]
>
>* [!DNL Experience Manager Forms] släpper tilläggspaketen en vecka efter det schemalagda datumet för  [!DNL Experience Manager] Service Pack.
>* Du kan nu utveckla och använda program med [!DNL Azul Zulu]-versioner av [!DNL OpenJDK] för [!DNL Experience Manager Forms] på OSGi-distributioner.


**Adaptiv Forms**

* Problem med språkinitiering i [!DNL Experience Manager Forms] 6.5.7.0 när flera översättningsordlistor genereras (NPR-36439).
* När du lägger till en bifogad fil i ett adaptivt formulärfragment och skickar formuläret visas följande felmeddelande (NPR-36195):[!DNL Experience Manager Forms]

   ```TXT
    POST /content/forms/af/attachmentissue/jcr:content/guideContainer.af.submit.jsp HTTP/1.1] com.adobe.aemds.guide.servlet.GuideSubmitServlet [AF] Invalid file name or mime type for file resulted in submission failure
   ```

* När du använder mänsklig översättning för att uppdatera ett lexikon och sedan förhandsgranska ett anpassat formulär visas inte ändringarna (NPR-36035).

**Interaktiv kommunikation**

* När du överför en bild med Interactive Communications Print-kanalen och redigerar den är bilden inte längre synlig (NPR-36518).

* När du redigerar en textresurs och fyller i en platshållare tas alla interaktiva element bort från navigeringsrutan (NPR-35991).

**Arbetsflöde**

* När du anropar REST-slutpunkten för en [!DNL Experience Manager Forms]-tjänst på JBoss visar [!DNL Experience Manager] följande felmeddelande (NPR-36305):

   ```TXT
   Invalid input. The maximum length of 2000 characters was exceeded.
   ```

**BackendIntegration**

* Det går inte att spara en formulärdatamodell när Lästjänstargumentet binds till ett literalt värde som innehåller ett bindestreck (NPR-36366).

**Dokumentsäkerhet**

* När du anger certifiering och HSM för GlobalSign visar [!DNL Experience Manager Forms] felmeddelandena `Unsuported Algorithm` och `Invalid TSA Certificate` när du lägger till en tidsstämpel till LTV (NPR-36026, NPR-36025).

**Dokumenttjänster**

* Uppdaterar till [!DNL Gibson]-biblioteket för integrering med [!DNL Experience Manager Forms] (NPR-36211).

**Foundation JEE**

* När du väljer Endpoint Management i AdminUI visar [!DNL Experience Manager Forms] felmeddelandet `endpoint registry failure` (CQ-4320249).

Mer information om säkerhetsuppdateringar finns på [Experience Manager-säkerhetsbulletinsidan](https://helpx.adobe.com/security/products/experience-manager.html).

## Installera 6.5.9.0 {#install}

**Installationskrav och mer information**

* Experience Manager 6.5.9.0 kräver Experience Manager 6.5. Mer information finns i [uppgraderingsdokumentationen](/help/sites-deploying/upgrade.md).
* Service Pack-nedladdningen finns på Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* Installera Experience Manager 6.5.9.0 på en av Author-instanserna med hjälp av Package Manager på en distribution med MongoDB och flera instanser.

>[!NOTE]
>
>Adobe rekommenderar inte att du tar bort eller avinstallerar paketet [!DNL Adobe Experience Manager] 6.5.9.0.

### Installera Service Pack {#install-service-pack}

Så här installerar du Service Pack på en [!DNL Adobe Experience Manager] 6.5-instans:

1. Starta om instansen innan installationen om instansen är i uppdateringsläge (och så är fallet när instansen uppdaterades från en tidigare version). Adobe rekommenderar också en omstart om den aktuella upptiden för en instans är hög.

1. Ta en ögonblicksbild eller en ny säkerhetskopia av din [!DNL Experience Manager]-instans innan du installerar.

1. Hämta Service Pack från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.9.zip).

1. Öppna Pakethanteraren och klicka på **[!UICONTROL Upload Package]** för att överföra paketet. Mer information finns i [Pakethanteraren](/help/sites-administering/package-manager.md).

1. Markera paketet och klicka på **[!UICONTROL Install]**.

1. Om du vill uppdatera S3-anslutningen stoppar du instansen efter installationen av Service Pack, byter ut den befintliga kopplingen mot en ny binär fil som finns i installationsmappen och startar om instansen. Se [Amazon S3-datalager](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Dialogrutan för pakethanterarens gränssnitt avslutas ibland när Service Pack installeras. Adobe rekommenderar att du väntar på att felloggarna ska stabiliseras innan du får åtkomst till distributionen. Vänta på de specifika loggarna för avinstallationen av uppdateringspaketet innan du försäkrar dig om att installationen lyckas. Vanligtvis inträffar detta på [!DNL Safari], men kan inträffa i alla webbläsare.

**Automatisk installation**

Det finns två sätt att installera Adobe Experience Manager 6.5.9.0 automatiskt på en fungerande instans:

S. Placera paketet i mappen `../crx-quickstart/install` när servern är tillgänglig online. Paketet installeras automatiskt.

B. Använd [HTTP-API:t från Package Manager](/help/sites-administering/package-manager.md#package-share). Använd `cmd=install&recursive=true` så att kapslade paket installeras.

>[!NOTE]
>
>Adobe Experience Manager 6.5.9.0 stöder inte installation av Bootstrap.

**Validera installation**

1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience Manager (6.5.9.0)` under [!UICONTROL Installed Products].

1. Alla OSGi-paket är antingen **[!UICONTROL ACTIVE]** eller **[!UICONTROL FRAGMENT]** i OSGi Console (Använd webbkonsol: `/system/console/bundles`).

1. OSGi-paketet `org.apache.jackrabbit.oak-core` är version 1.2.3 eller senare (Använd webbkonsol: `/system/console/bundles`).

Information om vilka plattformar som är certifierade för att fungera med den här versionen finns i [tekniska krav](/help/sites-deploying/technical-requirements.md).

### Installera Adobe Experience Manager Forms tilläggspaket {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Hoppa över om du inte använder Experience Manager Forms. Korrigeringar i Experience Manager Forms levereras via ett separat tilläggspaket en vecka efter den schemalagda versionen av [!DNL Experience Manager] Service Pack.

1. Kontrollera att du har installerat Adobe Experience Manager Service Pack.
1. Ladda ned motsvarande tilläggspaket från Forms som finns på [AEM Forms releases](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#forms-updates) för ditt operativsystem.
1. Installera Forms tilläggspaket enligt beskrivningen i [Installera AEM Forms tilläggspaket](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>AEM 6.5.9.0 innehåller en ny version av [AEM Forms-kompatibilitetspaket](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases). Om du använder en äldre version av AEM Forms Compatibility Package och uppdaterar till AEM 6.5.9.0 installerar du den senaste versionen av paketet efter installationen av Forms Add-On Package.

### Installera Adobe Experience Manager Forms på JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Hoppa över om du inte använder AEM Forms på JEE. Korrigeringar i Adobe Experience Manager Forms på JEE levereras via ett separat installationsprogram.

Information om hur du installerar det kumulativa installationsprogrammet för Experience Manager Forms på JEE och konfigurationen efter distributionen finns i [versionsinformationen](jee-patch-installer-65.md).

>[!NOTE]
>
>När du har installerat det kumulativa installationsprogrammet för Experience Manager Forms på JEE installerar du det senaste Forms-tilläggspaketet, tar bort Forms-tilläggspaketet från mappen `crx-repository\install` och startar om servern.

### UberJar {#uber-jar}

UberJar för Experience Manager 6.5.9.0 finns i [Maven Central-databasen](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.9/).

Om du vill använda UberJar i ett Maven-projekt läser du [hur du använder UberJar](/help/sites-developing/ht-projects-maven.md) och inkluderar följande beroende i projektstrukturen:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.9</version>
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
| Integreringar | Skärmen **[!UICONTROL AEM Cloud Services Opt-In]** är föråldrad. Tack vare integreringen mellan Experience Manager och Adobe Target som uppdaterades i Experience Manager 6.5 för att stödja Adobe Target Standard API, som använder autentisering via Adobe IMS och I/O, och den växande rollen hos Adobe Launch för att instrumentera Experience Manager sidor för analys och personalisering, har guiden för att välja In blivit funktionellt irrelevant. | Konfigurera systemanslutningar, Adobe IMS-autentisering och [!DNL Adobe I/O]-integreringar via respektive Experience Manager molntjänster. |
| Anslutningar | Adobe JCR Connector för Microsoft SharePoint 2010 och Microsoft SharePoint 2013 är föråldrad för Experience Manager 6.5. | Ej tillämpligt |

## Kända fel {#known-issues}

* Om du uppgraderar din [!DNL Experience Manager]-instans från version 6.5 till version 6.5.9.0 kan du visa `RRD4JReporter`-undantag i `error.log`-filen. Starta om instansen för att lösa problemet.

* Om du installerar [!DNL Experience Manager] 6.5 Service Pack 5 eller ett tidigare Service Pack på [!DNL Experience Manager] 6.5 tas körtidskopian av din resurskräddarsydda arbetsflödesmodell (skapad i `/var/workflow/models/dam`) bort.
Om du vill hämta körtidskopian rekommenderar Adobe att du synkroniserar designtidskopian av den anpassade arbetsflödesmodellen med körtidskopian med hjälp av HTTP API:
   `<designModelPath>/jcr:content.generate.json`.

* Om en mapp i hierarkin byter namn i [!DNL Experience Manager Assets] och den kapslade mappen som innehåller en resurs publiceras i [!DNL Brand Portal], uppdateras inte mappens namn i [!DNL Brand Portal] förrän rotmappen publiceras igen.

* När en användare väljer att konfigurera ett fält för första gången i ett adaptivt formulär visas inte alternativet att spara en konfiguration i egenskapsläsaren. Om du väljer att konfigurera ett annat fält i det adaptiva formuläret i samma redigerare åtgärdas problemet.

* Följande fel och varningsmeddelanden kan visas under installationen av Experience Manager 6.5.x.x:
   * &quot;När Adobe Target-integreringen har konfigurerats i Experience Manager med Target Standard API (IMS-autentisering) skapas felaktiga erbjudandetyper när Experience Fragments exporteras till Target. I stället för att skriva&quot;Experience Fragment&quot;/källa&quot;Adobe Experience Manager&quot; skapar Target flera erbjudanden med typen&quot;HTML&quot;/källa&quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Validering på serversidan av adaptiva formulär misslyckas när sammanställningsfunktioner som SUM, MAX och MIN används (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Aktiveringspunkten i en interaktiv Dynamic Media-bild syns inte när du förhandsvisar mediefilen via Shoppable Banner Viewer.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tidsgränsen överskreds i väntan på att reg.ändringen skulle slutföras utan registrering.

## OSGi-paket och innehållspaket som ingår {#osgi-bundles-and-content-packages-included}

Följande textdokument listar de OSGi-paket och innehållspaket som ingår i [!DNL Experience Manager] 6.5.9.0:

* [Förteckning över OSGi-paket som ingår i Experience Manager 6.5.9.0](assets/6590_bundles.txt)

* [Förteckning över innehållspaket som ingår i Experience Manager 6.5.9.0](assets/6590_packages.txt)

## Begränsade webbplatser {#restricted-sites}

Dessa webbplatser är bara tillgängliga för kunder. Om du är kund och behöver åtkomst kontaktar du din kontoansvarige på Adobe.

* [Nedladdning av produkt på licensing.adobe.com](https://licensing.adobe.com/)
* Se [hur du kontaktar Adobe kundtjänst](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5 Versionsinformation](/help/release-notes/release-notes.md)
* [[!DNL Experience Manager] produktsida](https://www.adobe.com/marketing/experience-manager.html)
* [[!DNL Experience Manager] 6.5-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-65.html)
* [Prenumerera på produktuppdateringar med Adobe prioritet](https://www.adobe.com/subscription/priority-product-update.html)

