---
title: Använda röstning
seo-title: Using Voting
description: Lägga till komponenten Voting på en sida
seo-description: Adding the Voting component to a page
uuid: 56e6cced-2f2d-434a-8fde-92a6c2478a04
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 071cac6d-05c5-47ab-85bc-ead6693ca1f4
exl-id: aa90bf1b-6053-4949-b061-232d72b80682
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Använda röstning {#using-voting}

The `Voting` är ett användbart verktyg som gör att communitymedlemmar kan betygsätta en viss del av innehållet, till exempel ett svar i en QnA-komponent. Med `Voting` -komponent väljer medlemmarna upp- eller nedpilar för att ange sin åsikt.

## Lägga till omröstning på en sida {#adding-voting-to-a-page}

Lägga till en `Voting` -komponent till en sida i redigeringsläge använder du komponentwebbläsaren för att leta upp `Communities / Voting` och dra den till rätt plats på en sida, t.ex. en position som är relativ till funktionen som användarna kan rösta på.

Nödvändig information finns på [Grunderna för communitykomponenter](basics.md).

När [nödvändiga bibliotek på klientsidan](essentials-voting.md#essentials-for-client-side) ingår så här `Voting` visas.

![röstningskomponent](assets/voting-component.png)

## Konfigurerar röstning {#configuring-voting}

Markera den monterade `Voting` -komponenten som ska få åtkomst till och markera `Configure` som öppnar redigeringsdialogrutan.

![konfigurera](assets/configure-new.png)

Under **[!UICONTROL Texts & Labels]** anger du de egenskaper som används för att spela in röster.

![röstsetikett](assets/voting-label.png)

* **[!UICONTROL Positive Response Label]**

   (*Obligatoriskt*) Det interna egenskapsnamnet för ett positivt svar.

* **[!UICONTROL Negative Response Label]**

   (*Obligatoriskt*) Det interna egenskapsnamnet för ett negativt svar.

* **[!UICONTROL Tally Name]**

   (*Obligatoriskt*) Det interna, identifierbara egenskapsnamnet för den här instansen av en röstningskomponent.

## Site Visitor Experience {#site-visitor-experience}

### Medlemmar {#members}

Ledamöter får endast rösta en gång, men de får när som helst ändra sin röst.

### Anonym {#anonymous}

Anonym röstning stöds inte. Besökare måste registrera sig (bli medlem) och logga in för att kunna delta i omröstningen en gång.

## Ytterligare information {#additional-information}

Mer information finns på [Grundläggande röstning](essentials-voting.md) för utvecklare.
