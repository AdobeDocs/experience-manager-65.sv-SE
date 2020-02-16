---
title: Säkerhetskopiera AEM-formulärdata
seo-title: Säkerhetskopiera AEM-formulärdata
description: I det här dokumentet beskrivs de steg som krävs för att slutföra en aktiverad, eller online, säkerhetskopiering av AEM-formulärdatabasen, GDS- och Content Storage Root-katalogerna.
seo-description: I det här dokumentet beskrivs de steg som krävs för att slutföra en aktiverad, eller online, säkerhetskopiering av AEM-formulärdatabasen, GDS- och Content Storage Root-katalogerna.
uuid: ac7856be-e3b7-4b81-b8b9-fc909b5907b4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 52187196-b091-4683-85ae-cc7c250dee54
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Säkerhetskopiera AEM-formulärdata {#backing-up-the-aem-forms-data}

I det här avsnittet beskrivs de steg som krävs för att slutföra en aktiverad, eller online, säkerhetskopiering av AEM-formulärdatabasen, GDS- och Content Storage Root-katalogerna.

När AEM-formulär har installerats och distribuerats till produktionsområden bör databasadministratören göra en inledande fullständig eller kall säkerhetskopiering av databasen. Databasen måste stängas av för den här säkerhetskopieringen. Sedan bör differentiell eller inkrementell (eller het) säkerhetskopiering av databasen göras regelbundet.

För att säkerhetskopieringen och återställningen ska lyckas måste det alltid finnas en säkerhetskopia av systemavbildningen. Om en förlust inträffar kan du återställa hela miljön till ett konsekvent tillstånd.

Genom att säkerhetskopiera databasen samtidigt som GDS-, AEM-databasen och katalogsäkerhetskopieringen Content Storage Root kan du synkronisera dessa system om återställning skulle behövas.

Säkerhetskopieringsproceduren som beskrivs i det här avsnittet kräver att du aktiverar säkert säkerhetskopieringsläge innan du säkerhetskopierar AEM-formulärdatabasen, AEM-databasen, GDS- och Content Storage Root-katalogerna. När säkerhetskopieringen är klar måste du avsluta läget för säker säkerhetskopiering. Säkert säkerhetskopieringsläge används för att markera långlivade och beständiga dokument som finns i GDS. I det här läget säkerställs att den automatiska filrensningsfunktionen (filinsamlaren) inte tar bort filer som har gått ut förrän det säkra säkerhetskopieringsläget har släppts. En GDS-säkerhetskopia måste synkroniseras med en databassäkerhetskopia.

Hur ofta GDS-platsen måste säkerhetskopieras beror på hur AEM-formulär används och vilka säkerhetskopieringsfönster som är tillgängliga. Säkerhetskopieringsfönstret kan påverkas av långvariga processer eftersom de kan köras i flera dagar. Om du kontinuerligt ändrar, lägger till och tar bort filer i den här katalogen bör du säkerhetskopiera GDS-platsen oftare.

Om databasen körs i ett loggningsläge, vilket beskrivs i föregående avsnitt, måste databasloggarna också säkerhetskopieras ofta så att de kan användas för att återställa databasen vid mediefel.

>[!NOTE]
>
>Filer som inte refereras kan finnas kvar i GDS-katalogen efter återställningsprocessen. Detta är en känd begränsning för tillfället.

## Säkerhetskopiera katalogerna databas, GDS, AEM-databas och Content Storage Root {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

Du måste placera AEM-formulär antingen i säkert läge (ögonblicksbild) eller i läget för rullande säkerhetskopiering (kontinuerlig täckning). Innan du anger att AEM-formulär ska ange något av säkerhetskopieringslägena bör du kontrollera följande:

* Verifiera systemversionen och registrera de korrigeringar eller uppdateringar som tillämpats sedan den senaste fullständiga säkerhetskopieringen av systemavbildningen.
* Om du använder säkerhetskopiering i rullnings- eller ögonblicksbildläge måste databasen vara konfigurerad med rätt logginställningar för att tillåta säkerhetskopiering av databasen under körning. (Se [AEM-formulärdatabas](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).)

Förutom detta bör du följa följande riktlinjer för säkerhetskopiering/återställning.

* Säkerhetskopiera GDS-katalogen med hjälp av ett tillgängligt operativsystem eller ett verktyg för säkerhetskopiering från tredje part. (Se [GDS-plats](/help/forms/using/admin-help/files-back-recover.md#gds-location).)
* (Valfritt) Säkerhetskopiera rotkatalogen för innehållslagring med hjälp av ett tillgängligt operativsystem eller ett säkerhetskopierings- och verktyg från tredje part. (Se [Rotplats för innehållslagring (fristående miljö)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) eller Rotplats för [innehållslagring (klustrad miljö)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment).)
* Säkerhetskopiera författare och publiceringsinstanser (crx -database backup).

   Om du vill säkerhetskopiera Correspondence Management Solution-miljön utför du stegen på författaren och publicerar instanser enligt beskrivningen i [Säkerhetskopiera och återställ](/help/sites-administering/backup-and-restore.md).

   Tänk på följande när du säkerhetskopierar författare och publiceringsinstanser:

   * Se till att säkerhetskopieringen för författare och publiceringsinstanser är synkroniserad så att den startar samtidigt. Även om du kan fortsätta använda författare- och publiceringsinstanser medan säkerhetskopieringen utförs, bör du inte publicera några resurser under säkerhetskopieringen för att undvika ohämtade ändringar. Vänta tills säkerhetskopieringen av både författare och publiceringsinstanser har avslutats innan du publicerar nya resurser.
   * Den fullständiga säkerhetskopieringen av Författarnoden omfattar säkerhetskopiering av data för Forms Manager och AEM Forms Workspace.
   * Workbench-utvecklare kan fortsätta att arbeta med sina processer lokalt. De bör inte driftsätta några nya processer under säkerhetskopieringsfasen.
   * Beslutet om längden på varje säkerhetskopieringssession (för rullande säkerhetskopieringsläge) bör baseras på den totala tid det tar att säkerhetskopiera alla data i AEM-formulär (DB, GDS, AEM-databas och andra anpassade data).

Du bör säkerhetskopiera AEM-formulärdatabasen, inklusive eventuella transaktionsloggar. (Se [AEM-formulärdatabas](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) Mer information finns i lämplig kunskapsbasartikel för din databas:

* [Oracle Backup and Recovery for AEM forms](https://www.adobe.com/go/kb403624)
* [MySQL Backup and Recovery for AEM forms](https://www.adobe.com/go/kb403625)
* [Säkerhetskopiering och återställning av Microsoft SQL Server för AEM-formulär](https://www.adobe.com/go/kb403623)
* [DB2 Säkerhetskopiering och återställning för AEM-formulär](https://www.adobe.com/go/kb403626)

Dessa artiklar ger vägledning om grundläggande databasfunktioner för säkerhetskopiering och återställning av data. De är inte avsedda som tekniska handledningar för en viss leverantörs säkerhetskopierings- och återställningsfunktion för databaser. De innehåller kommandon som behövs för att skapa en tillförlitlig strategi för säkerhetskopiering av databaser för AEM-formulärprogramdata.

>[!NOTE]
>
>Säkerhetskopieringen av databasen måste vara slutförd innan du börjar säkerhetskopiera GDS. Om säkerhetskopieringen av databasen inte är slutförd är dina data inte synkroniserade.

### Ange lägen för säkerhetskopiering {#entering-the-backup-modes}

Du kan antingen använda administrationskonsolen, kommandot LCBackupMode eller API:t som är tillgängligt med installationen av AEM-formulär för att gå in i och lämna säkerhetskopieringslägena. Observera att alternativet administrationskonsol inte är tillgängligt för rullande säkerhetskopiering (kontinuerlig täckning). använder du antingen kommandoradsalternativet eller API:t. <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>Om du har konfigurerat SSL på formulärservern kan du inte placera formulärservern i säkerhetskopieringsläge med hjälp av skriptet LCBackupMode.CMD.

**Använda administrationskonsolen för att gå in i säkert säkerhetskopieringsläge**

1. Logga in på administrationskonsolen.
1. Klicka på Inställningar > Systeminställningar > Verktyg för säkerhetskopiering.
1. Välj Använd i säkert säkerhetskopieringsläge och klicka på OK.

   Med den här metoden försätts AEM-formulär i oändligt säkerhetskopieringsläge (ingen timeout), och det försätts i ögonblicksbildsläge i stället för i rullande säkerhetskopieringsläge.

**Använda kommandoradsalternativet för att växla till säkert säkerhetskopieringsläge**

Du kan använda kommandoradsgränssnittets `LCBackupMode` skript för att placera AEM-formulär i säkert säkerhetskopieringsläge.

1. Ange ADOBE_LIVECYCLE och starta programservern.
1. Gå till `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` mappen.
1. Beroende på vilket operativsystem du använder kan du redigera `LCBackupMode.cmd` - eller `LCBackupMode.sh` skriptet och ange standardvärden som passar ditt system.
1. Kör följande kommando på en rad i kommandotolken:

   * (Windows) `LCBackupMode.cmd enter [-Host=`*värdnamn *`] [-port=`*portnumber* `] [-user=`*användarnamn *`] [-password=`*password* `] [-label=`*etikett *`] [-timeout=`** ¥seconds¥ `]`
   * (Linux, UNIX) `LCBackupMode.sh enter [-host=`*värdnamn *`] [-port=`*portnumber* `] [-user=`*användarnamn *`] [-password=`*password* `] [-label=`*etikett *`]`
   I de föregående kommandona definieras platshållarna enligt följande:

   `Host` är namnet på den värd där AEM-formulär körs.

   `port` är WebServices-porten för den programserver där AEM-formulär körs.

   `user` är användarnamnet för AEM-formuläradministratören.

   `password` är lösenordet för AEM-formuläradministratören.

   `label` är textetiketten, som kan vara vilken sträng som helst, för denna säkerhetskopiering.

   `timeout` är antalet sekunder efter vilket säkerhetskopieringsläget automatiskt lämnas. Den kan vara 0 till 10 080. Om värdet är 0, vilket är standardvärdet, kommer säkerhetskopieringsläget aldrig att fungera.

   Mer information om kommandoradens gränssnitt till säkerhetskopieringsläget finns i filen Viktigt i katalogen BackupRestoreCommandline.

### Lämna säkerhetskopieringslägen {#leaving-backup-modes}

Du kan använda administrationskonsolen eller kommandoradsalternativet om du vill lämna säkerhetskopieringslägena.

**Lämna läget för säker säkerhetskopiering (ögonblicksbild)**

Utför följande åtgärder om du vill använda administrationskonsolen för att ta bort AEM-formulär från säkert säkerhetskopieringsläge (ögonblicksbildsläge).

1. Logga in på administrationskonsolen.
1. Klicka på Inställningar > Systeminställningar > Verktyg för säkerhetskopiering.
1. Avmarkera Använd i säkert säkerhetskopieringsläge och klicka på OK.

**Lämna alla säkerhetskopieringslägen**

Du kan använda kommandoradsgränssnittet för att ta bort AEM-formulär från säkert säkerhetskopieringsläge (ögonblicksbildsläge) eller för att avsluta den aktuella säkerhetskopieringsläget (rullande läge). Observera att du inte kan använda administrationskonsolen för att lämna det rullande säkerhetskopieringsläget. I läget för rullande säkerhetskopiering är kontrollerna för Backup Utilities på administrationskonsolen inaktiverade. Du måste använda antingen API-anrop eller kommandot LCBackupMode.

1. Gå till `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` mappen.
1. Beroende på vilket operativsystem du använder kan du redigera `LCBackupMode.cmd` - eller `LCBackupMode.sh` skriptet och ange standardvärden som passar ditt system.

   >[!NOTE]
   >
   >Du måste ange katalogen JAVA_HOME enligt beskrivningen i det kapitel som passar programservern när du [förbereder installation av AEM-formulär](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)*.*

1. Kör följande kommando på en rad:

   * (Windows) `LCBackupMode.cmd leaveContinuousCoverage [-Host=`*värdnamn *`] [-port=`*portnummer* , `] [-user=`*användarnamn *,`] [-password=`*lösenord*`]`
   * (Linux, UNIX) `LCBackupMode.sh leaveContinuousCoverage [-Host=`*värdnamn *`] [-port=`*portnummer* `] [-user=`*användarnamn *`] [-password=`*lösenord*`]`

      I de föregående kommandona definieras platshållarna enligt följande:

      `Host` är namnet på den värd där AEM-formulär körs.

      `port` är den port där AEM-formulär körs på programservern.

      `user` är användarnamnet för AEM-formuläradministratören.

      `password` är lösenordet för AEM-formuläradministratören.

      `leaveContinuousCoverage` Använd det här alternativet om du vill inaktivera rullande säkerhetskopieringsläge helt.
   >[!NOTE]
   >
   >Det går inte att återupprätta kontinuerlig täckning för den tid som säkerhetskopieringsläget är inaktiverat. Ändringar under den tiden är inte skyddade.

   >[!NOTE]
   >
   >Om du har aktiverat dokumentlagring i databasen kan du inte använda läget för säkerhetskopiering av ögonblicksbilder och rullande säkerhetskopiering.

   Mer information om kommandoradens gränssnitt till säkerhetskopieringsläget finns i filen Viktigt i katalogen BackupRestoreCommandline.

