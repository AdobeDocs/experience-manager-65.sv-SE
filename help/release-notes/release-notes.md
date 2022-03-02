---
title: Versionsinformation för [!DNL Adobe Experience Manager] 6.5
description: '"[!DNL Adobe Experience Manager] 6.5 som beskriver versionsinformation, nyheter, hur man installerar och detaljerade ändringslistor."'
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: 6a89cb79ccfbcec7385832d5682bf61895253718
workflow-type: tm+mt
source-wordcount: '2630'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] 6.5 Versionsinformation om senaste Service Pack {#aem-service-pack-release-notes}

## Versionsinformation {#release-information}

| Produkter | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.12.0 |
| Typ | Service Pack-version |
| Date | 24 februari 2022 |
| Hämta URL | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.12.0.zip) |

## Vad ingår i [!DNL Adobe Experience Manager] 6.5.12.0 {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.12.0 innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat samt prestanda, stabilitet och säkerhetsförbättringar som släppts sedan 6.5-utgåvan släpptes i april 2019. Service Pack är installerat på [!DNL Adobe Experience Manager] 6.5.

De viktigaste funktionerna och förbättringarna i [!DNL Adobe Experience Manager] 6.5.12.0 är:

* När du har konfigurerat en anslutning mellan distributioner av fjärr-DAM och platser, blir resurserna på fjärr-DAM tillgängliga i Sites-distributionen. Nu kan du uppdatera, ta bort, byta namn på och flytta resurser eller mappar i fjärr-DAM. Uppdateringarna, med viss fördröjning, är automatiskt tillgängliga i Sites-distributionen (NPR-37816).

* Det går nu som standard att överföra en live-kopieringskälla till flera live-kopior, utan att en ritningskonfiguration krävs (CQ-4259951).
* Statusen för pågående asynkrona åtgärder visas nu i användargränssnittet för att förhindra att användare av misstag utlöser flera asynkrona åtgärder på samma sökväg (NPR-37611).
* Stöd för IMS-baserad autentisering tillhandahålls för API:er i Analytics 2.0 (CQ-4285474, NPR-37803, NPR-37701, NPR-37702, NPR-37703).
* API-stöd för JSON-erbjudandetypsfragment (NPR-37796).
* Erbjudandet gäller nu för Delete-erbjudandet (Experience Fragment API) i IMS (NPR-37668).
* Den inbyggda databasen (Apache Jackrabbit Oak) är fortfarande 1.22.9.

Nedan följer en lista över korrigeringar i [!DNL Experience Manager] 6.5.12.0.

### [!DNL Sites] {#sites-65120}

Följande problem har åtgärdats i [!DNL Sites]:

* Layouten för egenskaperna för innehållsfragmentet bryts eftersom flikarna Grundläggande och Avancerat inte har några marginaler till vänster (SITES-4484).
* Alternativet att stänga bannern på innehållsfragment som refereras på olika webbplatssidor fungerar inte. Den här banderollen informerar användarna om att det finns referenser till innehållsfragmentet på en eller flera sidor (SITES-4173).
* Kryssrutorna är inte justerade i dialogrutan Återställ arv (SITES-3514).
* Mallsidan på webbbutiker och webbplatser som fungerar fungerar fungerar inte eftersom komponenterna inte läses in och strukturalternativet inte är tillgängligt, eftersom pageinfo.json-servleten fastnar på LaunchManagerImpl.getLaunchStream (SITES-3489).
* Publicering av användarnoder från författare till publiceringsmiljö fungerar inte (NPR-38005).
* Om du försöker skapa ett upplevelsefragment med en redigerad mall visas inte redigeringarna av egenskaperna för den första sidan (NPR-37962).
* Sidflyttningen på Experience Manager är långsam (NPR-37961).
* Experience fragment translation uppdaterar inte referenser till språkkopieringssökvägar (NPR-37953).
* Användare utan replikeringsbehörighet kan inte ta bort eller flytta sidor, även om sidorna inte är aktiverade (NPR-37936).
* Slumpmässiga fel av typen org.apache.felix.metatype har observerats på servern (NPR-37935).
* Referenser i Pekanvändargränssnittet för Sites-administratörer visar inte inkommande länkar korrekt (NPR-37934).
* Startsökvägen för att lägga till nya sidor eller resurser är inte tillgänglig när du väljer sidor i ett översättningsjobb (NPR-37912).
* Referenssidor i en listkomponent som lagts till i upplevelsefragment uppdateras inte till målsidan när du befordrar starten (NPR-37886).
* Det finns gränssnittsproblem i redigeringsmiljön - t.ex. sidtitel i redigeringsläge är inte centrerat och den tillåtna komponentväljaren är inte i principredigeraren: kryssrutan för grupp tar hela behållarens bredd, så etiketten återges på nästa rad (NPR-37878).
* [Plattform] Versionsnumret för xmlns:metatype i filen metatype.xml för Commons-httpclient är &quot;http://www.osgi.org/xmlns/metatype/v1.0.0&quot; i stället för &quot;http://www.osgi.org/xmlns/metatype/v1.2.0&quot; (NPR-37865).
* Fel observeras och sidor kan inte flyttas när du försöker till en sida (NPR-37864).
* [RTF-redigerare] Bilden återges inte i det klassiska användargränssnittet när du lägger till bilden som ett listobjekt i RTF-redigeraren (NPR-37835).
* Författare kan lägga till taggar som ligger utanför den konfigurerade rotsökvägen när de använder taggfält i en dialogruta (NPR-37834).
* Multifält återges inte korrekt i layoutbehållaren och ger ett fel (NPR-37811).
* Försök att ändra storlek på komponentlayouten i sidredigeraren fungerar inte i den mobila layouten (NPR-37805).
* Experience Fragment-översättning uppdaterar inte cykliska referenser till språkkopieringssökvägar (NPR-37745).
* När du använder ett cq-msm-lockbart RTF-fält i sidegenskaper inaktiveras inte fältet när sidan rullas ut och det kan ändras av författarna (NPR-37714).
* När ett upplevelsefragment aktiveras skickar utgivaren många aktiveringsbegäranden till Dispatcher (NPR-37707).
* Vid topologiändring återställs jobbet för att bearbeta resurser, vilket resulterar i att de jobb som pågår när topologiändringen görs ignoreras (NPR-37706).
* Citattecken, kors och streck exporteras inte till CSV när användare av MacOS exporterar webbplatser och mediematerial-URL:er (NPR-37698).
* Layoutbehållaren i SPA sidmall kan inte registrera de anpassade CSS-klasserna som definieras i mallprincipen när SPA reagerar på sidor (NPR-37697).
* Bakgrundsbilden syns inte när användaren väljer mål för ett upplevelsefragment som har en bakgrund i behållaren (NPR-37662).
* Översättningsjobbet på ett upplevelsefragment översätter inte alla komponenter på det upplevelsefragmentet (NPR-37660).
* Översättning av upplevelsefragment och sidan som innehåller upplevelsefragmentet uppdaterar inte startsökvägen i upplevelsefragmentlänken (NPR-37659).
* Widgeten Filöverföring visar inte filnamnet, när en fil överförs och dialogrutan sparas (NPR-37634).
* Den schemalagda aktiveringen (publiceringen) av tillgången utlöses inte vid den schemalagda tidpunkten om mappen som innehåller resursen flyttas (NPR-37621).
* [Plattform] Kontrollpanelen för externa länkar kan inte återge resultat i [!DNL Adobe Experience Manager] WCM (NPR-37614).
* Innehållsfragmentredigeraren fungerar inte korrekt när versala bokstäver används i taggnamn när taggar redigeras i redigeraren (NPR-37601).
* Klassisk redigerare för användargränssnittet visar inte markering som i jämförelsevisning av pekanvändargränssnittet (NPR-37588).
* Tillfälligt 500-fel loggas när ett upplevelsefragment läggs till i översättningsjobb (NPR-37587).
* Författare kan välja och använda datumväljardatum även om datumväljaren är inaktiverad (NPR-37583).
* [Foundation] Författare kan inte ange vissa decimalvärden i nummerfältets resurstyp i en komponentdialogrutestruktur för beröringsanvändargränssnittet (NPR-37059).
* Sökvägarna i mappen libs tas bort när tidigare Service Pack installeras (NPR-36815).
* [Handel] Inaktiveringen av en rotmapp ändrar inte inaktiveringsstatusen för underordnade produkter i [!DNL Experience Manager Commerce] konsol, Dessutom visas antalet undermappar i en rotmapp vid tidpunkten för inaktiveringen felaktigt i användargränssnittet (CQ-4338261).
* [Lokaliseringsarbetsflöde] Innehållet för kolumnanpassning och anpassning av varumärkning finns inte i dialogrutan Administratörskontroll - om du väljer ikonen under profilikonen i [!DNL Adobe Experience Manager] inbox (CQ-4334864).
* [Communities] Det går inte att klicka på innehållet i tabellen för gruppmedlemmar (CQ-4334404).
* [Oak] Synkroniseringsprocessen i kalla vänteläge fungerar inte och loggningsfel (CQ-433868).
* [Plattformsbasens användargränssnitt] [!DNL Experience Manager] startsidan visas igen när användaren väljer [!DNL Adobe Experience Manager] -ikonen finns redan på startsidan (CQ-4317409).

### [!DNL Assets] {#assets-65120}

<!--
The following accessibility enhancements are available in [!DNL Assets]:

* enhancement 1
-->

Följande problem har åtgärdats i [!DNL Assets]:

* När du lägger till en resurs eller mapp (som innehåller `single quote` i namnet) i Anslutna resurser misslyckas referenssökvägen och resulterar som ett undantag (NPR-37712).
* När du lägger till en vattenstämpel i en resurs visas vattenstämpeln alltid i svart färg oavsett vilken färg användaren har definierat (NPR-37720).
* När du använder anslutna resurser kan en icke-adminanvändare söka efter en resurs även när icke-adminanvändare är begränsade till åtkomst till DAM-databasen (NPR-37644).
* När du uppdaterar metadata för resurser med hjälp av massredigering sparas inte ändringarna som används i listrutefälten och återställs till standardvärdena (NPR-37345).
* Om du tar bort en mapp som tar för lång tid vilket påverkar den övergripande prestandan (NPR-37107).
* När användaren tillämpar regler i metadataschemat kan användaren inte visa hela värdet för listrutan `Field Value` och `Field Choices` om värdet är större än textrutan (CQ-4338074).
* När du har uppgraderat till version 6.5.10.0 visar sidan med resursegenskaper ett återgivningsmeddelande i onödan HTML (CQ-4336994).
* Sortera resurserna i `List View` fungerar inte effektivt (CQ-4335298).
* När du delar resurser med hjälp av en delad länk hämtas resurserna i separata mappar (CQ-4335000).
* Vid verifiering av [!DNL Experience Manager] `Inbox` inställningar, `Share` och `Out of office` -flikar återspeglar oöversatt innehåll (CQ-4334858).

* Följande korrigeringar är relaterade till överlappande metadata i resursegenskaper.
   * En obligatorisk listruta visar flera felmeddelanden för varje markering i fältet för flera värden (NPR-37859).
   * Endast det sista urvalet av det överordnade fältet sparas för det beroende icke-redigerbara fältet (NPR-37858).
   * Den beroende listrutan (fältet för flera värden) visar standardvärdet för den valda överordnade listrutan (NPR-37791).


### [!DNL Dynamic Media] {#dynamic-media-65120}

Följande problem har åtgärdats i [!DNL Dynamic Media]:

* Resurserna i en mapp som innehåller `renditions` i mappnamnet är inte synkroniserat i `Dynamic Media` (CQ-4338428).
* När du skapar en bildförinställning i `tiff` format, skapas förinställningen men formatet ändras till `jpeg` (CQ-4335985).
* När du ändrar `Progressive JPEG Scan` värdet i bildförinställningsredigeraren återställs alltid listrutans värde till `auto`(CQ-4335971).
* Videometadata är inte synliga för `mxf` videor på sidan med resursegenskaper (CQ-4335499).
* När videoresurserna bearbetas på nytt avpubliceras AVS-filerna (Adaptive Video Set) och videoåtergivningarna från publiceringsservern (CQ-4335461).
* De PDF-miniatyrbilder som skapas skiljer sig från den första sidan i PDF. Vissa delar av bilden saknas i miniatyrbilden (CQ-431554).
* CDN-ogiltigförklaring misslyckas med ett felaktigt URL-svar om `companyName` och `companyRoot` är annorlunda (CQ-4339896).

### Arbetsflöden {#workflows-65120}

* Rullning fungerar inte som förväntat om du använder filter på inkorgsobjekt (CQ-4333594).


### [!DNL Forms] {#forms-65120}


>[!NOTE]
>
>* [!DNL Experience Manager Forms] släpper tilläggspaketen en vecka efter den schemalagda [!DNL Experience Manager] Lanseringsdatum för Service Pack.


<!--

**Adaptive Forms**

* Accessibility – When you set the `Wizard` layout for a panel in an adaptive form, the navigation buttons do not have Aria labels and role (NPR-37613).

* Validations on a date field in an adaptive form does not work, as expected (NPR-37556).

* When the label text for the Checkbox and Radio Button components is long, the text does not fit appropriately (NPR-37294).

* When you apply styling changes to the Thank You message of the AEM Forms Container component, the changes do not replicate in the source adaptive form (NPR-37284).

* Differences in the value of the `Switch` component on the user interface and in the backend (NPR-37268).

* When you use the keyboard keys to navigate to the `Submit` option and press the `Enter` key, you can submit the adaptive form multiple times (CQ-4333993).

* The Remove operation for the File Attachment component does not work, as expected (NPR-37376).

* When a label for a field exceeds 1000 characters in an adaptive form that translates to various languages, the dictionary fails to retrieve the translation of the label (CQ-4329290).

**Document Services**

* An error displays while using the Assembler service (NPR-37606):

  ```TXT
    500 Internal Server Error
  ```

* When the document attachments are passed to the Assembler service, the following exception displays (NPR-37582):

  ```TXT
    com.adobe.livecycle.assembler.client.ProcessingException: ⁪: Failed to execute the DDX
  ```

* Missing closing parenthesis from data after converting a PDF document to a PDF-A/1B PDF document (NPR-37608).

**HTML5 Forms**

* When you install AEM 6.5.10.0, the HTML preview for an XDP form does not work (NPR-37503, CQ-4331926).

* Text overlapping issues while migrating the PDF forms to HTML 5 forms in various languages (NPR-37173).

**Letters**

* When you submit a letter and reopen it in HTML view, the position of text document fragments does not remain the same (NPR-37307).

**Forms Workflow**

* In case of embedded container workflow, you get multiple workflow completion emails even after selecting the `Notify on Complete of Container Workflow` option (NPR-37280).

**Foundation JEE**

* After installing AEM 6.5 Forms Service Pack 9, the CRX repository URLs are no longer available (NPR-37592).

**Issues fixed in AEM Forms 6.5.11.1**

>[!NOTE]
>
>If you have not upgraded to AEM 6.5.11.0 Forms, install the AEM Forms 6.5.11.1 add-on package directly. If you have installed AEM 6.5.11.0 Forms, Adobe recommends to upgrade to AEM 6.5.11.1 Forms.

* Submit actions, Send Email and Invoke an AEM Workflow stop working after installing the Forms 6.5.11.0 add-on package.
* CreatePDF operation stops converting Microsoft Word documents to PDF documents after installing the Forms 6.5.11.0 add-on package.
* (JEE Only) Critical security vulnerabilities (CVE-2021-44228 and CVE-2021-45046) reported for Apache Log4j2.
* (JEE only) Assembler DSC in 6.5.11.0 patch contains incorrect metainfo like specification version and impl version.

-->


Mer information om säkerhetsuppdateringar finns i [[!DNL Experience Manager] säkerhetsbulletinsida](https://helpx.adobe.com/security/products/experience-manager.html).

## Installera 6.5.12.0 {#install}

**Installationskrav och mer information**

* Experience Manager 6.5.12.0 kräver Experience Manager 6.5. Se [uppgraderingsdokumentation](/help/sites-deploying/upgrade.md) för detaljerade anvisningar.
* Service Pack-nedladdning finns på Adobe [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* På en distribution med MongoDB och flera instanser installerar du Experience Manager 6.5.12.0 på en av författarinstanserna med hjälp av Package Manager.

>[!NOTE]
>
>Adobe rekommenderar inte att du tar bort eller avinstallerar [!DNL Adobe Experience Manager] 6.5.12.0-paket.

### Installera Service Pack {#install-service-pack}

Installera Service Pack på en [!DNL Adobe Experience Manager] 6.5-instansen gör du så här:

1. Starta om instansen innan installationen om instansen är i uppdateringsläge (när instansen uppdaterades från en tidigare version). Adobe rekommenderar att du startar om om den aktuella upptiden för en instans är hög.

1. Ta en ögonblicksbild eller en ny säkerhetskopia av din [!DNL Experience Manager] -instans.

1. Hämta Service Pack från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.12.0.zip).

1. Öppna Pakethanteraren och klicka på **[!UICONTROL Upload Package]** för att överföra paketet. Mer information finns på [Pakethanteraren](/help/sites-administering/package-manager.md).

1. Markera paketet och klicka på **[!UICONTROL Install]**.

1. Om du vill uppdatera S3-anslutningen stoppar du instansen efter installationen av Service Pack, byter ut den befintliga kopplingen mot en ny binär fil som finns i installationsmappen och startar om instansen. Se [Amazon S3 - datalager](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Dialogrutan för pakethanterarens gränssnitt avslutas ibland när Service Pack installeras. Adobe rekommenderar att du väntar på att felloggarna ska stabiliseras innan du får åtkomst till distributionen. Vänta på de specifika loggarna för avinstallationen av uppdateringspaketet innan du försäkrar dig om att installationen lyckas. Vanligtvis inträffar detta problem i [!DNL Safari] webbläsare, men kan ibland inträffa i vilken webbläsare som helst.

**Automatisk installation**

Det finns två sätt att installera automatiskt [!DNL Experience Manager] 6.5.12.0 på en fungerande instans:

S. Placera paketet i `../crx-quickstart/install` när servern är tillgänglig online. Paketet installeras automatiskt.

B. Använd [HTTP-API från Package Manager](/help/sites-administering/package-manager.md#package-share). Använd `cmd=install&recursive=true` så att de kapslade paketen installeras.

>[!NOTE]
>
>Adobe Experience Manager 6.5.12.0 stöder inte installation av Bootstrap.

**Validera installationen**

1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience Manager (6.5.12.0)` under [!UICONTROL Installed Products].

1. Alla OSGi-paket är antingen **[!UICONTROL ACTIVE]** eller **[!UICONTROL FRAGMENT]** i OSGi Console (Use Web Console: `/system/console/bundles`).

1. OSGi-paketet `org.apache.jackrabbit.oak-core` är version 1.2.2.3 eller senare (Använd webbkonsol: `/system/console/bundles`).

Om du vill veta vilka plattformar som är certifierade för att fungera med den här versionen kan du läsa [tekniska krav](/help/sites-deploying/technical-requirements.md).

<!-- 

### Install Adobe Experience Manager Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Skip if you are not using Experience Manager Forms. Fixes in Experience Manager Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

1. Ensure that you have installed the Adobe Experience Manager Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>Experience Manager 6.5.10.0 includes a new version of [AEM Forms Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases). If you are using an older version of AEM Forms Compatibility Package and updating to Experience Manager 6.5.10.0, install the latest version of the package post installation of Forms Add-On Package.

### Install Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Skip if you are not using AEM Forms on JEE. Fixes in Adobe Experience Manager Forms on JEE are delivered through a separate installer.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes](jee-patch-installer-65.md).

>[!NOTE]
>
>After installing the cumulative installer for Experience Manager Forms on JEE, install the latest Forms add-on package, delete the Forms add-on package from the `crx-repository\install` folder, and restart the server.

-->

### UberJar {#uber-jar}

UberJar för Experience Manager 6.5.12.0 finns i [Maven Central-arkivet](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.12/).

Information om hur du använder UberJar i ett Maven-projekt finns i [använda UberJar](/help/sites-developing/ht-projects-maven.md) och inkludera följande beroende i projektens POM:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.12</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar och andra tillhörande artefakter finns tillgängliga i Maven Central Repository i stället för i Adobe Public Maven-arkivet (`repo.adobe.com`). Huvudfilen för UberJar har bytt namn till `uber-jar-<version>.jar`. Så det finns ingen `classifier`, med `apis` som värdet, för `dependency` -tagg.

## Föråldrade funktioner {#removed-deprecated-features}

Nedan finns en lista över funktioner som är markerade som borttagna [!DNL Experience Manager] 6.5.7.0 Funktioner markeras som borttagna från början och senare i en framtida version. Ett alternativt alternativ anges.

Granska om du använder en funktion eller en funktion i en distribution. Planera också att ändra implementeringen så att ett alternativt alternativ används.

| Yta | Funktion | Ersättning |
|---|---|---|
| Integreringar | The **[!UICONTROL AEM Cloud Services Opt-In]** skärmen är föråldrad sedan [!DNL Experience Manager] och [!DNL Adobe Target] integreringen uppdateras i Experience Manager 6.5. Integreringen stöder Adobe Target Standard API. API använder autentisering via Adobe IMS och [!DNL Adobe I/O] och stöder Adobe Launch till instrumentets växande roll [!DNL Experience Manager] för analys och personalisering är anmälningsguiden funktionellt irrelevant. | Konfigurera systemanslutningar, Adobe IMS-autentisering och [!DNL Adobe I/O] integreringar via respektive [!DNL Experience Manager] molntjänster. |
| Anslutningar | Adobe JCR Connector för Microsoft® SharePoint 2010 och Microsoft® SharePoint 2013 är borttagen för Experience Manager 6.5. | Ej tillämpligt |

## Kända fel {#known-issues}

* När du installerar AEM 6.5 Service Pack 12 och försöker hämta status-ZIP-filen hämtar Experience Manager en skadad fil.

   >[!CAUTION]
   >
   >En ny version av indexdefinitionspaketet håller på att utvecklas. Länken nedan kommer att publiceras så snart den blir tillgänglig.
   >
   >Till dess ber vi dig kontakta kundtjänst för att få en snabbkorrigering.

   <!--
  Download and install [AEM Sites SEO Index Package](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/sites-seo-index-content-1.0.0.zip) on your AEM instance before downloading the ZIP file to resolve the issue.
  -->

   Ladda ned och installera AEM Sites SEO Index Package på din AEM innan du hämtar ZIP-filen för att lösa problemet.

* Som [!DNL Microsoft Windows Server 2019] stöder inte [!DNL MySQL 5.7] och [!DNL JBoss EAP 7.1], [!DNL Microsoft Windows Server 2019] stöder inte körklara installationer för [!DNL AEM Forms 6.5.10.0].

* Om du uppgraderar dina [!DNL Experience Manager] från version 6.5 till 6.5.10.0 kan du visa `RRD4JReporter` undantag i `error.log` -fil. Starta om instansen för att lösa problemet.

* Om du installerar [!DNL Experience Manager] 6.5 Service Pack 10 eller ett tidigare Service Pack på [!DNL Experience Manager] 6.5, runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) tas bort.
Om du vill hämta körtidskopian rekommenderar Adobe att du synkroniserar designtidskopian av den anpassade arbetsflödesmodellen med körtidskopian med hjälp av HTTP API:
   `<designModelPath>/jcr:content.generate.json`.

* Användare kan byta namn på en mapp i en hierarki i [!DNL Assets] och publicera en kapslad mapp i [!DNL Brand Portal]. Mappens namn uppdateras dock inte i [!DNL Brand Portal] tills rotmappen publiceras på nytt.

* När en användare väljer att konfigurera ett fält för första gången i ett adaptivt formulär visas inte alternativet att spara en konfiguration i egenskapsläsaren. Om du väljer att konfigurera ett annat fält i det adaptiva formuläret i samma redigerare åtgärdas problemet.

* Följande fel och varningsmeddelanden kan visas under installationen av Experience Manager 6.5.x.x:
   * &quot;När Adobe Target-integreringen har konfigurerats i Experience Manager med Target Standard API (IMS-autentisering) skapas felaktiga erbjudandetyper när Experience Fragments exporteras till Target. I stället för att skriva&quot;Experience Fragment&quot;/källa&quot;Adobe Experience Manager&quot; skapar Target flera erbjudanden med typen&quot;HTML&quot;/källa&quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Validering på serversidan av adaptiva formulär misslyckas när sammanställningsfunktioner som SUM, MAX och MIN används (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Aktiveringspunkten i en interaktiv Dynamic Media-bild syns inte när du förhandsvisar mediefilen via Shoppable Banner Viewer.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tidsgränsen överskreds i väntan på att reg.ändringen skulle slutföras utan registrering.

* När du försöker flytta/ta bort/publicera antingen innehållsfragment eller webbplatser/sidor uppstår ett problem när referenser till innehållsfragment hämtas, eftersom bakgrundsfrågan misslyckas. d.v.s. funktionen fungerar inte.
Du måste lägga till följande egenskaper i indexdefinitionsnoden för att se till att åtgärden fungerar korrekt: `/oak:index/damAssetLucene` (ingen omindexering krävs):

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## OSGi-paket och innehållspaket som ingår {#osgi-bundles-and-content-packages-included}

Följande textdokument listar de OSGi-paket och innehållspaket som ingår i [!DNL Experience Manager] 6.5.12.0:

* [Förteckning över OSGi-paket som ingår i Experience Manager 6.5.12.0](assets/65120_bundles.txt)

* [Förteckning över innehållspaket som ingår i Experience Manager 6.5.12.0](assets/65120_packages.txt)

## Begränsade webbplatser {#restricted-sites}

Dessa webbplatser är bara tillgängliga för kunder. Om du är kund och behöver åtkomst kontaktar du din kontoansvarige på Adobe.

* [Nedladdning av produkt på licensing.adobe.com](https://licensing.adobe.com/)
* Se [hur du kontaktar Adobe kundsupport](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] produktsida](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* [Prenumerera på produktuppdateringar med Adobe prioritet](https://www.adobe.com/subscription/priority-product-update.html)

