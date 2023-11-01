---
title: Getting Started with SPA in AEM - React
seo-title: Getting Started with SPAs in AEM - React
description: I den här artikeln visas ett exempel SPA programmet, hur det sätts ihop och hur du snabbt kommer igång med ditt eget SPA med React Framework.
seo-description: This article presents a sample SPA application, explains how it is put together, and lets you get up-and-running with your own SPA quickly using the React framework.
uuid: 2beca277-a381-4482-99f6-85005d826d06
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: cc1e5c20-cc9c-4222-8a11-ec5a963d4466
docset: aem65
exl-id: 552649e7-6054-4ae8-b570-5ba7230e6f19
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 0%

---

# Getting Started with SPA in AEM - React{#getting-started-with-spas-in-aem-react}

Single page applications (SPA) can offer compelling experiences for website users. Utvecklare vill kunna skapa webbplatser med SPA ramverk och författare vill smidigt redigera innehåll i AEM för en webbplats som byggts med SPA ramverk.

SPA innehåller en omfattande lösning för SPA inom AEM. I den här artikeln presenteras en förenklad SPA om React-ramverket, som förklarar hur det sätts ihop så att du snabbt kan komma igång med din egen SPA.

>[!NOTE]
>
>Artikeln bygger på React Framework. Motsvarande dokument för ramverket Angular finns i [Komma igång med SPA i AEM - Angular](/help/sites-developing/spa-getting-started-angular.md).

>[!NOTE]
>
>SPA Editor är den rekommenderade lösningen för projekt som kräver SPA ramverksbaserad rendering på klientsidan (till exempel React eller Angular).

## Introduktion {#introduction}

I den här artikeln sammanfattas grundläggande funktioner för en enkel SPA och det minimum du behöver känna till för att få igång ditt arbete.

Mer information om hur SPA fungerar i AEM finns i följande dokument:

* [SPA introduktion och genomgång](/help/sites-developing/spa-walkthrough.md)
* [Introduktion till SPA](/help/sites-developing/spa-overview.md)
* [SPA](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>Om du vill kunna skapa innehåll i en SPA måste innehållet lagras i AEM och kunna visas av innehållsmodellen.
>
>En SPA som utvecklats utanför AEM blir inte författande om den inte respekterar innehållsmodellkontraktet.

Det här dokumentet kommer att gå igenom strukturen i en förenklad SPA som skapats med React-ramverket och illustrera hur det fungerar så att du kan tillämpa den här förståelsen på din egen SPA.

## Beroenden, konfiguration och byggteknik {#dependencies-configuration-and-building}

Förutom det förväntade React-beroendet kan SPA utnyttja ytterligare bibliotek för att göra det enklare att skapa SPA.

### Beroenden {#dependencies}

The `package.json` -filen definierar kraven för det övergripande SPA. Här listas AEM beroenden för en fungerande SPA.

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

Eftersom det här exemplet bygger på React-ramverket finns det två React-specifika beroenden som är obligatoriska i `package.json` fil:

```
react
 react-dom
```

The `aem-clientlib-generator` används för att skapa klientbibliotek automatiskt som en del av byggprocessen.

`"aem-clientlib-generator": "^1.4.1",`

Mer information finns [på GitHub här](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>Den lägsta versionen av `aem-clientlib-generator` krävs är 1.4.1.

The `aem-clientlib-generator` är konfigurerad i `clientlib.config.js` filen enligt följande.

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-react-app/clientlibs",

    libs: {
        name: "my-react-app",
        allowProxy: true,
        categories: ["my-react-app"],
        embed: ["my-react-app.responsivegrid"],
        jsProcessor: ["min:gcc"],
        serializationFormat: "xml",
        assets: {
            js: [
                "dist/**/*.js"
            ],
            css: [
                "dist/**/*.css"
            ]
        }
    }
};
```

### Byggnad {#building}

Bygg appen faktiskt [Webpack](https://webpack.js.org/) för implementering förutom aem-clientlib-generator för automatisk generering av klientbibliotek. Därför påminner kommandot build om:

`"build": "webpack && clientlib --verbose"`

När paketet har skapats kan det överföras till en AEM.

### AEM Project Archettype {#aem-project-archetype}

Alla AEM ska utnyttja [AEM Project Archettype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html), som stöder SPA projekt med React eller Angular och använder SPA SDK.

## Programstruktur {#application-structure}

Om du tar med beroenden och bygger din app enligt beskrivningen ovan får du ett fungerande SPA som du kan överföra till din AEM.

I nästa avsnitt av det här dokumentet får du information om hur en SPA i AEM är strukturerad, vilka filer som är viktiga för programmet och hur de fungerar tillsammans.

En förenklad bildkomponent används som exempel, men alla komponenter i programmet är baserade på samma koncept.

### index.js {#index-js}

Ingångspunkten i SPA är förstås `index.js` filen som visas här förenklades för att fokusera på det viktiga innehållet.

```
import ReactDOM from 'react-dom';
import App from './App';
import { ModelManager, Constants } from "@adobe/aem-spa-page-model-manager";

...

ModelManager.initialize().then((pageModel) => {
ReactDOM.render(
    <App cqChildren={pageModel[Constants.CHILDREN_PROP]} cqItems={pageModel[Constants.ITEMS_PROP]} cqItemsOrder={pageModel[Constants.ITEMS_ORDER_PROP]} cqPath={ModelManager.rootPath} locationPathname={ window.location.pathname }/>
, document.getElementById('page'));

});
```

Huvudfunktionen i `index.js` är att utnyttja `ReactDOM.render` för att bestämma var i DOM programmet ska injiceras.

Det här är en standardanvändning av den här funktionen, som inte är unik för det här exempelprogrammet.

#### Statisk instansiering {#static-instantiation}

När komponenten instansieras statiskt med komponentmallen (till exempel JSX), måste värdet skickas från modellen till komponentens egenskaper.

### App.js {#app-js}

Genom att återge programmet `index.js` samtal `App.js`, som visas här i en förenklad version för att fokusera på det viktiga innehållet.

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` används främst för att kapsla in rotkomponenterna som utgör programmet. Startpunkten för alla program är sidan.

### Page.js {#page-js}

Genom att återge sidan `App.js` samtal `Page.js` som anges här i en förenklad version.

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

I detta exempel `AppPage` class extends `Page`, som innehåller de metoder för internt innehåll som sedan kan användas.

The `Page` infogar JSON-representationen av sidmodellen och bearbetar innehållet för att kapsla in/dekorera varje element på sidan. Mer information om `Page` finns i dokumentet [SPA](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### Image.js {#image-js}

När sidan renderas kan komponenterna som `Image.js` som visas här kan återges.

```
import React, {Component} from 'react';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Image.css');

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function() {
        return !this.props || !this.props.src || this.props.src.trim().length < 1;
    }
};

class Image extends Component {

    render() {
        return (<img src={this.props.src}>);
    }
}

MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);
```

Det centrala SPA i AEM är att mappa SPA komponenter till AEM och uppdatera komponenten när innehållet ändras (och omvänt). Se dokumentet [SPA](/help/sites-developing/spa-overview.md) för en sammanfattning av den här kommunikationsmodellen.

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

The `MapTo` metoden mappar SPA till AEM. Det stöder användningen av en enda sträng eller en array med strängar.

`ImageEditConfig` är ett konfigurationsobjekt som bidrar till att aktivera en komponents redigeringsfunktioner genom att tillhandahålla de metadata som behövs för att redigeraren ska kunna generera platshållare

Om det inte finns något innehåll visas etiketter som platshållare för det tomma innehållet.

#### Egenskaper som skickats dynamiskt {#dynamically-passed-properties}

Data som kommer från modellen skickas dynamiskt som egenskaper för komponenten.

## Exportera redigerbart innehåll {#exporting-editable-content}

Du kan exportera en komponent och göra den redigerbar.

```
import React, { Component } from 'react';
import { MapTo } from '@adobe/aem-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

The `MapTo` funktionen returnerar en `Component` som är resultatet av en komposition som utökar den angivna `PageClass` med klassnamn och attribut som aktiverar redigeringen. Den här komponenten kan exporteras för att senare instansieras i koden för programmet.

Vid export med `MapTo` eller `withModel` funktioner, `Page` -komponent, omsluts med en `ModelProvider` -komponent som ger standardkomponenter tillgång till den senaste versionen av sidmodellen eller en exakt plats i den sidmodellen.

Mer information finns i [SPA](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743).

>[!NOTE]
>
>Som standard får du hela komponentmodellen när du använder `withModel` funktion.

## Dela information mellan SPA {#sharing-information-between-spa-components}

Det är regelbundet nödvändigt att komponenter i ett ensidigt program delar information. Det finns flera rekommenderade sätt att göra detta, som anges nedan i ökande komplexitetsordning.

* **Alternativ 1:** Centralisera logiken och sända till nödvändiga komponenter, till exempel med React Context.
* **Alternativ 2:** Dela komponentlägen med hjälp av ett lägesbibliotek som Redux.
* **Alternativ 3:** Utnyttja objekthierarkin genom att anpassa och utöka behållarkomponenten.

## Nästa steg {#next-steps}

En steg-för-steg-guide till hur du skapar egna SPA finns i [Getting Started with the AEM SPA Editor - WKND Events Tutorial](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

Mer information om hur du organiserar dig för att utveckla SPA för AEM finns i artikeln [Utveckla SPA för AEM](/help/sites-developing/spa-architecture.md).

Mer information om den dynamiska modellen till komponentmappning och hur den fungerar i SPA i AEM finns i artikeln [Dynamisk mappning av modell till komponent för SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Om du vill implementera SPA i AEM för ett annat ramverk än React eller Angular eller bara vill fördjupa dig i hur SPA SDK för AEM fungerar, se [SPA](/help/sites-developing/spa-blueprint.md) artikel.
