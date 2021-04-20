---
title: Omstrukturering av lager i AEM 6.5
seo-title: Omstrukturering av lager i AEM 6.5
description: Läs mer om grunderna och resonemanget bakom omstruktureringen av databasen i AEM 6.5
seo-description: Läs mer om grunderna och resonemanget bakom omstruktureringen av databasen i AEM 6.5
uuid: e9cd3e88-e352-44a8-9b97-69488d3267cb
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: fc879b0b-823b-4bdc-aaa6-36f53a33fb22
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---


# Omstrukturering av lager i AEM 6.5{#repository-restructuring-in-aem}

## Introduktion {#introduction}

Före AEM 6.4 driftsattes kundkoden i oförutsägbara områden av JCR som kunde komma att ändras vid uppgraderingar. På grund av detta var det vanligt att formella AEM skulle skriva över anpassad kod, konfiguration eller innehåll. Dessutom skriver kundens ändringar ibland över AEM produktkod eller innehåll, vilket bryter mot produktfunktionaliteten.

Genom att tydligt definiera hierarkier för AEM produktkod och kundkod kan dessa konflikter undvikas.

Med början i AEM 6.4 och som kommer att fortsätta i framtida versioner struktureras innehållet därför om från /etc till andra mappar i databasen, tillsammans med riktlinjer om vilket innehåll som ska placeras, enligt följande högnivåregler:

* AEM produktkod placeras alltid i /libs, som inte får skrivas över av anpassad kod
* Anpassad kod ska placeras i /apps, /content och /conf

## Påverkan på 6.5 uppgraderingar {#impact-on-upgrades}

När du uppgraderar till AEM 6.5 dupliceras en stor delmängd av innehållet under /etc i andra mappar i databasen. Dessa nya platser är de populäraste platser där innehållet refereras. Alla försök har dock gjorts att AEM 6.5-uppgraderingen ska vara bakåtkompatibel med de tidigare platserna i mappen /etc, och i de flesta fall kommer den gamla platsen att refereras av AEM tills ändringar görs aktivt - och i många fall manuellt - i kundens applikation. Från tidslinjeperspektiv finns det två typer av ändringar:

* Med uppgradering av version 6.5 är en handfull av omstruktureringsförändringar av typen /etc inte bakåtkompatibla och ändringar bör därför planeras och genomföras som en del av uppgraderingen av AEM 6.5.
* Före framtida uppgradering - de allra flesta förändringarna i /etc-omstruktureringen kan skjutas upp till en tid i framtiden efter uppgraderingen. Som tidigare nämnts kommer AEM 6.5-koden att fortsätta referera till de gamla platserna tills ändringarna implementeras som en del av en kundrelease. Även om det inte finns någon tvingad tidslinje som ändringarna ska göras för rekommenderar vi att de görs före den framtida uppgraderingen eftersom framtida funktioner kan vara beroende av att nya platser refereras. Dokumentationen för en viss funktion refererar till de nya platserna enligt vedertaget bruk och det kan därför vara förvirrande om de gamla platserna fortfarande används.

### Omstruktureringsvägledning {#restructuring-guidance}

Vid planering av en uppgradering till AEM 6.5 ska följande sidor per lösning refereras för att bedöma arbetsinsatsen:

* [Omstrukturering av lager som är gemensamma för alla AEM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [Omstrukturering av AEM Sites-arkiv](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [Omstrukturering av AEM Assets-arkiv](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [Omstrukturering av AEM Assets Dynamic Media-arkiv](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [Omstrukturering av AEM Forms-arkiv](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [Omstrukturering av AEM Communities-arkiv](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [Omstrukturering av AEM handelslager](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

Varje sida innehåller två avsnitt som motsvarar hur angelägna ändringarna är. Allt under&quot;Med 6.5-uppgradering&quot; ska hanteras som en del av uppgraderingsprojektet för AEM 6.5. Om du vill kan du skjuta upp allt under&quot;Före framtida uppgradering&quot; till efter uppgraderingen.

Varje post på sidan innehåller ett fält för&quot;vägledning om omstrukturering&quot;, som beskriver den rekommenderade tekniska strategin för anpassning till den nya 6.5-databasmodellen så att det refereras till de nya platserna för innehåll som tidigare fanns under mappen /etc. Ett extra&quot;Anteckningsfält&quot; ger ytterligare användbar kontext.
