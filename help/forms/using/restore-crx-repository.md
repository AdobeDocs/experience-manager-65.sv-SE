---
title: Det går inte att återställa en skadad CRX-databas som kan användas på JEE-klusterservern
description: Steg för att återställa skadad CRX-databas
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
source-git-commit: cf034e8765317ee022aad4693ced37c3fa793ff2
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# Det går inte att återställa en skadad CRX-databas {#unable-to-restore-corrupt-crx-repository}

## Problem {#issue}

För AEM Forms på JEE som använder en relationsdatabas ska tiden på den dator som är värd för AEM Forms och relationsdatabasen alltid vara i absolut synk. Om tiden på dessa datorer blir osynkroniserad kan AEM Forms CRX-databas på JEE-servern bli otillgänglig. Den kan vara skadad och oåtkomlig via URL. The `AuthenticationsupportService missing` fel loggas.

## Förutsättningar {#prerequisites}

Säkerhetskopiera din CRX-databas innan du utför stegen nedan.

## Lösning {#solution}

Utför följande steg för att lösa problemet:
1. Gå till  `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. Leta reda på `oak-core` paketera och kontrollera om det körs.

1. Starta om `oak-core` paket om det inte körs. If  ![Pausa](/help/forms/using/assets/stop.png) ikonen visas framför `oak-core` paketet, och då anger det att paketet körs.

1. Om problemet fortfarande inte är löst kan du återställa från CRX-databasen från säkerhetskopian eller återskapa CRX-databasen om det inte finns någon säkerhetskopia.


## Gäller för {#applies-to}

Denna lösning gäller

* AEM Forms i JEE-klustermiljö