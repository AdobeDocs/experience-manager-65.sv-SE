---
title: Integrering av AEM Forms-data
seo-title: Integrering av AEM Forms-data
description: Med dataintegrering kan ni integrera AEM-formulär med olika datakällor och skapa formulärdatamodell för att skapa och arbeta med adaptiva formulär och interaktiv kommunikation.
seo-description: Med dataintegrering kan ni integrera AEM-formulär med olika datakällor och skapa formulärdatamodell för att skapa och arbeta med adaptiva formulär och interaktiv kommunikation.
uuid: 01df045e-1b26-437c-9674-fd223ecd5097
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: e397c6ce-d73f-4183-8445-1897a8906960
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Integrering av AEM Forms-data{#aem-forms-data-integration}

![](do-not-localize/data-integeration.png)

Företagsinfrastrukturer omfattar olika datasystem eller datakällor som databaser, webbtjänster, REST-tjänster, OData-tjänster och CRM-lösningar. Tillsammans utgör de ett informationssystem som skickar data till affärssystemen för att utföra den dagliga verksamheten. Å andra sidan hämtar applikationerna in data och skickar tillbaka dem för att uppdatera datakällorna.

AEM Forms-applikationer som adaptiva formulär och interaktiv kommunikation kräver integration med datakällor för att hämta in kunddata när man återger formulär och skapar interaktiv kommunikation. Det finns situationer när data hämtas från datakällor baserat på användarindata i anpassningsbara formulär. Dessutom kan inskickade data i anpassningsbara formulär skrivas tillbaka för att uppdatera respektive datakälla.

Ett distribuerat modulärt system har sina fördelar, men utmaningen består i att integrera och skapa dataassociationer mellan datakällor. Dataintegrering är nyckeln till en fungerande och effektiv företagsinfrastruktur med olika datakällor kopplade till applikationer för utbyte av affärsdata.

## Översikt över dataintegrering {#data-integration-overview}

![aem-forms-data-integeration](assets/aem-forms-data-integeration.png)

Med dataintegrering i AEM Forms kan du konfigurera och ansluta olika datakällor till AEM Forms. Det ger ett intuitivt användargränssnitt för att skapa ett enhetligt datarepresentationsschema för affärsenheter och tjänster över anslutna datakällor. Den enhetliga representationen kallas för en formulärdatamodell, ett tillägg till JSON-schema. Enheterna i en formulärdatamodell kallas datamodellsobjekt. Med en formulärdatamodell kan du:

* Få åtkomst till datamodellsobjekt, egenskaper och tjänster från anslutna datakällor.
* Skapa anpassade datamodellsobjekt och egenskaper
* Bygg kopplingar mellan datamodellsobjekt inom och mellan datakällor.
* Anropa datamodellsobjekttjänster för att fråga efter eller skriva data till och från datakällor.

När du har skapat en formulärdatamodell kan du använda den i olika anpassningsbara formulär och interaktiva kommunikationsarbetsflöden, till exempel:

* Skapa anpassningsbara formulär och interaktiv kommunikation baserat på formulärdatamodell
* Förifyll anpassningsbara formulär och interaktiv kommunikation från konfigurerade datakällor
* Anropa datakälltjänster/åtgärder med hjälp av anpassningsbara formulärregler
* Skriv anpassade formulärdata till datakällor

## Kom igång med dataintegrering {#get-started-with-data-integration}

Det första steget för att implementera dataintegrering är att identifiera och konfigurera datakällor som lagrar information som du vill använda i adaptiva formulär och interaktiva kommunikationssituationer. Därefter skapar du en formulärdatamodell som använder datamodellsobjekt, egenskaper och tjänster från en eller flera datakällor. Du kan skapa anpassningsbara formulär och interaktiv kommunikation baserat på en formulärdatamodell där adaptiva formulärfält eller platshållare i interaktiv kommunikation är bundna till respektive datakällegenskap.

Med AEM Forms kan du även skapa en formulärdatamodell som är oberoende av datakällor och associera eller binda datamodellsobjekt och egenskaper i formulärdatamodellen med datakällan senare. Det eliminerar eventuella beroenden till datakällor när du arbetar med en formulärdatamodell.

Läs följande för att komma igång, förstå och implementera dataintegrering.

* [Konfigurera datakällor](../../forms/using/configure-data-sources.md)
* [Skapa formulärdatamodell](../../forms/using/create-form-data-models.md)
* [Arbeta med formulärdatamodell](../../forms/using/work-with-form-data-model.md)
* [Använd formulärdatamodell](../../forms/using/using-form-data-model.md)

