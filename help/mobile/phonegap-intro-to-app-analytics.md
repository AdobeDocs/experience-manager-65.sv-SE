---
title: Spåra appprestanda med Adobe Mobile Analytics
seo-title: Spåra appprestanda med Adobe Mobile Analytics
description: Med Adobe mobiltjänster kan ni få insikt i hur era användare använder era mobilappar genom att spåra användningen, appkrascher, enhetsinformation och så många andra viktiga mätvärden för era mobilappar. Följ den här sidan om du vill veta mer.
seo-description: Med Adobe mobiltjänster kan ni få insikt i hur era användare använder era mobilappar genom att spåra användningen, appkrascher, enhetsinformation och så många andra viktiga mätvärden för era mobilappar. Följ den här sidan om du vill veta mer.
uuid: 139858c7-66a1-4fea-9f7e-4671b86f67e6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 377548fa-987a-4a59-84a3-067a3541b6b2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 0%

---


# Spåra appprestanda med Adobe Mobile Analytics{#track-app-performance-with-adobe-mobile-analytics}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

Ni vill öka kundkonverteringarna och lojaliteten.

Ni vill leverera relevanta och engagerande upplevelser till era kunder.

Vad gör er AEM Mobile-app för era marknadsföringskampanjer?

Hur kan ni finjustera era mobilapplikationer för att ge era användare den bästa upplevelsen?

Med Adobe mobiltjänster kan ni få insikt i hur era användare använder era mobilappar genom att spåra användningen, appkrascher, enhetsinformation och så många andra viktiga mätvärden för era mobilappar.

Adobe Experience Manager Mobile ger en glimt av detaljerna i mobilanalysen direkt från AEM Mobile Application Dashboard. **Mobile Metrics Tile** på kontrollpanelen ger realtidsanalyser för mobilappen, vilket gör att utvecklare, författare och administratörer kan få en snabb glimt av mobilappens hälsa. Under omslaget som ligger till grund för analysen finns [Adobe Mobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK. Adobe Mobile Analytics SDK kan kopplas in i dina program direkt eller via en PhoneGap bridge-plugin för webbvisningar. Mätvärden samlas in och cachelagras på enheten tills enheten är ansluten och data överförs till Adobe Mobile Services Cloud för rapportering och analys.

Adobe Mobile Analytics SDK innehåller följande:

1. **Datainsamling för mobila kanaler**  - Samla in omfattande data för era mobilwebbplatser och appar i alla större operativsystem.
1. **Analys**  av mobilengagemang - Förstå användarengagemanget i mobilappen, på webbplatsen eller i videon, inklusive hur ofta konsumenterna öppnar kanalen, oavsett om de gör inköp från den eller inte, med mera.
1. **Kontrollpaneler och rapporter**  för mobilappar - Få användningsrapporter med livscykelstatistik för dina appar och appbutikstatistik - se trender för användare, starter, genomsnittlig sessionslängd, kvarhållningslängd och krascher.
1. **Analys**  av mobilkampanjer - kvantifiera effekten av mobilspecifika kampanjer som SMS, mobil sökannonsering, mobil displayannonsering och QR-koder.
1. **Geolokaliseringsanalys**  - Hitta var era appanvändare öppnar och interagerar med era mobilupplevelser via GPS-positionering eller intressepunkter.
1. **Målningsanalys**  - Se hur användarna navigerar i appen för att avgöra vilka skärmar och gränssnittselement som engagerar användarna och vilka som får användarna att dra sig ur.

I det här avsnittet beskrivs hur [AEM utvecklare](#developers) kan lära sig hur du instrumenterar AEM Mobile-program med analysspårning.

[AEM administratörer](#administrators) lär sig slutligen att:

* skapa en molntjänst för Adobe Mobile Services
* skapa en mobiltjänstkonfiguration och associera en rapportserie
* associera mobiltjänstkonfigurationen med en mobilapp
* visa mätvärden via AEM Apps Command Center
* tilldela AMS SDK Config till din mobilapp

## För utvecklare - Integrera Analytics i appen {#for-developers-integrate-analytics-into-your-app}

**Krav:** AEM administratörer måste konfigurera molnkonfigurationen för Adobe Mobile Services  [enligt beskrivningen nedan](#amscloudserviceconfig).

Utvecklarna ansvarar för att [lägga till analyser till en AEM Mobile-app](/help/mobile/phonegap-add-analytics-to-apps.md) när det behövs för att spåra, rapportera och förstå hur användarna interagerar med mobilappsinnehållet och för att mäta nyckelvärden för livscykeln, som starter, apptid och kraschfrekvens.

## För administratörer - Konfigurera Cloud Servicen Adobe Mobile Services {#for-administrators-configure-the-adobe-mobile-services-cloud-service}

För att kunna dra nytta av Adobe mobiltjänster måste du konfigurera Cloud Servicen AEM Adobe mobiltjänster med din Adobe Analytics-kontoinformation. Apps Command Center tillhandahåller en **Analyze Metrics**-panel där du kan skapa och associera molntjänsten med din mobilapp.

Konfigurera molntjänsten för din mobilapp genom att klicka på kugghjulsikonen som finns i rutan Analysera mått.

![chlimage_1-125](assets/chlimage_1-125.png)

Om du klickar på kugghjulsikonen i rutan Analysera mått öppnas den modala dialogrutan Konfigurera Mobile Services Analytics. Välj din konfiguration i listrutan Välj en konfiguration för mobiltjänst. Om du behöver skapa en ny konfiguration klickar du på skiftknappen.

För att skapa en molntjänst för mobiltjänster i Adobe finns det två steg: anslutning till tjänsten och val av vilken rapporteringssvit som ska tilldelas konfigurationen.

Börja med att klicka på plusknappen (+) på panelen Hantera Cloud Services på kontrollpanelen.

![chlimage_1-126](assets/chlimage_1-126.png)

När du klickar på knappen **+** visas guiden **Lägg till Cloud Service**.

![chlimage_1-127](assets/chlimage_1-127.png)

Välj eller skapa en ny konfiguration för mobiltjänster genom att fylla i de obligatoriska fälten som visas nedan. Din AEM kräver den här informationen för att anslutningen till Adobe Mobile Services ska kunna skapas.

![chlimage_1-128](assets/chlimage_1-128.png)

När du har slutfört kontoinställningarna för mobiltjänster uppmanas du att välja en app. När du gör det kopplas analysrapporter för mobiltjänster från Adobe till det programmet.

Välj önskad mobiltjänst och klicka på Uppdatera för att tilldela mobiltjänstkonfigurationen och stänga dialogrutan.

Nu när du har kopplat mobiltjänstkonfigurationen till AEM Mobile-appen börjar panelen hämta mätdata och börja rapportera.

![chlimage_1-129](assets/chlimage_1-129.png)

### Adobe Mobile Services SDK-konfigurationsfil {#adobe-mobile-services-sdk-config-file}

I nuläget är mobilapplikationen kopplad till en molntjänst, men mobilappen vet ännu inte hur den insamlade mobilinformationen ska skickas tillbaka till Adobe Analytics. Om du vill koppla upp mobilappen till Adobe Analytics måste konfigurationsfilen för Adobe Mobile Services SDK läggas till i Adobe Experience Manager.

I rutan Analysera mått klickar du på pilikonen för att visa menyalternativen Hämta/överför AMS SDK-konfiguration.

![chlimage_1-130](assets/chlimage_1-130.png)

Det första steget är att hämta SDK-konfigurationen från Adobe Mobile Services. Om du klickar på Hämta AMS SDK Config omdirigeras du till webbplatsen Adobe Mobile Services där du kan hämta konfigurationsfilen från. När du har fått filen ADBMobilConfig.json klickar du på &quot;Överför AMS SDK-konfiguration&quot; för att överföra konfigurationsfilen till AEM.

![chlimage_1-131](assets/chlimage_1-131.png)

Klicka på knappen &quot;Upload Adobe Mobile Services Application Config&quot; och bläddra efter filen ADBMobleConfig.json och klicka sedan på &quot;Upload&quot;.

Nu när mobilappen har tillgång till filen ADBMobilConfig.json har den kunskap om hur man kommunicerar med Adobe Analytics och börjar rapportera om viktiga mätvärden som kan hjälpa er att lyckas med apparna.

## Vad händer nu? {#what-s-next}

1. [Starta min appupplevelse från AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Hantera appens innehåll](/help/mobile/phonegap-manage-app-content.md)
1. [Bygg min applikation](/help/mobile/building-app-mobile-phonegap.md)
1. [Spåra appens prestanda med Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Leverera en personaliserad appupplevelse med Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Skicka viktiga meddelanden till mina användare](/help/mobile/phonegap-push-notifications.md)