---
title: Startar och stoppar WebSphere Application Server
seo-title: Startar och stoppar WebSphere Application Server
description: Flera procedurer kräver att du stoppar eller startar instansen av WebSphere där du vill distribuera AEM formulärprodukter. I det här dokumentet beskrivs hur du startar och stoppar WebSphere Application Server.
seo-description: Flera procedurer kräver att du stoppar eller startar instansen av WebSphere där du vill distribuera AEM formulärprodukter. I det här dokumentet beskrivs hur du startar och stoppar WebSphere Application Server.
uuid: e0373197-aa57-4087-933d-92a86840a11a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: bcd16691-67ab-4694-9e6b-c9d3e0c7bf0b
translation-type: tm+mt
source-git-commit: 67ea825215d1ca7cc2e350ed1c128c3146de45ec
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---


# Startar och stoppar WebSphere Application Server {#starting-and-stopping-websphere-application-server}

Flera procedurer kräver att du stoppar eller startar instansen av WebSphere där du vill distribuera AEM formulärprodukter. Om du är osäker på om programservern har startats kan du först visa statusen för WebSphere Application Server.

## Visa status för WebSphere-programservern {#view-the-status-of-websphere-application-server}

1. Gå till katalogen `[appserver root]/bin` från en kommandotolk.
1. Ange följande kommando och ersätt *server_name* med namnet på WebSphere-programservern:

   * (Windows) `serverStatus.bat`*server_name*
   * (Linux, UNIX) ./ `serverStatus.sh`*servernamn*

## Starta WebSphere-programservern {#start-websphere-application-server}

1. Gå till katalogen `[appserver root]/bin` från en kommandotolk.
1. Ange följande kommando och ersätt *server_name* med namnet på WebSphere-programservern:

   * (Windows) `startServer.bat`*server_name*
   * (Linux, UNIX) ./ `startServer.sh`*servernamn*

## Stoppa WebSphere-programservern {#stop-websphere-application-server}

1. Gå till katalogen `[appserver root]/bin` från en kommandotolk.
1. Ange följande kommando och ersätt *server_name* med namnet på WebSphere-programservern:

   * (Windows) `stopServer.bat`*server_name*
   * (Linux, UNIX) ./ `stopServer.sh`*servernamn*

