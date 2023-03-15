---
title: Dynamisk mappning av modell till komponent för SPA
seo-title: Dynamic Model to Component Mapping for SPAs
description: I den här artikeln beskrivs hur den dynamiska mappningen av modell till komponent sker i Javascript SPA SDK för AEM.
seo-description: This article describes how the dynamic model to component mapping occurs in the Javascript SPA SDK for AEM.
uuid: 337b8d90-efd7-442e-9fac-66c33cc26212
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 8b4b0afc-8534-4010-8f34-cb10475a8e79
exl-id: 5b2ccac0-bf1d-4f06-8743-7fce6fb68378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# Dynamisk mappning av modell till komponent för SPA{#dynamic-model-to-component-mapping-for-spas}

I det här dokumentet beskrivs hur den dynamiska mappningen av modell till komponent sker i Javascript SPA SDK för AEM.

>[!NOTE]
>
>SPA Editor är den rekommenderade lösningen för projekt som kräver SPA ramverksbaserad återgivning på klientsidan (t.ex. Reaktion eller Angular).

## ComponentMapping-modul {#componentmapping-module}

The `ComponentMapping` -modulen tillhandahålls som ett NPM-paket till frontendprojektet. Det lagrar komponenter för användargränssnitt och tillhandahåller ett sätt för Single Page Application att mappa komponenter för användargränssnitt till AEM resurstyper. Detta aktiverar en dynamisk upplösning för komponenter när JSON-modellen för programmet analyseras.

Varje objekt i modellen innehåller en `:type` fält som visar en AEM resurstyp. När den är monterad kan den främre komponenten återge sig själv med det fragment av modellen som den har fått från de underliggande biblioteken.

Se [SPA Blueprint](/help/sites-developing/spa-blueprint.md) -dokument om du vill ha mer information om modellparsning och frontdelens åtkomst till modellen.

Se även npm-paketet: [https://www.npmjs.com/package/@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Modellstyrt Single Page-program {#model-driven-single-page-application}

Single Page-program som använder Javascript SPA SDK för AEM är modelldrivna:

1. Front-end-komponenter registrerar sig för [Komponentmappningsarkiv](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module).
1. Sedan [Behållare](/help/sites-developing/spa-blueprint.md#container), efter att ha fått en modell av [Modellprovider](/help/sites-developing/spa-blueprint.md#the-model-provider), itererar över sitt modellinnehåll ( `:items`).

1. För en sida, dess underordnade sidor ( `:children`) hämta först en komponentklass från [Komponentmappning](/help/sites-developing/spa-blueprint.md#componentmapping) och sedan instansiera den.

## Programinitiering {#app-initialization}

Varje komponent utökas med funktionerna i [ `ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider). Initieringen har därför följande allmänna form:

1. Varje modellprovider initierar sig själv och lyssnar efter ändringar som gjorts i den del av modellen som motsvarar dess inre komponent.
1. The [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) måste initieras så som representeras av [initieringsflöde](/help/sites-developing/spa-blueprint.md).

1. När sidmodellhanteraren har lagrats returnerar den hela appmodellen.
1. Den här modellen skickas sedan till frontendroten [Behållare](/help/sites-developing/spa-blueprint.md#container) -komponenten i programmet.
1. Delar av modellen sprids slutligen till varje enskild underordnad komponent.

![app_model_initialization](assets/app_model_initialization.png)
