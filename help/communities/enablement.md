---
title: Konfigurera aktiveringsfunktioner
seo-title: Configuring Enablement Features
description: Konfigurera aktiveringsfunktioner i Communities
seo-description: Configure enablement features in Communities
uuid: 27be3128-1a7d-412e-99a9-6e3b3b0aec1c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 765a3d9b-4552-403e-872c-fdf684ac271d
role: Admin
exl-id: b635e2ed-4637-4b2f-a746-ec8dc7541bab
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

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

   FFmpeg är en lösning för konvertering och direktuppspelning av ljud och video och används, när den är installerad, för korrekt transkodning av [Videoresurser](../../help/sites-authoring/default-components-foundation.md#video). För aktiveringscommunityn används den i redigeringsmiljön för att hämta metadata för överförda resurser och generera en miniatyrbild som visas när resursen listas.

Inställningar för:

* **Community Managers**

   Endast medlemmar i `Community Enablement Managers` användargruppen kan tilldelas rollen som `Community Site Enablement Manager`, vars behörigheter kan omfatta innehållsskapande, uppdrag och medlemshantering i publiceringsmiljön.

Valfri konfiguration av:

* **Adobe Analytics**

   Integrationen med Adobe Analytics ger omfattande rapportfunktioner och stöder tillägget Video Heartbeat i Analytics.

* **Dispatcher**

## Konfigurationssteg {#configuration-steps}

Följande steg är nödvändiga för aktiveringscommunityn.

Varje steg länkar till dokumentation med nödvändig information.

**På alla författar-/publiceringsinstanser:**

1. **[Installera JDBC-drivrutin för MySQL](deploy-communities.md#jdbc-driver-for-mysql)**

   Använd webbkonsol (paket): *http://localhost:4502/system/console/bundles*

   Installera *före* installera SCORM-paket

1. **[Installera SCORM-paket](deploy-communities.md#scorm-package)**


   Använd pakethanteraren: *http://localhost:4502/crx/packmgr/*

**På alla servrar:**

1. **[Installera MySQL, MySQL Workbench](mysql.md)**

1. **[Installera MySQL-databaser](mysql.md#database-setup)**

   Kör SQL-skript som hämtats från författarinstansen

   Använd MySQL Workbench

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

   Använd verktygs-, distributions- och Cloud Services-konsolen: *http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[Konfigurera FFmpeg](ffmpeg.md#configure-ffmpeg-transcoding-service)**

   Använd konsolen Arbetsflöde/Modeller

1. **[Aktivera tunneltjänsten](deploy-communities.md#tunnel-service-on-author)**

   Använd webbkonsol (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Skapa communityadministratörer](users.md#creating-community-members)**

   I författarmiljön använder du Classic-UI Security console: *http://localhost:4502/useradmin*

   Skapa användare med sökväg = /home/users/community

   * Lägg till medlemmar i följande grupper:

      * Community Enablement Managers
      * Communities-administratörer

## Dispatcher {#dispatcher}

När distributionen inkluderar [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)för att aktiveringsfunktionerna ska fungera på rätt sätt `clientheader` och `filter` -avsnitt behöver ändras. Se [Konfigurera Dispatcher för Communities](dispatcher.md#enablement).
