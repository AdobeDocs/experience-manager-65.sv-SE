---
title: Skapa en guide till Headless-konfiguration
description: Skapa en konfiguration som ett första steg till att komma igång med headless i AEM 6.5.
exl-id: 48801599-f279-4e55-8033-9c418d2af5bb
source-git-commit: 8ab774b8d21dd16e4873cd39ef0175ead3f2da23
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 1%

---

# Skapa en guide till Headless-konfiguration {#creating-configuration}

Som ett första steg till att komma igång med headless i AEM 6.5 måste du skapa en konfiguration.

## Vad är en konfiguration? {#what-is-a-configuration}

I Configuration Browser finns ett allmänt konfigurations-API, innehållsstruktur och lösningsmekanism för konfigurationer i AEM.

När det gäller headless content management i AEM kan du tänka på en konfiguration som en arbetsplats i AEM där du kan skapa dina innehållsmodeller, som definierar strukturen för ditt framtida innehåll och innehållsfragment. Du kan ha flera konfigurationer för att separera dessa modeller.

>[!NOTE]
>
>Om du känner till [sidmallar i en AEM-implementering,](/help/sites-authoring/templates.md) Användningen av konfigurationer för hantering av innehållsmodeller är likartad.

## Så här skapar du en konfiguration {#how-to-create-a-configuration}

En administratör behöver bara skapa en konfiguration en gång, eller mycket sällan, när det krävs en ny arbetsyta för att kunna ordna dina innehållsmodeller. I den här guiden behöver vi bara skapa en konfiguration.

1. Logga in AEM och välj **Verktyg -> Allmänt -> Konfigurationsläsaren**.
1. Ange en **Titel** för din konfiguration.
   * Ett namn genereras automatiskt baserat på titeln och justeras enligt [AEM namnkonventioner.](/help/sites-developing/naming-conventions.md). Det blir nodnamnet i databasen.
1. Markera följande alternativ:
   * **Modeller för innehållsfragment**
   * **Beständiga GraphQL-frågor**

   ![Skapa konfiguration](../assets/create-configuration.png)

1. Tryck eller klicka **Skapa**

Du kan skapa flera konfigurationer om det behövs. Konfigurationer kan också kapslas.

>[!NOTE]
>
>Konfigurationsalternativ utöver **Modeller för innehållsfragment** och **Beständiga GraphQL-frågor** kan vara nödvändigt beroende på implementeringskraven.

## Nästa steg {#next-steps}

Med den här konfigurationen kan du nu gå vidare till den andra delen av guiden Komma igång och [skapa modeller för innehållsfragment.](create-content-model.md)

<!--
>[!TIP]
>
>For complete details about the Configuration Browser, [see the Configuration Browser documentation.](/help/sites-developing/configurations.md)
-->
