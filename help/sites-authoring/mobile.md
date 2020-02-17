---
title: Skapa en sida för mobila enheter
seo-title: Skapa en sida för mobila enheter
description: När du skapar för mobilen kan du växla mellan flera emulatorer för att se vad slutanvändaren ser
seo-description: När du skapar för mobilen kan du växla mellan flera emulatorer för att se vad slutanvändaren ser
uuid: a7a1ba68-d608-4819-88d1-0dab5955d3f4
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 9554cdb3-b604-4d50-9760-89b9e7a7755f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Skapa en sida för mobila enheter{#authoring-a-page-for-mobile-devices}

När du skapar en mobilsida visas sidan på ett sätt som emulerar den mobila enheten. När du skapar sidan kan du växla mellan flera emulatorer för att se vad slutanvändaren ser när han/hon öppnar sidan.

Enheterna grupperas i kategorierna, funktion, smart och touchfunktion enligt enhetens funktioner för att återge en sida. När slutanvändaren öppnar en mobilsida upptäcker AEM enheten och skickar den representation som motsvarar enhetsgruppen.

>[!NOTE]
>
>Om du vill skapa en mobilwebbplats baserad på en befintlig standardwebbplats skapar du en live-kopia av standardwebbplatsen. (Se [Skapa en Live-kopia för olika kanaler](/help/sites-administering/msm-livecopy.md).)
>
>AEM-utvecklare kan skapa nya enhetsgrupper. (Se [Skapa enhetsgruppsfilter](/help/sites-developing/groupfilters.md).)

Använd följande procedur för att skapa en mobilsida:

1. Öppna konsolen **Platser** från global navigering.
1. Öppna sidan **We.Retail** -> **United States** -> **English**.

1. Växla till **förhandsvisningsläget** .
1. Växla till önskad emulator genom att klicka på enhetsikonen högst upp på sidan.
1. Dra och släpp komponenter från komponentwebbläsaren till sidan.

Sidan ser ut ungefär så här:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Emulatorerna inaktiveras när en sida på författarinstansen begärs från en mobilenhet.

