---
title: Installera och konfigurera interaktiv kommunikation
seo-title: Installera och konfigurera interaktiv kommunikation
description: Installera och konfigurera AEM Forms Interactive Communications för att skapa affärskommunikation, dokument, kontoutdrag, förmånsmeddelanden, marknadsföringsmejl, fakturor och välkomstpaket.
seo-description: Installera och konfigurera AEM Forms Interactive Communications för att skapa affärskommunikation, dokument, kontoutdrag, förmånsmeddelanden, marknadsföringsmejl, fakturor och välkomstpaket.
uuid: 8acb7f68-0b52-4acd-97e2-af31c9408e8d
topic-tags: installing
discoiquuid: 225f2bc1-6842-4c79-a66d-8024a29325c0
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Installera och konfigurera interaktiv kommunikation{#install-and-configure-interactive-communications}

## Introduktion {#introduction}

AEM Form kan centralisera framtagning, sammanställning, hantering och distribution av säkra och interaktiva dokument som affärskommunikation, dokument, kontoutdrag, förmånsmeddelanden, marknadsmeddelanden, räkningar och välkomstpaket. Den här funktionen kallas interaktiv kommunikation. Funktionen ingår i AEM Forms-tilläggspaketet. Tilläggspaketet distribueras på en Author- eller Publish-instans av AEM.

Du kan använda den interaktiva kommunikationsfunktionen för att producera kommunikation i flera format. Till exempel webb och PDF. Ni kan integrera interaktiv kommunikation med AEM Workflow för att bearbeta och leverera den sammanställda kommunikationen till kunderna via valfri kanal. Du kan till exempel skicka en kommunikation till slutanvändaren via e-post.

Om du uppgraderar från en tidigare version och redan har investerat i korrespondenshantering kan du installera [kompatibilitetspaketet](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package) för att fortsätta använda korrespondenshantering. Mer information om skillnaderna mellan interaktiv kommunikation och korrespondenshantering finns i Översikt över [interaktiv kommunikation](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management).

AEM Forms är en kraftfull plattform i företagsklass. Interaktiv kommunikation är bara en av funktionerna i AEM Forms. En fullständig lista över funktioner finns i [Introduktion till AEM Forms](../../forms/using/introduction-aem-forms.md).

## Distributionstopologi {#deployment-topology}

AEM Forms-tilläggspaketet är ett program som distribueras till AEM. Du behöver bara minst en instans av AEM Author och Processing för att kunna köra funktionen Interactive Communications. Följande topologi är en indikativ topologi för att köra AEM Forms Interactive Communications, Correspondence Management, AEM Forms data capture och Forms-Centric workflow på OSGi-funktioner. Mer information om topologin finns i [Arkitektur och distributionstopologier för AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![rekommenderad topologi](assets/recommended-topology.png)

AEM Forms Interactive Communications kör administratörs-, redigerings- och agentanvändargränssnitt på författarinstansen av AEM Forms. Publiceringsinstanserna är värdar för den slutliga versionen av interaktiv kommunikation som är klar att användas av slutanvändarna.

## Systemkrav {#system-requirements}

Innan du börjar installera och konfigurera funktioner för interaktiv kommunikation och korrespondenshantering i AEM Forms måste du se till att:

* Maskinvaru- och programvaruinfrastruktur finns på plats. En detaljerad lista över maskin- och programvara som stöds finns i [tekniska krav](/help/sites-deploying/technical-requirements.md).

* Installationssökvägen för AEM-instansen innehåller inte blanksteg.
* En AEM-instans körs. I AEM-terminologi är &quot;instance&quot; en kopia av AEM som körs på en server i författar- eller publiceringsläge. Du behöver minst en AEM-instans (Författare eller Bearbetning) för att köra AEM Forms-interaktiva funktioner för kommunikation och korrespondenshantering:

   * **Författare**: En AEM-instans som används för att skapa, överföra och redigera innehåll och för att administrera webbplatsen. När innehållet är klart att publiceras replikeras det till publiceringsinstansen.
   * **Bearbetar:** En bearbetningsinstans är en instans av en [AEM Author](/help/forms/using/hardening-securing-aem-forms-environment.md) . Du kan ställa in en Author-instans och göra den oskarp efter att du har utfört installationen.

   * **Publicera**: En AEM-instans som skickar det publicerade innehållet till allmänheten via Internet eller ett internt nätverk.

* Minneskraven uppfylls. AEM Forms-tilläggspaket kräver:

   * 15 GB temporärt utrymme för Microsoft Windows-baserade installationer.
   * 6 GB temporärt utrymme för UNIX-baserade installationer.

* Extra krav för UNIX-baserade system: Om du använder det UNIX-baserade operativsystemet installerar du följande paket från installationsmediet för respektive operativsystem.

<table>
 <tbody>
  <tr>
   <td>exponat</td>
   <td>libxcb</td>
   <td>freetype</td>
   <td>libXau</td>
  </tr>
  <tr>
   <td>libSM</td>
   <td>zlib</td>
   <td>libICE</td>
   <td>libuuid</td>
  </tr>
  <tr>
   <td>glibc</td>
   <td>libXext</td>
   <td><p>nss-softokn-free-bl</p> </td>
   <td>fontconfig</td>
  </tr>
  <tr>
   <td>libX11</td>
   <td>libXrender</td>
   <td>libXrandr</td>
   <td>libXinerama</td>
  </tr>
 </tbody>
</table>

## Installera AEM Forms-tilläggspaket {#install-aem-forms-add-on-package}

AEM Forms-tilläggspaketet är ett program som distribueras till AEM. Paketet innehåller interaktiv kommunikation med AEM Forms, korrespondenshantering och andra funktioner. Så här installerar du tilläggspaketet:

1. Logga in på [AEM-servern](https://localhost:4502) som administratör och öppna [paketresursen](https://localhost:4502/crx/packageshare). Du måste ha ett Adobe-id för att kunna logga in på paketresursen.
1. I [AEM-paketresursen](https://localhost:4502/crx/packageshare/login.html)söker du efter tilläggspaket **för** AEM 6.5-formulär eller **senaste servicepaket**, klickar på det paket som gäller för ditt operativsystem och klickar på **Hämta**. Läs och godkänn licensavtalet och klicka på **OK**. Nedladdningen startar. När du har hämtat **visas ordet Hämtad** bredvid paketet.

   Du kan också använda versionsnumret för att söka efter ett tilläggspaket. Versionsnummer för det senaste paketet finns i artikeln om [AEM Forms-versioner](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) .

1. När nedladdningen är klar klickar du på **Nedladdad**. Du omdirigeras till pakethanteraren. I pakethanteraren söker du efter det hämtade paketet och klickar på **Installera**.

   Om du hämtar paketet manuellt via den direktlänk som visas i artikeln [AEM Forms Relases](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) loggar du in på pakethanteraren, klickar på **Överför paket**, markerar det hämtade paketet och klickar på Överför. När paketet har överförts klickar du på paketnamnet och sedan på **Installera.**

1. När paketet har installerats uppmanas du att starta om AEM-instansen. **Starta inte om servern omedelbart.** Innan du stoppar AEM Forms-servern väntar du tills meddelandena ServiceEvent REGISTERED och ServiceEvent UNREGISTERED inte visas i filen [AEM-Installation-Directory]/crx-quickstart/logs/error.log och loggen är stabil.
1. Upprepa steg 1-4 för alla författarinstanser och publiceringsinstanser.

## Konfiguration efter installation {#post-installation-configurations}

AEM Forms har några obligatoriska och valfria konfigurationer. De obligatoriska konfigurationerna är bland annat att konfigurera BouncyCastle-bibliotek och serialiseringsagent. De valfria konfigurationerna är bland annat att konfigurera dispatcher och Adobe Target.

### Obligatoriska efterinstallationskonfigurationer {#mandatory-post-installation-configurations}

#### Konfigurera RSA- och BouncyCastle-bibliotek {#configure-rsa-and-bouncycastle-libraries}

Utför följande steg på alla författare- och publiceringsinstanser för att starta delegeringen av biblioteken:

1. Stoppa den underliggande AEM-instansen.
1. Öppna [AEM-installationskatalogen]\crx-quickstart\conf\sling.properties för redigering.

   Om du använde [installationskatalogen]för AEM \crx-quickstart\bin\start.bat för att starta AEM redigerar du sling.properties som finns på [AEM_root]\crx-quickstart\.

1. Lägg till följande egenskaper i filen sling.properties:

   ```
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. Spara och stäng filen och starta AEM-instansen.
1. Upprepa steg 1-4 för alla författarinstanser och publiceringsinstanser.

#### Konfigurera serialiseringsagenten {#configure-the-serialization-agent}

Utför följande steg på alla Author- och Publish-instanser för att vitlista paketet:

1. Öppna AEM Configuration Manager i ett webbläsarfönster. Standardwebbadressen är https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Sök efter och öppna **Brandväggskonfiguration** för deserialisering.
1. Lägg till paketet **sun.util.calendar** i **vitlistefältet** . Klicka på Spara.
1. Upprepa steg 1-3 för alla författare- och publiceringsinstanser.

### Ytterligare konfigurationer efter installation {#optional-post-installation-configurations}

#### Installera kompatibilitetspaket {#install-compatibility-package}

Interaktiv kommunikation är standardmetoden och rekommenderas för att skapa kundkommunikation i AEM 6.5-formulär. Om du har uppgraderat eller migrerat från en tidigare version och tänker fortsätta använda brev (Correspondence Management) installerar du [AEMFD-kompatibilitetspaketet](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-COMPAT).

Med AEMFD-kompatibilitetspaketet kan du använda följande resurser från AEM 6.4-formulär, AEM 6.3-formulär och AEM 6.2-formulär på AEM 6.5-formulär:

* Dokumentfragment
* Bokstäver
* Dataordlistor
* Mallar och sidor för anpassade formulär har tagits bort

#### Konfigurera Dispatcher {#configure-dispatcher}

Dispatcher är ett verktyg för cachelagring och lastbalansering för AEM. AEM Dispatcher skyddar även AEM-servern mot attacker. Du kan öka säkerheten för din AEM-instans genom att använda Dispatcher tillsammans med en webbserver i företagsklass. Om du använder [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)gör du följande konfigurationer för AEM Forms:

1. Konfigurera åtkomst för AEM Forms:

   Öppna filen dispatcher.any för redigering. Navigera till filteravsnittet och lägg till följande filter i filteravsnittet:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Spara och stäng filen. Mer information om filter finns i [Dispatcher-dokumentationen](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Konfigurera tjänsten för refererarfilter:

   Logga in som administratör i konfigurationshanteraren för Apache Felix. Konfigurationshanterarens standard-URL är https://&#39;server&#39;:[port_number]/system/console/configMgr. På menyn **Konfigurationer** väljer du alternativet **Apache Sling Reference Filter** . I fältet Tillåt värdar anger du värdnamnet för dispatchern så att den kan användas som referent och klickar på **Spara**. Posten har formatet https://&#39;[server]:[port]&#39;.

#### Integrera Adobe Target {#integrate-adobe-target}

Kunderna överger troligen interaktiv kommunikation om upplevelsen inte är engagerande. Även om det är frustrerande för kunderna kan det också öka supportvolymen och kostnaderna för organisationen. Det är viktigt och utmanande att identifiera och tillhandahålla rätt kundupplevelse som ökar konverteringsgraden. AEM-formulär innehåller nyckeln till det här problemet.

AEM-formulär integreras med Adobe Target, en Adobe Marketing Cloud-lösning, för att leverera personaliserade och engagerande kundupplevelser i flera digitala kanaler. Om du vill använda Adobe Target för att personalisera en interaktiv kommunikation [integrerar du Adobe Target med AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

#### Konfigurera SSL-kommunikation för formulärdatamodell {#configure-ssl-communcation-for-form-data-model}

Du kan aktivera SSL-kommunikation för formulärdatamodellen. Om du vill aktivera SSL-kommunikation för formulärdatamodellen ska du lägga till certifikat i Java Trust Store för alla instanser innan du startar en AEM Forms-instans. Du kan köra följande kommando för att lägga till certifikaten:

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## Nästa steg {#next-steps}

Du har konfigurerat en miljö för interaktiv kommunikation och korrespondenshantering. Stegen för att använda funktionen är nu:

* [Översikt över korrespondenshantering](/help/forms/using/interactive-communications-overview.md)

* [Skapa interaktiv kommunikation](../../forms/using/create-interactive-communication.md)

* [Skapa ett brev för korrespondenshantering](../../forms/using/create-letter.md)

