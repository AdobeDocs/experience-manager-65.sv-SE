---
title: Plattformar som stöds för AEM Forms på JEE
description: Lista över infrastrukturkomponenter som krävs och stöds för installation av AEM Forms i JEE
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
exl-id: 74d22cf4-56b2-48f5-92d9-928eaa134866
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE,Platform Matrix
source-git-commit: 71a6a9739800c2e2bd9f8b97e3ec2b0245d6e1cd
workflow-type: tm+mt
source-wordcount: '3819'
ht-degree: 0%

---



# Plattformar som stöds för AEM Forms på JEE {#supported-platforms-for-aem-forms-on-jee}


## Plattformar som stöds {#supported-platforms}


<div class="preview">


Adobe har släppt ett [fullständigt installationsprogram](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=sv-SE) med AEM 6.5.23.0 Forms Service Pack 23 (6.5.23.0) på JEE tillsammans med patch-installationsprogrammen. Det fullständiga installationsprogrammet har stöd för nya plattformar medan korrigeringsprogrammets installationsprogram endast innehåller felkorrigeringar.

Om du utför en ny installation eller planerar att använda den senaste programvaran för din AEM 6.5.23.0 Forms i JEE-miljö rekommenderar Adobe att du använder [ AEM 6.5.23.0 Forms i JEE med det fullständiga installationsprogrammet ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=sv-SE) som släpptes den 6 juni 2025 i stället för AEM 6.5.18 Forms som släpptes den 31 augusti 2023 eller AEM 6.5.12 Forms installationsprogrammet som släpptes 8 april 2019.


</div>


### Supportnivåer {#support-levels}


AEM Forms på JEE-server kan konfigureras med valfri kombination av operativsystem, programservrar, databaser, databasdrivrutiner, JDK, LDAP-servrar och e-postservrar som stöds.


I det här dokumentet visas vilka klient- och serverplattformar som stöds för AEM Forms på JEE. Adobe har flera supportnivåer, både för Adobe rekommenderade konfigurationer och för andra konfigurationer. I dokumentet listas även andra program som stöds och deras version, undantag, korrigeringsdefinitioner och supportregler för programfixar från tredje part.


>[!NOTE]
>
>- En fullständig lista över undantag för serverplattformar som stöds finns i [Undantag för serverplattformar som stöds](#exceptions-to-supported-server-platforms).
>- AEM Forms på JEE har endast stöd för engelska, franska, tyska och japanska versioner av de operativsystem och program som stöds.

### Policy för uppgradering och support

#### Full Installer

- **Uppgraderingsstöd för fullständiga installationsprogram**: Ett fullständigt installationsprogram släpps med varje sjätte version av AEM Service Pack. Ett fullständigt installationsprogram släpptes med 6.5.12.0- och 6.5.18.0 SP-versioner. AEM Forms tillåter endast direktuppgraderingar från de två sista fullständiga installationsprogrammen. AEM Forms underlättar till exempel endast direkta uppgraderingar till version 6.5.23.0 från de två sista fullständiga installationsprogrammen, nämligen 6.5.18.0 och 6.5.12.0. Om du behöver uppgradera från en tidigare uppgradering kan du använda en multi-hop-uppgradering för att först gå till en fullständig version som stöds och sedan till den senaste versionen.

- **Borttagning**: Plattformsstödet uppdateras med varje fullständig installationsversion. Alla program som markerats som inaktuella i plattformsmatrisen kan tas bort från de plattformar som stöds i efterföljande versioner eller när programvaran har upphört med stödet.

#### Service Pack


- **Service Pack-täckning**: Adobe ger teknisk support för AEM Forms-miljöer med hjälp av något av de senaste sex servicepaketen. Om din nuvarande version är äldre än de senaste sex servicepaketen rekommenderar Adobe starkt att du uppgraderar till den senaste versionen för optimala prestanda, säkerhet och kontinuerlig support.

- **Riktlinjer för uppdatering av korrigeringsfiler**: När du uppdaterar med hjälp av patch-installationsprogram är det viktigt att kontrollera att den underliggande fullständiga installationsversionen inte är mer än två versioner gammal. Kontrollera till exempel att den underliggande fullständiga installationsversionen är 6.5.23.0 eller 6.5.18.0 under installationen av Service Pack 6.5.12.0.

<!--
- **Patch Upgrade Support**: You can upgrade from an older service pack to a newer one (for example, from 6.5.18.0 to 6.5.23.0) using the patch installer, as long as the destination platform (OS, JDK, application server, etc.) is supported by the newer service pack.-->

### Rekommenderade konfigurationer {#recommendedconfigurations}


Adobe rekommenderar dessa konfigurationer och ger fullständig eller begränsad support som en del av standardavtalet för programunderhåll:


<table>
<tbody>
 <tr>
  <th>Supportnivå</th>
  <th>Beskrivning</th>
 </tr>
 <tr>
  <td>A: Stöds<br /> </td>
  <td>Adobe ger fullständig support och underhåll för den här konfigurationen. Den här konfigurationen omfattas av Adobe kvalitetssäkringsprocess.</td>
 </tr>
 <tr>
  <td>R: Begränsat stöd</td>
  <td>Adobe ger fullständigt stöd för den här konfigurationen när vissa förutsättningar är uppfyllda. Kontakta Adobe support för företag om du vill veta mer om förutsättningarna och begära support.</td>
 </tr>
 <tr>
  <td>L: Begränsat stöd</td>
  <td>Adobe ger fullständigt stöd och underhåll för den här konfigurationen när vissa förutsättningar är uppfyllda. Alla funktioner är inte tillgängliga i konfigurationen. Kontakta Adobe Enterprise Support om du vill veta mer om förutsättningarna och begära support.<br /> </td>
 </tr>
</tbody>
</table>


### Konfigurationer som inte stöds {#unsupported-configurations}


| Supportnivå | Beskrivning |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| E: Arbetet förväntas | Konfigurationen förväntas fungera och det finns inga rapporter om motsatsen. |
| Z: Stöds inte | Konfigurationen stöds inte. Adobe har inga programsatser om huruvida konfigurationen fungerar eller inte. |


>[!NOTE]
>
>För att hjälpa AEM Forms-kunder att minska ägandekostnaden, förenkla driftsättningsarkitekturen och modernisera utvecklingsstacken går Adobe Experience Manager Enterprise-plattform bort från applikationsserverbaserad driftsättning till förmån för fristående OSGi-baserade driftsättningar. Adobe fortsätter att stödja AEM Forms JEE-stacken med en reducerad matris med infrastrukturkomponenter.
>&#x200B;><br>
>&#x200B;>I och med version 6.5 stöds inte längre infrastrukturkomponenter som har den lägsta användningen bland Adobe-kunder, enligt följande:
>
> - IBM® DB2®-databas
> - IBM® AIX® och Sun Solaris™
>
>
>För nya installationer rekommenderar vi att man där det är möjligt driftsätter AEM Forms i den moderna OSGi-stacken för att använda de senaste innovationerna kring responsiv Adaptiv Forms för mobiler, interaktiv kommunikation i flera kanaler och dataintegrering i serverdelen med hjälp av Form Data Model.
>
>Adobe känner igen att befintliga användare måste fortsätta att distribuera AEM Forms på JEE-stacken. I sådana fall kräver Adobe att AEM Forms JEE distribueras på den infrastruktur som stöds enligt beskrivningen i den här dokumentationen. Om du uppgraderar till AEM 6.5 Forms och använder en plattform som inte stöds i den tidigare AEM Forms-versionen kan du kontakta Adobe support för hjälp med att uppgradera till en plattform som stöds.

### Java™ Virtual Machines (JVM) {#java-virtual-machines-jvm}


Adobe Experience Manager Forms kräver att en Java™ Virtual Machine körs, vilket ingår i Java™ Development Kit-distributionen (JDK). Adobe Experience Manager fungerar med följande versioner av Java™ Virtual Machines:


<table>
<tbody>
 <tr>
  <th><p><strong>Plattform</strong></p> </th>
  <th><p><strong>Supportnivå</strong></p> </th>
  <th><p><strong>Patch-definitioner som stöds</strong></p> </th>
 </tr>
 <tr>
  <td><p>Oracle Java™ SE 11 (64 bitar) <sup> [8] </sup> </p>  </td>
  <td><p>A: Stöds</p> </td>
  <td><p>Mindre releaser och uppdateringar </p> </td>
 </tr>
 <tr>
  <td>Azul Zulu OpenJDK 11-64 bitar</td>
  <td>Z: Stöds inte</td>
  <td><p> </p> </td>
 </tr>
 <tr>
  <td>Azul Zulu OpenJDK 8 - 64 bitar</td>
  <td>Z: Stöds inte</td>
  <td><p> </p> </td>
 </tr>
 <tr>
  <td>Oracle Java™ SE 8 (64 bitar)</td>
  <td>A: Stöds</td>
  <td>Mindre releaser och uppdateringar</td>
 </tr>
 <tr>
  <td>IBM® J9 Virtual Machine (bygge 2.9, JRE 1.8.0) IBM® JDK SR6-FP26<br /> </td>
  <td>A: Stöds</td>
  <td>Mindre releaser och uppdateringar</td>
 </tr>
 <tr>
  <td>IBM® JAVA1.8.0_291(build 8.0.6.30)<br /> </td>
  <td>A: Stöds</td>
  <td>Mindre releaser och uppdateringar</td>
 </tr>
</tbody>
</table>


>[!NOTE]
>
>- Spåra säkerhetsbulletiner från Java™-leverantören för att säkerställa säkerheten i produktionsmiljöer och installera de senaste Java™-uppdateringarna.
>- AEM Forms på JEE har endast stöd för 64-bitars JVM i produktionsmiljöer.

### Databaser och CRX Persistence {#databases-and-crx-persistence}


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
  <td><p> MongoDB Enterprise 6.0 (utgått) </p> </td>
  <td><p>Databasmikrokernel</p> </td>
  <td><p>Stöds</p> </td>
 </tr>
 <tr>
  <td><p> MongoDB Enterprise 7.0 </p> </td>
  <td><p>Databasmikrokernel</p> </td>
  <td><p>Stöds</p> </td>
 </tr>
  <tr>
  <td>Oracle Database 19c (Standard, Real Application Clusters (RAC) och Enterprise Edition) </td>
  <td>Repository Microkernal </td>
  <td>Stöds</td>
 </tr>
 <tr>
  <td><p>Databasmikrokernel</p> </td>
  <td><p>Stöds</p> </td>
  <td></td>
 </tr>
 <tr>
  <td><p>Microsoft® SQL Server 2019 (borttagen) </p> </td>
  <td><p>Databasmikrokernel</p> </td>
  <td><p>Stöds</p> </td>
 </tr>
 <tr>
  <td><p>Microsoft® SQL Server 2022 </p> </td>
  <td><p>Databasmikrokernel</p> </td>
  <td><p>Stöds</p> </td>
 </tr>
 <tr>
  <td>IBM® DB2® 11.1 (borttagen)</td>
  <td>Databasmikrokernel</td>
  <td>R: Begränsat stöd</td>
 </tr>
 <tr>
 <tr>
  <td>MySQL 8.0.27 (borttagen) </td>
  <td>-</td>
  <td>R: Begränsat stöd</td>
 </tr>
 <tr>
 <tr>
  <td>MySQL 8.4</td>
  <td>-</td>
  <td>R: Begränsat stöd</td>
 </tr>
</tbody>
</table>


- IBM® DB2® stöds inte för nya installationer. Det stöds endast för befintliga kunder som uppgraderar till AEM 6.5 Forms.
- MongoDB är en tredjepartsprogramvara som inte ingår i AEM licenspaket. Mer information finns i [MongoDB-licenspolicy](https://www.mongodb.org/about/licensing/).
- För att få ut så mycket som möjligt av er AEM rekommenderar Adobe att man licensierar MongoDB Enterprise-versionen för att få tillgång till professionell support.
@@ -242,187 +206,150 @ Adobe Experience Manager Forms kräver en Java™ Virtual Machine som kan köras
- Dokumentsäkerhetsmodulen använder inte innehållsdatabas. Det innebär att om du bara använder dokumentsäkerhet och inte tänker använda HTML Workspace-, HTML5-formulär eller adaptiva formulär ska du inte installera Content Repository.
- AEM Forms på JEE stöder inte användning av MySQL för beständig AEM-databas (CRX-Repository).


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
  <td><p>MySQL Connector/J 5.7 (utgått)</p> </td>
  <td><p>Tillhandahålls med AEM Forms i JEE-installation</p> </td>
 </tr>
 <tr>
  <td>MySQL</td>
  <td><p>MySQL Connector/J 8.4</p> </td>
  <td><p>Tillhandahålls med AEM Forms i JEE-installation</p> </td>
 </tr>
 <tr>
  <td>Microsoft® SQL Server<br /> </td>
  <td><p>Microsoft® SQL Server JDBC-drivrutin 8.2.2 <br /> </p> <p>sqljdbc8.jar (utgått) </p> </td>
  <td><p>Ladda ned från Microsoft® webbplats.</p> </td>
 </tr>
 <tr>
  <td>Microsoft® SQL Server<br /> </td>
  <td><p>Microsoft® SQL Server JDBC-drivrutin 12.10.0 <br /> </p> <p>sqljdbc12.10.0.jar</p> </td>
  <td><p>Ladda ned från Microsoft® webbplats.</p> </td>
 </tr>
 <tr>
  <td>Oracle</td>
  <td><p>Oracle Database 19.3.0.0.0 JDBC driver</p> <p>jodbc8.jar (version 19.3.0.0.0)<br /> </p> </td>
  <td><p>Hämta från <a href="https://www.oracle.com/database/technologies/appdev/jdbc-ucp-19c-downloads.html">Oracle webbplats</a>.</p> </td>
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
  <td>Oracle WebLogic Server 12.2.1 (12c R2) (borttagen) <sup>[9]</sup></td>
  <td>A: Stöds</td>
  <td>Service Pack och viktiga uppdateringar</td>
 </tr>
 <tr>
  <td>Oracle WebLogic Server 14c <sup>[9]</sup></td>
  <td>A: Stöds</td>
  <td>Service Pack och viktiga uppdateringar</td>
 </tr>
 <tr>
  <td>IBM® WebSphere® Application Server 9.0.0.10 <sup>[1] [4]</sup><br /> </td>
  <td>A: Stöds</td>
  <td>Service Pack och viktiga uppdateringar</td>
 </tr>
 <tr>
  <td><p>JBoss® Enterprise Application Platform (EAP) 7.4 <sup>[2] [3] [7]</sup> </p> </td>
  <td><p>A: Stöds</p> </td>
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
  <td>Microsoft® Windows Server 2019 (64-bitars) (borttagen)</td>
  <td>A: Stöds</td>
  <td>Servicepaket och viktiga uppdateringar</td>
 </tr>
    <tr>
  <td>Microsoft® Windows Server 2022 (64-bitars)</td>
  <td>A: Stöds</td>
  <td>Servicepaket och viktiga uppdateringar</td>
 </tr>
 <tr>
  <td>Ubuntu 20.04</td>
  <td>A: Stöds</td>
  <td>Servicepaket och viktiga uppdateringar</td>
 </tr>
 <tr>
  <td><p>Red Hat® Enterprise Linux® 8 (Kernel 4.x) (64 bitar) (borttaget)</p> </td>
  <td><p>A: Stöds</p> </td>
  <td><p>Mindre releaser, kumulativa uppdateringar och viktiga uppdateringar</p> </td>
 </tr>
 <tr>
  <td><p>Red Hat® Enterprise Linux® 7 (Kernel 3.x) (64-bitars) (borttaget)</td>
  <td><p>A: Stöds</p> </td>
  <td><p>Mindre releaser, kumulativa uppdateringar och viktiga uppdateringar</p> </td>
 </tr>
 <tr>
  <td><p>Red Hat® Enterprise Linux® 9 (Kernel 4.x) (64-bitars)</p> </td>
  <td><p>A: Stöds</p> </td>
  <td><p>Mindre releaser, kumulativa uppdateringar och viktiga uppdateringar</p> </td>
 </tr>
 <tr>
  <td><p>SUSE® Linux® Enterprise Server 15 SP6 (64-bitars) </p> </td>
  <td><p>A: Stöds</p> </td>
  <td><p>Service Pack, kumulativa patchar och viktiga säkerhetsuppdateringar</p> </td>
 </tr>
 <tr>
  <td>Oracle Linux® 7 Update 3 (64-bitars)</td>
  <td>A: Stöds</td>
  <td>Service Pack, kumulativa patchar och viktiga säkerhetsuppdateringar</td>
 </tr>
</tbody>
</table>


>[!NOTE]
>
> För Linux®-baserad server krävs följande körningsberoenden:
>
> - glibc.x86_64 (2.17-196)
> - libX11.x86_64 (1.6.7-4)
> - zlib.x86-64 (1.2.7-17)
> - libxcb.x86_64 (1.13-1.el7)
> - libXau.x86_64 (1.0.8-2.1.el7)
> - glibc-locale.x86_64 ( 2.17 eller senare)
> - OpenSSL 3 (krävs på standardplats i OS).

För installation av OpenSSL 3: Biblioteken libcrypto.so.3 och libssl.so.3 måste vara tillgängliga i standardbibliotekssökvägen som representeras av miljövariabeln LD_LIBRARY_PATH. Om de är installerade på en plats som inte är standard måste du se till att den här sökvägen läggs till i LD_LIBRARY_PATH innan du startar servern.

#### Virtualiserad miljö {#virtualized-environment}


Du kan köra AEM Forms på JEE på en fysisk dator eller en virtuell miljö. Om du råkar ut för något problem med AEM Forms i en virtuell miljö kan du försöka replikera problemet på en fysisk dator. Om problemet kvarstår på den fysiska datorn kontaktar du Adobe support för att få en lösning. Kontakta din leverantör av virtuell miljö om du inte kan replikera på en fysisk dator.


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
1. AEM Forms på JEE stöder inte JBoss® på SUSE® Linux® Enterprise Server 12. Endast IBM® WebSphere® stöds i SUSE® Linux® Enterprise Server 12.
1. AEM Forms på JEE stöder inte JDK med JBoss® annat än Oracle Java™ SE.
1. AEM Forms på JEE stöder inte JDK med andra IBM® WebSphere® än IBM® JDK.
1. CRX-databasen stöder beständighet av typen tarMK, MongoDB och relationsdatabaser (RDBMK). Du kan inte ha två olika databassystem mellan programservern och CRX-databasen. I en AEM Forms-miljö för JEE kan du emellertid använda MongoMK med CRX-databas och en relationsdatabas som stöds med programserver.
@@ -432,12 +359,12 @@ Tänk på följande undantag när du väljer en plattform för att konfigurera AEM F
1. JDK-versioner som är högre än 1.8.0_281 stöds inte för WebLogic-servern. (FORMS-8498)
1. JDK 11.0.20 stöds inte för installation av AEM Forms i JEE Installer. Endast JDK 11.0.19 och tidigare versioner stöds för installation av AEM Forms i JEE Installer.

1. [!DNL Microsoft® Windows Server 2019] stöder inte [!DNL MySQL 5.7] och [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] stöder inte körklara installationer för [!DNL Experience Manager Forms Service Pack 6.5.10.0 and later]. (CQDOC-18312)


Tänk dessutom på följande när du väljer program för Adobe AEM Forms i JEE-distributioner:


- AEM Forms på JEE har stöd för uppdateringar, patchar och korrigeringspaket utöver den angivna större och mindre versionen av den programvara som stöds. Uppdatering till nästa större eller mindre version stöds dock inte om det inte anges.
- Klusterbaserade installationer stöder inte TjärMK-beständighet. Mer information om stöd för beständighet finns i [Välja en beständig typ för en AEM Forms-installation](/help/forms/using/choosing-persistence-type-for-aem-forms.md).
- AEM Forms på JEE stöder olika tredjepartsprogram enligt Adobe [Supportpolicy för tredjepartsprogram](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p).
@@ -449,274 +376,219 @@ Tänk dessutom på följande när du väljer program för Adobe AEM

### LDAP-servrar (tillval) {#ldap-servers-optional}


<table>
<tbody>
 <tr>
  <th><p><strong>Produkt (grundversion)</strong></p> </th>
  <th><p><strong>Patch-definitioner som stöds</strong></p> </th>
 </tr>
 <tr>
  <td>Microsoft® Active Directory 2016 (borttagen)</td>
  <td>Underhållsrelease och programfix</td>
 </tr>
 <tr>
  <td>Microsoft® Active Directory 2022</td>
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
| ----------------------- |
| Microsoft® Exchange 2013 |
| Microsoft® Office 365 |


### Innehållshanterare och motsvarande kopplingar {#content-managers-and-corresponding-connectors}


<table>
<tbody>
 <tr>
  <td><strong>Produkt<br /> </strong></td>
  <td><strong>Version</strong></td>
 </tr>
 <tr>
  <td>EMC Documentum®</td>
  <td>7,3</td>
 </tr>
 <tr>
  <td>IBM® FileNet</td>
  <td>5.5.2</td>
 </tr>
 <tr>
  <td>IBM® Content Manager Server (borttagen) </td>
  <td>8.5 Fixpaket 2</td>
 </tr>
  <tr>
  <td> IBM® Content Manager Client (borttagen)</td>
  <td>8,5 </td>
 </tr>
  <td>Microsoft® Sharepoint </td>
  <td>2019<br /> </td>
 </tr>
</tbody>
</table>


### Stöd för Cordova {#support-for-cordova}


AEM Forms App har nu stöd för Apache Cordova. Följande plattformsspecifika versioner av Cordova stöds:


- Apache Cordova 6.4.0
- Cordova iOS 4.3.0
- Cordova Android™ 6.0.0
- Cordova Windows 4.4.3

### Överväganden för PDF Generator

<table>
<tbody>
 <tr>
  <th><p><strong>Produkt</strong></p> </th>
  <th><p><strong>Format som stöds för konvertering till PDF</strong></p> </th>
 </tr>
 <tr>
   <td><a href="https://helpx.adobe.com/se/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat Pro DC</a> senaste versionen</td>
   <td>XPS, bildformat (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML och HTML</td>
  </tr>
 <tr>
  <td>Microsoft® Office 2021  </td>
  <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF och TXT</td>
 </tr>
 </tr>

<tr>
  <td>WordPerfect 2020<br /> </td>
  <td>WP, WPD</td>
 </tr>
 <tr>
  <td>Microsoft® Publisher 2019<br /> </td>
  <td>PUB</td>
 </tr>
 <tr>
  <td>Microsoft® Publisher 2021<br /> </td>
  <td>PUB</td>
 </tr>
 <tr>
  <td>OpenOffice 4.1.10</td>
  <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, bildformat (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, JPC, HTML, HTM, RTF och TXT</td>
 </tr>
</tbody>
</table>


>[!NOTE]
>
>PDF Generator har endast stöd för engelska, franska, tyska och japanska versioner av de operativsystem och program som stöds.
>
>Dessutom:
>
>- PDF Generator kräver Adobe Acrobat Pro DC (32-bitars) för att kunna utföra konverteringen.
>- PDF Generator stöder endast 32-bitarsversionen av Microsoft® Office Professional Plus och andra program som krävs för konvertering.
>- Installationen av Microsoft® Office Professional Plus kan använda volymlicenser baserade på Retail eller MAK/KMS/AD.
>- Om en Microsoft® Office-installation inaktiveras eller inte licensieras av någon anledning, t.ex. en volymlicensierad installation som inte kan hitta en KMS-värd inom en angiven period, kan konverteringen misslyckas tills installationen har licensierats på nytt och återaktiverats.
>- PDF Generator stöder inte Microsoft® Office 365.
>- PDF Generator stöder 32-bitarsversionen av OpenOffice i Linux®.
>- PDF Generator-konverteringar för OpenOffice stöds endast i Windows och Linux®.
>- Funktionerna OCR PDF, Optimize PDF och Export PDF stöds endast i Windows.
>- En version av Acrobat medföljer AEM Forms för att aktivera PDF Generator-funktioner. Programmeringsversionen får endast användas med AEM Forms under AEM Forms-licensens löptid för användning med AEM Forms PDF Generator. Mer information finns i AEM Forms produktbeskrivning för din distribution ([On-Premise](https://helpx.adobe.com/se/legal/product-descriptions/adobe-experience-manager-on-premise.html) eller [Managed Services](https://helpx.adobe.com/se/legal/product-descriptions/adobe-experience-manager-managed-services.html))
>- PDF Generator-tjänsten stöder inte Microsoft® Windows 10.
>- PDF Generator kan inte konvertera filer med Microsoft® Visio 2019.
>- PDF Generator kan inte konvertera filer med Microsoft® Project 2019.

PDF Generator stöder endast 32-bitarsversionen av Microsoft® Office Professional Plus och andra program som krävs för konvertering.


Installationen av Microsoft® Office Professional Plus kan använda volymlicenser baserade på Retail eller MAK/KMS/AD.


Om en Microsoft® Office-installation inaktiveras eller inte licensieras av någon anledning, t.ex. en volymlicensierad installation som inte kan hitta en KMS-värd inom en angiven period, kan konverteringen misslyckas tills installationen har licensierats på nytt och återaktiverats.

<!-- Removed lines: >- PDF Generator fails to convert files using Microsoft&reg; Visio 2019. You can continue to use Microsoft&reg; Visio 2016 to convert .VSD and .VSDX files.
>- PDF Generator fails to convert files using Microsoft&reg; Project 2019. You can continue to use Microsoft&reg; Project 2016 to convert .MPP files.-->


### Undantag från tillgänglighetsstöd {#exceptions-to-accessibility-support}


Följande delsystem i AEM Forms är inte [508](https://www.section508.gov/)-kompatibla:


- Anpassat gränssnitt för Forms-redigering
- Redigeringsgränssnittet för Forms Manager
- Redigeringsgränssnitt för korrespondenshantering
- Administratörsgränssnitt (administrationskonsolens användargränssnitt)


## Systemkrav för AEM Forms i JEE {#system-requirements-for-aem-forms-on-jee}


### Lägsta maskinvarukrav {#minimum-hardware-requirements}


<table>
<tbody>
 <tr>
  <td>Plattform</td>
  <td>Minsta maskinvarukrav</td>
 </tr>
 <tr>
  <td>Microsoft® Windows Server</td>
  <td>Intel Xeon® E5-2680, 2,4 GHz-processor eller motsvarande <br /> VMWare ESX 5.1 eller senare<br /> RAM: 6 GB (64-bitars operativsystem med 64-bitars JVM) <br /> Ledigt diskutrymme: 15 GB temporärt utrymme plus 22 GB <br /> för AEM Forms på JEE</td>
 </tr>
 <tr>
  <td>SUSE® Linux® Enterprise Server</td>
  <td>Intel Xeon® E5-2670v2, 1 vCPU, 2,5 GHz-processor<br /> AWS m3.medium (3 ecu)<br /> RAM: 6 GB (64-bitars operativsystem med 64-bitars JVM) <br /> Ledigt diskutrymme: 6 GB temporärt utrymme plus 22 GB <br /> för AEM Forms på JEE</td>
 </tr>
 <tr>
  <td>Red Hat® Enterprise Linux®</td>
  <td>Intel Xeon® E5-2670v2, 1 vCPU, 2,5 GHz-processor<br /> AWS m3.medium (3 ecu)<br /> RAM: 6 GB (64-bitars operativsystem med 64-bitars JVM) <br /> Ledigt diskutrymme: 6 GB temporärt utrymme plus 22 GB <br /> för AEM Forms på JEE <br /> </td>
 </tr>
 <tr>
  <td>Maskinvarukrav för en liten produktionsmiljö</td>
  <td>
   <ul>
    <li><strong>Intel®-baserad miljö</strong>: Intel Xeon® E5-2680, 2,4 GHz eller högre. Om du använder en processor med dubbla kärnor förbättras prestandan ytterligare</li>
    <li><strong>Minne: </strong> 4 GB <br /> </li>
   </ul> </td>
 </tr>
</tbody>
</table>


Ytterligare krav finns i:

- [Systemkrav för en enda server-AEM Forms för JEE-distribution](https://www.adobe.com/go/learn_aemforms_sysreq_single_65)
- [Systemkrav för en klustrad AEM Forms för JEE-distribution](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_65)


### Adobe Acrobat och Adobe Reader {#adobe-acrobat-and-adobe-reader}


<table>
<tbody>
 <tr>
  <th><p><strong>Acrobat och Adobe Reader (bas)</strong></p> </th>
  <th><p><strong>Patch-definitioner som stöds</strong></p> </th>
 </tr>
 <tr>
  <td>Acrobat 2020 (klassiskt spår)</td>
  <td>Version 20.004.30006 eller senare<br /> </td>
 </tr>
 </tbody>
</table>


>[!NOTE]
>
>Acrobat DC-produktfamiljen innehåller två spår för både Acrobat och Reader som är olika produkter:&quot;Classic&quot; och&quot;Continuous&quot;. Mer information och en jämförelse av de två spåren finns på [https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html).

## Klienter som stöds för AEM Forms i JEE {#supported-clients-for-aem-forms-on-jee}


### Workbench {#workbench}


<table>
<tbody>
 <tr>
  <th><p><strong>Plattform</strong></p> </th>
  <th><p><strong>Patch-definitioner som stöds</strong></p> </th>
 </tr>
 <tr>
  <td><p>Microsoft® Windows® 10 (Enterprise, Pro, Basic)</p> <p>32- eller 64-bitarsversion</p> <p> </p> </td>
  <td>Servicepaket och viktiga uppdateringar</td>
 </tr>
 <tr>
  <td>Microsoft® Windows® 2019 Server (borttagen)</td>
  <td>Servicepaket och viktiga uppdateringar</td>
 </tr>
 <tr>
  <td>Microsoft® Windows® 2022 Server</td>
  <td>Servicepaket och viktiga uppdateringar</td>
 </tr>
</tbody>
</table>


- Diskutrymme för installation: 1,7 GB för Workbench, 2,7 GB på en enda enhet för en fullständig installation av Workbench, Designer och exempelpaketet innehåller 400 MB för temporära installationskataloger - 200 MB i användarens temp-katalog och 200 MB i Windows temporära katalog. Om alla dessa platser finns på en enda enhet måste det finnas 1,5 GB ledigt utrymme under installationen. De filer som kopieras till de tillfälliga katalogerna tas bort när installationen är klar.


- Minne för att köra Workbench: 2 GB RAM
- Maskinvarukrav: Intel® Pentium® 4 eller AMD®-motsvarighet, 1 GHz processor
- Minst 1 024 × 768 pixlar eller högre bildskärmsupplösning med 16-bitars färg eller högre
- TCP/IPv4- eller TCP/IPv6-nätverksanslutning till AEM Forms på JEE-server
- Du måste ha administratörsbehörighet för att installera Workbench i Windows. Om du installerar med ett icke-administratörskonto uppmanas du att ange autentiseringsuppgifter för ett lämpligt konto.


### Designer {#designer}


- Microsoft® Windows® 2016 Server, Microsoft® Windows® 2019 Server, Microsoft® Windows® 10 eller Windows® 11
- 1 GHz eller snabbare processor med stöd för PAE, NX och SSE2.
- 1 GB RAM för 32-bitars eller 2 GB RAM för 64-bitars operativsystem
@@ -729,49 +601,45 @@ Ytterligare krav finns i:
- Administrativ behörighet för att installera Designer
- Microsoft® Visual C++ 2019 (VC 14.28 eller senare) 32-bitars runtime


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
  <td><p>Microsoft® Edge (Evergreen)</p> </td>
  <td><p>A: Stöds</p> </td>
  <td><p>Service Pack och uppdateringar</p> </td>
 </tr>
 <tr>
  <td><p>Mozilla Firefox (Evergreen)</p> </td>
  <td><p>A: Stöds</p> </td>
  <td>Alla uppdateringar</td>
 </tr>
 <tr>
  <td>Mozilla Firefox ESR</td>
  <td>E: Arbetet förväntas</td>
  <td> Alla uppdateringar</td>
 </tr>
 <tr>
  <td><p>Google Chrome (Evergreen)</p> </td>
  <td><p>A: Stöds</p> </td>
  <td>Alla uppdateringar</td>
 </tr>
 <tr>
  <td>Apple Safari på macOS</td>
  <td>A: Stöds</td>
  <td>Alla uppdateringar</td>
 </tr>
</tbody>
</table>


>[!NOTE]
>
>Vissa webbläsarrelaterade undantag för stationära datorer är följande:
>
>- Correspondence Management stöder inte Windows® Internet Explorer 9.0 för AEM 6.1-formulär.
>- Forms Portal stöder JAWS 14.0 skärmläsarprogram i Internet Explorer 11.

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
  <td>Safari på iOS 15.1 och senare</td>
  <td>Alla uppdateringar</td>
 </tr>
 <tr>
  <td>Microsoft® Edge<br /> </td>
  <td>Alla uppdateringar<br /> </td>
 </tr>
 <tr>
  <td>Inbyggd Android™-webbläsare i Android™ 4.4 och senare</td>
  <td>Alla uppdateringar</td>
 </tr>
</tbody>
</table>


>[!NOTE]
>
>- Forms Portal stöds endast i Safari på iPad.

### AEM Forms {#aem-forms-workspace-app}


#### Stöd för mobila enheter {#mobile-device-support}


AEM Forms finns på följande plattformar:


| **Plattform** | **Enheter som stöds** |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- |
| Apple iOS | Apple iPhone, iPad, iPad Air och iPad mini med iOS 15.1 och senare. |
| Google Android™ | Android™ 5.1 och senare. AEM Forms-appen är certifierad på 7-tums och 10-tums Samsung Galaxy-surfplattor och populära smarttelefoner. |
| Microsoft® Windows | Microsoft® Surface-enheter, surfplattor, bärbara datorer och stationära datorer med operativsystemet Microsoft® Windows 10. |


### Adobe Document Security Extension for Microsoft® Office {#adobe-rights-management-extension-for-microsoft-office}


Klicka [här](https://www.adobe.com/products/livecycle/rightsmanagement/extension/downloads.html) för att se systemkraven för Adobe Document Security Extension för Microsoft® Office.


### Undantag från klientsupport {#exceptions-to-client-support}


AEM Forms på JEE har stöd för uppdateringar, patchar och korrigeringspaket utöver den angivna större och mindre versionen av den programvara som stöds. Uppdatering till nästa större eller mindre version stöds dock inte om det inte anges.


## Supportpolicy för korrigeringsstöd från tredje part {#third-party-patch-support-policy}


Tredjepartskraven för AEM Forms på JEE beskrivs i avsnittet Systemkrav i respektive produktdokument. Få tillgång till all dokumentation från [https://adobe.com/go/learn_aemforms_documentation_65](https://adobe.com/go/learn_aemforms_documentation_65) .


AEM Forms på JEE:s referensplattformar från tredje part anger den specifika korrigeringsnivån för tredjepartsinfrastruktur som var aktuell under utvecklingen och lanseringen av AEM Forms på JEE, och den minsta korrigerings-/servicepaketnivån för den infrastruktur som stöds av den versionen av AEM Forms på JEE.


Adobe stöder brådskande eller rekommenderade korrigeringsfiler som utfärdas av tredjepartsleverantörer när de släpps, förutsatt att tredjepartsleverantörer garanterar bakåtkompatibilitet med de versioner som AEM Forms på JEE stöder. Adobe stöder endast korrigeringsfiler som släpps efter den miniminivå som anges i AEM Forms för JEE-dokumentationen.


Ibland saknar Adobe stöd för tredjepartsuppdateringar som ändrar viktiga funktioner och därför inte stöder fullständig bakåtkompatibilitet. Mer information om vilka uppdateringar som stöds finns i [Patchdefinitioner som stöds](https://helpx.adobe.com/aem-forms/aem-forms-third-party-software-patch.html) för specifika leverantörsprodukter och korrigeringstyperna som Adobe stöder.


Under omständigheter som ligger utanför Adobe kontroll kan korrigeringsfiler från tredje part som gör anspråk på bakåtkompatibilitet ha negativ inverkan på Adobe produkter eller kundmiljöer. I sådana fall rekommenderar Adobe att man utvärderar effekten av brådskande korrigeringar från tredje part innan man lägger in dem i viktiga system. Adobe samarbetar med tredje part genom att göra rimliga ansträngningar för att lösa sådana problem, antingen genom vanliga Adobe-supportprogram eller genom att tredje part åtgärdar problemet i lagningen. Detta garanterar inte att en nyligen släppt korrigeringsfil från tredje part som stöds av Adobe fungerar som den dokumenterats av leverantören eller med AEM Forms på JEE.


Adobe förbehåller sig rätten att ändra de referensplattformar från tredje part som stöds av en AEM Forms on JEE-release och de korrigeringsdefinitioner som stöds vid varje given tidpunkt.


Ytterligare information om patchar från tredje part finns också på Adobe Enterprise Support-webbplatsen för kunskapsdatabasartiklar om din produkt.


<!--

## Platform updates {#platform-updates}
The following platforms are marked as deprecated with AEM Forms 6.5.18.0 release on August 31, 2023:
- Microsoft&reg; Windows Server 2019 (64-bit)
- Microsoft&reg; Active Directory 2016
The following platforms are marked as deprecated with AEM Forms 6.5.13.0 release on June 2, 2022:
- Microsoft&reg; SharePoint 2016
The following platforms are marked as deprecated with AEM Forms 6.5.10.0 release on September 7, 2021:
- Adobe Acrobat 2017 - [Core support for Adobe Acrobat 2017 ends on June 6, 2022](https://helpx.adobe.com/se/support/programs/eol-matrix.html).
- Red Hat&reg; Enterprise Linux&reg; 7 (Kernel 3.x) (64-bit)
- Microsoft&reg; Windows Server 2016 (64-bit)
- Microsoft&reg; Office 2016
- OpenOffice 4.1.2
-->




## Revisionshistorik {#revision-history}


<!--
- 6.5.18.0 (Aug 31, 2023)
 - **Added support**: [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platforms:
   - MongoDB Enterprise 4.4
   - Oracle WebLogic Server 14c
   - My SQL JDBC connector 8
   - Active Directory 2022
   - Microsoft&reg; Windows Server 2022 (64-bit)
 - **Removed support**: [!DNL Adobe Experience Manager Forms] on JEE has removed support for the following platforms:
   - Windows Server 2016 (64-bit)
   - MongoDB Enterprise 4.0
   - Oracle Database 12c Release 2 (12.2.0.1.0)
   - MySQL 5.7.35
   - Microsoft&reg; SQL Server 2016
   - JBoss&reg; EAP 7.1.4
   - My SQL JDBC connector 5.1.44
   - Microsoft&reg; SQL Server JDBC driver 6.2.1.0
   - Microsoft&reg; SQL Server JDBC driver 6.2.2.0
   - Microsoft&reg; JDBC Driver 8.x for SQL Server
   The release has also removed support for the following platforms for PDF Generator and in-general:
   - Microsoft&reg; Sharepoint 2016
   - Microsoft&reg; Office 2016
   - Microsoft&reg; Office Visio 2016
   - Microsoft&reg; Publisher 2016
   - Microsoft&reg; Project 2016
   - OpenOffice 4.1.2
   - Acrobat 2017 (Classic track) Version 17.011.30078 or later
 - **Deprecated support**: [!DNL Adobe Experience Manager Forms] on JEE has deprecated the following platforms:
   - Microsoft&reg; Windows Server 2019 (64-bit)
   - Microsoft&reg; Active Directory 2016
  
- 6.5.13.0 (June 2, 2022)
 The following platforms are deprecated with AEM Forms 6.5.13.0 release on:
 - Microsoft&reg; SharePoint 2016
- 6.5.12.0 (March 3, 2022)
   - **Platform Updates**: [!DNL Adobe Experience Manager Forms] on JEE has removed support for the following platforms:
     - IBM&reg; J9 Virtual Machine (build 2.8, JRE 1.8.0)
     - Oracle Database 12c Release 1
     - Oracle Database 18c
     - Oracle Unified Directory (OUD) 11g Release 2
     - IBM&reg; Lotus Domino 9.0
     - IBM&reg; FileNet 5.2
     - Adobe Flash Player
   - **Platform Updates**: [!DNL Adobe Experience Manager Forms] on JEE has deprecated the following platforms:
     - MongoDB Enterprise 4.0
     - MongoDB Enterprise 4.2
     - IBM&reg; DB2&reg; 11.1
     - Oracle Database 12c Release 2
     - MySQL 5.7.35
     - Microsoft&reg; SQL Server JDBC driver 6.2.1.0
     - JBoss&reg; Enterprise Application Platform (EAP) 7.1.4
     - IBM&reg; Content Manager Server 8.5 Fix pack 2
     - IBM&reg; Content Manager Client 8.5
     - Microsoft&reg; SQL Server 2016
- 6.5.10.0 (Sep 01, 2022)
 - **Added support**: [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platform:
    - Oracle Java&trade; SE 11 (64 bit) SDK for application server JBoss&reg; EAP 7.4.
 - **Deprecated support**: [!DNL Adobe Experience Manager Forms] on JEE has deprecated the following platforms:
   - Adobe Acrobat 2017 - [Core support for Adobe Acrobat 2017 ends on June 6, 2022](https://helpx.adobe.com/se/support/programs/eol-matrix.html).
   - Red Hat&reg; Enterprise Linux&reg; 7 (Kernel 3.x) (64-bit)
   - Microsoft&reg; Windows Server 2016 (64-bit)
   - Microsoft&reg; Office 2016
   - OpenOffice 4.1.2
### Release 6.5.23.0 (June 06, 2025)
| Added Support | Removed Support | Deprecated Support |
| -------------- | --------------- | ------------------- |
| MongoDB Enterprise 7.0 |    MongoDB Enterprise 5.0 | MongoDB Enterprise 6.0 |
| MYSQL 8.4 |SUSE&reg; Linux&reg; Enterprise Server 12 (64-bit) | MYSQL 8.0.27 |
| Microsoft&reg; SQL Server 2022 | |Microsoft&reg; SQL Server 2019 |
| Microsoft&reg; SQL Server JDBC driver 12.8 | | Microsoft&reg; SQL Server JDBC driver 8.2 |
| Microsoft&reg; Office 2021 | | Microsoft&reg; Office 2019 |
| Red Hat&reg; Enterprise Linux&reg; 9 (Kernel 4.x) (64-bit) | |Red Hat&reg; Enterprise Linux&reg; 8 (Kernel 4.x) (64-bit)  |
-->

### Utgåva 6.5.23.0 (6 juni 2025)

| Tillagd support | Borttaget stöd | Föråldrat stöd |
| -------------- | --------------- | ------------------- |
| MongoDB Enterprise 7.0 | MongoDB Enterprise 5.0 | MongoDB Enterprise 6.0 |
| MYSQL 8.4 | SUSE® Linux® Enterprise Server 12 (64-bitars) | MYSQL 8.0.27 |
| Microsoft® SQL Server 2022 | Centro 7 | Microsoft® SQL Server 2019 |
| Microsoft® SQL Server JDBC-drivrutin 12.10.0 | | Microsoft® SQL Server JDBC-drivrutin 8.2 |
| Red Hat® Enterprise Linux® 9 (Kernel 4.x) (64-bitars) | | Red Hat® Enterprise Linux® 8 (Kernel 4.x) (64-bitars) |

### Utgåva 6.5.22.0 (29 november 2024)


| Tillagd support | Borttaget stöd | Föråldrat stöd |
| -------------- | --------------- | ------------------- |
| SUSE® Linux® Enterprise Server 15 SP6 (64-bitars) | |  |

### Utgåva 6.5.21.0 (13 juni 2024)

| Tillagd support | Borttaget stöd | Föråldrat stöd |
| -------------- | --------------- | ------------------- |
| Microsoft® Office 2021 |  |  |

### Utgåva 6.5.19.1 (15 dec 2023)


| Tillagd support | Borttaget stöd | Föråldrat stöd |
| -------------- | --------------- | ------------------- |
| MongoDB Enterprise 6.0 | MongoDB Enterprise 4.4 |  |
| MongoDB Enterprise 5.0 |  |  |
|  | |  |


### Version 6.5.18.0 (31 aug 2023)


| Tillagd support | Borttaget stöd | Föråldrat stöd |
| -------------- | --------------- | ------------------- |
| MongoDB Enterprise 4.4 | Windows Server 2016 (64-bitars) | Microsoft® Windows Server 2019 (64-bitars) |
|  | Acrobat 2017 (Classic track) version 17.011.30078 eller senare |  |

### Utgåva 6.5.13.0 (2 juni 2022)


| Tillagd support | Borttaget stöd | Föråldrat stöd |
| -------------- | --------------- | ------------------- |
|  |  | Microsoft® SharePoint 2016 |

### Version 6.5.12.0 (3 mars 2022)


| Tillagd support | Borttaget stöd | Föråldrat stöd |
| -------------- | --------------- | ------------------- |
|  | IBM® J9 Virtual Machine (bygge 2.8, JRE 1.8.0) | MongoDB Enterprise 4.0 |
|  | | Microsoft® SQL Server 2016 |
|  | | Microsoft® Windows Server 2016 |

### Version 6.5.10.0 (1 september 2022)


| Tillagd support | Borttaget stöd | Föråldrat stöd |
| -------------- | --------------- | ------------------- |
| Oracle Java™ SE 11 (64 bitar) SDK för programservern JBoss® EAP 7.4. | | [Adobe Acrobat 2017 - Core-stöd för Adobe Acrobat 2017 upphör 6 juni 2022.](https://helpx.adobe.com/se/support/programs/eol-matrix.html) |
|  | | OpenOffice 4.1.2 |

>[!NOTE]
>
> En föråldrad plattform får support fram till nästa fullständiga installationsrelease eller tills tredjepartssupport för plattformen når sitt upphörande, beroende på vilket som inträffar först.

<!--
- Oct 10, 2021
 - Changed supported version of iOS for AEM Forms App to iOS 15.1. The previous version was iOS 12.
- Sep 07, 2021
 - **Platform Updates**: [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platforms:
   - [!DNL Adobe Acrobat 2020]
   - [!DNL Ubuntu 20.04]
   - [!DNL Open Office 4.1.10]
   - [!DNL Microsoft&reg;&reg; Office 2016]
   - [!DNL Microsoft&reg;&reg; Windows Server 2016]
   - [!DNL RHEL8]
- Dec 03, 2020
 - Support added with AEM Forms 6.5.7.0 or later for the following platform:
   - [!DNL Microsoft&reg;&reg; SQL Server 2019]
- Sep 09, 2020
   - Changed supported version of iOS for AEM Forms App to iOS 12. The previous version was iOS 11.
   -->