---
title: Startar och stoppar WebSphere Application Server
seo-title: Starting and stopping WebSphere Application Server
description: Flera procedurer kräver att du stoppar eller startar instansen av WebSphere där du vill distribuera AEM formulärprodukter. I det här dokumentet beskrivs hur du startar och stoppar WebSphere Application Server.
seo-description: Several procedures require you to stop or start the instance of WebSphere where you want to deploy AEM forms products. This document describes how to start and stop the WebSphere Application Server.
uuid: e0373197-aa57-4087-933d-92a86840a11a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: bcd16691-67ab-4694-9e6b-c9d3e0c7bf0b
exl-id: 1a4e8f20-0644-4c96-9f52-f7a59521eac9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Startar och stoppar WebSphere Application Server {#starting-and-stopping-websphere-application-server}

Flera procedurer kräver att du stoppar eller startar instansen av WebSphere där du vill distribuera AEM formulärprodukter. Om du är osäker på om programservern har startats kan du först visa statusen för WebSphere Application Server.

## Visa status för WebSphere Application Server {#view-the-status-of-websphere-application-server}

1. Gå till `[appserver root]/bin` katalog.
1. Ange följande kommando och ersätt *server_name* med namnet på WebSphere Application Server:

   * (Windows) `serverStatus.bat`*server_name*
   * (Linux, UNIX) ./ `serverStatus.sh`*server_name*

## Starta WebSphere Application Server {#start-websphere-application-server}

1. Gå till `[appserver root]/bin` katalog.
1. Ange följande kommando och ersätt *server_name* med namnet på WebSphere Application Server:

   * (Windows) `startServer.bat`*server_name*
   * (Linux, UNIX) ./ `startServer.sh`*server_name*

## Stoppa WebSphere-programserver {#stop-websphere-application-server}

1. Gå till `[appserver root]/bin` katalog.
1. Ange följande kommando och ersätt *server_name* med namnet på WebSphere Application Server:

   * (Windows) `stopServer.bat`*server_name*
   * (Linux, UNIX) ./ `stopServer.sh`*server_name*
