---
title: Versionsinformation för [!DNL Adobe Experience Manager] 6.5
description: Hitta versionsinformation, nyheter, installationsanvisningar och en detaljerad ändringslista för [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: a52311b9-ed7a-432e-8f35-d045c0d8ea4c
source-git-commit: 4035bfae6a525292ca71b182ebed2ac9839426b8
workflow-type: tm+mt
source-wordcount: '3027'
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
| Version | 6.5.21.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Typ | Service Pack-version |
| Datum | Torsdagen den 6 juni 2024 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Hämta URL | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Vad ingår i [!DNL Experience Manager] 6.5.21.0 {#what-is-included-in-aem-6521}

[!DNL Experience Manager] 6.5.21.0 innehåller nya funktioner, viktiga förbättringar som kunderna efterfrågat samt felkorrigeringar. Det innehåller även förbättringar av prestanda, stabilitet och säkerhet som släppts sedan den första tillgängligheten av 6.5 i april 2019. [Installera detta Service Pack](#install) på [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## Viktiga funktioner och förbättringar

<!-- * _6.5.21.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Några av de viktigaste funktionerna och förbättringarna i den här versionen är följande:

* Ett nytt och enklare att använda autentiseringsuppgifter för server-till-server-autentisering, vilket ersätter de befintliga JWT-autentiseringsuppgifterna (Service Account). (NPR-41994)

### [!DNL Assets]

#### Förbättringar

Nedan följer en lista över förbättringar som ingår i den här versionen:

* IPTC-fliken stöder nu [!UICONTROL Alt Text] och [!UICONTROL Extended Description] textfält. (ASSETS-34918)

#### Korrigeringar av hjälpmedel

Nedan följer en lista över tillgänglighetskorrigeringar i den här versionen:

* Om bearbetningsstatusen för en resurs är Misslyckad eller Metadata misslyckades fungerar inte beskrivningarna och ljudspårens användargränssnitt korrekt. (ASSETS-37281)
* När du sparar metadata för en resurs och försöker redigera den visas inte språknamnet. (ASSETS-37281)

<!-- ### [!DNL Forms]
* A -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Åtgärdade problem i Service Pack 21 {#fixed-issues}

### [!DNL Sites]{#sites-6521}

#### Tillgänglighet {#sites-accessibility-6521}

* The **[!UICONTROL Saved Searches]** etiketten är inte beständig. Platshållaren används som den enda visuella etiketten för ett textfält. (SITES-3050)

#### Administratörsgränssnitt{#sites-adminui-6521}

* När du klickar **[!UICONTROL Sites]** > **[!UICONTROL Core Core Components]** > **[!UICONTROL Properties]** > **[!UICONTROL Permissions]** tab > **[!UICONTROL Effective Permission]**, **Effektiva behörigheter** öppnas inte i. (SITES-17378)

<!-- #### Classic UI{#sites-classicui-6521} 

* A -->

#### [!DNL Content Fragments]{#sites-contentfragments-6521}

* Fixed the double include of the form elements. (SITES-21109)
* När du skapar ett innehållsfragment slutar knappen Stäng ibland att svara, vilket gör att hela sidan fryser och kräver en uppdatering av sidan för att stänga innehållsfragmentet. När det gäller problemet med att skapa en version skapar systemet en ny version av ett innehållsfragment. Problemet inträffar även när användaren inte har gjort några ändringar, bara genom att interagera med textredigeraren eller ett textfält. (SITES-21187)

#### [!DNL Content Fragments] - GRAPHQL API {#sites-graphql-api-6521}

* Vid uppgradering av Adobe Experience Manager från 6.5.19.0 till 6.5.20.0 är sökvägen `/libs/cq/graphql/sites/graphiql` togs bort. (SITES-20098)

<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6521}

* W -->

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6521}

* W -->

<!-- #### Core Backend{#sites-core-backend-6521}

* W -->

<!-- #### Core Components{#sites-core-components-6521}

* I -->

<!-- #### Campaign integration{#sites-campaign-integration-6521}

* A -->

#### Upplevelsefragment{#sites-experiencefragments-6521}

* utrullning av upplevelsefragment från `masters/language` till `country/language` uppdaterar inte korsreferenser. (SITES-21172)
* Mallar som inte bara anges i `cq:allowedTemplates`, men mallar som har `allowedPaths` som konfigurerats på mallnivå visas som alternativ när du skapar ett nytt Experience Fragment. (SITES-20855)

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6521}

* T -->

<!-- #### Launches{#sites-launches-6521} -->

<!-- DELETED MAY 22, 2024 FROM TOTAL RELEASE CANDIDATE ISSUES * The `sourceRootResource` configured in the Launch configuration within CRXDE Lite points to content that no longer exists, leading to a malfunction when attempts are made to delete launches. Delete launches even if the page is deleted or if the path is not the same. (SITES-20750) -->

#### MSM - Live-kopior{#sites-msm-live-copies-6521}

* Ersätta sidkomponenten för att lägga till tabbar i sidegenskaper. En av dem är sidkonfiguration och har en egenskap för att lägga till en URL för Experience Fragment. Länken som konfigurerats i sidegenskaperna för Experience Fragment ändras inte för språkkopior som skapats för den sidan. Den konfigurerade länken ska ändras med språkkopians URL. (SITES-19580)

#### Page Editor{#sites-pageeditor-6521}

* I redigeringsläget används en grå bakgrund inkonsekvent, vilket inte överensstämmer med färgkontraststandarden WCAG (Web Content Accessibility Guidelines). (SITES-20060)

### [!DNL Assets]{#assets-6521}

* Om en resurs publiceras till Brand Portal förblir publiceringsstatusen inkonsekvent. (ASSETS-36807)
* Resurser tas inte bort när du tar bort dem från en instans med ett API-anrop. (ASSETS-35131)
* När du försöker importera metadata kan du `question mark (?)` ersätter infogning av tecken på andra språk än engelska.  (ASSETS-35091)
* När `dc:title` egenskapen används med datatypsträng, resursinnehållsträdet fungerar inte korrekt efter installationen av Service Pack 6.5.19. (ASSETS-34684)
* Ett fel visas om det finns något specialtecken i namnet på en resurs. (ASSETS-33248)

#### [!DNL Dynamic Media]{#assets-dm-6521}

* I AEM 6.5.18 visas inte alla aktiveringspunkter som lagts till i en resurs när du redigerar aktiveringspunkter. Alla aktiveringspunkter fungerar dock i en publicerad resurs, men du kan inte redigera dem senare om det behövs. (ASSETS-33609)
* De senaste EPS-filerna som överförs genererar inte miniatyrer efter ombearbetningen. (ASSETS-32617)
* I Verktyg > Resurser > Publiceringsinställningar > fliken Begärandeattribut anger du `Width(px)` och `Height(px)` skiljer sig åt på spanska, italienska och portugisiska. De är inte justerade mot varandra för de här platserna. (ASSETS-31896)
* Från och med 1 maj 2024 upphörde Adobe Dynamic Media med stödet för följande:
   * SSL (Secure Socket Layer) 2.0
   * SSL 3.0
   * TLS (Transport Layer Security) 1.0 och 1.1
   * Följande svaga lärare i TLS 1.2:
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_RSA_WITH_AES_256_GCM_SHA384`
      * `TLS_RSA_WITH_AES_256_CBC_SHA256`
      * `TLS_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_AES_128_GCM_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
      * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`

### [!DNL Forms]{#forms-6521}

Korrigeringar i [!DNL Experience Manager] Forms levereras via ett separat tilläggspaket en vecka efter den schemalagda [!DNL Experience Manager] Lanseringsdatum för Service Pack. I det här fallet planeras AEM 6.5.21.0 Forms-tilläggspaketet för torsdagen den 13 juni 2024. En lista över Forms-korrigeringar och förbättringar har lagts till i det här avsnittet när utgåvan släppts.

<!-- #### [!DNL Adaptive Forms]

* THIS BUG WAS ALREADY REPORTED IN THE 6.5.20.0 RELEASE NOTES. IS IT NEEDED AGAIN IN THE 6.5.21.0 RELEASE NOTES? (AEM Forms on JEE Only) The PDF Generator service fails to enumerate the fonts available on the server. Consequently, the font selection panel on the Adobe PDF Settings page in the PDFG Admin UI remains empty, effectively preventing (un)embedding of chosen fonts. (FORMS-12095) -->


<!-- #### [!DNL Forms Designer] {#forms-designer-6521}

* W -->

### Foundation {#foundation-6521}

#### Apache Felix {#foundation-apachefelix-6521}

* Uppgraderingsproblem med AEM 6.5 Service Pack 19 (SP19) där programserverns kontextrotsökväg saknas för obehöriga begäranden till Apache Felix efter installation av SP19. Uppdatera till Apache Felix Web Management Console 4.9.8. (NPR-41933)

#### Campaign{#foundation-campaign-6521}

* AEM 6.5 Service Pack 15 genererar kontinuerliga felloggar med viktiga poster. Följande problem rapporterades:

   * 404 INFO-fel för saknad resurs på sökväg `/libs/granite/ui/content/shell/start.html`
   * Felloggpost för ett ohanterat SlingException på grund av `NullPointerException` på `CampaignsDataSourceServlet.java:147`

  Felloggarna ska inte fyllas med ofta förekommande och stora felposter, och AEM ska fungera utan problem med saknade resurser eller undantag. (CQ-4357064)

#### Cloud Service{#foundation-cloudservices-6521}

* Ta bort Google Guava från AEM Cloud Service. (CQ-4356436)

<!-- #### Communities {#foundation-communities-6521}

* U -->

<!-- #### Content distribution{#foundation-content-distribution-6521}

* T -->

#### Granit{#foundation-granite-6521}

* Du kan inte välja **Ta bort** eller **Ändra** utan **Bläddra** behörighet i konfigurationsläsaren. GRANITE-51002

#### Integreringar{#foundation-integrations-6521}

* Angående `cq-target-integration`, måste ta bort icke-testad användning av Google Guava. (CQ-4357101)
* Ersättning av autentiseringsuppgifter för tjänstkontot (JSON Web Token eller JWT) med autentiseringsuppgifterna för OAuth2 Server-till-Server (kallas även huvudkonton). (NPR-41994)
* Begäran om att skapa målgrupp misslyckas med konfigurationen av IMS (Identity Management System). (NPR-41888)
* När en kund försöker visa sidan Nyttolast visas inte innehållet korrekt på grund av en felaktig URL. Ett 404-fel visas. Felet uppstod om ett frågetecken saknas i URL:en, före frågeparametrarna. Det här problemet kräver att kunden infogar frågeteckensymbolen för att visa sidan Nyttolast korrekt. (NPR-41957)
* Ta bort kod och beroenden för Adobe Search &amp; Promote från AEM 6.5, som nådde slutet av livscykeln [September 2022 enligt meddelande](https://experienceleague.adobe.com/en/docs/discontinued/using/search-promote). (NPR-41855)

#### Lokalisering{#foundation-localization-6521}

* Textsträngen i mallredigeraren *`No video available.`* är inte lokaliserad. (SITES-13190)
* Sträng efter att en användare har aktiverats eller inaktiverats lokaliseras inte i **verktyg** > **Säkerhet** > **Användare** > *any_user_name* > **Aktivera** > **OK** och markera *any_user_name* > **Inaktivera** > **OK**. (NPR-41737)

#### Oak {#foundation-oak-6521}

* Prestandaregressionskorrigering - Undvik intervallfrågor på liknande villkor. (OAK-9481)

* Ny Oak-version är 1.2.20.

#### Plattform{#foundation-platform-6521}

* The `Unclosed resource resolver` fel inträffar för `com.day.cq.mailer.impl.DefaultMailService`. The `MessageGatewayService` klassen, som inte finns i lådan, användes utan en resurslösare. Problemet uppstod på alla sidor med en knapp för att skicka formulär som skickar ett e-postmeddelande med den här klassen. (NPR-41853)
* I **Om Adobe Experience Manager** år 2023 för copyrightinformation. (CQ-4356349)


<!-- #### Sling{#foundation-sling-6521}

* T -->

#### Översättning{#foundation-translation-6521}

* Ett problem med AEM 6.5.19 körklar översättningsstatus som inte uppdateras som förväntat vid start. När du har importerat en översatt fil till ett översättningsjobb som är associerat med en AEM start förväntades statusen ändras till `Approved`. I stället ändrades statusen till `Ready for Review`, vilket inte är förväntat. (NPR-41756)
* När du skapar flera konfigurationer och går till översättningskonfigurationerna visas inte alla Cloud Service i användargränssnittet. Endast de första 40 elementen/mapparna visas. Lös inläsning utlöses men inget mer innehåll läggs till. (NPR-41829)
* Förvrängda tecken uppstår om det finns japanska på sidan Behörigheter i Touch-användargränssnittet. (NPR-41794)
* AEM 6.5.14 och 6.5.9 skickar inte någon känslolägesikoner för översättning. (CQ-4357000)

#### Användargränssnitt{#foundation-ui-6521}

* In Tools > Security > Users > &lt;user_name> > Profiler, i **Redigera användarinställningar** dialogrutan stängs inte dialogrutan när du klickar på Avbryt. (NPR-41793)
* Graniten `pathfield` komponent vid `/libs/granite/ui/components/coral/foundation/form/pathfield` kan inte aktivera **[!UICONTROL Select]** när en resurs är markerad. När sökvägsfältet har öppnats och användaren har markerat kryssrutan för resursen, visas **[!UICONTROL Select]** knappen är inte aktiverad. Den ändras inte från grå till blå. (NPR-41970)
* Det finns ett problem med referensfältet CFM (Content Fragment Model) i AEM. Trots att CFM-referensfältet är inställt som obligatoriskt kan användare klicka på Spara för att spara innehåll med icke-CFM-värden i vissa scenarier. Knappen Spara bör vara nedtonad (inte tillgänglig). (NPR-41894)
* Standarddialogrutorna för Coral-användargränssnittet som använder `successresponse` åtgärden måste utlösa ett lyckat svar efter åtgärden. Men i AEM 6.5 Service Pack 19 anropas inte inläsningsåtgärden och inget meddelande visas. (NPR-41797)
* AEM meddelandelänkar fungerar inte i AEM 6.5 Service Pack 18. När du uppgraderar till Service Pack 18 fungerar inte AEM meddelandelänkar när du markerar meddelandena via meddelandeknappen. (NPR-41792)

<!-- #### WCM{#foundation-wcm-6521}

* T -->

#### Arbetsflöde{#foundation-workflow-6521}

* I AEM 6.5.18 uppstod upprepade fel vid borttagning från användarens metadatacache vid rensning. (NPR-41762)

## Installera [!DNL Experience Manager] 6.5.21.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.21.0 kräver [!DNL Experience Manager] 6.5. Se [uppgraderingsdokumentation](/help/sites-deploying/upgrade.md) för detaljerade anvisningar. <!-- UPDATE FOR EACH NEW RELEASE -->
* Service Pack-nedladdningen finns på Adobe [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip).
* På en distribution med MongoDB och flera instanser installerar du [!DNL Experience Manager] 6.5.21.0 på en av författarinstanserna med hjälp av Package Manager.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe rekommenderar inte att du tar bort eller avinstallerar [!DNL Experience Manager] 6.5.21.0-paket. Innan du installerar paketet bör du skapa en säkerhetskopia av `crx-repository` om du måste rulla tillbaka den. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Installera Service Pack på [!DNL Experience Manager] 6.5{#install-service-pack}

1. Starta om instansen innan installationen om instansen är i uppdateringsläge (när instansen uppdaterades från en tidigare version). Adobe rekommenderar att du startar om om den aktuella upptiden för en instans är hög.

1. Ta en ögonblicksbild eller en ny säkerhetskopia av din [!DNL Experience Manager] -instans.

1. Hämta Service Sack från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Öppna Pakethanteraren och välj **[!UICONTROL Upload Package]** för att överföra paketet. Mer information finns på [Pakethanteraren](/help/sites-administering/package-manager.md).

1. Markera paketet och välj **[!UICONTROL Install]**.

1. Om du vill uppdatera S3-anslutningen stoppar du instansen efter installationen av Service Pack, byter ut den befintliga kopplingen mot en ny binär fil som finns i installationsmappen och startar om instansen. Se [Amazon S3 - datalager](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Dialogrutan för pakethanterarens gränssnitt avslutas ibland när Service Pack installeras. Adobe rekommenderar att du väntar på att felloggarna ska stabiliseras innan du får åtkomst till distributionen. Vänta på de specifika loggarna för avinstallationen av uppdateringspaketet innan du försäkrar dig om att installationen lyckas. Vanligtvis inträffar det här problemet i [!DNL Safari] webbläsare, men kan då och då förekomma i vilken webbläsare som helst.

**Automatisk installation**

Det finns två olika metoder att installera [!DNL Experience Manager] 6.5.21.0<!-- UPDATE FOR EACH NEW RELEASE -->

* Placera paketet i `../crx-quickstart/install` när servern är tillgänglig online. Paketet installeras automatiskt.
* Använd [HTTP-API från Package Manager](/help/sites-administering/package-manager.md#package-share). Använd `cmd=install&recursive=true` så att de kapslade paketen installeras.

>[!NOTE]
>
>Experience Manager 6.5.21.0 stöder inte installation av Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validera installationen**

Om du vill veta vilka plattformar som är certifierade för att fungera med den här versionen kan du läsa [tekniska krav](/help/sites-deploying/technical-requirements.md).

1. Produktinformationssidan (`/system/console/productinfo`) visar den uppdaterade versionssträngen `Adobe Experience Manager (6.5.21.0)` under [!UICONTROL Installed Products]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Alla OSGi-paket är **[!UICONTROL ACTIVE]** eller **[!UICONTROL FRAGMENT]** i OSGi Console (Use Web Console: `/system/console/bundles`).

1. OSGi-paketet `org.apache.jackrabbit.oak-core` är version 1.2.20 eller senare (Använd webbkonsol: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installera Service Pack för [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Anvisningar om hur du installerar Service Pack på Experience Manager Forms finns i [Installationsanvisningar för Experience Manager Forms Service Pack](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>Funktionen Adaptive Forms, som finns i [AEM 6.5 QuickStart](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/deploying/deploying/deploy), är endast avsedd för prospektering och utvärdering. För produktion krävs en giltig licens för AEM Forms, eftersom Adaptive Forms-funktionaliteten kräver rätt licensiering.

### Installera GraphQL Index Package för Experience Manager Content Fragments{#install-aem-graphql-index-add-on-package}

Kunder som använder GraphQL måste installera [Experience Manager Content Fragment with GraphQL Index Package 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

På så sätt kan du lägga till den indexdefinition som krävs baserat på de funktioner som de faktiskt använder.

Om du inte installerar det här paketet kan GraphQL-frågor bli långsamma eller misslyckas.

>[!NOTE]
>
>Installera bara det här paketet en gång per instans. Det behöver inte installeras om med varje Service Pack.

### UberJar{#uber-jar}

UberJar för [!DNL Experience Manager] 6.5.21.0 finns i [Maven Central-arkivet](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.21/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Information om hur du använder UberJar i ett Maven-projekt finns i [använda UberJar](/help/sites-developing/ht-projects-maven.md) och inkludera följande beroende i projektens POM: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.21</version>
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

* När du försöker flytta, ta bort eller publicera antingen innehållsfragment, webbplatser eller sidor, uppstår ett problem när referenser till innehållsfragment hämtas. Bakgrundsfrågan misslyckas. Funktionen fungerar alltså inte.
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
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : Inga underhållsfönster hittades vid granit/drift/underhåll.
   * Den aktiva punkten i en interaktiv Dynamic Media-bild syns inte när du förhandsgranskar mediefilen via visningsprogrammet för den köpbara kanalen.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Timeout väntar på att registerändringen ska slutföras utan registrering.

* Från och med AEM 6.5.15, JavaScript-motorn i Rhino från ```org.apache.servicemix.bundles.rhino``` paket har ett nytt värdbeteende. Skript som använder strikt läge (```use strict;```) måste deklarera sina korrekta variabler. Annars körs de inte, vilket resulterar i ett körningsfel.

* Om du installerar taggning av relaterat innehåll som inte finns i kartongen med hjälp av ett officiellt uppdateringspaket återställs språkegenskapen för `/content/cq:tags` nod till standard. Den här åtgärden gäller för Service Packs, Security Service Pack, Extended Feature Packs, Cumulative Feature Packs, Patches osv. Det är därför nödvändigt att lägga till den från egenskaperna före installationen.

### Känt problem för AEM Sites {#known-issues-aem-sites-6521}

* SITES-17934 - Content Fragments - Preview misslyckas på grund av DoS-skydd för stora fragmentträd. Se [KB-artikel om standardkonfigurationsalternativ för GraphQL Query Executor](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23945)

### Kända fel för AEM Forms {#known-issues-aem-forms-6521}

* I ett adaptivt formulär som baseras på en XDP-fil med inbäddade skript i kryssrutor, körs inte skripten för element efter sådana kryssrutor. (FORMS-1424)
* Användarna kan inte skapa ett Correspondence Management-brev. När en användare skapar ett brev visas ett felmeddelande med beskrivningen`Object Object`&quot; visas och brevet skapas inte. Miniatyrbilder för layouter kan inte heller läsas in på skärmen där brevet skapas. Du kan installera [senaste AEM 6.5 Form Service Pack 20 (6.5.20.0)](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) för att lösa problemet. (FORMS-13496)
* Med tjänsten Interactive Communications skapas PDF-dokumentet, men användarens data fylls inte i automatiskt i formulärfälten. Förifyllningstjänsten fungerar inte som förväntat. Du kan installera [senaste AEM 6.5 Form Service Pack 20 (6.5.20.0)](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) för att lösa problemet. (FORMS-13413, FORMS-13493)
* Det går inte att läsa in RnC-redigeraren (Review and Correct) för en automated forms conversion-tjänst. Du kan installera [senaste AEM 6.5 Form Service Pack 20 (6.5.20.0)](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) för att lösa problemet. (FORMS-13491)
* Efter uppdatering från AEM 6.5 av Forms Service Pack 18 (6.5.18.0) eller AEM 6.5 av Forms Service Pack 19 (6.5.19.0) till AEM 6.5 av Forms Service Pack 20 (6.5.20.0) påträffas ett JSP-kompileringsfel. De kan inte öppna eller skapa anpassade formulär och de stöter på fel med andra AEM gränssnitt som sidredigeraren, AEM Forms gränssnitt och AEM Workflow editor. Du kan installera [senaste AEM 6.5 Form Service Pack 20 (6.5.20.0)](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) för att lösa problemet. (FORMS-13492)
* Rader i datumväljarwidgeten trunkeras när du går igenom flera månader i snabbwidgeten för fält med redigerings-/visningsmönster. (FORMS-13620)
* Det går inte att skicka formulär när DOR-tjänsten (Document of Record) används i serverdelen. Felmeddelandet som påträffades är: &quot;Det gick inte att skicka åtgärden eftersom formulärresursen inte är korrekt tilldelad.&quot; (FORMS-13798)
* När ett anpassat formulär skickas från en Adobe Experience Manager Publish-instans till ett Adobe Experience Manager-arbetsflöde, kan arbetsflödet inte spara de bifogade filerna. (FORMS-14209)
* När du installerar AEM 6.5 Forms Service Pack 20-paket (AEM Forms tilläggspaket för SP20) uppvisar AEM Sites användargränssnitt en avsevärd prestandaförsämring. (FORMS-13791)
* Förifyllningstjänsten misslyckas med ett null-pekarundantag i Interactive Communications. (CQDOC-21355)
* Med adaptiv Forms kan du använda anpassade funktioner med ECMAScript version 5 eller tidigare. När en anpassad funktion använder ECMAScript version 6 eller senare, som `let`, `const`eller pilfunktioner kanske inte regelredigeraren öppnas korrekt.

## OSGi-paket och innehållspaket som ingår{#osgi-bundles-and-content-packages-included}

Följande textdokument listar de OSGi-paket och innehållspaket som ingår i detta [!DNL Experience Manager] 6.5 Service Pack-version:

* [Förteckning över OSGi-paket i Experience Manager 6.5.21.0](/help/release-notes/assets/65210-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Förteckning över innehållspaket i Experience Manager 6.5.21.0](/help/release-notes/assets/65210-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Begränsade webbplatser{#restricted-sites}

Dessa webbplatser är bara tillgängliga för kunder. Om du är kund och behöver åtkomst kontaktar du din kontoansvarige på Adobe.

* [Nedladdning av produkt på licensing.adobe.com](https://licensing.adobe.com/)
* [Kontakta Adobe kundsupport](https://experienceleague.adobe.com/en/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] produktsida](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5-dokumentation](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [Prenumerera på produktuppdateringar för Adobe Priority](https://www.adobe.com/subscription/priority-product-update.html)
