---
title: Konfigurera användare och användargrupper
description: Följ den här sidan om du vill veta mer om användarroller och hur du konfigurerar användare och grupper för att stödja redigering och hantering av dina mobilappar.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 9f814204-8cd4-4ba9-9e25-3ff1b25c1955
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 1%

---

# Konfigurera dina användare och användargrupper {#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

I det här kapitlet beskrivs användarrollerna och hur du konfigurerar användare och grupper för att ge stöd åt utveckling och hantering av dina mobilappar.

## AEM Mobile Application Users and Group Administration {#aem-mobile-application-users-and-group-administration}

Följande två grupper är tillgängliga för att du ska kunna ordna och hantera behörighetsmodellen för AEM program:

* appadministratörer för appadministratörer
* appförfattare för appförfattare

### AEM Mobile Application Content Authors (app-author group) {#aem-mobile-application-content-authors-app-author-group}

Medlemmar i gruppen app-author ansvarar för att skapa AEM innehåll för mobilappar som sidor, text, bilder och videor.

#### Gruppkonfiguration - programförfattare {#group-configuration-app-authors}

1. Skapa en användargrupp med namnet&quot;app-authors&quot;:

   Navigera till Admin Console: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   I användargruppkonsolen väljer du plusknappen (+) för att skapa en grupp.

   Ange ID:t för den här gruppen som&quot;app-authors&quot; för att ange att det är en specifik typ av författaranvändargrupp som är specifik för utveckling av mobilprogram i AEM.

1. Lägg till medlem i grupp: Författare

   ![chlimage_1-18](assets/chlimage_1-18.png)

   Lägg till appförfattare i gruppen Författare

1. Nu när du har skapat användargruppen app-authors kan du lägga till enskilda teammedlemmar i den nya gruppen via [Admin Console](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-19](assets/chlimage_1-19.png)

   Redigera användargrupper

1. Navigera till [Behörighetskonsolen](http://localhost:4502/useradmin) och lägg till behörigheter för att administrera molntjänster

   * (Läs) på /etc/cloudServices

   >[!NOTE]
   >
   >Programförfattare utökar standardgruppen för innehållsförfattare (författare) från AEM, så att de ärver möjligheten att skapa innehåll under /content/phonegap

### AEM Mobile Application Administrators Group (app-admins group) {#aem-mobile-application-administrators-group-app-admins-group}

Medlemmar i gruppen app-admins kan skapa programinnehåll med samma behörigheter som finns i appförfattarna **AND** och dessutom ansvarar de för:

* Konfigurera molntjänster för PhoneGap Build och Adobe Mobile Services i AEM
* Mellanlagring, publicering och rensning av uppdateringar av innehållssynkronisering, OTA

>[!NOTE]
>
>Behörigheter avgör tillgängligheten för vissa användaråtgärder i AEM App Command Center.
>
>Observera att vissa alternativ inte är tillgängliga för appförfattare som är tillgängliga för appadministratörer.

#### Gruppkonfiguration - programadministratörer {#group-configuration-app-admins}

1. Skapa en grupp som kallas appadministratörer.
1. Lägg till följande grupper i den nya gruppen för programadministratörer:

   * innehållsförfattare
   * arbetsflöde-användare

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. Navigera till [Behörighetskonsolen](http://localhost:4502/useradmin) och lägg till behörigheter för att administrera molntjänster

   * (Läs, Ändra, Skapa, Ta bort, Replikera) på /etc/cloudServices/mobiltjänster
   * (Läs, Ändra, Skapa, Ta bort, Replikera) på /etc/cloudservices/phonegap-build

1. På samma behörighetskonsol lägger du till behörigheter på scenen, publicerar och rensar appinnehållsuppdateringar

   * (Läs, Ändra, Skapa, Ta bort, Replikera) på /etc/packages/mobileapp
   * (Läs) på /var/contentsync

   >[!NOTE]
   >
   >Paketreplikering används för att publicera appuppdateringar från författarinstansen till publiceringsinstansen

   >[!CAUTION]
   >
   >/var/contentsync åtkomst nekas.
   >
   >Om du utelämnar läsbehörigheten kan tomma uppdateringspaket skapas och replikeras.

1. Lägg till medlemmar i den här gruppen efter behov

## Behörigheter för paneler {#dashboard-tile-permissions}

Instrumentpaneler kan visa olika åtgärder baserat på de behörigheter som användaren har. Nedan beskrivs vilka åtgärder som är tillgängliga för varje platta.

Förutom dessa behörigheter kan en åtgärd också visas/döljas baserat på hur det aktuella programmet är konfigurerat. Det finns till exempel ingen punkt som visar åtgärden &#39;Remote Build&#39; om en PhoneGap-molnkonfiguration inte har tilldelats programmet. Dessa listas nedan under **Konfigurationsvillkor**.

### Hantera apppanel {#manage-app-tile}

Panelen har för närvarande inga åtgärder som kräver behörigheter, men informationssidan för programmet har följande åtgärder:

* *Redigera* för app-author och app-admin (UI Trigger - jcr:write - on /content/phonegap/{suffix})
* *Hämta* för appförfattare och app-admin (UI-utlösare - på /content/phonegap/{suffix})

Bilden nedan visar hämtnings- och redigeringsalternativen för ett program:

![chlimage_1-21](assets/chlimage_1-21.png)
