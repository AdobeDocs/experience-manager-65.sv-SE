---
title: Ramverk för sociala komponenter
seo-title: Ramverk för sociala komponenter
description: Det sociala ramverket (SCF) förenklar processen att konfigurera, anpassa och utöka webbgruppskomponenter
seo-description: Det sociala ramverket (SCF) förenklar processen att konfigurera, anpassa och utöka webbgruppskomponenter
uuid: 23b4418d-b91c-46fc-bf42-1154ef79fe5a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d7b5b5e3-2d84-4a6b-bcc2-d490882ff3ed
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Ramverk för sociala komponenter {#social-component-framework}

Det sociala ramverket (SCF) förenklar processen att konfigurera, anpassa och utöka webbgruppskomponenter på både server- och klientsidan.

Fördelarna med ramverket:

* **Funktionell**: Enkel integrering direkt med liten eller ingen anpassning för 80 % av användningsfallen
* **Skalbar**: Enhetlig användning av HTML-attribut för CSS-format
* **Utbyggbart**: Komponentimplementeringen är objektorienterad och lätt utifrån affärslogik - enkel att lägga till inkrementell företagsinloggning på servern
* **Flexibel**: Enkla logikfria javascript-mallar som enkelt kan överlappas och anpassas
* **Tillgänglig**: HTTP-API:t stöder publicering från alla klienter, inklusive mobilappar
* **Portable**: Integrera/bädda in i alla webbsidor som bygger på valfri teknik

Utforska en författare eller publicera en instans med hjälp av handboken [för interaktiva](components-guide.md)communitykomponenter.

## Översikt {#overview}

I SCF består en komponent av en SocialComponent POJO, en hanterarmall för JS (för att återge komponenten) och CSS (för att formatera komponenten).

JS-mallar för handtag kan utöka JS-komponenterna för modell/vy för att hantera användarinteraktion med komponenten på klienten.

Om en komponent behöver stödja ändring av data kan implementeringen av API:t för SocialComponent skrivas för att ge stöd för redigering/sparande av data som liknar modell-/dataobjekt i traditionella webbprogram. Dessutom kan operationer (kontrollanter) och en åtgärdstjänst läggas till för att hantera operationsbegäranden, utföra affärslogik och anropa API:erna för modell-/dataobjekten.

SocialComponent-API:t kan utökas för att tillhandahålla data som krävs av en klient för ett visningslager eller en HTTP-klient.

### Hur sidor återges för klienten {#how-pages-are-rendered-for-client}

![chlimage_1-25](assets/chlimage_1-25.png)

### Komponentanpassning och tillägg {#component-customization-and-extension}

Om du vill anpassa eller utöka komponenterna skriver du bara övertäckningar och tillägg till din /apps-katalog, vilket förenklar uppgraderingen till framtida versioner.

* För skal
   * Endast [CSS behöver redigeras](client-customize.md#skinning-css)
* For Look and Feel
   * Ändra JS-mall och CSS
* For Look, Feel och UX
   * Ändra JS-mallen, CSS och [utöka/åsidosätt JavaScript](client-customize.md#extending-javascript)
* Ändra informationen som är tillgänglig för JS-mallen eller för GET-slutpunkten
   * Utöka [SocialComponent](server-customize.md#socialcomponent-interface)
* Lägga till anpassad bearbetning under åtgärder
   * Skriv en [OperationExtension](server-customize.md#operationextension-class)
* Lägga till en ny anpassad åtgärd
   * Skapa en ny [skickapoståtgärd](server-customize.md#postoperation-class)
   * Använd befintliga [OperationServices](server-customize.md#operationservice-class) efter behov
   * Lägg till JavaScript-kod för att anropa åtgärden från klientsidan efter behov

## Serverside Framework {#server-side-framework}

Ramverket innehåller API:er för att komma åt funktioner på servern och stödja interaktion mellan klienten och servern.

### Java API:er {#java-apis}

Java-API:erna innehåller abstrakta klasser och gränssnitt som enkelt ärvs eller underklassas.

Huvudklasserna beskrivs på sidan [Serveranpassning](server-customize.md) .

Mer information om hur du arbetar med UGC finns i [Lagringsresursprovideröversikt](srp.md) .

### HTTP-API {#http-api}

HTTP-API:t har stöd för enkel anpassning och val av klientplattformar för PhoneGap-appar, inbyggda appar och andra integreringar och mashups. Dessutom gör HTTP API det möjligt för en community-webbplats att köras som en tjänst utan en klient, så att ramverkskomponenter kan integreras i alla webbsidor som bygger på valfri teknik.

### HTTP API - GET-begäranden {#http-api-get-requests}

För varje SocialComponent tillhandahåller ramverket en HTTP-baserad API-slutpunkt. Slutpunkten nås genom att en GET-begäran skickas till resursen med väljaren .social.json + tillägget. Med Sling lämnas begäran till `DefaultSocialGetServlet`.

The `DefaultSocialGetServlet`

1. Skickar resursen (resourceType) till `SocialComponentFactoryManager`och tar emot en SocialComponentFactory som kan välja en `SocialComponent`som representerar resursen.

1. Anropar fabriken och tar emot en `SocialComponent`kapacitet att hantera resursen och begäran.
1. Anropar `SocialComponent`, som bearbetar begäran och returnerar en JSON-representation av resultaten.
1. Returnerar JSON-svaret till klienten.

**`GET Request`**

En GET-standardserver lyssnar på .social.json-begäranden som SocialComponent svarar på med anpassningsbar JSON.

![chlimage_1-26](assets/chlimage_1-26.png)

### HTTP API - POST-begäranden {#http-api-post-requests}

Förutom GET-åtgärder (läsåtgärder) definierar ramverket ett slutpunktsmönster som möjliggör andra åtgärder för en komponent, inklusive Skapa, Uppdatera och Ta bort. Dessa slutpunkter är HTTP-API:er som accepterar indata och svarar med antingen en HTTP-statuskod eller med ett JSON-svarsobjekt.

Det här ramverkets slutpunktsmönster gör CUD-åtgärder utökningsbara, återanvändbara och testbara.

**`POST Request`**

Det finns en Sling POST:operation för varje SocialComponent-åtgärd. Affärslogik och underhållskod för varje åtgärd omsluts av en OperationService som är tillgänglig via HTTP-API:t eller någon annanstans som en OSGi-tjänst. Det finns kopplingar med stöd för utökningar av anslutningsbara åtgärder för åtgärder före/efter.

![chlimage_1-27](assets/chlimage_1-27.png)

### Lagringsresursleverantör (SRP) {#storage-resource-provider-srp}

Mer information om hur du hanterar UGC som lagras i [community-innehållslagringen](working-with-srp.md)finns i

* [Översikt över](srp.md) lagringsresursleverantör - introduktion och databasanvändning - översikt
* [SRP och UGC Essentials](srp-and-ugc.md) - metoder och exempel för SRP API-verktyg
* [Åtkomst till UGC med SRP](accessing-ugc-with-srp.md) - riktlinjer för kodning

### Anpassningar på serversidan {#server-side-customizations}

Besök Anpassningar [på](server-customize.md) serversidan om du vill ha information om hur du anpassar affärslogiken och beteendet för en Communities-komponent på serversidan.

## Hanterarfält - språk för JS-mallar {#handlebars-js-templating-language}

En av de mest märkbara förändringarna i det nya ramverket är användningen av [Handlebars JS-mallspråk (HBS)](https://www.handlebarsjs.com/), en populär öppen källkod-teknik för serverklientåtergivning.

HBS-skript är enkla, logikfria, kompilerade på både server och klient, är enkla att överlagra och anpassa och binds naturligt med klientens användargränssnitt eftersom HBS stöder rendering på klientsidan.

Ramverket innehåller flera [handtag](handlebars-helpers.md) som är användbara när du utvecklar sociala komponenter.

När Sling löser en GET-begäran på servern identifieras skriptet som ska användas för att svara på begäran. Om skriptet är en HBS-mall (.hbs) delegerar Sling begäran till Handlebars Engine. Handlebars Engine hämtar sedan SocialComponent från lämplig SocialComponentFactory, skapar en kontext och återger HTML.

### Ingen åtkomstbegränsning {#no-access-restriction}

HBS-mallfiler (Handlebars) (.hbs) är detsamma som .jsp- och .html-mallfiler, förutom att de kan användas för återgivning både i klientwebbläsaren och på servern. En klientwebbläsare som begär en klientmall får därför en .hbs-fil från servern.

Detta kräver att alla HBS-mallar i sling-söksökvägen (alla HBS-filer under /libs/ eller /apps) kan hämtas av alla användare från författaren eller publiceringen.

HTTP-åtkomst till HBS-filer är inte förbjuden.

### Lägg till eller inkludera en webbgruppskomponent {#add-or-include-a-communities-component}

De flesta communitykomponenter måste *läggas till* som en Sling-adresserbar resurs. Ett urval av Communities-komponenter kan *inkluderas* i en mall som en icke-befintlig resurs för att möjliggöra dynamisk inkludering och anpassning av den plats där användargenererat innehåll (UGC) ska skrivas.

I båda fallen måste komponentens [nödvändiga klientbibliotek](clientlibs.md) också finnas.

**Lägg till en komponent**

Att lägga till en komponent innebär att lägga till en instans av en resurs (komponent), till exempel när den dras från komponentens webbläsare (sidospark) till en sida i redigeringsläget för författare.

Resultatet är en underordnad JCR-nod under en par-nod, som är Sling-adresserbar.

**Inkludera en komponent**

Att inkludera en komponent avser processen att lägga till en referens till en [&quot;icke-befintlig&quot; resurs](srp.md#for-non-existing-resources-ners) (ingen JCR-nod) i mallen, till exempel med hjälp av ett skriptspråk.

Från och med AEM 6.1 går det att redigera komponentens egenskaper i *design *läge när en komponent inkluderas dynamiskt i stället för att läggas till.

Endast ett urval av AEM Communities-komponenterna kan inkluderas dynamiskt. De är:

* [Kommentarer](essentials-comments.md)
* [Klassificering](rating-basics.md)
* [Recensioner](reviews-basics.md)
* [Omröstning](essentials-voting.md)

I [Community Components Guide](components-guide.md) kan man växla mellan att lägga till och inkludera komponenter som inte kan ingå.

**När du använder Handlebars** mallspråk inkluderas den icke-befintliga resursen med hjälp av [Include-hjälpen](handlebars-helpers.md#include) genom att ange dess resourceType:

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**När du använder JSP** inkluderas en resurs med taggen [cq:include](../../help/sites-developing/taglib.md#lt-cq-include):

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>Om du vill lägga till en komponent dynamiskt på en sida, i stället för att lägga till eller ta med den i en mall, läser du [Komponentsidinläsning](sideloading.md).

### Handtag {#handlebars-helpers}

Se [SCF Handlebars Helpers](handlebars-helpers.md) för en lista och en beskrivning av anpassade hjälpredor som finns i SCF.

## Klientbaserat ramverk {#client-side-framework}

### Model-View Javascript Framework {#model-view-javascript-framework}

Ramverket innehåller ett tillägg till [Backbone.js](https://www.backbonejs.org/), ett JavaScript-ramverk för modellvisning, som underlättar utvecklingen av avancerade, interaktiva komponenter. Den objektorienterade naturen har stöd för ett utbyggbart/återanvändbart ramverk. Kommunikationen mellan klient och server förenklas med HTTP API.

Ramverket använder mallar för serversidans handtag för att återge komponenterna för klienten. Modellerna baseras på JSON-svar som genereras av HTTP API. Vyerna binds till HTML som genereras av Handlebars-mallarna och ger interaktivitet.

### CSS-konventioner {#css-conventions}

Följande är rekommenderade konventioner för att definiera och använda CSS-klasser:

* Använd CSS-klassväljarnamn med tydligt namn och undvik generiska namn som heading, image osv.
* Definiera specifika klassväljarformat så att CSS-formatmallarna fungerar bra med andra element och format på sidan. Exempel: `.social-forum .topic-list .li { color: blue; }`
* Håll CSS-klasser för formatering åtskilda från CSS-klasser för UX som drivs av JavaScript

### Anpassningar på klientsidan {#client-side-customizations}

Om du vill anpassa utseendet och beteendet för en webbgruppskomponent på klientsidan kan du läsa Anpassa [klientsidan](client-customize.md), som innehåller information om:

* [Övertäckningar](client-customize.md#overlays)
* [Tillägg](client-customize.md#extensions)
* [HTML-kod](client-customize.md#htmlmarkup)
* [CSS-skal](client-customize.md#skinning-css)
* [Utöka JavaScript](client-customize.md#extending-javascript)
* [Clientlibs for SCF](client-customize.md#clientlibs-for-scf)

## Grundläggande funktioner och komponenter {#feature-and-component-essentials}

Viktig information för utvecklare beskrivs i avsnittet [Funktioner och Component Essentials](essentials.md) .

Ytterligare utvecklarinformation finns i avsnittet [Kodningsriktlinjer](code-guide.md) .

## Felsökning {#troubleshooting}

Vanliga problem och kända problem beskrivs i avsnittet [Felsökning](troubleshooting.md) .

