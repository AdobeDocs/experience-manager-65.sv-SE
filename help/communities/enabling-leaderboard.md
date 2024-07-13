---
title: Funktion för resultatavla
description: Läs om hur medlemmarna interagerar i communityn genom att rangordna medlemmarna utifrån poäng och expertis.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 8b4d56d9-ba73-4eda-9773-3daaa9237abe
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---

# Funktion för resultatavla {#leaderboard-feature}

## Introduktion {#introduction}

Komponenten `Leaderboard` hjälper dig att förstå hur medlemmar interagerar inom communityn genom att rangordna medlemmar enligt poäng (grundläggande poängsättning) eller deras expertis (avancerad poängsättning).

Innan du inkluderar huvudpanelskomponenten på en sida måste du konfigurera [Webbgruppsbedömning och badges](/help/communities/implementing-scoring.md).

I det här avsnittet av dokumentationen beskrivs:

* Lägger till komponenten `Leaderboard` till en [community-webbplats](/help/communities/overview.md#community-sites).
* Konfigurationsinställningar för komponenten `Leaderboard`.

### Lägga till en huvudpanel på en sida {#adding-a-leaderboard-to-a-page}

Om du vill lägga till en `Leaderboard`-komponent på en sida i redigeringsläge letar du reda på komponenten

* `Communities / Leaderboard`

Och dra den till rätt plats på en sida.

Mer information finns på [Grunderna för communitykomponenter](/help/communities/basics.md).

När komponenten placeras på en sida i en community-webbplats är det så här den visas:

![rankningslista](assets/leaderboard.png)

### Konfigurerar huvudpanel {#configuring-leaderboard}

Markera den monterade `Leaderboard`-komponenten så att du kan komma åt och markera ikonen `Configure` som öppnar redigeringsdialogrutan.

![configure-new](assets/configure-new.png)

![configure-leaderboard](assets/configure-leaderboard.png)

#### Fliken Inställningar {#settings-tab}

Under fliken **[!UICONTROL Settings]** anger du vilken information om medlemmen som visas:

* **Visningsnamn**

  Ett beskrivande namn som ska visas för styrelsen, som återspeglar reglerna som valts för att visa märken och poäng.
Standardvärdet är `Leaderboard` om inget anges.

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

Under fliken **Regler**, communitywebbplatsen och dess regler för poäng och märkning

* **Regelplats**

  (Obligatoriskt) Plats där poängsättningsregeln/badging-regeln är konfigurerad.

* **Poängregel**

  (Obligatoriskt) Specifik regel som genererar de bakgrundsmusik som ska visas.

* **Badging-regel**

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
   * Badging-regel = `/libs/settings/community/badging/rules//reference-badging`
   * Visningsgräns = `10`

![deltagare-leaderboard](assets/participants-leaderboard.png)

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
   * Badging-regel = `/libs/settings/community/badging/rules/adv-forums-badging`
   * Visningsgräns = `10`

![expertpanel](assets/experts-leaderboard.png)

### Ytterligare information {#additional-information}

Mer information finns på sidan [Ledarpanel Essentials](/help/communities/leaderboard.md) för utvecklare.

Instruktioner för hur du skapar regler finns på sidan [Värderingar och märken för ](/help/communities/implementing-scoring.md) för administratörer.
