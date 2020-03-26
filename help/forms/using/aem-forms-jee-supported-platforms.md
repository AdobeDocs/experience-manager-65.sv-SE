---
title: Plattformar som stöds för AEM Forms på JEE
seo-title: Plattformar som stöds för AEM Forms på JEE
description: Lista över infrastrukturkomponenter som krävs och stöds för installation av AEM Forms på JEE
seo-description: Lista över infrastrukturkomponenter som krävs och stöds för installation av AEM Forms på JEE
uuid: 777f943b-4cb4-444e-a036-8032b9fce5be
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f777865e-d4a8-40ef-87b0-130c19eb1b91
docset: aem65
translation-type: tm+mt
source-git-commit: 6cf69dc86ce70a43e77b00d6b3986fa40ae0a4ec

---


# Plattformar som stöds för AEM Forms på JEE{#supported-platforms-for-aem-forms-on-jee}

## Plattformar som stöds {#supported-platforms}

### Supportnivåer {#support-levels}

AEM Forms på JEE-server kan konfigureras med valfri kombination av operativsystem, programservrar, databaser, databasdrivrutiner, JDK, LDAP-servrar och e-postservrar som stöds.

I det här dokumentet visas vilka klient- och serverplattformar som stöds för AEM Forms på JEE. Adobe tillhandahåller flera supportnivåer, både för våra rekommenderade konfigurationer och för andra konfigurationer. I dokumentet listas även andra program som stöds och deras version, undantag, korrigeringsdefinitioner och supportregler för programfixar från tredje part.

>[!NOTE]
>
>* En fullständig lista över undantag för serverplattformar som stöds finns i [Undantag för serverplattformar](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p)som stöds.
>* AEM Forms på JEE stöder endast engelska, franska, tyska och japanska versioner av de operativsystem och program som stöds.
>



### Rekommenderade konfigurationer {#recommendedconfigurations}

Adobe rekommenderar dessa konfigurationer och ger fullständig eller begränsad support som en del av standardavtalet för programunderhåll:

<table>
 <tbody>
  <tr>
   <th>Supportnivå</th>
   <th>Beskrivning</th>
  </tr>
  <tr>
   <td>S: Stöds<br /> </td>
   <td>Adobe ger support och underhåll för denna konfiguration. Denna konfiguration omfattas av Adobes kvalitetssäkringsprocess.</td>
  </tr>
  <tr>
   <td>R: Begränsat stöd</td>
   <td>Adobe ger fullständigt stöd för den här konfigurationen när vissa förutsättningar är uppfyllda. Kontakta Adobes support för företag om du vill veta mer om villkoren och begära support.</td>
  </tr>
  <tr>
   <td>L: Begränsad support</td>
   <td>Adobe ger fullständig support och underhåll för dessa konfigurationer när vissa förutsättningar är uppfyllda. Alla funktioner är inte tillgängliga i konfigurationen. Kontakta Adobes support för företag om du vill veta mer om villkoren och begära support.<br /> </td>
  </tr>
 </tbody>
</table>

### Konfigurationer som inte stöds {#unsupported-configurations}

| Supportnivå | Beskrivning |
|---|---|
| E: Arbetet förväntas | Konfigurationen förväntas fungera och det finns inga rapporter om motsatsen. |
| Z: Stöds inte | Konfigurationen stöds inte. Adobe gör inga utfästelser om huruvida konfigurationen fungerar eller inte. |

>[!NOTE]
>
>För att hjälpa AEM Forms-kunder att minska ägandekostnaden, förenkla driftsättningsarkitekturen och modernisera utvecklingsstacken går Adobe Experience Manager Enterprise-plattform bort från applikationsserverbaserad driftsättning till förmån för fristående OSGi-baserad driftsättning. Adobe fortsätter att stödja AEM Forms JEE-stacken med en reducerad matris av infrastrukturkomponenter.
>
>I och med releasen av 6.5 stöds inte längre infrastrukturkomponenter som har den lägsta användningen bland våra kunder, enligt följande:
>・ Oracle WebLogic-programserver
>・ IBM DB2-databas
>・ Operativsystemen IBM AIX och Sun Solaris
>
>För nya installationer rekommenderar vi att man där det är möjligt använder AEM Forms i den moderna OSGi-stacken för att utnyttja de senaste innovationerna kring responsiva adaptiva formulär för mobil, interaktiv kommunikation i flera kanaler och dataintegrering i serverdelen med hjälp av Form Data Model.
>
>Vi vet att befintliga användare måste fortsätta att distribuera AEM Forms på JEE-stacken. I sådana fall kräver Adobe att AEM Forms JEE distribueras till en infrastruktur som stöds enligt beskrivningen i den här dokumentationen. Om du uppgraderar till AEM 6.5-formulär och använder en plattform som inte stöds i den tidigare AEM Forms-versionen kan du kontakta Adobe Support för att få hjälp med att uppgradera till en plattform som stöds.

### Java Virtual Machines (JVM) {#java-virtual-machines-jvm}

Adobe Experience Manager Forms kräver att en Java Virtual Machine körs, vilket tillhandahålls av Java Development Kit-distributionen (JDK). Adobe Experience Manager fungerar med följande versioner av Java Virtual Machines:

<table>
 <tbody>
  <tr>
   <th><p><strong>Plattform</strong></p> </th>
   <th><p><strong>Supportnivå</strong></p> </th>
   <th><p><strong>Patch-definitioner som stöds</strong></p> </th>
  </tr>
  <tr>
   <td><p>Oracle Java™ SE 11 (64 bitar)</p> </td>
   <td><p>Z: Stöds inte</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>Oracle Java™ SE 8 (64 bitar)</td>
   <td>S: Stöds</td>
   <td>Mindre releaser och uppdateringar</td>
  </tr>
  <tr>
   <td>IBM® J9 Virtual Machine (bygge 2.8, JRE 1.8.0)</td>
   <td>S: Stöds</td>
   <td>Mindre releaser och uppdateringar</td>
  </tr>
  <tr>
   <td>IBM® J9 Virtual Machine (bygge 2.9, JRE 1.8.0)<br /> </td>
   <td>S: Stöds</td>
   <td>Mindre releaser och uppdateringar</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* AEM Forms på JEE har endast stöd för 64-bitars JVM i produktionsmiljöer.
>* Vi rekommenderar att du följer säkerhetsbulletinerna från Java-leverantören för att säkerställa säkerheten i produktionsmiljöer och installerar de senaste Java-uppdateringarna.
>



### Databaser och CRX-beständighet {#databases-and-crx-persistence}

<table>
 <tbody>
  <tr>
   <td><p><strong>Plattform</strong></p> </td>
   <td><p><strong> Beskrivning</strong></p> </td>
   <td><p><strong>Supportnivå</strong></p> </td>
  </tr>
  <tr>
   <td><p>Filsystem</p> </td>
   <td><p>Repository Microkernel (TAR MK-filer)</p> </td>
   <td><p>Stöds</p> </td>
  </tr>
  <tr>
   <td><p>MongoDB Enterprise 4.0 </p> </td>
   <td><p>Databasmikrokernel</p> </td>
   <td><p>Stöds</p> </td>
  </tr>
  <tr>
   <td><p>Oracle Database 12c version 1</p> </td>
   <td><p>Databasmikrokernel</p> </td>
   <td><p>Stöds</p> </td>
  </tr>
  <tr>
   <td>Oracle Database 18c </td>
   <td>Databasmikrokernel</td>
   <td>Stöds</td>
  </tr>

<tr>
   <td>Oracle Database 19c </td>
   <td>Databas</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2016</p> </td>
   <td><p>Databasmikrokernel</p> </td>
   <td><p>Stöds</p> </td>
  </tr>
  <tr>
   <td>IBM DB2 11.1</td>
   <td>Databasmikrokernel</td>
   <td>R: Begränsat stöd</td>
  </tr>
    <tr>
   <td>MySQL 5.7.19 </td>
   <td>-</td>
   <td>R: Begränsat stöd</td>
  </tr>
 </tbody>
</table>

* IBM DB2 stöds inte för nya installationer. Det stöds endast för befintliga kunder som uppgraderar till AEM 6.5 Forms.
* MongoDB är en tredjepartsprogramvara och ingår inte i AEM-licenspaketet. Mer information finns på sidan [MongoDB-licenspolicy](https://www.mongodb.org/about/licensing/) .
* För att få ut mesta möjliga av din AEM-distribution rekommenderar Adobe att du licensierar MongoDB Enterprise-versionen för att få tillgång till professionell support.
* Adobes kundtjänst kommer att hjälpa dig med frågor som rör användningen av MongoDB med AEM. Mer information finns på sidan [](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)MongoDB för Adobe Experience Manager.
* &#39;Filsystem&#39; inkluderar blocklagring som är POSIX-kompatibel. Detta inkluderar nätverkslagringsteknik. Tänk på att filsystemets prestanda kan variera och påverka den övergripande prestandan. Vi rekommenderar att du läser in test-AEM i kombination med nätverks-/fjärrfilsystemet.
* Endast WiredTiger stöds för lagringsmotorn MongoDB.
* MongoDB-delning stöds inte i AEM.
* AEM Forms på JEE stöder inte MySQL för RDBMK-beständighet.
* Dokumentsäkerhetsmodulen använder inte innehållsdatabas. Det innebär att om du bara använder dokumentsäkerhet och inte tänker använda HTML Workspace, HTML5-formulär eller adaptiva formulär ska du inte installera Content Repository.
* AEM Forms på JEE stöder inte användning av MySQL för beständig AEM Repository (CRX-Repository).


### Databasdrivrutiner {#database-drivers}

<table>
 <tbody>
  <tr>
   <th>Databas </th>
   <th><p><strong>Plattform</strong></p> </th>
   <th><p><strong>Patch-definitioner som stöds</strong></p> </th>
  </tr>
  <tr>
   <td>MySQL</td>
   <td><p>MySQL Connector/J 5.7</p> <p>mysql-connector-java-5.1.44-bin.jar (version 5.1.44)</p> </td>
   <td><p>Tillhandahålls med AEM Forms för JEE-installation</p> </td>
  </tr>
  <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC-drivrutin 6.2.1.0<br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>Tillhandahålls med AEM Forms för JEE-installation.</p> </td>
  </tr>
  <tr>
   <td>Oracle</td>
   <td><p>JDBC-drivrutin för Oracle Database 19.3.0.0.0</p> <p>jodbc8.jar (version 19.3.0.0.0)<br /> </p> </td>
   <td><p>Ladda ned från <a href="https://www.oracle.com/technetwork/database/features/jdbc/jdbc-ucp-122-3110062.html">Oracles webbplats</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Programservrar {#application-servers}

<table>
 <tbody>
  <tr>
   <td><p><strong> Plattform</strong></p> </td>
   <td><p><strong>Supportnivå</strong></p> </td>
   <td><p><strong>Patch-definitioner som stöds</strong></p> </td>
  </tr>
  <tr>
   <td>IBM® WebSphere® Application Server 9.0 <sup>[1] [4]</sup><br /> </td>
   <td>S: Stöds</td>
   <td>Service Pack och viktiga uppdateringar</td>
  </tr>
  <tr>
   <td><p>JBoss® Enterprise Application Platform (EAP) 7.1.4 <sup>[2] [3] [7]</sup></p> </td>
   <td><p>S: Stöds</p> </td>
   <td><p>Patchar och kumulativa patchar för den EAP-version som stöds</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>IBM® WebSphere®-kluster stöds endast i Network Deployment-utgåvor.

### Serveroperativsystem {#server-operating-systems}

#### Produktionsmiljöer {#production-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong> Plattform</strong></p> </th>
   <th><p><strong>Supportnivå</strong></p> </th>
   <th><p><strong>Patch-definitioner som stöds</strong></p> </th>
  </tr>
  <tr>
   <td>Microsoft Windows Server 2016 (64-bitars)</td>
   <td>S: Stöds</td>
   <td>Service Pack och viktiga uppdateringar</td>
  </tr>
  <tr>
   <td><p>Red Hat Enterprise Linux 7 (Kernel 3.x) (64-bitars)</p> </td>
   <td><p>S: Stöds</p> </td>
   <td><p>Mindre releaser, kumulativa uppdateringar och viktiga uppdateringar</p> </td>
  </tr>
  <tr>
   <td><p>SUSE® Linux® Enterprise Server 12 (64-bitars)</p> </td>
   <td><p>S: Stöds</p> </td>
   <td><p>Service Pack, kumulativa patchar och viktiga säkerhetsuppdateringar</p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7 Update 3 (64-bitars)</td>
   <td>S: Stöds</td>
   <td>Service Pack, kumulativa patchar och viktiga säkerhetsuppdateringar</td>
  </tr>
  <tr>
   <td>CentOS 7 (64 bitar)<sup> [6]</sup></td>
   <td>S: Stöds</td>
   <td>Service Pack, kumulativa patchar och viktiga säkerhetsuppdateringar</td>
  </tr>
 </tbody>
</table>

#### Virtualiserad miljö {#virtualized-environment}

Du kan köra AEM Forms på JEE på en fysisk dator eller i en virtuell miljö. Om du råkar ut för något problem med AEM Forms i en virtuell miljö kan du försöka replikera problemet på en fysisk dator. Om problemet kvarstår på den fysiska datorn kontaktar du Adobes support för en lösning. Kontakta din leverantör av virtuell miljö om du inte kan replikera på en fysisk dator.

#### Utvecklingsmiljöer {#development-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong>Plattform (grundversion)</strong></p> </th>
   <th>Supportnivå</th>
   <th><p><strong>Patch-definitioner som stöds</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 64-bitars</p> </td>
   <td>E: Arbetet förväntas</td>
   <td><p>Service Pack och viktiga uppdateringar</p> </td>
  </tr>
 </tbody>
</table>

### Undantag för serverplattformar som stöds {#exceptions-to-supported-server-platforms}

Tänk på följande undantag när du väljer en plattform för att konfigurera AEM Forms på JEE-servern.

1. AEM Forms på JEE stöder inte IBM® WebSphere® med MySQL.
1. AEM Forms på JEE stöder inte och JBoss på SUSE Linux Enterprise Server 12. Endast IBM WebSphere stöds i SUSE Linux Enterprise Server 12.
1. AEM Forms på JEE stöder inte JDK med JBoss® annat än Oracle Java™ SE.
1. AEM Forms på JEE stöder inte JDK med andra IBM® WebSphere® än IBM® JDK.
1. CRX-databasen har stöd för beständighet av typen tarMK, MongoDB och relationsdatabaser (RDBMK). Du kan inte ha två olika databassystem mellan programservern och CRX-databasen. I en AEM Forms i JEE-miljö kan du dock använda MongoMK med CRX-databas och en relationsdatabas som stöds med programserver.
1. AEM Forms i JEE stöder inte WebSphere-programserver i CentOS.
1. AEM Forms på JEE stöder inte JBoss-rollbaserad åtkomstkontroll (RBAC).

Tänk dessutom på följande när du väljer programvara för Adobe AEM Forms för JEE-distributioner:

* AEM Forms på JEE stöder uppdateringar, patchar och korrigeringspaket utöver den angivna större och mindre versionen av den programvara som stöds. Uppdatering till nästa större eller mindre version stöds dock inte om det inte anges.
* Klusterbaserade installationer stöder inte TjärMK-beständighet. Mer information om hur detta fungerar finns i [Välja en beständig typ för en AEM Forms-installation](/help/forms/using/choosing-persistence-type-for-aem-forms.md).
* AEM Forms på JEE har stöd för olika tredjepartsprogram enligt vår [tredjepartspolicy](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p)för programsupport.
* AEM Forms på JEE stöder plattformar enligt stöd från tredjepartsleverantörer. Vissa kombinationer kanske inte tillåts av tredjepartsleverantörer. Många leverantörer har t.ex. inte certifierat sina programservrar med Oracle. Därför stöder inte AEM Forms på JEE dessa kombinationer. Se även till att du väljer vilka programversioner som stöds i supportmatrisen för tredjepartsleverantörer.
* AEM Forms på JEE har inte stöd för TjärMK Cold Standby.
* AEM Forms på JEE stöder inte lodrät klustring.
* AEM Forms på JEE stöder inte MySQL-databaser i en klustermiljö.
* En lista över borttagna eller uppdaterade plattformar finns i dokumentet [AEM 6.5 Forms New Feature Summary](../../forms/using/whats-new.md) .

### LDAP-servrar (tillval) {#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>Produkt (grundversion)</strong></p> </th>
   <th><p><strong>Patch-definitioner som stöds</strong></p> </th>
  </tr>
  <tr>
   <td>Oracle Unified Directory (OUD) 11g version 2</td>
   <td>Service Pack</td>
  </tr>
  <tr>
   <td>Microsoft Active Directory 2016</td>
   <td>Underhållsrelease och programfix</td>
  </tr>
  <tr>
   <td><p>IBM® Tivoli Directory Server 6.4</p> </td>
   <td><p>Funktionspaket och tillfälliga korrigeringar</p> </td>
  </tr>
 </tbody>
</table>

### E-postservrar (valfritt) {#email-servers-optional}

| Produkt |
|---|
| IBM Lotus Domino 9.0 |
| Microsoft Exchange 2013 |
| Microsoft Office 365 |

### Innehållshanterare och motsvarande kopplingar {#content-managers-and-corresponding-connectors}

<table>
 <tbody>
  <tr>
   <td><strong>Produkt<br /> </strong></td>
   <td><strong>Version</strong></td>
  </tr>
  <tr>
   <td>EMC Documentum</td>
   <td>7.3</td>
  </tr>
  <tr>
   <td>IBM Filenet</td>
   <td>5.2</td>
  </tr>
  <tr>
   <td>IBM Content Manager Server</td>
   <td>8.5 Fixpaket 2</td>
  </tr>
  <tr>
   <td>IBM Content Manager-klient</td>
   <td>8.5 </td>
  </tr>
  <tr>
   <td>Microsoft Sharepoint</td>
   <td>2016<br /> </td>
  </tr>
 </tbody>
</table>

### Stöd för Cordova {#support-for-cordova}

AEM Forms App har nu stöd för Apache Cordova. Följande plattformsspecifika versioner av Cordova stöds:

* Apache Cordova 6.4.0
* Cordova iOS 4.3.0
* Cordova Android 6.0.0
* Cordova Windows 4.4.3

### Programvarusupport för PDF Generator {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>Produkt</strong></p> </th>
   <th><p><strong>Format som stöds för konvertering till PDF</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 Classic track</a> latest version</td>
   <td>XPS, bildformat (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF och DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF och TXT</td>
  </tr>
  <tr>
   <td>WordPerfect X7</td>
   <td>WP, WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016<br /> </td>
   <td>VSD, VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Project 2016<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, bildformat (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF och TXT</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>PDF Generator stöder endast engelska, franska, tyska och japanska versioner av de operativsystem och program som stöds.
>
>Dessutom:
>
>* PDF Generator kräver 32-bitarsversionen av [Acrobat 2017 Classic track version 17.011.30078 eller senare](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) för att kunna utföra konverteringen.
>* PDF Generator stöder endast 32-bitarsversionen av Microsoft Office Professional Plus och andra program som krävs för konvertering.
>* PDF Generator stöder inte Microsoft Office 365.
>* PDF Generator-konverteringar för OpenOffice stöds bara i Windows och Linux.
>* Funktionerna OCR PDF, Optimera PDF och Exportera PDF stöds bara i Windows.
>* En version av Acrobat medföljer AEM Forms för att aktivera PDF Generator-funktioner. Den paketerade versionen ska endast nås via programmering med AEM Forms, under AEM Forms-licensperioden, för användning med AEM Forms PDF Generator. Mer information finns i produktbeskrivningen för AEM Forms enligt din distribution ([lokal](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) eller [hanterade tjänster](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)).
   >
   >
* PDF Generator-tjänsten stöder inte Microsoft Windows 10.
>



### Undantag från tillgänglighetsstöd {#exceptions-to-accessibility-support}

Följande delsystem i AEM Forms är inte [508](https://www.section508.gov/) -kompatibla:

* Gränssnitt för redigering av adaptiva formulär
* Redigeringsgränssnitt för Forms Manager
* Redigeringsgränssnitt för korrespondenshantering
* Administratörsgränssnitt (administrationskonsolens användargränssnitt)

## Systemkrav för AEM-formulär på JEE {#system-requirements-for-aem-forms-on-jee}

### Lägsta maskinvarukrav {#minimum-hardware-requirements}

<table>
 <tbody>
  <tr>
   <td>Plattform</td>
   <td>Minsta maskinvarukrav</td>
  </tr>
  <tr>
   <td>Microsoft Windows Server</td>
   <td>Intel® Xeon® E5-2680, 2,4 GHz eller motsvarande<br /> VMWare ESX 5.1 eller senare<br /> RAM: 6 GB (64-bitars operativsystem med 64-bitars JVM)<br /> ledigt diskutrymme: 15 GB temporärt utrymme plus 22 GB<br /> för AEM Forms på JEE</td>
  </tr>
  <tr>
   <td>SUSE Linux Enterprise Server</td>
   <td>Intel Xeon E5-2670v2, 1 vCPU, 2,5 GHz processor<br /> AWS m3.medium (3 ecu)<br /> RAM: 6 GB (64-bitars operativsystem med 64-bitars JVM)<br /> ledigt diskutrymme: 6 GB temporärt utrymme plus 22 GB<br /> för AEM Forms på JEE</td>
  </tr>
  <tr>
   <td>Red Hat Enterprise Linux</td>
   <td>Intel Xeon E5-2670v2, 1 vCPU, 2,5 GHz processor<br /> AWS m3.medium (3 ecu)<br /> RAM: 6 GB (64-bitars operativsystem med 64-bitars JVM)<br /> ledigt diskutrymme: 6 GB temporärt utrymme plus 22 GB<br /> för AEM Forms på JEE<br /> </td>
  </tr>
  <tr>
   <td>Maskinvarukrav för en liten produktionsmiljö</td>
   <td>
    <ul>
     <li><strong>Intel-baserad miljö</strong>: Intel® Xeon® E5-2680, 2,4 GHz eller högre. Om du använder en processor med dubbla kärnor förbättras prestandan ytterligare</li>
     <li><strong>Minne: </strong>4 GB <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Ytterligare krav finns i:

* [Systemkrav för AEM-formulär med en enda server för JEE-distribution](https://www.adobe.com/go/learn_aemforms_sysreq_single_63)
* [Systemkrav för klustrade AEM-formulär vid JEE-distribution
   ](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_63)

## Klienter som stöds för AEM Forms på JEE {#supported-clients-for-aem-forms-on-jee}

### Workbench {#workbench}

<table>
 <tbody>
  <tr>
   <th><p><strong>Plattform</strong></p> </th>
   <th><p><strong>Patch-definitioner som stöds</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 (Enterprise, Pro, Basic)</p> <p>32- eller 64-bitarsversion</p> <p> </p> </td>
   <td>Service Pack och viktiga uppdateringar</td>
  </tr>
  <tr>
   <td>Microsoft® Windows® 2016 Server</td>
   <td>Service Pack och viktiga uppdateringar</td>
  </tr>
 </tbody>
</table>

* Diskutrymme för installation: 1,7 GB endast för Workbench, 2,7 GB på en enda enhet för en fullständig installation av Workbench, Designer och exempelsammansättningen 400 MB för tillfälliga installationskataloger - 200 MB i användarens temp-katalog och 200 MB i Windows temporära katalog. Om alla dessa platser finns på en enda enhet måste det finnas 1,5 GB ledigt utrymme under installationen. De filer som kopieras till de tillfälliga katalogerna tas bort när installationen är klar.

* Minne för att köra Workbench: 2 GB RAM
* Maskinvarukrav: Intel® Pentium® 4 eller AMD-motsvarighet, 1 GHz-processor
* Minst 1 024 × 768 pixlar eller högre bildskärmsupplösning med 16-bitars färg eller högre
* TCP/IPv4- eller TCP/IPv6-nätverksanslutning till AEM Forms på JEE-server
* Du måste ha administratörsbehörighet för att installera Workbench i Windows. Om du installerar med ett icke-administratörskonto uppmanas du att ange autentiseringsuppgifter för ett lämpligt konto.

### Designer {#designer}

**Obs!** Om du vill installera Designer i Windows kör du installationsprogrammet med administratörsbehörighet.

* Microsoft® Windows® 2016 Server, Microsoft Windows 10

   * 1 GHz eller snabbare processor med stöd för PAE, NX och SSE2.
   * 1 GB RAM för 32-bitars eller 2 GB RAM för 64-bitars operativsystem
   * 16 GB diskutrymme för 32-bitars eller 20 GB diskutrymme för 64-bitars operativsystem

* Grafikminne - 128 MB GPU (256 MB rekommenderas)
* 2,35 GB ledigt hårddiskutrymme
* DVD-ROM-enhet
* Internet Explorer 10 eller 11; Firefox 45.x
* Bildskärmsupplösning på 1 024 x 768 pixlar eller högre
* Maskinvaruacceleration för video (valfritt)
* Acrobat Pro DC, Acrobat Standard DC eller Adobe Acrobat Reader DC.

### Adobe Acrobat och Adobe Reader {#adobe-acrobat-and-adobe-reader}

<table>
 <tbody>
  <tr>
   <th><p><strong>Acrobat och Adobe Reader (bas)</strong></p> </th>
   <th><p><strong>Patch-definitioner som stöds</strong></p> </th>
  </tr>
  <tr>
   <td>Acrobat 2017 (Classic-spår)</td>
   <td>Version 17.011.30078 eller senare<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>I Acrobat DC-produktfamiljen introduceras två spår för både Acrobat och Reader som i huvudsak är olika produkter: &quot;Classic&quot; och &quot;Continuous.&quot; Mer information och en jämförelse av de två spåren finns på [https://www.adobe.com/go/acrobatdctracks.](https://www.adobe.com/go/acrobatdctracks)

### Webbläsare {#browsers}

#### Stationära datorer {#desktops}

<table>
 <tbody>
  <tr>
   <th><p><strong>Webbläsare (bas)</strong></p> </th>
   <th><p><strong>Supportnivå</strong></p> </th>
   <th><p><strong>Patch-definitioner som stöds</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft Edge (Evergreen)</p> </td>
   <td><p>S: Stöds</p> </td>
   <td><p>Service Pack och uppdateringar</p> </td>
  </tr>
  <tr>
   <td><p>Mozilla Firefox (Evergreen)</p> </td>
   <td><p>S: Stöds</p> </td>
   <td>Alla uppdateringar</td>
  </tr>
  <tr>
   <td>Microsoft Firefox ESR</td>
   <td>E: Arbetet förväntas</td>
   <td> Alla uppdateringar</td>
  </tr>
  <tr>
   <td><p>Google Chrome (Evergreen)</p> </td>
   <td><p>S: Stöds</p> </td>
   <td>Alla uppdateringar</td>
  </tr>
  <tr>
   <td>Google Chrome och Firefox på MAC OS X</td>
   <td>S: Stöds<br /><br /> </td>
   <td>Alla uppdateringar</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x</td>
   <td>S: Stöds</td>
   <td>Alla uppdateringar</td>
  </tr>
  <tr>
   <td>Apple Safari 12.x<br /><br /> </td>
   <td>S: Stöds</td>
   <td>Alla uppdateringar</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Vissa webbläsarrelaterade undantag för stationära datorer är följande:
>
>* De flesta moderna webbläsare stöder inte längre NPAPI-baserade plugin-program. Information om hur det påverkar AEM Forms-program och arbetsflöden finns i [Avbryta plugin-program för NPAPI-webbläsare och dess effekt](https://helpx.adobe.com/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html).
>* Safari stöds bara på Macintosh OS X.
>* Arbetsytan stöder Safari 5.1 i Macintosh OS X 10.6 och 10.7 med Acrobat DC eller senare. Mer information om Safari 5.1-kompatibilitet med Adobe Reader, Acrobat, finns på [https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html](https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html).
>* Administration Console stöds inte i Safari.
>* Correspondence Management stöder inte Windows® Internet Explorer 9.0 för AEM 6.1-formulär.
>* Formulärportalen har stöd för skärmläsarprogram JAWS 14.0 i Internet Explorer 11.
>



#### Mobila kunder {#mobile-clients}

<table>
 <tbody>
  <tr>
   <th><p><strong>Webbläsare (bas)</strong></p> </th>
   <th><p><strong>Patch-definitioner som stöds</strong></p> </th>
  </tr>
  <tr>
   <td><p>Chrome på Android™ 4.1.2 och senare</p> </td>
   <td><p>Alla uppdateringar</p> </td>
  </tr>
  <tr>
   <td>Safari på iOS 11.0 och senare</td>
   <td>Alla uppdateringar</td>
  </tr>
  <tr>
   <td>Microsoft Edge<br /> </td>
   <td>Alla uppdateringar<br /> </td>
  </tr>
  <tr>
   <td>Android-webbläsare på Android™ 4.4 och senare</td>
   <td>Alla uppdateringar</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Forms Portal stöds endast på Safari på iPad.
>



### Appen AEM Forms {#aem-forms-workspace-app}

#### Stöd för mobila enheter {#mobile-device-support}

Appen AEM Forms är tillgänglig på följande plattformar:

| **Plattform** | **Enheter som stöds** |
|---|---|
| Apple iOS | Apple iPhone, iPad, iPad Air och iPad mini med iOS 11 och senare. |
| Google Android | Android 5.1 och senare. Appen AEM Forms är certifierad på 7- och 10-tums Samsung Galaxy-surfplattor och populära smarttelefoner. |
| Microsoft Windows | Microsoft Surface-enheter, surfplattor, bärbara och stationära datorer med operativsystemet Microsoft Windows 10. |

### Adobe Flash Player {#adobe-flash-player}

<table>
 <tbody>
  <tr>
   <th><p><strong>Flash Player (bas)</strong></p> </th>
   <th><p><strong>Patch-definitioner som stöds</strong></p> </th>
  </tr>
  <tr>
   <td><p>Flash Player, senaste versionen</p> </td>
   <td><p>Mindre versioner och uppdateringar</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Adobe kommer att [sluta uppdatera och distribuera Flash Player i slutet av 2020](https://theblog.adobe.com/adobe-flash-update/).

### Adobe Document Security Extension for Microsoft Office {#adobe-rights-management-extension-for-microsoft-office}

Klicka [här](https://www.adobe.com/products/livecycle/rightsmanagement/extension/downloads.html) för att se systemkraven för Adobe Document Security Extension för Microsoft® Office.

### Undantag från klientsupport {#exceptions-to-client-support}

AEM Forms på JEE stöder uppdateringar, patchar och korrigeringspaket utöver den angivna större och mindre versionen av den programvara som stöds. Uppdatering till nästa större eller mindre version stöds dock inte om det inte anges.

## Supportpolicy för korrigeringsstöd från tredje part {#third-party-patch-support-policy}

Tredjepartskraven för AEM Forms on JEE beskrivs i avsnittet &quot;Systemkrav&quot; i respektive produktdokument. All dokumentation finns på [https://adobe.com/go/learn_aemforms_documentation_65](https://adobe.com/go/learn_aemforms_documentation_65) .

AEM Forms på JEE:s referensplattformar från tredje part anger den specifika korrigeringsnivån för den tredjepartsinfrastruktur som var aktuell under utvecklingen och releasen av AEM Forms på JEE, och den minsta korrigerings-/servicepaketnivån för den infrastruktur som stöds av den versionen av AEM Forms på JEE.

Adobe stöder brådskande eller rekommenderade korrigeringsfiler som utfärdas av tredjepartsleverantörer när de släpps, förutsatt att tredjepartsleverantörer garanterar bakåtkompatibilitet med de versioner som AEM Forms på JEE stöder. Adobe stöder endast korrigeringsfiler som släpps efter den miniminivå som anges i AEM Forms i JEE-dokumentationen.

I vissa fall stöder inte Adobe uppdateringar från tredje part som ändrar de viktigaste funktionerna och därför inte fullständig bakåtkompatibilitet. Mer information om vilka uppdateringar som stöds finns i [Korrigeringsdefinitioner](https://helpx.adobe.com/aem-forms/aem-forms-third-party-software-patch.html) som stöds för specifika leverantörsprodukter och de korrigeringstyper som Adobe stöder.

Under omständigheter som Adobe inte kan kontrollera kan korrigeringsfiler från tredje part som gör anspråk på bakåtkompatibilitet ha negativ inverkan på Adobes produkter eller kundmiljöer. I sådana fall rekommenderar Adobe att man utvärderar effekten av brådskande korrigeringar från tredje part innan man lägger in dem i kritiska system. Adobe kommer att arbeta tillsammans med tredje part och göra rimliga ansträngningar för att lösa sådana problem, antingen genom Adobes vanliga supportprogram eller genom att tredje part åtgärdar problemet i lagningen. Detta garanterar inte att en nyligen släppt korrigeringsfil från tredje part som kommer att stödjas av Adobe kommer att fungera enligt dokumentation från leverantören eller med AEM Forms på JEE.

Adobe förbehåller sig rätten att ändra de referensplattformar från tredje part som stöds av en AEM Forms on JEE-release och de korrigeringsdefinitioner som stöds vid varje given tidpunkt.

Ytterligare information om patchar från tredje part finns också på Adobe Enterprise Support-webbplatsen för kunskapsdatabasartiklar om din produkt.

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
