---
title: Skapa en startguide för en resursmapp utan rubrik
description: Använd AEM Content Fragment Models för att definiera strukturen för Content Fragments, som är grunden för ditt headless-innehåll.
exl-id: 8d913056-fcfa-4cdd-b40a-771f13dfd0f4
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Architect,Data Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Skapa en startguide för en resursmapp utan rubrik {#creating-an-assets-folder}

Använd AEM Content Fragment Models för att definiera strukturen för Content Fragments, som är grunden för ditt headless-innehåll. Innehållsfragment lagras sedan i resursmappar.

## Vad är en resursmapp? {#what-is-an-assets-folder}

[Nu när du har skapat modeller för innehållsfragment](create-content-model.md) som definierar den struktur du vill ha för framtida innehållsfragment, är du antagligen glad att kunna skapa några fragment.

Du måste dock först skapa en resursmapp där du lagrar dem.

Resursmappar används för [ordna traditionellt innehåll](/help/assets/manage-assets.md) som bilder, video och innehållsfragment.

## Skapa en resursmapp {#how-to-create-an-assets-folder}

En administratör behöver bara skapa mappar då och då för att ordna innehållet när det skapas. I den här guiden behöver vi bara skapa en mapp.

1. Logga in AEM och välj **Navigation > Assets > Files**.
1. Klicka **Skapa > Mapp**.
1. Ange en **Titel** och **Namn** för din mapp.
   * The **Titel** ska vara beskrivande.
   * The **Namn** blir nodnamnet i databasen.
      * Det genereras automatiskt baserat på titeln och justeras enligt [AEM namnkonventioner.](/help/sites-developing/naming-conventions.md)
      * Den kan vid behov justeras.

   ![Skapa mapp](assets/assets-folder-create.png)
1. Markera mappen som du skapade och välj sedan **Egenskaper** i verktygsfältet (eller använd `p` [kortkommando.](/help/sites-authoring/keyboard-shortcuts.md))
1. I **Egenskaper** väljer du **Cloud Service** -fliken.
1. För **Molnkonfiguration** Välj [konfiguration som du skapade tidigare.](create-configuration.md)
   ![Konfigurera resursmapp](assets/assets-folder-configure.png)
1. Klicka **Spara och stäng**.
1. Klicka **OK** i bekräftelsefönstret.

   ![Bekräftelsefönstret](assets/assets-folder-confirmation.png)

Du kan skapa ytterligare undermappar i den mapp du skapade. Undermapparna ärver **Molnkonfiguration** för den överordnade mappen. Detta kan dock åsidosättas om du vill använda modeller från en annan konfiguration.

Om du använder en lokaliserad platsstruktur kan du [skapa en språkrot](/help/assets/multilingual-assets.md) nedanför den nya mappen.

## Nästa steg {#next-steps}

Nu när du har skapat en mapp för dina innehållsfragment kan du gå vidare till den fjärde delen av guiden Komma igång och [skapa innehållsfragment.](create-content-fragment.md)

>[!TIP]
>
>Fullständig information om hur du hanterar innehållsfragment finns i [Dokumentation för innehållsfragment](/help/assets/content-fragments/content-fragments.md)
