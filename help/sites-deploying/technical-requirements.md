---
title: Tekniska krav
seo-title: Technical Requirements
description: En lista över de klient- och serverplattformar som stöds för AEM.
seo-description: A list of the supported client and server platforms for AEM.
content-type: reference
topic-tags: platform
exl-id: 47529b9a-c4e5-434f-ac26-b01714ff863b
source-git-commit: 80298613370c7187288b33e5a665a074ccb5cd3e
workflow-type: tm+mt
source-wordcount: '3292'
ht-degree: 0%

---

# Tekniska krav{#technical-requirements}

Adobe stöder Adobe Experience Manager (AEM) på plattformarna enligt följande information i det här dokumentet.

Kontakta plattformsleverantören om du har frågor som är specifikt relaterade till plattformen.

>[!NOTE]
>
>Beroende på vilken plattform du installerar AEM på kan det finnas olika uppsättningar krav för användarhantering.

## Förutsättningar {#prerequisites}

Lägsta krav för installation av Adobe Experience Manager:

* Installerad Java Platform, Standard Edition JDK eller annat som stöds [Java Virtual Machines](#java-virtual-machines)
* Experience Manager QuickStart-fil (fristående JAR eller WAR för webbapplikationsdistribution)

### Krav för minsta storlek {#minimum-sizing-requirements}

Lägsta krav för att köra Adobe Experience Manager:

* 5 GB ledigt diskutrymme i installationskatalogen
* 2 GB minne

>[!NOTE]
>
>* Användningsexempel för digitala resurser kräver mer basminne. Se [Driftsättning och underhåll](/help/sites-deploying/deploy.md#default-local-install) för mer information.
>* [AEM Forms tilläggspaket](/help/forms/using/installing-configuring-aem-forms-osgi.md) kräver 15 GB temporärt utrymme.
>


Mer information finns i [Riktlinjer för maskinvarans storlek](/help/managing/hardware-sizing-guidelines.md).

### Supportnivåer {#support-levels}

I det här dokumentet visas vilka klient- och serverplattformar som stöds för Adobe Experience Manager. Adobe har flera supportnivåer, både för rekommenderade konfigurationer och andra konfigurationer.

### Konfigurationer som stöds {#supported-configurations}

Adobe rekommenderar dessa konfigurationer och ger full support som en del av standardavtalet för programunderhåll.

<table>
 <tbody>
  <tr>
   <td>Supportnivå</td>
   <td>Beskrivning<br /> </td>
  </tr>
  <tr>
   <td><strong>S: Stöds</strong></td>
   <td>Adobe ger fullständigt stöd och underhåll för den här konfigurationen. Den här konfigurationen omfattas av Adobe kvalitetssäkringsprocess.</td>
  </tr>
  <tr>
   <td><strong>R: Begränsat stöd</strong></td>
   <td>För att våra kunder ska lyckas erbjuder Adobe full support inom ett begränsat supportprogram, vilket kräver att specifika villkor uppfylls. Support på R-nivå kräver en formell kundförfrågan och en bekräftelse från Adobe. Mer information får du av Adobe kundtjänst.</td>
  </tr>
 </tbody>
</table>

### Konfigurationer som inte stöds {#unsupported-configurations}

| Supportnivå | Beskrivning |
|---|---|
| **Z: Stöds inte** | Konfigurationen stöds inte. Adobe har inga programsatser om huruvida konfigurationen fungerar eller inte. |

## Plattformar som stöds {#supported-platforms}

### Java Virtual Machines {#java-virtual-machines}

Programmet kräver att en Java Virtual Machine körs, vilket tillhandahålls av JDK-distributionen (Java Development Kit).

Adobe Experience Manager arbetar med följande versioner av Java Virtual Machines:

>[!CAUTION]
>
>Vi rekommenderar att du följer säkerhetsbulletinerna från Java-leverantören för att säkerställa säkerheten i produktionsmiljöer och installerar de senaste Java-uppdateringarna.

| **Plattform** | **Supportnivå** | **Länk** |
|---|---|---|
| Oracle Java SE 11 JDK - 64 bitar | S: Stöds `[1]` | [Hämta](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+11*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=24&lt;td>) |
| Oracle Java SE 10 JDK | Z: Stöds inte `[1]` |
| Oracle Java SE 9 JDK | Z: Stöds inte `[1]` |
| Oracle Java SE 8 JDK - 64 bitar | S: Stöds `[1]` | [Hämta](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+8*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=10) |
| IBM J9 VM - build 2.9, JRE 1.8.0 | S: Stöds `[2]` |
| IBM J9 VM - build 2.8, JRE 1.8.0 | S: Stöds `[2]` |
| Azul Zulu OpenJDK 11 - 64 bitar | S: Stöds `[3]` |  |
| Azul Zulu OpenJDK 8 - 64 bitar | S: Stöds `[3]` |  |

1. Oraclet har flyttat till en LTS-modell (Long Term Support) för Oracle Java SE-produkter. Java 9, Java 10 och Java 12 är icke-LTS-versioner som Oracle (se [Oracle Java SE - supportöversikt](https://www.oracle.com/technetwork/java/eol-135779.html)). För att driftsätta AEM i produktionsmiljön tillhandahåller Adobe endast stöd för LTS-versionerna av Java. Stöd för och distribution av Oraclet Java SE JDK, inklusive alla underhållsuppdateringar av LTS-releaser efter slutet av de offentliga uppdateringarna, kommer att stödjas av Adobe direkt för alla AEM som använder Oraclet Java SE. Se [Java - supportpolicy för Adobe Experience Manager](assets/Java_Policy_for_Adobe_Experience_Manager.pdf) för mer information.


1. IBM JRE stöds endast tillsammans med WebSphere Application Server.

1. Azul Zulu OpenJDK LTS-versioner stöds för lokala AEM-distributioner från och med version 6.5 SP9. Support och distribution av Azul Zulu JDK LTS-versionerna måste licensieras direkt från Azul av våra kunder.


### Lagring och beständighet {#storage-persistence}

Det finns olika alternativ för att distribuera Adobe Experience Manager-databasen. Se följande lista för de tekniker och lagringsalternativ som stöds.

| **Plattform** | **Beskrivning** | **Supportnivå** |
|---|---|---|
| **Filsystem med TAR-filer** `[1]` | Databas | S: Stöds |
| **Filsystem med datastore** `[1]` | Binärfiler | S: Stöds |
| Lagra binärfiler i TAR-filer i filsystemet `[1]` | Binärfiler | Z: Stöds inte för produktion |
| Amazon S3 | Binärfiler | S: Stöds |
| Microsoft Azure Blob Storage | Binärfiler | S: Stöds |
| MongoDB Enterprise 4.2 | Databas | S: Stöds `[2, 3, 4]` |
| MongoDB Enterprise 4.0 | Databas | Z: Stöds inte |
| MongoDB Enterprise 3.6 | Databas | Z: Stöds inte |
| MongoDB Enterprise 3.4 | Databas | Z: Stöds inte |
| IBM DB2 10.5 | Databas och databas för Forms | R: Begränsat stöd `[5]` |
| Oracle Database 12c (12.1.x) | Databas och databas för Forms | R: Begränsat stöd |
| Microsoft SQL Server 2016 | Forms-databas | S: Stöds |
| **Apache Lucene (inbyggt i Quickstart)** | Söktjänst | S: Stöds |
| Apache Solr | Söktjänst | S: Stöds |

1. &#39;Filsystem&#39; inkluderar blocklagring som är POSIX-kompatibel. Detta inkluderar nätverkslagringsteknik. Tänk på att filsystemets prestanda kan variera och påverka den övergripande prestandan. Vi rekommenderar att du läser in AEM i kombination med nätverks-/fjärrfilsystemet.
1. MongoDB Enterprise 4.2 kräver minst AEM 6.5 SP9.
1. MongoDB-delning stöds inte i AEM.
1. MongoDB-lagringsmotorn WiredTiger stöds endast.
1. Stöds för AEM Forms uppgraderingskunder. Stöds inte för nya installationer.

>[!NOTE]
>
>Se [Distribuera webbgrupper](/help/communities/deploy-communities.md) om du vill ha mer information om AEM Communities.

>[!NOTE]
>
>MongoDB är en tredjepartsprogramvara och ingår inte i AEM licenspaket. Mer information finns i [MongoDB-licenspolicy](https://www.mongodb.org/about/licensing/) sida.
>
>För att få ut så mycket som möjligt av er AEM med MongoDB rekommenderar Adobe att ni har licenser för MongoDB Enterprise-versionen och får tillgång till professionell support. Se [Rekommenderade distributioner](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk) för mer information.
>
>Licensen innehåller en standarduppsättning av repliker, som består av en primär och två sekundära instanser som kan användas för antingen författaren eller publiceringsdistributionerna.
>
>Om du vill köra både författaren och publicera på MongoDB måste du köpa två separata licenser.
>
>Adobe kundtjänst kommer att hjälpa dig med kvalificeringsproblem i samband med användningen av MongoDB med AEM.
>
>Mer information finns i [MongoDB för Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).

>[!NOTE]
>
>De relationsdatabaser som stöds ovan är tredjepartsprogram och ingår inte i AEM licenspaket.
>
>För att köra AEM 6.5 med en relationsdatabas som stöds krävs ett separat supportavtal med en databasleverantör. Adobe kundtjänst kommer att hjälpa dig med kvalificeringsproblem i samband med användning av relationsdatabaser med AEM 6.5.
>
>**De flesta relationsdatabaser stöds för närvarande i Level-R på AEM 6.5, som innehåller stödkriterier och ett supportprogram enligt beskrivningen ovan.**

### Servletmotorer/programservrar {#servlet-engines-application-servers}

Adobe Experience Manager kan köras antingen som en fristående server (snabbstart-JAR-filen) eller som ett webbprogram på en tredjepartsprogramserver (WAR-filen).

Den lägsta servlet API-version som krävs är Servlet 3.1

| Plattform | Supportnivå |
|---|---|
| **Quickstart inbyggd servermotor (9.4)** | S: Stöds |
| Oracle WebLogic Server 12.2 (12cR2) | Z: Stöds inte |
| IBM WebSphere Application Server Continuous Delivery (LibertyProfile) med Web Profile 7.0 och IBM JRE 1.8 | R: Begränsad support för nya kontrakt `[2]` |
| IBM WebSphere Application Server 9.0 och IBM JRE 1.8 | R: Begränsad support för nya kontrakt `[1]` `[2]` |
| Apache Tomcat 8.5.x | R: Begränsad support för nya kontrakt `[2]` |
| JBoss EAP 7.2.x med JBoss Application Server | Z: Stöds inte |
| JBoss EAP 7.1.4 med JBoss Application Server | R: Begränsad support för nya kontrakt `[1]` `[2]` |
| JBoss EAP 7.0.x med JBoss Application Server | Z: Stöds inte |

1. Rekommenderas för driftsättningar med AEM Forms.
1. Från och med AEM 6.5-distributioner på programservrar går det till begränsad support. Befintliga kunder kan uppgradera till AEM 6.5 och fortsätta använda programservrar. För nya kunder innehåller det supportkriterier och ett supportprogram enligt beskrivningen ovan.

### Operativsystem för servrar {#server-operating-systems}

Adobe Experience Manager fungerar med följande serverplattformar för produktionsmiljöer:

| **Plattform** | **Supportnivå** |
|---|---|
| **Linux, baserat på Red Hat-distribution** | S: Stöds `[1]` `[3]` |
| Linux baserat på Debian-distribution inkl. Ubuntu | S: Stöds `[2]` |
| Linux, baserat på SUSE-distribution | S: Stöds |
| Microsoft Windows Server 2019 `[4]` | R: Begränsad support för nya kontrakt |
| Microsoft Windows Server 2016 `[4]` | R: Begränsad support för nya kontrakt `[5]` |
| Microsoft Windows Server 2012 R2 | Z: Stöds inte |
| Oracle Solaris 11 | Z: Stöds inte |
| IBM AIX 7.2 | Z: Stöds inte |

1. Linux Kernel 2.6, 3.x och 4.x innehåller derivat från Red Hat-distributionen, inklusive Red Hat Enterprise Linux, CentOS, Oracle Linux och Amazon Linux. AEM Forms tilläggsfunktioner stöds endast i CentOS 7, Red Hat Enterprise Linux 7 och Red Hat Enterprise Linux 8.
1. AEM Forms stöds bara på Ubuntu 16.04 LTS
1. Linux-distribution som stöds av Adobe Managed Services
1. Produktionsinstallationer i Microsoft Windows stöds för kunder som uppgraderar till 6.5 och för icke-produktionsanvändning. Nya driftsättningar är på begäran för AEM Sites och Assets.
1. AEM Forms stöds på Microsoft Windows Server utan begränsningar på supportnivå R.


### Virtuella miljöer och molnmiljöer {#virtual-cloud-computing-environments}

Adobe Experience Manager stöds i en virtuell dator i molnmiljöer som Microsoft Azure och Amazon Web Services (AWS), i enlighet med de tekniska krav som anges på den här sidan och i enlighet med Adobe standardsupportvillkoren.

Adobe rekommenderar att du använder Adobes hanterade tjänster för att distribuera AEM på Azure eller AWS. Adobes hanterade tjänster ger experterna erfarenhet och kunskaper av att driftsätta och AEM i dessa molndatormiljöer. Se [ytterligare dokumentation om Adobe Managed Services](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t).

I alla andra fall där AEM distribueras på Azure eller AWS, eller i någon annan molndatormiljö, kommer support från Adobe att finnas i den virtuella datormiljön i enlighet med de tekniska specifikationer som anges på den här sidan. Alla rapporterade problem som rör AEM som körs i någon av dessa molnmiljöer måste kunna reproduceras oberoende av alla molntjänster som är specifika för molndatormiljön, såvida inte molntjänsten specifikt stöds som en del av de tekniska krav som anges på den här sidan, till exempel Azure Blob Storage eller AWS S3.

För rekommendationer om hur du distribuerar AEM på Azure eller AWS, utanför Adobe Managed Services, rekommenderar Adobe starkt att du arbetar direkt med molnleverantören eller Adobe-partners som stöder distributionen av AEM i den molnmiljö du väljer. Den valda molnleverantören eller partnern ansvarar för storleksspecifikationerna, designen och implementeringen av arkitekturen, för att uppfylla dina specifika krav på prestanda, belastning, skalbarhet och säkerhet.

### Dispatcher Platforms (webbservrar) {#dispatcher-platforms-web-servers}

Dispatcher är komponenten för cachelagring och belastningsutjämning. [Ladda ned den senaste Dispatcher-versionen](https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html). Experience Manager 6.5 kräver Dispatcher version 4.3.2 eller senare.

Följande webbservrar kan användas med Dispatcher version 4.3.2:

| Plattform | Supportnivå |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | S: Stöds |
| Microsoft IIS 10 (Internet Information Server) | S: Stöds |
| Microsoft IIS 8.5 (Internet Information Server) | Z: Stöds inte |

1. Webbservrar som byggts utifrån Apache httpd-källkoden har samma supportnivå som den version av httpd som den baseras på. Om du är osäker kan du be Adobe om en bekräftelse av den supportnivå som gäller respektive serverprodukt. Följande fall:

   1. HTTP-servern byggdes med enbart officiella källdistributioner av Apache, eller
   1. HTTP-servern levererades som en del av det operativsystem där den körs. Exempel: IBM HTTP Server, Oracle HTTP Server

1. Dispatcher är inte tillgänglig för Apache 2.4.x för Windows.

## Klientplattformar som stöds {#supported-client-platforms}

### Webbläsare som stöds för redigeringsgränssnittet {#supported-browsers-for-authoring-user-interface}

Adobe Experience Manager användargränssnitt fungerar med följande klientplattformar. Alla webbläsare testas med standarduppsättningen med plugin-program och tillägg.

Det AEM användargränssnittet är optimerat för större skärmar (vanligen bärbara och stationära datorer) och surfplattor (t.ex. Apple iPad eller Microsoft Surface). Telefonformfaktorn stöds inte.

>[!NOTE]
>
>**Stöd för webbläsare med snabb lansering:**
>
>Uppdateringar för Mozilla Firefox, Google Chrome och Microsoft Edge var sjätte månad. Adobe tillhandahåller uppdateringar för Adobe Experience Manager för att upprätthålla den supportnivå som anges nedan för kommande versioner av dessa webbläsare.

<table>
 <tbody>
  <tr>
   <td><strong>Webbläsare</strong></td>
   <td><strong>Stöd för användargränssnitt<br /> </strong></td>
   <td><strong>Stöd för Classic UI</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome (Evergreen)</strong></td>
   <td>S: Stöds</td>
   <td>S: Stöds</td>
  </tr>
  <tr>
   <td>Microsoft Edge (Evergreen)</td>
   <td>S: Stöds</td>
   <td>S: Stöds</td>
  </tr>
  <tr>
   <td>Microsoft Internet Explorer 11</td>
   <td>Z: Stöds inte</td>
   <td>Z: Stöds inte</td>
  </tr>
  <tr>
   <td>Mozilla Firefox (Evergreen)</td>
   <td>S: Stöds</td>
   <td>S: Stöds</td>
  </tr>
  <tr>
   <td>Mozilla Firefox last ESR [1]</td>
   <td>S: Stöds</td>
   <td>S: Stöds</td>
  </tr>
  <tr>
   <td>Apple Safari på macOS (Evergreen)</td>
   <td>S: Stöds</td>
   <td>S: Stöds</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x på macOS</td>
   <td>Z: Stöds inte</td>
   <td>Z: Stöds inte</td>
  </tr>
  <tr>
   <td>Apple Safari på iOS 12.x</td>
   <td>S: Stöds [2]</td>
   <td>Z: Stöds inte</td>
  </tr>
  <tr>
   <td>Apple Safari på iOS 11.x</td>
   <td>Z: Stöds inte</td>
   <td>Z: Stöds inte</td>
  </tr>
 </tbody>
</table>

1. Extended Support Release för Firefox [Läs mer om detta på mozilla.org](https://www.mozilla.org/en-US/firefox/organizations/faq/)
1. stöd för Apple iPad

### Webbläsare som stöds för webbplatser {#supported-browsers-for-websites}

I allmänhet beror webbläsarstöd för webbplatser som återges av AEM Sites på implementeringen av AEM sidmallar, design och komponentutdata, och är därför styrande för den part som implementerar dessa delar.

### WebDAV-klienter {#webdav-clients}

**Microsoft Windows 7+**

Om du vill ansluta med Microsoft Windows 7+ till en AEM som inte är säker med SSL måste grundläggande autentisering över oskyddat nätverk aktiveras i Windows. Detta kräver en ändring i Windows-registret för WebClient:

1. Leta reda på registerundernyckeln:

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. Lägg till registerposten BasicAuthLevel till den här undernyckeln med värdet 2 eller mer.

För att WebDav-klienten ska bli mer responsiv i Windows - se [Microsoft Support KB 2445570](https://support.microsoft.com/kb/2445570)

## Information om ytterligare plattformar {#additional-platform-notes}

I det här avsnittet finns specialanteckningar och mer detaljerad information om hur du kör Adobe Experience Manager och dess tillägg.

### IPv4 och IPv6 {#ipv-and-ipv}

Alla element i Adobe Experience Manager (Instance, Dispatcher) kan installeras i både IPv4- och IPv6-nätverk.

Åtgärden är smidig eftersom ingen speciell konfiguration krävs. Du kan bara ange en IP-adress i det format som passar nätverkstypen om det behövs.

Det innebär att när en IP-adress måste anges kan du välja (efter behov) bland:

* en IPv6-adress, till exempel `https://[ab12::34c5:6d7:8e90:1234]:4502`

* en IPv4-adress, till exempel `https://123.1.1.4:4502`

* ett servernamn, till exempel `https://www.yourserver.com:4502`

* standardfallet för `localhost` tolkas för till exempel både IPv4- och IPv6-nätverksinstallationer, `https://localhost:4502`

### Krav för AEM Dynamic Media Add-on {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media är inaktiverat som standard. Här kan du [aktivera Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

När Dynamic Media är aktiverat gäller följande ytterligare tekniska krav.

>[!NOTE]
>
>Dessa systemkrav **endast** tillämpa om du använder Dynamic Media - hybrid-läge; Dynamic Media - Hybridläget har en inbäddad bildserver, som bara är certifierad på vissa operativsystem.
>
>För Dynamic Media-kunder som kör Dynamic Media - Scene7-läge (dvs. **dynamicmedia_scene7** runmode), det finns inga ytterligare systemkrav, endast samma systemkrav som AEM. Dynamic Media - Scene7-lägesarkitektur använder den molnbaserade bildtjänsten och inte den tjänst som är inbäddad i AEM.

#### Maskinvara {#hardware}

Följande maskinvarukrav gäller för både Linux och Windows:

* Intel Xeon- eller AMD Opteron-processor med minst 4 kärnor
* Minst 16 GB RAM

#### Linux {#linux}

Om du använder Dynamic Media i Linux måste följande krav vara uppfyllda:

* RedHat Enterprise 7 eller CentOS 7 och senare med de senaste korrigeringsfilerna
* 64-bitars operativsystem
* Växling inaktiverad (rekommenderas)
* SELinux är inaktiverat (se anm. nedan)

>[!NOTE]
>
>Om språkinställningen är inställd så att LC_CTYPE inte är lika med `en_US.UTF-8`så att Dynamic Media inte fungerar. Om du vill se vilket värde det har skriver du &quot;locale&quot; i kommandotolken. Om det inte är det anger du LC_CTYPE-miljövariabeln till den tomma strängen genom att skriva &quot;export LC_CTYPE=&quot; innan du kör AEM.

>[!NOTE]
>
>**Inaktiverar SELinux:** Image Serving fungerar inte med SELinux aktiverat. Det här alternativet är aktiverat som standard. Du kan åtgärda problemet genom att redigera **/etc/selinux/config** och ändra SELinux-värdet från:
>
>`SELINUX=enforcing` **till** `SELINUX=disabled`

>[!NOTE]
>
>**NUMA-arkitektur:** System med processorer med AMD64 och Intel EM64T är vanligtvis konfigurerade som icke-enhetliga minnesarkitekturplattformar (NUMA), vilket innebär att kärnan konstruerar flera minnesnoder vid start i stället för att konstruera en enda minnesnod.
>
>Konstruktionen för flera noder kan resultera i minnesöverbelastning på en eller flera av noderna innan andra noder töms. När minnesöverbelastning inträffar kan kärnan bestämma sig för att avsluta processer (till exempel Image Server eller Platform Server) trots att det finns tillgängligt minne.
>
>Därför rekommenderar Adobe att du stänger av NUMA med **numa=off** startalternativ för att undvika att kärnan tar kål på dessa processer.

>[!NOTE]
>
>**Servervärdnamnet måste matcha:** Kontrollera att serverns värdnamn kan matchas till en IP-adress. Om det inte är möjligt lägger du till det fullständiga, kvalificerade värdnamnet och IP-adressen i **/etc/värdar**:
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft Windows Server 2016
* Växla utrymme motsvarande minst dubbelt så mycket fysiskt minne (RAM)

Om du vill använda Dynamic Media i Windows installerar du omdistribuerbara Microsoft Visual Studio 2010, 2013 och 2015 för x64 och x86.

För Windows x64:

* Få Microsoft Visual Studio 2010 återdistribuerbart på [https://www.microsoft.com/en-us/download/details.aspx?id=13523](https://www.microsoft.com/en-us/download/details.aspx?id=13523)
* Få Microsoft Visual Studio 2013 återdistribuerbart på [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)
* Få Microsoft Visual Studio 2015 återdistribuerbart på [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

För Windows x86:

* Få Microsoft Visual Studio 2010 återdistribuerbart på [https://www.microsoft.com/en-in/download/details.aspx?id=5555](https://www.microsoft.com/en-in/download/details.aspx?id=5555)
* Få Microsoft Visual Studio 2013 återdistribuerbart på [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* Få Microsoft Visual Studio 2015 återdistribuerbart på [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)

#### macOS {#macos}

* 10.9.x och senare
* Stöds endast i demos- och testversioner

### Krav för AEM Forms PDF Generator {#requirements-for-aem-forms-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>Produkt</strong></p> </th>
   <th><p><strong>Format som stöds för konvertering till PDF</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Klassiskt Acrobat 2017-spår</a> senaste versionen</td>
   <td>XPS, bildformat (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF och DWF</td>
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
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, bildformat (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF och TXT</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>PDF Generator stöder endast engelska, franska, tyska och japanska versioner av de operativsystem och program som stöds.
>
>Dessutom:
>
>* PDF Generator kräver 32-bitarsversionen av [Acrobat 2017 Classic track version 17.011.30078 eller senare](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) för att utföra konverteringen.
>* PDF Generator stöder endast 32-bitarsversionen av Microsoft Office Professional Plus och andra program som krävs för konvertering.
>* PDF Generator stöder inte Microsoft Office 365.
>* PDF Generator-konverteringar för OpenOffice stöds bara i Windows och Linux.
>* Funktionerna OCR PDF, Optimize PDF och Export PDF stöds endast i Windows.
>* En version av Acrobat medföljer AEM Forms för att aktivera PDF Generator-funktionaliteten. Programmeringsversionen ska endast användas med AEM Forms under AEM Forms-licensens löptid, för användning med AEM Forms PDF Generator. Mer information finns i AEM Forms produktbeskrivning för din distribution ([Lokal](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) eller [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))&quot;
>
>* PDF Generator-tjänsten stöder inte Microsoft Windows 10.
>


### Krav för AEM Forms Designer {#requirements-for-aem-forms-designer}

* Microsoft® Windows® 2016 Server, Microsoft® Windows® 2019 Server eller Microsoft® Windows® 10
* 1 GHz eller snabbare processor med stöd för PAE, NX och SSE2.
* 1 GB RAM för 32-bitars eller 2 GB RAM för 64-bitars operativsystem
* 16 GB diskutrymme för 32-bitars eller 20 GB diskutrymme för 64-bitars operativsystem
* Grafikminne - 128 MB GPU (256 MB rekommenderas)
* 2,35 GB ledigt hårddiskutrymme
* Bildskärmsupplösning på 1 024 x 768 pixlar eller högre
* Maskinvaruacceleration för video (valfritt)
* Acrobat Pro DC, Acrobat Standard DC eller Adobe Acrobat Reader DC.
* Administrativ behörighet för att installera Designer.

### Krav för AEM Assets XMP metadata write-back {#requirements-for-aem-assets-xmp-metadata-write-back}

XMP stöds och är aktiverat för följande plattformar och filformat:

* **Operativsystem:**

   * Linux (stöd för 32-bitars och 32-bitars program i 64-bitarssystem). Anvisningar om hur du installerar 32-bitars klientbibliotek finns i [Aktivera XMP och återskrivning på 64-bitars RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).

   * Windows Server
   * Mac OS X (64-bitars)

* **Filformat**: JPEG, PNG, TIFF, PDF, INDD, AI och EPS.

### Krav för AEM Assets att bearbeta metadataintensiva resurser i Linux {#assetsonlinux}

XMPFilesProcessor-processen kräver biblioteket GLIBC_2.14 för att fungera. Använd en Linux-kärna som innehåller GLIBC_2.14, till exempel Linux-kärna version 3.1.x. Prestandan för bearbetning av resurser som innehåller en stor mängd metadata förbättras, till exempel PSD-filer. Om du använder en tidigare version av GLIBC uppstår fel i loggar som börjar med `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`.
