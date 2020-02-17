---
title: Ange alternativ för internationalisering
seo-title: Ange alternativ för internationalisering
description: Lär dig hur du anger språkområdet som används för att återge formulär och hur du anger teckenuppsättningen som används för att koda utdataströmmen.
seo-description: Lär dig hur du anger språkområdet som används för att återge formulär och hur du anger teckenuppsättningen som används för att koda utdataströmmen.
uuid: bb77f5f3-634f-4285-9b10-c4dd40085e69
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e845d13f-bef2-442d-af9a-4f92d7616a46
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Ange alternativ för internationalisering{#setting-internationalization-options}

## Ange den språkinställning som används för att återge formulär {#specify-the-locale-used-to-render-forms}

Du kan ange vilken språkinställning som ska användas vid återgivning av ett PDF-formulär. Fälten i ett PDF-formulär använder den angivna språkinställningen för att visa data. Om språkområdet till exempel är inställt på tyska, används decimalavgränsare för numeriska värden i formuläret. Språkinställningen används också för att skicka valideringsmeddelanden till klientenheter, som webbläsare, som en del av HTML-omvandlingar.

1. Klicka på Tjänster > Formulär i administrationskonsolen.
1. Under Internationalisering i listan Språk väljer du den språkinställning som används för att återge ett formulär. Standardvärdet är engelska (USA).
1. Klicka på Spara.

## Ange den teckenuppsättning som används för att koda utdataströmmen {#specify-the-character-set-used-to-encode-the-output-stream}

1. Välj en teckenuppsättning i listan Teckenuppsättning under Internationalisering. Den här inställningen beror på vilken API som används, antingen renderHTMLForm eller renderPDFForm. Om du vill ange en annan teckenuppsättning än de som visas väljer du Anpassad och anger ett kodningsvärde i rutan som visas.

   För HTML-omformningar stöder AEM-formulär teckenkodningsvärden som definieras av `java.nio.charset` paketet. Om sFormPreference är PDFForm stöds endast specifika teckenuppsättningar. Teckenuppsättningen måste vara ett giltigt kanoniskt namn. Standardvärdet är ISO-8859-1.

1. Klicka på Spara.

