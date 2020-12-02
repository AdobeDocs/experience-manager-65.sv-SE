---
title: Distribuera webbgrupper
seo-title: Distribuera webbgrupper
description: Så här distribuerar du AEM Communities
seo-description: Så här distribuerar du AEM Communities
uuid: 18d9b424-004d-43b2-968a-318e27a93759
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: c8d7355f-5a70-40d1-bf22-62fab8002ea0
docset: aem65
translation-type: tm+mt
source-git-commit: b29945dc73e85504cd42102eafb9e2bf6198c9cc
workflow-type: tm+mt
source-wordcount: '1890'
ht-degree: 1%

---


# Distribuerar communities{#deploying-communities}

## Förutsättningar {#prerequisites}

* [AEM 6.5 Platform](/help/sites-deploying/deploy.md)

* AEM Communities-licens

* Ytterligare licenser för:

   * [Funktioner i Adobe Analytics for Communities](/help/communities/analytics.md)
   * [MongoDB för MSRP](/help/communities/msrp.md)
   * [Adobe Cloud för ASRP](/help/communities/asrp.md)

## Checklista för installation {#installation-checklist}

**För  [AEM](/help/sites-deploying/deploy.md#what-is-aem)**:

* Installera de senaste [AEM 6.5 uppdateringarna](#aem64updates).

* Om du inte använder standardportarna (4502, 4503) kan du [konfigurera replikeringsagenter](#replication-agents-on-author).
* [Replikera krypteringsnyckel](#replicate-the-crypto-key)
* Om det finns stöd för globalisering [konfigurerar du automatisk översättning](/help/sites-administering/translation.md)
(exempelinställningar tillhandahålls för utveckling).

**För funktionaliteten [](/help/communities/overview.md)** Communities:

* Om du distribuerar en [publiceringsgrupp](/help/sites-deploying/recommended-deploys.md#tarmk-farm), [identifierar du den primära utgivaren](#primary-publisher)

* [Aktivera tunneltjänsten](#tunnel-service-on-author)
* [Aktivera social inloggning](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [Konfigurera Adobe Analytics](/help/communities/analytics.md)
* Konfigurera en [standardtjänst för e-post](/help/communities/email.md)
* Identifiera valet för [delad UGC-lagring](/help/communities/working-with-srp.md) (**SRP**)

   * Om MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [Installera och konfigurera MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [Konfigurera Solr](/help/communities/solr.md)
      * [Välj MSRP](/help/communities/srp-config.md)
   * Om relationsdatabasen SRP [(DSRP)](/help/communities/dsrp.md)

      * [Installera JDBC-drivrutinen för MySQL](#jdbc-driver-for-mysql)
      * [Installera och konfigurera MySQL för DSRP](/help/communities/dsrp-mysql.md)
      * [Konfigurera Solr](/help/communities/solr.md)
      * [Välj DSRP](/help/communities/srp-config.md)
   * Om Adobe SRP [(ASRP)](/help/communities/asrp.md)

      * Samarbeta med din kontorepresentant för etablering.
      * [Välj ASRP](/help/communities/srp-config.md)
   * Om JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * Inte ett delat UGC-arkiv:

         * UGC replikeras aldrig.
         * UGC är bara synligt på AEM eller kluster där det angavs.
      * Standard är JSRP

   För **[aktiveringsfunktionen](/help/communities/overview.md#enablement-community)**

   * [Installera och konfigurera FFmpeg](/help/communities/ffmpeg.md)
   * [Installera JDBC-drivrutinen för MySQL](#jdbc-driver-for-mysql)
   * [Installera AEM Communities SCORM-Engine](#scorm-package)
   * [Installera och konfigurera MySQL för aktivering](/help/communities/mysql.md)






## Senaste versionerna {#latest-releases}

AEM 6.5 Communities GA innehåller Communities-paketet. Mer information om uppdateringar av AEM 6.5 [Communities](/help/release-notes/release-notes.md#experiencemanagercommunities) finns i [AEM 6.5 Release Notes](/help/release-notes/release-notes.md#communities-release-notes.html).

### AEM 6.5-uppdateringar {#aem-updates}

Från och med AEM 6.4 levereras uppdateringar av Communities som en del av AEM Cumulative Fix Packs och Service Packs.

De senaste uppdateringarna av AEM 6.5 finns i [Adobe Experience Manager 6.4 Cumulative Fix Packs and Service Packs](https://helpx.adobe.com/experience-manager/aem-releases-updates.html).

### Versionshistorik {#version-history}

Liksom AEM 6.4 och senare är AEM Communities funktioner och snabbkorrigeringar en del av AEM Communities kumulativa korrigeringspaket och servicepaket. Det finns därför inga separata funktionspaket.

### JDBC-drivrutin för MySQL {#jdbc-driver-for-mysql}

Två Communities-funktioner använder en MySQL-databas:

* För [aktivering](/help/communities/enablement.md): spela in SCORM-aktiviteter
* För [DSRP](/help/communities/dsrp.md): lagra användargenererat innehåll (UGC)

MySQL-kopplingen måste hämtas och installeras separat.

Nödvändiga steg är:

1. Hämta ZIP-arkivet från [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * Versionen måste vara >= 5.1.38

1. Extrahera `mysql-connector-java-&lt;version&gt;-bin.jar (bundle) from the archive`
1. Använd webbkonsolen för att installera och starta paketet:

   * Till exempel https://localhost:4502/system/console/bundles
   * Välj **`Install/Update`**
   * Bläddra.. för att välja det paket som extraherats från det hämtade ZIP-arkivet
   * Kontrollera att *Oracle Corporations JDBC-drivrutin för MySQLcom.mysql.jdbc* är aktiv och starta den om inte (eller kontrollera loggarna)

1. Om du installerar på en befintlig distribution efter att JDBC har konfigurerats, binder du om JDBC till den nya anslutningen genom att spara om JDBC-konfigurationen från webbkonsolen:

   * Till exempel https://localhost:4502/system/console/configMgr
   * Leta reda på konfigurationen `Day Commons JDBC Connections Pool` och välj för att öppna konfigurationen.
   * Välj `Save`.

1. Upprepa steg 3 och 4 för alla författare och publiceringsinstanser.

Mer information om hur du installerar paket finns på sidan [Webbkonsol](/help/sites-deploying/web-console.md#bundles).

#### Exempel: Installerat MySQL Connector-paket {#example-installed-mysql-connector-bundle}

![](../assets/mysql-connector.png)

### SCORM-paket {#scorm-package}

SCORM (Shareable Content Object Reference Model) är en samling standarder och specifikationer för e-utbildning. SCORM definierar också hur innehåll kan paketeras i en överförbar ZIP-fil.

AEM Communities SCORM-motorn krävs för funktionen [enablement](/help/communities/overview.md#enablement-community). SCORM-paket som stöds i AEM 6.5 Communities:

* [cq-social-scorm-package, version 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) som innehåller  [motorn SCORM 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) .

**Installera ett SCORM-paket**

1. Installera [cq-social-scorm-package, version 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) från paketresursen
1. Hämta `/libs/social/config/scorm/database_scormengine_data.sql` från cq-instansen och kör den på mysql-servern för att skapa ett uppgraderat scormEngineDB-schema.
1. Lägg till `/content/communities/scorm/RecordResults` i egenskapen Undantagna sökvägar i CSRF-filter från `https://<hostname>:<port>/system/console/configMgr` på utgivare.

#### SCORM-loggning {#scorm-logging}

Alla aktiveringsaktiviteter loggas utförligt på systemkonsolen, som de är installerade.

Om du vill kan du ange loggnivån till WARN för `RusticiSoftware.*`-paketet.

Mer information om hur du arbetar med loggar finns i [Arbeta med granskningsposter och loggfiler](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files).

### AEM Advanced MLS {#aem-advanced-mls}

För att SRP-samlingen (MSRP eller DSRP) ska ha stöd för avancerad flerspråkig sökning (MLS) krävs nya Solr-plugin-program förutom ett anpassat schema och en Solr-konfiguration. Alla nödvändiga objekt paketeras i en nedladdningsbar zip-fil.

Den avancerade MLS-nedladdningen (kallas även &quot;phasetwo&quot;) är tillgänglig från Adobe-databasen:

* [AEM-SOLR-MLS-phasetwo](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * Version 1.2.40, 6 april 2016
   * Ladda ned AEM-SOLR-MLS-phasetwo-1.2.40.zip

Mer information och installationsinformation finns på [Solr Configuration](/help/communities/solr.md) för SRP.

### Om länkar till paketresurs {#about-links-to-package-share}

**Paket synliga i Adobe AEM Cloud**

Länkarna till paketen på den här sidan kräver ingen instans av AEM som körs eftersom de ska paketera resursen på `adobeaemcloud.com`. När paketen kan visas använder du `Install`-knappen för att installera paketen på en värdplats i Adobe. Om du tänker installera på en lokal AEM kommer ett fel att uppstå om du väljer `Install`.

**Installera på lokal AEM**

Om du vill installera de paket som visas i `adobeaemcloud.com` på en lokal AEM måste paketet först hämtas till en lokal disk:

* Välj fliken **Resurser**
* Välj **hämta till disk**

På den lokala AEM ska du använda pakethanteraren (till exempel [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/)) för att överföra till den lokala AEM.

Alternativt kan du komma åt paketet med hjälp av paketresursen från den lokala AEM (till exempel [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)), så hämtas knappen `Download` till den lokala AEM-instansens paketdatabas.

När du är i den lokala AEM-instansens paketdatabas använder du pakethanteraren för att installera paketet.

Mer information finns på [Arbeta med paket](/help/sites-administering/package-manager.md#package-share).

## Rekommenderade distributioner {#recommended-deployments}

I AEM Communities används en gemensam lagringsplats för att lagra användargenererat innehåll (UGC) och kallas ofta [lagringsresursleverantör (SRP)](/help/communities/working-with-srp.md). Rekommenderade distributionscenter när de väljer ett SRP-alternativ för den gemensamma butiken.

Den gemensamma lagringsplatsen stöder moderering av och analys av UGC i publiceringsmiljön samtidigt som behovet av [replikering](/help/communities/sync.md) av UGC elimineras.

* [Community Content Store](/help/communities/working-with-srp.md) : diskuterar SRP-lagringsalternativ för AEM communities

* [Rekommenderade topologier](/help/communities/topologies.md) : diskuterar topologi som ska användas beroende på användningsfall och val av SRP

## Uppgraderar {#upgrading}

När du uppgraderar till AEM 6.5 från tidigare versioner av AEM är det viktigt att du läser [Uppgradera till AEM 6.5](/help/sites-deploying/upgrade.md).

Förutom att uppgradera plattformen kan du läsa [Uppgradera till AEM Communities 6.5](/help/communities/upgrade.md) om du vill veta mer om ändringar i communities.

## Konfigurationer {#configurations}

### Primär utgivare {#primary-publisher}

När den valda distributionen är en [publiceringsgrupp](/help/communities/topologies.md#tarmk-publish-farm) måste en AEM publiceringsinstans identifieras som **`primary publisher`** för aktiviteter som inte ska inträffa i alla instanser, till exempel funktioner som kräver **meddelanden** eller **Adobe Analytics**.

Som standard är OSGi-konfigurationen `AEM Communities Publisher Configuration` konfigurerad med kryssrutan **`Primary Publisher`** markerad, så att alla publiceringsinstanser i en publiceringsgrupp identifierar sig själva som primär.

Därför är det nödvändigt att **redigera konfigurationen för alla sekundära publiceringsinstanser** för att avmarkera kryssrutan **`Primary Publisher`**.

![](../assets/primary-publisher.png)

För alla andra (sekundära) publiceringsinstanser i en publiceringsgrupp:

* Logga in med administratörsbehörighet
* Åtkomst till [webbkonsolen](/help/sites-deploying/configuring-osgi.md)

   * Till exempel [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* Leta reda på `AEM Communities Publisher Configuration`
* Markera redigeringsikonen
* Avmarkera kryssrutan **Primär utgivare**
* Välj **Spara**

### Replikeringsagenter på författaren {#replication-agents-on-author}

Replikering används för webbplatsinnehåll som skapas i publiceringsmiljön, t.ex. communitygrupper, samt för att hantera medlemmar och medlemsgrupper från författarmiljön med hjälp av [tunneltjänsten](#tunnel-service-on-author).

För den primära utgivaren måste du se till att [Replikeringsagentkonfigurationen](/help/sites-deploying/replication.md) identifierar publiceringsservern och den auktoriserade användaren korrekt. Den auktoriserade standardanvändaren `admin` har redan rätt behörigheter (är medlem i `Communities Administrators`).

För att andra användare ska ha rätt behörigheter måste de läggas till som medlem i `administrators`-användargruppen (även medlem i `Communities Administrators`).

Det finns två replikeringsagenter i författarmiljön som kräver att transportkonfigurationen är korrekt konfigurerad.

* Åtkomst till replikeringskonsolen på författaren

   * Från global navigering: **Verktyg, distribution, replikering, agenter på författaren**

* Följ samma procedur för båda agenterna:

   * **Standardagent (publicera)**
   * **Agenten för omvänd replikering (publicera omvänd)**

      1. Välj agenten.
      1. Välj **redigera**.
      1. Välj fliken **Transport**
      1. Om porten inte är `4503` redigerar du **URI** och anger rätt port.

      1. Om du inte använder `admin` redigerar du **User** och **Password** för att ange en medlem i `administrators`-användargruppen.

I följande bilder visas resultatet av en ändring av porten från 4503 till 6103 med :

#### Standardagent (publicera) {#default-agent-publish}

![configure-limits](../assets/default-agent-publish.png)

#### Omvänd replikeringsagent (återpublicera) {#reverse-replication-agent-publish-reverse}

![](../assets/reverse-replication-agent.png)

### Tunneltjänsten på författaren {#tunnel-service-on-author}

När du använder författarmiljön för att [skapa webbplatser](/help/communities/sites-console.md), [ändra webbplatsegenskaper](/help/communities/sites-console.md#modifying-site-properties) eller [hantera communitymedlemmar](/help/communities/members.md), måste du få åtkomst till medlemmar (användare) som är registrerade i publiceringsmiljön, inte till användare som är registrerade hos författaren.

Tunneltjänsten ger denna åtkomst med replikeringsagenten på författaren.

Så här aktiverar du tunneltjänsten:

* Logga in med administratörsbehörighet på **författare**.
* Om utgivaren inte är localhost:4503 eller transportanvändaren inte är `admin`,
[konfigurera replikeringsagenten](#replication-agents-on-author).

* Åtkomst till [webbkonsolen](/help/sites-deploying/configuring-osgi.md)

   * Till exempel [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* Leta reda på `AEM Communities Publish Tunnel Service`
* Markera redigeringsikonen
* Markera kryssrutan **aktivera**
* välj **Spara**

![](../assets/tunnel-service.png)

### Replikera krypteringsnyckeln {#replicate-the-crypto-key}

Det finns två funktioner i AEM Communities som kräver att alla AEM serverinstanser använder samma krypteringsnycklar. Dessa är [Analytics](/help/communities/analytics.md) och [ASRP](/help/communities/asrp.md).

Från och med AEM 6.3 lagras nyckelmaterialet i filsystemet och inte längre i databasen.

Om du vill kopiera nyckelmaterialet från författaren till alla andra instanser måste du:

* Få åtkomst till AEM, vanligtvis en författarinstans som innehåller det nyckelmaterial som ska kopieras

   * Leta reda på `com.adobe.granite.crypto.file`-paketet i det lokala filsystemet

      Till exempel,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * `bundle.info`-filen identifierar paketet
   * Navigera till datamappen
till exempel

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * Kopiera hmac- och primära nodfiler.



* För varje AEM

   * Navigera till datamappen
till exempel

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * Klistra in de två tidigare kopierade filerna
   * Du måste [uppdatera Granite Crypto-paketet](#refresh-the-granite-crypto-bundle) om AEM är igång.


>[!CAUTION]
>
>Om en annan säkerhetsfunktion redan har konfigurerats som baseras på krypteringsnycklarna kan konfigurationen skadas om du replikerar krypteringsnycklarna. [Kontakta kundtjänst](https://helpx.adobe.com/marketing-cloud/contact-support.html) om du behöver hjälp.

#### Databasreplikering {#repository-replication}

Du kan behålla nyckelmaterialet som lagras i databasen, vilket var fallet i AEM 6.2 och tidigare, genom att ange följande systemegenskap vid första starten av varje AEM (som skapar den ursprungliga databasen):

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>Det är viktigt att verifiera att [replikeringsagenten på författaren](#replication-agents-on-author) är korrekt konfigurerad.

Med nyckelmaterialet som lagras i databasen replikeras krypteringsnyckeln från författaren till andra instanser på följande sätt:

Använda [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Bläddra till [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* Välj `/etc/key`
* Öppna fliken `Replication`
* Välj `Replicate`

* [uppdatera Granite Crypto-paketet](#refresh-the-granite-crypto-bundle)

![](../assets/replicare-repository.png)

#### Uppdatera Granite Crypto Bundle {#refresh-the-granite-crypto-bundle}

* Gå till [webbkonsolen](/help/sites-deploying/configuring-osgi.md) för varje publiceringsinstans

   * Till exempel [https://&lt;server>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* Hitta `Adobe Granite Crypto Support`-paketet (com.adobe.granite.crypto)
* Välj **Uppdatera**

![](../assets/refresh-granite-bundle.png)

* Efter en stund visas en **dialogruta** Slutfört:
   `Operation completed successfully.`

### Apache HTTP Server {#apache-http-server}

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

* AEM [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)-dokumentation
* [Installerar Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [Konfigurera Dispatcher för Communities](/help/communities/dispatcher.md)
* [Kända fel](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## Dokumentation för relaterade communities {#related-communities-documentation}

* Besök [Administrera communityplatser](/help/communities/administer-landing.md) om du vill veta mer om hur du skapar en community-webbplats, konfigurerar mallar för communitywebbplatser, modererar communityinnehåll, hanterar medlemmar och konfigurerar meddelanden.

* Besök [Utveckla communityn](/help/communities/communities.md) om du vill veta mer om ramverket för sociala komponenter (SCF) och hur du anpassar communitykomponenter och -funktioner.

* Gå till [Komponenter för redigeringsgrupper](/help/communities/author-communities.md) om du vill veta mer om hur du skapar med och konfigurerar webbgruppskomponenter.

