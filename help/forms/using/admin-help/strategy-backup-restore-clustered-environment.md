---
title: Strategi för säkerhetskopiering och återställning i en klustrad miljö
seo-title: Strategi för säkerhetskopiering och återställning i en klustrad miljö
description: Om AEM-formulärimplementeringen lagrar ytterligare anpassade data i en annan databas måste du implementera en strategi för att säkerhetskopiera dessa data, så att de är synkroniserade med AEM-formulärdata.
seo-description: Om AEM-formulärimplementeringen lagrar ytterligare anpassade data i en annan databas måste du implementera en strategi för att säkerhetskopiera dessa data, så att de är synkroniserade med AEM-formulärdata.
uuid: c29b989c-30ed-4a8e-bab8-9b7746291a33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c332985b-4556-4056-961a-fce2356da88d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Strategi för säkerhetskopiering och återställning i en klustrad miljö {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>Om AEM-formulärimplementeringen lagrar ytterligare anpassade data i en annan databas måste du implementera en strategi för att säkerhetskopiera dessa data, så att de är synkroniserade med AEM-formulärdata. Dessutom måste programmet vara utformat så att det är tillräckligt robust för att hantera ett scenario där ytterligare databaser inte är synkroniserade. Vi rekommenderar starkt att alla databasåtgärder som utförs utförs i samband med en transaktion för att upprätthålla ett konsekvent tillstånd.

Du behöver säkerhetskopiera följande delar av AEM-formulärsystemet för att kunna återställa efter eventuella fel:

* Databas som används i AEM-formulär
* GDS som har långlivade data och andra beständiga dokument
* AEM-databas (crx-database)

>[!NOTE]
>
>Du måste säkerhetskopiera alla andra data som används i AEM-formulärinställningarna, som kundteckensnitt, anslutningsdata osv.

## Säkerhetskopiera en klustrad miljö {#back-up-a-clustered-environment}

I det här avsnittet diskuteras följande strategier för att säkerhetskopiera alla grupperade AEM-formulär:

* Offlinesäkerhetskopiering med driftstopp
* Offlinesäkerhetskopiering utan driftstopp (säkerhetskopiering av en slavnod som är avstängd)
* Onlinesäkerhetskopiering utan driftstopp och fördröjning
* Säkerhetskopiera Bootstrap-egenskapsfilen

### Offlinesäkerhetskopiering med driftstopp {#offline-backup-with-downtime}

1. Stäng av hela klustret och tillhörande tjänster. (se [Starta och stoppa tjänster](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Säkerhetskopiera databasen, GDS och Connectors på alla noder. (se [Filer som ska säkerhetskopieras och återställas](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Gör så här för att säkerhetskopiera AEM-databasen offline:

   1. För varje klusternod säkerhetskopierar du filen som innehåller klusternods-ID:t.
   1. Säkerhetskopiera alla filer i valfri underkatalognod, inklusive underkataloger.
   1. Säkerhetskopiera databas-/system-ID för varje klusternod separat.
   Detaljerade anvisningar finns i [Säkerhetskopiera och återställ](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html).

1. Säkerhetskopiera alla andra data, till exempel kundens typsnitt.
1. Starta klustret igen.

### Säkerhetskopiering offline utan driftstopp {#offline-backup-with-no-downtime}

1. Ange läget för rullande säkerhetskopiering. (se [Ange säkerhetskopieringslägen](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   Observera att vi måste lämna det rullande säkerhetskopieringsläget efter en återställning.

1. Stäng någon av klusterets slavnoder med avseende på AEM. (se [Starta och stoppa tjänster](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Säkerhetskopiera databasen, GDS och Connectors på alla noder. (se [Filer som ska säkerhetskopieras och återställas](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Gör så här för att säkerhetskopiera AEM-databasen offline:

   1. För varje klusternod säkerhetskopierar du filen som innehåller klusternods-ID:t.
   1. Säkerhetskopiera alla filer i valfri underkatalognod, inklusive underkataloger.
   1. Säkerhetskopiera repository/system.id av varje klusternod separat.
   Detaljerade anvisningar finns i [Säkerhetskopiera och återställ](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html).

1. Säkerhetskopiera alla andra data, till exempel kundens typsnitt.
1. Starta klustret igen.

### Onlinesäkerhetskopiering utan driftstopp och fördröjning {#online-backup-with-no-downtime-but-delay-in-response}

1. Ange läget för rullande säkerhetskopiering. (se [Ange säkerhetskopieringslägen](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   Observera att du måste lämna det rullande säkerhetskopieringsläget efter en återställning.

1. Stäng någon av klusterets slavnoder med avseende på AEM. (se [Starta och stoppa tjänster](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. Säkerhetskopiera databasen, GDS och Connectors på alla noder. (se [Filer som ska säkerhetskopieras och återställas](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. Gör så här för att säkerhetskopiera AEM-databasen online:

   1. För varje klusternod säkerhetskopierar du filen som innehåller Cluster_node.id.
   1. Säkerhetskopiera repository/system.id av varje klusternod separat.
   1. På valfri slavnod gör du en onlinesäkerhetskopiering av databasen. Mer information finns i Onlinesäkerhetskopiering.

1. Säkerhetskopiera alla andra data, till exempel kundens typsnitt.
1. Starta klustret igen.

### Säkerhetskopiera Bootstrap-egenskapsfilen {#back-up-the-bootstrap-properties-file}

När vi skapar ett AEM-kluster skapas en egenskapsfil i programservern för alla slavnoder. Vi rekommenderar att du säkerhetskopierar Bootstrap-egenskapsfilen. Du kan hitta filen på följande plats på programservern:

* JBoss: i BIN-katalogen
* WebLogic: i domänkatalogen
* WebSphere: i profilkatalogen

Du måste säkerhetskopiera filen för ett återställningsscenario för AEM-slavnod och ersätta den på den angivna platsen på programservern, om den återställs.

## Återställning i en klustrad miljö {#recovery-in-a-clustered-environment}

Om fel uppstår i hela klustret eller en enda nod måste du återställa den med hjälp av säkerhetskopian.

För en återställning av en nod behöver du bara stänga av den enskilda noden och köra återställningsproceduren för en nod.

Om hela klustret inte fungerar på grund av fel som t.ex. databaskrascher måste du utföra följande steg. Återställning beror på vilken säkerhetskopieringsmetod som används.

### Återställa en enskild nod {#restoring-a-single-node}

1. Stoppa den skadade noden.

   >[!NOTE]
   >
   >Om den skadade noden är en AEM-huvudnod stänger du av hela klusternoden.

1. Återskapa det fysiska systemet från en systemavbildning.
1. Använd patchar eller uppdateringar i AEM-formulär som har använts sedan bilden skapades. Denna information registrerades under säkerhetskopieringen. AEM-formulär måste återställas till samma korrigeringsnivå som när systemet säkerhetskopierades.
1. (*Valfritt*) Om alla andra noder fungerar som de ska kan även AEM-databasen vara skadad. I så fall visas ett osynkroniserat databasmeddelande i filen error.log i AEM-databasen.

   Så här återställer du databasen:

   >[!NOTE]
   >
   >Om en zippad crx-database backup togs online, packa upp den på valfri plats och följ processen för offlineåterställning.

   1. Ta bort katalogerna för databasen, delade arbetsytor, versioner och arbetsytor i katalogen ClusterNode i noden.
   1. Återställ säkerhetskopian av klusternoden (inklusive underkataloger) till noden.
   1. Ta bort filen clusterNode/revision.log på noden.
   1. Ta bort .lock-koden på noden, om sådan finns.
   1. Ta bort repository/system.id på noden, om det finns någon.
   1. Ta bort filerna &amp;ast;&amp;ast;/listener.properties på noden, om sådan finns.
   1. Återställ repository/cluster_node.id för enskilda klusternoder.

>[!NOTE]
>
>Tänk på följande:

* Om den misslyckade noden var en AEM-huvudnod kopierar du allt innehåll från den underordnade databasmappen (crx-database\crx.0000 där 000 kan vara valfri siffra) till databasmappen crx-database och tar bort den underordnade databasmappen.
* Innan du startar om en klusternod måste du ta bort databasen /clustered.txt från huvudnoden.
* Se till att huvudnoden startas först och starta andra noder när den är helt klar.

### Återställer hela klustret {#restoring-the-entire-cluster}

1. Stoppa alla klusternoder.
1. Återskapa det fysiska systemet från en systemavbildning.
1. Använd patchar eller uppdateringar i AEM-formulärAEM-formulär som har använts sedan bilden skapades. Denna information registrerades i steg 1 av säkerhetskopieringsproceduren. AEM-formulär måste återställas till samma korrigeringsnivå som när systemet säkerhetskopierades.
1. Återställ databasen, GDS och Connectors.
1. Så här återställer du AEM-databasen offline:

   >[!NOTE]
   >
   >Om en zippad crx-database backup togs online, packa upp den på valfri plats och följ processen för offlineåterställning.

   1. På alla klusternoder tar du bort katalogerna för databasen, delade arbetsytor, versioner och arbetsytor i mappen ClusterNode.
   1. Ta bort alla filer och kataloger i den delade katalogen.
   1. Återställ säkerhetskopian av klusternoden (inklusive underkataloger) till en klusternod.
   1. Kopiera alla filer i den återställda klusternoden till alla andra klusternoder. När du är klar innehåller varje klusternod samma data.
   1. Ta bort filen clusterNode/revision.log på alla klusternoder.
   1. Ta bort .lock på alla klusternoder, om det finns.
   1. Ta bort repository/system.id alla klusternoder, om sådana finns.
   1. Ta bort filerna &amp;ast;&amp;ast;/listener.properties på alla klusternoder, om sådana finns.
   1. Återställ repository/cluster_node.id för enskilda klusternoder.

>[!NOTE]
>
>Tänk på följande:

* Om den misslyckade noden var en AEM-huvudnod kopierar du allt innehåll från den underordnade databasmappen (den ser ut som crx-database\crx.0000 där 000 kan vara vilken siffra som helst) till databasmappen crx-database\.
* Innan du startar om en klusternod måste du ta bort databasen /clustered.txt från huvudnoden.
* Se till att huvudnoden startas först och starta andra noder när den är helt klar.

## Säkerhetskopiera och återställa publiceringsnoden för Correspondence Management Solution {#back-up-and-restore-correspondence-management-solution-publish-node}

Utgivarnoden har ingen master-slave-relation i en klustrad miljö. Du kan säkerhetskopiera alla Publisher-noder genom att följa [Säkerhetskopiera och återställa](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html).

### Återställa en enskild utgivarnod {#recover-a-single-publisher-node}

1. Stäng den nod som ska återställas och gör ingen publiceringsaktivitet förrän noden är uppe igen.
1. Återställ publiceringsnoden med [Återställ säkerhetskopian](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html#Restoring säkerhetskopian).

### Återställa ett kluster {#recover-a-cluster}

1. Stäng av klustret.
1. Återställ publiceringsnoden med [Återställ säkerhetskopian](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html#Restoring säkerhetskopian).
1. Starta huvudnoden följt av den underordnade noden i utvecklarklustret.

