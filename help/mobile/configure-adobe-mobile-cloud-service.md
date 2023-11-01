---
title: Konfigurera Cloud Servicen för Adobe Mobile Services
seo-title: Configure your Adobe Mobile Services Cloud Service
description: Följ den här sidan om du vill konfigurera Cloud Servicen för Adobe Mobile Services.
seo-description: Follow this page to configure your Adobe Mobile Services Cloud Service.
uuid: 21fe5b24-dc4d-4ee4-9e7f-ed4783baf276
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 962e9e98-a303-435b-a938-31319282e022
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
exl-id: 209c36f9-1a4b-4eea-8dde-22e0fc9718c1
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 1%

---

# Konfigurera Cloud Servicen för Adobe Mobile Services {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

The **Mobile Metrics Tile** på kommandocentralen ger realtidsanalyser för mobilapplikationer.

The [Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK är tillgängligt via en PhoneGap-plugin. Mätvärden samlas in och cachelagras på enheten tills enheten är ansluten, då data överförs till Adobe Mobile Services Cloud för rapportering och analys.

Adobe Mobile Analytics SDK innehåller följande:

1. **Datainsamling för mobila kanaler** - Samla in omfattande data för era mobilwebbplatser och -appar i alla större operativsystem.
1. **Analys av mobilengagemang** - Förstå användarengagemanget i mobilappar, på webbplatser eller i videor, inklusive hur ofta kunderna öppnar kanalen, oavsett om de gör inköp från den eller inte, med mera.
1. **Kontrollpaneler och rapporter för mobilappar** - Få användningsrapporter med livscykelstatistik för appar och appbutikstatistik - se trender för användare, starter, genomsnittlig sessionslängd, kvarhållningslängd och krascher.
1. **Mobilkampanjanalys** - Mät effekten av mobilspecifika kampanjer som SMS, mobil sökannonsering, mobil displayannonsering och QR-koder.
1. **Geolokaliseringsanalys** - Ta reda på var era appanvändare öppnar och interagerar med era mobilupplevelser via GPS-positionering eller intressepunkter.
1. **Bananalys** - Se hur användarna navigerar i appen för att avgöra vilka skärmar och gränssnittselement som är engagerande användare och vilka som får användarna att släppa.

>[!CAUTION]
>
>The **Analysera mått** Panelen visas bara på instrumentpanelen om du har konfigurerat molntjänster.

![chlimage_1-22](assets/chlimage_1-22.png)

AEM Command Center Metrics Tile

## Konfigurera Cloud Servicen {#configuring-the-cloud-service}

För att kunna dra nytta av Adobe Mobile Services Analytics måste du konfigurera AEM Mobile Analytics Cloud-tjänsten med din Adobe Analytics-kontoinformation.

1. Klicka på ikonen längst upp till höger för att lägga till eller redigera Cloud Service från **Hantera Cloud Service** från appkontrollpanelen.

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. The **Lägg till eller redigera Cloud Service** visas. Välj **Adobe Mobile Services** och klicka **Nästa**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. Välj en befintlig konfiguration på menyn **Mobiltjänster** eller välja **Skapa konfiguration** för att skapa en ny.

   För ny konfiguration anger du **Egenskaper för mobiltjänster** och klicka **Verifiera.**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   Om inloggningsuppgifterna verifieras visas **Verifiera** knappen ändras till **Verifierad**. Du kan välja en mobiltjänstapp från **Välj en mobilappstjänst**.

   Klicka **Skicka** för att konfigurera konfigurationen.

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. När du har konfigurerat ett moln kan du visa det på din instrumentpanel.

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >När du har konfigurerat molnkonfigurationen kan du visa **Analysera mått** Lägg sida vid sida på appkontrollpanelen.

   ![chlimage_1-28](assets/chlimage_1-28.png)
