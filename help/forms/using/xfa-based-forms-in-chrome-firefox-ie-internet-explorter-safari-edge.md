---
title: Det går inte att öppna XFA-baserad PDF forms i Google Chrome, Firefox, Microsoft&reg; Edge, Microsoft&reg; Internet Explorer eller Apple Safari
description: Det går inte att öppna XFA-baserad PDF forms i Google Chrome, Firefox, Microsoft&reg; Edge, Microsoft&reg; Internet Explorer eller Apple Safari
feature: Adaptive Forms,Document Services
exl-id: fdd15315-e0d6-4d80-acb4-2e0ecec716c4
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# Det går inte att öppna XFA-baserad PDF forms i Google Chrome, Firefox, Microsoft® Edge, Microsoft® Internet Explorer eller Apple Safari{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

Många senaste webbläsarversioner har fått sitt eget begränsade stöd för XFA-baserad PDF forms. Även om dessa webbläsare kan öppna XFA-baserad PDF forms är de tillgängliga funktionerna begränsade. Om du inte kan öppna eller skicka ett XFA-baserat PDF-formulär i en modern webbläsare använder du någon av följande metoder:

* Använd [Adobe® Acrobat®](https://www.adobe.com/acrobat.html) eller [Adobe® Adobe® Reader®](https://get.adobe.com/reader/), version 8 eller senare för att öppna och skicka XFA-baserad PDF forms.
* I Microsoft® Windows® kan du konfigurera till att öppna PDF i läget Skyddad vy i Acrobat och Reader, vilket förhindrar att XFA-baserade PDF forms öppnas. Kontrollera att Protected View-läget i Acrobat eller Reader är inaktiverat. Mer information finns i [Skyddad vy (endast Windows)](https://helpx.adobe.com/in/reader/using/protected-mode-windows.html).
* (För Forms-utvecklare) Adobe Experience Manager Forms erbjuder även support för:

   * [återge XFA-baserade formulär i HTML5 Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?lang=sv-SE&#key-capabilities-of-html-forms-br) så att formulären kan öppnas i webbläsare som stöder HTML5, inklusive webbläsare som körs på mobila enheter som iPad. Formuläråtergivningen i HTML 5 bevarar layouten i formulärdesignen och stöder de flesta formulärlogik (som JavaScript, formulärberäkning och formulärvalidering) som är inbäddad i XFA-formulärmallen.
   * [Konvertera XFA-baserade formulär till mobilresponsiv anpassad, anpassad Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?lang=sv-SE&#create-an-adaptive-form-based-on-an-xfa-form-template). Dessa formulär har en responsiv layout, personaliseringsfunktioner och anpassar sig dynamiskt efter användarnas svar genom att lägga till eller ta bort fält eller avsnitt efter behov. De tillhandahåller också färdiga anslutningar för olika datakällor, dokumentfunktioner och enkel anslutning till Adobe Analytics för utvärdering av prestanda. Mer information finns i [Nyckelfunktioner](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=sv-SE)
På så sätt är era teknikinvesteringar i XFA-formulär skyddade och fortsätter att ge optimala upplevelser för era slutanvändare. Mer information finns i [Adobe Experience Manager Forms produktdokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=sv-SE).
