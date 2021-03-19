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
feature: Uppgraderar
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---


# Uppgradera steg för programserverinstallationer{#upgrade-steps-for-application-server-installations}

I det här avsnittet beskrivs den procedur som måste följas för att uppdatera AEM för programserverinstallationer.

I alla exemplen i den här proceduren används Tomcat som Application Server och du antyder att du har en fungerande version av AEM redan distribuerad. Proceduren är avsedd att dokumentera uppgraderingar som utförts från **AEM version 6.4 till 6.5**.

1. Börja med TomCat. I de flesta fall kan du göra detta genom att köra startskriptet `./catalina.sh` genom att köra det här kommandot från terminalen:

   ```shell
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. Om AEM 6.4 redan är distribuerad kontrollerar du att paketen fungerar korrekt genom att gå till:

   ```shell
   https://<serveraddress:port>/cq/system/console/bundles
   ```

1. Avinstallera sedan AEM 6.4. Detta kan du göra med TomCat App Manager (`http://serveraddress:serverport/manager/html`)

1. Nu kan du migrera databasen med hjälp av crx2oak-migreringsverktyget. Om du vill göra det hämtar du den senaste versionen av crx2oak från [den här platsen](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak).

   ```shell
   SLING_HOME= $AEM-HOME/crx-quickstart java -Xmx4096m -XX:MaxPermSize=2048M -jar crx2oak.jar --load-profile segment-fds
   ```

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

   * Mappen **launchpad/startup**. Du kan ta bort den genom att köra följande kommando i terminalen: `rm -rf crx-quickstart/launchpad/startup`

   * Filen **base.jar**: `find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * Filen **BootstrapCommandFile_timestamp.txt**: `rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

   * Ta bort **sling.options.file** genom att köra: `find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf`

1. Skapa nu nodarkivet och datalagret som ska användas med AEM 6.5. Du kan göra detta genom att skapa två filer med följande namn under `crx-quickstart\install`:

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`
   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   De här två filerna konfigurerar AEM att använda ett StarMK-nodarkiv och ett File-datalager.

1. Redigera konfigurationsfilerna så att de blir klara att användas. Mer specifikt:

   * Lägg till följande rad i `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`:

      ```customBlobStore=true```

   * Lägg sedan till följande rader i `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`:

      ```
      path=./crx-quickstart/repository/datastore
      minRecordLength=4096
      ```

1. Nu måste du ändra körningslägena i AEM 6.5-filen. För att göra det skapar du först en tillfällig mapp som ska rymma AEM 6.5-kriget. Namnet på mappen i det här exemplet är `temp`. När krigsfilen har kopierats kan du extrahera innehållet genom att köra det inifrån den tillfälliga mappen:

   ```
   jar xvf aem-quickstart-6.5.0.war
   ```

1. När innehållet har extraherats går du till mappen **WEB-INF** och redigerar filen web.xml och ändrar körningslägena. Om du vill hitta platsen där de anges i XML söker du efter strängen `sling.run.modes`. När du har hittat den ändrar du körningslägena i nästa kodrad, som som standard är inställd på författare:

   ```bash
   <param-value >author</param-value>
   ```

1. Ändra ovanstående författarvärde och ställ in körningslägena på: `author,crx3,crx3tar`. Det sista kodblocket ska se ut så här:

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. Återskapa behållaren med det ändrade innehållet:

   ```bash
   jar cvf aem65.war
   ```

1. Distribuera slutligen den nya krigsfilen i TomCat.
