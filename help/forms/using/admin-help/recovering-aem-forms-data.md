---
title: Återställa AEM formulärdata
seo-title: Recovering the AEM forms data
description: I det här dokumentet beskrivs de steg som krävs för att återställa AEM formulärdata.
seo-description: This document describes the steps required to recover the AEM forms data.
uuid: b5735196-5a8d-4358-884f-e9b8d8f4f682
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e093114-219b-4018-9530-9002eb665448
exl-id: 9e648bab-9284-4fda-abb4-8bd7cd085981
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 0%

---

# Återställa AEM formulärdata {#recovering-the-aem-forms-data}

I det här avsnittet beskrivs de steg som krävs för att återställa AEM formulärdata. Se även [Specialöverväganden för säkerhetskopiering och återställning](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery).

>[!NOTE]
>
>Kataloger för databas, GDS, AEM och Content Storage Root måste återställas till en dator med samma DNS-namn som originalet.

AEM kan återställas på ett tillförlitligt sätt vid följande fel:

**Diskfel:** Det senaste säkerhetskopieringsmediet krävs för att återställa databasinnehållet.

**Skadade data:** Filsystemen registrerar inte tidigare transaktioner och systemen kan skriva över nödvändiga processdata av misstag.

**Användarfel:** Återställningen begränsas till de data som är tillgängliga i databasen. Om data har lagrats och är tillgängliga förenklas återställningen.

**Strömavbrott, systemkrasch:** Filsystems-API:er är ofta inte utformade eller används på ett robust sätt som skyddar mot oväntade systemfel. Om ett strömavbrott eller en systemkrasch inträffar är det troligare att dokumentinnehåll som lagras i databasen är uppdaterat än innehåll som lagras i ett filsystem.

Om du använder läget för rullande säkerhetskopiering är du fortfarande i säkerhetskopieringsläge efter återställning. Om du använder läget för säkerhetskopiering av ögonblicksbilder är du inte i säkerhetskopieringsläge efter återställning.

När du återställer från säkerhetskopiering till ett nytt system kan följande konfigurationer vara annorlunda. Den här skillnaden bör inte påverka en lyckad återställning av AEM formulärprogram:

* IP-adress
* Fysisk systemkonfiguration (CPU, disk, minne)
* GDS-plats

>[!NOTE]
>
>Säkerhetskopian av rotkatalogen för innehållslagring måste återställas till platsen för den katalogen som den angavs under konfigurationen för innehållstjänster.

Om en enskild nod i ett Multinode-kluster inte fungerar och de återstående noderna i klustret fungerar som de ska, utför du klusteråterställningen med en nod.

## Återställa AEM formulärdata {#recover-the-aem-forms-data}

1. Stoppa AEM formulärtjänster och programservern om programmet körs.
1. Om det behövs kan du återskapa det fysiska systemet från en systemavbildning. Det här steget är kanske inte nödvändigt om orsaken till återställningen är en felaktig databasserver.
1. Använd patchar eller uppdateringar på AEM formulär som använts sedan bilden skapades. Denna information registrerades under säkerhetskopieringen. AEM formulär måste korrigeras på samma nivå som när systemet säkerhetskopierades.
1. (WebSphere Application Server) Om du återställer till en ny instans av WebSphere Application Server kör du kommandot restoreConfig.bat/sh.
1. Återställ AEM formulärdatabas genom att först köra en databasåterställningsåtgärd med hjälp av databasens säkerhetskopieringsfiler och sedan använda transaktionsupprepningsloggarna på den återställda databasen. (Se [AEM](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) Mer information finns i en av följande artiklar i kunskapsbasen:

   * [Säkerhetskopiering och återställning av oracle för AEM](https://www.adobe.com/go/kb403624)
   * [MySQL Backup and Recovery for AEM forms](https://www.adobe.com/go/kb403625)
   * [Microsoft SQL Server Backup and Recovery for AEM forms](https://www.adobe.com/go/kb403623)
   * [DB2 Säkerhetskopiering och återställning av AEM formulär](https://www.adobe.com/go/kb403626)

1. Återställ GDS-katalogen genom att först ta bort innehållet i GDS-katalogen i den befintliga installationen av AEM formulär och sedan kopiera innehållet i GDS-katalogen från den säkerhetskopierade GDS-katalogen. Om du har ändrat GDS-katalogplatsen finns mer information i [Ändra GDS-platsen under återställning](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).
1. Byt namn på GDS-säkerhetskopieringskatalogen som ska återställas enligt följande exempel:

   >[!NOTE]
   >
   >Om katalogen /restore redan finns säkerhetskopierar du den och tar sedan bort den innan du byter namn på katalogen /backup som innehåller de senaste data.

   * (JBoss) Byt namn `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` till:

      `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`.

   * (WebLogic) Byt namn `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` till:

      `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`.

   * (WebSphere) Byt namn `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` till:

      `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`.

1. Återställ rotkatalogen för innehållslagring genom att först ta bort innehållet i rotkatalogen för innehållslagring i den befintliga installationen av AEM formulär och sedan återställa innehållet genom att utföra följande åtgärder för antingen fristående eller grupperade miljöer:

   >[!NOTE]
   >
   >Säkerhetskopian av rotkatalogen för innehållslagring måste återställas till platsen för rotkatalogen för innehållslagring så som den angavs under konfigurationen för innehållstjänster (borttagen).

   **Fristående:** Återställ alla kataloger som säkerhetskopierades under återställningsprocessen. När katalogerna återställs och katalogen /backup-lucene-indexes finns byter du namn på den till /lucene-indexes. I annat fall ska katalogen lucene-indexes redan finnas och ingen åtgärd krävs.

   **Grupperad:** Återställ alla kataloger som säkerhetskopierades under återställningsprocessen. Så här återställer du indexrotkatalogen:

   * Ta bort allt innehåll i indexrotkatalogen.
   * Om katalogen /backup-lucene-indexes finns kopierar du innehållet i *Rotkatalog för innehållslagring*/backup-lucene-indexes directory to the Index Root directory and delete the *Rotkatalog för innehållslagring*/backup-lucene-indexes katalog.
   * Om katalogen /lucene-indexes finns kopierar du innehållet i *Rotkatalog för innehållslagring*/lucene-indexes katalog till katalogen Index Root.

1. Återställ CRX-databasen.

   * **Fristående**

      *Återställa författare och publicera instanser*: Om ett haveri inträffar kan du återställa databasen till det senast säkerhetskopierade tillståndet genom att utföra de steg som beskrivs i [Säkerhetskopiera och återställ.](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)

      När författarnoden återställs kontrolleras även återställningen av Forms Manager- och AEM Forms Workspace-data.

   * **Grupperad**

      För återställning i en klustermiljö, se [Strategi för säkerhetskopiering och återställning i en klustrad miljö](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment).

1. Ta bort eventuella AEM temporära filer som har skapats i katalogen java.io.temp eller i Adobe temp-katalogen.
1. Starta AEM formulär (se [Starta och stoppa tjänster](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->.

## Ändra GDS-platsen under återställning {#changing-the-gds-location-during-recovery}

Om ditt GDS återställs till en annan plats än den ursprungliga kör du LCSetGDS-skriptet och anger GDS till den nya platsen. Skriptet finns i `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline` mapp. Skriptet har två parametrar, `defaultGDS` och `newGDS`. Se `ReadMe.txt` i samma mapp för instruktioner om hur skriptet ska köras.

>[!NOTE]
>
>Om du har aktiverat dokumentlagring i databasen behöver du inte ändra GDS-platsen.

>[!NOTE]
>
>Den här begränsningen är den enda under vilken du bör använda det här skriptet för att ändra GDS-platsen. Använd administrationskonsolen om du vill ändra GDS-platsen medan AEM är igång. (Se [Konfigurera allmänna inställningar AEM formulär](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).)

>[!NOTE]
>
>Komponentdistributionen misslyckas i Windows om GDS-katalogen finns i enhetsroten (till exempel D:\). För GDS måste du se till att katalogen inte finns i enhetens rot utan i en underkatalog. Katalogen ska till exempel vara D:\GDS and not simply D:\.

## Återställa GDS till en klustrad miljö {#recovering-the-gds-to-a-clustered-environment}

Om du vill ändra GDS-platsen i en klustrad miljö stänger du av hela klustret och kör LCSetGDS-skriptet på en enskild nod i klustret. (Se [Ändra GDS-platsen under återställning](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).) Starta bara den noden. När den noden har startats kan andra noder i klustret startas på ett säkert sätt och pekar korrekt på den nya GDS-servern.

>[!NOTE]
>
>Om du inte kan säkerställa att en nod startas fullständigt innan du startar andra noder måste du köra LCSetGDS-skriptet på alla noder i klustret innan du startar klustret.
