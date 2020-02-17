---
title: Översikt över interaktiv kommunikation
seo-title: Översikt över interaktiv kommunikation
description: Den här artikeln innehåller översikt, exempel på användningsområden, arbetsflöde för att skapa och skillnader mellan interaktiv kommunikation och brev.
seo-description: Nyckelfunktioner för interaktiv kommunikation, exempel på användning, arbetsflöde för att skapa och skillnader mellan interaktiv kommunikation och korrespondenshantering
uuid: a06b4ac7-ca20-4d6d-b2b7-87b21e2f5cf9
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
discoiquuid: 67b03098-c58d-4a57-90e0-e4ddd78e5d99
translation-type: tm+mt
source-git-commit: dc7804c9985bf9a14bfad40f546e393b39615dab

---


# Översikt över interaktiv kommunikation {#interactive-communications-overview}

Den här artikeln innehåller översikt, exempel på användningsområden, arbetsflöde för att skapa och skillnader mellan interaktiv kommunikation och brev.

![](do-not-localize/correspondence-management.png)

Interactive Communications centraliserar och hanterar framtagning, sammanställning och leverans av säkra, personaliserade och interaktiva korrespondenser som affärskorrespondens, dokument, kontoutdrag, förmånsmeddelanden, marknadsföringsmejl, räkningar och välkomstpaket.

## Viktiga funktioner {#key-capabilities}

Här följer några av de viktigaste funktionerna i Interactive Communications:

* Enkel integrering med formulärdatamodellen för enkel och smidig åtkomst till backend-databaser och andra CRM-system, som MS® Dynamics
* Integrerat redigeringsgränssnitt för tryck- och webbkanaler med möjlighet att automatiskt generera webbkanaler från tryckkanalen
* Diagram som visar information i lättbegripliga visuella format i tryck och på webben
* Dokumentfragment har stöd för regelredigerare och formulärdatamodell
* Agentanvändargränssnittet visar förhandsgranskning av interaktiv kommunikation i tryck och på webben
* Dra och släpp komponenter för att snabbt skapa utskrifts- och webbkanaler

## Exempel på användningsfall {#sample-use-case}

I [välkomstpaketet för ett](/help/forms/using/finance-reference-site-walkthrough.md#credit-card-application-walkthrough) exempel på hur en kreditkortskund kan användas visas hur en interaktiv kommunikation fungerar.

## Skapa interaktiv kommunikation {#interactive-communication-creation}

![interactive_communication-01](assets/interactive_communication-01.jpg)

### Arbetsflöde {#workflow}

Om du vill skapa en interaktiv kommunikation ska du förbereda [byggstenarna](#buildingblocks) för interaktiv kommunikation och sedan utföra följande steg:

1. Välj om du vill [skapa en interaktiv kommunikation](/help/forms/using/create-interactive-communication.md).

1. Ange [formulärdatamodell](/help/forms/using/data-integration.md), förifyllningstjänst samt mallar [för](/help/forms/using/web-channel-print-channel.md)utskrift och webbkanal. Du kan välja att generera en webbkanal från utskriftskanalen.

1. Använd gränssnittet [för att](/help/forms/using/introduction-interactive-communication-authoring.md)dra och släppa för att lägga till dokumentfragment, bilder, komponenter i tryckt och webbkanaler i den interaktiva kommunikationen efter behov.
1. Konfigurera egenskaperna för de infogade komponenterna, till exempel följande:

   1. [Bilder](/help/forms/using/create-interactive-communication.md#step2)
   1. [Tabeller](/help/forms/using/create-interactive-communication.md#tables) (inklusive layoutfragment)
   1. [Diagram](/help/forms/using/chart-component-interactive-communications.md)
   1. [Dokumentfragment](/help/forms/using/create-interactive-communication.md#document-fragment-properties)

1. Förhandsgranska tryck- och webbkanaler och redigera vid behov interaktiv kommunikation.
1. Agentens användargränssnitt används för att [förbereda interaktiv kommunikation](/help/forms/using/prepare-send-interactive-communication.md) för att skicka den till mottagare/post-processen.

### Byggklossarna {#buildingblocks}

Följande byggstenar krävs för att skapa en interaktiv kommunikation:

* [Formulärdatamodell](/help/forms/using/data-integration.md)
* [Mallar för tryck och webbkanal](/help/forms/using/web-channel-print-channel.md)
* [Dokumentfragment](/help/forms/using/document-fragments.md)
* Bilder
* [Teman](/help/forms/using/themes.md) för webbkanalen

## Interaktiv kommunikation jämfört med korrespondenshantering {#interactive-communications-vs-correspondence-management}

Interaktiv kommunikation är standardmetoden och rekommenderas för att skapa kundkommunikation. Om du vill fortsätta använda bokstäverna som skapats i AEM 6.3-formulär och AEM 6.2-formulär måste du [installera ett kompatibilitetspaket](/help/forms/using/compatibility-package.md). Här följer en jämförelse mellan funktionerna i Interactive Communication och letter.

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
   <td>Ingen dra och släpp-mekanism </td>
  </tr>
  <tr>
   <td>Diagram</td>
   <td>Diagram som kan användas både i tryck och i webbkanaler</td>
   <td> Stöds inte</td>
  </tr>
  <tr>
   <td>Teman</td>
   <td>Använder teman för att utforma webbkanaler</td>
   <td>Stöder inte teman</td>
  </tr>
  <tr>
   <td>Granskning och versionshantering</td>
   <td> Stöds inte</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Utkast och hantering av instans</td>
   <td> Stöds inte</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Gruppbearbetning</td>
   <td>Stöds </td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Agentsignatur</td>
   <td> Stöds inte</td>
   <td>Stöds</td>
  </tr>
  <tr>
   <td>Fjärrfunktioner</td>
   <td> Stöds inte</td>
   <td>Stöds</td>
  </tr>
 </tbody>
</table>

