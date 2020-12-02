---
title: '"Korrespondenshantering: Felsökning"'
seo-title: Felsökning av korrespondenshantering
description: Felsökning av korrespondenshantering
seo-description: Felsökning av korrespondenshantering
uuid: 25828cdd-110e-4a84-8f31-d82cd610a54f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: cc473808-e71a-4834-bb30-91e6df783e60
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# Korrespondenshantering: Felsökning {#correspondence-management-troubleshooting}

## Fel när en bokstav {#errors-when-saving-a-letter} sparades

### Utgåva {#issue}

Ett av följande fel visas när en bokstav sparas:

* Det finns ingen databindning för textmodulen
* Ange den egenskapsinformation som krävs för följande

### Orsak {#reason}

Felen kan bero på något av följande:

* En dataordlista är bunden till bokstaven men finns inte på servern.
* En dataordlista är bunden till bokstaven men har ett understreck (_) i namnet.

### Tillfällig lösning {#workaround}

Kontrollera att det datalexikon som du använder i brevet finns på servern och inte har något understreck (_) i namnet.

## Fel vid förhandsgranskning av en bokstav {#error-when-previewing-a-letter}

### Utgåva {#issue-1}

Felet&quot;Fel vid inläsning av brev: Det gick inte att importera resursen från XML-indata&quot; visas även när en tidigare opublicerad textresurs i bokstaven publiceras.

### Tillfällig lösning {#workaround-1}

Återställ bokstavscachen för publiceringsinstansen genom att följa följande steg och försök sedan visa brevet igen:

1. Gå till **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** och logga in som administratör.
1. Välj **Correspondence Management Configurations**.
1. I **Correspondence Management Configurations** inaktiverar du **Aktivera bokstavscache** och klickar sedan på&#x200B;**Spara.**
1. Aktivera **Aktivera bokstavscache** och klicka sedan på **Spara**.
1. Försök visa brevet igen.

