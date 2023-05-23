---
title: Anpassa sidor som visas av felhanteraren
seo-title: Customizing Pages shown by the Error Handler
description: AEM levereras med en standardfelhanterare för hantering av HTTP-fel
seo-description: AEM comes with a standard error handler for handling HTTP errors
uuid: aaf940fd-e428-4c7c-af7f-88b1d02c17c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 63c94c82-ed96-4d10-b645-227fa3c09f4b
exl-id: d6745baa-44da-45dd-b5d5-a9b218e7e8cf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---

# Anpassa sidor som visas av felhanteraren{#customizing-pages-shown-by-the-error-handler}

AEM har en standardfelhanterare för hantering av HTTP-fel. genom att till exempel visa:

![chlimage_1-67](assets/chlimage_1-67a.png)

Systemskript finns (under `/libs/sling/servlet/errorhandler`) för att svara på felkoder är som standard följande tillgängligt med en CQ-standardinstans:

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM baseras på Apache Sling, så se [https://sling.apache.org/site/errorhandling.html](https://sling.apache.org/site/errorhandling.html) om du vill ha mer information om felhantering vid körning.

>[!NOTE]
>
>På en författarinstans [CQ WCM-felsökningsfilter](/help/sites-deploying/osgi-configuration-settings.md) är aktiverat som standard. Detta resulterar alltid i svarskoden 200. Standardfelhanteraren svarar genom att skriva den fullständiga stackspårningen till svaret.
>
>I en publiceringsinstans är CQ WCM-felsökningsfiltret *alltid* inaktiverat (även om det har konfigurerats som aktiverat).

## Anpassa sidor som visas av felhanteraren {#how-to-customize-pages-shown-by-the-error-handler}

Du kan utveckla egna skript för att anpassa sidorna som visas i felhanteraren när ett fel inträffar. Dina anpassade sidor skapas under `/apps` och täcka över standardsidorna (som finns under `/libs`).

>[!NOTE]
>
>Se [Använda övertäckningar](/help/sites-developing/overlays.md) för mer information.

1. Kopiera standardskripten i databasen:

   * från `/libs/sling/servlet/errorhandler/`
   * till `/apps/sling/servlet/errorhandler/`

   Eftersom målsökvägen inte finns som standard måste du skapa den första gången.

1. Navigera till `/apps/sling/servlet/errorhandler`. Här kan du antingen:

   * redigera lämpligt skript för att ge den information som behövs.
   * skapa och redigera ett nytt skript för den kod som behövs.

1. Spara ändringarna och testa.

>[!CAUTION]
>
>Hanterarna 404.jsp och 403.jsp har utformats särskilt för att hantera CQ5-autentisering. särskilt för att möjliggöra systeminloggning vid dessa fel.
>
>Därför bör dessa två hanterare bytas ut med stor försiktighet.

### Anpassa svaret till HTTP 500-fel {#customizing-the-response-to-http-errors}

HTTP 500-fel orsakas av serversidans undantag.

* **[500 internt serverfel](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**
Servern påträffade ett oväntat tillstånd som gjorde att den inte kunde slutföra begäran.

När bearbetningen av en begäran resulterar i ett undantag, är Apache Sling-ramverket (som AEM är inbyggt i):

* loggar undantaget
* returnerar:

   * HTTP-svarskod 500
   * stackspårning för undantag

   i svarets brödtext.

Av [anpassa de sidor som visas i felhanteraren](#how-to-customize-pages-shown-by-the-error-handler) a `500.jsp` kan skapas. Det används dock bara om `HttpServletResponse.sendError(500)` exekveras uttryckligen, d.v.s. från en undantagskatalog.

Annars är svarskoden inställd på 500, men `500.jsp` skriptet körs inte.

Om du vill hantera 500 fel måste filnamnet för felhanterarskriptet vara detsamma som undantagsklassen (eller superklassen). Om du vill hantera alla sådana undantag kan du skapa ett skript `/apps/sling/servlet/errorhandler/Throwable.js`p eller `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!CAUTION]
>
>På en författarinstans [CQ WCM-felsökningsfilter](/help/sites-deploying/osgi-configuration-settings.md) är aktiverat som standard. Detta resulterar alltid i svarskoden 200. Standardfelhanteraren svarar genom att skriva den fullständiga stackspårningen till svaret.
>
>För en anpassad felhanterare behövs svar med koden 500, så [CQ WCM Debug Filter måste inaktiveras](/help/sites-deploying/osgi-configuration-settings.md). Detta garanterar att svarskoden 500 returneras, vilket i sin tur utlöser rätt Sling-felhanterare.
>
>I en publiceringsinstans är CQ WCM-felsökningsfiltret *alltid* inaktiverat (även om det har konfigurerats som aktiverat).
