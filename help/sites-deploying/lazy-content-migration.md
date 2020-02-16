---
title: Lazy Content Migration
seo-title: Lazy Content Migration
description: Lär dig mer om Lazy Content Migration i AEM 6.4.
seo-description: Lär dig mer om Lazy Content Migration i AEM 6.4.
uuid: f5b0aa84-5638-4708-9da2-89964d394632
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: d72b8844-d782-4b5b-8999-338217dbefb9
docset: aem65
translation-type: tm+mt
source-git-commit: 7d93df515bf98f0a947428b8093e059d63b21a34

---


# Lazy Content Migration {#lazy-content-migration}

För bakåtkompatibilitet kommer innehåll och konfiguration i **/etc** och **/eller innehåll** som börjar med AEM 6.3 inte att ändras eller omformas direkt med uppgraderingen. Detta görs för att säkerställa att kundapplikationernas beroenden av dessa strukturer förblir intakta. Funktionerna för dessa innehållsstrukturer är fortfarande desamma även om innehållet i en av adresserna till AEM 6.5 ligger på en annan plats.

Även om inte alla dessa platser kan omvandlas automatiskt finns det några fördröjningar `CodeUpgradeTasks` som också kallas för Lazy Content Migration. Detta gör att kunderna kan utlösa dessa automatiska omformningar genom att starta om instansen med den här systemegenskapen:

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

Detta gör att `CodeUpgradeTasks` programmet körs under migreringen.

Målet är en effektiv exekvering, men den här uppgraderingsprocessen är synkron och har därför en driftstopp beroende på hur mycket innehåll som behöver bearbetas. Vi rekommenderar att du utvärderar körningstiderna i en scenmiljö framför ett produktionssystem för att planera en underhållsperiod.

Eftersom detta vanligtvis även kräver att du justerar programmet bör aktiviteten utföras tillsammans med motsvarande programdistribution.

Nedan finns en fullständig lista över `CodeUpgradeTasks` som introducerades i 6.5:

| **Namn** | **Relevant** **för AEM-versioner före** | **Migreringstyp** **** | **Information** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | Omedelbar |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | Omedelbar | Identifierar alla `LiveRelationShips` från `VersionStorage` som har tagits bort och lägger till exkluderingsegenskap till överordnad |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | Omedelbar | Omstrukturerar molntjänster för säker som standard |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | Omedelbar | Tar bort egenskapsbaserad länkning från **/innehåll** till **/conf** (ersatt av OSGi-mekanismen), genererar motsvarande OSGi-konfiguration |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | Omedelbar | På grund av hanteringen av merge_preserve åsidosätter regeln för säkert som standard behörigheter som leder till behovet av att beställa om vid uppgradering |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | Omedelbar | Identifierar komponenter med hjälp av HTML5SmartFile-widgeten, söker efter användning av komponenten i innehållet och omstrukturerar beständighet, vilket innebär att binärfilen flyttas en nivå nedåt och inte lagras på komponentnivå. |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | Omedelbar | Flyttar gamla stilprojekt från **/etc/projekt** till **/innehåll/projekt** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | Omedelbar | Lägger till ett behållarlager i hierarkin (områden) och justerar referenser. |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | Omedelbar | Anger namn på fasta platser som målkomponenter. |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | Omedelbar | Komplex omvandling av arbetsflödesmodeller som föregår 6.2-strukturer, instanser, meddelanden, och sedan sammanfogas från säkerhetskopieringsplatsen från **/var/backup** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | Omedelbar | Flyttar resurser, anpassade metadatamatcheman och bearbetningsprofiler från **/appar** till **/conf** och översätter metadatamatchemat och metadataprofiler från coral2 till coral3. |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | Omedelbar | Flyttar resurser och anpassade sökfaktorer från **/appar** till **/conf** och översätter metadatamatchemat och metadataprofiler från coral2 till coral3. |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | Omedelbar | Uppdaterar InboxItems för att ordna inkorgsobjekt (justera metadata för effektiv sortering) |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | Omedelbar | Justerar egenskapen metadataSchema i mappen genom att ersätta relativa sökvägar till **/conf** i stället för **/apps** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | Omedelbar | Justera navigeringsstrukturen |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | Omedelbar | Flyttar anpassade konfigurationer för kontrollpaneler från **/libs** och **/apps** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | Omedelbar | Översätter egenskapen processingProfile (används till och med 6.1) i Assets för att matcha 6.3-strukturen och senare. Justerar också profilens relativa sökvägar till **/conf** i stället för **/apps**. |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | Omedelbar | Uppgradering som tar bort föråldrade menyposter för CRXDE Lite och Web Console vid en uppgradering. |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | Fördröjd | Flytta SRP-molnkonfigurationer, community watchwords-konfigurationer, rensa upp **/etc/social** och **/etc/enablement** (alla referenser och data måste justeras när lat migrering körs - ingen programdel ska längre vara beroende av den här strukturen). |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | Fördröjd | Rensar upp **/etc/molninställningar** (som innehåller ContextHub Configuration). Konfigurationen migreras automatiskt vid första åtkomsten. Om Lazy Content Migration startas tillsammans med en uppgradering måste innehållet i **/etc/cloudsettings** bevaras via paketet innan uppgraderingen och installeras om för att den implicita omvandlingen ska börja, tillsammans med en efterföljande avinstallation av paketet efter slutförandet. |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | Fördröjd | Justerar den äldre rubrikstrukturen till titeln i användarprofilnoden. |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | Fördröjd | Migrera e-handelsinnehåll från **/etc/commerce** till **/var/commerce**. När migreringsinnehållet flyttas och referenser till flyttat innehåll uppdateras för att återspegla den nya platsen. |
| `CQ65DMMigrationTask` | &lt; 6.5 | Fördröjd | Migrera äldre kataloginställningar och inställningar för dynamiska medielmolntjänster från **/etc** till **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6.5 | Fördröjd | Rensa gamla klienter under **/etc/clientlibs** |
