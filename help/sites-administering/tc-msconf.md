---
title: Ansluta till Microsoft Translator
seo-title: Connecting to Microsoft Translator
description: Lär dig hur du ansluter AEM till Microsoft Translator.
seo-description: Learn how to connect AEM to Microsoft Translator.
uuid: 5e3916ec-36a0-4d31-94ff-c340a462411a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: a7958411-b509-428e-bbe2-42efe8fd1add
feature: Language Copy
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---

# Ansluta till Microsoft Translator{#connecting-to-microsoft-translator}

Skapa en konfiguration för molntjänsten Microsoft Translator så att du kan använda ditt Microsoft Translation-konto för att översätta AEM sidinnehåll, communityinnehåll eller resurser.

| Egenskap | Beskrivning |
|---|---|
| Översättningsetikett | Översättningstjänstens visningsnamn. |
| Översättningsattribut | (Valfritt) För användargenererat innehåll visas den attribuering som visas bredvid översatt text, till exempel `Translations by Microsoft`. |
| ID för arbetsyta | (Valfritt) ID:t för den anpassade Microsoft Translator-motorn som ska användas. |
| Prenumerationsnyckel | Din Microsoft-prenumerationsnyckel för Microsoft Translator. |

När du har skapat konfigurationen måste du [aktivera den](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations).

Följande procedur använder det pekoptimerade användargränssnittet för att skapa en Microsoft Translator-konfiguration.

1. Klicka på eller tryck på Verktyg > Cloud Services på listen.
1. Klicka eller tryck på Visa konfigurationer i området Microsoft Translator.
1. Klicka på länken + bredvid Tillgängliga konfigurationer.

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. Ange en rubrik för konfigurationen. Titeln identifierar konfigurationen i konsolen Cloud Services samt i listrutor för sidegenskaper. Standardnamnet baseras på titeln. Du kan också ange ett namn som ska användas för databasnoden som lagrar konfigurationen. Du bör använda standardvärdet för egenskapen Överordnad konfiguration, som är sökvägen till databasnoden.
1. Klicka på Skapa.
1. I dialogrutan som visas skriver du värden för egenskaperna och klickar sedan på OK.

## Exempel på Microsoft Translator Cloud Service Configurations {#sample-microsoft-translator-cloud-service-configurations}

Följande molntjänstkonfigurationer för Microsoft Translator installeras tillsammans med Geometrixx. I vissa exempelkonfigurationer används ett Microsoft Translation-konto som kan användas för högst 2 000 000 kostnadsfria översatta tecken per månad.

### Microsoft Translator Trial License {#microsoft-translator-trial-license}

Microsoft Translator Trial License-konfigurationen är en exempelkonfiguration som installeras med exempelpaketet för Geometrixx Outdoors. Den här konfigurationen använder ett Microsoft Translator-konto med en kostnadsfri prenumeration som tillåter 2 000 000 översatta tecken per månad.

### Microsoft Translator Trial License - utomhuslicens för Geometrixx {#microsoft-translator-trial-license-geometrixx-outdoors}

Microsoft Translator Trial License - konfiguration utomhus för Geometrixx är en exempelkonfiguration som installeras med Geometrixx Outdoors. Den här konfigurationen använder samma kostnadsfria Microsoft Translator-konto som Microsoft Translator Trial License-konfigurationen. Kontot har en kostnadsfri prenumeration som tillåter 2 000 000 översatta tecken per månad.

Denna Microsoft Translator-konfiguration är optimerad för användning med den typ av innehåll som finns på exempelwebbplatsen för Geometrixx Outdoors.

### Uppgraderar Microsoft Translator Trial License Configuration {#upgrading-the-microsoft-translator-trial-license-configuration}

Konfigurationssidorna för Microsoft Translation är en praktisk länk till Microsoft webbplats där man kan få en kontoprenumeration som passar för produktionssystem.

1. Klicka på eller tryck på Verktyg > Åtgärder > Moln > Cloud Services.
1. Klicka eller tryck på Show Configurations (Visa konfigurationer) i området Microsoft Translator och klicka eller tryck sedan på Microsoft Translator Trial License (Microsoft Translation Configuration).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. Klicka på Uppgradera prenumeration på konfigurationssidan. Använd Microsoft webbsida som öppnas för att konfigurera ditt konto.

   ![chlimage_1-384](assets/chlimage_1-384.png)

### Anpassa Microsoft Translator Engine {#customizing-your-microsoft-translator-engine}

Konfigurationssidorna för Microsoft Translation är en praktisk länk till Microsoft webbplats där du kan anpassa Microsoft Translator-motorn. ([https://hub.microsofttranslator.com](https://hub.microsofttranslator.com/))

1. Klicka på eller tryck på Verktyg > Åtgärder > Moln > Cloud Services.
1. Klicka eller tryck på Show Configurations (Visa konfigurationer) i området Microsoft Translator och klicka eller tryck sedan på den konfiguration som du vill anpassa.
1. På konfigurationssidan klickar du på Anpassa översättare. Använd Microsoft webbsida som öppnas för att anpassa tjänsten.

## Aktivera tjänstkonfigurationer för översättare {#activating-the-translator-service-configurations}

Du måste aktivera dina molntjänstkonfigurationer för att stödja översatt innehåll som replikeras till publiceringsinstansen. Använd metoden [aktivera ett fullständigt avsnitt (träd)](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree) om du vill aktivera databasnoder som lagrar Microsoft Translator eller molntjänstkonfigurationer från tredje part. Noderna finns under följande överordnade noder:

* Microsoft Translation Service: /libs/settings/cloudconfigs/translation/msft-translation
* Översättning från tredje part: /etc/cloudservices/machine-translation
