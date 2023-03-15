---
title: Badges Console
seo-title: Badges Console
description: Med konsolen Communities Badges kan du lägga till egna emblem som kan visas för medlemmar när de har en viss roll i communityn (tilldelade) eller när de har en viss roll i communityn
seo-description: The Communities Badges console lets you add custom badges that can be displayed for members when earned (awarded) or when they take on a specific role in the community (assigned)
uuid: 7103b133-ef3f-47d6-a2dc-4e6ff92e8fed
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 135b3077-5343-4888-858d-de5e9b1d4b04
docset: aem65
role: Admin
exl-id: 50ed9ec4-ff04-4f9d-aefb-0837542a9455
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# Badges Console {#badges-console}

## Om Badges {#about-badges}

Konsolen Communities Badges innehåller funktioner för att lägga till egna emblem som kan visas för en medlem när den har tjänats in (tilldelats) eller när de har en specifik roll i communityn (tilldelats).

### Synlighet för emblem {#badge-visibility}

För närvarande visas emblem som en medlem i communityn får eller tilldelas tillsammans med sitt namn och avatar på följande platser:

* Profiler
* [Forum](/help/communities/forum.md)
* [QnA](/help/communities/working-with-qna.md)
* [Ledartavlor](/help/communities/enabling-leaderboard.md)
* [Ideation](/help/communities/ideation-feature.md)

Navigera till Badges-konsolen i redigeringsmiljön:

* Från global navigering: **[!UICONTROL Tools]** > **[!UICONTROL Communities]** > **[!UICONTROL Badges]**

Den här konsolen visar de emblem som är tillgängliga för tillfället och från vilka nya emblem kan läggas till.

![badges-homepage](assets/badges-homepage.png)

## Skapa märke {#create-badge}

Ett märke skapas genom att en lämplig liten bild (72 dpi med en höjd på mellan 26 och 32 pixlar) överförs och ett namn anges. Badge-bilden sparas i databasen på `/libs/settings/community/badging/images` och replikeras automatiskt till publiceringsmiljön.

Om publiceringsmiljön är en grupp utgivare måste du konfigurera [användarsynkronisering](/help/communities/sync.md).

![create-badge](assets/create-badge.png)

* **Överför bild**

   (*Obligatoriskt*) En badge-bild med en rekommenderad storlek på 32 x 32 pixlar vid 72 dpi i JPEG- eller PNG-format.

* **Namn**

   (*Obligatoriskt*) Namnet på märket. Det är standardinställningen `Display Name` samt databasens nodnamn. Om `Name` är inte ett giltigt databasnodnamn. Det kommer att ändras.

* **Visningsnamn**

   (*Valfritt*) Namnet som ska visas för märket i gränssnittet. Standard är den oförändrade text som anges för `Name`.

* **Beskrivning**

   (*Valfritt*) En beskrivning av märket.

## Ytterligare information {#additional-information}

Mer information om hur du ställer in regler för poäng och badging finns i [Betygsättning och emblem](/help/communities/implementing-scoring.md).

Information om hur du hanterar emblem för medlemmar finns i [Medlemskonsolen](/help/communities/members.md).
