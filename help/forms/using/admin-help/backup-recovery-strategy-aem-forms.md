---
title: Säkerhetskopierings- och återställningsstrategi för AEM-formulär
seo-title: Säkerhetskopierings- och återställningsstrategi för AEM-formulär
description: Lär dig hur du implementerar en strategi för att säkerhetskopiera data och se till att de är synkroniserade med AEM-formulärdata.
seo-description: Lär dig hur du implementerar en strategi för att säkerhetskopiera data och se till att de är synkroniserade med AEM-formulärdata.
uuid: 98fc3115-76e5-4e58-aa30-3601866a441f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f192a8a3-1116-4d32-9b57-b53d532c0dbf
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Säkerhetskopierings- och återställningsstrategi för AEM-formulär{#backup-and-recovery-strategy-for-aem-forms}

Om AEM-formulärimplementeringen lagrar ytterligare anpassade data i en annan databas ansvarar du för att implementera en strategi för att säkerhetskopiera dessa data och se till att de är synkroniserade med AEM-formulärdata. Dessutom måste programmet vara utformat så att det är tillräckligt robust för att hantera ett scenario där ytterligare databaser inte är synkroniserade. Vi rekommenderar starkt att alla databasåtgärder som utförs utförs i samband med en transaktion för att upprätthålla ett konsekvent tillstånd.

När du har identifierat hur AEM-formulär används, ska du bestämma vilka filer som ska säkerhetskopieras, hur ofta och vilket säkerhetskopieringsfönster som ska göras tillgängligt.

>[!NOTE]
>
>Precis som med andra aspekter av implementeringen av AEM-formulär måste strategin för säkerhetskopiering och återställning utvecklas och testas i en utvecklings- eller staging-miljö innan den används i produktionen för att säkerställa att hela lösningen fungerar som förväntat utan dataförlust.

Adobe Experience Manager (AEM) är en integrerad del av AEM-formulären. Därför måste du säkerhetskopiera AEM även synkroniserat med AEM-formulärsäkerhetskopior som Correspondence Management Solution och tjänster, t.ex. formulärhanterare, baserat på data som lagras i AEM-delar av AEM-formulär. För att förhindra dataförluster måste AEM-formulärspecifika data säkerhetskopieras på ett sätt som säkerställer att GDS och AEM (databasen) korrelerar med databasreferenser. Kataloger för databas, GDS, AEM och Content Storage Root måste återställas till en dator med samma DNS-namn som originalet.

## Olika typer av säkerhetskopiering {#types-of-backups}

Säkerhetskopieringsstrategin för AEM-formulär innefattar två typer av säkerhetskopiering:

**** Systemavbildning: En fullständig säkerhetskopia av systemet som du kan använda för att återställa datorns innehåll om hårddisken eller hela datorn slutar att fungera. Säkerhetskopiering av systemavbildning krävs endast före driftsättning av AEM-formulär. Interna regler styr sedan hur ofta säkerhetskopiering av systemavbildningar krävs.

**** Specifika data för AEM-formulär: Programdata finns i databasen, GDS (Global Document Storage) och AEM-databasen och måste säkerhetskopieras i realtid. GDS är en katalog som används för att lagra långlivade filer som används i en process. Dessa filer kan innehålla PDF-filer, profiler eller formulärmallar.

***Obs **: Om Content Services (Deprecated) är installerat säkerhetskopierar du även rotkatalogen för innehållslagring. (Se rotkatalog för[innehållslagring (endast innehållstjänster)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only).)*

Databasen används för att lagra formulärartefakter, tjänstkonfigurationer, processtillstånd och databasreferenser till GDS-filer. Om du har aktiverat dokumentlagring i databasen lagras beständiga data och dokument i GDS också i databasen. Databasen kan säkerhetskopieras och återställas på följande sätt:

* **Säkerhetskopieringsläget** för ögonblicksbilder anger att AEM-formulärsystemet är i säkerhetskopieringsläge antingen oändligt eller under ett visst antal minuter, varefter säkerhetskopieringsläget inte längre är aktiverat. Om du vill gå in i eller lämna läget för säkerhetskopiering av ögonblicksbilder kan du använda något av följande alternativ. Efter ett återställningsscenario bör läget för ögonblicksbildssäkerhetskopiering inte aktiveras.

   * Använd sidan Inställningar för säkerhetskopiering i administrationskonsolen. Markera kryssrutan Använd i säkert säkerhetskopieringsläge om du vill aktivera ögonblicksbildläge. Avmarkera kryssrutan för att avsluta läget för ögonblicksbild.
   * Använd skriptet LCBackupMode (se [Säkerhetskopiera katalogerna](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories)för databas, GDS och Content Storage Root). Om du vill avsluta läget för säkerhetskopiering av ögonblicksbilder anger du parametern `continuousCoverage` till `false` eller använder `leaveContinuousCoverage` alternativet i skriptargumentet.
   * Använd det angivna API:t för säkerhetskopiering/återställning. <!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* **Läget för rullande säkerhetskopiering** anger att systemet alltid är i säkerhetskopieringsläge, med en ny session för säkerhetskopieringsläge initierad så snart som föregående session släpps. Ingen timeout är associerad med rullande säkerhetskopieringsläge. När skriptet eller API:erna för LCBackupMode anropas för att lämna det rullande säkerhetskopieringsläget påbörjas en ny session för rullande säkerhetskopieringsläge. Det här läget är användbart när du vill ha stöd för kontinuerlig säkerhetskopiering men ändå vill att gamla och obehövliga dokument ska rensas bort från GDS-katalogen. Läget för rullande säkerhetskopiering stöds inte via sidan Säkerhetskopiering och återställning. Efter ett återställningsscenario är läget för rullande säkerhetskopiering fortfarande aktiverat. Du kan lämna läget för kontinuerlig säkerhetskopiering (rullande säkerhetskopieringsläge) genom att använda skriptet LCBackupMode med `leaveContinuousCoverage` alternativet.

***Obs**! Om du lämnar det rullande säkerhetskopieringsläget omedelbart startas en ny session i säkerhetskopieringsläge. Om du vill inaktivera läget för rullande säkerhetskopiering helt använder du alternativet i skriptet, som skriver över den befintliga rullande säkerhetskopieringssessionen. `leaveContinuousCoverage` I läget för säkerhetskopiering av ögonblicksbilder kan du lämna säkerhetskopieringsläget som vanligt. *

För att förhindra dataförlust måste AEM-formulärspecifika data säkerhetskopieras på ett sätt som säkerställer att GDS- och Content Storage Root-katalogdokument korrelerar med databasreferenser.

>[!NOTE]
>
>När GDS lagras i filsystemet och inte i databasen, utför du säkerhetskopieringen före GDS-säkerhetskopieringen.

## Specialöverväganden för säkerhetskopiering och återställning {#special-considerations-for-backup-and-recovery}

Använd följande riktlinjer om du måste återställa AEM-formulär till en annan miljö på grund av följande ändringar:

* Ändring av IP-adress, värdnamn eller port för AEM-formulärservern
* Ändringar i enhetsbokstäver eller katalogsökväg
* Byt till en annan databasvärd, port eller namn

Sådana återställningsscenarier orsakas vanligtvis av maskinvarufel på servern som är värd för programservern, databasservern eller formulärservern. Förutom de AEM-formulärspecifika konfigurationer som beskrivs i det här avsnittet bör du även göra nödvändiga ändringar för andra delar av AEM-formulärdistributionen, som belastningsutjämnare och brandväggar, om värdnamnet eller IP-adressen för en AEM-formulärserver ändras.

### Vad kan inte ändras {#what-cannot-be-changed}

Även om du kan ändra databasservern och många andra parametrar kan du inte ändra programservertypen eller databastypen när du återställer AEM-formulär från en säkerhetskopia. Om du till exempel återställer en säkerhetskopia av AEM-formulär kan du inte ändra programservern från JBoss till WebLogic eller databasen från Oracle till DB2. Dessutom måste återskapade AEM-formulär använda samma filsystemsökvägar, till exempel teckensnittskatalogen.

### Starta om efter återställning {#restarting-after-a-recovery}

Innan du startar om formulärservern efter en återställning gör du följande:

1. Starta systemet i underhållsläge.
1. Så här ser du till att Form Manager synkroniseras med AEM-formulär i underhållsläge:

   1. Gå till https://&lt;*server*>:&lt;*port*>/lc/fm och logga in med autentiseringsuppgifter för adminstrator/lösenord.
   1. Klicka på namnet på användaren (superadministratör i det här fallet) i det övre högra hörnet.
   1. Klicka på **Administratörsalternativ**.
   1. Klicka på **Start** för att synkronisera resurser från databasen.

1. I en klustrad miljö bör huvudnoden (med avseende på AEM) vara uppe före slavnoderna.
1. Se till att inga processer initieras från interna eller externa källor som Web-, SOAP- eller EJB-processinitierare förrän systemets normala funktion har validerats.

Om huvuddatabasen för AEM-formulär flyttas eller ändras läser du de installationsguider som är relevanta för programservern för att få information om hur du uppdaterar databasanslutningsinformationen för AEM-formulärdatakällorna IDP_DS och EDC_DS.

### Ändra värdnamn eller IP-adress för AEM-formulär {#changing-the-aem-forms-hostname-or-ip-address}

Om du använder TCP-cachelagring i stället för UDP i ett kluster måste du uppdatera cachepositionerarkonfigurationen. Mer information finns i&quot;Konfigurera cachelagringsplatser (endast cachelagring med TCP)&quot; i den konfigurationsguide som är relevant för programservern.

### Ändra sökvägar till filsystemet för noden AEM-formulär {#changing-the-aem-forms-node-file-system-paths}

Om du ändrar filsystemsökvägarna för en fristående nod måste du uppdatera lämpliga referenser i inställningar, andra systemkonfigurationer, anpassade program och distribuerade AEM-formulärprogram. Å andra sidan måste alla noder använda samma sökvägskonfiguration för filsystemet för ett kluster. Du måste ange rotkatalogen för GDS (Global Document Storage) och se till att den pekar på en kopia av den återställda GDS-servern som är synkroniserad med den återställda databasen. Det är viktigt att ange GDS-sökvägen eftersom GDS kan innehålla data som ska finnas kvar mellan omstarter av programservern.

I en klustrad miljö bör databasens filsystemskonfiguration vara densamma för alla klusternoder före och efter säkerhetskopieringen.

Använd `LCSetGDS`skriptet i `[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline` mappen för att ange GDS-sökvägen när du har ändrat sökvägarna i filsystemet. Mer information finns i `ReadMe.txt` filen i samma mapp. Om den gamla GDS-katalogsökvägen inte kan användas måste du använda `LCSetGDS` skriptet för att ange den nya sökvägen till GDS innan du startar AEM-formulär.

>[!NOTE]
>
>Den här begränsningen är den enda under vilken du bör använda det här skriptet för att ändra GDS-platsen. Använd administrationskonsolen om du vill ändra GDS-platsen medan AEM-formulär körs. (Se [Konfigurera allmänna AEM-formulärinställningar](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)*.) *

När du har angett GDS-sökvägen startar du formulärservern i underhållsläge och använder administrationskonsolen för att uppdatera de återstående filsystemsökvägarna för den nya noden. När du har verifierat att alla nödvändiga konfigurationer har uppdaterats startar du om och testar AEM-formulären.
