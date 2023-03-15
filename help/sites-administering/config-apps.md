---
title: Konfigurera för AEM program
seo-title: Configuring for AEM Apps
description: Lär dig hur du konfigurerar AEM.
seo-description: Learn how to configure AEM Apps.
uuid: ab9acd93-da7f-4bb7-8d26-224044899068
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 34f24837-f5e2-41f0-a359-fdb695e1b8f2
exl-id: f7aa5ac0-3d03-4c04-b9c2-1bda427b0588
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Konfigurera för AEM program{#configuring-for-aem-apps}

Med Adobe Experience Manager Apps kan du uppdatera innehållet i programmet direkt (OTA). Det uppdaterade innehållet lagras på publiceringsinstansen. Om du vill att appen på enheten ska kunna ansluta till publiceringsinstansen och söka efter uppdateringar måste publiceringsinstansen konfigureras så att en tom referensrubrik tillåts.

## Konfigurerar tomt referenshuvud {#configuring-empty-referrer-header}

Så här konfigurerar du referenspunktsfiltertjänsten:

* Öppna Apache Felix-konsolen (**Konfigurationer**) på:
* https://&lt;server>:&lt;port_number>/system/console/configMgr
* Logga in som administratör.
* I **Konfigurationer** väljer du: *Apache Sling Referer-filter*
* Markera fältet Tillåt tomt om du vill tillåta tomma/saknade hänvisningsrubriker.
* Klicka **Spara** för att spara ändringarna.

![chlimage_1-58](assets/chlimage_1-58a.png)

Se [OSGI-konfigurationsinställningar](/help/sites-deploying/osgi-configuration-settings.md) och [Säkerhetschecklista - Problem med förfalska begäran mellan webbplatser](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) för mer information.
