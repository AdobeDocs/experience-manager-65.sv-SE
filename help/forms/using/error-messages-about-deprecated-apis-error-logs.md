---
title: Felmeddelanden om inaktuella API:er i felloggar
description: Felmeddelanden om inaktuella API:er i felloggar
source-git-commit: b05666883645ca11784292e4bfb5bf9c1e35a43b
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 1%

---


# Felmeddelanden om inaktuella API:er i felloggar {#error-messages-about-deprecated-apis-in-error-logs}

Problemet gäller följande versioner:

* Experience Manager 6.5 Forms

## Problem {#issue}

* Följande felmeddelanden visas i error.log-filen:
  ` *WARN* [default task-36] org.apache.jackrabbit.oak.spi.security.principal.AclGroupDeprecation use of deprecated java.acl.Group-related API - this method is going to be removed in future Oak releases - see OAK-7358 for details` (NPR-38282)

## Upplösning {#workaround}

1. Installera [Experience Manager Forms Service Pack 13 eller senare (6.5.13.0 eller senare)](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html)
1. Använd följande länk för att hämta paket (.jar-fil med upplösning) från Software Distribution:

   https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[..]pack/com.adobe.livecycle.dsc.externalloginmodule-4.0.8.jar

1. Öppna Konfigurationshanteraren i Experience Manager och installera den hämtade filen com.adobe.livecycle.dsc.externalloginmodule-4.0.8.jar.

Problemet är löst.