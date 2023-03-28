---
title: AEM GraphQL API för användning med innehållsfragment
description: Lär dig hur du använder innehållsfragment i Adobe Experience Manager (AEM) med AEM GraphQL API för leverans av headless-innehåll.
feature: Content Fragments,GraphQL API
exl-id: beae1f1f-0a76-4186-9e58-9cab8de4236d
source-git-commit: f6bf99e58fabcb1fb51d8724e1442784811c47d7
workflow-type: tm+mt
source-wordcount: '3696'
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
>GraphQL används för närvarande i två (separata) scenarier i Adobe Experience Manager (AEM):
>
>* [AEM Commerce använder data från en Commerce-plattform via GraphQL](/help/commerce/cif/integrating/magento.md).
>* AEM Content Fragments fungerar tillsammans med det AEM GraphQL-API:t (en anpassad implementering som baseras på standard-GraphQL) för att leverera strukturerat innehåll som kan användas i dina program.


## GraphQL API {#graphql-api}

GraphQL är:

* &quot;*...ett frågespråk för API:er och en körningsmiljö för att utföra dessa frågor med dina befintliga data. GraphQL ger en fullständig och begriplig beskrivning av data i API:t, ger kunderna möjlighet att fråga efter exakt vad de behöver och ingenting mer, gör det enklare att utveckla API:er över tid och möjliggör kraftfulla utvecklingsverktyg.*&quot;.

   Se [GraphQL.org](https://graphql.org)

* &quot;*...en öppen specifikation för ett flexibelt API-lager. Placera GraphQL över era befintliga bakgrunder för att skapa produkter snabbare än någonsin ....*&quot;.

   Se [Utforska GraphQL](https://www.graphql.com).

* *&quot;...ett datameddelande och en specifikation som utvecklats internt av Facebook 2012 innan de blev offentligt tillgängliga 2015. Det är ett alternativ till REST-baserade arkitekturer i syfte att öka utvecklarnas produktivitet och minimera mängden data som överförs. GraphQL används i produktionen av hundratals organisationer av alla storlekar..&quot;*

   Se [GraphQL Foundation](https://foundation.graphql.org/).

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

Mer information om GraphQL API finns i följande avsnitt (bland annat på engelska):

* At [graphql.org](https://graphql.org):

   * [Introduktion till GraphQL](https://graphql.org/learn)

   * [GraphQL-specifikationen](https://spec.graphql.org/)

* At [graphql.com](https://graphql.com):

   * [Stödlinjer](https://www.graphql.com/guides/)

   * [Självstudiekurser](https://www.graphql.com/tutorials/)

   * [Fallstudier](https://www.graphql.com/case-studies/)

Implementeringen av GraphQL för AEM baseras på GraphQL Java Library. Se:

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GraphQL Java på GitHub](https://github.com/graphql-java)

### GraphQL Terminologi {#graphql-terminology}

GraphQL använder följande:

* **[Frågor](https://graphql.org/learn/queries/)**

* **[Scheman och typer](https://graphql.org/learn/schema/)**:

   * Scheman genereras av AEM baserat på modeller för innehållsfragment.
   * Med hjälp av dina scheman kan GraphQL presentera de typer och åtgärder som är tillåtna för implementeringen av GraphQL AEM.

* **[Fält](https://graphql.org/learn/queries/#fields)**

* **[GraphQL Endpoint](#graphql-aem-endpoint)**
   * Sökvägen i AEM som svarar på GraphQL-frågor och ger åtkomst till GraphQL-scheman.

   * Se [Aktivera din GraphQL-slutpunkt](#enabling-graphql-endpoint) för mer information.

Se [(GraphQL.org) Introduktion till GraphQL](https://graphql.org/learn/) för utförlig information, inklusive [Bästa praxis](https://graphql.org/learn/best-practices/).

### GraphQL Query Types {#graphql-query-types}

Med GraphQL kan du utföra frågor för att returnera:

* A **enkel inmatning**

* A **[lista över poster](https://graphql.org/learn/schema/#lists-and-non-null)**

AEM innehåller funktioner för att konvertera frågor (båda typerna) till [Beständiga frågor](/help/assets/content-fragments/persisted-queries.md), som kan cachas av Dispatcher och CDN.

### GraphQL Query Best Practices (Dispatcher and CDN) {#graphql-query-best-practices}

The [Beständiga frågor](/help/assets/content-fragments/persisted-queries.md) är den rekommenderade metod som ska användas för publiceringsinstanser som:

* de cachelagras
* de hanteras centralt av AEM

<!-- is this fully accurate? -->
>[!NOTE]
>
>Vanligtvis finns det ingen dispatcher/CDN på författaren, så det blir ingen prestandavinst att använda beständiga frågor där. förutom att testa dem.

GraphQL-frågor som använder förfrågningar om POST rekommenderas inte eftersom de inte cachelagras, så i en standardinstans är Dispatcher konfigurerad att blockera sådana frågor.

Även om GraphQL har stöd för GET-förfrågningar kan dessa få träffgränser (till exempel längden på URL:en) som kan undvikas med beständiga frågor.

>[!NOTE]
>
>Möjligheten att utföra direkta frågor kan vara föråldrad vid något tillfälle i framtiden.

## The GraphQL for AEM Endpoint {#graphql-aem-endpoint}

Slutpunkten är den sökväg som används för att komma åt GraphQL för AEM. Med den här sökvägen kan du (eller din app):

* tillgång till GraphQL schema,
* skicka dina GraphQL-frågor,
* ta emot svaren (på dina GraphQL-frågor).

Det finns två typer av slutpunkter i AEM:

* Global
   * Tillgängligt för alla webbplatser.
   * Den här slutpunkten kan använda alla modeller för innehållsfragment från alla platskonfigurationer (definieras i [Konfigurationsläsaren](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)).
   * Om det finns några modeller för innehållsfragment som ska delas mellan platskonfigurationer, ska dessa skapas under de globala platskonfigurationerna.
* Platskonfigurationer:
   * Motsvarar en platskonfiguration, enligt definitionen i [Konfigurationsläsaren](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser).
   * Specifikt för en angiven plats/ett angivet projekt.
   * En platskonfigurationsspecifik slutpunkt använder innehållsfragmentmodellerna från den specifika platskonfigurationen tillsammans med de från den globala platskonfigurationen.

>[!CAUTION]
>
>Innehållsfragmentsredigeraren kan tillåta att ett innehållsfragment av en platskonfiguration refererar till ett innehållsfragment av en annan platskonfiguration (via principer).
>
>I så fall går det inte att hämta allt innehåll med en platskonfigurationsspecifik slutpunkt.
>
>Innehållsförfattaren bör kontrollera detta scenario; Det kan till exempel vara bra att överväga att placera delade modeller för innehållsfragment under konfigurationen för globala platser.

Databassökvägen för den globala slutpunkten för GraphQL AEM är:

`/content/cq:graphql/global/endpoint`

För vilken ditt program kan använda följande sökväg i URL:en för begäran:

`/content/_cq_graphql/global/endpoint.json`

Om du vill aktivera en slutpunkt för GraphQL för AEM måste du:

* [Aktivera din GraphQL-slutpunkt](#enabling-graphql-endpoint)
* [Publicera din GraphQL-slutpunkt](#publishing-graphql-endpoint)

### Aktivera din GraphQL-slutpunkt {#enabling-graphql-endpoint}

Om du vill aktivera en GraphQL-slutpunkt måste du först ha en lämplig konfiguration. Se [Content Fragments - Configuration Browser](/help/assets/content-fragments/content-fragments-configuration-browser.md).

>[!CAUTION]
>
>Om [användning av innehållsfragmentmodeller inte har aktiverats](/help/assets/content-fragments/content-fragments-configuration-browser.md), **Skapa** kommer inte att vara tillgängligt.

Så här aktiverar du motsvarande slutpunkt:

1. Navigera till **verktyg**, **Resurser** väljer **GraphQL**.
1. Välj **Skapa**.
1. The **Skapa ny GraphQL-slutpunkt** öppnas. Här kan du ange:
   * **Namn**: Slutpunktens namn. du kan skriva vilken text som helst.
   * **Använd GraphQL-schema från**: Använd listrutan för att välja önskad plats/önskat projekt.

   >[!NOTE]
   >
   >Följande varning visas i dialogrutan:
   >
   >* *GraphQL slutpunkter kan medföra problem med datasäkerhet och prestanda om de inte hanteras varsamt. Kontrollera att du har angett rätt behörigheter när du har skapat en slutpunkt.*


1. Bekräfta med **Skapa**.
1. The **Nästa steg** kommer att innehålla en direktlänk till säkerhetskonsolen så att du kan se till att den nyskapade slutpunkten har rätt behörigheter.

   >[!CAUTION]
   >
   >Slutpunkten är tillgänglig för alla. Detta kan - särskilt när det gäller publiceringsinstanser - utgöra ett säkerhetsproblem, eftersom GraphQL-frågor kan belasta servern mycket.
   >
   >Du kan ställa in åtkomstkontrollistor, som passar ditt användningsfall, på slutpunkten.

### Publicera din GraphQL-slutpunkt {#publishing-graphql-endpoint}

Markera den nya slutpunkten och **Publicera** för att göra den helt tillgänglig i alla miljöer.

>[!CAUTION]
>
>Slutpunkten är tillgänglig för alla.
>
>På publiceringsinstanser kan detta utgöra ett säkerhetsproblem, eftersom GraphQL-frågor kan medföra en stor belastning på servern.
>
>Du måste konfigurera åtkomstkontrollistor som passar ditt användningsfall på slutpunkten.

## GraphiQL-gränssnitt {#graphiql-interface}

En implementering av standarden [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) -gränssnittet kan användas med AEM GraphQL.

>[!NOTE]
>
>GraphiQL ingår i alla miljöer med AEM (men är bara tillgängligt/synligt när du konfigurerar slutpunkterna).
>
>I tidigare versioner behövdes ett paket för att installera GraphiQL IDE. Om du har installerat den kan den nu tas bort.

Med det här gränssnittet kan du direkt mata in och testa frågor.

Till exempel:

* `http://localhost:4502/content/graphiql.html`

Detta innehåller funktioner som syntaxmarkering, automatisk komplettering, autoförslag, samt historik och onlinedokumentation:

![GraphiQL-gränssnitt](assets/cfm-graphiql-interface.png "GraphiQL-gränssnitt")

>[!NOTE]
>
>Mer information finns i [Använda GraphiQL IDE](/help/assets/content-fragments/graphiql-ide.md).

## Användningsexempel för skribent- och publiceringsmiljöer {#use-cases-author-publish-environments}

Användningsexemplen kan bero på vilken typ av AEM som används:

* Publiceringsmiljö. används för att:
   * Frågedata för JS-program (standardfall)

* Författarmiljö; används för att:
   * Fråga efter data för&quot;innehållshanteringssyften&quot;:
      * GraphQL i AEM är för närvarande ett skrivskyddat API.
      * REST API kan användas för CR(u)D-åtgärder.

## Behörigheter {#permission}

Behörigheterna är de som krävs för åtkomst av resurser.

GraphQL-frågor körs med tillstånd från den AEM användaren av den underliggande begäran. Om användaren inte har läsåtkomst till vissa fragment (som lagras som resurser) blir de inte en del av resultatuppsättningen.

Dessutom måste användaren ha åtkomst till en GraphQL-slutpunkt för att kunna köra GraphQL-frågor.

## Schemagenerering {#schema-generation}

GraphQL är ett starkt typbestämt API, vilket innebär att data måste vara tydligt strukturerade och ordnade efter typ.

GraphQL-specifikationen innehåller en serie riktlinjer för hur du skapar ett robust API för att förhöra data i en viss instans. För att göra detta måste en kund hämta [Schema](#schema-generation), som innehåller alla typer som behövs för en fråga.

För innehållsfragment baseras GraphQL-scheman (struktur och typer) på **Aktiverad** [Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md) och deras datatyper.

>[!CAUTION]
>
>Alla GraphQL-scheman (härledda från Content Fragment Models som har **Aktiverad**) går att läsa via GraphQL-slutpunkten.
>
>Detta innebär att ni måste se till att inga känsliga uppgifter finns tillgängliga, eftersom de skulle kunna läckas på detta sätt. Detta inkluderar till exempel information som kan finnas som fältnamn i modelldefinitionen.

Om en användare till exempel har skapat en innehållsfragmentmodell som kallas `Article`AEM genererar objektet `article` som är av en typ `ArticleModel`. Fälten i den här typen motsvarar fälten och datatyperna som definieras i modellen.

1. En innehållsfragmentmodell:

   ![Content Fragment Model for use with GraphQL](assets/cfm-graphqlapi-01.png "Content Fragment Model for use with GraphQL")

1. Motsvarande GraphQL-schema (utdata från den automatiska dokumentationen för GraphiQL):
   ![GraphQL-schema baserat på innehållsfragmentmodell](assets/cfm-graphqlapi-02.png "GraphQL-schema baserat på innehållsfragmentmodell")

   Detta visar att den genererade typen `ArticleModel` innehåller flera [fält](#fields).

   * Tre av dem har kontrollerats av användaren: `author`, `main` och `referencearticle`.

   * De andra fälten lades till automatiskt av AEM och representerar användbara metoder för att tillhandahålla information om ett visst innehållsfragment. i det här exemplet `_path`, `_metadata`, `_variations`. Dessa [hjälpfält](#helper-fields) markeras med föregående `_` för att skilja mellan vad som har definierats av användaren och vad som har genererats automatiskt.

1. När en användare har skapat ett innehållsfragment baserat på artikelmodellen kan det sedan förhöras via GraphQL. Mer information finns i [Exempelfrågor](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries) (baserat på [exempelstruktur för innehållsfragment för användning med GraphQL](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)).

I GraphQL for AEM är schemat flexibelt. Det innebär att den genereras automatiskt varje gång en innehållsfragmentmodell skapas, uppdateras eller tas bort. Cacheminnen för dataschemat uppdateras också när du uppdaterar en innehållsfragmentmodell.

Tjänsten Sites GraphQL avlyssnar (i bakgrunden) alla ändringar som görs i en innehållsfragmentmodell. När uppdateringar upptäcks återskapas endast den delen av schemat. Denna optimering sparar tid och ger stabilitet.

Om du till exempel:

1. Installera ett paket som innehåller `Content-Fragment-Model-1` och `Content-Fragment-Model-2`:

   1. GraphQL-typer för `Model-1` och `Model-2` kommer att genereras.

1. Ändra sedan `Content-Fragment-Model-2`:

   1. Endast `Model-2` GraphQL Type kommer att uppdateras.

   1. med beaktande av följande: `Model-1` kommer att förbli desamma.

>[!NOTE]
>
>Detta är viktigt att observera om du vill göra satsvisa uppdateringar på modeller för innehållsfragment via REST-API:t, eller på annat sätt.

Schemat hanteras via samma slutpunkt som GraphQL-frågorna, där klienthanteraren hanterar det faktum att schemat anropas med tillägget `GQLschema`. Du kan till exempel utföra en enkel `GET` begäran på `/content/cq:graphql/global/endpoint.GQLschema` resulterar i utdata från schemat med innehållstypen: `text/x-graphql-schema;charset=iso-8859-1`.

### Schemagenerering - opublicerade modeller {#schema-generation-unpublished-models}

När innehållsfragment är kapslade kan det hända att en överordnad Content Fragment Model publiceras, men ingen refererad modell gör det.

>[!NOTE]
>
>Gränssnittet AEM förhindrar detta, men om publiceringen görs programmatiskt eller med innehållspaket kan det ske.

När detta inträffar genererar AEM en *ofullständig* Schema för den överordnade innehållsfragmentmodellen. Det innebär att fragmentreferensen, som är beroende av den opublicerade modellen, tas bort från schemat.

## Fält {#fields}

Inom schemat finns det enskilda fält av två baskategorier:

* Fält som du genererar.

   Ett urval av [Fälttyper](#field-types) används för att skapa fält baserat på hur du konfigurerar innehållsfragmentmodellen. Fältnamnen hämtas från **Egenskapsnamn** fält för **Datatyp**.

   * Det finns också **Återge som** Egenskaper som ska beaktas, eftersom användare kan konfigurera vissa datatyper. t.ex. som en enda rad eller som ett multifält.

* GraphQL for AEM genererar också ett antal [hjälpfält](#helper-fields).

   Dessa används för att identifiera ett innehållsfragment eller för att få mer information om ett innehållsfragment.

### Fälttyper {#field-types}

GraphQL för AEM har stöd för en lista med typer. Alla Content Fragment Model-datatyper som stöds och motsvarande GraphQL-typer visas:

| Content Fragment Model - datatyp | GraphQL Type | Beskrivning |
|--- |--- |--- |
| Enkelradig text | String, [Sträng] |  Används för enkla strängar som författarnamn, platsnamn osv. |
| Flerradstext | Sträng |  Används för att skriva ut text, t.ex. brödtexten i en artikel |
| Siffra |  Float, [Float] | Används för att visa flyttal och reguljära tal |
| Boolean |  Boolean |  Används för att visa kryssrutor → enkla sant/falskt-satser |
| Datum och tid | Kalender |  Används för att visa datum och tid i ett ISO 8086-format. Beroende på vilken typ som valts finns det tre aromer som kan användas i AEM GraphQL: `onlyDate`, `onlyTime`, `dateTime` |
| Uppräkning |  Sträng |  Används för att visa ett alternativ från en lista med alternativ som definieras när modellen skapas |
|  Taggar |  [Sträng] |  Används för att visa en lista över strängar som representerar taggar som används i AEM |
| Innehållsreferens |  Sträng |  Används för att visa sökvägen till en annan resurs i AEM |
| Fragmentreferens |  *En modelltyp* |  Används för att referera till ett annat innehållsfragment av en viss modelltyp, som definieras när modellen skapades |

### Hjälpfält {#helper-fields}

Förutom datatyperna för användargenererade fält genererar GraphQL för AEM även ett antal *hjälpare* fält för att hjälpa till att identifiera ett innehållsfragment eller för att ge ytterligare information om ett innehållsfragment.

#### Bana {#path}

Sökvägsfältet används som en identifierare i GraphQL. Den representerar sökvägen till Content Fragment-resursen i AEM. Vi har valt detta som identifierare för ett innehållsfragment eftersom det:

* är unikt inom AEM,
* kan enkelt hämtas.

I följande kod visas sökvägarna för alla innehållsfragment som har skapats baserat på modellen för innehållsfragment `Person`.

```xml
{
  personList {
    items {
      _path
    }
  }
}
```

Om du vill hämta ett enstaka innehållsfragment av en viss typ måste du också bestämma sökvägen först. till exempel:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      firstName
      name
    }
  }
}
```

Se [Exempelfråga - Ett enskilt specifikt stadsfragment](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment).

#### Metadata {#metadata}

Via GraphQL visar AEM också metadata för ett innehållsfragment. Metadata är den information som beskriver ett innehållsfragment, till exempel titeln på ett innehållsfragment, miniatyrsökvägen, beskrivningen av ett innehållsfragment och datumet då det skapades, bland annat.

Eftersom metadata genereras via Schemaredigeraren och därför inte har någon särskild struktur, har `TypedMetaData` GraphQL-typ implementerades för att visa metadata för ett innehållsfragment. `TypedMetaData` visar informationen som grupperats med följande skalära typer:

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

Om du till exempel vill hämta titeln för ett innehållsfragment vet vi att den här egenskapen är en String-egenskap, så vi frågar efter alla strängmetadata:

Så här frågar du efter metadata:

```xml
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
>Genom att anropa `stringMetadata` får du en array med alla metadata som lagras i databasen som `String` och om du ringer `stringArrayMetadata` får du en array med alla metadata som lagras i databasen som `String[]`.

Se [Exempelfråga för metadata - Ange metadata för utmärkelserna med namnet GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb).

#### Variationer {#variations}

The `_variations` -fältet har implementerats för att förenkla frågor om variationer som ett innehållsfragment har. Till exempel:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

Se [Exempelfråga - Alla städer med en namngiven variant](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation).

>[!NOTE]
>
>Om den angivna varianten inte finns för ett innehållsfragment returneras den överordnad varianten som ett (fallback) standardvärde.

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL Variables {#graphql-variables}

GraphQL tillåter att variabler placeras i frågan. Mer information finns i [GraphQL-dokumentation för variabler](https://graphql.org/learn/queries/#variables).

Om du till exempel vill hämta alla innehållsfragment av typen `Article` som har en viss variant kan du ange variabeln `variation` i GraphiQL.

![GraphQL Variables](assets/cfm-graphqlapi-03.png "GraphQL Variables")

```xml
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

## GraphQL-direktiv {#graphql-directives}

I GraphQL finns en möjlighet att ändra frågan baserat på variabler, så kallade GraphQL-direktiv.

Du kan till exempel inkludera `adventurePrice` fält i en fråga för alla `AdventureModels`, baserat på en variabel `includePrice`.

![GraphQL-direktiv](assets/cfm-graphqlapi-04.png "GraphQL-direktiv")

```xml
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

Följande (grundläggande) fråga filtrerar till exempel alla personer som har namnet `Jobs` eller `Smith`:

```xml
query {
  personList(filter: {
    name: {
      _logOp: OR
      _expressions: [
        {
          value: "Jobs"
        },
        {
          value: "Smith"
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

Ytterligare exempel finns i:

* information om [GraphQL för AEM tillägg](#graphql-extensions)

* [Exempelfrågor med detta exempelinnehåll och -struktur](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * Och [Exempelinnehåll och struktur](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql) förberedda för användning i provfrågor

* [Exempelfrågor baserade på WKND-projektet](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## GraphQL for AEM - i korthet {#graphql-extensions}

Den grundläggande funktionen för frågor med GraphQL för AEM följer GraphQL standardspecifikation. För GraphQL-frågor med AEM finns det några tillägg:

* Om du behöver ett enda resultat:
   * använda modellnamnet, eg stad

* Om du förväntar dig en resultatlista:
   * add `List` till modellnamnet, till exempel  `cityList`
   * Se [Exempelfråga - All information om alla städer](#sample-all-information-all-cities)

* Filtret `includeVariations` ingår i `List` frågetyp.  Om du vill hämta variationer för innehållsfragment i frågeresultaten väljer du `includeVariations` filter måste anges till `true`.

   >[!CAUTION]
   >Filtret `includeVariations` kan inte användas tillsammans med det systemgenererade fältet `_variation`.

* Om du vill använda ett logiskt OR:
   * use ` _logOp: OR`
   * Se [Exempelfråga - Alla personer som har namnet &quot;Jobs&quot; eller &quot;Smith&quot;](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-all-persons-jobs-smith)

* Logiskt AND finns också, men är (ofta) implicit

* Du kan fråga efter fältnamn som motsvarar fälten i innehållsfragmentmodellen
   * Se [Exempelfråga - Fullständig information om företagets VD och anställda](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-full-details-company-ceos-employees)

* Förutom fälten från modellen finns det vissa systemgenererade fält (föregås av understreck):

   * För innehåll:

      * `_locale` : för att avslöja språket, baserat på Language Manager
         * Se [Exempelfråga för flera innehållsfragment för en viss språkinställning](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-multiple-fragments-given-locale)
      * `_metadata` : för att visa metadata för ditt fragment
         * Se [Exempelfråga för metadata - Ange metadata för utmärkelserna med namnet GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)
      * `_model` : tillåt frågor för en innehållsfragmentmodell (sökväg och rubrik)
         * Se [Exempelfråga för en innehållsfragmentmodell från en modell](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-content-fragment-model-from-model)
      * `_path` : sökvägen till ditt innehållsfragment i databasen
         * Se [Exempelfråga - Ett enskilt specifikt stadsfragment](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)
      * `_reference` : avslöja referenser, inkludera textbundna referenser i RTF-redigeraren
         * Se [Exempelfråga för flera innehållsfragment med förhämtade referenser](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation` : för att visa specifika variationer i ditt innehållsfragment

         >[!NOTE]
         >
         >Om den angivna varianten inte finns för ett innehållsfragment returneras den överordnad varianten som ett (fallback) standardvärde.

         >[!CAUTION]
         >Det systemgenererade fältet `_variation` kan inte användas tillsammans med filtret `includeVariations`.

         * Se [Exempelfråga - Alla städer med en namngiven variant](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)
      * `_tags` : visa ID:n för innehållsfragment eller variationer som innehåller taggar, this is an array of `cq:tags` identifierare.

         * Se [Exempelfråga - namn på alla städer som taggats som stadbrytningar](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-names-all-cities-tagged-city-breaks)
         * Se [Exempelfråga för innehållsfragmentvariationer för en viss modell som har en specifik tagg bifogad](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-fragment-variations-given-model-specific-tag)

         >[!NOTE]
         >
         >Taggar kan också efterfrågas genom att en lista med metadata för ett innehållsfragment visas.
   * Och åtgärder:

      * `_operator` : tillämpa särskilda operatörer, `EQUALS`, `EQUALS_NOT`, `GREATER_EQUAL`, `LOWER`, `CONTAINS`, `STARTS_WITH`
         * Se [Exempelfråga - Alla personer som inte har namnet &quot;Jobs&quot;](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-all-persons-not-jobs)
         * Se [Exempelfråga - Alla annonser där `_path` börjar med ett visst prefix](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply` : tillämpa särskilda villkor, till exempel  `AT_LEAST_ONCE`
         * Se [Exempelfråga - Filtrera en array med ett objekt som måste förekomma minst en gång](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-array-item-occur-at-least-once)
      * `_ignoreCase` : för att ignorera skiftläget vid fråga
         * Se [Exempelfråga - Alla städer med SAN i namnet, oavsett fall](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-all-cities-san-ignore-case)











* GraphQL-unionstyper stöds:

   * use `... on`
      * Se [Exempelfråga för ett innehållsfragment för en viss modell med en innehållsreferens](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-fragment-specific-model-content-reference)

* Reservation vid fråga om kapslade fragment:

   * Om den begärda varianten inte finns i ett kapslat fragment, kommer **Överordnad** kommer att returneras.

### CORS-filter {#cors-filter}

>[!NOTE]
>
>En detaljerad översikt över CORS resursdelningsprincip i AEM finns på [CORS (Cross-Origin Resource Sharing)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html#understand-cross-origin-resource-sharing-(cors)).

För att komma åt GraphQL-slutpunkten måste en CORS-princip konfigureras i kundens Git-databas. Detta görs genom att en lämplig OSGi CORS-konfigurationsfil läggs till för de önskade slutpunkterna.

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

Detta gör du genom att lägga till en lämplig konfigurationsfil för OSGi-referensfiltret som:

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
>* inte använda jokertecken [*] syntax, Detta inaktiverar både autentiserad åtkomst till GraphQL-slutpunkten och exponerar den även för hela världen.


>[!CAUTION]
>
>Alla GraphQL [scheman](#schema-generation) (härleds från Content Fragment Models som har **Aktiverad**) går att läsa via GraphQL-slutpunkten.
>
>Detta innebär att ni måste se till att inga känsliga uppgifter finns tillgängliga, eftersom de skulle kunna läckas på detta sätt. Detta inkluderar till exempel information som kan finnas som fältnamn i modelldefinitionen.

## Autentisering {#authentication}

Se [Autentisering för fjärrfrågor AEM GraphQL-frågor om innehållsfragment](/help/assets/content-fragments/graphql-authentication-content-fragments.md).

## Vanliga frågor {#faqs}

Frågor som har uppstått:

1. **Q**: &quot;*Hur skiljer sig GraphQL API för AEM från Query Builder API?*&quot;

   * **A**: &quot;*AEM GraphQL API ger total kontroll över JSON-utdata och är en branschstandard för att fråga efter innehåll.
AEM planerar att investera i det AEM GraphQL API:t.*&quot;

## Självstudiekurs - Komma igång med AEM Headless och GraphQL {#tutorial}

Söker du en praktisk självstudiekurs? Checka ut [Komma igång med AEM Headless och GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) en komplett självstudiekurs som visar hur man bygger upp och exponerar innehåll med AEM GraphQL API:er och som används av en extern app, i ett headless CMS-scenario.
