---
title: Upplev den publicerade webbplatsen
description: Lär dig hur du bläddrar till den URL som visas när du skapar en plats, men på publiceringsservern.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: ebc4e1e7-34f0-4f4e-9f00-178dfda23ce4
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 0%

---

# Upplev den publicerade webbplatsen {#experience-the-published-site}

## Bläddra till Ny webbplats i Publish {#browse-to-new-site-on-publish}

Nu när den nyligen skapade communitywebbplatsen har publicerats bläddrar du till den URL som visas när du skapar webbplatsen, men på publiceringsservern, till exempel:

* Författar-URL = https://localhost:4502/content/sites/engage/en.html
* PUBLISH URL = https://localhost:4503/content/sites/engage/en.html

För att minimera förvirring om vilken medlem som är inloggad på författare och publicera bör du använda olika webbläsare för varje instans.

Vid första ankomsten till den publicerade webbplatsen är besökaren vanligtvis inte inloggad och anonym.

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![författarePublicerad](assets/authorpublished.png)

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

En känd begränsning visar communitywebbplatsinnehållet för anonyma besökare via jcr-innehåll och json, även om **Tillåt anonym åtkomst** är inaktiverat för webbplatsens innehåll. Det här beteendet kan dock styras med delningsbegränsningar som en tillfällig lösning.

Följ de här stegen för att skydda communityplatsens innehåll från anonyma användare genom jcr-innehåll och json:

1. I AEM Author, gå till https://: port/editor.html/content/site/sitename.html.

   >[!NOTE]
   >
   >Gå inte till den lokaliserade webbplatsen.

1. Gå till **Sidegenskaper**.

   ![sidegenskaper](assets/page-properties.png)

1. Gå till fliken **Avancerat**.

1. Aktivera **autentiseringskrav**.

   ![webbplatsautentisering](assets/site-authentication.png)

1. Lägg till inloggningssidans sökväg. Till exempel **/innehåll/......../GetStarted**.
1. Publish sidan.

## Betrodd medlem i användargruppen {#trusted-community-member}

Den här upplevelsen förutsätter att [Aaron McDonald](/help/communities/tutorials.md#demo-users) har tilldelats rollerna för [community manager och moderator](/help/communities/create-site.md#roles). Om inte, går du tillbaka till författarmiljön för att [ändra webbplatsinställningarna](/help/communities/sites-console.md#modifying-site-properties) och väljer Aaron McDonald som både community manager och moderator.

I det övre högra hörnet väljer du `Log in` och signerar med användarnamn (aaron.mcdonald@mailinator.com) och lösenord (lösenord). Observera möjligheten att logga in med Twitter- eller Facebook-autentiseringsuppgifter.

![inloggning](assets/login.png)

När du har loggat in som registrerad community-medlem kan du lägga märke till följande menyalternativ för att klicka och utforska din community-webbplats:

* Med alternativet **Profil** kan du visa och redigera din profil.
* Alternativet [Meddelanden](/help/communities/configure-messaging.md) dirigerar dig till avsnittet för direktmeddelanden, där du kan göra följande:

   1. Visa direktmeddelanden som du har tagit emot (Inkorgen), skickat (Skickat) och tagit bort (Papperskorgen).
   1. Skapa nya direktmeddelanden så att du kan skicka till enskilda personer och grupper.

* Alternativet [Meddelanden](/help/communities/notifications.md) dirigerar dig till meddelandeavsnittet, där du kan visa dina intressanta händelser och redigera meddelandeinställningar.
* [Administration](/help/communities/published-site.md#moderationlink) dirigerar dig till AEM Communities modereringssida, om du har modereringsbehörighet.

![adminscreen](assets/adminscreen.png)

Observera att kalendersidan är hemsidan eftersom den valda referenswebbplatsmallen inkluderade kalenderfunktionen först, följt av aktivitetsströmfunktion, forumfunktion osv. Den här strukturen är synlig från konsolen [Platsmall](/help/communities/sites.md#edit-site-template) eller när du ändrar platsegenskaper i författarmiljön:

![platsmall](assets/sitetemplate.png)

>[!NOTE]
>
>Mer information om Communities-komponenter och -funktioner finns på:
>
>* [Webbgruppskomponenter](/help/communities/author-communities.md) (för författare)
>* [Komponent-, funktions- och funktionselement](/help/communities/essentials.md) (för utvecklare)

### Formlänk {#forum-link}

Visa den grundläggande forumfunktionen genom att välja länken Forum.

Medlemmarna kan publicera ett nytt ämne eller följa ett ämne.

Besökarna kan visa inlägg och sortera dem på olika sätt.

![forumlink](assets/forumlink.png)

### Länken Grupper {#groups-link}

Eftersom Aaron är gruppadministratör kan Aron, genom att välja länken Grupper, skapa en community-grupp genom att välja en gruppmall, bild, om gruppen är öppen eller hemlig samt bjuda in medlemmar.

Detta är ett exempel där en grupp skapas i publiceringsmiljön.

Grupper kan också skapas i författarmiljön och hanteras i communitywebbplatsen i författarmiljön ([Community Groups console](/help/communities/groups.md)). Upplevelsen av att [skapa grupper på författaren](/help/communities/nested-groups.md) är nästa i den här självstudiekursen.

![grupplänk](assets/grouplink.png)

Skapa en referensgrupp:

1. Välj **Ny grupp**
1. **Fliken Inställningar**

   * Gruppnamn: `Sports`
   * Beskrivning: `A parent group for various sporting groups`.
   * Grupp-URL-namn: `sports`
   * Välj `Open Group` (tillåt alla community-medlemmar att delta genom att ansluta)

1. **Fliken Mall**

   * Markera `Reference Group` (innehåller en gruppfunktion i strukturen för att tillåta kapslade grupper)

1. Välj **Skapa grupp**

   ![createggroup](assets/creategroup.png)

När en ny grupp har skapats **markerar du den nya sportgruppen** för att skapa två grupper (kapslade) inuti den. Eftersom en platsstruktur inte kan börja med gruppfunktionen måste du välja länken Grupper när du har öppnat gruppen Sport:

![grupplänk1](assets/grouplink1.png)

Den andra uppsättningen länkar, med början från `Blog`, tillhör den markerade gruppen, gruppen `Sports`. Genom att välja länken `Groups` för sport är det möjligt att kapsla två grupper inom gruppen Sport.

Lägg till två `new groups` som exempel.

* En med namnet `Baseball`

   * Ange det som `Open Group` (obligatoriskt medlemskap).
   * Välj `Conversational Group` på fliken Mallar.

* En med namnet `Gymnastics`

   * Ändra inställningen till `Member Only Group` (begränsat medlemskap).
   * Välj `Conversational Group` på fliken Mallar.

**Obs!**

* Det kan vara nödvändigt att uppdatera sidan innan båda grupperna visas.
* Den här mallen innehåller *inte* gruppfunktionen, så det går inte att kapsla in grupper ytterligare.
* På författaren har [gruppkonsolen](/help/communities/groups.md) ett tredje val - ett `Public Group` (valfritt medlemskap).

När båda grupperna har skapats väljer du Baseball-gruppen, en öppen grupp, och lägger märke till dess länkar:

`Discussions` `What's New` `Members`

Gruppens länkar visas under huvudplatsens länkar och ger följande resultat:

![grupplänk2](assets/grouplink2.png)

Vid författare - med administratörsbehörighet går du till konsolen [Communities-grupper](/help/communities/members.md) och lägger till Weston McCall i gruppen `Community Engage Gymnastics <uid> Members`.

Fortsätt publicera, logga ut som Aaron McDonald och visa grupperna i Sports Group som en anonym besökare:

* Från startsidan
* Markera länken `Groups`
* Markera länken `Sports`
* Välj länken `Groups` för sport

Endast Baseball-gruppen är synlig.

Logga in som Weston McCall (weston.mccall@dodgit.com / lösenord) och navigera till samma plats. Observera att Weston kan `Join` den öppna `Baseball`-gruppen och antingen `enter or Leave` den privata `Gymnastics`-gruppen.

![grupplänk3](assets/grouplink3.png)

### Länk till webbsida {#web-page-link}

Visa den grundläggande webbsidan som finns på webbplatsen genom att välja länken Webbsida. Standardverktygen AEM kan användas för att lägga till innehåll på den här sidan i författarmiljön.

Gå till exempel till instansen **author** , öppna mappen `engage` i konsolen [Webbplatser](/help/communities/sites-console.md) och välj ikonen **Öppna webbplats** för att öppna redigeringsläget. Välj sedan förhandsgranskningsläget så att du kan markera länken `Web Page` och sedan redigera läge för att lägga till titel- och textkomponenter. Publicera sedan om antingen bara sidan eller hela webbplatsen.

![webpagelink](assets/webpagelink.png)

### Modereringslänk {#moderationlink}

När communitymedlemmen har modereringsbehörighet visas länken Moderering. Om du väljer länken visas det communityinnehåll som är publicerat och det kan [modereras](/help/communities/moderate-ugc.md) på ett sätt som liknar [moderationskonsolen](/help/communities/moderation.md) i författarmiljön.

Använd webbläsarens bakåtknapp för att gå tillbaka till den publicerade webbplatsen. De flesta konsoler är inte tillgängliga via global navigering i publiceringsmiljön.

![moderationlink](assets/moderationlink.png)

## Självregistrering {#self-registration}

När du har loggat ut kan du skapa en användarregistrering.

* Välj `Log In`
* Välj `Sign up for a new account`

![registrering](assets/registration.png)

![registrering](assets/signup.png)

Som standard är e-postadressen inloggnings-ID. Om alternativet inte är markerat kan besökaren ange ett eget inloggnings-ID (användarnamn). Användarnamnet måste vara unikt i publiceringsmiljön.

När du har angett användarens namn, e-postadress och lösenord skapas användaren och de kan signeras om du väljer `Sign Up`.

När du har loggat in visas den första sidan på deras `Profile`-sida, som de kan anpassa.

![profil](assets/profile.png)

Om medlemmen glömmer sitt inloggnings-ID är det möjligt att återställa med sin e-postadress.

![forgotusername](assets/forgotusername.png)
