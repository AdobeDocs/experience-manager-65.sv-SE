---
title: Programfix AEM Form Service Pack
description: Tillhandahåller information om hur du hämtar och installerar snabbkorrigeringen för AEM Forms Service Pack
source-git-commit: 169d407835098add0312b0d12c2c80035b525762
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# Adobe Experience Manager Hotfixes{#aem-form-hotfix}

Installationen av den senaste [AEM Service Pack](/help/release-notes/release-notes.md) Vi rekommenderar att du inkluderar säkerhet, prestanda, stabilitet och viktiga kundkorrigeringar och förbättringar som har släppts sedan Adobe Experience Manager 6.5 blev allmänt tillgängligt.

## Programfixar för Adaptive Forms {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>Datum</strong></td>
    <td><strong>Programfixnamn</strong></td>
    <td><strong>Korrigeringar</strong></td>
   </tr>
   <tr>
    <td>20 november 2023</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">Programfix för AEM Service Pack 6.5.18.0 för Linux</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">Programfix för AEM Service Pack 6.5.18.0 för Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">Programfix för AEM Service Pack 6.5.18.0 för Mac OS</a></li>
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

## Hämta och installera Hotfix {#download-install-hotfix}

Utför följande steg för att hämta och installera programfixen:

1. Ladda ned [Hotfix](#hotfix-for-adaptive-forms) från SD-länken.
1. Extrahera Hotfix-arkivfilen så att du kan hämta Experience Manager-paketfiler (.zip) och paketfiler (.jar).
1. Överför och installera paketet (.zip) via Package Manager.
1. Öppna konfigurationshanterarpaketen `https://server:host/system/console/bundles`, ladda upp och installera paketet (.jar).
