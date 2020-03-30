---
title: Installera och konfigurera datainhämtningsfunktioner
seo-title: Installera och konfigurera datainhämtningsfunktioner
description: Installera och konfigurera adaptiva formulär, PDF-formulär och HTML5-formulär. Konfigurera Adobe Analytics och Adobe Target för adaptiva formulär för att analysera användningen av formulär och målanvändare utifrån deras profil.
seo-description: Installera och konfigurera adaptiva formulär, PDF-formulär och HTML5-formulär. Konfigurera Adobe Analytics och Adobe Target för adaptiva formulär för att analysera användningen av formulär och målanvändare utifrån deras profil.
uuid: 5d49032a-4dea-4f21-9dad-a7a30c5872ea
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dfc473eb-6091-4f5d-a5a0-789972c513a9
docset: aem65
translation-type: tm+mt
source-git-commit: f323b490c37effc3cbb36c793b62fa788eca9545

---


# Installera och konfigurera datainhämtningsfunktioner{#install-and-configure-data-capture-capabilities}

## Introduktion {#introduction}

AEM Forms innehåller en uppsättning formulär för att hämta data från slutanvändaren: adaptiva formulär, HTML5-formulär och PDF-formulär. Det innehåller även verktyg för att lista alla tillgängliga formulär på en webbsida, analysera formuläranvändningen och för att identifiera målanvändare utifrån deras profil. Dessa funktioner ingår i tilläggspaketet AEM Forms. Tilläggspaketet distribueras på en Author- eller Publish-instans av AEM.

**Adaptiva former:** Dessa formulär ändrar utseende baserat på enhetens skärmstorlek, är engagerande och interaktiva till sin natur. Adaptiva formulär kan även integreras med Adobe Analytics, Adobe Sign och Adobe Target. Ni kunde leverera personaliserade formulär och processorienterade upplevelser till användarna baserat på deras demografi och andra funktioner. Du kan även integrera adaptiva formulär med Adobe Sign.

**PDF-formulär** är lämpliga för utskrift på pixelnivå och digital information som samlas in i ett PDF-dokument. I den digitala avataren kan du använda Adobe Acrobat eller Acrobat Reader för att fylla i dessa formulär. Du kan lägga upp dessa formulär på din webbplats eller använda formulärportalen för att lista dem på en AEM-webbplats. Du kan även skicka dessa formulär till andra som bilagor. De här formulären passar bäst för skrivbordsmiljöer.

**HTML5-formulär** är den webbläsarvänliga versionen av PDF-formulär. HTML5-formulär är lämpliga för miljöer som inte stöder PDF-plugin-program. HTML5-formulär möjliggör återgivning av XFA-baserade formulär på mobila enheter och webbläsare på datorer där XFA-baserad PDF inte stöds. Dessa formulär passar bäst för surfplattor och datorer.

AEM Forms är en kraftfull plattform i företagsklass och datainhämtning (adaptiva formulär, PDF-formulär och HTML5-formulär) är bara en av funktionerna i AEM Forms. En fullständig lista över funktioner finns i [Introduktion till AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Distributionstopologi {#deployment-topology}

AEM Forms-tilläggspaketet är ett program som distribueras till AEM. Du behöver bara minst en AEM Author- och AEM Publish-instans för att kunna köra datainhämtningsfunktionerna i AEM Forms. Följande topologi rekommenderas för att köra datainsamlingsfunktionerna i AEM Forms AEM Forms. Mer information om topologin finns i [Arkitektur och distributionstopologier för AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![rekommenderad topologi](assets/recommended-topology.png)

## Systemkrav {#system-requirements}

Innan du börjar installera och konfigurera funktioner för datainhämtning i AEM Forms bör du kontrollera att:

* Maskinvaru- och programvaruinfrastruktur finns på plats. En detaljerad lista över maskin- och programvara som stöds finns i [tekniska krav](/help/sites-deploying/technical-requirements.md).

* Installationssökvägen för AEM-instansen innehåller inte blanksteg.
* En AEM-instans körs. I AEM-terminologi är &quot;instance&quot; en kopia av AEM som körs på en server i författar- eller publiceringsläge. Du måste ha minst två [AEM-instanser (en författare och en publicering)](/help/sites-deploying/deploy.md) för att kunna köra datainhämtningsfunktionerna i AEM Forms:

   * **Författare**: En AEM-instans som används för att skapa, överföra och redigera innehåll och för att administrera webbplatsen. När innehållet är klart att publiceras replikeras det till publiceringsinstansen.
   * **Publicera**: En AEM-instans som skickar det publicerade innehållet till allmänheten via internet eller ett internt nätverk.

* Minneskraven uppfylls. AEM Forms-tilläggspaket kräver:

   * 15 GB temporärt utrymme för Microsoft Windows-baserade installationer.
   * 6 GB temporärt utrymme för UNIX-baserade installationer.

* Replikering och omvänd replikering har angetts för författaren och publiceringsinstanserna. For details, see [Replication](/help/sites-deploying/replication.md).
* För UNIX-baserade system:

   * Installera följande 32-bitarspaket från installationsmediet:

<table>
 <tbody>
  <tr>
   <td>exponat</td>
   <td>fontconfig</td>
   <td>freetype</td>
   <td>glibc</td>
  </tr>
  <tr>
   <td>libcurl</td>
   <td>libICE</td>
   <td>libicu</td>
   <td>libSM</td>
  </tr>
  <tr>
   <td>libuuid</td>
   <td>libX11</td>
   <td><p>libXau</p> </td>
   <td>libxcb</td>
  </tr>
  <tr>
   <td>libXext</td>
   <td>libXinerama</td>
   <td>libXrandr</td>
   <td>libXrender</td>
  </tr>
  <tr>
   <td>nss-softokn-free-bl</td>
   <td>OpenSSL</td>
   <td>zlib</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Om OpenSSL redan är installerat på servern uppgraderar du det till den senaste versionen.
>* Skapa symbolerna libcurl.so, libcrypto.so och libssl.so som pekar på den senaste versionen av biblioteken libcurl, libcrypto och libssl.
>



* Installera följande 64-bitarspaket från installationsmediet:

   * libicu

## Installera AEM Forms-tilläggspaket {#install-aem-forms-add-on-package}

AEM Forms-tilläggspaketet är ett program som distribueras till AEM. Paketet innehåller datainhämtning från AEM Forms och andra funktioner. Så här installerar du tilläggspaketet:

1. Logga in på [AEM-servern](https://localhost:4502) som administratör och öppna [paketresursen](https://localhost:4502/crx/packageshare). Du måste ha ett Adobe-id för att kunna logga in på paketresursen.
1. I [AEM-paketresursen](https://localhost:4502/crx/packageshare/login.html)söker du i tilläggspaket **för** AEM 6.5-formulär, klickar på det paket som gäller för ditt operativsystem och klickar på **Hämta**. Läs och godkänn licensavtalet och klicka på **OK**. Nedladdningen startar. När du har hämtat **visas ordet Hämtad** bredvid paketet.

   Du kan också använda versionsnumret för att söka efter ett tilläggspaket. Versionsnummer för det senaste paketet finns i artikeln om [AEM Forms-versioner](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) .

1. När nedladdningen är klar klickar du på **Nedladdad**. Du omdirigeras till pakethanteraren. I pakethanteraren söker du efter det hämtade paketet och klickar på **Installera**.

   Om du hämtar paketet manuellt via den direktlänk som visas i artikeln [AEM Forms Relases](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) loggar du in på pakethanteraren, klickar på **Överför paket**, markerar det hämtade paketet och klickar på Överför. När paketet har överförts klickar du på paketnamnet och sedan på **Installera.**

1. När paketet har installerats uppmanas du att starta om AEM-instansen. **Starta inte om servern omedelbart.** Innan du stoppar AEM Forms-servern väntar du tills ServiceEvent REGISTERED- och ServiceEvent UNREGISTERED-meddelandena inte längre visas i `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` filen och loggen är stabil.
1. Upprepa steg 1-4 för alla författarinstanser och publiceringsinstanser.

## Konfiguration efter installation {#post-installation-configurations}

AEM Forms har några obligatoriska och valfria konfigurationer. De obligatoriska konfigurationerna är bland annat att konfigurera BouncyCastle-bibliotek och serialiseringsagent. De valfria konfigurationerna är bland annat att konfigurera dispatcher, Forms-portalen, Adobe Sign, Adobe Analytics och Adobe Target.

### Obligatoriska efterinstallationskonfigurationer {#mandatory-post-installation-configurations}

#### Konfigurera RSA- och BouncyCastle-bibliotek {#configure-rsa-and-bouncycastle-libraries}

Utför följande steg på alla författare- och publiceringsinstanser för att starta delegeringen av biblioteken:

1. Stoppa den underliggande AEM-instansen.
1. Öppna `[AEM installation directory]\crx-quickstart\conf\sling.properties` filen för redigering.

   Om du använde `[AEM installation directory]\crx-quickstart\bin\start.bat` för att starta AEM redigerar du sling.properties som finns på `[AEM_root]\crx-quickstart\`.

1. Lägg till följande egenskaper i filen sling.properties:

   ```
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. Spara och stäng filen och starta AEM-instansen.
1. Upprepa steg 1-4 för alla författarinstanser och publiceringsinstanser.

#### Konfigurera serialiseringsagenten {#configure-the-serialization-agent}

Utför följande steg på alla Author- och Publish-instanser för att vitlista paketet:

1. Öppna AEM Configuration Manager i ett webbläsarfönster. Standardwebbadressen är `https://'[server]:[port]'/system/console/configMgr`.
1. Sök efter **com.adobe.cq.deserfw.impl.DeserializationFirewallImpl.name** och öppna konfigurationen.
1. Lägg till paketet **sun.util.calendar** i **vitlistefältet** . Click **Save**.
1. Upprepa steg 1-3 för alla författarinstanser och publiceringsinstanser.

### Ytterligare konfigurationer efter installation {#optional-post-installation-configurations}

#### Konfigurera Dispatcher {#configure-dispatcher}

Dispatcher är ett verktyg för cachelagring och lastbalansering för AEM. AEM Dispatcher skyddar även AEM-servern mot attacker. Du kan öka säkerheten för din AEM-instans genom att använda Dispatcher tillsammans med en webbserver i företagsklass. Om du använder [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)gör du följande konfigurationer för AEM Forms:

1. Konfigurera åtkomst för AEM Forms:

   Öppna filen dispatcher.any för redigering. Navigera till filteravsnittet och lägg till följande filter i filteravsnittet:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Spara och stäng filen. Mer information om filter finns i [Dispatcher-dokumentationen](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Konfigurera tjänsten för refererarfilter:

   Logga in som administratör i konfigurationshanteraren för Apache Felix. Konfigurationshanterarens standardwebbadress är `https://[server]:[port_number]/system/console/configMgr`. På menyn **Konfigurationer** väljer du alternativet **Apache Sling Reference Filter** . I fältet Tillåt värdar anger du värdnamnet för dispatchern så att den kan användas som referent och klickar på **Spara**. Posten har formatet &quot;https://[server]:[port]&quot;.

#### Konfigurera cache {#configure-cache}

Cachelagring är en mekanism som förkortar dataåtkomsttider, minskar fördröjningen och förbättrar in-/utdatahastigheter (I/O). Cacheminnet för adaptiva formulär lagrar endast HTML-innehåll och JSON-strukturen i ett adaptivt formulär utan att några förfyllda data sparas. Det minskar tiden som krävs för att återge ett anpassat formulär.

* När du använder cacheminnet för adaptiva formulär använder du [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) för att cachelagra klientbibliotek (CSS och JavaScript) för ett adaptivt formulär.
* När du utvecklar anpassade komponenter bör du se till att cachen för anpassade formulär är inaktiverad på servern som används för utveckling.

Utför följande steg för att konfigurera cachen för adaptiva formulär:

1. Gå till konfigurationshanteraren för AEM-webbkonsolen på https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Klicka på **Adaptiv form och Interactive Communication Web Channel Configuration** för att redigera dess konfigurationsvärden. I dialogrutan Redigera konfigurationsvärden anger du det maximala antalet formulär eller dokument som en instans av AEM Forms-servern kan cachelagra i fältet **Antal adaptiva formulär** . Standardvärdet är 100. Click **Save**.

   >[!NOTE]
   >
   >Om du vill inaktivera cachen anger du värdet **0** i fältet Antal adaptiva formulär. Cacheminnet återställs och alla formulär och dokument tas bort från cacheminnet när du inaktiverar eller ändrar cachekonfigurationen.

#### Konfigurera SSL-kommunikation för formulärdatamodell {#configure-ssl-communcation-for-form-data-model}

Du kan aktivera SSL-kommunikation för formulärdatamodellen. Om du vill aktivera SSL-kommunikation för formulärdatamodellen ska du lägga till certifikat i Java Trust Store för alla instanser innan du startar en AEM Forms-instans. Du kan köra följande kommando för att lägga till certifikaten: &quot;

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### Konfigurera Adobe Sign {#configure-adobe-sign}

Adobe Sign möjliggör e-signaturarbetsflöden för anpassningsbara formulär. E-signaturer förbättrar arbetsflödena för att bearbeta dokument inom juridik, försäljning, löneadministration, personaladministration och många andra områden.

I ett typiskt Adobe Sign och anpassningsbara formulär fyller en användare i ett anpassat formulär som **ansöker om en tjänst**. Till exempel kan en kreditkortsansökan och en medborgare få förmåner. När en användare fyller i, skickar och signerar ansökningsformuläret skickas formuläret till tjänsteleverantören för ytterligare åtgärder. Tjänsteleverantören granskar programmet och använder Adobe Sign för att markera programmet som godkänt. Om du vill aktivera liknande arbetsflöden för elektroniska signaturer kan du integrera Adobe Sign med AEM Forms.

Om du vill använda Adobe Sign med AEM-formulär [integrerar du Adobe Sign med AEM-formulär](/help/forms/using/adobe-sign-integration-adaptive-forms.md).

#### Konfigurera Adobe Analytics {#configure-adobe-analytics}

AEM Forms kan integreras med Adobe Analytics så att ni kan hämta in och spåra prestandamått för era publicerade formulär och dokument. Syftet med att analysera dessa värden är att fatta välgrundade beslut baserat på uppgifter om de ändringar som krävs för att göra formulär eller dokument mer användbara.

Information om hur du använder Adobe Analytics med AEM Forms finns i [Konfigurera analyser och rapporter](/help/forms/using/configure-analytics-forms-documents.md).

#### Integrera Adobe Target {#integrate-adobe-target}

Kunderna överger troligtvis ett formulär om upplevelsen inte är engagerande. Även om det är frustrerande för kunderna kan det också öka supportvolymen och kostnaderna för organisationen. Det är både viktigt och utmanande att identifiera och tillhandahålla rätt kundupplevelse som ökar konverteringsgraden. AEM-formulär innehåller nyckeln till det här problemet.

AEM-formulär integreras med Adobe Target, en Adobe Marketing Cloud-lösning, för att leverera personaliserade och engagerande kundupplevelser i flera digitala kanaler. Om du vill använda Adobe Target till A/B-testformulär kan du [integrera Adobe Target med AEM Forms](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

## Nästa steg {#next-steps}

Du har konfigurerat en miljö för att använda funktionerna för datainhämtning i AEM Forms. Nästa steg mot att använda funktionen är:

* [Skapa ditt första anpassningsbara formulär](/help/forms/using/create-your-first-adaptive-form.md)
* [Skapa ditt första PDF-formulär](http://www.adobe.com/go/learn_aemforms_designer_quick_start_65)
* [Introduktion till HTML5-formulär](/help/forms/using/introduction.md)

