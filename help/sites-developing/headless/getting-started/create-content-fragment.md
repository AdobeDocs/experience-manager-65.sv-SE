---
title: Skapa innehållsfragment Headless Quick Start Guide
description: Lär dig använda AEM innehållsfragment för att utforma, skapa, strukturera och använda sidoberoende innehåll för rubrikfri leverans.
exl-id: 5787204d-bcce-447e-b98c-2bc1c0d744c3
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Architect,Data Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# Skapa innehållsfragment Headless Quick Start Guide {#creating-content-fragments}

Lär dig använda AEM innehållsfragment för att utforma, skapa, strukturera och använda sidoberoende innehåll för rubrikfri leverans.

## Vad är innehållsfragment? {#what-are-content-fragments}

[Nu när du har skapat en resursmapp](create-assets-folder.md) där du kan lagra dina innehållsfragment kan du nu skapa fragmenten!

Med Content Fragments kan du utforma, skapa, strukturera och publicera sidoberoende innehåll. De gör att du kan förbereda innehåll för användning på flera platser och i flera kanaler.

Innehållsfragment innehåller strukturerat innehåll och kan levereras i JSON-format.

## Så här skapar du ett innehållsfragment {#how-to-create-a-content-fragment}

Innehållsförfattare skapar valfritt antal innehållsfragment som representerar det innehåll de skapar. Detta kommer att vara deras huvuduppgift i AEM. I den här guiden behöver vi bara skapa en.

1. Logga in AEM och välj **Navigering > Resurser**.
1. Navigera till [mapp som du skapade tidigare.](create-assets-folder.md)
1. Klicka **Skapa > Innehållsfragment**.
1. Skapandet av ett innehållsfragment presenteras som en guide i två steg. Välj först vilken modell som du vill använda för att skapa ditt innehållsfragment och klicka sedan på **Nästa**.
   * Vilka modeller som är tillgängliga beror på [**Molnkonfiguration** du har definierat för resursmappen](create-assets-folder.md) där du skapar innehållsfragmentet.
   * Om du får meddelandet `We could not find any models`kontrollerar du konfigurationen för din resursmapp.

   ![Välj innehållsfragmentmodell](assets/content-fragment-model-select.png)
1. Ange en **Titel**, **Beskrivning** och **Taggar** vid behov och klicka **Skapa**.

   ![Skapa innehållsfragment](assets/content-fragment-create.png)
1. Klicka **Öppna** i bekräftelsefönstret.

   ![Bekräftelse på att innehållsfragment har skapats](assets/content-fragment-confirmation.png)
1. Ange information om innehållsfragmentet i Content Fragment Editor.

   ![Innehållsfragmentsredigerare](assets/content-fragment-edit.png)
1. Klicka **Spara** eller  **Spara och stäng**.

Innehållsfragment kan referera till andra innehållsfragment, vilket möjliggör en kapslad innehållsstruktur om det behövs.

Innehållsfragment kan också referera till andra resurser i AEM. [Dessa resurser måste lagras i AEM](/help/assets/manage-assets.md) innan du skapar ett referensinnehållsfragment.

## Nästa steg {#next-steps}

Nu när du har skapat ett innehållsfragment kan du gå vidare till den sista delen av guiden Komma igång och [skapa API-förfrågningar för åtkomst och leverans av innehållsfragment.](create-api-request.md)

>[!TIP]
>
>Fullständig information om hur du hanterar innehållsfragment finns i [Dokumentation för innehållsfragment](/help/assets/content-fragments/content-fragments.md)
