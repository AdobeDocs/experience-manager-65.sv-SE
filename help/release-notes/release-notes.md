---
title: Versionsinformation för [!DNL Adobe Experience Manager] 6.5
description: Hitta versionsinformation, nyheter, installationsanvisningar och en detaljerad ändringslista för [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
source-git-commit: a15b9dae5cc4405122ee95e036a83fdfbf34f9bd
workflow-type: tm+mt
source-wordcount: '4470'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] 6.5 Versionsinformation om senaste Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=7yhrWb&nav=MTVfe0U0RjdDQUM3LTZCQ0EtNDk1Qy04Mjc1LTM2MUJEMzE1OEVGN30 -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, June 1, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Versionsinformation {#release-information}

| Produkt | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.18.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Typ | Service Pack-version |
| Datum | Torsdag den 24 augusti 2023 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Hämta URL | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Vad ingår i [!DNL Experience Manager] 6.5.18.0 {#what-is-included-in-aem-6518}

[!DNL Experience Manager] 6.5.18.0 innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat, felkorrigeringar, prestanda, stabilitet och säkerhetsförbättringar som har släppts sedan den första tillgängligheten av 6.5 i april 2019. [Installera detta Service Pack](#install) på [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Några av de viktigaste funktionerna och förbättringarna i den här versionen är följande:

**Viktiga funktioner**

* Assets, Dynamic Media - [Stöd för flera undertexter och flerljudspår för videor i Dynamic Media](/help/assets/video.md#about-msma)—Nu kan du enkelt lägga till flera undertexter och flera ljudspår i en primär video. Detta innebär att videoklippen är tillgängliga för alla mottagare världen över. Du kan anpassa en enda publicerad primär video till en global publik på flera språk och följa riktlinjer för tillgänglighet för olika geografiska regioner. Författare kan också hantera undertexter och ljudspår från en enda flik i användargränssnittet.

* Resurser - Från sökresultat kan du nu navigera till den mapplats som innehåller en resurs, vilket gör att du kan utföra olika resurshanteringsåtgärder. (ASSETS-23182)

**Viktiga förbättringar**

* Sites Polaris Picker i Content Fragments har förbättrat prestandan. (SITES-14092)

* Användare av sidredigeraren/bildkomponenten har aktiverat platser för att referera till resurser från Cloud Servicen Fjärrresurser. (SITES-13448, SITES-13433)

* För att snabbt hitta ett projekt i listvyn där du kan ha många projekt i systemet har Adobe nu stöd för sortering på serversidan. Projektnoder sorteras på serverdelen baserat på den kolumn som valts av användaren innan de återges i användargränssnittet. (NPR-41027)

* AEM 6.5.18.0 stöder MongoDB 5.0 till 6.0.

**Inaktuell funktion**

* ActiveMQ i AEM är föråldrat. ActiveMQ användes för kommunikation mellan två AEM publiceringsinstanser. Adobe rekommenderar att man nu använder en belastningsutjämnare.

**Forms**

* **[Förbättrad felhantering med anpassade felhanterare i regelredigeraren](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms.html):** Du kan nu anropa en anpassad funktion (med Klientbibliotek) som svar på ett fel som returnerats av en extern tjänst och ge ett skräddarsytt svar till slutanvändarna. Du kan också vidta specifika åtgärder för fel som returneras av en tjänst. Du kan till exempel anropa ett anpassat arbetsflöde i serverdelen för specifika felkoder eller informera kunden om att tjänsten är nere

* **[Förbättrat arbetsflöde i Adobe Sign](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html#sign-document-step):** Adobe Sign arbetsflödessteg i AEM arbetsflöden är tillgängligt med följande förbättringar.

   * **Förbättrad säkerhet med ID-baserad autentisering för Adobe Sign för myndigheter:** Adobe Acrobat Sign Government ID-Based Authentication erbjuder ytterligare ett verifieringslager genom att användarna kan autentisera sin identitet med hjälp av foto-ID:n (körkort, nationellt ID, pass). Genom att använda pålitliga identifieringsdokument ger den här förbättringen ytterligare tillförlitlighet i signeringsprocessen, vilket gör den idealisk för scenarier som kräver högre säkerhet, regelefterlevnad och användarvalidering.

   * **Förbättrad transparens med granskningsspår för Adobe Sign-dokument:** Använd funktionen Granskningsspår för att få detaljerade insikter om livscykeln för dina Adobe Sign-dokument. Med granskningsspåret kan du nu föra ett omfattande register över alla åtgärder och interaktioner som rör dina dokument. Detta inkluderar information som vem som visade, redigerade eller signerade dokumentet, tillsammans med tidsstämplar för varje händelse. Den här förbättringen är avgörande för att upprätthålla regelefterlevnaden, lösa tvister och säkerställa integriteten för dina digitala avtal.


   * **Utökade roller för avtalsmottagare utöver bara signeraren:** Adobe Acrobat Sign har möjlighet att utöka rollerna för avtalsmottagare utöver bara signeraren för att bättre matcha deras arbetsflödeskrav. När det här alternativet är aktiverat kan varje mottagare i ett avtal konfigureras individuellt, med signerare som standard.


* **[AEM Forms på JEE, komplett installationsprogram](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms.html)**: Service Pack innehåller ett komplett installationsprogram för AEM Forms i JEE som har stöd för flera nya programkombinationer, bland annat:
   * Microsoft® Windows Server 2022
   * Microsoft® Active Directory 2022
   * Oracle WebLogic 14C på Windows Server 2022
   * Red Hat® JBoss® 7.4.10
   * MongoDB 4.4
   * MySQL JDBC Connector 8

Om du håller på med en ny installation eller planerar att använda den senaste programvaran för din AEM 6.5 Forms i JEE-miljö rekommenderar Adobe att du använder AEM 6.5.18.0 Forms i JEE-fullversionen. En fullständig lista över nyligen tillagda och ersatta program finns i dokumentationen för AEM Forms on JEE eller AEM Forms on OSGi.

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Åtgärdade problem i Service Pack 18 {#fixed-issues}

### [!DNL Sites]{#sites-6518}

* Använde gruppredigeraren för att uppdatera egenskaperna för flera sidor genom att hämta `tsv` Exportera, gjorde ändringar offline och överförde sedan `tsv` tillbaka till Experience Manager. JCR-egenskapen uppdaterades trots att sidorna uppdaterades `cq:lastModified` uppdaterades inte och i tidslinjen. (SITES-14072)
* Länkreferensen uppdateras inte i ett Experience Fragment när en live-kopia eller utrullning av ett Experience Fragment skapas. (SITES-14759)
* En arbetsflödessynkroniseringsåtgärd lades till i den körklara standardkonfigurationen för Experience Manager,&quot;utrullningssidan och undersidorna&quot;, från den överordnade sidan, och det asynkrona jobbet misslyckas med ett NullPointer-undantag. Källplatssidan (en-us) finns inte i det överordnade objektet, men finns på målplatsen (Live-kopia) (en). (SITES-12207)
* Du har en-sida som innehåller `jcr:description` och skickade sidan för översättning. The `jcr:description` översätts och egenskapen finns under start. Men när lanseringen befordras `jcr:description` uppdateras inte på sidan. (SITES-13146)
* Lokaliserat innehåll i Live Copy förloras efter utrullning av utkast. (SITES-12602)

#### Administratörsgränssnitt{#sites-adminui-6518}

* Om en användares borttagningsbehörighet tas bort via användaradministratörskonsolen, visas inte längre knappen Egenskaper i konsolen sites.html (när du markerar sidan). Det här alternativet är dock tillgängligt om användaren öppnar sidredigeraren. (SITES-14341)
* När en mapp har många sidor, där var och en har många versioner, blir inläsningen av instansen hög när du använder funktionen för att jämföra version. När flera användare använder funktionen samtidigt kan instansen gå ned. (SITES-13026)

#### [!DNL Content Fragments]{#sites-contentfragments-6518}

* Ett problem upptäcktes med undantagshanteringen i `RemoteAssetClientImpl`. När ett IOException eller RuntimeException inträffar när metadata efterfrågas försöker den aktuella tråden stänga och återskapa den delade httpClient, vilket kan resultera i en överlappning av andra fel i trådarna. (SITES-14092)
* När författare fyller i RTF-redigeringsfältet i ett innehållsfragment och infogar en bild i en länk, när innehållsfragmentet efterfrågas via GraphQL API, felmeddelandet `Exception while fetching data (/genericContentByPath) : null` returneras. Det här felet uppstod bara om det fanns en länk till en bild i den. Felmeddelandet försvinner när du tar bort bilden från länken. (SITES-13988)
* GraphQL implementering av Experience Manager 6.5 var inte i linje med huvudfunktionerna och flera viktiga korrigeringar saknades. (SITES-13096)
* En obligatorisk HTTP-rubrik krävs vid åtkomst till metadatatjänstens slutpunkt. (SITES-13068)

#### Kärnkomponenter{#sites-core-components-6518}

* Resursväljaren hämtar inte en uppdaterad lista över resurser när den stängs och öppnas igen. Om nya resurser överförs i databasen visas de inte i resursväljaren förrän sidan med resursväljaren uppdateras. (SITES-14828)
* Användargränssnittet för resursväljaren, som är integrerat i Sites Editor (CS), svarar inte när fönstret minskas. (SITES-14127)
* Integreringen av Adobe IMS (Identity Management System) Configuration för resursväljaren accepterade felaktiga värden. (SITES-13962)
* När resursväljaren är integrerad i Sites Image-komponenten bör det inte vara möjligt att välja resurser som inte är bilder. (SITES-13879)
* När inloggningen är klar omdirigeras användaren till sidredigeraren. Användaren måste öppna resursväljaren igen för att kunna välja Fjärrresurser. (SITES-13851)
* Väljaren för fjärrresurser dirigerar alltid om till scenmiljön för Adobe IMS (Identity Management System). (SITES-13448, SITES-13433)

<!-- #### [!DNL Experience Fragments]{#sites-experiencefragments-6518}

* A -->

#### Page Editor{#sites-pageeditor-6518}

* När författaren öppnar sidegenskaperna visas en felaktig vy i dialogrutan. Det innebär att en extra vågrät rullningslist och ytterligare marginaler visas. (SITES-14502)
* Format som lagts till i Experience Manager 6.5, Service Pack 17, för ankar- och body-taggar orsakade CSS-problem. Ankarmärkord visades inte under Författare. (SITES-14261)

### [!DNL Assets]{#assets-6518}

* Skärmläsaren meddelar inte om skärmläsaren har expanderat eller komprimerat [!UICONTROL Start Crop] när du redigerar en resurs. (NPR-40593)
* Experience Manager visar fel- och varningsmeddelanden när en resurs laddas upp i AEM 6.5.17.0. (ASSETS-26232)
* När du relaterar en resurs från en mapp med fullständig åtkomst till en resurs från en mapp med skrivskyddad åtkomst, visas ett felmeddelande i Experience Manager, men en partiell relation skapas mellan de två resurserna. (ASSETS-25832)
* Anslutna resurser fungerar inte mellan en AMS-instans och en Cloud Service-instans. (ASSETS-24930)
* När du redigerar Forms för metadataschemat är värdena för [!UICONTROL On time] och [!UICONTROL Off time] fält sparas inte korrekt. (ASSETS-24871)
* När rapporten med smarta taggar genereras för de utbildade taggarna visas inte taggar med låg konfidensgrad. (ASSETS-24109)
* Experience Manager visar en tom skärm när en bild redigeras och kommenteras i kolumnvyn. (ASSETS-24108)
* Skärmläsare meddelar inte syftet med fältet Lägg till användare när en samling skapas. (ASSETS-21736)
* The **Samlingar** etiketten är inte lokaliserad på egenskapssidan för samlingar. (ASSETS-21102)
* När du lägger till en regel eller redigerar en befintlig regel med standardformuläret för metadatamodell, översätts inte språken i listrutan. (ASSETS-21026)
* Experience Manager visar ett olokaliserat felmeddelande när en JSON-sökväg läggs till i metadataschemat. (ASSETS-21025)
* Alternativet för tidslinje till vänster i navigeringen visar inte rätt kontrastförhållande. (ASSETS-17348)
* Kalenderelementen använder inte de ARIA-attribut som krävs. (ASSETS-17282)
* Den vänstra navigeringstexten visar inte rätt kontrastförhållande. (ASSETS-17268)
* Ljuslådebilden är inte dold för skärmläsaranvändare. (ASSETS-17263, ASSETS-17242)
* Tillståndet för ett aktivt användargränssnitt ger inte ett lämpligt kontrastförhållande för bakgrunden. (ASSETS-17260)
* När du kommenterar en resurs känner skärmläsaren inte igen [!UICONTROL Save as version] eller [!UICONTROL Start workflow] knappar när du navigerar dem med piltangenterna på tangentbordet. (ASSETS-17253)
* Vissa ARIA-roller innehåller inte lämpliga underordnade roller på Assets-startsidan. (ASSETS-17248)
* När du navigerar till redigeringsalternativen för en resurs av bildtyp med hjälp av tangentbordet visas [!UICONTROL Launch Map] kan inte identifieras och tangentbordsfokus går till knappen Avbryt i stället. (ASSETS-17238)

#### [!DNL Dynamic Media]{#assets-dm-6518}

* När VTT inte kan hämtas är videon inte synlig. En tom skärm visas medan videobuggen visas framåt. (ASSETS-21909)
* Fokus flyttas inte till flera kontroller som finns under videon när du navigerar med Tabb på tangentbordet. De är därför inte tillgängliga. Förbättrad tangentbordsnavigering för interaktiva videor. (ASSETS-25749)
* Korrigerade inaktiverade visningsprogramförinställningar som visas i Dynamic Media-komponenten. (ASSETS-22922)
* Borttagen &quot;Image Serving&quot; från fliken General Settings Security. (ASSETS-24618)
* Anläggningstillgångar som inte kan överföras till Dynamic Media och StringIndexOutOfBoundsException. (ASSETS-25787)
* En visuell asterisk har lagts till för det obligatoriska breddredigeringsfältet på fliken Grundläggande. (ASSETS-25741)
* Korrigerad hämtning av Watermark Dynamic Media Rendition. (ASSETS-26173)
* 127 tecken för resursnamn som inte är videoresurser har återställts. (ASSETS-26074)

### [!DNL Forms]{#forms-6518}

<!-- Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.18.0 Forms add-on packages release is scheduled for Thursday, August 31, 2023. A list of Forms fixes and enhancements would be added to this section post the release. -->

* **Dokumenttjänster**
   * När en användare använder en transformPDF-tjänst misslyckas den med ett undantag: `java.lang.ClassNotFoundException: default task-158Class name com.adobe.internal.afml.AFMLExceptionInvalidParameter from package com.adobe.internal.afml` (FORMS-9957)
   * Om servern stängs av under dokumentgenereringen i PDF genereras fel vid bearbetning av jobb efter serverstart. Argumentet -Dcom.adobe.livecycle.dsc.deferServiceStart=true måste läggas till när servern startas. (FORMS-9836)
   * Om en användare försöker sammanfoga PDF med metoden AssemblerService.Invoke, kan inte sammansättaren utföra åtgärden. (FORMS-9550)
   * När du uppgraderar till AEM 6.5.15.0 Service Pack i OSGI- och JEE-miljöer slutar Assembler-tjänsten som använder en viss mall att fungera. (FORMS-9355, FORMS-9445, FORMS-9408)
   * Java™-skräpinsamlingen kan inte rensa gammal heap på en AEM Forms OSGi-server eftersom Global Timeout för XMLFormService inte har konfigurerats till ett korrekt värde. (FORMS-9384, FORMS-9035)
   * När du återger förhandsgranskningen av ett adaptivt formulär i PDF visas de oönskade Java™-stackdumparna i felloggarna. (FORMS-8865)
   * När en användare granskar dokumentstatus för dokument i dokumentinformationsavsnittet visas det inte korrekt. (FORMS-8946, FORMS-10424)
   * När en användare uppgraderar till AEM Forms och använder tjänsten sendToPrinter ökar heap-användningen kontinuerligt. (FORMS-10148)
   * På JBoss® 7.4 EAP-servern misslyckas e-postfunktionen med `java.io.IOException`. (FORMS-10138)
   * När en användare använder tjänsten transformPDF misslyckas den med ett fel: `java.lang.ClassNotFoundException: default task-158Class name com.adobe.internal.afml.AFMLExceptionInvalidParameter from package com.adobe.internal.afml`(FORMS-9957)
   * Efter uppgradering till AEM Service Pack 6.5.14.0 uppstår problemet i monteringsverktyget när en viss mall används. (FORMS-9445, FORMS-9408)
  <!-- *  When a user configures the watched folder endpoint for PDF Generator, it fails to pick documents on JDK 11. (FORMS-10152) -->
* **Adaptiv Forms**
   * När en användare försöker anropa en anpassad funktion utan att ändra ett fält, t.ex. ange värdet för ett annat fält, misslyckas det. (FORMS-9921)
   * När du arbetar med den anpassade felfunktionen för regelredigeraren i ett adaptivt format inträffar följande fel:
      * När en användare försöker använda @param{boolean} med en funktion tillåter inte regelredigeraren att booleska värden skickas till en funktion.
      * När en användare försöker använda @param{string} om en funktion används misslyckas regelredigeraren att skicka de valfria värdena och en varning om ofullständiga regler visas. (FORMS-9816, FORMS-9815)
   * Formuläranvändargruppen kan inte anropa regelredigeraren två gånger i ett anpassat formulär. (FORMS-9051)
   * När en användare väljer ett formulärobjekt i en visuell redigerare skickas hela fältinstansobjekt till den anpassade funktionen i stället för bara fältets värde. (FORMS-10015)
   * När en användare skapar ett huvudkomponentbaserat adaptivt formulär och lägger till en textindatakomponent, `Is Empty` och `Is Not Empty` fungerar inte i regelredigeraren. (FORMS-10098)
   * Om ett fält har markerats som ogiltigt i en huvudkomponentbaserad Adaptiv form, startar det en change-händelse i fältet. (FORMS-10087)
   * När en användare försöker skapa ett adaptivt formulär med ett komplext JSON-schema misslyckas det. Felet inträffar som:
     `GET /content/forms/af/katezeroone/testaf1.html HTTP/1.1] com.adobe.aemds.guide.service.impl.JsonObjectCreatorImpl Could not emit JSON with context java.lang.ArrayIndexOutOfBoundsException:0`. (FORMS-9639)
   * När en användare avmarkerar kryssrutan Jag accepterar villkoren i ett anpassat formulär aktiveras det igen när användaren rullar nedåt. (FORMS-9458)
   * När en användare öppnar ett adaptivt formulär på en Android™-enhet med Google Chrome/Firefox och anger maximalt antal tecken i en textruta, raderas inte värdet i textrutan. (FORMS-9354)
   * När kryssrutans etikett innehåller specialtecken som &#39;,&#39;, &#39;/&#39; eller &#39;.&#39;, markerar inte kryssrutan när du klickar på texten/etiketten. (FORMS-9313)
   * När en användare försöker att validera villkorskomponenten misslyckas det att validera om komponenten inte är i fokus medan den andra komponenten valideras. (FORMS-8725, FORMS-8913)
   * Om ett anpassat formulär laddas om efter uppgradering till AEM 6.5.16.0 Service Pack, misslyckas hämtningen av den bifogade filen. (FORMS-8906)
   * Om en kryssrutekomponent i ett adaptivt formulär som är baserat på en XDP-fil innehåller en titel som tilldelats ett numeriskt värde, kortas texten av och matchar inte det tilldelade värdet. (FORMS-8743)
   * Om en användare försöker implementera lat inläsning på ett fragment som är inbäddat i ett adaptivt formulär för författarmiljön, återspeglas inte reglerna/logiken som är definierad för fragmentet i formuläret. (FORMS-8554, FORMS-9182)
   * När du försöker öppna en koralldialogruta i AEM 6.5.16.0 Service Pack genereras `error.log: cannot render resource` undantag. (FORMS-8942)
   * När en användare försöker att översätta en kryssruta med ett enda alternativ i ett adaptivt formulär, misslyckas den. (FORMS-10181)
   * Alla DoR-mallar (Document of Record) kan inte publiceras. Endast engelska språkbaserade DoR-mallar och tillhörande Forms-baserade DoR-mallar publiceras. (FORMS-10535)

* **Tillgänglighet**
   * När du använder komponenten Klottsignatur i ett adaptivt formulär inträffar följande fel:
      * När det finns fler komponenter efter komponenten Skriptsignatur går inte tabbtangenten till signaturdialogrutan när det finns fler komponenter. I stället flyttas den till nästa komponent. Först efter att ha gått igenom alla komponenter, flyttas det till signaturdialogrutan.
      * När en användare signerar i signaturdialogrutan med en pensel eller ett tangentbord stängs inte dialogrutan om du trycker på Retur.
      * Det går inte att komma åt bekräftelsedialogrutan för rensad signatur via ett tangentbord.
      * Skärmläsaren kan inte läsa information som angetts i en dialogruta.
      * Det går inte att rensa signaturen utan att använda en mus.  (FORMS-9317)
   * När en användare skickar ett adaptivt formulär kan skärmläsaren inte läsa felmeddelanden för de obligatoriska fälten. (FORMS-9316)
   * När en skärmläsare läser upp ett HTML-formulär uppstår problemet när texten läses med kerning (mellanrum). (FORMS-9258)
   * I ett adaptivt formulär anropas inte de referenser/fotnoter som är länkade till texten med skärmläsaren. (FORMS-8920)
   * Hjälpmedelstaggar känns inte igen korrekt i den senaste designern. (FORMS-10139)
* **Interaktiv kommunikation**
   * I Correspondence Management fungerar inte lokaliseringen. (FORMS-8926)
   * Utkastbrevet kan inte öppnas när tjänsten publishAll används. (FORMS-8589)
   * Efter Experience Manager har Service Pack 16 installerats på servrarna och alla interaktiva kommunikationsbokstäver börjar klockan om de försöker redigera dessa bokstäver. Om de tillhandahåller någon provnyttolast för att förhandsgranska eller visa/redigera egenskapssidan fungerar de. De kan dock inte redigera bokstäverna. (FORMS-9067)


<!-- ### [!DNL Commerce]{#commerce-6518}

* A -->

### Foundation{#foundation-6518}

#### Innehållsdistribution{#foundation-content-distribution-6518}

* Borttagningskön för resurser ska inte blockeras och inget fel bör uppstå i loggfilen. (NPR-40570)

<!-- #### Integrations{#integrations-6518}

* A -->

<!-- #### Oak{#oak-6518}

* A -->

#### Plattform{#foundation-platform-6518}

* Efter en installation av vanilj Experience Manager, Service Pack 17, visas fel i `stderr.log`. Vanilla-installationer bör inte ge upphov till fel. (CQ-4353637)
* Knappen Skapa på taggningsskärmen uppfyller inte ACL (Access Control List). (NPR-40973)
* Det går inte att skapa, eller komma åt, eller båda, cachenoden för ContextHub på Experience Manager. (NPR-40515)

#### Replikering{#foundation-replication-6518}

* Replikeringsrensning tar bort alla underordnade för den begärda sökvägen. (NPR-40569)

#### Sling{#foundation-sling-6518}

* När en länkdelningsrapport genereras innehåller kolumnen Länk inte rätt värden. (NPR-40798)
* Med AEM 6.5.15.0 bryts alla e-postadresser, snedalias och snedkopplingar efter en AEM omstart. (NPR-40420)

#### Översättningsprojekt{#foundation-translation-6518}

* Översättning `rules.xml` sorteras på ett dåligt sätt när regler läggs till från användargränssnittet för översättningskonfigurationen. (NPR-40431)
* Stöd länkar med frågeparametrar under översättning. (NPR-40339)
* Användargränssnittet för ordlistan läses inte in för kunden efter att den extra kontextroten har uppdaterats. (NPR-40650)
* Det gick inte att skapa språkkopior när en av resurserna är ett innehållsfragment som innehåller ett flerfält med typerna ReferenceFragment eller ContentFragment. (NPR-40892)

#### Användargränssnitt{#foundation-ui-6518}

* Enligt beskrivningen i [Configuration Browser-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html?lang=en#using-configuration-browser), _Namnet blir nodnamnet i databasen_. I Configuration Browser används dock Configuration Title för sökväg i CRXDE Lite, och namnet på Configuration ignoreras. (NPR-40607)

<!-- #### WCM{#wcm-6518}

* A -->

#### Arbetsflöde{#foundation-workflow-6518}

* När du återställer en resursversion behålls objektets status i bearbetningsläge. (NPR-41029)
* Sorteringsproblem i användargränssnittet Resurser och Projekt. Vissa har åsidosatt de anpassade kolumnerna i användargränssnittet Resurser och Projekt enligt verksamhetskraven. De har implementerat en sortering med hjälp av egenskapen som är färdig `sortable=true`. De ser dock inkonsekvenser i sorteringen när det finns många poster i användargränssnittet Projekt eller Resurser. (NPR-41027)
* Loggar håller på att fyllas med `NullPointerException` i `EMailNotificationService`och e-post, som arbetsflöden ska skicka, skickas inte. (NPR-40898)
<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST  * The timeline is not providing references to the selected content. (NPR-40806) -->

## Installera [!DNL Experience Manager] 6.5.18.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.18.0 kräver [!DNL Experience Manager] 6.5. Se [uppgraderingsdokumentation](/help/sites-deploying/upgrade.md) för detaljerade anvisningar. <!-- UPDATE FOR EACH NEW RELEASE -->
* Service Pack-nedladdning finns på Adobe [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip).
* På en distribution med MongoDB och flera instanser installerar du [!DNL Experience Manager] 6.5.18.0 på en av författarinstanserna med hjälp av Package Manager.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe rekommenderar inte att du tar bort eller avinstallerar [!DNL Experience Manager] 6.5.18.0-paket. Innan du installerar paketet bör du skapa en säkerhetskopia av `crx-repository` om du måste rulla tillbaka den. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Installera Service Pack på [!DNL Experience Manager] 6.5{#install-service-pack}

1. Starta om instansen innan installationen om instansen är i uppdateringsläge (när instansen uppdaterades från en tidigare version). Adobe rekommenderar att du startar om om den aktuella upptiden för en instans är hög.

1. Ta en ögonblicksbild eller en ny säkerhetskopia av din [!DNL Experience Manager] -instans.

1. Hämta Service Pack från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Öppna Pakethanteraren och välj **[!UICONTROL Upload Package]** för att överföra paketet. Mer information finns på [Pakethanteraren](/help/sites-administering/package-manager.md).

1. Markera paketet och välj **[!UICONTROL Install]**.

1. Om du vill uppdatera S3-anslutningen stoppar du instansen efter installationen av Service Pack, byter ut den befintliga kopplingen mot en ny binär fil som finns i installationsmappen och startar om instansen. Se [Amazon S3 - datalager](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Dialogrutan för pakethanterarens gränssnitt avslutas ibland när Service Pack installeras. Adobe rekommenderar att du väntar på att felloggarna ska stabiliseras innan du får åtkomst till distributionen. Vänta på de specifika loggarna för avinstallationen av uppdateringspaketet innan du försäkrar dig om att installationen lyckas. Vanligtvis inträffar det här problemet i [!DNL Safari] webbläsare, men kan ibland inträffa i vilken webbläsare som helst.

**Automatisk installation**

Det finns två olika metoder som du kan använda för att installera automatiskt [!DNL Experience Manager] 6.5.18.0<!-- UPDATE FOR EACH NEW RELEASE -->

* Placera paketet i `../crx-quickstart/install` när servern är tillgänglig online. Paketet installeras automatiskt.
* Använd [HTTP-API från Package Manager](/help/sites-administering/package-manager.md#package-share). Använd `cmd=install&recursive=true` så att de kapslade paketen installeras.

>[!NOTE]
>
>Experience Manager 6.5.18.0 stöder inte installation av Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validera installationen**

Om du vill veta vilka plattformar som är certifierade för att fungera med den här versionen kan du läsa [tekniska krav](/help/sites-deploying/technical-requirements.md).

1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience Manager (6.5.18.0)` under [!UICONTROL Installed Products]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Alla OSGi-paket är **[!UICONTROL ACTIVE]** eller **[!UICONTROL FRAGMENT]** i OSGi Console (Use Web Console: `/system/console/bundles`).

1. OSGi-paketet `org.apache.jackrabbit.oak-core` är version 1.2.2.16 eller senare (Använd webbkonsol: `/system/console/bundles`). <!-- NPR-41010 for 6.5.18.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installera Service Pack för [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Anvisningar om hur du installerar Service Pack på Experience Manager Forms finns i [Installationsanvisningar för Experience Manager Forms Service Pack](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### Installera GraphQL Index Package för Experience Manager Content Fragments{#install-aem-graphql-index-add-on-package}

Kunder som använder GraphQL måste installera [Experience Manager Content Fragment with GraphQL Index Package 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

På så sätt kan du lägga till den indexdefinition som krävs baserat på de funktioner som de faktiskt använder.

Om du inte installerar det här paketet kan GraphQL-frågor bli långsamma eller misslyckas.

>[!NOTE]
>
>Installera bara det här paketet en gång per instans. Det behöver inte installeras om med varje Service Pack.

### UberJar{#uber-jar}

UberJar för [!DNL Experience Manager] 6.5.18.0 finns i [Maven Central-arkivet](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.18/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Information om hur du använder UberJar i ett Maven-projekt finns i [använda UberJar](/help/sites-developing/ht-projects-maven.md) och inkludera följande beroende i projektens POM: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.18</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar och andra tillhörande artefakter finns tillgängliga i Maven Central Repository i stället för i Adobe Public Maven-arkivet (`repo.adobe.com`). Huvudfilen för UberJar byter namn till `uber-jar-<version>.jar`. Så det finns ingen `classifier`, med `apis` som värdet, för `dependency` -tagg.

## Föråldrade och borttagna funktioner{#removed-deprecated-features}

Se [Föråldrade och borttagna funktioner](/help/release-notes/deprecated-removed-features.md/).

## Kända fel{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* I förhållande till eko från Service Pack 13 och senare har följande fellogg börjat visas som påverkar persistence-cachen:

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

  För att åtgärda problemet `damAssetLucene` måste konfigureras så att följande två egenskaper ingår:

   * `contentFragment`
   * `model`

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

* JDK-versioner som är högre än 1.8.0_281 stöds inte för WebLogic JEE-server. (FORMS-8498, CQDOC-20383)
* Som [!DNL Microsoft®® Windows Server 2019] stöder inte [!DNL MySQL 5.7] och [!DNL JBoss®® EAP 7.1], [!DNL Microsoft®® Windows Server 2019] stöder inte körklara installationer för [!DNL Experience Manager Forms 6.5.10.0]. (CQDOC-18312)
* JDK 11.0.20 stöds inte för installation av AEM Forms i JEE Installer. Endast JDK 11.0.19 och tidigare versioner stöds för installation av AEM Forms i JEE Installer. (FORMS-10659)

#### Installation

* På JBoss® 7.1.4-plattformen när användaren installerar Experience Manager 6.5.16.0 eller senare Service Pack, `adobe-livecycle-jboss.ear` distributionen misslyckas. (CQ-4351522, CQDOC-20159)
* När du har installerat AEM Service Pack 6.5.18.0, kan EAR-distributionen inte köras på JEE med JBoss® Turnkey (CQDOC-20803).
Du löser problemet genom att leta reda på `<AEM_Forms_Installation_dir>\jboss\bin\standalone.bat` fil och uppdatera `Adobe_Adobe_JAVA_HOME` till `Adobe_JAVA_HOME` för alla förekomster innan konfigurationshanteraren körs.

#### Adaptiv Forms

* När ett adaptivt formulär publiceras kommer alla dess beroenden, inklusive profiler, att publiceras på nytt, även om inga ändringar har gjorts i dem. (FORMS-10454)
* När en användare väljer att konfigurera ett fält för första gången i ett adaptivt formulär visas inte alternativet att spara en konfiguration i egenskapsläsaren. Problemet åtgärdas genom att ett annat fält i det adaptiva formuläret konfigureras i samma redigerare.
* När en omdirigerings-URL anges i stödlinjebehållaren för ett adaptivt formulär slutar den infogade signeringen att fungera. (FORMS-10493)
* Alla DoR-mallar (Document of Record) kan inte publiceras. Endast engelska språkbaserade DoR-mallar och tillhörande Forms-baserade DoR-mallar publiceras. (FORMS-10535)

#### Interaktiv kommunikation

* När du har uppgraderat till AEM Service Pack 18 går det inte att redigera interaktiva kommunikationsbrev. (FORMS-10578) Åtgärda problemet genom att utföra följande steg:

   1. Ladda ned [Programfix-FORMS-10578](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) från SD-länk.
   1. Extrahera Hotfix-arkivfilen för att få ett Experience Manager-paket (.zip) och en paketfil (.jar).
   1. Överför och installera paketet (.zip) via Package Manager.
   1. Öppna konfigurationshanterarpaketen `https://server:host/system/console/bundles`, ladda upp och installera paketet (.jar).

## OSGi-paket och innehållspaket som ingår{#osgi-bundles-and-content-packages-included}

Följande textdokument listar de OSGi-paket och innehållspaket som ingår i [!DNL Experience Manager] 6.5.18.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Förteckning över OSGi-paket i Experience Manager 6.5.18.0](/help/release-notes/assets/65180_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Förteckning över innehållspaket som ingår i Experience Manager 6.5.18.0](/help/release-notes/assets/65180_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Begränsade webbplatser{#restricted-sites}

Dessa webbplatser är bara tillgängliga för kunder. Om du är kund och behöver åtkomst kontaktar du din kontoansvarige på Adobe.

* [Nedladdning av produkt på licensing.adobe.com](https://licensing.adobe.com/)
* [Kontakta Adobe kundsupport](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] produktsida](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* [Prenumerera på produktuppdateringar med Adobe prioritet](https://www.adobe.com/subscription/priority-product-update.html)
