---
title: Utöka händelsespårning
seo-title: Extending Event Tracking
description: Med AEM Analytics kan ni spåra användarinteraktion på er webbplats
seo-description: AEM Analytics lets you track user interaction on your website
uuid: 722798ac-4043-4918-a6df-9eda2c85020b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e0372f4a-fe7b-4526-8391-5bb345b51d70
exl-id: a71d20e6-0321-4afb-95fe-6de8b7b37245
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# Utöka händelsespårning{#extending-event-tracking}

Med AEM Analytics kan ni spåra användarinteraktion på er webbplats. Som utvecklare kan du behöva:

* Spåra hur besökarna interagerar med era komponenter. Detta kan du göra med [Anpassade händelser.](#custom-events)
* [Åtkomstvärden i ContextHub](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).
* [Lägg till återanrop för poster](#adding-record-callbacks).

>[!NOTE]
>
>Den här informationen är i stort sett generisk, men den använder [Adobe Analytics](/help/sites-administering/adobeanalytics.md) för specifika exempel.
>
>Allmän information om utveckling av komponenter och dialogrutor finns i [Utveckla komponenter](/help/sites-developing/components.md).

## Anpassade händelser {#custom-events}

Anpassade händelser spårar allt som är beroende av tillgängligheten för en viss komponent på sidan. Detta inkluderar även händelser som är mallspecifika, eftersom sidkomponenten behandlas som en annan komponent.

### Spåra anpassade händelser vid sidinläsning {#tracking-custom-events-on-page-load}

Detta kan göras med pseudoattributet `data-tracking` (det äldre postattributet stöds fortfarande för bakåtkompatibilitet). Du kan lägga till det här till valfri HTML-tagg.

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

Vid sidinläsning, alla `data-tracking` attribut samlas in och läggs till i händelsearkivet för ContextHub, där de kan mappas till Adobe Analytics-händelser. Händelser som inte mappas spåras inte av Adobe Analytics. Se [Ansluta till Adobe Analytics](/help/sites-administering/adobeanalytics.md) för mer information om mappningshändelser.

### Spåra anpassade händelser efter sidinläsning {#tracking-custom-events-after-page-load}

Om du vill spåra händelser som inträffar efter att en sida har lästs in (till exempel användarinteraktioner) använder du `CQ_Analytics.record` JavaScript-funktion:

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

Plats

* `events` är antingen en sträng eller en strängarray (för flera händelser).

* `values` innehåller alla värden som ska spåras
* `collect` är valfri och returnerar en array som innehåller händelsen och dataobjektet.
* `options` är valfritt och innehåller alternativ för länkspårning som HTML-element `obj` och ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`.

* `componentPath` är ett nödvändigt attribut och vi rekommenderar att du anger det till `<%=resource.getResourceType()%>`

Med följande definition klickar en användare på **Hoppa till början** länken kommer att orsaka de två händelserna, `jumptop` och `headlineclick`, ska utlösas:

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## Åtkomst till värden i ContextHub {#accessing-values-in-the-contexthub}

ContextHub JavaScript API har en `getStore(name)` funktion som returnerar det angivna arkivet, om sådan finns. Butiken har en `getItem(key)` funktion som returnerar värdet för den angivna nyckeln, om sådan finns. Använda `getKeys()` kan du hämta en array med definierade nycklar för den specifika lagringsplatsen.

Du kan meddelas om värdeändringar på en butik genom att binda en funktion med `ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)` funktion.

Det bästa sättet att meddela om ContextHub är att använda `ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);` funktion.

**Ytterligare händelser för ContextHub:**

Alla butiker klara:

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

Butiksspecifik:

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>Se även hela [ContextHub API-referens](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)

## Lägger till återanrop för post {#adding-record-callbacks}

Före och efter återanrop registreras med funktionerna `CQ_Analytics.registerBeforeCallback(callback,rank)` och `CQ_Analytics.registerAfterCallback(callback,rank)`.

Båda funktionerna tar en funktion som det första argumentet och rangordnas som det andra argumentet, som anger i vilken ordning återanropen utförs.

Om återanropet returnerar false kommer återanropen som följer i körningskedjan inte att köras.
