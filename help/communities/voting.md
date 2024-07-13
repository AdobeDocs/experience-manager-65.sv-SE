---
title: Använda röstning
description: Lär dig hur du lägger till komponenten Voting på en sida där medlemmar i den inloggade communityn kan klassificera ett visst innehåll, till exempel ett svar.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: aa90bf1b-6053-4949-b061-232d72b80682
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Använda röstning {#using-voting}

Komponenten `Voting` är ett användbart verktyg som gör att communitymedlemmar kan klassificera en viss del av innehållet, till exempel ett svar i en QnA-komponent. Med komponenten `Voting` kan medlemmar markera upp- eller nedpilar för att ange sin åsikt.

## Lägga till omröstning på en sida {#adding-voting-to-a-page}

Om du vill lägga till en `Voting`-komponent på en sida i redigeringsläge använder du komponentwebbläsaren. Leta reda på `Communities / Voting` och dra den till plats på en sida, till exempel en position som är relativ till funktionen som användare kan rösta på.

Mer information finns på [Grunderna för communitykomponenter](basics.md).

När de [nödvändiga klientbiblioteken](essentials-voting.md#essentials-for-client-side) inkluderas visas `Voting`-komponenten på det här sättet.

![röstkomponent](assets/voting-component.png)

## Konfigurerar röstning {#configuring-voting}

Markera den monterade `Voting`-komponenten så att du kan komma åt och markera ikonen `Configure` som öppnar redigeringsdialogrutan.

![konfigurera](assets/configure-new.png)

Ange de egenskaper som ska användas för att spela in röster på fliken **[!UICONTROL Texts & Labels]**.

![röstsetikett](assets/voting-label.png)

* **[!UICONTROL Positive Response Label]**

  (*Obligatoriskt*) Det interna egenskapsnamnet för ett positivt svar.

* **[!UICONTROL Negative Response Label]**

  (*Obligatoriskt*) Det interna egenskapsnamnet för ett negativt svar.

* **[!UICONTROL Tally Name]**

  (*Obligatorisk*) Det interna, identifierbara egenskapsnamnet för den här instansen av en röstningskomponent.

## Site Visitor Experience {#site-visitor-experience}

### Medlemmar {#members}

Ledamöter får endast rösta en gång, men de får när som helst ändra sin röst.

### Anonym {#anonymous}

Anonym röstning stöds inte. Besökare måste registrera sig (bli medlem) och logga in för att kunna delta i omröstningen en gång.

## Ytterligare information {#additional-information}

Mer information finns på sidan [Grundläggande röstning](essentials-voting.md) för utvecklare.
