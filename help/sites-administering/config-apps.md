---
title: Konfigurera för AEM program
description: Lär dig hur du använder Adobe Experience Manager-appar för att uppdatera innehållet i OTA-programmet (i stället för AIR).
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: f7aa5ac0-3d03-4c04-b9c2-1bda427b0588
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 1%

---

# Konfigurera för AEM program{#configuring-for-aem-apps}

Med Adobe Experience Manager Apps kan du uppdatera innehållet i OTA-koden (i stället för AIR). Det uppdaterade innehållet lagras på publiceringsinstansen. Om du vill att appen på enheten ska kunna ansluta till publiceringsinstansen och söka efter uppdateringar, måste publiceringsinstansen konfigureras så att en tom referensrubrik tillåts.

## Konfigurerar tomt referenshuvud {#configuring-empty-referrer-header}

Så här konfigurerar du referenspunktsfiltertjänsten:

* Öppna Apache Felix-konsolen (**Konfigurationer**) på:
* https://&lt;server>:&lt;port_number>/system/console/configMgr
* Logga in som administratör.
* I **Konfigurationer** väljer du: *Apache Sling Referer-filter*
* Markera fältet Tillåt tomt så att du kan tillåta tomma/saknade hänvisningsrubriker.
* Klicka **Spara** för att spara ändringarna.

![chlimage_1-58](assets/chlimage_1-58a.png)

Se [OSGI-konfigurationsinställningar](/help/sites-deploying/osgi-configuration-settings.md) och [Säkerhetschecklista - Problem med förfalska begäran mellan webbplatser](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) för mer information.
