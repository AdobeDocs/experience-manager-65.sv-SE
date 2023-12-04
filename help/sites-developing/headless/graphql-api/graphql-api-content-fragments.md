---
title: AEM GraphQL API för användning med innehållsfragment
description: Lär dig hur du använder innehållsfragment i Adobe Experience Manager (AEM) med AEM GraphQL API för leverans av headless-innehåll.
feature: Content Fragments,GraphQL API
exl-id: beae1f1f-0a76-4186-9e58-9cab8de4236d
source-git-commit: 5e56441d2dc9b280547c91def8d971e7b1dfcfe3
workflow-type: tm+mt
source-wordcount: '4847'
ht-degree: 0%

---

# AEM GraphQL API för användning med innehållsfragment {#graphql-api-for-use-with-content-fragments}

Lär dig hur du använder innehållsfragment i Adobe Experience Manager (AEM) med AEM GraphQL API för leverans av headless-innehåll.

AEM GraphQL API som används med innehållsfragment är till stor del baserat på GraphQL-API:t med öppen källkod.

Genom att använda GraphQL API i AEM kan du effektivt leverera innehållsfragment till JavaScript-klienter i headless CMS-implementeringar:

* Undvika iterativa API-begäranden som REST,
* se till att leveransen begränsas till de specifika kraven,
* Det går att skicka exakt det som behövs för återgivningen som svar på en enda API-fråga.

>[!NOTE]
>
>GraphQL används i två (separata) scenarier i Adobe Experience Manager (AEM):
>
>* [AEM Commerce använder data från en Commerce-plattform via GraphQL](/help/commerce/cif/integrating/magento.md).
>* AEM Content Fragments fungerar tillsammans med det AEM GraphQL-API:t (en anpassad implementering som baseras på standard-GraphQL) för att leverera strukturerat innehåll som kan användas i dina program.

## Förutsättningar {#prerequisites}

Kunder som använder GraphQL bör installera AEM Content Fragment med GraphQL Index Package 1.0.5. Se [Versionsinformation](/help/release-notes/release-notes.md#install-aem-graphql-index-add-on-package) för mer information.

## GRAPHQL API {#graphql-api}

GraphQL är:

* &quot;*...ett frågespråk för API:er och en körningsmiljö för att utföra dessa frågor med dina befintliga data. GraphQL ger en fullständig och begriplig beskrivning av data i ditt API. Det ger kunderna möjlighet att fråga efter exakt vad de behöver och ingenting mer, gör det enklare att utveckla API:er över tid och möjliggör kraftfulla utvecklingsverktyg.*&quot;.

  Se [GraphQL.org](https://graphql.org)

* &quot;*...en öppen specifikation för ett flexibelt API-lager. Placera GraphQL över era befintliga backend-system så att ni kan skapa produkter snabbare än någonsin ...*&quot;.

  Se [Utforska GraphQL](https://graphql.com/).

* *&quot;... ett språk och en specifikation för datafrågor som utvecklats internt av Facebook under 2012 innan man började använda öppen källkod 2015. Det är ett alternativ till REST-baserade arkitekturer i syfte att öka utvecklarnas produktivitet och minimera mängden data som överförs. GraphQL används i produktionen av hundratals organisationer av alla storlekar..&quot;*

  Se [GraphQL Foundation](https://graphql.org/foundation).

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all the tools they need to understand and adopt GraphQL.*". 
-->

Mer information om GraphQL API finns i följande avsnitt (bland annat):

* At [graphql.org](https://graphql.org):

   * [Introduktion till GraphQL](https://graphql.org/learn)

   * [GraphQL-specifikationen](https://spec.graphql.org/)

* At [graphql.com](https://graphql.com):

   * [Självstudiekurser](https://graphql.com/tutorials/)


Implementeringen av GraphQL för AEM baseras på GraphQL Java™-standardbibliotek. Se:

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GraphQL Java™ på GitHub](https://github.com/graphql-java)

### GraphQL Terminologi {#graphql-terminology}

GraphQL använder följande:

* **[Frågor](https://graphql.org/learn/queries/)**

* **[Scheman och typer](https://graphql.org/learn/schema/)**:

   * Scheman genereras av AEM baserat på modeller för innehållsfragment.
   * Med hjälp av dina scheman kan GraphQL presentera de typer och åtgärder som är tillåtna för implementeringen av GraphQL AEM.

* **[Fält](https://graphql.org/learn/queries/#fields)**

* **[GraphQL Endpoint](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#graphql-aem-endpoint)**
   * Sökvägen i AEM som svarar på GraphQL-frågor och ger åtkomst till GraphQL-scheman.

   * Se [Aktivera din GraphQL-slutpunkt](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint) för mer information.

Se [(GraphQL.org) Introduktion till GraphQL](https://graphql.org/learn/) för utförlig information, inklusive [Bästa praxis](https://graphql.org/learn/best-practices/).

### GraphQL Query Types {#graphql-query-types}

Med GraphQL kan du utföra frågor för att returnera:

* A **enkel post**

* A **[lista över poster](https://graphql.org/learn/schema/#lists-and-non-null)**

AEM innehåller funktioner för att konvertera frågor (båda typerna) till [Beständiga frågor](/help/sites-developing/headless/graphql-api/persisted-queries.md) som cachas av Dispatcher och CDN.

### GraphQL Query Best Practices (Dispatcher and CDN) {#graphql-query-best-practices}

[Beständiga frågor](/help/sites-developing/headless/graphql-api/persisted-queries.md) är den rekommenderade metod som ska användas för publiceringsinstanser som:

* de är cachelagrade
* de hanteras centralt av AEM

<!-- is this fully accurate? -->
>[!NOTE]
>
>Vanligtvis finns det ingen dispatcher/CDN på författaren, så det blir ingen prestandavinst att använda beständiga frågor där, förutom att testa dem.

GraphQL-frågor som använder förfrågningar om POST rekommenderas inte eftersom de inte cachelagras, så i en standardinstans är Dispatcher konfigurerad att blockera sådana frågor.

Även om GraphQL har stöd för GET-förfrågningar kan dessa förfrågningar få en träffgräns (till exempel längden på URL:en) som kan undvikas med beständiga frågor.

Se [Aktivera cachelagring av beständiga frågor](#enable-caching-persisted-queries) för mer information.

>[!NOTE]
>
>Möjligheten att utföra direkta frågor kan vara föråldrad vid något tillfälle i framtiden.

## GraphiQL-gränssnitt {#graphiql-interface}

En implementering av standarden [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) -gränssnittet kan användas med AEM GraphQL.

>[!NOTE]
>
>GraphiQL ingår i alla miljöer med AEM (men är bara tillgängligt/synligt när du konfigurerar slutpunkterna).
>
>I tidigare versioner behövde du ett paket för att installera GraphiQL IDE. Om du har installerat det här paketet kan det nu tas bort.

Med det här gränssnittet kan du direkt mata in och testa frågor.

Till exempel:

* `http://localhost:4502/content/graphiql.html`

Den innehåller funktioner som syntaxmarkering, automatisk komplettering, autoföreslå, samt historik och onlinedokumentation:

![GraphiQL-gränssnitt](assets/cfm-graphiql-interface.png "GraphiQL-gränssnitt")

>[!NOTE]
>
>Se [Använda GraphiQL IDE](/help/sites-developing/headless/graphql-api/graphiql-ide.md).

## Användningsexempel för skribent- och publiceringsmiljöer {#use-cases-author-publish-environments}

Användningsexemplen kan bero på vilken typ av AEM som används:

* Publiceringsmiljö; används för att:
   * Frågedata för JS-program (standardfall)

* Författarmiljö, används för att:
   * Fråga efter data för&quot;innehållshanteringssyften&quot;:
      * GraphQL i AEM är ett skrivskyddat API.
      * REST API kan användas för CR(u)D-åtgärder.

## Behörigheter {#permission}

Behörigheterna krävs för åtkomst av resurser.

GraphQL-frågor körs med tillstånd från den AEM användaren av den underliggande begäran. Om användaren inte har läsåtkomst till vissa fragment (som lagras som resurser) blir de inte en del av resultatuppsättningen.

Användaren måste också ha tillgång till en GraphQL-slutpunkt för att kunna köra GraphQL-frågor.

## Schemagenerering {#schema-generation}

GraphQL är ett typbestämt API, vilket innebär att data måste vara tydligt strukturerade och ordnade efter typ.

GraphQL-specifikationen innehåller en serie riktlinjer för hur du skapar ett robust API för att förhöra data i en viss instans. Kunden måste hämta [Schema](#schema-generation), som innehåller alla typer som behövs för en fråga.

För innehållsfragment baseras GraphQL-scheman (struktur och typer) på **Aktiverad** [Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md) och deras datatyper.

>[!CAUTION]
>
>Alla GraphQL-scheman (härledda från Content Fragment Models som har **Aktiverad**) går att läsa via GraphQL-slutpunkten.
>
>Denna möjlighet innebär att ni måste se till att inga känsliga data är tillgängliga, eftersom de kan läcka på det här sättet. Den innehåller till exempel information som kan finnas som fältnamn i modelldefinitionen.

Om en användare till exempel har skapat en innehållsfragmentmodell som kallas `Article`AEM sedan generera en GraphQL-typ `ArticleModel`. Fälten i den här typen motsvarar fälten och datatyperna som definieras i modellen. Dessutom skapas vissa startpunkter för frågor som arbetar med den här typen, till exempel `articleByPath` eller `articleList`.

1. En innehållsfragmentmodell:

   ![Content Fragment Model for use with GraphQL](assets/cfm-graphqlapi-01.png "Content Fragment Model for use with GraphQL")

1. Motsvarande GraphQL-schema (utdata från den automatiska dokumentationen för GraphiQL):
   ![GraphQL-schema baserat på innehållsfragmentmodell](assets/cfm-graphqlapi-02.png "GraphQL-schema baserat på innehållsfragmentmodell")

   Den här bilden visar att den genererade typen `ArticleModel` innehåller flera [fält](#fields).

   * Tre av dem har kontrollerats av användaren: `author`, `main`och `referencearticle`.

   * De andra fälten lades till automatiskt av AEM och representerar användbara metoder för att tillhandahålla information om ett visst innehållsfragment. I detta exempel [hjälpfält](#helper-fields)) `_path`, `_metadata`, `_variations`.

1. När en användare har skapat ett innehållsfragment baserat på artikelmodellen kan det sedan förhöras via GraphQL. Mer information finns i [Exempelfrågor](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#graphql-sample-queries) (baserat på [exempelstruktur för innehållsfragment för användning med GraphQL](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#content-fragment-structure-graphql)).

I GraphQL for AEM är schemat flexibelt. Denna flexibilitet innebär att den genereras automatiskt varje gång en innehållsfragmentmodell skapas, uppdateras eller tas bort. Cacheminnen för dataschemat uppdateras också när du uppdaterar en innehållsfragmentmodell.

Tjänsten Sites GraphQL avlyssnar (i bakgrunden) alla ändringar som görs i en innehållsfragmentmodell. När uppdateringar upptäcks återskapas endast den delen av schemat. Denna optimering sparar tid och ger stabilitet.

Om du till exempel:

1. Installera ett paket som innehåller `Content-Fragment-Model-1` och `Content-Fragment-Model-2`:

   1. GraphQL-typer för `Model-1` och `Model-2` genereras.

1. Ändra sedan `Content-Fragment-Model-2`:

   1. Endast `Model-2` GraphQL-typsnitt uppdateras.

   1. med beaktande av följande: `Model-1` förblir detsamma.

>[!NOTE]
>
>Den här informationen är viktig att notera om du vill göra satsvisa uppdateringar på modeller för innehållsfragment via REST-API:t, eller på något annat sätt.

Schemat hanteras via samma slutpunkt som GraphQL-frågorna, där klienthanteraren hanterar det faktum att schemat anropas med tillägget `GQLschema`. Du kan till exempel utföra en enkel `GET` begäran på `/content/cq:graphql/global/endpoint.GQLschema` resulterar i utdata från schemat med innehållstypen: `text/x-graphql-schema;charset=iso-8859-1`.

### Schemagenerering - opublicerade modeller {#schema-generation-unpublished-models}

När innehållsfragment är kapslade kan det hända att en överordnad Content Fragment Model publiceras, men ingen refererad modell gör det.

>[!NOTE]
>
>Det AEM användargränssnittet förhindrar detta, men om publiceringen görs programmatiskt eller med innehållspaket kan det ske.

När det inträffar genererar AEM en *ofullständig* Schema för den överordnade innehållsfragmentmodellen. Det innebär att fragmentreferensen, som är beroende av den opublicerade modellen, tas bort från schemat.

## Fält {#fields}

Inom schemat finns det enskilda fält av två baskategorier:

* Fält som du genererar.

  Ett urval av [Datatyper](#data-types) används för att skapa fält baserat på hur du konfigurerar innehållsfragmentmodellen. Fältnamnen hämtas från **Egenskapsnamn** fält för **Datatyp**.

   * Det finns också **Återge som** inställningar som ska beaktas, eftersom användare kan konfigurera vissa datatyper. Ett textfält med en rad kan till exempel konfigureras att innehålla flera enkelradiga texter genom att välja `multifield` i listrutan.

* GraphQL för AEM genererar också flera [hjälpfält](#helper-fields).

  Dessa fält används för att identifiera ett innehållsfragment eller för att få mer information om ett innehållsfragment.

### Datatyper {#data-types}

GraphQL för AEM har stöd för en lista med typer. Alla Content Fragment Model-datatyper som stöds och motsvarande GraphQL-typer visas:

| Content Fragment Model - datatyp | GraphQL Type | Beskrivning |
|--- |--- |--- |
| Enkelradig text | `String`, `[String]` |  Används för enkla strängar som författarnamn och platsnamn. |
| Flerradstext | `String` |  Används för att skriva ut text, t.ex. brödtexten i en artikel |
| Siffra |  `Float`, `[Float]` | Används för att visa flyttal och reguljära tal |
| Boolean |  `Boolean` |  Används för att visa kryssrutor → enkla sant/falskt-satser |
| Datum och tid | `Calendar` |  Används för att visa datum och tid i ett ISO 8086-format. Beroende på vilken typ som valts finns det tre aromer som kan användas i AEM GraphQL: `onlyDate`, `onlyTime`, `dateTime` |
| Uppräkning |  `String` |  Används för att visa ett alternativ från en lista med alternativ som definieras när modellen skapas |
|  Taggar |  `[String]` |  Används för att visa en lista över strängar som representerar taggar som används i AEM |
| Innehållsreferens |  `String` |  Används för att visa sökvägen till en annan resurs i AEM |
| Fragmentreferens |  *En modelltyp* <br><br>Ett fält: `Model` - Modelltyp, refereras direkt <br><br>Multifält, med en referenstyp: `[Model]` - Array av typen `Model`, som refereras direkt från en array <br><br>Multifält, med flera refererade typer: `[AllFragmentModels]` - Array med alla modelltyper, refererad från array med unionstyp |  Används för att referera till en eller flera innehållsfragment av vissa modelltyper, som definieras när modellen skapades |

{style="table-layout:auto"}

### Hjälpfält {#helper-fields}

Förutom datatyperna för användargenererade fält genererar GraphQL för AEM även flera *hjälpare* fält som hjälper dig att identifiera ett innehållsfragment eller att ge mer information om ett innehållsfragment.

Dessa [hjälpfält](#helper-fields) markeras med föregående `_` för att skilja mellan vad som har definierats av användaren och vad som har genererats automatiskt.

#### Bana {#path}

Sökvägsfältet används som en identifierare i AEM GraphQL. Den representerar sökvägen till Content Fragment-resursen i AEM. Den här sökvägen väljs som identifierare för ett innehållsfragment eftersom den:

* är unikt inom AEM,
* kan enkelt hämtas.

I följande kod visas sökvägarna för alla innehållsfragment som har skapats baserat på modellen för innehållsfragment `Person`.

```graphql
{
  personList {
    items {
      _path
    }
  }
}
```

Om du vill hämta ett enstaka innehållsfragment av en viss typ måste du också bestämma sökvägen först. Till exempel:

```graphql
{
  authorByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      firstName
      name
    }
  }
}
```

Se [Exempelfråga - Ett enskilt specifikt stadsfragment](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-single-specific-city-fragment).

#### Metadata {#metadata}

Via GraphQL visar AEM också metadata för ett innehållsfragment. Metadata är den information som beskriver ett innehållsfragment, till exempel följande:

* titeln på ett innehållsfragment
* miniatyrbildssökvägen
* beskrivningen av ett innehållsfragment
* och det datum då den skapades, bland annat.

Eftersom metadata genereras via Schemaredigeraren och därför inte har någon särskild struktur, har `TypedMetaData` GraphQL-typ implementerades för att visa metadata för ett innehållsfragment. The `TypedMetaData` visar informationen som grupperats med följande skalära typer:

| Fält |
|--- |
| `stringMetadata:[StringMetadata]!` |
| `stringArrayMetadata:[StringArrayMetadata]!` |
| `intMetadata:[IntMetadata]!` |
| `intArrayMetadata:[IntArrayMetadata]!` |
| `floatMetadata:[FloatMetadata]!` |
| `floatArrayMetadata:[FloatArrayMetadata]!` |
| `booleanMetadata:[BooleanMetadata]!` |
| `booleanArrayMetadata:[booleanArrayMetadata]!`  |
| `calendarMetadata:[CalendarMetadata]!` |
| `calendarArrayMetadata:[CalendarArrayMetadata]!` |

Varje skalär typ representerar antingen ett namn/värde-par eller en array med namn/värde-par, där värdet för det paret är av den typ som det grupperades i.

Om du till exempel vill hämta titeln för ett innehållsfragment är den här egenskapen en String-egenskap, så du vill fråga efter alla strängmetadata:

Så här frågar du efter metadata:

```graphql
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      _metadata {
        stringMetadata {
          name
          value
        }
      }
    }
  }
}
```

Du kan visa alla metadata för GraphQL-typer om du visar det genererade GraphQL-schemat. Alla modelltyper har samma `TypedMetaData`.

>[!NOTE]
>
>**Skillnad mellan normala metadata och arraymetadata**
>Kom ihåg att `StringMetadata` och `StringArrayMetadata` båda hänvisar till vad som lagras i databasen, inte till hur du hämtar dem.
>
>Genom att anropa `stringMetadata` får du en array med alla metadata som lagras i databasen som `String`. Och om du ringer `stringArrayMetadata`får du en array med alla metadata som lagras i databasen som `String[]`.

Se [Exempelfråga för metadata - Ange metadata för utmärkelserna med namnet GB](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-metadata-awards-gb).

#### Variationer {#variations}

The `_variations` -fältet har implementerats för att förenkla frågor om variationer som ett innehållsfragment har. Till exempel:

```graphql
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

>[!NOTE]
>
>The `_variations` fältet innehåller inte `master` variation, som tekniskt sett originaldata (refereras som *Master* i användargränssnittet) inte betraktas som en explicit variation.

Se [Exempelfråga - Alla städer med en namngiven variant](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-cities-named-variation).

>[!NOTE]
>
>Om den angivna variationen inte finns för ett innehållsfragment returneras originaldata (kallas även huvudvariant) som ett (reservformat) standardvärde.

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL Variables {#graphql-variables}

GraphQL tillåter att variabler placeras i frågan. Mer information finns i [GraphQL-dokumentation för variabler](https://graphql.org/learn/queries/#variables).

Om du till exempel vill hämta alla innehållsfragment av typen `Article` som har en viss variant kan du ange variabeln `variation` i GraphiQL.

![GraphQL Variables](assets/cfm-graphqlapi-03.png "GraphQL Variables")

```graphql
### query
query GetArticlesByVariation($variation: String!) {
    articleList(variation: $variation) {
        items {
            _path
            author
            _variations
        }
    }
}
 
### in query variables
{
    "variation": "uk"
}
```

## GraphQL Direktiv {#graphql-directives}

I GraphQL finns det en möjlighet att ändra frågan baserat på variabler, så kallade GraphQL-direktiv.

Här kan du till exempel inkludera `adventurePrice` fält i en fråga för alla `AdventureModels`, baserat på en variabel `includePrice`.

![GraphQL Direktiv](assets/cfm-graphqlapi-04.png "GraphQL Direktiv")

```graphql
### query
query GetAdventureByType($includePrice: Boolean!) {
  adventureList {
    items {
      adventureTitle
      adventurePrice @include(if: $includePrice)
    }
  }
}
 
### in query variables
{
    "includePrice": true
}
```

## Filtrering {#filtering}

Du kan också använda filtrering i dina GraphQL-frågor för att returnera specifika data.

Vid filtrering används en syntax som baseras på logiska operatorer och uttryck.

Den mest atomiska delen är ett enstaka uttryck som kan tillämpas på innehållet i ett visst fält. Innehållet i fältet jämförs med ett givet konstantvärde.

Följande uttryck skulle till exempel jämföra innehållet i fältet med värdet `some text`och lyckas om innehållet är lika med värdet. Annars misslyckas uttrycket:

```graphql
{
  value: "some text"
  _op: EQUALS
}
```

Följande operatorer kan användas för att jämföra fält med ett visst värde:

| Operator | Typer | Uttrycket lyckas om ... |
|--- |--- |--- |
| `EQUALS` | `String`, `ID`, `Boolean` | ... värdet är detsamma som innehållet i fältet |
| `EQUALS_NOT` | `String`, `ID` | ... värdet är *not* samma som fältets innehåll |
| `CONTAINS` | `String` | ... innehållet i fältet innehåller värdet (`{ value: "mas", _op: CONTAINS }` matchar `Christmas`, `Xmas`, `master`, ...) |
| `CONTAINS_NOT` | `String` | ... fältets innehåll *not* innehåller värdet |
| `STARTS_WITH` | `ID` | ... ID:t börjar med ett visst värde (`{ value: "/content/dam/", _op: STARTS_WITH` matchar `/content/dam/path/to/fragment`, men inte `/namespace/content/dam/something` |
| `EQUAL` | `Int`, `Float` | ... värdet är detsamma som innehållet i fältet |
| `UNEQUAL` | `Int`, `Float` | ... värdet är *not* samma som fältets innehåll |
| `GREATER` | `Int`, `Float` | ... fältets innehåll är större än värdet |
| `GREATER_EQUAL` | `Int`, `Float` | ... fältets innehåll är större än eller lika med värdet |
| `LOWER` | `Int`, `Float` | ... fältets innehåll är lägre än värdet |
| `LOWER_EQUAL` | `Int`, `Float` | ... fältets innehåll är lägre än eller lika med värdet |
| `AT` | `Calendar`, `Date`, `Time` | ... fältets innehåll är detsamma som värdet (inklusive tidszonsinställning) |
| `NOT_AT` | `Calendar`, `Date`, `Time` | ... fältets innehåll är *not* samma som värdet |
| `BEFORE` | `Calendar`, `Date`, `Time` | ... den tidpunkt som anges av värdet ligger före den tidpunkt som anges av fältets innehåll |
| `AT_OR_BEFORE` | `Calendar`, `Date`, `Time` | ... den tidpunkt som anges av värdet är före eller vid samma tidpunkt som anges av fältets innehåll |
| `AFTER` | `Calendar`, `Date`, `Time` | ... tidpunkten som anges av värdet är efter tidpunkten som anges av fältets innehåll |
| `AT_OR_AFTER` | `Calendar`, `Date`, `Time` | ... den tidpunkt som anges av värdet är efter eller vid samma tidpunkt som anges av fältets innehåll |

I vissa typer kan du även ange ytterligare alternativ som ändrar hur ett uttryck utvärderas:

| Alternativ | Typer | Beskrivning |
|--- |--- |--- |
| `_ignoreCase` | `String` | Ignorerar skiftläget för en sträng, till exempel värdet `time` matchar `TIME`, `time`, `tImE`, ... |
| `_sensitiveness` | `Float` | Tillåter en viss marginal för `float` värden som ska anses vara desamma (för att kringgå tekniska begränsningar på grund av den interna representationen av `float` värden; bör undvikas eftersom detta alternativ kan ha en negativ inverkan på prestandan |

Uttryck kan kombineras till en uppsättning med hjälp av en logisk operator (`_logOp`):

* `OR` - uttrycksuppsättningen lyckas om minst ett uttryck lyckas
* `AND` - uttrycksuppsättningen lyckas om alla uttryck lyckas (standard)

Varje fält kan filtreras med en egen uppsättning uttryck. Uttrycksuppsättningarna för alla fält som omnämns i filterargumentet kombineras till slut av den egna logiska operatorn.

En filterdefinition (skickas som `filter` argument till en fråga) innehåller:

* En underdefinition för varje fält (fältet kan nås via namnet, till exempel finns det en `lastName` i filtret för `lastName` i fältet Data (fälttyp)
* Varje underdefinition innehåller `_expressions` -array, som innehåller uttrycksuppsättningen och `_logOp` fält som definierar den logiska operatorn ska uttrycken kombineras med
* Varje uttryck definieras av värdet (`value` fält) och operatorn (`_operator` fält) innehållet i ett fält ska jämföras med

Du kan utesluta `_logOp` om du vill kombinera objekt med `AND` och `_operator` om du vill kontrollera om de är lika, eftersom dessa värden är standardvärden.

I följande exempel visas en fullständig fråga som filtrerar alla personer som har en `lastName` av `Provo` eller innehåller `sjö`, oberoende av omständigheterna:

```graphql
{
  authorList(filter: {
    lastname: {
      _logOp: OR
      _expressions: [
        {
          value: "sjö",
          _operator: CONTAINS,
          _ignoreCase: true
        },
        {
          value: "Provo"
        }
      ]
    }
  }) {
    items {
      lastName
      firstName
    }
  }
}
```

Du kan även filtrera efter kapslade fält, men det rekommenderas inte eftersom det kan leda till prestandaproblem.

Ytterligare exempel finns i:

* information om [GraphQL for AEM extensions](#graphql-extensions)

* [Exempelfrågor med detta exempelinnehåll och -struktur](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * Och [Exempelinnehåll och struktur](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#content-fragment-structure-graphql) förberedda för användning i provfrågor

* [Exempelfrågor baserade på WKND-projektet](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## Sortering {#sorting}

>[!NOTE]
>
>För bästa prestanda bör du tänka på [Uppdatera dina innehållsfragment för sidindelning och sortering i GraphQL-filtrering](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md).

Med den här funktionen kan du sortera frågeresultaten enligt ett angivet fält.

Sorteringskriterierna:

* är en kommaavgränsad lista med värden som representerar fältsökvägen
   * det första fältet i listan definierar den primära sorteringsordningen
      * det andra fältet används om två värden för det primära sorteringsvillkoret är lika
      * det tredje fältet används om de första två kriterierna är lika, och så vidare.
   * punktnotation, d.v.s. `field1.subfield.subfield`och så vidare.
* med valfri orderriktning
   * ASC (stigande) eller DESC (fallande); som standard används ASC
   * riktningen kan anges per fält. Det innebär att du kan sortera ett fält i stigande ordning och ett annat i fallande ordning (namn, firstName DESC)

Till exempel:

```graphql
query {
  authorList(sort: "lastName, firstName") {
    items {
      firstName
      lastName
    }
  }
}
```

Och dessutom:

```graphql
{
  authorList(sort: "lastName DESC, firstName DESC") {
    items {
        lastName
        firstName
    }
  }
}
```

Du kan även sortera ett fält i ett kapslat fragment med formatet `nestedFragmentname.fieldname`.

>[!NOTE]
>
>Det här formatet kan påverka prestandan negativt.

Till exempel:

```graphql
query {
  articleList(sort: "authorFragment.lastName")  {
    items {
      title
      authorFragment {
        firstName
        lastName
        birthDay
      }
      slug
    }
  }
}
```

## Sidindelning {#paging}

>[!NOTE]
>
>För bästa prestanda bör du tänka på [Uppdatera dina innehållsfragment för sidindelning och sortering i GraphQL-filtrering](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md).

Med den här funktionen kan du utföra sidindelning på frågetyper som returnerar en lista. Det finns två metoder:

* `offset` och `limit` i en `List` fråga
* `first` och `after` i en `Paginated` fråga

### Listfråga - förskjutning och begränsning {#list-offset-limit}

I en `...List`fråga som du kan använda `offset` och `limit` om du vill returnera en viss delmängd av resultaten:

* `offset`: Anger den första datauppsättningen som ska returneras
* `limit`: Anger maximalt antal datauppsättningar som ska returneras

Om du till exempel vill visa en resultatsida som innehåller upp till fem artiklar, med början från den femte artikeln från *complete* resultatlista:

```graphql
query {
   articleList(offset: 5, limit: 5) {
    items {
      authorFragment {
        lastName
        firstName
      }
    }
  }
}
```

<!-- When available link to BP and replace "JCR query level" with a more neutral term. -->

<!-- When available link to BP and replace "JCR query result set" with a more neutral term. -->

>[!NOTE]
>
>* Sidindelning kräver en stabil sorteringsordning för att fungera korrekt i flera frågor som begär olika sidor i samma resultatuppsättning. Som standard används databassökvägen för varje objekt i resultatuppsättningen för att säkerställa att ordningen alltid är densamma. Om en annan sorteringsordning används, och om sorteringen inte kan göras på JCR-frågenivå, så har resultatet en negativ effekt. Orsaken är att hela resultatuppsättningen måste läsas in i minnet innan sidorna bestäms.
>
>* Ju högre förskjutning, desto längre tid tar det att hoppa över objekten från den fullständiga JCR-frågeresultatuppsättningen. En alternativ lösning för stora resultatuppsättningar är att använda den numrerade frågan med `first` och `after` -metod.

### Sidnumrerad fråga - första och efter {#paginated-first-after}

The `...Paginated` frågetypen återanvänder de flesta `...List` frågetypsfunktioner (filtrering, sortering), men i stället för att använda `offset`/`limit` argument, använder `first`/`after` argument som definieras av [GraphQL Cursor Connections Specification](https://relay.dev/graphql/connections.htm). Du hittar en mindre formell introduktion i [GraphQL introduktion](https://graphql.org/learn/pagination/#pagination-and-edges).

* `first`: `n` första objekt som ska returneras.
Standardvärdet är `50`.
Maxvärdet är `100`.
* `after`: Markören som bestämmer början på den begärda sidan. Det objekt som markören representerar tas inte med i resultatuppsättningen. Markören för ett objekt bestäms av `cursor` fält för `edges` struktur.

Du kan till exempel skriva ut en resultatsida som innehåller upp till fem äventyr, med början från markörobjektet i *complete* resultatlista:

```graphql
query {
    adventurePaginated(first: 5, after: "ODg1MmMyMmEtZTAzMy00MTNjLThiMzMtZGQyMzY5ZTNjN2M1") {
        edges {
          cursor
          node {
            title
          }
        }
        pageInfo {
          endCursor
          hasNextPage
        }
    }
}
```

<!-- When available link to BP -->
<!-- Due to internal technical constraints, performance will degrade if sorting and filtering is applied on nested fields. Therefore it is recommended to use filter/sort fields stored at root level. For more information, see the [Best Practices document](link). -->

>[!NOTE]
>
>* Som standard används UUID för databasnoden som representerar fragmentet för att säkerställa att resultatordningen alltid är densamma. När `sort` används UUID implicit för att säkerställa en unik sortering, även för två objekt med identiska sorteringsnycklar.
>
>* På grund av interna tekniska begränsningar försämras prestanda om sortering och filtrering används i kapslade fält. Använd därför filter-/sorteringsfält som lagras på rotnivå. Den här tekniken rekommenderas också om du vill fråga efter stora sidnumrerade resultatuppsättningar.

## GraphQL Persistent Queries - aktivera cachelagring i Dispatcher {#graphql-persisted-queries-enabling-caching-dispatcher}

>[!CAUTION]
>
>Om cachelagring i Dispatcher är aktiverad är [CORS-filter](#cors-filter) behövs inte och därför kan avsnittet ignoreras.

Cachelagring av beständiga frågor är inte aktiverat som standard i Dispatcher. Standardaktivering är inte möjlig eftersom kunder som använder CORS (Cross-Origin Resource Sharing) med flera ursprung måste granska och eventuellt uppdatera sin Dispatcher-konfiguration.

>[!NOTE]
>
>Dispatcher cachelagrar inte `Vary` header.
>
>Cachelagring av andra CORS-relaterade rubriker kan aktiveras i Dispatcher, men kan vara otillräcklig om det finns flera CORS-ursprung.

### Aktivera cachelagring av beständiga frågor {#enable-caching-persisted-queries}

Om du vill aktivera cachelagring av beständiga frågor definierar du variabeln Dispatcher `CACHE_GRAPHQL_PERSISTED_QUERIES`:

1. Lägg till variabeln i Dispatcher-filen `global.vars`:

   ```xml
   Define CACHE_GRAPHQL_PERSISTED_QUERIES
   ```

>[!NOTE]
>
>När Dispatcher-cachning är aktiverat för beständiga frågor med hjälp av `Define CACHE_GRAPHQL_PERSISTED_QUERIES` en `ETag` skickas till svaret av Dispatcher.
>
>Som standard är `ETag` har konfigurerats med följande direktiv:
>
>```
>FileETag MTime Size 
>```
>
>Den här inställningen kan dock orsaka problem när den används på de beständiga frågesvaren, eftersom den inte tar hänsyn till små ändringar i svaret.
>
>Att uppnå individuella `ETag` beräkningar på *var* ett unikt svar `FileETag Digest` -inställningen måste användas i dispatcherkonfigurationen:
>
>```xml
><Directory />    
>   ...    
>   FileETag Digest
></Directory> 
>```

>[!NOTE]
>
>Anpassa till [Dispatcher-krav för dokument som kan cachas](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/troubleshooting/dispatcher-faq.html#how-does-the-dispatcher-return-documents%3F)lägger Dispatcher till suffixet `.json` till alla beständiga fråge-URL:er, så att resultatet kan cachelagras.
>
>Det här suffixet läggs till av en omskrivningsregel när den beständiga frågecachelagringen är aktiverad.

### CORS-konfiguration i Dispatcher {#cors-configuration-in-dispatcher}

Kunder som använder CORS-begäranden kan behöva granska och uppdatera sin CORS-konfiguration i Dispatcher.

* The `Origin` får inte skickas till AEM publicera via Dispatcher:
   * Kontrollera `clientheaders.any` -fil.
* CORS-begäranden måste i stället utvärderas för tillåtna ursprung på Dispatcher-nivå. På så sätt säkerställs också att CORS-relaterade rubriker ställs in korrekt, på ett och samma ställe, i samtliga fall.
   * En sådan konfiguration bör läggas till i `vhost` -fil. En exempelkonfiguration ges nedan. För enkelhetens skull har endast den korrespondensrelaterade delen angetts. Du kan anpassa den efter dina specifika användningsexempel.

  ```xml
  <VirtualHost *:80>
     ServerName "publish"
  
     # ...
  
     <IfModule mod_headers.c>
         Header add X-Vhost "publish"
  
          ################## Start of the CORS specific configuration ##################
  
          SetEnvIfExpr "req_novary('Origin') == ''"  CORSType=none CORSProcessing=false
          SetEnvIfExpr "req_novary('Origin') != ''"  CORSType=cors CORSProcessing=true CORSTrusted=false
  
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') == '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''  " CORSType=invalidpreflight CORSProcessing=false
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') != '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''  " CORSType=preflight CORSProcessing=true CORSTrusted=false
          SetEnvIfExpr "req_novary('Origin') -strcmatch 'https://%{HTTP_HOST}*'"  CORSType=samedomain CORSProcessing=false
  
          # For requests that require CORS processing, check if the Origin can be trusted
          SetEnvIfExpr "%{HTTP_HOST} =~ /(.*)/ " ParsedHost=$1
  
          ################## Adapt the regex to match CORS origin for your environment
          SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*.your-domain.tld(:\d+)?$)#" CORSTrusted=true
  
          # Extract the Origin header 
          SetEnvIfNoCase ^Origin$ ^https://(.*)$ CORSTrustedOrigin=https://$1
  
          # Flush If already set
          Header unset Access-Control-Allow-Origin
          Header unset Access-Control-Allow-Credentials
  
          # Trusted
          Header always set Access-Control-Allow-Credentials "true" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Origin "%{CORSTrustedOrigin}e" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Methods "GET" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Max-Age 1800 "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Headers "Origin, Accept, X-Requested-With, Content-Type, Access-Control-Request-Method, Access-Control-Request-Headers" "expr=reqenv('CORSTrusted') == 'true'"
  
          # Non-CORS or Not Trusted
          Header unset Access-Control-Allow-Credentials "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Origin "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Methods "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Max-Age "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
  
          # Always vary on origin, even if its not there.
          Header merge Vary Origin
  
          # CORS - send 204 for CORS requests which are not trusted
          RewriteCond expr "reqenv('CORSProcessing') == 'true' && reqenv('CORSTrusted') == 'false'"
          RewriteRule "^(.*)" - [R=204,L]
  
          ################## End of the CORS specific configuration ##################
  
     </IfModule>
  
     <Directory />
  
         # ...
  
     </Directory>
  
     # ...
  
  </VirtualHost>
  ```

## GraphQL for AEM - i korthet {#graphql-extensions}

Den grundläggande funktionen för frågor med GraphQL för AEM följer GraphQL standardspecifikation. Det finns några tillägg för GraphQL-frågor med AEM:

* Om du behöver ett enda resultat:
   * använd modellnamnet, till exempel ort

* Om du förväntar dig en resultatlista:
   * lägg till `List` till modellnamnet, till exempel  `cityList`
   * Se [Exempelfråga - All information om alla städer](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-all-information-all-cities)

  Då kan du:

   * [Sortera resultaten](#sorting)

      * `ASC` : stigande
      * `DESC` : fallande

   * Returnera en resultatsida med antingen:

      * [En listfråga med förskjutning och begränsning](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#list-offset-limit)
      * [En sidnumrerad fråga med första och efter](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#paginated-first-after)
   * Se [Exempelfråga - All information om alla städer](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-all-information-all-cities)

* Filtret `includeVariations` ingår i `List` frågetyp. Om du vill hämta variationer för innehållsfragment i frågeresultaten, `includeVariations` filter måste anges till `true`.

  >[!CAUTION]
  >Filtret `includeVariations` kan inte användas tillsammans med det systemgenererade fältet `_variation`.

* Om du vill använda ett logiskt OR:
   * use ` _logOp: OR`
   * Se [Exempelfråga - Alla personer som har namnet &quot;Jobs&quot; eller &quot;Smith&quot;](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-all-persons-jobs-smith)

* Logiskt AND finns också, men är (ofta) implicit

* Du kan fråga efter fältnamn som motsvarar fälten i innehållsfragmentmodellen
   * Se [Exempelfråga - Fullständig information om företagets VD och anställda](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-full-details-company-ceos-employees)

* Förutom fälten från modellen finns det vissa systemgenererade fält (föregås av understreck):

   * För innehåll:

      * `_locale` : för att visa språket, baserat på Språkhanteraren
         * Se [Exempelfråga för flera innehållsfragment för en viss språkinställning](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-multiple-fragments-given-locale)

      * `_metadata` : för att visa metadata för ditt fragment
         * Se [Exempelfråga för metadata - Ange metadata för utmärkelserna med namnet GB](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-metadata-awards-gb)

      * `_model` : tillåt frågor för en innehållsfragmentmodell (sökväg och rubrik)
         * Se [Exempelfråga för en innehållsfragmentmodell från en modell](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-content-fragment-model-from-model)

      * `_path` : sökvägen till ditt innehållsfragment i databasen
         * Se [Exempelfråga - Ett enskilt specifikt stadsfragment](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)

      * `_reference` : för att visa referenser, inklusive textbundna referenser i RTF-redigeraren
         * Se [Exempelfråga för flera innehållsfragment med förhämtade referenser](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-multiple-fragments-prefetched-references)

      * `_variation` : för att visa specifika variationer i ditt innehållsfragment

        >[!NOTE]
        >
        >Om den angivna variationen inte finns för ett innehållsfragment returneras huvudvarianten som ett (fallback) standardvärde.

        >[!CAUTION]
        >Det systemgenererade fältet `_variation` kan inte användas tillsammans med filtret `includeVariations`.

         * Se [Exempelfråga - Alla städer med en namngiven variant](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-cities-named-variation)

      * `_tags` : för att visa ID:n för innehållsfragment eller variationer som innehåller taggar; den här listan är en array med `cq:tags` identifierare.

         * Se [Exempelfråga - namn på alla städer som taggats som stadbrytningar](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-names-all-cities-tagged-city-breaks)
         * Se [Exempelfråga för innehållsfragmentvariationer för en viss modell som har en specifik tagg bifogad](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-fragment-variations-given-model-specific-tag)

        >[!NOTE]
        >
        >Taggar kan också efterfrågas genom att en lista med metadata för ett innehållsfragment visas.

   * Och åtgärder:

      * `_operator` : tillämpa särskilda operatörer, `EQUALS`, `EQUALS_NOT`, `GREATER_EQUAL`, `LOWER`, `CONTAINS`, `STARTS_WITH`
         * Se [Exempelfråga - Alla personer som inte har namnet &quot;Jobs&quot;](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-all-persons-not-jobs)
         * Se [Exempelfråga - Alla annonser där `_path` börjar med ett visst prefix](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-all-adventures-cycling-path-filter)

      * `_apply` : att tillämpa särskilda villkor, till exempel  `AT_LEAST_ONCE`
         * Se [Exempelfråga - Filtrera en array med ett objekt som måste förekomma minst en gång](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-array-item-occur-at-least-once)

      * `_ignoreCase` : att ignorera skiftläget vid fråga
         * Se [Exempelfråga - Alla städer med SAN i namnet, oavsett fall](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-all-cities-san-ignore-case)

* GraphQL-unionstyper stöds:

   * use `... on`
      * Se [Exempelfråga för ett innehållsfragment för en viss modell med en innehållsreferens](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-fragment-specific-model-content-reference)

* Reservation vid fråga om kapslade fragment:

   * Om den begärda varianten inte finns i ett kapslat fragment, kommer **Master** variationen returneras.

### CORS-filter {#cors-filter}

>[!CAUTION]
>
>If [cachelagring i Dispatcher har aktiverats](#graphql-persisted-queries-enabling-caching-dispatcher) behövs inte CORS-filtret, så det här avsnittet kan ignoreras.

>[!NOTE]
>
>En detaljerad översikt över CORS resursdelningsprincip i AEM finns på [CORS (Cross-Origin Resource Sharing)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html#understand-cross-origin-resource-sharing-(cors)).

Konfigurera en CORS-princip i kundens Git-databas för att få åtkomst till GraphQL-slutpunkten. Den här konfigurationen görs genom att en lämplig OSGi CORS-konfigurationsfil läggs till för en eller flera önskade slutpunkter.

Den här konfigurationen måste ange en betrodd webbplatsens ursprung `alloworigin` eller `alloworiginregexp` för vilka tillträde måste beviljas.

Om du till exempel vill ge åtkomst till GraphQL slutpunkt och beständiga frågeslutpunkter för `https://my.domain` du kan använda:

```xml
{
  "supportscredentials":true,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/_cq_graphql/global/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```

Om du har konfigurerat en hjälpsökväg för slutpunkten kan du även använda den i `allowedpaths`.

### Referensfilter {#referrer-filter}

Förutom CORS-konfigurationen måste ett referensfilter konfigureras så att åtkomst från tredjepartsvärdar tillåts.

Det här filtret görs genom att en lämplig konfigurationsfil för OSGi-referensfiltret läggs till:

* anger ett betrott värdnamn för en webbplats, antingen `allow.hosts` eller `allow.hosts.regexp`,
* ger åtkomst till det här värdnamnet.

Om du till exempel vill ge åtkomst för begäranden med referenten `my.domain` du kan:

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

>[!CAUTION]
>
>Det är kundens ansvar att
>
>* endast ge åtkomst till betrodda domäner
>* se till att ingen känslig information exponeras
>* inte använda jokertecken [*] syntax; den här funktionen inaktiverar autentiserad åtkomst till GraphQL-slutpunkten och exponerar den även för hela världen.

>[!CAUTION]
>
>Alla GraphQL [scheman](#schema-generation) (härleds från Content Fragment Models som har **Aktiverad**) går att läsa via GraphQL-slutpunkten.
>
>Den här funktionen innebär att du måste se till att det inte finns några känsliga data tillgängliga eftersom de kan läcka på det här sättet. Den innehåller till exempel information som kan finnas som fältnamn i modelldefinitionen.

## Autentisering {#authentication}

Se [Autentisering för fjärrfrågor AEM GraphQL-frågor om innehållsfragment](/help/sites-developing/headless/graphql-api/graphql-authentication-content-fragments.md).

## Vanliga frågor {#faqs}

Frågor som har uppstått:

1. **Q**: &quot;*Hur skiljer sig GraphQL API för AEM från Query Builder API?*&quot;

   * **A**: &quot;*AEM GraphQL API ger total kontroll över JSON-utdata och är en branschstandard för att fråga efter innehåll.
I framtiden planerar AEM att investera i AEM GraphQL API.*&quot;

## Självstudiekurs - Komma igång med AEM Headless och GraphQL {#tutorial}

Söker du en praktisk självstudiekurs? Checka ut [Komma igång med AEM Headless och GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) en komplett självstudiekurs som visar hur man bygger upp och exponerar innehåll med hjälp av AEM GraphQL API:er och som används av en extern app, i ett headless CMS-scenario.
