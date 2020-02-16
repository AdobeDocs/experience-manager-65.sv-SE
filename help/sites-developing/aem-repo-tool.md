---
title: AEM Repo Tool
seo-title: AEM Repo Tool
description: AEM Repo Tool är en enkel lösning för att överföra JCR-innehåll mellan det lokala filsystemet och AEM-servern via kommandoraden som kan jämföras med FTP. AEM Repo Tool liknar Jackrabbit FileVault-verktyget, men är snabbare, har minimalt med beroenden och är ett enkelt basskript.
seo-description: AEM Repo Tool är en enkel lösning för att överföra JCR-innehåll mellan det lokala filsystemet och AEM-servern via kommandoraden som kan jämföras med FTP. AEM Repo Tool liknar Jackrabbit FileVault-verktyget, men är snabbare, har minimalt med beroenden och är ett enkelt basskript.
uuid: 6c4a3504-e8e8-46c0-83cb-c18d9791f93e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 7de7b2f9-770e-4af3-8a31-c7b4de64fd43
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM Repo Tool{#aem-repo-tool}

AEM Repo Tool är en enkel lösning för att överföra JCR-innehåll mellan det lokala filsystemet och AEM-servern via kommandoraden som kan jämföras med FTP. AEM Repo Tool liknar [Jackrabbit FileVault-verktyget](/help/sites-developing/ht-vlttool.md), men är snabbare, har minimalt med beroenden och är ett enkelt basskript.

Det här verktyget förenklar filöverföringen för utvecklaren och kan även integreras i IntelliJ och Eclipse för ännu effektivare utveckling.

## Översikt {#overview}

För en given sökväg i en `jcr_root` filnivåstruktur i filsystemet skapar AEM Repo Tool ett paket med ett enda filter för hela underträdet och överför det till servern (liknande FTP `put`), hämtar det från servern ( `get`) eller jämför skillnaderna ( `status` och `diff`).

Verktyget stöder inte flera filtersökvägar eller FileVault-sökvägar `filter.xml`.

>[!CAUTION]
>
>Observera att AEM Repo-verktyget alltid skriver över hela filen eller katalogen som anges.

## Ladda ned och dokumentation {#download-and-documentation}

AEM [Repo Tool finns på GitHub via den här länken](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) tillsammans med detaljerade installations- och användningsanvisningar.

Om du vill hämta källan till AEM Repo Tool ska du läsa GitHub-projektet som är länkat nedan.

KOD PÅ GITHUB

Koden för den här sidan finns på GitHub

* [Öppna verktygsprojekt på GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Hämta projektet som [en ZIP-fil](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)

