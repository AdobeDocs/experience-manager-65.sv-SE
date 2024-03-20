---
title: API:er för systeminformationstjänst
description: Det här dokumentet innehåller detaljerad information om de API:er som tillhandahålls av systeminformationstjänsten.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 4da96c8f-8bd0-4cad-9087-18e324f084e7
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# API:er för systeminformationstjänst {#system-information-service-apis}

Systeminformationstjänsten tillhandahåller en uppsättning REST API:er för att hämta information. Följande tabell innehåller detaljerad information om API:erna:

<table>
 <thead>
  <tr>
   <th><p>Namn</p></th>
   <th><p>URL</p></th>
   <th><p>Beskrivning</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>SystemInfo.properties</p></td>
   <td><p>https://'[server]:[port]'/rest/services/SystemInfo.properties'</p></td>
   <td><p>Detta API är en wrapper för <a href="https://docs.oracle.com/javase/6/docs/api/java/lang/System.html#getProperties()">system.getProperties</a> Java API. Den hämtar konfigurationen för den aktuella arbetsmiljön. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.envVar</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.envVar</p></td>
   <td><p>Hämtar alla miljövariabler i värdoperativsystemet. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.logs</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.logs</p></td>
   <td><p>Hämtar en zip-fil som innehåller programserverloggar. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.config</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.config</p></td>
   <td><p>Hämtar allt innehåll i filen config.xml. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.services</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.services</p></td>
   <td><p>Hämtar status- och konfigurationsparametrar för AEM formulärtjänster.</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.vitalDetails</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.essentialDetails</p></td>
   <td><p>Hämtar serverns drifttid, JVM-argument, systemminne, stackstorlek, operativsystemets namn, antal aktiva trådar och trådantal. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.coreSettings</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.coreSettings</p></td>
   <td><p>Hämtar värden för följande egenskaper:</p>
    <ul>
     <li><p>AdobeTempDir</p></li>
     <li><p>AdobeServerFontDir</p></li>
     <li><p>CustomerFontDir</p></li>
     <li><p>GlobalDocumentStorageRootDir</p></li>
     <li><p>DefaultDocumentMaxInlineSize</p></li>
     <li><p>DefaultDocumentDisposeTimeout</p></li>
     <li><p>EnableDocumentDBStorage</p></li>
     <li><p>GlobalDocumentStorageUseNetworkShare</p></li>
     <li><p>EnableFIPS</p></li>
     <li><p>EnableWSDL</p></li>
     <li><p>DataServicesConfigFile </p></li>
     <li><p>EnableRDS</p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.database</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.database</p></td>
   <td><p>Hämtar detaljerad information om databasen.</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.licenseInfo</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.licenseInfo</p></td>
   <td><p>Hämtar versions- och licensinformation för installerade AEM. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfNo.serverConfig</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.serverConfig</p></td>
   <td><p>Hämtar konfigurationsfiler för värdprogramservern. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>Hämtar antal och stackspårning för aktiva trådar. Följande parametrar godkänns:</p>
    <ul>
     <li><p>iterationer= [n]: Anger antalet iterationer. Ersätt n med en siffra. </p></li>
     <li><p>Fördröjning= [n]: Anger antalet millisekunder som ska vänta innan nästa iteration startas. </p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.info</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.info</p></td>
   <td><p>Detta API är en wrapper för alla API:er för systeminformationstjänsten. Internt körs alla API:er för systeminformation och information hämtas i zip-format. </p><p><i><strong>anteckning</strong>: SystemInfo.info innehåller inte antal och stackspårning av aktiva trådar. </i></p></td>
  </tr>
 </tbody>
</table>
