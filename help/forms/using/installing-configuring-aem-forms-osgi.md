---
title: Installera och konfigurera datainhämtningsfunktioner
seo-title: Install and configure data capture capabilities
description: Installera och konfigurera adaptiva formulär, PDF forms och HTML5 Forms. Konfigurera Adobe Analytics och Adobe Target för adaptiva formulär för att analysera användningen av formulär och målanvändare utifrån deras profil.
seo-description: Install and configure adaptive forms, PDF Forms, and HTML5 Forms. Configure Adobe Analytics and Adobe Target for adaptive forms to analyze usage of forms and target users based on their profile.
uuid: 5d49032a-4dea-4f21-9dad-a7a30c5872ea
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dfc473eb-6091-4f5d-a5a0-789972c513a9
docset: aem65
role: Admin
exl-id: 19b5765e-50bc-4fed-8af5-f6bb464516c8
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1864'
ht-degree: 0%

---

# Installera och konfigurera datainhämtningsfunktioner{#install-and-configure-data-capture-capabilities}

## Introduktion {#introduction}

AEM Forms tillhandahåller en uppsättning formulär för att hämta data från slutanvändaren: adaptiva formulär, HTML5 Forms och PDF forms. Det innehåller även verktyg för att lista alla tillgängliga formulär på en webbsida, analysera formuläranvändningen och för att identifiera målanvändare utifrån deras profil. Dessa funktioner ingår i AEM Forms tilläggspaket. Tilläggspaketet distribueras på en Author- eller Publish-instans av AEM.

**Adaptiva former:** Dessa formulär ändrar utseende baserat på enhetens skärmstorlek, är engagerande och interaktiva till sin natur. Adaptiv Forms kan även integreras med Adobe Analytics, Adobe Sign och Adobe Target. Ni kunde leverera personaliserade formulär och processorienterade upplevelser till användarna baserat på deras demografi och andra funktioner. Man kan också integrera adaptiva blanketter med Adobe Sign.

**PDF forms** är lämpliga för pixelperfekt utskrift och digital informationsinhämtning i ett PDF-dokument. I den digitala avataren kan du använda Adobe Acrobat eller Acrobat Reader för att fylla i dessa formulär. Du kan lägga upp dessa formulär på din webbplats eller använda formulärportalen för att lista dem på en AEM webbplats. Du kan även skicka dessa formulär till andra som bilagor. De här formulären passar bäst för skrivbordsmiljöer.

**HTML5 Forms** är en webbläsarvänlig version av PDF forms. HTML5 Forms passar för miljöer som inte stöder plugin-program för PDF. HTML5 Forms möjliggör återgivning av XFA-baserade formulär på mobila enheter och webbläsare på stationära datorer där XFA-baserad PDF inte stöds. Dessa formulär passar bäst för surfplattor och datorer.

AEM Forms är en kraftfull plattform i företagsklass och datainhämtning (adaptiva formulär, PDF forms och HTML5 Forms) är bara en av AEM Forms funktioner. En fullständig lista över funktioner finns på [Introduktion till AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Distributionstopologi {#deployment-topology}

AEM Forms tilläggspaket är ett program som distribueras till AEM. Du behöver bara minst en AEM Author och AEM Publish-instans för att kunna köra AEM Forms datainhämtningsfunktioner. Följande topologi rekommenderas för att köra AEM Forms AEM Forms datainsamlingsfunktioner. Mer information om topologin finns i [Arkitektur och driftsättningstopologier för AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![rekommenderad topologi](assets/recommended-topology.png)

## Systemkrav {#system-requirements}

Innan du börjar installera och konfigurera datainhämtningsfunktionen i AEM Forms måste du se till att:

* Maskinvaru- och programvaruinfrastruktur finns på plats. En detaljerad lista över maskin- och programvara som stöds finns på [tekniska krav](/help/sites-deploying/technical-requirements.md).

* Installationssökvägen för AEM-instansen innehåller inte blanksteg.
* En AEM-instans körs. För Windows-användare måste du installera AEM i förhöjt läge. I AEM är &quot;instance&quot; en kopia av AEM som körs på en server i författar- eller publiceringsläge. Du behöver minst två [AEM (en författare och en publicering)](/help/sites-deploying/deploy.md) för att köra AEM Forms datainhämtningsfunktioner:

   * **Upphovsman**: En AEM som används för att skapa, överföra och redigera innehåll och för att administrera webbplatsen. När innehållet är klart att publiceras replikeras det till publiceringsinstansen.
   * **Publicera**: En AEM instans som skickar det publicerade innehållet till allmänheten via internet eller ett internt nätverk.

* Minneskraven är uppfyllda. AEM Forms tilläggspaket kräver:

   * 15 GB temporärt utrymme för Microsoft Windows-baserade installationer.
   * 6 GB temporärt utrymme för UNIX-baserade installationer.

* Replikering och omvänd replikering har angetts för författaren och publiceringsinstanserna. Mer information finns i [Replikering](/help/sites-deploying/replication.md).
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

* Installera [Microsoft Visual Studio 2019 32-bitars Redistributable](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170).


## Installera AEM Forms-tilläggspaket {#install-aem-forms-add-on-package}

AEM Forms tilläggspaket är ett program som distribueras till AEM. Paketet innehåller AEM Forms datainhämtning och andra funktioner. Så här installerar du tilläggspaketet:

1. Öppna [Programvarudistribution](https://experience.adobe.com/downloads). Du behöver en Adobe ID för att logga in på Software Distribution.
1. Tryck **[!UICONTROL Adobe Experience Manager]** finns i rubrikmenyn.
1. I **[!UICONTROL Filters]** avsnitt:
   1. Välj **[!UICONTROL Forms]** från **[!UICONTROL Solution]** listruta.
   2. Välj version och typ för paketet. Du kan också använda **[!UICONTROL Search Downloads]** för att filtrera resultaten.
1. Tryck på det paketnamn som gäller för ditt operativsystem och välj **[!UICONTROL Accept EULA Terms]** och trycka **[!UICONTROL Download]**.
1. Öppna [Pakethanteraren](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  och klicka **[!UICONTROL Upload Package]** för att överföra paketet.
1. Markera paketet och klicka på **[!UICONTROL Install]**.

   Du kan även hämta paketet via länken direkt i [AEM Forms-versioner](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) artikel.
1. När paketet har installerats uppmanas du att starta om AEM. **Starta inte om servern omedelbart.** Innan du stoppar AEM Forms-servern väntar du tills meddelandena ServiceEvent REGISTERED och ServiceEvent UNREGISTERED inte visas i `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` och loggen är stabil.
1. Upprepa steg 1-7 för alla författare- och publiceringsinstanser.

### (Endast Windows) Automatisk installation av Visual Studio-omdistribuerbara filer {#automatic-installation-visual-studio-redistributables}

Om du installerar en AEM i förhöjt läge installeras 32-bitars visuella Studio-omdistribuerbara automatiskt under installationen av AEM Forms tilläggspaket.

Om du vill utvärdera om Visual Studio-omdistribuerbara filer installeras automatiskt öppnar du `error.log` filen finns på `/crx-repository/logs/` katalog. Loggarna innehåller följande meddelande:

`Redist <service name> already installed on system, will not attempt re-installation`

Om omdistributables inte kan installeras innehåller loggarna följande meddelande:

`Current user does not have elevated privileges, aborting installation of redist <service name>`

Du löser problemet genom att starta om AEM, installera AEM i förhöjt läge och sedan installera AEM Forms tilläggspaket.

Om behörighetskontrollen misslyckas innehåller loggarna följande meddelande:

`Privilege escalation check failed with error: <error message>`

## Konfiguration efter installation {#post-installation-configurations}

AEM Forms har några obligatoriska och valfria konfigurationer. De obligatoriska konfigurationerna är bland annat att konfigurera BouncyCastle-bibliotek och serialiseringsagent. De valfria konfigurationerna är bland annat att konfigurera dispatcher, Forms-portalen, Adobe Sign, Adobe Analytics och Adobe Target.

### Obligatoriska konfigurationer efter installation {#mandatory-post-installation-configurations}

#### Konfigurera RSA- och BouncyCastle-bibliotek  {#configure-rsa-and-bouncycastle-libraries}

Utför följande steg på alla författare- och publiceringsinstanser för att starta delegeringen av biblioteken:

1. Stoppa den underliggande AEM.
1. Öppna `[AEM installation directory]\crx-quickstart\conf\sling.properties` fil för redigering.

   Om du använt `[AEM installation directory]\crx-quickstart\bin\start.bat` för att starta AEM och sedan redigera sling.properties som finns på `[AEM_root]\crx-quickstart\`.

1. Lägg till följande egenskaper i filen sling.properties:

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. Spara och stäng filen och starta AEM.
1. Upprepa steg 1-4 för alla författarinstanser och publiceringsinstanser.

#### Konfigurera serialiseringsagenten {#configure-the-serialization-agent}

Utför följande steg på alla Author- och Publish-instanser för att lägga till paketet i tillåtelselista:

1. Öppna AEM Configuration Manager i ett webbläsarfönster. Standardwebbadressen är `https://'[server]:[port]'/system/console/configMgr`.
1. Sök efter **com.adobe.cq.deserfw.impl.DeserializationFirewallImpl.name** och öppna konfigurationen.
1. Lägg till **sun.util.calendar** till **tillåtelselista** fält. Klicka **Spara**.
1. Upprepa steg 1-3 för alla författarinstanser och publiceringsinstanser.

### Ytterligare konfigurationer efter installation {#optional-post-installation-configurations}

#### Konfigurera Dispatcher {#configure-dispatcher}

Dispatcher är ett Adobe Experience Manager verktyg för cachelagring och/eller belastningsutjämning som kan användas tillsammans med en webbserver i företagsklass. Om du [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)och sedan utföra följande konfigurationer för AEM Forms:

1. Konfigurera åtkomst för AEM Forms:

   Öppna filen dispatcher.any för redigering. Navigera till filteravsnittet och lägg till följande filter i filteravsnittet:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Spara och stäng filen. Mer information om filter finns i [Dispatcher-dokumentation](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Konfigurera tjänsten för refererarfilter:

   Logga in som administratör i konfigurationshanteraren för Apache Felix. Konfigurationshanterarens standardwebbadress är `https://[server]:[port_number]/system/console/configMgr`. I **Konfigurationer** väljer du **Apache Sling Referer-filter** alternativ. I fältet Tillåt värdar anger du avsändarens värdnamn för att tillåta det som referent och klickar på **Spara**. Formatet på posten är `https://[server]:[port]`.

#### Konfigurera cache {#configure-cache}

Cachelagring är en mekanism som förkortar dataåtkomsttider, minskar fördröjningen och förbättrar in-/utdatahastigheter (I/O). Cacheminnet för adaptiva formulär lagrar endast HTML-innehåll och JSON-struktur i ett adaptivt formulär utan att några förfyllda data sparas. Det minskar tiden som krävs för att återge ett anpassat formulär.

* När du använder cacheminnet för anpassade formulär använder du [AEM](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) för att cachelagra klientbibliotek (CSS och JavaScript) för ett adaptivt formulär.
* När du utvecklar anpassade komponenter bör du se till att cachen för anpassade formulär är inaktiverad på servern som används för utveckling.

Utför följande steg för att konfigurera cachen för adaptiva formulär:

1. Gå till konfigurationshanteraren AEM webbkonsolen på https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Klicka **Konfiguration av webbkanal för adaptiv form och interaktiv kommunikation** om du vill redigera dess konfigurationsvärden. I dialogrutan Redigera konfigurationsvärden anger du det maximala antalet formulär eller dokument som en instans av AEM Forms-servern kan cachelagra i dialogrutan Redigera konfigurationsvärden **Antal adaptiva Forms** fält. Standardvärdet är 100. Klicka **Spara**.

   >[!NOTE]
   >
   >Om du vill inaktivera cachen anger du värdet i fältet Antal adaptiva Forms till **0**. Cacheminnet återställs och alla formulär och dokument tas bort från cacheminnet när du inaktiverar eller ändrar cachekonfigurationen.

#### Konfigurera SSL-kommunikation för formulärdatamodell {#configure-ssl-communcation-for-form-data-model}

Du kan aktivera SSL-kommunikation för formulärdatamodellen. Om du vill aktivera SSL-kommunikation för formulärdatamodellen ska du lägga till certifikat i Java Trust Store för alla instanser innan du startar en AEM Forms-instans. Du kan köra följande kommando för att lägga till certifikaten: &quot;

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### Konfigurera Adobe Sign {#configure-adobe-sign}

Adobe Sign möjliggör e-signaturarbetsflöden för anpassningsbara formulär. E-signaturer förbättrar arbetsflödena för att bearbeta dokument inom juridik, försäljning, löneadministration, personaladministration och många andra områden.

I ett typiskt Adobe Sign och anpassningsbara formulär fyller en användare i ett anpassat formulär för att **ansöka om en tjänst**. Till exempel kan en kreditkortsansökan och en medborgare få förmåner. När en användare fyller i, skickar och signerar ansökningsformuläret skickas formuläret till tjänsteleverantören för ytterligare åtgärder. Tjänsteleverantören granskar programmet och använder Adobe Sign för att markera det som godkänt. För att möjliggöra liknande arbetsflöden för elektroniska signaturer kan du integrera Adobe Sign med AEM Forms.

Om du vill använda Adobe Sign med AEM Forms [Integrera Adobe Sign med AEM Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md).

#### Konfigurera Adobe Analytics {#configure-adobe-analytics}

AEM Forms kan integreras med Adobe Analytics så att ni kan hämta in och spåra prestandamått för era publicerade formulär och dokument. Syftet med att analysera dessa värden är att fatta välgrundade beslut baserat på uppgifter om de ändringar som krävs för att göra formulär eller dokument mer användbara.

Information om hur du använder Adobe Analytics med AEM Forms finns i [Konfigurera analyser och rapporter](/help/forms/using/configure-analytics-forms-documents.md).

#### Integrera Adobe Target {#integrate-adobe-target}

Kunderna överger troligtvis ett formulär om upplevelsen inte är engagerande. Även om det är frustrerande för kunderna kan det också öka supportvolymen och kostnaderna för organisationen. Det är viktigt och utmanande att identifiera och tillhandahålla rätt kundupplevelse som ökar konverteringsgraden. AEM innehåller nyckeln till detta problem.

AEM kan integreras med Adobe Target, en Adobe Marketing Cloud-lösning, för att leverera personaliserade och engagerande kundupplevelser i flera digitala kanaler. Om du vill använda Adobe Target för att A/B-testa adaptiva formulär [Integrera Adobe Target med AEM Forms](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

## Nästa steg {#next-steps}

Du har konfigurerat en miljö för att använda AEM Forms datainsamlingsfunktioner. Nästa steg mot att använda funktionen är:

* [Skapa ditt första anpassningsbara formulär](/help/forms/using/create-your-first-adaptive-form.md)
* [Skapa ditt första PDF-formulär](https://www.adobe.com/go/learn_aemforms_designer_quick_start_65)
* [Introduktion till HTML5 Forms](/help/forms/using/introduction.md)
