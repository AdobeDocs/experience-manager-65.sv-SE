---
title: Konfigurera för AEM program
seo-title: Konfigurera för AEM program
description: Lär dig hur du konfigurerar AEM.
seo-description: Lär dig hur du konfigurerar AEM.
uuid: ab9acd93-da7f-4bb7-8d26-224044899068
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 34f24837-f5e2-41f0-a359-fdb695e1b8f2
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# Konfigurera för AEM program{#configuring-for-aem-apps}

Med Adobe Experience Manager Apps kan du uppdatera innehållet i programmet direkt (OTA). Det uppdaterade innehållet lagras på publiceringsinstansen. Om du vill att appen på enheten ska kunna ansluta till publiceringsinstansen och söka efter uppdateringar måste publiceringsinstansen konfigureras så att en tom referensrubrik tillåts.

## Konfigurerar tomt referenshuvud {#configuring-empty-referrer-header}

Så här konfigurerar du referenspunktsfiltertjänsten:

* Öppna Apache Felix-konsolen (**Configurations**) på:
* https://&lt;server>:&lt;portnummer>/system/console/configMgr
* Logga in som administratör.
* Välj: **Referensfilter för Apache Sling****
* Markera fältet Tillåt tomt om du vill tillåta tomma/saknade hänvisningsrubriker.
* Klicka på **Spara** för att spara ändringarna.

![chlimage_1-58](assets/chlimage_1-58a.png)

Mer information finns i [OSGI Configuration Settings](/help/sites-deploying/osgi-configuration-settings.md) och [Security Checklist - Issues with Cross-Site Request Forgery](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery).
