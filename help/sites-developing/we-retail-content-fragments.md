---
title: Testa innehållsfragment i webb.detaljhandel
seo-title: Testa innehållsfragment i webb.detaljhandel
description: 'null'
seo-description: 'null'
uuid: 66daddfe-8e98-47b6-8499-db055887ac17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d1326737-f378-46d0-9916-61ead4d31639
translation-type: tm+mt
source-git-commit: dca52c05c413fc96bf7fab012a3be52f6769c2e0

---


# Testa innehållsfragment i webb.detaljhandel{#trying-out-content-fragments-in-we-retail}

Med innehållsfragment kan du skapa kanalneutralt innehåll tillsammans med (eventuellt kanalspecifika) variationer. **We.Retail** (som tillgängligt i en körklar instans av AEM) innehåller fragmentet **Arktis Surfing i Lofoten** som ett grundläggande exempel. Detta visar att:

* Adobe Experience Manager-innehållsfragment (AEM) [skapas och hanteras som sidoberoende resurser](/help/assets/content-fragments.md). Med dem kan du skapa kanalneutralt innehåll tillsammans med (eventuellt kanalspecifika) variationer.

   * Se [var innehållsfragmentresurser ska hittas i Web.Retail](#where-to-find-content-fragments-in-we-retail)

* Du kan sedan [använda dessa fragment och deras varianter när du redigerar](/help/sites-authoring/content-fragments.md) innehållssidorna.

   * Se [var innehållsfragment används i Web.Retail](#where-content-fragments-are-used-in-we-retail)

Den fullständiga dokumentationen om hur du skapar, hanterar, använder och utvecklar innehållsfragment finns i:

* Se [mer information](#further-information)

>[!NOTE]
>
>**Innehållsfragment** och **[Experience Fragments](/help/sites-authoring/experience-fragments.md)**är olika funktioner i AEM:
>
>* **Innehållsfragment** är redaktionellt innehåll, främst text och relaterade bilder. De är rent innehåll, utan design och layout.
>* **Experience Fragments** är helt utformat för innehåll, ett fragment av en webbsida.
>
>
Upplevelsefragment kan innehålla innehåll i form av innehållsfragment, men inte tvärtom.

## Var kan man hitta innehållsfragment i webb.butik {#where-to-find-content-fragments-in-we-retail}

Det finns flera exempelinnehållsfragment i We.Retail; navigera via **Assets**, **Files**, **We.Retail**, **English**, **Experiences**.

Detta omfattar **arktisk surfning i Lofoten**, ett fragment tillsammans med relaterade visuella resurser:

* Navigera via **Assets**, **Files**, **We.Retail**, **English**, **Experiences******,¥Artic Surfing in Lofoten¥:

   * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

Du kan markera och redigera den **arktiska surfningen i fragmentet Lofoten** :

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

Här kan du [redigera och hantera](/help/assets/content-fragments.md) fragment med hjälp av flikarna (vänstra panelen):

<!--![](do-not-localize/cf-45-aa.png) ![](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[Variationer](/help/assets/content-fragments-variations.md)**inklusive[Markering](/help/assets/content-fragments-markdown.md)
* **[Associerat innehåll](/help/assets/content-fragments-assoc-content.md)**
* **[Metadata](/help/assets/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## Där innehållsfragment används i webb.butik {#where-content-fragments-are-used-in-we-retail}

För att illustrera [sidredigering med ett innehållsavdrag](/help/sites-authoring/content-fragments.md) finns det flera exempelsidor under:

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

Till exempel refereras **arktisk surfning i innehållsavsnittet Lofoten** på sidan Platser:

* Navigera via **Sites**, **We.Retail**, **Language Masters**, **English**, **Experience**. Öppna sedan **Arktisk surfning i Lofoten** för redigering:

   * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## Ytterligare information {#further-information}

Mer information finns i:

* [Arbeta med innehållsfragment](/help/assets/content-fragments.md)

   * Lär dig hur du skapar, redigerar och hanterar resurser för innehållsfragment.

* [Sidredigering med innehållsfragment](/help/sites-authoring/content-fragments.md)

   * Använd ditt innehållsfragment när du redigerar en sida.

* [Utveckla AEM - Komponenter för innehållsfragment](/help/sites-developing/components-content-fragments.md)

   * En översikt över komponenterna för innehållsfragment.

* [Utveckla och utöka innehållsfragment](/help/sites-developing/customizing-content-fragments.md)

   * Information som hjälper dig att utveckla och utöka innehållsfragment.

