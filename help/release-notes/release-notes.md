---
title: Versionsinformation för [!DNL Adobe Experience Manager] 6.5
description: Hitta versionsinformation, nyheter, installationsanvisningar och en detaljerad ändringslista för [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
source-git-commit: 156e83ad9f73e200da70f824b598a713c0e2e97f
workflow-type: tm+mt
source-wordcount: '2171'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] 6.5 Versionsinformation om senaste Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=WRAZ43&nav=MTVfezk2OTJDQTNFLUI4QTQtNDY2RS05NEVCLUQ5QjcyNEVENkJDNn0 -->

## Versionsinformation {#release-information}

| Produkt | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.16.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Typ | Service Pack-version |
| Date | Torsdagen den 23 februari 2023 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Hämta URL | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[..]be/packages/cq650/servicepack/aem-service-pkg-6.5.16.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Vad ingår i [!DNL Experience Manager] 6.5.16.0 {#what-is-included-in-aem-6516}

[!DNL Experience Manager] 6.5.16.0 innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat, felkorrigeringar, prestanda, stabilitet och säkerhetsförbättringar som släppts sedan den första tillgängligheten av 6.5 i april 2019. [Installera detta Service Pack](#install) på [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

En viktig förbättring i Dynamic Media är följande:

Det nya protokollet DASH (Dynamic Adaptive Streaming over HTTP) har startats för adaptiv strömning i Dynamic Media (med CMAF) [Gemensamt format för medieprogram] aktiverat).

* Adaptiv direktuppspelning (DASH/HLS) ger en bättre tittarupplevelse för videor.
* DASH är det internationella standardprotokollet för strömning av adaptiv video och är en vida spridd bransch.
* Finns nu i Nordamerika (via supportanmälan) som snart kommer i Asien-Stillahavsområdet och Europa-Mellanöstern-Afrika.

Se [Aktivera DASH på ditt konto](/help/assets/video.md#enable-dash).

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6516}

* Anslutna resurser: När du aktiverar alternativen för smart beskärning för bilder på fjärr-DAM, överför bilder till en mapp och synkroniserar mappen till lokala platser, öppnas inte mappen på den lokala platsdistributionen. (NPR-39912)
* När en samling sorteras efter namn fungerar listvyn inte korrekt (ASSETS-19401)
* När en stor mediefil (JPEG) överförs till samlingar slutar Experience Manager svara. (ASSETS-19387)
* I innehållsträdets ruta är det visade resursnamnet felaktigt eftersom resursens plats inte återges korrekt. (ASSETS-18870)
* När du delar en samling med hjälp av en länk matchar inte data i URL-adressen mellan kortvyns och listvyns sammanslagning. (ASSETS-18758)
* När du utför en sökning med ett filter för mapptypen blir sökresultaten inkonsekventa. (ASSETS-18227)
* The `dam:size` egenskapen uppdateras inte efter XMP tillbakaskrivning, vilket resulterar i att felaktig information returneras från `/platform/path/to/asset.jpg;resource=metadata` API. (ASSETS-17631)
* Resurslösaren som inte stängts för alla Experience Manager-instanser. (ASSETS-16904)
* Det går inte att skapa en version för en resurs även om du har tilldelats `create` och `modify` behörigheter. (ASSETS-15956)
* The `move` -knappen inaktiveras slumpmässigt när en resurs flyttas från en punkt till en annan. (ASSETS-14889)
* Skärmläsare kan inte identifiera rubriker eftersom texten inte är definierad i rubriktaggar utan som allmän text. (ASSETS-6924)
* Den alternativa texten under bilden är inte obligatorisk, men texten som visas under bilden är upprepad med en `Type` -attribut. (ASSETS-6915)


## [!DNL Assets] - [!DNL Dynamic Media] {#dm-6516}

* Formulärelementet innehåller ingen etikett. I skärmläsare som NVDA och JAWS presenteras inte etikettinformation korrekt. (CQ-4344078)
* Listrutor stängs inte när `Escape` -tangenten används på ett tangentbord. (CQ-4344077)
* Informationsikonen (bokstaven&quot;i&quot;) som visas för det infogade felförslaget efter att en ogiltig inmatning har angetts går inte att komma åt med ett tangentbord. (CQ-4344076)
* `getManifestURI` returnerar null på grund av att en JCR-egenskap läses som `toString` i stället för `getString`. (ASSETS-18674)
* SmartCrop-videokomponenten fungerar inte korrekt. Komponenten utför uppspelning i stället för direktuppspelning, och VTT-anrop misslyckas, vilket ger ett 404-fel. (ASSETS-18468)
* Markera **[!UICONTROL Properties]** på en medias visningsprogramsida orsakar ett null-pekarundantag. (ASSETS-18420)
* [!DNL Experience Manager] ändringar i användargränssnittet för DASH-direktuppspelning som inkluderar följande:
   * som har ett synligt CMAF-fält (Common Media Application Format) i videoprofilsredigeraren.
   * om du vill att videoöverföringen ska skicka en CMAF-flagga.
   * alternativen **[!UICONTROL auto]**, **[!UICONTROL hls]** och **[!UICONTROL dash]** finns nu i listrutan för uppspelning i redigeraren för visningsförinställningar **[!UICONTROL Behavior]** -fliken.
(ASSETS-17428)
* I Navigering, när du väljer **[!UICONTROL Assets]** > **[!UICONTROL Files]** > **[!UICONTROL Create]** > **[!UICONTROL Carousel Set]**&#x200B;är bildikonen överlappad med textsträngen &quot;Bild 1&quot;. (ASSETS-18578)
* Opublicerade resurser publiceras igen. (ASSETS-16428)
* Skribenten i Experience Manager går ned på grund av ett inläsningsproblem som kräver att en syntetisk avisering skapas. (ASSETS-15937)
* På sidan Allmänna inställningar i Dynamic Media visas ett oöversatt felmeddelande `Failed to fetch data` visas. (ASSETS-15617)

## [!DNL Forms] {#forms-6516}

>[!NOTE]
>
>Korrigeringar i [!DNL Experience Manager] Forms levereras via ett separat tilläggspaket en vecka efter den schemalagda [!DNL Experience Manager] Lanseringsdatum för Service Pack. I detta fall kommer tilläggspaketen att släppas torsdagen den 2 mars 2023. Dessutom har en lista med korrigeringar och förbättringar för Forms lagts till i det här avsnittet.

<!--
### [!DNL Forms] Fixes {#forms-fixes-6516}
-->

## Integreringar {#integrations-6516}

* Ta bort Adobe Search &amp; Promote-kod och beroenden från Experience Manager 6.5. Adobe Search &amp; Promote nådde slutet av sin tjänst september 2022. Se [Adobe Search &amp; Promote meddelande om att tjänsten upphör](https://experienceleague.adobe.com/docs/discontinued/using/search-promote.html?lang=en). (NPR-39706)

## [!DNL Sites] {#sites-6516}

* Aktuell `cq-wcm-core` artifabriken har inte POM. (SITES-10983)
* Åtgärden Förhandsvisa utrullning ska inte visa sidan som ska skapas. (SITES-10355, CQ-4266213)
* Utlöses när MSM-frikopplingen återskapar den frånkopplade sidan. (SITES-9841)
* Tidsgränsen för att starta programmet har överskridits. användaren måste vänta många minuter på en inläsningsskärm innan begäran tids ut. (SITES-9051)
* Användargränssnittet Rollout Page visar överordnade sidsökvägar som inte finns. Du kan rulla ut sidan med ett meddelande om att det lyckades, men den underordnade sidan introduceras inte eftersom den överordnade sidan aldrig introducerades. (SITES-8621)

### [!DNL Sites] - Kärnkomponenter {#sites-core-components-6516}

* Centralisera länkhanteringen på e-postsidor så att modellanpassningar inte längre behövs. (SITES-9002)

### [!DNL Sites] - Administratörsgränssnitt {#sites-adminui-6516}

* CSV-export exporterar inte alla sidor under den valda sidan. (SITES-9390)

### [!DNL Sites] - [!DNL Content Fragments] {#sites-contentfragments-6516}

* Det går inte att skriva ut ett innehålls-JSON. Orsaken är att GraphQL-frågan inte kan genereras när du öppnar innehållsfragmentets förhandsgranskningssida. (SITES-8619)
* När Content Fragment Model Editor öppnas igen **[!UICONTROL Date and Time]** fälten är som standard av typen Datum och tid. (SITES-8401)

### [!DNL Sites] - [!DNL Experience Fragments] {#sites-experiencefragments-6516}

* Du kan inte flytta ett Experience Fragment till en annan mapp även om mallen finns under tillåtna mallar. (SITES-8601)
* (SITES-7989)


### [!DNL Sites] - sidredigeraren {#sites-pageeditor-6516}

* Uppdatera beroenden för resurslösarförbättringen som gjordes i SITES-8464 där sidåtergivning i redigeringsläge skapade ett stort antal `TemplatedResourceImpl` objekt. (SITES-9350)


## Sling {#sling-6516}

* Experience Manager är dödläget vid start. (NPR-39832)
* När det finns många ovanlighetssökvägar i Experience Manager version-lagringsutrymmet kan Experience Manager inte startas. (NPR-38955)


## Översättningsprojekt {#translation-6516}

* I `MicrosoftTranslationServiceImpl`, frågesträngsparametern `Category` är felaktigt. (NPR-39828)
* Om du skapar ett översättningsprojekt visas felet *Överordnad sidresurs finns inte*; översättningsprojektet inte skapas. (NPR-39762)
* Det går inte att ange ett förfallodatum i ett översättningsprojekt som använder en mänsklig översättningskoppling. (NPR-39593)

## Användargränssnitt {#ui-6516}

* När du ändrar till en lägre upplösning visas inte DatePicker och AM/PM-markeringen visas eller ändras inte synligt. (NPR-39948)
* När minify js (minimering av JavaScript) används bearbetas inte minifieringen på grund av ett tolkningsfel. (NPR-39650)
* Taggfält (`/libs/cq/gui/components/coral/common/form/tagfield`) står i konflikt med tidslinjen. (CQ-4350751)


## WCM {#wcm-6516}

* Åtgärden Förhandsvisa utrullning ska inte visa sidan som ska skapas. (CQ-4266213, SITES-10355)

## Arbetsflöde {#workflow-6516}

* Ta bort den redigerbara arbetsflödesmodellen manuellt från `/conf` lämnar en kvarvarande instans av körningsmodellen utan någon redigerbar modell. (CQ-4349365)


## Installera [!DNL Experience Manager] 6.5.16.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.16.0 kräver [!DNL Experience Manager] 6.5. Se [uppgraderingsdokumentation](/help/sites-deploying/upgrade.md) för detaljerade anvisningar. <!-- UPDATE FOR EACH NEW RELEASE -->
* Service Pack-nedladdning finns på Adobe [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* På en distribution med MongoDB och flera instanser installerar du [!DNL Experience Manager] 6.5.16.0 på en av författarinstanserna med hjälp av Package Manager.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe rekommenderar inte att du tar bort eller avinstallerar [!DNL Experience Manager] 6.5.16.0-paket. Innan du installerar paketet bör du skapa en säkerhetskopia av `crx-repository` om du behöver rulla tillbaka den. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for AEM Forms, see [AEM Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Installera Service Pack på [!DNL Experience Manager] 6.5 {#install-service-pack}

1. Starta om instansen innan installationen om instansen är i uppdateringsläge (när instansen uppdaterades från en tidigare version). Adobe rekommenderar att du startar om om den aktuella upptiden för en instans är hög.

1. Ta en ögonblicksbild eller en ny säkerhetskopia av din [!DNL Experience Manager] -instans.

1. Hämta Service Pack från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Öppna Pakethanteraren och välj **[!UICONTROL Upload Package]** för att överföra paketet. Mer information finns på [Pakethanteraren](/help/sites-administering/package-manager.md).

1. Markera paketet och välj **[!UICONTROL Install]**.

1. Om du vill uppdatera S3-anslutningen stoppar du instansen efter installationen av Service Pack, byter ut den befintliga kopplingen mot en ny binär fil som finns i installationsmappen och startar om instansen. Se [Amazon S3 - datalager](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Dialogrutan för pakethanterarens gränssnitt avslutas ibland när Service Pack installeras. Adobe rekommenderar att du väntar på att felloggarna ska stabiliseras innan du får åtkomst till distributionen. Vänta på de specifika loggarna för avinstallationen av uppdateringspaketet innan du försäkrar dig om att installationen lyckas. Vanligtvis inträffar detta problem i [!DNL Safari] webbläsare, men kan ibland inträffa i vilken webbläsare som helst.

**Automatisk installation**

Det finns två olika metoder som du kan använda för att installera automatiskt [!DNL Experience Manager] 6.5.16.0<!-- UPDATE FOR EACH NEW RELEASE -->

* Placera paketet i `../crx-quickstart/install` när servern är tillgänglig online. Paketet installeras automatiskt.
* Använd [HTTP-API från Package Manager](/help/sites-administering/package-manager.md#package-share). Använd `cmd=install&recursive=true` så att de kapslade paketen installeras.

>[!NOTE]
>
>Experience Manager 6.5.16.0 stöder inte installation av Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validera installationen**

Om du vill veta vilka plattformar som är certifierade för att fungera med den här versionen kan du läsa [tekniska krav](/help/sites-deploying/technical-requirements.md).

1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience Manager (6.5.16.0)` under [!UICONTROL Installed Products]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Alla OSGi-paket är antingen **[!UICONTROL ACTIVE]** eller **[!UICONTROL FRAGMENT]** i OSGi Console (Use Web Console: `/system/console/bundles`).

1. OSGi-paketet `org.apache.jackrabbit.oak-core` är version 1.2.2.14 eller senare (Använd webbkonsol: `/system/console/bundles`). <!-- NPR-39939 for 6.5.16.0 --> <!-- NPR-39436 for 6.5.15.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installera Service Pack för [!DNL Experience Manager] Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Hoppa över om du inte använder [!DNL Experience Manager] Forms.

Korrigeringar i [!DNL Experience Manager] Forms levereras via ett separat tilläggspaket en vecka efter den schemalagda [!DNL Experience Manager] Service Pack-version.

<!-- 

For instructions to install the service pack on AEM Forms, see [AEM Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).
-->

### UberJar {#uber-jar}

UberJar för [!DNL Experience Manager] 6.5.16.0 finns i [Maven Central-arkivet](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.15/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>I Experience Manager 6.5.16.0 är UberJar-versionen (6.5.15.0) densamma som i den tidigare versionen.


Information om hur du använder UberJar i ett Maven-projekt finns i [använda UberJar](/help/sites-developing/ht-projects-maven.md) och inkludera följande beroende i projektens POM: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.15</version>
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
| Integreringar | The **[!UICONTROL AEM Cloud Services Opt-In]** skärmen är föråldrad sedan [!DNL Experience Manager] och [!DNL Adobe Target] integreringen uppdateras i [!DNL Experience Manager] 6.5. Integreringen stöder Adobe Target Standard API. API:t använder autentisering via Adobe IMS och [!DNL Adobe I/O Runtime]. Det stöder den växande rollen för Adobe Launch till instrument [!DNL Experience Manager] för analys och personalisering är anmälningsguiden funktionellt irrelevant. | Konfigurera systemanslutningar, Adobe IMS-autentisering och [!DNL Adobe I/O Runtime] integreringar via respektive [!DNL Experience Manager] molntjänster. |
| Anslutningar | Adobe JCR Connector för Microsoft® SharePoint 2010 och Microsoft® SharePoint 2013 är föråldrad för [!DNL Experience Manager] 6.5. | Ej tillämpligt |

## Kända fel {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* [AEM innehållsfragment med GraphQL indexpaket 1.0.5](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip)
Detta paket behövs för kunder som använder GraphQL; på så sätt kan de lägga till den indexdefinition som behövs baserat på de funktioner de faktiskt använder.

* Uppdatera dina GraphQL-frågor som kan ha använt ett anpassat API-namn för innehållsmodellen till att använda standardnamnet för innehållsmodellen i stället.

* Som [!DNL Microsoft® Windows Server 2019] stöder inte [!DNL MySQL 5.7] och [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] stöder inte körklara installationer för [!DNL AEM Forms 6.5.10.0].

* Om du uppgraderar [!DNL Experience Manager] från 6.5.0 till 6.5.4 till senaste Service Pack på Java™ 11, se `RRD4JReporter` undantag i `error.log` -fil. Starta om instansen av [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Användare kan byta namn på en mapp i en hierarki i [!DNL Assets] och publicera en kapslad mapp i [!DNL Brand Portal]. Mappens namn uppdateras dock inte i [!DNL Brand Portal] tills rotmappen publiceras på nytt.

* När en användare väljer att konfigurera ett fält för första gången i ett adaptivt formulär visas inte alternativet att spara en konfiguration i egenskapsläsaren. Om du väljer att konfigurera ett annat fält i det adaptiva formuläret i samma redigerare åtgärdas problemet.

* Följande fel och varningsmeddelanden kan visas under installationen av [!DNL Experience Manager] 6.5.x.x:
   * &quot;När Adobe Target-integreringen är konfigurerad i [!DNL Experience Manager] med Target Standard API (IMS-autentisering) och sedan exportera Experience Fragments till Target så att fel erbjudandetyper skapas. I stället för att skriva&quot;Experience Fragment&quot;/källa&quot;Adobe Experience Manager&quot; skapar Target flera erbjudanden med typen&quot;HTML&quot;/källa&quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Validering på serversidan av adaptiva formulär misslyckas när sammanställningsfunktioner som SUM, MAX och MIN används (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Aktiveringspunkten i en interaktiv Dynamic Media-bild syns inte när du förhandsvisar mediefilen via Shoppable Banner Viewer.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tidsgränsen överskreds i väntan på att registerändringen skulle slutföras utan registrering.

* När du försöker flytta/ta bort/publicera antingen innehållsfragment eller webbplatser/sidor uppstår ett problem när referenser till innehållsfragment hämtas, eftersom bakgrundsfrågan misslyckas. d.v.s. funktionen fungerar inte.
Du måste lägga till följande egenskaper i indexdefinitionsnoden för att få en korrekt åtgärd `/oak:index/damAssetLucene` (ingen omindexering krävs):

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## OSGi-paket och innehållspaket som ingår {#osgi-bundles-and-content-packages-included}

Följande textdokument listar de OSGi-paket och innehållspaket som ingår i [!DNL Experience Manager] 6.5.16.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Förteckning över OSGi-paket som ingår i Experience Manager 6.5.16.0](/help/release-notes/assets/65160_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Förteckning över innehållspaket som ingår i Experience Manager 6.5.16.0](/help/release-notes/assets/65160_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Begränsade webbplatser {#restricted-sites}

Dessa webbplatser är bara tillgängliga för kunder. Om du är kund och behöver åtkomst kontaktar du din kontoansvarige på Adobe.

* [Nedladdning av produkt på licensing.adobe.com](https://licensing.adobe.com/)
* [Kontakta Adobe kundsupport](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] produktsida](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* [Prenumerera på produktuppdateringar med Adobe prioritet](https://www.adobe.com/subscription/priority-product-update.html)

