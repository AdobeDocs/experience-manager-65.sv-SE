---
title: Platshållartext i AEM Forms
description: Platshållartext är avsedd att hjälpa användaren med datainmatning när kontrollen saknar värde. Det kan vara ett exempelvärde eller en kort beskrivning av det förväntade formatet.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: 6b6e27b5-8b4e-489c-9e72-4d256692c1ca
source-git-commit: 6dbec0f41396c2b41d5324c4ecf6f1f33b1d0780
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# Platshållartext i AEM Forms {#placeholder-text-in-aem-forms}

<span class="preview"> Adobe rekommenderar att man använder modern och utbyggbar datainhämtning [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) for [skapa ny Adaptive Forms](/help/forms/using/create-an-adaptive-form-core-components.md) eller [lägga till adaptiv Forms på AEM Sites-sidor](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter. </span>

Platshållartexten representerar ett ord eller en kort fras. Avsikten är att hjälpa användaren att ange data när kontrollen inte har något värde. En platshållartext kan vara ett exempelvärde eller en kort beskrivning av det förväntade formatet. Platshållartexten visas innan användaren anger ett värde, den tas bort när användaren anger eller väljer ett värde.

>[!NOTE]
>
>Om platshållartexten har angetts måste den ha ett värde som inte innehåller några nya radtecken.

![Datumkomponent med och utan platshållartext](assets/dat-picker-place-holder-text.png)

**S.** Datumkomponent med platshållartext **B.** Datumkomponent utan platshållartext

AEM Forms stöder platshållartext för lösenordsrutor, datumväljare, numeriska rutor och textrutefält.\
Platshållartexter stöds inte för den inbyggda HTML5-datumwidgeten. Så här anger du en platshållartext:

1. Högerklicka på en komponent som stöder platshållartext och klicka på **Redigera**. Dialogrutan Redigera komponent visas.

1. Öppna **Titel och text** -fliken.
1. Ange ett ord eller en kort fras i **Platshållartextruta**. Klicka **OK**.

>[!NOTE]
>
>Platshållartext stöds inte i Microsoft Internet Explorer 9.