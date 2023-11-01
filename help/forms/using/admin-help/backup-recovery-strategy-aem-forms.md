---
title: Strategier för säkerhetskopiering och återställning av AEM formulär
description: Lär dig hur du implementerar en strategi för att säkerhetskopiera data och se till att de är synkroniserade med AEM formulärdata.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 01ec6ebc-6d80-4417-9604-c8571aebb57e
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '1489'
ht-degree: 0%

---

# Strategier för säkerhetskopiering och återställning av AEM formulär{#backup-and-recovery-strategy-for-aem-forms}

Om implementeringen av AEM sparar ytterligare anpassade data i en annan databas ansvarar du för att implementera en strategi för att säkerhetskopiera dessa data och se till att de är synkroniserade med de AEM formulärdata. Dessutom måste programmet vara utformat så att det är tillräckligt robust för att hantera ett scenario där ytterligare databaser inte är synkroniserade. Vi rekommenderar starkt att alla databasåtgärder som utförs utförs i samband med en transaktion för att upprätthålla ett konsekvent tillstånd.

När du har identifierat hur AEM formulär ska användas, bestämmer du vilka filer som ska säkerhetskopieras, hur ofta och vilket säkerhetskopieringsfönster som ska göras tillgängligt.

>[!NOTE]
>
>Precis som med andra aspekter av implementeringen av AEM måste strategin för säkerhetskopiering och återställning utvecklas och testas i en utvecklings- eller staging-miljö innan den används i produktionen för att säkerställa att hela lösningen fungerar som förväntat utan dataförlust.

Adobe Experience Manager (AEM) är en integrerad del av AEM formulär. Därför måste du även säkerhetskopiera AEM och synkronisera med säkerhetskopiering AEM formulär som Correspondence Management-lösning och -tjänster, t.ex. formulärhanterare, baserat på data som lagras i AEM del av AEM formulär. För att förhindra dataförlust måste AEM formulärspecifika data säkerhetskopieras på ett sätt som säkerställer att GDS och AEM (databasen) korrelerar med databasreferenser. Databasen, GDS, AEM och Content Storage Root-katalogerna måste återställas till en dator med samma DNS namnet som original.

## Olika typer av säkerhetskopiering {#types-of-backups}

AEM strategi för säkerhetskopiering av formulär omfattar två typer av säkerhetskopiering:

**Systemavbildning:** En fullständig säkerhetskopia av systemet som du kan använda för att återställa datorns innehåll om hårddisken eller hela datorn slutar att fungera. Säkerhetskopiering av systemavbildning krävs endast innan AEM distribueras. Interna regler styr sedan hur ofta säkerhetskopiering av systemavbildningar krävs.

**AEM blanketter:** Programdata finns i databasen, GDS (Global Document Storage) och AEM och måste säkerhetskopieras i realtid. GDS är en katalog som används för att lagra långlivade filer som används i en process. Dessa filer kan innehålla PDF, profiler eller formulärmallar.

>[!NOTE]
>
>Om Content Services (Deprecated) är installerat säkerhetskopierar du även rotkatalogen för innehållslagring. Se [Rotkatalog för innehållslagring (endast innehållstjänster)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only).

Databasen används för att lagra formulärartefakter, tjänstkonfigurationer, processtillstånd och databasreferenser till GDS-filer. Om du har aktiverat dokumentlagring i databasen lagras beständiga data och dokument i GDS också i databasen. Databasen kan säkerhetskopieras och återställas på följande sätt:

* **Säkerhetskopiering av ögonblicksbild** I det här läget anges att systemet för AEM formulär är i säkerhetskopieringsläge antingen oändligt eller under ett visst antal minuter. Därefter är säkerhetskopieringsläget inte längre aktiverat. Om du vill gå in i eller lämna läget för säkerhetskopiering av ögonblicksbilder kan du använda något av följande alternativ. Efter ett återställningsscenario bör läget för ögonblicksbildssäkerhetskopiering inte aktiveras.

   * Använd sidan Inställningar för säkerhetskopiering i administrationskonsolen. Markera kryssrutan Använd i säkert säkerhetskopieringsläge om du vill aktivera ögonblicksbildläge. Avmarkera kryssrutan för att avsluta läget för ögonblicksbild.
   * Använd skriptet LCBackupMode (se [Säkerhetskopiera katalogerna database, GDS och Content Storage Root](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories)). Om du vill avsluta läget för säkerhetskopiering av ögonblicksbilder anger du i skriptargumentet `continuousCoverage` parameter till `false` eller använder `leaveContinuousCoverage` alternativ.
   * Använd det angivna API:t för säkerhetskopiering/återställning. <!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* **Rullande säkerhetskopiering** -läget anger att systemet alltid är i säkerhetskopieringsläge, med en ny session för säkerhetskopieringsläge initierad så snart som föregående session släpps. Ingen timeout är associerad med rullande säkerhetskopieringsläge. När skriptet eller API:erna för LCBackupMode anropas för att lämna det rullande säkerhetskopieringsläget påbörjas en ny session för rullande säkerhetskopieringsläge. Det här läget är användbart när du vill ha stöd för kontinuerlig säkerhetskopiering men ändå vill att gamla och obehövliga dokument ska rensas bort från GDS-katalogen. Läget för rullande säkerhetskopiering stöds inte via sidan Säkerhetskopiering och återställning. Efter ett återställningsscenario är läget för rullande säkerhetskopiering fortfarande aktiverat. Du kan lämna det kontinuerliga säkerhetskopieringsläget (rullande säkerhetskopieringsläge) genom att använda skriptet LCBackupMode med `leaveContinuousCoverage` alternativ.

>[!NOTE]
>
>Om du lämnar det rullande säkerhetskopieringsläget omedelbart startas en ny session i säkerhetskopieringsläge. Om du vill inaktivera läget för rullande säkerhetskopiering fullständigt använder du `leaveContinuousCoverage` i skriptet, som skriver över den befintliga rullande säkerhetskopieringssessionen. I läget för säkerhetskopiering av ögonblicksbilder kan du lämna säkerhetskopieringsläget som vanligt.

För att förhindra dataförlust måste de AEM formulärspecifika data säkerhetskopieras på ett sätt som säkerställer att dokument i GDS- och Content Storage Root-katalogen korrelerar med databasreferenser.

>[!NOTE]
>
>När GDS lagras i filsystemet och inte i databasen, utför du säkerhetskopieringen före GDS-säkerhetskopieringen.

## Specialöverväganden för säkerhetskopiering och återställning {#special-considerations-for-backup-and-recovery}

Använd följande riktlinjer om du måste återställa AEM formulär till en annan miljö på grund av följande ändringar:

* Ändringar i IP-adressen, värdnamnet eller porten för AEM formulärserver
* Ändringar i enhetsbokstäver eller katalogsökväg
* Byt till en annan databasvärd, port eller namn

Sådana återställningsscenarier orsakas vanligtvis av maskinvarufel på servern som är värd för programservern, databasservern eller formulärservern. Förutom de AEM formulärspecifika konfigurationer som beskrivs i det här avsnittet, bör du även göra nödvändiga ändringar för andra delar av distributionen av AEM, som belastningsutjämnare och brandväggar, om värdnamnet eller IP-adressen för en AEM formulärserver ändras.

### Vad kan inte ändras {#what-cannot-be-changed}

Även om du kan ändra databasservern och många andra parametrar kan du inte ändra programservertypen eller databastypen när du återställer AEM från en säkerhetskopia. Om du till exempel återställer en säkerhetskopia av AEM kan du inte ändra programservern från JBoss till WebLogic eller databasen från Oracle till DB2. Dessutom måste återskapade AEM använda samma sökvägar i filsystemet som teckensnittskatalogen.

### Starta om efter återställning {#restarting-after-a-recovery}

Innan du startar om formulärservern efter en återställning gör du följande:

1. Starta systemet i underhållsläge.
1. Gör följande för att se till att Form Manager synkroniseras med AEM formulär i underhållsläge:

   1. Gå till https://*server*>:&lt;*port*>/lc/fm och logga in med autentiseringsuppgifter för adminstrator/password.
   1. Klicka på namnet på användaren (superadministratör i det här fallet) längst upp till höger.
   1. Klicka **Administratörsalternativ**.
   1. Klicka **Starta** för att synkronisera resurser från databasen.

1. I en klustrad miljö ska den primära noden (med avseende på AEM) vara uppe före de sekundära noderna.
1. Se till att inga processer initieras från interna eller externa källor som Web-, SOAP- eller EJB-processinitierare förrän systemets normala funktion har validerats.

Om huvuddatabasen AEM formulär flyttas eller ändras läser du de installationsguider som är relevanta för programservern för att få information om hur du uppdaterar databasanslutningsinformationen för AEM formulärdatakällor IDP_DS och EDC_DS.

### Ändra värdnamn eller IP-adress för AEM formulär {#changing-the-aem-forms-hostname-or-ip-address}

Om du använder TCP-cachelagring i stället för UDP i ett kluster måste du uppdatera cachepositionerarkonfigurationen. Mer information finns i&quot;Konfigurera cachelagringsplatser (endast cachelagring med TCP)&quot; i den konfigurationsguide som är relevant för programservern.

### Ändra sökvägar för AEM formulärnodfil {#changing-the-aem-forms-node-file-system-paths}

Om du ändrar filsystemsökvägarna för en fristående nod måste du uppdatera lämpliga referenser i inställningar, andra systemkonfigurationer, anpassade program och distribuerade AEM formulärprogram. För ett kluster måste alla noder däremot använda samma sökvägskonfiguration i filsystemet. Du måste ange rotkatalogen för GDS (Global Document Storage) och se till att den pekar på en kopia av den återställda GDS-servern som är synkroniserad med den återställda databasen. Det är viktigt att ange GDS-sökvägen eftersom GDS kan innehålla data som ska finnas kvar mellan omstarter av programservern.

I en klustrad miljö bör databasens filsystemskonfiguration vara densamma för alla klusternoder före och efter säkerhetskopieringen.

Använd `LCSetGDS`skript i `[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline` mapp för att ange GDS-sökvägen när du har ändrat filsystemsökvägarna. Se `ReadMe.txt` i samma mapp för mer information. Om den gamla GDS-katalogsökvägen inte kan användas, `LCSetGDS` måste användas för att ange den nya sökvägen till GDS innan du börjar AEM formulär.

>[!NOTE]
>
>Den här begränsningen är den enda under vilken du bör använda det här skriptet för att ändra GDS-platsen. Använd administrationskonsolen om du vill ändra GDS-platsen medan AEM är igång. (Se [Konfigurera allmänna inställningar AEM formulär](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)*.) *

När du har angett GDS-sökvägen startar du formulärservern i underhållsläge och använder administrationskonsolen för att uppdatera de återstående filsystemsökvägarna för den nya noden. När du har verifierat att alla nödvändiga konfigurationer har uppdaterats startar du om och testar AEM.
