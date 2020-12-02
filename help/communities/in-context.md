---
title: Sammanhangsbaserad moderering
seo-title: Sammanhangsbaserad moderering
description: Så här utför du moderatoråtgärder
seo-description: Så här utför du moderatoråtgärder
uuid: 282a8bea-2822-4e5c-b9f4-4d9a5380d895
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ee104f6f-123b-4a6e-9031-849fc1318cc5
translation-type: tm+mt
source-git-commit: 917fceffb58883df83e96f60da4769046a18f3c0
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---


# Kontextmoderering {#in-context-moderation}

För AEM Communities kan moderering utföras av administratörer och betrodda communitymedlemmar direkt på den publicerade sidan där communityinnehållet publicerades.

När du använder en [moderationskonsol](moderation.md) innehåller den information som visas för innehållet en länk till den publicerade sidan som ger åtkomst till ytterligare modereringsåtgärder som är tillgängliga vid moderering i kontext.

## Modereringsåtgärder {#moderation-actions}

På modereringsöversikten finns en beskrivning av [modereringsåtgärder](moderate-ugc.md#moderation-actions).

## Modereringsgränssnitt {#moderation-ui}

Användargränssnittet som visas för moderatorn i publiceringsinstansen finns i dialogrutan för publicering och hantering av användargenererat innehåll (UGC). Elementen i användargränssnittet bestäms av besökarens status - oavsett om de är...

1. Medlemmen som publicerade innehållet.
1. En tillförlitlig medlemsmoderator.
1. En administratör.
1. Inloggad, men varken administratör, moderator eller författare till innehållet.
1. Inte inloggad.

## Exempel {#example}

Med hjälp av [Geometrixx Engage](http://localhost:4503/content/sites/engage/en.html)-webbplatsen som skapades när [Komma igång med AEM Communities](getting-started.md) går det snabbt att konfigurera en tråd i ett forum där olika modereringsaktiviteter i publiceringsmiljön kan användas, vilket visas nedan.

Aaron McDonald (aaron.mcdonald@mailinator.com) identifierades som en betrodd community-medlem genom att han lades till i gruppen community-engage-moderators när webbplatsen skapades.

Rebekah Larsen (rebekah.larsen@trashymail.com) kan läggas till som medlem i en community-engage-members-grupp med [Medlemskonsolen](members.md).

Mer information om användargrupper finns på [Hantera användare och användargrupper](users.md).

### Skapa foruminlägg {#create-the-forum-posts}

* Logga in som Rebekah Larsen (rebekah.larsen@trashymail.com)

   * Välj forum
   * Välj nytt inlägg
   * Ange ämne

      När nektaret ska bytas ut mot födoämnen från Humming Bird

   * Ange brödtexten

      Jag har inte haft så stor framgång när jag har lagt på en matare till en luftfågel varje år. De verkar komma en dag eller två, då är det klart. Jag ändrar det en gång i veckan är det för långt? Måste jag ändra den tidigare?

   * Välj inlägg
   * Välj Logga ut

* Logga in som Aaron McDonald (aaron.mcdonald@mailinator.com)

   * Välj forum
   * Välj Läs mer för ämnet Hummingbird
   * Ange kommentaren för Posta svar

      Jag byter min en gång i veckan och får dem från maj till oktober.

   * Välj svar
   * Välj Logga ut

* Logga in som Andrew Schaeffer (andrew.schaeffer@trashymail.com)

   * Välj forum
   * Välj Läs mer för ämnet Hummingbird
   * Ange kommentaren för Posta svar

      Jag säljer nektar och feeds - gå till https://my.viral.url/

   * Välj svar
   * Välj Logga ut

### Anonym webbplatsbesökare (#5) {#anonymous-site-visitor}

Här följer en översikt över det forum som visas av en besökare som inte är inloggad (5).

En anonym besökare kan endast visa forumet, men inte publicera något innehåll eller utföra några modereringsåtgärder.

![community-forum-visitor](assets/community-forum-visitor.png)

### Ny medlem (#4) {#new-member}

Logga in som administratör och lägg till Boyd Larsen (boyd.larsen@dodgit.com) som ny medlem i en community-engage-members-grupp med [Medlemskonsolen](members.md) och logga sedan ut.

Vid publicering loggar du in som Boyd Larsen och öppnar tråden genom att välja `Forum` och sedan `Read more` för den hummingbird-posten.

Obs!

* Boyd har inte deltagit i forumet.
* Boyd kan inte ta bort någonting.
* Boyd är inloggad och kan svara eller flagga innehåll.

Låt Boyd markera Flagga för att flagga innehållet som publicerats av Andrew.

Logga ut

![community-forum-medlem](assets/community-forum-member.png)

### Administratör (#3) {#administrator}

Logga in som administratör (administratör) och öppna tråden genom att välja Forum och sedan Läs mer för ett inlägg.

Obs!

* Administratören kan flagga, ta bort, redigera, neka, klippa ut, stänga, fästa, använda.
* Administratören kan välja Administration för att komma åt modereringskonsolen.

![community-admin-forum](assets/community-admin-forum.png)

Välj menyalternativet Administration om du vill få åtkomst till [moderationskonsolen](moderation.md) från publiceringsmiljön.

Observera att för en administratör är allt modereringsbart innehåll synligt, inte bara innehåll från Geometrixx Engage Community-webbplatsen.

Sökfiltret är en sidopanel som växlar mellan att öppna och stänga.

Logga ut.

![moderation-console-publish](assets/moderation-console-publish.png)

### Community-moderator (#2) {#community-moderator}

Logga in som Aaron McDonald (aaron.mcdonal@mailinator.com), som är moderator i communityn, och gå till tråden genom att välja Forum och sedan Läs mer för den hummingbird-posten.

Obs!

* Aaron kan svara, ta bort, redigera eller neka sitt eget inlägg.
* Aaron kan också flagga/tillåt, svara, ta bort, redigera, neka annat innehåll.
* Aaron kan klippa ut forumämnet och flytta det till ett annat forum som han modererar för.
* Aaron kan välja Administration för att komma åt moderationskonsolen.

![community-forum-moderator](assets/community-forum-moderator.png)

Välj menyalternativet Administration om du vill få åtkomst till [moderationskonsolen](moderation.md) från publiceringsmiljön.

Observera att för en community-moderator är det bara moderatorbart innehåll från Geometrixx Engage community-webbplatsen som visas.

Observera att community-moderatorn har samma alternativ som administratören (bilden är när söksidofältet är stängt), men ingen åtkomst till andra AEM.

Logga ut.

![moderatoråtkomst](assets/moderator-access.png)

### Innehållsförfattare (#1) {#content-author}

Logga in som Rebekah Larsen (rebekah.larsen@mailinator.com), en community-medlem som startade tråden, och gå till tråden genom att välja Forum och sedan Läs mer för den hummingbird-posten.

Obs!

* Rebekah kan ta bort eller redigera sin egen post.
* Rebekah kan även svara på eller flagga annat innehåll.
* Rebekah har inte åtkomst till moderationskonsolen.

![community-forum-author](assets/community-forum-author.png)

