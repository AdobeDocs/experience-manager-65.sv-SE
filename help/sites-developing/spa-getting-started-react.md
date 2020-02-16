---
title: Komma igång med SPA i AEM - Reaktion
seo-title: Komma igång med SPA i AEM - Reaktion
description: I den här artikeln presenteras ett exempel på ett SPA-program, som förklarar hur det sätts ihop och gör att du snabbt kan komma igång med ditt eget SPA-program med hjälp av React Framework.
seo-description: I den här artikeln presenteras ett exempel på ett SPA-program, som förklarar hur det sätts ihop och gör att du snabbt kan komma igång med ditt eget SPA-program med hjälp av React Framework.
uuid: 2beca277-a381-4482-99f6-85005d826d06
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: cc1e5c20-cc9c-4222-8a11-ec5a963d4466
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# Komma igång med SPA i AEM - Reaktion{#getting-started-with-spas-in-aem-react}

Single page applications (SPAs) can offer compelling experiences for website users. Utvecklare vill kunna bygga webbplatser med SPA-ramverk och författare vill smidigt redigera innehåll i AEM för en webbplats som byggts med SPA-ramverk.

SPA-funktionen är en omfattande lösning för att ge stöd åt SPA:er i AEM. I den här artikeln presenteras en förenklad SPA-applikation i React-ramverket, som förklarar hur det är uppbyggt, så att du snabbt kan komma igång med din egen SPA.

>[!NOTE]
>
>Artikeln bygger på React Framework. Motsvarande dokument för vinkelramverket finns i [Komma igång med SPA i AEM - Vinkel](/help/sites-developing/spa-getting-started-angular.md).

>[!NOTE]
>
>SPA-redigeraren är den rekommenderade lösningen för projekt som kräver SPA-ramverksbaserad rendering på klientsidan (t.ex. React eller Angular).

## Introduktion {#introduction}

I den här artikeln sammanfattas grundläggande funktioner i ett enkelt SPA-avtal och det minimum du behöver känna till för att få igång det.

Mer information om hur SPA fungerar i AEM finns i följande dokument:

* [Introduktion och genomgång av SPA](/help/sites-developing/spa-walkthrough.md)
* [SPA-introduktion](/help/sites-developing/spa-overview.md)
* [SPA Blueprint](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>För att kunna skapa innehåll i ett SPA måste innehållet lagras i AEM och kunna visas av innehållsmodellen.
>
>En SPA som utvecklats utanför AEM kommer inte att vara generös om den inte följer innehållsmodellkontraktet.

Det här dokumentet kommer att gå igenom strukturen i en förenklad SPA som skapats med React-ramverket och illustrera hur det fungerar så att du kan tillämpa den här förståelsen på din egen SPA.

## Beroenden, konfiguration och byggteknik {#dependencies-configuration-and-building}

Förutom det förväntade React-beroendet kan SPA-exemplet utnyttja ytterligare bibliotek för att göra skapandet av SPA mer effektivt.

### Beroenden {#dependencies}

Filen definierar kraven för det övergripande SPA-paketet `package.json` . Här listas de lägsta AEM-beroendena för en fungerande SPA.

```
  "dependencies": {
    "@adobe/cq-react-editable-components": "~1.0.3",
    "@adobe/cq-spa-component-mapping": "~1.0.3",
    "@adobe/cq-spa-page-model-manager": "~1.0.4"
  }
```

Eftersom det här exemplet baseras på React-ramverket finns det två React-specifika beroenden som är obligatoriska i `package.json` filen:

```
react
 react-dom
```

Det `aem-clientlib-generator` används för att göra det automatiskt att skapa klientbibliotek som en del av byggprocessen.

`"aem-clientlib-generator": "^1.4.1",`

Mer information finns [på GitHub här](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>Den lägsta versionen av `aem-clientlib-generator` som krävs är 1.4.1.

Den `aem-clientlib-generator` är konfigurerad i `clientlib.config.js` filen enligt följande.

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

Genom att bygga appen används [Webpack](https://webpack.js.org/) för distribution utöver aem-clientlib-generator för att automatiskt skapa klientbibliotek. Därför påminner kommandot build om:

`"build": "webpack && clientlib --verbose"`

När paketet har skapats kan det överföras till en AEM-instans.

### Maven Archetype for SPA Starter Kit {#maven-archetype-for-spa-starter-kit}

Adobe rekommenderar att du använder [Maven Archetype för SPA Starter Kit](https://github.com/adobe/aem-spa-project-archetype) för att starta ditt eget SPA-projekt för AEM.

## Programstruktur {#application-structure}

Om du tar med beroenden och bygger din app enligt beskrivningen ovan får du ett fungerande SPA-paket som du kan överföra till din AEM-instans.

I nästa avsnitt av det här dokumentet får du information om hur ett SPA i AEM är strukturerat, vilka filer som är viktiga för programmet och hur de fungerar tillsammans.

En förenklad bildkomponent används som exempel, men alla komponenter i programmet är baserade på samma koncept.

### index.js {#index-js}

Ingångspunkten i produktresumén är förstås den fil som visas här förenklad för att fokusera på det viktiga innehållet. `index.js`

```
import ReactDOM from 'react-dom';
import App from './App';
import { ModelManager, Constants } from "@adobe/cq-spa-page-model-manager";

...

ModelManager.initialize().then((pageModel) => {
ReactDOM.render(
    <App cqChildren={pageModel[Constants.CHILDREN_PROP]} cqItems={pageModel[Constants.ITEMS_PROP]} cqItemsOrder={pageModel[Constants.ITEMS_ORDER_PROP]} cqPath={ModelManager.rootPath} locationPathname={ window.location.pathname }/>
, document.getElementById('page'));

});
```

Huvudfunktionen för `index.js` är att utnyttja `ReactDOM.render` funktionen för att avgöra var i DOM som programmet ska injiceras.

Det här är en standardanvändning av den här funktionen, som inte är unik för det här exempelprogrammet.

#### Statisk instansiering {#static-instantiation}

När komponenten instansieras statiskt med komponentmallen (t.ex. JSX), måste värdet skickas från modellen till komponentens egenskaper.

### App.js {#app-js}

Genom att återge programmet anropar `index.js` du `App.js`som visas här i en förenklad version för att fokusera på det viktiga innehållet.

```
import {Page, withModel } from '@adobe/cq-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` används främst för att kapsla in rotkomponenterna som appen består av. Startpunkten för alla program är sidan.

### Page.js {#page-js}

Genom att återge sidan anropas `App.js` anrop `Page.js` som listas här i en förenklad version.

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/cq-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

I det här exemplet utökas `AppPage` klassen `Page`som innehåller de interna innehållsmetoderna som sedan kan användas.

I `Page` importeras JSON-representationen av sidmodellen och bearbetas innehållet för att kapsla in/dekorera varje element på sidan. Mer information om `Page` finns i dokumentet [SPA Blueprint](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### Image.js {#image-js}

När sidan återges kan komponenterna som `Image.js` visas här återges.

```
import React, {Component} from 'react';
import {MapTo} from '@adobe/cq-react-editable-components';

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

Den centrala idén med SPA i AEM är att mappa SPA-komponenter till AEM-komponenter och uppdatera komponenten när innehållet ändras (och vice versa). I dokumentet [SPA Editor Overview](/help/sites-developing/spa-overview.md) finns en sammanfattning av kommunikationsmodellen.

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

Metoden mappar `MapTo` SPA-komponenten till AEM-komponenten. Det stöder användningen av en enda sträng eller en array med strängar.

`ImageEditConfig` är ett konfigurationsobjekt som bidrar till att aktivera en komponents redigeringsfunktioner genom att tillhandahålla de metadata som behövs för att redigeraren ska kunna generera platshållare

Om det inte finns något innehåll visas etiketter som platshållare för det tomma innehållet.

#### Dynamiskt överförda egenskaper {#dynamically-passed-properties}

Data som kommer från modellen skickas dynamiskt som egenskaper för komponenten.

## Exportera redigerbart innehåll {#exporting-editable-content}

Du kan exportera en komponent och göra den redigerbar.

```
import React, { Component } from 'react';
import { MapTo } from '@cq/cq-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

Funktionen `MapTo` returnerar ett `Component` som är resultatet av en disposition som utökar det angivna `PageClass` med de klassnamn och attribut som aktiverar redigeringen. Den här komponenten kan exporteras för att senare instansieras i koden för programmet.

När komponenten exporteras med `MapTo` eller `withModel` funktioner omsluts `Page` komponenten av en `ModelProvider` komponent som ger standardkomponenter tillgång till den senaste versionen av sidmodellen eller en exakt plats i den sidmodellen.

Mer information finns i [SPA-designdokumentet](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743).

>[!NOTE]
>
>Som standard tar du emot hela komponentmodellen när du använder `withModel` funktionen.

## Dela information mellan SPA-komponenter {#sharing-information-between-spa-components}

Det är regelbundet nödvändigt att komponenter i ett ensidigt program delar information. Det finns flera rekommenderade sätt att göra detta, som anges nedan i ökande komplexitetsordning.

* **** Alternativ 1: Centralisera logiken och sända till nödvändiga komponenter, till exempel med React Context.
* **** Alternativ 2: Dela komponentlägen med hjälp av ett lägesbibliotek som Redux.
* **** Alternativ 3: Utnyttja objekthierarkin genom att anpassa och utöka behållarkomponenten.

## Nästa steg {#next-steps}

En stegvis guide till hur du skapar en egen SPA finns i [Komma igång med AEM SPA Editor - WKND Events Tutorial](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

Mer information om hur du organiserar dig för att utveckla SPA för AEM finns i artikeln [Developing SPAs for AEM](/help/sites-developing/spa-architecture.md).

Mer information om den dynamiska mappningen av modell till komponent och hur den fungerar i SPA i AEM finns i artikeln [Dynamic Model to Component Mapping for SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Om du vill implementera SPA i AEM för ett annat ramverk än React eller Angular, eller bara vill fördjupa dig i hur SPA SDK för AEM fungerar, se artikeln [SPA-utkast](/help/sites-developing/spa-blueprint.md) .
