---
title: Distribuera webbgrupper
description: Lär dig hur du distribuerar communityn och communityfunktioner i Adobe Experience Manager.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: 5b3d572d-e73d-4626-b664-c985949469c9
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '1653'
ht-degree: 0%

---

# Distribuera webbgrupper {#deploying-communities}

## Förutsättningar {#prerequisites}

* [AEM 6.5 Platform](/help/sites-deploying/deploy.md)

* AEM Communities-licens

* Ytterligare licenser för:

   * [Funktioner i Adobe Analytics for Communities](/help/communities/analytics.md)
   * [MongoDB för MSRP](/help/communities/msrp.md)
   * [Adobe Cloud för ASRP](/help/communities/asrp.md)

## Checklista för installation {#installation-checklist}

**För [AEM](/help/sites-deploying/deploy.md#what-is-aem)**

* Installera den senaste [AEM 6.5 - uppdateringar](#aem64updates)

* Om du inte använder standardportarna (4502, 4503) [konfigurera replikeringsagenter](#replication-agents-on-author)
* [Replikera krypteringsnyckeln](#replicate-the-crypto-key)
* Om globaliseringen stöds [konfigurera automatisk översättning](/help/sites-administering/translation.md)
(exempelinställningar tillhandahålls för utveckling)

**För [Funktioner i Communities](/help/communities/overview.md)**

* Om en [publicera servergrupp](/help/sites-deploying/recommended-deploys.md#tarmk-farm), [identifiera den primära utgivaren](#primary-publisher)

* [Aktivera tunneltjänsten](#tunnel-service-on-author)
* [Aktivera social inloggning](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [Konfigurera Adobe Analytics](/help/communities/analytics.md)
* Konfigurera en [standardtjänst för e-post](/help/communities/email.md)
* Identifiera valet för [delad UGC-lagring](/help/communities/working-with-srp.md) (**SRP**)

   * Om MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [Installera och konfigurera MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [Konfigurera Solr](/help/communities/solr.md)
      * [Välj MSRP](/help/communities/srp-config.md)

   * Om relationsdatabas SRP [(DSRP)](/help/communities/dsrp.md)

      * [Installera JDBC-drivrutinen för MySQL](#jdbc-driver-for-mysql)
      * [Installera och konfigurera MySQL för DSRP](/help/communities/dsrp-mysql.md)
      * [Konfigurera Solr](/help/communities/solr.md)
      * [Välj DSRP](/help/communities/srp-config.md)

   * Om Adobe SRP [(ASRP)](/help/communities/asrp.md)

      * Arbeta med din kontorepresentant för etablering
      * [Välj ASRP](/help/communities/srp-config.md)

   * Om JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * Inte ett delat UGC-arkiv (användargenererat innehåll):

         * UGC replikeras aldrig
         * UGC är bara synligt på AEM eller kluster där det angavs

         * Standardvärdet är JSRP

## Senaste releaser {#latest-releases}

AEM 6.5 Communities GA innehåller Communities-paketet. Läs mer om uppdateringar av AEM 6.5 [Communities](/help/release-notes/release-notes.md#experiencemanagercommunities), se [Versionsinformation för AEM 6.5](/help/release-notes/release-notes.md#communities-release-notes.html).

### AEM 6.5 - uppdateringar {#aem-updates}

Från och med AEM 6.4 levereras uppdateringar av Communities som en del av AEM Cumulative Fix Packs och Service Packs.

De senaste uppdateringarna av AEM 6.5 finns på [Adobe Experience Manager 6.4 Cumulative Fix Packs and Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html).

### Tidigare versioner {#version-history}

Liksom AEM 6.4 och senare är AEM Communities funktioner och snabbkorrigeringar en del av AEM Communities kumulativa korrigeringspaket och servicepaket. Det finns därför inga separata funktionspaket.

### JDBC-drivrutin för MySQL {#jdbc-driver-for-mysql}

En webbgruppsfunktion använder en MySQL-databas:

* För [DSRP](/help/communities/dsrp.md): lagra UGC

MySQL-kopplingen måste hämtas och installeras separat.

De nödvändiga stegen är:

1. Hämta ZIP-arkivet från [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * Versionen måste vara >= 5.1.38

1. Extract mysql-connector-java-&lt;version>-bin.jar (bundle) från arkivet
1. Använd webbkonsolen för att installera och starta paketet:

   * Till exempel https://localhost:4502/system/console/bundles
   * Välj **`Install/Update`**
   * Bläddra.. för att välja det paket som extraherats från det hämtade ZIP-arkivet
   * Kontrollera att *Oracle Corporations JDBC-drivrutin för MySQLcom.mysql.jdbc* är aktivt och starta det om inte (eller kontrollera loggarna)

1. Om du installerar på en befintlig distribution efter att JDBC har konfigurerats, binder du om JDBC till den nya anslutningen genom att spara om JDBC-konfigurationen från webbkonsolen:
   * Till exempel https://localhost:4502/system/console/configMgr
   * Sök `Day Commons JDBC Connections Pool` konfiguration
   * Markera för att öppna
   * Välj `Save`

1. Upprepa steg 3 och 4 för alla författare- och publiceringsinstanser

Mer information om hur du installerar paket finns på [Webbkonsol](/help/sites-deploying/web-console.md) sida.

#### Exempel: Installerat MySQL Connector-paket {#example-installed-mysql-connector-bundle}

![kopplingspaket](assets/connector-bundle.png)



### AEM avancerad MLS {#aem-advanced-mls}

För att SRP-samlingen (MSRP eller DSRP) ska ha stöd för avancerad flerspråkig sökning (MLS) krävs nya Solr-plugin-program förutom ett anpassat schema och en Solr-konfiguration. Alla nödvändiga objekt paketeras i en nedladdningsbar zip-fil.

Avancerad MLS-nedladdning (kallas även `phasetwo`) finns i Adobe-databasen:

* AEM-SOLR-MLS-phasetwo

  Information om hur du hämtar det avancerade MLS-paketet finns i [AEM avancerad MLS](deploy-communities.md#aem-advanced-mls) i distributionsavsnittet i dokumentationen.

   * Version 1.2.40, 6 april 2016
   * Ladda ned AEM-SOLR-MLS-phasetwo-1.2.40.zip

Mer information och installationsinformation finns på [Solr-konfiguration](/help/communities/solr.md) för SRP.

### Om länkar att paketera resurs {#about-links-to-package-share}

**Paket synliga i Adobe AEM Cloud**

Länkarna till paketen på den här sidan kräver ingen instans av AEM som körs eftersom de ska paketera Dela på `adobeaemcloud.com`. Paketen kan visas, men `Install` är till för att installera paketen på en värdplats i Adobe. Om du tänker installera på en lokal AEM väljer du `Install` resulterar i ett fel.

**Installera på lokal AEM**

Installera de paket som visas i `adobeaemcloud.com` på en lokal AEM måste paketet först hämtas till en lokal disk:

* Välj **Resurser** tab
* Välj **ladda ned till disk**

På den lokala AEM ska du använda Package Manager (till exempel [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/)) för att överföra till den lokala AEM.

Du kan också komma åt paketet med hjälp av Package Share från den lokala AEM-instansen (till exempel [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)), `Download` laddar ned till den lokala AEM instansens paketdatabas.

När du är i den lokala AEM-instansens paketdatabas använder du Package Manager för att installera paketet.

Mer information finns på [Så här arbetar du med paket](/help/sites-administering/package-manager.md#package-share).

## Rekommenderade distributioner {#recommended-deployments}

I AEM Communities används en gemensam butik för att lagra användargenererat innehåll och kallas ofta [lagringsresursleverantör (SRP)](/help/communities/working-with-srp.md). Rekommenderade distributionscenter när de väljer ett SRP-alternativ för den gemensamma butiken.

Den gemensamma lagringsplatsen har stöd för moderering och analys av användargenererat innehåll i publiceringsmiljön samtidigt som behovet av [replikering](/help/communities/sync.md) av UGC.

* [Community Content Store](/help/communities/working-with-srp.md) : diskuterar SRP-lagringsalternativ för AEM Communities

* [Rekommenderade topologier](/help/communities/topologies.md) : diskuterar topologin som ska användas beroende på användningsfall och SRP-val

## Uppgraderar {#upgrading}

När du uppgraderar till AEM 6.5 från tidigare versioner av AEM är det viktigt att du läser [Uppgradera till AEM 6.5](/help/sites-deploying/upgrade.md).

Förutom att uppgradera plattformen kan du läsa [Uppgradera till AEM Communities 6.5](/help/communities/upgrade.md) om du vill veta mer om förändringar i communities.

## Konfigurationer {#configurations}

### Primär utgivare {#primary-publisher}

När den valda distributionen är en [publicera servergrupp](/help/communities/topologies.md#tarmk-publish-farm)måste en AEM publiceringsinstans identifieras som **`primary publisher`** för aktiviteter som inte ska förekomma i alla instanser. Funktioner som är beroende av **meddelanden** eller **Adobe Analytics**.

Som standard är `AEM Communities Publisher Configuration` OSGi-konfigurationen är konfigurerad med **`Primary Publisher`** kryssrutan är markerad så att alla publiceringsinstanser i en publiceringsgrupp identifierar sig själva som primär.

Det är därför nödvändigt att **redigera konfigurationen för alla sekundära publiceringsinstanser** för att avmarkera **`Primary Publisher`** kryssrutan.

![primär utgivare](assets/primary-publisher.png)

För alla andra (sekundära) publiceringsinstanser i en publiceringsgrupp:

* Logga in med administratörsbehörighet
* Öppna [webbkonsol](/help/sites-deploying/configuring-osgi.md)

   * Till exempel: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* Leta reda på `AEM Communities Publisher Configuration`
* Markera redigeringsikonen
* Avmarkera **Primär utgivare** box
* Välj **Spara**

### Replikeringsagenter på författare {#replication-agents-on-author}

Replikering används för webbplatsinnehåll som skapas i publiceringsmiljön, t.ex. communitygrupper, och hanterar medlemmar och medlemsgrupper från författarmiljön med hjälp av [tunneltjänst](#tunnel-service-on-author).

För den primära utgivaren måste du se till att [Konfiguration för replikeringsagent](/help/sites-deploying/replication.md) identifierar publiceringsservern och den behöriga användaren korrekt. Den standardauktoriserade användaren, `admin,` har redan rätt behörigheter (är medlem i `Communities Administrators`).

För att andra användare ska ha rätt behörigheter måste de läggas till som medlem i `administrators` användargrupp (även medlem av `Communities Administrators`).

Det finns två replikeringsagenter i författarmiljön som kräver att transportkonfigurationen är korrekt konfigurerad.

* Åtkomst till replikeringskonsolen på författaren

   * Navigera från global navigering till **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** > **[!UICONTROL Agents on author]**

* Följ samma procedur för båda agenterna:

   * **Standardagent (publicera)**
   * **Agenten för omvänd replikering (publicera omvänd)**

      1. Välj agent
      1. Välj **redigera**
      1. Välj **Transport** tab
      1. Om den inte är port `4503`, redigera **URI** för att ange rätt port

      1. Om det inte är en användare `admin`, redigera **Användare** och **Lösenord** för att ange en medlem i `administrators` användargrupp

I följande bilder visas resultatet av en ändring av porten från 4503 till 6103 med:

#### Standardagent (publicera) {#default-agent-publish}

![default-agent-publish](assets/default-agent-publish.png)

#### Agenten för omvänd replikering (publicera omvänd) {#reverse-replication-agent-publish-reverse}

![reverse-replication-agent](assets/reverse-replication-agent.png)

### Tunneltjänst på författare {#tunnel-service-on-author}

När du använder redigeringsmiljön för att [skapa webbplatser](/help/communities/sites-console.md), [ändra webbplatsegenskaper](/help/communities/sites-console.md#modifying-site-properties) eller [hantera communitymedlemmar](/help/communities/members.md)måste du ha åtkomst till medlemmar (användare) som är registrerade i publiceringsmiljön, inte till användare som är registrerade hos författaren.

Tunneltjänsten ger denna åtkomst med replikeringsagenten på författaren.

Så här aktiverar du tunneltjänsten:

* Logga in med administratörsbehörighet för din författarinstans.
* Om utgivaren inte är localhost:4503 eller transportanvändaren inte är `admin`sedan [konfigurera replikeringsagenten](#replication-agents-on-author)

* Öppna [Webbkonsol](/help/sites-deploying/configuring-osgi.md)

   * Till exempel: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* Leta reda på `AEM Communities Publish Tunnel Service`
* Markera redigeringsikonen
* Kontrollera **enable** box
* Välj **Spara**

  ![tunnel-service](assets/tunnel-service.png)

### Replikera krypteringsnyckeln {#replicate-the-crypto-key}

Det finns två funktioner i AEM Communities som kräver att alla AEM serverinstanser använder samma krypteringsnycklar. Dessa är [Analyser](/help/communities/analytics.md) och [ASRP](/help/communities/asrp.md).

Från och med AEM 6.3 lagras nyckelmaterialet i filsystemet och inte längre i databasen.

Om du vill kopiera nyckelmaterialet från författaren till alla andra instanser måste du:

* Åtkomst till AEM, vanligtvis en Author-instans som innehåller det nyckelmaterial som ska kopieras

   * Leta reda på `com.adobe.granite.crypto.file` i det lokala filsystemet, till exempel

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * The `bundle.info` filen identifierar paketet

   * Navigera till datamappen, till exempel

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

      * Kopiera hmac- och primär nodfiler

* För varje AEM

   * Navigera till datamappen, till exempel

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

   * Klistra in de två tidigare kopierade filerna
   * Du måste [uppdatera Granite Crypto-paketet](#refresh-the-granite-crypto-bundle) om AEM körs

>[!CAUTION]
>
>Om en annan säkerhetsfunktion redan har konfigurerats som baseras på krypteringsnycklarna kan konfigurationen skadas om du replikerar krypteringsnycklarna. För assistans: [kontakta kundtjänst](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support).

#### Databasreplikering {#repository-replication}

Nyckelmaterialet som lagras i databasen, som i AEM 6.2 och tidigare, kan bevaras. Ange systemegenskapen `-Dcom.adobe.granite.crypto.file.disable=true` vid första starten av varje AEM (vilket skapar den inledande databasen).

>[!NOTE]
>
>Verifiera att [replikeringsagent på författare](#replication-agents-on-author) är korrekt konfigurerad.

Med nyckelmaterialet som lagras i databasen replikeras krypteringsnyckeln från författaren till andra instanser på följande sätt:

Använda [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Bläddra till [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* Välj `/etc/key`
* Öppna `Replication` tab
* Välj `Replicate`

* [Uppdatera Granite Crypto-paketet](#refresh-the-granite-crypto-bundle)

  ![replikera databas](assets/replicare-repository.png)

#### Uppdatera Granite-krypteringspaketet {#refresh-the-granite-crypto-bundle}

* I varje publiceringsinstans kan du få åtkomst till [Webbkonsol](/help/sites-deploying/configuring-osgi.md)

   * Till exempel: [https://&lt;server>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* Sök `Adobe Granite Crypto Support` bundle (com.adobe.granite.crypto)
* Välj **Uppdatera**

  ![granitkrypto](assets/granite-crypto.png)

* Efter ett ögonblick **Lyckades** ska visas:
  `Operation completed successfully.`

### Apache HTTP-server {#apache-http-server}

Om du använder Apache HTTP-servern måste du använda rätt servernamn för alla relevanta poster.

Var särskilt försiktig med att använda rätt servernamn, inte `localhost`, i `RedirectMatch`.

#### httpd.conf-exempel {#httpd-conf-sample}

```shell
<IfModule alias_module>
     # XAMPP does not have a favicon; this prevents any 404 errors which may arise.
     Redirect 404 /favicon.ico
     <Location /favicon.ico>
         ErrorDocument 404 "No favicon"
     </Location>

    # Return from "Sign Out" generates response header directing you to "/", generating a 404 error
    # The RedirectMatch resolves it correctly when modified for the target Community Site :
    RedirectMatch ^/$ https://[server name]/content/sites/engage/en.html
 ...
 </IfModule>
```

### Dispatcher {#dispatcher}

Om du använder en Dispatcher läser du:

* AEM [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html) dokumentation
* [Installerar Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/dispatcher-install.html)
* [Konfigurera Dispatcher för Communities](/help/communities/dispatcher.md)
* [Kända fel](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## Dokumentation för relaterade communities {#related-communities-documentation}

* Besök [Administrera webbgruppsplatser](/help/communities/administer-landing.md) om du vill veta mer om hur du skapar en community-webbplats, konfigurerar mallar för communitysajter, modererar communityinnehåll, hanterar medlemmar och konfigurerar meddelanden.

* Besök [Utveckla webbgrupper](/help/communities/communities.md) där du kan lära dig mer om det sociala ramverket (SCF) och hur du anpassar communitykomponenter och -funktioner.

* Besök [Komponenter i redigeringsgrupper](/help/communities/author-communities.md) där du kan lära dig hur du skapar med och konfigurerar webbgruppskomponenter.
