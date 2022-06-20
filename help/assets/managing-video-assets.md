---
title: Hantera videoresurser
description: Överföra, förhandsgranska, kommentera och publicera videomaterial i [!DNL Adobe Experience Manager].
contentOwner: AG
role: User
feature: Asset Management
exl-id: 21d3e0bd-5955-470a-8ca2-4d995c17eb4c
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 9%

---

# Hantera videoresurser {#manage-video-assets}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-video-assets.html?lang=en) |
| AEM 6.5 | Den här artikeln |
| AEM 6.4 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/managing-video-assets.html?lang=en) |

Videoformatet är en viktig del av ett företags digitala resurser. [!DNL Adobe Experience Manager] erbjuder mogna erbjudanden och funktioner för att hantera hela livscykeln för videomaterialet när de har skapats.

Lär dig hantera och redigera videomaterialet i [!DNL Adobe Experience Manager Assets]. Videokodning och omkodning, till exempel FFmpeg-omkodning, är möjlig med [!DNL Dynamic Media] integrering.

## Överföra och förhandsgranska videomaterial {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] skapar förhandsvisningar för videoresurser med filnamnstillägget MP4. Om resursens format inte är MP4 installerar du FFmpeg-paketet för att generera en förhandsvisning. FFmpeg skapar videoåtergivningar av typen OGG och MP4. Du kan förhandsgranska återgivningarna i [!DNL Assets] användargränssnitt.

1. Navigera till den plats där du vill lägga till digitala resurser i mappen eller undermapparna för digitala resurser.
1. Om du vill överföra resursen klickar du på **[!UICONTROL Create]** i verktygsfältet och välj **[!UICONTROL Files]**. Du kan också dra en fil till användargränssnittet. Se [överföra resurser](manage-assets.md#uploading-assets) för mer information.
1. Om du vill förhandsgranska en video i kortvyn klickar du på **[!UICONTROL Play]** ![uppspelningsalternativ](assets/do-not-localize/play.png) på videoresursen. Du kan bara pausa eller spela upp video i kortvyn. The [!UICONTROL Play] och [!UICONTROL Pause] alternativen är inte tillgängliga i listvyn.

1. Om du vill förhandsgranska videon på sidan med resursinformation klickar du på **[!UICONTROL Edit]** på kortet. Videon spelas upp i webbläsarens inbyggda videospelare. Du kan spela upp, pausa, styra volymen och zooma videon till helskärm.

   ![Videouppspelningskontroller](assets/video-playback-controls.png)

## Konfiguration för att överföra resurser som är större än 2 GB {#configuration-to-upload-assets-that-are-larger-than-gb}

Som standard [!DNL Assets] gör att du inte kan överföra resurser som är större än 2 GB på grund av en filstorleksgräns. Du kan dock skriva över den här gränsen genom att gå till CRXDE Lite och skapa en nod under `/apps` katalog. Noden måste ha samma nodnamn, katalogstruktur och jämförbara nodegenskaper i ordningen.

Förutom [!DNL Assets] ändrar du följande konfigurationer för att överföra stora resurser:

* Öka tokens förfallotid. Se [!UICONTROL Adobe Granite CSRF Servlet] i webbkonsolen på `https://[aem_server]:[port]/system/console/configMgr`. Mer information finns i [CSRF-skydd](/help/sites-developing/csrf-protection.md).
* Öka `receiveTimeout` i Dispatcher-konfiguration. Mer information finns i [Experience Manager Dispatcher-konfiguration](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options).

>[!NOTE]
>
>The [!DNL Experience Manager] Klassiskt användargränssnitt har ingen begränsning för filstorlek på 2 GB. Slutgiltigt arbetsflöde för stor video stöds inte heller helt.

Om du vill konfigurera en större filstorleksgräns utför du följande steg i `/apps` katalog.

1. I [!DNL Experience Manager], klicka **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. I CRXDE Lite går du till `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. Om du vill visa katalogfönstret klickar du på `>>`.
1. I verktygsfältet klickar du på **[!UICONTROL Overlay Node]**. Du kan också välja **[!UICONTROL Overlay Node]** på snabbmenyn.
1. I dialogrutan **[!UICONTROL Overlay Node]** klickar du på **[!UICONTROL OK]**.

   ![Överläggsnod](assets/overlay-node-path.png)

1. Uppdatera webbläsaren. Överläggsnoden `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` är markerat.
1. I **[!UICONTROL Properties]** anger du ett värde i byte för att öka storleksgränsen till önskad storlek. Om du till exempel vill öka storleksgränsen till 30 GB anger du `32212254720` värde.

1. Klicka på **[!UICONTROL Save All]** i verktygsfältet.
1. I [!DNL Experience Manager], klicka **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. På [!DNL Adobe Experience Manager] [!UICONTROL Web Console Bundles] under kolumnen Namn i tabellen letar du upp och klickar på **[!UICONTROL Adobe Granite Workflow External Process Job Handler]**.
1. På [!UICONTROL Adobe Granite Workflow External Process Job Handler] sida, ange sekunder för båda **[!UICONTROL Default Timeout]** och **[!UICONTROL Max Timeout]** fält till `18000` (fem timmar). Klicka på **[!UICONTROL Save]**.
1. I [!DNL Experience Manager], klicka **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. På sidan Arbetsflödesmodeller väljer du **[!UICONTROL Dynamic Media Encode Video]** och sedan klicka **[!UICONTROL Edit]**.
1. Dubbelklicka på arbetsflödessidan **[!UICONTROL Dynamic Media Video Service Process]** -komponenten.
1. I dialogrutan [!UICONTROL Step Properties], på fliken **[!UICONTROL Common]**, expanderar du **Avancerade inställningar**.
1. I **[!UICONTROL Timeout]** fält, ange ett värde för `18000`och sedan klicka **[!UICONTROL OK]** för att gå tillbaka till **[!UICONTROL Dynamic Media Encode Video]** arbetsflödessida.
1. Nära sidans överkant, under [!UICONTROL Dynamic Media Encode Video] sidrubrik, klicka **[!UICONTROL Save]**.

## Publicera videomaterial {#publish-video-assets}

Efter publiceringen kan du inkludera videomaterialet på en webbsida som en URL eller bädda in resurserna direkt. Mer information finns i [publicera Dynamic Media-resurser](/help/assets/publishing-dynamicmedia-assets.md).

## Kommentera videomaterial {#annotate-video-assets}

1. Från [!DNL Assets] konsol, välj **[!UICONTROL Edit]** på tillgångskortet för att visa sidan med tillgångsinformation.
1. Om du vill spela upp videon klickar du på **[!UICONTROL Preview]**.
1. Om du vill kommentera videon klickar du på **[!UICONTROL Annotate]**. En anteckning läggs till vid en viss tidpunkt (bildruta) i videon. När du gör anteckningar kan du rita på arbetsytan och ta med en kommentar med ritningen. Kommentarerna sparas automatiskt. Om du vill avsluta anteckningsguiden klickar du på **[!UICONTROL Close]**.

   ![Rita och kommentera i en videobildruta](assets/annotate-video.png)

1. Gå till en viss punkt i videon, ange tiden i sekunder i **textfältet** och klicka på **Hoppa**. Om du till exempel vill hoppa över de första 20 sekunderna av videon anger du 20 i textfältet.

   ![Söka efter en tid i en video att hoppa över med angivna sekunder](assets/seek-in-video.png)

1. Klicka på en anteckning om du vill visa den i tidslinjen. Om du vill ta bort anteckningen från tidslinjen klickar du på **[!UICONTROL Delete]**.

   ![Visa anteckningar och detaljer på tidslinjen](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [Hantera digitala resurser i Experience Manager Assets](/help/assets/manage-assets.md)
>* [Hantera samlingar i Experience Manager Assets](/help/assets/manage-collections.md)
>* [Dynamic Media videodokumentation](/help/assets/video.md).

