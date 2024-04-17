---
title: Felsöka integreringsproblem
description: Lär dig felsöka problem när du integrerar med Adobe Experience Manager.
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 11b0023e-34bd-4dfe-8173-5466db9fbe34
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 0%

---

# Felsöka integreringsproblem{#troubleshooting-integration-issues}

## Allmänna felsökningstips {#general-troubleshooting-tips}

### Kontrollera att det inte finns några JavaScript-fel {#ensure-there-are-no-javascript-errors}

Kontrollera om webbläsarens JavaScript-konsol visar några fel. Ohanterade fel kan förhindra att efterföljande kod körs korrekt. Om fel uppstår ska du kontrollera vilket skript som orsakar felet och i vilket område. Sökvägen till skriptet kan ge en indikation på vilken funktion skriptet tillhör.

### Inloggning på komponentnivå {#logging-on-component-level}

I vissa fall kan det vara praktiskt att lägga till ytterligare programsatser på komponentnivå. Eftersom komponenten återges kan du lägga till en temporär markering för att visa variabelvärden som kan hjälpa dig att identifiera potentiella problem. Till exempel:

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

Mer information om loggning finns i [Loggning](/help/sites-deploying/configure-logging.md) och [Arbeta med granskningsposter och loggfiler](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) sidor.

## Integreringsproblem med analyser {#analytics-integration-issues}

### Rapportimporteraren orsakar hög CPU-/minnesanvändning {#the-report-importer-causes-high-cpu-memory-usage}

Rapportimporteraren orsakar hög CPU-/minnesanvändning eller orsakar `OutOfMemoryError` undantag.

#### Lösning {#solution}

Du kan åtgärda problemet genom att prova följande:

* Se till att det inte finns någon stor mängd registrerade PollingImporters (se avsnittet&quot;Shutdown take a long time due to PollingImporter&quot; nedan).
* Kör rapportimporterare vid en viss tidpunkt på dagen med CRON-uttryck för `ManagedPollingImporter` konfigurationer i [OSGi-konsol](/help/sites-deploying/configuring-osgi.md).

Mer information om hur du skapar anpassade dataimporteringstjänster i AEM finns i följande artikel [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

### Avstängningen tar lång tid på grund av PollingImporter {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

Analyserna har utformats med en arvsmekanism i åtanke. Vanligtvis aktiverar du Analytics för en webbplats genom att lägga till en referens till en Analytics-konfiguration i sidegenskaperna [Cloud Service](/help/sites-developing/extending-cloud-config.md) -fliken. Konfigurationen ärvs sedan automatiskt till alla undersidor utan att du behöver referera till den igen, såvida inte en sida kräver en annan konfiguration. När du lägger till en referens till en plats skapas automatiskt flera noder (12 för AEM 6.3 och tidigare eller 6 för AEM 6.4 och senare) av typen. `cq;PollConfig` som instansierar PollingImporters som används för att importera analysdata till AEM. Resultatet blir:

* Många sidor som refererar till Analytics leder till en stor mängd PollingImporters.
* Om du dessutom kopierar och klistrar in sidor med en referens till en Analytics-konfiguration dupliceras dess PollingImporters.

#### Lösning {#solution-1}

För det första analyserar vi [error.log](/help/sites-deploying/configure-logging.md) kan ge dig lite information om mängden aktiva eller registrerade PollingImporters. Till exempel:

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

The [DTM](/help/sites-administering/dtm.md) script-taggen inkluderas inte korrekt på sidan även om konfigurationen har refererats i sidegenskaperna [Cloud Service](/help/sites-developing/extending-cloud-config.md) -fliken.

#### Lösning {#solution-2}

Du kan försöka åtgärda problemet genom att göra följande:

* Se till att krypterade egenskaper kan dekrypteras (observera att krypteringen kan använda olika automatiskt genererade nycklar för varje AEM). Mer information finns även i [Krypteringsstöd för konfigurationsegenskaper](/help/sites-administering/encryption-support-for-configuration-properties.md).
* Publicera konfigurationerna som finns i `/etc/cloudservices/dynamictagmanagement`
* Kontrollera åtkomstkontrollistor på `/etc/cloudservices`. Åtkomstkontrollistorna ska vara:

   * allow; jcr:read; webservice-support-serviclibfinder
   * allow; jcr:read; alla; `rep:glob:`&amp;ast;`/defaults/`&amp;ast;
   * allow; jcr:read; alla; `rep:glob:`&amp;ast;`/defaults`
   * allow; jcr:read; alla; `rep:glob:`&amp;ast;`/public/`&amp;ast;
   * allow; jcr:read; alla; `rep:glob:`&amp;ast;`/public`

Mer information om hur du hanterar åtkomstkontrollistor finns i [Användaradministration och -säkerhet](/help/sites-administering/security.md#permissions-in-aem) sida.

## Målintegreringsproblem {#target-integration-issues}

### Målinriktat innehåll som inte visas i förhandsgranskningsläget när anpassade sidkomponenter används {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

Problemet inträffar eftersom anpassade sidkomponenter inte innehåller rätt JSP- eller klientbibliotek som hanterar DTM-målintegreringarna.

#### Lösning {#solution-3}

Du kan testa följande lösningar:

* Se till att den anpassade `headlibs.jsp` (om `/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`) innehåller följande:

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* Se till att den anpassade `head.html` (om `/apps/<CUSTOM-COMPONENTS-PATH>/head.html`) **inte** Ta med specifika integrationsrubriker som i exemplet nedan:

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

The `servicelibs.jsp` lägger till de JavaScript-objekt för analys som krävs och läser in de molntjänstbibliotek som är kopplade till webbplatsen. För måltjänsten läses biblioteken in via `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

Den uppsättning bibliotek som läses in beror på typen av målklientbibliotek ( `mbox.js` eller `at.js`) som används i målkonfigurationen.

När DTM används för att leverera `mbox.js` eller `at.js` Kontrollera att biblioteken är inlästa innan innehållet återges. Om du använder Tag Management Systems som läser in dessa bibliotek asynkront kan det uppstå problem när målspecifik JavaScript-kod körs.

Mer information finns i [Utveckla för riktat innehåll](/help/sites-developing/target.md#understanding-the-target-component) sida.

### Felmeddelandet&quot;Report Suite ID saknas i AppMeasurementet initieras&quot; visas i webbläsarkonsolen {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

Problemet kan uppstå när Adobe Analytics implementeras på webbplatsen med DTM och använder anpassad kod. Orsaken är att `s = new AppMeasurement()` för att instansiera `s` -objekt.

#### Lösning {#solution-4}

Använd `s_gi` i stället för `new AppMeasurement` instansieringsmetod. Till exempel:

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### Ett standarderbjudande visas slumpmässigt i stället för rätt erbjudande {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

Det här problemet kan ha flera orsaker:

* Läser in målklientbibliotek ( `mbox.js` eller `at.js`) asynkront när du använder Tag Management Systems från tredje part kan det leda till att målgruppsanpassningen avbryts slumpmässigt. Målbiblioteken ska läsas in synkront i sidhuvudet. Detta gäller alltid när biblioteken levereras från AEM.

* Läser in två målklientbibliotek ( `at.js`) samtidigt, till exempel en som använder DTM och en som använder Target-konfigurationen i AEM. Detta kan orsaka konflikter för `adobe.target` definition om `at.js` olika versioner.

#### Lösning {#solution-5}

Du kan testa följande lösningar:

* Kontrollera att kundkoden som läser in DTM-liknande bibliotek (som i sin tur läser in Target-biblioteken) körs synkront i [sidhuvud](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages).
* om webbplatsen är konfigurerad att använda DTM för att leverera Target-bibliotek säkerställer att **Clientlib levererad av DTM** alternativet är markerat i [Målkonfiguration](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/target-configuring.html) för webbplatsen.

### Ett standarderbjudande visas alltid i stället för rätt erbjudande när AT.js 1.3+ används {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}

Ut ur kartongen AEM 6.2 och 6.3 är inte kompatibla med AT.js version 1.3.0+. Med AT.js version 1.3.0 och parametervalidering för dess API:er, `adobe.target.applyOffer()` kräver en mbox-parameter som inte tillhandahålls av `atjs-itegration.js` kod.

#### Lösning {#solution-6}

Så här löser du den här problemredigeringen `atjs-itegration.js` och lägg till `"mbox": mboxName` fält i parameterobjektet för `adobe.target.applyOffer()` enligt följande:

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

Det här problemet är sannolikt en [A4T Analytics Cloud-konfiguration](/help/sites-administering/target-configuring.md) provisioneringsproblem.

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

Om svaret innehåller raden `a4tEnabled:false`, contanct [Adobe kundtjänst](https://helpx.adobe.com/contact.html) för att få ditt konto etablerat korrekt.

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
