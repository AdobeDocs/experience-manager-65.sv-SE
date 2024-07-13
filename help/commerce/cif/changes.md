---
title: Betydande ändringar av Commerce integrationa frameworken (CIF)
description: Betydande ändringar av tillägget Commerce integration framework (CIF) jämfört med tidigare CIF.
exl-id: 41dee21a-9ae2-4067-a32a-2d4633323fc4
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Betydande ändringar i tillägget Commerce integration framework (CIF){#notable-changes}

I det här dokumentet beskrivs de viktiga skillnaderna mellan tilläggen för Commerce integration framework (CIF) och äldre CIF, främst CIF Classic (QuickStart) och CIF OpenSource.

## Installation och uppdateringar

AEM CIF-tilläggspaketet installeras och uppdateras med AEM Package Manager.

**Tidigare CIF versioner**

* CIF Classic: Ingen installation behövs. CIF ingick i QuickStart. CIF uppdateringar ingick i regelbundna AEM- eller servicepaketuppdateringar
* CIF: Installation via GitHub. Uppdateringarna var en del av det manuella uppdaterings-/underhållsarbetet.

## Konfiguration av slutpunkt

Slutpunkten konfigureras via OSGi-konsolen.

**Tidigare CIF versioner**

* CIF Classic: Via OSGi-konfiguration i AEM
* CIF öppen källkod: via CIF Configuration Browser

## Driftsättning CIF Veniaprojektet

Projektet är tillgängligt på [GitHub AEM Guides - CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia) och distributionen görs via AEM Package Manager.

**Tidigare CIF versioner**

* CIF Classic: Via AEM

## Produktkatalogdata

Produktkatalogdata efterfrågas vid behov via realtidsanrop till en extern slutpunkt som stöder de GraphQL API:er som krävs. Dessa API:er har stöd för åtkomst till livedata eller mellanlagrade data vid ett visst datum. Ingen replikering behövs.

**Tidigare CIF versioner**

* CIF Classic: Live- och mellanlagrade produktdata importeras och lagras i JCR på AEM Author via import av full- eller deltaprodukter. Live-produktdata replikeras till AEM Publish.

## Produktkatalogupplevelser med AEM rendering

AEM återger produktkatalogupplevelser direkt med hjälp AEM katalogmallar som har tilldelats produkter och kategorier. Ingen replikering behövs.

**Tidigare CIF versioner**

* CIF Classic: AEM skapar en AEM sida för varje kategori/produkt med hjälp av katalogritningsverktyget. Dessa sidor replikeras till AEM Publish.

>[!NOTE]
>
>Mer information om hur du använder CIF med AEM hanterade tjänster eller AEM lokalt finns i [Commerce integration framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
