---
title: Grunderna för communitykomponenter
seo-title: Grunderna för communitykomponenter
description: Lägg till webbgruppsfunktioner på AEM-webbplatser i redigeringsläge och konfigurera komponenter
seo-description: Lägg till webbgruppsfunktioner på AEM-webbplatser i redigeringsläge och konfigurera komponenter
uuid: c017a7c5-40d1-4592-9317-96fd727dac86
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 21714581-7645-4b47-a9b0-9f1424013240
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Grunderna för communitykomponenter {#communities-components-basics}

## Översikt {#overview}

I redigeringsavsnittet i dokumentationen beskrivs hur du lägger till webbgruppsfunktioner på AEM-webbplatser i redigeringsläge för författare samt hur du beskriver komponentkonfigurationer.

Komponenter kan utforskas med hjälp av en AEM-instans och den interaktiva [communitykomponentguiden](components-guide.md).

## Åtkomst till webbgruppskomponenter {#accessing-communities-components}

Om den underliggande mallen tillåter ändringar av sidans design vid redigering av sidinnehåll, är det möjligt att aktivera komponenter som inte redan är tillgängliga i komponentwebbläsaren som en del av webbplatsdesignen.

Tillgängliga webbgruppskomponenter listas [här](author-communities.md#available-communities-components).

>[!NOTE]
>
>Allmän redigeringsinformation finns i [snabbguiden till redigeringssidorna](../../help/sites-authoring/qg-page-authoring.md).
>
>Om du inte känner till AEM läser du dokumentationen om [grundläggande hantering](../../help/sites-authoring/basic-handling.md).

### Gå in i designläge {#entering-design-mode}

Om en **webbgruppskomponent** inte hittas i komponentwebbläsaren (sidespark) måste du ange `Design Mode` att andra webbgruppskomponenter ska läggas till. [Nödvändiga klientbibliotek](#required-clientlibs) (klientbibliotek) kan också behöva läggas till.

Mer information finns i [Konfigurera komponenter i designläge](../../help/sites-authoring/default-components-designmode.md).

Nedan följer bilder på hur du väljer ett fåtal Communities-komponenter och visar dem i komponentwebbläsaren:

![chlimage_1-424](assets/chlimage_1-424.png)

De valda komponenterna är nu tillgängliga i komponentwebbläsaren:

![chlimage_1-425](assets/chlimage_1-425.png)

## Nödvändiga klienter {#required-clientlibs}

[Klientbaserade bibliotek](../../help/sites-developing/clientlibs.md) (clientlibs) krävs för att en komponent ska fungera korrekt (JavaScript) och formatera (CSS).

När du lägger till en webbgruppskomponent på en sida, om resultatet är ett fel eller ett oväntat utseende, är det första du bör försöka att lägga till de nödvändiga klientlibs för webbkomponenterna. Mer information finns i [Clientlibs for Communities Components](clientlibs.md).

### Exempel: Inledningsvis placerade granskningar utan klientbibliotek... {#example-initially-placed-reviews-without-client-libraries}

![chlimage_1-426](assets/chlimage_1-426.png)

### ... Och med klientbibliotek {#and-with-client-libraries}

![chlimage_1-427](assets/chlimage_1-427.png)

## Taggning {#tagging}

Många webbgruppsfunktioner kan konfigureras så att medlemmar kan tagga innehåll som anges (publiceras) i publiceringsmiljön.

Om taggning tillåts kan communityplatsens konfiguration ställas in så att den begränsar de namnutrymmen som visas för medlemmar i publiceringsmiljön. Se konsolen [](sites-console.md#tagging)Community Sites.

Funktioner som tillåter taggning: [blogg](blog-feature.md), [kalender](calendar.md), [filbibliotek](file-library.md), [forum](forum.md)

Funktioner som använder taggar: [katalog](catalog.md), [sökning](search.md), [socialt taggmoln](tagcloud.md)

För redigeringsinformation:

* [Använda taggar](../../help/sites-authoring/tags.md)

För administrativ information:

* Skapa taggnamnutrymmen (taxonomi): Administrera [taggar](../../help/sites-administering/tags.md)
* Konfiguration av communityplats: se [TAGGNING](sites-console.md#tagging)
* [Tagga användargenererat innehåll](../../help/sites-authoring/tags.md)
* [Aktiveringsresurser för taggning](tag-resources.md)

För utvecklarinformation:

* [AEM Tagging Framework](../../help/sites-developing/framework.md)
* [Tagga viktiga](tag.md)

