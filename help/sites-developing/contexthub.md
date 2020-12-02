---
title: ContextHub
seo-title: ContextHub
description: ContextHub är ett ramverk för att lagra, ändra och presentera kontextdata
seo-description: ContextHub är ett ramverk för att lagra, ändra och presentera kontextdata
uuid: 14e6ff4f-ffbe-454a-b2ec-a35333526e27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: acf5c17a-95b7-43ba-9734-241e20f4f374
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---


# ContextHub{#contexthub}

ContextHub är ett ramverk för att lagra, ändra och presentera kontextdata. Javascript-API:t på klientsidan gör att du kan komma åt data för att anpassa innehåll.

>[!NOTE]
>
>Referensimplementeringen [We.Retail](/help/sites-developing/we-retail.md) implementerar ContextHub och kan fungera som referens när du integrerar ContextHub i ditt eget projekt.

>[!CAUTION]
>
>Sökvägen som innehåller den exempel på ContextHub-konfiguration som används av [We.Retail-referensimplementeringen](/help/sites-developing/we-retail.md) ( `/libs/settings/cloudsettings/legacy`) ska bara användas som referens när du skapar en egen konfiguration.
>
>Den ska inte användas i ett projekt som din egen ContextHub-konfiguration.

## Persistence {#persistence}

ContextHub lagrar kontextdata på klienten. Med ContextHub Javascript API kan du komma åt arkiv för att skapa, uppdatera och ta bort data efter behov. Därför representerar ContextHub ett datalager på dina sidor.

Varje ContextHub-butik är en instans av en fördefinierad lagringstyp:

* ContextHub innehåller flera [typer av exempelarkiv](/help/sites-developing/ch-samplestores.md).
* Använd AEM konsoler för att [skapa butiker](ch-configuring.md#creating-a-contexthub-store).
* Utvecklare kan [skapa anpassade butikstyper](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).
* Utvecklare kan [komma åt butiksdata](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) via Javascript.

## Segmentering {#segmentation}

ContextHub innehåller en segmenteringsmotor som hanterar segment och fastställer vilka segment som matchas för den aktuella kontexten. Flera segment är definierade. Du kan använda Javascript-API:t för att [identifiera lösta segment](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments).

## Presentation {#presentation}

Med verktygsfältet [ContextHub](/help/sites-authoring/ch-previewing.md) kan marknadsförare och författare visa och ändra lagringsdata för att simulera användarupplevelsen när de skapar sidor. Verktygsfältet består av grupper med gränssnittsmoduler som ger åtkomst till ContextHub-butiker.

Varje ContextHub-gränssnittsmodul är en instans av en fördefinierad modultyp:

* ContextHub innehåller flera [exempelmodultyper](/help/sites-developing/ch-samplemodules.md).
* Använd AEM konsoler för att [lägga till gränssnittsmoduler](ch-configuring.md#adding-a-ui-module) och för att [gruppera dem i gränssnittslägen](ch-configuring.md#adding-a-ui-mode).

* Utvecklare kan [skapa anpassade modultyper](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

Utvecklare måste [lägga till ContextHub-komponenten på sidan](/help/sites-developing/ch-adding.md).
