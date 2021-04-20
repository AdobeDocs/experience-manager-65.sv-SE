---
title: Utföra en uppgradering på plats
seo-title: Utföra en uppgradering på plats
description: Lär dig hur du utför en uppgradering på plats.
seo-description: Lär dig hur du utför en uppgradering på plats.
uuid: 478cb9db-1ea8-4bdb-b333-411dcbf2d927
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: fcb17227-ff1f-4b47-ae94-6b7f60923876
docset: aem65
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1276'
ht-degree: 0%

---


# Utföra en uppgradering på plats{#performing-an-in-place-upgrade}

>[!NOTE]
>
>På den här sidan beskrivs uppgraderingsproceduren för AEM 6.5. Om du har en installation som distribueras till en programserver läser du [Uppgradera steg för programserverinstallationer](/help/sites-deploying/app-server-upgrade.md).

## Steg före uppgradering {#pre-upgrade-steps}

Innan du utför uppgraderingen måste du utföra flera steg. Mer information finns i [Uppgradera kod och anpassningar](/help/sites-deploying/upgrading-code-and-customizations.md) och [Underhållsaktiviteter före uppgradering](/help/sites-deploying/pre-upgrade-maintenance-tasks.md). Kontrollera dessutom att datorn uppfyller kraven för den nya versionen av AEM. Se hur Mönsteravkännare kan hjälpa dig att beräkna uppgraderingens komplexitet och se även avsnittet Upgrade Scope och Requirements i [Planera din uppgradering](/help/sites-deploying/upgrade-planning.md) för mer information.

<!--Finally, note that the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## Migreringskrav {#migration-prerequisites}

* **Minimikrav för Java-version:** Migreringsverktyget fungerar bara med Java-version 7 och senare. Observera att för AEM 6.3 och senare är Oraclets JRE 8 och IBM:s JRE 7 och 8 de enda versionerna som stöds.

* **Uppgraderad instans:** Om du uppgraderar från en version som är  **äldre än 5.6** bör du kontrollera att du har utfört en på plats-uppgradering till AEM 6.0 genom att följa proceduren som beskrivs i version 6.0 av uppgraderingsdokumentationen.

## Förberedelse av AEM Quickstart jar-filen {#prep-quickstart-file}

1. Stoppa instansen om den körs.

1. Ladda ned den nya AEM jar-filen och använd den för att ersätta den gamla filen utanför `crx-quickstart`-mappen.

1. Packa upp den nya snabbstartsburken genom att köra:

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

## Migrering av innehållsdatabas {#content-repository-migration}

Migreringen krävs inte om du uppgraderar från AEM 6.3. För versioner som är äldre än 6.3 tillhandahåller Adobe ett verktyg som kan användas för att migrera databasen till den nya versionen av den eksegmentstjärna som finns i AEM 6.3. Det ingår som en del av snabbstartspaketet och är obligatoriskt för alla uppgraderingar som ska använda tarMK. Uppgraderingar för miljöer där MongoMK används kräver inte databasmigrering. Mer information om fördelarna med det nya segmenttjärformatet finns i [Vanliga frågor och svar om migrering till eksegmenttjära](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

Den faktiska migreringen utförs med AEM snabbredigeringsfil, som körs med ett nytt `-x crx2oak`-alternativ som kör crx2oak-verktyget för att förenkla uppgraderingen och göra den mer robust.

>[!NOTE]
>
>Om du utför Innehållsmigrering för en TjärMK-databas med tillägget CRX2Oak QuickStart kan du ta bort körläget **sampling content** genom att lägga till följande på migreringskommandoraden:
>
>* `--promote-runmode nosamplecontent`

>



Använd följande kommando för att bestämma vilket kommando du ska köra:

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

Där `<<YOUR_PROFILE>>` och `<<ADDITIONAL_FLAGS>>` ersätts med profilen och flaggorna i följande tabell:

<table>
 <tbody>
  <tr>
   <td><strong>Källdatabas</strong></td>
   <td><strong>Måldatabas</strong></td>
   <td><strong>Profil</strong></td>
   <td><strong>Ytterligare flaggor</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2 eller tarMK med <code>FileDataStore</code></td>
   <td>tarMK</td>
   <td>segment-fds</td>
   <td>Se avsnittet Felsökning nedan</td>
  </tr>
  <tr>
   <td>crx2</td>
   <td>MongoMK</td>
   <td>mongo-from-crx2 </td>
   <td><code>-T mongo-uri=mongo://mongo-host:mongo-port -T mongo-db=mongo-database-name</code></td>
  </tr>
  <tr>
   <td>tarMK eller crx2 med <code>S3DataStore</code></td>
   <td>tarMK</td>
   <td>segment-custom-ds</td>
   <td>Se avsnittet Felsökning nedan</td>
  </tr>
  <tr>
   <td>tarMK utan datastore</td>
   <td>tarMK</td>
   <td>segment-no-ds</td>
   <td> </td>
  </tr>
  <tr>
   <td>MongoMK</td>
   <td>MongoMK</td>
   <td>Ingen migrering behövs</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**Var:**

* `mongo-host` är MongoDB-serverns IP-adress (till exempel 127.0.0.1)

* `mongo-port` är MongoDB-serverporten (till exempel: 27017)

* `mongo-database-name` representerar databasens namn (till exempel: aem-author)

**Du kan också behöva ytterligare växlar för följande scenarier:**

* Om du utför uppgraderingen på en Windows-dator där Java-minnesmappningen inte hanteras på rätt sätt lägger du till parametern `--disable-mmap` i kommandot.

* Om du använder Java 7 lägger du till parametern `-XX:MaxPermSize=2048m` precis efter parametern `-Xmx`.

Mer information om hur du använder crx2oak-verktyget finns i Använda [CRX2Oak Migration Tool](/help/sites-deploying/using-crx2oak.md). JAR-hjälpfilen för crx2oak kan vid behov uppgraderas manuellt genom att manuellt ersätta den med senare versioner efter att snabbstarten har packats upp. Sökvägen i AEM installationsmapp är: `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. Den senaste versionen av CRX2Oak-migreringsverktyget kan hämtas från Adobe-databasen på: [https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/)

Om migreringen har slutförts avslutas verktyget med en avslutningskod på noll. Kontrollera dessutom om det finns WARN- och ERROR-meddelanden i filen `upgrade.log`, som finns under `crx-quickstart/logs` i AEM installationskatalog, eftersom dessa kan tyda på icke-allvarliga fel som uppstod under migreringen.

Kontrollera konfigurationsfilerna under mappen `crx-quickstart/install`. Om en migrering var nödvändig kommer dessa att uppdateras för att återspegla måldatabasen.

**En anteckning om datalager:**

`FileDataStore` är det nya standardvärdet för AEM 6.3-installationer, men det krävs inte att ett externt datalager används. Även om du bör använda ett externt datalager som bästa praxis för produktionsdistributioner är det inte en förutsättning för uppgradering. På grund av den komplexitet som redan finns vid uppgradering av AEM rekommenderar vi att du utför uppgraderingen utan att behöva göra en datastrimmigrering. Om du vill kan du utföra en datalagermigrering efteråt som en separat åtgärd.

## Felsöka migreringsproblem {#troubleshooting-migration-issues}

Hoppa över det här avsnittet om du uppgraderar från 6.3. De tillhandahållna crx2oak-profilerna bör tillgodose behoven hos de flesta kunder, men det finns tillfällen då ytterligare parametrar behövs. Om ett fel inträffar under migreringen kan det finnas aspekter av miljön som kräver ytterligare konfigurationsalternativ. I så fall kommer du förmodligen att få följande fel:

**Kontrollpunkter kopieras inte eftersom inget externt datalager har angetts. Detta resulterar i att hela databasen indexeras om första gången du startar. Använd —skip-checkpoints för att framtvinga migreringen eller läs https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration för mer information.**

Av någon anledning behöver migreringsprocessen åtkomst till binärfiler i datalagret och kan inte hitta den. Om du vill ange din datalagerkonfiguration inkluderar du följande flaggor i `<<ADDITIONAL_FLAGS>>`-delen av ditt migreringskommando:

**För S3-datastorer:**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

Där `/path/to/SharedS3DataStore.config` representerar sökvägen till S3-datalagrets konfigurationsfil och `/path/to/datastore` representerar sökvägen till S3-datalagret.

**För fildatalager:**

```shell
--src-datastore=/path/to/datastore
```

Där `/path/to/datastore` representerar sökvägen till File DataStore.

## Utför uppgraderingen {#performing-the-upgrade}

**Om du använder S3:**

1. Ta bort alla tecken under `crx-quickstart/install` som är associerade med en tidigare version av S3-kopplingen.

1. Hämta den senaste versionen av 1.10.x S3-anslutningen från [https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/)

1. Extrahera paketet till en tillfällig mapp och kopiera innehållet i `jcr_root/libs/system/install` till mappen `crx-quickstart/install`.

### Kontrollera rätt startkommando för uppgradering {#determining-the-correct-upgrade-start-command}

För att kunna genomföra uppgraderingen är det viktigt att du börjar AEM använda filen jar för att ta fram instansen. Om du vill uppgradera till 6.5 kan du även läsa andra alternativ för innehållsomstrukturering och migrering i [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md) som du kan välja med uppgraderingskommandot.

>[!IMPORTANT]
>
>Om du kör Oracle Java 11 (eller i allmänhet versioner av Java nyare än 8) måste ytterligare växlar läggas till på kommandoraden när du startar AEM. Mer information finns i [Java 11 Considerations](/help/sites-deploying/custom-standalone-install.md#java-considerations).

Observera att AEM från startskriptet inte startar uppgraderingen. De flesta kunder börjar AEM med startskriptet och har anpassat det här startskriptet för att inkludera växlar för miljökonfigurationer som minnesinställningar, säkerhetscertifikat osv. Därför rekommenderar vi att du följer den här proceduren för att fastställa rätt uppgraderingskommando:

1. Kör följande från kommandoraden på en AEM som körs:

   ```shell
   ps -ef | grep java
   ```

1. Leta efter AEM. Det ser ut ungefär så här:

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.2.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. Ändra kommandot genom att ersätta sökvägen till den befintliga burken ( `crx-quickstart/app/aem-quickstart*.jar` i det här fallet) med den nya burken som är jämställd med mappen `crx-quickstart`. Om du använder vårt tidigare kommando som exempel blir vårt kommando:

   ```shell
   /usr/bin/java -server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar cq-quickstart-6.5.0.jar -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   Detta säkerställer att alla korrekta minnesinställningar, anpassade körningssätt och andra miljöparametrar används för uppgraderingen. När uppgraderingen har slutförts kan instansen startas från startskriptet vid framtida starter.

## Distribuera uppgraderad kodbas {#deploy-upgraded-codebase}

När uppgraderingsprocessen på plats har slutförts ska den uppdaterade kodbasen distribueras. Steg för att uppdatera kodbasen så att den fungerar i målversionen av AEM finns på [sidan Uppgraderingskod och anpassningar](/help/sites-deploying/upgrading-code-and-customizations.md).

## Utför efteruppgraderingskontroller och felsökning {#perform-post-upgrade-check-troubleshooting}

Se [Efterbelys uppgraderingskontroller och felsökning](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).
