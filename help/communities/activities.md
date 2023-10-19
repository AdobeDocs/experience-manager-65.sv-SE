---
title: Funktionen Aktivitetsströmmar
description: Lär dig hur aktiviteter hos en inloggad community samlas in i en ström som du kan filtrera och visa via komponenten Activity Streams.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2b2a5de0-e7c7-4417-a217-4b929bc7dcfb
source-git-commit: b8887b4a6f757352e9dbfdf074c10e9ccd6dbd4f
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Funktionen Aktivitetsströmmar {#activity-streams-feature}

## Introduktion {#introduction}

En inloggad community-medlems aktiviteter, till exempel publicering på ett forum eller en blogg, samlas i en ström som kan filtreras och visas på olika sätt genom att konfigurationen av `Activity Streams` -komponenten.

Möjligheten att följa ger en annan bild av aktiviteter när communitymedlemmar följer inlägg av intresse eller följer aktiviteter som andra communitymedlemmar utför.

Dokumentet beskriver:

* Lägga till komponenten Activity Streams på en AEM webbplats
* Konfigurationsinställningar för komponenten Activity Streams

### Lägga till aktivitetsströmmar till en sida {#adding-activity-streams-to-a-page}

Om du vill lägga till en `Activity Streams` -komponent till en sida i redigeringsläge använder du komponentwebbläsaren för att leta upp

* `Communities / Activity Streams`

Dra den till en sida där aktivitetsströmmar ska visas.

Nödvändig information finns på [Grunderna för communitykomponenter](/help/communities/basics.md).

När [nödvändiga bibliotek på klientsidan](/help/communities/essentials-activities.md#essentials-for-client-side) ingår så här `Activity Streams` visas:

![activity-streams](assets/activity-component.png)

### Konfigurera aktivitetsströmmar {#configuring-activity-streams}

Markera den monterade `Activity Streams` så att du kan komma åt och välja `Configure` -ikonen som öppnar redigeringsdialogrutan.

![konfigurera](assets/configure-new.png)

Under **Användaraktiviteter** -flik, ange vilka aktiviteter som ska visas:

![användaraktiviteter](assets/user-activities.png)

* **Maximalt antal aktiviteter**

  Antalet aktiviteter som ska visas

* **Sökväg för direktuppspelningsresurs**

  Lämna tomt som standard till communitywebbplatsen eller communitygruppen. Direktuppspelningsresursens sökväg identifierar aktivitetskällan. Standardvärdet är tomt.

* **Visa vy för användaraktiviteter**

  Om det här alternativet är markerat innehåller aktivitetssidan en flik som filtrerar aktiviteter baserat på aktiviteter som genererats i communityn av den aktuella medlemmen. Standard är markerat.

* **Visa vyn Alla aktiviteter**

  Om det här alternativet är markerat innehåller aktivitetssidan en flik som innehåller alla aktiviteter som genereras i den community som den aktuella medlemmen har tillgång till. Standard är markerat.

* **Visa följande vy**

  Om det här alternativet är markerat innehåller aktivitetssidan en flik som filtrerar aktiviteter baserat på de som den aktuella medlemmen följer. Standard är markerat.

### Följande vy {#following-view}

Komponenter måste konfigureras för att aktivera följande. Funktioner som tillåter följande är [blogg](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [kalender](/help/communities/calendar.md), [filbibliotek](/help/communities/file-library.md)och [kommentarer](/help/communities/comments.md).

![följande vy](assets/following-activities.png)

The **Följ** knappen är ett sätt att följa inmatningar som aktiviteter, [meddelanden](/help/communities/notifications.md), eller [prenumerationer](/help/communities/subscriptions.md). Varje gång **Följ** är markerad går det att aktivera eller inaktivera en markering. The `Email Subscriptions` markeringen finns bara när den är konfigurerad.

Om någon av följande metoder är markerad ändras texten till **Följande**. Det går att välja `Unfollow All` för att växla mellan olika metoder.

The **Följ** visas:

* När en annan medlems profil visas.
* På en huvudfunktionssida, till exempel forum, QnA och bloggar.

   * Följer alla aktiviteter för den allmänna funktionen.

* För ett visst inlägg, t.ex. ett forumämne, QnA-fråga eller bloggartikel.

   * Följer all aktivitet för den specifika posten.

### Ytterligare information {#additional-information}

Mer information finns på [Grundläggande om aktivitetsströmmar](/help/communities/essentials-activities.md) för utvecklare.
