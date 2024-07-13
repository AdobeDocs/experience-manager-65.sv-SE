---
title: Introduktion till HTML5-formulär
description: HTML5-formulär är en ny funktion i Adobe Experience Manager 6.0 (AEM 6.0) som kan återge XFA-formulärmallar i HTML5-format.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 0facca18-ffa1-420c-859a-6f1f2c449d71
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# Introduktion till HTML5-formulär{#introduction-to-html-forms}

HTML5-formulär är en ny funktion i Adobe Experience Manager 6.0 (AEM 6.0) som kan återge XFA-formulärmallar i HTML5-format. Denna funktion gör det möjligt att återge formulär på mobila enheter och webbläsare på datorer där XFA-baserad PDF inte stöds. HTML5-formulär har inte bara stöd för XFA-formulärmallarnas befintliga funktioner, utan även nya funktioner, som klottersignaturer, för mobila enheter.

HTML5-formulär genererar dokument som baseras på HTML 5-standardkonstruktioner. Du kan visa HTML5-formulär i alla moderna webbläsare som stöder HTML5. Inga ytterligare webbläsarplugin-program behöver installeras för webbläsarna. Mer information om webbläsare som stöds finns i [Klientplattformar som stöds](https://adobe.com/go/learn_aemforms_supportedplatforms_63).

![HTML5-formulärförhandsgranskning](do-not-localize/mobile_form_on_an_ipad_date_14.png)

## Viktiga funktioner i HTML5-formulär {#key-capabilities-of-html-forms-br}

* Återger befintliga XFA-formulär i HTML5 som stöds i alla kompatibla webbläsare.
* Använder XFA:s standardfunktioner för blankettkonstruktion för att skapa blanketter för mobila enheter.
* Använder dynamiska XFA-funktioner i HTML5-format.
* Använder mycket exakt SVG-textlayout (SVG 1.1) för att matcha PDF-textlayouten.
* Tillhandahåller stöd för JavaScript och FormCalc.
* Sammanställer fragment dynamiskt till interaktiva formulär baserat på datadrivna händelser eller användarindata.
* Ger stöd för anpassad CSS som matchar formulärens utseende enligt företagets standarder.
* Möjliggör anpassade widgetar för datainhämtning.
* Ger stöd för integrering med webbprogram.

### Flerkanalspublicering {#multichannel-publishing}

Formulärutvecklare kan använda en XFA-mall för att återge formulär i PDF och HTML 5-format. Den här funktionen är bra i scenarier där du har en stor uppsättning XFA-formulär som kräver minimala ändringar för att kunna anpassa dig till HTML5-formulärdesignen. Du kan återge befintliga XFA-formulär till HTML5 för att ange olika enheter där XFA-baserad PDF ännu inte stöds.

## Hantera HTML5-formulär {#manage-html-forms}

AEM har också en enhetlig vy för att lista och hantera alla formulärmallar med hjälp av AEM Forms användargränssnitt. Du kan aktivera, inaktivera, publicera och förhandsgranska formulär. Mer information finns i [Introduktion till formulärhantering](../../forms/using/introduction-managing-forms.md).

### Forms-anpassning {#forms-customization}

HTML5-formulär återger formulärmallar med HTML 5-standardkonstruktioner. Detta gör det enkelt att anpassa och utöka formulär i HTML5-format med hjälp av webbtekniker, främst CSS och JavaScript. Du kan enkelt anpassa utseendet på befintliga widgetar, skapa egna widgetar eller använda anpassade format i formulär. Mer information om hur du skapar anpassade widgetar och anpassar befintliga widgetar finns i [Plug in anpassade widgetar med HTML5-formulär](../../forms/using/custom-widgets.md).
