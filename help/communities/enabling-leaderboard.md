---
title: Funktion för resultatavla
seo-title: Leaderboard Feature
description: Lägga till en Leaderboard-komponent på en sida
seo-description: Adding a Leaderboard component to a page
uuid: c4633919-75d3-4bc7-830c-ef9c28cc1cba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9045ce2e-a06d-4da5-9b83-56dd823007bb
docset: aem65
exl-id: 8b4d56d9-ba73-4eda-9773-3daaa9237abe
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# Funktion för resultatavla {#leaderboard-feature}

## Introduktion {#introduction}

The `Leaderboard` -komponenten ger möjlighet att få en uppfattning om hur medlemmarna interagerar inom communityn genom att rangordna medlemmar enligt poäng (grundläggande poängsättning) eller deras sakkunskap (avancerad poängsättning).

Innan du tar med huvudpanelskomponenten på en sida måste du konfigurera [Communities Scoring and Badges](/help/communities/implementing-scoring.md).

I det här avsnittet av dokumentationen beskrivs:

* Lägga till `Leaderboard` till en [communitywebbplats](/help/communities/overview.md#community-sites).
* Konfigurationsinställningar för `Leaderboard` -komponenten.

### Lägga till en huvudpanel på en sida {#adding-a-leaderboard-to-a-page}

Lägga till en `Leaderboard` till en sida i redigeringsläge, leta reda på komponenten

* `Communities / Leaderboard`

och dra den till rätt plats på en sida.

Nödvändig information finns på [Grunderna för communitykomponenter](/help/communities/basics.md).

När komponenten placeras på en sida i en community-webbplats är det så här den visas:

![rankningslista](assets/leaderboard.png)

### Konfigurerar huvudpanel {#configuring-leaderboard}

Markera den monterade `Leaderboard` -komponenten som ska få åtkomst till och markera `Configure` som öppnar redigeringsdialogrutan.

![configure-new](assets/configure-new.png)

![configure-leaderboard](assets/configure-leaderboard.png)

#### Fliken Inställningar {#settings-tab}

Under **[!UICONTROL Settings]** anger du vilken information om medlemmen som visas:

* **Visningsnamn**

   Ett beskrivande namn som ska visas för styrelsen, som återspeglar reglerna som valts för att visa märken och poäng.
Standard är `Leaderboard`, om inget anges.

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

   (Obligatoriskt) Specifik regel som genererar poängen som ska visas.

* **Märkningsregel**

   (Obligatoriskt) Specifik regel som genererar märket som ska visas.

* **Visningsgräns**

   Antal medlemmar som ska visas per sida. Standard är 10.

### Exempel: Deltagare i ledningsgruppen {#example-participants-leaderboard}

Den här resultatöversikten är en följd av att grundläggande poängregler har tillämpats.

Konfiguration av huvudpanelskomponent:

* Fliken Inställningar:

   * Visningsnamn = `Participation Board`
   * `checked`:

      * Badge
      * Märkesnamn
      * Använd avatar

* Fliken Regler:

   * Regelplats = `/content/sites/<site name>/jcr:content`
   * Poängregel = `/libs/settings/community/scoring/rules/forums-scoring`
   * Badningsregel = `/libs/settings/community/badging/rules//reference-badging`
   * Visningsgräns = `10`

![deltagare-rankningslista](assets/participants-leaderboard.png)

### Exempel: Experter Leaderboard {#example-experts-leaderboard}

Den här resultatöversikten är en följd av att avancerade poängregler har tillämpats.

Konfiguration av huvudpanelskomponent:

* Fliken Inställningar:

   * Visningsnamn = `Expertise Board`
   * `checked`:

      * Badge
      * Använd avatar

* Fliken Regler:

   * Regelplats = `/content/sites/<site name>/jcr:content`
   * Poängregel = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * Badningsregel = `/libs/settings/community/badging/rules/adv-forums-badging`
   * Visningsgräns = `10`

![expertråd](assets/experts-leaderboard.png)

### Ytterligare information {#additional-information}

Mer information finns på [Grundläggande om Ledningsbord](/help/communities/leaderboard.md) för utvecklare.

Instruktioner för hur du skapar regler finns i [Communities Scoring and Badges](/help/communities/implementing-scoring.md) för administratörer.
