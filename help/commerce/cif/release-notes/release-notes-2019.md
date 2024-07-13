---
title: AEM Content and Commerce Release Notes 2019
description: Adobe Experience Manager Content och Commerce Release Notes 2019.
exl-id: 7e61a75d-6b35-46ee-b88a-444c10b2708f
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 4%

---

# Commerce integration framework GitHub Release Overview

## Releasedatum: november 2019

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF | 0.7.1 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF kärnkomponenter | 0.6.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF | 0.6.2 | [Versionsinformation](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nyheter {#what-is-new-november}

* Författare kan förhandsgranska produktinformation och produktlistsidor med produkter/kategorier med ett nytt&quot;Visa med produkt/kategori&quot;-alternativ i Sites Editor.

* Upphovsmannen kan tagga materialet efter produkt-SKU och söka efter produktspecifika mediefiler efter SKU.

* Lägg till/ta bort kupongstöd i kundvagn.

* Betalningsstöd för Braintree har lagts till AEM Venia store front.

### Vad har förbättrats {#what-is-improved-november}

* Kategori-/produktväljare har förbättrats så att den angivna vyn för Adobe Commerce Store respekteras i en konfiguration för flera butiker.

* Reaktionsbaserade komponenter finns tillgängliga som ett nPM-paket. Detta gör att utvecklare kan använda React Components-paketet som ett beroende för ett nytt React-projekt för att anpassa befintliga komponenter eller utveckla nya React-baserade komponenter.

* Anpassningen av GraphQL-frågor förenklas. Detta gör att utvecklare kan anpassa CIF kärnkomponenter med mindre kod.

## Releasedatum: oktober 2019

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF | 0.6.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF kärnkomponenter | 0.5.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF | 0.5.0 | [Versionsinformation](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nyheter {#what-is-new-october}

* Helt redigerbara mallar för produktinformationssidor och produktlistsidor. Nu kan författare skapa mallar och dra och släppa produktlistor och produktinformationskomponenter på dessa mallar. Förutom att lägga till andra komponenter kan författarna nu ändra layouten på mallarna också, vilket ger dem obegränsad frihet att skapa fantastiska upplevelser som kombinerar marknadsförings- och e-handelsinnehåll.

* Alla författarvänliga CIF kärnkomponenter har förbättrats med stöd för [AEM Style System](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/siteandpage/style-system.html). Exempelformat har angetts för produktlistkomponenten.

* Reaktionsbaserade komponenter på klientsidan för kontohantering. Den här versionen har stöd för följande funktioner: Logga in, Har du glömt lösenordet och Skapa ett konto.

### Vad har förbättrats {#what-is-improved-october}

* Produktinformation och produktlistekomponenter har förbättrats så att man kan visa dummy-data och ge författarna en förhandsgranskning av layouten när dessa komponenter placeras på en mall/sida.

* Minicart- och Checkout-komponenterna använder nu React-kopplingar för förbättrad utbyggbarhet.

## Releasedatum: september 2019

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF | 0.5.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF kärnkomponenter | 0.4.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF | 0.4.0 | [Versionsinformation](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nyheter {#what-is-new-september}

* Med funktionen för flera mallar kan författare förbättra en specifik produktinformationssida eller produktlistsida. Författare kan enkelt skapa en anpassad produktinformationssida eller produktlistsida och använda produkt- eller kategoriväljaren för att tilldela den anpassade sidan till en viss produkt eller kategori.

* Koppling till flera kataloger så att författare kan binda flera kataloger i AEM produktkonsol. Författare kan också redigera och visa katalogens bindningsegenskaper efter att bindningen har skapats.

* Reaktionsbaserad kundsidoutcheckning och Mini Cart med GraphQL som stöd för en komplett shoppingresa.

* Komponenten för utcheckning innehåller adressformulär, betalningsval och val av leveransmetod.

### Vad har förbättrats {#what-is-improved-september}

* Product Teaser- och Product Carousel-komponenterna har stöd för produktvarianter.

## Releasedatum: augusti 2019

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF | 0.4.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF kärnkomponenter | 0.3.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF | 0.3.0 | [Versionsinformation](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nyheter {#what-is-new-august}

* Inbäddning CIF Connector i CIF Archetype är valfritt för att ge utvecklare större flexibilitet.

* CIF komponenter som inte är kopplade till den lokala CSS-formateringen så att utvecklare kan använda valfri CSS-formatering.

* Funktion för flera butiker/sajter som tillåter användning av CIF kärnkomponenter i flera AEM webbplatsstrukturer och gör det möjligt för den underliggande GraphQL-klientimplementeringen att ansluta till olika Adobe Commerce-butiksvyer.

* GraphQL-cachning är aktiverat för vissa GraphQL-frågor via HTTP-GET för att minska svarstiden.

* Produktbeskrivningsvyn är aktiverad i AEM.

* Commerce Teaser utökar WCM Teaser-komponenten så att författare även kan lägga till CTA-fält på en produktinformationssida eller en produktlistsida.

* Knapp som tillåter författare att placera på en AEM sida och länka till antingen en AEM, produktinformationssida, produktlistsida eller en extern länk.

### Vad har förbättrats {#what-is-improved-august}

* Adobe Commerce Store-konfigurationen har flyttats från OSGi till AEM produktkonsol för att göra integreringskonfigurationen mer redigeringsvänlig.

## Releasedatum: juli 2019

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF | 0.3.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF kärnkomponenter | 0.2.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF | 0.2.0 | [Versionsinformation](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nyheter {#what-is-new-july}

* Första CIF-arkitekturen som ger utvecklare flera distributionsalternativ: 1. Distribuera AEM Venia storefront 2. Driftsätt ställningar för ett nytt projekt 3. Använd CIF element i ett befintligt projekt

* Katalognavigering på flera nivåer som stöder navigering genom kategorier och underkategorier.

* Sidindelning på kategorisidor för bättre användargränssnitt.

* Klientåtergivning av prisattribut i komponenterna Produktinformation och Produktlista som stöder återgivning av dynamiska attribut.

* ProduktCarousel på serversidan för att visa en lista över produkter i karusellstil.

* Aktuell kategorilista på serversidan om du vill visa en lista med kategorier på en AEM sida.

### Vad har förbättrats {#what-is-improved-july}

* Stöd för Adobe Commerce 2.3.2 och felkorrigeringar för produktegenskaper visas i produktkonsolen.

## Releasedatum: juni 2019

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF | 0.2.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF kärnkomponenter | 0.1.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |

### Nyheter {#what-is-new-june}

* AEM B2C-butiken med Venia CSS-format för mobilen först, landningssida, dynamisk katalognavigering via produkt- och kategorisidor, produktsöksidor och kundvagnsfunktioner för att komma igång med och snabba upp affärsprojekt.

* CIF Connector och redigeringsverktyg (produktkonsol, produktväljare och kategoriväljare) som gör det möjligt för författare att skapa upplevelser i AEM med e-handelsinnehåll.

* Första versionen av CIF Core Components som är kompatibla med Adobe Commerce 2.3.1:
   * Produktinformation
   * Produktlista
   * Product Teaser
   * Navigering
   * Produktsökning
   * Kundvagn (REST)
