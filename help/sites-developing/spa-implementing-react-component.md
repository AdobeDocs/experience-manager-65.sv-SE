---
title: Implementera en React Component for SPA
seo-title: Implementing a React Component for SPA
description: I den här artikeln visas ett exempel på hur du anpassar en enkel, befintlig React-komponent så att den fungerar med AEM SPA Editor.
seo-description: This article presents an example of how to adapt a simple, existing React component to work with the AEM SPA Editor.
uuid: ae6a0a6f-0c3c-4820-9b58-c2a85a9f5291
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6ed15763-02cc-45d1-adf6-cf9e5e8ebdb0
docset: aem65
exl-id: f4959c12-54c5-403a-9973-7a4ab5f16bed
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Implementera en React Component for SPA{#implementing-a-react-component-for-spa}

Single page applications (SPA) can offer compelling experiences for website users. Utvecklare vill kunna skapa webbplatser med SPA ramverk och författare vill smidigt redigera innehåll i AEM för en webbplats som byggts med SPA ramverk.

SPA innehåller en omfattande lösning för SPA inom AEM. I den här artikeln visas ett exempel på hur du anpassar en enkel, befintlig React-komponent så att den fungerar med AEM SPA Editor.

>[!NOTE]
>
>SPA Editor är den rekommenderade lösningen för projekt som kräver SPA ramverksbaserad återgivning på klientsidan (t.ex. Reaktion eller Angular).

## Introduktion {#introduction}

Tack vare det enkla och lätta kontrakt som AEM kräver och som upprättas mellan SPA och SPA Editor är det enkelt att ta ett befintligt JavaScript-program och anpassa det för användning med ett SPA i AEM.

I den här artikeln visas exemplet på väderkomponenten i exempelSPA för Web.Retail Journal.

Du bör känna till [struktur i en SPA för AEM](/help/sites-developing/spa-getting-started-react.md) innan du läser den här artikeln.

>[!CAUTION]
>Det här dokumentet använder [App för återförsäljningsjournal](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) endast i demonstrationssyfte. Det ska inte användas för något projektarbete.
>
>Alla AEM ska utnyttja [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html), som stöder SPA projekt med React eller Angular och använder SPA SDK.

## Väderkomponenten {#the-weather-component}

väderkomponenten finns i det övre vänstra hörnet i appen We.Retail Journal. Den visar det aktuella vädret på en angiven plats och drar in väderdata dynamiskt.

### Använda Widgeten Väder {#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

När du redigerar innehåll i SPA i SPA Editor visas väderkomponenten som vilken annan AEM komponent som helst, komplett med ett verktygsfält, och kan redigeras.

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

Staden kan uppdateras i en dialog precis som andra AEM.

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

Ändringen kvarstår och komponenten uppdateras automatiskt med nya väderdata.

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### Implementering av väderkomponent {#weather-component-implementation}

väderkomponenten bygger i själva verket på en allmänt tillgänglig React-komponent som kallas [Reagera på öppet väder](https://www.npmjs.com/package/react-open-weather), som har anpassats för att fungera som en komponent i Web.Retail Journal-SPA.

Nedan följer NPM-dokumentation om hur komponenten React Open Weather används.

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

Granska koden för den anpassade väderkomponenten ( `Weather.js`) i We.Retail Journal:

* **Rad 16**: Widgeten React Open Weather (Reagera Öppna väder) läses in efter behov.
* **Rad 46**: The `MapTo` funktionen relaterar den här React-komponenten till en motsvarande AEM så att den kan redigeras i SPA Editor.

* **Raderna 22-29**: The `EditConfig` är definierad, kontrollerar om staden har fyllts i och definierar värdet om det är tomt.

* **Rader 31-44**: Komponenten Väder utökar `Component` och innehåller de data som krävs enligt NPM-användningsdokumentationen för komponenten React Open Weather och återger komponenten.

```javascript
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
import {MapTo} from '@adobe/aem-react-editable-components';

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

Även om det redan finns en backend-komponent kan den som utvecklar frontend utnyttja React Open Weather-komponenten i SPA We.Retail Journal med mycket liten kodning.

## Nästa steg {#next-step}

Mer information om hur du utvecklar SPA för AEM finns i artikeln [Utveckla SPA för AEM](/help/sites-developing/spa-architecture.md).
