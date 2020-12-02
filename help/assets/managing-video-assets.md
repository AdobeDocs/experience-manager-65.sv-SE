---
title: Hantera videoresurser
description: Överför, förhandsgranska, kommentera och publicera videomaterial i [!DNL Adobe Experience Manager].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 8%

---


# Hantera videoresurser {#manage-video-assets}

Videoformatet är en viktig del av ett företags digitala resurser. [!DNL Adobe Experience Manager] erbjuder mogna erbjudanden och funktioner för att hantera hela livscykeln för videomaterialet när de har skapats.

Lär dig hur du hanterar och redigerar videoresurserna i [!DNL Adobe Experience Manager Assets]. Videokodning och transkodning, till exempel FFmpeg-transkodning, är möjlig med [!DNL Dynamic Media]-integrering.

## Överför och förhandsgranska videomaterial {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] skapar förhandsvisningar för videoresurser med filnamnstillägget MP4. Om resursens format inte är MP4 installerar du FFmpeg-paketet för att generera en förhandsvisning. FFmpeg skapar videoåtergivningar av typen OGG och MP4. Du kan förhandsgranska återgivningarna i [!DNL Assets]-användargränssnittet.

1. Navigera till den plats där du vill lägga till digitala resurser i mappen eller undermapparna för digitala resurser.
1. Om du vill överföra resursen klickar du på **[!UICONTROL Create]** i verktygsfältet och väljer **[!UICONTROL Files]**. Du kan också dra en fil till användargränssnittet. Mer information finns i [överföra resurser](manage-assets.md#uploading-assets).
1. Om du vill förhandsgranska en video i kortvyn klickar du på **[!UICONTROL Play]** ![uppspelningsalternativet](assets/do-not-localize/play.png) i videoresursen. Du kan bara pausa eller spela upp video i kortvyn. Alternativen [!UICONTROL Play] och [!UICONTROL Pause] är inte tillgängliga i listvyn.

1. Om du vill förhandsgranska videon på sidan med resursinformation klickar du på **[!UICONTROL Edit]** på kortet. Videon spelas upp i webbläsarens inbyggda videospelare. Du kan spela upp, pausa, styra volymen och zooma videon till helskärm.

   ![Videouppspelningskontroller](assets/video-playback-controls.png)

## Konfiguration för att överföra resurser som är större än 2 GB {#configuration-to-upload-assets-that-are-larger-than-gb}

Som standard kan du inte överföra resurser som är större än 2 GB med [!DNL Assets] eftersom filstorleken är begränsad. Du kan dock skriva över den här gränsen genom att gå till CRXDE Lite och skapa en nod under katalogen `/apps`. Noden måste ha samma nodnamn, katalogstruktur och jämförbara nodegenskaper i ordningen.

Förutom [!DNL Assets]-konfigurationen kan du ändra följande konfigurationer för att överföra stora resurser:

* Öka tokens förfallotid. Se [!UICONTROL Adobe Granite CSRF Servlet] i webbkonsolen på `https://[aem_server]:[port]/system/console/configMgr`. Mer information finns i [CSRF-skydd](/help/sites-developing/csrf-protection.md).
* Öka `receiveTimeout` i Dispatcher-konfigurationen. Mer information finns i [Experience Manager Dispatcher configuration](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options).

>[!NOTE]
>
>Användargränssnittet [!DNL Experience Manager] Classic har ingen begränsning för filstorlek på 2 GB. Slutgiltigt arbetsflöde för stor video stöds inte heller helt.

Utför följande steg i katalogen `/apps` om du vill konfigurera en större filstorleksgräns.

1. I [!DNL Experience Manager] klickar du på **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. Gå till `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` i CRXDE Lite. Om du vill visa katalogfönstret klickar du på `>>`.
1. Klicka på **[!UICONTROL Overlay Node]** i verktygsfältet. Du kan också välja **[!UICONTROL Overlay Node]** på snabbmenyn.
1. I dialogrutan **[!UICONTROL Overlay Node]** klickar du på **[!UICONTROL OK]**.

   ![Överläggsnod](assets/overlay-node-path.png)

1. Uppdatera webbläsaren. Överläggsnoden `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` är markerad.
1. På fliken **[!UICONTROL Properties]** anger du lämpligt värde i byte för att öka storleksgränsen till önskad storlek. Om du till exempel vill öka storleksgränsen till 30 GB anger du `32212254720`-värdet.

1. Klicka på **[!UICONTROL Save All]** i verktygsfältet.
1. I [!DNL Experience Manager] klickar du på **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. På sidan [!DNL Adobe Experience Manager] [!UICONTROL Web Console Bundles], under kolumnen Namn i tabellen, letar du reda på och klickar på **[!UICONTROL Adobe Granite Workflow External Process Job Handler]**.
1. På sidan [!UICONTROL Adobe Granite Workflow External Process Job Handler] anger du sekunder för både **[!UICONTROL Default Timeout]** och **[!UICONTROL Max Timeout]** fält till `18000` (fem timmar). Klicka på **[!UICONTROL Save]**.
1. I [!DNL Experience Manager] klickar du på **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. Välj **[!UICONTROL Dynamic Media Encode Video]** på sidan Arbetsflödesmodeller och klicka sedan på **[!UICONTROL Edit]**.
1. Dubbelklicka på komponenten **[!UICONTROL Dynamic Media Video Service Process]** på arbetsflödessidan.
1. I dialogrutan [!UICONTROL Step Properties], på fliken **[!UICONTROL Common]**, expanderar du **Avancerade inställningar**.
1. I fältet **[!UICONTROL Timeout]** anger du värdet `18000` och klickar sedan på **[!UICONTROL OK]** för att återgå till arbetsflödessidan för **[!UICONTROL Dynamic Media Encode Video]**.
1. Klicka **[!UICONTROL Save]** nära sidans överkant, under sidtiteln [!UICONTROL Dynamic Media Encode Video].

## Publicera videoresurser {#publish-video-assets}

Efter publiceringen kan du inkludera videomaterialet på en webbsida som en URL eller bädda in resurserna direkt. Mer information finns i [publicera dynamiska medieresurser](/help/assets/publishing-dynamicmedia-assets.md).

## Kommentera videoresurser {#annotate-video-assets}

1. På [!DNL Assets]-konsolen väljer du **[!UICONTROL Edit]** på resurskortet för att visa sidan med resursinformation.
1. Om du vill spela upp videon klickar du på **[!UICONTROL Preview]**.
1. Klicka på **[!UICONTROL Annotate]** om du vill kommentera videon. En anteckning läggs till vid en viss tidpunkt (bildruta) i videon. När du gör anteckningar kan du rita på arbetsytan och ta med en kommentar med ritningen. Kommentarerna sparas automatiskt. Om du vill avsluta anteckningsguiden klickar du på **[!UICONTROL Close]**.

   ![Rita och kommentera i en videobildruta](assets/annotate-video.png)

1. Gå till en viss punkt i videon, ange tiden i sekunder i **textfältet** och klicka på **Hoppa**. Om du till exempel vill hoppa över de första 20 sekunderna av videon anger du 20 i textfältet.

   ![Söka efter en tid i en video att hoppa över med angivna sekunder](assets/seek-in-video.png)

1. Klicka på en anteckning om du vill visa den i tidslinjen. Om du vill ta bort anteckningen från tidslinjen klickar du på **[!UICONTROL Delete]**.

   ![Visa anteckningar och detaljer på tidslinjen](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [Hantera digitala resurser i Experience Manager Assets](/help/assets/manage-assets.md)
>* [Hantera samlingar i Experience Manager Assets](/help/assets/manage-collections.md)
>* [Videodokumentation](/help/assets/video.md) för Dynamic Media.

