---
title: Arbeta med loggar
seo-title: Arbeta med loggar
description: Lär dig hur du felsöker AEM genom att arbeta med loggar.
seo-description: Lär dig hur du felsöker AEM genom att arbeta med loggar.
uuid: af8b7f50-c8d4-4760-9f00-3feb0b79ee4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: da92d751-6f14-4512-9d77-7ecf098bd58e
docset: aem65
translation-type: tm+mt
source-git-commit: 8b53e79e3a88f58423e99477db930a4912a1ba09

---


# Arbeta med loggar{#working-with-logs}

I det här avsnittet finns detaljerad information om loggar som du kan använda för att felsöka.

CRX registrerar detaljerade loggar. När du har packat upp och startat Quickstart finns loggarna på följande platser:

* crx-quickstart/launchpad/logs
* crx-quickstart/server/logs
* crx-quickstart/logs

## Aktivera felsökningsloggnivån {#activating-the-debug-log-level}

Standardloggnivån är INFO, d.v.s. DEBUG-meddelanden loggas inte.

Om du vill aktivera DEBUG-loggnivån använder du CRX-utforskaren för att ange

```xml
/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level
```

egenskap som ska felsökas. Lämna inte loggen på DEBUG-loggnivån längre än nödvändigt eftersom den genererar många loggar.

En rad i felsökningsfilen börjar oftast med DEBUG och anger sedan loggnivån, installationsåtgärden och loggmeddelandet. Exempel:

```xml
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

Loggnivåerna är följande:

| 0 | Allvarligt fel | Åtgärden misslyckades och installationsprogrammet kan inte fortsätta. |
|---|---|---|
| 1 | Fel | Åtgärden misslyckades. Installationen fortsätter, men en del av CRX installerades inte korrekt och kommer inte att fungera. |
| 2 | Varning | Åtgärden har slutförts men problem uppstod. CRX fungerar eventuellt inte korrekt. |
| 3 |  Information | Åtgärden har slutförts. |

## Detaljerat alternativ som används för felsökning {#verbose-option-used-for-troubleshooting}

När du startar CRX kan du lägga till alternativet -v (utförligt) på kommandoraden som i:

` java -jar crx-<*version*>-<*edition*>.jar -v`

Använd det utförliga alternativet för felsökning eftersom det här alternativet visar några av snabbstartsloggens utdata på konsolen.