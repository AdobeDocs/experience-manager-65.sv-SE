---
title: AEM Content and Commerce Release Notes 2024
description: Adobe Experience Manager Content och Commerce Release Notes 2024.
exl-id: 372e6a46-72bb-4db4-ad01-534ca723ae58
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 1788e5f77d4c46a548710361e9e5dae3c6daab28
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 2%

---

# Commerce integration framework GitHub Release Overview

## Översikt över systemkrav

Granska de lägsta systemkraven i tabellen nedan för den CIF versionen som du använder eller planerar att använda i framtiden.

| Komponent | Systemkrav |
|:-------|:-----------------------------------------------------------------------------------------------:|
| CIF | Minst: AEM 6.5.18, Adobe Commerce 2.3.5 GraphQL scheman |
| CIF kärnkomponenter | [Systemkrav](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM Project Archettype | [Systemkrav](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## Releasedatum: oktober 2024

| Komponent | Version | Information |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| CIF kärnkomponenter | 2.15.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.15.0) |

### Felkorrigeringar {#bug-fixes-October}

* Korrigerade gränssnittstester för att fungera korrekt med CIF kärnkomponenter.
* Ett problem med kategorins URL-format som inte fungerar som väntat i molninstansen har åtgärdats.

## Releasedatum: september 2024

| Komponent | Version | Information |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| CIF kärnkomponenter | 2.14.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.14.2) |

### Förbättringar {#improvements-September}

* Gör kategorigränsen anpassningsbar.

### Felkorrigeringar {#bug-fixes-September}

* Commerce-fälten är inte korrekt integrerade med Assets metadataschredigerare.
* Problem med Carousel Products Multifield för dra och släpp.
* Problem med Carousel Category Multifield för dra och släpp
* Det går inte att klicka på menyerna på sidan Sidinformation på kategoritexten och produktredigeringssidan.
* Ordernummer visas inte på orderbekräftelsesidan.

## Releasedatum: januari 2024

| Komponent | Version | Information |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| CIF kärnkomponenter | 2.12.6 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.12.6) |

### Felkorrigeringar {#bug-fixes-january}

* Korrigerat tillägg i kundvagnsknappen och lägg till i önskelisteknappen i produktsamlingskomponenten
