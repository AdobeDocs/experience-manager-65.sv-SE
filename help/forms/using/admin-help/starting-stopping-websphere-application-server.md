---
title: Startar och stoppar WebSphere Application Server
description: Flera procedurer kräver att du stoppar eller startar instansen av WebSphere där du vill distribuera AEM formulärprodukter. I det här dokumentet beskrivs hur du startar och stoppar WebSphere Application Server.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1a4e8f20-0644-4c96-9f52-f7a59521eac9
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '180'
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
