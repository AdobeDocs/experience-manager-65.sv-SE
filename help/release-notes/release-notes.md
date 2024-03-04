---
title: Versionsinformation för [!DNL Adobe Experience Manager] 6.5
description: Hitta versionsinformation, nyheter, installationsanvisningar och en detaljerad ändringslista för [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
source-git-commit: 348b82f0bd0d99eeb771aa4ed2719ee10d8cee68
workflow-type: tm+mt
source-wordcount: '3440'
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
| Version | 6.5.20.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Typ | Service Pack-version |
| Datum | Torsdag den 22 februari 2024 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Hämta URL | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Vad ingår i [!DNL Experience Manager] 6.5.20.0 {#what-is-included-in-aem-6520}

[!DNL Experience Manager] 6.5.20.0 innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat, felkorrigeringar, prestanda, stabilitet och säkerhetsförbättringar som har släppts sedan den första tillgängligheten av 6.5 i april 2019. [Installera detta Service Pack](#install) på [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## Viktiga funktioner och förbättringar

<!-- * _6.5.20.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Några av de viktigaste funktionerna och förbättringarna i den här versionen är följande:

* Dynamic Media stöder nu förlustfritt HEIC-bildformat för Apple iOS/iPadOS. Se [fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html?lang=en) i Dynamic Media Image Serving and Rendering API.

* Multisite Manager (MSM) har nu stöd för Experience Fragment-strukturer, inklusive mappar och undermappar, för effektiv gruppdistribution av Experience Fragments till Live Copies.

### [!DNL Forms]

* **Transaktionsrapportering i AEM Forms på JEE**: Transaktionsrapportering har införts för AEM Forms på JEE, vilket möjliggör omfattande registrering av dokumenttransaktioner som konverteringar, återgivningar och inskickade dokument. Den här förbättringen ökar effektiviteten och underlättar bättre registrering. Funktionen är inaktiverad som standard. Du kan aktivera det från administratörsgränssnittet.
* **Förbättrad säkerhet med stöd för ECDSA**: AEM Forms erbjuder nu robust stöd för ECDSA (Elliptic Curve Digital Signature Algorithm) i både JEE- och OSGi-stackar. Användare kan nu signera, certifiera och verifiera PDF-dokument med högre säkerhet. Följande algoritmer för EC-kurvor stöds:
   * ECDSA-elliptisk kurva P256 med SHA256-sammandragsalgoritm
   * ECDSA-elliptisk kurva P384 med SHA384-sammandragsalgoritm
   * ECDSA elliptisk kurva P512 med SHA512-algoritm
* **Smidig kompatibilitet med Windows 11 för Forms Designer**: AEM Forms Designer har nu stöd för Windows 11, vilket ger smidig installation och drift. Användare kan tryggt uppgradera till Windows 11 utan att behöva installera om Forms Designer eller oroa sig för kompatibilitetsproblem, vilket ger ett avbrottsfritt arbetsflöde.
* **Förbättrad tillgänglighet med en anpassad&quot;bildtextsroll&quot; i AEM Forms Designer**: AEM Forms Designer har nu en anpassad tillgänglighetsroll som kallas &quot;Bildtext&quot; som gör det möjligt för användare att skapa XDP-filer med anpassade bildtextelement. Den här funktionen förbättrar tillgängligheten genom att användarna kan integrera anpassade bildtexter i sina dokumentdesigner så att de kan förbättra integriteten och användarupplevelsen.

<!-- ### [!DNL Forms]

* text -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Åtgärdade problem i Service Pack 20 {#fixed-issues}

### [!DNL Sites]{#sites-6520}

<!--#### Accessibility{#sites-accessibility-6520}

* text -->

#### Administratörsgränssnitt{#sites-adminui-6520}

* The `Workflow Title` fältet är markerat med `*` efter behov, men det finns ingen validering. (SITES-16491)

<!--#### Classic UI{#sites-classicui-6520}

* text -->

#### [!DNL Content Fragments]{#sites-contentfragments-6520}

* Kapslade konfigurationsmappar stöds inte längre och mapparna för innehållsfragmentmodellen var inte längre synliga efter uppgradering till AEM 6.5.18 eller till AEM 6.5.19. (SITES-18110)
* Vissa undermappar kan inte välja bland ärvda innehållsfragmentmodeller. Den måste ha stöd för mappar utan att ha `jcr:content` -egenskapen, även om DAM-mapparna som skapas via användargränssnittet har en sådan nod. (SITES-17943)

#### [!DNL Content Fragments] - GRAPHQL API {#sites-graphql-api-6520}

<!-- REMOVED AS PER EMAIL FROM SAMEER DHAWAN FEBRUARY 19, 2024 * When upgrading AEM from 6.5.19.0 to 6.5.20.0, the path `/libs/cq/graphql/sites/graphiql` was getting deleted. (SITES-19530) CRITICAL -->
* När en GraphQL-fråga körs till [filterresultat](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#filtering) med valfria variabler, om ett specifikt värde är **not** som anges för den valfria variabeln ignoreras variabeln i filterutvärderingen. (SITES-17051)

<!--#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6520}

* text -->

#### [!DNL Content Fragments] - REST API{#sites-restapi-6520}

* Med uppgraderingen av `org.json` i biblioteket ändrades hur decimaltal avserialiserades. Innan de konverterades till &quot;som standard&quot; till &quot;Doubles&quot; och nu till BigDecimals. I stället ska egenskapsvärdena för metadata, som lagras med REST API, konverteras till Double från BigDecimal. (SITES-16857)

#### Core Backend{#sites-core-backend-6520}

* När Snabbpublicering av ett innehållsfragment används fortsätter inläsningen och publiceras inte. Snabbpublicering fungerar alltså inte för innehållsfragment efter en uppgradering av ett Service Pack från AEM 6.5.7 till AEM 6.5.17. När användaren testade hanterad publicering fungerade det. Men när de försökte med Snabbpublicering publicerades den inte. I synnerhet `com.day.cq.wcm.core.impl.reference.ActivationReferenceSearchBuilder` orsakade att systemet kraschade. (SITES-17311)
* Innehållsfragment kan inte serialiseras med Jackson-exporteraren: Sidan läses in när det finns ett innehållsfragment som refereras till på en sida (använder Jackson-exportkod) och taggar som har lagts till i ett innehållsfragment. (SITES-18096)

#### Kärnkomponenter{#sites-core-components-6520}

* Installation CIF Core Components package på AEM orsakar `:type` värdet på befintliga komponenter som ska ändras. Ändringen innebär att de inte längre återges på sidor som de har lagts till på. (SITES-17601)

#### Kampanjintegrering{#sites-campaign-integration-6520}

* AEM använde en tillåtelselista-även kallad `whitelist`-på grund av en sårbarhetsrapport. Tillåtelselista hindrade kunderna från att använda de funktioner som behövdes. (SITES-16822)

#### Upplevelsefragment{#sites-experiencefragments-6520}

* MSM for Experience Fragments har nu stöd för massutrullning till Experience Fragment-innehållsstrukturer som mappar och undermappar. (SITES-16004)

<!--#### Foundation Components (Legacy){#sites-foundation-components-legacy-6520}

* text

#### Launches{#sites-launches-6520}

* text -->

#### MSM - Live-kopior{#sites-msm-live-copies-6520}

* An &quot;`Is not modifiable`&quot;-undantag genereras när komponenten rullas ut. I synnerhet en `org.apache.sling.servlets.post.impl.operations.ModifyOperation` undantag inträffar under svarsbearbetningen. (SITES-18809)
* Det går inte att rulla ut ändringar i specifika Live-kopior av Experience Fragments. (SITES-17930)
* När en användare lägger till en anteckning i en komponent på en ritningssida och sedan placerar ut den, visas anteckningsantalet i Live Copy felaktigt. (SITES-17099)
* Knappen MSM-utfällning från överordnad sida till underordnad sida bryts i det grafiska användargränssnittet för pekfunktioner. När du väljer det här alternativet visas följande fel: `Uncaught TypeError: _g.shared is undefined`. (SITES-16991)

#### Page Editor{#sites-pageeditor-6520}

* Förhandsgranskningen av Forms Theme Editor är bruten. När Förhandsvisa är markerat visas bara en inläsningsikon. (SITES-17164)

### [!DNL Assets]{#assets-6520}

* Det går inte att validera regelbaserade fält i hjälpen för metadataredigeraren och ett felmeddelande om att obligatoriska fält saknas visas. (ASSETS-31396)
* När PDF har flyttats till en annan plats visas **[!UICONTROL View Page]** försvinner. (ASSETS-30538)
* Det går inte att välja en bild med läsbehörighet. (ASSETS-32199)
* Det går inte att ändra kortstorleken i visningsinställningarna. (ASSETS-31667)
* Överföringen misslyckas när filtypen .oft överförs. (ASSETS-30109)
* När du försöker lägga till ett anpassat metadatafält som en extra kolumn i rapporten markeras inte kryssrutorna. (ASSETS-31671)
* Resursflyttåtgärden fungerar inte korrekt i Experience Manager Service Pack 16. (ASSETS-30598)

#### [!DNL Dynamic Media]{#assets-dm-6520}

* När en resurs överförs till AEM `Update_asset` arbetsflödet aktiveras. Arbetsflödet avslutas dock aldrig. Arbetsflödet slutförs endast fram till produktöverföringssteget. Nästa steg är att ladda upp en Scene7-batch, men den processen kommer inte in i AEM. (ASSETS-30443)
* Behöver ett bättre sätt att hantera icke-Dynamic Media-filmer på ett smidigt sätt i Dynamic Media-komponenten. Det här problemet gav ett undantagsfel som instansierade `dynamicmedia_sly.js`. (ASSETS-31301)
* Förhandsgranskning fungerar för alla resurser, anpassningsbara videouppsättningar och videoklipp. 403-fel genereras dock för `.m3u8` filer (som för övrigt fortfarande fungerar som offentliga länkar). (ASSETS-31882)
* The `scene7SmartCropProcessingStatus` status korrigerad. Metadata för Smart Crop-video används för att visa fel även när det lyckades. (ASSETS-31255)

### [!DNL Forms]{#forms-6520}

<!--Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.20.0 Forms add-on package release is scheduled for Thursday, February 29, 2024. A list of Forms fixes and enhancements is added to this section post the release.-->

#### [!DNL Adaptive Forms]

* När en användare försöker integrera AEM Forms till en utskicksplattform med en AEM publicerad URL, lägger AEM Forms inte till `method=post` när sidan återges. Problemet inträffar trots att `POST` anges i åtgärden skicka med URL:en. Det gör att e-postplattformen inte kan identifiera detta som ett formulär. (FORMS-1214)
* När en användare väljer datumfältet med ett visningsmönster AEM Form Service Pack 6.5.18.0 kan användaren inte välja aktuellt datum med tangentbordet. (FORMS-12736)
* I AEM Forms Service Pack 6.5.17.0 och Service Pack 6.5.18.0 visas en extra rad när en användare växlar mellan månader i kalenderwidgeten. (FORMS-1869)
* När en användare klickar på en bild med&quot;Ta ett foto&quot; i komponenten Bilaga på en iOS-enhet läggs alla bilder till i mappen med samma namn. (FORMS-1224)
* När en användare uppdaterar ett befintligt alternativ i en alternativknappsgrupp publiceras felaktiga översättningsvärden. (FORMS-12575)
* När en användare lägger till tecken i ett adaptivt formulär på en Android™-enhet kan användaren skriva fler än det definierade maximala antalet tecken i textfältet vid fokus på Android™-enheter. Det fungerar emellertid när en användare väljer indatatypen HTML5. (FORMS-12748)
* På grund av matchande etiketter i Arial®, som är märkta med och Arial®, kan skärmläsarna inte skilja mellan dessa två. För att lösa problemet ersätts etiketten &quot;aria-marked-by&quot; med &quot;aria-describedby&quot; för formulärfälten. (FORMS-12436)
* När en författare använder komponenten &quot;Adaptive Forms - Embed (v2)&quot; för att bädda in ett adaptivt formulär på sin webbplatssida och det inbäddade formuläret innehåller en CAPTCHA-komponent (CAPTCHA-tjänst -> reCAPTCHA, Inställningar -> reCAPTCHA-v2) återges inte webbplatssidan när användaren försöker visa webbsidan med &quot;View as Published&quot; på författaren -instans. Följande fel visas som (FORMS-11859):
  `Failed to construct 'URL': Invalid base URL at Object.renderRecaptcha`

* När en användare försöker välja datumet med datumväljarkomponenten uppdateras inte värdet och NULL visas. (FORMS-12742, FORMS-12736)

* När en användare uppgraderar till AEM Form Service Pack 6.5.19.0, efter att ha uppdaterat ett nytt språk till den befintliga ordlistan, sammanfogas den inte med raderna &quot;guideContainer&quot; för att lägga till en språkinställning i ett formulär. (FORMS-12947)

* På AEM Forms Service Pack 6.5.19.0 misslyckas den anropade webbtjänståtgärden på Java™ 11 med felet (FORMS-12329):
  `java.lang.NoClassDefFoundError message:sun/misc/BASE64Decoder`

* När en användare anropar&quot;receive&quot;-åtgärden för&quot;EmailService&quot; i AEM Forms Service Pack 6.5.18.0 genereras ett undantag (FORMS-12050):
  `java.util.ServiceConfigurationError: javax.mail.Provider: Provider com.sun.mail.imap.IMAPProvider not a subtype`

* När FIPS-läget är aktiverat på AEM Forms Service Pack 6.5.18.0 misslyckas skapandet av en användare med standardinställningen DOM med felet (FORMS-11857):
  `com.adobe.idp.cx.a: error seeding random number generator`

* När en användare väljer teckensnitt i ADMINUI under sökvägen `Home>Services>PDF Generator>Adobe PDF Settings`, blir det inte markerat. Dessutom är listrutan med tillgängliga teckensnitt tom i en standardprofil eller en anpassad profil. Det är därför inte möjligt att anpassa underlistan till **Inkludera alltid** eller **Inkludera aldrig**. Användaren kan inte konfigurera teckensnittet för PDF med PDF Generator. Loggarna visar inga relevanta felmeddelanden. (FORMS-12095)

* På AEM Forms Service Pack 6.5.18.0 kan användaren inte skapa säkerhetsinställningar, inga fel- eller serverloggar visas, men ett popup-felmeddelande visas på skärmen. (FORMS-1212)

* När en användare av AEM Forms Service Pack 6.5.18.0 skickar ett adaptivt formulär i JEE-arbetsflödet skickas inte bilagan i det adaptiva formuläret till JEE-processen, vilket orsakar programfel. (FORMS-12232, FORMS-1228)

* När en användare konverterar PDF till PDF/A-2b eller PDF/A-3B misslyckas konverteringen visas felet som: (FORMS-12790)

  ```
  OCCD contains Order key that does not reference all layers.
  -> Optional content configuration dictionary has no Name entry.
  -> Font not embedded (and text rendering mode not 3).
  obj(65, 0)
  Page: 1
  -> Font not embedded (and text rendering mode not 3).
  obj(67, 0)
  Page: 1
  -> PDF/A entry missing. 
  -> PDF/A entry missing.
  ```

* När ett anpassat formulär publiceras på AEM Forms 6.5.18.0 publiceras alla beroenden, inklusive profiler, på nytt, även om inga ändringar har gjorts. (FORMS-10454)

* När en användare väljer &quot;Microsoft SharePoint&quot; när konfigurationshanteraren körs på AEM Forms 6.5.19.1 med JBoss® Turnkey-konfiguration misslyckas installationen av LiveCyclet JBoss® EAR och följande fel visas: (FORMS-12463)

  ` Caused by: org.jboss.as.server.deployment.DeploymentUnitProcessingException: WFLYEE0031: Unable to process modules in application.xml for EAR ["/C:/AEM/jboss/bin/content/ adobe-livecycle-jboss.ear "], module file adobe-connectorformssharepoint-config-ejb.jar not found.`

#### [!DNL Forms Designer] {#forms-designer-6520}


* När en användare uppgraderar till AEM Forms Service Pack 6.5.18.0 misslyckas XDP-filer som skickas via utdatatjänsten med alternativet tagged PDF. Detta beror på att undantagshantering saknas. (LC-3921757)

* När en användare skapar ett PDF med AEM Forms Designer, taggas rubriknivåer i hjälpmedelsträdet tillsammans med det grafiska elementet, till exempel en rektangulär ruta. (LC-3921687)

* På AEM Forms Designer som installerats via Workbench är versionsinformationen inte explicit i `Control Panel/Programs/Programs and Features`. (LC-3921976)

<!--* When a user creates an XDP on AEM Forms Designer, the user is not able to add the custom Caption Tag. (LC-3921246)-->

* När en användare skapar en XDP-tagg i AEM Forms Designer, vid utdata från PDF, kapslas inte knappformulärtaggen i den överordnade stycketaggen (p-tagg). (LC-3921719)

* När en användare skapar en XDP-fil i AEM Forms Designer, i PDF-utdata när en användare navigerar genom formulärtaggarna, taggas även bakgrundsobjektet. (LC-3921687)

### Foundation {#foundation-6520}

#### Communities {#communities-6520}

* Diagnostik för användarsynkronisering misslyckas efter att användarsynkroniseringen har konfigurerats. (NPR-41693)

<!-- #### Content distribution{#foundation-content-distribution-6520}

* text -->

#### Integreringar{#integrations-6520}

* Ta bort all kod och alla beroenden för Adobe Search &amp; Promote från AEM 6.5. (NPR-40856)

#### Lokalisering{#localization-6520}

* Aria-etiketten&quot;close&quot; är inte lokaliserad i **[!UICONTROL Assets]** > **[!UICONTROL Files]**, markerar en mapp och väljer sedan **[!UICONTROL Properties]** > **[!UICONTROL Permissions]** tab > member name. (NPR-41705)
* Det finns ett trunkerat verktygstips för **[!UICONTROL Key Store Password]** på SSL-inställningssidan för språkområden ENG, FRA, KOR, DEU och PTB. (NPR-41367)

#### Plattform{#foundation-platform-6520}

* Problem med att integrera Campaign med AEM som orsakas av att /api-servern inte returnerar rätt schema i href json. Orsaken var att AEM inte fick rubriken X-Forward-Proto som tvingade begäran att svara med ett HTTP-schema i stället för HTTPS. Därför bör man lägga till möjligheten att växla mellan schemaval baserat på en OSGI-konfiguration. (GRANITE-48454)

#### Sling{#foundation-sling-6520}

* The `org.apache.sling.resourceMerger` bundle 1.4.2 genererar ett undantag från AEM 6.5, Service Pack 17 och senare. Sling-resurskoncentrationen 1.4.4 bör ingå i Service Pack 20. (NPR-41630)

#### Översättning{#foundation-translation-6520}

* Efter distributionen av AEM 6.5 Service Pack 18 uppstod ett problem med fliken Filter i Översättningsregelredigeraren. När en kontext är markerad och du klickar på Redigera > Spara, visas ett dubbelt citattecken som HTML nästa gång du öppnar samma kontext. Översättningsreglerna sparades inte korrekt. (NPR-41624)
* Problem som rör översättningar av innehållsfragment, där de översatta strängarna skickas tillbaka från översättningsleverantören till AEM, men de sitter fast på `/content/projects` och inte uppdatera innehållsfragmenten. (NPR-41516)
* Ett felmeddelande visas när en språkkopia skapas. Det förekommer på en sida som har ett innehållsfragment som refereras i en sidegenskap, med hjälp av innehållsfragmentmodeller. (NPR-41441)
* Länkar i Experience Fragments justeras inte till rätt språk under Language Copy. I stället pekar Experience Fragment på det primära språkområdet. (NPR-41343)

#### Användargränssnitt{#foundation-ui-6520}

* Konsolfel uppstår efter en uppgradering till AEM 6.5, Service Pack 18. Felet finns i `coralUI3.js` och inträffar när du väljer en nedrullningsbar meny i AEM. I synnerhet händer det med en `onOverlayToggle` -händelse. Felet `Uncaught TypeError: Cannot read properties of null (reading 'innerText')` visas. (NPR-41467)
* AEM **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Tagging]** > **[!UICONTROL Create]** > **[!UICONTROL Create Tag]**, ange icke-latinska tecken i **Titel** fältet orsakar **Namn** fält som bara ska fyllas med bindestreck ( `-` ). (NPR-41623)
* Upphovsrättsåret är felaktigt i `About Adobe Experience Manager` -dialogrutan. (NPR-41526)
* Det finns oöversatta **[!UICONTROL Profile Properties]** strängar när användarinställningar redigeras. Inträffar i alla språkområden. (NPR-41365)

<!-- #### WCM{#wcm-6520}

* text

#### Workflow{#foundation-workflow-6520}

* text -->

## Installera [!DNL Experience Manager] 6.5.20.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.20.0 kräver [!DNL Experience Manager] 6.5. Se [uppgraderingsdokumentation](/help/sites-deploying/upgrade.md) för detaljerade anvisningar. <!-- UPDATE FOR EACH NEW RELEASE -->
* Service Pack-nedladdning finns på Adobe [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip).
* På en distribution med MongoDB och flera instanser installerar du [!DNL Experience Manager] 6.5.20.0 på en av författarinstanserna med hjälp av Package Manager.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe rekommenderar inte att du tar bort eller avinstallerar [!DNL Experience Manager] 6.5.20.0-paket. Innan du installerar paketet bör du skapa en säkerhetskopia av `crx-repository` om du måste rulla tillbaka den. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Installera Service Pack på [!DNL Experience Manager] 6.5{#install-service-pack}

1. Starta om instansen innan installationen om instansen är i uppdateringsläge (när instansen uppdaterades från en tidigare version). Adobe rekommenderar att du startar om om den aktuella upptiden för en instans är hög.

1. Ta en ögonblicksbild eller en ny säkerhetskopia av din [!DNL Experience Manager] -instans.

1. Hämta Service Pack från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Öppna Pakethanteraren och välj **[!UICONTROL Upload Package]** för att överföra paketet. Mer information finns på [Pakethanteraren](/help/sites-administering/package-manager.md).

1. Markera paketet och välj **[!UICONTROL Install]**.

1. Om du vill uppdatera S3-anslutningen stoppar du instansen efter installationen av Service Pack, byter ut den befintliga kopplingen mot en ny binär fil som finns i installationsmappen och startar om instansen. Se [Amazon S3 - datalager](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Dialogrutan för pakethanterarens gränssnitt avslutas ibland när Service Pack installeras. Adobe rekommenderar att du väntar på att felloggarna ska stabiliseras innan du får åtkomst till distributionen. Vänta på de specifika loggarna för avinstallationen av uppdateringspaketet innan du försäkrar dig om att installationen lyckas. Vanligtvis inträffar det här problemet i [!DNL Safari] webbläsare, men kan ibland inträffa i vilken webbläsare som helst.

**Automatisk installation**

Det finns två olika metoder som du kan använda för att installera automatiskt [!DNL Experience Manager] 6.5.20.0<!-- UPDATE FOR EACH NEW RELEASE -->

* Placera paketet i `../crx-quickstart/install` när servern är tillgänglig online. Paketet installeras automatiskt.
* Använd [HTTP-API från Package Manager](/help/sites-administering/package-manager.md#package-share). Använd `cmd=install&recursive=true` så att de kapslade paketen installeras.

>[!NOTE]
>
>Experience Manager 6.5.20.0 stöder inte installation av Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validera installationen**

Om du vill veta vilka plattformar som är certifierade för att fungera med den här versionen kan du läsa [tekniska krav](/help/sites-deploying/technical-requirements.md).

1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience Manager (6.5.20.0)` under [!UICONTROL Installed Products]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Alla OSGi-paket är **[!UICONTROL ACTIVE]** eller **[!UICONTROL FRAGMENT]** i OSGi Console (Use Web Console: `/system/console/bundles`).

1. OSGi-paketet `org.apache.jackrabbit.oak-core` är version 1.2.2.18 eller senare (Använd webbkonsol: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installera Service Pack för [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Anvisningar om hur du installerar Service Pack på Experience Manager Forms finns i [Installationsanvisningar för Experience Manager Forms Service Pack](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>Funktionen Adaptive Forms, som finns i [AEM 6.5 QuickStart](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/deploying/deploy.html), är endast avsedd för prospektering och utvärdering. För produktion krävs en giltig licens för AEM Forms, eftersom Adaptive Forms-funktionaliteten kräver rätt licensiering.

### Installera GraphQL Index Package för Experience Manager Content Fragments{#install-aem-graphql-index-add-on-package}

Kunder som använder GraphQL måste installera [Experience Manager Content Fragment with GraphQL Index Package 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

På så sätt kan du lägga till den indexdefinition som krävs baserat på de funktioner som de faktiskt använder.

Om du inte installerar det här paketet kan GraphQL-frågor bli långsamma eller misslyckas.

>[!NOTE]
>
>Installera bara det här paketet en gång per instans. Det behöver inte installeras om med varje Service Pack.

### UberJar{#uber-jar}

UberJar för [!DNL Experience Manager] 6.5.20.0 finns i [Maven Central-arkivet](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.20/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Information om hur du använder UberJar i ett Maven-projekt finns i [använda UberJar](/help/sites-developing/ht-projects-maven.md) och inkludera följande beroende i projektens POM: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.20</version>
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


### Kända fel för AEM Forms {#known-issues-aem-forms-6520}

* Efter uppdatering från AEM 6.5 av Forms Service Pack 18 (6.5.18.0) eller AEM 6.5 av Forms Service Pack 19 (6.5.19.0) till AEM 6.5 av Forms Service Pack 20 (6.5.20.0) påträffas ett JSP-kompileringsfel. De kan inte öppna eller skapa anpassade formulär och de stöter på fel med andra AEM gränssnitt som sidredigeraren, AEM Forms gränssnitt och AEM Workflow editor. Ett felmeddelande som liknar följande visas:

`Unable to compile class for JSP: An error occurred at line: 162 in the jsp file: /libs/granite/ui/components/coral/foundation/anchorbutton/anchorbutton.jsp The method transformLinkInUriIfExternal(String) is undefined for the type ComponentHelper`

Du kan kontakta Adobe support för att få en lösning på problemet.

* Förifyllningstjänsten misslyckas med ett null-pekarundantag i Interactive Communications. (CQDOC-21355)

<!--Known issues in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.20.0 Forms add-on package release is scheduled for Thursday, February 29, 2024. A list of known issues for forms is added to this section post the release.-->

<!--
#### Install the servlet fragment (AEM Service Pack 6.5.14.0 or earlier)

* If you are upgrading to AEM Service Pack 6.5.15.0 or higher, and your AEM instance is operating on Tomcat 8.5.88, it is mandatory that you install the servlet fragment *before* you proceed with the installation of Service Pack 6.5.15.0 or higher.
* It is mandatory that you install the servlet fragment for all application servers except those running on JBoss&reg; EAP 7.4.0.

**To install the servlet fragment:**

1. Download the servlet fragment from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).
1. Start the application server. 
1. Wait for the logs to stabilize and check the bundle state.
1. Open Web Console Bundles. The default URL is `http://[Server]:[Port]/system/console/bundles`.
1. Select **[!UICONTROL Install]** or **[!UICONTROL Update]**. 
1. Select the downloaded fragment 
`org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar` 
1. Select **[!UICONTROL Install]** or **[!UICONTROL Update]**. 
1. Wait for the application server to stabilize.
1. Stop the application server.

-->

## OSGi-paket och innehållspaket som ingår{#osgi-bundles-and-content-packages-included}

Följande textdokument listar de OSGi-paket och innehållspaket som ingår i detta [!DNL Experience Manager] 6.5 Service Pack-version:

* [Förteckning över OSGi-paket i Experience Manager 6.5.20.0](/help/release-notes/assets/65200-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Förteckning över innehållspaket som ingår i Experience Manager 6.5.20.0](/help/release-notes/assets/65200-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Begränsade webbplatser{#restricted-sites}

Dessa webbplatser är bara tillgängliga för kunder. Om du är kund och behöver åtkomst kontaktar du din kontoansvarige på Adobe.

* [Nedladdning av produkt på licensing.adobe.com](https://licensing.adobe.com/)
* [Kontakta Adobe kundsupport](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] produktsida](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* [Prenumerera på produktuppdateringar med Adobe prioritet](https://www.adobe.com/subscription/priority-product-update.html)
