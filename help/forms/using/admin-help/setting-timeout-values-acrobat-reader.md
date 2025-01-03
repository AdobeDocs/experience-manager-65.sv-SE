---
title: Ange timeoutvärden för användning med Acrobat Reader DC Extensions
description: Lär dig hur du anger timeoutvärden för Acrobat Reader DC Extensions.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0a55aab3-14a3-41ad-8533-dc2cd116a848
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Ange timeoutvärden för användning med Acrobat Reader DC Extensions  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

>[!NOTE]
> 
> Kontrollera att användaren har administratörsbehörighet för att komma åt administratörskonsolen.

När du arbetar med många PDF-filer i Acrobat Reader DC Extensions måste du se till att följande tidsgränsvärden är korrekt inställda för att förhindra att jobben tajmar ut och misslyckas:

**Tidsgräns för dokumentborttagning**

Det här värdet kan anges i administrationskonsolen. Klicka på Inställningar > Systeminställningar > Konfigurationer och ange ett värde för Standardtidsgräns för dokumentborttagning.

**Timeout för användarhanterarens AEM:** Det här värdet kan anges genom redigering av filen config.xml. I administrationskonsolen klickar du på Inställningar > Användarhantering > Konfiguration > Importera och exportera konfigurationsfiler och sedan på Exportera. Öppna den exporterade filen config.xml och redigera följande rader:

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

Spara och importera sedan filen config.xml tillbaka till administrationskonsolen.

**Tidsgräns för programserversession:** Det här värdet kan anges på programservern. Mer information finns i dokumentationen som medföljer programservern.
