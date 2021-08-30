---
title: AEM Content and Commerce Release Notes 2021
description: AEM Content and Commerce Release Notes 2021
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
source-git-commit: b6703f519295eef728d5504360d99de69438064c
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 7%

---

# GitHub-versionsöversikt för Commerce Integration Framework

## Översikt över systemkrav

Granska de lägsta systemkraven i tabellen nedan för den CIF-version som du använder eller planerar att använda i framtiden.

**I aprilversionen har vi ersatt CIF Connector från GitHub med CIF-tillägget** som finns tillgängligt på  [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). Övergången till tillägget ger stora fördelar för projekten:

* De flesta av de nya funktionerna är omedelbart tillgängliga AEM 6.5 (ingen mer väntan på sidoport för funktionen)
* Enkelt att uppgradera till nya tilläggsversioner
* Klar för Cloud Service

Den gamla AEM CIF Connector försätts i underhållsläge och ska inte användas längre. Ersätt CIF Connector med det nya CIF-tillägget. Det är enkelt att ersätta paket för de flesta projekt.

| Komponent | Systemkrav |
|:-------|:-----:|
| CIF-tillägg | Minimum: AEM 6.5.7, Magento 2.3.5 GraphQL scheman |
| CIF-kärnkomponenter | [Systemkrav](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM Project Archetype | [Systemkrav](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Releasedatum: Augusti 2021

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF-tillägg | 2021.08.20 | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.08.20.zip) |
| CIF-kärnkomponenter | 2.1.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.1.0) |
| CIF Venias referenswebbplats | 2021.08.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.08.27) |

### Nyheter {#what-is-new-august}

* Nytt användargränssnitt för kategoriväljare för förbättrad användarupplevelse, ökad effektivitet och bättre stöd för komplexa produktkataloger

   ![Ny kategoriväljare](/help/assets/CIF/category-picker.png)

* Bättre stöd för A11Y för CIF Core-komponenter

### Felkorrigeringar {#bug-fixes-august}

* Det går inte att stänga kategorifilterdragspelet när det har öppnats

* Egenskapen Call to action text bruten i produktsuddgummi

* CIF JS-fel under AEM CS-driftsättning

* Korrigera åtkomst till råprodukt för mappade produktlisteobjekt

## Releasedatum: Juli 2021

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF-tillägg | 2021.07.21 | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.07.21.zip) |
| CIF-kärnkomponenter | 2.0.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.0.0) |
| CIF Venias referenswebbplats | 2021.07.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.07.22) |

### Nyheter {#what-is-new-july}

* CIF Core Components v2
   * Förenklade och förbättrade konfigurationer för PDP/PLP URL och SEO
   * Visuell indikator för mellanlagrade produktdata i redigeringsläge för bättre synlighet för kommande ändringar
   * Ny platskarta för innehålls- och e-handelssidor

* Stöd för [Adobe Commerce Sensei-produktrekommendation, som drivs av Adobe Sensei](https://business.adobe.com/products/magento/product-recommendations.html) i AEM Storefront med fördefinierade eller direkt skapade rekommendationer

## Releasedatum: Juni 2021

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF-tillägg | 2021.06.18 | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.06.18.zip) |
| CIF-kärnkomponenter | 1.12.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.12.0) |
| CIF Venias referenswebbplats | 2021.06.12 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.06.17) |

### Nyheter {#what-is-new-june}

* Nya referensdatatyper för CIF-produkt och kategori för innehållsfragment (Inkl. användargränssnittsstöd för produkt-/kategoriväljare)
* Ny kärnkomponent för Commerce Content Fragment
* Heltextbaserad e-handelssökning stöds i AEM
* Commerce Core Components stöder datainsamling i Adobe Commerce Sensei Recs
* Förbättrade SEO-vänliga URL:er för kategorisidor
* Stöd för anpassade HTTP-huvuden per plats/konfiguration

## Releasedatum: Maj 2021

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF-tillägg | 2021.05.26 | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.05.26.zip) |
| CIF-kärnkomponenter | 1.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.11.0) |
| CIF Venias referenswebbplats | 2021.05.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.05.24) |

### Nyheter {#what-is-new-may}

* Sidnumreringsstöd för associerat innehåll i produktkonsolens egenskaper

### Felkorrigeringar {#bug-fixes-may}

* Miniatyrbilder av resurser visas inte på fliken Resurser i produktegenskaper

* Breadcrumb återställer förhandsvisningsdata i produktkonsolen

## Releasedatum: April, 2021

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF-tillägg | 2021.04.22 | [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| CIF-kärnkomponenter | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venias referenswebbplats | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nyheter {#what-is-new-april}

* Stöd för kategori-UID - Detta frigör e-handelsintegreringar från tredje part för system som använder strängar för kategori-ID

* AEM för PWA Studio inkl. exempelintegrering

* Ny kärnkomponent för CIF-navigering som utökar kärnkomponenten för WCM-navigering

### Felkorrigeringar {#bug-fixes-april}

* Rotkategorifältet visades inte under fliken E-handel i sidegenskaperna för kategorisidor

## Releasedatum: Mars 2021 {#what-is-new-march}

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF Connector | 1.9.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF-kärnkomponenter | 1.9.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venias referenswebbplats | 2021.03.25 | [Versionsinformation](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nyheter

* Stöd för Magento 2.4.2

### Vad har förbättrats

* Förbättrad återanvändning av produktdetaljkomponenten för innehållsdrivna sidor

* Bättre cachning och färre backend-anrop för PDP:er

* Flera felkorrigeringar.

## Releasedatum: Februari 2021

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF Connector | 1.8.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF-kärnkomponenter | 1.8.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venias referenswebbplats | 2021.02.24 | [Versionsinformation](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nyheter {#what-is-new-february}

* Product Experience Management: Berika katalogsidorna individuellt med Experience Fragments.

* Utökade egenskaper för produktkonsolen för att visa länkade resurser och upplevelsefragment, inklusive åtgärder för att snabbt navigera till det associerade innehållet.

### Vad har förbättrats  {#what-is-improved-february}

* Förbättrat datalager på klientsidan med produktbild-URL och kategoriinformation.

* Flera felkorrigeringar.

## Releasedatum: Januari 2021

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF Connector | 1.7.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF-kärnkomponenter | 1.7.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venias referenswebbplats | 2021.02.02 | [Versionsinformation](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nyheter {#what-is-new-january}

* Product Experience Management: Ny egenskapsflik för Commerce för Assets och Experience Fragments. På den här fliken kan du länka resurser och Experience Fragments till produkter och kategorier. På fliken visas även realtidsdata för länkade e-handelsobjekt och en länk som visar information i produktkonsolen.

### Vad har förbättrats  {#what-is-improved-january}

* Skicka användardata efter autentisering till Adobe-klientdatalagret.

* Flera felkorrigeringar.
