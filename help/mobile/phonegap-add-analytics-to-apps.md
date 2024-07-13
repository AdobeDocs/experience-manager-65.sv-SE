---
title: Lägg till Adobe Analytics i ditt mobilprogram
description: Följ den här sidan för att lära dig mer om hur du kan använda mobilappsanalys i dina Adobe Experience Manager-appar genom att integrera med Adobe mobiltjänster.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 8d965e94-c368-481d-b000-6e22456c34db
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# Lägg till Adobe Analytics i ditt mobilprogram{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

Vill du skapa engagerande och relevanta upplevelser för mobilanvändare? Om du inte använder Adobe Mobile Services SDK för att övervaka och mäta programmets livscykel och användning, vad baserar du dina beslut på? Var är era mest lojala kunder? Hur kan ni garantera att ni är relevanta och optimerar konverteringarna?

Kommer användarna åt allt innehåll? Överger de appen, och i så fall, var? Hur ofta stannar de i appen och hur ofta de kommer tillbaka för att använda appen? Vilka förändringar kan ni införa och sedan mäta den ökade lojaliteten? Vad gäller för kraschfrekvenser, kraschar din app för dina användare?

Dra nytta av [mobilappsanalys](https://business.adobe.com/products/analytics/mobile-marketing.html) i dina Adobe Experience Manager-appar (AEM) genom att integrera med [Adobe mobiltjänster](https://business.adobe.com/products/campaign/mobile-marketing.html).

Instrumentera era AEM appar för att spåra, rapportera och förstå hur användarna interagerar med mobilappen och -innehållet och för att mäta nyckeltal under livscykeln, som starter, apptid och kraschfrekvens.

I det här avsnittet beskrivs hur AEM *utvecklare* kan:

* Integrera mobilanalys i mobilapplikationer
* Testa er analysspårning med Bloodhound

## Förutsättningar {#prerequisties}

AEM Mobile kräver ett Adobe Analytics-konto för att samla in och rapportera spårningsdata i appen. Som en del av konfigurationen måste AEM *Administrator* först:

* Konfigurera ett Adobe Analytics-konto och skapa en rapportsserie för ditt program i Mobiltjänster.
* Konfigurera en AMS-Cloud Service i Adobe Experience Manager (AEM).

## För utvecklare - Integrera mobilanalys i appen {#for-developers-integrate-mobile-analytics-into-your-app}

### Konfigurera ContentSync för att hämta konfigurationsfilen {#configure-contentsync-to-pull-in-configuration-file}

När Analytics-kontot har konfigurerats skapar du en konfiguration för innehållssynkronisering som hämtar in innehållet i ditt mobilprogram.

Mer information finns i Konfigurera Innehållssynkronisering. Konfigurationen måste instruera Innehållssynkronisering att placera ADBMobleConfig i katalogen /www. I Geometrixx Outdoors App är till exempel konfigurationen för innehållssynkronisering: */content/phonegap/geometrixx-outdoor/shell/jcr:content/page-app/app-config/ams-ADBMobleConfig*. Det finns även en konfiguration för utveckling. Den är dock identisk med icke-utvecklingskonfigurationen om det finns Geometrixx Outdoors.

Mer information om hur du hämtar ADBMomobileConfig från kontrollpanelen för mobilprogram AEM appar finns i Analytics - Mobile Services - Adobe Mobile Services SDK Config-fil.

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

För varje plattform krävs att ADBMomobileConfig kopieras till en viss plats.

Om du bygger med PhoneGap CLI kan du göra detta med ett cordova-byggkrokskript. Det här kan du se i Geometrixx-appen utomhus på:*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js.*

För iOS måste filen kopieras till XCode-projektets **Resources** -katalog (till exempel &quot;platforms/ios/Geometrixx/Resources/ADBMobileConfig.json&quot;). Om appen har Android™ som mål är sökvägen&quot;platforms/android/assets/ADBMobileConfig.json&quot;. Mer information om hur du använder kopplingar under PhoneGap CLI-bygget finns i [Tre kopplingar som ditt Cordova-/PhoneGap-projekt behöver](https://gist.github.com/jlcarvalho/22402d013bc72f795d45a01836ce735c).

```xml
///////////////////////////
//          iOS
///////////////////////////
    ios : [
        {
            "www/ADBMobileConfig.json": "platforms/ios/<YOUR_APP_NAME>/Resources/ADBMobileConfig.json"
        }
    ],
///////////////////////////
//          ANDROID
///////////////////////////
    android: [
        {
            "www/ADBMobileConfig.json": "platforms/android/assets/ADBMobileConfig.json"
        }
    ]
```

### Lägg till plugin-programmet AMS i appen {#add-the-ams-plugin-in-the-app}

För att appen ska kunna samla in data måste plugin-programmet för Adobe Mobile Services (AMS) ingå i appen. Genom att ta med plugin-programmet som en funktion i programmets config.xml kan en annan Cordova-krok användas för att automatiskt lägga till plugin-programmet under PhoneGap-byggprocessen.

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

Geometrixx Outdoors App config.xml finns på */content/phonegap/geometrixx-outdoor/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*. I exemplet ovan efterfrågas en specifik version av plugin-programmet som ska användas genom att ett &#39;#&#39; läggs till och sedan ett taggvärde efter plugin-URL:en. Det här är en bra metod att följa för att se till att oväntade problem inte uppstår på grund av att otestade plugin-program läggs till under ett bygge.

När du har utfört dessa steg aktiveras appen för att rapportera alla livscykelvärden som tillhandahålls av Adobe Analytics. Detta inkluderar data som starter, krascher och installationer. Om det är den enda informationen du bryr dig om, så är du klar. Om du vill samla in anpassade data måste du mäta koden.

### Instrumentera koden för fullständig appspårning {#instrument-your-code-for-full-app-tracking}

Det finns flera spårnings-API:er i API:t för [AMS PhoneGap Plugin.](https://github.com/Adobe-Marketing-Cloud/mobile-services/blob/master/docs/ios/phonegap/phonegap-methods.md)

På så sätt kan du spåra lägen och åtgärder, t.ex. var sidor användarna navigerar till i appen, vilka kontroller som används mest. Det enklaste sättet att mäta hur appen fungerar för spårning är att använda Analytics-API:erna som finns i AMS-pluginen.

* ADB.trackState()
* ADB.trackAction()

Titta på koden i appen Geometrixx Outdoors. I appen Geometrixx Outdoors spåras all sidnavigering med metoden ADB.trackState(). Mer information finns i källkoden för /libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js

Genom att instrumentera källkoden med dessa metodanrop kan du samla in fullständiga mätvärden mot programmet.

#### Egenskaper för anslutning till AMS {#properties-for-connecting-to-ams}

*com.adobe.cq.moMobile.mobileservices.impl.service.MobileServicesHttpClientImp* l visar följande egenskaper för anslutning till AMS:

| **Etikett** | **Beskrivning** | **Standard** |
|---|---|---|
| API-slutpunkt | Bas-URL:en för Adobe Mobile Services HTTP API:er | https://api.omniture.com |
| Konfig. slutpunkt | Den URL som används för att hämta ADB Mobile Config för det angivna rapportsvitens-ID:t | /ams/1.0/app/config/ |
| Appar för mobiltjänster | Få en lista över appar i användarföretaget | /ams/1.0/apps |
