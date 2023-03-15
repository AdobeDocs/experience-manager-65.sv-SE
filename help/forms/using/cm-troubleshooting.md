---
title: "Korrespondenshantering: Felsökning"
seo-title: Correspondence Management Troubleshooting
description: Felsökning av korrespondenshantering
seo-description: Correspondence Management Troubleshooting
uuid: 25828cdd-110e-4a84-8f31-d82cd610a54f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: cc473808-e71a-4834-bb30-91e6df783e60
feature: Correspondence Management
exl-id: cf06796b-bb8c-4a65-8f42-02fb0cfa3ebd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '199'
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

Felet&quot;Fel vid inläsning av brev: Det gick inte att importera resursen från XML-indata&quot; visas även när en tidigare opublicerad textresurs i bokstaven publiceras.

### Tillfällig lösning {#workaround-1}

Återställ bokstavscachen för publiceringsinstansen genom att följa följande steg och försök sedan visa brevet igen:

1. Gå till **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** och logga in som administratör.
1. Välj **Konfigurationer för korrespondenshantering**.
1. I **Konfigurationer för korrespondenshantering**, inaktivera **Aktivera bokstavscache** och sedan klicka **Spara.**
1. Aktivera **Aktivera bokstavscache** och sedan klicka **Spara**.
1. Försök visa brevet igen.
