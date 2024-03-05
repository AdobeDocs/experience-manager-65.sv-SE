---
title: Programfixar för AEM Forms
description: Innehåller information om hur du hämtar och installerar en snabbkorrigering för AEM Forms.
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
source-git-commit: 0aa929021aa724e4ec18d49fea26f8c0b0538bdc
workflow-type: tm+mt
source-wordcount: '322'
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

1. Ladda ned [Hotfix](#hotfix-for-adaptive-forms) från Software Distribution link.
1. Extrahera Hotfix-arkivfilen så att du kan hämta Experience Manager-paketfiler (.zip) och paketfiler (.jar).
1. Överför och installera paketet (.zip) via [Pakethanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).
1. Öppna konfigurationshanterarpaketen `https://server:host/system/console/bundles`, ladda upp och installera paketet (.jar). Programfixen är installerad.
