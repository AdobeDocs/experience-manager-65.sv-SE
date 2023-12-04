---
title: Analyserar sidprestanda
seo-title: Analyzing Page Performance
description: Använd sidan Content Insight för att analysera prestandan för sidan som du redigerar
seo-description: Use the Content Insight page to analyze the performance of the page that you are authoring
uuid: 563d3e98-20d9-4cca-a174-bafd6e65c1bb
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 57cd61d5-78f2-4f8c-99ee-75e100c052ef
docset: aem65
exl-id: 14484a90-4e44-4c85-9411-b78ed11dc70d
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 1%

---

# Analyserar sidprestanda{#analyzing-page-performance}

Öppna [Content Insight](/help/sites-authoring/content-insights.md) för att analysera hur sidan du redigerar fungerar. Konfigurera rapporteringsperioden så att analysen fokuseras.

## Öppna Analytics och Recommendations för en sida {#opening-analytics-and-recommendations-for-a-page}

Använd följande procedur för att visa Analytics och Recommendations för en sida:

1. Navigera till sidan som du vill analysera.
1. Klicka på i verktygsfältet **Analyser och Recommendations**.

   >[!NOTE]
   >
   >Analyser och Recommendations för en sida visas bara om du har konfigurerat AEM till [integrera med Adobe Analytics](/help/sites-administering/adobeanalytics-connect.md).

   ![screen-shot_2019-03-05at115319](assets/screen-shot_2019-03-05at115319.png)

### Ändra rapporteringsperioden {#changing-the-reporting-period}

Ändra följande tidsrelaterade aspekter av analysrapporterna:

* Den tidsperiod som ska rapporteras.
* Datas granularitet.

Verktygen för att ändra de tidsrelaterade aspekterna av rapporterna visas högst upp på sidan Innehållsinsikter. ![chlimage_1-126](assets/chlimage_1-126.png)

#### Ändra rapporteringsperioden {#changing-the-reporting-period-1}

Ändra rapporteringsperioden för Content Insight-sidan så att analysen av sidaktiviteten fokuseras till en viss tidsperiod. När du ändrar rapporteringsperioden uppdateras rapporterna automatiskt. Det skuggade området i tidsramen representerar rapporteringsperioden. Datumen i tidsramen ökar från vänster till höger.

![chlimage_1-127](assets/chlimage_1-127.png)

Så här ändrar du rapporteringsperioden för en Content Insight-sida:

1. Om tidsramen inte visas överst på sidan klickar du på ikonen Växla tidsram.

   ![Växla tidsram](do-not-localize/chlimage_1-22.png)

1. Om du vill ändra startdatumet för rapportperioden drar du cirkeln som visas till vänster om det skuggade området till önskat startdatum.

   Om du inte kan se den vänstra sidan av det skuggade området använder du rullningslisten för att visa det.

1. Om du vill ändra slutdatumet för rapportperioden drar du cirkeln som visas till höger om det skuggade området till önskat slutdatum.

#### Ändra rapportperiodens kornighet {#changing-the-granularity-of-the-reporting-period}

Ändra den tid som varje datapunkt sträcker sig över i en rapport. Om du t.ex. markerar granulariteten för vecka, representerar varje datapunkt i rapporten Vyer antalet vyer under en vecka.

![screen_shot_2017-11-29at141001](assets/screen_shot_2017-11-29at141001.png)

Granulariteten påverkar rapporter som anger data i förhållande till tid, t.ex. rapporter om Vyer och Genomsnittligt engagerade sidminuter. Kornigheten påverkar också skalan för tidsramen.

1. Om granularitetskontrollen inte visas klickar du på ikonen Växla granularitet.

   ![chlimage_1-128](assets/chlimage_1-128.png)

1. Klicka på önskad granularitet. När du har valt det här alternativet uppdateras rapporten automatiskt så att den avspeglar granulariteten.

### Tilldela uppgifter för SEO Recommendations {#assigning-tasks-for-seo-recommendations}

Använd SEO Recommendations-rapporten för att skapa uppgifter för att förbättra sidsynligheten för sökmotorer. För varje rekommendation i rapporten som inte har någon bock kan du skapa en uppgift som du tilldelar en användare för att utföra det arbete som krävs.

![chlimage_1-129](assets/chlimage_1-129.png)

Statusen för SEO-rekommendationen anger när uppgiften har skapats men inte slutförts än.

![chlimage_1-130](assets/chlimage_1-130.png)

När uppgiften skapas visas den i användarens uppgiftslista. Mer information om uppgifter finns i [Arbeta med uppgifter](/help/sites-authoring/task-content.md).

Använd följande procedur för att skapa en uppgift för en SEO-rekommendation.

1. Klicka på informationsikonen för SEO-rekommendationen.

   ![Informationsikon](do-not-localize/chlimage_1-23.png)

1. Klicka på den inringade triangeln som visas bredvid informationsikonen.

   ![chlimage_1-131](assets/chlimage_1-131.png)

1. Fyll i formulärfälten som visas och tryck sedan på Skapa:

   * Projekt: Välj i vilket projekt uppgiften ska skapas.
   * Namn: Namnet som identifierar uppgiften. Standardnamnet är titeln på SEO-rekommendationen.
   * Tilldela till: Välj den användare som ska tilldelas uppgiften. Börja skriva användarens namn för att filtrera listan.
   * Beskrivning: En beskrivning av aktiviteten som krävs för att slutföra uppgiften. Standardbeskrivningen är den information som medföljer SEO-rekommendationen.
   * Aktivitetsprioritet: Uppgiftens prioritet.
   * Förfallodatum: Det datum då uppgiften ska vara slutförd.

   **Obs!** Uppgiften som skapas innehåller även sökvägen till sidan som SEO-rekommendationen gäller för.

1. Klicka på Klar för att stänga meddelandet Aktiviteten har skapats.
