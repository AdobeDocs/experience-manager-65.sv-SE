---
title: Använda röstning
seo-title: Använda röstning
description: Lägga till komponenten Voting på en sida
seo-description: Lägga till komponenten Voting på en sida
uuid: 56e6cced-2f2d-434a-8fde-92a6c2478a04
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 071cac6d-05c5-47ab-85bc-ead6693ca1f4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Använda röstning {#using-voting}

Komponenten är ett användbart verktyg som gör att communitymedlemmar kan betygsätta en viss del av innehållet, till exempel ett svar i en QnA-komponent. `Voting` Med komponenten markerar `Voting` medlemmarna upp- eller nedpilarna för att ange sin åsikt.

## Lägga till omröstning på en sida {#adding-voting-to-a-page}

Om du vill lägga till en `Voting` komponent på en sida i redigeringsläge använder du komponentwebbläsaren för att leta reda på `Communities / Voting` och dra den till rätt plats på en sida, t.ex. en position som är relativ till funktionen som användarna kan rösta på.

Mer information finns i Grunderna för [communitykomponenter](basics.md).

När de [nödvändiga klientbiblioteken](essentials-voting.md#essentials-for-client-side) inkluderas visas `Voting` komponenten på det här sättet.

![chlimage_1-307](assets/chlimage_1-307.png)

## Konfigurerar röstning {#configuring-voting}

Markera den monterade `Voting` komponent som du vill öppna och välj den `Configure` ikon som öppnar redigeringsdialogrutan.

![chlimage_1-308](assets/chlimage_1-308.png)

Under fliken **[!UICONTROL Texter och etiketter]** anger du vilka egenskaper som ska användas för röstinspelning.

![chlimage_1-309](assets/chlimage_1-309.png)

* **[!UICONTROL Positiv svarsetikett]**(*obligatoriskt*) Det interna egenskapsnamnet för ett positivt svar.

* **[!UICONTROL Negativ svarsetikett]**(*obligatoriskt*) Det interna egenskapsnamnet för ett negativt svar.

* **[!UICONTROL Tally Name]**(*Required*) The internal, identifier identifier property name for this instance of a vobe component.

## Site Visitor Experience {#site-visitor-experience}

### Medlemmar {#members}

Ledamöter får endast rösta en gång, men de får när som helst ändra sin röst.

### Anonym {#anonymous}

Anonym röstning stöds inte. Besökare måste registrera sig (bli medlem) och logga in för att kunna delta i omröstningen en gång.

## Additional Information {#additional-information}

Mer information finns på [sidan Voice Essentials](essentials-voting.md) för utvecklare.
