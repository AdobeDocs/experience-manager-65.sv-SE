---
title: Content Fragments - Configuration Browser
description: Lär dig hur du aktiverar vissa Content Fragment-funktioner i Configuration Browser så att du kan använda Adobe Experience Manager kraftfulla headless-leveransfunktioner.
feature: Content Fragments
role: User
exl-id: a9990b0c-56c7-4e61-bae9-98e19a7f364e
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 12%

---

# Content Fragments - Configuration Browser{#content-fragments-configuration-browser}

Lär dig hur du aktiverar vissa Content Fragment-funktioner i Configuration Browser så att du kan använda Adobe Experience Manager (AEM) kraftfulla headless-leveransfunktioner.

## Aktivera funktionen för innehållsfragment för instansen {#enable-content-fragment-functionality-instance}

Innan du använder innehållsfragment använder du **Konfigurationsläsaren** för att aktivera följande:

* **Modeller för innehållsfragment** - obligatoriskt
* **GraphQL Beständiga frågor** - valfritt

>[!CAUTION]
>
>Om du inte aktiverar **Modeller för innehållsfragment**:
>
>* den **Skapa** kan inte användas för att skapa modeller.
>* du inte kan [välj platskonfigurationen för att skapa den relaterade slutpunkten](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint).

Om du vill aktivera funktionen för innehållsfragment måste du göra följande:

* Aktivera användning av innehållsfragmentsfunktioner via konfigurationsläsaren
* Använda konfigurationen i resursmappen

### Aktivera funktionen för innehållsfragment i konfigurationsläsaren {#enable-content-fragment-functionality-in-configuration-browser}

Till [använda vissa funktioner för innehållsfragment](#creating-a-content-fragment-model), du **måste** först aktivera dem via **Konfigurationsläsaren**:

>[!NOTE]
>
>Mer information finns i [Konfigurationsläsaren:](/help/sites-administering/configurations.md#using-configuration-browser).

1. Navigera till **Verktyg**, **Allmänt** och öppna sedan **Konfigurationsläsaren**.

1. Använd **Skapa** för att öppna dialogrutan där du:

   1. Ange en **Titel**.
   1. Om du vill aktivera deras användning väljer du
      * **Modeller för innehållsfragment**
      * **GraphQL Beständiga frågor**

      ![Definiera konfiguration](assets/cfm-conf-01.png)

1. Välj **Skapa** för att spara definitionen.

<!-- 1. Select the location appropriate to your website. -->

### Använd konfigurationen i resursmappen {#apply-the-configuration-to-your-assets-folder}

När konfigurationen **global** är aktiverat för innehållets fragmentfunktion och gäller sedan för alla resursmappar.

Om du vill använda andra konfigurationer (d.v.s. exkludera globala) med en jämförbar resursmapp måste du definiera anslutningen. Detta gör du genom att välja lämplig **konfiguration** på fliken **Cloud Services** i **Mappegenskaper** för rätt mapp.

![Använd konfiguration](assets/cfm-conf-02.png)
