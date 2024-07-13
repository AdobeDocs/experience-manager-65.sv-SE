---
title: Badges Console
description: Med konsolen Communities Badges kan du lägga till egna emblem som kan visas för medlemmar när de har en viss roll i communityn (tilldelade) eller när de har en viss roll i communityn
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 50ed9ec4-ff04-4f9d-aefb-0837542a9455
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Badges Console {#badges-console}

## Om Badges {#about-badges}

Med Konsolen Communities Badges kan du lägga till egna emblem som kan visas för en medlem när den har en viss roll i communityn (tilldelad).

### Synlighet för emblem {#badge-visibility}

För närvarande visas emblem som en community-medlem får, eller tilldelas, tillsammans med sitt namn och avatar på följande platser:

* Profiler
* [Forum](/help/communities/forum.md)
* [QnA](/help/communities/working-with-qna.md)
* [Ledartavlor](/help/communities/enabling-leaderboard.md)
* [Ideation](/help/communities/ideation-feature.md)

Navigera till Badges-konsolen i redigeringsmiljön:

* Från global navigering: **[!UICONTROL Tools]** > **[!UICONTROL Communities]** > **[!UICONTROL Badges]**

Den här konsolen visar de märken som är tillgängliga för tillfället och från vilka nya märken kan läggas till.

![badges-homepage](assets/badges-homepage.png)

## Skapa märke {#create-badge}

Ett märke skapas genom att en lämplig liten bild (72 dpi med en höjd på mellan 26 och 32 pixlar) överförs och ett namn anges. Badge-bilden lagras i databasen på `/libs/settings/community/badging/images` och replikeras automatiskt till publiceringsmiljön.

Om publiceringsmiljön är en grupp utgivare måste du konfigurera [användarsynkronisering](/help/communities/sync.md).

![create-badge](assets/create-badge.png)

* **Överför bild**

  (*Obligatoriskt*) En badge-bild med en rekommenderad storlek på 32 x 32 pixlar vid 72 dpi i JPEG- eller PNG-format.

* **Namn**

  (*Obligatoriskt*) Namnet på märket. Det är standardvärdet `Display Name` och databasnodens namn. Om `Name` inte är ett giltigt databasnodnamn ändras det.

* **Visningsnamn**

  (*Valfritt*) Namnet som ska visas för märket i användargränssnittet. Standard är den oförändrade text som har angetts för `Name`.

* **Beskrivning**

  (*Valfritt*) En beskrivning av märket.

## Ytterligare information {#additional-information}

Mer information om hur du konfigurerar regler för poäng och badging finns i [Betygsättning och emblem](/help/communities/implementing-scoring.md).

Information om hur du hanterar emblem för medlemmar finns i [Medlemskonsolen](/help/communities/members.md).
