---
title: Det går inte att öppna XFA-baserad PDF forms i Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer eller Apple Safari
seo-title: Unable to open XFA-based PDF forms in Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer, or Apple Safari
feature: Adaptive Forms
source-git-commit: abaef885f1324c4e0e4c5d74485d5b419ff88e2b
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---


# Det går inte att öppna XFA-baserad PDF forms i Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer eller Apple Safari{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

Många senaste webbläsarversioner har fått sitt eget begränsade stöd för XFA-baserad PDF forms. Även om dessa webbläsare kan öppna XFA-baserad PDF forms är de tillgängliga funktionerna begränsade. Om du inte kan öppna eller skicka ett XFA-baserat PDF-formulär i en modern webbläsare använder du någon av följande metoder:

* Använd [Adobe® Acrobat®](https://www.adobe.com/acrobat.html) eller [Adobe® Adobe® Reader®](https://get.adobe.com/reader/), version 8 eller senare för att öppna och skicka XFA-baserad PDF forms.
* Med Acrobat och Reader i Microsoft® Windows® kan du konfigurera så att PDF öppnas i skyddat läge, vilket förhindrar att XFA-baserat PDF forms öppnas. Kontrollera att Protected View-läget i Acrobat eller Reader är inaktiverat. Mer information finns i [Skyddad vy (endast Windows)](https://helpx.adobe.com/in/reader/using/protected-mode-windows.html).
* (För Forms-utvecklare) Adobe Experience Manager Forms erbjuder även support för
   * [återge XFA-baserade formulär i HTML5 Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?#key-capabilities-of-html-forms-br) så att formulären kan öppnas i webbläsare som har stöd för HTML5, även på mobila enheter som iPad. Formuläråtergivningen i HTML5 bevarar layouten i formulärdesignen och stöder de flesta formulärlogik (till exempel JavaScript, formulärberäkning och formulärvalidering) som är inbäddad i XFA-formulärmallen.
   * [konvertera XFA-baserade formulär till mobilresponsiv Adaptiv Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?#create-an-adaptive-form-based-on-an-xfa-form-template). Dessa formulär har en responsiv layout, personaliseringsfunktioner och anpassar sig dynamiskt efter användarnas svar genom att lägga till eller ta bort fält eller avsnitt efter behov. De har också färdiga kopplingar för olika datakällor, funktioner för att dokumentera poster och enkel anslutning till Adobe Analytics för prestandautvärdering. Mer information finns i [Viktiga funktioner](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/key-features.html).

På så sätt är era teknikinvesteringar i XFA-formulär skyddade och fortsätter att ge optimala upplevelser för era slutanvändare. Mer information finns i [Adobe Experience Manager Forms produktdokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html).
