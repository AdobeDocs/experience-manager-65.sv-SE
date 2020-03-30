---
title: Installera och konfigurera formulärcentrerade arbetsflöden i OSGi
seo-title: Installera och konfigurera formulärcentrerade arbetsflöden i OSGi
description: Installera och konfigurera AEM Forms Interactive Communications för att skapa affärskommunikation, dokument, kontoutdrag, förmånsmeddelanden, marknadsföringsmejl, fakturor och välkomstpaket.
seo-description: Installera och konfigurera AEM Forms Interactive Communications för att skapa affärskommunikation, dokument, kontoutdrag, förmånsmeddelanden, marknadsföringsmejl, fakturor och välkomstpaket.
uuid: 1ceae822-215a-4b83-a562-4609a09c3a54
topic-tags: installing
discoiquuid: de292a19-07db-4ed3-b13a-7a2f1cd9e0dd
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Installera och konfigurera formulärcentrerade arbetsflöden i OSGi{#installing-and-configuring-forms-centric-workflow-on-osgi}

## Introduktion {#introduction}

Företag samlar in och bearbetar data från olika typer av formulär, bakomliggande system och andra datakällor. Bearbetningen av data innefattar rutiner för granskning och godkännande, repetitiva uppgifter och arkivering av data. Du kan till exempel granska ett formulär och konvertera det till ett PDF-dokument. När du gör det manuellt kan de repetitiva uppgifterna ta lång tid och ta lång tid och resurser.

Du kan använda [formulärbaserade arbetsflöden i OSGi](../../forms/using/aem-forms-workflow.md) för att snabbt skapa anpassningsbara formulärbaserade arbetsflöden. Dessa arbetsflöden kan hjälpa er att automatisera gransknings- och godkännandearbetsflöden, affärsprocessarbetsflöden och andra repetitiva uppgifter. De här arbetsflödena hjälper dig även att bearbeta dokument (skapa, sammanställa, distribuera och arkivera PDF-dokument, lägga till digitala signaturer för att begränsa tillgången till dokument, avkoda streckkodsformulär med mera) och använda arbetsflödet för Adobe Sign-signaturer med formulär och dokument.

När du väl har konfigurerat arbetsflödena kan de aktiveras manuellt för att slutföra en definierad process eller köras programmatiskt när användare skickar ett formulär eller en interaktiv kommunikation. Funktionen ingår i AEM Forms-tilläggspaketet.

AEM Forms är en kraftfull plattform i företagsklass. Formulärcentrerat arbetsflöde i OSGi är bara en av funktionerna i AEM Forms. En fullständig lista över funktioner finns i [Introduktion till AEM Forms](../../forms/using/introduction-aem-forms.md).

>[!NOTE]
>
>Med ett formulärbaserat arbetsflöde i OSGi kan du snabbt skapa och distribuera arbetsflöden för olika uppgifter i OSGi-stacken, utan att behöva installera den fullständiga processhanteringsfunktionen i JEE-stacken. Se en [jämförelse](../../forms/using/capabilities-osgi-jee-workflows.md) av de formulärbaserade AEM-arbetsflödena om OSGi och Process Management på JEE för att lära dig skillnaden och likheterna i funktionerna.
>
>Efter jämförelsen finns mer detaljerad information om hur du installerar och konfigurerar JEE-stacken i [Installera eller uppgradera AEM Forms på JEE](/help/forms/home.md) om du väljer att installera processhanteringsfunktionen på JEE-stacken.

## Distributionstopologi {#deployment-topology}

AEM Forms-tilläggspaketet är ett program som distribueras till AEM. Du behöver bara minst en AEM-författare eller bearbetningsinstans (produktionsförfattare) för att köra det formulärbaserade arbetsflödet på OSGi-funktionen. En bearbetningsinstans är en instans av en [AEM Author](/help/forms/using/hardening-securing-aem-forms-environment.md) . Gör inga riktiga skribenter, som att skapa arbetsflöden eller anpassningsbara formulär, åt produktionsförfattaren.

Följande topologi är en indikativ topologi för att köra AEM Forms Interactive Communications, Correspondence Management, AEM Forms data capture och Forms-Centric workflow på OSGi-funktioner. Mer information om topologin finns i [Arkitektur och distributionstopologier för AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![rekommenderad topologi](assets/recommended-topology.png)

Det AEM Forms Forms-baserade arbetsflödet på OSGi kör användargränssnittet för AEM Inbox och AEM Workflow Model på författarinstanserna av AEM Forms.

## Systemkrav {#system-requirements}

>[!NOTE]
>
>Gå till avsnittet [Nästa steg](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps) i dokumentet om du redan har installerat AEM Forms på OSGi enligt anvisningarna i artikeln [Installera och konfigurera datainhämtningsfunktioner](../../forms/using/installing-configuring-aem-forms-osgi.md) .

Innan du börjar installera och konfigurera ett formulärcentrerat arbetsflöde i OSGi måste du se till att:

* Maskinvaru- och programvaruinfrastruktur finns på plats. En detaljerad lista över maskin- och programvara som stöds finns i [tekniska krav](/help/sites-deploying/technical-requirements.md).

* Installationssökvägen för AEM-instansen innehåller inte blanksteg.
* En AEM-instans körs. I AEM-terminologi är &quot;instance&quot; en kopia av AEM som körs på en server i författar- eller publiceringsläge. Du måste ha minst en AEM-instans (författare eller bearbetning) för att kunna köra ett formulärcentrerat arbetsflöde på OSGi:

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

AEM Forms-tilläggspaketet är ett program som distribueras till AEM. Paketet innehåller formulärorienterat arbetsflöde för OSGi och andra funktioner. Så här installerar du tilläggspaketet:

1. Logga in på [AEM-servern](https://localhost:4502) som administratör och öppna [paketresursen](https://localhost:4502/crx/packageshare). Du måste ha ett Adobe-id för att kunna logga in på paketresursen.
1. I [AEM-paketresursen](https://localhost:4502/crx/packageshare/login.html)söker du efter tilläggspaket för **AEM 6.5-formulär** eller **senaste Service Pack**, klickar på det paket som gäller för ditt operativsystem och klickar på **Hämta**. Läs och godkänn licensavtalet och klicka på **OK**. Nedladdningen startar. När du har hämtat **visas ordet Hämtad** bredvid paketet.

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

#### Konfigurera Dispatcher {#configure-dispatcher}

Dispatcher är ett verktyg för cachelagring och lastbalansering för AEM. AEM Dispatcher skyddar även AEM-servern mot attacker. Du kan öka säkerheten för din AEM-instans genom att använda Dispatcher tillsammans med en webbserver i företagsklass. Om du använder [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)gör du följande konfigurationer för AEM Forms:

1. Konfigurera åtkomst för AEM Forms:

   Öppna filen dispatcher.any för redigering. Navigera till filteravsnittet och lägg till följande filter i filteravsnittet:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Spara och stäng filen. Mer information om filter finns i [Dispatcher-dokumentationen](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Konfigurera tjänsten för refererarfilter:

   Logga in som administratör i konfigurationshanteraren för Apache Felix. Konfigurationshanterarens standard-URL är https://&#39;server&#39;:[port_number]/system/console/configMgr. På menyn **Konfigurationer** väljer du alternativet **Apache Sling Reference Filter** . I fältet Tillåt värdar anger du värdnamnet för dispatchern så att den kan användas som referent och klickar på **Spara**. Formatet på posten är `https://'[server]:[port]'`.

#### Konfigurera cache {#configure-cache}

Cachelagring är en mekanism som förkortar dataåtkomsttider, minskar fördröjningen och förbättrar in-/utdatahastigheter (I/O). Cacheminnet för adaptiva formulär lagrar endast HTML-innehåll och JSON-strukturen i ett adaptivt formulär utan att några förfyllda data sparas. Det minskar tiden som krävs för att återge ett anpassat formulär.

* När du använder cacheminnet för adaptiva formulär använder du [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) för att cachelagra klientbibliotek (CSS och JavaScript) för ett adaptivt formulär.
* När du utvecklar anpassade komponenter bör du se till att cachen för anpassade formulär är inaktiverad på servern som används för utveckling.

Utför följande steg för att konfigurera cachen för adaptiva formulär:

1. Gå till konfigurationshanteraren för AEM-webbkonsolen på `https://'[server]:[port]'/system/console/configMgr`.
1. Klicka på **tjänsten** Adaptiv formulärkonfiguration för att redigera dess konfigurationsvärden. I dialogrutan Redigera konfigurationsvärden anger du det maximala antalet formulär eller dokument som en instans av AEM Forms-servern kan cachelagra i fältet **Antal adaptiva formulär** . Standardvärdet är 100. Click **Save**.

   >[!NOTE]
   >
   >Om du vill inaktivera cachen anger du värdet **0** i fältet Antal adaptiva formulär. Cacheminnet återställs och alla formulär och dokument tas bort från cacheminnet när du inaktiverar eller ändrar cachekonfigurationen.

#### Konfigurera Adobe Sign {#configure-adobe-sign}

Adobe Sign möjliggör e-signaturarbetsflöden för anpassningsbara formulär. E-signaturer förbättrar arbetsflödena för att bearbeta dokument inom juridik, försäljning, löneadministration, personaladministration och många andra områden.

I ett typiskt Adobe Sign- och Forms-centrerat arbetsflöde i OSGi-scenarier fyller en användare i ett anpassningsbart formulär som **ska användas för en tjänst**. Till exempel kan en kreditkortsansökan och en medborgare få förmåner. När en användare fyller i, skickar och signerar ansökningsformuläret startas ett arbetsflöde för godkännande/avvisning. Tjänsteleverantören granskar programmet i AEM Inbox och använder Adobe Sign för att signera programmet elektroniskt. Om du vill aktivera liknande arbetsflöden för elektroniska signaturer kan du integrera Adobe Sign med AEM Forms.

Om du vill använda Adobe Sign med AEM-formulär [integrerar du Adobe Sign med AEM-formulär](../../forms/using/adobe-sign-integration-adaptive-forms.md).

## Nästa steg {#next-steps}

Du har konfigurerat en miljö för att använda ett formulärcentrerat arbetsflöde på OSGi-funktioner. Stegen för att använda funktionerna är nu:

* [Använda formulärcentrerat arbetsflöde på OSGi](../../forms/using/aem-forms-workflow.md)
* [Referens för arbetsflödessteg](/help/sites-developing/workflows-step-ref.md)
* [Efterbearbetning av brev och interaktiv kommunikation](../../forms/using/submit-letter-topostprocess.md)

