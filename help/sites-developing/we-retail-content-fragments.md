---
title: Testa innehållsfragment i webb.detaljhandel
description: Lär dig hur du provar innehållsfragment i Adobe Experience Manager med hjälp av We.Retail.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 1e5d8184-7164-4984-b43e-421015e8bf52
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Testa innehållsfragment i webb.detaljhandel{#trying-out-content-fragments-in-we-retail}

Med innehållsfragment kan du skapa kanalneutralt innehåll tillsammans med (eventuellt kanalspecifika) variationer. **Vi.butik** (som är tillgängligt i en körklar instans av Adobe Experience Manager) innehåller fragmentet **Arktisk surfning i Lofoten** som ett grundläggande urval. Detta visar att:

* Adobe Experience Manager (AEM) innehållsfragment är [skapat och hanterat som sidoberoende resurser](/help/assets/content-fragments/content-fragments.md). Med dem kan du skapa kanalneutralt innehåll tillsammans med (eventuellt kanalspecifika) variationer.

   * Se [Var kan du hitta resurser för innehållsfragment i webb.butik](#where-to-find-content-fragments-in-we-retail)

* Då kan du [använda dessa fragment och deras variationer vid redigering](/help/sites-authoring/content-fragments.md) dina innehållssidor.

   * Se [Där innehållsfragment används i webb.butik](#where-content-fragments-are-used-in-we-retail)

Den fullständiga dokumentationen om hur du skapar, hanterar, använder och utvecklar innehållsfragment finns i:

* Se [Ytterligare information](#further-information)

>[!NOTE]
>
>**Innehållsfragment** och **[Upplevelsefragment](/help/sites-authoring/experience-fragments.md)** har olika funktioner i AEM:
>
>* **Innehållsfragment** är redaktionellt innehåll, främst text, och relaterade bilder. De är rent innehåll, utan design och layout.
>* **Upplevelsefragment** är helt utformat för innehåll, ett fragment av en webbsida.
>
>Upplevelsefragment kan innehålla innehåll i form av innehållsfragment, men inte tvärtom.

## Var kan man hitta innehållsfragment i webb.butik {#where-to-find-content-fragments-in-we-retail}

Det finns flera exempelinnehållsfragment i We.Retail; navigera via **Resurser**, **Filer**, **Vi.butik**, **Engelska**, **Erfarenheter**.

Dessa innehåller **Arktisk surfning i Lofoten**, ett fragment tillsammans med relaterade visuella resurser:

* Navigera genom **Resurser**, **Filer**, **Vi.butik**, **Engelska**, **Erfarenheter**, **Arktisk surfning i Lofoten**:

   * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![cf-4](assets/cf-44.png)

Du kan markera och redigera **Arktisk surfning i Lofoten** fragment:

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

Här kan du [redigera och hantera](/help/assets/content-fragments/content-fragments.md) fragmentet med hjälp av flikarna (vänster sida):

<!--![cf-45-aa](do-not-localize/cf-45-aa.png) ![cf-45-a](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[Variationer](/help/assets/content-fragments/content-fragments-variations.md)** inkluderar [Markering](/help/assets/content-fragments/content-fragments-markdown.md)
* **[Associerat innehåll](/help/assets/content-fragments/content-fragments-assoc-content.md)**
* **[Metadata](/help/assets/content-fragments/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## Där innehållsfragment används i webb.butik {#where-content-fragments-are-used-in-we-retail}

För att illustrera [skapa sidor med ett innehållsfragment](/help/sites-authoring/content-fragments.md) det finns flera exempelsidor i, till exempel:

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

Till exempel **Arktisk surfning i Lofoten** Det finns referenser till innehållsfragment på sidan Platser:

* Navigera via **Webbplatser**, **Vi.butik**, **Språkmallar**, **Engelska**, **Upplevelse**. Öppna **Arktisk surfning i Lofoten** för redigering:

   * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## Ytterligare information {#further-information}

Mer information finns i:

* [Arbeta med innehållsfragment](/help/assets/content-fragments/content-fragments.md)

   * Lär dig hur du skapar, redigerar och hanterar resurser för innehållsfragment.

* [Sidredigering med innehållsfragment](/help/sites-authoring/content-fragments.md)

   * Använd ditt innehållsfragment när du redigerar en sida.

* [Utveckla AEM - komponenter för innehållsfragment](/help/sites-developing/components-content-fragments.md)

   * En översikt över komponenterna för innehållsfragment.

* [Utveckla och utöka innehållsfragment](/help/sites-developing/customizing-content-fragments.md)

   * Information som hjälper dig att utveckla och utöka innehållsfragment.
