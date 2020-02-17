---
title: Implementera en React Component for SPA
seo-title: Implementera en React Component for SPA
description: I den här artikeln finns ett exempel på hur du anpassar en enkel, befintlig React-komponent till AEM SPA-redigeraren.
seo-description: I den här artikeln finns ett exempel på hur du anpassar en enkel, befintlig React-komponent till AEM SPA-redigeraren.
uuid: ae6a0a6f-0c3c-4820-9b58-c2a85a9f5291
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6ed15763-02cc-45d1-adf6-cf9e5e8ebdb0
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# Implementera en React Component for SPA{#implementing-a-react-component-for-spa}

Single page applications (SPAs) can offer compelling experiences for website users. Utvecklare vill kunna bygga webbplatser med SPA-ramverk och författare vill smidigt redigera innehåll i AEM för en webbplats som byggts med SPA-ramverk.

SPA-funktionen är en omfattande lösning för att ge stöd åt SPA:er i AEM. I den här artikeln finns ett exempel på hur du anpassar en enkel, befintlig React-komponent till AEM SPA-redigeraren.

>[!NOTE]
>
>SPA-redigeraren är den rekommenderade lösningen för projekt som kräver SPA-ramverksbaserad rendering på klientsidan (t.ex. React eller Angular).

## Introduktion {#introduction}

Tack vare det enkla och lätta avtal som krävs av AEM och som finns mellan SPA och SPA Editor är det enkelt att ta ett befintligt Javascript-program och anpassa det för användning med ett SPA i AEM.

I den här artikeln visas exemplet på väderkomponenten i exemplet SPA för Web.Retail Journal.

Du bör känna till [strukturen för ett SPA-program för AEM](/help/sites-developing/spa-getting-started-react.md) innan du läser den här artikeln.

## Väderkomponenten {#the-weather-component}

väderkomponenten finns i det övre vänstra hörnet i appen We.Retail Journal. Den visar det aktuella vädret på en angiven plats och drar in väderdata dynamiskt.

### Använda Widgeten Väder {#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

När du redigerar innehåll i SPA i SPA-redigeraren visas väderkomponenten som vilken annan AEM-komponent som helst, komplett med ett verktygsfält, och kan redigeras.

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

Staden kan uppdateras i en dialogruta precis som andra AEM-komponenter.

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

Ändringen kvarstår och komponenten uppdateras automatiskt med nya väderdata.

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### Implementering av väderkomponent {#weather-component-implementation}

Väderkomponenten är i själva verket baserad på en allmänt tillgänglig React-komponent, som kallas [React Open Weather](https://www.npmjs.com/package/react-open-weather), som har anpassats för att fungera som en komponent i Web.Retail Journal SPA-programmet.

Nedan följer NPM-dokumentation om hur komponenten React Open Weather används.

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

Granska koden för den anpassade väderkomponenten ( `Weather.js`) i programmet We.Retail Journal:

* **Rad 16**: Widgeten React Open Weather (Reagera Öppna väder) läses in efter behov.
* **Rad 46**: Funktionen relaterar den här React-komponenten till en motsvarande AEM-komponent så att den kan redigeras i SPA-redigeraren. `MapTo`

* **Raderna 22-29**: Värdet `EditConfig` definieras, kontrollerar om staden har fyllts i och definierar värdet om det är tomt.

* **Raderna 31-44**: Komponenten Weather utökar `Component` klassen och tillhandahåller de data som krävs enligt NPM-användningsdokumentationen för komponenten React Open Weather och återger komponenten.

```
/*~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 ~ Copyright 2018 Adobe Systems Incorporated
 ~
 ~ Licensed under the Apache License, Version 2.0 (the "License");
 ~ you may not use this file except in compliance with the License.
 ~ You may obtain a copy of the License at
 ~
 ~     https://www.apache.org/licenses/LICENSE-2.0
 ~
 ~ Unless required by applicable law or agreed to in writing, software
 ~ distributed under the License is distributed on an "AS IS" BASIS,
 ~ WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 ~ See the License for the specific language governing permissions and
 ~ limitations under the License.
 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~*/
import React, {Component} from 'react';
import ReactWeather from 'react-open-weather';
import {MapTo} from '@adobe/cq-react-editable-components';

require('./Weather.css');

const WeatherEditConfig = {

    emptyLabel: 'Weather',

    isEmpty: function() {
        return !this.props || !this.props.cq_model || !this.props.cq_model.city || this.props.cq_model.city.trim().length < 1;
    }
};

class Weather extends Component {

    render() {
        let apiKey = "12345678901234567890";
        let city;

        if (this.props.cq_model) {
            city = this.props.cq_model.city;
            return <ReactWeather key={'react-weather' + Date.now()} forecast="today" apikey={apiKey} type="city" city={city} />
        }

        return null;
    }
}

MapTo('we-retail-journal/global/components/weather')(Weather, WeatherEditConfig);
```

Även om det redan finns en backend-komponent kan den som utvecklar frontend utnyttja React Open Weather-komponenten i Web.Retail Journal SPA med mycket liten kodning.

## Nästa steg {#next-step}

Mer information om hur du utvecklar SPA för AEM finns i artikeln [Developing SPA for AEM](/help/sites-developing/spa-architecture.md).
