---
title: Skapa en startguide för en resursmapp utan rubrik
description: Använd AEM Content Fragment Models för att definiera strukturen för Content Fragments, som är grunden för ditt headless-innehåll.
exl-id: 9a156a17-8403-40fc-9bd0-dd82fb7b2235
source-git-commit: 40922b222e15aa3ef12b54d65addff32b679d36e
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# Skapa en startguide för en resursmapp utan rubrik {#creating-an-assets-folder}

Använd AEM Content Fragment Models för att definiera strukturen för Content Fragments, som är grunden för ditt headless-innehåll. Innehållsfragment lagras sedan i resursmappar.

## Vad är en resursmapp? {#what-is-an-assets-folder}

[Nu när du har skapat modeller för innehållsfragment](create-content-model.md) som definierar den struktur du vill ha för framtida innehållsfragment, är du antagligen glad att kunna skapa några fragment.

Du måste dock först skapa en resursmapp där du lagrar dem.

Resursmappar används för [ordna traditionellt innehåll](/help/assets/manage-assets.md) som bilder, video och innehållsfragment.

## Så här skapar du en resursmapp {#how-to-create-an-assets-folder}

En administratör behöver bara skapa mappar då och då för att ordna innehållet när det skapas. I den här guiden behöver vi bara skapa en mapp.

1. Logga in AEM och välj **Navigering -> Resurser -> Filer**.
1. Tryck eller klicka **Skapa -> Mapp**.
1. Ange en **Titel** och **Namn** för din mapp.
   * The **Titel** ska vara beskrivande.
   * The **Namn** blir nodnamnet i databasen.
      * Det genereras automatiskt baserat på titeln och justeras enligt [AEM namnkonventioner.](/help/sites-developing/naming-conventions.md)
      * Den kan vid behov justeras.

   ![Skapa mapp](../assets/assets-folder-create.png)
1. Markera mappen som du just skapade och välj sedan **Egenskaper** i verktygsfältet (eller använd `p` [kortkommando.](/help/sites-authoring/keyboard-shortcuts.md))
1. I **Egenskaper** väljer du **Cloud Services** -fliken.
1. För **Molnkonfiguration** Välj [som du skapade tidigare.](create-configuration.md)

   ![Konfigurera resursmapp](../assets/assets-folder-configure.png)
1. Tryck eller klicka **Spara och stäng**.
1. Tryck eller klicka **OK** i bekräftelsefönstret.

   ![Bekräftelsefönstret](../assets/assets-folder-confirmation.png)

Du kan skapa ytterligare undermappar i den mapp du just skapade. Undermapparna ärver **Molnkonfiguration** för den överordnade mappen. Detta kan dock åsidosättas om du vill använda modeller från en annan konfiguration.

Om du använder en lokaliserad platsstruktur kan du [skapa en språkrot](/help/assets/multilingual-assets.md) nedanför den nya mappen.

## Nästa steg {#next-steps}

Nu när du har skapat en mapp för dina innehållsfragment kan du gå vidare till den fjärde delen av guiden Komma igång och [skapa innehållsfragment.](create-content-fragment.md)

>[!TIP]
>
>Fullständig information om hur du hanterar innehållsfragment finns i [Dokumentation för innehållsfragment](/help/assets/content-fragments/content-fragments.md)
