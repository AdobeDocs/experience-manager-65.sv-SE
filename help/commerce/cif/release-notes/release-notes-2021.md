---
title: Adobe Experience Manager Content and Commerce Release Notes 2021
description: Adobe Experience Manager Content and Commerce Release Notes 2021.
exl-id: ec47c5f8-d4dd-469f-94df-5ee28f25d696
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 4%

---

# Commerce integration framework GitHub Release Overview

## Översikt över systemkrav

Granska de lägsta systemkraven i tabellen nedan för den CIF versionen som du använder eller planerar att använda i framtiden.

| Komponent | Systemkrav |
|:-------|:-----:|
| CIF | Minimum: Adobe Experience Manager (AEM) 6.5.7, Adobe Commerce 2.3.5 GraphQL scheman |
| CIF kärnkomponenter | [Systemkrav](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM Project Archettype | [Systemkrav](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Releasedatum: november 2021

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF | 2021.11.18.00 | [Programdistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.11.18.00.zip) |
| CIF kärnkomponenter | 2.4.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.2) |
| CIF Venia Reference Site | 2021.12.01 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.12.01) |

### Nyheter {#what-is-new-november}

* Utökade myAccount-komponenter som baseras på Commerce utbyggbara Premiere-komponenter

![Utökade komponenter för mitt konto](/help/assets/CIF/extended-myAccount-components.png)

* Författare kan skapa ad hoc-produkter för Commerce Recommendations med hjälp av ytterligare rekommendationstyper

* Stöd för presentkort i AEM Storefront

## Releasedatum: oktober 2021

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF | 2021.10.20.02 | [Programdistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.10.20.02.zip) |
| CIF kärnkomponenter | 2.4.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.4.0) |
| CIF Venia Reference Site | 2021.11.01 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.11.01) |

### Nyheter {#what-is-new-october}

* Tillägget CIF stöder den senaste versionen av Commerce v2.4.3 med nya GraphQL API:er och scheman

* Författare kan lägga till länkar till produkt- och katalogsidor i textfält med textredigeraren. En CIF ikon har lagts till i verktygsfältet som öppnar väljarna för att snabbt söka efter och välja produkten eller kategorin utan att lämna sammanhanget.

* Befintlig snabbkundvagn och utcheckning har ersatts med dedikerade AEM- och utcheckningssidor. Komponenterna på dessa sidor byggs med Adobe Commerce utökningsbara Premiere-komponenter

* Marknadsförare kan dölja vissa produktkatalogkategorier i navigeringen med hjälp av Commerce serverdel. Den CIF kärnkomponenten för navigering respekterar e-handelsserverdelens konfiguration &quot;include in menu&quot; för att visa/dölja kategorier i navigering

* AEM Storefront Venia returnerar HTTP 404-fel om kategori eller produktsida inte hittas

## Releasedatum: september 2021

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF | 2021.09.27 | [Programdistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.27.zip) |
| CIF kärnkomponenter | 2.2.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.2.0) |
| CIF Venia Reference Site | 2021.09.23 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.09.23) |

### Nyheter {#what-is-new-september}

* Ny flik för associerat e-handelsinnehåll i Sites editor ökar redigeringens effektivitet genom att snabbt få tillgång till relevant AEM för det aktuella sammanhanget

  ![Associerat e-handelsinnehåll](/help/assets/CIF/associated-commerce-content.png)

* Förbättrat användargränssnitt för produktväljare för bättre användarupplevelse, ökad effektivitet och stöd för komplexa produktkataloger

  ![Ny produktväljare](/help/assets/CIF/product-picker.png)

* Respektera egenskapen include_in_menu i navigeringskomponenten

### Felkorrigeringar {#bug-fixes-september}

* Borttagning av menycache fungerar inte som förväntat

* JS-fel AEM CS-driftsättningssteget och när komponenter på klientsidan inte används

* Det går inte att skapa CIF molnkonfiguration i mappar som har en sling:configs-nod

## Releasedatum: augusti 2021

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF | 2021.09.02 | [Programdistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.09.02.zip) |
| CIF kärnkomponenter | 2.1.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.1.0) |
| CIF Venia Reference Site | 2021.08.27 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.08.27) |

### Nyheter {#what-is-new-august}

* Nytt användargränssnitt för kategoriväljare för förbättrad användarupplevelse, ökad effektivitet och bättre stöd för komplex produktkatalog

  ![Ny kategoriväljare](/help/assets/CIF/category-picker.png)

* Bättre stöd för A11Y för CIF kärnkomponenter

### Felkorrigeringar {#bug-fixes-august}

* Det går inte att stänga kategorifilterdragspelet när det har öppnats

* Egenskapen Call to action text bruten i produktsuddgummi

* CIF JS-fel AEM CS-driftsättningssteget

* Korrigera åtkomst till råprodukt för mappade produktlisteobjekt

## Releasedatum: juli 2021

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF | 2021.07.21 | [Programdistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.07.21.zip) |
| CIF kärnkomponenter | 2.0.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.0.0) |
| CIF Venia Reference Site | 2021.07.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.07.22) |

### Nyheter {#what-is-new-july}

* CIF Core Components v2
   * Förenklade och förbättrade konfigurationer för PDP/PLP URL och SEO
   * Visuell indikator för mellanlagrade produktdata i redigeringsläge för bättre synlighet för kommande ändringar
   * Ny platskarta för innehålls- och e-handelssidor

* Stöd för [Adobe Commerce Sensei produktrekommendation från Adobe Sensei](https://business.adobe.com/products/magento/product-recommendations.html) i AEM Storefront med fördefinierade eller direkt skapade rekommendationer

## Releasedatum: juni 2021

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF | 2021.06.18 | [Programdistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.06.18.zip) |
| CIF kärnkomponenter | 1.12.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.12.0) |
| CIF Venia Reference Site | 2021.06.12 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.06.17) |

### Nyheter {#what-is-new-june}

* Nya CIF för produkt- och kategorireferensdatatyper för innehållsfragment (Inkl. användargränssnitt för produkt-/kategoriväljare)
* Ny kärnkomponent i Commerce Content Fragment
* Heltextbaserad e-handelssökning stöds i AEM
* Commerce Core Components har stöd för Adobe Commerce Sensei Recs datainsamling
* Förbättrade SEO-vänliga URL:er för kategorisidor
* Stöd för anpassade HTTP-huvuden per plats/konfiguration

## Releasedatum: maj 2021

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF | 2021.05.26 | [Programdistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.05.26.zip) |
| CIF kärnkomponenter | 1.11.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.11.0) |
| CIF Venia Reference Site | 2021.05.24 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.05.24) |

### Nyheter {#what-is-new-may}

* Sidnumreringsstöd för associerat innehåll i produktkonsolens egenskaper

### Felkorrigeringar {#bug-fixes-may}

* Miniatyrbilder av resurser visas inte på fliken Resurser i produktegenskaper

* Breadcrumb återställer förhandsvisningsdata i produktkonsolen

## Releasedatum: april 2021

| Komponent | Version | Information |
|:-------|:-----:|---------------------:|
| CIF | 2021.04.22 | [Programdistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2021.04.22.zip) |
| CIF kärnkomponenter | 1.10.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia Reference Site | 2021.04.22 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nyheter {#what-is-new-april}

* Stöd för kategori-UID - Detta frigör e-handelsintegreringar från tredje part för system som använder strängar för kategori-ID

* AEM för PWA Studio inkl. exempelintegrering

* Ny CIF navigeringskärnkomponent som utökar WCM-navigeringskärnkomponenten

### Felkorrigeringar {#bug-fixes-april}

* Rotkategorifältet visades inte under fliken E-handel i sidegenskaperna för kategorisidor

## Releasedatum: mars 2021 {#what-is-new-march}

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF | 1.9.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF kärnkomponenter | 1.9.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia Reference Site | 2021.03.25 | [Versionsinformation](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nyheter

* Stöd för Adobe Commerce 2.4.2

### Vad har förbättrats

* Förbättrad återanvändning av produktdetaljkomponenten för innehållsdrivna sidor

* Bättre cachning och färre backend-anrop för PDP:er

* Flera felkorrigeringar.

## Releasedatum: februari 2021

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF | 1.8.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF kärnkomponenter | 1.8.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia Reference Site | 2021.02.24 | [Versionsinformation](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nyheter {#what-is-new-february}

* Product Experience Management: Berika katalogsidorna individuellt med Experience Fragments.

* Utökade egenskaper för produktkonsolen för att visa länkade Assets- och Experience Fragments, inklusive åtgärder för att snabbt navigera till associerat innehåll.

### Vad har förbättrats  {#what-is-improved-february}

* Förbättrat datalager på klientsidan med produktbild-URL och kategoriinformation.

* Flera felkorrigeringar.

## Releasedatum: januari 2021

| GitHub | Version | Detaljerade versionsinformation |
|:-------|:-----:|---------------------:|
| CIF | 1.7.0 | [Versionsinformation](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF kärnkomponenter | 1.7.0 | [Versionsinformation](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia Reference Site | 2021.02.02 | [Versionsinformation](https://github.com/adobe/aem-cif-guides-venia/releases) |

### Nyheter {#what-is-new-january}

* Product Experience Management: Ny egenskapsflik för Commerce för Assets och Experience Fragments. På den här fliken kan du länka Assets- och Experience Fragments till produkter och kategorier. På fliken visas även realtidsdata för länkade e-handelsobjekt och en länk som visar information i produktkonsolen.

### Vad har förbättrats  {#what-is-improved-january}

* Skicka användardata efter autentisering till Adobe-klientdatalagret.

* Flera felkorrigeringar.
