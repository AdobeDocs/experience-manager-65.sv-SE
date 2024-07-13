---
title: Uppgradera till Adobe Experience Manager 6.5
description: Lär dig mer om grunderna för uppgradering av en äldre Adobe Experience Manager-installation (AEM) till AEM 6.5.
contentOwner: sarchiz
topic-tags: upgrading
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: 722d544c-c342-4c1c-80e5-d0a1244f4d36
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---

# Uppgradera till Adobe Experience Manager (AEM) 6.5 {#upgrading-to-aem}

Detta avsnitt behandlar uppgradering av en AEM till AEM 6.5:

* [Planera din uppgradering](/help/sites-deploying/upgrade-planning.md)
* [Utvärdera Upgrade Complexity med Pattern Detector](/help/sites-deploying/pattern-detector.md)
* [Bakåtkompatibilitet i AEM 6.5](/help/sites-deploying/backward-compatibility.md)
  <!--* [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->
* [Uppgraderingsförfarande](/help/sites-deploying/upgrade-procedure.md)
* [Uppgradera kod och anpassningar](/help/sites-deploying/upgrading-code-and-customizations.md)
* [Underhållsaktiviteter före uppgraderingen](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [Utföra en uppgradering på plats](/help/sites-deploying/in-place-upgrade.md)
* [Post Upgrade Checks and Troubleshooting](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [Hållbara uppgraderingar](/help/sites-deploying/sustainable-upgrades.md)
* [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md)
* [Omstrukturering av lager i AEM 6.5](/help/sites-deploying/repository-restructuring.md)

För att underlätta referensen till de AEM förekomsterna i dessa procedurer används följande termer i alla dessa artiklar:

* *source*-instansen är den AEM instansen som du uppgraderar från.
* *target*-instansen är den som du uppgraderar till.

>[!NOTE]
>
>Som en del av arbetet med att förbättra uppgraderingarnas tillförlitlighet har AEM genomgått en omfattande omstrukturering av databasen. Mer information om hur du anpassar dig till den nya strukturen finns i [Databasomstrukturering i AEM.](/help/sites-deploying/repository-restructuring.md)

## Vad har ändrats? {#what-has-changed}

Nedan följer viktiga ändringar av anmärkningar under de senaste versionerna av AEM:

AEM 6.0 introducerade den nya Jackrabbit Oak-databasen. Persistence Managers ersattes av [Micro Kernels](/help/sites-deploying/platform.md#contentbody_title_4). Från och med version 6.1 stöds inte längre CRX2. Ett migreringsverktyg som kallas crx2oak måste köras för att migrera CRX2-databaser från 5.6.1-instanser. Mer information finns i [Använda migreringsverktyget för CRX2OAK](/help/sites-deploying/using-crx2oak.md).

Om Assets Insights används och du uppgraderar från en version som är äldre än AEM 6.2, måste resurserna migreras och ha ID:n som genereras via en JMX-böna. För Adobe interna tester migrerades 125 K-resurser på en TjärMK-miljö på en timme, men resultatet kan variera.

6.3 introducerade ett nytt format för `SegmentNodeStore`, som är grunden för TjäraMK-implementeringen. Om du uppgraderar från en version som är äldre än AEM 6.3, kräver detta en databasmigrering som en del av uppgraderingen, inklusive driftstopp.

Adobe Engineering beräknar att det är ca 20 minuter. Omindexering behövs inte. Dessutom har en ny version av crx2oak-verktyget släppts för att fungera med det nya databasformatet.

**Migreringen krävs inte om du uppgraderar från AEM 6.3 till AEM 6.5.**

Underhållsuppgifterna före uppgraderingen har optimerats för automatisering.

Kommandoradsalternativen för crx2oak-verktyget har ändrats till att vara automatiseringsvänliga och stöder fler uppgraderingsalternativ.

Kontrollerna efter uppgraderingen har också gjorts automatiseringsvänliga.

Periodisk skräpinsamling med revideringar och skräpinsamling i datalager är nu rutinuppgifter som måste utföras regelbundet. I och med introduktionen av AEM 6.3 stöder och rekommenderar Adobe Online Revision Cleanup. Mer information om hur du konfigurerar de här aktiviteterna finns i [Revision Cleanup](/help/sites-deploying/revision-cleanup.md).

AEM introducerar nyligen [Mönsteravkännaren](/help/sites-deploying/pattern-detector.md) för att bedöma uppgraderingens komplexitet när du börjar planera för uppgraderingen. 6.5 har också ett starkt fokus på [bakåtkompatibilitet](/help/sites-deploying/backward-compatibility.md) för funktioner. Slutligen läggs även bästa praxis för [hållbara uppgraderingar](/help/sites-deploying/sustainable-upgrades.md) till.

Mer information om vad mer som har ändrats i de senaste AEM versionerna finns i den fullständiga versionsinformationen:

* [Versionsinformation om Adobe Experience Manager 6.5 Senaste Service Pack](/help/release-notes/release-notes.md)

## Uppgradera - översikt {#upgrade-overview}

Uppgradering av AEM är en flerstegsprocess som ibland tar flera månader. Följande översikt har bifogats som en översikt över vad som ingår i ett uppgraderingsprojekt och det innehåll som ingår i den här dokumentationen:

![screen_shot_2018-03-30at80708am](assets/screen_shot_2018-03-30at80708am.png)

## Uppgraderingsflöde {#upgrade-overview-1}

Bilden nedan visar det rekommenderade arbetsflödet för uppgradering. Notera referensen till de nya funktioner som Adobe har infört. Uppgraderingen ska börja med mönsteravkännaren (se [Utvärderar uppgraderingskomplexiteten med mönsteravkännaren](/help/sites-deploying/pattern-detector.md)), som du kan använda för att bestämma vilken sökväg du vill använda för kompatibilitet med AEM 6.4 baserat på mönstren i den genererade rapporten.

I 6.5 fokuserades allt för att bakåtkompatibiliteten skulle bli bättre, men i de fall där vissa bakåtkompatibilitetsproblem kvarstår kan du i kompatibilitetsläget tillfälligt skjuta upp utvecklingen så att den anpassade koden är kompatibel med 6.5. Med den här metoden undviker du utvecklingsarbete direkt efter uppgraderingen (se [Bakåtkompatibilitet i AEM 6.5](/help/sites-deploying/backward-compatibility.md)).

I din 6.5-utvecklingscykel kan funktioner som introducerats under Hållbara uppgraderingar (se [Hållbara uppgraderingar](/help/sites-deploying/sustainable-upgrades.md)) hjälpa dig att följa bästa praxis för att göra framtida uppgraderingar ännu effektivare och smidigare.

![6_4_upgrade_overview_flowchart-newpage3](assets/6_4_upgrade_overviewflowchart-newpage3.png)
