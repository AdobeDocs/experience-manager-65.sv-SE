---
title: Grunderna för communitykomponenter
seo-title: Grunderna för communitykomponenter
description: Lägg till communityfunktioner AEM webbplatser i redigeringsläge och konfigurera komponenter
seo-description: Lägg till communityfunktioner AEM webbplatser i redigeringsläge och konfigurera komponenter
uuid: c017a7c5-40d1-4592-9317-96fd727dac86
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 21714581-7645-4b47-a9b0-9f1424013240
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 1%

---


# Grunderna för communitykomponenter {#communities-components-basics}

## Översikt {#overview}

I redigeringsavsnittet i dokumentationen beskrivs hur du lägger till communityfunktioner AEM webbplatser i redigeringsläge för författare samt beskriver komponentkonfigurationer.

Komponenter kan undersökas med hjälp av en AEM och den interaktiva [communitykomponentguiden](components-guide.md).

## Åtkomst till webbgruppskomponenter {#accessing-communities-components}

Om den underliggande mallen tillåter ändringar av sidans design vid redigering av sidinnehåll, är det möjligt att aktivera komponenter som inte redan är tillgängliga i komponentwebbläsaren som en del av webbplatsdesignen.

Tillgängliga webbgruppskomponenter listas [här](author-communities.md#available-communities-components).

>[!NOTE]
>
>Allmän redigeringsinformation finns i [snabbguiden till redigeringssidorna](../../help/sites-authoring/qg-page-authoring.md).
>
>Om du inte känner till AEM kan du läsa dokumentationen om [grundläggande hantering](../../help/sites-authoring/basic-handling.md).

### Gå in i designläge {#entering-design-mode}

Om en **webbgruppskomponent** inte hittas i komponentwebbläsaren (sidespark) måste du ange `Design Mode` att andra webbgruppskomponenter ska läggas till. [Nödvändiga klientbibliotek](#required-clientlibs) (klientbibliotek) kan också behöva läggas till.

Mer information finns i [Konfigurera komponenter i designläge](../../help/sites-authoring/default-components-designmode.md).

Nedan följer bilder på hur du väljer ett fåtal Communities-komponenter och visar dem i komponentwebbläsaren:

![komponentdesign](assets/component-design.png)

De valda komponenterna är nu tillgängliga i komponentwebbläsaren:

![component-design1](assets/component-design1.png)

## Nödvändiga klienter {#required-clientlibs}

[Klientbaserade bibliotek](../../help/sites-developing/clientlibs.md) (clientlibs) krävs för att en komponent ska fungera korrekt (JavaScript) och formatera (CSS).

När du lägger till en webbgruppskomponent på en sida, om resultatet är ett fel eller ett oväntat utseende, är det första du ska försöka att lägga till de nödvändiga klientlibs för webbkomponenterna. Mer information finns i [Clientlibs for Communities Components](clientlibs.md).

### Exempel: Inledningsvis placerade granskningar utan klientbibliotek... {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ... Och med klientbibliotek {#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## Taggar {#tagging}

Många webbgruppsfunktioner kan konfigureras så att medlemmar kan tagga innehåll som anges (publiceras) i publiceringsmiljön.

Om taggning tillåts kan communityplatsens konfiguration ställas in så att den begränsar de namnutrymmen som visas för medlemmar i publiceringsmiljön. Se konsolen [](sites-console.md#tagging)Community Sites.

Funktioner som tillåter taggning: [blogg](blog-feature.md), [kalender](calendar.md), [filbibliotek](file-library.md), [forum](forum.md)

Funktioner som använder taggar: [katalog](catalog.md), [sökning](search.md), moln för [sociala taggar](tagcloud.md)

För redigeringsinformation:

* [Använda taggar](../../help/sites-authoring/tags.md)

För administrativ information:

* Skapa taggnamnutrymmen (taxonomi): [Administrera taggar](../../help/sites-administering/tags.md)
* Konfiguration av communityplats: se [TAGGNING](sites-console.md#tagging)
* [Tagga användargenererat innehåll](../../help/sites-authoring/tags.md)
* [Aktiveringsresurser för taggning](tag-resources.md)

För utvecklarinformation:

* [AEM Taggningsramverk](../../help/sites-developing/framework.md)
* [Tagga viktiga](tag.md)

