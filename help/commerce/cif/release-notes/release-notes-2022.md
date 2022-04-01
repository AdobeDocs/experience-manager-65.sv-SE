---
title: AEM Content and Commerce Release Notes 2022
description: AEM Content and Commerce Release Notes 2022
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
source-git-commit: 1a82930d9f0aa84cea590782aba2e70ec23b41c3
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 3%

---

# GitHub-versionsöversikt för Commerce Integration Framework

## Översikt över systemkrav

Granska de lägsta systemkraven i tabellen nedan för den CIF-version som du använder eller planerar att använda i framtiden.

| Komponent | Systemkrav |
|:-------|:-----:|
| CIF-tillägg | Minimum: AEM 6.5.7, Magento 2.3.5 GraphQL scheman |
| CIF-kärnkomponenter | [Systemkrav](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM Project Archetype | [Systemkrav](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Releasedatum: Mars 2022

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
* Produktrekommendationskomponenten stöder ytterligare sidtyper (hemsida, kundvagn, orderbekräftelse)
* **Önsklista**
   * Inloggade besökare kan lägga till produkter i en önskelista
   * Du kan hantera önskelistan och dess produkter via mitt konto
   * Knappen&quot;Lägg till i önskelista&quot; kan aktiveras/inaktiveras på komponentnivå via en policy (exempel produktnivå, produktinformation)
   * Finns som kärnkomponent och i AEM Venia Storefront

![Önsklista](/help/assets/CIF/wishlist.png)
