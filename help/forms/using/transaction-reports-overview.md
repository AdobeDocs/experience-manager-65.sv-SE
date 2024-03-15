---
title: Översikt över transaktionsrapporter
description: Räkna med alla inskickade blanketter, interaktiv kommunikation, dokument som konverterats till ett format till ett annat, med mera
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Transaction Reports
exl-id: bb812614-f4d8-4f57-bea2-8f7d31457039
source-git-commit: d0db00de6b767a12a9492bbbcec49a8c5d25ff27
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Transaktionsrapporter för AEM Forms på OSGi {#transaction-reports-overview}

<!--## Introduction {#introduction}

Transaction reports in AEM Forms let you keep a count of all transactions taken place since a specified date on your AEM Forms deployment. The objective is to provide information about product usage and help business stakeholders understand their digital processing volumes. Examples of a transaction include:

* Submission of an adaptive form, an HTML5 Form, or a form set
* Rendition of a print or a web version of an interactive communication
* Conversion of a document from one file format to another

For more information on what is considered a transaction, see [Billable APIs](../../forms/using/transaction-reports-billable-apis.md).-->

Transaktionsregistrering är inaktiverat som standard. Du kan [aktivera transaktionsregistrering](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) från AEM webbkonsol. Du kan visa transaktionsrapporter om författare, bearbetning eller publicering. Visa transaktionsrapporter om författare eller bearbetningsinstanser för en sammanställd summa av alla transaktioner. Visa transaktionsrapporter på publiceringsinstanserna för att se antalet transaktioner som bara äger rum på den publiceringsinstans som rapporten körs från.

Skapa inte innehåll (skapa anpassningsbara formulär, interaktiv kommunikation, teman och andra redigeringsaktiviteter) eller bearbeta dokument (använd arbetsflöden, dokumenttjänster och andra bearbetningsaktiviteter) på samma AEM. Behåll transaktionsinspelningen inaktiverad för AEM Forms-servrar som används för att skapa innehåll. Låt transaktionsregistrering vara aktiverat för AEM Forms-servrar som används för att bearbeta dokument.

![sample-transaction-report-author-1](assets/sample-transaction-report-author-1.png)

En transaktion finns kvar i bufferten under en angiven period (Tömningstid för buffert + Omvänd replikeringstid). Som standard tar det ca 90 sekunder för antalet transaktioner att återspeglas i transaktionsrapporten.

Åtgärder som att skicka ett PDF-formulär, använda agentanvändargränssnittet för att förhandsgranska interaktiv kommunikation eller använda icke-standardiserade metoder för att skicka formulär räknas inte som transaktioner. AEM Forms tillhandahåller ett API för att registrera sådana transaktioner. Anropa API:t från dina anpassade implementeringar för att registrera en transaktion.

## Topologi som stöds {#supported-topology}

Transaktionsrapporter finns endast för AEM Forms i OSGi-miljö. Det stöder författarpublicering, författarbearbetning-publicering och endast bearbetningstopologier. Till exempel finns topologier i [Arkitektur och driftsättningstopologier för AEM Forms](../../forms/using/transaction-reports-overview.md).

Transaktionsantalet replikeras baklänges från publiceringsinstanser till författare eller bearbetningsinstanser. En indikativ topologi för författarpublicering visas nedan:

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>AEM Forms transaktionsrapporter stöder inte topologier som bara innehåller publiceringsinstanser.

### Riktlinjer för att använda transaktionsrapporter {#guidelines-for-using-transaction-reports}

* Inaktivera transaktionsrapporter för alla författarinstanser som rapporter om författarinstanser inkluderar transaktioner som registrerats under redigeringsaktiviteter.
* Aktivera **Visa endast transaktioner från publicering** på författarinstansen för att visa kumulativa transaktioner från alla publiceringsinstanser. Du kan också visa transaktionsrapporter för varje publiceringsinstans för faktiska transaktioner endast för den aktuella publiceringsinstansen.
* Använd inte författarinstanser för att köra arbetsflöden och bearbeta dokument.
* Innan du använder transaktionsrapportering måste du se till att omvänd replikering är aktiverat för alla publiceringsinstanser om du har en tologi med publiceringsservrar.
* Transaktionsdata återreplikeras från en publiceringsinstans till endast motsvarande författare eller bearbetningsinstans. Författaren eller bearbetningsinstansen kan inte replikera data till en annan instans. Om du till exempel har en topologi för redigeringsbearbetning/publicering, replikeras aggregerade transaktionsdata bara till bearbetningsinstansen.

## Relaterade artiklar {#related-articles}

* [Visa och förstå en transaktionsrapport för AEM Forms på OSGi](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [Transaction Reports Billable APIs for AEM Forms on OSGi](../../forms/using/transaction-reports-billable-apis.md)
* [Registrera en transaktion för anpassade implementeringar för AEM Forms på OSGi](/help/forms/using/record-transaction-custom-implementation.md)
