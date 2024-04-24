---
title: Spåra appprestanda med Adobe Mobile Analytics
description: Med Adobe Mobile Services kan ni få insikt i hur era användare använder era mobilappar genom att spåra användningen, appkrascher, enhetsinformation och så många andra viktiga mätvärden för era mobilappar. Följ den här sidan om du vill veta mer.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 7e358660-bc2f-4d8f-8d74-6cdb6c1ea7b5
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 1%

---

# Spåra appprestanda med Adobe Mobile Analytics{#track-app-performance-with-adobe-mobile-analytics}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

Ni vill öka kundkonverteringarna och lojaliteten.

Ni vill leverera relevanta och engagerande upplevelser till era kunder.

Vad gör er AEM Mobile-app för era marknadsföringskampanjer?

Hur kan ni finjustera era mobilapplikationer för att ge era användare den bästa upplevelsen?

Med Adobe Mobile Services kan ni få insikt i hur era användare använder era mobilappar genom att spåra användningen, appkrascher, enhetsinformation och så många andra viktiga mätvärden för era mobilappar.

Adobe Experience Manager Mobile ger en glimt av detaljerna i mobilanalysen direkt från AEM Mobile Application Dashboard. The **Mobile Metrics Tile** på kontrollpanelen tillhandahåller Real-Time Analytics för mobilappen så att utvecklare, författare och administratörer snabbt kan få en inblick i hur mobilappen fungerar. Under omslaget är kraften i analysen [Adobe Mobile Analytics](https://business.adobe.com/products/analytics/mobile-marketing.html) SDK. Adobe Mobile Analytics SDK kan kopplas in i programmen direkt eller via en PhoneGap Bridge-plugin för webbvisningar. Mätvärden samlas in och cachelagras på enheten tills enheten är ansluten och data överförs till Adobe Mobile Services Cloud för rapportering och analys.

Adobe Mobile Analytics SDK innehåller följande:

1. **Datainsamling för mobila kanaler** - Samla in omfattande data för era mobilwebbplatser och -appar i alla större operativsystem.
1. **Analys av mobilengagemang** - Förstå användarengagemanget i mobilappar, på webbplatser eller i videor, inklusive hur ofta kunderna öppnar kanalen, oavsett om de gör inköp från den eller inte, med mera.
1. **Kontrollpaneler och rapporter för mobilappar** - Få användningsrapporter med livscykelstatistik för appar och appbutikstatistik - se trender för användare, starter, genomsnittlig sessionslängd, kvarhållningslängd och krascher.
1. **Mobilkampanjanalys** - Mät effekten av mobilspecifika kampanjer som SMS, mobil sökannonsering, mobil displayannonsering och QR-koder.
1. **Geolokaliseringsanalys** - Ta reda på var era appanvändare öppnar och interagerar med era mobilupplevelser via GPS-positionering eller intressepunkter.
1. **Bananalys** - Se hur användarna navigerar i appen för att avgöra vilka skärmar och gränssnittselement som är engagerande användare och vilka som får användarna att släppa.

Detta avsnitt beskriver hur [AEM](#developers) kan sedan lära sig hur man kan mäta AEM Mobile-appar med analysspårning.

Äntligen [AEM administratörer](#administrators) lära dig:

* skapa en molntjänst för Adobe Mobile Services
* skapa en mobiltjänstkonfiguration och associera en rapportserie
* associera mobiltjänstkonfigurationen med en mobilapp
* visa mätvärden via AEM Apps Command Center
* tilldela AMS SDK Config till din mobilapp

## För utvecklare - Integrera Analytics i er app {#for-developers-integrate-analytics-into-your-app}

**Krav:** AEM måste konfigurera molnkonfigurationen för Adobe Mobile Services, [enligt nedan](#amscloudserviceconfig).

Utvecklare ansvarar för [lägga till analyser i en AEM Mobile-app](/help/mobile/phonegap-add-analytics-to-apps.md) vid behov för att spåra, rapportera och förstå hur användarna interagerar med mobilappsinnehållet och för att mäta nyckeltal under livscykeln, som starter, apptid och kraschfrekvens.

## För administratörer - Konfigurera Cloud Servicen Adobe Mobile Services {#for-administrators-configure-the-adobe-mobile-services-cloud-service}

För att kunna utnyttja Adobe Mobile Services måste du konfigurera Cloud Servicen AEM Adobe Mobile Services med din Adobe Analytics-kontoinformation. Apps Command Center innehåller en **Analysera mått** där du kan skapa och koppla molntjänsten till din mobilapp.

Konfigurera molntjänsten för din mobilapp genom att klicka på kugghjulsikonen i rutan Analysera mått.

![chlimage_1-125](assets/chlimage_1-125.png)

Om du klickar på kugghjulsikonen i rutan Analysera mått öppnas den modala dialogrutan&quot;Konfigurera analys av mobila tjänster&quot;. Välj din konfiguration i listrutan Välj en konfiguration för mobiltjänst. Om du måste skapa en konfiguration klickar du på växlingsknappen.

För att skapa en molntjänst för mobiltjänster i Adobe finns det två steg: anslutning till tjänsten och val av vilken rapporteringssvit som ska tilldelas konfigurationen.

Börja med att klicka på plusknappen (+) på panelen Hantera Cloud Service på kontrollpanelen.

![chlimage_1-126](assets/chlimage_1-126.png)

När du klickat på&#x200B;**+**&#39;, **Lägg till Cloud Service** visas.

![chlimage_1-127](assets/chlimage_1-127.png)

Välj eller skapa en mobiltjänstkonfiguration genom att fylla i obligatoriska fält enligt nedan. Din AEM kräver den här informationen för att anslutningen till Adobe Mobile Services ska kunna skapas.

![chlimage_1-128](assets/chlimage_1-128.png)

När du har slutfört kontoinställningarna för mobiltjänster uppmanas du att välja en app. När du gör det kopplas analysrapporter för mobiltjänster från Adobe till det programmet.

Välj önskad mobiltjänst och klicka på Uppdatera för att tilldela mobiltjänstkonfigurationen och stänga dialogrutan.

Nu när du har kopplat mobiltjänstkonfigurationen till AEM Mobile-appen börjar panelen hämta mätdata och börja rapportera.

![chlimage_1-129](assets/chlimage_1-129.png)

### Konfigurationsfil för Adobe Mobile Services SDK {#adobe-mobile-services-sdk-config-file}

I nuläget är mobilapplikationen kopplad till en molntjänst, men mobilappen vet ännu inte hur den insamlade mobilinformationen ska skickas tillbaka till Adobe Analytics. Om du vill ansluta mobilappen till Adobe Analytics måste konfigurationsfilen för Adobe Mobile Services SDK läggas till i Adobe Experience Manager.

I rutan Analysera mått klickar du på pilikonen för att visa menyalternativen Hämta/överför AMS SDK-konfiguration.

![chlimage_1-130](assets/chlimage_1-130.png)

Det första steget är att hämta SDK-konfigurationen från Adobe Mobile Services. Klicka på Hämta AMS SDK Config om du vill omdirigera till webbplatsen Adobe Mobile Services där du kan hämta konfigurationsfilen från. När du har hämtat filen ADBMobleConfig.json klickar du på &quot;Överför AMS SDK-konfiguration&quot; för att överföra konfigurationsfilen till AEM.

![chlimage_1-131](assets/chlimage_1-131.png)

Klicka på knappen &quot;Upload Adobe Mobile Services Application Config&quot; och bläddra efter filen ADBMobleConfig.json och klicka sedan på &quot;Upload&quot;.

Nu när mobilappen har tillgång till filen ADBMobilConfig.json har den kunskap om hur man kommunicerar med Adobe Analytics och börjar rapportera om viktiga mätvärden som hjälper er att lyckas med apparna.

## Vad händer nu? {#what-s-next}

1. [Starta min appupplevelse från AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Hantera appens innehåll](/help/mobile/phonegap-manage-app-content.md)
1. [Bygg min applikation](/help/mobile/building-app-mobile-phonegap.md)
1. [Spåra appens prestanda med Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Leverera en personaliserad appupplevelse med Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Skicka viktiga meddelanden till mina användare](/help/mobile/phonegap-push-notifications.md)
