---
title: Programfixar för AEM Forms
description: Innehåller information om hur du hämtar och installerar en snabbkorrigering för AEM Forms.
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
source-git-commit: 276b0122fb3d88c584dd6b2b4c2c6f6eda9d0537
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# Adobe Experience Manager Forms Hotfixes{#aem-form-hotfix}

I den här artikeln listas de viktiga korrigeringar som har implementerats för att åtgärda kända fel, förbättra systemstabiliteten och förbättra AEM Forms övergripande prestanda.

## Programfixar för Adaptive Forms {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>Datum</strong></td>
    <td><strong>Hämtningslänk för snabbkorrigering (AEM Software Distribition link)</strong></td>
    <td><strong>Åtgärdade problem</strong></td>
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

## Hämta och installera en programfix {#download-install-hotfix}

Utför följande steg för att hämta och installera programfixen:

1. Ladda ned [Hotfix](#hotfix-for-adaptive-forms) från Software Distribition link.
1. Extrahera Hotfix-arkivfilen så att du kan hämta Experience Manager-paketfiler (.zip) och paketfiler (.jar).
1. Överför och installera paketet (.zip) via [Pakethanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).
1. Öppna konfigurationshanterarpaketen `https://server:host/system/console/bundles`, ladda upp och installera paketet (.jar). Programfixen är installerad.
