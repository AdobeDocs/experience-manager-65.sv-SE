---
title: Förhandsgranska ett formulär
description: Du kan förhandsgranska formulären innan du publicerar eller aktiverar dem för att säkerställa att de motsvarar förväntningarna. Alternativen för förhandsgranskning kan variera mellan olika formulärtyper som stöds.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
feature: Adaptive Forms,Foundation Components
exl-id: aed5703e-4fe6-4839-9657-c660ac48521e
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Förhandsgranska ett formulär {#previewing-a-form}

<span class="preview"> Adobe rekommenderar att du använder den moderna och utbyggbara datainhämtningen [Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=sv-SE) för [att skapa nya adaptiva Forms](/help/forms/using/create-an-adaptive-form-core-components.md) eller [att lägga till adaptiva Forms på AEM Sites-sidor](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter. </span>

## Ökning {#overview}

I AEM Forms kan du förhandsgranska de formulär och dokument som finns i databasen. Med Förhandsgranska vet man exakt hur formulären ser ut och beter sig när de släpps för slutanvändarna.

När du förhandsgranskar formulär återges de i ett interaktivt gränssnitt och användaren kan fylla i formulären med data. När du förhandsgranskar dokument återges de i icke-interaktivt läge och användaren kan bara visa dokumentet. För formulär finns ytterligare ett alternativ för Anpassad förhandsgranskning. Med det här alternativet kan du förhandsgranska formuläret med data från en XML-fil. Informationen fyller i vissa eller alla fält i formuläret som förhandsgranskas.

I följande tabell visas de förhandsvisningsalternativ som är tillgängliga för olika typer av formulär som stöds:

<table>
 <tbody>
  <tr>
   <td><strong>Resurstyp</strong><br /> </td>
   <td><strong>Tillgängliga alternativ för förhandsgranskning</strong><br /> </td>
  </tr>
  <tr>
   <td>Dokument</td>
   <td>PDF preview</td>
  </tr>
  <tr>
   <td>PDF Form</td>
   <td>Förhandsgranska och förhandsgranska PDF med data<br /> </td>
  </tr>
  <tr>
   <td>adaptiv form</td>
   <td>Förhandsgranska HTML och HTML med data</td>
  </tr>
  <tr>
   <td>Formulärmall</td>
   <td>PDF-förhandsgranskning, PDF-förhandsgranskning med data, HTML-förhandsvisning, HTML-förhandsvisning med data<br /> </td>
  </tr>
 </tbody>
</table>

## Förhandsgranska ett formulär {#previewing-a-form-1}

1. Markera en resurs som du vill förhandsgranska och klicka på Förhandsgranska ![aem6forms_preview](assets/aem6forms_preview.png) i verktygsfältet Åtgärder.

   >[!NOTE]
   >
   >Om du vill välja en resurs växlar du till listvyn från standardkortvyn. Klicka på ![aem6forms_viewlist](assets/aem6forms_viewlist.png) eller ![aem6forms_viewcard](assets/aem6forms_viewcard.png) för att växla vy.

1. Om du klickar på Förhandsvisa visas en lista med möjliga förhandsvisningsalternativ för den valda resurstypen. Klicka på önskat alternativ för att återge den markerade resursen på en ny flik.

   Dina alternativ är:

   * Förhandsgranska som HTML
   * Förhandsgranska med data
   * Förhandsgranska som PDF (tillgängligt för formulärmallar)

## Förhandsgranska med data {#preview-with-data}

När du väljer **Förhandsgranska med data** kan du se hur formuläret ser ut med verkliga data som anges i det. Med alternativet Förhandsgranska med data kan du överföra en XML-fil som innehåller exempelanvändardata. Exempelinformationen används för att fylla i förhandsgranskningsformuläret i det format du väljer.

1. Välj en resurs, klicka på Förhandsgranska ![aem6forms_preview](assets/aem6forms_preview.png) och välj **Förhandsgranska med data**.
1. Ange FormData som en XML-fil i dialogrutan Förhandsgranska formulär. Klicka på Förhandsgranska om du vill återge formuläret med sammanfogade data från XML.
