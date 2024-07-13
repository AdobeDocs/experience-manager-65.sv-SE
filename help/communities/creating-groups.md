---
title: Community-grupper
description: Lär dig hur funktionen för communitygrupper gör att du dynamiskt kan skapa en undercommunity inom en community för behöriga användare i Publish och Author.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: edcda6cb-df47-4afe-8a9a-82d8e386fe05
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---

# Community-grupper {#community-groups}

Funktionen för communitygrupper är möjligheten för en undercommunity att skapas dynamiskt på en community-webbplats av behöriga användare (community-medlemmar och författare) från publicerings- och författarmiljöerna.

Den här möjligheten finns när [gruppfunktionen](/help/communities/functions.md#groups-function) finns i [communitywebbplatsens](/help/communities/sites-console.md) struktur.

En [community-gruppmall](/help/communities/tools-groups.md) innehåller designen för community-gruppsidan när en community-grupp skapas dynamiskt.

En eller flera gruppmallar väljs för gruppfunktionen när funktionen läggs till i en community-webbplatsstruktur eller i en community-webbplatsmall. Den här listan över gruppmallar visas för den medlem eller författare som dynamiskt skapar en grupp på communitywebbplatsen.

## Skapa en ny grupp {#creating-a-new-group}

Möjligheten att skapa en community-grupp är beroende av att det finns en community-webbplats som innehåller gruppfunktionen, till exempel en som har skapats från [referenswebbplatsmallen](/help/communities/sites.md).

Exemplen som följer använder den communitywebbplats som skapats från `Reference Site Template` enligt beskrivningen i självstudiekursen [Komma igång med AEM Communities](/help/communities/getting-started.md).

Det här är sidan som läses in vid publicering när menyobjektet **Grupper** har valts:

![ny grupp](assets/new-group.png)

När du väljer ikonen **Ny grupp** öppnas en redigeringsdialogruta.

Under fliken **Inställningar** anger du grundläggande funktioner för gruppen:

![group-settings](assets/group-settings.png)

* **Gruppnamn**

  Namnet på gruppen som du vill visa på communitywebbplatsen. Undvik att använda understreck (_) och nyckelord som resurser och konfiguration i gruppnamnet.

* **Beskrivning**

  En beskrivning av gruppen som ska visas på communitywebbplatsen.

* **Bjud in**

  En lista med medlemmar som ska bjudas in till gruppen. I typsnittssökningen ges förslag på communitymedlemmar som ska bjudas in.

* **Gruppens URL-namn**

  Namnet på gruppsidan som blir en del av URL:en.

* **Öppna grupp**

  Om du väljer `Open Group` kan alla anonyma besökare visa innehållet och `Member Only Group` avmarkeras.

* **Endast medlem, grupp**

  Om du väljer `Member Only Group` innebär det att bara medlemmar i gruppen kan visa innehållet, och `Open Group` avmarkeras.

Under fliken **Mall** kan du välja från listan med mallar för communitygrupper. Dessa mallar angavs när gruppfunktionen inkluderades i communityplatsens struktur eller i en mall för communityplats.

![group-template](assets/group-template.png)

Under fliken **Bild** kan du överföra en bild som ska visas för gruppen på gruppwebbplatsens gruppsida. Standardformatmallen ändrar bildens storlek till 170 x 90 pixlar.

![group-image](assets/group-image.png)

Genom att välja **Skapa grupp** skapas sidorna för gruppen baserat på den valda mallen, och en användargrupp skapas för medlemskap och sidan Grupper uppdateras för att visa den nya undergruppen.

Sidan Grupper med en ny undercommunity med namnet&quot;Focus Group&quot;, som en miniatyrbild överfördes för, ser ut så här (fortfarande inloggad som administratör för en community-grupp):

![gruppsida](assets/group-page.png)

Om du väljer länken `Focus Group` öppnas sidan Fokusgrupp i webbläsaren, som har ett ursprungligt utseende baserat på den valda mallen, och som innehåller en undermeny under den huvudsakliga communitywebbplatsens meny:

![open-group-page](assets/open-group-page.png)

### Medlemslistkomponent för community {#community-group-member-list-component}

Komponenten `Community Group Member List` är avsedd för utvecklare av gruppmallar.

### Ytterligare information {#additional-information}

Mer information finns på sidan [Grundläggande om communitygrupper](/help/communities/essentials-groups.md) för utvecklare.

Mer information om communitygrupper finns på [Hantera användare och användargrupper](/help/communities/users.md).
