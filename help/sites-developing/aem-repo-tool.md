---
title: AEM
seo-title: AEM Repo Tool
description: AEM är en enkel lösning för att överföra JCR-innehåll mellan det lokala filsystemet och den AEM servern via kommandoraden som kan jämföras med FTP. AEM liknar Jacka-kanins FileVault-verktyg, men är snabbare, har minimalt med beroenden och är ett enkelt basskript.
seo-description: The AEM Repo Tool is a simple solution to transfer JCR content between your local filesystem and the AEM server via the command line comparable to FTP. The AEM Repo Tool is similar to the Jackrabbit FileVault tool, but is faster, has minimal dependencies, and is a simple bash script.
uuid: 6c4a3504-e8e8-46c0-83cb-c18d9791f93e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 7de7b2f9-770e-4af3-8a31-c7b4de64fd43
exl-id: c46c9f0c-b0d2-4f2f-b95c-90fd3ced32a9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# AEM{#aem-repo-tool}

AEM är en enkel lösning för att överföra JCR-innehåll mellan det lokala filsystemet och den AEM servern via kommandoraden som kan jämföras med FTP. AEM liknar [Jackrabbit FileVault-verktyget](/help/sites-developing/ht-vlttool.md), men är snabbare, har minimalt med beroenden och är ett enkelt basskript.

Det här verktyget förenklar filöverföringen för utvecklaren och kan även integreras i IntelliJ och Eclipse för ännu effektivare utveckling.

## Översikt {#overview}

För en given bana inuti en `jcr_root` filsystemens struktur AEM postverktyget skapar ett paket med ett enda filter för hela underträdet och skickar det till servern (liknande FTP) `put`), hämtar den från servern ( `get`) eller jämför skillnaderna ( `status` och `diff`).

Verktyget stöder inte flera filtersökvägar eller FileVault-filer `filter.xml`.

>[!CAUTION]
>
>Observera att AEM alltid skriver över hela filen eller katalogen som anges.

## Ladda ned och dokumentation {#download-and-documentation}

The [AEM finns på GitHub via den här länken](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) tillsammans med detaljerade installations- och användningsanvisningar.

Om du vill hämta källan till AEM kan du läsa GitHub-projektet som är länkat nedan.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna verktygsprojekt på GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
