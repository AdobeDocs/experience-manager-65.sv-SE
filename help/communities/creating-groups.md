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
source-git-commit: 6337a57ea12f1e026f6c754a083307ce018a1c13
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# Community Groups {#community-groups}

Funktionen för communitygrupper är möjligheten för en undercommunity att skapas dynamiskt på en community-webbplats av behöriga användare (community-medlemmar och författare) från publicerings- och författarmiljöerna.

Den här möjligheten finns när [gruppfunktionen](/help/communities/functions.md#groups-function) finns i [community-strukturen](/help/communities/sites-console.md).

En [community-gruppmall](/help/communities/tools-groups.md) innehåller designen för communitygruppssidan när en community-grupp skapas dynamiskt.

En eller flera gruppmallar väljs för gruppfunktionen när funktionen läggs till i en community-webbplatsstruktur eller i en community-webbplatsmall. Den här listan över gruppmallar visas för den medlem eller författare som dynamiskt skapar en ny grupp på communitywebbplatsen.

## Skapar en ny grupp {#creating-a-new-group}

Möjligheten att skapa en ny community-grupp är beroende av att det finns en community-webbplats som innehåller gruppfunktionen, till exempel en som skapats med [Reference Site Template](/help/communities/sites.md).

Exemplen som följer använder den communitywebbplats som skapats från `Reference Site Template` enligt beskrivningen i [Komma igång med AEM Communities](/help/communities/getting-started.md)-självstudiekursen.

Det här är sidan som läses in vid publicering när menyobjektet **Grupper** är markerat:

![new-group](assets/new-group.png)

När du väljer ikonen **Ny grupp** öppnas en redigeringsdialogruta.

Under fliken **Inställningar** anger du gruppens grundläggande funktioner:

![group-settings](assets/group-settings.png)

* **Gruppnamn**

   Namnet på gruppen som ska visas på communitywebbplatsen.

* **Beskrivning**

   En beskrivning av gruppen som ska visas på communitywebbplatsen.

* **Bjud in**

   En lista med medlemmar som ska bjudas in för att gå med i gruppen. I typsnittssökningen ges förslag på communitymedlemmar som ska bjudas in.

* **Grupp-URL-namn**

   Namnet på gruppsidan som blir en del av URL:en.

* **Öppna grupp**

   Om du väljer `Open Group` innebär det att alla anonyma besökare kan visa innehållet och avmarkerar `Member Only Group`.

* **Endast medlemsgrupp**

   Om du väljer `Member Only Group` innebär det endast att medlemmar i gruppen kan visa innehållet, och avmarkerar `Open Group`.

Under fliken **Mall** kan du
välj i listan över mallar för communitygrupper som angavs när gruppfunktionen inkluderades i communityplatsens struktur eller i en mall för communitywebbplatser.

![group-template](assets/group-template.png)

Under fliken **Bild** kan du överföra en bild som ska visas för gruppen på gruppwebbplatsens gruppsida. Standardformatmallen ändrar bildens storlek till 170 x 90 pixlar.

![group-image](assets/group-image.png)

Genom att klicka på knappen **Skapa grupp** skapas sidorna för gruppen baserat på den valda mallen, och en användargrupp skapas för medlemskap och sidan Grupper uppdateras för att visa den nya undergruppen.

Sidan Grupper med en ny undercommunity med namnet&quot;Focus Group&quot;, som en miniatyrbild överfördes för, ser ut så här (fortfarande inloggad som administratör för en community-grupp):

![gruppsida](assets/group-page.png)

Om du väljer länken `Focus Group` öppnas sidan Fokusgrupp i webbläsaren, som har ett ursprungligt utseende baserat på den valda mallen, och som innehåller en undermeny under den huvudsakliga communityplatsens meny:

![open-group-page](assets/open-group-page.png)

### Medlemsländlistkomponent för community-grupper {#community-group-member-list-component}

Komponenten `Community Group Member List` är avsedd för utvecklare av gruppmallar.

### Ytterligare information {#additional-information}

Mer information finns på sidan [Community Group Essentials](/help/communities/essentials-groups.md) för utvecklare.

Mer information om communitygrupper finns på [Hantera användare och användargrupper](/help/communities/users.md).
