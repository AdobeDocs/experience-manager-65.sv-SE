---
title: Funktionen Aktivitetsströmmar
seo-title: Funktionen Aktivitetsströmmar
description: En inloggad community-medlems verksamhet
seo-description: En inloggad community-medlems verksamhet
uuid: decd2d6c-4d4b-4698-a92c-2b5b441458cf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 89f3630f-c01a-4dc0-9ff5-169785f22c01
docset: aem65
translation-type: tm+mt
source-git-commit: fcdae5363e7a0070b5d6b76227e5c65efb71bc03
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 0%

---


# Aktivitetsströmmar, funktion {#activity-streams-feature}

## Introduktion {#introduction}

Aktiviteter som tillhör en signerad medlem i communityn, till exempel publicering på ett forum eller en blogg, samlas i en ström som kan filtreras och visas på olika sätt genom konfiguration av `Activity Streams`-komponenten.

Möjligheten att följa ger en annan bild av aktiviteter när communitymedlemmar följer inlägg av intresse eller följer aktiviteter som andra communitymedlemmar utför.

Dokumentet beskriver:

* Lägga till komponenten Activity Streams på en AEM
* Konfigurationsinställningar för komponenten för aktivitetsströmmar

### Lägga till aktivitetsströmmar på en sida {#adding-activity-streams-to-a-page}

Om du vill lägga till en `Activity Streams`-komponent på en sida i redigeringsläge använder du komponentwebbläsaren för att leta reda på

* `Communities / Activity Streams`

och dra den till rätt plats på en sida där aktivitetsströmmar ska visas.

Mer information finns på [Grunderna för communitykomponenter](/help/communities/basics.md).

När de [nödvändiga klientbiblioteken](/help/communities/essentials-activities.md#essentials-for-client-side) inkluderas visas följande `Activity Streams`-komponent:

![activity-streams](assets/activity-component.png)

### Konfigurerar aktivitetsströmmar {#configuring-activity-streams}

Markera den monterade `Activity Streams`-komponenten som ska öppnas och välj ikonen `Configure` som öppnar redigeringsdialogrutan.

![konfigurera](assets/configure-new.png)

Under fliken **Användaraktiviteter** anger du vilka aktiviteter som ska visas:

![användaraktiviteter](assets/user-activities.png)

* **Maximalt antal aktiviteter**

   Antalet aktiviteter som ska visas

* **Sökväg för direktuppspelningsresurs**

   Lämna tomt som standard till communitywebbplatsen eller community-gruppen. Direktuppspelningsresursens sökväg identifierar aktivitetskällan. Standardvärdet är tomt.

* **Visa vy för användaraktiviteter**

   Om det här alternativet är markerat innehåller aktivitetssidan en flik som filtrerar aktiviteter baserat på aktiviteter som genererats i communityn av den aktuella medlemmen. Standard är markerat.

* **Visa vyn Alla aktiviteter**

   Om det här alternativet är markerat kommer aktivitetssidan att innehålla en flik som innehåller alla aktiviteter som har skapats i den community som den aktuella medlemmen har åtkomst till. Standard är markerat.

* **Visa följande vy**

   Om det här alternativet är markerat innehåller aktivitetssidan en flik som filtrerar aktiviteter baserat på de som den aktuella medlemmen följer. Standard är markerat.

### Följande vy {#following-view}

Komponenter måste konfigureras för att aktivera följande. Följande funktioner tillåter [blogg](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [kalender](/help/communities/calendar.md), [filelibrary](/help/communities/file-library.md) och [kommentarer](/help/communities/comments.md).

![följande vy](assets/following-activities.png)

Med knappen **Följ** kan du följa poster som aktiviteter, [meddelanden](/help/communities/notifications.md) eller [prenumerationer](/help/communities/subscriptions.md). Varje gång knappen **Följ** är markerad går det att aktivera eller inaktivera en markering. Markeringen `Email Subscriptions` finns bara när den är konfigurerad.

Om någon av följande metoder är markerad ändras knappens text till **Följande**. Du kan av praktiska skäl välja `Unfollow All` för att inaktivera alla metoder.

Knappen **Följ** visas:

* När en annan medlems profil visas.
* På en huvudfunktionssida, till exempel forum, QnA och bloggar.

   * Följer alla aktiviteter för den allmänna funktionen.

* För ett visst inlägg, t.ex. ett forumämne, en QnA-fråga eller en bloggartikel.

   * Följer all aktivitet för den specifika posten.

### Ytterligare information {#additional-information}

Mer information finns på sidan [Activity Streams Essentials](/help/communities/essentials-activities.md) för utvecklare.
