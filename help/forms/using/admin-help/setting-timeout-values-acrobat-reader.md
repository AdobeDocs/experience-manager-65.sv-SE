---
title: Ange timeoutvärden för användning med Acrobat Reader DC-tillägg
seo-title: Ange timeoutvärden för användning med Acrobat Reader DC-tillägg
description: Lär dig hur du anger timeoutvärden som ska användas med Acrobat Reader DC-tillägg.
seo-description: Lär dig hur du anger timeoutvärden som ska användas med Acrobat Reader DC-tillägg.
uuid: d6d072a0-0a30-417a-98b1-df8b4ff8f911
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a9aeeb89-45e9-4d5d-aa25-8145c89b64f2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Ange timeoutvärden för användning med Acrobat Reader DC-tillägg {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

När du arbetar med många PDF-filer i Acrobat Reader DC-tillägg måste du se till att följande tidsgränsvärden är korrekt inställda för att förhindra att jobben tajmar ut och misslyckas:

**Tidsgräns för borttagning av dokument**

Det här värdet kan anges i administrationskonsolen. Klicka på Inställningar > Systeminställningar > Konfigurationer och ange ett värde för Standardtidsgräns för dokumentborttagning.

**** Timeout för användarhanterarens AEM-formulär: Det här värdet kan anges genom att redigera filen config.xml. I administrationskonsolen klickar du på Inställningar > Användarhantering > Konfiguration > Importera och exportera konfigurationsfiler och sedan på Exportera. Öppna den exporterade filen config.xml och redigera följande rader:

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

Spara och importera sedan filen config.xml tillbaka till administrationskonsolen.

**** Tidsgräns för programserversession: Det här värdet kan anges på programservern. Mer information finns i dokumentationen som medföljer programservern.
