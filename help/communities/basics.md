---
title: Grunderna för communitykomponenter
seo-title: Communities Components Basics
description: Lägg till communityfunktioner AEM webbplatser i redigeringsläge och konfigurera komponenter
seo-description: Add Communities features to AEM sites in edit mode and configure components
uuid: c017a7c5-40d1-4592-9317-96fd727dac86
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 21714581-7645-4b47-a9b0-9f1424013240
exl-id: eb5ce76a-bf28-4540-bc2d-3b5ecb8286f2
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 1%

---

# Grunderna för communitykomponenter {#communities-components-basics}

## Översikt {#overview}

I redigeringsavsnittet i dokumentationen beskrivs hur du lägger till communityfunktioner AEM webbplatser i redigeringsläge för författare samt beskriver komponentkonfigurationer.

Komponenter kan utforskas med hjälp av en AEM och den interaktiva [Community Components Guide](components-guide.md).

## Åtkomst till webbgruppskomponenter {#accessing-communities-components}

Om den underliggande mallen tillåter ändringar av sidans design vid redigering av sidinnehåll, är det möjligt att aktivera komponenter som inte redan är tillgängliga i komponentwebbläsaren som en del av webbplatsdesignen.

Tillgängliga webbgruppskomponenter visas [här](author-communities.md#available-communities-components).

>[!NOTE]
>
>Allmän redigeringsinformation finns i [snabbguide till framtagning av sidor](../../help/sites-authoring/qg-page-authoring.md).
>
>Om du inte känner till AEM kan du läsa dokumentationen om [grundläggande hantering](../../help/sites-authoring/basic-handling.md).

### Gå in i designläge {#entering-design-mode}

Om en **Communities** -komponenten finns inte i komponentwebbläsaren (sidespark). Du måste ange `Design Mode` om du vill lägga till andra webbgruppskomponenter. [Nödvändiga bibliotek på klientsidan](#required-clientlibs) (klientlibs) kan också behöva läggas till.

Mer information finns i [Konfigurera komponenter i designläge](../../help/sites-authoring/default-components-designmode.md).

Nedan följer bilder på hur du väljer ett fåtal Communities-komponenter och visar dem i komponentwebbläsaren:

![komponentdesign](assets/component-design.png)

De valda komponenterna är nu tillgängliga i komponentwebbläsaren:

![component-design1](assets/component-design1.png)

## Nödvändiga klienter {#required-clientlibs}

[Bibliotek på klientsidan](../../help/sites-developing/clientlibs.md) (clientlibs) krävs för att en komponent ska fungera korrekt (JavaScript) och formatera (CSS).

När du lägger till en webbgruppskomponent på en sida, om resultatet är ett fel eller ett oväntat utseende, är det första du bör försöka att lägga till de nödvändiga klientlibs för webbkomponenterna. Mer information finns i [Clientlibs for Communities Components](clientlibs.md).

### Exempel: Inledningsvis placerade granskningar utan klientbibliotek... {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ... Och med klientbibliotek {#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## Taggar {#tagging}

Många webbgruppsfunktioner kan konfigureras så att medlemmar kan tagga innehåll som anges (publiceras) i publiceringsmiljön.

Om taggning tillåts kan communityplatsens konfiguration ställas in så att den begränsar de namnutrymmen som visas för medlemmar i publiceringsmiljön. Se [Konsol för communityplatser](sites-console.md#tagging).

Funktioner som tillåter taggning: [blogg](blog-feature.md), [kalender](calendar.md), [filbibliotek](file-library.md), [forum](forum.md)

Funktioner som använder taggar: [sök](search.md), [social tag cloud](tagcloud.md)

För redigeringsinformation:

* [Använda taggar](../../help/sites-authoring/tags.md)

För administrativ information:

* Skapa taggnamnutrymmen (taxonomi): [Administrera taggar](../../help/sites-administering/tags.md)
* Konfiguration av communityplats: se [TAGGNING](sites-console.md#tagging)
* [Tagga användargenererat innehåll](../../help/sites-authoring/tags.md)

För utvecklarinformation:

* [AEM Taggningsramverk](../../help/sites-developing/framework.md)
* [Tagga viktiga](tag.md)
