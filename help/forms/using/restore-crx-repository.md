---
title: Det går inte att återställa en skadad CRX-databas som kan användas på JEE-klusterservern
description: Steg för att återställa skadad CRX-databas
source-git-commit: a7d125503b0bd3c52cb3a959e2f0dde1a69cbe2b
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# Det går inte att återställa en skadad CRX-databas {#unable-to-restore-corrupt-crx-repository}

## Problem {#issue}

För AEM Forms som körs på JEE med RDB-beständighet måste AEM Forms värddatorer och databasdatorer vara synkroniserade i absolut tid. Men om det av någon anledning inte längre finns någon synk möjlighet blir CRX-databasen skadad och URL:erna blir otillgängliga. Felet som `AuthenticationsupportService missing` inträffar i loggfiler.

## Lösning {#solution}

Utför följande steg för att lösa problemet:
1. Gå till  [https://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).

1. Leta reda på `oak-core` paketera och kontrollera om det körs.

1. Starta om `oak-core` paket om det inte körs. Om pausknappen finns framför `oak-core` paketet, då anger det att paketet körs.

1. Om problemet fortfarande inte är löst kan du återställa från CRX-databasen från säkerhetskopian eller återskapa CRX-databasen om det inte finns någon säkerhetskopia.

   >[!NOTE]
   >
   >Säkerhetskopiera din CRX-databas innan du utför ovanstående steg.

## Gäller för {#applies-to}

Denna lösning gäller

* AEM Forms på JEE Cluster Server


