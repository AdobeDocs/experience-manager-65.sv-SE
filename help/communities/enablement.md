---
title: Konfigurera aktiveringsfunktioner
seo-title: Konfigurera aktiveringsfunktioner
description: Konfigurera aktiveringsfunktioner i Communities
seo-description: Konfigurera aktiveringsfunktioner i Communities
uuid: 27be3128-1a7d-412e-99a9-6e3b3b0aec1c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 765a3d9b-4552-403e-872c-fdf684ac271d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Konfigurera aktiveringsfunktioner {#configuring-enablement-features}

## Översikt {#overview}

Med aktiveringsfunktionerna kan du skapa [aktiveringscommunityn](overview.md#enablement-community).

* Den här funktionen kräver ytterligare licensiering för användning i en produktionsmiljö.

Användning av aktiveringsfunktionerna kräver följande:

Installation av:

* **SCORM** Sharable Content Object Reference Model (SCORM) är en samling standarder och specifikationer för e-learning. SCORM definierar också hur innehåll kan paketeras i en överförbar ZIP-fil.

* **MySQL** MySQL är en relationsdatabas som i första hand används för SCORM-spårning och för att rapportera data för aktivering, samt tabeller för att spåra videoförloppet. SCORM för aktiveringsfunktionspaketet kräver JDBC-drivrutinen MySQL.

* **FFmpeg** FFmpeg är en lösning för konvertering och direktuppspelning av ljud och video. När den är installerad används den för korrekt omkodning av [videomaterial](../../help/sites-authoring/default-components-foundation.md#video). För aktiveringscommunityn används den i redigeringsmiljön för att hämta metadata för överförda resurser och generera en miniatyrbild som visas när resursen listas.

Inställningar för:

* **Community Managers** för aktiveringsgrupper: Endast medlemmar i `Community Enablement Managers` användargruppen kan tilldelas rollen `*Community Site* Enablement Manager`vars behörigheter kan omfatta innehållsskapande, uppdrag och medlemshantering i publiceringsmiljön.

Valfri konfiguration av:

* **Adobe Analytics**-integrering med Adobe Analytics ger omfattande rapporteringsfunktioner och stöder tillägget Video Heartbeat i Analytics.

* **Dispatcher**

## Konfigurationssteg {#configuration-steps}

Följande steg är nödvändiga för aktiveringscommunityn.

Varje steg länkar till dokumentation med nödvändig information.

**På alla författar-/publiceringsinstanser:**

1. **[installera JDBC-drivrutin för MySQL](deploy-communities.md#jdbc-driver-for-mysql)**Use Web Console (paket):*http://localhost:4502/system/console/bundles*Installera *innan*du installerar SCORM-paketet

1. **[installera SCORM-paketet](deploy-communities.md#scorm-package)**Använd pakethanteraren:*http://localhost:4502/crx/packmgr/*

**På alla servrar:**

1. **[installera MySQL, MySQL Workbench](mysql.md)**

1. **[installera MySQL-databaser](mysql.md#database-setup)**Kör SQL-skript som hämtats från författarinstansenAnvänd MySQL Workbench

**På samma server som är värd för författarinstans:**

1. **[installera FFmpeg](ffmpeg.md)**

**På alla författar-/publiceringsinstanser:**

1. **[konfigurera poolen](mysql.md#configure-jdbc-connections)**JDBC-anslutningar med webbkonsolen (configMgr):*http://localhost:4502/system/console/configMgr*

1. **[konfigurera SCORM-motortjänsten](mysql.md#aem-communities-scormengine-service)**Använd webbkonsol (configMgr):*http://localhost:4502/system/console/configMgr*

1. **[konfigurera CSRF-filter](mysql.md#adobe-granite-csrf-filter)**Använd webbkonsol (configMgr):*http://localhost:4502/system/console/configMgr*

**On author instance:**

1. (*valfritt*) **[konfigurera tjänsten](analytics.md)**Analytics med konsolen Verktyg, Distribution och Cloud Services:*http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[konfigurera konsolen](ffmpeg.md#configure-ffmpeg-transcoding-service)**Använd arbetsflöde/modeller för FFmpeg

1. **[aktivera tunneltjänsten](deploy-communities.md#tunnel-service-on-author)**Använd webbkonsol (configMgr):*http://localhost:4502/system/console/configMgr*

1. **[skapa Community-administratörer](users.md#creating-community-members)**I författarmiljön använder du Classic-UI Security console:*http://localhost:4502/useradmin*skapa användare med sökväg = /home/users/community

   * Lägg till medlemmar i följande grupper:

      * Community Enablement Managers
      * Communities-administratörer

## Dispatcher {#dispatcher}

När distributionen innehåller [AEM&#39;s Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)måste `clientheader``filter`avsnitten ändras för att aktiveringsfunktionerna ska fungera korrekt. Se [Konfigurera Dispatcher för Communities](dispatcher.md#enablement).
