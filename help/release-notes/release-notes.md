---
title: Versionsinformation för  [!DNL Adobe Experience Manager] 6.5
description: Hitta versionsinformation, nyheter, installationsguider och en detaljerad ändringslista för  [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 7939703fe7ef9382e9d1a426c0eb9f021b964d1a
workflow-type: tm+mt
source-wordcount: '4665'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] 6.5 Versionsinformation om senaste Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Versionsinformation {#release-information}

| Produkt | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.22.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Typ | Service Pack-version |
| Datum | Torsdag den 21 november 2024 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Hämta URL | [Programdistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Vad ingår i [!DNL Experience Manager] 6.5.22.0 {#what-is-included-in-aem-6522}

[!DNL Experience Manager] 6.5.22.0 innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat samt felkorrigeringar. Det innehåller även förbättringar av prestanda, stabilitet och säkerhet som släppts sedan den första tillgängligheten av 6.5 i april 2019. [Installera detta Service Pack](#install) på [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## Viktiga funktioner och förbättringar

### Sites {#sites}

[Den universella redigeraren](/help/sites-developing/universal-editor/introduction.md) finns nu i AEM 6.5 för headless-användning.


### [!DNL Forms]

Några av de viktigaste funktionerna och förbättringarna i den här versionen är följande:


<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Åtgärdade problem i Service Pack 22 {#fixed-issues}


### [!DNL Sites]{#sites-6522}


#### Tillgänglighet {#sites-accessibility-6522}

* Det saknades ett hjälpmedelsnamn för knappen för val av anteckningsfärgruta. Det vill säga att det inte finns något namn på knappen som kan tolkas av användaren när ett nytt hexvärde har angetts. (SITES-11992) MAJOR
* Följande element på menyn för den vänstra listen visas som en lista men markeras inte som sådana i skärmläsaren:

   * Plats
   * Live copy
   * Starta
   * Språkkopia
   * Mapp
   * CSV-rapport (SITES-2874)

* AEM Core Web Content Management kräver en hjälpmedelsetikett för hyperlänkar i RTF-redigeraren. När en hyperlänk används i textkomponenten bör ankartaggen innehålla attributet `aria-label` för att säkerställa att skärmläsare kan läsa och förmedla länktexten korrekt i hjälpmedelssyfte. (SITES-11511)
* I AEM har de interaktiva elementen i tabellrubriken i listvyn inte den knapproll som krävs. Skärmläsaren NVDA meddelar därför inte de förväntade knapprollerna för följande tabellrubriker: Rubrik, Namn, Ändrad, Publicerad, Förhandsgranska, Mall, Åtgärd, Arbetsflöde. Varje interaktivt element i tabellhuvudet ska tilldelas en&quot;knapproll&quot; för att säkerställa kompatibilitet med hjälpmedelstekniker som NVDA. (SITES-10962)


#### Administratörsgränssnitt{#sites-adminui-6522}

* I vissa fall av AEM fungerade inte funktionerna för förhandsgranskning och jämförelse som förväntat på flera sidor. Mer specifikt:

   * **Förhandsgranskningsproblem:** Ett fel visas från början när du försöker förhandsgranska en sidversion. När du har försökt igen blir förhandsgranskningen en tom sida.
   * **Versionsjämförelseproblem:** Funktionen Jämför med aktuell visade bara den aktuella versionen, utan att markera några skillnader mellan versionerna. (SITES-23988) MAJOR

* En oväntad `<br>`-tagg visas i RTE-fältet (Rich Text Editor) när `defaultPasteMode` inställd på `plaintext` används under en kopiera- och klistra in-åtgärd. Det här problemet resulterar i olika markeringar för samma innehåll, vilket resulterar i att samma textinnehåll översätts två gånger i kundens översättningsminne. (SITES-23606) MAJOR
* I AEM 6.5.20.0 påträffades ett funktionsfel med funktionen **Hantera publikation**. När du väljer en nod och schemalägger den för framtida publicering kan ett felmeddelande,&quot;Det gick inte att hämta underordnade resurser för valda objekt&quot;, visas när underordnade noder ska inkluderas. Det här problemet blockerade användningen av alternativet **Inkludera underordnade**, vilket förhindrar att den avsedda innehållshierarkin publiceras fullständigt. (SITES-23000) MAJOR
* En malls&quot;publicerade&quot; tidsstämpel uppdaterades inte i författarmiljön, även om mallen replikerades till publiceringsinstanserna. Det förväntade beteendet var att tidsstämpeln på författarinstansen skulle återspegla den senaste publikationen, men den här uppdateringen gjordes inte som förväntat. (SITES-21585) MAJOR
* Antalet inkommande länkar i AEM författarmiljö var inte korrekt. Den vänstra listen visade färre länkar jämfört med det klassiska användargränssnittet. Vissa inkommande länkar som var berättigade fungerar inte heller. (SITES-24837)
* Extremt långa inläsningstider rapporterades när sidversionerna visades i tidslinjevyn i AEM. Det tog upp till 19 minuter att visa versioner. Detta problem pågick sedan uppgraderingen från AEM 6.4.8 till 6.5.18, vilket avsevärt stör arbetsflödets effektivitet. (SITES-22468 &amp; SITES-22467)

<!-- #### Classic UI{#sites-classicui-6522} 

* A -->


#### [!DNL Content Fragments]{#sites-contentfragments-6522}

* Om du sparar innehållsfragment i den uppgraderade AEM 6.5.17 uppstod följande fel: *FEL: Det gick inte att spara innehållsfragment.* (SITES-22993) CRITICAL
* Ett problem identifierades med en icke stängd resurslösare i `ContentFragmentModelOmniSearchHandler` på utgivaren i AEM. (SITES-24903)


#### [!DNL Content Fragments] - Admin{#sites-admin-6522}

* Om du klickar på länken i e-postmeddelandet dirigeras användaren till standardresursläsaren eller -redigeraren. Det gör det i stället för innehållsfragmentsredigeraren, även när resursen i arbetsflödet bedöms vara ett innehållsfragment. (SITES-24338) MAJOR


#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6522}

* När du använder innehållsfragment med flerradiga textfältsobjekt, bibehölls inte formateringen som angavs i HTML i den kod som genererades när du frågade med GraphQL. En ny rad saknades till exempel efter listan. Följden blev att det sista stycket blev en del av listan. (SITES-23233)


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6522}

* A


#### [!DNL Content Fragments] - REST API{#sites-restapi-6522}

* A -->

#### Core Backend{#sites-core-backend-6522}

* Återkommande `SegmentNotFoundException` fel rapporterades för en AEM författarinstans. Problemet löstes tillfälligt när författaren startades om, men en långsiktig korrigering krävdes för att förhindra ytterligare händelser. (SITES-22573)
* Ett problem uppstod med tidslinjefunktionen i AEM Sites, särskilt när `cq:lastModified`-egenskaper hanterades i anteckningar. Efter att AEM 6.5.20 tillämpats var det osäkert om befintligt innehåll behövde åtgärdas för den saknade egenskapen eller om tidslinjen uppdaterades för att fungera korrekt utan den. (SITES-21861)


#### Kärnkomponenter{#sites-core-components-6522}

* Efter en uppgradering från AEM 6.5.18 till 6.5.21 identifierades ett problem med funktionen som kontrollerar komponenternas användning i realtid. När du försökte bläddra efter ytterligare objekt på sidan Live-användning kunde tabellen inte läsa in fler resultat trots att&quot;Läsa in fler objekt&quot; visades i användargränssnittet. (SITES-23919)
* Ett problem rapporterades med valideringen av obligatoriska fält i en dialogruta för AEM som innehåller två flikar. Fliken 1 innehöll en textredigerare (RTE) och textfält, medan Flik 2 hade sökvägsfält och textfält. Även om alla fält har markerats som obligatoriska (`required=true`) kvarstår felmeddelanden felaktigt i flik 1, även efter att alla obligatoriska fält har fyllts i. Fel i tabb 2 rensas däremot som förväntat. (SITES-23243)
* Efter migrering till AEM 6.5.21 fungerar inte längre programsatsen `data-sly-include` för HTML-mallspråk som förväntat, vilket innebär att `appendPath`- och `prependPath`-uttryck inte stöds. Resultatet blev att den inkluderade resursens utdata inte renderades korrekt, även om den fungerade korrekt före migreringen. Det här problemet orsakade återgivningsfel för resurser som är beroende av dessa uttryck för sökvägsändring. (GRANITE-52970)


<!-- #### Campaign integration{#sites-campaign-integration-6522}

* A -->


#### Upplevelsefragment{#sites-experiencefragments-6522}

* Experience Fragments sorterar inte efter rubrik som förväntat när du klickar på kolumnrubriken **Title** i listvyn. En snabb flimmer av skärmen visas, men den sorteras inte. (SITES-23706) MAJOR

* I AEM 6.5.17 påträffades ett fel när en sidkomponent konverterades till ett Experience Fragment med hjälp av funktionen som inte finns i kartongen. Efter konverteringen verkade Experience Fragment tomt under redigeringen, trots att det visades korrekt på sidan där det användes. Problemet uppstod när en felaktig nod skapades: komponentnoden placerades utanför rot-/behållarnoden, vilket bröt mot mallens struktur. Du måste flytta komponentnoden manuellt till rätt rot-/behållarnod för att kunna återställa fragmentets redigerbarhet. (SITES-22974) MAJOR

* Efter migrering från AEM 6.5.11 till 6.5.20 sparades inte molnkonfigurationer på Experience Fragments korrekt. Även om konfigurationerna verkade ha sparats i `crx/de`, visas de inte när konfigurationskonsolen öppnas igen, vilket tyder på ett problem med beständighet. (SITES-2287) MAJOR


<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6522}

* A -->


#### Launches{#sites-launches-6522}

* När användaren lägger till Experience Fragment-resurser med taggningsfiltret i AEM kan han/hon markera det, men ett fel uppstod när **Skapa språkkopia** valdes. Det förväntade beteendet var att Experience Fragment-resursen som valdes från taggningsfiltret skulle läggas till i översättningsprojektet. (SITES-24152) MAJOR

#### Länkkontroll{#sites-link-checker-6522}

* LinkCheckerTask kan inte autentiseras eftersom HTTP-klienten försöker med NTLM före grundläggande autentisering, vilket gör att proxyn blockerar användare efter flera misslyckade försök. Systemet bör i stället använda grundläggande autentisering för att autentisera mot proxyn, så att LinkCheckerTask-tjänsterna fungerar korrekt. (SITES-25034) MAJOR


#### MSM - Live-kopior{#sites-msm-live-copies-6522}

* När SEO Robots-taggar används på den primära kopian och distribueras till Live Copy-sidor, visades värdena korrekt i `crx/de`. Värdena speglades emellertid inte i användargränssnittet under Sidegenskaper på Live Copy-sidorna. (SITES-23475) MAJOR
* Fel som rör startprogram uppstod när ett försök gjordes att befordra en startsida via användargränssnittet. Guiden för att starta upp kampanjen förblev tom, vilket förhindrar att kampanjprocessen slutförs. (SITES-19718)
* Problem uppstod med Experience Fragments i AEM efter försök att skapa Live-kopior och utföra rollouts. Problemet uppstod när användare påträffade ett `NotFound`-fel när de försökte navigera tillbaka till hanteringsskärmen för Experience Fragments från utrullningsskärmen. (SITES-21933)


#### Page Editor{#sites-pageeditor-6522}

* Knappen Ångra ändrade komponentens position förutom att ändra texten till den senaste versionen. (SITES-17465) BLOCKER
* När en kopierad behållarkomponent klistrades in visuellt visuellt två gånger, vilket resulterar i tre instanser på sidan. När sidan har uppdaterats försvann dock dubbletten, vilket tyder på att problemet troligen var ett tillfälligt visuellt fel. (SITES-21890) MAJOR
* När du navigerade i den vänstra rutan Komponenter med tangenterna Tabb eller Skift+Tabb på tangentbordet var flera textelement inte tydliga, både visuellt och i tabbläge. Det här problemet påverkade tillgängligheten, vilket gjorde det svårt att identifiera eller interagera med dessa komponenter under tangentbordsnavigeringen. (SITES-2266)

#### Replikering{#sites-replication-6522}

* I AEM 6.5.18 och 6.5.19 genererades flera inaktiveringsbegäranden för varje underordnad sida när en överordnad sida inaktiverades. Detta gjorde också att huvuddelen av GraphQL-slutpunkterna inte kunde publiceras. (NPR-42075 &amp; NPR42010) CRITICAL


### [!DNL Assets]{#assets-6522}

* När du använder funktionen för uppkopplade Assets återspeglas inte uppdateringarna i AEM Assets i AEM Sites-miljön. (ASSETS-42344) MAJOR <!-- Leave the "MAJOR" status priorities in place. -->
* (ASSETS-41158) MAJOR
* Om du överför resurser med API visas ett felmeddelande om `unclosed resource resolver`. (ASSETS-41049) MAJOR
* (ASSETS-40384) MAJOR
* I AEM version 6.5.19 avmarkeras även alla andra tillgängliga kryssrutor när du tar bort ett alternativ från sökpanelsresultaten. (ASSETS-37335) MAJOR
* Skräppostvärden visas i Excel-utdata när gruppmetadataexporten utförs. (ASSETS-37260) MAJOR
* I AEM version 6.5.19 blir utdata oskarpa när du överför en SVG-fil i UTF-8-format. (ASSETS-36616) MAJOR
* Alternativet `Fetch original rendition for Dynamic Media Connected Assets` saknas i den anslutna Assets-konfigurationen. (ASSETS-41726)
* Resursegenskaper sparas även om du inte definierar ett värde för obligatoriska fält. (ASSETS-37914)

#### [!DNL Dynamic Media]{#assets-dm-6522}

* Ett produktionsproblem avbröt migreringsprocessen när en videoöverföring till Dynamic Media misslyckades och ett processfel i användargränssnittet visades. (ASSETS-36038)


### [!DNL Forms]{#forms-65220}

Korrigeringar i [!DNL Experience Manager] Forms levereras via ett separat tilläggspaket en vecka efter den schemalagda versionen av [!DNL Experience Manager] Service Pack. I det här fallet planeras AEM 6.5.22.0 Forms-tilläggspaketet för torsdagen den 28 november 2024. En lista över Forms-korrigeringar och förbättringar har lagts till i det här avsnittet när utgåvan släppts.


<!-- #### [!DNL Adaptive Forms] {#forms-6522}

* A


#### [!DNL Forms Designer] {#forms-designer-6522}

* A -->


### Foundation {#foundation-6522}

* Ett fel uppstod i AEM Assets Console när DITA-dokument skulle sorteras om. Det synliga spåret högst upp i dialogrutan för sökvägsläsaren visar felaktigt nodnamnet i stället för nodrubriken för rotens överordnade nod. Korrekt nodtitel visas bara när du har markerat ett objekt i den synliga sökvägen, vilket anger ett tillfälligt visningsfel. (NPR-42106) MAJOR


<!-- #### Apache Felix {#foundation-apachefelix-6522}


* A

#### Campaign{#foundation-campaign-6522}

* A


#### Cloud Services{#foundation-cloudservices-6522}

* A -->


#### Communities {#foundation-communities-6522}

* Efter uppgradering från AEM 6.5.19 till 6.5.20 uppstod ett fel där `Connection evic` trådar inte kunde stängas korrekt efter anrop till `UgcSearch`. Detta problem, som observerats i produktionsmiljön, gör att dessa trådar kvarstår och ackumuleras över tid, vilket kan påverka prestandan. (NPR-42019) MAJOR


<!-- #### Content distribution{#foundation-content-distribution-6522}

* A -->


#### CRX {#foundation-crx-6522}

* Sorteringen fungerade inte enligt **grupper** på den vänstra menyn i CRX Package Manager. (GRANITE-53277)
* Pakethanteraren i AEM begränsar installationen av lägre paketversioner som standard, men tillåter att äldre versioner installeras med tvång. Om du använder kraftinstallationsalternativet kan det dock störa framtida installationer genom standardförloppet. Om till exempel version 1.21 installeras och version 1.24 läggs till, slutförs installationen och båda versionerna listas. Det går emellertid inte att installera version 1.22 över 1.24 i pipeline, men det fungerar om versionen är installerad med tvång, så att alla versioner listas. På samma sätt blockeras installation av version 1.23 om version 1.24 redan finns, eftersom pipeline inte tillåter nedgraderingar. GRANITE-53263


#### Granit{#foundation-granite-6522}

* Fixeringspaket installerades i AEM med CURL-kommandon. Under installationen skannade JCR-installationsprogrammet paketen med OSGI Installer för att säkerställa att inga ytterligare OSGI-paket eller konfigurationer krävs. Om en paketversion innehöll &quot;SNAPSHOT&quot; utlöste OSGI-installationsprogrammet VLT för att skapa ett motsvarande ögonblickspaket. Eftersom varje AEM författarinstans kör sitt eget OSGI Installer kan båda instanserna försöka generera ögonblicksbilden samtidigt, vilket leder till sessionskonflikter i databasen. (NPR-42003) MAJOR
* Det fanns en låskonflikt i `ScriptDependencyResolver` med AEM 6.5.21. (GRANITE-53181) MAJOR
* Efter uppgradering av AEM till 6.5.21 uppstod problem när relativa sökvägar användes i syntaxen Sjust (HTL), till exempel `data-sly-use`. (GRANITE-53080) MAJOR


#### Integreringar{#foundation-integrations-6522}

* Lagt till behörighetsförklaring för Cloud Servicens användargränssnitt. (FORMS-16373)
* Läsbehörighet har lagts till för användaren **fd-cloudService** som kan komma åt hCaptcha- och Turnstile-konfigurationer, vilket gör att klienten kan hämta klient-ID och klienthemlighet som krävs för captcha-återgivning och validering. Dessutom implementerades en åtkomstkontrollistmodell för att hantera åtkomsten till dessa konfigurationer. (FORMS-16360)


#### Lokalisering{#foundation-localization-6522}

* I ![Hammer-ikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) Verktyg > **Säkerhet** > ![Användarikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_User_18_N.svg) **Användare** på sidan Användarhantering visades data i kolumnen **Status** i tabellen lodrätt. GRANITE-48304


<!-- #### Oak {#foundation-oak-6522}

* A -->


#### Plattform{#foundation-platform-6522}

* Den spårning av företagsinformationshantering som introducerades i AEM 6.5.18 orsakade avvikelser i beräkningen av poängen för produktanvändning. Adobe Metrics-biblioteket orsakade detta problem genom att skriva över användardata från Omega-spårningsbiblioteket. Därför sjönk antalet användare för många av AEM Sites- och AEM Assets-kunderna till noll från och med februari 2024. (CQ-4358438) CRITICAL
* Ett kritiskt problem har identifierats i produktionsmiljön där skräpinsamlaren felaktigt hanterade taggar. När en tagg flyttades eller fick ett nytt namn kunde inte skräpinsamlaren uppdatera egenskapen `cq:MovedTo`, vilket gjorde att taggen försvann från sidorna. (CQ-4358293) MAJOR
* Ett problem med ContextHub i AEM 6.5.19 orsakade att segment inte löstes korrekt när en kontextsökväg lades till i en AEM. Problemet påverkade specifikt URL-fältet i JavaScript-objekten som genererades av sidkomponenten, där det nödvändiga kontextsökvägsprefixet saknades. Detta förhindrade att segment fungerade som förväntat. (SITES-21852)
* AEM QuickStart har uppdaterats för att använda biblioteket `commons-collections-3.2.2-adobe-2`. Uppdateringen ser till att programmet kan fortsätta att köras utan problem. (NPR-42150)
* SMTP OAuth2-konfigurationen i AEM 6.5 skiljer sig avsevärt från vad som används i AEM as a Cloud Service. För att effektivisera konfigurationen och säkerställa enhetlighet måste konfigurationen i AEM 6.5 anpassas till de standarder som används i AEM as a Cloud Service. (GRANITE-53273)
* Ett fel uppstod när du klickade på ikonen ![Komprimera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Compass_18_N.svg) > ![Projektikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Project_18_N.svg) Projekt och sedan placerade muspekaren över ikonen ![Rail till vänster](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RailLeft_18_N.svg) ![Sparron nedåt](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) , som visas framför verktygstipstexten&quot;Endast innehåll&quot;. (CQ-4356633)

#### Dokumentskydd{#foundation-security-6522}

* Problem uppstod med ett inaktuellt JSAFE-kryptografiskt bibliotek (version 6.0.0) i AEM. Ett patchat paket med JSAFE version 6.2.5 ingår i AEM 6.5.22. (NPR-42006) CRITICAL
* Vid validering av tillåtna protokoll vid XSS-kontroller jämförs hanterare med&quot;http&quot; och&quot;https&quot;. Egenskapen `protocol` för ett URL-objekt returnerade emellertid dessa värden med ett efterföljande kolon, till exempel `http:` och `https:`. Felmatchningen orsakade valideringsproblem. För att säkerställa korrekt parsning krävs en protokollkontroll för att ta hänsyn till kolonet eller för att justera jämförelselogiken i enlighet med detta.  (NPR-42119)
* Efter installation av AEM 6.5.21 (föregående version var AEM 6.5.19) på IBM® WebSphere® Liberty Profile och Semeru Java 8.0 gick det inte att öppna några sidor. Felloggarna indikerade problem relaterade till serverversioner som olika paket kräver. För att åtgärda det här problemet måste beroendet av `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar` återställas eftersom det var relaterat till problemet. (NPR-42116)
* Flera webbläsare håller på att fasa ut stödet för **SameSite=None**-cookies, som används för att tillåta åtkomst till cookies mellan webbplatser. Som ett alternativ introduceras **partitionerade cookies**. Dessa cookies isolerar lagring efter i vilket sammanhang de används, vilket förbättrar sekretess och säkerhet genom att förhindra spårning mellan webbplatser samtidigt som cookies fortfarande fungerar inom specifika partitioner, till exempel inbäddat innehåll från tredje part. GRANITE-51953


<!-- #### Sling{#foundation-sling-6522}

* A -->


#### Översättning{#foundation-translation-6522}

* Stöd för de senaste ändringarna i kärnkomponenter har lagts till i standardöversättningsreglerna. (NPR-42029) CRITICAL
* Ett problem uppstod vid export av XLIFF-filer i AEM Forms. När du använder alternativet **Exportera markering som XLIFF (endast strängar)** bibehölls inte komponentsekvensen konsekvent. Däremot förblir sekvensen korrekt när du exporterar XLIFF för ett visst språk. Två filer tillhandahölls för att demonstrera problemet: **DE-CH_Export.xliff** (korrekt sekvens) och **String_Export.xliff** (felaktig sekvens). (NPR-42118) MAJOR


#### Användargränssnitt{#foundation-ui-6522}

* `coralui-component-dialog` ändrade placeringen av `cq-dialog-actions`, vilket eventuellt kunde påverka layout eller beteende för åtgärdsknappar i dialogrutor i AEM. (NPR-42294) BLOCKER
* Färgväljarfunktionen i AEM fungerade inte som den ska. När den används visas en tom modal bild, vilket förhindrar färgmarkering. Problemet uppstod när AEM 6.5.20 installerades i scenmiljön. Färgväljaren fungerade korrekt *före* för uppdateringen. (NPR-42163)
* I ikonen ![Hammer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) **Verktyg** > **Arbetsflöde** > **Modeller** > välj en modell > **Starta arbetsflöde** saknades ikonen Bläddra i fältet Nyttolast i dialogrutan **Kör arbetsflöde** . (NPR-42162)


<!-- #### WCM{#foundation-wcm-6522}

* A


#### Workflow{#foundation-workflow-6522}

* A 


## Install [!DNL Experience Manager] 6.5.22.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.2.0 kräver [!DNL Experience Manager] 6.5. Mer information finns i [ uppgraderingsdokumentationen ](/help/sites-deploying/upgrade.md) . <!-- UPDATE FOR EACH NEW RELEASE -->
* Nedladdningen av Service Pack är tillgänglig på Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip).
* På en distribution med MongoDB och flera instanser installerar du [!DNL Experience Manager] 6.5.22.0 på en av författarinstanserna med hjälp av Package Manager.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe rekommenderar inte att du tar bort eller avinstallerar paketet [!DNL Experience Manager] 6.5.22.0. Därför bör du skapa en säkerhetskopia av `crx-repository` innan du installerar paketet, ifall du måste återställa det. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Installera Service Pack på [!DNL Experience Manager] 6.5{#install-service-pack}

1. Starta om instansen innan installationen om instansen är i uppdateringsläge (när instansen uppdaterades från en tidigare version). Adobe rekommenderar att du startar om om den aktuella upptiden för en instans är hög.

1. Ta en ögonblicksbild eller en ny säkerhetskopia av din [!DNL Experience Manager]-instans innan du installerar.

1. Hämta Service Sack från [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Öppna Pakethanteraren och välj sedan **[!UICONTROL Upload Package]** för att överföra paketet. Mer information finns i [Pakethanteraren](/help/sites-administering/package-manager.md).

1. Markera paketet och välj sedan **[!UICONTROL Install]**.

1. Om du vill uppdatera S3-anslutningen stoppar du instansen efter installationen av Service Pack, byter ut den befintliga kopplingen mot en ny binär fil som finns i installationsmappen och startar om instansen. Se [Amazon S3-datalager](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Dialogrutan i pakethanterarens gränssnitt stängs ibland under installationen av Service Pack. Adobe rekommenderar att du väntar på att felloggarna ska stabiliseras innan du får åtkomst till distributionen. Vänta på de specifika loggarna för avinstallationen av uppdateringspaketet innan du försäkrar dig om att installationen lyckas. Vanligtvis inträffar det här problemet i webbläsaren [!DNL Safari], men kan inträffa i alla webbläsare.

**Automatisk installation**

Det finns två olika metoder att använda för att installera [!DNL Experience Manager] 6.5.22.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Placera paketet i mappen `../crx-quickstart/install` när servern är tillgänglig online. Paketet installeras automatiskt.
* Använd [HTTP-API:t från Package Manager](/help/sites-administering/package-manager.md#package-share). Använd `cmd=install&recursive=true` så att kapslade paket installeras.

>[!NOTE]
>
>Experience Manager 6.5.22.0 stöder inte installation av Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Verifiera installationen**

Information om vilka plattformar som är certifierade för att fungera med den här versionen finns i [tekniska krav](/help/sites-deploying/technical-requirements.md).

1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience Manager (6.5.22.0)` under [!UICONTROL Installed Products]. <!-- UPDATE FOR EACH NEW RELEASE -->

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

UberJar för [!DNL Experience Manager] 6.5.22.0 är tillgängligt i [Maven Central-databasen](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.21/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Om du vill använda UberJar i ett Maven-projekt ska du läsa [Använda UberJar](/help/sites-developing/ht-projects-maven.md) och inkludera följande beroende i projektstrukturen: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.22</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar och andra relaterade artefakter är tillgängliga i Maven Central Repository i stället för i Adobe Public Maven-databasen (`repo.adobe.com`). Huvudfilen för UberJar har bytt namn till `uber-jar-<version>.jar`. Det finns alltså ingen `classifier`, med `apis` som värde, för taggen `dependency`.


## Föråldrade och borttagna funktioner{#removed-deprecated-features}

Se [Inaktuella och borttagna funktioner](/help/release-notes/deprecated-removed-features.md/).

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
   * Den aktiva punkten i en interaktiv Dynamic Media-bild syns inte när du förhandsgranskar mediefilen via visningsprogrammet för den köpbara kanalen.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Timeout uppstod i väntan på att registerändringen skulle slutföras utan registrering.

* Från och med AEM 6.5.15 har den Rhino JavaScript-motor som tillhandahålls av ```org.apache.servicemix.bundles.rhino```-paketet ett nytt värdbeteende. Skript som använder strikt läge (```use strict;```) måste deklarera sina korrekta variabler. Annars körs de inte, vilket resulterar i ett körningsfel.

* Om du installerar taggning av relaterat innehåll som inte finns i kartongen med hjälp av ett officiellt uppdateringspaket återställs språkegenskapen för noden `/content/cq:tags` till standardvärdet. Den här åtgärden gäller för Service Packs, Security Service Pack, Extended Feature Packs, Cumulative Feature Packs, Patches osv. Det är därför nödvändigt att lägga till den från egenskaperna före installationen.

### Känt problem för AEM Sites {#known-issues-aem-sites-6522}

* Content Fragments-Preview misslyckas på grund av DoS-skydd för stora fragmentträd. Se artikeln [KB om standardkonfigurationsalternativ för GraphQL Query Executor](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934)


### Kända fel för AEM Forms {#known-issues-aem-forms-6522}


* När du har installerat AEM Forms JEE Service Pack 21 (6.5.21.0) kan du lösa problemet genom att utföra följande steg om du hittar dubblettposter för Geode jars `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` i mappen `<AEM_Forms_Installation>/lib/caching/lib` (FORMS-14926):

   1. Stoppa positionerarna om de är igång.
   1. Stoppa AEM.
   1. Gå till `<AEM_Forms_Installation>/lib/caching/lib`.
   1. Ta bort alla Geode-korrigeringsfiler utom `geode-*-1.15.1.2.jar`. Bekräfta att det bara finns Geode-burkar med `version 1.15.1.2`.
   1. Öppna kommandotolken i administratörsläge.
   1. Installera Geode-korrigeringen med filen `geode-*-1.15.1.2.jar`.

* Om en användare försöker förhandsgranska ett utkast med sparade XML-data fastnar den i läget `Loading` för vissa specifika bokstäver. Läs artikeln [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) om du vill hämta och installera snabbkorrigeringen. (FORMS-14521)

* När du har uppgraderat till AEM Forms Service Pack 6.5.21.0 kan tjänsten `PaperCapture` inte utföra OCR-åtgärder (Optical Character Recognition) på PDF. Tjänsten genererar inte utdata i form av PDF eller en loggfil. Läs artikeln [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) om du vill hämta och installera snabbkorrigeringen. (CQDOC-21680)

* När användare uppgraderade från AEM 6.5 Forms Service Pack 18 eller 19 till Service Pack 20 eller 21 påträffades ett JSP-kompileringsfel. Det här felet hindrade dem från att öppna eller skapa anpassade formulär. Det orsakade även problem med andra AEM gränssnitt. Gränssnitten innehåller sidredigeraren, AEM Forms-gränssnittet, arbetsflödesredigeraren och användargränssnittet för systemöversikt. (FORMS-1256)

  Om du råkar ut för ett sådant problem följer du de här stegen för att lösa det:
   1. Navigera till katalogen `/libs/fd/aemforms/install/` i CRXDE.
   1. Ta bort paketet med namnet `com.adobe.granite.ui.commons-5.10.26.jar`.
   1. Starta om AEM.

* När du har uppdaterat till AEM Forms Service Pack 20 (6.5.20.0) med Forms Add-On fungerar inte konfigurationer som är beroende av den äldre Adobe Analytics Cloud-tjänsten med autentiseringsbaserad autentisering. Det här problemet förhindrade att analysreglerna kördes korrekt. Läs artikeln [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) om du vill hämta och installera snabbkorrigeringen. (FORMS-15428)

* När en användare uppdaterar till AEM Forms Service Pack 20 (6.5.20.0) på JEE-servern och genererar PDF med hjälp av utdatatjänster återges PDF med tillgänglighetsproblem. Läs artikeln [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) om du vill hämta och installera snabbkorrigeringen. (LC-3922112)
* När en användare genererar taggat PDF med hjälp av utdatatjänsten för JEE visas&quot;Olämplig strukturvarning&quot;. Läs artikeln [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) om du vill hämta och installera snabbkorrigeringen. (LC-3922038)
* När ett formulär skickas i AEM Forms JEE tas instanser av ett upprepat XML-element bort från data. Läs artikeln [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) om du vill hämta och installera snabbkorrigeringen. (LC-3922017)
* När en användare i en Linux®-miljö återger ett adaptivt formulär (på JEE) i HTML återges det inte korrekt. Läs artikeln [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) om du vill hämta och installera snabbkorrigeringen. (LC-3921957)
* När en användare konverterar en XTG-fil till PostScript-format med hjälp av utdatatjänsten i AEM Forms JEE misslyckas den med följande fel: `AEM_OUT_001_003: Unexpected Exception: PAExecute Failure: XFA_RENDER_FAILURE`. Läs artikeln [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) om du vill hämta och installera snabbkorrigeringen. (LC-3921720)
* När en användare har uppgraderat till AEM Forms Service Pack 18 (6.5.18.0) på JEE-servern återges inte HTML5 eller PDF forms och XMLFM-krascher när användaren skickar ett formulär. Läs artikeln [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) om du vill hämta och installera snabbkorrigeringen. (LC-3921718)
* I förhandsgranskningen av gränssnittet för Interactive Communications Agent visas valutasymbolen (till exempel dollartecknet $) inkonsekvent för alla fältvärden. Den visas för värden upp till 999 men saknas för värden över 1 000. (FORMS-1657)
* Eventuella ändringar av det kapslade layoutfragmentets XDP i en interaktiv kommunikation återspeglas inte i IC-redigeraren. (FORMS-16575)
* I förhandsgranskningen av gränssnittet för den interaktiva kommunikationsagenten visas vissa beräknade värden inte korrekt. (FORMS-16603)
* När brevet visas i Förhandsgranska utskrift ändras innehållet. Vissa blanksteg försvinner och vissa bokstäver ersätts med&quot;x&quot; (FORMS-15681)

## OSGi-paket och innehållspaket som ingår{#osgi-bundles-and-content-packages-included}

Följande textdokument innehåller en lista över de OSGi-paket och innehållspaket som ingår i den här versionen av [!DNL Experience Manager] 6.5 Service Pack:

* [Lista över OSGi-paket i Experience Manager 6.5.22.0](/help/release-notes/assets/65210-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista över innehållspaket i Experience Manager 6.5.22.0](/help/release-notes/assets/65210-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Begränsade webbplatser{#restricted-sites}

Dessa webbplatser är bara tillgängliga för kunder. Om du är kund och behöver åtkomst kontaktar du din kontoansvarige på Adobe.

* [Nedladdning av produkt på licensing.adobe.com](https://licensing.adobe.com/)
* [Kontakta Adobe kundsupport](https://experienceleague.adobe.com/en/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] produktsida](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5-dokumentation](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [Prenumerera på produktuppdateringar för Adobe Priority](https://www.adobe.com/subscription/priority-product-update.html)
