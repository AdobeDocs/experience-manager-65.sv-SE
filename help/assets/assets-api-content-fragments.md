---
title: Stöd för Content Fragments i AEM Assets HTTP API
seo-title: Stöd för Content Fragments i AEM Assets HTTP API
description: Läs mer om stöd för innehållsfragment i AEM Assets HTTP API.
seo-description: Läs mer om stöd för innehållsfragment i AEM Assets HTTP API.
uuid: c500d71e-ceee-493a-9e4d-7016745c544c
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: extending-assets
discoiquuid: 03502b41-b448-47ab-9729-e0a66a3389fa
docset: aem65
feature: Innehållsfragment
role: User, Admin
exl-id: 0f9efb47-a8d1-46d9-b3ff-a6c0741ca138
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1861'
ht-degree: 2%

---

# Stöd för Content Fragments i AEM Assets HTTP API{#content-fragments-support-in-aem-assets-http-api}

## Översikt {#overview}

>[!NOTE]
>
>[Resursens HTTP API](/help/assets/mac-api-assets.md) omfattar:
>
>* Resurser REST API
>* inklusive stöd för innehållsfragment

>
>
Den aktuella implementeringen av AEM Assets HTTP API är REST.

Med Adobe Experience Manager (AEM) [Assets REST API](/help/assets/mac-api-assets.md) kan utvecklare komma åt innehåll (som lagras i AEM) direkt via HTTP API, via CRUD-åtgärder (Create, Read, Update, Delete).

Med API:t kan du använda AEM som headless CMS (Content Management System) genom att tillhandahålla Content Services till ett JavaScript-klientprogram. Eller något annat program som kan köra HTTP-begäranden och hantera JSON-svar.

Enkelsidiga program (SPA), ramverksbaserade eller anpassade, kräver till exempel innehåll som tillhandahålls via HTTP API, ofta i JSON-format.

AEM Core Components har ett mycket omfattande, flexibelt och anpassningsbart API som kan hantera de nödvändiga läsåtgärderna i detta syfte, och vars JSON-utdata kan anpassas, men kräver AEM WCM-kunskaper (Web Content Management) för implementering eftersom de måste finnas på API-sidor som baseras på dedikerade AEM. Alla SPA har inte tillgång till sådana resurser.

Detta är när REST API:t för resurser kan användas. Med den kan utvecklare komma åt resurser (till exempel bilder och innehållsfragment) direkt, utan att först behöva bädda in dem på en sida, och leverera innehållet i serialiserat JSON-format. (Observera att det inte går att anpassa JSON-utdata från Resurser REST API). Med Assets REST API kan utvecklare ändra innehåll genom att skapa nya, uppdatera eller ta bort befintliga resurser, innehållsfragment och mappar.

Resursens REST API:

* följer [HATEOAS-principen](https://en.wikipedia.org/wiki/HATEOAS)

* implementerar [SIREN-format](https://github.com/kevinswiber/siren)

## Förutsättningar {#prerequisites}

Resursens REST API är tillgängligt för varje körklar installation av en nyligen AEM version.

## Viktiga begrepp {#key-concepts}

Resursens REST API ger [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)-åtkomst till resurser som lagras i en AEM. Slutpunkten `/api/assets` används och resursens sökväg krävs för att komma åt den (utan inledande `/content/dam`).

HTTP-metoden avgör vilken åtgärd som ska utföras:

* **GET**  - för att hämta en JSON-representation av en resurs eller en mapp
* **POST**  - för att skapa nya resurser eller mappar
* **PUT** - för att uppdatera egenskaperna för en resurs eller mapp
* **DELETE** - för att ta bort en resurs eller mapp

>[!NOTE]
>
>Begärandetexten och/eller URL-parametrarna kan användas för att konfigurera vissa av dessa åtgärder. Ange till exempel att en mapp eller en resurs ska skapas med en **POST**-begäran.

Det exakta formatet för begäranden som stöds definieras i [API Reference](/help/assets/assets-api-content-fragments.md#api-reference)-dokumentationen.

### Transaktionsbeteende {#transactional-behavior}

Alla förfrågningar är atomiska.

Det innebär att efterföljande (`write`)-begäranden inte kan kombineras till en enda transaktion som kan lyckas eller misslyckas som en enskild enhet.

### AEM (Resurser) REST API jämfört med AEM komponenter {#aem-assets-rest-api-versus-aem-components}

<table>
 <tbody>
  <tr>
   <td>Proportioner</td>
   <td>Resurser REST API<br /> </td>
   <td>AEM<br /> (komponenter med Sling Models)</td>
  </tr>
  <tr>
   <td>Användningsfall som stöds</td>
   <td>Allmänt syfte.</td>
   <td><p>Optimerad för konsumtion i ett Single Page-program (SPA) eller i något annat (innehållsförbrukande) sammanhang.</p> <p>Kan även innehålla layoutinformation.</p> </td>
  </tr>
  <tr>
   <td>Åtgärder som stöds</td>
   <td><p>Skapa, läsa, uppdatera, ta bort.</p> <p>Med ytterligare åtgärder beroende på enhetstyp.</p> </td>
   <td>Skrivskyddad.</td>
  </tr>
  <tr>
   <td>Åtkomst</td>
   <td><p>Kan nås direkt.</p> <p>Använder <code>/api/assets </code>slutpunkten, mappad till <code>/content/dam</code> (i databasen).</p> <p>Till exempel för att få åtkomst till:<code class="code">
       /content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten</code><br />-begäran:<br /> <code>/api/assets/we-retail/en/experiences/arctic-surfing-in-lofoten.model.json</code></p> </td>
   <td><p>Måste refereras via en AEM på en AEM.</p> <p>Använder <code>.model</code>-väljaren för att skapa JSON-representationen.</p> <p>En exempel-URL skulle se ut så här:<br /> <code>https://localhost:4502/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.model.json</code></p> </td>
  </tr>
  <tr>
   <td>Dokumentskydd</td>
   <td><p>Flera alternativ är möjliga.</p> <p>OAuth föreslås. kan konfigureras separat från standardinställningarna.</p> </td>
   <td>Använder AEM standardinställningar.</td>
  </tr>
  <tr>
   <td>Arkitektur</td>
   <td><p>Skrivåtkomst avser vanligtvis en författarinstans.</p> <p>Läsningen kan även dirigeras till en publiceringsinstans.</p> </td>
   <td>Eftersom det här arbetssättet är skrivskyddat används det vanligtvis för publiceringsinstanser.</td>
  </tr>
  <tr>
   <td>Utdata</td>
   <td>JSON-baserade SIREN-utdata: mycket, men kraftfullt. Tillåter navigering i innehållet.</td>
   <td>JSON-baserade egna produkter. som kan konfigureras med Sling Models. Att navigera i innehållsstrukturen är svårt att implementera (men inte nödvändigtvis omöjligt).</td>
  </tr>
 </tbody>
</table>

### Dokumentskydd {#security}

Om REST API:t för Resurser används i en miljö utan särskilda autentiseringskrav måste AEM CORS-filtret konfigureras korrekt.

>[!NOTE]
>
>Mer information finns i:
>
>* [CORS/AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
>* [Video - Utveckla för CORS med AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)

>



I miljöer med specifika autentiseringskrav rekommenderas OAuth.

## Tillgängliga funktioner {#available-features}

Innehållsfragment är en specifik typ av resurs, se [Arbeta med innehållsfragment](/help/assets/content-fragments/content-fragments.md).

Mer information om funktioner som är tillgängliga via API finns i:

* [Tillgängliga funktioner ](/help/assets/mac-api-assets.md#assets) för REST API:t för resurser
* [Enhetstyper](/help/assets/assets-api-content-fragments.md#entity-types)

### Sidindelning {#paging}

Resursens REST API stöder sidindelning (för GET-begäranden) via URL-parametrarna:

* `offset` - numret på den första (underordnade) entiteten som ska hämtas
* `limit` - det maximala antalet returnerade enheter

Svaret kommer att innehålla växlingsinformation som en del av `properties`-avsnittet i SIREN-utdata. Den här `srn:paging`-egenskapen innehåller det totala antalet (underordnade) entiteter ( `total`), förskjutningen och gränsen ( `offset`, `limit`) som anges i begäran.

>[!NOTE]
>
>Sidindelning används vanligtvis för behållarentiteter (d.v.s. mappar eller resurser med återgivningar), eftersom det relaterar till den begärda entitetens underordnade.

#### Exempel: Sidindelning {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```
...
"properties": {
    ...
    "srn:paging": {
        "total": 7,
        "offset": 2,
        "limit": 3
    }
    ...
}
...
```

## Enhetstyper {#entity-types}

### Mappar {#folders}

Mappar fungerar som behållare för resurser och andra mappar. De återspeglar strukturen i AEM innehållsdatabas.

Resursens REST API ger åtkomst till en mapps egenskaper. till exempel namn, titel osv. Resurser visas som underordnade enheter till mappar.

>[!NOTE]
>
>Beroende på resurstypen kan listan med underordnade enheter redan innehålla den fullständiga uppsättningen egenskaper som definierar respektive underordnade enhet. Alternativt kan bara en reducerad uppsättning egenskaper visas för en enhet i den här listan över underordnade enheter.

### Assets {#assets}

Om en resurs begärs returneras dess metadata. som titel, namn och annan information som definieras i respektive resursschema.

Den binära informationen för en resurs visas som en SIREN-länk av typen `content` (kallas även `rel attribute`).

Resurser kan ha flera renderingar. Dessa visas vanligtvis som underordnade enheter, ett undantag är en miniatyrrendering som visas som en länk av typen `thumbnail` ( `rel="thumbnail"`).

### Innehållsfragment {#content-fragments}

Ett [innehållsfragment](/help/assets/content-fragments/content-fragments.md) är en speciell typ av resurs. De kan användas för att komma åt strukturerade data, t.ex. texter, siffror och datum.

Eftersom det finns flera skillnader mellan *standardobjekt*-resurser (t.ex. bilder eller ljud) gäller vissa ytterligare regler för att hantera dem.

#### Representation {#representation}

Innehållsfragment:

* Visa inga binära data.
* Finns helt i JSON-utdata (inom egenskapen `properties`).

* betraktas också som atomiska, dvs. elementen och variationerna exponeras som en del av fragmentets egenskaper jämfört med som länkar eller underordnade enheter. Detta ger effektiv åtkomst till nyttolasten för ett fragment.

#### Innehållsmodeller och innehållsfragment {#content-models-and-content-fragments}

För närvarande visas inte modellerna som definierar strukturen för ett innehållsfragment via ett HTTP-API. Därför måste *konsumenten* känna till modellen för ett fragment (åtminstone ett minimum), även om den mesta informationen kan härledas från nyttolasten. som datatyper, osv. är en del av definitionen.

Om du vill skapa ett nytt innehållsfragment måste sökvägen (intern databas) anges.

#### Associerat innehåll {#associated-content}

Associerat innehåll visas för närvarande inte.

## Använda {#using}

Användningen kan variera beroende på om du använder en AEM författare eller publiceringsmiljö, tillsammans med ditt specifika användningsexempel.

* Skapandet är strikt bundet till en författarinstans ([och det finns för närvarande inget sätt att replikera ett fragment för publicering med denna API](/help/assets/assets-api-content-fragments.md#limitations)).
* Leverans är möjlig från båda, eftersom AEM endast skickar begärt innehåll i JSON-format.

   * Lagring och leverans från en AEM författarinstans bör räcka för program som ligger bakom brandväggen och mediabibliotek.
   * För direktwebbleverans rekommenderas en publiceringsinstans AEM.

>[!CAUTION]
>
>Dispatcher-konfigurationen på AEM molninstanser kan blockera åtkomsten till `/api`.

>[!NOTE]
>
>Mer information finns i [API-referens](/help/assets/assets-api-content-fragments.md#api-reference). Speciellt [Adobe Experience Manager Assets API - Content Fragments](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html).

### Läsning/leverans {#read-delivery}

Användning sker via:

`GET /{cfParentPath}/{cfName}.json`

Till exempel:

`https://localhost:4502/api/assets/we-retail/en/experiences/arctic-surfing-in-lofoten.json`

Svaret är serialiserat JSON med innehållet strukturerat som i innehållsfragmentet. Referenser levereras som referens-URL:er.

Det finns två typer av läsåtgärder:

* När du läser ett visst innehållsfragment efter sökväg, returneras JSON-representationen av innehållsfragmentet.
* Läsa en mapp med innehållsfragment efter sökväg: returnerar JSON-representationerna för alla innehållsfragment i mappen.

### Skapa {#create}

Användning sker via:

`POST /{cfParentPath}/{cfName}`

Brödtexten måste innehålla en JSON-representation av det innehållsfragment som ska skapas, inklusive allt ursprungligt innehåll som ska anges för elementen i innehållsfragmentet. Det är obligatoriskt att ange egenskapen `cq:model` och den måste peka på en giltig innehållsfragmentmodell. Om du inte gör det uppstår ett fel. Du måste också lägga till en rubrik `Content-Type` som är inställd på `application/json`.

### Uppdatera {#update}

Användning sker via

`PUT /{cfParentPath}/{cfName}`

Brödtexten måste innehålla en JSON-representation av vad som ska uppdateras för det angivna innehållsfragmentet.

Detta kan helt enkelt vara titeln eller beskrivningen av ett innehållsfragment, ett enskilt element eller alla elementvärden och/eller metadata. Det är också obligatoriskt att ange en giltig `cq:model`-egenskap för uppdateringar.

### Ta bort {#delete}

Användning sker via:

`DELETE /{cfParentPath}/{cfName}`

## Begränsningar {#limitations}

Det finns några begränsningar:

* **Variationer kan inte skrivas och uppdateras.** Om dessa variationer läggs till i en nyttolast (t.ex. för uppdateringar) kommer de att ignoreras. Variationen hanteras dock via leverans ( `GET`).

* **Modeller för innehållsfragment stöds** inte för närvarande: kan inte läsas eller skapas. För att kunna skapa ett nytt, eller uppdatera ett befintligt, innehållsfragment, måste utvecklarna veta rätt sökväg till innehållsfragmentmodellen. För närvarande är det enda sättet att få en översikt över dessa genom administrationsgränssnittet.
* **Referenser ignoreras**. För närvarande finns det inga kontroller för om ett befintligt innehållsfragment refereras. Om du t.ex. tar bort ett innehållsfragment kan det leda till problem på en sida som innehåller en referens.

## Statuskoder och felmeddelanden {#status-codes-and-error-messages}

Följande statuskoder kan ses under de relevanta omständigheterna:

* **200 (OK)**

   Returneras när:

   * begära ett innehållsfragment via `GET`

   * uppdaterar ett innehållsfragment via `PUT`

* **201 (skapad)**

   Returneras när:

   * har skapat ett innehållsfragment via `POST`

* **404 (Hittades inte)**

   Returneras när:

   * det begärda innehållsfragmentet inte finns

* **500 (Internt serverfel)**

   >[!NOTE]
   >
   >Detta fel returneras:
   >
   >
   >
   >    * när ett fel som inte kan identifieras med en viss kod har inträffat
   >    * när den angivna nyttolasten inte var giltig


   I följande exempel visas vanliga scenarier när den här felstatusen returneras, tillsammans med felmeddelandet (monospace) som genereras:

   * Den överordnade mappen finns inte (när du skapar ett innehållsfragment via `POST`)
   * Ingen innehållsfragmentmodell har angetts (null-värde), resursen är null (eventuellt ett behörighetsproblem) eller resursen är ingen giltig fragmentmall:

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`
      * `Cannot adapt the resource '/foo/bar/qux' to a content fragment template`
   * Det gick inte att skapa innehållsfragmentet (eventuellt ett behörighetsproblem):

      * `Could not create content fragment`
   * Titeln och/eller beskrivningen kunde inte uppdateras:

      * `Could not set value on content fragment`
   * Det gick inte att ange metadata:

      * `Could not set metadata on content fragment`
   * Innehållselementet kunde inte hittas eller kunde inte uppdateras

      * `Could not update content element`
      * `Could not update fragment data of element`

   De detaljerade felmeddelandena returneras vanligtvis på följande sätt:

   ```xml
   {
     "class": "core/response",
     "properties": {
       "path": "/api/assets/foo/bar/qux",
       "location": "/api/assets/foo/bar/qux.json",
       "parentLocation": "/api/assets/foo/bar.json",
       "status.code": 500,
       "status.message": "...{error message}.."
     }
   }
   ```

## API-referens {#api-reference}

Här finns detaljerade API-referenser:

* [Adobe Experience Manager Assets API - innehållsfragment](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)
* [HTTP API för Assets](/help/assets/mac-api-assets.md)

   * [Tillgängliga funktioner](/help/assets/mac-api-assets.md#assets)

## Ytterligare resurser {#additional-resources}

Mer information finns i:

* [Resurser för HTTP API-dokumentation](/help/assets/mac-api-assets.md)
* [AEM Gem-session: OAuth](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-oauth-server-functionality-in-aem.html)
