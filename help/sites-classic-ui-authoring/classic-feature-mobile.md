---
title: Skapa en sida för mobila enheter
description: När du skapar en mobilsida visas sidan på ett sätt som emulerar den mobila enheten. När du redigerar sidan kan du växla mellan flera emulatorer för att se vad slutanvändaren ser när han/hon öppnar sidan.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: d5372474-d8aa-4e64-919d-0bd29ba99d99
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# Skapa en sida för mobila enheter{#authoring-a-page-for-mobile-devices}

När du skapar en mobilsida visas sidan på ett sätt som emulerar den mobila enheten. När du redigerar sidan kan du växla mellan flera emulatorer för att se vad slutanvändaren ser när han/hon öppnar sidan.

Enheterna grupperas i kategorierna, funktion, smart och touchfunktion enligt enhetens funktioner för att återge en sida. När slutanvändaren öppnar en mobilsida upptäcker AEM enheten och skickar den representation som motsvarar enhetsgruppen.

>[!NOTE]
>
>Om du vill skapa en mobilwebbplats baserad på en befintlig standardwebbplats skapar du en live-kopia av standardwebbplatsen. (Se [Skapa en Live-kopia för olika kanaler](/help/sites-administering/msm-livecopy.md).)
>
>AEM kan skapa nya enhetsgrupper. (Se [Skapa enhetsgruppsfilter.](/help/sites-developing/groupfilters.md))

Använd följande procedur för att skapa en mobilsida:

1. Gå till konsolen **SiteAdmin** i webbläsaren.
1. Öppna sidan **Produkter** nedan **Webbplatser** >> **Geometrixx Mobile Demo Site** >> **English**.

1. Växla till en annan emulator. Om du vill göra det kan du antingen:

   * Klicka på enhetsikonen högst upp på sidan.
   * Klicka på knappen **Redigera** i **Sidekick** och markera enheten i listrutan.

1. Dra och släpp komponenten **Text och bild** från fliken Mobil i Sidekick till sidan.
1. Redigera komponenten och lägg till text. Klicka på **OK** för att spara ändringarna.

Sidan ser ut på samma sätt som följande:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Emulatorerna inaktiveras när en sida på författarinstansen begärs från en mobilenhet. Du kan sedan skapa med hjälp av det pekaktiverade användargränssnittet.
