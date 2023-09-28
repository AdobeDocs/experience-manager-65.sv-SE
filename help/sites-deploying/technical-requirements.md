---
title: Tekniska krav
description: En lista över de klient- och serverplattformar som stöds för Adobe Experience Manager.
topic-tags: platform
exl-id: 47529b9a-c4e5-434f-ac26-b01714ff863b
source-git-commit: 0dd6e3fc2fa9539e5c3ce4e99ab367752dfeaad6
workflow-type: tm+mt
source-wordcount: '3597'
ht-degree: 0%

---

# Tekniska krav{#technical-requirements}

Adobe stöder (AEM) Adobe Experience Manager på plattformarna enligt följande information i det här dokumentet.

Kontakta plattformsleverantören om du har frågor som rör plattformen.

>[!NOTE]
>
>Beroende på vilken plattform du installerar AEM på kan det finnas olika uppsättningar krav för användarhantering.

## Förutsättningar {#prerequisites}

Lägsta krav för installation av Adobe Experience Manager:

* Installerad Java™ Platform, Standard Edition JDK eller annat som stöds [Java™ Virtual Machines](#java-virtual-machines)
* Experience Manager QuickStart-fil (fristående JAR eller WAR för webbapplikationsdistribution)

### Krav för minsta storlek {#minimum-sizing-requirements}

Lägsta krav för Adobe Experience Manager:

* 5 GB ledigt utrymme i installationskatalogen
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
   <td><strong>A: Stöds</strong></td>
   <td>Adobe ger fullständigt stöd och underhåll för den här konfigurationen. Den här konfigurationen omfattas av Adobe kvalitetssäkringsprocess.</td>
  </tr>
  <tr>
   <td><strong>R: Begränsat stöd</strong></td>
   <td>För att våra kunder ska lyckas erbjuder Adobe full support inom ramen för ett begränsat supportprogram, vilket kräver att specifika villkor uppfylls. Support på R-nivå kräver en formell kundförfrågan och en bekräftelse från Adobe. Mer information får du av Adobe kundtjänst.</td>
  </tr>
 </tbody>
</table>

### Konfigurationer som inte stöds {#unsupported-configurations}

| Supportnivå | Beskrivning |
|---|---|
| **Z: Stöds inte** | Konfigurationen stöds inte. Adobe gör inga programsatser om huruvida konfigurationen fungerar eller inte. |

## Plattformar som stöds {#supported-platforms}

### Java™ Virtual Machines {#java-virtual-machines}

Programmet kräver att en Java™ Virtual Machine körs, vilket tillhandahålls av Java™ Development Kit-distributionen (JDK).

Adobe Experience Manager fungerar med följande versioner av Java™ Virtual Machines:

>[!CAUTION]
>
>Spåra säkerhetsbulletiner från Java™-leverantören. Detta garanterar produktionsmiljöernas säkerhet och säkerhet. Installera även alltid de senaste Java™-uppdateringarna.

| **Plattform** | **Supportnivå** | **Länk** |
|---|---|---|
| Oracle Java™ SE 17 JDK | Z: Stöds inte `[1]` |
| Oracle Java™ SE 11 JDK - 64 bitar | A: Stöds `[1]` | [Ladda ned](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+11*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=24&lt;td>) |
| Oracle Java™ SE 10 JDK | Z: Stöds inte `[1]` |
| Oracle Java™ SE 9 JDK | Z: Stöds inte `[1]` |
| Oracle Java™ SE 8 JDK - 64 bitar | A: Stöds `[1]` | [Ladda ned](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+8*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=10) |
| IBM® J9 VM - build 2.9, JRE 1.8.0 | A: Stöds `[2]` |
| IBM® J9 VM - build 2.8, JRE 1.8.0 | A: Stöds `[2]` |
| Azul Zulu OpenJDK 11 - 64 bitar | A: Stöds `[3]` | |
| Azul Zulu OpenJDK 8 - 64 bitar | A: Stöds `[3]` | |

1. Oraclet har övergått till en&quot;LTS-modell (Long Term Support) för Oracle Java™ SE-produkter. Java™ 9, Java™ 10 och Java™ 12 är icke-LTS-versioner som Oracle (se [Oracle Java™ SE - supportöversikt](https://www.oracle.com/technetwork/java/eol-135779.html)). För att driftsätta AEM i en produktionsmiljö har Adobe endast stöd för LTS-versionerna av Java™. Stöd för och distribution av Oraclet Java™ SE JDK, inklusive alla underhållsuppdateringar av LTS-releaser som ligger utanför de offentliga uppdateringarna, stöds av Adobe direkt för alla AEM som använder Oraclet Java™ SE. Se [Java™ - supportpolicy för Adobe Experience Manager](assets/Java_Policy_for_Adobe_Experience_Manager.pdf).
   **Viktigt: Oraclet Java™ 11 stöds minst fram till september 2026. Stöd för Oraclet Java™ 17 är under utveckling.**

1. IBM® JRE stöds endast tillsammans med WebSphere® Application Server.

1. Azul Zulu OpenJDK LTS-versioner stöds för lokala AEM-distributioner från och med version 6.5 SP9. Support och distribution av Azul Zulu JDK LTS-versionerna måste licensieras direkt från Azul av Adobe-kunder.


### Lagring och beständighet {#storage-persistence}

Det finns olika alternativ för att distribuera Adobe Experience Manager-databasen. Se följande lista för de tekniker och lagringsalternativ som stöds.

| **Plattform** | **Beskrivning** | **Supportnivå** |
|---|---|---|
| **Filsystem med TAR-filer** `[1]` | Databas | A: Stöds |
| **Filsystem med datastore** `[1]` | Binärfiler | A: Stöds |
| Lagra binärfiler i TAR-filer i filsystemet `[1]` | Binärfiler | Z: Stöds inte för produktion |
| Amazon S3 | Binärfiler | A: Stöds |
| Microsoft® Azure Blob Storage | Binärfiler | A: Stöds |
| MongoDB Enterprise 4.4 | Databas | A: Stöds `[2, 3, 4]` |
| MongoDB Enterprise 4.2 | Databas | A: Stöds `[2, 3, 4]` |
| MongoDB Enterprise 4.0 | Databas | Z: Stöds inte |
| MongoDB Enterprise 3.6 | Databas | Z: Stöds inte |
| MongoDB Enterprise 3.4 | Databas | Z: Stöds inte |
| IBM® DB2® 10.5 | Databas och databas för Forms | R: Begränsat stöd `[5]` |
| Oracle Database 12c (12.1.x) | Databas och databas för Forms | R: Begränsat stöd |
| Microsoft® SQL Server 2016 | Forms-databas | A: Stöds |
| **Apache Lucene (inbyggt i Quickstart)** | Söktjänst | A: Stöds |
| Apache Solr | Söktjänst | A: Stöds |

1. &#39;Filsystem&#39; inkluderar blocklagring som är POSIX-kompatibel. Innehåller nätverkslagringsteknik. Tänk på att filsystemets prestanda kan variera och påverka den övergripande prestandan. Läs in AEM med nätverks-/fjärrfilsystemet.
1. MongoDB Enterprise version 4.2 och 4.4 kräver minst AEM 6.5 SP9.
1. MongoDB-delning stöds inte i AEM.
1. MongoDB-lagringsmotorn WiredTiger stöds endast.
1. Stöds för AEM Forms uppgraderingskunder. Stöds inte för nya installationer.
1. Gäller endast AEM Forms:
   * Stöd för Oracle Database 12c har tagits bort och stöd för Oracle Database 19c har lagts till.
   * Borttaget stöd för Microsoft® SQL Server 2016 och utökat stöd för Microsoft® SQL Server 2019.

>[!NOTE]
>
Se [Distribuera webbgrupper](/help/communities/deploy-communities.md) om du vill ha mer information om AEM Communities.

>[!NOTE]
>
MongoDB är ett program från tredje part och ingår inte i AEM licenspaket. Mer information finns i [MongoDB-licenspolicy](https://www.mongodb.com/licensing/server-side-public-license/faq) sida.
>
För att få ut så mycket som möjligt av er AEM med MongoDB rekommenderar Adobe att ni har licenser för MongoDB Enterprise-versionen och får tillgång till professionell support. Se [Rekommenderade distributioner](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk) för mer information.
>
Licensen innehåller en standardreplikuppsättning som består av en primär och två sekundära instanser som kan användas för antingen författar- eller publiceringsdistributionerna.
>
Om du vill köra både författare och publicera på MongoDB måste två separata licenser köpas.
>
Adobe kundtjänst hjälper till med kvalificerande problem som rör användningen av MongoDB med AEM.
>
Mer information finns i [MongoDB för Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).

>[!NOTE]
>
De relationsdatabaser som stöds enligt ovan är tredjepartsprogram och ingår inte i AEM licenspaket.
>
För att köra AEM 6.5 med en relationsdatabas som stöds krävs ett separat supportavtal med en databasleverantör. Adobe kundtjänst hjälper dig att hantera kvalificeringsproblem som rör användningen av relationsdatabaser med AEM 6.5.
>
**De flesta relationsdatabaser stöds för närvarande i Level-R på AEM 6.5, som innehåller stödkriterier och ett supportprogram enligt beskrivningen ovan.**

### Servletmotorer/programservrar {#servlet-engines-application-servers}

Adobe Experience Manager kan köras antingen som en fristående server (snabbstart-JAR-filen) eller som ett webbprogram i en tredjepartsprogramserver (WAR-filen).

Den lägsta servlet API-version som krävs är Servlet 3.1

| Plattform | Supportnivå |
|---|---|
| **Quickstart inbyggd servermotor (9.4)** | A: Stöds |
| Oracle WebLogic Server 12.2 (12cR2) | Z: Stöds inte |
| IBM® WebSphere® Application Server Continuous Delivery (LibertyProfile) med Web Profile 7.0 och IBM® JRE 1.8 | R: Begränsad support för nya kontrakt `[2]` |
| IBM® WebSphere® Application Server 9.0 och IBM® JRE 1.8 | R: Begränsad support för nya kontrakt `[1]` `[2]` |
| Apache Tomcat 8.5.x | R: Begränsad support för nya kontrakt `[2]` |
| JBoss® EAP 7.2.x med JBoss® Application Server | Z: Stöds inte |
| JBoss® EAP 7.1.4 med JBoss® Application Server | R: Begränsad support för nya kontrakt `[1]` `[2]` |
| JBoss® EAP 7.0.x med JBoss® Application Server | Z: Stöds inte |

1. Rekommenderas för driftsättningar med AEM Forms.
1. Från och med AEM 6.5-distributioner på programservrar går det till begränsad support. Befintliga kunder kan uppgradera till AEM 6.5 och fortsätta använda programservrar. För nya kunder innehåller det supportkriterier och ett supportprogram enligt beskrivningen ovan.
1. Gäller endast AEM Forms:
   * Borttaget stöd för JBoss® EAP 7.1.4 och utökat stöd för JBoss® EAP 7.4.10.

### Operativsystem för servrar {#server-operating-systems}

Adobe Experience Manager fungerar med följande serverplattformar för produktionsmiljöer:

| **Plattform** | **Supportnivå** |
|---|---|
| **Linux®, baserat på distributionen av Red Hat®** | A: Stöds `[1]` `[3]` |
| Linux®, baserat på Debian-distribution inkl. Ubuntu | A: Stöds `[1]` `[2]` |
| Linux®, baserat på SUSE®-distribution | A: Stöds `[1]` |
| Microsoft® Windows Server 2019 `[4]` | R: Begränsad support för nya kontrakt `[5]` |
| Microsoft® Windows Server 2016 `[4]` | R: Begränsad support för nya kontrakt `[5]` |
| Microsoft® Windows Server 2012 R2 | Z: Stöds inte |
| Oracle Solaris™ 11 | Z: Stöds inte |
| IBM® AIX® 7.2 | Z: Stöds inte |

1. Linux® Kernel 2.6, 3. x, 4. x och 5. x innehåller derivat från distributionen av Red Hat®, inklusive Red Hat® Enterprise Linux®, CentOS, Oracle Linux® och Amazon Linux®. AEM Forms tilläggsfunktioner stöds endast i CentOS 7, Red Hat® Enterprise Linux® 7, Red Hat® Enterprise Linux® 8 och Red Hat® Enterprise Linux® 9.
1. AEM Forms stöds på Ubuntu 20.04 LTS.
1. Linux®-distribution stöds av Adobe Managed Services.
1. Produktionsinstallationer i Microsoft® Windows stöds för kunder som uppgraderar till 6.5 och för icke-produktionsanvändning. Nya distributioner är på begäran för AEM Sites and Assets.
1. AEM Forms stöds på Microsoft® Window Server utan begränsningar på supportnivå R.
1. AEM Forms har tagit bort stöd för Microsoft® Windows Server 2016.

>[!NOTE]
>
Om du installerar AEM Forms 6.5 kontrollerar du att du har installerat följande 32-bitars Microsoft® Visual C++ Redistributable.
>
* Microsoft® Visual C++ 2008 återdistribuerbar
* Återdistribuerbar Microsoft® Visual C++ 2010
* Microsoft® Visual C++ 2012 återdistribuerbar
* Microsoft® Visual C++ 2013 återdistribuerbar
* Microsoft® Visual C++ 2019 (VC14.28 eller senare) återdistribuerbar



### Virtuella miljöer och molnmiljöer {#virtual-cloud-computing-environments}

Adobe Experience Manager stöds när det körs i en virtuell dator i molnmiljöer. Dessa miljöer omfattar Microsoft® Azure och Amazon Web Services (AWS), som körs i enlighet med de tekniska krav som anges på den här sidan och enligt Adobe standardsupportvillkor.

För en molnbaserad miljö kan du titta på det senaste erbjudandet från produktserien AEM: Adobe Experience Manager as a Cloud Service. Se [Adobe Experience Manager as a Cloud Service Documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=en) för mer information.

Adobe erbjuder också Adobe Managed Services att distribuera AEM på Azure eller AWS. Adobe Managed Services förser experterna med erfarenhet och kompetens av att driftsätta och AEM i dessa molnmiljöer. Se [ytterligare dokumentation om Adobe Managed Services](https://business.adobe.com/products/experience-manager/managed-services.html?aemClk=t).

I alla andra fall där AEM distribueras på Azure eller AWS, eller i någon annan molndatormiljö, finns stöd från Adobe i den virtuella datormiljön. Den virtuella miljön måste köras i enlighet med de tekniska specifikationer som anges på den här sidan. Alla rapporterade problem som rör AEM som körs i någon av dessa molnmiljöer måste kunna reproduceras oberoende av alla molntjänster som är specifika för molndatormiljön. Det vill säga, om inte molntjänsten stöds som en del av de tekniska krav som anges på den här sidan, till exempel Azure Blob Storage eller AWS S3.

Adobe rekommenderar att du arbetar direkt med molnleverantören för att få rekommendationer om hur du ska distribuera AEM på Azure eller AWS utanför Adobe Managed Services. Eller i samarbete med Adobe partners som stöder driftsättningen av AEM i molnmiljön. Den valda molnleverantören eller partnern ansvarar för storleksspecifikationer, utformning och implementering av arkitekturen för att uppfylla dina specifika krav på prestanda, belastning, skalbarhet och säkerhet.

### Dispatcher Platforms (webbservrar) {#dispatcher-platforms-web-servers}

Dispatcher är komponenten för cachelagring och belastningsutjämning. [Hämta den senaste Dispatcher-versionen](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html?lang=en). Experience Manager 6.5 kräver Dispatcher version 4.3.2 eller senare.

Följande webbservrar kan användas med Dispatcher version 4.3.2:

| Plattform | Supportnivå |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | A: Stöds |
| Microsoft® IIS 10 (Internet Information Server) | A: Stöds |
| Microsoft® IIS 8.5 (Internet Information Server) | Z: Stöds inte |

1. Webbservrar som byggts utifrån Apache httpd-källkoden har lika mycket stöd som den version av httpd som den baseras på. Om du är osäker kan du be Adobe om en bekräftelse av den supportnivå som gäller respektive serverprodukt. Följande fall:

   1. HTTP-servern byggdes med enbart officiella källdistributioner av Apache, eller
   1. HTTP-servern levererades som en del av det operativsystem där den körs. Exempel: IBM® HTTP Server, Oracle HTTP Server

1. Dispatcher är inte tillgänglig för Apache 2.4.x för Windows.

## Klientplattformar som stöds {#supported-client-platforms}

### Webbläsare som stöds för redigeringsgränssnittet {#supported-browsers-for-authoring-user-interface}

Adobe Experience Manager användargränssnitt fungerar med följande klientplattformar. Alla webbläsare testas med standarduppsättningen med plugin-program och tillägg.

AEM användargränssnitt är optimerat för större skärmar (vanligtvis bärbara och stationära datorer) och surfplattans formfaktor (till exempel Apple iPad eller Microsoft® Surface). Telefonformfaktorn stöds inte.

>[!NOTE]
>
**Stöd för webbläsare med snabb lansering:**
>
Uppdateringar för Mozilla Firefox, Google Chrome och Microsoft® Edge var sjätte månad. Adobe tillhandahåller uppdateringar för Adobe Experience Manager för att upprätthålla den supportnivå som anges nedan för kommande versioner av dessa webbläsare.

<table>
 <tbody>
  <tr>
   <td><strong>Webbläsare</strong></td>
   <td><strong>Stöd för användargränssnitt<br /> </strong></td>
   <td><strong>Stöd för Classic UI</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome (vintergrön)</strong></td>
   <td>A: Stöds</td>
   <td>A: Stöds</td>
  </tr>
  <tr>
   <td>Microsoft® Edge (Evergreen)</td>
   <td>A: Stöds</td>
   <td>A: Stöds</td>
  </tr>
  <tr>
   <td>Microsoft® Internet Explorer 11</td>
   <td>Z: Stöds inte</td>
   <td>Z: Stöds inte</td>
  </tr>
  <tr>
   <td>Mozilla Firefox (Evergreen)</td>
   <td>A: Stöds</td>
   <td>A: Stöds</td>
  </tr>
  <tr>
   <td>Mozilla Firefox last ESR [1]</td>
   <td>A: Stöds</td>
   <td>A: Stöds</td>
  </tr>
  <tr>
   <td>Apple Safari på macOS (vintergrön)</td>
   <td>A: Stöds</td>
   <td>A: Stöds</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x på macOS</td>
   <td>Z: Stöds inte</td>
   <td>Z: Stöds inte</td>
  </tr>
  <tr>
   <td>Apple Safari på iOS 12.x</td>
   <td>A: Stöds [2]</td>
   <td>Z: Stöds inte</td>
  </tr>
  <tr>
   <td>Apple Safari på iOS 11.x</td>
   <td>Z: Stöds inte</td>
   <td>Z: Stöds inte</td>
  </tr>
 </tbody>
</table>

1. Extended Support Release för Firefox [Läs mer på mozilla.org](https://www.mozilla.org/en-US/firefox/enterprise/)
1. stöd för Apple iPad

### Webbläsare som stöds för webbplatser {#supported-browsers-for-websites}

I allmänhet är webbläsarstöd för webbplatser som återges av AEM Sites beroende av implementeringen av AEM sidmallar, design och komponentutdata, och det är därför den part som implementerar dessa delar som bestämmer.

### WebDAV-klienter {#webdav-clients}

**Microsoft® Windows 7+**

När du ansluter med Microsoft® Windows 7+ till en AEM som inte är skyddad med SSL måste grundläggande autentisering över ett oskyddat nätverk aktiveras i Windows. Det kräver en ändring i Windows-registret för WebClient:

1. Leta reda på registerundernyckeln:

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. Lägg till registerposten BasicAuthLevel till den här undernyckeln med värdet 2 eller mer.

## Ytterligare plattformsanteckningar {#additional-platform-notes}

Det här avsnittet innehåller särskilda anteckningar och mer detaljerad information om hur du kör Adobe Experience Manager och dess tillägg.

### IPv4 och IPv6 {#ipv-and-ipv}

Alla element i Adobe Experience Manager (Instance, Dispatcher) kan installeras i både IPv4- och IPv6-nätverk.

Driften är sömlös eftersom ingen speciell konfiguration krävs. Du anger en IP-adress med det format som är lämpligt för din nätverkstyp, om det behövs.

När en IP-adress måste anges kan du välja (efter behov) från följande:

* En IPv6-adress. Till exempel, `https://[ab12::34c5:6d7:8e90:1234]:4502`

* En IPv4-adress. Till exempel, `https://123.1.1.4:4502`

* Ett servernamn. Till exempel, `https://www.yourserver.com:4502`

* Standardskiftläget för `localhost` tolkas för både IPv4- och IPv6-nätverksinstallationer. Till exempel, `https://localhost:4502`

### Krav för AEM Dynamic Media Add-on {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media är inaktiverat som standard. Se här för att [aktivera Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

När Dynamic Media är aktiverat gäller följande ytterligare tekniska krav.

>[!NOTE]
>
Dessa systemkrav **gäller endast** om du använder Dynamic Media - Hybrid-läge. Dynamic Media - Hybrid-läget har en inbäddad bildserver som endast är certifierad på vissa operativsystem.
>
För Dynamic Media-kunder som kör Dynamic Media - Scene7-läge (d.v.s. dynamicmedia_scene7 **körningsläge) finns det inga ytterligare systemkrav, bara samma systemkrav som AEM.** Dynamic Media - Scene7-lägesarkitektur använder den molnbaserade bildtjänsten och inte den tjänst som är inbäddad i AEM.

#### Maskinvara {#hardware}

Följande maskinvarukrav gäller för både Linux® och Windows:

* Intel Xeon®- eller AMD® Opteron-processor med minst fyra kärnor
* Minst 16 GB RAM

#### Linux® {#linux}

Om du använder Dynamic Media i Linux® måste följande krav vara uppfyllda:

* Red Hat® Enterprise 7 eller CentOS 7 och senare med de senaste korrigeringsfilerna
* 64-bitars operativsystem
* Växling inaktiverad (rekommenderas)
* SELinux är inaktiverat (se anm. nedan)

>[!NOTE]
>
Om språkinställningen är inställd så att LC_CTYPE inte är lika med `en_US.UTF-8`så att Dynamic Media inte fungerar. Om du vill se vilket värde det har skriver du&quot;locale&quot; i kommandotolken. Om den inte är korrekt inställd anger du LC_CTYPE-miljövariabeln till den tomma strängen genom att skriva &quot;export LC_CTYPE=&quot; innan du kör AEM.

>[!NOTE]
>
**Inaktiverar SELinux:** Image Serving fungerar inte med SELinux aktiverat. Det här alternativet är aktiverat som standard. Du kan åtgärda problemet genom att redigera **/etc/selinux/config** och ändra SELinux-värdet från:
>
`SELINUX=enforcing` **till** `SELINUX=disabled`

>[!NOTE]
>
**NUMA-arkitektur:** System med processorer med AMD64 och Intel® EM64T är vanligtvis konfigurerade som icke-enhetliga minnesarkitekturplattformar (NUMA). Det innebär att kärnan konstruerar flera minnesnoder vid start i stället för att konstruera en enda minnesnod.
>
Konstruktionen för flera noder kan resultera i minnesöverbelastning på en eller flera av noderna innan andra noder töms. När minnet är uttömt kan kärnan välja att döda processer (till exempel Image Server eller Platform Server) trots att det finns tillgängligt minne.
>
Därför rekommenderar Adobe att du, om du kör ett sådant system, stänger av NUMA med startalternativet **numa=off** för att undvika att kärnan dödar dessa processer.

>[!NOTE]
>
**Servervärdnamnet måste matchas:** Kontrollera att serverns värdnamn kan matchas mot en IP-adress. Om det inte är möjligt, lägg till det fullständigt kvalificerade värdnamnet och IP-adressen till **/etc/hosts**:
>
`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft® Windows Server 2016
* Växla utrymme motsvarande minst dubbelt så mycket fysiskt minne (RAM)

Installera Microsoft® Visual Studio 2010, 2013 och 2015 som kan distribueras om för x64 och x86 om du vill använda Dynamic Media i Windows.

För Windows x64:

* Få Microsoft® Visual Studio 2010 återdistribuerbart på [https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/en-us/download/details.aspx?id=26999)
* Få Microsoft® Visual Studio 2013 återdistribuerbart på [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)
* Få Microsoft® Visual Studio 2015 återdistribuerbart på [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

För Windows x86:

* Få Microsoft® Visual Studio 2010 återdistribuerbart på [https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/en-us/download/details.aspx?id=26999)
* Få Microsoft® Visual Studio 2013 återdistribuerbart på [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* Få Microsoft® Visual Studio 2015 återdistribuerbart på [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)

#### macOS {#macos}

* 10.9.x och senare
* Stöds endast i demos- och testversioner

### Krav för AEM Forms PDF Generator {#requirements-for-aem-forms-pdf-generator}

### Programsupport för PDF Generator {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>Produkt</strong></p> </th>
   <th><p><strong>Format som stöds för konvertering till PDF</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2020 Classic track</a> senaste versionen</td>
   <td>XPS, bildformat (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF och DWF</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 klassiskt spår</a> senaste versionen (föråldrad)</td>
   <td>XPS, bildformat (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF och DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2019</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF och TXT</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016 (föråldrad)</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF och TXT</td>
  </tr>
  <tr>
   <td>WordPerfect 2020<br /> </td>
   <td>WP, WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016 (inaktuellt)<br /> </td>
   <td>VSD, VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2019<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016 (utgått)<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Project 2016 (föråldrad)<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.10</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, bildformat (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF och TXT</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2 (inaktuellt)</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, bildformat (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF och TXT</td>
  </tr>  
 </tbody>
</table>

>[!NOTE]
>
PDF Generator har endast stöd för engelska, franska, tyska och japanska versioner av de operativsystem och program som stöds.
>
Dessutom
>
* PDF Generator kräver en 32-bitarsversion av [Acrobat 2020 classic track version 20.004.30006](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) eller Acrobat 2017 version 17.011.30078 för att utföra konverteringen.
* PDF Generator-konverteringar för OpenOffice stöds bara i Windows och Linux®.
* PDF Generator har endast stöd för 32-bitarsversionen av Microsoft® Office Professional Plus och andra program som krävs för konvertering i Windows.
* PDF Generator stöder 32- och 64-bitarsversionerna av OpenOffice i Linux®.
* PDF Generator stöder inte Microsoft® Office 365.
* Funktionerna OCR PDF, Optimize PDF och Export PDF stöds endast i Windows.
* En version av Acrobat medföljer AEM Forms för att aktivera PDF Generator. Programmatiskt få tillgång till den paketerade versionen endast med AEM Forms, under AEM Forms-licensens löptid, för användning med AEM Forms PDF Generator. Mer information finns i AEM Forms produktbeskrivning för din distribution ([Lokal](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) eller [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))
* Tjänsten PDF Generator stöder inte Microsoft® Windows 10.
* PDF Generator kan inte konvertera filer med Microsoft® Visio 2019. Du kan fortsätta använda Microsoft® Visio 2016 för att konvertera `.VSD` och `.VSDX` filer.
* PDF Generator kan inte konvertera filer med Microsoft® Project 2019. Du kan fortsätta använda Microsoft® Project 2016 för att konvertera `.VSD` och `.VSDX` filer.
>

### Krav för AEM Forms Designer {#requirements-for-aem-forms-designer}

* Microsoft Windows 2016 Server, Microsoft Windows 2019 Server eller Microsoft®®® Windows®®® 10
* 1 GHz eller snabbare processor med stöd för PAE, NX och SSE2.
* 1 GB RAM för 32-bitars eller 2 GB RAM för 64-bitars operativsystem
* 16 GB diskutrymme för 32-bitars eller 20 GB för 64-bitars operativsystem
* Grafikminne - 128 MB GPU (256 MB rekommenderas)
* 2,35 GB ledigt hårddiskutrymme
* Bildskärmsupplösning på 1 024 x 768 pixlar eller högre
* Maskinvaruacceleration för video (valfritt)
* Acrobat Pro DC, Acrobat Standard DC eller Adobe Acrobat Reader DC
* Administrativ behörighet för att installera Designer
* Microsoft Visual C++ 2019 (VC 14.28 eller senare) 32-bitars runtime

### Krav för AEM Assets XMP metadata write-back {#requirements-for-aem-assets-xmp-metadata-write-back}

XMP stöds och är aktiverat för följande plattformar och filformat:

* **Operativsystem:**

   * Linux® (stöd för 32-bitars och 32-bitars program i 64-bitarssystem). Anvisningar om hur du installerar 32-bitars klientbibliotek finns i [Möjliggör extrahering och återskrivning XMP 64-bitars Red Hat® Linux®](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).

   * Windows Server
   * macOS X (64 bitar)

* **Filformat**: JPEG, PNG, TIFF, PDF, INDD, AI och EPS.

### Krav för AEM Assets att bearbeta metadataintensiva resurser i Linux® {#assetsonlinux}

XMPFilesProcessor-processen kräver att biblioteket GLIBC_2.14 fungerar. Använd en Linux®-kärna som innehåller GLIBC_2.14, till exempel Linux®-kärna version 3.1.x. Prestandan för bearbetning av resurser som innehåller en stor mängd metadata förbättras, till exempel PSD-filer. Om du använder en tidigare version av GLIBC uppstår fel i loggar som börjar med `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`.
