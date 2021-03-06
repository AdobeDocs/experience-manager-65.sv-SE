---
title: Namnkonventioner
seo-title: Namnkonventioner
description: Noderna i databasen omfattas av namnkonventioner i Java Content Repository
seo-description: Noderna i databasen omfattas av namnkonventioner i Java Content Repository
uuid: 0515c5c5-3e93-4710-983f-c08c146467fc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 198098c0-432b-4a93-a94e-2552337435dd
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# Namnkonventioner{#naming-conventions}

Noderna i databasen omfattas av namnkonventioner i [Java Content Repository](/help/sites-developing/the-basics.md#java-content-repository). AEM lägger dock till ytterligare konventioner för sidnodernas namn.

## Namngivningskonventioner för sidor {#naming-conventions-for-pages}

Dessa namnkonventioner implementeras på olika nivåer:

* JcrUtil: den AEM implementeringen av [JCR-verktygen](#jcr-utilities).
* PageManager: [Sidhanteraren](#page-manager) innehåller metoder för åtgärder på sidnivå.
* Enligt det användargränssnitt som används:

   * [Pekaktiverat användargränssnitt som standard](#standard-ui)
   * [Klassiskt användargränssnitt](#classic-ui)

### JCR-verktyg {#jcr-utilities}

[JCR](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) använder den AEM implementeringen av JCR-verktygen. Det är särskilt intressant att validera namn om du kontrollerar teckenmappningar och följande valideringar:

* `isValidName`

   * Kontrollerar om namnet inte är tomt och bara innehåller giltiga tecken.
   * Kan användas för att kontrollera om ett föreslaget namn är giltigt.

* `createValidName`

   * Detta skapar en giltig etikett av en godtycklig sträng.
   * Den kan användas för att skapa ett namn från en titel.

### Sidhanteraren {#page-manager}

[I ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) PageManager finns metoder för sidnivååtgärder som baseras på  [JCRUtil](#jcr-utilities).

### Standardgränssnitt {#standard-ui}

Standardgränssnittet med pekskärm:

* Validerar namnet enligt de begränsningar som PageManager har när något av följande inträffar:

   * en sidrubrik tillhandahålls för konvertering till nodnamnet
   * ett explicit nodnamn anges

### Klassiskt gränssnitt {#classic-ui}

Det klassiska användargränssnittet har tätare begränsningar:

* Validerar namnet när ett explicit nodnamn är:

   * en sidrubrik tillhandahålls för konvertering till nodnamnet
   * ett explicit nodnamn anges

* Giltiga tecken (endast dessa tecken är giltiga när en sida skapas i det klassiska användargränssnittet, även om `PageManagerImpl` tillåter ytterligare tecken):

   * &#39;a&#39; till &#39;z&#39;
   * &#39;A&#39; till &#39;Z&#39;
   * 0 till 9
   * _ (understreck)
   * `-` (tankstreck/minustecken)

