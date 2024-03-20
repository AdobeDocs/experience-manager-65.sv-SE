---
title: "Korrespondenshantering: felsökning"
description: Lär dig hur du hanterar fel som uppstår när du sparar ett brev i en AEM Forms-miljö.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: cf06796b-bb8c-4a65-8f42-02fb0cfa3ebd
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Korrespondenshantering: Felsökning {#correspondence-management-troubleshooting}

## Fel när en bokstav sparades {#errors-when-saving-a-letter}

### Problem {#issue}

Ett av följande fel visas när en bokstav sparas:

* Det finns ingen databindning för textmodulen
* Ange den egenskapsinformation som krävs för följande

### Orsak {#reason}

Felen kan bero på något av följande:

* En dataordlista är bunden till bokstaven men finns inte på servern.
* En dataordlista är bunden till bokstaven men har ett understreck (_) i namnet.

### Tillfällig lösning {#workaround}

Kontrollera att det datalexikon som du använder i brevet finns på servern och inte har något understreck (_) i namnet.

## Fel vid förhandsgranskning av brev {#error-when-previewing-a-letter}

### Problem {#issue-1}

När du förhandsgranskar en bokstav visas felet&quot;Fel vid inläsning av bokstav: Det gick inte att importera resurs från XML-indata&quot; även när en tidigare opublicerad textresurs i bokstaven publiceras.

### Tillfällig lösning {#workaround-1}

Återställ bokstavscachen för publiceringsinstansen genom att följa följande steg och försök sedan visa brevet igen:

1. Gå till **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** och logga in som administratör.
1. Välj **Konfigurationer för korrespondenshantering**.
1. I **Konfigurationer för korrespondenshantering**, inaktivera **Aktivera bokstavscache** och sedan klicka **Spara.**
1. Kontrollera **Aktivera bokstavscache** och sedan klicka **Spara**.
1. Försök att visa brevet igen.
