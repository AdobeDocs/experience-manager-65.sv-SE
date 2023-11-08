---
title: AEM
description: AEM är en enkel lösning för att överföra JCR-innehåll mellan det lokala filsystemet och den AEM servern via kommandoraden som kan jämföras med FTP. AEM liknar Jacka-kanins FileVault-verktyg, men är snabbare, har minimalt med beroenden och är ett enkelt basskript.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: c46c9f0c-b0d2-4f2f-b95c-90fd3ced32a9
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# AEM{#aem-repo-tool}

AEM är en enkel lösning för att överföra JCR-innehåll mellan det lokala filsystemet och den AEM servern via kommandoraden som kan jämföras med FTP. AEM liknar [Jackrabbit FileVault-verktyget](/help/sites-developing/ht-vlttool.md), men är snabbare, har minimalt med beroenden och är ett enkelt basskript.

Det här verktyget förenklar filöverföringen för utvecklaren och kan även integreras i IntelliJ och Eclipse för att göra utvecklingen ännu effektivare.

## Översikt {#overview}

För en given bana inuti en `jcr_root` filsystemens struktur AEM postverktyget skapar ett paket med ett enda filter för hela underträdet och skickar det till servern (liknande FTP) `put`), hämtar den från servern ( `get`) eller jämför skillnaderna ( `status` och `diff`).

Verktyget stöder inte flera filtersökvägar eller FileVault-filer `filter.xml`.

>[!CAUTION]
>
>AEM skriver alltid över hela filen eller katalogen som anges.

## Ladda ned och dokumentation {#download-and-documentation}

The [AEM finns på GitHub via den här länken](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) tillsammans med detaljerade installations- och användningsanvisningar.

Om du vill hämta källan till AEM kan du läsa GitHub-projektet som är länkat nedan.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna verktygsprojekt på GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
