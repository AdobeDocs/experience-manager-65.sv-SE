---
title: Badges Console
seo-title: Badges Console
description: Med konsolen Communities Badges kan du lägga till egna emblem som kan visas för medlemmar när de har en viss roll i communityn (tilldelade) eller när de har en viss roll i communityn
seo-description: Med konsolen Communities Badges kan du lägga till egna emblem som kan visas för medlemmar när de har en viss roll i communityn (tilldelade) eller när de har en viss roll i communityn
uuid: 7103b133-ef3f-47d6-a2dc-4e6ff92e8fed
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 135b3077-5343-4888-858d-de5e9b1d4b04
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Badges Console{#badges-console}

## Om Badges {#about-badges}

Konsolen Communities Badges innehåller funktioner för att lägga till egna emblem som kan visas för en medlem när den har tjänats in (tilldelats) eller när de har en specifik roll i communityn (tilldelats).

### Synlighet för emblem {#badge-visibility}

För närvarande visas emblem som en medlem i communityn får eller tilldelas tillsammans med sitt namn och avatar på följande platser:

* profiler
* [forum](/help/communities/forum.md)
* [QnA](/help/communities/working-with-qna.md)
* [lederboards](/help/communities/enabling-leaderboard.md)
* [ideation](/help/communities/ideation-feature.md)

För att nå Badges-konsolen i redigeringsmiljön

* från global navigering: **Verktyg, Communities, Badges**

Den här konsolen visar de emblem som är tillgängliga för tillfället och från vilka nya emblem kan läggas till.

![chlimage_1-123](assets/chlimage_1-123.png)

## Skapa märke {#create-badge}

Ett märke skapas genom att en lämplig liten bild (72 dpi med en höjd på mellan 26 och 32 pixlar) överförs och ett namn anges. Badge-bilden lagras i databasen på `/etc/community/badging/images` och replikeras automatiskt till publiceringsmiljön.

Om publiceringsmiljön är en grupp utgivare måste du konfigurera [användarsynkronisering](/help/communities/sync.md).

![chlimage_1-124](assets/chlimage_1-124.png)

* **Överför bild**(*krävs*) En badge-bild med en rekommenderad storlek på 32 x 32 pixlar vid 72 dpi i antingen JPEG- eller PNG-format.

* **Namn**(*obligatoriskt*) Namnet på märket. Det är standardnodnamnet `Display Name` och databasnodnamnet. Om `Name` databasen inte är ett giltigt databasnodnamn ändras det.

* **Visningsnamn**(*valfritt*) Namnet som ska visas för märket i gränssnittet. Standard är den oförändrade text som anges för `Name`.

* **Beskrivning**(*valfritt*) En beskrivning av märket.

## Additional Information {#additional-information}

Mer information om hur du ställer in regler för poängsättning och märkning finns i [Betygsättning och emblem](/help/communities/implementing-scoring.md).

Information om hur du hanterar emblem för medlemmar finns i [Medlemskonsolen](/help/communities/members.md).
