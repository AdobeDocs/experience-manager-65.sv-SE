---
title: Namnkonventioner för tillgångstestning
seo-title: Namnkonventioner för resurser
description: Noderna i databasen omfattas av namnkonventioner i Java Content Repository. Adobe Experience Manager lägger dock till ytterligare konventioner för namnet på resursnoder.
seo-description: Noderna i databasen omfattas av namnkonventioner i Java Content Repository. Adobe Experience Manager lägger dock till ytterligare konventioner för namnet på resursnoder.
uuid: 6b622a60-90e8-461e-9b67-42c11c7038f9
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 55e66c66-0120-4ed4-94c5-d65a434bb59b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Namnkonventioner för tillgångstestning{#naming-conventions-for-assets-testing}

Noderna i databasen omfattas av namnkonventioner i [Java Content Repository](/help/sites-developing/the-basics.md#java-content-repository). Adobe Experience Manager lägger dock till ytterligare konventioner för namnet på resursnoder.

## Klassiskt användargränssnitt {#classic-ui}

Det klassiska användargränssnittet har tätare begränsningar:

* Validerar resursnamnet när ett explicit nodnamn är:

   * en resurstitel tillhandahålls för konvertering till nodnamnet
   * ett explicit nodnamn anges

* Giltiga tecken (endast dessa tecken är giltiga när en resurs skapas i det klassiska användargränssnittet):

   * &#39;a&#39; till &#39;z&#39;
   * &#39;A&#39; till &#39;Z&#39;
   * 0 till 9
   * _ (understreck)
   * `-` (tankstreck/minustecken)

