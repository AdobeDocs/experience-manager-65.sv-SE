---
title: Konfigurera Cloud Servicen för Adobe Mobile Services
description: Följ den här sidan om du vill konfigurera Cloud Servicen för Adobe Mobile Services.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
exl-id: 209c36f9-1a4b-4eea-8dde-22e0fc9718c1
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 3%

---

# Konfigurera Cloud Servicen för Adobe Mobile Services {#configure-your-adobe-mobile-services-cloud-service}

{{ue-over-mobile}}

**Mobile Metrics Tile** på kommandocentralen ger realtidsanalyser för ditt mobilprogram.

SDK [Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) är tillgänglig via en PhoneGap-plugin. Mätvärden samlas in och cachelagras på enheten tills enheten är ansluten, då data överförs till Adobe Mobile Services Cloud för rapportering och analys.

Adobe Mobile Analytics SDK tillhandahåller följande:

1. **Datainsamling för mobila kanaler** - Samla in omfattande data för dina mobila webbplatser och appar på alla större operativsystem.
1. **Analys av mobilengagemang** - Förstå användarengagemanget i mobilappen, på webbplatsen eller i videon, inklusive hur ofta konsumenterna öppnar kanalen, oavsett om de gör köp från den eller inte.
1. **Kontrollpaneler och rapporter för mobilappar** - Få användningsrapporter med livscykelstatistik för dina appar och appbutiksmått - se trender för användare, starter, genomsnittlig sessionslängd, kvarhållningslängd och krascher.
1. **Analys av mobilkampanjer** - Mät effekten av mobilspecifika kampanjer som SMS, mobil sökannonsering, mobil displayannonsering och QR-koder.
1. **Geolokaliseringsanalys** - Hitta var era appanvändare startar och interagerar med era mobilupplevelser via GPS-platser eller intressepunkter.
1. **Målningsanalys** - Se hur användarna navigerar i appen för att avgöra vilka skärmar och gränssnittselement som engagerar användarna och vilka som får användarna att sluta.

>[!CAUTION]
>
>**Analysera måttenhet** visas bara på kontrollpanelen om du har konfigurerat molntjänster.

![chlimage_1-22](assets/chlimage_1-22.png)

AEM Command Center Metrics Tile

## Konfigurera Cloud Servicen {#configuring-the-cloud-service}

För att kunna dra nytta av Adobe Mobile Services Analytics måste du konfigurera AEM Mobile Analytics Cloud-tjänsten med din Adobe Analytics-kontoinformation.

1. Klicka på den övre högra ikonen för att lägga till eller redigera Cloud Service från panelen **Hantera Cloud Service** på appkontrollpanelen.

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. Skärmen **Lägg till eller redigera Cloud Service** visas. Välj **Adobe Mobile Services** och klicka på **Next**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. Välj en befintlig konfiguration från **Mobiltjänster** eller välj **Skapa konfiguration** för att skapa en.

   Ange **Mobile Services-egenskaperna** och klicka på **Verifiera för att få en ny konfiguration.**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   Om autentiseringsuppgifterna verifieras ändras knappen **Verifiera** till **Verifierad**. Du kan välja en mobiltjänstapp från **Välj en mobilappstjänst**.

   Klicka på **Skicka** för att konfigurera konfigurationen.

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. När du har konfigurerat ett moln kan du visa det på din instrumentpanel.

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >När du har konfigurerat din molnkonfiguration kan du visa **Analysera måttpanel** på din appinstrumentpanel.

   ![chlimage_1-28](assets/chlimage_1-28.png)
