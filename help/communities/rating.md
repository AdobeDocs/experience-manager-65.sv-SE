---
title: Använda klassificeringar
seo-title: Använda klassificeringar
description: Lägga till en klassificeringskomponent på en sida
seo-description: Lägga till en klassificeringskomponent på en sida
uuid: a986970b-1221-4648-9a69-410f4480e0ae
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a0e5491e-66bc-47b0-94a5-45a02bc558da
translation-type: tm+mt
source-git-commit: 0051791da06d15a48b82cf93164a89b4ea42ce98
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Använda klassificeringar {#using-ratings}

Komponenten `Rating` används fristående eller tillsammans med andra webbgruppsfunktioner. Med den här komponenten kan inloggade communitymedlemmar uttrycka sina åsikter genom att gradera innehåll.

## Lägga till en klassificering på en sida {#adding-a-rating-to-a-page}

Om du vill lägga till en `Rating`-komponent på en sida i redigeringsläge, letar du reda på komponenten `Communities / Rating` och drar den till rätt plats på en sida, t.ex. i förhållande till funktionen som medlemmarna ska betygsätta.

Mer information finns på [Grunderna för communitykomponenter](basics.md).

När de [nödvändiga klientbiblioteken](rating-basics.md#essentials-for-client-side) inkluderas visas `Rating`-komponenten så här.

![värdering](assets/rating.png)

## Konfigurerar klassificering {#configuring-rating}

Markera den monterade `Rating`-komponenten som ska öppnas och välj ikonen `Configure` som öppnar redigeringsdialogrutan.

![configure-new](assets/configure-new.png)

Under fliken **[!UICONTROL Texts & Labels]** anger du den interna identifieraren för klassificeringen.

![tallyname](assets/tallyname.png)

**[!UICONTROL Tally Name]**
(*Obligatoriskt*) Ett enkelt namn  `Rating` som unikt identifierar den här instansen. Måste vara ett giltigt nodnamn för databasen.

## Site Visitor Experience {#site-visitor-experience}

### Medlemmar {#members}

Endast en klassificering per medlem tillåts. Medlemmen kan när som helst ändra sin klassificering.

### Anonym {#anonymous}

Anonym publicering av en klassificering stöds inte. Besökarna måste registrera sig (bli medlem) och logga in för att kunna delta.

## Ytterligare information {#additional-information}

Mer information finns på sidan [Rating Essentials](rating-basics.md) för utvecklare.
