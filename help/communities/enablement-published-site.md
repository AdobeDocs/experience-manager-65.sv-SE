---
title: Upplev den publicerade webbplatsen
seo-title: Upplev den publicerade webbplatsen
description: Bläddra till en publicerad webbplats för aktivering
seo-description: Bläddra till en publicerad webbplats för aktivering
uuid: 1bfefa8a-fd9c-4ca8-b2ff-add79776c8ae
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 26715b94-e2ea-4da7-a0e2-3e5a367ac1cd
translation-type: tm+mt
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---



# Upplev den publicerade webbplatsen {#experience-the-published-site}


**[⇐ Skapa och tilldela aktiveringsresurser](resource.md)**

## Bläddra till Ny webbplats vid publicering {#browse-to-new-site-on-publish}

Nu när den nyligen skapade communitysajten och dess aktiveringsresurser och utbildningsväg har publicerats är det möjligt att se webbplatsen för självstudiekursen om aktivering.

Börja med att bläddra till den URL som visas när du skapar webbplatsen, men på publiceringsservern, t.ex.

* Författar-URL = [http://localhost:4502/content/sites/enable/en.html](http://localhost:4502/content/sites/enable/en.html)
* Publicera URL = [http://localhost:4503/content/sites/enable/en.html](http://localhost:4503/content/sites/enable/en.html)

Om [standardhemsidan var inställd](enablement-create-site.md#changethedefaulthomepage)startar du webbplatsen genom att bläddra till [http://localhost:4503/](http://localhost:4503/) .

Vid första ankomsten till den publicerade webbplatsen är besökaren vanligtvis inte redan inloggad och anonym.

**http://localhost:4503/content/sites/enable/en.html**

![chlimage_1-433](assets/chlimage_1-433.png)

## Anonym webbplatsbesökare {#anonymous-site-visitor}

En anonym besökare visas omedelbart på inloggningssidan för den här privata aktiveringscommunityn. Observera att det inte finns något alternativ för självregistrering eller inloggning på Facebook eller Twitter.

Observera att den här startsidan innehåller fyra menyalternativ: och `Assignments, Ski Catalog, What's New` `Discussions`men ingen kan nås utan att logga in.

>[!NOTE]
>
>Det går att ge anonym åtkomst till en aktiveringswebbplats utan att tillåta besökare att registrera sig själva.
>Om en aktiveringsresurs är inställd på `show in catalog` och `allow anonymous access`kan anonyma webbplatsbesökare visa resurser i katalogen.

### Förhindra anonym åtkomst på JCR {#prevent-anonymous-access-on-jcr}

En känd begränsning exponerar communityinnehållet för anonyma besökare via jcr-innehåll och json, även om anonym åtkomst **** är inaktiverat för webbplatsens innehåll. Det här beteendet kan dock styras med delningsbegränsningar som en tillfällig lösning.

Följ de här stegen för att skydda communityplatsens innehåll från anonyma användare genom jcr-innehåll och json:

1. På AEM Author-instansen går du till https://&lt;host>:&lt;port>/editor.html/content/site/&lt;sitename>.html.

   >[!NOTE]
   >
   >Gå inte till den lokaliserade webbplatsen.

1. Gå till **[!UICONTROL Sidegenskaper]**.

   ![page-properties-1](assets/page-properties-1.png)

1. Gå till fliken **[!UICONTROL Avancerat]** .
1. Aktivera **[!UICONTROL autentiseringskrav]**.

   ![site-authentication-1](assets/site-authentication-1.png)

1. Lägg till inloggningssidans sökväg. Exempel, `/content/......./GetStarted`.
1. Publicera sidan.

## Registrerad medlem {#enrolled-member}

Den här upplevelsen är beroende av användare `Riley Taylor` och `Sidney Croft` att de [skapas](enablement-setup.md#publishcreateenablementmembers) och [tilldelas](resource.md#settings) till utbildningsvägen för *Ski-lektioner* genom deras medlemskap i gruppen *Community Ski Class* .

Logga in med

* `Username: riley`
* `Password: password`

Om användarprofilen inte skapades genom självregistrering visas profilsidan den första gången en medlem loggar in, så att de kan verifiera och ändra den om det behövs.

Nästa gång medlemmen loggar in visas startsidan, som identifieras av det första menyalternativet.

![chlimage_1-434](assets/chlimage_1-434.png)

### Uppdrag {#assignments}

På uppdragssidan visas alla utbildningsvägar och aktiveringsresurser som är specifikt tilldelade till medlemmarna.

Varje uppdrag innehåller grundläggande information om

* Tilldelningstypen
* Om det är ett nytt uppdrag
* Namnet
* Information som är relevant för uppdragstypen
* Uppdragskontakt, expert och författare (om sådan finns)

Tilldelningstypen anges med en ikon i kortets övre vänstra hörn. Bilden av en väg är för en inlärningsväg med antalet medföljande aktiveringsresurser.

![chlimage_1-435](assets/chlimage_1-435.png)

Om du väljer *Ski-lektioner* visas två aktiveringsresurser som refereras av utbildningssökvägen.

![chlimage_1-436](assets/chlimage_1-436.png)

Om du väljer *Ski Lesson 1* öppnas informationssidan för aktiveringsresursen.

På informationssidan kan medlemmen lära sig mer, [betygsätta](rating.md) lektionen och lägga till [kommentarer](comments.md). Alla medlemsaktiviteter återspeglas i avsnittet Nyheter på webbplatsen.

Interaktion med aktiveringsresursen beskrivs i rapportavsnittet som är tillgängligt i författarmiljön.

![chlimage_1-437](assets/chlimage_1-437.png)

### Ski-katalog {#ski-catalog}

Ski Catalog-sidan är katalogen med aktiveringsresurser som taggats med taggar från `Tutorial` namnutrymmet. De två *Ski Lesson* -resurserna är taggade med `Skiing` -taggen, vilket innebär att om någon annan tagg än `All` eller `Tutorial: Sports / Skiing` är markerad visas ingenting.

När en medlem inte har tilldelats aktiveringsresurser, antingen direkt eller via en utbildningsväg, är det möjligt att interagera med aktiveringsresurser som finns i en katalog och ge feedback via kommentarer och omdömen.

![chlimage_1-438](assets/chlimage_1-438.png)

### Diskussioner {#discussions}

Förutom klassificering och kommentering av aktiveringsresurser ([när de är aktiverade](enablement-create-site.md#step33asettings)) innehåller communityplatsmallen som `Enablement Tutorial` skapades från [forumfunktionen](functions.md#forum-function) (title är `Discussions)`.

Markera `Discussions`länken och lägg upp ett ämne.

Logga ut och logga in som Sidney Croft (sidney/lösenord) och svara på frågan samt Följ ämnet.

Observera, förutom intern moderering, att det finns alternativ för att dela ämnet i sociala medier eller för att skicka ämnet via e-post.

![chlimage_1-439](assets/chlimage_1-439.png)

### Nyheter {#what-s-new}

Menyalternativet är den titel som anges av `What's New` aktivitetsströmsfunktionen [](functions.md#activity-stream-function) i den här communityplatsens struktur.

Du är fortfarande inloggad som Sidney och väljer länken för `What's New` att visa aktiviteten.

![chlimage_1-440](assets/chlimage_1-440.png)

## Betrodd medlem i användargruppen {#trusted-community-member}

Detta förutsätter att rollerna för ` [Quinn Harper](enablement-setup.md#publishcreateenablementmembers)` moderatorn [och](enablement-create-site.md#moderation) resurskontakten [](resource.md#settings)har tilldelats.

Logga in med

* `Username: quinn`
* `Password: password`

När du har loggat in finns det ett nytt menyalternativ, `Administration`som visas eftersom medlemmen fick rollen som moderator.

![chlimage_1-441](assets/chlimage_1-441.png)

Hemsidan identifieras av det första menyalternativet, Uppdrag. Quinn är moderator- och aktiveringsresurskontakt och är inte registrerad i några aktiveringsresurser eller utbildningsvägar, så det finns inget att visa.

### Administration {#administration}

Vad det finns, är aktivitet av de två eleverna `Riley Taylor` och `Sidney Croft`. Genom att klicka på `Administration` länken för att komma åt modereringskonsolen kan Quinn använda konsolen [för](moderation.md) moderering av flera objekt för att moderera sina inlägg.

Om du väljer ikonen för sidpanelen växlar du de filter som används för att söka efter innehåll i communityn.

När du hovrar över ett kommentarskort visas modereringsåtgärder.

![chlimage_1-442](assets/chlimage_1-442.png)

## Rapporter om författare {#reports-on-author}

Det finns två sätt att få åtkomst till rapporter om studerande och aktiveringsresurser.

Navigera till **Communities,[Resources console](resources.md)**, där aktiveringsresurserna hanteras, och när du har valt en community-webbplats kan du generera rapporter för

* Alla aktiveringsresurser och utbildningsvägar
* En specifik aktiveringsresurs eller utbildningsväg

Navigera till **Communities,[Reports console](reports.md)**och generera rapporter enligt

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

* On author
* Logga in med administratörsbehörighet
* Navigera från huvudmenyn till **[!UICONTROL Communities > Resources]**
* Markera `Enablement Tutorial` platsen
* Välj `Report` ikonen om du vill se en sammanfattning av alla resurser
* Välj en resurs och sedan `Report` ikonen för en rapport om resursen

Observera att det troligen är för tidigt att visa data från Adobe Analytics, som kan ta mellan 1 och 12 timmar att visa. Men grundläggande SCORM-rapportering är redan tillgänglig.

#### Resursrapport för SKI-lektioner {#ski-lessons-resource-report}

![chlimage_1-443](assets/chlimage_1-443.png)

#### Användarrapport för SKI-lektioner {#ski-lessons-user-report}

* Välj **[!UICONTROL Communities > Resources]**

* Open Card `Enablement Tutorial`
* Open Card `Ski Lessons`
* Välj `Report > User Report`

![chlimage_1-444](assets/chlimage_1-444.png)

### Rapportkonsol {#reports-console}

Med rapportkonsolen kan du skapa rapporter på

* **Uppdrag** för alla aktiveringscommunitysajter
* **Vyer** för alla communitysajter
* **Poster** för alla communitysajter

För rapporter om tilldelningar:

* On author
* Logga in med administratörsbehörighet
* Navigera till **[!UICONTROL Communities > Reports > Assignments Report]**
* Välj en **[!UICONTROL plats]** i listrutan (välj `Enablement Tutorial`)

* Markera **[!UICONTROL grupp]** (välj `Community Ski Class`)

* Markera ett **[!UICONTROL uppdrag]** (välj `Ski Lessons`)

* Välj **[!UICONTROL Generera]**

![chlimage_1-445](assets/chlimage_1-445.png)

För rapporter om vyer:

* On author
* Logga in med administratörsbehörighet
* Navigera till **[!UICONTROL Communities > Reports > Views Report]**
* Välj en **plats **i listrutan (välj`Enablement Tutorial`)

* Välj **[!UICONTROL innehållstyp]** (välj `all`)

* Välj ett **[!UICONTROL datumintervall]** (välj `Last 7 days`)

* Välj **[!UICONTROL Generera]**

![chlimage_1-446](assets/chlimage_1-446.png)

**[⇐ Skapa och tilldela aktiveringsresurser](resource.md)**
