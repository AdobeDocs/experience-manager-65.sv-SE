---
title: Kontrollpaneler
seo-title: Kontrollpaneler
description: Lär dig hur du skapar, konfigurerar och utvecklar nya AEM.
seo-description: Lär dig hur du skapar, konfigurerar och utvecklar nya AEM.
uuid: 3eadbba2-0ce1-41be-a9f8-e6cafa109893
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 40560e06-2508-45a4-a648-39629ed54f28
translation-type: tm+mt
source-git-commit: 69dfd6b41b32cb9131fd90fd7039a0c224889db5
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 1%

---


# Kontrollpaneler{#dashboards}

När du använder AEM kan du hantera många olika typer av innehåll (t.ex. sidor, resurser). AEM Dashboards är ett enkelt och anpassningsbart sätt att definiera sidor som visar konsoliderade data.

>[!NOTE]
>
>AEM Dashboards skapas per användare så att en användare bara kan komma åt sin egen kontrollpanel.
>
>[Kontrollpanelsmallar](#creating-a-dashboard-template) kan dock användas för att dela gemensam konfiguration och Dashboard-layout.

![chlimage_1-22](assets/chlimage_1-22.jpeg)

## Administrera kontrollpaneler {#administering-dashboards}

### Skapar en instrumentpanel {#creating-a-dashboard}

Så här skapar du en ny kontrollpanel:

1. I avsnittet **Verktyg** klickar du på **Configuration Console**.
1. Dubbelklicka på **Kontrollpanelen** i trädet.
1. Klicka på **Ny instrumentpanel**.
1. Skriv **titeln** (t.ex. Min instrumentpanel) och **namnet**.
1. Klicka på **Skapa**.

### Klona en instrumentpanel {#cloning-a-dashboard}

Du kanske vill ha flera kontrollpaneler för att snabbt se information om ditt innehåll från olika vyer. AEM innehåller en klonfunktion som du kan använda för att duplicera en befintlig Dashboard för att hjälpa dig att skapa en ny Dashboard. Så här klonar du en kontrollpanel:

1. I avsnittet **Verktyg** klickar du på **Configuration Console**.

1. Klicka på **Kontrollpanel** i trädet.
1. Klicka på den kontrollpanel som du vill klona.

1. Klicka på **Klona**.

1. Skriv **namnet** på den nya instrumentpanelen.

### Tar bort en instrumentpanel {#removing-a-dashboard}

1. I avsnittet **Verktyg** klickar du på **Configuration Console**.

1. Klicka på **Kontrollpanel** i trädet.
1. Klicka på den kontrollpanel som du vill ta bort.

1. Klicka på **Ta bort**.

1. Bekräfta genom att klicka på **Ja**.

## Kontrollpanelskomponenter {#dashboard-components}

### Översikt {#overview}

Kontrollpanelskomponenter är inget mer än vanliga [AEM komponenter](/help/sites-developing/developing-components-samples.md). I det här avsnittet beskrivs rapportkomponenter som levereras med AEM.

### Rapporteringskomponenter för Web Analytics {#web-analytics-reporting-components}

AEM levereras med en uppsättning komponenter som återger flera mätvärden för dina [SiteCatalyst](/help/sites-administering/adobeanalytics.md)-data. Dessa komponenter listas i Spark under **Kontrollpanelen**.

Varje rapportkomponent har minst tre flikar:

* **Grundläggande**: innehåller huvudkonfigurationen.

* **Rapport:** innehåller konfigurationen som är specifik för varje rapport.
* **Format**: innehåller formatkonfiguration som diagramstorlek och marginal.

Rapporteringskomponenterna initieras med en standardkonfiguration som hjälper dig att snabbt konfigurera instrumentpanelen.

#### Grundkonfiguration {#basic-configuration}

Fliken **Basic** ger åtkomst till följande konfigurationsposter:

**Titel** Den titel som visas på instrumentpanelen.

**Typ av** begäranDet sätt på vilket data begärs.

**Konfiguration i SiteCatalyst (valfritt)** Den konfiguration du vill använda för att ansluta till SiteCatalyst. Om den inte anges antas konfigurationen vara konfigurerad på kontrollpanelssidan (via sidegenskaper).

**Report Suite ID (valfritt)** Den SiteCatalyst-rapportsserie som du vill använda för att generera diagrammet.

#### Rapportkonfiguration {#report-configuration}

För att kunna visa webbstatistik måste du definiera datumintervallet för de data som du vill hämta. Fliken **Rapport** innehåller två fält som definierar intervallet.

>[!NOTE]
>
>Om du anger ett stort datumintervall kan kontrollpanelens svarstider försämras.

**Datum** frånAbsolut eller relativt datum som data hämtas från.

**Datum** till absolut eller relativt datum som data hämtas till.

Varje komponent definierar också specifika inställningar.

#### Övertidsrapport {#overtime-report}

![chlimage_1-26](assets/chlimage_1-26a.png)

**Date** GranulityTime-enhet för X-axeln (t.ex. dag, timme).

**** MätvärdenListan med händelser som du vill visa.

**Elements** En lista med element som delar upp måttdata i diagrammet.

#### Rankad listrapport {#ranked-list-report}

![chlimage_1-27](assets/chlimage_1-27a.png)

**** ElementsElementet som delar upp måttdata i diagrammet.

**** MetriskHändelsen som du vill visa.

**Nej. av de översta objekten** Antal objekt som visas av rapporten.

#### Rankad rapport {#ranked-report}

![chlimage_1-28](assets/chlimage_1-28a.png)

**** MetriskHändelsen som du vill visa.

**** ElementsElementet som delar upp måttdata i diagrammet.

#### Avsnittsrapport för översta webbplatsen {#top-site-section-report}

Den här komponenten visar ett diagram över det mer besökta avsnittet på en webbplats enligt följande konfiguration.

![chlimage_1-29](assets/chlimage_1-29a.png)

**Nej. av de översta objekten** Antal avsnitt som visas i rapporten.

#### Trendrapport {#trended-report}

![chlimage_1-30](assets/chlimage_1-30a.png)

**Date** GranulityTime-enhet för X-axeln (t.ex. dag, timme).

**** MetriskHändelsen som du vill visa.

**** ElementsElementet som delar upp måttdata i diagrammet.

## Utöka instrumentpanelen {#extending-dashboard}

### Översikt {#overview-1}

Kontrollpaneler är normala sidor ( `cq:Page`), och därför kan alla komponenter användas för att montera kontrollpaneler.

Det finns en standardkomponentgrupp `Dashboard` som innehåller analysrapportkomponenter som är aktiverade i mallen som standard.

### Skapar en instrumentpanelsmall {#creating-a-dashboard-template}

En mall definierar standardinnehållet för en ny kontrollpanel. Du kan använda flera mallar för att skapa olika typer av kontrollpaneler.

Kontrollpanelsmallar skapas som andra sidmallar, förutom att de lagras under `/libs/cq/dashboards/templates/`. Se avsnittet [Skapa innehållsidesmall](/help/sites-developing/website.md#creating-the-contentpage-template).

>[!NOTE]
>
>Instrumentpanelsmallar delas mellan användare.

### Utveckla en Dashboard-komponent {#developing-a-dashboard-component}

Utveckla en kontrollpanelskomponent genom att skapa en vanlig AEM. I det här avsnittet beskrivs ett exempel på en komponent som visar de 10 viktigaste deltagarna.

![chlimage_1-31](assets/chlimage_1-31a.png)

De översta författarkomponenterna lagras i databasen på `/apps/geometrixx-outdoors/components/reporting` och består av:

1. en `jsp`-fil som läser jcr-data och definierar platshållaren `html`.

1. ett klientbibliotek som innehåller en `js`-fil som hämtar och beställer data och fyller sedan i platshållaren för `html`.

![chlimage_1-32](assets/chlimage_1-32a.png)

Följande JavaScript-fil definieras i `geout.reporting.topauthors` [klientbiblioteket](/help/sites-developing/clientlibs.md) som underordnad till själva komponenten.

[QueryBuilder](/help/sites-developing/querybuilder-api.md) används för att fråga databasen om att läsa `cq:AuditEvent`-noder. Frågeresultatet är ett JSON-objekt från vilket författarbidrag extraheras.

#### top_authors.js {#top-authors-js}

```
$.ajax({
  url: "/bin/querybuilder.json",
  cache: false,
  data: {
       "orderby": "cq:time",
       "orderby.sort": "desc",
       "p.hits": "full",
       "p.limit": 100,
       "path": "/var/audit/com.day.cq.wcm.core.page/",
       "type": "cq:AuditEvent"
   },
  dataType: "json"
}).done(function( res ) {
    var authors = {};
    // from JSON to Object
    for(var r in res.hits) {
        var userId = res.hits[r].userId;
        if(userId == undefined) {
            continue;
        }
        var auth = authors[userId] || {userId : userId};
        auth.contrib = (auth.contrib || 0) +1;

        authors[userId] = auth;
    }

    // order by contribution
    var orderedByContrib = [];
    for(var a in authors) {
        orderedByContrib.push(authors[a]);
    }
    orderedByContrib.sort(function(a,b){return b.contrib - a.contrib});

    // produce the list
    for (var i=0, tot=orderedByContrib.length; i < tot; i++) {
        var current = orderedByContrib[i];
        $("<div> #" + (i + 1) +" "+ current.userId + " (" + current.contrib +" contrib.)</div>").appendTo("#authors-list");

    }
});
```

`JSP` innehåller både `global.jsp` och `clientlib`.

#### top_authors.jsp {#top-authors-jsp}

```java
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%
%><%@include file="/libs/foundation/global.jsp" %><%
%>
<ui:includeClientLib categories="geout.reporting.topauthors" />
<%
String reportletTitle = properties.get("title", "Top Authors");
%>
<html>
     <h3><%=xssAPI.encodeForHTML(reportletTitle) %></h3>
     <div id="authors-list"></div>
</html>
```

