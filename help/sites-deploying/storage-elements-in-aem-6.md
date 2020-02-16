---
title: Lagringselement i AEM 6.5
seo-title: Lagringselement i AEM 6.5
description: Lär dig mer om nodlagringsimplementeringar i AEM 6.5 och hur du underhåller databasen.
seo-description: Lär dig mer om nodlagringsimplementeringar i AEM 6.5 och hur du underhåller databasen.
uuid: 3b018830-c42e-48e0-9b6f-cd230b02d914
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0aa2c22f-32bb-4e50-8328-63ed73c0f19e
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# Lagringselement i AEM 6.5{#storage-elements-in-aem}

I den här artikeln ska vi ta upp:

* [Översikt över lagring i AEM 6](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [Underhålla databasen](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## Översikt över lagring i AEM 6 {#overview-of-storage-in-aem}

En av de viktigaste ändringarna i AEM 6 är innovationerna på databasnivå.

För närvarande finns det två nodlagringsimplementationer i AEM6: Tjärlagring och MongoDB-lagring.

### Tjärlagring {#tar-storage}

#### Köra en nyinstallerad AEM-instans med Tjäragring {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>PID:t för segmentnodarkivet har ändrats från org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService i tidigare versioner av AEM 6 till org.apache.jackrabbit.oak.segment.SegmentNodeStoreService i AEM 6.3. Se till att du gör de nödvändiga konfigurationsjusteringarna för att återspegla den här ändringen.

Som standard använder AEM 6 Tjärlagring för att lagra noder och binära filer med standardkonfigurationsalternativen. Så här konfigurerar du lagringsinställningarna manuellt:

1. Ladda ned AEM 6 quickstart jar och placera den i en ny mapp.
1. Packa upp AEM genom att köra:

   `java -jar cq-quickstart-6.jar -unpack`

1. Skapa en mapp med namnet `crx-quickstart\install` i installationskatalogen.

1. Skapa en fil som anropas `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` i den nyligen skapade mappen.

1. Redigera filen och ange konfigurationsalternativ. Följande alternativ är tillgängliga för Segment Node Store, som är grunden för AEM&#39;s TAR-lagringsimplementering:

   * `repository.home`: Sökväg till databasstartplats där olika databasrelaterade data lagras. Som standard lagras segmentfiler under katalogen crx-quickstart/segmentstore.
   * `tarmk.size`: Maximal storlek för ett segment i MB. Standardvärdet är 256 MB.

1. Starta AEM.

### Mongo-lagring {#mongo-storage}

#### Köra en nyinstallerad AEM-instans med Mongo Storage {#running-a-freshly-installed-aem-instance-with-mongo-storage}

AEM 6 kan konfigureras att köras med MongoDB-lagring enligt följande procedur:

1. Ladda ned AEM 6 quickstart jar och placera den i en ny mapp.
1. Packa upp AEM genom att köra följande kommando:

   `java -jar cq-quickstart-6.jar -unpack`

1. Kontrollera att MongoDB är installerat och att en instans av `mongod` körs. Mer information finns i [Installera MongoDB](https://docs.mongodb.org/manual/installation/).
1. Skapa en mapp med namnet `crx-quickstart\install` i installationskatalogen.
1. Konfigurera nodarkivet genom att skapa en konfigurationsfil med namnet på den konfiguration som du vill använda i `crx-quickstart\install` katalogen.

   I Document Node Store (som är grunden för AEM:s implementering av MongoDB-lagring) används en fil som kallas `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`

1. Redigera filen och ange konfigurationsalternativ. Följande alternativ är tillgängliga:

   * `mongouri`: Den [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) som krävs för att ansluta till Mongo-databasen. The default is `mongodb://localhost:27017`
   * `db`: Namn på Mongo-databasen. Som standard använder nya AEM 6-installationer **aem-author** som databasnamn.
   * `cache`: Cachestorleken i MB. Detta fördelas mellan olika cacheminnen som används i DocumentNodeStore. Standardvärdet är 256.
   * `changesSize`: Storlek i MB på den mappade samling som används i Mongo för cache-lagring av diff-utdata. Standardvärdet är 256.
   * `customBlobStore`: Booleskt värde som anger att ett anpassat datalager kommer att användas. Standardvärdet är false.

1. Skapa en konfigurationsfil med PID för det datalager som du vill använda och redigera filen för att ange konfigurationsalternativen. Mer information finns i [Konfigurera nodarkiv och datalager](/help/sites-deploying/data-store-config.md).

1. Starta AEM 6 jar med en MongoDB-lagringsserver genom att köra:

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   Där **`-r`** är serverdelens körningsläge. I det här exemplet börjar det med stöd för MongoDB.

#### Inaktivera genomskinliga stora sidor {#disabling-transparent-huge-pages}

Red Hat Linux använder en minneshanteringsalgoritm som kallas för Transparent Huge Pages (THP). Även om AEM utför finkorniga läsningar och skrivningar är THP optimerat för stora operationer. Därför rekommenderar vi att du inaktiverar THP för både Tjärs- och Mongo-lagring. Så här inaktiverar du algoritmen:

1. Öppna `/etc/grub.conf` filen i valfritt textredigeringsprogram.
1. Lägg till följande rad i **filen slib.conf** :

   ```
   transparent_hugepage=never
   ```

1. Kontrollera slutligen om inställningen har börjat gälla genom att köra:

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   Om THP är inaktiverat bör utdata för ovanstående kommando vara:

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>Du kan även använda följande resurser:
>
>* Mer information om genomskinliga stora sidor i Red Hat Linux finns i den här [artikeln](https://access.redhat.com/solutions/46111).
>* Linux-justeringstips finns i den här [artikeln](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html).
>



## Underhålla databasen {#maintaining-the-repository}

Varje uppdatering av databasen skapar en ny innehållsrevision. Det innebär att databasstorleken ökar för varje uppdatering. För att undvika okontrollerad databastillväxt måste gamla ändringar rensas bort för att frigöra diskutrymme. Den här underhållsfunktionen kallas Revision Cleanup. Revision Cleanup-funktionen frigör diskutrymme genom att ta bort föråldrade data från databasen. Mer information om Revision Cleanup finns på sidan [](/help/sites-deploying/revision-cleanup.md)Revision Cleanup.
