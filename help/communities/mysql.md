---
title: MySQL-konfiguration för aktiveringsfunktioner
seo-title: MySQL-konfiguration för aktiveringsfunktioner
description: Ansluta MySQL-servern
seo-description: Ansluta MySQL-servern
uuid: e02d9404-de75-4fdb-896c-ea3f64f980a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 9222bc93-c231-4ac8-aa28-30d784a4ca3b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# MySQL-konfiguration för aktiveringsfunktioner {#mysql-configuration-for-enablement-features}

MySQL är en relationsdatabas som främst används för SCORM-spårning och rapportdata för aktiveringsresurser. Här finns tabeller för andra funktioner som att spåra paus/återupptagning av video.

Dessa instruktioner beskriver hur du ansluter till MySQL-servern, skapar aktiveringsdatabasen och fyller i databasen med initiala data.

## Krav {#requirements}

Innan du konfigurerar aktiveringsfunktionen i MySQL för Communities måste du se till att

* Installera [MySQL server](https://dev.mysql.com/downloads/mysql/) Community Server version 5.6
   * Version 5.7 stöds inte för SCORM
   * Kan vara samma server som författarens AEM-instans
* Installera den officiella [JDBC-drivrutinen för MySQL på alla AEM-instanser](deploy-communities.md#jdbc-driver-for-mysql)
* Installera [MySQL Workbench](https://dev.mysql.com/downloads/tools/workbench/)
* Installera [SCORM-paketet på alla AEM-instanser](enablement.md#scorm)

## Installerar MySQL {#installing-mysql}

MySQL ska laddas ned och installeras enligt instruktionerna för måloperativsystemet.

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

## Aktivera anslutning {#enablement-connection}

När MySQL Workbench startas första gången visas inga anslutningar, såvida den inte redan används för andra syften:

![chlimage_1-327](assets/chlimage_1-327.png)

### Nya anslutningsinställningar {#new-connection-settings}

1. Markera +-ikonen till höger om `MySQL Connections`.
1. I dialogrutan `Setup New Connection`anger du värden som är lämpliga för din plattform i demonstrationssyfte, med författarens AEM-instans och MySQL på samma server:
   * Anslutningsnamn: `Enablement`
   * Anslutningsmetod: `Standard (TCP/IP)`
   * Värdnamn: `127.0.0.1`
   * Användarnamn: `root`
   * Lösenord: `no password by default`
   * Standardschema: `leave blank`
1. Välj `Test Connection` för att verifiera anslutningen till den MySQL-tjänst som körs

**Anteckningar**:

* Standardporten är `3306`
* Det `Connection Name` valda namnet anges som `datasource` namn i [JDBC OSGi-konfiguration](#configure-jdbc-connections)

#### Anslutningen lyckades {#successful-connection}

![chlimage_1-328](assets/chlimage_1-328.png)

#### Ny aktiveringsanslutning {#new-enablement-connection}

![chlimage_1-329](assets/chlimage_1-329.png)

## Databasinställningar {#database-setup}

Observera att det finns ett testschema och standardanvändarkonton när du öppnar den nya aktiveringsanslutningen.

![chlimage_1-330](assets/chlimage_1-330.png)

### Hämta SQL-skript {#obtain-sql-scripts}

SQL-skripten hämtas med CRXDE Lite på författarinstansen. SCORM- [paketet](deploy-communities.md#scorm) måste vara installerat:

1. Bläddra till CRXDE Lite
   * Till exempel [http://localhost:4502/crx/de](http://localhost:4502/crx/de)
1. Expandera `/libs/social/config/scorm/` mappen
1. Hämta `database_scormengine.sql`
1. Hämta `database_scorm_integration.sql`

![chlimage_1-331](assets/chlimage_1-331.png)

En metod för att hämta schemat är att

* Markera `jcr:content`noden för SQL-filen
* Observera att värdet för `jcr:data`egenskapen är en visningslänk
* Markera vylänken om du vill spara data i en lokal fil

### Skapa SCORM-databas {#create-scorm-database}

Den Aktivera SCORM-databas som ska skapas är:

* name: `ScormEngineDB`
* som skapats från skript:
   * schema: `database_scormengine.sql`
   * data: `database_scorm_integration.sql`Följ stegen nedan ([öppna](#step-open-sql-file), [kör](#step-execute-sql-script)) för att installera varje [SQL-skript](#obtain-sql-scripts) . [Uppdatera](#refresh) vid behov för att se resultatet av skriptkörningen.

Installera schemat innan du installerar data.

>[!CAUTION]
>
>Om databasnamnet ändras måste du ange det korrekt i
>
>* [JDBC-konfiguration](#configure-jdbc-connections)
>* [SCORM-konfiguration](#configure-scorm)
>



#### Steg 1: öppna SQL-fil {#step-open-sql-file}

I MySQL Workbench

* I listrutan Arkiv
* Välj `Open SQL Script ...`
* Välj något av följande i den här ordningen:
   1. `database_scormengine.sql`
   1. `database_scorm_integration.sql`

![chlimage_1-332](assets/chlimage_1-332.png)

#### Steg 2: köra SQL-skript {#step-execute-sql-script}

I Workbench-fönstret för den fil som öppnas i steg 1 väljer du det `lightening (flash) icon` som ska köra skriptet.

Observera att körningen av skriptet för att skapa SCORM-databasen kan ta en minut att slutföra. `database_scormengine.sql`

![chlimage_1-333](assets/chlimage_1-333.png)

#### Uppdatera {#refresh}

När skripten har körts måste du uppdatera `SCHEMAS`avsnittet i `Navigator` för att kunna se den nya databasen. Använd uppdateringsikonen till höger om SCHEMAS:

![chlimage_1-334](assets/chlimage_1-334.png)

#### Resultat: scormenginedb {#result-scormenginedb}

När du har installerat och uppdaterat SCHEMAS visas **`scormenginedb`**.

![chlimage_1-335](assets/chlimage_1-335.png)

## Konfigurera JDBC-anslutningar {#configure-jdbc-connections}

OSGi-konfigurationen för **Day Commons JDBC Connections Pool** konfigurerar MySQL JDBC-drivrutinen.

Alla AEM-instanser för publicering och författare ska peka på samma MySQL-server.

När MySQL körs på en annan server än AEM måste serverns värdnamn anges i stället för localhost i JDBC-kopplingen (som fyller i [ScormEngine](#configurescormengineservice) -konfigurationen).

* På varje författare och publicera AEM-instansen
* Inloggad med administratörsbehörighet
* Åtkomst till [webbkonsolen](../../help/sites-deploying/configuring-osgi.md)
   * Till exempel [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* Leta reda på `Day Commons JDBC Connections Pool`
* Skapa en ny konfiguration genom att klicka på `+` ikonen

![chlimage_1-336](assets/chlimage_1-336.png)

* Ange följande värden:
   * **[!UICONTROL JDBC-drivrutinsklass]**: `com.mysql.jdbc.Driver`
   * **URIJ **för DBC-anslutning:`jdbc:mysql://localhost:3306/aem63reporting`ange server i stället för localhost om MySQL-servern inte är samma som den här AEM-servern
   * **[!UICONTROL Användarnamn]**: Rot eller ange det konfigurerade användarnamnet för MySQL-servern, om inte &#39;root&#39;
   * **[!UICONTROL Lösenord]**: Rensa det här fältet om inget lösenord har angetts för MySQL, annars anger du det konfigurerade lösenordet för MySQL-användarnamnet
   * **[!UICONTROL Datakällans namn]**: Namn som angetts för [MySQL-anslutningen](#new-connection-settings), till exempel &#39;enablement&#39;
* Välj **[!UICONTROL Spara]**

## Konfigurera korm {#configure-scorm}

### Tjänsten AEM Communities ScormEngine {#aem-communities-scormengine-service}

OSGi-konfigurationen för **AEM Communities ScormEngine-tjänsten** konfigurerar SCORM för en aktiveringscommunitys användning av MySQL-servern.

Den här konfigurationen finns när [SCORM-paketet](deploy-communities.md#scorm-package) installeras.

Alla publicerings- och författarinstanser pekar på samma MySQL-server.

När MySQL körs på en annan server än AEM, måste serverns värdnamn anges i stället för localhost i ScormEngine-tjänsten, som vanligtvis fylls i från konfigurationen för [JDBC-anslutningen](#configure-jdbc-connections) .

* På varje författare och publicera AEM-instansen
* Inloggad med administratörsbehörighet
* Åtkomst till [webbkonsolen](../../help/sites-deploying/configuring-osgi.md)
   * Till exempel [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* Leta reda på `AEM Communities ScormEngine Service`
* Markera redigeringsikonen
   ![chlimage_1-337](assets/chlimage_1-337.png)
* Kontrollera att följande parametervärden är konsekventa med [JDBC Connection](#configurejdbcconnectionspool) -konfigurationen:
   * **[!UICONTROL JDBC-anslutnings-URI]**: `jdbc:mysql://localhost:3306/ScormEngineDB` ScormEngineDB ** är standarddatabasnamnet i SQL-skripten
   * **[!UICONTROL Användarnamn]**: Rot eller ange det konfigurerade användarnamnet för MySQL-servern, om inte &#39;root&#39;
   * **[!UICONTROL Lösenord]**: Rensa det här fältet om inget lösenord har angetts för MySQL, annars anger du det konfigurerade lösenordet för MySQL-användarnamnet
* Angående följande parameter:
   * **[!UICONTROL Lösenord]**: REDIGERA INTE

      Endast för internt bruk. Den är avsedd för en särskild serviceanvändare som används av AEM Communities för att kommunicera med scorm-motorn.
* Välj **[!UICONTROL Spara]**

### Adobe Granite CSRF-filter {#adobe-granite-csrf-filter}

För att se till att aktiveringskurser fungerar korrekt i alla webbläsare måste Mozilla läggas till som en användaragent som inte är markerad av CSRF-filtret.

* På varje publicerad AEM-instans
* Inloggad med administratörsbehörighet
* Åtkomst till [webbkonsolen](../../help/sites-deploying/configuring-osgi.md)
   * Till exempel [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)
* Sök `Adobe Granite CSRF Filter`
* Markera redigeringsikonen
   ![chlimage_1-337](assets/chlimage_1-338.png)
* Välj `[+]` ikonen för att lägga till en säker användaragent
* Enter `Mozilla/*`
* Välj **[!UICONTROL Spara]**

