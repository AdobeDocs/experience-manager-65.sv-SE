---
title: EAR-distribution misslyckades på JEE WebLogic-server
description: Steg för att åtgärda problem med EAR-driftsättning på JEE WebLogic-server
exl-id: b87a9eee-ee56-4dca-b4a3-a42c91db0b4f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 3%

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
