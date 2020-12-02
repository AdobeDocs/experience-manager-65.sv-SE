---
title: Utvärdera uppgraderingskomplexiteten med mönsteravkännaren
seo-title: Utvärdera uppgraderingskomplexiteten med mönsteravkännaren
description: Lär dig hur du använder mönsteravkännaren för att bedöma hur komplicerad din uppgradering är.
seo-description: Lär dig hur du använder mönsteravkännaren för att bedöma hur komplicerad din uppgradering är.
uuid: 84d0add9-3123-4188-9877-758911b1899f
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: b5607343-a13b-4520-a771-f1a555bfcc7b
docset: aem65
translation-type: tm+mt
source-git-commit: ba7ac70858b7b2fd610d63355a22a69c3a7586e3
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 1%

---


# Utvärdera uppgraderingskomplexiteten med mönsteravkännaren

## Översikt {#overview}

Med den här funktionen kan du kontrollera om befintliga AEM kan uppgraderas genom att identifiera mönster som används:

1. Brott mot vissa regler och görs i områden som kommer att påverkas eller skrivas över av uppgraderingen
1. Använd en AEM 6.x-funktion eller ett API som inte är bakåtkompatibelt med AEM 6.5 och som kan brytas efter uppgraderingen.

Detta kan fungera som en bedömning av den utvecklingsinsats som är nödvändig för att uppgradera till AEM 6.5.

## Konfigurera {#how-to-set-up}

Mönsteravkännaren släpps separat som ett [paket](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/compatpack/pd-all-aem65) som fungerar med AEM källversioner från 6.1 till 6.5 AEM 6.5. Den kan installeras med [Package Manager](/help/sites-administering/package-manager.md).

## Användning {#how-to-use}

>[!NOTE]
>
>Mönsteravkännaren kan köras i alla miljöer, inklusive lokala utvecklingsinstanser. För att
>
>* öka detekteringsgraden
>* undvika flaskhalsar i affärskritiska instanser

>
>
båda samtidigt rekommenderas att köra den **på mellanlagringsmiljöer** som är så nära produktionsmiljöer som möjligt inom användarprogram, innehåll och konfigurationer.

Du kan använda flera metoder för att kontrollera mönsteravkännarens utdata:

* **Via Felix Inventory Console:**

1. Gå till AEM webbkonsol genom att gå till *https://serveraddress:serverport/system/console/configMgr*
1. Välj **Status - Mönsteravkännare** så som visas i bilden nedan:

   ![screenshot-2018-2-5pattern-Dettor](assets/screenshot-2018-2-5pattern-detector.png)

* **Via ett reaktivt textbaserat eller reguljärt JSON-gränssnitt**
* **Via ett reaktivt gränssnitt för JSON-rader, **som genererar ett separat JSON-dokument på varje rad.

Båda dessa metoder beskrivs nedan:

## Reaktivt gränssnitt {#reactive-interface}

Det reaktiva gränssnittet gör det möjligt att bearbeta överträdelserapporten så snart en misstanke upptäcks.

Utdata är för närvarande tillgängliga under två URL:er:

1. Gränssnitt för oformaterad text
1. JSON-gränssnitt

## Hantera gränssnittet för oformaterad text {#handling-the-plain-text-interface}

Informationen i utdata formateras som en serie händelseposter. Det finns två kanaler - en för publiceringsöverträdelser och den andra för publicering av aktuella framsteg.

Du kan hämta dem med följande kommandon:

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep SUSPICION
```

Utdata ser ut så här:

```
2018-02-13T14:18:32.071+01:00 [SUSPICION] The pattern=ECU/extraneous.content.usage was found by detector=ContentAccessDetector with id=a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f message="Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid". More info at=https://www.adobe.com/go/aem6_EC
```

Förloppet kan filtreras med kommandot `grep`:

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep PROGRESS
```

Detta ger följande utdata:

```
2018-02-13T14:19:26.909+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=45780/16 MB items, found=0 suspicions so far in period=PT5.005S (throughput=34667 items/sec)
2018-02-13T14:19:31.904+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=106050/39 MB items, found=0 suspicions so far in period=PT10S (throughput=23378 items/sec)
2018-02-13T14:19:35.685+01:00 [PROGRESS] Finished in period=PT13.782
```

## Hantera JSON-gränssnittet {#handling-the-json-interface}

På samma sätt kan JSON bearbetas med [jq-verktyget](https://stedolan.github.io/jq/) så fort det publiceras.

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == true)'
```

Med utdata:

```
{
  "timestamp": "2018-02-13T14:20:18.894+01:00",
  "suspicion": true,
  "pattern": {
    "code": "ECU",
    "type": "extraneous.content.usage",
    "detective": "ContentAccessDetector",
    "moreInfo": "https://www.adobe.com/go/aem6_ECU"
  },
  "item": {
    "id": "a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f",
    "message": "Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid"
  }
}
```

Förloppet rapporteras var femte sekund och kan hämtas genom att andra meddelanden utelämnas än de som markerats som misstänkta:

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == false)'
```

Med utdata:

```
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:17.279+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 57209,
    "itemsAnalysedSize": "26 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT5.003S",
    "elapsedTimeMilliseconds": 5003,
    "itemsPerSecond": 36965
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:22.276+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 113194,
    "itemsAnalysedSize": "46 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT10S",
    "elapsedTimeMilliseconds": 10000,
    "itemsPerSecond": 24092
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:25.762+01:00",
  "type": "FINISHED",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 140744,
    "itemsAnalysedSize": "63 MB",
    "suspicionsFound": 1
  },
  "progress": {
    "elapsedTime": "PT13.486S",
    "elapsedTimeMilliseconds": 13486,
    "itemsPerSecond": 19907
  }
}
{
  "suspicion": false,
  "type": "SUMMARY",
  "suspicionsFound": 1,
  "totalTime": "PT13.487S"
}
```

>[!NOTE]
>
>Det rekommenderade sättet är att spara hela utdata från url i filen och sedan bearbeta det via `jq` eller `grep` för att filtrera informationstypen.

## Identifieringsomfång {#scope}

Mönsteravkännaren kan för närvarande kontrollera:

* OSGi-paket matchar inte export och import
* Dela resurstyper och supertyper (med innehållsövertäckningar för sökvägar) - överanvändning
* definitioner av ekindexvärden (kompatibilitet)
* VLT-paket (överanvändning)
* rep:kompatibilitet med användarnoder (i samband med OAuth-konfiguration)

>[!NOTE]
>
>Observera att mönsteravkännaren försöker förutsäga varningarna för uppgraderingen korrekt. I vissa scenarier kan det dock generera falska positiva resultat.
