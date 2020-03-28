---
title: Grundläggande om uppdrag
seo-title: Grundläggande om uppdrag
description: Översikt över uppdragsfunktionen för aktiveringscommunities
seo-description: Översikt över uppdragsfunktionen för aktiveringscommunities
uuid: e49fce26-1091-4f37-93e8-c4ec85371811
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 6bac681e-59e1-4786-9c50-6679c936cfd1
docset: aem65
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# Grundläggande om uppdrag {#assignments-essentials}

Läs vidare om du vill veta mer om den viktigaste informationen för att arbeta med uppdragsfunktionen på webbplatser [i användargrupper](/help/communities/overview.md#enablement-community) .

Tilldelningsfunktionen är möjligheten att tilldela aktiveringsresurser och utbildningsvägar till medlemmar i aktiveringscommunityn.

## Grundläggande för klientsidan {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/aktivering/components/hbs/myassign</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>oklanderlig</strong></a></td>
   <td>Nej</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>klientlibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.mysigned<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningpath</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/enablement/components/hbs/myassigned/myassigned.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/enablement/components/hbs/myassigned/clientlibs/myassigned.css</td>
  </tr>
  <tr>
   <td><strong> egenskaper</strong></td>
   <td>Se, <a href="/help/communities/assignments.md">Uppdragsfunktion</a></td>
  </tr>
 </tbody>
</table>

### Status för slutförande och slutförande {#completion-and-success-status}

Slutförings- och Slutförandestatus används i rapporter och statusbanners för tilldelningar.

Slutförandestatus:

* Inte tilldelad
* Inte startad (ny)
* Pågår
* Slutförd

Status:

* Okänd
* Pass
* Misslyckades

De enda möjliga kombinationerna av slutförande och lyckad status är:

| **Slutförande** | **Lyckades** |
|---|---|
| Har inte startats | Okänd |
| Pågår | Okänd |
| Slutförd | Pass |
| Slutförd | Misslyckades |

## Grundläggande för serversidan {#essentials-for-server-side}

### Tilldelningsfunktion {#assignments-function}

En community-platsstruktur som innehåller [uppdragsfunktionen](/help/communities/functions.md#assignments-function), innehåller en konfigurerad ` [assignments](/help/communities/assignments.md)` komponent.

### Referens-API:er {#reference-apis}

* [API för aktivering](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [Rapporterings-API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [API för rapporteringsanalys](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/analytics/api/package-summary.html)

