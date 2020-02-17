---
title: Introduktion till AEM Platform
seo-title: Introduktion till AEM Platform
description: I den här artikeln finns en allmän översikt över AEM-plattformen och dess viktigaste komponenter.
seo-description: I den här artikeln finns en allmän översikt över AEM-plattformen och dess viktigaste komponenter.
uuid: 214d4c49-1f5c-432c-a2c0-c1fbdceee716
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: fccf9a0f-ebab-45ab-8460-84c86b3c4192
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/introduction-to-oak
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Introduktion till AEM Platform{#introduction-to-the-aem-platform}

AEM-plattformen i AEM 6 bygger på Apache Jackrabbit Oak.

Apache Jackrabbit Oak är ett försök att implementera en skalbar och prestandabaserad hierarkisk innehållsdatabas som kan användas som grund för moderna webbplatser i världsklass och andra krävande innehållsprogram.

Det är efterföljaren till Jackrabbit 2 och används av AEM 6 som standardbackend för sin innehållsdatabas, CRX.

## Utforma principer och mål {#design-principles-and-goals}

Oak implementerar specifikationen [JSR-283](https://www.day.com/day/en/products/jcr/jsr-283.html) (JCR 2.0). Dess främsta designmål är att

* Bättre stöd för stora databaser
* Flera distribuerade klusternoder för hög tillgänglighet
* Bättre prestanda
* Stöd för många underordnade noder och åtkomstkontrollsnivåer

## Arkitekturbegrepp {#architecture-concept}

![chlimage_1-84](assets/chlimage_1-84.png)

### Lagring {#storage}

Syftet med lagringslagret är att

* Implementera en trädmodell
* Gör lagring ansluten
* Tillhandahåll en klustermekanism

### Oak Core {#oak-core}

Oak Core lägger till flera lager i lagringslagret:

* Åtkomstnivåkontroller
* Sökning och indexering
* Observera

### Oak JCR {#oak-jcr}

Det främsta målet för JCR-rapporterna är att omvandla JCR-semantik till trädverksamhet. Byrån ansvarar också för

* Implementera JCR-API
* Innehåller implementeringskopplingar som implementerar JCR-begränsningar

Dessutom är nu icke-Java-implementeringar möjliga och en del av JCR-konceptet för eken.

## Lagringsöversikt {#storage-overview}

Lagringslagret Oak innehåller ett abstraktionslager för den faktiska lagringen av innehållet.

För närvarande finns det två lagringsimplementeringar i AEM6: **Tjärlagring** och **MongoDB-lagring**.

### Tjärlagring {#tar-storage}

Tjärlagringen använder tjärfiler. Innehållet lagras som olika typer av poster inom större segment. Journaler används för att spåra databasens senaste status.

Det finns flera viktiga designprinciper som den bygger på:

* **Oändringsbara segment**

Innehållet lagras i segment som kan vara upp till 256 kB stort. De är oföränderliga, vilket gör det enkelt att cachelagra segment som du använder ofta och minska antalet systemfel som kan skada databasen.

Varje segment identifieras av en unik identifierare (UUID) och innehåller en kontinuerlig delmängd av innehållsträdet. Dessutom kan segment referera till annat innehåll. Varje segment innehåller en lista med UUID:n för andra refererade segment.

* **Lokalitet**

Relaterade poster som en nod och dess direkt underordnade noder lagras vanligtvis i samma segment. Detta gör det mycket snabbt att söka i databasen och undviker de flesta cachemissar för vanliga klienter som har åtkomst till mer än en relaterad nod per session.

* **Kompacitet**

Formateringen av posterna är optimerad för att minska IO-kostnaderna och för att passa så mycket innehåll som möjligt i cacheminnen.

### Mongo-lagring {#mongo-storage}

MongoDB-lagringsutrymmet utnyttjar MongoDB för att dela och klustra. Databasträdet sparas i en MongoDB-databas där varje nod är ett separat dokument.

Den har flera särdrag:

* Revisioner

För varje uppdatering (implementering) av innehållet skapas en ny revision. En revidering är i princip en sträng som består av tre element:

1. En tidsstämpel som härleds från systemtiden för datorn som den skapades på
1. En räknare som särskiljer revideringar som skapats med samma tidsstämpel
1. Klusternod-ID där revisionen skapades

* Förgreningar

Förgreningar stöds, vilket gör att klienten kan mellanlagra flera ändringar och göra dem synliga med ett enda sammanfogningsanrop.

* Föregående dokument

MongoDB-lagring lägger till data i ett dokument vid varje ändring. Data tas dock bara bort om en rensning aktiveras explicit. Gammala data flyttas när ett visst tröskelvärde uppnås. Tidigare dokument innehåller bara oföränderliga data, vilket betyder att de bara innehåller genomförda och sammanfogade versioner.

* Klusternodmetadata

Data om aktiva och inaktiva klusternoder sparas i databasen för att underlätta klusteråtgärder.

En typisk AEM-klusterkonfiguration med MongoDB-lagring:

![chlimage_1-85](assets/chlimage_1-85.png)

## Vad är annorlunda än Jackrabbit 2? {#what-is-different-from-jackrabbit}

Eftersom Oak är utformad för att vara bakåtkompatibel med JCR 1.0-standarden kommer det att ske nästan inga förändringar på användarnivå. Det finns dock vissa märkbara skillnader som du måste ta hänsyn till när du konfigurerar en Oak-baserad AEM-installation:

* Oak skapar inte index automatiskt. Därför måste anpassade index skapas när det behövs.
* Till skillnad från Jackrabbit 2, där sessionerna alltid återspeglar databasens senaste status, visar Oak en session en stabil vy av databasen från den tidpunkt då sessionen skapades. Detta beror på MVCC-modellen som Oak baseras på.
* Samma namn på jämställda (SNS) stöds inte i Oak.

## Annan plattformsrelaterad dokumentation {#other-platform-related-documentation}

Mer information om AEM-plattformen finns i följande artiklar:

* [Konfigurera nodarkiv och datalager i AEM 6](/help/sites-deploying/data-store-config.md)
* [Fråga och indexering](/help/sites-deploying/queries-and-indexing.md)
* [Lagringselement i AEM 6](/help/sites-deploying/storage-elements-in-aem-6.md)
* [AEM med MongoDB](/help/sites-deploying/aem-with-mongodb.md)

