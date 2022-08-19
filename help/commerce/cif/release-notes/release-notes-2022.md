---
title: AEM Content and Commerce Release Notes 2022
description: AEM Content and Commerce Release Notes 2022
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: 6c5c37c1c365e1f03ea9b5c935adf63a33faba5d
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 6%

---

# GitHub-versionsöversikt för Commerce Integration Framework

## Översikt över systemkrav

Granska de lägsta systemkraven i tabellen nedan för den CIF-version som du använder eller planerar att använda i framtiden.

| Komponent | Systemkrav |
|:-------|:-----:|
| CIF-tillägg | Minimum: AEM 6.5.7, Magento 2.3.5 GraphQL scheman |
| CIF-kärnkomponenter | [Systemkrav](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM Project Archetype | [Systemkrav](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Releasedatum: Juli 2022

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF-tillägg | 2022.08.02.00 | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.08.02.00.zip) |

### Nyheter {#what-is-new-july}

* Sammanslutning av AEM sidor till produkter och kategorier via AEM sidegenskaper plus en översikt i produktcockpit
   ![association för produktcockpitsida](/help/assets/CIF/product_cockpit_page_association.png)

## Releasedatum: Juni 2022

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF-tillägg | 2022.07.05.00 | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.07.05.00.zip) |
| CIF-kärnkomponenter | 2.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) |
| CIF Venias referenswebbplats | 2022.07.04 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.07.04) |

### Nyheter {#what-is-new-june}

* Produktkatalogsberikning har nu stöd för AEM sidor. Detta gör att författare kan hantera sida - produktassociation.

* Olika förbättringar av CIF-kärnkomponenten

### Felkorrigeringar {#bug-fixes-june}

* Lägg till inloggningstoken till prishämtning på klientsidan

* Fel sidkomponent i datalagret

## Releasedatum: Maj 2022

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF-tillägg | 2022.05.31.00 | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.05.31.00.zip) |
| CIF-kärnkomponenter | 2.9.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.9.0) |
| CIF Venias referenswebbplats | 2022.05.30 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.05.30) |

### Nyheter {#what-is-new-may}

* Ny egenskapssida för produktcockpit för bättre och enklare översikt

![översikt över egenskaper för produktcockpit](/help/assets/CIF/product_cockpit_properties_overview.png)

* Förbättrad kompatibilitet och tillförlitlighet för anslutningar från tredje part vid I/O-körning

* Förbättra stödet för överskrivningar av GQL-klientkonfiguration (t.ex. ange anpassad cachelagring)

### Felkorrigeringar {#bug-fixes-may}

* Produktväljarfältet för flera värden visar att andra och ytterligare produkter är ogiltiga

* Produktväljaren döljs ibland bakom komponenter

## Releasedatum: April, 2022

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF-tillägg | 2022.04.28.00 | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.04.28.00.zip) |
| CIF-kärnkomponenter | 2.8.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.8.0) |
| CIF Venias referenswebbplats | 2022.04.28 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.04.28) |

### Nyheter {#what-is-new-april}

* Snabb åtkomst till produktcockpit: Få enkelt tillgång till detaljerad produktinformation med ett enda klick i Sites Editor

   ![Aktivera önskelista](/help/assets/CIF/enable-wishlist.png)

* Stöd för ytterligare marknadsföringskomponenter: Komponenter kan konfigureras för att visa ett anrop till åtgärd för tillägg i varukorgen och tilläggslistan

   ![Kortkommando för webbplatsredigeraren till produktcockpit](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## Releasedatum: Februari 2022

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF-tillägg | 2022.02.24.00 | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.02.24.00.zip) |
| CIF-kärnkomponenter | 2.6.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) |
| CIF Venias referenswebbplats | 2022.02.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.02.24) |

### Nyheter {#what-is-new-march}

* Beta: AEM CIF Search Core Component support Commerce LiveSearch
* Förbättrad SEO för scenarier med flera butiker: URL-format för PDP/PLP kan nu konfigureras på en butiksnivå via CIF Cloud Config-egenskaper
* Produktväljaren har stöd för mellanlagrade produkter via ett nytt filteralternativ i användargränssnittet.  Detta gör att innehållsutvecklare kan förbereda innehållshantering för kommande produktlanseringar
* Förenklad CIF-konfigurationshantering och felhantering genom att använda CIF Cloud Config-namn i stället för konfigurationsproxy-URL
* Manuellt kategorival för produktlista och Carousel-komponenter. På så sätt kan innehållsutvecklare använda dessa komponenter på innehållssidor, utanför katalogupplevelsen

## Releasedatum: Januari 2022

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF-tillägg | 2022.01.20.00 | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.01.20.00.zip) |
| CIF-kärnkomponenter | 2.5.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.5.0) |
| CIF Venias referenswebbplats | 2022.01.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.01.27) |

### Nyheter {#what-is-new-january}

* Förbättrade komponenter för myAccount
* Produktrekommendationskomponenten har stöd för ytterligare sidtyper (hemsida, kundvagn, orderbekräftelse)
* **Önsklista**
   * Inloggade besökare kan lägga till produkter i en önskelista
   * Du kan hantera önskelistan och dess produkter via mitt konto
   * Knappen&quot;Lägg till i önskelista&quot; kan aktiveras/inaktiveras på komponentnivå via en policy (exempel produktnivå, produktinformation)
   * Finns som kärnkomponent och i AEM Venia Storefront

![Önsklista](/help/assets/CIF/wishlist.png)
