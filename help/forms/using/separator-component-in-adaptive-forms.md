---
title: Avgränsningskomponent i adaptiva formulär
description: Du kan använda avgränsningskomponenten för att segmentera ett formulär visuellt.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: 11cbf865-c8e2-4833-b0b8-a3cb5e42f5cd
source-git-commit: d85fc98d9a31bc4014aef4311ba0f838c7ef619a
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# Avgränsningskomponent i adaptiva formulär{#separator-component-in-adaptive-forms}

<span class="preview"> Adobe rekommenderar att man använder modern och utbyggbar datainhämtning [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) for [skapa ny Adaptive Forms](/help/forms/using/create-an-adaptive-form-core-components.md) eller [lägga till adaptiv Forms på AEM Sites-sidor](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs ett äldre sätt att skapa adaptiva Forms med baskomponenter. </span>

Du kan använda avgränsarkomponenten för att dela upp paneler i ett formulär visuellt. Du kan definiera det övergripande utseendet och formatet för en avgränsningskomponent genom att ange följande egenskaper för avgränsningskomponenten:

* **Elementnamn:** Anger komponentens namn. SOM-uttrycken adresserar komponenten med ett värde angivet i fältet Elementnamn.
* **Tjocklek:** Anger tjockleken på avgränsningskomponenten i pixlar.

* **CSS-klass:** Anger den anpassade CSS-klassen för avgränsarkomponenten

* **Textbundna format:** Med AEM Forms kan du nu använda infogade CSS-format på enskilda adaptiva formulärkomponenter och förhandsgranska ändringarna i realtid.

Du kan använda layoutläget för att definiera antalet kolumner som avgränsningskomponenten sträcker sig till. Mer information finns i [Använd layoutläget för att ändra storlek på komponenter](../../forms/using/resize-using-layout-mode.md).

Så här anger du egenskaper för en avgränsningskomponent:

1. Markera en avgränsningskomponent och markera ![cmppr](assets/cmppr.png). Egenskaperna öppnas i sidofältet.
1. Klicka på en flik i avsnittet Infoga CSS-egenskaper så att du kan ange CSS-egenskaper. Till exempel: a. Klicka på fliken Fält **Lägg till objekt**. En rad med två fält läggs till.
1. I det första fältet från vänster anger du den CSS3-egenskap som du vill använda. Till exempel: **border**. Du kan också välja en egenskap genom att klicka på nedpilsknappen. Listrutan är inte fullständig och du kan ange ett CSS3-egenskapsnamn som stöds i det här fältet.
1. Ange ett giltigt värde för den angivna CSS3-egenskapen i det intilliggande fältet. Till exempel: **3-pixlars solid black**.
1. Klicka **Lägg till objekt** för att ange en annan egenskap och dess värde.
1. Klicka **Förhandsgranska** så att du kan förhandsgranska ändringarna i formuläret.
1. Klicka **OK** om du vill bekräfta ändringarna eller **Avbryt** för att stänga dialogrutan utan ändringar.
