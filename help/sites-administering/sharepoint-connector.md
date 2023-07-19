---
title: SharePoint Connector
seo-title: SharePoint Connector
description: Day JCR Connector for Microsoft SharePoint 2010 and Microsoft SharePoint 2013, version 4.0.
seo-description: Learn about the Sharepoint Connector in AEM.
uuid: df650476-4e2a-486f-a007-b5ac437ff99f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 907316d1-3d23-4c46-bccb-bad6fe1bd1bb
docset: aem65
exl-id: 10ea7d2e-6e44-4d5c-a2b2-63c73b18f172
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1563'
ht-degree: 0%

---

# SharePoint Connector{#sharepoint-connector}

Den här artikeln innehåller information om Adobe JCR Connector för Microsoft SharePoint 2010 och Microsoft SharePoint 2013, version 4.0.

SharePoint-anslutningen stöder följande grundläggande funktioner:

* Läsa innehåll och metadata från SharePoint.
* Bekräfta SharePoint säkerhetsinställningar för åtkomst av innehåll genom att använda SharePoint autentisering och behörighet
* Innehållsintegrering med Content Finder
* Använda AEM, till exempel Extern resurs, för att visa SharePoint-bilder och -videor
* Synkronisera SharePoint med AEM Assets

Alla funktioner implementeras med SharePoint inbyggda webbtjänster som gränssnitt till SharePoint innehåll och tjänster.

>[!NOTE]
>
>SharePoint Connector stöds även med AEM 6.1 Service Pack 2. Kopplingen stöder inte längre montering av virtuell databas och kan därför inte monteras. Om du vill komma åt SharePoint-databasen med Java API:er använder du SharePoint-anslutarens JCR-databasimplementering i ditt projekt.
>
>Installation, konfigurering, hantering och IT-drift av SharePoint-servern och relaterad IT-infrastruktur omfattas inte av detta dokument. Se leverantörsdokumentation på [SharePoint](https://www.microsoft.com/sharepoint) för information om dessa ämnen. Kopplingen kräver att dessa delar av infrastrukturen är korrekt installerade, konfigurerade och i drift.
>

## Komma igång {#getting-started}

Så här kommer du igång med anslutningen:

* Kontrollera att du har minst Java 7 installerat.
* Ladda ned distributionsfilen för kopplingspaketet från Software Distribution.
* Kopiera en giltig *license.properties* till katalogen som innehåller *cq-quickstart-6.4.0.jar* -fil.

* Dubbelklicka/tryck på .jar-filen för att starta AEM eller starta den från kommandoraden.
* Installera kopplingspaketet från Package Manager.
* Konfigurera anslutningsalternativen.

## Installerar SharePoint Connector {#installing-sharepoint-connector}

Kopplingen är ett innehållspaket som underlättar enkel installation. Installera paketet med hjälp av Pakethanteraren och ange sedan webbadressen till SharePoint-servern och andra konfigurationsalternativ. SharePoint-innehållet finns i AEM.

### Installationskrav {#installation-requirements}

Kopplingen kräver följande:

* Java Runtime Environment 1.7 eller senare
* SharePoint webbtjänster som är tillgängliga via nätverket
* SharePoint server-URL
* Autentiseringsuppgifter och behörigheter för CRX- och SharePoint-databaser
* [Plattformar som stöds](#supported-platforms)

SharePoint Connector kan hämtas från [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-17673).

### Plattformar som stöds {#supported-platforms}

Kopplingen stöder följande:

* AEM versioner:

   * AEM 6.4, 6.3

* Microsoft SharePoint:

   * Microsoft Office SharePoint Server (MOSS) 2010
   * Microsoft Office SharePoint Server (MOSS) 2013

* Om du behöver support för anpassad driftsättning av anslutningsprogrammet (OEM, särskilda krav, anpassade autentiseringsmetoder) kontaktar du Adobe-kontoret i ditt område.

>[!NOTE]
>
>Kopplingen stöder endast konfigurationer som officiellt stöds av Microsoft. Se [MOSS 2010](https://technet.microsoft.com/en-us/library/cc262485(office.14).aspx) och [MOSS 2013](https://technet.microsoft.com/en-us/library/cc262485.aspx) systemkrav.

### Standardinstallation {#standard-installation}

Distribution av programvara används för att distribuera produktfunktioner, exempel och snabbkorrigeringar. Mer information finns i [Dokumentation om programdistribution](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html#software-distribution).


#### Integrera med AEM {#integrating-with-aem}

Så här installerar du innehållspaketet för anslutningsprogrammet.

1. Öppna en Adobe Support-biljett och begär anslutningsfunktionen.
1. Hämta paketet när det är tillgängligt och öppna sedan Package Manager för AEM.
1. Tryck/klicka **Installera** från paketbeskrivningssidan.
1. Från **Installera paket** dialogruta, trycka/klicka **Installera**.

   **Anteckning**: Kontrollera att du är inloggad som administratör.

1. Tryck/klicka på paketet när det är installerat **Stäng**.

## Konfigurerar SharePoint Connector {#configuring-sharepoint-connector}

När du har installerat SharePoint-anslutningen konfigurerar du programmet och SharePoint-lagren för anslutningen.

Ange webbadressen till SharePoint-servern så att SharePoint-databasen är JCR-kompatibel. Du kan ange extra parametrar för att konfigurera anslutningen till SharePoint-servern. Konfigurera dessutom autentisering med SharePoint Connector.

### Konfigurera anslutningen till SharePoint-servern {#configuring-the-connection-with-the-sharepoint-server}

Så här anger du URL-adressen för SharePoint-servern och avancerade alternativ:

1. Gå till OSGi Management Console: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Sök efter **JCR Connector för Microsoft Sharepoint** paket.
1. Redigera konfigurationsvärdena.
1. Ange SharePoint Server-URL som värdet för **Arbetsytor**.
1. Tryck/klicka **Spara**.

![chlimage_1-62](assets/chlimage_1-62.png)

Parametrarna &quot;Arbetsytor&quot; och &quot;Standardnamn på arbetsyta&quot;:

Som standard visar kopplingen en enda JCR-arbetsyta. SharePoint-servern som visas av den här arbetsytan anges med konfigurationsparametern SharePoint Server URL.

Kopplingen kan även konfigureras för flera arbetsytor. I det här fallet är varje arbetsyta associerad med URL-adressen för respektive SharePoint-server som visas via arbetsytan. Om du vill lägga till en arbetsyta lägger du till en arbetsytedefinition i parametern Arbetsytor. En arbetsytedefinition har följande format:
`<name>`= `<url>` där
`<name>` är namnet på JCR-arbetsytan och
`<url>` är webbadressen till SharePoint-servern för den arbetsytan.

I AEM utför du ett steg till utöver konfigurationsstegen ovan. Tillåtelselista the &#39;**com.day.cq.dam.cq-dam-jcr-connectors**&#39; bundle.

Gör så här för att tillåtelselista-paket i AEM:

1. Gå till OSGi Management Console: http://localhost:4502/system/console/configMgr.
1. Sök efter tjänsten Apache Sling Login Admin Whitelist.
1. Välj **Kringgå vitlistan**.
1. Lägg till `com.day.cq.dam.cq-dam-jcr-connectors` i vitlistningspaket som standard
1. Klicka på Spara.

![chlimage_1-82](assets/chlimage_1-82a.png)

>[!NOTE]
>
>Om du konfigurerar flera arbetsytor anger du namnet på standardarbetsytan i parametern Standardnamn på arbetsyta.

Mer information om autentiseringsrelaterade parametrar finns i [Autentisering](/help/sites-administering/sharepoint-connector.md#configuring-authentication).

### Verifiera SharePoint-konfigurationen {#verifying-the-sharepoint-setup}

Kontrollera följande när du har konfigurerat anslutningen:

* SharePoint-servern körs och webbtjänsterna är tillgängliga för anslutningsinstansen
* SharePoint inloggningsuppgifter är giltiga och användaren har nödvändiga SharePoint-behörigheter
* Kopplingen är installerad och korrekt konfigurerad

### Konfigurera DAM-synkronisering med SharePoint-servern {#configuring-dam-sync-with-the-sharepoint-server}

Så här synkroniserar du SharePoint Assets med AEM:

1. Gå till OSGi Management Console: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Sök efter tjänsten DAMAssetSynchronization som standard.
1. Redigera konfigurationsvärdena.
1. Ange användarnamnet och motsvarande lösenord för den användare som har åtkomst på SharePoint webbplats.
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
* Forms-baserad

Bland annat finns följande typer av autentisering:

* Classic-Basic
* Klassisk-Forms-baserad
* Claims-Basic
* Claims-Forms-based

AEM JCR Connector för Microsoft SharePoint 2010 och Microsoft SharePoint 2013, version 4.0. har stöd för anspråksbaserad autentisering (som föreslås av Microsoft) som fungerar i följande lägen:

* **Grundläggande/NTLM-autentisering**: Kopplingen försöker först ansluta med grundläggande autentisering. Om den inte är tillgänglig växlar den till NTLM-baserad autentisering.
* **Forms-baserad autentisering**: SharePoint validerar användare baserat på inloggningsuppgifter som användare skriver i ett inloggningsformulär (vanligtvis en webbsida). Systemet utfärdar en token för autentiserade begäranden som innehåller en nyckel för att återupprätta identiteten för efterföljande begäranden.

**Konfigurerar Forms-baserad autentisering**

Gå till: [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)

1. Klicka på OSGI -> Konfiguration
1. Sök efter&quot;Day JCR Connector for Microsoft Sharepoint&quot;
1. Klicka på&quot;Redigera konfigurationsvärden&quot;
1. Ange värdet för Sharepoint Connection Factory som com.day.crx.spi.sharepoint.security.FormsBasedAuthenticationConnectionFactory
1. Klicka **Spara**.

**Konfigurerar grundläggande autentisering (Windows)**

1. [Inaktivera tokenautentisering](#disable-token-authentication).
1. Gå till [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).
1. Klicka på OSGI > Konfiguration.
1. Sök efter **JCR Connector för Microsoft Sharepoint**.
1. Klicka på `Edit the configuration values`.
1. Ange värdet för SharePoint Connection Factory till `com.day.crx.spi.sharepoint.security.WindowsAuthenticationConnectionFactory`.
1. Klicka **Spara**.

Endast användare som är autentiserade på både AEM och SharePoint har åtkomst till SharePoint-innehållet via anslutningen.

Du kan också använda anslutningstillägget för autentisering för att skapa en anpassad autentiseringsmodul, som t.ex. mappar åtkomst AEM användare till specifika SharePoint-användare. Skapa AEM användare som motsvarar SharePoint-användare (användarnamn och lösenord måste matcha) för att kunna se SharePoint-innehåll mappat till anslutningsinstansen.

Så här skapar du en användare i AEM:

1. Logga in på http://localhost:9502/with administratörsanvändaren.
1. Klicka på Verktyg.
1. Klicka på Dokumentskydd.
1. Klicka på Användare.
1. Klicka **Skapa användare**.
1. Ange användar-ID (användarnamn med åtkomst på SharePoint).
1. Ange motsvarande lösenord.
1. Klicka på den gröna skalmarkeringssymbolen för att skapa användaren.

Så här lägger du till användaren i administratörsgruppen:

1. Gå till Gruppadministration.
1. Klicka på noden&quot;a&quot;.
1. Klicka på&quot;administratörer&quot;.
1. Skriv det användar-ID som skapades ovan i textrutan före **Bläddra** -knappen.
1. Klicka på den gröna markeringssymbolen för att lägga till användaren i administratörsgruppen.

### Inaktivera tokenautentisering {#disable-token-authentication}

1. Hämta och installera paketet `basic auth`. `zip` från Software Distribution.

1. Stäng QuickStart.
1. Öppna filen *\crx-quickstart\repository\repository.xml*.
1. Hitta taggen `<LoginModule class="com.day.crx.core.CRXLoginModule"> ... </LoginModule>.`
1. Infoga taggen `<param name="disableTokenAuth" value="true"/>` inuti taggen som nämns i steg 4.
1. Spara och stäng xml-filen.
1. Starta om QuickStart och logga in med dina inloggningsuppgifter.

#### Stöd för olika autentiseringsmetoder på SharePoint-servern {#supporting-different-authentication-methods-of-the-sharepoint-server}

I standardversionen har kopplingen stöd för standard-IIS **Windows** autentisering (grundläggande) och Forms-baserad autentisering (tokenbaserad). The [andra autentiseringsmetoder](https://technet.microsoft.com/en-us/library/cc262350.aspx#section2) kan stödjas via utökningsmekanismen.

Följande steg innehåller riktlinjer om hur du utökar standardautentiseringen så att den stöder olika autentiseringsmetoder på SharePoint-servern:

1. Implementera `com.day.crx.spi.sharepoint.security.SharepointConnectionFactory` för att hantera klientsidan av din specifika autentiseringsprocess.
1. Installera `SharepointConnectionFactory` implementering som ett fragmentpaket med fragmentvärd `com.day.crx.spi.crx2sharepoint-bundle`.

   När du använder Maven anpassar du följande konfiguration av `maven-bundle-plugin` till projektkraven:

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

1. Registrera `SharepointConnectionFactory` implementering i anslutningskonfigurationen. Klicka på i anslutningsprogrammets konfigurationsfönster **Avancerade alternativ**. I **Sharepoint Connection Factory** fält, ange implementeringens namn `com.day.crx.spi.sharepoint.auth.CustomConnectionFactory`.

1. Starta om kopplingen.
