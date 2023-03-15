---
title: Sökfunktion
seo-title: Search Feature
description: Lägga till och konfigurera sökning på en webbgruppsplats
seo-description: Adding and configuring Search to a Communities site
uuid: ca633456-911f-447f-881e-653533125d5f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 3acac082-efbe-4995-b374-851cb9aaf62d
exl-id: e252b0e5-a2f8-468e-ac8c-951a5b0f2e32
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# Sökfunktion {#search-feature}

Sökfunktionen fungerar med olika andra funktioner, till exempel forum, som gör det möjligt att söka efter innehåll.

När du lägger till möjligheten att söka efter inlägg som lagts in av communitymedlemmar, så kallade användargenererat innehåll (UGC), finns det två komponenter: [Sök](#search) och [Sökresultat](#search-results).

Sidan som innehåller `Search Results` -komponenten har stöd för både sökning och visning av resultat.

Sidan som innehåller `Search` -komponenten ger dig en plats att starta en sökning med resultat som visas på `Search Results` sida.

Sökfunktionen kan användas med andra funktioner som gör att besökare och medlemmar kan visa innehåll.

## Sökning {#search-features}

### Lägg till sökning på en sida {#add-search-to-a-page}

Lägga till en `Search` -komponent till en sida i redigeringsläge använder du komponentwebbläsaren för att leta upp `Communities / Search` och dra den till rätt plats på en sida. Användning av `Search` kräver en andra sida för `Search Results.`

Nödvändig information finns på [Grunderna för communitykomponenter](basics.md).

När det nödvändiga klientbiblioteket `cq.social.hbs.search`, finns med, det är så här `Search` visas.

![add-search](assets/add-search.png)

### Konfigurera den tillagda sökningen {#configure-the-added-search}

Markera den monterade `Search` -komponenten som ska få åtkomst till och markera `Configure` som öppnar redigeringsdialogrutan.

![giva](assets/configure-new.png)

Under **[!UICONTROL Search Settings]** anger du hur sökvägarna ska sökas igenom när en fråga anges av en besökare.

![sökinställningar](assets/search-settings.png)

* **[!UICONTROL Search Paths]**
Genom att lägga till sökvägar med knappen Lägg till objekt begränsas innehållssökningen. Om du till exempel vill begränsa sökningen till ett specifikt forum väljer du en forumkomponent som placeras på en sida:

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL Result Page]**
Resultatet visas på en separat sida som du anger med webbläsaren för att välja en sida som innehåller 
`Search Results` -komponenten.

## Sökresultat {#search-results}

### Lägg till sökresultat på en sida {#add-search-results-to-a-page}

Lägga till en `Search Results` -komponent till en sida i redigeringsläge använder du komponentwebbläsaren för att leta upp

* `Communities / Search Results`

och dra den till rätt plats på en sida. Till skillnad från sökkomponenten behövs ingen andra sida eftersom resultaten visas på samma sida.

Om du använder Sök någon annanstans på webbplatsen är den här sidan med `Search Results` kan konfigureras att vara `Result Page` för alla eller alla förekomster av `Search`.

Nödvändig information finns på [Grunderna för communitykomponenter](basics.md).

När det nödvändiga klientbiblioteket `cq.social.hbs.search`, finns med, det är så här `Search Result` visas:

![sökresultat](assets/search-result1.png)

### Konfigurera det tillagda sökresultatet {#configure-the-added-search-result}

Markera den monterade `Search Results` -komponenten som ska få åtkomst till och markera `Configure` som öppnar redigeringsdialogrutan.

![konfigurera](assets/configure-new.png)

Under **[!UICONTROL Search Result Settings]** kan du ange vilka sökvägar som ska ingå i sökningen när en fråga anges av en besökare.

![search-result-settings](assets/search-result-settings.png)

* **[!UICONTROL Search Results Per Page]**

   Definiera antalet ämnen/inlägg som visas per sida. Standardvärdet är 10.

* **[!UICONTROL Search Paths]**

   Genom att lägga till sökvägar med knappen Lägg till objekt begränsas innehållssökningen.

## Ytterligare information {#additional-information}

Mer information finns på [Sök i Grundläggande](search-implementation.md) för utvecklare.
