---
title: Avgränsningskomponent i adaptiva formulär
seo-title: Separator component in adaptive forms
description: Du kan använda avgränsningskomponenten för att segmentera ett formulär visuellt.
seo-description: You can use the separator component to visually segregate sections of a form.
uuid: f8d2aed3-52aa-437f-bfe3-0c8779e7986c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: a8aa77fe-5880-4c4e-9e1b-3c5a8772c29d
docset: aem65
feature: Adaptive Forms
exl-id: 11cbf865-c8e2-4833-b0b8-a3cb5e42f5cd
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Avgränsningskomponent i adaptiva formulär{#separator-component-in-adaptive-forms}

<span class="preview"> Adobe rekommenderar att man använder modern och utbyggbar datainhämtning [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) for [skapa ny Adaptive Forms](/help/forms/using/create-an-adaptive-form-core-components.md) eller [lägga till adaptiv Forms på AEM Sites-sidor](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-program, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptive Forms med grundläggande komponenter. </span>

Du kan använda avgränsarkomponenten för att dela upp paneler i ett formulär visuellt. Du kan definiera det övergripande utseendet och formatet för en avgränsningskomponent genom att ange följande egenskaper för avgränsningskomponenten:

* **Elementnamn:** Anger komponentens namn. SOM-uttrycken adresserar komponenten med ett värde som anges i fältet Elementnamn.
* **Tjocklek:** Anger tjockleken på avgränsarkomponenten i pixlar.

* **CSS-klass:** Anger den anpassade CSS-klassen för avgränsarkomponenten

* **Textbundna format:** Med AEM Forms kan du nu använda infogade CSS-format på enskilda adaptiva formulärkomponenter och förhandsgranska ändringarna i realtid.

Du kan använda layoutläget för att definiera antalet kolumner som avgränsningskomponenten sträcker sig till. Mer information finns i [Använd layoutläget för att ändra storlek på komponenter](../../forms/using/resize-using-layout-mode.md).

Så här anger du egenskaper för en avgränsningskomponent:

1. Markera en separationskomponent och tryck på ![cmppr](assets/cmppr.png). Egenskaperna öppnas i sidofältet.
1. Klicka på en flik i avsnittet Infogade CSS-egenskaper för att ange CSS-egenskaper. Till exempel: a. Klicka på fliken Fält **Lägg till objekt**. En rad med två fält läggs till.
1. I det första fältet från vänster anger du den CSS3-egenskap som du vill använda. Till exempel: **border**. Du kan också välja en egenskap genom att klicka på nedpilsknappen. Listrutan är inte fullständig och du kan ange ett CSS3-egenskapsnamn som stöds i det här fältet.
1. Ange ett giltigt värde för den angivna CSS3-egenskapen i det intilliggande fältet. Till exempel: **3px solid svart**.
1. Klicka **Lägg till objekt** för att ange en annan egenskap och dess värde.
1. Klicka **Förhandsgranska** om du vill förhandsgranska ändringarna i formuläret.
1. Klicka **OK** för att bekräfta ändringarna eller **Avbryt** för att stänga dialogrutan utan ändringar.
