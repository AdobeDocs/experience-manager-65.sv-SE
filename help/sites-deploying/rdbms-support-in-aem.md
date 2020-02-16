---
title: Stöd för RDBMS i AEM 6.4
seo-title: Stöd för RDBMS i AEM 6.4
description: Lär dig mer om relationsdatabasens beständighetsstöd i AEM 6.4 och de tillgängliga konfigurationsalternativen.
seo-description: Lär dig mer om relationsdatabasens beständighetsstöd i AEM 6.4 och de tillgängliga konfigurationsalternativen.
uuid: c8422b0d-c6df-488d-bb6a-af92c9afda50
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6a754d42-da30-4c2f-8b9c-369e1f1f92b5
docset: aem65
translation-type: tm+mt
source-git-commit: 38ef8fc8d80009c8ca79aca9e45cf10bd70e1f1e

---


# Stöd för RDBMS i AEM 6.4{#rdbms-support-in-aem}

## Översikt {#overview}

Stöd för relationsdatabasbeständighet i AEM implementeras med Document Microkernel. Dokumentmikrokärnan är grunden som också används för implementering av MongoDB-beständighet.

Det består av ett Java-API som baseras på Mongo Java API. En implementering av ett BlobStore API ingår också. Bloggar lagras som standard i databasen.

Mer information om implementeringen finns i dokumentationen för [RDBDocumentStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html) och [RDBBlobStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html) .

>[!NOTE]
>
>Stöd för **PostgreSQL 9.4** ges också, men endast för demoändamål. Den kommer inte att vara tillgänglig för produktionsmiljöer.

## Databaser som stöds {#supported-databases}

Mer information om nivån på Relational Database-stödet i AEM finns på sidan [](/help/sites-deploying/technical-requirements.md)Tekniska krav.

## Konfigurationssteg {#configuration-steps}

Databasen skapas genom att `DocumentNodeStoreService` OSGi-tjänsten konfigureras. Det har utökats med stöd för relationsdatabasbeständighet utöver MongoDB.

För att en datakälla ska fungera måste den konfigureras med AEM. Detta görs via `org.apache.sling.datasource.DataSourceFactory.config` filen. JDBC-drivrutinerna för respektive databas måste anges separat som OSGi-paket i den lokala konfigurationen.

Anvisningar om hur du skapar OSGi-paket för JDBC-drivrutiner finns i den här [dokumentationen](https://sling.apache.org/documentation/bundles/datasource-providers.html#convert-driver-jars-to-bundle) på webbplatsen Apache Sling.

När paketen är på plats följer du stegen nedan för att konfigurera AEM med RDB-beständighet:

1. Kontrollera att databasdaemon har startats och att du har en aktiv databas som kan användas med AEM.
1. Kopiera AEM 6.3 jar till installationskatalogen.
1. Skapa en mapp som anropas `crx-quickstart\install` i installationskatalogen.
1. Konfigurera dokumentnodarkivet genom att skapa en konfigurationsfil med följande namn i `crx-quickstart\install` katalogen:

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. Konfigurera datakällan och JDBC-parametrarna genom att skapa en annan konfigurationsfil med följande namn i `crx-quickstart\install` mappen:

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`
   >[!NOTE]
   >
   >Mer information om datakällkonfigurationen för varje databas som stöds finns i Konfigurationsalternativ för [datakälla](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options).

1. Förbered sedan JDBC OSGi-paketen som ska användas med AEM:

   1. Skapa en mapp med namnet i `crx-quickstart/install` mappen `9`.

   1. Placera JDBC-behållaren i den nya mappen.

1. Slutligen startar du AEM med `crx3` - och `crx3rdb` runmodes:

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## Konfigurationsalternativ för datakälla {#data-source-configuration-options}

OSGi- `org.apache.sling.datasource.DataSourceFactory-oak.config` konfigurationen används för att konfigurera de parametrar som behövs för kommunikation mellan AEM och databasens beständighetslager.

Följande konfigurationsalternativ är tillgängliga:

* `datasource.name:` Datakällans namn. The default is `oak`.

* `url:` URL-strängen för den databas som ska användas med JDBC. Varje databastyp har ett eget URL-strängformat. Mer information finns i [URL-strängformat](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats) nedan.

* `driverClassName:` Klassnamnet för JDBC-drivrutinen. Detta varierar beroende på vilken databas du vill använda och därefter vilken drivrutin som behövs för att ansluta till den. Nedan visas klassnamnen för alla databaser som stöds av AEM:

   * `org.postgresql.Driver` för PostgreSQL,
   * `com.ibm.db2.jcc.DB2Driver` för DB2,
   * `oracle.jdbc.OracleDriver` för Oracle,
   * `com.mysql.jdbc.Driver` MySQL och MariaDB (experimentell);
   * c `om.microsoft.sqlserver.jdbc.SQLServerDriver` för Microsoft SQL Server (experimentell).

* `username:` Användarnamnet som databasen körs under.

* `password:` Databaslösenordet.

### URL-strängformat {#url-string-formats}

Ett annat URL-strängformat används i datakällkonfigurationen beroende på vilken databastyp som ska användas. Nedan finns en lista över format för de databaser som AEM stöder:

* `jdbc:postgresql:databasename` för PostgreSQL,
* `jdbc:db2://localhost:port/databasename` för DB2,
* `jdbc:oracle:thin:localhost:port:SID` för Oracle,
* `jdbc:mysql://localhost:3306/databasename` MySQL och MariaDB (experimentell);
* `jdbc:sqlserver://localhost:1453;databaseName=name` för Microsoft SQL Server (experimentell).

## Kända begränsningar {#known-limitations}

Samtidigt bruk av flera AEM-instanser med en databas stöds av RDBMS-persistence, men inte samtidiga installationer.

För att undvika detta måste du först köra installationen med en enda medlem och lägga till de andra efter att den första installationen är klar.

