---
title: Förstå segmentering
seo-title: Förstå segmentering
description: Segmentering är en viktig faktor när man skapar en kampanj
seo-description: Segmentering är en viktig faktor när man skapar en kampanj
uuid: 900da068-5dda-4b6b-8be3-4b7ad614126d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 36c87684-e62a-4983-b123-87f56dbf7bc5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Förstå segmentering{#understanding-segmentation}

Segmentering är en viktig faktor när man skapar en kampanj. I de flesta fall måste ni ha definierade segment innan ni kan påbörja kampanjen.

Besökare har olika intressen och mål när de besöker en webbplats. Att förstå dessa mål och uppfylla förväntningarna är en viktig framgångsrik faktor för onlinemarknadsföring.

Segmentering hjälper till att uppnå detta genom att analysera och karakterisera besökarens:

* aktivitet på webbplatsen
* profil
* aktivitet på andra webbplatser

Innehållet kan sedan anpassas specifikt efter besökarens behov och intressen, beroende på vilket segment de matchar.

## Använda segmentering {#using-segmentation}

Segment definieras i [Konfigurera segmentering](/help/sites-administering/campaign-segmentation.md). De används för att styra det faktiska innehåll som ses av en viss målgrupp.

## Segmenteringsterminologi {#segmentation-terminology}

Vid diskussion av segmentering används följande terminologi:

**Besökare** En besökare är en person som besöker en webbplats. Personens besök börjar oftast från en hänvisande sida och går sedan vidare till en eller flera sidvisningar på din egen webbplats. En beteendeprofil kan skapas utifrån detaljerna från den personens besök.

**Användare** En användare är en besökare som registrerar sig hos webbplatsen för att få en kontoprofil. För att generera en profil kan de tillhandahålla ytterligare identifiering, till exempel en e-postadress och ett kön, bland annat. Ytterligare information kan också samlas in, bland annat om communityaktiviteter och köpmönster. Baserat på informationen i profilen kan en demografisk profil skapas.

**Trait** A trait är en egenskap hos en besökare som kan användas för att bestämma medlemskap i ett visst segment.

**Segment** Ett segment är en samling besökare som delar vissa egenskaper. Segmenten bör vara distinkta, med ett minimum av överlappning med andra segment.

**Beteenden** är beteenden som relaterar till besökarens beteende på webbplatsen. Bland dessa finns:

* Intresset på er webbplats; inklusive besökta sidor och köpta produkter.
* Intresse för den webbplats som refererar. inklusive söktermer som används eller annonser som klickas på.
* Intresse av andra anläggningar. med verktyg som Spyjax.
* Besökarnas lojalitet. Besöken ska pågå, besöksfrekvens.

**Demografiska egenskaper** Dessa är utvalda populationsegenskaper, inklusive:

* Ålder
* Inkomst
* Familjestorlek
* Civilstånd
* Kön
* Plats

**Härledda egenskaper** Vissa demografiska egenskaper är svåra att fastställa utan registrering, men kan härledas genom en kombination av beteendemässiga och demografiska egenskaper.

Om du till exempel kombinerar den refererande URL:en (som en beteendeegenskap) med demografiska data (som hämtats från verktyg som [Google Ad Planner](https://www.google.com/adplanner/)) kan webbplatsägarna skapa demografiska egenskaper för sina besökare.

**Delsegment** Ett segment kan delas upp i flera delsegment. Detta görs genom att definiera ytterligare egenskaper.

**Teaser Page** A teaser page is directed to a specific audias. Den innehåller återanvändbart innehåll som kan användas i det underordnade stycket.

**Campaign** En kampanj består av en samling interaktiva sidor och e-postmarknadsföringssidor, som nyhetsbrev och inbjudningar. En kampanj körs vanligtvis under en begränsad period och ersätts av en annan kampanj.

**Teaser Paragraph** Det här är ett stycke som hämtar innehåll från en annan sida beroende på en markeringsstrategi. Denna urvalsstrategi kan ta segment och kampanjer i beaktande.

**Lista** En lista extraheras från ett segment med registrerade användare. Den plats som t.ex. används för att styra innehållet i det traderande stycket.

>[!NOTE]
>
>Mer information om segment i AEM finns i [Segmentering](/help/sites-administering/campaign-segmentation.md) .

