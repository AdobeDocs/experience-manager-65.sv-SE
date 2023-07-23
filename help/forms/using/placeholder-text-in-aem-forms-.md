---
title: Platshållartext i AEM Forms
seo-title: Placeholder text in AEM Forms
description: Platshållartext är avsedd att hjälpa användaren med datainmatning när kontrollen inte har något värde. Det kan vara ett exempelvärde eller en kort beskrivning av det förväntade formatet.
seo-description: Placeholder text is intended to aid the user with data entry when the control has no value. It could be a sample value or a brief description of the expected format.
uuid: 69f80722-93db-4932-9016-4b530e183d4e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: f9ff2cc5-3f0a-4b2f-a206-2fe0985646ea
docset: aem65
feature: Adaptive Forms
exl-id: 6b6e27b5-8b4e-489c-9e72-4d256692c1ca
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Platshållartext i AEM Forms {#placeholder-text-in-aem-forms}

<span class="preview"> Adobe rekommenderar att man använder modern och utbyggbar datainhämtning [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) for [skapa ny Adaptive Forms](/help/forms/using/create-an-adaptive-form-core-components.md) eller [lägga till adaptiv Forms på AEM Sites-sidor](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-program, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptive Forms med grundläggande komponenter. </span>

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
