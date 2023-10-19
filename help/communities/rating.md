---
title: Använda klassificeringar
description: Lär dig hur du lägger till en klassificeringskomponent på en sida där inloggade communitymedlemmar kan uttrycka sina åsikter genom att klassificera innehåll.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# Använda klassificeringar {#using-ratings}

The `Rating` används fristående eller tillsammans med andra webbgruppsfunktioner. Med den här komponenten kan inloggade communitymedlemmar uttrycka sina åsikter genom att gradera innehåll.

## Lägga till en klassificering på en sida {#adding-a-rating-to-a-page}

Lägga till en `Rating` till en sida i redigeringsläge, leta reda på komponenten `Communities / Rating` och dra den till plats på en sida, till exempel en position i förhållande till funktionen som medlemmarna kan betygsätta.

Nödvändig information finns på [Grunderna för communitykomponenter](basics.md).

När [nödvändiga bibliotek på klientsidan](rating-basics.md#essentials-for-client-side) ingår så här `Rating` visas.

![värdering](assets/rating.png)

## Konfigurerar klassificering {#configuring-rating}

Markera den monterade `Rating` så att du kan komma åt och välja `Configure` -ikonen som öppnar redigeringsdialogrutan.

![configure-new](assets/configure-new.png)

Under **[!UICONTROL Texts & Labels]** anger du den interna identifieraren för klassificeringen.

![tallyname](assets/tallyname.png)

**[!UICONTROL Tally Name]**
(*Obligatoriskt*) Ett enkelt namn för `Rating` som unikt identifierar den här instansen. Måste vara ett giltigt nodnamn för databasen.

## Site Visitor Experience {#site-visitor-experience}

### Medlemmar {#members}

Endast ett omdöme per medlem tillåts. Medlemmen kan när som helst ändra sin klassificering.

### Anonym {#anonymous}

Anonym publicering av en klassificering stöds inte. Besökarna måste registrera sig (bli medlem) och logga in för att kunna delta.

## Ytterligare information {#additional-information}

Mer information finns på [Grundläggande omdömen](rating-basics.md) för utvecklare.
