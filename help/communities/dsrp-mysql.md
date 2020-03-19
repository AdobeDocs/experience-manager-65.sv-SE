---
title: MySQL-konfiguration för DSRP
seo-title: MySQL-konfiguration för DSRP
description: Ansluta till MySQL-servern och upprätta UGC-databasen
seo-description: Ansluta till MySQL-servern och upprätta UGC-databasen
uuid: c058cc88-7ca2-4aed-9a36-b080e603f886
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: edc3043c-7ec4-4e4a-b008-95f1784f012e
translation-type: tm+mt
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---


# MySQL-konfiguration för DSRP {#mysql-configuration-for-dsrp}

MySQL är en relationsdatabas som kan användas för att lagra användargenererat innehåll (UGC).

Dessa instruktioner beskriver hur du ansluter till MySQL-servern och skapar UGC-databasen.

## Krav {#requirements}

* [senaste webbgruppsfunktionspaket](deploy-communities.md#latestfeaturepack)
* [JDBC-drivrutin för MySQL](deploy-communities.md#jdbc-driver-for-mysql)
* En relationsdatabas:

   * [MySQL server](https://dev.mysql.com/downloads/mysql/) Community Server version 5.6 eller senare

      * Kan köras på samma värd som AEM eller fjärrköras
   * [MySQL Workbench](https://dev.mysql.com/downloads/tools/workbench/)


## Installerar MySQL {#installing-mysql}

[MySQL](https://dev.mysql.com/downloads/mysql/) ska laddas ned och installeras enligt instruktionerna för måloperativsystemet.

### Tabellnamn med gemener {#lower-case-table-names}

Eftersom SQL inte är skiftlägeskänsligt måste du, för skiftlägeskänsliga operativsystem, inkludera en inställning som anger alla tabellnamn med gemener.

Om du till exempel vill ange alla tabellnamn med gemener i ett Linux-operativsystem:

* Redigera fil `/etc/my.cnf`
* Lägg till följande rad i `[mysqld]` avsnittet:

   `lower_case_table_names = 1`

### UTF8-teckenuppsättning {#utf-character-set}

För att få bättre stöd för flera språk måste du använda teckenuppsättningen UTF8.

Ändra MySQL till att ha UTF8 som teckenuppsättning:

* mysql> SET NAMES &#39;utf8&#39;;

Ändra MySQL-databasen till standard till UTF8:

* Redigera fil `/etc/my.cnf`
* Lägg till följande rad i `[client]` avsnittet:

   `default-character-set=utf8`

* Lägg till följande rad i `[mysqld]` avsnittet:

   `character-set-server=utf8`

## Installerar MySQL Workbench {#installing-mysql-workbench}

MySQL Workbench tillhandahåller ett gränssnitt för körning av SQL-skript som installerar schemat och initiala data.

MySQL Workbench ska laddas ned och installeras enligt instruktionerna för måloperativsystemet.

## Communities Connection {#communities-connection}

När MySQL Workbench startas första gången visas inga anslutningar, såvida den inte redan används för andra syften:

![chlimage_1-104](assets/chlimage_1-104.png)

### Nya anslutningsinställningar {#new-connection-settings}

1. Markera `+` ikonen till höger om `MySQL Connections`.
1. I dialogrutan `Setup New Connection`anger du värden som passar din plattform

   I demonstrationssyfte med författaren AEM-instans och MySQL på samma server:

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

![chlimage_1-105](assets/chlimage_1-105.png)

## Databasinställningar {#database-setup}

Öppna Communities-anslutningen för att installera databasen.

![chlimage_1-106](assets/chlimage_1-106.png)

### Hämta SQL-skriptet {#obtain-the-sql-script}

SQL-skriptet hämtas från AEM-databasen:

1. Bläddra till CRXDE Lite

   * Till exempel [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. Välj mappen /libs/social/config/datastore/dsrp/schema
1. Hämta `init-schema.sql`

![chlimage_1-107](assets/chlimage_1-107.png)

En metod för att hämta schemat är att

* Markera `jcr:content` noden för SQL-filen
* Observera att värdet för `jcr:data` egenskapen är en visningslänk

* Markera vylänken om du vill spara data i en lokal fil

### Skapa DSRP-databasen {#create-the-dsrp-database}

Installera databasen genom att följa stegen nedan. Databasens standardnamn är `communities`.

Om databasnamnet ändras i skriptet måste du även ändra det i [JDBC-konfigurationen](#configurejdbcconnections).

#### Steg 1: öppna SQL-fil {#step-open-sql-file}

I MySQL Workbench

* I listrutan Arkiv
* Välj den hämtade `init_schema.sql`

![chlimage_1-108](assets/chlimage_1-108.png)

#### Steg 2: köra SQL-skript {#step-execute-sql-script}

I Workbench-fönstret för den fil som öppnas i steg 1 väljer du det `lightening (flash) icon` som ska köra skriptet.

I följande bild är `init_schema.sql` filen klar att köras:

![chlimage_1-109](assets/chlimage_1-109.png)

#### Uppdatera {#refresh}

När skriptet har körts måste du uppdatera `SCHEMAS` avsnittet i skriptet `Navigator` för att kunna se den nya databasen. Använd uppdateringsikonen till höger om SCHEMAS:

![chlimage_1-110](assets/chlimage_1-110.png)

## Konfigurera JDBC-anslutning {#configure-jdbc-connection}

OSGi-konfigurationen för **Day Commons JDBC Connections Pool** konfigurerar MySQL JDBC-drivrutinen.

Alla AEM-instanser för publicering och författare ska peka på samma MySQL-server.

När MySQL körs på en annan server än AEM måste servervärdnamnet anges i stället för localhost i JDBC-anslutningen.

* På varje författare och publicera AEM-instansen
* Inloggad med administratörsbehörighet
* Åtkomst till [webbkonsolen](../../help/sites-deploying/configuring-osgi.md)

   * Till exempel [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* Leta reda på `Day Commons JDBC Connections Pool`
* Välj `+` ikonen för att skapa en ny anslutningskonfiguration

![chlimage_1-111](assets/chlimage_1-111.png)

* Ange följande värden:

   * **[!UICONTROL JDBC-drivrutinsklass]**: `com.mysql.jdbc.Driver`
   * **[!UICONTROL JDBC-anslutnings-URI]**: `jdbc:mysql://localhost:3306/communities?characterEncoding=UTF-8`

      Ange en server i stället för localhost om MySQL-servern inte är samma som den här AEM-servern

      *Communities* är standarddatabasens (schemats) namn

   * **[!UICONTROL Användarnamn]**: `root`

      Eller ange det konfigurerade användarnamnet för MySQL-servern, om inte &#39;root&#39;

   * **[!UICONTROL Lösenord]**:

      Rensa det här fältet om inget lösenord har angetts för MySQL,

      Annars anger du det konfigurerade lösenordet för MySQL-användarnamnet
   * **[!UICONTROL Datakällans namn]**: namn som angetts för [MySQL-anslutningen](#new-connection-settings), till exempel &#39;communities&#39;

* Välj **[!UICONTROL Spara]**

