---
title: Visa problem för XFA-baserade PDF forms-dokument och policyskyddade dokument
description: Visa problem för XFA-baserade PDF forms-dokument och policyskyddade dokument
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ebb61f2c5056a780e829e64031f8eba69a8ae25b
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Visa problem för XFA-baserade PDF forms-dokument och policyskyddade dokument

Kontrollera följande om du inte kan öppna ett XFA-baserat PDF-formulär eller ett policyskyddat dokument med Adobe LiveCycle Rights Management:

* XFA-baserade PDF forms-dokument och policyskyddade dokument kräver Adobe® Acrobat® eller Adobe® Reader® version 8 och senare. Läs [Adobe nedladdningar](https://www.adobe.com/downloads.html) om du vill hämta de senaste Reader- eller Acrobat-filerna.
* Webbläsare som Mozilla Firefox och Google Chrome har ett inbyggt visningsprogram för PDF som inte stöder XFA-baserade PDF forms. Om du vill visa XFA-baserade PDF forms i dessa webbläsare måste du konfigurera så att PDF-filer öppnas med Acrobat eller Reader. Mer information finns i XFA-baserad PDF forms på Mozilla Firefox och Google Chrome.
* I Acrobat och Reader i Microsoft® Windows® kan du konfigurera så att PDF-filer öppnas i skyddat visningsläge, vilket förhindrar att XFA-baserade PDF forms-dokument och principskyddade dokument öppnas. Kontrollera att Protected View-läget i Acrobat eller Reader är inaktiverat. Mer information finns i [Skyddad vy (endast Windows)](https://helpx.adobe.com/se/acrobat/kb/end-of-support-acrobat-x-reader-x.html).
* Om du försöker få åtkomst till XFA-baserade PDF forms-dokument eller policyskyddade dokument på din mobila enhet bör du tänka på följande:

   * Adobe Reader för mobilen krävs för att öppna policyskyddade dokument på mobila enheter. Mer information finns i [mobilappen Adobe Reader](https://www.adobe.com/in/acrobat/mobile/acrobat-reader.html).
   * iOS, Android, Blackberry och mobila enheter och smarttelefoner har inte stöd för plugin-programmet Adobe Reader med XFA-formulär. LiveCycle ES4 är en tjänst som riktar sig till mobila enheter som använder HTML5. Den som skapar formuläret måste använda den tjänsten för att kunna använda formulären på dessa enheter.
   * Om du använder Metro-stilen på en Windows 8-mobilenhet ska du ändra till vyn Klassisk eller använda HTML5 med LiveCycle ES4.

>[!NOTE]
>
>LiveCycle ES4 har stöd för återgivning av XFA-baserade formulär till HTML5 så att formulären kan öppnas i webbläsare med stöd för HTML5, även på mobila enheter som iPad. Formuläråtergivningen i HTML5 bevarar layouten i formulärdesignen och stöder de flesta formulärlogik (som JavaScript, formulärberäkning och formulärvalidering) som är inbäddad i XFA-formulärmallen. På så sätt överförs era teknikinvesteringar i XFA-formulär enkelt till de enheter där Adobe Reader-pluginen inte kan köras.
>Mer information finns i Uppgradera till [LiveCycle-produktdokumentation](https://business.adobe.com/products/experience-manager/forms/aem-forms.html).

[Juridiska meddelanden](https://chl-author-preview.corp.adobe.com/content/help/en/legal/legal-notices.html)    |    [Integritetspolicy &#x200B;](https://www.adobe.com/privacy.html)