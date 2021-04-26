---
title: AEM Content and Commerce Release Notes 2021
description: AEM Content and Commerce Release Notes 2021
translation-type: tm+mt
source-git-commit: c2fb9af056fa4be13cfd7e60e8a44485e8712c0b
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 6%

---

# GitHub-versionsöversikt för Commerce Integration Framework

## Releasedatum: November 2019

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF Connector | 0.7.1 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF-kärnkomponenter | 0.6.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF-arkityp | 0.6.2 | [Versionsinformation](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nyheter {#what-is-new-november}

* Författare kan förhandsgranska produktinformation och produktlistsidor med produkter/kategorier med ett nytt&quot;Visa med produkt/kategori&quot;-alternativ i Sites Editor.

* Upphovsmannen kan tagga materialet efter produkt-SKU och söka efter produktspecifika mediefiler efter SKU.

* Lägg till/ta bort kupongstöd i kundvagn.

* Betalningsstöd för Braintree har lagts till AEM Venia store front.

### Förbättringar {#what-is-improved-november}

* Kategori-/produktväljare har förbättrats så att den angivna Magento-butiksvyn respekteras i en konfiguration med flera butiker.

* Reaktionsbaserade komponenter som finns som nPM-paket. Detta gör att utvecklare kan använda React Components-paketet som ett beroende för ett nytt React-projekt för att anpassa befintliga komponenter eller utveckla nya React-baserade komponenter.

* Anpassningen av GraphQL-frågan har förenklats. Detta gör att utvecklare kan anpassa CIF-kärnkomponenter med mindre kod.

## Releasedatum: Oktober 2019

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF Connector | 0.6.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF-kärnkomponenter | 0.5.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF-arkityp | 0.5.0 | [Versionsinformation](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nyheter {#what-is-new-october}

* Helt redigerbara mallar för produktinformationssidor och produktlistsidor. Nu kan författare skapa nya mallar och dra och släppa produktlistor och produktinformationskomponenter på dessa mallar. Förutom att lägga till andra komponenter kan författarna nu ändra layouten på mallarna också, vilket ger dem obegränsad frihet att skapa fantastiska upplevelser som kombinerar marknadsförings- och e-handelsinnehåll.

* Alla redigeringsvänliga CIF-kärnkomponenter har förbättrats med stöd för [AEM Style System](https://helpx.adobe.com/experience-manager/6-5/sites/authoring/using/style-system.html). Exempelformat har angetts för produktlistkomponenten.

* Reaktionsbaserade komponenter på klientsidan för kontohantering. Den här versionen har stöd för följande funktioner: Logga in, Glömt lösenordet och Skapa konto.

### Förbättringar {#what-is-improved-october}

* Produktinformation och produktlistekomponenter har förbättrats så att man kan visa dummy-data och ge författarna en förhandsgranskning av layouten när dessa komponenter placeras på en mall/sida.

* Minicart- och Checkout-komponenterna använder nu React-kopplingar för förbättrad utbyggbarhet.

## Releasedatum: September 2019

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF Connector | 0.5.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF-kärnkomponenter | 0.4.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF-arkityp | 0.4.0 | [Versionsinformation](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nyheter {#what-is-new-september}

* Funktion för flera mallar som tillåter författare att utöka en specifik produktinformationssida eller produktlistsida. Författare kan enkelt skapa en anpassad produktinformationssida eller produktlistsida och använda produkt- eller kategoriväljaren för att tilldela den anpassade sidan till en viss produkt eller kategori(er).

* Koppling till flera kataloger så att författare kan binda flera kataloger i AEM produktkonsol. Författare kan också redigera och visa katalogens bindningsegenskaper efter att bindningen har skapats.

* Reaktionsbaserad kundsidoutcheckning och Mini Cart med GraphQL som stöd för en komplett grundläggande shoppingresa.

* Utcheckningskomponenten innehåller adressformulär, betalningsval och val av leveransmetod.

### Förbättringar {#what-is-improved-september}

* Product Teaser- och Product Carousel-komponenterna har stöd för produktvarianter.

## Releasedatum: Augusti 2019

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF Connector | 0.4.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF-kärnkomponenter | 0.3.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF-arkityp | 0.3.0 | [Versionsinformation](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nyheter {#what-is-new-august}

* Inbäddning av CIF Connector i CIF-arkitekturen är valfritt för att ge utvecklare större flexibilitet.

* CIF-komponenter som inte är kopplade till den lokala CSS-formateringen så att utvecklare kan använda valfri CSS-formatering.

* Funktion för flera butiker/sajter som tillåter användning av CIF Core-komponenter på flera AEM platsstrukturer och gör det möjligt för den underliggande GraphQL-klientimplementeringen att ansluta till olika Magento store-/store-vyer.

* GraphQL-cachelagring aktiverad för vissa GraphQL-frågor via HTTP-GET för att minska svarstiden.

* Produktbeskrivningsvyn är aktiverad i AEM.

* Commerce Teaser utökar WCM Teaser-komponenten så att författare även kan lägga till CTA-fält på en produktinformationssida eller en produktlistsida.

* Knapp som tillåter författare att placera på en AEM sida och länka till antingen en AEM, produktinformationssida, produktlistsida eller en extern länk.

### Förbättringar {#what-is-improved-august}

* Magento store-konfigurationen flyttades från OSGi till AEM produktkonsolen för att göra integreringskonfigurationen mer författarvänlig.

## Releasedatum: Juli 2019

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF Connector | 0.3.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF-kärnkomponenter | 0.2.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF-arkityp | 0.2.0 | [Versionsinformation](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nyheter {#what-is-new-july}

* Den första CIF-arkitekturen som ger utvecklare flera distributionsalternativ: 1. Driftsätt AEM Venia storefront 2. Installera ställningar för ett nytt projekt 3. Använd CIF-element i ett befintligt projekt

* Katalognavigering på flera nivåer som stöder navigering genom kategorier och underkategorier.

* Sidindelning på kategorisidor för bättre användargränssnitt.

* Klientåtergivning av prisattribut i komponenterna Produktinformation och Produktlista som stöder återgivning av dynamiska attribut.

* ProduktCarousel på serversidan för att visa en lista över produkter i karusellstil.

* Aktuell kategorilista på serversidan om du vill visa en lista över kategorier på en AEM.

### Förbättringar {#what-is-improved-july}

* Stöd för Magento 2.3.2 och felkorrigeringar för produktegenskaper visas i produktkonsolen.

## Releasedatum: Juni 2019

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF Connector | 0.2.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF-kärnkomponenter | 0.1.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |

### Nyheter {#what-is-new-june}

* AEM B2C-butiken med Venia CSS-format för mobilen först, landningssida, dynamisk katalognavigering via produkt- och kategorisidor, produktsöksidor och kundvagnsfunktioner för att komma igång med och snabba upp affärsprojekt.

* CIF Connector och redigeringsverktyg (produktkonsol, produktväljare och kategoriväljare) som gör att författare kan skapa upplevelser i AEM med e-handelsinnehåll.

* Första versionen av CIF Core Components kompatibel med Magento 2.3.1:
   * Produktinformation
   * Produktlista
   * Product Teaser
   * Navigering
   * Produktsökning
   * Kundvagn (REST)

