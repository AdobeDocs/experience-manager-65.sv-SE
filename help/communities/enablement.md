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
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# Konfigurera aktiveringsfunktioner {#configuring-enablement-features}

## Översikt {#overview}

Med aktiveringsfunktionerna kan du skapa [aktiveringscommunityn](overview.md#enablement-community).

* Den här funktionen kräver ytterligare licensiering för användning i en produktionsmiljö.

Användning av aktiveringsfunktionerna kräver följande:

Installation av:

* **SCORM**

   SCORM (Sharable Content Object Reference Model) är en samling standarder och specifikationer för e-learning. SCORM definierar också hur innehåll kan paketeras i en överförbar ZIP-fil.

* **MySQL**

   MySQL är en relationsdatabas som i första hand används för SCORM-spårning och rapportdata för aktivering, samt för tabeller för att spåra videoförloppet. SCORM för aktiveringsfunktionspaketet kräver JDBC-drivrutinen MySQL.

* **FFmpeg**

   FFmpeg är en lösning för konvertering och direktuppspelning av ljud och video och används, när den är installerad, för korrekt omkodning av [videoresurser](../../help/sites-authoring/default-components-foundation.md#video). För aktiveringscommunityn används den i redigeringsmiljön för att hämta metadata för överförda resurser och generera en miniatyrbild som visas när resursen listas.

Inställningar för:

* **Community Managers**

   För aktiveringsgrupper kan endast medlemmar i `Community Enablement Managers` användargruppen tilldelas rollen `Community Site Enablement Manager`vars behörigheter kan omfatta innehållsskapande, uppdrag och medlemshantering i publiceringsmiljön.

Valfri konfiguration av:

* **Adobe Analytics**

   Integrationen med Adobe Analytics ger omfattande rapportfunktioner och stöder tillägget Video Heartbeat i Analytics.

* **Dispatcher**

## Konfigurationssteg {#configuration-steps}

Följande steg är nödvändiga för aktiveringscommunityn.

Varje steg länkar till dokumentation med nödvändig information.

**På alla författar-/publiceringsinstanser:**

1. **[Installera JDBC-drivrutin för MySQL](deploy-communities.md#jdbc-driver-for-mysql)**

   Använd webbkonsol (paket): *http://localhost:4502/system/console/bundles* Installera *innan* du installerar SCORM-paketet

1. **[Installera SCORM-paketet](deploy-communities.md#scorm-package)**Använd pakethanteraren:*http://localhost:4502/crx/packmgr/*

**På alla servrar:**

1. **[Installera MySQL, MySQL Workbench](mysql.md)**

1. **[Installera MySQL-databaser](mysql.md#database-setup)**

   Kör SQL-skript som hämtats från författarinstansenAnvänd MySQL Workbench

**På samma server som är värd för författarinstans:**

1. **[Installera FFmpeg](ffmpeg.md)**

**På alla författar-/publiceringsinstanser:**

1. **[Konfigurera JDBC-anslutningspool](mysql.md#configure-jdbc-connections)**

   Använd webbkonsol (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Konfigurera SCORM-motortjänsten](mysql.md#aem-communities-scormengine-service)**

   Använd webbkonsol (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Konfigurera CSRF-filter](mysql.md#adobe-granite-csrf-filter)**

   Använd webbkonsol (configMgr): *http://localhost:4502/system/console/configMgr*

**On author instance:**

1. (*Valfritt*) **[Konfigurera analystjänsten](analytics.md)**

   Använd verktygs-, distributions- och molntjänstkonsolen: *http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[Konfigurera FFmpeg](ffmpeg.md#configure-ffmpeg-transcoding-service)**

   Använd konsolen Arbetsflöde/Modeller

1. **[Aktivera tunneltjänsten](deploy-communities.md#tunnel-service-on-author)**

   Använd webbkonsol (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Skapa communityadministratörer](users.md#creating-community-members)**

   I författarmiljön använder du Classic-UI Security console: *http://localhost:4502/useradmin* skapa användare med sökväg = /home/users/community

   * Lägg till medlemmar i följande grupper:

      * Community Enablement Managers
      * Communities-administratörer

## Dispatcher {#dispatcher}

När distributionen inkluderar [AEM&#39;s Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)måste avsnitten `clientheader` och `filter` ändras för att aktiveringsfunktionerna ska fungera korrekt. Se [Konfigurera Dispatcher för Communities](dispatcher.md#enablement).
