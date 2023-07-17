---
title: Åtkomst till enhetsfunktioner
description: Följ den här sidan om du vill veta mer om hur du skapar Adobe Experience Manager-komponenter (AEM) som använder enhetsfunktioner. AEM PhoneGap Kitchen Sink GitHub-databas ger utvecklare en funktionell AEM som illustrerar användningen av flera Cordova API:er.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 385f7924-e8ab-4dcb-83f0-7b81bead3dda
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# Åtkomst till enhetsfunktioner{#access-device-features}

>[!NOTE]
>
>Adobe rekommenderar att du använder SPA Editor för projekt som kräver ramverksbaserad klientåtergivning för en sida (till exempel React). [Läs mer](/help/sites-developing/spa-overview.md).

## Skapa Adobe Experience Manager-komponenter (AEM) som har åtkomst till enhetsfunktioner {#building-aem-components-that-access-device-features}

The [AEM PhoneGap Kitchen Sink](https://github.com/blefebvre/aem-phonegap-kitchen-sink) GitHub-databasen ger utvecklare en funktionell AEM som visar hur flera Cordova API:er används. När appen körs på iOS eller Android™ via PhoneGap CLI öppnas den på följande sida, som innehåller en länk till varje enhets-API som visas:

![chlimage_1-107](assets/chlimage_1-107.png)

Källkoden för var och en av dessa enhets-API-komponenter är [finns på GitHub](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/apps/brucelefebvre/kitchen-sink/components).

Mer information om hur respektive API används finns i dokumentationen för Cordova-pluginprogrammet (`https://docs.phonegap.com/en/4.0.0/cordova_plugins_pluginapis.md.html`).

## Nästa steg {#the-next-steps}

Se [Spåra appprestanda med Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md).
