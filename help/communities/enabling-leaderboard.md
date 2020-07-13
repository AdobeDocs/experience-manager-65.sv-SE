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


# Funktion för resultatavla {#leaderboard-feature}

## Introduktion {#introduction}

Komponenten `Leaderboard` ger möjlighet att få en uppfattning om hur medlemmarna interagerar inom communityn genom att rangordna medlemmar enligt poäng (grundläggande poängsättning) eller deras sakkunskap (avancerad poängsättning).

Innan du tar med huvudpanelskomponenten på en sida måste du konfigurera [Scoring and Badges](/help/communities/implementing-scoring.md)för Communities.

I det här avsnittet av dokumentationen beskrivs:

* Lägga till `Leaderboard` komponenten på en [communitywebbplats](/help/communities/overview.md#community-sites).
* Konfigurationsinställningar för `Leaderboard` komponenten.

### Lägga till en huvudpanel på en sida {#adding-a-leaderboard-to-a-page}

Om du vill lägga till en `Leaderboard` komponent på en sida i redigeringsläge letar du reda på komponenten

* `Communities / Leaderboard`

och dra den till rätt plats på en sida.

Mer information finns i Grunderna för [communitykomponenter](/help/communities/basics.md).

När komponenten placeras på en sida i en community-webbplats är det så här den visas:

![chlimage_1-8](assets/chlimage_1-8.png)

### Konfigurerar huvudpanel {#configuring-leaderboard}

Markera den monterade `Leaderboard` komponent som du vill öppna och välj den `Configure` ikon som öppnar redigeringsdialogrutan.

![chlimage_1-9](assets/chlimage_1-9.png)

![chlimage_1-10](assets/chlimage_1-10.png)

#### Fliken Inställningar {#settings-tab}

Under **[!UICONTROL Settings]** fliken anger du vilken information om medlemmen som ska visas:

* **Visningsnamn**

   Ett beskrivande namn som ska visas för styrelsen, som återspeglar reglerna som valts för att visa märken och bakgrundsmusik.
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

Under fliken **Regler** , communitywebbplatsen och dess regler för poäng och badging

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

![chlimage_1-11](assets/chlimage_1-11.png)

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

![chlimage_1-12](assets/chlimage_1-12.png)

### Additional Information {#additional-information}

Mer information finns på sidan [Ledarpanel Essentials](/help/communities/leaderboard.md) för utvecklare.

Instruktioner för hur du skapar regler finns på sidan [Värderingslista och badges](/help/communities/implementing-scoring.md) för webbgrupper för administratörer.
