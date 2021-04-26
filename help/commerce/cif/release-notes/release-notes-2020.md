---
title: AEM Content and Commerce Release Notes 2021
description: AEM Content and Commerce Release Notes 2021
translation-type: tm+mt
source-git-commit: c859aa89e481e852302e9cda0adf2acc04d68a55
workflow-type: tm+mt
source-wordcount: '1323'
ht-degree: 8%

---


# GitHub-versionsöversikt för Commerce Integration Framework

## Releasedatum: November 2020

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF Connector | 1.6.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF-kärnkomponenter | 1.6.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venias referenswebbplats | 2020.12.01 | [Versionsinformation](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nyheter {#what-is-new-november}

* Mallarv har lagts till på en viss kategorisida. Den här funktionen förbättrar effektiviteten för affärsanvändare eftersom det gör det möjligt för alla underkategorier att ärva mallen som skapades för en viss toppkategori.

* Platinas referensarkiv har uppdaterats för att använda Experience Fragment för sidfoten. Affärsanvändare kan redigera sidfoten med hjälp AEM redigeringsverktyg.

### Förbättringar {#what-is-improved-november}

* Utcheckningskomponenten har förbättrats för att ge kunderna möjlighet att komma in i destinationslandet för att tillåta fakturerings-/leveransadresser utanför USA.

* Navigeringskomponenten har utökats till att hydratisera Adobe-klientdatalagret.

* Flera felkorrigeringar.

## Releasedatum: Oktober 2020

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF Connector | 1.5.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF-kärnkomponenter | 1.5.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venias referenswebbplats | 2020.10.27 | [Versionsinformation](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nyheter {#what-is-new-october}

* En ny kategoriCarousel-komponent har lagts till för att göra det möjligt för affärsanvändare att dra och släppa den här komponenten på AEM innehållssidor för att berika innehållssidor med handelsdata.

* CIF-kärnkomponenter har utökats för att hydratisera Adobe Client Data Layer genom att skicka e-handelsdata. Adobe Client Data Layer är en standardiserad metod för att samla in data och kommunicera data till digitala analyser och rapportservrar. Mer information finns i [Adobe Client Data Layer](https://github.com/adobe/adobe-client-data-layer/wiki).

* Sidorna Produktinformation och Produktlista utökas för att automatiskt fylla i SEO-metadata (t.ex. titel, metabeskrivning, metanyckelord) som konfigurerats inifrån Magento Admin UI

* Fel i Commerce teaser-komponent har åtgärdats.

## Releasedatum: September 2020

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF Connector | 1.4.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF-kärnkomponenter | 1.4.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venias referenswebbplats | 2020.10.2 | [Versionsinformation](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nyheter {#what-is-new-september}

* Stöder frågor för Magento 2.4.0 Schema.

* Funktioner för kontoinformation har lagts till så att kunderna kan uppdatera personlig information.

* Lazy loading av sidnumreringsformat som implementerats för produktlistor och sökresultatsidor för att utvecklare ska kunna konfigurera de här komponenterna så att knappen Läs in mer visas som sidnumreringsformat.

* Sidan för återställning av lösenord har implementerats så att kunderna kan uppdatera/återställa sitt kontolösenord.

* Stöd för tillgängliga produkttyper.

* Utvecklare kan konfigurera HTML-taggarna för komponenterna Product Carousel, Related Products och Featured Category List så att de följer SEO:s bästa praxis.

* Mina kontobuggar har åtgärdats.

* Flera felkorrigeringar.

## Releasedatum: Augusti 2020

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF Connector | 1.3.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF-kärnkomponenter | 1.3.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venias referenswebbplats | 2020.9.2 | [Versionsinformation](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nyheter {#what-is-new-august}

* Breadcrumb-komponenten har lagts till för att stödja innehålls- och e-handelssidor.

* Fliken Commerce har lagts till i sidegenskaper för att visa CIF-egenskaper för landningssidor och upplevelsefragment.

* Sökfältskomponenten har förbättrats med stöd för att visa platshållartext

* Flexibilitet i komponenterna Product och Product Teaser ger stöd för enkla anpassningar.

* Flexibilitet att åsidosätta och konfigurera CTA-knappetiketten för Product Teaser-komponenten har lagts till.

* Adressbokskomponenten har förbättrats så att registrerade kunder kan välja frakt- och faktureringsadresser som sparats i adressboken under utcheckningen.

* Flera felkorrigeringar.

## Releasedatum: Juli 2020

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF Connector | 1.2.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF-kärnkomponenter | 1.2.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venias referenswebbplats | 2020.8.14 | [Versionsinformation](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nyheter {#what-is-new-july}

* CIF Venia Reference Site extraherades från CIF Archetype-repo och är nu en fristående GitHub-databas.

* CIF-arkityp som sammanfogats med AEM Project Archetype. Använd [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) som startpunkt för nya projekt.

* Adressbokshantering har lagts till för att tillåta inloggade användare att hantera sina adresser.

* CIF Cloud Configuration UI har stöd för publicerings-/avpubliceringsåtgärder.

### Förbättringar {#what-is-improved-july}

* Inloggningskomponenten har flyttats till listrutan Användare för enkel åtkomst.

* Förenklat paketet med aem-core-cif-affischkomponenter.

* Flera felkorrigeringar.

## Releasedatum: Juni 2020

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF Connector | 1.1.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF-kärnkomponenter | 1.1.1 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF-arkityp | 0.11.0 | [Versionsinformation](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nyheter {#what-is-new-june}

Detta är den första versionen av CIF Core Components som stöds i Adobe Experience Manager.

* Produktsorteringen har lagts till på sidan Produktlista och sidan Sökresultat så att kunderna kan sortera baserat på relevans, pris och produktnamn.

* Kategorifiltrering har lagts till som en fasett så att kunderna kan filtrera baserat på kategori.

* Tjänstanvändarmappning har lagts till som en del av säkerhetskraven för att säkerställa åtkomst till /conf via tjänstanvändare och inte genom att direkt ändra åtkomstkontrollistor. CIF Core Components måste nu använda en tjänstanvändare för att få åtkomst till konfigurationer.

### Förbättringar {#what-is-improved-june}

* Sidan Produktlista och sidan Sökresultat visar totalt antal objekt. Antalet objekt uppdateras när användaren använder filter.

* Fasetterad sökning optimerad genom att kombinera kategorifrågan med produktsökfrågan.

* Kategori-/produktväljare för sidförhandsgranskning följer cq:catalogPath.

* Flera felkorrigeringar.

## Releasedatum: Maj 2020

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF Connector | 1.0.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF-kärnkomponenter | 1.0.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF-arkityp | 0.11.0 | [Versionsinformation](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nyheter {#what-is-new-may}

* Stöder frågor för Magento 2.3.5 Schema.

* Stöd för fasetterad sökning har lagts till i sidan Sök och produktlista så att kunderna kan filtrera sökresultat baserat på produktaspekter.

* Ny OSGi-tjänst har lagts till för att anpassa PDP/PLP-URL:er för SEO. Mer information finns i den här [dokumentationen](https://github.com/adobe/aem-core-cif-components/wiki/configuration).

* Produktbindning skapas automatiskt när en molnkonfiguration skapas.

### Förbättringar

* Molnkonfigurationen har utökats så att åtgärden Skapa mapp visas.

* Flera felkorrigeringar har tillämpats.

## Releasedatum: April, 2020

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF Connector | 0.10.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF-kärnkomponenter | 0.10.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF-arkityp | 0.10.0 | [Versionsinformation](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nyheter {#what-is-new-april}

* Konfigurationsinställningar för CIF Connector är enhetliga och förenklade. Mer information finns i avsnittet [Komma igång](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html) eller [Nya AEM CIF-projektinställningar](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html#!AdobeDocs/commerce-cif-documentation/master/getting-started/02-new-cif-project.md)

### Förbättringar {#what-is-improved-april}

* Kundvagn- och utcheckningsflödet har utökats för att stödja registrerade kunder.

* Utökat stöd för internationalisering i alla komponenter.

* Stöd för grupperade produkter och virtuella produkter finns.

* Komponenter i relaterade produkter, produktkaruseller och den aktuella kategorin har förbättrats för att ge stöd åt valfri titel.

* Flera felkorrigeringar har tillämpats.

## Releasedatum: Februari 2020

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF Connector | 0.9.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF-kärnkomponenter | 0.9.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF-arkityp | 0.9.0 | [Versionsinformation](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nyheter {#what-is-new-february}

* Stöder frågor för Magento 2.3.4 Schema.

* Tillagt sökstöd i kategoriväljaren.

* Sidnumrering i komponenten Catogory List som stöder stora kataloguppsättningar.

### Förbättringar {#what-is-improved-february}

* Kundvagnen har förbättrats och visar rabatter.

* Produktinformation, Product Teaser och Product List-komponenter har stöd för visning av avancerad prisinformation.

* Produktsökning i produktkonsolen och produktväljaren har förbättrats.

* Flera felkorrigeringar har tillämpats.

## Releasedatum: Januari 2020

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF Connector | 0.8.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF-kärnkomponenter | 0.8.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF-arkityp | 0.7.0 | [Versionsinformation](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nyheter {#what-is-new-january}

* Komponenten Experience Fragment (XF) har lagts till så att kunderna kan skapa XF i sina e-handelsprojekt.

* Ändra lösenordsfunktionaliteten som finns på mitt konto.

* i18n-stöd för AEM CIF-kärnkomponenter på serversidan.

* Allmän relaterad produktkomponent tillgänglig.

### Förbättringar {#what-is-improved-january}

* Stöd för att visa CTA-knappen på produktsuddgummit.

* Alternativ för att ändra/välja bilder i komponenten Kategorilista.

* Alternativ för att dölja/visa rubrik/banderoll i produktlistkomponenten.

* Dra-och-släpp-funktionen som används på Product Carousel-komponenten.

* Flera felkorrigeringar har tillämpats.
