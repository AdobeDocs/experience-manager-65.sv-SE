---
title: "Korrespondenshantering: felsökning"
description: Lär dig hur du hanterar fel som uppstår när du sparar ett brev i en AEM Forms-miljö.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: cf06796b-bb8c-4a65-8f42-02fb0cfa3ebd
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
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
1. Välj **Correspondence Management Configurations**.
1. I **Correspondence Management Configurations** inaktiverar du **Aktivera bokstavscache** och klickar sedan på **Spara.**
1. Markera **Aktivera bokstavscache** och klicka sedan på **Spara**.
1. Försök att visa brevet igen.
