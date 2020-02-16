---
title: SharePoint-anslutning
seo-title: SharePoint-anslutning
description: Day JCR Connector för Microsoft SharePoint 2010 och Microsoft SharePoint 2013, version 4.0.
seo-description: Läs mer om Sharepoint Connector i AEM.
uuid: df650476-4e2a-486f-a007-b5ac437ff99f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 907316d1-3d23-4c46-bccb-bad6fe1bd1bb
docset: aem65
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# SharePoint-anslutning{#sharepoint-connector}

Den här artikeln innehåller information om Adobe JCR Connector för Microsoft SharePoint 2010 och Microsoft SharePoint 2013, version 4.0.

SharePoint-anslutningen stöder följande grundfunktioner:

* Läser innehåll och metadata från SharePoint.
* Bekräftar SharePoint-säkerhetsinställningar för åtkomst av innehåll genom att tillämpa intern SharePoint-autentisering och -auktorisering
* Innehållsintegrering med Content Finder
* Använda AEM-komponenter, till exempel Extern resurs, för att visa SharePoint-bilder och -videor
* Synkroniserar SharePoint med AEM Resurser

Alla funktioner implementeras med SharePoint-webbtjänster som gränssnitt till SharePoint-innehåll och -tjänster.

>[!NOTE]
>
>SharePoint Connector stöds även med AEM 6.1 Service Pack 2. Kopplingen stöder inte längre montering av virtuell databas och kan därför inte monteras. Om du vill komma åt SharePoint-databasen med Java API:er använder du SharePoint-anslutarens JCR-databasimplementering i ditt projekt.
>
>Installation, konfigurering, hantering och IT-åtgärder för SharePoint-servern och relaterad IT-infrastruktur omfattas inte av det här dokumentet. Mer information om de här avsnitten finns i leverantörsdokumentationen för [SharePoint](https://www.microsoft.com/sharepoint) . Kopplingen kräver att dessa delar av infrastrukturen är korrekt installerade, konfigurerade och i drift.


## Getting started {#getting-started}

Så här kommer du igång med anslutningen:

* Kontrollera att du har minst Java 7 installerat.
* Hämta distributionsfilen för kopplingspaketet från paketresursen.
* Kopiera en giltig *license.properties* -fil till katalogen som innehåller *filen cq-quickstart-6.4.0.jar* .

* Dubbelklicka/tryck på .jar-filen för att starta AEM eller starta den från kommandoraden.
* Installera kopplingspaketet från Package Manager.
* Konfigurera anslutningsalternativen.

## Installerar SharePoint-anslutning {#installing-sharepoint-connector}

Kopplingen är ett innehållspaket som underlättar enkel installation. Installera paketet med hjälp av Pakethanteraren och ange sedan URL:en för SharePoint-servern och andra konfigurationsalternativ. SharePoint-innehållet är tillgängligt i AEM-databasen.

### Installationskrav {#installation-requirements}

Kopplingen kräver följande:

* Java Runtime Environment 1.7 eller senare
* SharePoint-webbtjänster som är tillgängliga via nätverket
* URL för SharePoint-server
* Användarautentiseringsuppgifter och behörigheter för CRX- och SharePoint-databaser
* [Plattformar som stöds](#supported-platforms)

SharePoint-anslutningen är tillgänglig för hämtning från [paketdelning](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-17673).

### Plattformar som stöds {#supported-platforms}

Kopplingen stöder följande:

* AEM-versioner:

   * AEM 6.5, 6.4, 6.3

* Microsoft SharePoint-versioner:

   * Microsoft Office SharePoint Server (MOSS) 2010
   * Microsoft Office SharePoint Server (MOSS) 2013

* Om du behöver support för anpassad driftsättning av anslutningsprogrammet (OEM, särskilda krav, anpassade autentiseringsmetoder) kontaktar du Adobe-kontoret i din region.

>[!NOTE]
>
>Kopplingen stöder endast konfigurationer som officiellt stöds av Microsoft. Se systemkraven för [MOSS 2010](https://technet.microsoft.com/en-us/library/cc262485(office.14).aspx) och [MOSS 2013](https://technet.microsoft.com/en-us/library/cc262485.aspx) .

### Standardinstallation {#standard-installation}

AEM Package Share används för att distribuera produktfunktioner, exempel och snabbkorrigeringar. Mer information finns i dokumentationen [för](/help/sites-administering/package-manager.md#package-share)paketdelning.

Tryck/klicka på **Verktyg** och välj sedan **Paketresurs** för att öppna Paketdelning på AEM-välkomstsidan. Du måste ha ett giltigt Adobe-ID som innehåller företagets e-postadress. När du har loggat in på ditt konto ansöker du dessutom om åtkomst till paketdelning.

#### Integrera med AEM {#integrating-with-aem}

Installera innehållspaketet för anslutningsprogrammet.

1. Öppna en Adobe Support-biljett och begär anslutningsfunktionen.
1. Hämta paketet när det är tillgängligt och öppna sedan Package Manager för din AEM-instans.
1. Tryck/klicka på **Installera** på paketbeskrivningssidan.
1. I dialogrutan **Installera paket** trycker/klickar du på **Installera**.

   **Obs**: Kontrollera att du är inloggad som administratör.

1. Tryck/klicka på **Stäng** när paketet är installerat.

## Konfigurerar SharePoint-koppling {#configuring-sharepoint-connector}

När du har installerat SharePoint-anslutningen konfigurerar du programmet och SharePoint-lagren för anslutningen.

Ange SharePoint-serverns URL så att SharePoint-databasen är JCR-kompatibel. Du kan ange extra parametrar för att konfigurera anslutningen till SharePoint-servern. Konfigurera dessutom autentisering med SharePoint-anslutningen.

### Konfigurera anslutningen till SharePoint-servern {#configuring-the-connection-with-the-sharepoint-server}

Så här anger du URL:en för SharePoint-servern och avancerade alternativ:

1. Gå till OSGi Management Console: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Sök efter **Dag JCR Connector för Microsoft Sharepoint** -paketet.
1. Redigera konfigurationsvärdena.
1. Ange SharePoint Server-URL:en som värde för **Arbetsytor**.
1. Tryck/klicka på **Spara**.

![chlimage_1-62](assets/chlimage_1-62.png)

Parametrarna &quot;Arbetsytor&quot; och &quot;Standardnamn på arbetsyta&quot;:

Som standard visar kopplingen en enda JCR-arbetsyta. SharePoint-servern som visas av den här arbetsytan anges med konfigurationsparametern SharePoint Server URL.

Kopplingen kan även konfigureras för flera arbetsytor. I det här fallet är varje arbetsyta associerad med URL:en för respektive SharePoint-server som visas via arbetsytan. Om du vill lägga till en arbetsyta lägger du till en arbetsytedefinition i parametern Arbetsytor. En arbetsytedefinition har följande format:
`<name>`= `<url>` där`<name>` är namnet på JCR-arbetsytan och`<url>` är URL:en för SharePoint-servern för den arbetsytan.

I AEM utför du ett steg till utöver konfigurationsstegen ovan. Ta en vitlista med paketet &#39;**com.day.cq.dam.cq-dam-jcr-connectors**&#39;.

Så här vitlistar du paket i AEM:

1. Gå till OSGi Management Console: http://localhost:4502/system/console/configMgr.
1. Sök efter tjänsten Apache Sling Login Admin Whitelist.
1. Välj Kringgå vitlistan.
1. Lägg till &#39;**com.day.cq.dam.cq-dam-jcr-connectors**&#39; i standardpaket för vitlistpaket
1. Klicka på Spara.

![chlimage_1-82](assets/chlimage_1-82a.png)

>[!NOTE]
>
>Om du konfigurerar flera arbetsytor anger du namnet på standardarbetsytan i parametern Standardnamn på arbetsyta.

Mer information om autentiseringsrelaterade parametrar finns i [Autentisering](/help/sites-administering/sharepoint-connector.md#configuring-authentication).

### Verifiera SharePoint-konfigurationen {#verifying-the-sharepoint-setup}

Kontrollera följande när du har konfigurerat anslutningen:

* SharePoint-servern körs och webbtjänsterna är tillgängliga för anslutningsinstansen
* SharePoint-inloggningsuppgifterna är giltiga och användaren har nödvändiga SharePoint-behörigheter
* Kopplingen är installerad och korrekt konfigurerad

### Konfigurera DAM-synkronisering med SharePoint-servern {#configuring-dam-sync-with-the-sharepoint-server}

Så här synkroniserar du SharePoint-resurser med AEM:

1. Gå till OSGi Management Console: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Sök efter tjänsten DAMAssetSynchronization som standard.
1. Redigera konfigurationsvärdena.
1. Ange användarnamnet och motsvarande lösenord för den användare som har åtkomst på SharePoint-webbplatsen.
1. Klicka på Spara.

Aktivera DAM-synkroniseringstjänsten som är inaktiverad som standard:

1. Navigera till OSGi Web Console-komponenterna: [http://localhost:4502/system/console/components](http://localhost:4502/system/console/components)
1. Sök efter&quot;com.day.cq.dam.jcrconnectors.impl.AssetSynchronizationService.&quot;
1. Klicka på Aktivera.

Du kan också konfigurera synkroniseringsfördröjningen mellan olika synkroniseringscykler:

1. Gå till OSGi Management Console: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
1. Sök efter &quot;DAY CQ DAM JCR Connector Asset Synchronization Service.&quot;
1. Redigera konfigurationsvärdena.
1. Ange värdet för synkroniseringsperioden (i sekunder).
1. Klicka på Spara.

### Konfigurerar autentisering {#configuring-authentication}

SharePoint innehåller klassiska och anspråksbaserade autentiseringsmetoder, som båda stöder följande autentiseringstyper:

* Grundläggande
* Formulärbaserad

Bland annat finns följande typer av autentisering:

* Classic-Basic
* Klassisk-formulärbaserad
* Claims-Basic
* Anspråksblanketter-baserade

AEM JCR Connector för Microsoft SharePoint 2010 och Microsoft SharePoint 2013, version 4.0. har stöd för anspråksbaserad autentisering (som föreslås av Microsoft) som fungerar i följande lägen:

* **Grundläggande/NTLM-autentisering**: Kopplingen försöker först ansluta med grundläggande autentisering. Om den inte är tillgänglig växlar den till NTLM-baserad autentisering.
* **Formulärbaserad autentisering**: SharePoint validerar användare baserat på inloggningsuppgifter som användare skriver i ett inloggningsformulär (vanligtvis en webbsida). Systemet utfärdar en token för autentiserade begäranden som innehåller en nyckel för att återupprätta identiteten för efterföljande begäranden.

**Konfigurerar formulärbaserad autentisering**

Gå till: [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)

1. Klicka på OSGI -> Konfiguration
1. Sök efter&quot;Day JCR Connector for Microsoft Sharepoint&quot;
1. Klicka på&quot;Redigera konfigurationsvärden&quot;
1. Ange värdet för Sharepoint Connection Factory som com.day.crx.spi.sharepoint.security.FormsBasedAuthenticationConnectionFactory
1. Click **Save**.

**Konfigurerar grundläggande autentisering (Windows)**

1. [Inaktivera tokenautentisering](#disable-token-authentication).
1. Gå till [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).
1. Klicka på OSGI > Konfiguration.
1. Sök efter JCR Connector för **Dag för Microsoft Sharepoint**.
1. Click `Edit the configuration values`.
1. Ange värdet för Sharepoint Connection Factory till `com.day.crx.spi.sharepoint.security.WindowsAuthenticationConnectionFactory`.
1. Click **Save**.

Endast användare som är autentiserade på både AEM och SharePoint kan komma åt SharePoint-innehållet via anslutningen.

Du kan också använda anslutningstillägget för autentisering för att skapa en anpassad autentiseringsmodul, som t.ex. mappar AEM-användares åtkomst till specifika SharePoint-användare. Skapa AEM-användare som motsvarar SharePoint-användare (användarnamn och lösenord måste matcha) för att kunna se SharePoint-innehåll som mappas till kopplingsinstansen.

Så här skapar du en användare i AEM:

1. Logga in på http://localhost:9502/with administratörsanvändaren.
1. Klicka på Verktyg.
1. Klicka på Dokumentskydd.
1. Klicka på Användare.
1. Klicka på **Skapa användare**.
1. Ange användar-ID (användarnamn med åtkomst i SharePoint).
1. Ange motsvarande lösenord.
1. Klicka på den gröna skalmarkeringssymbolen för att skapa användaren.

Så här lägger du till användaren i administratörsgruppen:

1. Gå till Gruppadministration.
1. Klicka på noden&quot;a&quot;.
1. Klicka på&quot;administratörer&quot;.
1. Skriv det användar-ID som skapades ovan i textrutan före knappen **Bläddra** .
1. Klicka på den gröna markeringssymbolen för att lägga till användaren i administratörsgruppen.

### Inaktivera tokenautentisering {#disable-token-authentication}

1. Hämta och installera paketet `basic auth`. `zip` från paketresurs.

1. Stäng QuickStart.
1. Öppna filen *\crx-quickstart\repository\repository.xml*.
1. Hitta taggen `<LoginModule class="com.day.crx.core.CRXLoginModule"> ... </LoginModule>.`
1. Infoga taggen `<param name="disableTokenAuth" value="true"/>` inuti taggen som nämns i steg 4.
1. Spara och stäng xml-filen.
1. Starta om QuickStart och logga in med dina inloggningsuppgifter.

#### Stöd för olika autentiseringsmetoder i SharePoint-servern {#supporting-different-authentication-methods-of-the-sharepoint-server}

I standardversionen har kopplingen stöd för standardautentisering i IIS **Windows** (Basic) och formulärbaserad autentisering (tokenbaserad). De [andra autentiseringsmetoderna](https://technet.microsoft.com/en-us/library/cc262350.aspx#section2) kan stödjas via utökningsmekanismen.

Följande steg innehåller riktlinjer om hur du utökar standardautentiseringen så att den stöder olika autentiseringsmetoder i SharePoint-servern:

1. Implementera `com.day.crx.spi.sharepoint.security.SharepointConnectionFactory` för att hantera klientsidan av din specifika autentiseringsprocess.
1. Installera `SharepointConnectionFactory` implementeringen som ett fragmentpaket med fragmentvärden `com.day.crx.spi.crx2sharepoint-bundle`.

   När du använder Maven kan du anpassa följande konfiguration av `maven-bundle-plugin` för att uppfylla dina projektkrav:

   ```xml
              <plugin>
                  <groupId>org.apache.felix</groupId>
                  <artifactId>maven-bundle-plugin</artifactId>
                  <extensions>true</extensions>
                  <configuration>
                      <instructions>
                          <Export-Package />
                          <Private-Package>
                              <!-- your private package here -->
                          </Private-Package>
                          <Fragment-Host>
                              com.day.crx.spi.crx2sharepoint-bundle
                          </Fragment-Host>
                       </instructions>
                  </configuration>
              </plugin>
   ```

1. Registrera `SharepointConnectionFactory` implementeringen i anslutningskonfigurationen. Klicka på **Avancerade alternativ** i anslutningsprogrammets konfigurationsfönster. Ange implementeringens namn i fältet for **Sharepoint Connection Factory** `com.day.crx.spi.sharepoint.auth.CustomConnectionFactory`.

1. Starta om kopplingen.

