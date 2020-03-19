---
title: Community-grupper
seo-title: Community-grupper
description: Skapa communitygrupper
seo-description: Skapa communitygrupper
uuid: c677d23d-5edb-414c-9013-130c88c2ea52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d94708ee-ca6b-420c-9536-6889d752f9de
docset: aem65
translation-type: tm+mt
source-git-commit: e8d8bf89971d3d9d5ec150308dda247aa53c77bb

---


# Community-grupper {#community-groups}

Funktionen för communitygrupper är möjligheten för en undercommunity att skapas dynamiskt på en community-webbplats av behöriga användare (community-medlemmar och författare) från publicerings- och författarmiljöerna.

Den här möjligheten finns när [gruppfunktionen](/help/communities/functions.md#groups-function) finns i [communitywebbplatsens](/help/communities/sites-console.md) struktur.

En mall [för en](/help/communities/tools-groups.md) community-grupp ger designen för communitygruppssidan när en community-grupp skapas dynamiskt.

En eller flera gruppmallar väljs för gruppfunktionen när funktionen läggs till i en community-webbplatsstruktur eller i en community-webbplatsmall. Den här listan över gruppmallar visas för den medlem eller författare som dynamiskt skapar en ny grupp på communitywebbplatsen.

## Skapa en ny grupp {#creating-a-new-group}

Möjligheten att skapa en ny community-grupp bygger på att det finns en community-webbplats som innehåller gruppfunktionen, till exempel en som skapats från ` [Reference Site Template](/help/communities/sites.md)`.

Exemplen som följer använder den communitywebbplats som skapats från `Reference Site Template` enligt beskrivningen i självstudiekursen [Komma igång med AEM Communities](/help/communities/getting-started.md) .

Det här är sidan som läses in vid publicering när menyalternativet **Grupper** är markerat:

![chlimage_1-85](assets/chlimage_1-85.png)

När du väljer ikonen **Ny grupp** öppnas en redigeringsdialogruta.

Under fliken **Inställningar** kan du ange gruppens grundläggande funktioner:

![chlimage_1-86](assets/chlimage_1-86.png)

* **Gruppnamn**

   Namnet på gruppen som ska visas på communitywebbplatsen.

* **Beskrivning**

   En beskrivning av gruppen som ska visas på communitywebbplatsen.

* **Bjud in**

   En lista med medlemmar som ska bjudas in för att gå med i gruppen. I typsnittssökningen ges förslag på communitymedlemmar som ska bjudas in.

* **Grupp-URL-namn**

   Namnet på gruppsidan som blir en del av URL:en.

* **Öppna grupp**

   Markeringen `Open Group` anger att en anonym besökare kan visa innehållet och kommer att avmarkera `Member Only Group`.

* **Endast medlemsgrupp**

   Om du väljer `Member Only Group` det här alternativet visas endast gruppens medlemmar som kan visa innehållet, och det avmarkeras `Open Group`.

Under fliken **Mall** kan du välja från listan med gruppmallar som angavs när gruppfunktionen inkluderades i communityplatsens struktur eller i en mall för communitywebbplatser.

![chlimage_1-87](assets/chlimage_1-87.png)

Under fliken **Bild** finns möjligheten att överföra en bild som ska visas för gruppen på gruppwebbplatsens gruppsida. Standardformatmallen ändrar bildens storlek till 170 x 90 pixlar.

![chlimage_1-88](assets/chlimage_1-88.png)

Genom att klicka på knappen **Skapa grupp** skapas sidorna för gruppen baserat på den valda mallen, och en användargrupp skapas för medlemskap och sidan Grupper uppdateras för att visa den nya undergruppen.

Sidan Grupper med en ny undercommunity med namnet&quot;Focus Group&quot;, som en miniatyrbild överfördes för, ser ut så här (fortfarande inloggad som administratör för en community-grupp):

![chlimage_1-89](assets/chlimage_1-89.png)

Om du väljer `Focus Group` länken öppnas sidan Fokusgrupp i webbläsaren, som har ett ursprungligt utseende baserat på den valda mallen, och som innehåller en undermeny under den huvudsakliga communitywebbplatsens meny:

![chlimage_1-90](assets/chlimage_1-90.png)

### Medlemslistkomponent för community {#community-group-member-list-component}

Komponenten är avsedd att användas av utvecklare av gruppmallar. `Community Group Member List`

### Additional Information {#additional-information}

Mer information finns på sidan [Community Group Essentials](/help/communities/essentials-groups.md) för utvecklare.

Mer information om communitygrupper finns på [Hantera användare och användargrupper](/help/communities/users.md).
