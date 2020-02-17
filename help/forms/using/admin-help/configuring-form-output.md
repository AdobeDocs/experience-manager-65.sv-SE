---
title: Konfigurera formulärutdata
seo-title: Konfigurera formulärutdata
description: Lär dig hur du konfigurerar formulärutdata.
seo-description: Lär dig hur du konfigurerar formulärutdata.
uuid: 70aad14e-c845-4ef3-a751-ad8860d5d505
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 17c9b69a-3c6f-47e3-a828-841bb90eba8b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konfigurera formulärutdata{#configuring-form-output}

## Ange vilken typ av HTML-utdata som returneras till webbläsaren {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. Klicka på Tjänster > Formulär i administrationskonsolen.
1. Välj något av följande alternativ i listan Utdatatyp under Formulärutdata:

   **** Fullständig HTML: Återge formuläret med fullständiga HTML-taggar (en komplett HTML-sida). Det här värdet är standardvärdet.

   **** Formulärbrödtext: Om du vill återge formuläret inom `<BODY>` -taggar (inte en fullständig HTML-sida).

1. Klicka på Spara.

## Ange platsen där PDF-innehåll återges {#specify-the-location-where-pdf-content-is-rendered}

1. Välj något av följande alternativ i listan Återge vid under Formulärutdata:

   **** Klient: Återge PDF-formulär i Adobe Acrobat eller Adobe Reader. Klientsidesrendering förbättrar prestanda för AEM-formulär och gäller endast för PDFForm-omvandling.

   **** Server: Återge PDF-formulär på programservern.

   **** Auto: Om du vill återge PDF-formuläret på den plats som anges av XDP-filens `dynamicRender` konfigurationsvärde. Det här värdet är standardvärdet.

1. Klicka på Spara.

## Konfigurera anrop av anpassade skript innan formuläret skickas {#configuring-invocation-of-custom-scripts-before-form-submit}

Gör så här för att aktivera funktionen:

1. Logga in på administrationskonsolen.
1. Gå till **Tjänster** > **Formulär**.
1. Ange utdatatypen som Formulärbrödtext.
1. Spara inställningarna.
1. Deklarera en JavaScript-variabel, __CUSTOM_SCRIPTS_VERSION, i HTML-kodens head-avsnitt och ställ in värdet på 1.

   >[!NOTE]
   >
   >*Om du vill inaktivera funktionen kan du ta bort JavaScript-variabeln eller ange värdet 0.*

