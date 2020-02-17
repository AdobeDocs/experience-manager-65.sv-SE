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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Funktionen Aktivitetsströmmar{#activity-streams-feature}

## Introduktion {#introduction}

En inloggad community-medlems aktiviteter, till exempel publicering på ett forum eller i en blogg, samlas i en ström som kan filtreras och visas på olika sätt genom att `Activity Streams` komponenten konfigureras.

Möjligheten att följa ger en annan bild av aktiviteter när communitymedlemmar följer inlägg av intresse eller följer aktiviteter som andra communitymedlemmar utför.

Dokumentet beskriver:

* lägga till komponenten Activity Streams på en AEM-webbplats
* konfigurationsinställningar för komponenten Activity Streams

### Lägga till aktivitetsströmmar till en sida {#adding-activity-streams-to-a-page}

Om du vill lägga till en `Activity Streams` komponent på en sida i redigeringsläge använder du komponentwebbläsaren för att hitta

* `Communities / Activity Streams`

och dra den till rätt plats på en sida där aktivitetsströmmar ska visas.

Mer information finns i Grunderna för [communitykomponenter](/help/communities/basics.md).

När de [nödvändiga klientbiblioteken](/help/communities/essentials-activities.md#essentials-for-client-side) inkluderas visas `Activity Streams` komponenten så här:

![chlimage_1-24](assets/chlimage_1-24.png)

### Konfigurera aktivitetsströmmar {#configuring-activity-streams}

Markera den monterade `Activity Streams` komponent som du vill öppna och välj den `Configure` ikon som öppnar redigeringsdialogrutan.

![chlimage_1-25](assets/chlimage_1-25.png)

Ange vilka aktiviteter som ska visas på fliken **Användaraktiviteter** :

![chlimage_1-26](assets/chlimage_1-26.png)

* **Maximalt antal aktiviteter** antalet aktiviteter som ska visas

* **Sökväg till** direktuppspelningsresurs Lämna tomt om du vill använda community-webbplatsen eller community-gruppen som standard. Direktuppspelningsresursens sökväg identifierar aktivitetskällan. Standardvärdet är tomt.

* **Visa vyn** Användaraktiviteter, om den är markerad, innehåller aktivitetssidan en flik som filtrerar aktiviteter baserat på aktiviteter som genererats i communityn av den aktuella medlemmen. Standard är markerat.

* **Visa vyn** Alla aktiviteter, om den är markerad, innehåller aktivitetssidan en flik som innehåller alla aktiviteter som genereras i den community som den aktuella medlemmen har åtkomst till. Standard är markerat.

* **Visa följande vy** om det här alternativet är markerat innehåller aktivitetssidan en flik som filtrerar aktiviteter baserat på de som den aktuella medlemmen följer. Standard är markerat.

### Följande vy {#following-view}

Komponenter måste konfigureras för att aktivera följande. Funktioner som tillåter följande är [blogg](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [kalender](/help/communities/calendar.md), [filbibliotek](/help/communities/file-library.md)[](/help/communities/comments.md)och¥comments.

![chlimage_1-27](assets/chlimage_1-27.png)

Med knappen **Följ **kan du följa upp tävlingsbidrag som aktiviteter, [meddelanden](/help/communities/notifications.md)eller [prenumerationer](/help/communities/subscriptions.md). Varje gång **Följ **knappen är markerad går det att aktivera eller inaktivera en markering. Markeringen visas bara när den är konfigurerad. `Email Subscriptions`

Om någon av följande metoder är markerad ändras texten för knappen till **Följ**. Du kan välja `Unfollow All` att inaktivera alla metoder.

Knappen **Följ **visas

* när du visar en annan medlems profil
* på en huvudfunktionssida, t.ex. forum, QnA och bloggar

   * följer all aktivitet för den allmänna funktionen

* för ett visst inlägg, t.ex. ett forumämne, en QnA-fråga eller en bloggartikel

   * följer all aktivitet för den specifika posten

### Additional Information {#additional-information}

Mer information finns på sidan [Activity Streams Essentials](/help/communities/essentials-activities.md) för utvecklare.
