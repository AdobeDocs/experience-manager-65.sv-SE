---
title: Dynamisk mappning av modell till komponent för SPA
description: Lär dig hur den dynamiska mappningen av modell till komponent sker i JavaScript SPA SDK för Adobe Experience Manager.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
exl-id: 5b2ccac0-bf1d-4f06-8743-7fce6fb68378
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# Dynamisk mappning av modell till komponent för SPA{#dynamic-model-to-component-mapping-for-spas}

I det här dokumentet beskrivs hur den dynamiska mappningen av modell till komponent sker i JavaScript SPA SDK för Adobe Experience Manager (AEM).

>[!NOTE]
>
>SPA Editor är den rekommenderade lösningen för projekt som kräver SPA ramverksbaserad klientåtergivning (till exempel React eller Angular).

## ComponentMapping-modul {#componentmapping-module}

The `ComponentMapping` -modulen tillhandahålls som ett NPM-paket till frontendprojektet. Det lagrar komponenter för användargränssnitt och tillhandahåller ett sätt för Single Page Application att mappa komponenter för användargränssnitt till AEM resurstyper. Detta aktiverar en dynamisk upplösning för komponenter när JSON-modellen för programmet analyseras.

Varje objekt i modellen innehåller en `:type` fält som visar en AEM. När den är monterad kan den främre komponenten återge sig själv med det fragment av modellen som den har fått från de underliggande biblioteken.

Se [SPA](/help/sites-developing/spa-blueprint.md) om du vill ha mer information om modellparsning och åtkomst till modellen för komponenter i gränssnittet.

Se även npm-paketet: [https://www.npmjs.com/package/@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Modellstyrt Single Page-program {#model-driven-single-page-application}

Single Page-program som använder JavaScript SPA SDK för AEM är modelldrivna:

1. Front-end-komponenter registrerar sig för [Komponentmappningsarkiv](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module).
1. Sedan [Behållare](/help/sites-developing/spa-blueprint.md#container), efter att ha fått en modell av [Modellprovider](/help/sites-developing/spa-blueprint.md#the-model-provider), itererar över sitt modellinnehåll ( `:items`).

1. Om det finns en sida, dess underordnade sidor ( `:children`) hämta först en komponentklass från [Komponentmappning](/help/sites-developing/spa-blueprint.md#componentmapping) och sedan instansiera den.

## Programinitiering {#app-initialization}

Varje komponent utökas med funktionerna i [`ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider). Initieringen har därför följande allmänna form:

1. Varje modellprovider initierar sig själv och lyssnar efter ändringar som gjorts i den del av modellen som motsvarar dess inre komponent.
1. The [`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) måste initieras så som representeras av [initieringsflöde](/help/sites-developing/spa-blueprint.md).

1. När sidmodellhanteraren har lagrats returnerar den hela appmodellen.
1. Den här modellen skickas sedan till frontendroten [Behållare](/help/sites-developing/spa-blueprint.md#container) -komponenten i programmet.
1. Delar av modellen sprids slutligen till varje enskild underordnad komponent.

![app_model_initialization](assets/app_model_initialization.png)
