---
title: EAR-distribution misslyckades på JEE WebLogic-server
seo-title: EAR Deployment failing on JEE Weblogic Server
description: Steg för att åtgärda problem med EAR-driftsättning på JEE WebLogic-server
seo-description: Steps to resolve EAR Deployment failing on JEE Weblogic Server
source-git-commit: 45bb54a2666c2c196a8fb52795a7f428aa751e4d
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 2%

---


# EAR-driftsättning misslyckas på JEE WebLogic-server {#ear-deployment-failing-on-jee-weblogic-server}

## Problem {#issue}

När en användare försöker distribuera `adobe-livecycle-weblogic.ear`, `Null Pointer` undantag påträffades.

## Gäller för {#applies-to}

Denna lösning gäller

* AEM Forms på WebLogic JEE-server version 12.2.1.x.

## Lösning {#solution}

Så här löser du problemet:

1. Gå till `<domain_home>\bin` katalog för den installerade WebLogic JEE-servern.

1. Redigera `setDomainEnv.cmd` eller `setDomainEnv.sh` fil, som `applicable`.

1. Sök efter den sista förekomsten av `JAVA_OPTS` och lägga till `-DANTLR_USE_DIRECT_CLASS_LOADING=true` till den. Den uppdaterade strängen visas till exempel som:

       set`JAVA_OPTIONS=%JAVA_OPTIONS% -DANTLR_USE_DIRECT_CLASS_LOADING=true`
   
1. Spara ändringarna.


