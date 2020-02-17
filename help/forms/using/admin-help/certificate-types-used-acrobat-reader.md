---
title: Certifikattyper som används av Acrobat Reader DC-tillägg
seo-title: Certifikattyper som används av Acrobat Reader DC-tillägg
description: Lär dig mer om de certifikattyper som används i Acrobat Reader DC-tillägg.
seo-description: Lär dig mer om de certifikattyper som används i Acrobat Reader DC-tillägg.
uuid: 93c02abc-2d5a-44ed-b93c-981afbd0553d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 331b9317-87b5-4a96-a1bc-429675ff90c5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Certifikattyper som används av Acrobat Reader DC-tillägg {#certificate-types-used-by-acrobat-reader-dc-extensions}

Certifikatgranskaren ger följande information om certifikatet:

* Certifikatets eget namn
* Certifikatprofiler
* Giltighetsperiod
* Användningsrättigheter för Acrobat Reader DC-tillägg

## Certifikatets eget namn {#certificate-friendly-name}

Det &quot;egna&quot; namnet på ett Acrobat Reader DC-tilläggscertifikat är en sträng som beskriver certifikatets egenskaper, som i följande exempel:

ÄR 2D-streckkod, fullständig produktion V6.1 P8 0002054

Strängen innehåller följande element:

**** Certifikattyp: Beskriver de AEM-formulärmoduler som certifikatet aktiverar och aktiveringsnivån, till exempel ARE 2D-streckkod Full. En lista över tillgängliga certifikattyper finns i kolumnen Typ i tabellen i avsnittet Certifikatprofiler.

**** Distributionstyp: Anger certifikatets avsedda användning, t.ex. produktion. Värdet kan vara Evaluation eller Production. En lista över distributionstyper som är associerade med varje certifikattyp finns i kolumnen Distributionstyp i tabellen i avsnittet Certifikatprofiler.

**** Användarrättigheter: Beskriver vilken version av användarrättighetsalgoritmen som certifikatet kan användas för, till exempel V6.1. Den här versionen betyder inte versionen av Acrobat eller Acrobat Reader DC-tilläggen.

**** Profilkod: Profilkoden är en kort beskrivning av fullständiga certifikategenskaper, till exempel P8. En lista över profilkoder som är associerade med varje filtyp finns i kolumnen Profilkod i tabellen i avsnittet Certifikatprofiler.

**** Serienummer: Varje certifikat som utfärdas av Adobe tilldelas ett serienummer, till exempel 0002054. Adobe Enterprise Support eller en Adobe Enterprise-kontorepresentant kan använda detta serienummer för att spåra certifikatet till en viss produktorder eller till en OEM-relation.

## Certifikatprofiler {#certificate-profiles}

I följande tabell visas de certifikatprofiler som du kan stöta på när du analyserar tilläggscertifikat för Acrobat Reader DC.

<table>
 <thead>
  <tr>
   <th><p>Profilkod</p></th>
   <th><p>Typ</p></th>
   <th><p>Giltighetsperiod</p></th>
   <th><p>Distributionstyp</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>P1</p></td>
   <td><p>SAP-produktion</p></td>
   <td><p>Max</p></td>
   <td><p>Produktion</p></td>
  </tr>
  <tr>
   <td><p>P2</p></td>
   <td><p>SAP Internal Test</p></td>
   <td><p>2 år</p></td>
   <td><p>Utvärdering och test</p></td>
  </tr>
  <tr>
   <td><p>P3</p></td>
   <td><p>Acrobat Reader DC-tillägg, produktion</p></td>
   <td><p>Max</p></td>
   <td><p>Produktion</p></td>
  </tr>
  <tr>
   <td><p>P4</p></td>
   <td><p>Acrobat Reader DC-tillägg, intern Adobe-användning</p></td>
   <td><p>2 år</p></td>
   <td><p>Produktion</p></td>
  </tr>
  <tr>
   <td><p>P5</p></td>
   <td><p>Acrobat Reader DC-tillägg, partnerintegrering</p></td>
   <td><p>2 år</p></td>
   <td><p>Utvärdering och test</p></td>
  </tr>
  <tr>
   <td><p>P6</p></td>
   <td><p>Acrobat Reader DC-tillägg, utvärdering</p></td>
   <td><p>60 dagar</p></td>
   <td><p>Utvärdering</p></td>
  </tr>
  <tr>
   <td><p>P8</p></td>
   <td><p>Formulär, produktion</p></td>
   <td><p>Max</p></td>
   <td><p>Produktion</p></td>
  </tr>
  <tr>
   <td><p>P9</p></td>
   <td><p>Adobe Acrobat 7.x, produktion</p></td>
   <td><p>Max</p></td>
   <td><p>Produktion</p></td>
  </tr>
  <tr>
   <td><p>I10</p></td>
   <td><p>Formulär; kan användas av OEM-tillverkare</p></td>
   <td><p>Max</p></td>
   <td><p>Produktion och utvärdering</p></td>
  </tr>
  <tr>
   <td><p>I11</p></td>
   <td><p>Formulär; kan användas av OEM-tillverkare</p></td>
   <td><p>Max</p></td>
   <td><p>Produktion och utvärdering</p></td>
  </tr>
  <tr>
   <td><p>I12</p></td>
   <td><p>Endast underskrift; kan användas av OEM-tillverkare</p></td>
   <td><p>Max</p></td>
   <td><p>Produktion och utvärdering</p></td>
  </tr>
  <tr>
   <td><p>I13</p></td>
   <td><p>Endast offlinekommentarer; kan användas av OEM-tillverkare</p></td>
   <td><p>Max</p></td>
   <td><p>Produktion och utvärdering</p></td>
  </tr>
  <tr>
   <td><p>I14</p></td>
   <td><p>Endast kommentarer. kan användas av OEM-tillverkare</p></td>
   <td><p>Max</p></td>
   <td><p>Produktion och utvärdering</p></td>
  </tr>
  <tr>
   <td><p>I15</p></td>
   <td><p>Fullständigt tillstånd; kan användas av OEM-tillverkare</p></td>
   <td><p>Max</p></td>
   <td><p>Produktion och utvärdering</p></td>
  </tr>
 </tbody>
</table>

## Giltighetsperiod {#validity-period}

Utvärderingscertifikat utfärdas till kunder och utvecklare så att de kan utvärdera och utveckla produktexempel. Dessa certifikats giltighetstid är mellan 60 och 90 dagar. De löper ut i slutet av den andra månaden efter den månad då uppgifterna om utfärdandet daterades.

Certifikat för partnerintegrering utfärdas till Adobes affärspartners för att stödja programutveckling, integrering, prototyper och demonstration. Dessa certifikat gäller i två år från och med utfärdandedagen.

Adobes certifikat för intern användning används i Adobe för att stödja programutveckling, integrering, prototyper och demonstration. Dessa certifikat gäller i två år från och med utfärdandedagen.

Produktionscertifikat utfärdas till kunder som har köpt Acrobat Reader DC-tillägg. Dessa certifikat gäller under den maximala period som tillåts av certifikatutfärdaren (CA), vilket visas som *Max* i tabellen Certifikatprofiler.

## Användningsrättigheter för Acrobat Reader DC-tillägg {#acrobat-reader-dc-extensions-usage-rights}

När du granskar Acrobat Reader DC-tilläggscertifikatet i Certifikatgranskaren kan du välja användningsbehörighetsobjektet på fliken Information (om den är konfigurerad) för att se en detaljerad lista över de användningsrättigheter för Adobe Reader som certifikatet kan aktivera. De användarrättigheter som är aktiverade för ett visst dokument kan vara en delmängd av de som är aktiverade av certifikatet.

Om det krävs kommentarer online i en icke-samarbetsmiljö kontaktar du Adobes support för mer information. Egenskapen Mode matchar distributionstypen och är antingen *produktion* eller *utvärdering*.

Tillåtna användningsrättigheter för Acrobat Reader DC-tillägg består av ett eller flera specifika element. Dessa element används i olika kombinationer för att uppnå olika typer av licensierad produktfunktionalitet.

<table>
 <thead>
  <tr>
   <th><p>Element för användningsrättigheter</p></th>
   <th><p>Funktion aktiverad i Adobe Reader vid visning av ett rättighetsaktiverat PDF-dokument</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>FormFillInAndSave</p></td>
   <td><p>Fyll i formulärfält och spara filer lokalt.</p></td>
  </tr>
  <tr>
   <td><p>FormImportExport</p></td>
   <td><p>Importera och exportera formulärdata som FDF-, XFDF-, XML- och XDP-filer.</p></td>
  </tr>
  <tr>
   <td><p>FormAddDelete</p></td>
   <td><p>Lägg till, ändra eller ta bort fält och fältegenskaper i PDF-formuläret.</p></td>
  </tr>
  <tr>
   <td><p>SubmitStandalone</p></td>
   <td><p>Skicka data via e-post eller offline till en server när den inte körs i en webbläsarsession.</p></td>
  </tr>
  <tr>
   <td><p>SpawnTemplate</p></td>
   <td><p>Skapa sidor från mallsidor i samma PDF-formulär.</p></td>
  </tr>
  <tr>
   <td><p>Signering</p></td>
   <td><p>Signera och spara PDF-dokument digitalt och rensa digitala signaturer.</p></td>
  </tr>
  <tr>
   <td><p>AnnotModify</p></td>
   <td><p>Skapa och ändra dokumentanteckningar som kommentarer.</p></td>
  </tr>
  <tr>
   <td><p>AnnotImportExport</p></td>
   <td><p>Spara anteckningar som kommentarer i en separat datafil och läs in kommentarer från en fil.</p></td>
  </tr>
  <tr>
   <td><p>BarcodePlaintext</p></td>
   <td><p>Skriv ut ett dokument med formulärdata streckkodade i okrypterad form som inte kräver att licensierad serverprogramvara avkodar.</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>Överför och ladda ned kommentarer som kommentarer till och från en dokumentgranskning online och kommentarserver.</p></td>
  </tr>
  <tr>
   <td><p>FormOnline</p></td>
   <td><p>Anslut till webbtjänster eller databaser som är definierade i ett PDF-formulär.</p></td>
  </tr>
  <tr>
   <td><p>EFModif</p></td>
   <td><p>Ändra inbäddade filobjekt som är kopplade till PDF-dokumentet.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Användningsrättigheter för Acrobat Reader DC-tillägg kan endast licensieras från Adobe i vissa kombinationer som fungerar tillsammans. Det går inte att licensiera dessa funktioner separat. Om du vill ha information om vilka kombinationer av användarrättigheter som finns kontaktar du en kontorepresentant för AEM-formulär.

