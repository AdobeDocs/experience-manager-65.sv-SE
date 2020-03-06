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
source-git-commit: 5035c9630b5e861f4386e1b5ab4f4ae7a8d26149

---


# Distribuera webbgrupper{#deploying-communities}

## Förutsättningar {#prerequisites}

* [AEM 6.5 Platform](/help/sites-deploying/deploy.md)

* AEM Communities-licens

* Valfria licenser för:

   * [Funktioner i Adobe Analytics for Communities](/help/communities/analytics.md)
   * [MongoDB för MSRP](/help/communities/msrp.md)
   * [Adobe Cloud för ASRP](/help/communities/asrp.md)

## Checklista för installation {#installation-checklist}

**För[AEM-plattformen](/help/sites-deploying/deploy.md#what-is-aem)**

* installera de senaste [AEM 6.5-uppdateringarna](#aem64updates)

* Om du inte använder standardportarna (4502, 4503) [konfigurerar du replikeringsagenter](#replication-agents-on-author)
* [replikera krypteringsnyckeln](#replicate-the-crypto-key)
* om det finns stöd för globalisering, [konfigurera automatisk översättning](/help/sites-administering/translation.md)(exempelinställningar tillhandahålls för utveckling)

**För[communityfunktionen](/help/communities/overview.md)**

* om du distribuerar en [publiceringsgrupp](/help/sites-deploying/recommended-deploys.md#tarmk-farm), [identifiera den primära utgivaren](#primary-publisher)

* [aktivera tunneltjänsten](#tunnel-service-on-author)
* [aktivera social inloggning](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [konfigurera Adobe Analytics](/help/communities/analytics.md)
* konfigurera en [standardtjänst för e-post](/help/communities/email.md)
* identifiera valet för [delad UGC-lagring](/help/communities/working-with-srp.md) (**SRP**)

   * om MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [installera och konfigurera MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [konfigurera Solr](/help/communities/solr.md)
      * [välj MSRP](/help/communities/srp-config.md)
   * om relationsdatabas SRP [(DSRP)](/help/communities/dsrp.md)

      * [installera JDBC-drivrutinen för MySQL](#jdbc-driver-for-mysql)
      * [installera och konfigurera MySQL för DSRP](/help/communities/dsrp-mysql.md)
      * [konfigurera Solr](/help/communities/solr.md)
      * [välj DSRP](/help/communities/srp-config.md)
   * om Adobe SRP [(ASRP)](/help/communities/asrp.md)

      * arbeta med din kontorepresentant för etablering
      * [välj ASRP](/help/communities/srp-config.md)
   * om JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * inte ett delat UGC-arkiv:

         * UGC replikeras aldrig
         * UGC är bara synligt på AEM-instansen eller klustret där det angavs
      * standard är JSRP
   För **[aktiveringsfunktionen](/help/communities/overview.md#enablement-community)**

   * [installera och konfigurera FFmpeg](/help/communities/ffmpeg.md)
   * [installera JDBC-drivrutinen för MySQL](#jdbc-driver-for-mysql)
   * [installera AEM Communities SCORM-Engine](#scorm-package)
   * [installera och konfigurera MySQL för aktivering](/help/communities/mysql.md)






## Senaste releaser {#latest-releases}

AEM 6.5 Communities GA levereras med Communities-paket. Om du vill veta mer om uppdateringar av AEM 6.5 [Communities](/help/release-notes/release-notes.md#experiencemanagercommunities)kan du läsa [AEM 6.5 Release Notes](/help/release-notes/release-notes.md#communities-release-notes.html).

### AEM 6.5 - uppdateringar {#aem-updates}

Från och med AEM 6.4 levereras uppdateringar av Communities som en del av AEM Cumulative Fix Packs och Service Packs.

De senaste uppdateringarna till AEM 6.5 finns i [Adobe Experience Manager 6.4 Cumulative Fix Packs och Service Packs](https://helpx.adobe.com/experience-manager/aem-releases-updates.html).

### Versionshistorik {#version-history}

Precis som med AEM 6.4 och senare är AEM Communities-funktioner och snabbkorrigeringar en del av AEM Communities kumulativa korrigeringspaket och servicepaket. Det finns därför inga separata funktionspaket.

### JDBC-drivrutin för MySQL {#jdbc-driver-for-mysql}

Två webbgruppsfunktioner använder en MySQL-databas:

* för [aktivering](/help/communities/enablement.md) : spela in SCORM-aktiviteter
* för [DSRP](/help/communities/dsrp.md) : lagra användargenererat innehåll (UGC)

MySQL-kopplingen måste hämtas och installeras separat.

De nödvändiga stegen är:

1. hämta ZIP-arkivet från [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * version måste vara >= 5.1.38

1. extrahera mysql-connector-java-&lt;version>-bin.jar (bundle) från arkivet
1. använda webbkonsolen för att installera och starta paketet:

   * till exempel https://localhost:4502/system/console/bundles
   * select **`Install/Update`**
   * Bläddra.. för att välja det paket som extraherats från det hämtade ZIP-arkivet
   * kontrollera att* JDBC-drivrutinen för Oracle Corporation för MySQLcom.mysql.jdbc* är aktiv och starta den om inte (eller kontrollera loggarna)

1. Om du installerar på en befintlig distribution efter att JDBC har konfigurerats, binder du om JDBC till den nya anslutningen genom att spara om JDBC-konfigurationen från webbkonsolen:

   * till exempel https://localhost:4502/system/console/configMgr
   * hitta `Day Commons JDBC Connections Pool` konfiguration
   * välj att öppna
   * select `Save`

1. Upprepa steg 3 och 4 för alla författare- och publiceringsinstanser

Mer information om hur du installerar paket finns på [webbkonsolsidan](/help/sites-deploying/web-console.md#bundles) .

#### Exempel: Installerat MySQL Connector-paket {#example-installed-mysql-connector-bundle}

![](/help/communities/assets/chlimage_1-125.png)

### SCORM-paket {#scorm-package}

SCORM (Shareable Content Object Reference Model) är en samling standarder och specifikationer för e-utbildning. SCORM definierar också hur innehåll kan paketeras i en överförbar ZIP-fil.

AEM Communities SCORM-motorn krävs för [aktiveringsfunktionen](/help/communities/overview.md#enablement-community) . SCORM-paket som stöds i AEM 6.5 Communities:

* [cq-social-scorm-package, version 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) som innehåller motorn [SCORM 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) .

**Installera ett SCORM-paket**

1. Installera [cq-social-scorm-paketet, version 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg)från paketresursen
1. Hämta `/libs/social/config/scorm/database_scormengine_data.sql` från cq-instansen och kör den på mysql-servern för att skapa ett uppgraderat scormEngineDB-schema.
1. Lägg till `/content/communities/scorm/RecordResults` i egenskapen Uteslutna sökvägar i CSRF-filter från`https://<hostname>:<port>/system/console/configMgr&#39; på utgivare.

#### SCORM-loggning {#scorm-logging}

Alla aktiveringsaktiviteter loggas utförligt på systemkonsolen, som de är installerade.

Om du vill kan du ställa in loggnivån på WARN för `RusticiSoftware.*` paketet.

Mer information om hur du arbetar med loggar finns i [Arbeta med granskningsposter och loggfiler](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files).

### AEM Advanced MLS {#aem-advanced-mls}

För att SRP-samlingen (MSRP eller DSRP) ska ha stöd för avancerad flerspråkig sökning (MLS) krävs nya Solr-plugin-program förutom ett anpassat schema och en Solr-konfiguration. Alla nödvändiga objekt paketeras i en nedladdningsbar zip-fil.

Den avancerade nedladdningen av MLS (kallas även &quot;phasetwo&quot;) finns tillgänglig från Adobe-databasen:

* [AEM-SOLR-MLS-phasetwo](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * version 1.2.40, 6 april 2016
   * ladda ned AEM-SOLR-MLS-phasetwo-1.2.40.zip

Mer information och installationsinformation finns på [Solr Configuration](/help/communities/solr.md) for SRP.

### Om länkar att paketera resurs {#about-links-to-package-share}

**Synliga paket i Adobe AEM Cloud**

Länkarna till paketen på den här sidan kräver ingen instans av AEM som körs eftersom de ska paketera delning på `adobeaemcloud.com`. Paketen kan visas, men `Install`knappen används för att installera paketen på en Adobe-värdplats. Om du tänker installera på en lokal AEM-instans `Install`uppstår ett fel om du väljer det.

**Installera på lokal AEM-instans**

Om du vill installera de paket som visas i `adobeaemcloud.com` en lokal AEM-instans måste paketet först hämtas till en lokal disk:

* välj fliken **Resurser**
* välj **Hämta till disk**

På den lokala AEM-instansen använder du pakethanteraren (till exempel [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/)) för att överföra till den lokala AEM-paketdatabasen.

Om du använder paketet med hjälp av paketresursen från den lokala AEM-instansen (till exempel [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)) hämtas `Download`knappen till den lokala AEM-instansens paketdatabas.

När du är i den lokala AEM-instansens paketdatabas använder du pakethanteraren för att installera paketet.

Mer information finns i [Arbeta med paket](/help/sites-administering/package-manager.md#package-share).

## Rekommenderade distributioner {#recommended-deployments}

I AEM Communities används en gemensam butik för att lagra användargenererat innehåll (UGC) och kallas ofta [lagringsresursleverantör (SRP)](/help/communities/working-with-srp.md). Rekommenderade distributionscenter när de väljer ett SRP-alternativ för den gemensamma butiken.

Den gemensamma lagringsplatsen stöder moderering av och analys av UGC i publiceringsmiljön samtidigt som behovet av [replikering](/help/communities/sync.md) av UGC elimineras.

* [Community Content Store](/help/communities/working-with-srp.md) : diskuterar SRP-lagringsalternativ för AEM-communities

* [Rekommenderade topologier](/help/communities/topologies.md) : diskuterar topologi som ska användas beroende på användningsfall och val av SRP

## Uppgraderar {#upgrading}

När du uppgraderar till AEM 6.5-plattformen från tidigare versioner av AEM är det viktigt att du läser [Uppgradera till AEM 6.5](/help/sites-deploying/upgrade.md).

Förutom att uppgradera plattformen kan du läsa [Uppgradera till AEM Communities 6.5](/help/communities/upgrade.md) för att få information om ändringar i Communities.

## Konfigurationer {#configurations}

### Primär utgivare {#primary-publisher}

När den valda distributionen är en [publiceringsgrupp](/help/communities/topologies.md#tarmk-publish-farm)måste en AEM-publiceringsinstans identifieras som **`primary publisher`** för aktiviteter som inte ska förekomma i alla instanser, till exempel funktioner som kräver **notifications **eller **Adobe Analytics**.

Som standard är `AEM Communities Publisher Configuration` OSGi-konfigurationen konfigurerad med kryssrutan **`Primary Publisher`** markerad, så att alla publiceringsinstanser i en publiceringsgrupp identifierar sig själva som primär.

Det är därför nödvändigt att **redigera konfigurationen för alla sekundära publiceringsinstanser** för att avmarkera **`Primary Publisher`** kryssrutan.

![](/help/communities/assets/chlimage_1-126.png)

För alla andra (sekundära) publiceringsinstanser i en publiceringsgrupp:

* logga in med administratörsbehörighet
* gå till [webbkonsolen](/help/sites-deploying/configuring-osgi.md)

   * till exempel [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* leta upp `AEM Communities Publisher Configuration`
* markera redigeringsikonen
* avmarkera rutan **Primär utgivare**
* välj **Spara**

### Replikeringsagenter på författare {#replication-agents-on-author}

Replikering används för webbplatsinnehåll som skapas i publiceringsmiljön, t.ex. communitygrupper, samt för att hantera medlemmar och medlemsgrupper från författarmiljön med hjälp av [tunneltjänsten](#tunnel-service-on-author).

För den primära utgivaren måste du se till att [replikeringsagentkonfigurationen](/help/sites-deploying/replication.md) identifierar publiceringsservern och den behöriga användaren korrekt. Den auktoriserade standardanvändaren har `admin,` redan rätt behörigheter (är medlem i `Communities Administrators`).

För att en annan användare ska ha rätt behörigheter måste de läggas till som medlem i `administrators` användargruppen (även som medlem i `Communities Administrators`).

Det finns två replikeringsagenter i författarmiljön som kräver att transportkonfigurationen är korrekt konfigurerad.

* få åtkomst till replikeringskonsolen på författaren

   * från global navigering: **Verktyg, Driftsättning, replikering, agenter på författaren**

* följer samma förfarande för båda agenterna:

   * **Standardagent (publicera)**
   * **Agenten för omvänd replikering (publicera omvänd)**

      1. välj agenten
      1. markera **redigering**
      1. välj fliken **Transport**
      1. om porten inte finns `4503`redigerar du **URI** för att ange rätt port

      1. om ingen användare `admin`finns, redigera **Användare** och **lösenord** för att ange en medlem i `administrators` användargruppen

I följande bilder visas resultatet av en ändring av porten från 4503 till 6103 med :

#### Standardagent (publicera) {#default-agent-publish}

![](/help/communities/assets/chlimage_1-127.png)

#### Agenten för omvänd replikering (publicera omvänd) {#reverse-replication-agent-publish-reverse}

![](/help/communities/assets/chlimage_1-128.png)

### Tunneltjänst på författare {#tunnel-service-on-author}

När du använder författarmiljön för att [skapa webbplatser](/help/communities/sites-console.md), [ändra webbplatsegenskaper](/help/communities/sites-console.md#modifying-site-properties) eller [hantera communitymedlemmar](/help/communities/members.md)måste du ha tillgång till medlemmar (användare) som är registrerade i publiceringsmiljön, inte användare som är registrerade på författaren.

Tunneltjänsten ger denna åtkomst med replikeringsagenten på författaren.

Så här aktiverar du tunneltjänsten:

* on **author**
* logga in med administratörsbehörighet
* Om utgivaren inte är lokal värd:4503 eller om transportanvändaren inte är det `admin`ska du [konfigurera replikeringsagenten](#replication-agents-on-author)

* åtkomst till [webbkonsolen](/help/sites-deploying/configuring-osgi.md)

   * till exempel [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* leta upp `AEM Communities Publish Tunnel Service`
* markera redigeringsikonen
* markera rutan **enable **box
* välj **Spara**

![](/help/communities/assets/chlimage_1-129.png)

### Replikera krypteringsnyckeln {#replicate-the-crypto-key}

Det finns två funktioner i AEM Communities som kräver att alla AEM-serverinstanser använder samma krypteringsnycklar. Dessa är [Analytics](/help/communities/analytics.md) och [ASRP](/help/communities/asrp.md).

Från och med AEM 6.3 lagras nyckelmaterialet i filsystemet och inte längre i databasen.

Om du vill kopiera nyckelmaterialet från författaren till alla andra instanser måste du:

* få tillgång till AEM-instansen, vanligtvis en författarinstans, som innehåller det nyckelmaterial som ska kopieras

   * hitta paketet i det lokala filsystemet, till exempel `com.adobe.granite.crypto.file`

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * filen `bundle.info` identifierar paketet
   * navigera till datamappen, till exempel

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * kopiera hmac- och mallfiler



* för varje AEM-målinstans

   * navigera till datamappen, till exempel

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * klistra in de två tidigare kopierade filerna
   * det är nödvändigt att [uppdatera Granite Crypto-paketet](#refresh-the-granite-crypto-bundle) om AEM-målinstansen körs


>[!CAUTION]
>
>Om en annan säkerhetsfunktion redan har konfigurerats som baseras på krypteringsnycklarna kan konfigurationen skadas om du replikerar krypteringsnycklarna. Om du behöver hjälp [kontaktar du kundtjänst](https://helpx.adobe.com/marketing-cloud/contact-support.html).

#### Databasreplikering {#repository-replication}

Att ha nyckelmaterialet lagrat i databasen, som var fallet i AEM 6.2 och tidigare, kan bevaras genom att ange följande systemegenskap vid första starten av varje AEM-instans (som skapar den ursprungliga databasen):

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>Det är viktigt att kontrollera att [replikeringsagenten på författaren](#replication-agents-on-author) är korrekt konfigurerad.

Med nyckelmaterialet som lagras i databasen replikeras krypteringsnyckeln från författaren till andra instanser på följande sätt:

Använda [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) :

* gå till [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* select `/etc/key`
* öppna `Replication` flik
* select `Replicate`

* [uppdatera Granite Crypto-paketet](#refresh-the-granite-crypto-bundle)

![](/help/communities/assets/chlimage_1-130.png)

#### Uppdatera Granite Crypto Bundle {#refresh-the-granite-crypto-bundle}

* Gå till [webbkonsolen för varje publiceringsinstans](/help/sites-deploying/configuring-osgi.md)

   * till exempel [https://&lt;server>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* locate `Adobe Granite Crypto Support` bundle (com.adobe.granite.crypto)
* välj **Uppdatera**

![](/help/communities/assets/chlimage_1-131.png)

* Efter ett ögonblick visas en **Success **dialog:
   `Operation completed successfully.`

### Apache HTTP-server {#apache-http-server}

Om du använder Apache HTTP-servern måste du använda rätt servernamn för alla relevanta poster.

Var särskilt försiktig med att använda rätt servernamn, inte `localhost`i `RedirectMatch`.

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

* AEM&#39;s [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) documentation
* [Installerar Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [Konfigurera Dispatcher för Communities](/help/communities/dispatcher.md)
* [Kända fel](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## Dokumentation för relaterade communities {#related-communities-documentation}

* Besök [Administrera communitysajter](/help/communities/administer-landing.md) om du vill veta mer om hur du skapar en community-webbplats, konfigurerar mallar för communitysajter, modererar communityinnehåll, hanterar medlemmar och konfigurerar meddelanden.

* Besök [Utvecklingsgrupper](/help/communities/communities.md) om du vill veta mer om ramverket för sociala komponenter (SCF) och hur du anpassar komponenter och funktioner i Communities.

* Besök [Authoring Communities Components](/help/communities/author-communities.md) om du vill veta mer om hur du skapar med och konfigurerar Communities-komponenter.

