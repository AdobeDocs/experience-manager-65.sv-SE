---
title: AEM Mobile SetUp
seo-title: AEM Mobile SetUp
description: Följ den här sidan för att konfigurera AEM Mobile och på så sätt låta användaren skapa och hantera innehållet i AEM. Den här sidan innehåller information om hur du integrerar den AEM instansen med det molnbaserade AEM Mobile On-demand Services-kontot och -projekten.
seo-description: Follow this page for setting up AEM Mobile and thus allowing the user to create and manage the content within AEM. This page provides information on integrating the AEM instance with the cloud-based AEM Mobile On-Demand Services account and project(s).
uuid: 03bf5b56-7750-4f76-b079-43761367655a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: 393cf504-917e-4bf6-9a8b-b7a5bd862c65
exl-id: 0ead982d-2315-4947-b762-596aa2aa42a1
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 0%

---

# AEM Mobile SetUp{#aem-mobile-setup}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>Befintliga AEM Mobile-appskunder som migrerar från AEM 6.2 eller 6.3 till AEM 6.5 kan fortsätta använda AEM Mobile-appar genom att hämta ett paket från PackageShare. Nya installationer av AEM 6.5 stöder dock inte AEM Mobile Apps-funktioner.

För att kunna använda AEM för att producera innehåll för AEM Mobile-program måste du integrera den AEM instansen med det molnbaserade AEM Mobile On-demand Services-kontot och -projekten.

Följ de här stegen för att konfigurera AEM Mobile och på så sätt låta användaren skapa och hantera innehållet i AEM.

## AEM Mobile Provisioning {#aem-mobile-provisioning}

För att komma igång med AEM Mobile måste du:

* **Begär en API-nyckel**: Om du vill få åtkomst till API:t för On-Demand Services måste du begära en API-nyckel. Om du vill begära API-nyckeln fyller du i [PDF form](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html). Skicka det ifyllda formuläret till Adobe Developer Support: [wwds@adobe.com](mailto:wwds@adobe.com)

* **Generera enhets-ID och enhetstoken**: När du har fått din API-nyckel kan du generera enhets-ID och enhetstoken. Gå till `https://aex.aemmobile.adobe.com` och gör följande:

   * Ange API-nyckeln
   * Logga in med en Adobe ID som du har lagt till i ett AEM Mobile-projekt med följande behörigheter (se stegen nedan för att skapa ett projekt)

      * Administration > Hantera projekt och användare
      * Innehåll > Lägg till och redigera innehåll, ta bort innehåll, visa innehåll, publicera innehåll

Om alla villkor uppfylls genereras ett enhets-ID och en enhetstoken.

>[!NOTE]
>
>Den Adobe ID som behövs ska ges åtkomst till ett AEM Mobile-projekt. Se [Kontoadministration för AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html) i onlinehjälpen.

## Skapa projekt för AEM Mobile {#creating-projects-for-aem-mobile}

När du skapar ett projekt anger du inställningar för de plattformar du har som mål: iOS, Android, Windows och Desktop Web Viewer. Många av de projektinställningar du anger påverkar programmets beteende.

Om du vill skapa ett projekt måste du logga in på On-Demand Services-portalen med en Adobe ID som har en Överordnad administratörsroll. Att redigera ett projekt kräver antingen en Överordnad administratörsroll eller en användarroll med en **Hantera projekt och användare** behörighet.

>[!NOTE]
>
>Om du vill veta mer om hur du skapar projekt i AEM Mobile klickar du på [här](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html).

## Konfigurera en AEM Mobile Connector {#configuring-an-aem-mobile-connector}

AEM konfigurering omfattar följande steg för kopplingskonfiguration. När AEM Mobile Connector-konfigurationen är klar kan användaren konfigurera användargrupper och behörigheter.

AEM Mobile On-Demand-kontakten används för att binda AEM Mobile-hanterat innehåll med Adobe Experience Manager Mobile On-Demand-tjänster. Detta gör att innehållsförfattare kan skapa och hantera material för mobilapplikationer med hjälp av AEM verktyg och AEM Mobile On-Demand-tjänster för enkel distribution av mobilmaterial.

>[!NOTE]
>
>Detta är ett steg för att konfigurera AEM.

### Konfigurera AEM Mobile On-demand Services Client {#configuring-aem-mobile-on-demand-services-client}

Du måste slutföra konfigurationsstegen för att AEM Mobile-integreringarna ska fungera korrekt.

1. Gå till konfiguration av OSGI-tjänster

   1. AEM > Verktyg > Åtgärder > Webbkonsol
   1. Bläddra eller sök efter ***Experience Manager Mobile On-demand Services Client (tidigare Adobe Digital Publishing Solution Client)***

1. Redigera ***Klient för Experience Manager Mobile On-demand-tjänster***

   1. **(Obligatoriskt)** Ange obligatoriska fält:

      1. Klient-ID.
      1. Klienthemlighet.
   1. **(Valfritt)** Redigera befintliga värden.


1. Spara ändringarna.
1. Här är ett exempel på konfiguration:

![chlimage_1-53](assets/chlimage_1-53.png)

### Konfigurera AEM Mobile On-demand Services CloudService {#configuring-aem-mobile-on-demand-services-cloudservice}

1. Gå till Cloud Services

   1. AEM > Verktyg > Distribution> [CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). Bläddra eller sök efter ***Adobe Experience Manager Mobile On-demand-tjänster***

1. Välj ***Konfigurera nu*** eller ***Visa konfigurationer*** och välj ikonen Lägg till ny konfiguration

1. Skapa en ny konfiguration

   1. Ange en titel och ett namn
   1. Ange enhets-ID
   1. Ange enhetstoken
   1. Välj ***Testa enhetskonfiguration*** för att validera angivna värden
   1. Välj OK

## Lägga till AEM Mobile användarroller och tilldela behörigheter {#adding-aem-mobile-user-roles-and-assigning-permissions}

När du har skapat ett projekt bör du skapa roller och ge användarna åtkomst. Endast Överordnad administratörer kan skapa och redigera roller. När du skapar en roll aktiverar du funktioner (eller behörigheter) för de användare som tilldelas dessa behörigheter. Du kan t.ex. skapa en roll som innehåller behörigheter för appskapande och en annan roll som innehåller behörigheter för att skapa och publicera innehåll.

I AEM Mobile apputveckling finns det tre olika roller:

* Administratör
* Developer
* Författare

Mer information om hur du skapar roller med olika behörigheter, t.ex. för att skapa och publicera innehåll, finns i [Skapa användarroller och bevilja åtkomst](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) i hjälpen för AEM Mobile.

>[!NOTE]
>
>Att hantera appinnehåll kräver en gemensam insats från utvecklare, innehållsförfattare och administratörer. Författare hanterar sidor, som i sin tur bygger på mallar och komponenter som genereras av apputvecklare. Slutligen publicerar administratörer det uppdaterade programinnehållet strategiskt. När du konfigurerar AEM grupper och behörigheter definieras deras roller i appkontrollpanelen eller kontrollcentret.
>
>Mer information om AEM Mobile Dashboard får du om du klickar på [här](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

När du är klar med att skapa roller med olika behörigheter, t.ex. för att skapa och publicera innehåll, finns mer information i [**Konfigurera användar- och användargrupper**](/help/mobile/aem-mobile-configure-users.md) för att konfigurera dina användare och grupper så att de kan hantera redigering och hantering av dina mobilappar.

### Ytterligare resurser {#additional-resources}

Mer information om de två andra rollerna och ansvarsområdena för att skapa en AEM Mobile On-demand Services-app finns i följande resurser:

* [Utveckla AEM för AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [AEM innehåll för AEM Mobile On-demand Services App](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>Information om hur du förhandsgranskar appinnehållet, inklusive bläddringssidor och artiklar, finns i [Förhandsgranska med Preflight](/help/mobile/aem-mobile-manage-ondemand-services.md).
