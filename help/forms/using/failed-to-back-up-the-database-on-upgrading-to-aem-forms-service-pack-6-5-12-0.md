---
title: Det gick inte att säkerhetskopiera databasen under uppgradering till 6.5.12.0 för MySQL.
description: När en användare uppgraderar till Experience Manager 6.5.12.0 och klickar på "Uppgradera MySQL" kan konfigurationshanteraren inte säkerhetskopiera den tidigare Experience Manager Forms-databasen.
exl-id: 1af000fa-439b-4ffd-8b5a-3ba45f0c524c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Troubleshooting
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Det gick inte att säkerhetskopiera databasen under uppgradering till 6.5.12.0 för MySQL {#issue}

När en användare uppgraderar till Experience Manager 6.5.12.0 och klickar på &quot;Uppgradera MySQL&quot; kan konfigurationshanteraren inte säkerhetskopiera den tidigare Experience Manager Forms-databasen. Felet visas:

`Failed to backup the previous Adobe Experience Manager Forms Database`


## Gäller för {#applies-to}

* Experience Manager 6.5 Forms

## Lösning {#solution}

Lös problemet genom att öka databasens max_packet_size till 100 M eller så som krävs i filen my.ini som finns på {AEM_HOME}/mysql.
