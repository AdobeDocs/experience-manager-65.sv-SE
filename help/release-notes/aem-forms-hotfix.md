---
title: Programfixar för AEM Forms
description: Innehåller information om hur du hämtar och installerar en snabbkorrigering för AEM Forms.
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: fb689e86deaabcc4033ed75f615086b630a9a525
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 0%

---

# Adobe Experience Manager Forms Hotfixes{#aem-form-hotfix}

I den här artikeln listas de viktiga korrigeringar som har implementerats för att åtgärda kända fel, förbättra systemstabiliteten och förbättra AEM Forms övergripande prestanda.

>[!NOTE]
>
> Programfixarna är avsedda att vara kumulativa och omfattar alla föregående korrigeringar. När du tillämpar den senaste snabbkorrigeringen på en release åtgärdar den inte bara det senaste problemet utan även alla tidigare felkorrigeringar och förbättringar.

## Programfixar för Adaptive Forms {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>Datum</strong></td>
    <td><strong>Länk för hämtning av snabbkorrigeringar (AEM Software Distribution link)</strong></td>
    <td><strong>Åtgärdade problem</strong></td>
  </tr>
  <tr>
    <td>10 juli 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-jboss.zip.zip">Programfix för AEM Service Pack 6.5.21.0 i Windows för JBoss JEE-server </a> </li>
      <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-jboss.tar.gz">Programfix för AEM Service Pack 6.5.21.0 i Linux för JBoss JEE-server </a> </li>
       <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-websphere.zip.zip">Programfix för AEM Service Pack 6.5.21.0 i Windows för Webshpere JEE-server </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-websphere.tar.gz">Programfix för AEM Service Pack 6.5.21.0 i Linux för Webshpere JEE-server</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-weblogic.zip.zip">Programfix för AEM Service Pack 6.5.21.0 i Windows för Weblogic JEE-server </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-weblogic.tar.gz">Programfix för AEM Service Pack 6.5.21.0 i Linux för Weblogic JEE-server</a> </li>
     </ul>
     </td>
    <td>
    <ul><li>När en användare uppdaterar till AEM Forms Service Pack 20 (6.5.20.0) på JEE-servern och genererar PDF med hjälp av utdatatjänster, återges PDF med tillgänglighetsproblem. (LC-3922112)</li><li>Taggad PDF som genererats med utdatatjänsten i AEM Forms JEE visar "Olämplig strukturvarning". (LC-3922038)</li><li>När ett formulär skickas i AEM Forms JEE tas instanser av ett upprepat XML-element bort från data. (LC-3922017)</li><li>När en användare i en Linux-miljö återger ett adaptivt formulär (på JEE) i HTML återges det inte korrekt. (LC-3921957)</li><li>När en användare konverterar en XTG-fil till PostScript-format med hjälp av utdatatjänsten i AEM Forms JEE misslyckas den med följande fel: AEM_OUT_001_003: Oväntat undantag: PAExecute-fel: XFA_RENDER_FAILURE. (LC-3921720)</li><li>När en användare har uppgraderat till AEM Forms Service Pack 18 (6.5.18.0) på JEE-servern återges inte HTML5 eller PDF forms och XMLFM-krascher när användaren skickar ett formulär. (LC-3921718)
    </ul>
    </td>    
  </tr>
  <tr>
    <td>21 juni 2024</td>
     <td>
     <ul>
     <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Programfix för AEM Service Pack 6.5.21.0 på JBoss JEE-server </a> </li>
      <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Programfix för AEM Service Pack 6.5.21.0 på Weblogic JEE-server </a> </li>
       <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Programfix för AEM Service Pack 6.5.21.0 på JEE-webbserver </a> </li>
        <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Programfix för AEM Service Pack 6.5.21.0 på OSGi-server </a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li> När du har uppgraderat till AEM Forms Service Pack 6.5.21.0 kan tjänsten PaperCapture inte utföra OCR-åtgärder (Optical Character Recognition) på PDF. Installationsanvisningar finns i artikeln <a href="/help/forms/using/papercapture-service-resolution.md"> troubleshooting</a> (Felsökning).(CQDOC-21680) </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>21 juni 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Fccm-ccr-content-10.0.206.zip">Programfix för AEM Service Pack 6.5.21.0 </a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>Utkastbrev med XML-data fastnar i inläsningsläget under förhandsgranskningen. Instruktioner för hämtning och installation av snabbkorrigeringen finns i avsnittet <a href="#install-hotfix"> Hämta och installera snabbkorrigering för formulärproblem </a>.(FORMS-14521)</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>16 maj 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1192-010.zip">Programfix för AEM Service Pack 6.5.20.0 för Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1192-010.zip">Programfix för AEM Service Pack 6.5.20.0 för Linux </a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1192-010.zip">Programfix för AEM Service Pack 6.5.20.0 för Apple macOS</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>I ett adaptivt formulär som baseras på en XDP-fil med inbäddade skript i kryssrutor, körs inte skripten för element efter sådana kryssrutor. Det finns en programfix för den här utgåvan. (FORMS-1424) </li>
     <li> Rader i datumväljarwidgeten trunkeras när du går igenom flera månader i snabbwidgeten för fält med redigerings-/visningsmönster. Det finns en programfix för den här utgåvan. (FORMS-13620) </li>
     <li>Det går inte att skicka formulär när DOR-tjänsten (Document of Record) används i serverdelen. Felmeddelandet som påträffades är: "Det gick inte att skicka åtgärden eftersom formulärresursen inte är korrekt tilldelad." (FORMS-13798) </li>
     <li>När ett anpassat formulär skickas från en Adobe Experience Manager Publish-instans till ett Adobe Experience Manager-arbetsflöde, kan arbetsflödet inte spara de bifogade filerna.  (FORMS-14209) </li>
     <li> När du installerar AEM 6.5 Forms Service Pack 20-paket (AEM Forms tilläggspaket för SP20) uppvisar AEM Sites användargränssnitt en avsevärd prestandaförsämring.  (FORMS-13791) </li>
     <li>Förifyllningstjänsten misslyckas med ett null-pekarundantag i Interactive Communications. (CQDOC-21355)</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>29 januari 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fforms-foundation-qs-content-4.0.170-FORMS-12692-B0001.zip">Programfix för AEM Service Pack 6.5.19.0 för Windows på JEE-server</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>På AEM Forms på JEE-servern kan inte HTML5 Forms som använder kontextsökvägen återges. (FORMS-12485, FORMS-12691).</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>29 januari 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-win-pkg-6.0.1016-004.zip">Programfix för AEM Service Pack 6.5.18.0 för Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-linux-pkg-6.0.1016-004.zip">Programfix för AEM Service Pack 6.5.18.0 för Linux</a></li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-osx-pkg-6.0.1016-004.zip">Programfix för AEM Service Pack 6.5.18.0 för Apple macOS</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li> Komponenten Skriptsignatur som är klar att användas kan inte återges för en förhandsgranskning i ett anpassat formulär. (FORMS-12073).</li>
    </ul>
    </td>    
   </tr>
   <tr>
    <td>20 november 2023</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">Programfix för AEM Service Pack 6.5.18.0 för Linux</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">Programfix för AEM Service Pack 6.5.18.0 för Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">Programfix för AEM Service Pack 6.5.18.0 för Apple macOS</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li>Inline-signering slutar fungera när en omdirigerings-URL anges i stödlinjebehållaren för ett adaptivt formulär. (FORMS-10493)</li>
    <li>DoR-mallar (Document of Record) kan inte publiceras för lokaliserade adaptiva Forms. (FORMS-10535)</li>
    <li>Interaktiv kommunikation med stora textbundna bilder kan inte öppnas i redigeringsläge. (FORMS-10578)</li>
    </ul>
    </td>    
  </tr>
  <tbody>
</table>

## Hämta och installera en programfix {#download-install-hotfix}

Utför följande steg för att hämta och installera programfixen:

1. Hämta [snabbkorrigering](#hotfix-for-adaptive-forms) från länken för programdistribution.
1. Extrahera Hotfix-arkivfilen så att du kan hämta Experience Manager-paketfiler (.zip) och paketfiler (.jar).
1. Överför och installera paketet (.zip) via [Package Manager](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).
1. Öppna konfigurationshanterarpaketen `https://server:host/system/console/bundles`, ladda upp och installera paketet (.jar). Programfixen är installerad.


## Ladda ned och installera snabbkorrigering för problem med utkast {#install-hotfix}

Så här löser du problemet:

1. Hämta [snabbkorrigeringen](#hotfix-for-adaptive-forms) från portalen för programvarudistribution.
2. Överför och installera paketet (.zip) med [CRX Package Manager](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).