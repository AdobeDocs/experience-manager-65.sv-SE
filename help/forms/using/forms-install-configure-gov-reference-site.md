---
title: Konfigurera referenswebbplatsen för Web.Gov och We.Finance
seo-title: Konfigurera referenswebbplatsen för Web.Gov
description: Installera, konfigurera och anpassa ett AEM Forms-demopaket.
seo-description: Installera, konfigurera och anpassa ett AEM Forms-demopaket.
uuid: 0a6ad8f9-0d38-40c3-ad8d-e705edef55f8
contentOwner: anujkapo
discoiquuid: fe5da0aa-d3a8-4b77-a447-9e429fdc2816
docset: aem65
translation-type: tm+mt
source-git-commit: 0560eb8e3c127964920827609a9982acf07b515f
workflow-type: tm+mt
source-wordcount: '4728'
ht-degree: 1%

---


# Konfigurera referenswebbplatsen för Web.Gov och We.Finance {#set-up-and-configure-we-gov-reference-site}

## Information om demopaket {#demo-package-details}

### Installationskrav {#installation-prerequisites}

Paketet skapades för **AEM Forms 6.4 OSGI Author**, har testats och stöds därför i följande plattformsversioner:

| AEM | AEM FORMS PACKAGE VERSION | STATUS |
|---|---|---|
| 6.4 | 5.0.86 | **Stöds** |
| 6.5 | 6.0.80 | **Stöds** |
| 6.5.3 | 6.0.122 | **Stöds** |

Paketet innehåller en molnkonfiguration som stöder följande plattformsversioner:

| MOLNLEVERANTÖR | SERVICEVERSION | STATUS |
|---|---|---|
| Adobe Sign | v5 API | **Stöds** |
| Microsoft Dynamics 365 | 1710 (9.1.0.3020) | **Stöds** |
| Adobe Analytics | v1.4 Rest API | **Stöds** |
**Paketinstallationshänsyn:**

* Paketet förväntas installeras på en ren server, utan andra demopaket eller äldre versioner av demopaket
* Paketet förväntas installeras på en OSGI-server som körs i redigeringsläge

### Vad innehåller det här paketet {#what-does-this-package-include}

[AEM Forms We.Gov demo package](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/we-gov-forms.pkg.all-2.0.2.zip) (**we-gov-forms.pkg.all-&lt;version>.zip**) levereras som ett paket som innehåller flera andra underpaket och tjänster. Paketet innehåller följande moduler:

* **we-gov-forms.pkg.all-&lt;version>.zip** -  *Komplett demopaket*

   * **we-gov-forms.ui.apps-&lt;version>.zip** *- Innehåller alla komponenter, klientbibliotek, exempelanvändare, arbetsflödesmodeller osv.*

      * **we-gov-forms.core-&lt;version>.jar** -  *Innehåller alla OSGI-tjänster, anpassad implementering av arbetsflödessteg osv.*

      * **we-gov-forms.derby&lt;version>.jar** -  *Innehåller alla OSGI-tjänster, databasschema osv.*

      * **core.wcm.components.all-2.0.4.zip** -  *Samling av WCM-exempelkomponenter*

      * **grid-aem.ui.apps-1.0-SNAPSHOT.zip** -  *AEM Sites Grid layout package for Sites page column control*
   * **we-gov-forms.ui.content-&lt;version>.zip** -  *Innehåller allt innehåll, alla sidor, bilder, formulär, interaktiva kommunikationsresurser osv.*

   * **we-gov-forms.ui.analytics-&lt;version>.zip** -  *Innehåller alla Web.Gov Forms Analytics-data som ska lagras i databasen.*

   * **we-gov-forms.config.public-&lt;version>.zip** -  *Innehåller alla standardkonfigurationsnoder, inklusive platshållarmolnkonfigurationer för att undvika formulärdatamodell och tjänstbindningsproblem.*


De tillgångar som ingår i detta paket omfattar:

* AEM webbplatssidor med redigerbara mallar
* AEM Forms Adaptive Forms
* AEM Forms Interactive Communications (Print and Web Channel)
* AEM Forms XDP-dokument för inspelning
* AEM Forms MS Dynamics Forms datamodell
* Adobe Sign Integration
* AEM arbetsflödesmodell
* AEM Assets exempelbilder
* Exempel (i minnet) på Apache Derby-databas
* Apache Derby-datakälla (för användning med formulärdatamodell)

## Installation av demopaket {#demo-package-installation}

Det här avsnittet innehåller information om hur du installerar demopaketet.

### Från programvarudistribution {#from-software-distribution}

1. Öppna [Programvarudistribution](https://experience.adobe.com/downloads). Du behöver en Adobe ID för att logga in på Software Distribution.
1. Tryck på **[!UICONTROL Adobe Experience Manager]** som finns i rubrikmenyn.
1. I avsnittet **[!UICONTROL Filters]**:
   1. Välj **[!UICONTROL Forms]** i listrutan **[!UICONTROL Solution]**.
   2. Välj version och typ för paketet. Du kan också använda alternativet **[!UICONTROL Search Downloads]** för att filtrera resultaten.
1. Tryck på **we-gov-forms.pkg.all-&lt;version>.zip** paketnamn, välj **[!UICONTROL Accept EULA Terms]** och tryck på **[!UICONTROL Download]**.
1. Öppna [Pakethanteraren](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) och klicka på **[!UICONTROL Upload Package]** för att överföra paketet.
1. Markera paketet och klicka på **[!UICONTROL Install]**.

   ![webbforum](assets/wegov_forms_package.jpg)

1. Tillåt att installationsprocessen slutförs.
1. Gå till *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html?wcmmode=disabled* för att kontrollera att installationen lyckades.

### Från en lokal ZIP-fil {#from-a-local-zip-file}

1. Hämta och hitta filen **we-gov-forms.pkg.all-&lt;version>.zip**.
1. Gå till *https://&lt;aemserver>:&lt;port>/crx/packmgr/index.jsp*.
1. Välj alternativet &quot;Överför paket&quot;.

   ![Överför paket](assets/upload_package.jpg)

1. Använd filläsaren för att navigera till och välja den hämtade ZIP-filen.
1. Klicka på Öppna för att överföra.
1. När du har överfört paketet väljer du alternativet Installera för att installera det.

   ![Installera Forms-paketet för WebGov](assets/wegov_forms_package-1.jpg)

1. Tillåt att installationsprocessen slutförs.
1. Gå till *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html?wcmmode=disabled* för att kontrollera att installationen lyckades.

### Installerar nya paketversioner {#installing-new-package-versions}

Installera den nya paketversionen genom att följa stegen i 4.1 och 4.2. Det går att installera en nyare paketversion medan ett annat äldre paket redan är installerat, men du bör avinstallera den äldre paketversionen först. Gör så här:

1. Navigera till *https://&lt;aemserver>:&lt;port>/crx/packmgr/index.jsp*
1. Leta reda på den äldre filen **we-gov-forms.pkg.all-&lt;version>.zip**.
1. Välj alternativet &quot;Mer&quot;.
1. I listrutan väljer du alternativet Avinstallera.

   ![Avinstallera WebGov-paket](assets/uninstall_wegov_forms_package.jpg)

1. När du har bekräftat väljer du Avinstallera igen och tillåter att avinstallationen slutförs.

## Konfiguration av demonstrationspaket {#demo-package-configuration}

Det här avsnittet innehåller information och instruktioner om konfigurationen efter distributionen av demopaketet innan presentationen.

### Konfiguration för praktisk användare {#fictional-user-configuration}

1. Navigera till *https://&lt;aemserver>:&lt;port>/libs/granite/security/content/groupadmin.html*
1. Logga in som administratör för att utföra uppgifterna nedan.
1. Bläddra ned till slutet av sidan om du vill läsa in alla användargrupper.
1. Sök efter **arbetsflöde**.
1. Markera gruppen &quot;**workflow-users**&quot; och klicka på &quot;Properties&quot;.
1. Gå till fliken Medlemmar.
1. Skriv in **wegov** i fältet Välj användare eller grupp.
1. Välj i listrutan &quot;**We.Gov Forms Users**&quot;.

   ![Redigera gruppinställningar för arbetsflödesanvändare](assets/edit_group_settings.jpg)

1. Klicka på&quot;Spara och stäng&quot; i menyraden.
1. Upprepa steg 2-7 genom att söka efter &quot;**analys**&quot;, markera gruppen &quot;**Analysadministratörer**&quot; och lägga till gruppen &quot;**Web.Gov Forms Users**&quot; som medlem.
1. Upprepa steg 2-7 genom att söka efter &quot;**formuläranvändare**&quot;, markera gruppen &quot;**forms-power-users**&quot; och lägga till gruppen &quot;**We.Gov Forms Users**&quot; som medlem.
1. Upprepa steg 2-7 genom att söka efter &quot;**forms-users**&quot;, markera gruppen &quot;**forms-users**&quot; och den här gången lägga till gruppen &quot;**We.Gov Users**&quot; som medlem.

### E-postserverkonfiguration {#email-server-configuration}

1. Granska installationsdokumentationen [Konfigurera e-postmeddelande](/help/sites-administering/notification.md)
1. Logga in som administratör för att utföra den här uppgiften.
1. Navigera till *https://&lt;aemserver>:&lt;port>/system/console/configMgr*
1. Leta upp och klicka på tjänsten **Day CQ Mail Service** för att konfigurera.

   ![Konfigurera daglig CQ Mail-tjänst](assets/day_cq_mail_service.jpg)

1. Konfigurera tjänsten så att den ansluter till valfri SMTP-server:

   1. **SMTP-servervärdnamn**: t.ex. (smtp.gmail.com)
   1. **Serverport**: t.ex. (465) för gmail med SSL
   1. **SMTP-användare:** demo@  &lt;companyname> .com
   1. **&quot;Från&quot;-adress**: aemformsdemo@adobe.com

   ![Konfigurera SMTP](assets/configure_smtp.jpg)

1. Klicka på Spara för att spara konfigurationen.

### (Valfritt) AEM SSL-konfiguration {#aemsslconfig}

Det här avsnittet innehåller information om hur du konfigurerar SSL på AEM för att kunna konfigurera Adobe Sign Cloud-konfigurationen.

**Referenser:**

1. [SSL som standard](/help/sites-administering/ssl-by-default.md)

**Anteckningar:**

1. Gå till https://&lt;port>/aem/inbox där du kan slutföra processen som beskrivs i länken för referensdokumentation ovan.
1. Paketet `we-gov-forms.pkg.all-[version].zip` innehåller ett exempel på en SSL-nyckel och ett certifikat som du kan komma åt genom att extrahera mappen `we-gov-forms.pkg.all-[version].zip/ssl` som ingår i paketet.

1. SSL-certifikat och nyckelinformation:

   1. utfärdas till &quot;CN=localhost&quot;
   1. 10 års giltighet
   1. lösenordsvärde för password
1. Den privata nyckeln är *localhostprivate.der*.
1. Certifikatet är *localhost.crt*.
1. Klicka på Nästa.
1. HTTPS-värdnamn ska anges till *localhost*.
1. Porten bör anges till en port som systemet har exponerat.

### (Valfritt) Adobe Sign molnkonfiguration {#adobe-sign-cloud-configuration}

Det här avsnittet innehåller information och instruktioner om Adobe Sign Cloud-konfigurationen.

**Referenser:**

1. [Integrera Adobe Sign med AEM Forms](adobe-sign-integration-adaptive-forms.md)

#### Molnkonfiguration {#cloud-configuration}

1. Granska förutsättningarna. Se [AEM SSL-konfiguration](../../forms/using/forms-install-configure-gov-reference-site.md#aemsslconfig) för nödvändig SSL-konfiguration.
1. Navigera till:

   *https://&lt;aemserver>:&lt;port>/libs/adobesign/cloudservices/adobesign.html/conf/we-gov*

   >[!NOTE]
   >
   >Den URL som används för att komma åt AEM ska matcha den URL som konfigurerats i Adobe Sign OAuth Redirect URI för att undvika konfigurationsproblem (t.ex. *https://&lt;aemserver>:&lt;port>/mnt/overlay/adobesign/cloudservices/adobesign/properties.html*)

1. Välj konfigurationen &quot;We.gov Adobe Sign&quot;.
1. Klicka på &quot;Egenskaper&quot;.
1. Gå till fliken Inställningar.
1. Ange autentiserings-URL, t.ex.: [https://secure.na1.echosign.com/public/oauth](https://secure.na1.echosign.com/public/oauth)
1. Ange konfigurerat klient-ID och klienthemlighet från den konfigurerade Adobe Sign-instansen.
1. Klicka på&quot;Anslut till Adobe Sign&quot;.
1. När anslutningen är klar klickar du på Spara och stäng för att slutföra integreringen.

### (Valfritt) MS Dynamics molnkonfiguration {#ms-dynamics-cloud-configuration}

Det här avsnittet innehåller information och instruktioner om konfigurationen för MS Dynamics Cloud.

**Referenser:**

1. [Microsoft Dynamics OData-konfiguration](https://docs.adobe.com/content/help/en/experience-manager-64/forms/form-data-model/ms-dynamics-odata-configuration.html)
1. [Konfigurerar Microsoft Dynamics för AEM Forms](https://helpx.adobe.com/experience-manager/kt/forms/using/config-dynamics-for-aem-forms.html)

#### MS Dynamics OData-molntjänsten {#ms-dynamics-odata-cloud-service}

1. Navigera till:

   https://&lt;aemserver>:&lt;port>/libs/fd/fdm/gui/components/admin/fdmcloudservice/fdm.html/conf/we-gov

   1. Se till att du använder samma omdirigerings-URL som konfigurerats i MS Dynamics-programregistreringen.

1. Markera konfigurationen för Microsoft Dynamics OData-Cloud Service.
1. Klicka på &quot;Egenskaper&quot;.

   ![Egenskaper för Microsoft OData-Cloud Service](assets/properties_odata_cloud_service.jpg)

1. Gå till fliken Autentiseringsinställningar.
1. Ange följande information:

   1. **Tjänstrot:** t.ex. https://msdynamicsserver.api.crm3.dynamics.com/api/data/v9.1/
   1. **Autentiseringstyp:** OAuth 2.0
   1. **Autentiseringsinställningar**  (se  [konfigurationsinställningar för ](../../forms/using/forms-install-configure-gov-reference-site.md#dynamicsconfig) MS Dynamics för att samla in den här informationen):

      1. Klient-ID - även kallat program-ID
      1. Klienthemlighet
      1. OAuth URL - t.ex. [https://login.windows.net/common/oauth2/authorize](https://login.windows.net/common/oauth2/authorize)
      1. Uppdatera token-URL - t.ex. [https://login.windows.net/common/oauth2/token](https://login.windows.net/common/oauth2/token)
      1. Åtkomsttoken-URL - t.ex. [https://login.windows.net/common/oauth2/token](https://login.windows.net/common/oauth2/token)
      1. Auktoriseringsomfång - **openid**
      1. Autentiseringshuvud - **auktoriseringsansvarig**
      1. Resurs - t.ex. [https://msdynamicsserver.api.crm3.dynamics.com](https://msdynamicsserver.api.crm3.dynamics.com)
   1. Klicka på Anslut till OAuth.


1. När autentiseringen är klar klickar du på Spara och stäng för att slutföra integreringen.

#### Konfigurationsinställningar för MS Dynamics-molnet {#dynamicsconfig}

Stegen som beskrivs i det här avsnittet finns för att hjälpa dig att hitta klient-ID, klienthemlighet och information från din MS Dynamics Cloud-instans.

1. Navigera till [https://portal.azure.com/](https://portal.azure.com/) och logga in.
1. Välj Alla tjänster på den vänstra menyn.
1. Sök efter eller navigera till&quot;App Registration&quot;.
1. Skapa eller välj en befintlig programregistrering.
1. Kopiera **program-ID** som ska användas som OAuth **klient-ID** i AEM molnkonfiguration
1. Klicka på Inställningar eller Manifest för att konfigurera **Reply URL:er.**

   1. Den här URL:en måste matcha den URL som används för att komma åt AEM när OData-tjänsten konfigureras.

1. I inställningsvyn klickar du på&quot;Tangenter&quot; för att visa den nya nyckeln (som används som klienthemlighet i AEM).

   1. Se till att behålla en kopia av nyckeln eftersom du inte kan visa den senare i Azure eller AEM.

1. Navigera till MS Dynamics-instansens kontrollpanel för att hitta resurs-URL:en/tjänstens rot-URL.
1. I det övre navigeringsfältet klickar du på&quot;Försäljning&quot; eller på din egen instanstyp och&quot;Välj inställningar&quot;.
1. Klicka på&quot;Anpassningar&quot; och&quot;Resurser för utvecklare&quot; längst ned till höger.
1. Där hittar du Service Root URL: t.ex.

   *[https://msdynamicsserver.api.crm3.dynamics.com/api/data/v9.1/](https://msdynamicsserver.api.crm3.dynamics.com/api/data/v9.1/)*

1. Information om URL:en för uppdaterings- och åtkomsttoken finns här:

   *[https://docs.microsoft.com/en-us/rest/api/datacatalog/authenticate-a-client-app](https://docs.microsoft.com/en-us/rest/api/datacatalog/authenticate-a-client-app)*

#### Testar Forms datamodell (Dynamics) {#testing-the-form-data-model}

När molnkonfigurationen är klar kanske du vill testa formulärdatamodellen.

1. Navigera till

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments-fdm/we-gov*

1. Välj &quot;We.gov Microsoft Dynamics CRM FDM&quot; och välj &quot;Properties&quot;.

   ![Egenskaper för Dynamics CRM FDM](assets/properties_dynamics_crm.jpg)

1. Gå till fliken Uppdatera källa.
1. Kontrollera att Kontextmedveten konfiguration är inställd på /conf/we-gov och att den konfigurerade datakällan är ms-dynamics-data-cloud-service.

   ![Konfigurerad datakälla](assets/configured_data_source.jpg)

1. Redigera formulärdatamodellen.

1. Testa tjänsterna för att kontrollera att de är anslutna till den konfigurerade datakällan.

   >[!NOTE]
   När du har testat tjänsterna klickar du på **Avbryt** för att se till att ofrivilliga ändringar inte sprids till formulärdatamodellen.

   >[!NOTE]
   Det har rapporterats att en AEM Server måste startas om för att datakällan ska kunna bindas till FDM.

#### Testar Forms datamodell (Derby) {#test-fdm-derby}

När molnkonfigurationen är klar kanske du vill testa formulärdatamodellen.

1. Navigera till *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments-fdm/we-gov*

1. Välj **We.gov Enrollment FDM** och välj **Egenskaper**.

   ![Egenskaper för Dynamics CRM FDM](assets/aftia-enrollment-fdm.jpg)

1. Gå till fliken **Uppdatera källa**.

1. Kontrollera att **Kontextmedveten konfiguration** är `/conf/we-gov` och att den konfigurerade datakällan är **We.Gov Derby DS**.

   ![Egenskaper för Dynamics CRM FDM](assets/aftia-update-data-source.jpg)

1. Klicka på **Spara och stäng**.

1. [Testa ](work-with-form-data-model.md#test-data-model-objects-and-services) tjänsterna för att kontrollera att de är anslutna till den konfigurerade datakällan

   * Om du vill testa anslutningen väljer du **HOMEMORTGAGEACCOUNT** och ger den en get-tjänst. Testa tjänsten och systemadministratörerna för att se data som hämtas.

### Adobe Analytics-konfiguration (valfritt) {#adobe-analytics-configuration}

Det här avsnittet innehåller information och instruktioner om Adobe Analytics Cloud Configuration.

**Referenser:**

* [Integrera med Adobe Analytics](../../sites-administering/adobeanalytics.md)

* [Ansluta till Adobe Analytics och skapa ramverk](../../sites-administering/adobeanalytics-connect.md)

* [Visa sidanalysdata](../../sites-authoring/pa-using.md)

* [Konfigurera analyser och rapporter](configure-analytics-forms-documents.md)

* [Visa och förstå AEM Forms analysrapporter](view-understand-aem-forms-analytics-reports.md)

### Adobe Analytics molntjänstkonfiguration {#adobe-analytics-cloud-service-configuration}

Det här paketet levereras förkonfigurerat för att ansluta till Adobe Analytics. Följ stegen nedan för att tillåta att konfigurationen uppdateras.

1. Navigera till *https://&lt;aemserver>:&lt;port>/libs/cq/core/content/tools/cloudservices.html*
1. Gå till Adobe Analytics och välj länken &quot;Visa konfigurationer&quot;.
1. Välj konfigurationen &quot;Web.Gov Adobe Analytics (Analytics Configuration)&quot;.

   ![Konfiguration av molntjänster för Analytics](assets/analytics_config.jpg)

1. Klicka på knappen&quot;Redigera&quot; för att uppdatera Adobe Analytics-konfigurationen (du måste ange den delade hemligheten). Klicka på Anslut till analys för att ansluta och OK för att slutföra.

   ![We.Gov Adobe Analytics](assets/wegov_adobe_analytics.jpg)

1. På samma sida klickar du på&quot;We.Gov Adobe Analytics Framework (Analytics Framework)&quot; om du vill uppdatera ramverkskonfigurationerna (se [Aktivera AEM](../../forms/using/forms-install-configure-gov-reference-site.md#enableauthoring) för redigering).

#### Adobe Analytics Locating User Credentials {#analytics-locating-user-credentials}

Kontoadministratören måste utföra följande uppgifter för att kunna hitta inloggningsuppgifterna för ett Adobe Analytics-konto.

1. Gå till Adobe Experience Cloud-portalen.
   * Logga in med dina administratörsuppgifter
1. Välj ikonen Adobe Analytics på huvudkontrollpanelen.
   ![Snabb åtkomst](assets/aftia-quick-access.jpg)
1. Navigera till fliken Admin och markera alternativet Användarhantering (äldre)
   ![Rapporter](assets/aftia-reports.jpg)
1. Välj fliken **Användare**.
   ![Användarhantering](assets/aftia-user-management.jpg)
1. Välj önskad användare i listan över användare.
1. Rulla längst ned på sidan så visas inloggningsinformationen längst ned på sidan.
   ![Hantera åtkomst](assets/aftia-admin-user-access.jpg)
1. Användarnamnet och den delade hemliga informationen visas till höger om behörighetsrutan.
1. Observera att användarnamnet kommer att ha ett kolon i namnet. All information till vänster om kolonet är användarnamnet, och all information till höger om kolonet kommer att vara företagsnamnet.
   * Här är ett exempel: *användarnamn: företagsnamn*

#### Konfigurera användarautentisering i Adobe Analytics {#setup-user-authentication}

Administratörer kan ge användare AEM analysbehörigheter genom att utföra följande åtgärder.

1. Gå till Adobe Admin Console.

1. Klicka på den Analytics-instans som visas för Admin Console.

   * Detta finns på administratörsidans huvudsida.

1. Välj fullständig administratörsåtkomst för Analytics.

1. Lägg till en användare i profilen.

   ![Fullständig administratörsåtkomst för Analytics](assets/aftia-full-admin-access.jpg)

1. Klicka på fliken Behörigheter när användar-ID:t har mappats till profilen.

1. Kontrollera att alla behörigheter är mappade till profilen.

   ![Redigera behörigheter](assets/aftia-admin-access-edit.jpg)

1. Observera att när behörigheterna har mappats kan det ta några timmar för en användare att logga in.

### Adobe Analytics rapporterar {#adobe-analytics-reporting}

#### Visa rapporter om Adobe Analytics-webbplatser {#view-adobe-analytics-sites-reporting}

>[!NOTE]
AEM Forms Analytics-data är tillgängliga offline eller utan en Adobe Analytics-molnkonfiguration om `we-gov-forms.ui.analytics-<version>.zip`-paketet är installerat, men AEM Sites-data kräver en aktiv molnkonfiguration.

1. Navigera till *https://&lt;aemserver>:&lt;port>/sites.html/content*
1. Välj&quot;AEM Forms Web.Gov Site&quot; för att visa webbplatssidorna.
1. Välj en av webbplatssidorna (t.ex. Hem) och välj&quot;Analytics &amp; Recommendations&quot;.

   ![Analys och Recommendations](assets/analytics_recommendations.jpg)

1. På den här sidan ser du hämtad information från Adobe Analytics som gäller AEM Sites (Obs! den här informationen uppdateras regelbundet från Adobe Analytics och visas inte i realtid).

   ![AEM Sites-analys](assets/sites_analysis.jpg)

1. På sidan för sidvisning (som du kommer åt i steg 3.0) kan du även visa sidvisningsinformationen genom att ändra visningsinställningen så att objekt i listvyn visas.
1. Leta upp listrutan Visa och välj Listvy.

   ![Listvy](assets/list_view.jpg)

1. På samma meny väljer du &quot;Visningsinställning&quot; och markerar de kolumner som du vill visa under &quot;Analys&quot;.

   ![Konfigurera kolumner](assets/configure_columns.jpg)

1. Klicka på Uppdatera för att göra de nya kolumnerna tillgängliga.

   ![Visa nya kolumner](assets/new_columns_display.jpg)

#### Visa Adobe Analytics-formulärrapportering {#view-adobe-analytics-forms-reporting}

>[!NOTE]
AEM Forms Analytics-data är tillgängliga offline eller utan en Adobe Analytics-molnkonfiguration om `we-gov-forms.ui.analytics-<version>.zip`-paketet är installerat, men AEM Sites-data kräver en aktiv molnkonfiguration.

1. Navigera till

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. Välj anpassningsformuläret &quot;Registreringsprogram för hälsoförmåner&quot; och välj alternativet &quot;Analysrapport&quot;.

   ![Analysrapport](assets/analytics_report.jpg)

1. Vänta tills sidan har lästs in och visa analysrapportdata.

   ![Visa analysrapportdata](assets/analytics_report_data.jpg)

### Aktivera automatisk Forms-konfiguration för Adobe {#automated-forms-enablement}

För att installera och konfigurera AEM Forms med Adobe Forms måste användare av konverteringsverktyget ha följande:

1. Tillgång till Adobe I/O.

1. Behörighet att skapa en integrering med Adobe Forms Conversion-tjänsten.

1. Adobe AEM 6.5 senaste Service Pack som körs som författare.

Läs mer här:

* [Konfigurera den automatiserade konverteringstjänsten för formulär](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/configure-service.html)

#### Skapar en IMS-konfigurationsdel 1 {#creating-ims-config}

För att kunna konfigurera tjänsten så att den kommunicerar korrekt med formulärkonverteringsverktyget måste användarna konfigurera tjänsten Identity Management System (IMS) så att den kan registreras hos Adobe I/O.

1. Navigera till https://&lt;aemserver>:&lt;port> > Klicka på Adobe Experience
Ansvarig överst till vänster > Verktyg > Säkerhet > Adobe IMS-konfiguration.

1. Klicka på Skapa.

1. Utför åtgärderna i bilden nedan.

   ![Konfiguration av IMS-konto](assets/aftia-technical-account-configuration.jpg)

1. Glöm inte att hämta certifikatet.

1. Fortsätt inte med resten av konfigurationen - gå igenom avsnittet [Skapa integrering i Adobe I/O](#create-integration-adobeio)

>[!NOTE]
Certifikatet som skapas i det här avsnittet kommer att användas för att skapa integreringstjänsten i Adobe I/O. När användarna har skapat integreringstjänsten kan de använda informationen från Adobe I/O för att slutföra konfigurationen.

#### Skapar integrering i Adobe I/O {#create-integration-adobeio}

Se till att du har möjlighet att skapa en integrering inom din Adobe-domän om du inte kontaktar systemadministratören för att göra det.

1. Navigera till [Adobe I/O-konsolen](https://console.adobe.io/).

1. Klicka på Skapa integrering.

1. Välj Åtkomst till ett API.

1. Se till att du är i rätt grupp (den övre högra listrutan).

1. I sektionen Experience Cloud väljer du Forms Conversion Tool.

1. Klicka på Fortsätt.

1. Ange integreringens namn och beskrivning.

1. Använd den publika nyckeln från Avsnitt 2.1 för att placera den i integreringen av nyckeln.

1. Välj en profil för automated forms conversion.

   ![Skapa ny integrering](assets/aftia-create-new-integration.jpg)

#### Skapar IMS-konfigurationsdel 2 {#create-ims-config-part-next}

Nu när du har skapat en integrering kan vi slutföra installationen av IMS-konfigurationen.

1. Klicka på integreringen i Adobe I/O för att visa anslutningsinformationen.

1. Navigera till din IMS-konfiguration i AEM (Verktyg > Säkerhet > IMS)

1. Klicka på Nästa på skärmen IMS-konfiguration.

1. Ange auktoriseringsservern (värdet visas på skärmbilden).

1. Ange API-nyckeln.

1. Ange klienthemligheten (måste klicka på exponera på integreringen i Adobe I/O för att den ska visas).

1. Klicka på JWT-fliken i Adobe I/O för att hämta JWT-nyttolasten och klistra in den i nyttolasten för IMS-konfigurationen.

   ![IMS-konfiguration för nyttolast](assets/aftia-payload-ims-config.jpg)

1. Klicka på IMS-konfigurationen och välj Hälsokontroll för att se följande resultat.

   ![Hälsobekräftelse](assets/aftia-health-confirmation.jpg)

#### Konfigurera molnkonfiguration (Web.Gov AFC-produktion) {#configure-cloud-configuration}

När IMS-konfigurationen är klar kan vi gå vidare och granska molnkonfigurationen i AEM. Om konfigurationen inte finns skapar du molnkonfigurationen i AEM enligt följande:

1. Öppna webbläsaren och gå till system-URL:en https://&lt;domän_namn>:&lt;system_port>

1. Klicka på Adobe Experience Manager längst upp till vänster på skärmen > Verktyg > Cloud Services > Automatiserad Forms-konversationskonfiguration.

1. Markera konfigurationsmappen som du vill montera konfigurationen i.

1. Klicka på Skapa.

1. Ange informationen i skärmbilden nedan.

   ![AFC-produktion](assets/aftia-afc-production.jpg)

1. Ange en titel och ett namn för konfigurationen.

1. Tjänst-URL:en för systemet är inställd på https://aemformsconversion.adobe.io/.

1. Mallens URL */conf/we-gov/settings/wcm/templates/we-gov-flamingo-template*.

1. Temats-URL: */content/dam/formsanddocuments-themes/adobe-gov-forms-themes/we-gov-theme*

1. Klicka på Nästa.

1. För den här konfigurationen lämnade vi de två värdena för kryssrutorna tomma.

   * Mer information om de här alternativen finns i [Konfigurera molntjänsten](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/configure-service.html#configure-the-cloud-service).

#### Konfigurera molnkonfiguration (Web.Finance AFC Production) {#configure-cloud-configuration-wefinance}

När IMS-konfigurationen är klar kan vi fortsätta att skapa molnkonfigurationen i AEM.

1. Öppna webbläsaren och gå till system-URL:en https://&lt;domän_namn>:&lt;system_port>

1. Klicka på Adobe Experience Manager längst upp till vänster på skärmen > Verktyg > Cloud Services > Automatiserad Forms-konversationskonfiguration.

1. Markera konfigurationsmappen som du vill montera konfigurationen i.

1. Klicka på Skapa.

1. Ange informationen i skärmbilden nedan.

   ![Web.Finance AFC Production](assets/aftia-wefinance-afc-prod.jpg)

1. Ange en titel och ett namn för konfigurationen.

1. Tjänst-URL:en för systemet är inställd på https://aemformsconversion.adobe.io/

1. Mall-URL: */conf/we-Finance/settings/wcm/templates/we-Finance-adaptive-form*

1. Temats-URL: */content/dam/formsanddocuments-themes/adobe-Finance-forms-themes/we-Finance-theme*

1. Klicka på Nästa.

1. För den här konfigurationen lämnade vi de två värdena för kryssrutorna tomma.

   * Mer information om de här alternativen finns i [Konfigurera molntjänsten](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/configure-service.html#configure-the-cloud-service).

#### Testa formulärkonverteringen (programmet för registrering hos Web.Gov) {#test-forms-conversion}

När konfigurationen är klar kan användarna testa den genom att ladda upp ett PDF-dokument.

1. Navigera till AEM https://&lt;domän_namn>:&lt;system_port>

1. Klicka på Forms > Forms &amp; Documents > AEM Forms Web.gov Forms > AFC.

1. Välj PDF-filen till registreringsprogrammet Web.GOV.

1. Klicka på knappen **Starta automatisk konvertering** i det övre högra hörnet.

1. Användarna ska kunna se alternativet som visas nedan.

   ![Konverterat adaptivt formulär](assets/aftia-converted-adaptive-form.jpg)

1. När knappen har valts visas följande alternativ för användarna

   * Se till att användarna väljer konfigurationen *Web.Gov AFC Production*

   ![Konverteringsinställningar](assets/aftia-conversion-settings.jpg)

   ![Avancerade konverteringsinställningar](assets/aftia-conversion-settings-2.jpg)

1. Välj att starta konverteringen när du har konfigurerat alla alternativ som du vill använda.

1. När konverteringsprocessen börjar bör användarna se följande skärm:

   ![Konverteringsinställningar](assets/aftia-conversion-in-progress.jpg)

1. När konverteringen är klar visas följande skärm:

   ![Konverterat adaptivt formulär](assets/aftia-converted-adaptive-form-2.jpg)

   Klicka på mappen **Utdata** för att visa det skapade adaptiva formuläret.

#### Kända fel och anteckningar {#known-issues-notes}

Tjänsten Automated forms conversion innehåller vissa [metodtips, kända komplexa mönster](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/styles-and-pattern-considerations-and-best-practices.html) och [kända fel](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/known-issues.html). Granska dessa innan du börjar använda tjänsten AEM Forms Automated forms conversion.

1. Generera formuläret med Skapa anpassningsbara formulär utan aktiverade databindningar om du vill binda formuläret till en FDM efter konverteringen.

1. Se till att mallmappen har jcr:read för alla behörigheter aktiverade, annars kan tjänstanvändaren inte läsa mallen från databasen och konverteringen misslyckas.

## Anpassningar av demopaket {#demo-package-customizations}

I det här avsnittet finns anvisningar om hur du anpassar demon.

### Anpassning av mallar {#templates-customization}

Redigerbara mallar finns på följande plats:

*https://&lt;aemserver>:&lt;port>/libs/wcm/core/content/sites/templates.html/conf/we-gov*

Mallarna innehåller mallarna AEM Site, Adaptive Form och Interactive Communications, som skapats och sammanställts med komponenter som finns på:

*https://&lt;aemserver>:&lt;port>/crx/de/index.jsp#/apps/we-gov/components*

#### Formatsystem {#customizetemplates}

Den här webbplatsen innehåller även klientbibliotek, varav ett importerar Bootstrap 4 ( [https://getbootstrap.com/](https://getbootstrap.com/) ). Det här klientbiblioteket är tillgängligt på

*https://&lt;aemserver>:&lt;port>/crx/de/index.jsp#/apps/we-gov/clientlibs/clientlib-base/css/bootstrap*

De redigerbara mallarna som ingår i det här paketet levereras även förkonfigurerade med mall-/sidprinciper som använder CSS-klasserna Bootstrap 4 för sidnumrering, formatering osv. Alla klasser har inte lagts till i mallprofilerna, men alla klasser som stöds av Bootstrap 4 kan läggas till i profilerna. På sidan Komma igång finns en lista med tillgängliga klasser:

[https://getbootstrap.com/docs/4.1/getting-started/introduction/](https://getbootstrap.com/docs/4.1/getting-started/introduction/)

Mallar som ingår i paketet har även stöd för Style System:

[Formatsystem](../../sites-authoring/style-system.md)

#### Malllogotyper {#template-logos}

Project DAM Assets innehåller också logotyper och bilder från We.Gov. Dessa resurser finns på:

*https://&lt;aemserver>:&lt;port>/assets.html/content/dam/we-gov*

När du redigerar sid- och formulärmallar kan du välja att uppdatera logotyper genom att redigera komponenterna Navigering och Sidfot. De här komponenterna har en konfigurerbar varumärkesdialogruta och logotypdialogruta som kan användas för att uppdatera logotyper:

![Malllogotyper](assets/template_logos.jpg)

Mer information finns i Redigera sidinnehåll:

[Redigera sidinnehåll](../../sites-authoring/editing-content.md)

### Anpassning av webbplatssidor {#sites-pages-customization}

Alla webbplatssidor är tillgängliga från: *https://&lt;aemserver>:&lt;port>/sites.html/content/we-gov*

Dessa webbplatssidor använder även paketet AEM stödraster för att styra layouten för några komponenter.

#### Formatsystem {#style-system}

Sidorna i paketet har också stöd för Style System:

[Formatsystem](../../sites-authoring/style-system.md)

Du kan även läsa [Mallar och anpassningsstilsystem](../../forms/using/forms-install-configure-gov-reference-site.md#customizetemplates) för att få information om vilka format som stöds.

### Anpassning av anpassade formulär {#adaptive-forms-customization}

Alla anpassningsbara formulär finns i:

*https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

Dessa formulär kan anpassas efter vissa användningssätt. Observera att vissa fält och inskickningslogik inte bör ändras för att säkerställa att formuläret fortsätter att fungera korrekt. Detta omfattar följande:

**Registreringsprogram för hälsofördelar:**

* contact_id - dolt fält som används för att ta emot kontakt-ID för MS Dynamics under överföringen
* Skicka - Knapplogiken för överföring kräver anpassning för att stödja återanrop. Anpassningen är dokumenterad, men ett stort skript krävdes för att skicka formuläret samtidigt som en POST- och GET-åtgärd utfördes till MS Dynamics via Forms datamodell.
* Rotpanelen - Händelsen Initialize används för att lägga till en MS Dynamics-knapp i AEM Inkorg på ett så lite påträngande sätt som möjligt eftersom alla komponenter i gränssnittet för AEM Inkorg inte kan ändras.

#### Anpassad formulärformatering {#adaptive-form-styling}

Anpassningsbara formulär kan också formateras med stilredigeraren eller temaredigeraren:

* [Textbunden formatering av adaptiva formulärkomponenter](inline-style-adaptive-forms.md)
* [Skapa och använda teman](themes.md)

### Anpassning av arbetsflöde {#workflow-customization}

Anmälningsblanketten skickas till ett arbetsflöde för att behandlas av OSGI. Det här arbetsflödet finns på *https://&lt;aemserver>:&lt;port>/conf/we-gov/settings/models/we-gov-process.html*.

På grund av vissa begränsningar innehåller det här arbetsflödet flera skript och anpassade arbetsflödessteg för OSGI. Dessa arbetsflödessteg skapades som allmänna steg och har inte skapats med konfigurationsdialogrutor. För närvarande bygger konfigurationen av arbetsflödesstegen på processargument.

All Java-kod för arbetsflödessteg finns i **we-gov-forms.core-&lt;version>.jar**-paketet.

## Demonstrationsfrågor och kända fel {#demo-considerations-and-known-issues}

Det här avsnittet innehåller information om demonstrationsfunktioner och designbeslut som kan kräva speciella överväganden under demonstrationsprocessen.

### Demoversioner {#demo-considerations}

* Enligt AGRS-159 ska namnet (för-, mitten- och efternamn) på kontakten som används i det anpassade registreringsformuläret vara unikt.
* Det anpassningsbara registreringsformuläret skickar e-postmeddelandet från Adobe Sign till det e-postmeddelande som anges i formulärets e-postfält. E-postadressen får inte vara samma e-postadress som e-postadressen som används för att konfigurera Adobe Sign molnkonfiguration.

### Kända fel {#known-issues}

* (AGRS-120) Webbplatsnavigeringskomponenten stöder för närvarande inte kapslade underordnade sidor som är mer än två nivåer djupa.
* (AGRS-159) Aktuell MS Dynamics FDM måste utföra två åtgärder först, först POST av data i det anpassade registreringsformuläret till Dynamics och sedan hämta användarposten för att hämta kontakt-ID:t. I det aktuella läget kommer hämtning av kontakt-ID att misslyckas om fler än två användare med samma namn finns i Dynamics, vilket inte tillåter att det anpassade registreringsformuläret skickas.

## Konfigurerar hjälpmedelstestning {#configure-accessibility-testing}

### Aktiverar tillägg av hjälpmedelstestningskrom på {#enable-chrome-add-on}

För att kunna utföra tillgänglighetstestning först måste du installera Chrome-plugin-programmet, detta finns [här](https://chrome.google.com/webstore/detail/accessibility-developer-t/fpkknkljclfencbdbgkenhalefipecmb?hl=en).

När den är installerad läser du in sidan som du vill testa i webbläsaren Chrome (Obs! Om du har flera flikar öppna kan det påverka poängen, du bör bara ha en flik öppen). När sidan har lästs in
**högerklicka på** på sidan och välj fliken **Granskningar** . Utvecklarna kan välja vilken typ av granskning som ska utföras av plugin-programmet för tillgänglighet. När alla önskade alternativ har valts kan användaren välja knappen Generera rapport. Detta genererar ett PDF-dokument som visar den övergripande tillgänglighetsgraderingen och vad som kan användas för att öka tillgänglighetsgraderingen generellt.

När rapporten har körts kan användarna förvänta sig följande:

![Tillgänglighetsrapport](assets/aftia-accessibility.jpg)

Antalet som visas framför användarna är den övergripande tillgänglighetsgraderingen som de har fått. Det finns också en beskrivning av hur detta beräknades efter poängen.

Om du vill exportera det här kan du klicka på de tre knapparna till höger på skärmen och välja bland de andra alternativ som finns i plugin-programmet.

![Tillgänglighetsrapport](assets/aftia-accessibility-report.jpg)

### Ultramarin-tema {#ultramarine-theme}

Det allmänt tillgängliga Ultramarine-temat som underhålls av Adobe är inbyggt i
`we-gov-forms.pkg.all-<version>.zip` installerbar ZIP-fil. När paketet har installerats med CRX.

Med Package Manager kan man komma åt Ultramarine-temat i AEM Forms genom att gå till **Forms** > **Themes** > **Reference Themes** > **Ultramarine-Accessible**.

![Ultramarintema](assets/aftia-ultramarine-theme.jpg)

## Konfigurationsalternativ {#configuration-options}

Användare kan konfigurera olika alternativ för arbetsflödestjänster, som omfattar följande:

1. Microsoft Dynamics-post
1. Adobe Sign
1. AEM anpassad kommunikationshantering
1. Adobe Analytics

För att kunna konfigurera dem så att de aktiveras i arbetsflödet måste användarna utföra följande uppgifter.

1. Gå till https://&#39;[server]:[port]&#39;/system/console/configMgr.

1. Leta reda på *WebGov-konfigurationer*.

1. Öppna tjänstdefinitionen och aktivera de valda tjänsterna för att anropas i arbetsflödet.

   >[!NOTE]
   Bara för att en användare aktiverar tjänsten på Configuration Manager-sidan måste användaren ändå konfigurera en tjänstkonfiguration för att kunna kommunicera med de externa tjänster som efterfrågas.

   ![webbforum](assets/aftia-configuration-options.jpg)

1. Klicka på knappen Spara när du är klar för att spara inställningarna.

## Nästa steg {#next-steps}

Nu är du redo att utforska referenswebbplatsen We.Gov. Mer information om hur du använder referenswebbplatsarbetsflödet och -stegen för Web.Gov finns i [Genomgång av referenswebbplatsen för Web.Gov](../../forms/using/forms-gov-reference-site-user-demo.md).
