---
title: Stöd för RDBMS i AEM 6.4
seo-title: RDBMS Support in AEM 6.4
description: Läs mer om stöd för relationsdatabasens beständighet i AEM 6.4 och de tillgängliga konfigurationsalternativen.
seo-description: Learn about the relational database persistence support in AEM 6.4 and the available configuration options.
uuid: c8422b0d-c6df-488d-bb6a-af92c9afda50
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6a754d42-da30-4c2f-8b9c-369e1f1f92b5
docset: aem65
feature: Configuring
exl-id: 1e34c5ca-9e08-4b2a-901c-ab28aeb4a807
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 0%

---

# Stöd för RDBMS i AEM 6.4{#rdbms-support-in-aem}

## Översikt {#overview}

Stöd för relationsdatabasbeständighet i AEM implementeras med Document Microkernel. Dokumentmikrokärnan är grunden som också används för implementering av MongoDB-beständighet.

Det består av ett Java-API som baseras på Mongo Java API. En implementering av ett BlobStore API ingår också. Bloggar lagras som standard i databasen.

Mer information om implementering finns i [RDBDocumentStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html) och [RDBBlobStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html) dokumentation.

>[!NOTE]
>
>Stöd för **PostgreSQL 9.4** tillhandahålls också, men endast för demoändamål. Den kommer inte att vara tillgänglig för produktionsmiljöer.

## Databaser som stöds {#supported-databases}

Mer information om nivån på Relational Database-stöd i AEM finns i [sidan Tekniska krav](/help/sites-deploying/technical-requirements.md).

## Konfigurationssteg {#configuration-steps}

Databasen skapas genom att `DocumentNodeStoreService` OSGi-tjänst. Det har utökats med stöd för relationsdatabasbeständighet utöver MongoDB.

För att en datakälla ska fungera måste den konfigureras med AEM. Detta görs via `org.apache.sling.datasource.DataSourceFactory.config` -fil. JDBC-drivrutinerna för respektive databas måste anges separat som OSGi-paket i den lokala konfigurationen.

Anvisningar om hur du skapar OSGi-paket för JDBC-drivrutiner finns i detta [dokumentation](https://sling.apache.org/documentation/bundles/datasource-providers.html#convert-driver-jars-to-bundle) på webbplatsen Apache Sling.

När paketen är på plats följer du stegen nedan för att konfigurera AEM med RDB-beständighet:

1. Kontrollera att databasdaemon har startats och att du har en aktiv databas som kan användas med AEM.
1. Kopiera AEM 6.3 burk till installationskatalogen.
1. Skapa en mapp med namnet `crx-quickstart\install` i installationskatalogen.
1. Konfigurera dokumentnodarkivet genom att skapa en konfigurationsfil med följande namn i `crx-quickstart\install` katalog:

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. Konfigurera datakällan och JDBC-parametrarna genom att skapa en annan konfigurationsfil med följande namn i `crx-quickstart\install` mapp:

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`
   >[!NOTE]
   >
   >Detaljerad information om datakällkonfigurationen för varje databas som stöds finns i [Konfigurationsalternativ för datakälla](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options).

1. Förbered sedan JDBC OSGi-paketen som ska användas med AEM:

   1. I `crx-quickstart/install` mapp, skapa en mapp med namnet `9`.

   1. Placera JDBC-behållaren i den nya mappen.

1. Till sist AEM du med `crx3` och `crx3rdb` runmodes:

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## Konfigurationsalternativ för datakälla {#data-source-configuration-options}

The `org.apache.sling.datasource.DataSourceFactory-oak.config` OSGi-konfigurationen används för att konfigurera de parametrar som behövs för kommunikation mellan AEM och databasens beständighetslager.

Följande konfigurationsalternativ är tillgängliga:

* `datasource.name:` Datakällans namn. Standardvärdet är `oak`.

* `url:` URL-strängen för den databas som ska användas med JDBC. Varje databastyp har ett eget URL-strängformat. Mer information finns på [URL-strängformat](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats) nedan.

* `driverClassName:` Klassnamnet för JDBC-drivrutinen. Detta varierar beroende på vilken databas du vill använda och därefter vilken drivrutin som behövs för att ansluta till den. Nedan visas klassnamnen för alla databaser som stöds av AEM:

   * `org.postgresql.Driver` för PostgreSQL,
   * `com.ibm.db2.jcc.DB2Driver` för DB2,
   * `oracle.jdbc.OracleDriver` för Oracle,
   * `com.mysql.jdbc.Driver` MySQL och MariaDB (experimentell);
   * c `om.microsoft.sqlserver.jdbc.SQLServerDriver` för Microsoft SQL Server (experimentell).

* `username:` Användarnamnet som databasen körs under.

* `password:` Databaslösenordet.

### URL-strängformat {#url-string-formats}

Ett annat URL-strängformat används i datakällkonfigurationen beroende på vilken databastyp som ska användas. Nedan visas en lista över format för de databaser som AEM för närvarande stöder:

* `jdbc:postgresql:databasename` för PostgreSQL,
* `jdbc:db2://localhost:port/databasename` för DB2,
* `jdbc:oracle:thin:localhost:port:SID` för Oracle,
* `jdbc:mysql://localhost:3306/databasename` MySQL och MariaDB (experimentell);
* `jdbc:sqlserver://localhost:1453;databaseName=name` för Microsoft SQL Server (experimentell).

## Kända begränsningar {#known-limitations}

Samtidigt bruk av flera AEM-instanser med en databas stöds av RDBMS-beständighet, men inte samtidiga installationer.

För att undvika detta måste du först köra installationen med en enda medlem och lägga till de andra efter att den första installationen är klar.
