---
title: Översikt över transaktionsrapporter
description: Räkna med alla inskickade blanketter, interaktiv kommunikation, dokument som konverterats till ett format till ett annat, med mera
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: bb812614-f4d8-4f57-bea2-8f7d31457039
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# Översikt över transaktionsrapporter{#transaction-reports-overview}

## Introduktion {#introduction}

Med transaktionsrapporter i AEM Forms kan du räkna med alla transaktioner som har utförts sedan ett visst datum i din AEM Forms-distribution. Målet är att tillhandahålla information om produktanvändning och hjälpa företagsintressenter att förstå sina digitala bearbetningsvolymer. Exempel på transaktioner:

* Inlämning av ett anpassningsbart formulär, ett HTML5-formulär eller en formuläruppsättning
* Återgivning av en utskrift eller webbversion av en interaktiv kommunikation
* Konvertering av ett dokument från ett filformat till ett annat

Mer information om vad som betraktas som en transaktion finns i [Fakturerbara API:er](../../forms/using/transaction-reports-billable-apis.md).

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

* [Visa och förstå transaktionsrapporter](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [Fakturerbara API:er för transaktionsrapporter](../../forms/using/transaction-reports-billable-apis.md)
* [Registrera en transaktion för anpassade implementeringar](/help/forms/using/record-transaction-custom-implementation.md)
