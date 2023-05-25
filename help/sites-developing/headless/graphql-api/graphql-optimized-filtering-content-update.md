---
title: Uppdatera dina innehållsfragment för optimerad GraphQL-filtrering
description: Lär dig hur du uppdaterar innehållsfragment för optimerad GraphQL-filtrering i Adobe Experience Manager för leverans av headless-innehåll.
source-git-commit: 1481d613783089046b44d4652d38f7b4b16acc4d
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# Uppdatera dina innehållsfragment för optimerad GraphQL-filtrering {#updating-content-fragments-for-optimized-graphql-filtering}

Om du vill optimera prestanda för dina GraphQL-filter kör du en procedur för att uppdatera dina innehållsfragment.

>[!NOTE]
>
>När du har uppdaterat dina innehållsfragment kan du följa rekommendationerna för [Optimera GraphQL-frågor](/help/sites-developing/headless/graphql-api/graphql-optimization.md).

## Förutsättningar {#prerequisites}

Kontrollera att du har minst 6.5.17.0-versionen av AEM.

## Uppdatera dina innehållsfragment {#updating-content-fragments}

Så här kör du proceduren:

1. [Konfigurera OSGi-inställningarna](/help/sites-deploying/configuring-osgi.md) för **Konfiguration av migreringsjobb för innehållsfragment**:

   ![Jobbkonfiguration för migreringsjobb för OSGi-innehållsfragment](assets/cfm-graphql-update-01.png "Jobbkonfiguration för migreringsjobb för OSGi-innehållsfragment")

1. I dialogrutan ställer du in följande två parametrar:

   * **ContentFragmentMigration:Enabled** : `1`
   * **ContentFragmentMigration:Enforce** : `1`

1. **Spara** specifikationer - uppdateringsproceduren startar.

1. Vänta tills proceduren har slutförts. Proceduren är slutförd när egenskapen `cfGlobalVersion` visas på `/content/dam` och är inställd på `1`.

1. Återgå till OSGi-konfigurationen för att inaktivera proceduren.

   I dialogrutan för **Konfiguration av migreringsjobb för innehållsfragment** Ställ in dessa två parametrar enligt följande:

   * **ContentFragmentMigration:Enabled** : `0`
   * **ContentFragmentMigration:Enforce** : `0`

## Begränsningar {#limitations}

Tänk på följande begränsningar:

* Optimering av prestanda för GraphQL-filter är endast möjligt efter en fullständig uppdatering av alla dina innehållsfragment (vilket indikeras av närvaron av `cfGlobalVersion` egenskap för JCR-noden `/content/dam`)

* Om innehållsfragment importeras från ett innehållspaket (med `crx/de`) när uppdateringsproceduren har körts kommer dessa innehållsfragment inte att beaktas i GraphQL-frågeresultat förrän uppdateringsproceduren körs igen.