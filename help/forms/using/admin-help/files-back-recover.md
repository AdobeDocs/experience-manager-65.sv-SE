---
title: Filer som ska säkerhetskopieras och återställas
seo-title: Filer som ska säkerhetskopieras och återställas
description: Det här dokumentet beskriver programmet och de datafiler som måste säkerhetskopieras.
seo-description: Det här dokumentet beskriver programmet och de datafiler som måste säkerhetskopieras.
uuid: ba04adb9-675a-48f2-ad52-39c1266e423b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f9a294d-24bd-4e4b-b929-2809f5e6cef9
translation-type: tm+mt
source-git-commit: 67ea825215d1ca7cc2e350ed1c128c3146de45ec

---


# Filer som ska säkerhetskopieras och återställas {#files-to-back-up-and-recover}

De program- och datafiler som måste säkerhetskopieras beskrivs mer ingående i följande avsnitt.

Tänk på följande när det gäller säkerhetskopiering och återställning:

* Databasen bör säkerhetskopieras före GDS- och AEM-databasen.
* Om du behöver ta ned noderna i en klustrad klustermiljö för säkerhetskopiering kontrollerar du att slavnoderna är avstängda före huvudnoden. Annars kan det leda till inkonsekvens i klustret eller servern. Dessutom bör huvudnoden göras live före en slavnod.
* För återställningsåtgärden i ett kluster bör programservern stoppas för varje nod i klustret.

## Katalog för global dokumentlagring {#global-document-storage-directory}

GDS är en katalog som används för att lagra långlivade filer som används i en process. Långvariga filer är avsedda att omfatta en eller flera lanseringar av ett AEM-formulärsystem och kan sträcka sig över flera dagar och till och med år. Dessa långa filer kan innehålla PDF-filer, profiler och formulärmallar. Långvariga filer är en viktig del av det övergripande tillståndet för många AEM-formulärdistributioner. Om vissa eller alla långlivade dokument förloras eller skadas kan formulärservern bli instabil.

Indatadokument för asynkrona jobbanrop lagras också i GDS och måste vara tillgängliga för bearbetning av begäranden. Därför är det viktigt att du ser tillförlitligheten i det filsystem som är värd för GDS och använder en redundant uppsättning av oberoende diskar (RAID) eller annan teknik som passar för dina krav på kvalitet och servicenivå.

Platsen för GDS bestäms under installationen av AEM-formulär eller senare med hjälp av administrationskonsolen. Förutom att ha en plats med hög tillgänglighet för GDS kan du även aktivera databaslagring för dokument. Se Alternativ för [säkerhetskopiering när databasen används för dokumentlagring](files-back-recover.md#backup-options-when-database-is-used-for-document-storage).

### GDS-plats {#gds-location}

Om du lämnar platsinställningen tom under installationen blir platsen som standard en katalog under programserverinstallationen. Du måste säkerhetskopiera följande katalog för programservern:

* (JBoss) `[appserver root]/server/[server]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/[server]/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/[server]/DocumentStorage`

Om du har ändrat GDS-platsen till en annan plats än standardplatsen kan du bestämma den på följande sätt:

* Logga in på administrationskonsolen och klicka på Inställningar > Systeminställningar > Konfigurationer.
* Registrera platsen som anges i rutan Global Document Storage Directory.

I en klustrad miljö pekar GDS vanligtvis på en katalog som delas i nätverket och som kan läsas/skrivas för varje klusternod.

GDS-platserna kan ändras under en återställning om den ursprungliga platsen inte längre är tillgänglig. (Se [Ändra GDS-plats under återställning](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).)

### Alternativ för säkerhetskopiering när databasen används för dokumentlagring {#backup-options-when-database-is-used-for-document-storage}

Du kan aktivera dokumentlagring för AEM-formulär i AEM-formulärdatabasen med administrationskonsolen. Även om det här alternativet behåller alla beständiga dokument i databasen, kräver AEM-formulär fortfarande den filsystembaserade GDS-katalogen eftersom den används för att lagra permanenta och tillfälliga filer och resurser relaterade till sessioner och anrop av AEM-formulär.

När du väljer alternativet Aktivera dokumentlagring i databasen i Core System Settings i administrationskonsolen eller med Configuration Manager, tillåter inte AEM-formulär läge för säkerhetskopiering av ögonblicksbilder och rullande säkerhetskopieringsläge. Därför behöver du inte hantera säkerhetskopieringslägen med AEM-formulär. Om du använder det här alternativet bör du endast säkerhetskopiera GDS en gång efter att du har aktiverat alternativet. När du återställer AEM-formulär från en säkerhetskopia behöver du inte byta namn på säkerhetskopieringskatalogen för GDS eller återställa GDS.

## AEM-databas {#aem-repository}

AEM-databasen (crx-database) skapas om crx-databasen konfigureras när AEM-formulär installeras. Platsen för katalogen i crx-databasen bestäms under installationen av AEM-formulär. Säkerhetskopiering och återställning av AEM-databas krävs tillsammans med databas och GDS för enhetliga AEM-formulärdata i AEM-formulär. AEM-databasen innehåller data för Correspondence Management Solution, Forms Manager och AEM Forms Workspace.

### Correspondence Management Solution {#correspondence-management-solution}

Correspondence Management Solution centraliserar och hanterar framtagning, sammanställning och leverans av säkra, personaliserade och interaktiva korrespondenser. Det gör att ni snabbt kan sammanställa korrespondens från både förgodkänt och skräddarsytt material i en smidig process från det att det skapas till arkivering. Resultatet blir att era kunder får snabb, korrekt, bekväm, säker och relevant kommunikation. Företaget maximerar värdet av kundinteraktioner och minimerar kostnader och risker med en smidig process som ger smidighet, snabbhet och produktivitet.

En enkel konfiguration av Correspondence Management Solution innehåller en författarinstans och en publiceringsinstans på samma dator eller på olika datorer

### formulärhanterare {#forms-manager}

blanketthanteraren effektiviserar processen att uppdatera, hantera och ta tillbaka blanketter.

### AEM Forms Workspace {#html-workspace}

AEM Forms Workspace matchar funktionerna i (Borttaget för AEM-formulär i JEE) Flex Workspace och lägger till nya funktioner för att utöka och integrera Workspace och göra det mer användarvänligt.

>[!NOTE]
>
>Flex Workspace används inte i AEM-formulärsversioner.

Den möjliggör uppgiftshantering för klienter utan Flash Player och Adobe Reader. Det underlättar återgivning av HTML-formulär, förutom PDF-formulär och Flex-formulär.

## AEM-formulärdatabas {#aem-forms-database}

AEM-formulärdatabasen lagrar innehåll som formulärartefakter, tjänstkonfigurationer, processtillstånd och databasreferenser till filer i GDS och rotkatalogen för innehållslagring (för Content Services). Säkerhetskopiering av databaser kan utföras i realtid utan avbrott i tjänsten, och återställning kan ske till en viss tidpunkt eller till en viss ändring. I det här avsnittet beskrivs hur du konfigurerar databasen så att den kan säkerhetskopieras i realtid.

I ett korrekt konfigurerat AEM-formulärsystem kan systemadministratören och databasadministratören enkelt samarbeta för att återställa systemet till ett konsekvent och känt tillstånd.

Om du vill säkerhetskopiera databasen i realtid måste du antingen använda läget för ögonblicksbild eller konfigurera databasen så att den körs i det angivna loggläget. Detta gör att dina databasfiler kan säkerhetskopieras medan databasen är öppen och tillgänglig för användning. Databasen bevarar dessutom sina återställnings- och transaktionsloggar när den körs i dessa lägen.

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES (utgått) är ett innehållshanteringssystem som installeras med LiveCycle. Det gör det möjligt för användarna att utforma, hantera, övervaka och optimera humancentrerade processer. Supporten för innehållstjänster (borttaget) upphör 2014-12-31. Se [Adobes livscykeldokument](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html). Mer information om hur du konfigurerar innehållstjänster (borttaget) finns i [Administrera innehållstjänster](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf).

### DB2 {#db2}

Konfigurera din DB2-databas så att den körs i arkivloggningsläge.

>[!NOTE]
>
>Om din AEM-formulärmiljö uppgraderades från en tidigare version av AEM-formulär och använder DB2 stöds inte säkerhetskopiering online. I så fall måste du stänga av AEM-formulär och göra en offlinesäkerhetskopiering. Framtida versioner av AEM-formulär har stöd för onlinesäkerhetskopiering för uppgraderingskunder.

IBM har en uppsättning verktyg och hjälpsystem som hjälper databasadministratörer att hantera säkerhetskopierings- och återställningsuppgifter:

* IBM DB2 Archive Log Accelerator (Se [IBM DB2 Archive Log Accelerator för z/OS User&#39;s Guide](https://publib.boulder.ibm.com/infocenter/dzichelp/v2r2/topic/com.ibm.db2tools.alc.doc.ug/alcugb20.pdf?noframes=true).)
* IBM DB2 Data Archive Expert (See [IBM DB2 Data Archive Expert User&#39;s Guide and Reference](https://publib.boulder.ibm.com/infocenter/mptoolic/v1r0/topic/com.ibm.db2tools.aeu.doc.ug/ahxugb13.pdf?noframes=true).)

DB2 har inbyggda funktioner för att säkerhetskopiera en databas till Tivoli Storage Manager. Genom att använda Tivoli Storage Manager kan DB2-säkerhetskopior lagras på andra medier eller på den lokala hårddisken.

Mer information om säkerhetskopiering och återställning av DB2-databaser finns i [Utveckla en strategi för säkerhetskopiering och återställning för DB2](https://publib.boulder.ibm.com/infocenter/db2luw/v9/index.jsp?topic=/com.ibm.db2.udb.admin.doc/doc/c0005945.htm).

### Oracle {#oracle}

Använd säkerhetskopiering av ögonblicksbilder eller konfigurera Oracle-databasen så att den körs i arkivloggläge. (Se [Oracle Backup: En introduktion](https://www.databasedesign-resource.com/oracle-backup.md).) Mer information om hur du säkerhetskopierar och återställer Oracle-databasen finns på följande platser:

[](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) Säkerhetskopiering och återställning i Oracle: Beskriver koncepten för säkerhetskopiering och återställning och de vanligaste teknikerna för användning av Recovery Manager (RMAN) för säkerhetskopiering, återställning och rapportering, samt ger mer information om hur du planerar en strategi för säkerhetskopiering och återställning.

[](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) Användarhandbok för säkerhetskopiering och återställning av Oracle-databas: Innehåller detaljerad information om RMAN-arkitektur, koncept och mekanismer för säkerhetskopiering och återställning, avancerade återställningstekniker som återställning vid tidpunkt och funktioner för databasflashback samt prestandajustering för säkerhetskopiering och återställning. Det omfattar även användarhanterad säkerhetskopiering och återställning med användarens operativsystem istället för RMAN. Den här volymen är väsentlig för säkerhetskopiering och återställning av mer avancerade databasdistributioner och för avancerade återställningsscenarier.

[](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) Referens för säkerhetskopiering och återställning av Oracle-databas: Innehåller fullständig information om syntax och semantik för alla RMAN-kommandon och beskriver de databasvyer som är tillgängliga för rapportering av säkerhetskopierings- och återställningsaktiviteter.

### SQL Server {#sql-server}

Använd säkerhetskopiering av ögonblicksbilder eller konfigurera SQL Server-databasen så att den körs i transaktionsloggläge.

SQL Server har även två verktyg för säkerhetskopiering och återställning:

* SQL Server Management Studio (GUI)
* T-SQL (kommandorad)

Se [Strategier](https://articles.techrepublic.com.com/5100-1035_61-1043671.md)för säkerhetskopiering och [Säkerhetskopiering och återställning](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx).

### MySQL {#mysql}

Använd MySQLAdmin eller ändra INI-filerna i Windows för att konfigurera MySQL-databasen så att den körs i binärt loggläge. (Se [Binär loggning](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html)för MySQL.) Ett verktyg för säkerhetskopiering av MySQL är också tillgängligt från InnoBase. (Se [Innobase Hot Backup](https://www.innodb.com/hot-backup/features.md).)

**Obs**: Standardläget *för binär loggning för MySQL är &quot;Statement&quot;, vilket är inkompatibelt med tabeller som används av Content Services (utgått). Om du använder binär loggning i det här standardläget misslyckas Content Services (Borttagen). Om ditt system innehåller innehållstjänster (borttaget) använder du loggningsläget Blandat.*Om du vill aktivera&quot;blandad&quot; loggning lägger du till följande argument i filen my.ini:
`binlog_format=mixed log-bin=logname`

Du kan använda verktyget mysqldump för att få en fullständig säkerhetskopiering av databasen. Fullständig säkerhetskopiering krävs, men är inte alltid lämplig. De producerar stora säkerhetskopior och tar tid att generera. Om du vill göra en stegvis säkerhetskopiering måste du starta servern med alternativet - `log-bin` enligt beskrivningen i föregående avsnitt. Varje gång MySQL-servern startas om slutar den skriva till den aktuella binära loggen, skapar en ny och från och med då blir den nya den aktuella. Du kan tvinga en växel manuellt med `FLUSH LOGS SQL` kommandot. Efter den första fullständiga säkerhetskopieringen utförs efterföljande stegvisa säkerhetskopieringar med hjälp av verktyget mysqladmin med `flush-logs` kommandot, som skapar nästa loggfil.

Se [Sammanfattning](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html)av säkerhetskopieringsstrategi.

```as3
binlog_format=mixed
log-bin=logname
```

## Rotkatalog för innehållslagring (endast innehållstjänster) {#content-storage-root-directory-content-services-only}

Katalogen Content Storage Root innehåller databasen Content Services (Borttagen) där alla dokument, artefakter och index lagras. Katalogträdet för innehållslagring måste säkerhetskopieras. I det här avsnittet beskrivs hur du fastställer platsen för rotkatalogen för innehållslagring för både fristående och klustrade miljöer.

### Rotplats för innehållslagring (fristående miljö) {#content-storage-root-location-stand-alone-environment}

Rotkatalogen för innehållslagring skapas när Content Services (Borttagen) installeras. Platsen för rotkatalogen för innehållslagring bestäms under installationen av AEM-formulär.

Standardplatsen för rotkatalogen för innehållslagring är `[aem-forms root]/lccs_data`.

Säkerhetskopiera följande kataloger i rotkatalogen för innehållslagring:

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

Om katalogen /backup-lucene-indexes inte finns säkerhetskopierar du katalogen /lucene-indexes, som också finns i katalogen Content Storage Root. Om katalogen /backup-lucene-indexes finns ska du inte säkerhetskopiera katalogen /lucene-indexes eftersom det kan orsaka fel.

### Rotplats för innehållslagring (klustrad miljö) {#content-storage-root-location-clustered-environment}

När du installerar innehållstjänster (borttagna) i en klustrad miljö delas rotkatalogen för innehållslagring upp i två separata kataloger:

**** Rotkatalog för innehållslagring: Vanligtvis är en delad nätverkskatalog som är läsbar/skrivskyddad för alla noder i klustret

**** Indexrotkatalog: En katalog som skapas på varje nod i klustret och som alltid har samma sökväg och katalognamn

Standardplatsen för rotkatalogen för innehållslagring är `[GDS root]/lccs_data`, där `[GDS root]` är platsen som beskrivs i [GDS-platsen](files-back-recover.md#gds-location). Säkerhetskopiera följande kataloger i rotkatalogen för innehållslagring:

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

Om katalogen /backup-lucene-indexes inte finns säkerhetskopierar du katalogen /lucene-indexes, som också finns i katalogen Content Storage Root. Om katalogen /backup-lucene-indexes finns ska du inte säkerhetskopiera katalogen /lucene-indexes eftersom det kan orsaka fel.

Standardplatsen för indexrotkatalogen finns `[aem-forms root]/lucene-indexes` på varje nod.

## Kundinstallerade teckensnitt {#customer-installed-fonts}

Om du har installerat ytterligare teckensnitt i AEM-formulärmiljön måste du säkerhetskopiera dem separat. Säkerhetskopiera alla teckensnittskataloger från Adobe och kunder som anges i administrationskonsolen under Inställningar > Kärnsystem > Konfigurationer. Se till att du säkerhetskopierar hela teckensnittskatalogen.

>[!NOTE]
>
>Som standard finns de Adobe-teckensnitt som installeras med AEM-formulär i `[aem-forms root]/fonts` katalogen.

Om du initierar om operativsystemet på värddatorn och vill använda teckensnitt från det tidigare operativsystemet, bör innehållet i systemteckensnittskatalogen också säkerhetskopieras. (Mer information finns i dokumentationen för ditt operativsystem).
