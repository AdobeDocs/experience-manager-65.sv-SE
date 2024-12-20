---
title: MySQL-konfiguration för DSRP
description: Ansluta till MySQL-servern och upprätta UGC-databasen
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: eafb60be-2963-4ac9-8618-50fd9bc6fe6c
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# MySQL-konfiguration för DSRP {#mysql-configuration-for-dsrp}

MySQL är en relationsdatabas som kan användas för att lagra användargenererat innehåll.

Dessa instruktioner beskriver hur du ansluter till MySQL-servern och skapar UGC-databasen.

## Krav {#requirements}

* [Funktionspaket för senaste webbgrupper](deploy-communities.md#latestfeaturepack)
* [JDBC-drivrutin för MySQL](deploy-communities.md#jdbc-driver-for-mysql)
* En relationsdatabas:

   * [MySQL-server](https://dev.mysql.com/downloads/mysql/) Community Server version 5.6 eller senare

      * Kan köras på samma värd som AEM eller fjärrköras

   * [MySQL-workbench](https://dev.mysql.com/downloads/tools/workbench/)

## Installerar MySQL {#installing-mysql}

[MySQL](https://dev.mysql.com/downloads/mysql/) ska hämtas och installeras enligt instruktionerna för måloperativsystemet.

### Tabellnamn med gemener {#lower-case-table-names}

Eftersom SQL inte är skiftlägeskänsligt måste du, för skiftlägeskänsliga operativsystem, inkludera en inställning som anger alla tabellnamn med gemener.

Om du till exempel vill ange alla tabellnamn med gemener i ett Linux-operativsystem:

* Redigera filen `/etc/my.cnf`
* Lägg till följande rad i avsnittet `[mysqld]`:

  `lower_case_table_names = 1`

### UTF8-teckenuppsättning {#utf-character-set}

För att få bättre stöd för flera språk måste du använda teckenuppsättningen UTF8.

Ändra MySQL till att ha UTF8 som teckenuppsättning:

* mysql > SET NAME &#39;utf8&#39;;

Ändra MySQL-databasen till standard till UTF8:

* Redigera filen `/etc/my.cnf`
* Lägg till följande rad i avsnittet `[client]`:

  `default-character-set=utf8`

* Lägg till följande rad i avsnittet `[mysqld]`:

  `character-set-server=utf8`

## Installerar MySQL Workbench {#installing-mysql-workbench}

MySQL Workbench tillhandahåller ett gränssnitt för körning av SQL-skript som installerar schemat och initiala data.

MySQL Workbench ska laddas ned och installeras enligt instruktionerna för måloperativsystemet.

## Communities-anslutning {#communities-connection}

När MySQL Workbench startas första gången visas inga anslutningar, såvida den inte redan används för andra syften:

![mysqlconnection](assets/mysqlconnection.png)

### Nya anslutningsinställningar {#new-connection-settings}

1. Välj ikonen `+` till höger om `MySQL Connections`.
1. Ange värden som passar din plattform i dialogrutan `Setup New Connection`

   I demonstrationssyfte med författarinstansen AEM och MySQL på samma server:

   * Anslutningsnamn: `Communities`
   * Anslutningsmetod: `Standard (TCP/IP)`
   * Värdnamn: `127.0.0.1`
   * Användarnamn: `root`
   * Lösenord: `no password by default`
   * Standardschema: `leave blank`

1. Välj `Test Connection` för att verifiera anslutningen till den MySQL-tjänst som körs

**Anteckningar**:

* Standardporten är `3306`
* Det valda anslutningsnamnet anges som datakällans namn i [JDBC OSGi-konfigurationen](#configurejdbcconnections)

#### Ny webbgruppsanslutning {#new-communities-connection}

![community-connection](assets/community-connection.png)

## Databasinställningar {#database-setup}

Öppna Communities-anslutningen för att installera databasen.

![install-database](assets/install-database.png)

### Hämta SQL-skriptet {#obtain-the-sql-script}

SQL-skriptet hämtas från AEM:

1. Bläddra till CRXDE Lite

   * Exempel: [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. Välj mappen /libs/social/config/datastore/dsrp/schema
1. Hämta `init-schema.sql`

   ![database-schema-crxde](assets/database-schema-crxde.png)

En metod för att hämta schemat är:

* Välj noden `jcr:content` för SQL-filen
* Observera att värdet för egenskapen `jcr:data` är en vylänk

* Markera vylänken om du vill spara data i en lokal fil

### Skapa DSRP-databasen {#create-the-dsrp-database}

Installera databasen genom att följa stegen nedan. Databasens standardnamn är `communities`.

Om databasnamnet ändras i skriptet måste du även ändra det i [JDBC-konfigurationen](#configurejdbcconnections).

#### Steg 1: öppna SQL-fil {#step-open-sql-file}

I MySQL Workbench

* Välj alternativet **[!UICONTROL Open SQL Script]** på menyn Arkiv
* Välj det hämtade `init_schema.sql`-skriptet

![select-sql-script](assets/select-sql-script.png)

#### Steg 2: kör SQL Script {#step-execute-sql-script}

I Workbench-fönstret för filen som öppnas i steg 1 väljer du `lightening (flash) icon` för att köra skriptet.

I följande bild är filen `init_schema.sql` klar att köras:

![execute-sql-script](assets/execute-sql-script.png)

#### Uppdatera {#refresh}

När skriptet har körts måste du uppdatera avsnittet `SCHEMAS` i `Navigator` för att se den nya databasen. Använd uppdateringsikonen till höger om SCHEMAS:

![refresh-schema](assets/refresh-schema.png)

## Konfigurera JDBC-anslutning {#configure-jdbc-connection}

OSGi-konfigurationen för **Day Commons JDBC Connections Pool** konfigurerar MySQL JDBC-drivrutinen.

Alla publicerings- och författarinstanser AEM peka på samma MySQL-server.

När MySQL körs på en annan server än AEM måste servervärdnamnet anges i stället för localhost i JDBC-kopplingen.

* På varje författare och publicera AEM.
* Inloggad med administratörsbehörighet.
* Gå till [webbkonsolen](../../help/sites-deploying/configuring-osgi.md).

   * Exempel: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* Hitta `Day Commons JDBC Connections Pool`
* Välj ikonen `+` om du vill skapa en anslutningskonfiguration.

  ![configure-jdbc-connection](assets/configure-jdbc-connection.png)

* Ange följande värden:

   * **[!UICONTROL JDBC driver class]**: `com.mysql.jdbc.Driver`
   * **[!UICONTROL JDBC connection URI]**: `jdbc:mysql://localhost:3306/communities?characterEncoding=UTF-8`

     Ange en server i stället för localhost om MySQL-servern inte är densamma som &#39;this&#39; AEM servern *communities* är standarddatabasens (schemats) namn.

   * **[!UICONTROL Username]**: `root`

     Eller ange det konfigurerade användarnamnet för MySQL-servern, om inte &#39;root&#39;.

   * **[!UICONTROL Password]**:

     Rensa det här fältet om inget lösenord har angetts för MySQL,

     I annat fall anger du det konfigurerade lösenordet för MySQL-användarnamnet.

   * **[!UICONTROL Datasource name]**: namn angivet för [MySQL-anslutningen](#new-connection-settings), till exempel &#39;communities&#39;.

* Välj **[!UICONTROL Save]**
