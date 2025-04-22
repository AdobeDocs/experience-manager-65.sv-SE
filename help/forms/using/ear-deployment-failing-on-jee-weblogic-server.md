---
title: EAR-distribution misslyckades på JEE WebLogic-server
seo-title: EAR Deployment failing on JEE Weblogic Server
description: Steg för att åtgärda problem med EAR-driftsättning på JEE WebLogic-server
source-git-commit: 05712cfcef1d9c37b7cd015133abaf6df0e351d2
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 3%

---


# EAR-driftsättning misslyckas på JEE WebLogic-server {#ear-deployment-failing-on-jee-weblogic-server}

## Problem {#issue}

När en användare försöker distribuera `adobe-livecycle-weblogic.ear` påträffas undantaget `Null Pointer` .

## Gäller för {#applies-to}

Denna lösning gäller

* AEM Forms på WebLogic JEE-server version 12.2.1.x.

## Lösning {#solution}

Så här löser du problemet:

1. Gå till katalogen `<domain_home>\bin` för den installerade WebLogic JEE-servern.

1. Redigera filen `setDomainEnv.cmd` eller `setDomainEnv.sh` som `applicable`.

1. Sök efter den sista förekomsten av `JAVA_OPTS` och lägg till `-DANTLR_USE_DIRECT_CLASS_LOADING=true` i den. Den uppdaterade strängen visas till exempel som:

       set`JAVA_OPTIONS=%JAVA_OPTIONS% -DANTLR_USE_DIRECT_CLASS_LOADING=true`
   
1. Spara ändringarna.
