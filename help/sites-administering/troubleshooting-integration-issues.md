---
title: Felsöka integreringsproblem
seo-title: Felsöka integreringsproblem
description: Lär dig hur du felsöker integreringsproblem.
seo-description: Lär dig hur du felsöker integreringsproblem.
uuid: fe080e58-a855-4308-a611-f72eb47ba82d
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 422ee332-23ae-46bd-8394-a4e0915beaa2
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# Felsöka integreringsproblem{#troubleshooting-integration-issues}

## Allmänna felsökningstips {#general-troubleshooting-tips}

### Kontrollera att det inte finns några JavaScript-fel {#ensure-there-are-no-javascript-errors}

Kontrollera om webbläsarens JavaScript-konsol visar några fel. Ohanterade fel kan förhindra att efterföljande kod körs korrekt. Om fel uppstår ska du kontrollera vilket skript som orsakar felet och i vilket område. Sökvägen till skriptet kan ge en indikation på vilken funktion skriptet tillhör.

### Inloggning på komponentnivå {#logging-on-component-level}

I vissa fall kan det vara praktiskt att lägga till ytterligare programsatser på komponentnivå. Eftersom komponenten återges kan du lägga till en temporär markering för att visa variabelvärden som kan hjälpa dig att identifiera potentiella problem. Exempel:

```
<%
log.info("myVariable={}", myVariable);
%>

<!--
<%= myJspVariable %>
-->

<!--
${ myHtlVariable }
-->
```

Mer information om loggning finns på sidorna [Loggning](/help/sites-deploying/configure-logging.md) och [Arbeta med Granskningsposter och Loggfiler](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) .

## Integreringsproblem med analyser {#analytics-integration-issues}

### Rapportimporteraren orsakar hög CPU-/minnesanvändning {#the-report-importer-causes-high-cpu-memory-usage}

Rapportimporteraren orsakar hög CPU-/minnesanvändning eller orsakar `OutOfMemoryError` undantag.

#### Lösning {#solution}

Du kan åtgärda det här problemet genom att försöka med följande:

* Se till att det inte finns någon stor mängd registrerade PollingImporters (se avsnittet&quot;Shutdown take a long time due to PollingImporter&quot; nedan).
* Kör rapportimporterare vid en viss tidpunkt på dagen med CRON-uttryck för konfigurationerna i `ManagedPollingImporter` OSGi-konsolen [](/help/sites-deploying/configuring-osgi.md).

Mer information om hur du skapar anpassade dataimporteringstjänster i AEM finns i följande artikel [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

### Avstängningen tar lång tid på grund av PollingImporter {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

Analyserna har utformats med en arvsmekanism i åtanke. Vanligtvis aktiverar du Analytics för en webbplats genom att lägga till en referens till en Analytics-konfiguration på sidegenskaperna på fliken [Cloud Services](/help/sites-developing/extending-cloud-config.md) . Konfigurationen ärvs sedan automatiskt till alla undersidor utan att du behöver referera till den igen, såvida inte en sida kräver en annan konfiguration. När du lägger till en referens till en webbplats skapas automatiskt flera noder (12 för AEM 6.3 och tidigare eller 6 för AEM 6.4 och senare) av den typ `cq;PollConfig` som initierar de PollingImporters som används för att importera Analytics-data till AEM. Resultatet blir:

* Många sidor som refererar till Analytics leder till en stor mängd PollingImporters.
* Om du dessutom kopierar och klistrar in sidor med en referens till en Analytics-konfiguration dupliceras dess PollingImporters.

#### Lösning {#solution-1}

För det första kan en analys av [error.log](/help/sites-deploying/configure-logging.md) ge dig insikt i mängden aktiva eller registrerade PollingImporters. Exempel:

```
# Count PollingImporter entries
$ sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\),interval.*/\1/p" error.log | wc -l
86415
# Count PollingImporter entries for last30days
$ sed -n "s/.*(aem-analytics-integration-last30Days).*target=\(.*\),interval.*/\1/p" error.log | wc -l
14531
# Count unique paths of PollingImporter registrations
sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\)\/jcr:content.*/\1/p" error.log | sort | uniq -c
28115
```

För det andra måste du se till att endast de översta sidorna (högst upp i hierarkin) har en analyskonfiguration som refereras.

Mer information om hur du skapar anpassade dataimporteringstjänster i AEM finns i följande artikel [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

## DTM-problem (äldre) {#dtm-legacy-issues}

### DTM-skripttaggen återges inte i sidkällan {#the-dtm-script-tag-is-not-rendered-in-the-page-source}

Skripttaggen [DTM](/help/sites-administering/dtm.md) inkluderas inte korrekt på sidan trots att det finns referenser till konfigurationen på fliken för sidegenskaper i [molntjänster](/help/sites-developing/extending-cloud-config.md) .

#### Lösning {#solution-2}

Du kan åtgärda problemet genom att göra följande:

* Kontrollera att krypterade egenskaper kan dekrypteras (observera att krypteringen kan använda olika automatiskt genererade nycklar på varje AEM-instans). Mer information finns också i [Krypteringsstöd för konfigurationsegenskaper](/help/sites-administering/encryption-support-for-configuration-properties.md).
* Publicera konfigurationerna som finns i `/etc/cloudservices/dynamictagmanagement`
* Kontrollera åtkomstkontrollistor på `/etc/cloudservices`. Åtkomstkontrollistorna ska vara:

   * tillåta, jcr:read; webservice-support-service-libfinder
   * tillåta, jcr:read; alla, rep:glob:&amp;ast;/defaults/&amp;ast;
   * tillåta, jcr:read; alla, rep:glob:&amp;ast;/defaults
   * tillåta, jcr:read; alla, rep:glob:&amp;ast;/public/&amp;ast;
   * tillåta, jcr:read; alla, rep:glob:&amp;ast;/public

Mer information om hur du hanterar åtkomstkontrollistor finns på sidan [Användaradministration och -säkerhet](/help/sites-administering/security.md#permissions-in-aem) .

## Målintegreringsproblem {#target-integration-issues}

### Målinriktat innehåll som inte visas i förhandsgranskningsläget när anpassade sidkomponenter används {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

Problemet inträffar eftersom anpassade sidkomponenter inte innehåller rätt JSP- eller klientbibliotek som hanterar DTM-målintegreringarna.

#### Lösning {#solution-3}

Du kan testa följande lösningar:

* Kontrollera att den anpassade `headlibs.jsp` (om det finns någon `/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`) innehåller följande:

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* Kontrollera att det anpassade `head.html` (om det finns något `/apps/<CUSTOM-COMPONENTS-PATH>/head.html`) **inte** innehåller särskilda integrationsrubriker som i exemplet nedan:

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

Detta `servicelibs.jsp` lägger till de JavaScript-objekt för analys som krävs och läser in molntjänstbiblioteken som är kopplade till webbplatsen. För måltjänsten läses biblioteken in via `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

Vilken uppsättning bibliotek som läses in beror på vilken typ av målklientbibliotek ( `mbox.js` eller `at.js`) som används i målkonfigurationen.

När du använder DTM för att leverera `mbox.js` eller `at.js` kontrollera att biblioteken är inlästa innan innehållet renderas. Om du använder tagghanteringssystem som läser in dessa bibliotek asynkront kan det uppstå problem när målspecifik JavaScript-kod körs.

Mer information finns på sidan [Utveckla för riktat innehåll](/help/sites-developing/target.md#understanding-the-target-component) .

### Felmeddelandet&quot;Report Suite ID saknas i AppMeasurement-initieringen&quot; visas i webbläsarkonsolen {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

Problemet kan uppstå när Adobe Analytics implementeras på webbplatsen med DTM och använder anpassad kod. Orsaken är att du använder `s = new AppMeasurement()` för att instansiera `s` objektet.

#### Lösning {#solution-4}

Använd `s_gi` i stället för `new AppMeasurement` instansieringsmetoden. Exempel:

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### Ett standarderbjudande visas slumpmässigt i stället för rätt erbjudande {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

Det här problemet kan ha flera orsaker:

* Inläsning av målklientbibliotek ( `mbox.js` eller `at.js`) asynkront med tagghanteringssystem från tredje part kan göra att målinriktningen bryts slumpmässigt. Målbiblioteken ska läsas in synkront i sidhuvudet. Detta gäller alltid när biblioteken levereras från AEM.

* Läsa in två målklientbibliotek ( `at.js`) samtidigt, till exempel ett med DTM och ett med Target-konfigurationen i AEM. Detta kan orsaka konflikter för `adobe.target` definitionen om `at.js` versionerna skiljer sig åt.

#### Lösning {#solution-5}

Du kan testa följande lösningar:

* Kontrollera att kundkoden som läser in DTM-liknande bibliotek (som i sin tur läser in Target-biblioteken) körs synkront i [sidhuvudet](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages).
* om webbplatsen är konfigurerad att använda DTM för att leverera målbibliotek ser du till att alternativet **Clientlib levererat av DTM** är markerat i platsens [målkonfiguration](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/target-configuring.html) .

### Ett standarderbjudande visas alltid i stället för rätt erbjudande när AT.js 1.3+ används {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}

Som standard är AEM 6.2 och 6.3 inte kompatibelt med AT.js version 1.3.0+. Med AT.js version 1.3.0 som lägger in parametervalidering för sina API:er, `adobe.target.applyOffer()` krävs en &quot;mbox&quot;-parameter som inte finns i `atjs-itegration.js` koden.

#### Lösning {#solution-6}

Så här löser du problemet `atjs-itegration.js` och lägger till `"mbox": mboxName` fältet i parameterobjektet `adobe.target.applyOffer()` :

```
adobe.target.getOffer({
    "mbox": mboxName,
    "params": params,
    "success": function (response) {
        adobe.target.applyOffer({
            "mbox": mboxName, //<--- ADDED PARAM
            "selector": "#" + mboxName,
            "offer": response
        })
    },
```

### Sidan Mål och inställningar visar inte avsnittet Rapporteringskällor {#the-goals-settings-page-does-not-show-the-reporting-sources-section}

Det här problemet är troligen ett [A4T Analytics Cloud Configuration](/help/sites-administering/target-configuring.md) Provisioning-problem.

#### Lösning {#solution-7}

Du måste verifiera att A4T är korrekt aktiverat för ditt Target-konto genom att skicka följande verifieringsbegäran till AEM:

```
http://localhost:4502/etc/cloudservices/testandtarget/<YOUR-CONFIG>/jcr:content.a4t.json

{
    "a4tEnabled": true,
    "sharedsecret": "SECRET",
    "proxyUrl": "/libs/cq/contentinsight/content/proxy.reportingservices.json",
    "active": "true",
    "pageName": "",
    "url": "https://api5.omniture.com/rs/0.5/",
    "username": "USER@DOMAIN"
}
```

Om svaret innehåller raden kontaktar du `a4tEnabled:false`Adobes kundtjänst [](https://helpx.adobe.com/contact.html) för att få ditt konto etablerat korrekt.

### Användbara mål-API:er {#helpful-target-apis}

Nedan visas två mål-API:er som kan vara användbara vid felsökning av Target-problem:

* Hämta målslutpunkten för en angiven klientkod

```
https://admin.testandtarget.omniture.com/rest/v1/endpoint/<CLIENTCODE>.json

{"api":"https://admin<N>.testandtarget.omniture.com/admin/rest/v1"}
```

* Hämta en klientprofil

```
https://admin<N>.testandtarget.omniture.com/admin/rest/v1/clients/<CLIENT>?email=<EMAIL>&password=<PASSWORD>

Response for N=4, CLIENT-dayintegrationintern
{
    "clientCode": "dayintegrationintern",
    "companyName": "Day Integration - Internal",
    "omnitureCompanyId": "Day Integration Internal",
    "softTraxId": -1,
    "address1": "XYZ",
    "city": "San Francisco",
    "state": "ca",
    "zip": "94107",
    "country": "UNITED STATES",
    "locale": "de_DE",
    "timeZone": "Europe/Berlin",
    "phone": "XX-XX-XXXX",
    "serviceLevel": "Up to 100,000",
    "privileges": [
        "a4t",
        "hosts",
        "TnT-SC-integration",
        "mvt",
        "steps",
        "testing-campaigns",
        "view-snapshot",
        "on-site-editor",
        "optimizing-campaign",
        "third-party-id-support",
        "landing-page-campaigns",
        "segment",
        "rest-create-user",
        "advanced-targeting",
        "mobile-device-targeting",
        "beta",
        "geolocation"
    ]
}
```

