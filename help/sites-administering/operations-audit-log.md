---
title: Granskningslogghantering i AEM 6
seo-title: Granskningslogghantering i AEM 6
description: Lär dig mer om underhåll av granskningslogg i AEM.
seo-description: Lär dig mer om underhåll av granskningslogg i AEM.
uuid: 212de4df-6bf4-434c-94e1-74186d21945a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 565d89de-b3ca-41a5-8e1c-d10905c25fb5
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---


# Granskningslogghantering i AEM 6{#audit-log-maintenance-in-aem}

AEM som är kvalificerade för granskningsloggning genererar mycket arkiverade data. Dessa data kan snabbt växa med tiden på grund av replikeringar, överföringar av resurser och andra systemaktiviteter.

Underhållet i granskningsloggen innehåller flera delar av funktionaliteten som gör det möjligt att automatisera underhåll av granskningsloggar enligt specifika policyer.

Den implementeras som en konfigurerbar underhållsåtgärd varje vecka och är tillgänglig via kontrollkonsolen för Operations Dashboard.

Mer information finns i [dokumentationen för kontrollpanelen för åtgärder](/help/sites-administering/operations-dashboard.md).

Det finns tre typer av rensningsalternativ för granskningslogg:

1. [Rensning av sidgranskningslogg](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [Rensa granskningslogg för DAM](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [Rensning av replikeringsgranskningslogg](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

Du kan konfigurera var och en genom att skapa regler i AEM webbkonsol. När de har konfigurerats kan du utlösa dem genom att gå till **Verktyg - Åtgärder - Underhåll - Underhållsfönster varje vecka** och köra **underhållsaktiviteten för granskningsloggen**.

## Konfigurera rensning av sidgranskningslogg {#configure-page-audit-log-purging}

Så här konfigurerar du rensning av granskningslogg:

1. Gå till Web Console Admin genom att peka webbläsaren till `http://localhost:4502/system/console/configMgr/`

1. Sök efter ett objekt med namnet **Rensningsregel för sidgranskningslogg** och klicka på det.

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. Konfigurera sedan schemaläggaren för rensning enligt dina krav. De tillgängliga alternativen är:

   * **Regelnamn:** namnet på granskningspolicyregeln;
   * **Innehållssökväg:sökvägen** till innehållet som regeln gäller för;
   * **Minsta ålder:** den tid i dagar som revisionsloggarna måste sparas.
   * **Granskningsloggtyp:** den typ av granskningslogg som ska rensas.

   >[!NOTE]
   >
   >Innehållssökvägen gäller endast för underordnade noder till `/var/audit/com.day.cq.wcm.core.page`-noden i databasen.

1. Spara regeln.
1. Regeln som du nyss skapade måste visas på kontrollpanelen för åtgärder för att den ska kunna köras. Om du vill göra det går du **Verktyg - Åtgärder - Underhåll** från AEM välkomstskärm.

1. Tryck på kortet **Veckounderhåll Fönster**.

1. Underhållsuppgiften finns redan under kortet **AuditLog Maintenance Task**.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. Du kan antingen kontrollera datumet för nästa körning, konfigurera det eller köra det manuellt genom att trycka på uppspelningsknappen.

I AEM 6.3 stoppas aktiviteten automatiskt om det schemalagda underhållsfönstret stängs innan rensningsaktiviteten för granskningslogg kan slutföras. Den återupptas när nästa underhållsfönster öppnas.

**Med AEM 6.5** kan du stoppa en rensningsaktivitet för granskningslogg manuellt genom att klicka på  **** stoppikonen. Nästa körning innebär att uppgiften återupptas.

>[!NOTE]
>
>Att stoppa underhållsaktiviteten innebär att avbryta körningen utan att förlora spårning av det pågående jobbet.

## Konfigurera rensning av DAM-granskningslogg {#configure-dam-audit-log-purging}

1. Gå till systemkonsolen på *https://&lt;serveradress>:&lt;serverport>/system/console/configMgr*
1. Sök efter regeln **Rensa DAM-granskningslogg** och klicka på resultatet.
1. Konfigurera regeln i nästa fönster. Alternativen är:

   * **Regelnamn:** namnet på granskningspolicyregeln;
   * **Innehållssökväg:sökvägen** till innehållet som regeln gäller för
   * **Minsta ålder:** den tid i dagar som revisionsloggarna måste sparas
   * **Granska loggfönsterhändelsetyper:** de typer av DAM-granskningshändelser som ska rensas.

1. Klicka på **Spara** för att spara konfigurationen

## Konfigurera rensning av replikeringsgranskningslogg {#configure-replication-audit-log-purging}

1. Gå till systemkonsolen på *https://&lt;serveradress>:&lt;serverport>/system/console/configMgr*
1. Sök efter **Rensa schemaläggare för replikeringsgranskningslogg** och klicka på resultatet
1. Konfigurera regeln i nästa fönster. Alternativen är:

   * **Regelnamn:** namnet på granskningspolicyregeln
   * **Innehållssökväg:sökvägen** till innehållet som regeln gäller för
   * **Minsta ålder:** den tid i dagar som revisionsloggarna måste sparas
   * **händelsetyper** för replikeringsloggens replikering:typer av replikeringsgranskningshändelser som ska rensas

1. Klicka på **Spara** för att spara konfigurationen.

