---
title: Granskningslogghantering i AEM 6
description: Läs mer om underhåll av granskningsloggar i Adobe Experience Manager (AEM).
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 1e05faf5-619a-4ea3-acbf-2fd37c71e6d2
feature: Operations
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---

# Granskningslogghantering i AEM 6{#audit-log-maintenance-in-aem}

AEM som är kvalificerade för granskningsloggning genererar mycket arkiverade data. Dessa data kan snabbt växa med tiden på grund av replikeringar, överföringar av resurser och andra systemaktiviteter.

Underhållet i granskningsloggen innehåller flera delar av funktionaliteten som gör det möjligt att automatisera underhåll av granskningsloggar enligt specifika policyer.

Den implementeras som en konfigurerbar underhållsåtgärd varje vecka och är tillgänglig via kontrollkonsolen för Operations Dashboard.

Mer information finns i [Instrumentpanelsdokumentation för åtgärder](/help/sites-administering/operations-dashboard.md).

Det finns tre typer av rensningsalternativ för granskningslogg:

1. [Rensning av sidgranskningslogg](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [Rensa granskningslogg för DAM](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [Rensning av replikeringsgranskningslogg](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

Du kan konfigurera var och en genom att skapa regler i AEM webbkonsol. När de har konfigurerats kan du utlösa dem genom att gå till **Verktyg - Drift - Underhåll - Underhållsfönster varje vecka** och köra **Underhållsaktivitet för granskningslogg**.

## Konfigurera rensning av sidgranskningslogg {#configure-page-audit-log-purging}

Så här konfigurerar du rensning av granskningslogg:

1. Gå till Web Console Admin och peka webbläsaren till `http://localhost:4502/system/console/configMgr/`

1. Sök efter ett objekt som anropats **Rensa regel för sidgranskningslogg** och klicka på den.

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. Konfigurera sedan schemaläggaren för rensning enligt dina krav. De tillgängliga alternativen är:

   * **Regelnamn:** Namnet på revisionspolicyregeln.
   * **Innehållssökväg:** Sökvägen för det innehåll som regeln gäller.
   * **Minsta ålder:** Den tidpunkt i dagar som revisionsloggarna behöver sparas.
   * **Granskningsloggtyp:** vilken typ av granskningslogg som ska rensas.

   >[!NOTE]
   >
   >Innehållssökvägen gäller endast för underordnade objekt till `/var/audit/com.day.cq.wcm.core.page` i databasen.

1. Spara regeln.
1. Regeln som du skapade måste visas på kontrollpanelen för åtgärder för att den ska kunna köras. För att göra detta, gå **Verktyg - Drift - Underhåll** på AEM välkomstskärm.

1. Tryck på **Underhållsfönster varje vecka** kort.

1. Underhållsuppgiften finns redan i **Underhållsaktivitet för granskningslogg** kort.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. Du kan antingen kontrollera datumet för nästa körning, konfigurera det eller köra det manuellt genom att trycka på uppspelningsknappen.

I AEM 6.3 stoppas aktiviteten automatiskt om det schemalagda underhållsfönstret stängs innan rensningsaktiviteten för granskningslogg kan slutföras. Den återupptas när nästa underhållsfönster öppnas.

**Med AEM 6.5** kan du stoppa en rensningsaktivitet för granskningslogg manuellt genom att klicka på **Stoppa** -ikon. Nästa körning innebär att uppgiften återupptas.

>[!NOTE]
>
>Att stoppa underhållsaktiviteten innebär att avbryta körningen utan att förlora spårning av det pågående jobbet.

## Konfigurera rensning av DAM-granskningslogg {#configure-dam-audit-log-purging}

1. Navigera till systemkonsolen på *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Sök efter **Rensa DAM-granskningslogg** och klicka på resultatet.
1. Konfigurera regeln i nästa fönster. Alternativen är:

   * **Regelnamn:** Namnet på revisionspolicyregeln.
   * **Innehållssökväg:** sökvägen till innehållet som regeln gäller för
   * **Minsta ålder:** den tidpunkt i dagar som revisionsloggarna måste sparas
   * **Händelsetyper för granskningslogg:** de typer av DAM-granskningshändelser som ska rensas.

1. Klicka **Spara** för att spara konfigurationen

## Konfigurera rensning av replikeringsgranskningslogg  {#configure-replication-audit-log-purging}

1. Navigera till systemkonsolen på *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Sök efter **Rensa schemaläggare för replikeringsgranskningslogg** och klicka på resultatet
1. Konfigurera regeln i nästa fönster. Alternativen är:

   * **Regelnamn:** namnet på granskningspolicyregeln
   * **Innehållssökväg:** sökvägen till innehållet som regeln gäller för
   * **Minsta ålder:** den tidpunkt i dagar som revisionsloggarna måste sparas
   * **Händelsetyper för granskningsloggens replikering:** de typer av replikeringsgranskningshändelser som ska rensas

1. Klicka **Spara** för att spara konfigurationen.
