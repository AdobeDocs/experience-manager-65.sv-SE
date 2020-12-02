---
title: Konfigurera Cloud Servicen för Adobe Mobile Services
seo-title: Konfigurera Cloud Servicen för Adobe Mobile Services
description: Följ den här sidan om du vill konfigurera Cloud Servicen för Adobe Mobile Services.
seo-description: Följ den här sidan om du vill konfigurera Cloud Servicen för Adobe Mobile Services.
uuid: 21fe5b24-dc4d-4ee4-9e7f-ed4783baf276
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 962e9e98-a303-435b-a938-31319282e022
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 1%

---


# Konfigurera Cloud Servicen för Adobe Mobile Services {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

**Mobile Metrics Tile** på kommandocentralen ger realtidsanalyser för ditt mobilprogram.

[Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK är tillgängligt via ett PhoneGap-plugin-program. Mätvärden samlas in och cachelagras på enheten tills enheten är ansluten, då data överförs till Adobe Mobile Services Cloud för rapportering och analys.

Adobe Mobile Analytics SDK innehåller följande:

1. **Datainsamling för mobila kanaler**  - Samla in omfattande data för era mobilwebbplatser och appar i alla större operativsystem.
1. **Analys**  av mobilengagemang - Förstå användarengagemanget i mobilappen, på webbplatsen eller i videon, inklusive hur ofta konsumenterna öppnar kanalen, oavsett om de gör inköp från den eller inte, med mera.
1. **Kontrollpaneler och rapporter**  för mobilappar - Få användningsrapporter med livscykelstatistik för dina appar och appbutikstatistik - se trender för användare, starter, genomsnittlig sessionslängd, kvarhållningslängd och krascher.
1. **Analys**  av mobilkampanjer - kvantifiera effekten av mobilspecifika kampanjer som SMS, mobil sökannonsering, mobil displayannonsering och QR-koder.
1. **Geolokaliseringsanalys**  - Hitta var era appanvändare öppnar och interagerar med era mobilupplevelser via GPS-positionering eller intressepunkter.
1. **Målningsanalys**  - Se hur användarna navigerar i appen för att avgöra vilka skärmar och gränssnittselement som engagerar användarna och vilka som får användarna att dra sig ur.

>[!CAUTION]
>
>**Analysera mått**-plattan visas på kontrollpanelen endast om du har konfigurerat molntjänster.

![chlimage_1-22](assets/chlimage_1-22.png)

AEM Command Center Metrics Tile

## Konfigurera Cloud Servicen {#configuring-the-cloud-service}

För att kunna utnyttja Adobe Mobile Services Analytics måste du konfigurera AEM Mobile Analytics Cloud-tjänsten med din Adobe Analytics-kontoinformation.

1. Klicka på ikonen längst upp till höger för att lägga till eller redigera Cloud Services från panelen **Hantera Cloud Services** från appkontrollpanelen.

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. Skärmen **Lägg till eller redigera Cloud Services** visas. Välj **Adobe Mobile Services** och klicka på **Nästa**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. Välj en befintlig konfiguration från **Mobiltjänster** eller välj **Skapa konfiguration** för att skapa en ny.

   Ange **Mobile Services Properties** och klicka på&#x200B;**Verify för att få en ny konfiguration.**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   Om inloggningsuppgifterna verifieras ändras knappen **Verifiera** till **Verifierad**. Du kan välja en mobiltjänstapp i **Välj en mobilappstjänst**.

   Klicka på **Skicka** för att konfigurera konfigurationen.

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. När du har konfigurerat ett moln kan du visa det på din instrumentpanel.

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >När du har konfigurerat molnet kan du visa **Analyze Metrics** Tile i din appkontrollpanel.

   ![chlimage_1-28](assets/chlimage_1-28.png)

