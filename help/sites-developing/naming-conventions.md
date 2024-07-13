---
title: Namnkonventioner för noder i Java Content Repository
description: Noderna i databasen omfattas av namnkonventioner i Java Content Repository
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 01c6bb29-1d2d-4a45-b291-0e8d97c01a08
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# Namnkonventioner {#naming-conventions}

Noderna i databasen omfattas av namnkonventioner i [Java Content Repository](/help/sites-developing/the-basics.md#java-content-repository). AEM lägger dock till ytterligare konventioner för sidnodernas namn.

## Namnkonventioner för sidor {#naming-conventions-for-pages}

Dessa namnkonventioner implementeras på olika nivåer:

* JcrUtil: den AEM implementeringen av [JCR-verktygen](#jcr-utilities).
* PageManager: [Page Manager](#page-manager) innehåller metoder för sidnivååtgärder.
* Enligt det användargränssnitt som används:

   * [Pekaktiverat användargränssnitt som standard](#standard-ui)
   * [Klassiskt användargränssnitt](#classic-ui)

### JCR-verktyg {#jcr-utilities}

[JcrUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) är den AEM implementeringen av JCR-verktygen. Det är särskilt intressant att validera namn om du kontrollerar teckenmappningar och följande valideringar:

* `isValidName`

   * Kontrollerar om namnet inte är tomt och bara innehåller giltiga tecken.
   * Kan användas för att kontrollera om ett föreslaget namn är giltigt.

* `createValidName`

   * Detta skapar en giltig etikett av en godtycklig sträng.
   * Den kan användas för att skapa ett namn från en titel.

### Sidhanteraren {#page-manager}

[PageManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) innehåller metoder för sidnivååtgärder, baserade på [JCRUtil](#jcr-utilities).

### Standardgränssnitt {#standard-ui}

Standardgränssnittet med pekskärm:

* Validerar namnet enligt de begränsningar som PageManager har när något av följande inträffar:

   * en sidrubrik tillhandahålls för konvertering till nodnamnet
   * ett explicit nodnamn har angetts

### Klassiskt användargränssnitt {#classic-ui}

Det klassiska användargränssnittet har tätare begränsningar:

* Validerar namnet när ett explicit nodnamn är:

   * en sidrubrik tillhandahålls för konvertering till nodnamnet
   * ett explicit nodnamn har angetts

* Giltiga tecken (endast dessa tecken är giltiga när en sida skapas i det klassiska användargränssnittet, även om `PageManagerImpl` tillåter ytterligare tecken):

   * &#39;a&#39; till &#39;z&#39;
   * &#39;A&#39; till &#39;Z&#39;
   * 0 till 9
   * _ (understreck)
   * `-` (tankstreck/minustecken)
