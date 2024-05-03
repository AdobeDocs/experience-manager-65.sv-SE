---
title: Konfigurera formulärutdata
description: Lär dig konfigurera formulärutdata. Om du vill konfigurera formulärutdata och aktivera funktionen använder du de anpassade skripten innan formuläret skickas.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d739806c-ce72-40fd-b304-3262a0988d96
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# Konfigurera formulärutdata{#configuring-form-output}

## Ange vilken typ av HTML-utdata som returneras till webbläsaren {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. Klicka på Tjänster > Formulär i administrationskonsolen.
1. Välj något av följande alternativ i listan Utdatatyp under Formulärutdata:

   **Full HTML:** Om du vill återge formuläret med fullständiga HTML-taggar (en hel HTML-sida). Det här värdet är standardvärdet.

   **Formulärtext:** Återge formuläret inom `<BODY>` taggar (inte en fullständig HTML-sida).

1. Klicka på Spara.

## Ange platsen där PDF-innehåll återges {#specify-the-location-where-pdf-content-is-rendered}

1. Välj något av följande alternativ i listan Återge vid under Formulärutdata:

   **Klient:** Återge PDF forms i Adobe Acrobat eller Adobe Reader. Klientsidorendering förbättrar prestanda för AEM formulär och gäller endast för PDFForm-omvandling.

   **Server:** Om du vill återge PDF forms på programservern.

   **Auto:** Återge formuläret PDF på den plats som anges av `dynamicRender` XDP-filens konfigurationsvärde. Det här värdet är standardvärdet.

1. Klicka på Spara.

## Konfigurera anrop av anpassade skript innan formuläret skickas {#configuring-invocation-of-custom-scripts-before-form-submit}

Gör så här för att aktivera funktionen:

1. Logga in på administrationskonsolen.
1. Gå till **Tjänster** > **formulär**.
1. Ange utdatatypen Form Body.
1. Spara inställningarna.
1. Deklarera en JavaScript-variabel, __CUSTOM_SCRIPTS_VERSION, i huvudsektionen i HTML-koden och ställ in värdet på 1.

   >[!NOTE]
   >
   >*Om du vill inaktivera funktionen kan du ta bort JavaScript-variabeln eller ange värdet 0.*
