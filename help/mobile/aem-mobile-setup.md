---
title: AEM Mobile SetUp
description: Följ den här sidan för att konfigurera AEM Mobile och på så sätt tillåta användare att skapa och hantera innehåll i Adobe Experience Manager (AEM). Den här sidan innehåller information om hur du integrerar den AEM instansen med det molnbaserade AEM Mobile On-demand Services-kontot och -projekten.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
exl-id: 0ead982d-2315-4947-b762-596aa2aa42a1
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---

# AEM Mobile SetUp{#aem-mobile-setup}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>Befintliga användare av Adobe Experience Manager (AEM) mobilappar som migrerar från AEM 6.2 eller 6.3 till AEM 6.5 kan fortsätta använda AEM Mobile-appar genom att hämta ett paket från paketresursen. Nya installationer av AEM 6.5 har dock inte stöd för AEM Mobile Apps-funktioner.

Om du vill använda AEM för att producera innehåll för AEM Mobile-program måste du integrera den AEM instansen med det molnbaserade AEM Mobile On-demand Services-kontot och -projekten.

Följ de här stegen för att konfigurera AEM Mobile och på så sätt låta användaren skapa och hantera innehållet i AEM.

## AEM Mobile Provisioning {#aem-mobile-provisioning}

För att komma igång med AEM Mobile måste du:

* **Begär en API-nyckel**: Om du vill komma åt API:t för behovsstyrda tjänster måste du begära en API-nyckel. Om du vill begära API-nyckeln fyller du i formuläret [PDF](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html). Skicka det ifyllda formuläret till Adobe Developer Support: [wwds@adobe.com](mailto:wwds@adobe.com)

* **Generera enhets-ID och enhetstoken**: När du har fått din API-nyckel kan du generera enhets-ID och enhetstoken. Gå till `https://aex.aemmobile.adobe.com` och gör följande:

   * Ange API-nyckeln
   * Logga in med en Adobe ID som du har lagt till i ett AEM Mobile-projekt med följande behörigheter (se stegen nedan för att skapa ett projekt)

      * Administration > Hantera projekt och användare
      * Innehåll > Lägg till och redigera innehåll, ta bort innehåll, visa innehåll, Publish-innehåll

Om alla villkor uppfylls genereras ett enhets-ID och en enhetstoken.

>[!NOTE]
>
>Den Adobe ID som behövs ska ges åtkomst till ett AEM Mobile-projekt. Se [Kontoadministration för AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html) i onlinehjälpen.

## Skapa projekt för AEM Mobile {#creating-projects-for-aem-mobile}

När du skapar ett projekt anger du inställningar för de plattformar du har som mål: iOS, Android™, Windows och Desktop Web Viewer. Många av de projektinställningar du anger påverkar programmets beteende.

Om du vill skapa ett projekt måste du logga in på On-Demand Services-portalen med en Adobe ID som har rollen Master Admin. Redigering av ett projekt kräver antingen en huvudadministratörsroll eller en användarroll med behörigheten **Hantera projekt och användare**.

>[!NOTE]
>
>Klicka [här](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html) om du vill veta mer om hur du skapar projekt i AEM Mobile.

## Konfigurera en AEM Mobile Connector {#configuring-an-aem-mobile-connector}

AEM konfigurering omfattar följande steg för kopplingskonfigurationen. När AEM Mobile Connector-konfigurationen är klar kan användaren konfigurera användargrupper och behörigheter.

AEM Mobile On-Demand-kontakten används för att binda AEM Mobile-hanterat innehåll med Adobe Experience Manager Mobile On-Demand-tjänster. Detta gör att innehållsförfattare kan skapa och hantera material för mobilapplikationer med hjälp av AEM verktyg och AEM Mobile On-Demand-tjänster för enkel distribution av mobilmaterial.

>[!NOTE]
>
>Detta är ett engångssteg för att konfigurera AEM.

### Konfigurera AEM Mobile On-demand Services Client {#configuring-aem-mobile-on-demand-services-client}

Slutför konfigurationsstegen för att AEM Mobile-integreringarna ska fungera korrekt.

1. Gå till konfiguration av OSGI-tjänster

   1. AEM > Verktyg > Åtgärder > Webbkonsol
   1. Bläddra eller sök efter ***Experience Manager Mobile On Demand Services Client (var Adobe Digital Publishing Solution Client)***

1. Redigera klienten för ***Experience Manager Mobile On-demand-tjänster***

   1. **(Obligatoriskt)** Ange obligatoriska fält:

      1. Klient-ID.
      1. Klienthemlighet.

   1. **(Valfritt)** Redigera befintliga värden.

1. Spara ändringarna.
1. Här är ett exempel på konfiguration:

![chlimage_1-53](assets/chlimage_1-53.png)

### Konfigurera AEM Mobile On-demand Services CloudService {#configuring-aem-mobile-on-demand-services-cloudservice}

1. Gå till Cloud Service.

   1. AEM > Verktyg > Distribution > [CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). Bläddra eller sök efter ***Adobe Experience Manager Mobile On-demand-tjänster***

1. Välj ***Konfigurera nu*** eller ***Visa konfigurationer*** och välj ikonen Lägg till konfiguration.

1. Skapa en konfiguration

   1. Ange en titel och ett namn
   1. Ange enhets-ID
   1. Ange enhetstoken
   1. Välj ***Testa enhetskonfiguration*** så att du kan validera angivna värden
   1. Välj OK

## Lägga till AEM Mobile användarroller och tilldela behörigheter {#adding-aem-mobile-user-roles-and-assigning-permissions}

När du har skapat ett projekt bör du skapa roller och ge användarna åtkomst. Endast malladministratörer kan skapa och redigera roller. När du skapar en roll aktiverar du funktioner (eller behörigheter) för de användare som tilldelas dessa behörigheter. Du kan t.ex. skapa en roll som innehåller behörigheter för appskapande och en annan roll som innehåller behörigheter för att skapa och publicera innehåll.

I AEM Mobile apputveckling finns det tre olika roller:

* Administratör
* Developer
* Författare

Mer information om hur du skapar roller med olika behörigheter, t.ex. för att skapa och publicera innehåll, får du om du klickar på [Skapa användarroller och bevilja åtkomst](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) i AEM Mobile-hjälpen.

>[!NOTE]
>
>Att hantera appinnehåll kräver en gemensam insats från utvecklare, innehållsförfattare och administratörer. Författare hanterar sidor, som i sin tur bygger på mallar och komponenter som genereras av apputvecklare. Slutligen publicerar administratörer det uppdaterade programinnehållet strategiskt. När du konfigurerar AEM grupper och behörigheter definieras deras roller i appkontrollpanelen eller kontrollcentret.
>
>Se [AEM Mobile Dashboard](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

När du är klar med att skapa roller med olika behörigheter, t.ex. för att bygga appar eller för att skapa och publicera innehåll, se [**Konfigurera användar- och användargrupper**](/help/mobile/aem-mobile-configure-users.md). Om du gör det kan det hjälpa dig att konfigurera användare och grupper så att de kan hantera redigering och hantering av dina mobilappar.

### Ytterligare resurser {#additional-resources}

Mer information om de två andra rollerna och ansvarsområdena för att skapa en AEM Mobile On-demand Services-app finns i följande resurser:

* [Utveckla AEM för AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [AEM innehåll för AEM Mobile On-demand Services App](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>Mer information om hur du förhandsgranskar appinnehållet, inklusive bläddringssidor och artiklar, finns i [Förhandsgranska med preflight](/help/mobile/aem-mobile-manage-ondemand-services.md).
