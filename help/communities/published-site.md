---
title: Upplev den publicerade webbplatsen
description: Lär dig hur du bläddrar till den URL som visas när du skapar en plats, men på publiceringsservern.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: ebc4e1e7-34f0-4f4e-9f00-178dfda23ce4
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
workflow-type: tm+mt
source-wordcount: '1205'
ht-degree: 0%

---

# Upplev den publicerade webbplatsen {#experience-the-published-site}

## Bläddra till Ny webbplats vid publicering {#browse-to-new-site-on-publish}

Nu när den nyligen skapade communitywebbplatsen har publicerats bläddrar du till den URL som visas när du skapar webbplatsen, men på publiceringsservern, till exempel:

* Författar-URL = https://localhost:4502/content/sites/engage/en.html
* Publicera URL = https://localhost:4503/content/sites/engage/en.html

För att minimera förvirring om vilken medlem som är inloggad på författare och publicera bör du använda olika webbläsare för varje instans.

Vid första ankomsten till den publicerade webbplatsen är besökaren vanligtvis inte inloggad och anonym.

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![författarpublicerad](assets/authorpublished.png)

## Anonym webbplatsbesökare {#anonymous-site-visitor}

En anonym besökare ser följande i användargränssnittet:

* Webbplatsens namn (självstudiekurs för att komma igång)
* Ingen profillänk
* Ingen meddelandelänk
* Ingen meddelandelänk
* Sökfält
* Inloggningslänk
* Varumärkesbanderoll
* Menylänkar för de komponenter som ingår i referenswebbplatsmallen.

Om du markerar olika länkar är de skrivskyddade.

### Förhindra anonym åtkomst på JCR {#prevent-anonymous-access-on-jcr}

En känd begränsning exponerar communityinnehållet för anonyma besökare via jcr-innehåll och json, även om **tillåta anonym åtkomst** är inaktiverat för webbplatsens innehåll. Det här beteendet kan dock styras med delningsbegränsningar som en tillfällig lösning.

Följ de här stegen för att skydda communityplatsens innehåll från anonyma användare genom jcr-innehåll och json:

1. I AEM Author, gå till https://: port/editor.html/content/site/sitename.html.

   >[!NOTE]
   >
   >Gå inte till den lokaliserade webbplatsen.

1. Gå till **Sidegenskaper**.

   ![page-properties](assets/page-properties.png)

1. Gå till **Avancerat** -fliken.

1. Aktivera **Autentiseringskrav**.

   ![webbplatsautentisering](assets/site-authentication.png)

1. Lägg till inloggningssidans sökväg. Till exempel: **/content/....../GetStarted**.
1. Publicera sidan.

## Betrodd medlem i användargruppen {#trusted-community-member}

Den här upplevelsen förutsätter [Aaron McDonald](/help/communities/tutorials.md#demo-users) tilldelades rollerna för [community manager och moderator](/help/communities/create-site.md#roles). Om inte, gå tillbaka till författarmiljön till [ändra platsinställningarna](/help/communities/sites-console.md#modifying-site-properties) och väljer Aaron McDonald som både community manager och moderator.

I det övre högra hörnet väljer du `Log in`och signera med användarnamn (aaron.mcdonald@mailinator.com) och lösenord (lösenord). Observera möjligheten att logga in med Twitter- eller Facebook-autentiseringsuppgifter.

![inloggning](assets/login.png)

När du har loggat in som registrerad community-medlem kan du lägga märke till följande menyalternativ för att klicka och utforska din community-webbplats:

* **Profil** kan du visa och redigera din profil.
* [Meddelanden](/help/communities/configure-messaging.md) till avsnittet för direktmeddelanden där du kan göra följande:

   1. Visa direktmeddelanden som du har tagit emot (Inkorgen), skickat (Skickat) och tagit bort (Papperskorgen).
   1. Skapa nya direktmeddelanden så att du kan skicka till enskilda personer och grupper.

* [Meddelanden](/help/communities/notifications.md) går till meddelandeavsnittet där du kan visa dina intressanta händelser och redigera meddelandeinställningar.
* [Administration](/help/communities/published-site.md#moderationlink) dirigerar dig till AEM Communities Moderation Page, om du har modereringsbehörighet.

![adminscreen](assets/adminscreen.png)

Observera att kalendersidan är hemsidan eftersom den valda referenswebbplatsmallen inkluderade kalenderfunktionen först, följt av aktivitetsströmfunktion, forumfunktion osv. Den här strukturen visas från [Webbplatsmall](/help/communities/sites.md#edit-site-template) konsol eller när webbplatsegenskaper ändras i redigeringsmiljön:

![platsmall](assets/sitetemplate.png)

>[!NOTE]
>
>Mer information om Communities-komponenter och -funktioner finns på:
>
>* [Communities-komponenter](/help/communities/author-communities.md) (för författare)
>* [Grundläggande om komponenter, funktioner och funktioner](/help/communities/essentials.md) (för utvecklare)

### Formlänk {#forum-link}

Visa den grundläggande forumfunktionen genom att välja länken Forum.

Medlemmarna kan publicera ett nytt ämne eller följa ett ämne.

Besökarna kan visa inlägg och sortera dem på olika sätt.

![forumlink](assets/forumlink.png)

### Länken Grupper {#groups-link}

Eftersom Aaron är gruppadministratör kan Aron, genom att välja länken Grupper, skapa en community-grupp genom att välja en gruppmall, bild, om gruppen är öppen eller hemlig samt bjuda in medlemmar.

Detta är ett exempel där en grupp skapas i publiceringsmiljön.

Grupper kan också skapas i författarmiljön och hanteras i communitywebbplatsen i författarmiljön ([Community Groups console](/help/communities/groups.md)). Erfarenheten av [skapa grupper vid författare](/help/communities/nested-groups.md) är nästa i den här självstudien.

![grouplink](assets/grouplink.png)

Skapa en referensgrupp:

1. Välj **Ny grupp**
1. **Fliken Inställningar**

   * Gruppnamn: `Sports`
   * Beskrivning : `A parent group for various sporting groups`.
   * Grupp-URL-namn: `sports`
   * Välj `Open Group` (tillåt alla community-medlemmar att delta genom att gå med)

1. **Fliken Mallar**

   * Välj `Reference Group` (innehåller en gruppfunktion i sin struktur för att tillåta kapslade grupper)

1. Välj **Skapa grupp**

   ![creategroup](assets/creategroup.png)

När en ny grupp har skapats **välj den nya sportgruppen** om du vill skapa två grupper (kapslade) inuti. Eftersom en platsstruktur inte kan börja med gruppfunktionen måste du välja länken Grupper när du har öppnat gruppen Sport:

![grouplink1](assets/grouplink1.png)

Den andra uppsättningen länkar, med början `Blog`, tillhör den markerade gruppen, `Sports` grupp. Genom att välja sportar `Groups` kan du kapsla två grupper i gruppen Sport.

Lägg till två `new groups`.

* En namngiven `Baseball`

   * Låt det vara som `Open Group` (obligatoriskt medlemskap).
   * Välj på fliken Mallar `Conversational Group`.

* En namngiven `Gymnastics`

   * Ändra inställningen till `Member Only Group` (begränsat medlemskap).
   * Välj på fliken Mallar `Conversational Group`.

**Meddelande**:

* Det kan vara nödvändigt att uppdatera sidan innan båda grupperna visas.
* Den här mallen gör det *not* inkluderar funktionen groups, så att inga fler kapslingar av grupper är möjliga.
* På författaren [Gruppkonsol](/help/communities/groups.md) har ett tredje val - en `Public Group` (valfritt medlemskap).

När båda grupperna har skapats väljer du Baseball-gruppen, en öppen grupp, och lägger märke till dess länkar:

`Discussions` `What's New` `Members`

Gruppens länkar visas under huvudplatsens länkar och ger följande resultat:

![grouplink2](assets/grouplink2.png)

Vid författare - med administratörsbehörighet går du till [Konsol för webbgrupper](/help/communities/members.md) och lägg till Weston McCall i `Community Engage Gymnastics <uid> Members` grupp.

Fortsätt publicera, logga ut som Aaron McDonald och visa grupperna i Sports Group som en anonym besökare:

* Från startsidan
* Välj `Groups` link
* Välj `Sports` link
* Välj sport `Groups` link

Endast Baseball-gruppen är synlig.

Logga in som Weston McCall (weston.mccall@dodgit.com / lösenord) och navigera till samma plats. Observera att Weston kan `Join` öppna `Baseball` grupp och antingen `enter or Leave` private `Gymnastics` grupp.

![grouplink3](assets/grouplink3.png)

### Länk till webbsida {#web-page-link}

Visa den grundläggande webbsidan som finns på webbplatsen genom att välja länken Webbsida. Standardverktygen AEM kan användas för att lägga till innehåll på den här sidan i författarmiljön.

Till exempel, gå till **författare** -instans, öppna `engage` i [Konsolen Webbplatser i Communities](/help/communities/sites-console.md)väljer du **Öppna webbplats** om du vill öppna redigeringsläget. Välj sedan förhandsvisningsläget så att du kan välja `Web Page` och välj sedan redigeringsläge för att lägga till titel- och textkomponenter. Publicera sedan om antingen bara sidan eller hela webbplatsen.

![webpagelink](assets/webpagelink.png)

### Modereringslänk {#moderationlink}

När communitymedlemmen har modereringsbehörighet visas länken Moderering. Om du väljer länken visas det communityinnehåll som är publicerat och det kan [modererad](/help/communities/moderate-ugc.md) på ett sätt som liknar [modereringskonsol](/help/communities/moderation.md) i redigeringsmiljön.

Använd webbläsarens bakåtknapp för att gå tillbaka till den publicerade webbplatsen. De flesta konsoler är inte tillgängliga via global navigering i publiceringsmiljön.

![moderationlink](assets/moderationlink.png)

## Självregistrering {#self-registration}

När du har loggat ut kan du skapa en användarregistrering.

* Välj `Log In`
* Välj `Sign up for a new account`

![registrering](assets/registration.png)

![registrering](assets/signup.png)

Som standard är e-postadressen inloggnings-ID. Om alternativet inte är markerat kan besökaren ange ett eget inloggnings-ID (användarnamn). Användarnamnet måste vara unikt i publiceringsmiljön.

När du har angett användarens namn, e-postadress och lösenord väljer du `Sign Up` skapar användaren och aktiverar den för signering.

När du har loggat in visas den första sidan som `Profile` sida, som de kan personalisera.

![profil](assets/profile.png)

Om medlemmen glömmer sitt inloggnings-ID är det möjligt att återställa med sin e-postadress.

![forgotusername](assets/forgotusername.png)
