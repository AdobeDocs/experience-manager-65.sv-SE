---
title: Betydande ändringar av tillägget Commerce Integration Framework (CIF)
description: Betydande ändringar av tillägget i Commerce Integration Framework (CIF) jämfört med tidigare CIF-versioner.
exl-id: 41dee21a-9ae2-4067-a32a-2d4633323fc4
source-git-commit: a2ababa9dd9115e963b91a7271d204d287557c40
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# Betydande ändringar av tillägget Commerce Integration Framework (CIF){#notable-changes}

I det här dokumentet belyses de viktiga skillnaderna mellan tillägget i Commerce Integration Framework (CIF) och äldre CIF-versioner, främst kända som CIF Classic (Quickstart) och CIF Open source.

## Installation och uppdateringar

AEM CIF-tilläggspaketet installeras och uppdateras med AEM Package Manager.

**Tidigare CIF-versioner**

* CIF Classic: CIF var en del av QuickStart och behövde inte installeras. CIF-uppdateringar var en del av regelbundna AEM- eller Service Pack-uppdateringar
* CIF öppen källkod: Installation via GitHub. Uppdateringarna var en del av det manuella uppdaterings-/underhållsarbetet.

## Konfiguration av slutpunkt

Slutpunkten konfigureras via OSGi-konsolen.

**Tidigare CIF-versioner**

* CIF Classic: Via OSGi-konfiguration i AEM
* CIF öppen källkod: Via CIF Configuration Browser

## Distribution av CIF Venia-projektet

Projektet är tillgängligt på [GitHub AEM Guides - CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia) och driftsättning via AEM Package Manager.

**Tidigare CIF-versioner**

* CIF Classic: Via AEM

## Produktkatalogdata

Produktkatalogdata efterfrågas vid behov via realtidsanrop till en extern slutpunkt som stöder de GraphQL API:er som krävs. Dessa API:er har stöd för åtkomst till livedata eller mellanlagrade data vid ett visst datum. Ingen replikering behövs.

**Tidigare CIF-versioner**

* CIF Classic: Live- och mellanlagrade produktdata importeras och lagras i JCR på AEM Author via import av hela eller deltaprodukter. Live-produktdata replikeras till AEM Publish.

## Produktkatalogupplevelser med AEM rendering

AEM återger produktkatalogupplevelser direkt med hjälp AEM katalogmallar som har tilldelats produkter och kategorier. Ingen replikering behövs.

**Tidigare CIF-versioner**

* CIF Classic: AEM Author skapar en AEM sida för varje kategori/produkt med hjälp av katalogdesignverktyget. Dessa sidor replikeras till AEM Publish.

>[!NOTE]
>
>Mer information om hur du använder CIF med AEM Managed Service eller AEM On-Premise finns i [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
