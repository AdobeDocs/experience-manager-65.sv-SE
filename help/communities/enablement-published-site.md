---
title: Upplev den publicerade webbplatsen
seo-title: Experience the Published Site
description: Bläddra till en publicerad webbplats för aktivering
seo-description: Browse to a published site for enablement
uuid: 1bfefa8a-fd9c-4ca8-b2ff-add79776c8ae
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 26715b94-e2ea-4da7-a0e2-3e5a367ac1cd
exl-id: 801416ed-d321-45a2-8032-8935094a4d44
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 1%

---

# Upplev den publicerade webbplatsen {#experience-the-published-site}


**[⇐ Skapa och tilldela aktiveringsresurser](resource.md)**

## Bläddra till Ny webbplats vid publicering {#browse-to-new-site-on-publish}

Nu när den nyligen skapade communitysajten och dess aktiveringsresurser och utbildningsväg har publicerats är det möjligt att se webbplatsen för självstudiekursen om aktivering.

Börja med att bläddra till den URL som visas när du skapar webbplatsen, men på publiceringsservern, t.ex.

* Författar-URL = [http://localhost:4502/content/sites/enable/en.html](http://localhost:4502/content/sites/enable/en.html)
* Publicera URL = [http://localhost:4503/content/sites/enable/en.html](http://localhost:4503/content/sites/enable/en.html)

Om [standardstartsida har angetts](enablement-create-site.md#changethedefaulthomepage)och sedan bara gå till [http://localhost:4503/](http://localhost:4503/) bör starta webbplatsen.

Vid första ankomsten till den publicerade webbplatsen är besökaren vanligtvis inte redan inloggad och anonym.

**http://localhost:4503/content/sites/enable/en.html**

![enablement-login](assets/enablement-login.png)

## Anonym webbplatsbesökare {#anonymous-site-visitor}

En anonym besökare visas omedelbart på inloggningssidan för den här privata aktiveringscommunityn. Observera att det inte finns något alternativ för självregistrering eller inloggning med Facebook eller Twitter.

Observera att den här startsidan innehåller fyra menyalternativ: `Assignments, Ski Catalog, What's New` och `Discussions`, men ingen kan nås utan att logga in.

>[!NOTE]
>
>Det går att ge anonym åtkomst till en aktiveringswebbplats utan att tillåta besökare att registrera sig själva.
>
>Om en aktiveringsresurs är inställd på `show in catalog` och `allow anonymous access`kan anonyma besökare visa resurser i katalogen.

### Förhindra anonym åtkomst på JCR {#prevent-anonymous-access-on-jcr}

En känd begränsning exponerar communityinnehållet för anonyma besökare via jcr-innehåll och json, även om **[!UICONTROL allow anonymous access]** är inaktiverat för webbplatsens innehåll. Det här beteendet kan dock styras med delningsbegränsningar som en tillfällig lösning.

Följ de här stegen för att skydda communityplatsens innehåll från anonyma användare genom jcr-innehåll och json:

1. AEM författarinstansen går till https://&lt;host>:&lt;port>/editor.html/content/site/&lt;sitename>.html.

   >[!NOTE]
   >
   >Gå inte till den lokaliserade webbplatsen.

1. Gå till **[!UICONTROL Page Properties]**.

   ![page-properties](assets/page-properties.png)

1. Gå till **[!UICONTROL Advanced]** -fliken.
1. Aktivera **[!UICONTROL Authentication Requirement]**.

   ![webbplatsautentisering](assets/site-authentication.png)

1. Lägg till inloggningssidans sökväg. Till exempel, `/content/......./GetStarted`.
1. Publicera sidan.

## Registrerad medlem {#enrolled-member}

Den här upplevelsen är beroende av användare `Riley Taylor` och `Sidney Croft` att [skapad](enablement-setup.md#publishcreateenablementmembers) och [tilldelad](resource.md#settings) till *Ski-lektioner* utbildningsväg genom sitt medlemskap i *Klassen Community Ski* grupp.

Logga in med

* `Username: riley`
* `Password: password`

Om användarprofilen inte skapades genom självregistrering visas profilsidan den första gången en medlem loggar in, så att de kan verifiera och ändra den om det behövs.

Nästa gång medlemmen loggar in visas startsidan, som identifieras av det första menyalternativet.

![registrerad medlem](assets/enrolled-member.png)

### Uppdrag {#assignments}

På uppdragssidan visas alla utbildningsvägar och aktiveringsresurser som är specifikt tilldelade till medlemmarna.

Varje uppdrag innehåller grundläggande information om:

* Tilldelningstypen
* Om det är ett nytt uppdrag
* Namnet
* Information som är relevant för uppdragstypen
* Uppdragskontakt, expert och författare (om sådan finns)

Tilldelningstypen anges med en ikon i kortets övre vänstra hörn. Bilden av en väg är för en inlärningsväg med antalet medföljande aktiveringsresurser.

![assignment1](assets/assignment1.png)

Markera *Ski-lektioner* visar de två aktiveringsresurserna som utbildningsvägen refererar till.

![assignment2](assets/assignment2.png)

Markera *Ski Lesson 1* öppnar informationssidan för aktiveringsresursen.

På informationssidan kan medlemmarna lära sig [ränta](rating.md) lektionen och lägga till [kommentarer](comments.md). Alla medlemsaktiviteter återspeglas i avsnittet Nyheter på webbplatsen.

Interaktion med aktiveringsresursen beskrivs i rapportavsnittet som är tillgängligt i författarmiljön.

![assignment3](assets/assignment3.png)

### Ski-katalog {#ski-catalog}

Ski Catalog-sidan är katalogen med aktiveringsresurser som taggats med taggar från `Tutorial` namnutrymme. De två *Ski Lesson* resurser är taggade med `Skiing` -taggen, så att om någon annan tagg än `All` eller `Tutorial: Sports / Skiing` är markerat visas ingenting.

När en medlem inte har tilldelats aktiveringsresurser, antingen direkt eller via en utbildningsväg, är det möjligt att interagera med aktiveringsresurser som finns i en katalog och ge feedback via kommentarer och omdömen.

![skidkatalog](assets/ski-catalog.png)

### Diskussioner {#discussions}

Förutom att betygsätta och kommentera aktiveringsresurser ([när aktiverat](enablement-create-site.md#step33asettings)), som communitywebbplatsmallen från vilken `Enablement Tutorial` skapades med [forumfunktion](functions.md#forum-function) (title is `Discussions)`.

Välj `Discussions`för att länka och publicera ett ämne.

Logga ut och logga in som Sidney Croft (sidney/lösenord) och svara på frågan samt Följ ämnet.

Observera, förutom intern moderering, att det finns alternativ för att dela ämnet i sociala medier eller för att skicka ämnet via e-post.

![diskussioner](assets/discussions.png)

### Nyheter {#what-s-new}

The `What's New` menyalternativet är den rubrik som ges [aktivitetsströmfunktion](functions.md#activity-stream-function) i den här communitywebbplatsens struktur.

Fortfarande inloggad som Sidney, välj `What's New` för att visa aktiviteten.

![whats-new-menu](assets/whats-new-menu.png)

## Betrodd medlem i användargruppen {#trusted-community-member}

Den här upplevelsen förutsätter ` [Quinn Harper](enablement-setup.md#publishcreateenablementmembers)` tilldelades rollerna för [moderator](enablement-create-site.md#moderation) och [resurskontakt](resource.md#settings).

Logga in med

* `Username: quinn`
* `Password: password`

Observera att det finns ett nytt menyalternativ när du har loggat in. `Administration`, vilket visas för att medlemmen fick rollen som moderator.

![tillförlitlig-medlemshemsida](assets/trusted-member-homepage.png)

Hemsidan identifieras av det första menyalternativet, Uppdrag. Quinn är moderator- och aktiveringsresurskontakt och är inte registrerad i några aktiveringsresurser eller utbildningsvägar, så det finns inget att visa.

### Administration {#administration}

Vad som finns, är de två elevernas aktivitet, `Riley Taylor` och `Sidney Croft`. Genom att välja `Administration` för att komma åt modereringskonsolen kan Quinn använda [masmodereringskonsol](moderation.md) till att moderera sina inlägg.

Om du väljer ikonen för sidpanelen växlar du de filter som används för att söka efter innehåll i communityn.

När du hovrar över ett kommentarskort visas modereringsåtgärder.

![administration](assets/administration.png)

## Rapporter om författare {#reports-on-author}

Det finns två sätt att få åtkomst till rapporter om studerande och aktiveringsresurser.

Navigera till **Communities, [Resurskonsol](resources.md)**, där aktiveringsresurserna hanteras och efter att du har valt en communitywebbplats är det möjligt att generera rapporter för

* Alla aktiveringsresurser och utbildningsvägar
* En specifik aktiveringsresurs eller utbildningsväg

Navigera till **Communities, [Rapportkonsol](reports.md)** och generera rapporter enligt:

* Tilldelningar för aktiveringsresurser och utbildningsvägar
* Publicerar på en communitywebbplats under en viss period
* Vyer (besök på plats) av en communitywebbplats under en viss period

* Inlägg och vyer kan gälla allt innehåll eller specifikt innehåll:

   * Forum
   * Forum
   * QnA
   * QnA-fråga
   * Blogg
   * Bloggartikel
   * Kalender
   * Kalenderhändelse

### Resurskonsol {#resources-console}

Med lite aktivitet och interaktion med resurserna när de publiceras är det värt att titta närmare på rapporterna om författaren.

* Logga in med administratörsbehörighet på författaren.
* Navigera från huvudmenyn till **[!UICONTROL Communities]** > **[!UICONTROL Resources]**.
* Välj `Enablement Tutorial` webbplats.
* Välj `Report` om du vill se en sammanfattning av alla resurser.
* Välj en resurs och sedan `Report` -ikon för en rapport om den resursen.

Observera att det troligen är för tidigt att visa data från Adobe Analytics, som kan ta mellan 1 och 12 timmar att visa. Men grundläggande SCORM-rapportering är redan tillgänglig.

#### Resursrapport för SKI-lektioner {#ski-lessons-resource-report}

![skidlektionsrapport](assets/ski-lessons-report.png)

#### Användarrapport för SKI-lektioner {#ski-lessons-user-report}

* Välj **[!UICONTROL Communities > Resources]**

* Open Card `Enablement Tutorial`
* Open Card `Ski Lessons`
* Välj `Report > User Report`

![skidlektioner-användarrapport](assets/ski-lessons-user-report.png)

### Rapportkonsol {#reports-console}

Med rapportkonsolen kan du skapa rapporter på

* **Uppdrag** för alla aktiveringscommunitysajter
* **Vyer** för alla communitysajter
* **Inlägg** för alla communitysajter

För rapporter om tilldelningar:

* Logga in med administratörsbehörighet på författaren.
* Navigera till **[!UICONTROL Communities]** > **[!UICONTROL Reports]** > **[!UICONTROL Assignments Report]**.
* Välj en **[!UICONTROL Site]** i listrutan (välj `Enablement Tutorial`).

* Välj **[!UICONTROL Group]** (välj `Community Ski Class`)

* Välj en **[!UICONTROL Assignment]** (välj `Ski Lessons`)

* Välj **[!UICONTROL Generate]**

![rapporttilldelning](assets/report-assignment.png)

För rapporter om vyer:

* Logga in med administratörsbehörighet på författaren.
* Navigera till **[!UICONTROL Communities]** > **[!UICONTROL Reports]** > **[!UICONTROL Views Report]**.
* Välj en **Plats** i listrutan (välj `Enablement Tutorial`).

* Välj **[!UICONTROL Content Type]** (välj `all`).

* Välj en **[!UICONTROL date range]** (välj `Last 7 days`).

* Välj **[!UICONTROL Generate]**.

![rapportvisningar](assets/report-views.png)

**[⇐ Skapa och tilldela aktiveringsresurser](resource.md)**
