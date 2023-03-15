---
title: Egenskaper för konfiguration av korrespondenshantering
seo-title: Correspondence Management Configuration Properties
description: I det här avsnittet beskrivs hur du kan ändra Resursdisposition med lösningsspecifika konfigurationer. I det här avsnittet beskrivs de egenskaper som du kan redigera, med beskrivning, standardvärden och godkända värden.
seo-description: This topic explains how you can modify Asset Composer with solution-specific configurations. This topic details the properties you can edit, with their description, default values, and acceptable values.
uuid: 6b401d51-9332-459b-b751-42a9b5a1462d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: f2955419-c680-44a7-9913-c594b4577551
feature: Correspondence Management
exl-id: c9c007d0-c545-4738-b11b-4c50986342ee
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 1%

---

# Egenskaper för konfiguration av korrespondenshantering {#correspondence-management-configuration-properties}

Om du vill konfigurera de här egenskaperna öppnar du följande URL-adress i en webbläsare: `https://<server>:<port>/<contextPath>/system/console/configMgr` och markera **Konfigurationer för korrespondenshantering**.

Correspondence Management har följande konfigurationsegenskaper:

<table>
 <tbody>
  <tr>
   <th><p><strong>Egenskap</strong></p> </th>
   <th><p><strong>Beskrivning</strong></p> </th>
   <th><p><strong>Standard</strong></p> </th>
   <th><p><strong>Godtagbara värden</strong></p> </th>
  </tr>
  <tr>
   <td><p>Indrag</p> </td>
   <td>Indrag för moduler<p> </p> </td>
   <td><p>12.7mm</p> </td>
   <td><p>Valfritt tal</p> </td>
  </tr>
  <tr>
   <td>Minsta numerisk bredd</td>
   <td>Minsta bredd som ska användas i fältet punkt/nummer när numrerade listor används utom latinska nummer</td>
   <td>8.0mm</td>
   <td>Valfritt tal</td>
  </tr>
  <tr>
   <td><p>Minsta bredd för romerska siffror</p> </td>
   <td><p>Minsta bredd som ska användas på punkt-/nummerfältet när romerska siffror används</p> </td>
   <td><p>12.7mm</p> </td>
   <td><p>Valfritt tal</p> </td>
  </tr>
  <tr>
   <td>Återgivningstyp</td>
   <td>Den typ av återgivning som programmet Skapa korrespondens använder för att återge förhandsgranskningen av bokstaven. </td>
   <td>HTML Rendition</td>
   <td>HTML Rendition/PDF Rendition</td>
  </tr>
  <tr>
   <td><p>Aktivera CCR PDF-markering</p> </td>
   <td><p>Aktiverar markering på PDF i Create Correspondence-programmet</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Målmarkeringstyp</p> </td>
   <td><p>Målmarkeringstyp i programmet Skapa korrespondens</p> </td>
   <td><p>border</p> </td>
   <td><p>border/fill / none</p> </td>
  </tr>
  <tr>
   <td><p>Markeringsfärg för mål</p> </td>
   <td><p>Målmarkeringsfärg i programmet Skapa korrespondens</p> </td>
   <td><p>90;155;245</p> </td>
   <td><p>Valfri RGB-färg i formatet R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Markeringstyp för innehåll</p> </td>
   <td><p>Markeringstyp för innehåll i programmet Skapa korrespondens</p> </td>
   <td><p>Fyllning</p> </td>
   <td><p>border/fill / none</p> </td>
  </tr>
  <tr>
   <td><p>Markeringsfärg för innehåll</p> </td>
   <td><p>Markeringsfärg för innehåll i programmet Skapa korrespondens</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>Valfri RGB-färg i formatet R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Markeringstyp för fält</p> </td>
   <td><p>Markeringstyp för fält i programmet Skapa korrespondens</p> </td>
   <td><p>fill</p> </td>
   <td><p>border/fill / none</p> </td>
  </tr>
  <tr>
   <td><p>Markeringsfärg för fält</p> </td>
   <td><p>Markeringsfärg för fält i programmet Skapa korrespondens</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>Valfri RGB-färg i formatet R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Programtimeout</p> </td>
   <td><p>Programtimeout i sekunder</p> </td>
   <td><p>1200</p> </td>
   <td><p>Valfritt tal</p> </td>
  </tr>
  <tr>
   <td><p>Parameternamn för PDF-dokument</p> </td>
   <td><p>Parameternamn för PDF-dokument i efterbearbetning</p> </td>
   <td><p>inPDFDoc</p> </td>
   <td><p>Valfritt strängvariabelnamn</p> </td>
  </tr>
  <tr>
   <td><p>XML-dataparameterns namn</p> </td>
   <td><p>Parameternamn för XML-dokument (data) i efterbearbetning</p> </td>
   <td><p>inXMLDoc</p> </td>
   <td><p>Valfritt strängvariabelnamn</p> </td>
  </tr>
  <tr>
   <td><p>Parameternamn för XDP-dokument</p> </td>
   <td><p>Parameternamn för XDP-dokument som skickats till efterbearbetningen</p> </td>
   <td><p>inXDPDoc</p> </td>
   <td><p>Valfritt strängvariabelnamn</p> </td>
  </tr>
  <tr>
   <td><p>Parameternamn för omdirigerings-URL</p> </td>
   <td><p>Parameternamn för den omdirigerings-URL som skickas från efterbearbetningen Det här värdet kan vara vilket strängvariabelnamn som helst</p> </td>
   <td><p>redirectURL</p> </td>
   <td><p>Valfritt strängvariabelnamn</p> </td>
  </tr>
  <tr>
   <td><p>PDF Submit Type</p> </td>
   <td><p>PDF Submit Type (typ av PDF som genereras när formuläret skickas från Create Correspondence-programmet)</p> </td>
   <td><p>nonInteractive</p> </td>
   <td><p>interaktiv/icke-interaktiv</p> </td>
  </tr>
  <tr>
   <td><p>Optimera instansen för datamordlista</p> </td>
   <td><p>Möjliggör optimerad överföring av Data Dictionary-instansen b/w-server och klient</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Autokorrigera inkonsekvenser </p> </td>
   <td><p>När det här alternativet är aktiverat hanteras automatiskt eventuella inkonsekvenser i bokstavstilldelningar</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Använd konfigurerade dataformat</p> </td>
   <td><p>Anger om konfigurerade dataredigeringsformat och datavisningsformat ska användas</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Datavisningsformat</p> </td>
   <td><p>Anger språkspecifikt visningsformat för data</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=truelocale=de_DE; dateFormat=dd-MM-yyyy; numberDecimalSeparator=,; numberGroupSeparator=.; numberUseGroupSeparator=truelocale=fr_FR; dateFormat=dd-MM-yyyy; numberDecimalSeparator=,; numberGroupSeparator= ; numberUseGroupSeparator=truelocale=ja_JP; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td><p>—</p> </td>
  </tr>
  <tr>
   <td><p>Dataredigeringsformat</p> </td>
   <td><p>Redigera dataformat. Detta används vid skrivning av data som String eller tolkning av data från String</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td>--<p> </p> </td>
  </tr>
  <tr>
   <td><p>Hantera bokstavsinstanser vid publicering</p> </td>
   <td><p>Aktivera/inaktivera funktionen Hantera brev (gäller endast för Publish Server)</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Aktivera granskning</p> </td>
   <td><p>Aktivera/inaktivera granskningsfunktioner. Om värdet är false inaktiveras granskningsloggar för alla åtgärder</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Aktivera läsgranskning</p> </td>
   <td><p>Aktivera/inaktivera granskningsfunktioner för tillgångsläsningar</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Aktivera Skapa granskning</p> </td>
   <td><p>Aktivera/inaktivera granskningsfunktioner för att skapa resurser</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Aktivera uppdateringsgranskning</p> </td>
   <td><p>Aktivera/inaktivera granskningsfunktioner för resursuppdatering</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Aktivera Återställ granskning</p> </td>
   <td><p>Aktivera/inaktivera granskningsfunktioner för återställning av resurser</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Aktivera publiceringsgranskning</p> </td>
   <td><p>Aktivera/inaktivera granskningsfunktioner för publicering av resurser</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Aktivera SparaSomUtkastgranskning</p> </td>
   <td><p>Aktivera/inaktivera granskningsfunktioner för att spara bokstavsutkast</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Aktivera granskning</p> </td>
   <td><p>Aktivera/inaktivera granskningsfunktioner för att skicka brev</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Aktivera e-postgranskning</p> </td>
   <td><p>Aktivera/inaktivera granskningsfunktioner för e-postbrev</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Aktivera granskning av utskrift</p> </td>
   <td><p>Aktivera/inaktivera granskningsfunktioner för utskrift av brev</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Aktivera anpassad leveransgranskning</p> </td>
   <td><p>Aktivera/inaktivera granskningsfunktioner för anpassad leverans av brev</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Parameternamn för dokumentbilaga</p> </td>
   <td><p>Parameternamn för bifogade dokument som skickats till postprocessen</p> </td>
   <td><p>inAttachmentDocs</p> </td>
   <td><p>Valfritt strängvariabelnamn</p> </td>
  </tr>
  <tr>
   <td><p>CM-användarrot</p> </td>
   <td><p>URL för mappen som innehåller alla Correspondence Management-användarresurser</p> </td>
   <td><p>--</p> </td>
   <td><p>Giltig mapplats</p> </td>
  </tr>
  <tr>
   <td><p>Storlek på bokstavscache</p> </td>
   <td><p>Ange maximalt antal bokstäver som ska behållas i cachen.</p> <p>Om du ändrar det här värdet rensas <code>in-memory</code> cache.</p> </td>
   <td><p>100</p> </td>
   <td><p>Valfritt numeriskt värde</p> </td>
  </tr>
  <tr>
   <td><p>Aktivera bokstavscache</p> </td>
   <td><p>Aktivera/inaktivera bokstavscachen.</p> <p>Om du ändrar det här värdet rensas <code>in-memory </code> cache.</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Dataelementsordning</p> </td>
   <td><p>Behåller dataelementens ordning i det skapade korrespondensgränssnittet enligt sekvensen i Letter</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Support vid omladdning</p> </td>
   <td><p>Aktivera/inaktivera omladdningsstöd i bokstäver som återges på serversidan.</p> <p>Om du inaktiverar det här alternativet förbättras återgivningsprestandan för bokstäver.</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> <p> </p> </td>
  </tr>
  <tr>
   <td>Tillfällig mapp</td>
   <td>Plats för den tillfälliga mappen.</td>
   <td>acm.tpmFolder</td>
   <td> </td>
  </tr>
  <tr>
   <td>Fjärrspara</td>
   <td>Sparar bokstavsinstanser på den angivna författaren.</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Kompatibilitetsalternativ</td>
   <td>Kompatibilitetsalternativ för formatet configname:configvalue avgränsat med kommatecken.</td>
   <td>acm.compatibilityOptions</td>
   <td> </td>
  </tr>
  <tr>
   <td><p>Felsökningskatalog </p> <p> </p> </td>
   <td>Sökväg till filsystemmappen för felsökning. Om katalogen inte gör det <code>exists</code>kommer inga felsökningsdumpar att genereras.</td>
   <td>acm.debugDirectory</td>
   <td> </td>
  </tr>
 </tbody>
</table>
