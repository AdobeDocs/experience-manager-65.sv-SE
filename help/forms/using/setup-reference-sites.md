---
title: Konfigurera referensplatser för Web.Finance och Employee Self Service
seo-title: Konfigurera referensplatser för Web.Finance och Employee Self Service
description: AEM Forms referenswebbplatser visar hur du kan använda AEM Forms för att implementera ett arbetsflöde från början till slut i en organisation.
seo-description: AEM Forms referenswebbplatser visar hur du kan använda AEM Forms för att implementera ett arbetsflöde från början till slut i en organisation.
uuid: 199349b7-97bd-4eca-a2e7-19d6708fcbee
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
discoiquuid: 03886dd3-5873-4908-912b-fbbddb26c322
docset: aem65
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '2788'
ht-degree: 0%

---


# Konfigurera referensplatser för Web.Finance och Employee Self Service{#set-up-and-configure-we-finance-and-employee-self-service-reference-sites}

AEM Forms tillhandahåller en referensimplementering av webbplatser som visar hur AEM Forms hjälper finanssektorn och myndigheter att omvandla sina komplexa transaktioner till enkla och engagerande digitala upplevelser var som helst, när som helst, på vilken enhet som helst.

Referensplatsen för Vi.Finance bygger på verkliga användningsfall för att engagera befintliga och potentiella kunder, direkt från första kontakten till att hantera korrespondenser och transaktioner på ett personaliserat och kostnadseffektivt sätt.

Med referenswebbplatserna kan du utforska och visa upp följande nyckelfunktioner i AEM Forms.

* Förenklad redigeringsupplevelse med engagerande och responsiva adaptiva formulär och interaktiv kommunikation.
* Interaktiv kommunikation för att skapa interaktiv, personaliserad och responsiv kundkommunikation som anpassar sig till enhetsinställningarna och layouten.
* Dataintegrering för att ansluta till olika datakällor för att förifylla och skicka formulärdata via en formulärdatamodell.
* Formulärarbetsflöde för att automatisera affärsprocesser och arbetsflöden.
* Avancerade funktioner för hantering och bearbetning av användardata.
* Integrering med Adobe Sign för att säkert signera och skicka adaptiva formulär.
* Integrering med Adobe Target för att leverera riktade rekommendationer och utföra A/B-tester för att maximera avkastningen från ett formulär.
* Integrering med Adobe Analytics för att mäta hur väl ett formulär eller en kampanj fungerar och fatta välgrundade beslut.
* Förbättrad formulärifyllning.

Referenswebbplatserna innehåller återanvändbara resurser som du kan använda som mallar för att skapa egna resurser.

* Integrering med Adobe Sign för att säkert signera och skicka adaptiva formulär.

* Integrering med Adobe Sign för att säkert signera och skicka adaptiva formulär.

## Krav och steg för att konfigurera referensplatser {#prerequisites-and-steps-to-set-up-reference-sites}

Innan du konfigurerar referensplatsen måste du ha följande:

* **Grundläggande AEM** -funktioner, AEM QuickStart, tilläggspaket för AEM Forms samt referenspaket för webbplatser. Mer information om paket med tillägg och referensplatser finns i [AEM Forms-releaser](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) .

* **En SMTP-tjänst** Du kan använda vilken SMTP-tjänst som helst.

* **Adobe Signs utvecklarkonto och Adobe Signs API-program** För att kunna använda digitala signeringsfunktioner krävs ett Adobe Sign-utvecklarkonto. Se [Adobe Sign](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html).

* En instans av Microsoft Dynamics 365 som körs och som kan integreras med AEM Forms. Om du vill köra referenswebbplatsen importerar du exempeldata till Microsoft Dynamics-instansen för att förifylla den interaktiva kommunikation som används på referenswebbplatsen.
* En instans av AEM med tilläggsprogrammet Forms som körs. Mer information finns i [Installera och konfigurera AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).

Utför följande steg i den rekommenderade sekvensen för att konfigurera och konfigurera referensplatserna.

<table>
 <tbody>
  <tr>
   <th><strong>Steg</strong></th>
   <th><strong>Konfigurera</strong></th>
   <th><strong>Anteckningar</strong></th>
  </tr>
  <tr>
   <td><a href="#installandconfigureaemform">Installera och konfigurera AEM Forms</a></td>
   <td>Skapa och publicera</td>
   <td>Installera och konfigurera AEM Forms författare och publiceringsinstanser.</td>
  </tr>
  <tr>
   <td><a href="#ssl">Konfigurera SSL</a></td>
   <td>Author and Publish<br /> </td>
   <td>Aktivera HTTP över SSL för säker kommunikation med Adobe Sign.</td>
  </tr>
  <tr>
   <td><p><a href="#externalizer">Konfigurera konfiguration av Dag CQ Link Externalizer</a></p> </td>
   <td>Author and Publish<br /> </td>
   <td><p>Referensfall för användning på webbplats levererar e-post för olika transaktioner. Den här inställningen krävs för nyhetsbrev som levereras via e-post. Det ser till att URL:er och bilder pekar på publiceringsinstansen. </p> </td>
  </tr>
  <tr>
   <td><a href="#cqmail">Konfigurera daglig CQ Mail-tjänst</a></td>
   <td>Skapa och publicera</td>
   <td>Krävs för e-postkommunikation.</td>
  </tr>
  <tr>
   <td><a href="#xss">Åsidosätt standard-XSS-konfiguration</a></td>
   <td>Publicera</td>
   <td>Används för att åsidosätta $-, {- och }-tecken som blockeras av XSS-säkerhet.</td>
  </tr>
  <tr>
   <td><a href="#aemds">Konfigurera AEM DS-inställningar</a></td>
   <td>Författare</td>
   <td>Konfigurera AEM DS för formuläröverföring vid publiceringsinstans och arbetsflöden för bearbetning på författarinstansen.</td>
  </tr>
  <tr>
   <td><a href="#refsite">Distribuera referensplatspaket</a></td>
   <td>Författare</td>
   <td>Distribuera referensplatspaket på AEM Forms författarinstans.</td>
  </tr>
  <tr>
   <td><a href="../../forms/using/setup-reference-sites.md#optional-import-sample-data-into-microsoft-dynamics">Importera exempeldata till Microsoft Dynamics</a></td>
   <td>Skapa och publicera</td>
   <td>Importera exempeldata för genomgång av kreditkortsansökningar, bostadslåneansökningar och hemförsäkringsansökningar</td>
  </tr>
  <tr>
   <td><a href="../../forms/using/setup-reference-sites.md#configure-oauth-cloud-service-for-microsoft-dynamics">Konfigurera OAuth-molntjänsten för Microsoft Dynamics</a></td>
   <td>Skapa och publicera</td>
   <td>Konfigurera OAuth-molntjänsten i AEM Forms för att aktivera kommunikation mellan AEM Forms och Microsoft Dynamics. </td>
  </tr>
  <tr>
   <td><a href="#scheduler">Konfigurera Adobe Sign Scheduler</a></td>
   <td>Author and Publish<br /> </td>
   <td>Ändra schemaläggarens konfiguration för att kontrollera status varannan minut.</td>
  </tr>
  <tr>
   <td><a href="#sign-service">Konfigurera referenswebbplats för Adobe Sign-Cloud Service</a></td>
   <td>Author and Publish<br /> </td>
   <td>En konfiguration som levereras med referenspaket för webbplatser och behöver konfigureras om med giltiga autentiseringsuppgifter.</td>
  </tr>
  <tr>
   <td><a href="#anonymous">Konfigurera Forms Common Configuration Service för anonyma användare</a></td>
   <td>Publicera</td>
   <td>Konfigurationen tillåter att anonyma användare skickar, signerar och dokumenterar poster.</td>
  </tr>
  <tr>
   <td><a href="#fdm">Ändra Rest Service Swagger-fil för formulärdatamodell</a></td>
   <td>Author and Publish<br /> </td>
   <td>Ändra tjänsten för din miljö.</td>
  </tr>
 </tbody>
</table>

## Installera och konfigurera AEM Forms {#installandconfigureaemform}

Installera och distribuera AEM Forms enligt beskrivningen i [Installera och konfigurera AEM Forms på OSGi](../../forms/using/installing-configuring-aem-forms-osgi.md).

>[!NOTE]
>
>Konfigurera replikerings- och omvända replikeringsagenter om det finns fler än en publiceringsinstans eller författar- och publiceringsinstanser på olika datorer.

## Konfigurera SSL {#ssl}

SSL-konfiguration krävs för att kommunicera med Adobe Sign-servrar. Detaljerade steg finns i [Aktivera HTTP över SSL](/help/sites-administering/ssl-by-default.md).

>[!CAUTION]
>
>Konfigurera inte tvingad SSL för `/etc/map` mapp.

## Konfigurera konfiguration av Dag CQ Link Externalizer {#externalizer}

I AEM är **Externalizer** en OSGI-tjänst som du kan använda för att programmässigt omvandla en resurssökväg (t.ex. /path/to/my/page) till en extern och absolut URL (t.ex. https://www.mycompany.com/path/to/my/page) genom att prefix the path with a preconfigure DNS. Se [Externalisera URL:er](/help/sites-developing/externalizer.md).

>[!CAUTION]
>
>Externa inte till HTTPS-URL om du använder självsignerat certifikat för SSL.
>
>Använd också localhost i stället för värdnamnet för den lokala servern.

Utför följande steg på både författare och publiceringsinstanser:

1. Gå till OSGi Configuration på https://&lt;*värdnamn>*:&lt;*port>*/system/console/configMgr.
1. Hitta och tryck på **Day CQ Link Externalizer** -konfigurationen.
Dialogrutan Day CQ Link Externalizer öppnas för redigering av konfigurationen.
1. I dialogrutan Dag CQ Link Externalizer, i fältet Domäner:

   * På författarinstansen anger du en publicerings-URL som du kan komma åt från ett externt system. Exempel: ett värdnamn eller en publiceringswebbserver.
   * I publiceringsinstansen anger du både författar- och publicerings-URL:er.

1. Kontrollera att den lokala serverns URL anges i fältet Domäner på både författare- och publiceringsinstanser.
1. Tryck på **Spara**. Vänta en stund tills alla tjänster har startats om.

## Konfigurera daglig CQ Mail-tjänst {#cqmail}

Implementering av referensplats kräver att e-post skickas till exempelanvändare när de fyller i och skickar formulär. Genom att konfigurera Day CQ Mail Service kan du tillhandahålla information om SMTP-tjänster för att skicka automatiska e-postmeddelanden till kunder. Se [Konfigurera e-postmeddelanden](/help/sites-administering/notification.md).

Utför följande steg för att konfigurera e-posttjänsten på publiceringsinstansen:

1. Gå till OSGi Configuration på https://&lt;*värdnamn>*:&lt;*port>*/system/console/configMgr.
1. Hitta och tryck på **Day CQ Mail Service** för att öppna den för konfiguration.
1. Ange värdnamn och portvärden för SMTP-servern.
1. Tryck på **Spara.**

>[!NOTE]
>
>Du kan använda företagets SMTP-tjänst eller offentliga tjänster som Gmail. Information om hur du konfigurerar SMTP-tjänsten finns i dokumentationen för SMTP-tjänsten.

## Åsidosätt standard-XSS-konfiguration {#xss}

E-postmallarna för referenswebbplatsen We.Finance innehåller anpassade länkar i e-postmeddelanden. Länkarna har platshållare som `${placeholder}`. Dessa platshållare ersätts med verkliga värden innan e-postmeddelanden skickas. Standardkonfigurationen för XSS-skydd för AEM tillåter inte klammerparenteser (**{ }**) i URL:en i HTML-innehåll. Du kan dock åsidosätta standardkonfigurationen genom att utföra följande steg på en publiceringsinstans:

1. Kopiera `/libs/cq/xssprotection/config.xml` till `/apps/cq/xssprotection/config.xml`.
1. Öppna `/apps/cq/xssprotection/config.xml`.
1. I `common-regexps` avsnittet ändrar du `onsiteURL` posten på följande sätt och sparar filen.

   `<regexp name="onsiteURL" value="([\p{L}\p{N}\\\.\#@\$\{\}%\+&;\-_~,\?=/!\*\(\)]*|\#(\w)+)"/>`

>[!NOTE]
>
>Klammerparenteser (**{ }**) inkluderas som accepterade tecken i URL:en i HTML-innehåll.

När du har konfigurerat SMTP-servern kan du försöka fylla i ett formulär med Sarah Rose-persona och spara det som ett utkast. När du sparar som utkast får du ett alternativ för att ta emot utkastet via e-post. Om du får ett e-postmeddelande med en länk till programutkastet när du trycker på knappen **Skicka e-post** , lyckas e-postkonfigurationen. Se till att du loggar in med Sarah inloggningsuppgifter för att se utkastet.

## Konfigurera AEM DS-inställningar {#aemds}

AEM DS-tjänstinställningar krävs på publiceringsinstansen för e-postkommunikation i referenswebbplatsens användningsfall. Detaljerade anvisningar om hur du konfigurerar AEM DS-tjänstkonfigurationen på Publish-instansen finns i [Konfigurera AEM DS-inställningar](../../forms/using/configuring-the-processing-server-url-.md).

I AEM DS-inställningstjänsten anger du URL:en för publiceringsservern i stället för URL:en för bearbetningsservern för referenswebbplatser för AEM Forms.

>[!CAUTION]
>
>Ange inte URL:en `/lc` för bearbetningsservern om du konfigurerar den för AEM Forms OSGi.

## Distribuera referensplatspaket {#refsite}

Installera referensplatspaketen med hjälp av [Programvarudistribution](https://docs.adobe.com/content/help/en/experience-cloud/software-distribution/home.html).

* [AEM Forms FSI Reference Site Package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/fd/AEM-FORMS-6.5-FSI-REF-SITE)
* [AEM Forms GOV Reference Site Package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/fd/AEM-FORMS-6.5-GOV-REF-SITE)

Mer information om hur du använder paket finns i [Arbeta med paket](/help/sites-administering/package-manager.md).

När du har installerat paketen och startat författaren och publicerat instanserna kan du gå till följande URL:er i webbläsaren:

* `https://'[server]:[port]'/wegov`
* `https://'[server]:[port]'/wefinance`

Om installationen lyckas får du tillgång till landningssidorna för referensplatserna och We.Finance.

## (Valfritt) Importera exempeldata till Microsoft Dynamics {#optional-import-sample-data-into-microsoft-dynamics}

Referenswebbplatserna för bostadslån och autoförsäkringsprogram är konfigurerade att använda poster från Microsoft Dynamics. Referensplatspaketet installerar en anpassad entitet och exempelposter som du kan importera till Microsoft Dynamics för att köra referensplatsen. Utför följande steg för att migrera och konfigurera exempeldata:

Så här importerar du den anpassade entiteten för programmet för automatisk försäkring:

1. Ladda ned **lösningspaketet WeFinanceAutoInsurance_1_0.zip** från `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/WeFinanceAutoInsurance_1_0.zip` din AEM-författarinstans.
1. Gå till **Inställningar > Lösningar** i din Microsoft Dynamics-instans och klicka på **Importera**. Markera och importera paketet.

Så här importerar du den anpassade entiteten för programmet för automatisk försäkring:

1. Hämta paketet **AEMFormsFSIRefsite_1_0.zip** från `https://[author]:'port'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`. Markera och importera paketet.

1. Gå till **Inställningar > Lösningar** i din Microsoft Dynamics-instans och klicka på **Importera**. Markera och importera paketet.

Så här importerar du kund- och försäkringspolicyposter:

1. Ladda ned datafilerna **We.Finance Customers.csv, We.Finance Auto Insurance Renewals.csv** och **home inteckning** från följande platser hos din AEM-författare:

   * `https://'server':[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Customers.csv`
   * `https://'server':[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Auto Insurance Renewals.csv`
   * `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

1. Gör följande i din Microsoft Dynamics-instans:

   * Gå till **Försäljning** > **Vi.Finance-kunder** och klicka på **Importera**.

   * Gå till **Försäljning** > **Automatisk försäkring** och klicka på **Importera**.

   * Gå till **Försäljning** > **Vi.Finance Home Mortgage** och klicka på **Importera**.

## Konfigurera OAuth-molntjänsten för Microsoft Dynamics {#configure-oauth-cloud-service-for-microsoft-dynamics}

Konfigurera OAuth-molntjänsten i AEM Forms för att aktivera kommunikation mellan AEM Forms och Microsoft Dynamics. Utför följande steg för att konfigurera OAuth-Cloud Servicen på AEM-författaren och publicera instanser:

1. I AEM-författarinstansen går du till **Verktyg** > **Cloud Service** > **Datakällor** > **global**. Tryck på ikonen **Refsite Dynamics Integration** och tryck på Properties (Egenskaper).
1. Gå till Microsoft Azure Active Directory-kontot. Lägg till den kopierade molntjänstens konfigurations-URL i inställningen **Svara-URL** för det registrerade programmet. Spara konfigurationen.
1. Ange **tjänstrot**, **klient-ID**, **klienthemlighet** och **resurs-URL** för din Microsoft Dynamics-instans på fliken Autentiseringsinställningar. Klicka på **Anslut till OAuth** som dirigerar om till inloggningssidan för Microsoft Dynamics.
1. Ange dina inloggningsuppgifter. När du har loggat in omdirigeras du till AEM Forms molntjänstkonfigurationssida. Klicka på **Spara och stäng**. Molntjänstkonfigurationen sparas.
1. Gå till **Formulär** > **Dataintegreringar** > **We.Finance**. Välj Automatisk försäkring (Dynamics) och klicka på Redigera. Microsoft Dynamics-enheter visas på fliken Datakällor. Vänta tills alla entiteter har hämtats från Microsoft Dynamics och listats under fliken Datakällor.
1. Markera **entiteten** AutoInsuranceRenewal och klicka på **Testmodellobjekt**. I avsnittet för indatabegäran anger du värdet för kund-ID som&quot;900001&quot; och klickar på **Testa**. I avsnittet Utdata visas de poster som hämtats från Microsoft Dynamics för kund-ID 90001.
1. I avsnittet för indatabegäran anger du värdet för kund-ID som&quot;900001&quot; och klickar på **Testa**. I avsnittet Utdata visas de poster som hämtats från Microsoft Dynamics för kund-ID 90001.
1. Upprepa steg 1-6 i publiceringsinstansen.

## Konfigurera Adobe Sign Scheduler {#scheduler}

Gör följande på både författare- och publiceringsinstanser:

1. Gå till AEM Web Configuration-konsolen på `https://'[server]:[port]'system/console/configMgr`.
1. Sök och tryck **[!UICONTROL Adobe Sign Configuration Service]** för att öppna den för konfiguration.
1. Konfigurera **[!UICONTROL Status Update Scheduler Expression]** som **0 0/2 * * * ?**.

   >[!NOTE]
   >
   >Ovanstående schemaläggningskonfiguration kontrollerar statusen för Adobe Sign-tjänsten varannan minut.

1. Tryck på **[!UICONTROL Save]**.

## Konfigurera referensplats för Adobe Sign-molntjänsten {#sign-service}

Gör följande på både författare- och publiceringsinstanser:

1. Gå till **Verktyg** > **Cloud Service** > **Adobe Sign** > **global**. Markera **AEM Forms Reference Site Sign** och tryck på Properties (Egenskaper).

   >[!CAUTION]
   >
   >Kontrollera att URL:en har lagts till i listan över omdirigerings-URL:er för OAuth-konfigurationen i Adobe Sign API-programmet. `https://[host]:[ssl_port]/mnt/overlay/adobesign/cloudservices/adobesign/properties.html`

1. Ange klient-ID och hemlighet för OAuth-konfigurationen för Adobe Sign-programmet.
1. (Valfritt) Markera **[!UICONTROL Enable Adobe Sign for attachments also]** alternativet och tryck på **[!UICONTROL Connect to Adobe Sign]**. Den bifogar filerna som är kopplade till ett anpassat formulär till motsvarande Adobe Sign-dokument som skickats för signering.
1. Tryck **[!UICONTROL Connect to Adobe Sign]** och logga in med dina inloggningsuppgifter för Adobe Sign.

## Konfigurera Forms Common Configuration Service {#anonymous}

Gör följande på publiceringsinstansen för att tillåta åtkomst för anonyma användare:

1. Gå till AEM Web Configuration-konsolen på `https://'[server]:[port]'/system/console/configMgr`.
1. Sök och tryck **[!UICONTROL Forms Common Configuration Service]** för att öppna den för konfiguration.
1. Konfigurera **[!UICONTROL Allow]** fältet för **[!UICONTROL All Users]**.
1. Tryck på **[!UICONTROL Save]**.

## Ändra resttjänst för formulärdatamodell {#fdm}

Gör följande på både författare- och publiceringsinstanser:

1. Gå till CRXDE på `https://'[server]:[port]'/crx/de/index.jsp`.
1. Navigera till **/conf/global/settings/cloudconfigs/fdm/roi-rest/jcr:content/swaggerFile** och öppna swagger-filen.
1. Uppdatera värd- och portinställningarna enligt din miljö.
1. Spara inställningarna.
1. (Endast **författarinstans**) Gå till **Verktyg** > **Cloud Service** > **Datakällor** > **Global**. Välj **roi-rest** och tryck på **Properties**.Tryck på **Authentication Settings** och ange **Authentication Type** till **Basic Authentication**. Ange `admin`/ `admin`som användarnamn/lösenord för att komma åt tjänsten. Tryck på **Spara och stäng**.

## Integrera med Marketing Cloud {#integrate-with-marketing-cloud}

Du kan integrera AEM Forms med Adobe Analytics och Adobe Target. Med Adobe Analytics kan ni generera rapporter och analysera hur anpassade formulär fungerar, men med Adobe Target kan ni leverera personaliserade upplevelser och utföra A/B-tester för anpassade formulär.

Gör följande för att konfigurera Adobe Analytics och Adobe Target i AEM Forms.

### Konfigurera Adobe Analytics {#configureanalytics}

Tack vare integreringen med AEM Forms Analytics kan ni övervaka och analysera hur era kunder interagerar med era formulär och dokument. Det hjälper dig att identifiera och åtgärda problemområden och öka konverteringsgraden.

Konfigurera ditt Analytics-konto så som beskrivs i [Konfigurera analyser och rapporter](../../forms/using/configure-analytics-forms-documents.md)om du vill använda den här funktionen på referenswebbplatsen.

För att generera en rapport paketeras startdata med referenswebbplatserna. Gör följande innan du använder startvärdesdata:

1. Kontrollera att det finns konfigurationer för Web.Finance-analys i AEM cloud services. Du kan hitta molntjänster på något av följande sätt:

   * Navigera till **[!UICONTROL Tools>Cloud Services>Legacy Cloud Services]** eller bläddra till https://&lt;host>:&lt;port>/libs/cq/core/content/tools/cloudservices.html.
   * Klicka på under **[!UICONTROL Cloud Services]** avsnitt på **[!UICONTROL Adobe Analytics]** sidan `Show Configurations`. Vi.Finance-konfigurationer är tillgängliga. Klicka för att öppna konfigurationen. Klicka på på konfigurationssidan **[!UICONTROL Edit]**. Ange ett giltigt företag, användarnamn, delad hemlighet (lösenord) och datacenter och klicka på **[!UICONTROL Connect to Analytics]**. När du har öppnat dialogrutan Anslutningen klickar du **[!UICONTROL OK]** på konfigurationsdialogrutan. Konfigurera ramverket under Analytics-konfigurationen enligt beskrivningen i [Konfigurera Analytics och Rapporter](../../forms/using/configure-analytics-forms-documents.md).

1. Gå till https://&lt;*host*>:&lt;*port*>/system/console/configMgr och gör följande:

   * Leta upp och klicka på **[!UICONTROL Web Console Configuration]** sidan **[!UICONTROL AEM Forms Analytics Configuration]**.

   * Välj we-Finance(we-Finance) eller we-gov(we-gov) i dialogrutan Konfigurera i AEM Forms Analytics. **[!UICONTROL SiteCatalyst Framework]**
   * Klicka **[!UICONTROL Save]** och låt sidan uppdateras.

1. Navigera till formulärhanteraren på https://&lt;host>:&lt;port>/aem/forms och gör följande:

   * Öppna mappen We.Finance och välj det formulär som du vill visa rapporten för.
   * Klicka på Aktivera Analytics i verktygsfältet Åtgärder. När du har aktiverat analys för formuläret klickar du på Analytics Report. Du kan se en tom rapport genereras. När en tom rapport har skapats måste du tillhandahålla startdata som levereras med refsite-paket för att generera analysrapporten för demosyfte.

   Referenswebbplatser tillhandahåller analysrapporter med startdata för kreditkort, bostadslån och ärenden som rör barnsupport.

### Konfigurera Target {#configure-target}

På referenswebbplatsen visas integreringen av AEM Forms med Adobe Target som gör att du kan inkludera riktat och personaliserat innehåll i adaptiva dokument. Det gör det även möjligt att skapa A/B-tester för adaptiva formulär.

Så här konfigurerar du Target i AEM för att få en upplevelse av integrationen på referenswebbplatsen:

1. Starta författarens snabbstart med jvm-argumentet `-Dabtesting.enabled=true` för att aktivera A/B-testning på servern.

   >[!NOTE]
   >
   >Om AEM-instansen körs på JBoss, som startas som en tjänst från körkortsinstallationen, lägger du till `-Dabtesting.enabled=true` parametern i följande post i `jboss\bin\standalone.conf.bat` filen:
   `set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

1. Öppna `https://<hostname>:<port>/libs/cq/core/content/tools/cloudservices.html`.

1. In the **[!UICONTROL Adobe Target]** section, click **[!UICONTROL Show Configurations]**. Vi.Finance Target Configuration finns tillgänglig. Klicka för att öppna konfigurationen. Klicka på på konfigurationssidan **[!UICONTROL Edit]**. Dialogrutan **[!UICONTROL Edit Component]** för konfigurationen öppnas.

1. Ange klientkod, e-postadress och lösenord som är kopplade till ditt Target-konto. Välj API-typ som **[!UICONTROL REST]**.
1. Klicka på **[!UICONTROL Connect to Adobe target]**. När Target-kontot har konfigurerats klickar du på **[!UICONTROL OK]**. Den paketerade konfigurationen har ett Target Framework.

1. Gå till `https://<hostname>:<port>/system/console/configMgr`.

1. Klicka på **[!UICONTROL AEM Forms Target Configuration]**.
1. Välj ett Target-ramverk.
1. I **[!UICONTROL Target URLs]** fältet anger du URL:en till AEM Forms. Till exempel: `https://<hostname>:<port>/`.

1. Klicka på **[!UICONTROL Save]**.

Användningsexempel för kreditkortsansökningar och hemmasamlingsprogram visar hur man utför A/B-tester och visar en rapport i demonstrationssyfte. Mer information om genomgångar finns i [Genomgång](../../forms/using/finance-reference-site-walkthrough.md)av referenswebbplatser för Web.Finance.

## Nästa steg {#next-step}

Nu är du redo att utforska referenswebbplatsen. Mer information om arbetsflöde och steg för referensplatsen finns i:

* [Genomgång av referenswebbplatser för ekonomi](../../forms/using/finance-reference-site-walkthrough.md)
* [Genomgång av referenswebbplatser för självbetjäning för medarbetare](../../forms/using/employee-self-service-reference-site.md)

