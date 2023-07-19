---
title: Molnkonfiguration
seo-title: Cloud Configuration
description: Genom att koppla en On-Demand-app till en molnkonfiguration kan Adobe Experience Manager (AEM) kommunicera direkt med ett Mobile On-Demand-projekt genom att skapa en tvåvägslänk. Följ den här sidan om du vill veta mer.
seo-description: Associating an On-Demand App to a Cloud Configuration allows Adobe Experience Manager (AEM) to communicate directly with a Mobile On-Demand hosted project by establishing a two way link. Follow this page to learn more.
uuid: f377f2af-864b-43df-9d42-4a5fd6cd70d5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: d0d29b99-53d4-4b0d-947b-39d91b381de7
exl-id: 37428543-c310-4712-a4ec-1f482579fb4b
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 1%

---

# Molnkonfiguration{#cloud-configuration}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

Genom att koppla en On-Demand-app till en molnkonfiguration kan Adobe Experience Manager (AEM) kommunicera direkt med ett Mobile On-Demand-projekt genom att skapa en tvåvägslänk. Genom att länka din app till ett Mobile On-Demand-projekt kan du skapa innehåll, till exempel artiklar, banners och samlingar i AEM, men även skicka det till Mobile On-Demand.

Därifrån blir det möjligt att publicera, förhandsgranska och hantera innehåll. Du kan också importera befintligt mobilt on demand-innehåll till AEM och redigera innehåll.

## Konfigurera molnkonfiguration {#setting-up-cloud-configuration}

>[!CAUTION]
>
>Innan du börjar konfigurera molnkonfigurationen för ditt On-Demand-program måste du känna till AEM Mobile Provisioning and Configuring AEM Mobile On-demand Services Client.
>
>Mer information finns i [Konfigurera AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md) i avsnittet Administrera.

Om du vill konfigurera Cloud Services för mobil on demand klickar du på den översta kugghjulet i det högra hörnet av **Hantera anslutning** från appkontrollpanelen.

Du bör känna till appkontrollpanelen och tillgängliga paneler. Se [AEM Mobile Application Dashboard](/help/mobile/mobile-apps-ondemand-application-dashboard.md) för mer information.

### Konfigurera länk till molnkonfiguration {#setting-up-link-to-cloud-configuration}

>[!CAUTION]
>
>Kontrollera att du har en befintlig On-Demand-klient och molnkonfiguration.
>
>Mer information finns i [Konfigurera AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md) i avsnittet Administrera.

I följande steg beskrivs hur du konfigurerar länken till molnkonfigurationen:

1. Från **Mobil**, välja **Appar** och sedan mobilappen On-Demand från katalogen.
1. Klicka på kugghjulsikonen på **Hantera anslutning** platta.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Ange den befintliga konfigurationen eller skapa en ny genom att ange **Konfigurationstitel**, **Enhets-ID** och **Enhetstoken**.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. När du **Enhets-ID** och **Enhetstoken** Om du har verifierat det väljer du ett On-Demand-projekt i listan.

   Klicka **Skicka**.

   ![chlimage_1-67](assets/chlimage_1-67.png)

   The **Hantera anslutning** visas din molnkonfiguration.

   ![chlimage_1-68](assets/chlimage_1-68.png)

   >[!CAUTION]
   >
   >Om du försöker ändra vilket projekt som den här appen är kopplad till och byter projekt på kontrollpanelen får du en varning om innehållsintegritetsproblem enligt bilden nedan:

   ![chlimage_1-69](assets/chlimage_1-69.png)

### Nästa steg {#the-next-steps}

När du har konfigurerat molnkonfigurationen för din app kan du läsa följande resurser för att hantera innehåll:

* [Hantera artiklar](/help/mobile/mobile-on-demand-managing-articles.md)
* [Hantera banners](/help/mobile/mobile-on-demand-managing-banners.md)
* [Hantera samlingar](/help/mobile/mobile-on-demand-managing-collections.md)
* [Överför delade resurser](/help/mobile/mobile-on-demand-shared-resources.md)
* [Publicera/avpublicera innehållet](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Förhandsgranska med Preflight](/help/mobile/aem-mobile-manage-ondemand-services.md)
