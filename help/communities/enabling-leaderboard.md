---
title: Funktion för resultatavla
description: Läs om hur medlemmarna interagerar i communityn genom att rangordna medlemmarna utifrån poäng och expertis.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 8b4d56d9-ba73-4eda-9773-3daaa9237abe
source-git-commit: b8887b4a6f757352e9dbfdf074c10e9ccd6dbd4f
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# Funktion för resultatavla {#leaderboard-feature}

## Introduktion {#introduction}

The `Leaderboard` kan du få en uppfattning om hur medlemmar interagerar inom communityn genom att rangordna medlemmar enligt poäng (grundläggande poängsättning) eller deras sakkunskap (avancerad poängsättning).

Innan du tar med komponenten för rankningslistan på en sida måste du konfigurera [Communities Scoring and Badges](/help/communities/implementing-scoring.md).

I det här avsnittet av dokumentationen beskrivs:

* Lägga till `Leaderboard` till en [communitywebbplats](/help/communities/overview.md#community-sites).
* Konfigurationsinställningar för `Leaderboard` -komponenten.

### Lägga till en huvudpanel på en sida {#adding-a-leaderboard-to-a-page}

Lägga till en `Leaderboard` till en sida i redigeringsläge, leta reda på komponenten

* `Communities / Leaderboard`

Och dra den till rätt plats på en sida.

Nödvändig information finns på [Grunderna för communitykomponenter](/help/communities/basics.md).

När komponenten placeras på en sida i en community-webbplats är det så här den visas:

![huvudbok](assets/leaderboard.png)

### Konfigurerar huvudpanel {#configuring-leaderboard}

Markera den monterade `Leaderboard` så att du kan komma åt och välja `Configure` -ikonen som öppnar redigeringsdialogrutan.

![configure-new](assets/configure-new.png)

![configure-leaderboard](assets/configure-leaderboard.png)

#### Fliken Inställningar {#settings-tab}

Under **[!UICONTROL Settings]** anger du vilken information om medlemmen som visas:

* **Visningsnamn**

  Ett beskrivande namn som ska visas för styrelsen, som återspeglar reglerna som valts för att visa märken och poäng.
Standard är `Leaderboard` om inget anges.

* **Badge**

  Om du markerar det här alternativet inkluderas en kolumn för ikoner för emblem i rankningspanelen.
Standard är avmarkerat.

* **Märkesnamn**

  Om du markerar det här alternativet inkluderas en kolumn för märkordsnamnet i resultatlistan.
Standard är avmarkerat.

* **Använd avatar**

  Om det här alternativet är markerat inkluderas medlemmens avatarbild i ledningsgruppen bredvid namnlänken till medlemsprofilen.
Standard är avmarkerat.

#### Fliken Regler {#rules-tab}

Under **Regler** -fliken, communitywebbplatsen och dess regler för poäng och badning

* **Regelplats**

  (Obligatoriskt) Plats där poängsättningsregeln/badging-regeln är konfigurerad.

* **Poängregel**

  (Obligatoriskt) Specifik regel som genererar de bakgrundsmusik som ska visas.

* **Märkningsregel**

  (Obligatoriskt) Specifik regel som genererar märket som ska visas.

* **Visningsgräns**

  Antal medlemmar som ska visas per sida. Standardvärdet är 10.

### Exempel: Deltagarlista {#example-participants-leaderboard}

Den här resultatöversikten är en följd av att grundläggande poängregler har tillämpats.

Konfiguration av huvudpanelskomponent:

* Fliken Inställningar:

   * Visningsnamn = `Participation Board`
   * `checked`:

      * Badge
      * Märkesnamn
      * Använd avatar

* fliken Regler:

   * Regelplats = `/content/sites/<site name>/jcr:content`
   * Poängregel = `/libs/settings/community/scoring/rules/forums-scoring`
   * Badningsregel = `/libs/settings/community/badging/rules//reference-badging`
   * Visningsgräns = `10`

![deltagare-rankningslista](assets/participants-leaderboard.png)

### Exempel: Expert Leaderboard {#example-experts-leaderboard}

Den här resultatöversikten är en följd av att avancerade poängregler har tillämpats.

Konfiguration av huvudpanelskomponent:

* Fliken Inställningar:

   * Visningsnamn = `Expertise Board`
   * `checked`:

      * Badge
      * Använd avatar

* fliken Regler:

   * Regelplats = `/content/sites/<site name>/jcr:content`
   * Poängregel = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * Badningsregel = `/libs/settings/community/badging/rules/adv-forums-badging`
   * Visningsgräns = `10`

![expertråd](assets/experts-leaderboard.png)

### Ytterligare information {#additional-information}

Mer information finns på [Grundläggande om Ledningsbord](/help/communities/leaderboard.md) för utvecklare.

Instruktioner för hur du skapar regler finns i [Communities Scoring and Badges](/help/communities/implementing-scoring.md) sida för administratörer.
