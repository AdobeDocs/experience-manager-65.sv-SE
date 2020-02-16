---
title: Utveckla mobilprogram i AEM
seo-title: Utveckla mobilprogram i AEM
description: Följ den här sidan när du vill börja utveckla mobilprogram i AEM med Adobe PhoneGap Enterprise.
seo-description: Följ den här sidan när du vill börja utveckla mobilprogram i AEM med Adobe PhoneGap Enterprise.
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Utveckla mobilprogram i AEM {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (t.ex. Reagera). [Läs mer](/help/sites-developing/spa-overview.md).

AEM utnyttjar Adobe PhoneGap och Adobe Publishing Solutions så att du kan skapa och hantera både innehållsrika och verktygsbaserade, plattformsoberoende mobilappar:

* Hantera alla era företagsappar på ett och samma ställe.
* Granska appar i utvecklings- och staging-miljöer utan de komplexa provisioneringsprofilerna och den extra ansträngningen att skapa och överföra din app för delning.
* Använd AEM-utvecklingsmiljön för att skapa och hantera avancerat innehåll för dina appar.
* Använd HTML5 med Adobe PhoneGap för att skapa engagerande upplevelser med enhetsspecifika funktioner.
* Lägg in HTML5-webbvisningar i nya eller befintliga **inbyggda** applikationer via Cordova WebViews.
* Skapa, strukturera och dela multimediematerial i alla kanaler, inklusive webben, mobilsajter, mobilappar och tryck.

AEM integreras med tjänsten **[Adobe](https://build.phonegap.com/)**PhoneGap Build för att förenkla processen för programbygge och driftsättning.

**Med Adobe ContentSync** kan användare enkelt hämta sidor och innehållsuppdateringar Over-the-Air (OTA) till sina enheter utan att behöva installera om programmet eller hämta det från appStore, Google Play eller andra appkällor.

**Adobe Analytics** är helintegrerat i AEM-appar och möjliggör detaljerad spårning av distribution, geopositionering, operativsystem, enheter, klickströmmar, iBeacon-spårning med mera.

## Skapa appar {#creating-apps}

Utvecklare kan använda [AEM PhoneGap Starter Kit](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) tillsammans med ytterligare resurser som finns i [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) för att starta AEM-program med PhoneGap, inklusive en intern referensapp som kör Cordova-webbvyer.

Viktigt om Git-databasen för Starter Kit innehåller en självstudiekurs om hur du använder startpaketet:

* Anpassa varumärket
* Mål för Maven-exempelbygge och -driftsättning
* Konfiguration av källkontrollsdatabas
* Installera och distribuera i lokala eller fjärranslutna AEM-instanser
* Avinstallera från AEM

>[!NOTE]
>
>Ytterligare referensimplementeringskälla, inklusive labb, finns på GitHub [här](https://github.com/adobe-marketing-cloud-apps) och &quot;köksink&quot; [här](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## Utveckla för IOS 9- och HTTP-värdar {#developing-for-ios-and-http-hosts}

IOS-utvecklare bör vara medvetna om ett öppet problem med Cordova-appar som körs på iOS 9. Det här problemet förhindrar att förfrågningar görs till osäkra värdar (till exempel *http://localhost:4502*). Problemet kommer att lösas med en kommande version av cordova-ios (som Cordova CLI konsumerar), men under tiden finns det två tillfälliga lösningar:

1. Som en omedelbar lösning kan du fortfarande använda någon av iOS 8-simulatorerna utan problem.
1. Om du måste använda iOS 9 kan din app -Info.plist (som du hittar när du har kört `cordova platform add ios` i filen &lt;app root>/platforms/ios/&lt;app name>/&lt;app name>-Info.plist&quot;) redigeras manuellt för att inkludera följande egenskap:

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>Mer information om&quot;App Transport Security&quot; finns i följande avsnitt i [Apples prerelease-dokument](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) för iOS9 och i denna [Stack Overflow-diskussion](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/).

## Utveckla mobilprogram i AEM {#developing-mobile-applications-in-aem-1}

* [Startar AEM PhoneGap](/help/mobile/starting-aem-phonegap-app.md)
* [Bygger mobilprogram](/help/mobile/building-app-mobile-phonegap.md)
* [Strukturera ett program](/help/mobile/phonegap-structure-an-app.md)
* [Skapa och redigera appar med Apps-konsolen](/help/mobile/phonegap-apps-console.md)
* [Enkelsidiga program](/help/mobile/phonegap-single-page-applications.md)
* [Utveckla appar med PhoneGap CLI](/help/mobile/phonegap-apps-pg-cli.md)
* [Åtkomst till enhetsfunktioner](/help/mobile/phonegap-access-device-features.md)
* [Spåra appprestanda med Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
* [Lägg till Adobe Analytics i er mobilapplikation](/help/mobile/phonegap-add-analytics-to-apps.md)
* [Push-meddelanden](/help/mobile/phonegap-push-notifications.md)
* [AEM Mobile-innehållspersonalisering](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [The Anatomy of an App](/help/mobile/phonegap-apps-arch.md)
* [Är din hybridapp redo för AEM Mobile?](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Additional Resources {#additional-resources}

Mer information om roller och ansvar för en administratör och utvecklare finns i resurserna nedan:

* [Om du skriver för Adobe PhoneGap Enterprise med AEM](/help/mobile/phonegap.md)
* [Administrera innehåll för Adobe PhoneGap Enterprise med AEM](/help/mobile/administer-phonegap.md)
