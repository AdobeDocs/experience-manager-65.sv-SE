---
title: Översikt över interaktiv kommunikation
description: Den här artikeln innehåller översikt, exempel på användningsområden, arbetsflöde för att skapa och skillnader mellan interaktiv kommunikation och brev.
contentOwner: gtalwar
topic-tags: interactive-communications, introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6cfbeec0-0be3-48b2-a4bb-fd19c69c92c7
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 3%

---


# Översikt över interaktiv kommunikation {#interactive-communications-overview}

Den här artikeln innehåller översikt, exempel på användningsområden, arbetsflöde för att skapa och skillnader mellan interaktiv kommunikation och brev.

![hero-image](do-not-localize/correspondence-management.png)

Interactive Communications centraliserar och hanterar framtagning, sammanställning och leverans av säkra, personaliserade och interaktiva korrespondenser som affärskorrespondens, dokument, kontoutdrag, förmånsmeddelanden, marknadsföringsmejl, räkningar och välkomstpaket.

## Viktiga funktioner {#key-capabilities}

Här följer några av de viktigaste funktionerna i Interactive Communications:

- Enkel integrering med formulärdatamodellen för enkel och smidig åtkomst till backend-databaser och andra CRM-system, som MS® Dynamics
- Integrerat redigeringsgränssnitt för tryck- och webbkanaler med möjlighet att automatiskt generera webbkanaler från tryckkanalen
- Diagram som visar information i lättbegripliga visuella format i tryck och på webben
- Dokumentfragment stöder regelredigerare och formulärdatamodell
- Agentanvändargränssnittet visar förhandsgranskning av interaktiv kommunikation i tryck och på webben
- Dra och släpp komponenter för att snabbt skapa utskrifts- och webbkanaler

## Skapa interaktiv kommunikation {#interactive-communication-creation}

![interactive_communication-01](assets/interactive_communication-01.jpg)

### Arbetsflöde {#workflow}

Skapa en interaktiv kommunikation med [byggstenar](#buildingblocks) för Interactive Communication och utför sedan följande steg:

1. Välj [skapa en interaktiv kommunikation](/help/forms/using/create-interactive-communication.md).

1. Ange [formulärdatamodell](/help/forms/using/data-integration.md), förifyllningstjänst och [mallar för tryck och webbkanaler](/help/forms/using/web-channel-print-channel.md). Du kan välja att generera en webbkanal från utskriftskanalen.

1. Använda [dra-och-släpp-gränssnitt](/help/forms/using/introduction-interactive-communication-authoring.md), lägger till dokumentfragment, bilder, komponenter i utskriften och webbkanalen i interaktiv kommunikation efter behov.
1. Konfigurera egenskaperna för de infogade komponenterna, till exempel följande:

   1. [Bilder](/help/forms/using/create-interactive-communication.md#step2)
   1. [Tabeller](/help/forms/using/create-interactive-communication.md#tables) (inklusive layoutfragment)
   1. [Diagram](/help/forms/using/chart-component-interactive-communications.md)
   1. [Dokumentfragment](/help/forms/using/create-interactive-communication.md#document-fragment-properties)

1. Förhandsgranska tryck- och webbkanaler och redigera vid behov interaktiv kommunikation.
1. Agentens användargränssnitt använder [färdigställa interaktiv kommunikation](/help/forms/using/prepare-send-interactive-communication.md) för att skicka det till mottagar-/postprocessen.

### Byggblock {#buildingblocks}

Följande byggstenar krävs för att skapa en interaktiv kommunikation:

- [Formulärdatamodell](/help/forms/using/data-integration.md)
- [Mallar för tryck och webbkanal](/help/forms/using/web-channel-print-channel.md)
- [Dokumentfragment](/help/forms/using/document-fragments.md)
- Bilder
- [Teman](/help/forms/using/themes.md) för webbkanalen

## Interaktiv kommunikation jämfört med korrespondenshantering {#interactive-communications-vs-correspondence-management}

Interaktiv kommunikation är standardmetoden och rekommenderas för att skapa kundkommunikation. Om du vill fortsätta använda bokstäverna som skapas i AEM 6.3 Forms och AEM 6.2 Forms måste du [installera ett kompatibilitetspaket](/help/forms/using/compatibility-package.md). Här följer en jämförelse mellan funktionerna i Interactive Communication och letter.

<table>
 <tbody>
  <tr>
   <td><strong>Funktion</strong></td>
   <td><strong>Interaktiv kommunikation</strong></td>
   <td><strong>Bokstaven</strong></td>
  </tr>
  <tr>
   <td>Utdata</td>
   <td>Tryck och webb</td>
   <td>Skriv ut</td>
  </tr>
  <tr>
   <td>Schema</td>
   <td>Formulärdatamodell </td>
   <td>Dataordlista </td>
  </tr>
  <tr>
   <td>Lokalisering</td>
   <td>Stöds inte i formulärdatamodellen</td>
   <td>Stöds i dataordlista</td>
  </tr>
  <tr>
   <td>Regelredigerare</td>
   <td>
    <ul>
     <li>Regelredigerare för stöd av text och villkor för att skapa infogade villkor</li>
     <li>Interactive Communication editor supports application rules on components of the web channel</li>
    </ul> </td>
   <td>Inget användargränssnitt för att skapa villkorsuttryck</td>
  </tr>
  <tr>
   <td>Redigering</td>
   <td>Dra-och-släpp-gränssnitt för att skapa utskrift och webbkanal</td>
   <td>Ingen dra-och-släpp-mekanism </td>
  </tr>
  <tr>
   <td>Diagram</td>
   <td>Diagram som stöds i tryck- och webbkanaler</td>
   <td>Stöds inte</td>
  </tr>
  <tr>
   <td>Teman</td>
   <td>Använder teman för att utforma webbkanalen</td>
   <td>Stöder inte teman</td>
  </tr>
   <tr>
   <td>Utkast</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
   <tr>
   <td>Inlämningar</td>
   <td>Stöds</td>
   <td>Stöds</td>
  </tr>
  <tr>
  <tr>
   <td>Granskning</td>
   <td>Stöds ej</td>
   <td>Stöds</td>
  </tr>
   <tr>
   <td>Versioner</td>
   <td>Stöds ej</td>
   <td>Stöds</td>
  </tr>
   <td>Gruppbearbetning</td>
   <td>Stöds </td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Agentsignatur</td>
   <td>Stöds inte</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Fjärrfunktioner</td>
   <td>Stöds inte</td>
   <td>Stöds</td>
  </tr>
 </tbody>
</table>
