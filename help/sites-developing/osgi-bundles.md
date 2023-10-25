---
title: OSGi Bundles
description: Läs några tips om hur du hanterar OSGi-paket i Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: e18065c7-75b9-4b37-8294-cf94122a4dcf
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# OSGi Bundles{#osgi-bundles}

## Använd semantisk versionshantering {#use-semantic-versioning}

Godkänd om bästa praxis för semantisk versionsnumrering finns på [https://semver.org/](https://semver.org/).

## Bädda inte in fler klasser och burkar än vad som är absolut nödvändigt i OSGi-paket {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

Gemensamma bibliotek bör delas upp i separata paket. På så sätt kan de återanvändas i alla era paket. När en *JAR* i ett OSGi-paket kontrollerar du om någon redan har gjort detta på nätet. Några vanliga platser att hitta befintliga paketbrytare är: Apache Felix, Apache Sling, Apache Geronimo, Apache ServiceMix, Eclipse Bundle Recipes och SpringSource Enterprise Bundle Repository.

## Beroende på vilka paketversioner som finns till låg kostnad {#depend-on-the-lowest-needed-bundle-versions}

För kompileringsberoenden i POM-filer är alltid beroende av vilken version som har lägst storlek som visar det API som behövs. Detta ger bättre bakåtkompatibilitet och underlättar korrigering av äldre versioner.

## Exportera en minimal uppsättning paket från OSGi-paket {#export-a-minimal-set-of-packages-from-osgi-bundles}

När ett paket har exporterats har ett API skapats som andra kan lita på. Se till att exportera så lite som möjligt och se till att det som exporteras är ett API. Det är mycket enklare att ta en privat metod/klass och göra den offentlig än att ta något som tidigare exporterats och göra den privat.

Placera alltid implementeringar i en separat *impl* paket. Som standard är *maven-bundle-plugin* exporterar allt i projektet som inte har en *impl* i namnet.

## Definiera alltid explicit en semantisk version för varje exporterat paket {#always-explicitly-define-a-semantic-version-for-each-package-exported}

Detta gör att era API-kunder kan utvecklas tillsammans med er. När du gör det ska du alltid följa vedertagna standarder för semantisk versionshantering. På så sätt kan användare av ditt API veta vilka typer av ändringar som förväntas i en ny version.

## Inkludera metatypsinformation där den exponeras {#include-metatype-information-where-exposed}

Genom att ange meningsfull metatypsinformation blir era tjänster och komponenter enklare att förstå i Felix-konsolen. En lista över SCR-anteckningar och -attribut finns på: [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html).
