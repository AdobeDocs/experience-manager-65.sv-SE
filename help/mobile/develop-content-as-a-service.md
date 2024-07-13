---
title: Innehållsleverans
description: Lär dig hur du använder allt innehåll i Adobe Experience Manager för att leverera en målinriktad appupplevelse.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 85e73679-684e-402f-8186-8b56d8bd9372
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 1%

---

# Innehållsleverans{#content-delivery}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

Mobilappar bör kunna använda allt innehåll i AEM efter behov för att leverera målinriktade appupplevelser.

Detta inkluderar användning av resurser, webbplatsinnehåll, CAAS-innehåll (over-the-air) och anpassat innehåll som kan ha en egen struktur.

>[!NOTE]
>
>**Innehåll som ligger över AIR** kan komma från något av ovanstående via ContentSync-hanterare. Den kan användas för att batchpaketera och leverera i form av zips och underhålla uppdateringar för dessa paket.

Det finns tre huvudtyper av material som Content Services levererar:

1. **Assets**
1. **Paketerat HTML-innehåll (HTML/CSS/JS)**
1. **Kanaloberoende innehåll**

![chlimage_1-154](assets/chlimage_1-154.png)

## Assets {#assets}

Resurssamlingar är AEM som innehåller referenser till andra samlingar.

En resurssamling kan visas via innehållstjänster. När en resurssamling anropas i en begäran returneras ett objekt som är en lista över resurserna, inklusive deras URL:er. Assets nås via en URL. URL:en anges i ett objekt. Till exempel:

* En sidenhet returnerar JSON (sidobjekt) som innehåller en bildreferens. Bildreferensen är en URL som används för att hämta resursens binärfil för bilden.
* En begäran om en lista med resurser i en mapp returnerar JSON med information om alla enheter i den mappen. Listan är ett objekt. JSON har URL-referenser som används för att hämta resursens binärfil för varje resurs i den mappen.

### Optimering av tillgångar {#asset-optimization}

Ett viktigt värde för Content Services är möjligheten att returnera resurser som är optimerade för enheten. Detta minskar behovet av lagring på lokala enheter och förbättrar appprestanda.

Resursoptimering är en funktion på serversidan som baseras på information som anges i API-begäran. Där det är möjligt bör resursåtergivningarna cachelagras så att liknande förfrågningar inte kräver omgenerering av resursåtergivningen.

### Assets Workflow {#assets-workflow}

Resursarbetsflödet är följande:

1. Resursreferens finns i AEM
1. Skapa en resursreferensenhet utifrån dess modell
1. Redigera entitet

   1. Välj en tillgång eller en tillgångssamling
   1. Anpassa JSON-återgivning

I följande diagram visas **Assets Reference Workflow**:

![chlimage_1-155](assets/chlimage_1-155.png)

### Hantera Assets {#managing-assets}

Content Services ger åtkomst till AEM resurser som inte kan refereras via annat AEM.

#### Befintliga hanterade Assets {#existing-managed-assets}

En användare av AEM Sites och Assets använder AEM Assets för att hantera allt digitalt material för alla kanaler. De utvecklar en intern mobilapp och måste använda flera resurser som hanteras av AEM Assets. Till exempel logotyper, bakgrundsbilder och knappikoner.

Dessa är för närvarande spridda runt Assets-databasen. De filer som programmet måste referera till finns i följande:

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/gray_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### Åtkomst till CS-resursenheter {#accessing-cs-asset-entities}

Låt oss lägga undan stegen för hur sidan görs tillgänglig via API:t för tillfället (den omfattas av AEM gränssnittsbeskrivning) och anta att den har gjorts. Resursenheter har skapats och lagts till i utrymmet&quot;appImages&quot;. Ytterligare mappar skapades under utrymmet för organisationssyften. Resursenheterna lagras i AEM JCR som:

* /content/entities/appImages/logos/logo_light
* /content/entities/appImages/logos/logo_dark
* /content/entities/appImages/bkgnd/gray_blue
* /content/entities/appImages/icons/cart
* /content/entities/appImages/icons/home

#### Hämta en lista med tillgängliga resursenheter {#getting-a-list-of-available-asset-entities}

En apputvecklare kan få en lista över vilka resurser som är tillgängliga genom att hämta resursenheter. Slutpunkten för Content Services space kan tillhandahålla den informationen via webbtjänstens API SDK.

Resultatet blir ett objekt i JSON-format som ger en lista över resurserna i mappen&quot;icons&quot;.

![chlimage_1-156](assets/chlimage_1-156.png)

#### Hämta en bild {#getting-an-image}

JSON tillhandahåller en URL för varje bild som genereras av Content Services till bilden.

Klientbiblioteket används en gång till för att hämta binärfilen för kundvagnsbilden.

## Paketerat HTML-innehåll {#packaged-html-content}

HTML-innehåll behövs för kunder som måste behålla innehållets layout. Detta är användbart för inbyggda program som använder en webbbehållare, till exempel en Cordova-webbvy, för att visa innehållet.

AEM Content Services förser mobilappen med HTML via API:t. Kunder som vill visa AEM innehåll som HTML kan skapa en HTML-sidenhet som pekar mot AEM innehållskälla.

Följande alternativ beaktas:

* **Zip-fil:** Om du vill ha den bästa möjligheten att visas korrekt på enheten, inkluderas sidans refererade material-css, JavaScript, resurser och så vidare i en enda komprimerad fil med svaret. Referenserna på HTML-sidan kan justeras så att en relativ sökväg till dessa filer används.
* **Direktuppspelning:** Hämtar ett manifest med nödvändiga filer från AEM. Använd sedan det manifestet för att begära alla filer (HTML, CSS, JS o.s.v.) med efterföljande begäranden.

![chlimage_1-157](assets/chlimage_1-157.png)

## Kanaloberoende innehåll {#channel-independent-content}

Kanaloberoende innehåll är ett sätt att exponera AEM innehållskonstruktioner - t.ex. sidor - utan att behöva bekymra sig om layout, komponenter eller annan kanalspecifik information.

Dessa innehållsenheter genereras med en innehållsmodell för att översätta de AEM strukturerna till ett JSON-format. Resulterande JSON-data innehåller information om innehållets data som är frikopplade från AEM. Detta innefattar att returnera metadata och AEM referenslänkar till resurser och relationer mellan innehållsstrukturer - inklusive entitetshierarki.

### Hantera kanaloberoende innehåll {#managing-channel-independent-content}

Innehåll kan komma åt appen på flera sätt.

1. GET-innehåll ZIPS genom AEM:s luftburet

   * Hanterare för innehållssynkronisering kan uppdatera zip-paketet direkt eller genom att anropa befintliga innehållsrenderare

      * Platshanterare
      * AEM
      * Anpassade hanterare

1. GET material direkt via innehållsrenderare

   * Körklara standardåtergivningsprogram
   * AEM Mobile/Content Services Content Renderers
   * Anpassade återgivningar
