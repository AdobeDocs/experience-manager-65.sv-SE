---
title: Konfigurera dina användare och användargrupper
description: Följ den här sidan om du vill veta mer om användarroller och hur du konfigurerar användare och grupper så att de kan hantera redigering och hantering av appen för on-demand-tjänster.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
exl-id: 58b7d1b9-a851-442a-9d02-212cad8abbed
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# Konfigurera dina användare och användargrupper {#configure-your-users-and-user-groups}

{{ue-over-mobile}}

I det här kapitlet beskrivs användarrollerna och hur du konfigurerar användare och grupper för att ge stöd åt utveckling och hantering av dina mobilappar.

## AEM Mobile Application Users and Group Administration {#aem-mobile-application-users-and-group-administration}

### AEM Mobile Application Content Authors (app-author group) {#aem-mobile-application-content-authors-app-author-group}

Medlemmar i gruppen app-author ansvarar för att skapa AEM innehåll för mobilappar som sidor, text, bilder och videor.

#### Gruppkonfiguration - programförfattare {#group-configuration-app-authors}

1. Skapa en användargrupp med namnet&quot;app-authors&quot;:

   Navigera till Admin Console: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   I användargruppkonsolen väljer du plusknappen (+) för att skapa en grupp.

   Ange ID:t för den här gruppen som&quot;app-authors&quot; för att ange att det är en specifik typ av författaranvändargrupp som är specifik för utveckling av mobilprogram i AEM.

1. Lägg till medlem i grupp: Författare

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Nu när du har skapat användargruppen app-authors kan du lägga till enskilda teammedlemmar i den nya gruppen via [Admin Console](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. Med följande kan du lägga till i AEM innehållsförfattargrupp:

   (Läs) den

   * /app
   * /etc/clientlibs
   * /etc/designs
   * /etc/cloudservices/dps2015

### AEM Mobile Application Administrators Group (app-admins group) {#aem-mobile-application-administrators-group-app-admins-group}

Medlemmar i gruppen app-admins kan skapa programinnehåll med samma behörigheter som finns i appförfattarna **AND** och dessutom ansvarar de för:

* Förproduktion, publicering och rensning av programuppdateringar för ContentSync OTA

>[!NOTE]
>
>Behörigheter avgör tillgängligheten för vissa användaråtgärder i AEM App Command Center.
>
>Observera att vissa alternativ inte är tillgängliga för appförfattare som är tillgängliga för appadministratörer.

### Gruppkonfiguration - programadministratörer {#group-configuration-app-admins}

1. Skapa en grupp som kallas appadministratörer.
1. Lägg till följande grupper i den nya gruppen för programadministratörer:

   * innehållsförfattare
   * arbetsflöde-användare

   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >arbetsflödesanvändare krävs för att fjärrbygga med PhoneGap Build-tjänsten

1. Navigera till [Behörighetskonsolen](http://localhost:4502/useradmin) och lägg till behörigheter för att administrera molntjänster

   * (Läs, Ändra, Skapa, Ta bort, Replikera) på /etc/cloudServices/mobiltjänster

1. På samma behörighetskonsol lägger du till behörigheter på scenen, publicera och rensa innehållsuppdateringar för appar.

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
1. Exportera innehåll eller överföra

   * (Läs) på /etc/contentsync för att komma åt exportmallar
   * (Läs) på /var to path traversal on read
   * (Läs, skriv, ändra, ta bort) på /var/contentsync för att skriva, läsa och rensa cachelagrat ContentSync-exportinnehåll

### Ytterligare resurser {#additional-resources}

Mer information om de två andra rollerna och ansvarsområdena för att skapa en AEM Mobile On-demand Services-app finns i följande resurser:

* [Utveckla AEM för AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [AEM innehåll för AEM Mobile On-demand Services App](/help/mobile/mobile-apps-ondemand.md)
