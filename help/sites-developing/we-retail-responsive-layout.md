---
title: Provar Responsiv layout i We.Retail
description: Lär dig hur du provar responsiv layout i Adobe Experience Manager med We.Retail.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 6df5fb10-a7f1-4d5d-ac00-b4be3d5d3d18
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 3%

---

# Provar Responsiv layout i We.Retail{#trying-out-responsive-layout-in-we-retail}

Alla webbsidor använder komponenten Layoutbehållare för att implementera responsiv design. Layoutbehållaren har ett styckesystem där du kan placera komponenter i ett responsivt rutnät. Rutnätet kan ändra layouten beroende på enhetens/fönstrets storlek och format. Komponenten används tillsammans med **Layout** i sidredigeraren, där du kan skapa och redigera din responsiva layout beroende på enhet.

## Prova {#trying-it-out}

1. Redigera sidan Arktisk surfning i sektionen Erfarenheter i huvudgrenen för språk.

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html

1. Växla till **Förhandsgranska** för att se sidan som den skulle återges för en besökare på webbplatsen. Bläddra nedåt till artikelns innehåll *Aloha-sprit i Norge*.

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. Ändra storlek på webbläsarfönstret och se hur layouten anpassas dynamiskt efter storleksändringen.

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. Växla till layoutläge. Emulatorverktygsfältet visas automatiskt så att du kan planera layouten per målenhet.

   Om du markerar en komponent visas flytande och dolda alternativ på redigeringsmenyn tillsammans med storlekshandtag för komponenten.

   ![chlimage_1-180](assets/chlimage_1-180.png)

1. När du tar och drar i storlekshandtaget för komponenten visas automatiskt layoutstödrastret så att du lättare kan ändra storlek.

   ![chlimage_1-181](assets/chlimage_1-181.png)

## Ytterligare information {#further-information}

Mer information finns i redigeringsdokumentet [Responsiv layout](/help/sites-authoring/responsive-layout.md) eller administratörsdokumentet [Konfigurera layoutbehållare och layoutläge](/help/sites-administering/configuring-responsive-layout.md) för fullständig teknisk information.
