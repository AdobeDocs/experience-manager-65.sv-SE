---
title: Konfigurera formulärutdata
description: Lär dig konfigurera formulärutdata. Om du vill konfigurera formulärutdata och aktivera funktionen använder du de anpassade skripten innan formuläret skickas.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d739806c-ce72-40fd-b304-3262a0988d96
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Konfigurera formulärutdata{#configuring-form-output}

## Ange vilken typ av HTML-utdata som returneras till webbläsaren {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. Klicka på Tjänster > Formulär i administrationskonsolen.
1. Välj något av följande alternativ i listan Utdatatyp under Formulärutdata:

   **Fullt HTML:** Om du vill återge formuläret med fullständiga HTML-taggar (en fullständig HTML-sida). Det här värdet är standardvärdet.

   **Formulärbrödtext:** Återge formuläret inom `<BODY>` -taggar (inte en fullständig HTML-sida).

1. Klicka på Spara.

## Ange platsen där PDF-innehåll återges {#specify-the-location-where-pdf-content-is-rendered}

1. Välj något av följande alternativ i listan Återge vid under Formulärutdata:

   **Klient:** Återge PDF forms i Adobe Acrobat eller Adobe Reader. Klientsidorendering förbättrar prestanda för AEM formulär och gäller endast för PDFForm-omvandling.

   **Server:** Återge PDF forms på programservern.

   **Auto:** Om du vill återge formuläret PDF på den plats som anges av konfigurationsvärdet `dynamicRender` för XDP-filen. Det här värdet är standardvärdet.

1. Klicka på Spara.

## Konfigurera anrop av anpassade skript innan formuläret skickas {#configuring-invocation-of-custom-scripts-before-form-submit}

>[!NOTE]
> 
> Kontrollera att användaren har administratörsbehörighet för att komma åt administratörskonsolen.

Gör så här för att aktivera funktionen:

1. Logga in på administrationskonsolen.
1. Gå till **Tjänster** > **formulär**.
1. Ange utdatatypen Form Body.
1. Spara inställningarna.
1. Deklarera en JavaScript-variabel, __CUSTOM_SCRIPTS_VERSION, i huvudsektionen i HTML-koden och ställ in värdet på 1.

   >[!NOTE]
   >
   >*Om du vill inaktivera funktionen kan du ta bort variabeln JavaScript eller ange värdet 0.*
