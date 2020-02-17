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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Korrespondenshantering:Felsökning {#correspondence-management-troubleshooting}

## Fel när en bokstav sparades {#errors-when-saving-a-letter}

### Problem {#issue}

Ett av följande fel visas när en bokstav sparas:

* Det finns ingen databindning för textmodulen
* Ange den egenskapsinformation som krävs för följande

### Reason {#reason}

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

1. Gå till **`https://[server]:[port]/[contextPath]/system/console/configMgr`** och logga in som administratör.
1. Välj **Korrespondenshanteringskonfigurationer**.
1. I **Correspondence Management Configurations** inaktiverar du **Enable Letter Cache** och klickar sedan på&#x200B;**Save.**
1. Aktivera **Aktivera cacheminne** för brev och klicka sedan på **Spara**.
1. Försök visa brevet igen.

