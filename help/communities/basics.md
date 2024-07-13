---
title: Grunderna för communitykomponenter
description: Lägg till communityfunktioner AEM webbplatser i redigeringsläge och konfigurera komponenter
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: eb5ce76a-bf28-4540-bc2d-3b5ecb8286f2
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# Grunderna för communitykomponenter {#communities-components-basics}

## Ökning {#overview}

I redigeringsavsnittet i dokumentationen beskrivs hur du lägger till communityfunktioner AEM webbplatser i redigeringsläge för författare och beskriver komponentkonfigurationer.

Komponenter kan utforskas med hjälp av en AEM och den interaktiva [Community Components-guiden](components-guide.md).

## Åtkomst till webbgruppskomponenter {#accessing-communities-components}

Om den underliggande mallen tillåter ändringar av sidans design vid redigering av sidinnehåll, är det möjligt att aktivera komponenter som inte redan är tillgängliga i komponentwebbläsaren som en del av webbplatsdesignen.

Tillgängliga webbgruppskomponenter visas [här](author-communities.md#available-communities-components).

>[!NOTE]
>
>Allmän redigeringsinformation finns i [snabbguiden för redigering av sidor](../../help/sites-authoring/qg-page-authoring.md).
>
>Om du inte känner till AEM kan du läsa dokumentationen om [grundläggande hantering](../../help/sites-authoring/basic-handling.md).

### Gå in i designläge {#entering-design-mode}

Om en **Communities**-komponent inte hittas i komponentwebbläsaren (sidespark) måste du ange `Design Mode` för att lägga till andra Communities-komponenter. [Nödvändiga klientbibliotek](#required-clientlibs) (klientbibliotek) kan också behöva läggas till.

Mer information finns i [Konfigurera komponenter i designläge](../../help/sites-authoring/default-components-designmode.md).

Nedan följer bilder på hur du väljer ett fåtal webbgruppskomponenter och visar dem i komponentwebbläsaren:

![komponent-design](assets/component-design.png)

De valda komponenterna är nu tillgängliga i komponentwebbläsaren:

![component-design1](assets/component-design1.png)

## Nödvändiga klienter {#required-clientlibs}

[Klientbibliotek](../../help/sites-developing/clientlibs.md) (klientbibliotek) krävs för att en komponent ska fungera korrekt (JavaScript) och formatera (CSS).

När du lägger till en webbgruppskomponent på en sida och resultatet är ett fel eller ett oväntat utseende, är det första du bör försöka att lägga till nödvändiga klientlibs för webbkomponenterna. Mer information finns i [Clientlibs for Communities Components](clientlibs.md).

### Exempel: Inledande granskningar utan klientbibliotek.. {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ... Och med klientbibliotek {#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## Taggar {#tagging}

Många webbgruppsfunktioner kan konfigureras så att medlemmar kan tagga innehåll som anges (publiceras) i publiceringsmiljön.

Om taggning tillåts kan communityplatsens konfiguration ställas in så att den begränsar de namnutrymmen som visas för medlemmar i publiceringsmiljön. Se konsolen [Community Sites](sites-console.md#tagging).

Funktioner som tillåter taggning: [blogg](blog-feature.md), [kalender](calendar.md), [filbibliotek](file-library.md), [forum](forum.md)

Funktioner som använder taggar: [sök](search.md), [socialt taggmoln](tagcloud.md)

För redigeringsinformation:

* [Använda taggar](../../help/sites-authoring/tags.md)

För administrativ information:

* Skapar taggnamnutrymmen (taxonomi): [Administrera taggar](../../help/sites-administering/tags.md)
* Konfiguration av communityplats: se [TAGGING](sites-console.md#tagging)
* [Tagga användargenererat innehåll](../../help/sites-authoring/tags.md)

För utvecklarinformation:

* [AEM Taggningsramverk](../../help/sites-developing/framework.md)
* [Tagga viktiga](tag.md)
