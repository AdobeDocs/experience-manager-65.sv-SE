---
title: Uppgradera steg för programserverinstallationer
seo-title: Uppgradera steg för programserverinstallationer
description: Lär dig hur du uppgraderar instanser av AEM som distribueras via programservrar.
seo-description: Lär dig hur du uppgraderar instanser av AEM som distribueras via programservrar.
uuid: e4020966-737c-40ea-bfaa-c63ab9a29cee
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 1876d8d6-bffa-4a1c-99c0-f6001acea825
docset: aem65
translation-type: tm+mt
source-git-commit: 38ef8fc8d80009c8ca79aca9e45cf10bd70e1f1e

---


# Uppgradera steg för programserverinstallationer{#upgrade-steps-for-application-server-installations}

I det här avsnittet beskrivs den procedur som måste följas för att uppdatera AEM för programserverinstallationer.

I alla exemplen i den här proceduren används JBoss som Application Server och du antyder att du har en fungerande version av AEM som redan är distribuerad. Proceduren är avsedd att dokumentera uppgraderingar som gjorts från **AEM version 5.6 till 6.3**.

1. Börja med JBoss. I de flesta fall kan du göra detta genom att köra `standalone.sh` startskriptet genom att köra det här kommandot från terminalen:

   ```shell
   jboss-install-folder/bin/standalone.sh
   ```

1. Om AEM 5.6 redan är distribuerat kontrollerar du att paketen fungerar som de ska genom att köra:

   ```shell
   wget https://<serveraddress:port>/cq/system/console/bundles
   ```

1. Avinstallera sedan AEM 5.6:

   ```shell
   rm jboss-install-folder/standalone/deployments/cq.war
   ```

1. Stoppa JBoss.

1. Nu kan du migrera databasen med hjälp av crx2oak-migreringsverktyget:

   ```shell
   java -jar crx2oak.jar crx-quickstart/repository/ crx-quickstart/oak-repository
   ```

   >[!NOTE]
   >
   >I det här exemplet är ekadatabas den tillfälliga katalog där den nyligen konverterade databasen finns. Kontrollera att du har den senaste versionen av crx2oak.jar innan du utför det här steget.

1. Ta bort de nödvändiga egenskaperna i filen sling.properties genom att göra följande:

   1. Öppna filen som finns på `crx-quickstart/launchpad/sling.properties`
   1. Stegtext Ta bort följande egenskaper och spara filen:

      1. `sling.installer.dir`

      1. `felix.cm.dir`

      1. `granite.product.version`

      1. `org.osgi.framework.system.packages`

      1. `osgi-core-packages`

      1. `osgi-compendium-services`

      1. `jre-*`

      1. `sling.run.mode.install.options`

1. Ta bort filer och mappar som inte längre behövs. De objekt du behöver ta bort är:

   * Startmappen **för** pad/startmapp. Du kan ta bort den genom att köra följande kommando i terminalen: `rm -rf crx-quickstart/launchpad/startup`

   * Filen **** base.jar: `find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * Filen **** BootstrapCommandFile_timestamp.txt: `rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

1. Kopiera det nyligen migrerade segmentlagret till rätt plats:

   ```shell
   mv crx-quickstart/oak-repository/segmentstore crx-quickstart/repository/segmentstore
   ```

1. Kopiera datalagret också:

   ```shell
   mv crx-quickstart/repository/repository/datastore crx-quickstart/repository/datastore
   ```

1. Därefter måste du skapa den mapp som ska innehålla de OSGi-konfigurationer som ska användas med den nya uppgraderade instansen. Mer specifikt måste en mapp med namnet install skapas under **crx-quickstart**.

1. Skapa nu nodarkivet och datalagret som ska användas med AEM 6.3. Du kan göra detta genom att skapa två filer med följande namn under **crx-quickstart\install**:

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`

   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`
   De här två filerna konfigurerar AEM att använda ett StarMK-nodarkiv och ett File-datalager.

1. Redigera konfigurationsfilerna så att de blir klara att användas. Mer specifikt:

   * Lägg till följande rad i **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**:\
      `customBlobStore=true`

   * Lägg sedan till följande rader i **org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config**:

      ```
      path=./crx-quickstart/repository/datastore
       minRecordLength=4096
      ```

1. Ta bort körningsläget crx2 genom att köra:

   ```shell
   find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf {} \
   ```

1. Nu måste du ändra körningslägena i AEM 6.3-krigsfilen. För att göra det skapar du först en tillfällig mapp som ska innehålla AEM 6.3-kriget. Namnet på mappen i det här exemplet blir **tillfälligt**. När krigsfilen har kopierats kan du extrahera innehållet genom att köra det inifrån den tillfälliga mappen:

   ```shell
   jar xvf aem-quickstart-6.3.0.war
   ```

1. När innehållet har extraherats går du till mappen **WEB-INF** och redigerar `web.xml` filen för att ändra körningslägena. Om du vill hitta platsen där de anges i XML söker du efter `sling.run.modes` strängen. När du har hittat den ändrar du körningslägena i nästa kodrad, som som standard är inställd på författare:

   ```shell
   <param-value >author</param-value>
   ```

1. Ändra ovanstående författarvärde och ställ in körningslägena på: author,crx3,crx3tar Det sista kodblocket ska se ut så här:

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. Återskapa behållaren med det ändrade innehållet:

   ```shell
   jar cvf aem62.war
   ```

1. Distribuera slutligen den nya krigsfilen:

   ```shell
   cp temp/aem62.war jboss-install-folder/standalone/deployments/aem61.war
   ```

