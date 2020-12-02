---
title: Enterprise DevOps
seo-title: Enterprise DevOps
description: Läs om processer, metoder och kommunikation som krävs för att underlätta driftsättning och samarbete.
seo-description: Läs om processer, metoder och kommunikation som krävs för att underlätta driftsättning och samarbete.
uuid: ca4806d2-c845-4c18-9498-4b66f0980a5e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
discoiquuid: 934eda2a-bd3b-4018-86dc-dbb01d246386
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 94%

---


# Enterprise DevOps{#enterprise-devops}

DevOps omfattar processer, metoder och kommunikation som krävs för att:

* Underlätta driftsättningen av programvaran i olika miljöer.
* Förenkla samarbetet mellan utvecklings-, testnings- och driftsättningsteamen.

DevOps vill undvika problem som:

* Manuella fel.
* Glömda element: till exempel filer och konfigurationsinformation.
* Avvikelser: till exempel mellan en utvecklares lokala miljö och andra miljöer.

## Miljöer {#environments}

En Adobe Experience Manager-driftsättning (AEM) består vanligtvis av flera miljöer som används för olika syften på olika nivåer:

* [Utveckling](#development)
* [Kvalitetssäkring](#quality-assurance)
* [Mellanlagring](#staging)
* [Produktion](#production-author-and-publish)

>[!NOTE]
>
>Produktionsmiljön måste ha minst en författar- och en publiceringsmiljö.
>
>Vi rekommenderar att alla andra miljöer också består av en författar- och en publiceringsmiljö som speglar produktionsmiljön och möjliggör tidig testning.

### Utveckling {#development}

Utvecklarna ansvarar för att utveckla och anpassa det föreslagna projektet (oavsett om det är en webbplats, mobilappar, DAM-implementering osv.) med alla funktioner som krävs. De ska:

* utveckla och anpassa de nödvändiga delarna, till exempel mallar, komponenter, arbetsflöden och program
* förverkliga designen
* utveckla de tjänster och skript som krävs för att implementera de funktioner som krävs

Konfigurationen av [utvecklingsmiljön](/help/sites-developing/best-practices.md) kan vara beroende av olika faktorer, men består vanligtvis av:

* Ett integrerat utvecklingssystem med versionskontroll som ger en integrerad kodbas. Detta används för att sammanfoga och konsolidera kod från de enskilda utvecklingsmiljöer som används av varje utvecklare.
* En personlig miljö för varje utvecklare, vilken vanligtvis finns på hens lokala dator. Koden synkroniseras med versionskontrollsystemet vid lämpliga intervall

Beroende på hur omfattande ditt system är kan utvecklingsmiljön ha både författar- och publiceringsinstanser.

### Kvalitetssäkring {#quality-assurance}

Den här miljön används av kvalitetssäkringsteamet för att på ett heltäckande sätt [testa](/help/sites-developing/test-plan.md) ditt nya system. både design och funktion. Den bör ha både författar- och publiceringsmiljöer med lämpligt innehåll och tillhandahålla alla tjänster som behövs för att möjliggöra en komplett serie tester.

### Mellanlagring {#staging}

Mellanlagringsmiljön bör vara en spegling av produktionsmiljön – konfiguration, kod och innehåll:

* Den används för att testa de skript som används för att implementera den faktiska driftsättningen.
* Den kan användas för sluttester (design, funktionalitet och gränssnitt) före driftsättning till produktionsmiljöerna.
* Även om det inte alltid är möjligt att ha samma mellanlagringsmiljö som produktionsmiljön bör den vara så lik som möjligt för att möjliggöra prestanda- och lasttestning.

### Produktion – Author och Publish {#production-author-and-publish}

Produktionsmiljön består av de miljöer som behövs för att [författa och publicera](/help/sites-authoring/author.md#concept-of-authoring-and-publishing) implementeringen.

En produktionsmiljö består av minst en författarinstans och en publiceringsinstans:

* En [författarinstans](#author) för inmatning av innehåll.
* En [publiceringsinstans](#publish) för innehåll som är tillgängligt för besökare/användare.

Beroende på projektets omfattning består det ofta av flera författar- och/eller publiceringsinstanser. På en lägre nivå kan databasen även grupperas i flera instanser.

#### Författare {#author}

Författarinstanser ligger vanligtvis bakom den interna brandväggen. I den här miljön kommer du, och dina kolleger, att utföra författaruppgifter som att:

* administrera hela systemet
* mata in innehåll
* konfigurera layout och design för innehållet
* aktivera innehållet i Publish-miljön

Innehåll som aktiverats paketeras och placeras i författarmiljöns replikeringskö. Replikeringsprocessen överför sedan innehållet till publiceringsmiljön.

För att data som genererats i en publiceringsmiljö ska återreplikeras tillbaka till författarmiljön kommer en replikeringslyssnare i författarmiljön att undersöka publiceringsmiljön och hämta sådant innehåll från publiceringsmiljöns utkorg för omvänd replikering.

#### Publicera {#publish}

En Publish-miljö finns vanligtvis i DMZ (Demilitarized Zone). Det är i den här miljön som besökare kommer att få tillgång till ditt innehåll (t.ex. via en webbplats eller i form av en mobilapp) och interagera med det oavsett om det är offentligt eller finns i intranätet. En publiceringsmiljö:

* innehåller innehåll som replikerats från författarmiljön
* gör innehållet tillgängligt för besökare
* lagrar användardata som genererats av besökarna, t.ex. kommentarer eller andra inskickade formulär
* kan konfigureras för att lägga till sådana användardata i en utkorg, för återreplikering tillbaka till författarmiljön

I publiceringsmiljön genereras ditt innehåll dynamiskt i realtid och innehållet kan anpassas för varje enskild användare.

## Kodförflyttning {#code-movement}

Kod ska alltid spridas nedifrån och upp:

* koden utvecklas först lokalt och sedan i integrerade utvecklingsmiljöer
* följt av grundlig testning i QA-miljön
* testas sedan på nytt i mellanlagringsmiljöer
* endast därefter får koden driftsättas till produktionsmiljöerna

Koden (t.ex. anpassade webbprogramfunktioner och designmallar) överförs vanligtvis genom att paket exporteras och importeras mellan olika innehållsdatabaser. Om det behövs kan den här replikeringen konfigureras som en automatisk process.

AEM utlöser ofta koddistribution:

* Automatiskt: för överföring till utvecklings- och QA-miljöer.
* Manuellt: driftsättning till mellanlagrings- och produktionsmiljöerna sker på ett mer kontrollerat sätt, ofta manuellt, men automatisering är dock möjlig vid behov.

![chlimage_1](assets/chlimage_1.png)

## Innehållsförflyttning {#content-movement}

Innehåll som skapas för produktion ska **alltid** författas inom författarinstansen.

Innehåll bör inte följa kod från lägre miljöer till högre, eftersom det inte är bra att låta författare skapa innehåll på lokala datorer eller lägre miljöer, och att sedan flytta innehållet till produktionsmiljön, vilket troligen kan orsaka fel och inkonsekvenser.

Produktionsinnehållet bör flyttas från produktionsmiljön till mellanlagringsmiljön för att säkerställa att mellanlagringsmiljön är effektiv och korrekt.

>[!NOTE]
>
>Detta innebär inte att mellanlagringsinnehåll måste synkroniseras kontinuerligt med produktionen, regelbundna uppdateringar är tillräckligt, men framför allt bör det ske innan en ny koditeration testas. Innehåll i kvalitetssäkrings- och utvecklingsmiljöer behöver inte uppdateras lika ofta, utan bara vara en bra representation av produktionsinnehållet.

Innehåll kan överföras:

* Mellan olika miljöer – genom exporter och importer av paket.
* Mellan olika instanser - genom direkt replikering ([AEM replikering](/help/sites-deploying/replication.md)) av innehållet (med HTTP-, eller HTTPS-anslutning).

![chlimage_1-1](assets/chlimage_1-1.png)