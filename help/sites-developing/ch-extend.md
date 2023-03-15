---
title: Utökar ContextHub
seo-title: Extending ContextHub
description: Definiera nya typer av ContextHub-butiker och moduler när de angivna lagren inte uppfyller dina lösningskrav
seo-description: Define new types of ContextHub stores and modules when the ones provided do not meet your solution requirements
uuid: 1d80c01d-ec5d-4e76-849d-bec0e1c3941a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 13a908ae-6965-4438-96d0-93516b500884
exl-id: 41898fa7-a369-4c63-8ccb-69eb3fa146a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---

# Utökar ContextHub{#extending-contexthub}

Definiera nya typer av ContextHub-butiker och moduler när de angivna lagren inte uppfyller dina lösningskrav.

## Skapa anpassade butikskandidater {#creating-custom-store-candidates}

ContextHub-butiker skapas från registrerade butikskandidater. Om du vill skapa en anpassad butik måste du skapa och registrera en butikskandidater.

JavaScript-filen som innehåller koden som skapar och registrerar butikskandidaten måste inkluderas i en [biblioteksmapp för klient](/help/sites-developing/clientlibs.md#creating-client-library-folders). Mappens kategori måste matcha följande mönster:

```xml
contexthub.store.[storeType]
```

The `[storeType]` en del av kategorin är `storeType` som butikskandidaten registreras med. (Se [Registrerar en ContextHub Store-kandidat](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate)). Till exempel för storeType för `contexthub.mystore`måste kategorin för klientbiblioteksmappen vara `contexthub.store.contexthub.mystore`.

### Skapa en ContextHub Store-kandidat {#creating-a-contexthub-store-candidate}

Om du vill skapa en butikskandidat använder du [`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent) för att utöka en av basbutikerna:

* [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

Observera att varje basbutik utökar [`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core) butik.

I följande exempel skapas det enklaste tillägget för `ContextHub.Store.PersistedStore` butikskandidat:

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

I realiteten definierar dina anpassade butikskandidater ytterligare funktioner eller åsidosätter butikens ursprungliga konfiguration. Flera [exempel på arkivkandidater](/help/sites-developing/ch-samplestores.md) installeras i databasen nedan `/libs/granite/contexthub/components/stores`. Använd CRXDE Lite för att öppna javascript-filerna om du vill lära dig av dessa exempel.

### Registrerar en ContextHub Store-kandidat {#registering-a-contexthub-store-candidate}

Registrera en butikskandidat för att integrera den med ContextHub-ramverket så att butiker kan skapas utifrån det. Om du vill registrera en butikskandidat använder du [`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) funktionen i `ContextHub.Utils.storeCandidates` klassen.

När du registrerar en butikskandidat anger du ett namn för butikstypen. När du skapar en butik från kandidaten använder du butikstypen för att identifiera den kandidat som den baseras på.

När du registrerar en butikskandidat anger du dess prioritet. När en butikskandidat registreras med samma butikstyp som en redan registrerad butikskandidat, används den som har den högre prioriteten. Därför kan du åsidosätta befintliga butikskandidater med nya implementeringar.

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

I de flesta fall behövs bara en kandidat och prioriteten kan anges till `0`, men om du är intresserad kan du läsa mer om [mer avancerade registreringar,](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) vilket gör att en av få butiksimplementationer kan väljas baserat på javascript-villkor (`applies`) och kandidatprioritet.

## Skapar gränssnittsmodultyper för ContextHub {#creating-contexthub-ui-module-types}

Skapa anpassade gränssnittsmodultyper när de [installerat med ContextHub](/help/sites-developing/ch-samplemodules.md) uppfyller inte dina krav. Om du vill skapa en gränssnittsmodultyp skapar du en ny gränssnittsmodulrenderare genom att utöka `ContextHub.UI.BaseModuleRenderer` och sedan registrera den med `ContextHub.UI`.

Skapa en användargränssnittsåtergivning moduler en `Class` -objekt som innehåller den logik som återger UI-modulen. Klassen måste minst utföra följande åtgärder:

* Utöka `ContextHub.UI.BaseModuleRenderer` klassen. Den här klassen är den grundläggande implementeringen för alla UI-modulrenderare. The `Class` objektet definierar en egenskap med namnet `extend` som du använder för att namnge den här klassen som den som utökas.

* Ange en standardkonfiguration. Skapa en `defaultConfig` -egenskap. Den här egenskapen är ett objekt som innehåller de egenskaper som har definierats för [`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) UI-modulen och andra egenskaper som du behöver.

Källan för `ContextHub.UI.BaseModuleRenderer` finns på /libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js.  Om du vill registrera renderaren använder du [`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) metoden `ContextHub.UI` klassen. Du måste ange ett namn för modultypen. När administratörer skapar en gränssnittsmodul som baseras på den här renderaren anger de det här namnet.

Skapa och registrera återgivningsklassen i en anonym funktion som körs automatiskt. Följande exempel baseras på källkoden för gränssnittsmodulen contexthub.browserinfo. Den här gränssnittsmodulen är ett enkelt tillägg till `ContextHub.UI.BaseModuleRenderer` klassen.

```xml
;(function() {

    var SurferinfoRenderer = new Class({
        extend: ContextHub.UI.BaseModuleRenderer,

        defaultConfig: {
            icon: 'coral-Icon--globe',
            title: 'Browser/OS Information',

            storeMapping: {
                surferinfo: 'surferinfo'
            },

            template:
                '<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p>' +
                '<p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>'
        }
    });

    ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());

}());
```

JavaScript-filen som innehåller koden som skapar och registrerar återgivaren måste inkluderas i en [biblioteksmapp för klient](/help/sites-developing/clientlibs.md#creating-client-library-folders). Mappens kategori måste matcha följande mönster:

```xml
contexthub.module.[moduleType]
```

The `[moduleType]` en del av kategorin är `moduleType` som modulåtergivaren registreras med. För `moduleType` av `contexthub.browserinfo`måste kategorin för klientbiblioteksmappen vara `contexthub.module.contexthub.browserinfo`.
