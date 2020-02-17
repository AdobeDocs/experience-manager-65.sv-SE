---
title: OSGI Bundles
seo-title: OSGI Bundles
description: Tips för att hantera OSGi-paket
seo-description: Tips för att hantera OSGi-paket
uuid: 07af7089-a233-4e5b-928c-76ddc0af8839
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8d3374ac-51dd-4ff5-84c9-495c937ade12
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# OSGI Bundles{#osgi-bundles}

## Använd semantisk versionshantering {#use-semantic-versioning}

Information om de bästa metoderna för semantisk versionsnumrering finns på [https://semver.org/](https://semver.org/).

## Bädda inte in fler klasser och burkar än vad som är absolut nödvändigt i OSGi-paket {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

Gemensamma bibliotek bör delas upp i separata paket. På så sätt kan de återanvändas i alla dina paket. När du paketerar en *JAR* i ett OSGI-paket ska du kontrollera om någon redan har gjort det. En del vanliga platser att hitta befintliga paketbrytare på är: Apache Felix, Apache Sling, Apache Geronimo, Apache ServiceMix, Eclipse Bundle Recipes och SpringSource Enterprise Bundle Repository.

## Beroende på vilka paketversioner som finns till låg kostnad {#depend-on-the-lowest-needed-bundle-versions}

För kompileringsberoenden i POM-filer är alltid beroende av vilken version som har lägst storlek som visar det API som behövs. Detta ger bättre bakåtkompatibilitet och underlättar korrigering av äldre versioner.

## Exportera en minimal uppsättning paket från OSGi-paket {#export-a-minimal-set-of-packages-from-osgi-bundles}

När ett paket har exporterats har vi skapat ett API som andra kan lita på. Se till att exportera så lite som möjligt och se till att det som exporteras är ett API. Det är mycket enklare att ta en privat metod/klass och göra den offentlig än att ta något som tidigare exporterats och göra den privat.

Implementeringar ska alltid placeras i ett separat *impl* -paket. Som standard exporterar *maven-bundle-plugin* allt i projektet som inte har någon *impl* .

## Definiera alltid explicit en semantisk version för varje exporterat paket {#always-explicitly-define-a-semantic-version-for-each-package-exported}

Detta kommer att göra det möjligt för användare av ditt API att utvecklas tillsammans med dig. När du gör det ska du alltid följa vedertagna standarder för semantisk versionshantering. På så sätt kan användare av ditt API veta vilka typer av ändringar som förväntas i en ny version.

## Inkludera metatypsinformation där den exponeras {#include-metatype-information-where-exposed}

Genom att specificera meningsfull metatypsinformation blir era tjänster och komponenter lättare att förstå i Felix-konsolen. En lista över SCR-anteckningar och -attribut finns på: [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html).
