---
title: Content Insight
seo-title: Content Insight
description: Content Insight ger information om sidprestanda med hjälp av webbanalys och SEO-rekommendation
seo-description: Content Insight ger information om sidprestanda med hjälp av webbanalys och SEO-rekommendation
uuid: 32f5b37c-2a82-462a-9f0a-c19bed46e198
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 60f980fd-049e-43c1-8b5d-60a8279b357a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Content Insight{#content-insight}

Content Insight ger information om sidprestanda med hjälp av webbanalyser och SEO-rekommendationer. Använd Content Insight för att fatta beslut om hur du ändrar sidor eller för att lära dig hur tidigare ändringar har ändrat prestandan. För varje sida som du skapar kan du öppna Content Insight och analysera sidan.

![chlimage_1-311](assets/chlimage_1-311.png)

Layouten på sidan Content Insight ändras så att den passar skärmdimensionerna och orienteringen för den enhet som du använder.

## Rapportdata

På Content Insight-sidan finns rapporter som använder data från Adobe SiteCatalyst, Adobe Target, Adobe Social och BrightStor:

* SiteCatalyst: Det finns rapporter om följande mätvärden:

   * Sidvyer
   * Genomsnittlig tid på sidan
   * Källor

* Mål: Rapporter om kampanjaktiviteter som din sida innehåller erbjudanden för.
* BrightEdge: Rapporterar sidfunktioner som gör sidan mer synlig för sökmotorer och rekommenderar funktioner som ska implementeras.

Se [Öppna analyser och rekommendationer för en sida](/help/sites-authoring/ci-analyze.md#opening-analytics-and-recommendations-for-a-page).

## Rapporteringsperiod

Rapporterna visar data för en tidsperiod som du bestämmer. När du justerar rapportperioden uppdateras rapporterna automatiskt med data för den perioden. Visuella ledtrådar anger när sidversioner ändras, så att du kan jämföra prestanda för varje version.

Du kan också ange hur detaljerad den rapporterade informationen är, t.ex. kan du se data varje dag, vecka, månad eller år.

Se [Ändra rapporteringsperiod](/help/sites-authoring/ci-analyze.md#changing-the-reporting-period).

>[!NOTE]
>
>Content Insights-rapporterna kräver att administratören har integrerat AEM med SiteCatalyst, Target och BrightEdge. Se [Integrera med SightCatalyst](/help/sites-administering/adobeanalytics.md), [Integrera med Adobe Target](/help/sites-administering/target.md)och [Integrera med BrightEdge](/help/sites-administering/brightedge.md).

## Vyrapporten {#the-views-report}

Vyrapporten innehåller följande funktioner för utvärdering av sidtrafik:

* Det totala antalet vyer för en sida för rapporteringsperioden.
* En diagram över antalet visningar under rapporteringsperioden:

   * Totalt antal vyer.
   * Unika besökare.

![chlimage_1-312](assets/chlimage_1-312.png)

## Genomsnittlig engagerad sidrapport {#the-page-average-engaged-report}

Rapporten Page Average Engaged innehåller följande funktioner för utvärdering av sideffektivitet:

* Den genomsnittliga tid som sidan är öppen under hela rapporteringsperioden.
* Ett diagram över den genomsnittliga längden på en sidvy under rapporteringsperioden.

![chlimage_1-313](assets/chlimage_1-313.png)

## Källrapporten {#the-sources-report}

Källrapporten visar hur användare navigerade till sidan, t.ex. från sökmotorresultat eller med den kända URL:en.

![chlimage_1-314](assets/chlimage_1-314.png)

## Studsrapporten {#the-bounces-report}

Satsrapporten innehåller ett diagram som visar antalet studsar som har inträffat för en sida under den valda rapporteringsperioden.

![chlimage_1-315](assets/chlimage_1-315.png)

## Kampanjaktivitetsrapporten {#the-campaign-activity-report}

För varje kampanj som sidan är aktiv för visas en rapport med namnet *Kampanjnamnsaktivitet* . Rapporten visar hur många sidor och konverteringar som gjorts för varje segment som erbjudandet gäller.

![chlimage_1-316](assets/chlimage_1-316.png)

## SEO-rekommendationsrapporten {#the-seo-recommendations-report}

SEO-rekommendationsrapporten innehåller resultaten av BrightEdge-analysen för sidan. Rapporten är en checklista med sidfunktioner som anger vilka funktioner sidan innehåller och inte innehåller för att maximera sökbarheten med sökmotorer.

I rapporten kan du skapa uppgifter så att det görs förbättringar för att förbättra sidans sökbarhet. Rekommendationer indikerar att åtgärder har skapats för att implementera rekommendationen. Se [Tilldela uppgifter för SEO-rekommendationer](/help/sites-authoring/ci-analyze.md#assigning-tasks-for-seo-recommendations).

![chlimage_1-317](assets/chlimage_1-317.png)

