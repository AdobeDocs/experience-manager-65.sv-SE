---
title: Begär analysskript
seo-title: Begär analysskript
description: Analysskriptet för begäran görs för att underlätta analysen av access.log-filerna som skapar en läsbar rapport för senare bearbetning
seo-description: Analysskriptet för begäran görs för att underlätta analysen av access.log-filerna som skapar en läsbar rapport för senare bearbetning
uuid: 24eff3c6-5748-46f3-a30c-4a3a6427ce1d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 1b5e0ccf-4157-45e3-8caf-1d6739d7d9d2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Begär analysskript{#request-analysis-script}

## Hämta {#download}

Skriptet görs för att underlätta analysen av de filer som `access.log` producerar en läsbar rapport för senare bearbetning.

[Hämta fil](assets/analyse-access.sh)

## Beskrivning {#description}

Skriptet görs för att underlätta analysen av de filer som `access.log` producerar en läsbar rapport för senare bearbetning.

Det genererar det totala antalet förfrågningar, GET kontra POST, Begär distribution över tid med mera.

Utdata är i Markdown-syntax och därför blir det enklare att konvertera dem till PDF-filer med verktyg som pandoc eller att visa dem i en webbläsare med plugin-program som Markdown Viewer.

Den kan analysera en anpassad sökväg som finns på kommandoraden.

Utgå från kommentaren i filen som talar om hur den ska köras:

Analysera CQ `access.log` genom att extrapolera olika information och skapa ett Markdown-resultat på `stdout`.

## Usage {#usage}

`./analyse-access.sh access.log.2013-&ast;`

du kan ange ytterligare anpassade sökvägar att analysera på kommandoraden

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

du kan spara utdata med en enkel rörledning

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
