---
title: Utveckla SPA för Adobe Experience Manager
description: I den här artikeln finns viktiga frågor att tänka på när en frontendutvecklare ska utveckla en SPA för Adobe Experience Manager (AEM) och en översikt över AEM arkitektur för SPA som ska beaktas när en utvecklad SPA distribueras på AEM.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: c1429889-e2ed-4e2f-a45f-33f8a6a52745
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '2051'
ht-degree: 0%

---

# Utveckla SPA för AEM{#developing-spas-for-aem}

Single page applications (SPA) can offer compelling experiences for website users. Utvecklare vill kunna skapa webbplatser med SPA ramverk och författare vill smidigt redigera innehåll i Adobe Experience Manager (AEM) för en webbplats som skapats med sådana ramverk.

I den här artikeln finns viktiga frågor att tänka på när en frontutvecklare ska utveckla en SPA för AEM och en översikt över arkitekturen i AEM för att distribuera SPA på AEM.

>[!NOTE]
>
>SPA Editor är den rekommenderade lösningen för projekt som kräver SPA ramverksbaserad rendering på klientsidan (till exempel React eller Angular).

## SPA för AEM {#spa-development-principles-for-aem}

Utveckla single page-applikationer AEM förutsätter att frontutvecklaren följer vedertagna standarder när han skapar en SPA. Om du som gränssnittsutvecklare följer dessa allmänna bästa metoder och några AEM specifika principer fungerar SPA med [AEM och funktioner för att skapa innehåll](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa).

* **[Portabilitet](/help/sites-developing/spa-architecture.md#portability) -** Precis som med andra komponenter bör komponenterna vara så flyttbara som möjligt. SPA bör byggas med rörliga och återanvändbara komponenter.
* **[AEM diskar platsstruktur](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)** - Utvecklaren skapar komponenter och äger sin interna struktur, men använder AEM för att definiera webbplatsens innehållsstruktur.
* **[Dynamisk återgivning](/help/sites-developing/spa-architecture.md#dynamic-rendering)** - All återgivning ska vara dynamisk.
* **[Dynamisk routning](#dynamic-routing) -** SPA ansvarar för routningen och AEM lyssnar på den och hämtar baserat på den. Alla routningar ska också vara dynamiska.

Om du håller dessa principer i åtanke när du utvecklar SPA blir det så flexibelt och säkert som möjligt i framtiden, samtidigt som du aktiverar alla funktioner för AEM som stöds.

Om du inte behöver stöd för AEM redigeringsfunktioner kan du behöva överväga ett annat [SPA designmodell](/help/sites-developing/spa-architecture.md#spa-design-models).

### Portabilitet {#portability}

Precis som när du utvecklar en komponent bör dina komponenter utformas på ett sådant sätt att de blir så bärbara som möjligt. Mönster som motverkar komponenternas bärbarhet eller återanvändbarhet bör undvikas för att säkerställa kompatibilitet, flexibilitet och underhållbarhet.

Den resulterande SPA ska byggas med mycket portabla och återanvändbara komponenter.

### AEM diskar platsstruktur {#aem-drives-site-structure}

Utvecklaren måste tänka på sig själv som ansvarig för att skapa ett bibliotek med SPA komponenter som används för att bygga appen. Utvecklaren har fullständig kontroll över komponenternas interna struktur. [AEM äger dock alltid platsens struktur.](/help/sites-developing/spa-overview.md)

Det innebär att frontendutvecklaren kan lägga till kundinnehåll före eller efter startpunkten för komponenterna och även göra tredjepartsanrop inuti komponenten. Utvecklaren har dock inte fullständig kontroll över hur komponenterna kapslas, till exempel.

### Dynamisk återgivning {#dynamic-rendering}

SPA ska endast förlita sig på dynamisk återgivning av innehåll. Detta är standardförväntningen där AEM hämtar och återger alla underordnade element i innehållsstrukturen.

All explicit återgivning som pekar på visst innehåll betraktas som statisk återgivning och även om den stöds kommer den inte att vara kompatibel med AEM innehållsredigeringsfunktioner. Detta strider också mot principen om [bärbarhet](/help/sites-developing/spa-architecture.md#portability).

### Dynamisk routning {#dynamic-routing}

Precis som vid återgivning ska all routning också vara dynamisk. AEM [SPA ska alltid äga routningen](/help/sites-developing/spa-routing.md) och AEM lyssnar på den och hämtar innehåll baserat på den.

Alla statiska routningar fungerar mot [bärbarhetsprincip](/help/sites-developing/spa-architecture.md#portability) och begränsar författaren genom att inte vara kompatibel med redigeringsfunktionerna i AEM. Om innehållsförfattaren till exempel vill ändra en väg eller ändra en sida med statisk routning måste han eller hon be frontutvecklaren att göra det.

## AEM Project Archettype {#aem-project-archetype}

Alla AEM ska använda [AEM Project Archettype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html), som stöder SPA projekt med React eller Angular och använder SPA SDK.

## SPA designmodeller {#spa-design-models}

Om [principer för utveckling av SPA inom AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem) följer du SPA med alla funktioner som stöds AEM innehållsredigeringsfunktionen.

Det kan dock finnas fall där detta inte är helt nödvändigt. Tabellen nedan ger en översikt över de olika designmodellerna, deras fördelar och nackdelar.

<table>
 <tbody>
  <tr>
   <th><strong>Designmodell<br /> </strong></th>
   <th><strong>Fördelar</strong></th>
   <th><strong>Nackdelar</strong></th>
  </tr>
  <tr>
   <td>AEM används som headless CMS utan att använda <a href="/help/sites-developing/spa-reference-materials.md">SPA SDK-ramverket.</a></td>
   <td>Utvecklaren har fullständig kontroll över appen.</td>
   <td><p>Innehållsförfattare kan inte använda AEM.</p> <p>Koden är inte portabel eller återanvändbar om den innehåller statiska referenser eller routning.</p> <p>Det går inte att använda mallredigeraren, så frontendutvecklaren måste underhålla redigerbara mallar via JCR.</p> </td>
  </tr>
  <tr>
   <td>Utvecklaren använder SDK-ramverket för SPA Editor, men bara vissa områden öppnas för innehållsförfattaren.</td>
   <td>Utvecklaren behåller kontrollen över appen genom att endast aktivera redigering i begränsade delar av appen.</td>
   <td><p>Innehållsförfattare är begränsade till en begränsad uppsättning AEM upplevelser.</p> <p>Koden kan varken vara flyttbar eller återanvändbar om den innehåller statiska referenser eller routning.</p> <p>Det går inte att använda mallredigeraren, så frontendutvecklaren måste underhålla redigerbara mallar via JCR.</p> </td>
  </tr>
  <tr>
   <td>I projektet används SPA Editor SDK fullt ut och klientkomponenterna utvecklas som ett bibliotek och innehållsstrukturen i programmet delegeras till AEM.</td>
   <td><p>Appen är återanvändbar och portabel.</p> <p>Innehållsförfattaren kan redigera appen med hjälp av AEM.<br /> </p> <p>SPA är kompatibelt med mallredigeraren.</p> </td>
   <td><p>Utvecklaren har inte kontroll över programmets struktur och den del av innehållet som har delegerats till AEM.</p> <p>Utvecklaren kan fortfarande reservera områden i programmet för innehåll som inte ska redigeras med AEM.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Även om alla modeller stöds i AEM, är det bara genom att implementera den tredje (och därför följa den rekommenderade [SPA utvecklingsprinciper inom AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)) kan skribenter interagera med och redigera innehållet i SPA i AEM som de är vana vid.

## Migrerar befintliga SPA till AEM {#migrating-existing-spas-to-aem}

Om SPA följer [SPA för AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem), fungerar SPA i AEM och kan redigeras med AEM SPA Editor.

Följ de här stegen för att göra dina befintliga SPA redo att arbeta med AEM.

1. **Gör dina JS-komponenter modulära.**

   Gör dem kapabla att återges i valfri ordning, position och storlek.
1. **Använd behållarna från Adobe SDK för att placera dina komponenter på skärmen.**

   AEM innehåller en sid- och styckesystemkomponent som du kan använda.
1. **Skapa en AEM för varje JS-komponent.**

   De AEM komponenterna definierar dialogrutan och JSON-utdata.

## Instruktioner för gränssnittsutvecklare {#instructions-for-front-end-developers}

Den främsta uppgiften att engagera en gränssnittsutvecklare för att skapa en SPA för AEM är att komma överens om komponenterna och deras JSON-modeller.

Här följer en översikt över de steg som en frontendutvecklare måste följa när han eller hon utvecklar en SPA för AEM.

1. **Godkänn komponenterna och deras JSON-modell**

   Utvecklare och AEM måste komma överens om vilka komponenter som är nödvändiga och en modell så att det går att hitta en exakt motsvarighet mellan komponenterna SPA bakomliggande komponenter.

   AEM är fortfarande nödvändiga för att kunna tillhandahålla redigeringsdialogrutor och exportera komponentmodellen.

1. **I React-komponenter får du åtkomst till modellen via`this.props.cqModel`**

   När komponenterna är överenskomna och JSON-modellen är på plats kan den som utvecklar SPA utveckla den och enkelt komma åt JSON-modellen via `this.props.cqModel`.

1. **Implementera komponentens `render()` method**

   Utvecklaren implementerar `render()` metoden så som den passar och kan använda fälten i `cqModel` -egenskap. Då skrivs DOM- och HTML-fragmenten som infogas på sidan ut. Det här är standardsättet att bygga en app i React.

1. **Mappa komponenten till AEM-resurstypen via`MapTo()`**

   Mappningen lagrar komponentklasser och används internt av den angivna `Container` för att hämta och dynamiskt instansiera komponenter baserat på den angivna resurstypen.

   Det här fungerar som en&quot;limma&quot; mellan fram- och bakände så att redigeraren vet vilka komponenter som de olika reaktionskomponenterna motsvarar.

   The `Page` och `ResponsiveGrid` är bra exempel på klasser som utökar basen `Container`.

1. **Definiera komponentens `EditConfig` som parameter till`MapTo()`**

   Den här parametern är nödvändig för att tala om för redigeraren hur komponenten ska namnges så länge som den inte har återgetts eller inte har något innehåll att återge.

1. **Utöka den angivna `Container` klass för sidor och behållare**

   Sidor och styckesystem bör utöka den här klassen så att delegering till inre komponenter fungerar som förväntat.

1. **Implementera en routningslösning som använder HTML5 `History` API.**

   När `ModelRouter` är aktiverat, anropar `pushState` och `replaceState` funktioner som utlöser en begäran till `PageModelManager` för att hämta ett saknat fragment av modellen.

   Den aktuella versionen av `ModelRouter` stöder endast användning av URL:er som pekar på den faktiska resurssökvägen för Sling Model-startpunkter. Det stöder inte användning av vanity-URL:er eller alias.

   The `ModelRouter` kan inaktiveras eller konfigureras för att ignorera en lista med reguljära uttryck.

## AEM {#aem-agnostic}

Dessa kodblock illustrerar hur komponenterna React och Angular inte behöver något som är specifikt för Adobe eller AEM.

* Allt som finns inuti JavaScript-komponenten är AEM-agnostiskt.
* Men det som är specifikt för AEM är att JS-komponenten måste mappas till en AEM med MapTo-hjälpen.

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

The `MapTo` helper är den limning som gör att bakände och framände kan matchas ihop:

* Den talar om för JS-behållaren (eller JS-styckesystemet) vilken JS-komponent som ansvarar för återgivningen av varje komponent som finns i JSON.
* Det lägger till ett dataattribut för HTML i HTML som JS-komponenten återger, så att SPA Editor vet vilken dialogruta som ska visas för författaren när komponenten redigeras.

Mer information om hur du använder `MapTo` och skapa SPA för AEM i allmänhet, se Komma igång-guiden för ditt valda ramverk.

* [Getting Started with SPA in AEM - React](/help/sites-developing/spa-getting-started-react.md)
* [Komma igång med SPA i AEM - Angular](/help/sites-developing/spa-getting-started-angular.md)

## AEM och SPA {#aem-architecture-and-spas}

Den allmänna arkitekturen för AEM, inklusive utvecklings-, skribent- och publiceringsmiljöer, förändras inte när SPA används. Men det är bra att förstå hur SPA kan integreras i arkitekturen.

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **Bygg miljö**

  Det är här som källan för SPA programkälla och komponentkälla checkas ut.

   * NPM-generatorn för klientlib skapar ett klientbibliotek från SPA.
   * Biblioteket tas av Maven och distribueras av Maven Build-pluginen tillsammans med komponenten till AEM författare.

* **AEM**

  Innehåll skapas på AEM författare, inklusive SPA.

  När en SPA redigeras med SPA Editor i redigeringsmiljön:

   1. SPA begär yttre HTML.
   1. CSS läses in.
   1. JavaScript-koden för det SPA programmet läses in.
   1. När SPA körs begärs JSON, vilket gör att programmet kan skapa sidans DOM inklusive `cq-data` attribut.
   1. Detta `cq-data` kan redigeraren läsa in ytterligare sidinformation så att den vet vilka redigeringskonfigurationer som är tillgängliga för komponenterna.

* **AEM Publish**

  Det är här som det innehåll och de kompilerade biblioteken, inklusive SPA, programartefakter, klientlibs och komponenter publiceras för allmänheten.

* **Dispatcher/CDN**

  Dispatcher fungerar som AEM för webbplatsens besökare.

   * Förfrågningar behandlas på samma sätt som de behandlas i AEM författare, men det finns ingen begäran om sidinformation eftersom detta bara behövs av redigeraren.
   * JavaScript, CSS, JSON och HTML cachelagras, vilket optimerar sidan för snabb leverans.

>[!NOTE]
>
>I AEM finns ingen anledning att köra JavaScript-byggmekanismer eller själva JavaScript. AEM är bara värd för de kompilerade artefakterna från det SPA programmet.

## Nästa steg {#next-steps}

En översikt över hur en enkel SPA i AEM är strukturerad och hur den fungerar finns i guiden Komma igång för båda [Reagera](/help/sites-developing/spa-getting-started-react.md) och [Angular](/help/sites-developing/spa-getting-started-angular.md).

En steg-för-steg-guide till hur du skapar egna SPA finns i [Getting Started with the AEM SPA Editor - WKND Events Tutorial](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

Mer information om den dynamiska modellen till komponentmappning och hur den fungerar i SPA i AEM finns i artikeln [Dynamisk mappning av modell till komponent för SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Om du vill implementera SPA i AEM för ett annat ramverk än React eller Angular eller bara vill ta en grundlig titt på hur SPA SDK för AEM fungerar, se [SPA](/help/sites-developing/spa-blueprint.md) artikel.
