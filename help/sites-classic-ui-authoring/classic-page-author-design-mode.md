---
title: Konfigurera komponenter i designläge
seo-title: Konfigurera komponenter i designläge
description: När AEM-instansen är installerad direkt är ett urval av komponenter omedelbart tillgängliga i sidosparken. Förutom dessa finns även andra komponenter tillgängliga. Du kan använda designläget för att aktivera/inaktivera sådana komponenter.
seo-description: När AEM-instansen är installerad direkt är ett urval av komponenter omedelbart tillgängliga i sidosparken. Förutom dessa finns även andra komponenter tillgängliga. Du kan använda designläget för att aktivera/inaktivera sådana komponenter.
uuid: 2cd5dad0-2f9c-4f34-aae8-1638d1445eb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 10466b49-f8bd-4c2c-8106-b0c7ba054989
docset: aem65
translation-type: tm+mt
source-git-commit: bcb1840d23ae538c183eecb0678b6a75d346aa50

---


# Konfigurera komponenter i designläge{#configuring-components-in-design-mode}

När AEM-instansen är installerad direkt är ett urval av komponenter omedelbart tillgängliga i sidosparken.

Förutom dessa finns även andra komponenter tillgängliga. Du kan använda designläget för att [aktivera/inaktivera sådana komponenter](#enabledisablecomponentsusingdesignmode). När det är aktiverat och finns på sidan kan du sedan använda designläget för att [konfigurera olika aspekter av komponentdesignen](#configuringcomponentsusingdesignmode) genom att redigera attributparametrarna.

>[!NOTE]
>
>Försiktighet måste iakttas vid redigering av dessa komponenter. Designinställningarna är ofta en viktig del av designen för hela webbplatsen, så de bör bara ändras av någon med rätt behörighet (och upplevelse), ofta administratör eller utvecklare. Mer information finns i [Utveckla komponenter](/help/sites-developing/components.md) .

Detta innebär att lägga till, eller ta bort, de komponenter som är tillåtna i sidans styckesystem. Styckesystemet ( `parsys`) är en sammansatt komponent som innehåller alla andra styckekomponenter. Med styckesystemet kan författare lägga till komponenter av olika typer på en sida eftersom det innehåller alla andra styckekomponenter. Varje stycketyp representeras som en komponent.

Innehållet på en produktsida kan till exempel innehålla ett styckesystem som innehåller följande:

* En bild av produkten (i form av en bild eller ett textimagestycke)
* Produktbeskrivningen (som ett textstycke)
* En tabell med tekniska uppgifter (som ett tabellstycke)
* En formuläranvändare fyller i (när ett formulär börjar, formulärelement och slutstycke för formulär)

>[!NOTE]
>
>Mer information om hur du använder mallar och komponenter finns i [Utveckla komponenter](/help/sites-developing/components.md#paragraphsystem) och [Riktlinjer för användning av mallar och komponenter](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components) `parsys`.

## Aktivera/inaktivera komponenter {#enable-disable-components}

I designläget minimeras sidosparken och du kan konfigurera komponenter som är tillgängliga för redigering:

1. Öppna en sida för redigering och använd ikonen för att öppna designläget:

   ![](do-not-localize/chlimage_1.png)

1. Klicka på **Redigera** i styckesystemet (**Utformning av paragraf**).

   ![screen_shot_2012-02-08at102726am](assets/screen_shot_2012-02-08at102726am.png)

1. En dialogruta öppnas med en lista över de komponentgrupper som visas i Spark tillsammans med de enskilda komponenterna som de innehåller.

   Välj vad som krävs för att lägga till eller ta bort komponenterna som ska vara tillgängliga i sidosparken.

   ![screen_shot_2012-02-08at103407am](assets/screen_shot_2012-02-08at103407am.png)

1. The Sidekick minimeras i designläge. Genom att klicka på pilen kan du maximera sparken och återgå till redigeringsläget:

   ![](do-not-localize/sidekick-collapsed.png)

## Konfigurera designen för en komponent {#configuring-the-design-of-a-component}

I designläget kan du även konfigurera attribut för de enskilda komponenterna. Varje komponent har sina egna parametrar visas i följande exempel **Image** -komponenten:

1. Öppna en sida för redigering och använd ikonen för att öppna designläget:

   ![](do-not-localize/chlimage_1-1.png)

1. Du kan konfigurera komponenternas design.

   Om du till exempel klickar på **Redigera** i bildkomponenten (**Design of image**) kan du konfigurera komponentspecifika parametrar:

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. Spara ändringarna genom att klicka på **OK** .

1. The Sidekick minimeras i designläge. Genom att klicka på pilen kan du maximera sparken och återgå till redigeringsläget:

   ![](do-not-localize/sidekick-collapsed-1.png)
