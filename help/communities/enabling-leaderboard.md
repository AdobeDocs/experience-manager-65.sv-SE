---
title: Funktion för resultatavla
seo-title: Funktion för resultatavla
description: Lägga till en Leaderboard-komponent på en sida
seo-description: Lägga till en Leaderboard-komponent på en sida
uuid: c4633919-75d3-4bc7-830c-ef9c28cc1cba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9045ce2e-a06d-4da5-9b83-56dd823007bb
docset: aem65
translation-type: tm+mt
source-git-commit: 6720d5a0fdf1facc0b10011ec306dffbb31f4ac5
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 1%

---


# Ledarbordsfunktion {#leaderboard-feature}

## Introduktion {#introduction}

Komponenten `Leaderboard` ger möjlighet att förstå hur medlemmar interagerar inom communityn genom att rangordna medlemmar enligt poäng (grundläggande poängsättning) eller deras sakkunskap (avancerad poängsättning).

Innan du inkluderar huvudpanelskomponenten på en sida måste du konfigurera [Webbgruppsbedömning och emblem](/help/communities/implementing-scoring.md).

I det här avsnittet av dokumentationen beskrivs:

* Lägger till komponenten `Leaderboard` i en [community-webbplats](/help/communities/overview.md#community-sites).
* Konfigurationsinställningar för komponenten `Leaderboard`.

### Lägga till en huvudpanel på en sida {#adding-a-leaderboard-to-a-page}

Om du vill lägga till en `Leaderboard`-komponent på en sida i redigeringsläge letar du reda på komponenten

* `Communities / Leaderboard`

och dra den till rätt plats på en sida.

Mer information finns på [Grunderna för communitykomponenter](/help/communities/basics.md).

När komponenten placeras på en sida i en community-webbplats är det så här den visas:

![chlimage_1-8](assets/chlimage_1-8.png)

### Konfigurerar huvudpanelen {#configuring-leaderboard}

Markera den monterade `Leaderboard`-komponenten som ska öppnas och välj ikonen `Configure` som öppnar redigeringsdialogrutan.

![chlimage_1-9](assets/chlimage_1-9.png)

![chlimage_1-10](assets/chlimage_1-10.png)

#### Fliken Inställningar {#settings-tab}

Under fliken **[!UICONTROL Settings]** anger du vilken information om medlemmen som visas:

* **Visningsnamn**

   Ett beskrivande namn som ska visas för styrelsen, som återspeglar reglerna som valts för att visa märken och poäng.
Standardvärdet är `Leaderboard`, om inget anges.

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

Under fliken **Regler**, communitywebbplatsen och dess regler för bedömning och märkning

* **Regelplats**

   (Obligatoriskt) Plats där poängsättningsregeln/badging-regeln är konfigurerad.

* **Poängregel**

   (Obligatoriskt) Specifik regel som genererar poängen som ska visas.

* **Märkningsregel**

   (Obligatoriskt) Specifik regel som genererar märket som ska visas.

* **Visningsgräns**

   Antal medlemmar som ska visas per sida. Standard är 10.

### Exempel: Deltagarnas huvudpanel {#example-participants-leaderboard}

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

![chlimage_1-11](assets/chlimage_1-11.png)

### Exempel: Expertledare {#example-experts-leaderboard}

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

![chlimage_1-12](assets/chlimage_1-12.png)

### Ytterligare information {#additional-information}

Mer information finns på sidan [Leaderboard Essentials](/help/communities/leaderboard.md) för utvecklare.

Instruktioner för hur du skapar regler finns på sidan [Webbgruppsbedömning och emblem](/help/communities/implementing-scoring.md) för administratörer.
