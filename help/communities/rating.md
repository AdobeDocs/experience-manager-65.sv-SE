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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Använda klassificeringar {#using-ratings}

Komponenten `Rating`används fristående eller tillsammans med andra communityfunktioner. Med den här komponenten kan inloggade communitymedlemmar uttrycka sina åsikter genom att gradera innehåll.

## Lägga till en klassificering på en sida {#adding-a-rating-to-a-page}

Om du vill lägga till en `Rating`komponent på en sida i redigeringsläge, letar du reda på komponenten `Communities / Rating` och drar den till rätt plats på en sida, t.ex. en position som är relativ till funktionen som medlemmarna ska betygsätta.

Mer information finns i Grunderna för [communitykomponenter](basics.md).

När de [nödvändiga klientbiblioteken](rating-basics.md#essentials-for-client-side) inkluderas visas `Rating` komponenten på det här sättet.

![chlimage_1-493](assets/chlimage_1-493.png)

## Konfigurerar klassificering {#configuring-rating}

Markera den monterade `Rating` komponent som du vill öppna och välj den `Configure` ikon som öppnar redigeringsdialogrutan.

![chlimage_1-494](assets/chlimage_1-494.png)

Under fliken **[!UICONTROL Texter och etiketter]** anger du den interna identifieraren för klassificeringen.

![chlimage_1-495](assets/chlimage_1-495.png)

**[!UICONTROL Tally Name]**(*Required*) Ett enkelt namn på den instans `Rating`som unikt identifierar den här instansen. Måste vara ett giltigt nodnamn för databasen.

## Site Visitor Experience {#site-visitor-experience}

### Medlemmar {#members}

Endast en klassificering per medlem tillåts. Medlemmen kan när som helst ändra sin klassificering.

### Anonym {#anonymous}

Anonym publicering av en klassificering stöds inte. Besökare måste registrera sig (bli medlem) och logga in för att kunna delta.

## Additional Information {#additional-information}

Mer information finns på sidan [Värderingsgrunder](rating-basics.md) för utvecklare.
