---
title: Loggning
seo-title: Loggning
description: Lär dig hur du konfigurerar globala parametrar för den centrala loggningstjänsten, specifika inställningar för enskilda tjänster eller hur du begär dataloggning.
seo-description: Lär dig hur du konfigurerar globala parametrar för den centrala loggningstjänsten, specifika inställningar för enskilda tjänster eller hur du begär dataloggning.
uuid: 8c9e3628-2f2c-445d-9706-5c7725b85fe2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5aa69b10-2cd0-4d34-8104-8c3b88405926
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---


# Loggning{#logging}

AEM ger dig möjlighet att konfigurera:

* globala parametrar för den centrala loggningstjänsten
* begära dataloggning, en särskild loggningskonfiguration för begärandeinformation
* särskilda inställningar för de enskilda tjänsterna, t.ex. en enskild loggfil och ett format för loggmeddelandena

Dessa är alla [OSGi-konfigurationer](/help/sites-deploying/configuring-osgi.md).

>[!NOTE]
>
>Inloggning AEM baseras på Sling-principer. Mer information finns i [Sling Logging](https://sling.apache.org/site/logging.html).

## Global loggning {#global-logging}

[Konfigurationen ](/help/sites-deploying/osgi-configuration-settings.md) för Apache Sling-loggning används för att konfigurera rotloggaren. Detta definierar de globala inställningarna för inloggning AEM:

* loggningsnivån
* platsen för den centrala loggfilen
* antalet versioner som ska behållas
* versionsrotation; antingen maximal storlek eller ett tidsintervall
* det format som ska användas när loggmeddelanden skrivs

>[!NOTE]
>
>I den här [kunskapsbasartikeln](https://helpx.adobe.com/experience-manager/kb/HowToRotateRequestAndAccessLog.html) beskrivs hur du roterar filen request.log och access.log.

## Loggare och författare för enskilda tjänster {#loggers-and-writers-for-individual-services}

Förutom de globala loggningsinställningarna kan du med AEM konfigurera specifika inställningar för en enskild tjänst:

* den specifika loggningsnivån
* platsen för den enskilda loggfilen
* antalet versioner som ska behållas
* versionsrotation; antingen maxstorlek eller tidsintervall
* det format som ska användas när loggmeddelanden skrivs
* loggaren (OSGi-tjänsten som tillhandahåller loggmeddelanden)

På så sätt kan du kanalisera loggmeddelanden för en enskild tjänst till en separat fil. Detta kan vara särskilt användbart under utveckling eller testning. om du till exempel behöver en högre loggnivå för en viss tjänst.

AEM använder följande för att skriva loggmeddelanden till filen:

1. En **OSGi-tjänst** (logger) skriver ett loggmeddelande.
1. En **loggningsloggare** tar det här meddelandet och formaterar det enligt din specifikation.
1. En **loggningsskrivare** skriver alla dessa meddelanden till den fysiska filen som du har definierat.

Dessa element är länkade med följande parametrar för de relevanta elementen:

* **Logger (loggningsloggare)**

   Definiera de tjänster som genererar meddelandena.

* **Loggfil (loggningslogg)**

   Definiera den fysiska filen för lagring av loggmeddelanden.

   Detta används för att länka en loggningslogg till en loggningsförfattare. Värdet måste vara identiskt med samma parameter i loggningsskrivarens konfiguration för att anslutningen ska kunna upprättas.

* **Loggfil (loggningsskrivare)**

   Definiera den fysiska fil som loggmeddelandena ska skrivas till.

   Detta måste vara identiskt med samma parameter i loggningsskrivarkonfigurationen, annars görs ingen matchning. Om det inte finns någon matchning skapas ett implicit skrivprogram med standardkonfigurationen (daglig loggrotation).

### Standardloggare och -författare {#standard-loggers-and-writers}

Vissa loggare och skrivprogram ingår i en AEM standardinstallation.

Det första är ett specialfall eftersom det styr både `request.log`- och `access.log`-filerna:

* Loggaren:

   * Dataloggning för anpassningsbara Apache Sling-begäranden

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * Skriv meddelanden om begärandeinnehåll till `request.log`.

* Länkar till:

   * Apache Sling Request Logger

      (org.apache.sling.engine.impl.log.RequestLogger)

   * Skriver meddelanden till antingen `request.log` eller `access.log`.

Dessa kan anpassas vid behov, men standardkonfigurationen passar de flesta installationer.

De andra paren följer standardkonfigurationen:

* Loggaren:

   * Konfiguration av loggningsloggare för Apache Sling

      (org.apache.sling.Commons.log.LogManager.factory.config)

   * Skriver `Information` meddelanden till `logs/error.log`.

* Länkar till skrivprogrammet:

   * Konfiguration av skrivprogram för Apache Sling Logging

      (org.apache.sling.Commons.log.LogManager.factory.writer)

* Loggaren:

   * Konfiguration av loggningsloggare för Apache Sling
(org.apache.sling.Commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * Skriver `Warning`-meddelanden till `../logs/error.log` för tjänsten `org.apache.pdfbox`.

* Länkar inte till ett specifikt skrivprogram, så skapar och använder ett implicit skrivprogram med standardkonfiguration (daglig loggrotation).

### Skapa egna loggare och författare {#creating-your-own-loggers-and-writers}

Du kan definiera ett eget par för loggare/skrivare:

1. Skapa en ny instans av Factory Configuration [Loggningsloggningskonfiguration för Apache Sling](/help/sites-deploying/osgi-configuration-settings.md).

   1. Ange loggfilen.
   1. Ange loggaren.
   1. Konfigurera de andra parametrarna efter behov.

1. Skapa en ny instans av fabrikskonfigurationen [Konfiguration för Apache Sling Logging Writer](/help/sites-deploying/osgi-configuration-settings.md).

   1. Ange loggfilen - den måste matcha den som har angetts för loggaren.
   1. Konfigurera de andra parametrarna efter behov.

>[!NOTE]
>
>Under vissa omständigheter kanske du vill skapa en [anpassad loggfil](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).

