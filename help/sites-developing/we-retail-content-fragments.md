---
title: Testa innehållsfragment i webb.detaljhandel
seo-title: Testa innehållsfragment i webb.detaljhandel
description: Testa innehållsfragment i webb.detaljhandel
seo-description: 'null'
uuid: 66daddfe-8e98-47b6-8499-db055887ac17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d1326737-f378-46d0-9916-61ead4d31639
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 3%

---


# Provar Content Fragments in We.Retail{#trying-out-content-fragments-in-we-retail}

Med innehållsfragment kan du skapa kanalneutralt innehåll tillsammans med (eventuellt kanalspecifika) variationer. **We.Retail**  (som tillgängligt i en körklar instans av AEM) är fragmentet  **Arktis Surfing i** Lofotensom ett grundläggande exempel. Detta visar att:

* Innehållsfragment i Adobe Experience Manager (AEM) [skapas och hanteras som sidoberoende resurser](/help/assets/content-fragments/content-fragments.md). Med dem kan du skapa kanalneutralt innehåll tillsammans med (eventuellt kanalspecifika) variationer.

   * Se [Var finns resurser för innehållsfragment i We.Retail](#where-to-find-content-fragments-in-we-retail)

* Du kan sedan [använda dessa fragment och deras variationer när du redigerar](/help/sites-authoring/content-fragments.md) dina innehållssidor.

   * Se [Var innehållsfragment används i Web.Retail](#where-content-fragments-are-used-in-we-retail)

Den fullständiga dokumentationen om hur du skapar, hanterar, använder och utvecklar innehållsfragment finns i:

* Se [Mer information](#further-information)

>[!NOTE]
>
>**Innehållsfragment** och  **[Upplevelsefragment](/help/sites-authoring/experience-fragments.md)** är olika funktioner i AEM:
>
>* **Innehållsfragmenterarär** redaktionellt innehåll, främst text och relaterade bilder. De är rent innehåll, utan design och layout.
>* **Upplevelsefragment** är helt utformat. ett fragment av en webbsida.

>
>
Upplevelsefragment kan innehålla innehåll i form av innehållsfragment, men inte tvärtom.

## Var ska vi hitta innehållsfragment i Web.Retail {#where-to-find-content-fragments-in-we-retail}

Det finns flera exempelinnehållsfragment i We.Retail; navigera via **Resurser**, **Filer**, **We.Retail**, **Engelska**, **upplevelser**.

Dessa är **Arktisk surfning i Lofoten**, ett fragment tillsammans med relaterade visuella resurser:

* Navigera via **Resurser**, **Filer**, **We.Retail**, **Engelska**, **upplevelser**, **Artic Surfing in Lofoten**:

   * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

Du kan markera och redigera **arktisk surfning i fragmentet Lofoten**:

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

Här kan du [redigera och hantera](/help/assets/content-fragments/content-fragments.md) ditt fragment med hjälp av flikarna (vänsterpanelen):

<!--![](do-not-localize/cf-45-aa.png) ![](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[](/help/assets/content-fragments/content-fragments-variations.md)** Variationer inklusive  [Markering](/help/assets/content-fragments/content-fragments-markdown.md)
* **[Associerat innehåll](/help/assets/content-fragments/content-fragments-assoc-content.md)**
* **[Metadata](/help/assets/content-fragments/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## Där innehållsfragment används i Web.Retail {#where-content-fragments-are-used-in-we-retail}

För att illustrera [sidredigering med ett innehållsfragment](/help/sites-authoring/content-fragments.md) finns det flera exempelsidor under:

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

Till exempel refereras innehållsfragmentet **Arktis surfning i Lofoten** på sidan Platser:

* Navigera via **Sites**, **We.Retail**, **Language Masters**, **English**, **Experience**. Öppna sedan **Arktisk surfning i Lofoten** för redigering:

   * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## Ytterligare information {#further-information}

Mer information finns i:

* [Arbeta med innehållsfragment](/help/assets/content-fragments/content-fragments.md)

   * Lär dig hur du skapar, redigerar och hanterar resurser för innehållsfragment.

* [Sidredigering med innehållsfragment](/help/sites-authoring/content-fragments.md)

   * Använd ditt innehållsfragment när du redigerar en sida.

* [Utveckla AEM - Komponenter för innehållsfragment](/help/sites-developing/components-content-fragments.md)

   * En översikt över komponenterna för innehållsfragment.

* [Utveckla och utöka innehållsfragment](/help/sites-developing/customizing-content-fragments.md)

   * Information som hjälper dig att utveckla och utöka innehållsfragment.

