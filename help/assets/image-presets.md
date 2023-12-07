---
title: Använd Dynamic Media-bildförinställningar
description: Lär dig hur du kan aktivera resurser för att dynamiskt kunna leverera bilder i olika storlekar, i olika format eller med andra bildegenskaper som genereras dynamiskt.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Image Presets
role: User,Admin
exl-id: 98d88b59-eb8f-42db-abb8-04506a5b8c30
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 3%

---

# Använda förinställningar för Dynamic Media-bilder {#applying-image-presets}

Med bildförinställningar kan resurser dynamiskt leverera bilder i olika storlekar, i olika format eller med andra bildegenskaper som genereras dynamiskt. Du kan välja en förinställning när du exporterar bilder. I förinställningen formateras bilderna om enligt de specifikationer som administratören har angett.

Dessutom kan du välja en bildförinställning som är responsiv (anges av **[!UICONTROL RESS]** när du har valt den).

I det här avsnittet beskrivs hur du använder bildförinställningar. [Administratörer kan skapa och konfigurera bildförinställningar](managing-image-presets.md).

>[!NOTE]
>
>Smart bildbehandling fungerar med befintliga bildförinställningar och använder intelligens under de sista millisekunderna i leveransen för att ytterligare minska bildfilens storlek baserat på webbläsarens eller nätverkets anslutningshastighet. Se [Smart bildbehandling](imaging-faq.md) för mer information.

Du kan använda en bildförinställning på en bild när du vill förhandsvisa den.

>[!NOTE]
>
>I Dynamic Media - Scene7-läget stöds endast bildförinställningar för bildresurser.

**Så här använder du Dynamic Media-bildförinställningar:**

1. Öppna resursen och välj den nedrullningsbara menyn i den vänstra listen och välj **[!UICONTROL Renditions]**.

   >[!NOTE]
   >
   >* Statiska återgivningar visas i den övre halvan av rutan. Dynamiska återgivningar visas i den nedre halvan. Om du bara använder dynamiska återgivningar kan du använda URL-adressen för att visa bilden. The **[!UICONTROL URL]** visas bara om du väljer en dynamisk återgivning. The **[!UICONTROL RESS]** visas bara om du väljer en förinställning för responsiv bild.
   >
   >* Systemet visar flera renderingar när du väljer **[!UICONTROL Renditions]** i en tillgångs detaljvy. Du kan öka antalet förinställningar som visas. Se [Öka antalet bildförinställningar som visas](managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display).

   ![chlimage_1-208](assets/chlimage_1-208.png)

1. Gör något av följande:

   * Välj en dynamisk återgivning så att du kan förhandsgranska bildförinställningen.
   * Om du vill visa popup-fönstret väljer du **[!UICONTROL URL]**, **[!UICONTROL Embed]**, eller **[!UICONTROL RESS]**.

   >[!NOTE]
   >
   >Om tillgången *och* bildförinställningen ännu inte publiceras, **[!UICONTROL URL]** knapp (eller **[!UICONTROL URL]** och **[!UICONTROL RESS]** (om tillämpligt) är inte tillgängliga.
   >
   >Observera också att bildförinställningar automatiskt publiceras på en Dynamic Media-server.
