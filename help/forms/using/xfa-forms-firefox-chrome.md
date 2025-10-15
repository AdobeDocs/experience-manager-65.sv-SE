---
title: Öppna XFA-baserade PDF forms i Firefox och Chrome
description: Öppna XFA-baserade PDF forms i Firefox och Chrome
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ebb61f2c5056a780e829e64031f8eba69a8ae25b
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# Öppna XFA-baserade PDF forms i Firefox och Chrome

## Problem

Det inbyggda PDF-visningsprogrammet som introducerades med Mozilla Firefox och Google Chrome stöder inte XFA-baserade PDF forms. Därför öppnas inte XFA-baserade PDF forms i senare versioner av Firefox och Chrome.

## Lösning

Om du vill använda XFA-baserade PDF forms i Firefox och Chrome utför du följande steg för att konfigurera Firefox och Chrome att öppna PDF-filer med Adobe Reader eller Adobe Acrobat.

>[!NOTE]
> 
> Kontrollera att du har Adobe Reader eller Adobe Acrobat installerat på datorn.

### Konfigurera Firefox

1. I Firefox väljer du **Verktyg > Alternativ**.

1. Klicka på **Program** i dialogrutan Alternativ.

1. Skriv PDF i sökfältet på fliken Program.

1. För PDF-innehållstypen (Portable Document Format) i sökresultatet väljer du **Använd Adobe Acrobat (i Firefox)** i listrutan Åtgärd.
   ![use-adobe-acrobat](/help/forms/using/assets/use-adobe-acrobat.png)
1. Klicka på OK.

1. Starta om Firefox.

### Konfigurera Chrome

1. Gå till chrome://plugins/ i Chrome.

1. Klicka på Inaktivera under Chrome PDF Viewer och klicka på Aktivera under Adobe PDF Plug-In.
   ![chrome-pdf-viewer](/help/forms/using/assets/chrome-image.png)
Mer information finns i [Adobe PDF plug-in &#x200B;](https://support.google.com/chrome/?hl=en&visit_id=638803785294106945-2276548125&rd=4&topic=3421431#topic=7439538) -dokumentationen från Google.

>[!NOTE]
> 
> LiveCycle ES4 har stöd för återgivning av XFA-baserade formulär till HTML5 så att formulären kan öppnas i webbläsare med stöd för HTML5, även på mobila enheter som iPad. Formuläråtergivningen i HTML5 bevarar layouten i formulärdesignen och stöder de flesta formulärlogik (som JavaScript, formulärberäkning och formulärvalidering) som är inbäddad i XFA-formulärmallen. På så sätt överförs era teknikinvesteringar i XFA-formulär enkelt till enheter där det inte går att köra Adobe Reader-pluginprogrammet.
>Mer information finns i [LiveCycle-produktdokumentation](https://business.adobe.com/se/products/experience-manager/forms/aem-forms.html).

[Juridiska meddelanden](https://chl-author-preview.corp.adobe.com/content/help/en/legal/legal-notices.html)    |    [Integritetspolicy &#x200B;](https://www.adobe.com/privacy.html)