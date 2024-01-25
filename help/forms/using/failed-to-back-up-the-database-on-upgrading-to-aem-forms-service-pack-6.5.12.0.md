---
title: Det gick inte att säkerhetskopiera den tidigare databasen på AEM Forms 6.5.12.0.
description: När en användare uppgraderar till Experience Manager 6.5.12.0 och klickar på "Uppgradera MySQL" kan konfigurationshanteraren inte säkerhetskopiera den tidigare Experience Manager Forms-databasen.
source-git-commit: d232bfdad7b8413eb015f6fe5dd3442cebf1001d
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# Problem (#issue)

När en användare uppgraderar till Experience Manager 6.5.12.0 och klickar på &quot;Uppgradera MySQL&quot; kan konfigurationshanteraren inte säkerhetskopiera den tidigare Experience Manager Forms-databasen. Felet visas:

`Failed to backup the previous Adobe Experience Manager Forms Database`


## Gäller för {#applies-to}

* Experience Manager 6.5 Forms

## Lösning {#solution}

Lös problemet genom att öka databasens max_packet_size till 100 M eller så som krävs i filen my.ini som finns på {AEM_HOME}/mysql.
