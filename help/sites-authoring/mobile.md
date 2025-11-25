---
title: Skapa en innehållssida för mobila enheter
description: När du skapar för mobilen kan du växla mellan flera emulatorer för att se vad slutanvändaren ser.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 9c6c6386-5ffd-4fa6-9aa1-f5b0e31d1046
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Skapa en sida för mobila enheter{#authoring-a-page-for-mobile-devices}

När du skapar en mobilsida visas sidan på ett sätt som emulerar den mobila enheten. När du redigerar sidan kan du växla mellan flera emulatorer för att se vad slutanvändaren ser när han/hon öppnar sidan.

Enheterna grupperas i kategorierna, funktion, smart och touchfunktion enligt enhetens funktioner för att återge en sida. När slutanvändaren kommer åt en mobilsida identifierar AEM enheten och skickar den representation som motsvarar enhetsgruppen.

>[!NOTE]
>
>Om du vill skapa en mobilwebbplats baserad på en befintlig standardwebbplats skapar du en live-kopia av standardwebbplatsen. (Se [Skapa en Live-kopia för olika kanaler](/help/sites-administering/msm-livecopy.md).)
>
>AEM-utvecklare kan skapa nya enhetsgrupper. (Se [Skapa enhetsgruppsfilter](/help/sites-developing/groupfilters.md).)

Använd följande procedur för att skapa en mobilsida:

1. Öppna konsolen **Platser** från global navigering.
1. Öppna sidan **We.Retail** > **United States** > **English**.

1. Växla till läget **Förhandsgranska**.
1. Växla till önskad emulator genom att klicka på enhetsikonen högst upp på sidan.
1. Dra och släpp komponenter från komponentwebbläsaren till sidan.

Sidan ser ut ungefär så här:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Emulatorerna inaktiveras när en sida på författarinstansen begärs från en mobilenhet.
