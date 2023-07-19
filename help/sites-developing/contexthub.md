---
title: ContextHub
seo-title: ContextHub
description: ContextHub är ett ramverk för att lagra, ändra och presentera kontextdata
seo-description: ContextHub is a framework for storing, manipulating, and presenting context data
uuid: 14e6ff4f-ffbe-454a-b2ec-a35333526e27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: acf5c17a-95b7-43ba-9734-241e20f4f374
exl-id: 3fd50655-7461-4900-a3b8-c01b04c7ba7a
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# ContextHub{#contexthub}

ContextHub är ett ramverk för att lagra, ändra och presentera kontextdata. Med JavaScript API:t på klientsidan kan du komma åt data för att anpassa innehåll.

>[!NOTE]
>
>The [Referensimplementering för Vi.butik](/help/sites-developing/we-retail.md) implementerar ContextHub och kan fungera som referens när du integrerar ContextHub i ditt eget projekt.

>[!CAUTION]
>
>Sökvägen som innehåller exempelkonfigurationen för ContextHub som används av [Referensimplementering för Vi.butik](/help/sites-developing/we-retail.md) ( `/libs/settings/cloudsettings/legacy`) ska bara användas som referens när du skapar en egen konfiguration.
>
>Den ska inte användas i ett projekt som din egen ContextHub-konfiguration.

## Persistence {#persistence}

ContextHub lagrar kontextdata på klienten. Med ContextHub JavaScript API kan du komma åt butiker för att skapa, uppdatera och ta bort data efter behov. Därför representerar ContextHub ett datalager på dina sidor.

Varje ContextHub-butik är en instans av en fördefinierad lagringstyp:

* ContextHub innehåller flera [exempelarkivtyper](/help/sites-developing/ch-samplestores.md).
* Använd AEM konsoler för att [skapa butiker](ch-configuring.md#creating-a-contexthub-store).
* Utvecklare kan [skapa anpassade butikstyper](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).
* Utvecklare kan [åtkomstarkivdata](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) via JavaScript.

## Segmentering {#segmentation}

ContextHub innehåller en segmenteringsmotor som hanterar segment och fastställer vilka segment som matchas för den aktuella kontexten. Flera segment är definierade. Du kan använda JavaScript-API:t för att [identifiera matchade segment](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments).

## Presentation {#presentation}

The [ContextHub-verktygsfältet](/help/sites-authoring/ch-previewing.md) gör det möjligt för marknadsförare och författare att se och ändra butiksdata för att simulera användarupplevelsen när de skapar sidor. Verktygsfältet består av grupper med gränssnittsmoduler som ger åtkomst till ContextHub-butiker.

Varje ContextHub-gränssnittsmodul är en instans av en fördefinierad modultyp:

* ContextHub innehåller flera [exempelmodultyper](/help/sites-developing/ch-samplemodules.md).
* Använd AEM konsoler för att [lägg till gränssnittsmoduler](ch-configuring.md#adding-a-ui-module)och till [gruppera dem i gränssnittslägen](ch-configuring.md#adding-a-ui-mode).

* Utvecklare kan [skapa anpassade modultyper](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

Utvecklare måste [lägg till ContextHub-komponenten på sidan](/help/sites-developing/ch-adding.md).
