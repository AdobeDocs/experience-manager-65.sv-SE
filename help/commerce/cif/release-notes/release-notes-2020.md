---
title: AEM Content and Commerce Release Notes 2020
description: Adobe Experience Manager Content and Commerce Release Notes 2020.
exl-id: 440ecd8e-55dc-4606-8678-c65cda1d2b3a
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 6%

---

# Commerce integration framework GitHub Release Overview

## Releasedatum: november 2020

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF | 1.6.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF kärnkomponenter | 1.6.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia Reference Site | 2020.12.01 | [Versionsinformation](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nyheter {#what-is-new-november}

* Mallarv har lagts till på en viss kategorisida. Den här funktionen förbättrar effektiviteten för affärsanvändare eftersom det gör det möjligt för alla underkategorier att ärva mallen som skapades för en viss toppkategori.

* Platinas referensarkiv har uppdaterats för att använda Experience Fragment för sidfoten. Affärsanvändare kan redigera sidfoten med hjälp AEM redigeringsverktyg.

### Vad har förbättrats {#what-is-improved-november}

* Utcheckningskomponenten har förbättrats för att ge kunderna möjlighet att komma in i destinationslandet för att tillåta fakturerings-/leveransadresser utanför USA.

* Navigeringskomponenten har utökats till att hydratisera Adobe-klientdatalagret.

* Flera felkorrigeringar.

## Releasedatum: oktober 2020

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF | 1.5.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF kärnkomponenter | 1.5.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia Reference Site | 2020.10.27 | [Versionsinformation](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nyheter {#what-is-new-october}

* En ny kategoriCarousel-komponent lades till för att göra det möjligt för företagsanvändare att dra och släppa den här komponenten på AEM innehållssidor för att berika innehållssidor med handelsdata.

* CIF kärnkomponenter har utökats för att utrusta Adobe Client Data Layer genom att skicka e-handelsdata. Adobe Client Data Layer är en standardiserad metod för att samla in data och kommunicera data till digitala analyser och rapportservrar. Mer information finns i [Adobe-klientdatalagret](https://github.com/adobe/adobe-client-data-layer/wiki).

* Sidorna Produktinformation och Produktlista utökas för att automatiskt fylla i SEO-metadata (som titel, metabeskrivning, meta-nyckelord) som konfigurerats inifrån Adobe Commerce administratörsgränssnitt

* Commerce teaser Component bug har åtgärdats.

## Releasedatum: september 2020

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF | 1.4.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF kärnkomponenter | 1.4.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia Reference Site | 2020.10.2 | [Versionsinformation](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nyheter {#what-is-new-september}

* Stöder frågor för Adobe Commerce 2.4.0 Schema.

* Funktioner för kontoinformation har lagts till så att kunderna kan uppdatera personlig information.

* En lat sidnumreringsstil för inläsning implementeras för produktlistor och sökresultatsidor så att utvecklare kan konfigurera de här komponenterna så att knappen Läs in mer visas som sidnumreringsstil.

* Sidan för återställning av lösenord implementeras så att kunderna kan uppdatera/återställa sitt kontolösenord.

* Det finns stöd för olika produkttyper.

* Utvecklare kan konfigurera HTML-taggarna för komponenterna Product Carousel, Related Products och Featured Category List så att de följer SEO:s bästa praxis.

* Mina kontofel har åtgärdats.

* Flera felkorrigeringar.

## Releasedatum: augusti 2020

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF | 1.3.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF kärnkomponenter | 1.3.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia Reference Site | 2020.9.2 | [Versionsinformation](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nyheter {#what-is-new-august}

* Breadcrumb-komponenten har lagts till för att stödja innehålls- och e-handelssidor.

* Fliken Commerce har lagts till i sidegenskaperna för att visa CIF egenskaper för landningssida och Experience Fragments.

* Sökfältskomponenten har förbättrats med stöd för alternativet att visa platshållartext

* Flexibilitet i komponenterna Product och Product Teaser ger stöd för enkla anpassningar.

* Flexibilitet att åsidosätta och konfigurera standardetiketten för CTA-knappen för Product Teaser-komponenten har lagts till.

* Adressbokskomponenten har förbättrats så att registrerade kunder kan välja frakt- och faktureringsadresser som sparats i adressboken vid utcheckning.

* Flera felkorrigeringar.

## Releasedatum: juli 2020

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF | 1.2.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF kärnkomponenter | 1.2.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia Reference Site | 2020.8.14 | [Versionsinformation](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nyheter {#what-is-new-july}

* CIF Venia Reference Site extraherades från CIF Archetype och är nu en fristående GitHub-databas.

* CIF Archetype har sammanfogats med AEM Project Archetype. Använd [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) som startpunkt för nya projekt.

* Adressbokshantering har lagts till för att tillåta inloggade användare att hantera sina adresser.

* Gränssnittet för konfiguration av CIF Cloud har stöd för publicerings-/avpubliceringsåtgärder.

### Vad har förbättrats {#what-is-improved-july}

* Inloggningskomponenten har flyttats till listrutan Användare för enkel åtkomst.

* Förenklat paketet med aem-core-cif-affischkomponenter.

* Flera felkorrigeringar.

## Releasedatum: juni 2020

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF | 1.1.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF kärnkomponenter | 1.1.1 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF | 0.11.0 | [Versionsinformation](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nyheter {#what-is-new-june}

Detta är den första versionen av CIF Core Components som stöds i Adobe Experience Manager.

* Produktsorteringen har lagts till på sidan Produktlista och sidan Sökresultat så att kunderna kan sortera baserat på relevans, pris och produktnamn.

* Kategorifiltrering har lagts till som en fasett så att kunderna kan filtrera baserat på kategori.

* Tjänstanvändarmappning har lagts till som en del av säkerhetskraven för att säkerställa åtkomst till /conf via tjänstanvändare och inte genom att direkt ändra åtkomstkontrollistor. CIF Core Components måste använda en tjänstanvändare för att få åtkomst till konfigurationer.

### Vad har förbättrats {#what-is-improved-june}

* På sidan Produktlista och sidan Sökresultat visas det totala antalet objekt. Antalet objekt uppdateras när användaren använder filter.

* Fasetterad sökning optimeras genom att en kategorifråga kombineras med en produktsökfråga.

* Kategori-/produktväljare för sidförhandsgranskning följer cq:catalogPath.

* Flera felkorrigeringar.

## Releasedatum: maj 2020

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF | 1.0.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF kärnkomponenter | 1.0.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF | 0.11.0 | [Versionsinformation](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nyheter {#what-is-new-may}

* Stöder frågor för Adobe Commerce 2.3.5 Schema.

* Stöd för fasetterad sökning har lagts till i sidan Sök och produktlista så att kunderna kan filtrera sökresultat baserat på produktaspekter.

* Ny OSGi-tjänst har lagts till för att anpassa PDP/PLP-URL:er för SEO-syften. Mer information finns i [dokumentationen](https://github.com/adobe/aem-core-cif-components).

* Produktbindning skapas automatiskt när en molnkonfiguration skapas.

### Vad har förbättrats

* Molnkonfiguration utökad för att visa åtgärden Skapa mapp.

* Flera felkorrigeringar har tillämpats.

## Releasedatum: april 2020

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF | 0.10.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF kärnkomponenter | 0.10.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF | 0.10.0 | [Versionsinformation](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nyheter {#what-is-new-april}

* Konfigurationsinställningarna för CIF Connector är enhetliga och förenklade. Mer information finns i [Komma igång](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/home.html?lang=sv-SE) eller [Ny AEM CIF projektinställningar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/home.html?lang=sv-SE)

### Vad har förbättrats {#what-is-improved-april}

* Kundvagn- och utcheckningsflödet har utökats för att stödja registrerade kunder.

* Utökat stöd för internationalisering i alla komponenter.

* Det finns stöd för grupperade produkter och virtuella produkter.

* Komponenter i relaterade produkter, produktkaruseller och den aktuella kategorin har förbättrats för att ge stöd åt valfri titel.

* Flera felkorrigeringar har tillämpats.

## Releasedatum: februari 2020

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF | 0.9.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF kärnkomponenter | 0.9.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF | 0.9.0 | [Versionsinformation](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nyheter {#what-is-new-february}

* Stöder frågor för Adobe Commerce 2.3.4 Schema.

* Tillagt sökstöd i kategoriväljaren.

* Sidindelning i kategorilistkomponenten som stöder stora kataloguppsättningar.

### Vad har förbättrats {#what-is-improved-february}

* Kundvagnen har förbättrats och visar rabatter.

* Komponenterna Produktinformation, Product Teaser och Product List har stöd för visning av avancerad prisinformation.

* Produktsökning i produktkonsolen och produktväljaren har förbättrats.

* Flera felkorrigeringar har tillämpats.

## Releasedatum: januari 2020

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF | 0.8.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF kärnkomponenter | 0.8.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF | 0.7.0 | [Versionsinformation](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Nyheter {#what-is-new-january}

* Komponenten Experience Fragment (XF) har lagts till så att kunderna kan skapa XF i sina e-handelsprojekt.

* Ändra de lösenordsfunktioner som är tillgängliga på mitt konto.

* i18n-stöd för AEM kärnkomponenter på serversidan.

* Allmän relaterad produktkomponent finns tillgänglig.

### Vad har förbättrats {#what-is-improved-january}

* Stöd för att visa CTA-knappen på produktsuddgummit.

* Alternativ för att ändra/välja bilder i komponenten Kategorilista.

* Alternativ för att dölja/visa rubrik/banderoll i produktlistkomponenten.

* Dra och släpp-funktionen som används på Product Carousel-komponenten.

* Flera felkorrigeringar har tillämpats.
