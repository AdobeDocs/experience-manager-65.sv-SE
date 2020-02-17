---
title: Skapa en sida för mobila enheter
seo-title: Skapa en sida för mobila enheter
description: När du skapar en mobilsida visas sidan på ett sätt som emulerar den mobila enheten. När du skapar sidan kan du växla mellan flera emulatorer för att se vad slutanvändaren ser när han/hon öppnar sidan.
seo-description: När du skapar en mobilsida visas sidan på ett sätt som emulerar den mobila enheten. När du skapar sidan kan du växla mellan flera emulatorer för att se vad slutanvändaren ser när han/hon öppnar sidan.
uuid: ca16979d-6e5f-444d-b959-ae92542039b2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 430a27b5-f344-404f-8bf8-0d91b49b605e
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
>AEM-utvecklare kan skapa nya enhetsgrupper. (Se [Skapa enhetsgruppsfilter.](/help/sites-developing/groupfilters.md))

Använd följande procedur för att skapa en mobilsida:

1. Gå till **SiteAdmin** Console i webbläsaren.
1. Öppna sidan **Produkter** nedan **Webbplatser** > **Geometrixx Mobile Demo Site** >> **English**.

1. Växla till en annan emulator. Om du vill göra det kan du antingen:

   * Klicka på enhetsikonen högst upp på sidan.
   * Klicka på knappen **Redigera** i **sidosparken** och välj enheten i listrutan.

1. Dra och släpp **text- och bildkomponenten** från fliken Mobil i sidsparken till sidan.
1. Redigera komponenten och lägg till text. Spara ändringarna genom att klicka på **OK** .

Sidan ser ut på samma sätt som följande:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Emulatorerna inaktiveras när en sida på författarinstansen begärs från en mobilenhet. Du kan sedan skapa med hjälp av det pekaktiverade användargränssnittet.

