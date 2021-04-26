---
title: Betydande ändringar av tillägget Commerce Integration Framework (CIF)
description: Betydande ändringar av tillägget i Commerce Integration Framework (CIF) jämfört med tidigare CIF-versioner.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32,c136763f-56aa-450e-8796-bc84bf6c205d
translation-type: tm+mt
source-git-commit: a8dba82029168660b84b085ab46d0406b19961ef
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# Noterbara ändringar av tillägget Commerce Integration Framework (CIF){#notable-changes}

I det här dokumentet belyses de viktiga skillnaderna mellan tillägget i Commerce Integration Framework (CIF) och äldre CIF-versioner, främst kända som CIF Classic (Quickstart) och CIF Open source.

## Installation och uppdateringar

AEM CIF-tilläggspaketet installeras och uppdateras med AEM.

**Tidigare CIF-versioner**

* CIF Classic: CIF var en del av QuickStart och behövde inte installeras. CIF-uppdateringar var en del av regelbundna AEM- eller Service Pack-uppdateringar
* CIF öppen källkod: Installation via GitHub. Uppdateringarna var en del av det manuella uppdaterings-/underhållsarbetet.

## Konfiguration av slutpunkt

Slutpunkten konfigureras via OSGi-konsolen.

**Tidigare CIF-versioner**

* CIF Classic: Via OSGi-konfiguration i AEM
* CIF öppen källkod: Via CIF Configuration Browser

## Distribution av CIF Venia-projektet

Projektet finns på [GitHub AEM Guides - CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia) och distributionen görs via paket-AEM

**Tidigare CIF-versioner**

* CIF Classic: Via AEM

## Produktkatalogdata

Produktkatalogdata hämtas vid behov via realtidsanrop till en extern slutpunkt som stöder de GraphQL API:er som krävs. Dessa API:er har stöd för åtkomst till livedata eller mellanlagrade data vid ett visst datum. Ingen replikering behövs.

**Tidigare CIF-versioner**

* CIF Classic: Live- och mellanlagrade produktdata importeras och lagras i JCR på AEM Author via import av hela eller deltaprodukter. Live-produktdata replikeras till AEM Publish.

## Produktkatalogupplevelser med AEM rendering

AEM återger produktkatalogupplevelser direkt med hjälp AEM katalogmallar som har tilldelats produkter och kategorier. Ingen replikering behövs.

**Tidigare CIF-versioner**

* CIF Classic: AEM Author skapar en AEM sida för varje kategori/produkt med hjälp av katalogdesignverktyget. Dessa sidor replikeras till AEM Publish.

>[!NOTE]
>
>Mer information om hur du använder CIF med AEM hanterade tjänster eller AEM lokalt finns i [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
