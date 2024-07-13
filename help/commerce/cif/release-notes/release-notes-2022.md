---
title: AEM Content and Commerce Release Notes 2022
description: Adobe Experience Manager Content och Commerce Release Notes 2022.
exl-id: d0a66e70-c4f1-4051-8161-11f07dad0612
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 2%

---

# Commerce integration framework GitHub Release Overview

## Översikt över systemkrav

Granska de lägsta systemkraven i tabellen nedan för den CIF versionen som du använder eller planerar att använda i framtiden.

| Komponent | Systemkrav |
|:-------|:-----:|
| CIF | Minst: AEM 6.5.7, Adobe Commerce 2.3.5 GraphQL scheman |
| CIF kärnkomponenter | [Systemkrav](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM Project Archettype | [Systemkrav](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Releasedatum: september 2022

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF | 2022.09.20.00 | [Programdistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.09.20.00.zip) |
| CIF kärnkomponenter | 2.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.11.0) |
| CIF Venia Reference Site | 2022.09.02 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.09.02) |

### Nyheter {#what-is-new-september}

* Författare kan dynamiskt förbättra produktlistor med Experience Fragments (Exempel: Placera banner mellan produktlistor)
* List-komponenten stöder kopplade produkt-/kategorisidor för att dynamiskt visa relaterade sidor
* Stöd för komponenter i Peregrine 12.5
* Stöd för prissättning på klientsidan i produktlasrar och karuseller

## Releasedatum: juli 2022

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF | 2022.08.02.00 | [Programdistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.08.02.00.zip) |

### Nyheter {#what-is-new-july}

* Sammanslutning av AEM sidor till produkter och kategorier via AEM sidegenskaper plus en översikt i produktcockpit
  ![association för produktcockpitsida](/help/assets/CIF/product_cockpit_page_association.png)

## Releasedatum: juni 2022

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF | 2022.07.05.00 | [Programdistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.07.05.00.zip) |
| CIF kärnkomponenter | 2.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) |
| CIF Venia Reference Site | 2022.07.04 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.07.04) |

### Nyheter {#what-is-new-june}

* Produktkatalogsberikning har nu stöd för AEM sidor, vilket gör att författare kan hantera sida - produktassociation.

* Förbättringar av CIF kärnkomponent

### Felkorrigeringar {#bug-fixes-june}

* Lägg till inloggningstoken till prishämtning på klientsidan

* Fel sidkomponent i datalagret.

## Releasedatum: maj 2022

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF | 2022.05.31.00 | [Programdistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.05.31.00.zip) |
| CIF kärnkomponenter | 2.9.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.9.0) |
| CIF Venia Reference Site | 2022.05.30 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.05.30) |

### Nyheter {#what-is-new-may}

* Ny egenskapssida för produktcockpit för bättre och enklare översikt

![egenskapsöversikt för produktcockpit](/help/assets/CIF/product_cockpit_properties_overview.png)

* Förbättrad kompatibilitet och tillförlitlighet för tredjepartsanslutningar i I/O-miljön

* Förbättra stödet för överskrivningar av GQL-klientkonfigurationen (ange t.ex. anpassad cachelagring)

### Felkorrigeringar {#bug-fixes-may}

* Produktväljarfältet för flera värden visar andra och ytterligare produkter som ogiltiga

* Produktväljaren döljs ibland bakom komponenter

## Releasedatum: april 2022

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF | 2022.04.28.00 | [Programdistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.04.28.00.zip) |
| CIF kärnkomponenter | 2.8.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.8.0) |
| CIF Venia Reference Site | 2022.04.28 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.04.28) |

### Nyheter {#what-is-new-april}

* Snabb åtkomst till produktcockpit: Få enkelt tillgång till detaljerad produktinformation med ett enda klick i Sites Editor

  ![Aktivera önskelista](/help/assets/CIF/enable-wishlist.png)

* Stöd för ytterligare marknadsföringskomponenter: Komponenter kan konfigureras för att visa ett tillägg i en kundvagn och tillägg i en önskelista som anropar till en åtgärd

  ![Kortkommando för webbplatsredigeraren till produktcockpit](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## Releasedatum: februari 2022

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF | 2022.02.24.00 | [Programdistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.02.24.00.zip) |
| CIF kärnkomponenter | 2.6.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) |
| CIF Venia Reference Site | 2022.02.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.02.24) |

### Nyheter {#what-is-new-march}

* Beta: AEM Search Core Component har stöd för Commerce LiveSearch CIF
* Förbättrad SEO för scenarier med flera butiker: URL-format för PDP/PLP kan nu konfigureras på en butiksnivå via CIF Cloud Config-egenskaper
* Produktväljaren har stöd för mellanlagrade produkter via det nya filteralternativet i användargränssnittet. Gör det möjligt för innehållsutvecklare att förbereda innehållshantering för kommande produktlanseringar
* Förenklad CIF och felhantering genom att använda CIF Cloud Config-namn i stället för config proxy-URL
* Manuellt kategorival för produktlista och Carousel-komponenter. Innehållsutvecklare kan använda dessa komponenter på innehållssidor, utanför katalogupplevelsen

## Releasedatum: januari 2022

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF | 2022.01.20.00 | [Programdistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2022.01.20.00.zip) |
| CIF kärnkomponenter | 2.5.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.5.0) |
| CIF Venia Reference Site | 2022.01.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2022.01.27) |

### Nyheter {#what-is-new-january}

* Förbättrade komponenter för myAccount
* Produktrekommendationskomponenten stöder ytterligare sidtyper (hemsida, kundvagn, orderbekräftelse)
* **Önsklista**
   * Inloggade besökare kan lägga till produkter i en önskelista
   * Du kan hantera önskelistan och dess produkter via mitt konto
   * Knappen&quot;Lägg till i önskelista&quot; kan aktiveras/inaktiveras på komponentnivå via en policy (exempel produktnivå, produktinformation)
   * Finns som kärnkomponent och i AEM Venia Storefront

![Önsklista](/help/assets/CIF/wishlist.png)
