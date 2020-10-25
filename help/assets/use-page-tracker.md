---
title: Använda sidspåraren och bädda in kod på webbsidor
description: Lär dig hur du inkluderar sidspåraren och bäddar in JavaScript-koder i webbplatskoden så att Adobe Analytics kan samla in användningsdata runt resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c1362c2c1f32d02d36d2067e0e74d927ddbc1554
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# Använda sidspårning och bädda in kod på webbsidor {#using-page-tracker-and-embed-code-in-web-pages}

Page Tracker är en del av JavaScript-kod som du inkluderar i koden för tredjepartswebbplatser så att Adobe Analytics kan samla in användningsdata runt [!DNL Adobe Experience Manager Assets] dessa webbplatser.

Om du vill fånga händelser, t.ex. klick, som är specifika för resurser, inkluderar du även koden för inbäddning i koden för tredjepartswebbplatser.

I följande exempelkod visas hur en webbsida som innehåller både sidspårningskod och inbäddningskod ser ut:

```html
<!DOCTYPE html>
<html>
    <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc/clientlibs/foundation/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in millis
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","xxxx","xxx","list1","eVar3","event8","event7");
            </script>

    </head>

    <body>

                                <img
            src="https://10.41.52.147:4502/xxxx/content/dam/test/abc.jpg"
            data-aem-asset-id="aaid:a386f2cd78234becb66bd11575f9452d"
            data-trackable=true
            onload=assetAnalytics.core.assetLoaded(this)>

        <a
            href="https://www.adobe.com"

            onclick="assetAnalytics.core.assetClicked(this);return false">
                <img
                    src="http://localhost/xxxx/content/dam/test/xyz.jpg"
                    data-aem-asset-id="aaid:7fa01fce0ebe40268cd6dcf07e2d9cb1"
                    data-trackable=true
                    onload=assetAnalytics.core.assetLoaded(this)>
        </a>

    </body>
</html>
```

## Lägg till sidspårningskod {#adding-page-tracker-code}

Du lägger till sidspårningskoden i sidhuvudsavsnittet i webbplatskoden. I följande kodutdrag visas den sidspårningskod som finns på en exempelwebbsida:

```xml
 <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc/clientlibs/foundation/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in millis
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","abc.net","bee","list1","eVar3","event8","event7");
            </script>

 </head>
```

## Lägg till inbäddningskod {#add-embed-code}

Du lägger till inbäddningskoden i webbplatskoden. I följande kodfragment visas den inbäddade koden som finns på en exempelwebbsida:

```xml
<body>

      <img
            src="http://localhost:4502/xxxx/content/dam/test/xyz.jpg"
            data-aem-asset-id="aaid:a386f2cd78234becb66bd11575f9452d"
            data-trackable=true
            onload=assetAnalytics.core.assetLoaded(this)>

        <a
            href="https://www.adobe.com"

            onclick="assetAnalytics.core.assetClicked(this);return false">
           <img
                    src="http://localhost:4502/xxxx/content/dam/test/xyz.jpg"
                    data-aem-asset-id="aaid:7fa01fce0ebe40268cd6dcf07e2d9cb1"
                    data-trackable=true
                    onload=assetAnalytics.core.assetLoaded(this)>
        </a>

    </body>
```
