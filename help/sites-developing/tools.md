---
title: Testnings- och spårningsverktyg
seo-title: Testnings- och spårningsverktyg
description: AEM tillhandahåller ett ramverk för testning av komponentens användargränssnitt och en mekanism för testning och felsökning av komponenter
seo-description: AEM tillhandahåller ett ramverk för testning av komponentens användargränssnitt och en mekanism för testning och felsökning av komponenter
uuid: 12abedb5-4ee7-4389-9340-e628adbbc053
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 3cf0fd8d-7fc8-468a-bb1e-1debb68a82a5
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---


# Testnings- och spårningsverktyg{#testing-and-tracking-tools}

## Testning {#testing}

AEM tillhandahåller:

* [ett ramverk för testning av komponentens användargränssnitt](/help/sites-developing/hobbes.md).
* [en mekanism för att testa och felsöka komponenter](/help/sites-developing/developer-mode.md).

Här följer två testverktyg för öppen källkod:

**Selen**

Selenium används för funktionstestning i en webbläsare med en användare per aktivitet. Den registrerar teststeg (klickningar) som antingen HTML-tabeller eller Java-klasser.

Mer information finns i [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**JMeter**

JMeter används för att spåra förfrågningar och kan användas för funktions-, prestanda- och stresstester.

Mer information finns i [https://jakarta.apache.org/jmeter/](https://jakarta.apache.org/jmeter).

Det finns också många egna verktyg för att automatisera tester och hantera testplaner.

### Spårning {#tracking}

Följande verktyg är enkelt tillgängliga. Men ett nyckelproblem i alla fall är att alla medlemmar i projektteamet - partner och kund - har tillgång till data.

**Bugzilla**

Ett felsökningssystem som kan konfigureras efter dina egna behov.

**Kalkylblad**

Även om det inte är specifikt ett felspårningsverktyg, används kalkylblad ofta *mis* för detta ändamål eftersom de är lätta att förstå och de flesta användare har erfarenhet av sin funktionalitet.

Om dessa används för spårning:

* de ska vara enkla.
* Antalet enskilda kalkylblad bör begränsas till ett minimum.
* måste uppdateras regelbundet.
* endast en överordnad kopia ska bevaras och alla ska veta var den överordnad kopian finns.
* De ska vara tillgängliga för alla projektmedlemmar.
* Om säkerhet är ett problem (ofta i stora företag) och gemensam åtkomst inte är möjlig, kan kopior distribueras så länge alla förstår att det är kopior som inte kan uppdateras.

Det finns också många egna verktyg för att spåra buggar och funktionsbehov.
