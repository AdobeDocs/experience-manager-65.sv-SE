---
title: Förbereder AEM-formulär för säkerhetskopiering
seo-title: Förbereder AEM-formulär för säkerhetskopiering
description: 'null'
seo-description: 'null'
uuid: b8ef2bed-62e2-4000-b55a-30d2fc398a5f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e747147e-e96d-43c7-87b3-55947eef81f5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Förbereder AEM-formulär för säkerhetskopiering {#preparing-aem-forms-for-backup}

## Om tjänsten Säkerhetskopiering och återställning {#about-the-backup-and-restore-service}

Med tjänsten Säkerhetskopiering och återställning kan du ställa in AEM Forms i *säkerhetskopieringsläge*, vilket gör det möjligt att göra säkerhetskopieringar. Säkerhetskopierings- och återställningstjänsten utför inte någon säkerhetskopiering av AEM-formulär eller återställning av systemet. I stället försätts servern i ett läge där det går att utföra konsekventa och tillförlitliga säkerhetskopieringar samtidigt som servern kan fortsätta att köras. Du ansvarar för åtgärderna för att säkerhetskopiera GDS (Global Document Storage) och databasen som är ansluten till formulärservern. GDS är en katalog som används för att lagra filer som används i en långvarig process.

Säkerhetskopieringsläget är ett läge som servern försätts i så att filer i GDS inte rensas när en säkerhetskopieringsprocedur utförs. I stället skapas underkataloger under GDS-katalogen för att behålla en post med filer som ska rensas när säkerhetskopieringsläget har avslutats. En fil är avsedd att överleva systemomstarter och kan sträcka sig över flera dagar eller till och med år. Dessa filer utgör en viktig del av formulärserverns övergripande status och kan innehålla PDF-filer, profiler eller formulärmallar. Om någon av dessa filer förloras eller skadas kan processerna på formulärservern bli instabila och data gå förlorade.

Du kan välja att utföra säkerhetskopiering av ögonblicksbilder, där du vanligtvis aktiverar säkerhetskopieringsläget under en period och sedan lämnar säkerhetskopieringsläget när du har slutfört säkerhetskopieringsaktiviteterna. Du måste lämna säkerhetskopieringsläget för att filer ska kunna rensas från GDS så att de inte växer i onödan. Du kan antingen lämna säkerhetskopieringsläget explicit eller vänta på att tiden ska gå ut i en session i säkerhetskopieringsläge.

Du kan också lämna servern i permanent säkerhetskopieringsläge, vilket är typiskt för strategier för säkerhetskopiering vid rullande säkerhetskopiering eller kontinuerlig systemtäckning. Läget för rullande säkerhetskopiering anger att systemet alltid är i säkerhetskopieringsläge, med en ny session i säkerhetskopieringsläge initierad så snart som föregående session släpps. I läget för kontinuerlig säkerhetskopiering töms en fil efter två sessioner med säkerhetskopieringsläge och refereras inte längre till den.

Du kan använda tjänsten Säkerhetskopiering och återställning för att lägga till befintliga program eller nya program som du skapar för att utföra säkerhetskopieringar av GDS eller databasen som är ansluten till formulärservern.

>[!NOTE]
>
>Precis som med andra aspekter av implementeringen av AEM Forms bör strategin för säkerhetskopiering och återställning utvecklas och testas i en utvecklings- eller staging-miljö innan den används i produktionen för att säkerställa att hela lösningen fungerar som förväntat utan dataförlust.

Du kan utföra följande åtgärder med tjänsten Säkerhetskopiera och återställ:

* Gå till säkerhetskopieringsläge.
* Lämna säkerhetskopieringsläget.

>[!NOTE]
>
>Mer information om vad du bör tänka på när du gör säkerhetskopieringar för AEM Forms finns i [administrationshjälpen](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Mer information om tjänsten Backup and Restore finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Läget Säkerhetskopiera på formulärservern aktiveras {#entering-backup-mode-on-the-forms-server}

Du aktiverar säkerhetskopieringsläget för att tillåta säkerhetskopiering av en formulärserver. När du aktiverar säkerhetskopieringsläge anger du följande information baserat på din organisations procedurer för säkerhetskopiering:

* En unik etikett som identifierar den session i säkerhetskopieringsläget som kan vara användbar för dina säkerhetskopieringsprocesser.
* Den tid det tar för säkerhetskopieringen att slutföras.
* En flagga som anger om du ska vara i kontinuerligt säkerhetskopieringsläge, vilket bara är användbart om du utför rullande säkerhetskopiering.

Innan du skriver program som ska gå in i säkerhetskopieringsläge bör du känna till de säkerhetskopieringsprocedurer som ska användas när formulärservern har placerats i säkerhetskopieringsläge. Mer information om vad du bör tänka på när du gör säkerhetskopieringar för AEM Forms finns i [administrationshjälpen](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Mer information om tjänsten Backup and Restore finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary-of-steps}

Så här skapar du ett program som övergår till säkerhetskopieringsläge:

1. Inkludera projektfiler.
1. Skapa ett BackupService-klientobjekt.
1. Bestäm en unik etikett, hur lång tid säkerhetskopieringen ska utföras och om den ska vara i kontinuerligt säkerhetskopieringsläge.
1. Gå till säkerhetskopieringsläge.
1. (Valfritt) Hämta information om sessionen för säkerhetskopieringsläge på servern.
1. Säkerhetskopiera GDS (Global Data Store) och databasen.

**Inkludera projektfiler**

Inkludera nödvändiga filer i utvecklingsprojektet. Dessa filer är viktiga att inkludera i ditt projekt för att kompilera koden på rätt sätt och använda API:t för tjänsten Backup and Restore.

Mer information om var dessa filer finns i [Inkludera Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)för AEM Forms.

**Skapa ett BackupService Client API-objekt**

Om du vill lämna säkerhetskopieringsläget programmatiskt skapar du ett BackupService-klientobjekt som ska använda API:t för tjänsten för säkerhetskopiering och återställning.

**Bestäm på en unik etikett, bestäm hur lång tid säkerhetskopieringen ska utföras och bestäm om den ska vara i kontinuerligt säkerhetskopieringsläge**

Innan du går in i säkerhetskopieringsläget bör du bestämma en unik etikett, fastställa hur lång tid du vill tilldela för att utföra säkerhetskopieringen och bestämma om du vill att formulärservern ska vara i säkerhetskopieringsläge. Dessa överväganden är viktiga att integrera med de säkerhetskopieringsprocedurer som din organisation har fastställt. (Se [Administrationshjälp](https://www.adobe.com/go/learn_aemforms_admin_63).)

**Ange säkerhetskopieringsläge**

Använd säkerhetskopieringsläget med de parametrar som överensstämmer med de säkerhetskopieringsprocedurer som används i organisationen.

**Hämta information om sessionen för säkerhetskopieringsläge på servern**

När du har aktiverat säkerhetskopieringsläget kan du hämta information om sessionen. Den här informationen kan användas för att integrera med dina säkerhetskopieringsprocedurer

**Säkerhetskopiera GDS och databasen**

När du har aktiverat säkerhetskopieringsläget kan du säkerhetskopiera GDS (Global Document Storage) och den databas som formulärservern är ansluten till. Det här steget är specifikt för din organisation eftersom du kan utföra det här steget manuellt eller köra andra verktyg för att utföra säkerhetskopieringsproceduren.

### Ange säkerhetskopieringsläge med Java API {#enter-backup-mode-using-the-java-api}

Ange säkerhetskopieringsläge med API:t för säkerhetskopiering och återställning:

1. Inkludera projektfiler

   Inkludera nödvändiga JAR-klientfiler, t.ex. adobe-backup-restore-client-sdk.jar, i klassökvägen för Java-projektet. Om du vill skapa Java-klientprogrammet måste följande JAR-filer läggas till i projektets klasssökväg:

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (krävs om AEM Forms distribueras på JBoss Application Server)
   * jbossall-client.jar (krävs om AEM Forms distribueras på JBoss Application Server)

1. Skapa ett BackupService Client API-objekt

   Du använder ett `ServiceClientFactory` objekt och BackupService klient-API-objektet tillsammans.

   * Skapa ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper. (Se [Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Skapa ett `BackupService` objekt med hjälp av dess konstruktor och skicka `ServiceClientFactory` objektet.

1. Bestäm på en unik etikett, bestäm hur lång tid säkerhetskopieringen ska utföras och bestäm om den ska vara i kontinuerligt säkerhetskopieringsläge

   Bestäm på en unik etikett, bestäm hur lång tid du vill tilldela för att utföra säkerhetskopieringen och bestäm om du vill att formulärservern ska vara i kontinuerligt säkerhetskopieringsläge.

1. Ange säkerhetskopieringsläge

   Ange säkerhetskopieringsläge genom att anropa `enterBackupMode` metoden med följande parametrar:

   * Ett `String` värde som anger en unik etikett som kan läsas av människor och som identifierar sessionen för säkerhetskopieringsläge. Du bör inte använda blanksteg eller tecken som inte kan kodas i XML-format.
   * Ett `int` värde som anger antalet minuter som ska behållas i säkerhetskopieringsläge. Du kan ange ett värde från `1` till `10080` (antalet minuter i en vecka). Detta värde ignoreras när läget för kontinuerlig säkerhetskopiering används.
   * Ett `Boolean` värde som anger om det ska vara i kontinuerligt säkerhetskopieringsläge. Värdet `True` anger att den ska vara i kontinuerligt säkerhetskopieringsläge. I läget för kontinuerlig säkerhetskopiering ignoreras det värde du anger för hur många minuter som ska vara kvar i läget för säkerhetskopiering.

      Kontinuerligt säkerhetskopieringsläge innebär att en ny session i säkerhetskopieringsläge startas när den aktuella sessionen har slutförts. Värdet är `False` att kontinuerligt säkerhetskopieringsläge inte används och att rensning av filer från GDS återupptas efter att säkerhetskopieringsläget har avslutats.

1. Hämta information om sessionen för säkerhetskopieringsläge på servern

   Hämta information med objektet som `BackupModeEntryResult` returneras efter att `enterBackupMode` metoden anropats. Den information du kan hämta när du har aktiverat säkerhetskopieringsläget kan vara användbar för integrering med dina säkerhetskopieringsprocedurer. Etiketten, säkerhetskopierings-ID:t och starttiden kan till exempel vara användbara som indata för filnamn för säkerhetskopieringsproceduren.

1. Säkerhetskopiera GDS och databasen

   Säkerhetskopiera GDS (Global Document Storage) och den databas som formulärservern är ansluten till. Säkerhetskopieringsåtgärderna ingår inte i AEM Forms SDK och kan till och med innehålla manuella steg som är specifika för säkerhetskopieringsrutinerna i organisationen.

### Ange säkerhetskopieringsläge med webbtjänstens API {#enter-backup-mode-using-the-web-service-api}

Ange säkerhetskopieringsläge med webbtjänsten som tillhandahålls av API:t för tjänsten Backup and Restore:

1. Inkludera projektfiler

   * Skapa en Microsoft .NET-klientsammansättning som använder WSDL för API:t för tjänsten för säkerhetskopiering och återställning.
   * Referera till Microsoft .NET-klientsammansättningen.

1. Skapa ett BackupService Client API-objekt

   Skapa ett objekt med Microsoft .NET-klientsammansättningen genom att anropa dess standardkonstruktor och ange autentiseringsuppgifterna med `BackupServiceService` `Credentials` metoden.

1. Bestäm på en unik etikett, bestäm hur lång tid säkerhetskopieringen ska utföras och bestäm om den ska vara i kontinuerligt säkerhetskopieringsläge

   Bestäm på en unik etikett, bestäm hur lång tid du vill tilldela för att utföra säkerhetskopieringen och bestäm om du vill att formulärservern ska vara i kontinuerligt säkerhetskopieringsläge.

1. Ange säkerhetskopieringsläge

   Aktivera metoden enterBackupMode och skicka följande värden för att aktivera säkerhetskopieringsläget:

   * Ett `String` värde som anger en unik etikett som kan läsas av människor och som identifierar sessionen för säkerhetskopieringsläge. Du bör inte använda blanksteg eller tecken som inte kan kodas i XML-format.
   * Ett `Uint32` värde som anger antalet minuter som ska behållas i säkerhetskopieringsläge. Du kan ange ett värde mellan `1` och `10080` (antal minuter i en vecka). Detta värde ignoreras när läget för kontinuerlig säkerhetskopiering används.
   * Ett `Boolean` värde som anger om det ska vara i kontinuerligt säkerhetskopieringsläge. Värdet `True` anger att den ska vara i kontinuerligt säkerhetskopieringsläge. I läget för kontinuerlig säkerhetskopiering ignoreras det värde du anger för hur många minuter som ska vara kvar i läget för säkerhetskopiering. Kontinuerligt säkerhetskopieringsläge innebär att en ny session i säkerhetskopieringsläge startas när den aktuella sessionen har slutförts.

      Värdet är `False` att kontinuerligt säkerhetskopieringsläge inte används och att rensning av filer från GDS återupptas efter att säkerhetskopieringsläget har avslutats.

1. Hämta information om sessionen för säkerhetskopieringsläge på servern

   Hämta information om säkerhetskopieringsläget när du har anropat metoden enterBackupMode från BackupModeEntryResult som returneras för att bekräfta att den lyckades. Den information du kan hämta när du har aktiverat säkerhetskopieringsläget kan vara användbar för integrering med dina säkerhetskopieringsprocedurer. Etiketten, säkerhetskopierings-ID:t och starttiden kan till exempel vara användbara som indata för filnamn för säkerhetskopieringsproceduren.

1. Säkerhetskopiera GDS och databasen

   Säkerhetskopiera GDS (Global Document Storage) och den databas som formulärservern är ansluten till. Säkerhetskopieringsåtgärderna ingår inte i AEM Forms SDK och kan till och med innehålla manuella steg som är specifika för säkerhetskopieringsrutinerna i organisationen.

## Avslutar säkerhetskopieringsläge på formulärservern {#leaving-backup-mode-on-the-forms-server}

Du lämnar säkerhetskopieringsläget så att formulärservern fortsätter att tömma filer från GDS (Global Document Storage) på formulärservern.

Innan du skriver program för att övergå till viloläge rekommenderar vi att du förstår de säkerhetskopieringsprocedurer som används med AEM Forms. Mer information om vad du bör tänka på när du gör säkerhetskopieringar för AEM Forms finns i [administrationshjälpen](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>Mer information om tjänsten Backup and Restore finns i [Tjänstreferens för AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Sammanfattning av steg {#summary_of_steps-1}

Så här lämnar du säkerhetskopieringsläget:

1. Inkludera projektfiler.
1. Skapa ett BackupService-klientobjekt.
1. Lämna säkerhetskopieringsläget.
1. (Valfritt) Hämta information om sessionen för säkerhetskopieringsläge som kördes på formulärservern.

**Inkludera projektfiler**

Inkludera alla nödvändiga filer i utvecklingsprojektet. De här filerna är viktiga för att kompilera koden på rätt sätt och för att använda API:t för tjänsten för säkerhetskopiering och återställning.

Mer information om var dessa filer finns i [Inkludera Java-biblioteksfiler](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)för AEM Forms.

**Skapa ett BackupService Client API-objekt**

Om du vill lämna säkerhetskopieringsläget programmatiskt skapar du ett BackupService-klientobjekt som ska använda API:t för tjänsten för säkerhetskopiering och återställning.

**Lämna säkerhetskopieringsläge**

Lämna säkerhetskopieringsläget för att återuppta normal rensning av filer från GDS (Global Document Storage). Innan du lämnar säkerhetskopieringsläget bör du kontrollera att dina säkerhetskopieringsprocedurer har slutförts.

**Hämta information om sessionen för säkerhetskopieringsläget som avslutades**

När du lämnar säkerhetskopieringsläget kan du hämta information om sessionen. Den här informationen kan användas för att integrera med dina säkerhetskopieringsprocedurer.

### Lämna säkerhetskopieringsläget med Java API {#leave-backup-mode-using-the-java-api}

Lämna säkerhetskopieringsläget med hjälp av API:t för säkerhetskopiering och återställning (Java):

1. Inkludera projektfiler

   Inkludera nödvändiga JAR-klientfiler, t.ex. adobe-backup-restore-client-sdk.jar, i klassökvägen för Java-projektet. Om du vill skapa ett Java-klientprogram måste följande JAR-filer läggas till i projektets klasssökväg:

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar (krävs om AEM Forms distribueras på JBoss Application Server)
   * jbossall-client.jar (krävs om AEM Forms distribueras på JBoss Application Server)

1. Skapa ett BackupService Client API-objekt

   Du använder ett `ServiceClientFactory` objekt och BackupService klient-API-objektet tillsammans.

   * Skapa ett `ServiceClientFactory` objekt som innehåller anslutningsegenskaper. (Se [Ange anslutningsegenskaper](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Skapa ett `BackupService` objekt med hjälp av dess konstruktor och skicka `ServiceClientFactory` objektet som parameter.

1. Ange säkerhetskopieringsläge

   Lämna säkerhetskopieringsläget genom att anropa `leaveBackupMode` metoden.

1. Hämta information om sessionen för säkerhetskopieringsläge på servern

   Hämta information om åtgärden med det returnerade `BackupModeResult` objektet. Den information du kan hämta när du har aktiverat säkerhetskopieringsläget kan vara användbar för integrering med dina säkerhetskopieringsprocedurer. Etiketten, säkerhetskopierings-ID:t och starttiden kan till exempel vara användbara som indata för filnamn för säkerhetskopieringsproceduren.

### Lämna säkerhetskopieringsläget med hjälp av webbtjänstens API {#leave-backup-mode-using-the-web-service-api}

Lämna säkerhetskopieringsläget med hjälp av API:t för säkerhetskopiering och återställning (webbtjänsten):

1. Inkludera projektfiler

   Om du vill använda webbtjänster måste du se till att du inkluderar proxyfilerna. Följ de här stegen för att konfigurera projektet så att det använder API:t för tjänsten för säkerhetskopiering och återställning som en webbtjänst.

   * Skapa en Microsoft .NET-klientsammansättning som använder WSDL för API:t för tjänsten för säkerhetskopiering och återställning.
   * Referera till Microsoft .NET-klientsammansättningen.

1. Skapa ett BackupService Client API-objekt

   Skapa ett objekt med Microsoft .NET-klientsammansättningen genom att anropa dess standardkonstruktor. `BackupServiceService`

1. Ange säkerhetskopieringsläge

   Lämna säkerhetskopieringsläget genom att anropa `leaveBackupMode` webbtjänståtgärden.

1. Hämta information om sessionen för säkerhetskopieringsläge på servern

   Hämta identifieraren för säkerhetskopieringsläget efter åtgärden för att verifiera att den lyckades. Den information du kan hämta när du lämnar säkerhetskopieringsläget kan vara användbar för integrering med dina säkerhetskopieringsprocedurer.

