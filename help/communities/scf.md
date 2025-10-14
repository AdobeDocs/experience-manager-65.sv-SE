---
title: Ramverk för sociala komponenter
description: Det sociala ramverket (SCF) förenklar processen att konfigurera, anpassa och utöka webbgruppskomponenter
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 5ca58bc3-8505-4d91-9cd1-6b2e2671f1be
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1478'
ht-degree: 0%

---

# Ramverk för sociala komponenter {#social-component-framework}

Det sociala ramverket (SCF) förenklar processen att konfigurera, anpassa och utöka webbgruppskomponenter på både server- och klientsidan.

Fördelarna med ramverket:

* **Funktion**: Enkel integrering med små eller inga anpassningar för 80 % av användningsfallen.
* **Kan skalas**: Konsekvent användning av HTML-attribut för CSS-format.
* **Utbyggbar**: Komponentimplementeringen är objektorienterad och har ljus på affärslogiken - enkel att lägga till inkrementell företagsinloggning på servern.
* **Flexibel**: Enkla, logiklösa JavaScript-mallar som är enkla att täcka över och anpassa.
* **Tillgänglig**: HTTP-API:t stöder publicering från alla klienter, inklusive mobilappar.
* **Portable**: Integrera/bädda in på en webbsida som bygger på valfri teknik.

Utforska en författare eller publicera en instans med hjälp av den interaktiva [communitykomponentguiden](components-guide.md).

## Ökning {#overview}

I SCF består en komponent av en SocialComponent POJO, en Handlebars JS-mall (som återger komponenten) och CSS (som formaterar komponenten).

JS-mallar för handtag kan utöka JS-komponenterna för modell/vy för att hantera användarinteraktion med komponenten på klienten.

Om en komponent måste ha stöd för dataändringar kan implementeringen av API:t för SocialComponent skrivas för att ge stöd för redigering/sparande av data som liknar modell-/dataobjekt i traditionella webbprogram. Dessutom kan operationer (kontrollanter) och en åtgärdstjänst läggas till för att hantera operationsbegäranden, utföra affärslogik och anropa API:erna för modell-/dataobjekten.

SocialComponent-API:t kan utökas för att tillhandahålla data som krävs av en klient för ett visningslager eller en HTTP-klient.

### Hur sidor återges för klienten {#how-pages-are-rendered-for-client}

![scf-page-rendering](assets/scf-overview.png)

### Komponentanpassning och tillägg {#component-customization-and-extension}

Om du vill anpassa eller utöka komponenterna skriver du bara övertäckningar och tillägg till din /apps-katalog, vilket förenklar uppgraderingen till framtida versioner.

* För skal:
   * Endast [CSS behöver redigeras](client-customize.md#skinning-css).
* För Look and Feel:
   * Ändra JS-mallen och CSS.
* För Look, Feel och UX:
   * Ändra JS-mallen, CSS och [utöka/åsidosätt JavaScript](client-customize.md#extending-javascript).
* Så här ändrar du informationen som är tillgänglig för JS-mallen eller för GETENS slutpunkt:
   * Utöka [SocialComponent](server-customize.md#socialcomponent-interface).
* Så här lägger du till anpassad bearbetning under åtgärder:
   * Skriv ett [OperationExtension](server-customize.md#operationextension-class).
* Så här lägger du till en anpassad åtgärd:
   * Skapa en [Sling Post-åtgärd](server-customize.md#postoperation-class).
   * Använd befintliga [OperationServices](server-customize.md#operationservice-class) efter behov.
   * Lägg till JavaScript-kod för att anropa åtgärden från klientsidan efter behov.

## Serverside Framework {#server-side-framework}

Ramverket innehåller API:er för att komma åt funktioner på servern och stödja interaktion mellan klienten och servern.

### Java™-API:er {#java-apis}

Java™-API:erna innehåller abstrakta klasser och gränssnitt som är enkla att ärva eller gruppera.

Huvudklasserna beskrivs på sidan [Anpassning på serversidan](server-customize.md).

Gå till [Översikt över lagringsresursprovidern](srp.md) om du vill veta mer om hur du arbetar med UGC.

### HTTP-API {#http-api}

HTTP-API:t har stöd för enkel anpassning och val av klientplattformar för PhoneGap-appar, inbyggda appar och andra integreringar och mashups. Dessutom gör HTTP API det möjligt för en community-webbplats att köras som en tjänst utan en klient, så att ramverkskomponenter kan integreras i alla webbsidor som bygger på valfri teknik.

### HTTP API - GET-begäranden {#http-api-get-requests}

För varje SocialComponent tillhandahåller ramverket en HTTP-baserad API-slutpunkt. Slutpunkten nås genom att en GET-begäran skickas till resursen med väljaren .social.json + tillägget. Med Sling skickas begäran till `DefaultSocialGetServlet`.

**`DefaultSocialGetServlet`**

1. Skickar resursen (resourceType) till `SocialComponentFactoryManager` och tar emot en SocialComponentFactory som kan välja en `SocialComponent` som representerar resursen.

1. Anropar fabriken och tar emot en `SocialComponent` som kan hantera resursen och begäran.
1. Anropar `SocialComponent` som bearbetar begäran och returnerar en JSON-representation av resultaten.
1. Returnerar JSON-svaret till klienten.

**`GET Request`**

En standardserver för GET lyssnar på .social.json-begäranden som SocialComponent svarar på med anpassningsbar JSON.

![scf-framework](assets/scf-framework.png)

### HTTP API - POST-begäranden {#http-api-post-requests}

Förutom åtgärderna GET (Läs) definierar ramverket ett slutpunktsmönster som möjliggör andra åtgärder för en komponent, inklusive Skapa, Uppdatera och Ta bort. Dessa slutpunkter är HTTP-API:er som accepterar indata och svarar med antingen en HTTP-statuskod eller med ett JSON-svarsobjekt.

Det här ramverkets slutpunktsmönster gör CUD-åtgärder utökningsbara, återanvändbara och testbara.

**`POST Request`**

Det finns en Sling-POST:åtgärd för alla SocialComponent-åtgärder. Affärslogik och underhållskod för varje åtgärd omsluts av en OperationService som är tillgänglig via HTTP-API:t eller någon annanstans som en OSGi-tjänst. Det finns kopplingar med stöd för utökningar av anslutningsbara åtgärder för åtgärder före/efter.

![scf-post-request](assets/scf-post-request.png)

### Lagringsresursleverantör (SRP) {#storage-resource-provider-srp}

Mer information om hur du hanterar UGC som lagras i [community-innehållslagringen](working-with-srp.md) finns i:

* [Lagringsresursprovideröversikt](srp.md) - Översikt över introduktion och databasanvändning.
* [SRP och UGC Essentials](srp-and-ugc.md) - Verktygsmetoder och exempel för SRP API.
* [Åtkomst till UGC med SRP](accessing-ugc-with-srp.md) - riktlinjer för kodning.

### Anpassningar på serversidan {#server-side-customizations}

Besök [Anpassningar på serversidan](server-customize.md) om du vill ha information om hur du anpassar affärslogiken och beteendet för en Communities-komponent på serversidan.

## Hanterarfält - språk för JS-mallar {#handlebars-js-templating-language}

En av de mer märkbara förändringarna i det nya ramverket är användningen av mallspråket `Handlebars JS` (HBS), en populär öppen källkod-teknik för server-klientåtergivning.

HBS-skript är enkla, logikfria, kompilerade på både server och klient, är enkla att överlagra och anpassa och binds naturligt med klientens användargränssnitt eftersom HBS stöder rendering på klientsidan.

Ramverket innehåller flera [Handlebars-hjälpredor](handlebars-helpers.md) som är användbara vid utveckling av SocialComponents.

När Sling löser en GET-begäran på servern identifieras det skript som används för att svara på begäran. Om skriptet är en HBS-mall (.hbs) delegerar Sling begäran till Handlebars Engine. Handlebars Engine hämtar sedan SocialComponent från lämplig SocialComponentFactory, skapar en kontext och återger HTML.

### Ingen åtkomstbegränsning {#no-access-restriction}

HBS-mallfiler (Handlebars) (.hbs) är detsamma som .jsp- och .html-mallfiler, förutom att de kan användas för återgivning både i klientwebbläsaren och på servern. En klientwebbläsare som begär en klientmall får därför en .hbs-fil från servern.

Detta kräver att alla HBS-mallar i den sling-söksökvägen (alla HBS-filer under /libs/ eller /apps) kan hämtas av alla användare från författaren eller publiceringen.

HTTP-åtkomst till HBS-filer är inte förbjuden.

### Lägg till eller inkludera en webbgruppskomponent {#add-or-include-a-communities-component}

De flesta Communities-komponenter måste vara *tillagda* som en Sling-adresserbar resurs. Ett urval av Communities-komponenter kan *inkluderas* i en mall som en icke-befintlig resurs för att möjliggöra dynamisk inkludering och anpassning av den plats där användargenererat innehåll (UGC) ska skrivas.

I båda fallen måste komponentens [nödvändiga klientbibliotek](clientlibs.md) också finnas.

**Lägg till en komponent**

Att lägga till en komponent innebär att lägga till en instans av en resurs (komponent), till exempel när den dras från komponentens webbläsare (sidospark) till en sida i redigeringsläget för författare.

Resultatet är en underordnad JCR-nod under en par-nod, som är Sling-adresserbar.

**Inkludera en komponent**

Att ta med en komponent hänvisar till processen att lägga till en referens till en [&quot;icke-befintlig&quot; resurs &#x200B;](srp.md#for-non-existing-resources-ners) (ingen JCR-nod) i mallen, till exempel med ett skriptspråk.

Från och med Adobe Experience Manager (AEM) 6.1 går det att redigera komponentens egenskaper i *designläge* när en komponent inkluderas dynamiskt i stället för att läggas till.

Endast ett fåtal av AEM Communities-komponenterna kan inkluderas dynamiskt. De är:

* [Kommentar](essentials-comments.md)
* [Klassificering](rating-basics.md)
* [Recensioner](reviews-basics.md)
* [Omröstning](essentials-voting.md)

I [Community Components Guide](components-guide.md) kan inkluderande komponenter växlas från att läggas till till till att inkluderas.

**När du använder hanterarfält** för att malla språk inkluderas den icke-befintliga resursen med hjälp av [include-hjälpen](handlebars-helpers.md#include) genom att ange dess resourceType:

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**När du använder JSP** inkluderas en resurs med taggen [cq:include](../../help/sites-developing/taglib.md#lt-cq-include):

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>Mer information om hur du lägger till en komponent på en sida dynamiskt, i stället för att lägga till eller ta med den i en mall, finns i [Komponentsidinläsning](sideloading.md).

### Handtag {#handlebars-helpers}

I [SCF Handlebars Helpers](handlebars-helpers.md) finns en lista och en beskrivning av anpassade hjälpprogram som är tillgängliga i SCF.

## Klientbaserat ramverk {#client-side-framework}

### Model-View JavaScript Framework {#model-view-javascript-framework}

Ramverket innehåller ett tillägg till [Backbone.js](https://backbonejs.org/), ett JavaScript-ramverk för modellvisning, som underlättar utvecklingen av avancerade, interaktiva komponenter. Den objektorienterade naturen har stöd för ett utbyggbart/återanvändbart ramverk. Kommunikationen mellan klient och server förenklas med HTTP API.

I ramverket används hanterarmallar på serversidan för att återge komponenterna för klienten. Modellerna baseras på JSON-svar som genereras av HTTP API. Vyerna binder sig till HTML som genereras av Handlebars-mallarna och ger interaktivitet.

### CSS-konventioner {#css-conventions}

Följande är rekommenderade konventioner för att definiera och använda CSS-klasser:

* Använd CSS-klassväljarnamn med tydligt namn och undvik generiska namn som heading och image.
* Definiera specifika klassväljarformat så att CSS-formatmallarna fungerar bra med andra element och format på sidan. Till exempel: `.social-forum .topic-list .li { color: blue; }`
* Håll CSS-klasser för formatering åtskilda från CSS-klasser för UX som drivs av JavaScript.

### Anpassningar på klientsidan {#client-side-customizations}

Om du vill anpassa utseendet och beteendet för en webbgruppskomponent på klientsidan, ska du läsa [Anpassningar på klientsidan](client-customize.md), som innehåller information om:

* [Övertäckningar](client-customize.md#overlays)
* [Tillägg](client-customize.md#extensions)
* [HTML Markup](client-customize.md#htmlmarkup)
* [CSS-skal](client-customize.md#skinning-css)
* [Utöka JavaScript](client-customize.md#extending-javascript)
* [Clientlibs for SCF](client-customize.md#clientlibs-for-scf)

## Grundläggande funktioner och komponenter {#feature-and-component-essentials}

Viktig information för utvecklare beskrivs i avsnittet [Funktions- och Component Essentials](essentials.md).

Ytterligare utvecklarinformation finns i avsnittet [Kodningsriktlinjer](code-guide.md).

## Felsökning {#troubleshooting}

Vanliga problem och kända problem beskrivs i avsnittet [Felsökning](troubleshooting.md).
