---
title: Använda förinställningar för Dynamic Media-bilder
description: Lär dig hur du använder bildförinställningar i Dynamic Media
uuid: 8bafcbd0-6df0-4d5b-b2f7-116ddb4ec060
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 5c1f60ac-3741-4002-9c5d-c128f118342b
translation-type: tm+mt
source-git-commit: fed2e6474f710fd02cf27946252896ac33f3b256
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 12%

---


# Använda förinställningar för Dynamic Media-bilder {#applying-image-presets}

Med bildförinställningar kan resurser dynamiskt leverera bilder i olika storlekar, i olika format eller med andra bildegenskaper som genereras dynamiskt. Du kan välja en förinställning när du exporterar bilder. Då formateras bilderna också om till de specifikationer som administratören har angett.

Du kan dessutom välja en bildförinställning som är responsiv (anges av knappen när du har valt den). **[!UICONTROL RESS]**

I det här avsnittet beskrivs hur du använder bildförinställningar. [Administratörer kan skapa och konfigurera bildförinställningar](managing-image-presets.md).

>[!NOTE]
>
>Smart bildbehandling fungerar med befintliga bildförinställningar och använder intelligens under de sista millisekunderna i leveransen för att ytterligare minska bildfilens storlek baserat på webbläsarens eller nätverkets anslutningshastighet. Mer information finns i [Smart](imaging-faq.md) Imaging.

Du kan använda en bildförinställning på en bild när du vill förhandsvisa den.

>[!NOTE]
>
>I Dynamic Media - Scene7-läget stöds endast bildförinställningar för bildresurser.

**Använda förinställningar för dynamiska mediabilder**

1. Öppna resursen och tryck på den nedrullningsbara menyn till vänster och tryck sedan på **[!UICONTROL Renditions.]**

   >[!NOTE]
   >
   >* Statiska återgivningar visas i den övre halvan av rutan. Dynamiska återgivningar visas i den nedre halvan. Om du bara använder dynamiska återgivningar kan du använda URL-adressen för att visa bilden. Knappen visas bara om du väljer en dynamisk återgivning. **[!UICONTROL URL]** Knappen visas bara om du väljer en förinställning för responsiv bild. **[!UICONTROL RESS]**
      >
      >
   * Systemet visar flera återgivningar när du väljer **[!UICONTROL Renditions]** i detaljvyn för en resurs. Du kan öka antalet förinställningar som visas. See [Increasing the number of image presets that display](managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display).


   ![chlimage_1-208](assets/chlimage_1-208.png)

1. Gör något av följande:

   * Välj en dynamisk återgivning om du vill förhandsgranska bildförinställningen.
   * Tryck **[!UICONTROL URL]**, **[!UICONTROL Embed]** eller **[!UICONTROL RESS]** så visas popup-fönstret.

   >[!NOTE]
   >
   >Om resursen *och* bildförinställningen ännu inte har publicerats är knappen **[!UICONTROL URL]** (eller knapparna **[!UICONTROL URL]** och **[!UICONTROL RESS]**, i förekommande fall) inte tillgängliga.
   >
   >Observera också att bildförinställningar automatiskt publiceras på en Dynamic Media S7-server.

