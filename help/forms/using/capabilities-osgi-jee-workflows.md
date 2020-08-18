---
title: Åtgärder och funktioner i formulärcentrerade AEM arbetsflöden i OSGi- och AEM Forms JEE-arbetsflöden
description: Åtgärder och funktioner i formulärcentrerade AEM arbetsflöden i OSGi- och AEM Forms JEE-arbetsflöden
contentOwner: khsingh
translation-type: tm+mt
source-git-commit: dfa5a0dbfdd2c63ea0ec66d805e8b452baa3d0ac
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 19%

---


# Åtgärder och funktioner i formulärcentrerade AEM arbetsflöden i OSGi- och AEM Forms JEE-arbetsflöden {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## AEM Inkorgen och HTML-arbetsytan {#aem-inbox-and-html-workspace}

Du kan använda AEM Inbox för att köra och övervaka Forms-centrerade AEM arbetsflöden i OSGi. HTML-arbetsytan gör att du kan köra och övervaka AEM Forms JEE-arbetsflöden. Följande tabell hjälper dig att förstå olika viktiga åtgärder som är tillgängliga i AEM Inbox för Forms-baserade AEM Workflows on OSGi and in HTML Workspace for AEM Forms JEE Workflows.

<table>
 <tbody>
  <tr>
   <td>Åtgärder</td>
   <td>AEM</td>
   <td>HTML-arbetsyta</td>
  </tr>
  <tr>
   <td>Starta en process, en uppgift eller ett formulärprogram<br /> </td>
   <td>Stöds<br /> </td>
   <td>Stöds<br /> </td>
  </tr>
  <tr>
   <td>Skicka uppgifter</td>
   <td>Stöds<br /> </td>
   <td>Stöds<br /> </td>
  </tr>
  <tr>
   <td>Tilldela en uppgift till en grupp</td>
   <td>Stöds<br /> </td>
   <td>Stöds<br /> </td>
  </tr>
  <tr>
   <td>Skicka till flera rutter</td>
   <td>Stöds<br /> </td>
   <td>Stöds<br /> </td>
  </tr>
  <tr>
   <td>Spåra aktivitetshistorik och uppgiftssammanfattning</td>
   <td>Stöds<br /> </td>
   <td>Stöds<br /> </td>
  </tr>
  <tr>
   <td>E-postaviseringar</td>
   <td>Stöds<br /> </td>
   <td>Stöds<br /> </td>
  </tr>
  <tr>
   <td>Tilldela uppgifter igen</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Bifogade filer på fältnivå för anpassade formulär</td>
   <td>Stöds</td>
   <td>Stöds ej</td>
  </tr>
  <tr>
   <td>Kalendervy</td>
   <td>Stöds</td>
   <td>Stöds ej</td>
  </tr>
  <tr>
   <td>Kommentarer på aktivitetsnivå</td>
   <td>Stöds</td>
   <td>Stöds ej</td>
  </tr>
  <tr>
   <td>Köer (delad personlig kö, göra anspråk på uppgifter från kö)</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Underrättelse utanför kontoret</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
    <tr>
   <td>Anpassa gränssnittselement</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Tilldela en uppgift till flera användare</td>
   <td>Stöds ej</td>
   <td>Stöds</td>
  </tr>
 </tbody>
</table>

## Formulärbaserade AEM arbetsflöden för OSGi- och AEM Forms JEE-arbetsflöden {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

Formulärbaserade AEM arbetsflöden för OSGi- och AEM Forms JEE-arbetsflöden (AEM Forms on JEE Process Management) har en annan uppsättning funktioner. Följande tabell hjälper dig att förstå viktiga funktioner som finns i formulärbaserade AEM arbetsflöden i OSGi och AEM Forms i JEE-arbetsflöden:

<table>
 <tbody>
  <tr>
   <td>Funktioner</td>
   <td>Formulärbaserade AEM arbetsflöden i OSGi<br /> </td>
   <td>AEM Forms JEE Workflows</td>
  </tr>
  <tr>
   <td>Adaptiv Forms</td>
   <td>Stöds</td>
   <td>Stöds<br /> </td>
  </tr>
  <tr>
   <td>Integrering med andra AEM</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Klottersignatur</td>
   <td>Stöds</td>
   <td>Stöds<br /> </td>
  </tr>
  <tr>
   <td>Egna e-postmallar</td>
   <td>Stöds</td>
   <td>Stöds<br /> </td>
  </tr>
  <tr>
   <td>Definiera uppgiftsprioritet</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Timeout för en aktivitet efter förfallodatum</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Slingor i arbetsflödet</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Välja en tilldelad dynamiskt </td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Använda anpassade metadata</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>E-signatur (Adobe Sign)</td>
   <td>Supported <sup>[1]</sup></td>
   <td>Supported <sup>[5]</sup></td>
  </tr>
  <tr>
   <td>Hantera uppgifter och formulärprogram</td>
   <td>Supported <sup>[2]</sup><br /> </td>
   <td>Supported <sup>[2]</sup></td>
  </tr>
  <tr>
   <td>Dokumenttjänster</td>
   <td>Supported <sup>[3]</sup></td>
   <td>Supported <sup>[3]</sup></td>
  </tr>
  <tr>
   <td>Rendera slutförda uppgifter som anpassningsbara formulär eller PDF-dokument</td>
   <td>Stöds</td>
   <td>Stöds [4]</td>
  </tr>
  <tr>
   <td>Integrering med Correspondence Management</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
   <tr>
   <td>Gateways, INGA VÄNTNINGAR </td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
   <tr>
   <td>Variabler som lagrar data </td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>ELLER, OCH dela</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>User avatar</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Skicka ett e-postmeddelande i slutet av arbetsflödet</td>
   <td>Supported <sup>[7]</sup></td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Anropa en webbtjänst från ett arbetsflöde</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Digital signatur</td>
   <td>Stöds<br /> </td>
   <td>Stöds<br /> </td>
  </tr>
  <tr>
   <td>Knappen Återställ</td>
   <td>Stöds</td>
   <td>Stöds ej</td>
  </tr>
  <tr>
   <td>Arbetsflödesfaser</td>
   <td>Stöds</td>
   <td>Stöds ej</td>
  </tr>
  <tr>
   <td>Skrivskyddade anpassningsbara formulär</td>
   <td>Stöds</td>
   <td>Stöds ej</td>
  </tr>
  <tr>
   <td>Dölja standardknappen för att spara</td>
   <td>Stöds</td>
   <td>Stöds ej</td>
  </tr>
  <tr>
   <td>Detaljerad kontroll över avsnittet med arbetsflödesinformation</td>
   <td>Stöds</td>
   <td>Stöds ej</td>
  </tr>
  <tr>
   <td>Avsökning/schemaläggning</td>
   <td>Finns att köpa direkt</td>
   <td>Anpassad implementering krävs</td>
  </tr>
  <tr>
   <td>Adaptiv Forms-app</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Assembler Service</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Tjänsten PDF Generator</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Forms Service</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Utdatatjänst</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Dokumentsäkerhet</td>
   <td>Stöds</td>
   <td>Stöds </td>
  </tr>
  <tr>
   <td>Kör skript</td>
   <td>Stöder ECMAScript</td>
   <td>Stöder Java-kodfragment</td>
  </tr>
  <tr>
   <td>Assembler</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>  
  <tr>
   <td>HTML5 Forms, Interactive PDF forms, Form Set</td>
   <td>Stöds ej</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Processrapportering</td>
   <td>Stöds ej</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Digital signatur</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Startpunktskategorier</td>
   <td>Stöds ej </td>
   <td>Stöds </td>
  </tr>
  <tr>
   <td>Godkännande av gruppuppgift </td>
   <td>Stöds ej </td>
   <td>Stöds </td>
  </tr>
  <tr>
   <td>Spara utkast med ett eget namn</td>
   <td>Stöds ej </td>
   <td>Stöds </td>
  </tr>
  <tr>
   <td>Initiera en process med befintliga processdata<br /> </td>
   <td>Stöds ej</td>
   <td>Stöds </td>
  </tr>
  <tr>
   <td>Spara en startpunkt som ett utkast</td>
   <td>Stöds ej</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Hanterarvy</td>
   <td>Stöds ej</td>
   <td>Stöds<br /> </td>
  </tr>
  <tr>
   <td>Sökmallar</td>
   <td>Stöds ej</td>
   <td>Stöds<br /> </td>
  </tr>
  <tr>
   <td>Integrering med tredjepartsprogram</td>
   <td>Not Supported <sup>[6]</sup></td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Bifogade filer på aktivitetsnivå för arbetsflödesprogram eller startpunkt</td>
   <td>Stöds ej</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Påminnelse - e-post</td>
   <td>Stöds ej</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Ändra titel på timeout för uppgift</td>
   <td>Stöds ej</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>E-post om uppgiftsdelegering och aktivitetskrav</td>
   <td>Stöds ej</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Delegera mellan osammanhängande grupper</td>
   <td>Stöds ej</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>XSLT-omvandling</td>
   <td>Stöds ej</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Prioritet för dynamisk aktivitet</td>
   <td>Stöds ej</td>
   <td>Stöds ej</td>
  </tr>
  <tr>
   <td>Dynamisk titel</td>
   <td>Stöds ej</td>
   <td>Stöds ej</td>
  </tr>
    <tr>
   <td>Dynamisk beskrivning</td>
   <td>Stöds ej</td>
   <td>Stöds ej</td>
  </tr>
 </tbody>
</table>

1. Du kan använda formulärbaserade AEM arbetsflöden i OSGi för att signera ett ifyllt anpassat formulär. Formulärbaserade AEM i OSGi-arbetsflöden stöder inte formulärsignering. Signeringsfunktionen [i form](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience) stöds inte.

1. Du måste ha tillgång till AEM Inbox för att kunna köra och övervaka formulärcentrerade arbetsflöden på AEM Forms OSGi och HTML Workspace för att kunna köra och övervaka AEM Forms JEE-arbetsflöden.
1. AEM Forms Document Services finns för både formulärbaserade AEM arbetsflöden i OSGi och AEM Forms i JEE-arbetsflöden. AEM Workflow använder inbyggda dokumenttjänster för formulärbaserade AEM arbetsflöden i OSGi- och AEM Forms JEE-arbetsflöden (Process Management).
1. AEM Forms JEE-arbetsflöden kan bara återge ett anpassat formulär. Det stöder inte återgivning av anpassningsbara formulär som PDF-dokument.
1. AEM formulär JEE-arbetsflöden har inget separat steg för Adobe Sign. Du behöver ett anpassningsbart formulär som kan aktiveras av Adobe Sign för AEM formulär i JEE-arbetsflöden. Mer information finns i [Adobe Sign-dokumentationen](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. Du kan använda steget [Anropa datamodelltjänst](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) för att anropa en webbtjänst och publicera eller hämta data från ett tredjepartsprogram.
1. Du kan använda steget [Skicka e-post](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) för att skicka e-postmeddelanden.

## Skillnader mellan funktionerna AEM Inkorgen och AEM Forms app {#differences-between-aem-inbox-and-aem-forms-app-features}

Två av de framträdande sätten att starta ett Forms-orienterat arbetsflöde är att använda [AEM Inbox](../../forms/using/manage-applications-inbox.md) och AEM Forms. Funktionerna i AEM Inbox och AEM Forms App skiljer sig dock åt. AEM Inkorg fungerar endast med [Forms-centrerade arbetsflöden](../../forms/using/aem-forms-workflow.md) medan AEM Forms-appen fungerar med både Forms-centrerade arbetsflöden och processhantering.

I följande tabell visas funktionerna i AEM Inbox och AEM Forms app:

<table>
 <tbody>
  <tr>
   <td><p><strong>Åtgärder</strong></p> </td>
   <td><p><strong>AEM</strong></p> </td>
   <td><p><strong>AEM Forms App</strong></p> </td>
  </tr>
  <tr>
   <td><p>Starta ett formulärprogram</p> </td>
   <td><p>Stöds</p> </td>
   <td><p>Stöds</p> </td>
  </tr>
  <tr>
   <td><p>Skicka uppgifter</p> </td>
   <td><p>Stöds</p> </td>
   <td><p>Stöds</p> </td>
  </tr>
  <tr>
   <td><p>Delegera uppgifter</p> </td>
   <td><p>Stöds</p> </td>
   <td><p>Stöds ej</p> </td>
  </tr>
  <tr>
   <td><p>Spåra aktivitetshistorik och uppgiftssammanfattning</p> </td>
   <td><p>Stöds</p> </td>
   <td><p>Stöds ej</p> </td>
  </tr>
  <tr>
   <td><p>Lägga till bilagor på aktivitetsnivå</p> </td>
   <td><p>Stöds</p> </td>
   <td><p>Stöds</p> </td>
  </tr>
  <tr>
   <td><p>Visa bilagor på aktivitetsnivå</p> </td>
   <td><p>Stöds</p> </td>
   <td><p>Stöds</p> </td>
  </tr>
  <tr>
   <td><p>Lägga till bilagor på fältnivå</p> </td>
   <td><p>Stöds</p> </td>
   <td><p>Stöds</p> </td>
  </tr>
  <tr>
   <td><p>Visa kalendervyn</p> </td>
   <td><p>Stöds</p> </td>
   <td><p>Stöds ej</p> </td>
  </tr>
  <tr>
   <td><p>Infogning av kommentarer.</p> </td>
   <td><p>Stöds</p> </td>
   <td><p>Stöds</p> </td>
  </tr>
 </tbody>
</table>

