---
title: Utöka händelsespårning
seo-title: Utöka händelsespårning
description: Med AEM Analytics kan ni spåra användarinteraktion på er webbplats
seo-description: Med AEM Analytics kan ni spåra användarinteraktion på er webbplats
uuid: 722798ac-4043-4918-a6df-9eda2c85020b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e0372f4a-fe7b-4526-8391-5bb345b51d70
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Utöka händelsespårning{#extending-event-tracking}

Med AEM Analytics kan ni spåra användarinteraktion på er webbplats. Som utvecklare kan du behöva:

* Spåra hur besökarna interagerar med era komponenter. Detta kan göras med [anpassade händelser.](#custom-events)
* [Åtkomstvärden i ContextHub](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).
* [Lägg till återanrop](#adding-record-callbacks)för poster.

>[!NOTE]
>
>Den här informationen är i princip generisk, men den använder [Adobe Analytics](/help/sites-administering/adobeanalytics.md) för specifika exempel.
>
>Allmän information om hur du utvecklar komponenter och dialogrutor finns i [Utveckla komponenter](/help/sites-developing/components.md).

## Anpassade händelser {#custom-events}

Anpassade händelser spårar allt som är beroende av tillgängligheten för en viss komponent på sidan. Detta inkluderar även händelser som är mallspecifika, eftersom sidkomponenten behandlas som en annan komponent.

### Spåra anpassade händelser vid sidinläsning {#tracking-custom-events-on-page-load}

Detta kan göras med pseudoattributet `data-tracking` (det äldre postattributet stöds fortfarande för bakåtkompatibilitet). Du kan lägga till det här i alla HTML-taggar.

Syntaxen för `data-tracking` är

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

Du kan skicka valfritt antal nyckelvärdepar som den andra parametern, som kallas nyttolast.

Ett exempel kan se ut så här:

```xml
<span data-tracking="{event:'blogEntryView',
                                values:{
                                   'blogEntryContentType': 'blog',
                                   'blogEntryUniqueID': '<%= xssAPI.encodeForJSString(entry.getId()) %>',
                                   'blogEntryTitle': '<%= xssAPI.encodeForJSString(entry.getTitle()) %>',
                                   'blogEntryAuthor':'<%= xssAPI.encodeForJSString(entry.getAuthor()) %>',
                                   'blogEntryPageLanguage':'<%= currentPage.getLanguage(true) %>'
                                },
                                componentPath:'myapp/component/mycomponent'}">
</span>
```

Vid sidinläsning samlas alla `data-tracking` attribut in och läggs till i händelsearkivet i ContextHub, där de kan mappas till Adobe Analytics-händelser. Händelser som inte mappas kommer inte att spåras av Adobe Analytics. Mer information om mappningshändelser finns i Ansluta [till Adobe Analytics](/help/sites-administering/adobeanalytics.md) .

### Spåra anpassade händelser efter sidinläsning {#tracking-custom-events-after-page-load}

Om du vill spåra händelser som inträffar efter att en sida har lästs in (till exempel användarinteraktioner) använder du `CQ_Analytics.record` JavaScript-funktionen:

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

Plats

* `events` är antingen en sträng eller en strängarray (för flera händelser).

* `values` innehåller alla värden som ska spåras
* `collect` är valfri och returnerar en array som innehåller händelsen och dataobjektet.
* `options` är valfritt och innehåller alternativ för länkspårning som HTML-element `obj` och ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`.

* `componentPath` är ett nödvändigt attribut och vi rekommenderar att du anger det till `<%=resource.getResourceType()%>`

Med följande definition aktiveras de två händelserna **och** så att användaren klickar på länken `jumptop` Hoppa till överst `headlineclick`:

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## Åtkomst till värden i ContextHub {#accessing-values-in-the-contexthub}

ContextHub JavaScript-API:t har en `getStore(name)` funktion som returnerar det angivna arkivet, om en sådan finns. Butiken har en `getItem(key)` funktion som returnerar värdet för den angivna nyckeln, om en sådan finns. Med hjälp av `getKeys()` funktionen är det möjligt att hämta en array med definierade nycklar för det specifika arkivet.

Du kan meddelas om värdeändringar på en butik genom att binda en funktion med hjälp av `ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)` funktionen.

Det bästa sättet att bli informerad om den initiala tillgängligheten för ContextHub är att använda `ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);` -funktionen.

**Ytterligare händelser för ContextHub:**

Alla butiker klara:

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

Butiksspecifik:

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>Se även den fullständiga [ContextHub API Reference](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)

## Lägger till återanrop för post {#adding-record-callbacks}

Före och efter att återanrop registreras med funktionerna `CQ_Analytics.registerBeforeCallback(callback,rank)` och `CQ_Analytics.registerAfterCallback(callback,rank)`.

Båda funktionerna tar en funktion som det första argumentet och rangordnas som det andra argumentet, som anger i vilken ordning återanropen utförs.

Om återanropet returnerar false kommer återanropen som följer i körningskedjan inte att köras.
