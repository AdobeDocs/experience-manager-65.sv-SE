---
title: Skapa och konfigurera program
description: Att skapa en app är ofta det första steget mot att skapa och hantera AEM Mobile On-Demand-innehåll. Följ den här sidan om du vill veta mer.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: dbe81ead-dfaa-4af0-9b66-a14917a1bcc7
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# Skapa och konfigurera program{#application-create-and-configuration-actions}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

## Skapa ett on demand-program {#creating-an-on-demand-application}

Att skapa en app är ofta det första steget mot att skapa och hantera AEM Mobile On-Demand-innehåll, och det görs ofta på AEM administratörsnivå. Det representerar ett innehållskal som kan visas på mobila enheter, klart att visa innehåll som författaren skapat, t.ex. artiklar, bilder, samlingar och så vidare.

Information om ditt program kan visas på kontrollpanelen eller i AEM Mobile Control Center.

>[!NOTE]
>
>Kontrollpanelen är en serie användbara paneler som ger en översikt över programmets innehåll, metadata och anslutningsstatus för AEM Mobile On-Demand.
>
>Se [AEM Mobile Application Dashboard](/help/mobile/mobile-apps-ondemand-application-dashboard.md) för mer information.

**Så här skapar du en on demand-app:**

1. Välj **Mobil** från sidospåret.
1. Välj **Appar** från Navigation.
1. Klicka **Skapa** och markera **App** i listrutan.
1. Välj mallen för mobilappar och klicka på **Nästa**.
1. Ange appegenskaper som **Titel**, **Namn**, **Beskrivning**.
1. Klicka på **Nästa**.
1. Om du känner till detta anger du information om molnkonfigurationen. Klicka annars på **Skapa**.
1. Klicka **Klar** för att visa din nya AEM Mobile-app i katalogen.

![chlimage_1](assets/chlimage_1.gif)

>[!NOTE]
>
>Med den här processen kan du skapa en programinstans i AEM.

## Använda appmallar {#using-app-templates}

Appmallar är ett enkelt sätt att använda befintliga designer som skapats av utvecklare och som används för att skapa nya appar i AEM.

Vad är en appmall? Se det som en samling sidmallar och komponenter som utgör en grund eller grund för ett program.
När du skapar ett program baserat på en mall för ett annat program får du ett program som har en startpunkt som representerar det program som det skapades från.

Du måste ha en befintlig mobilappsmall (eller en app som har en appmall) för att kunna använda den här funktionen.

### Nästa steg {#the-next-step}

När du har skapat en On-Demand-app från kontrollpanelen för program är nästa steg att koppla din app till molnkonfigurationen.

Se [Koppla ditt program till molnkonfigurationen](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md) för mer information.

### Komma i förväg {#getting-ahead}

När du är bekant med att skapa ett on-demand-program och därmed koppla det programmet till en molnkonfiguration kan du läsa [Innehållshanteringsåtgärder](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md).

**Innehållshanteringsåtgärder** innebär att följande innehåll skapas och hanteras:

* [Hantera artiklar](/help/mobile/mobile-on-demand-managing-articles.md)
* [Hantera banners](/help/mobile/mobile-on-demand-managing-banners.md)
* [Hantera samlingar](/help/mobile/mobile-on-demand-managing-collections.md)
* [Överför delade resurser](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicera inte publicera innehåll](/help/mobile/mobile-on-demand-publishing-unpublishing.md)

Mer information om roller och ansvar för en administratör och utvecklare finns i resurserna nedan:

* [Utveckla AEM för AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Administrera innehåll för användning av AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)
