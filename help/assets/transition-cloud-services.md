---
title: Använd översättningsmolntjänster på mappar
description: Använd översättningsmolntjänster på mappar
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 45%

---


# Använd översättningsmolntjänster på mappar {#applying-translation-cloud-services-to-folders}

[!DNL Adobe Experience Manager] Med kan du använda molnbaserade översättningstjänster från den översättningsleverantör som du väljer för att se till att dina resurser översätts baserat på dina behov.

Du kan använda översättningsmolntjänsten direkt i resursmappen så att den kan användas under översättningsarbetsflöden.

## Använd översättningstjänsterna {#applying-the-translation-services}

Genom att använda översättningsmolntjänster direkt i resursmappen behöver du inte konfigurera översättningstjänster när du skapar eller uppdaterar översättningsarbetsflöden.

1. I [!DNL Assets]-användargränssnittet väljer du den mapp som du vill använda översättningstjänster på.
1. Klicka på **[!UICONTROL Properties]** i verktygsfältet för att visa sidan **[!UICONTROL Folder Properties]**.

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. Navigera till fliken **[!UICONTROL Cloud Services]**.
1. I listan Cloud Service Configurations väljer du önskad översättningsleverantör. Om du till exempel vill använda översättningstjänster från Microsoft väljer du **[!UICONTROL Microsoft Translator]**.

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. Välj koppling för översättningsprovidern.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Klicka på **[!UICONTROL Save]** i verktygsfältet och klicka sedan på **[!UICONTROL OK]** för att stänga dialogrutan. Översättningstjänsten tillämpas på mappen.

## Använd anpassad översättningskoppling {#applying-custom-translation-connector}

Du kan använda en anpassad koppling för de översättningstjänster som du vill använda i översättningsarbetsflöden. Om du vill använda en anpassad koppling måste du först installera kopplingen från pakethanteraren. Konfigurera sedan kopplingen från Cloud Services-konsolen. När du har konfigurerat kopplingen är den tillgänglig i listan över kopplingar på fliken Cloud Services som beskrivs i [Använda översättningstjänsterna](transition-cloud-services.md#applying-the-translation-services). När du har använt den anpassade kopplingen och kört översättningsarbetsflödena visas kopplingsinformationen under rubrikerna **[!UICONTROL Provider]** och **[!UICONTROL Method]** i rutan **[!UICONTROL Translation Summary]** för översättningsprojektet.

1. Installera kopplingen från Package Manager.
1. Klicka på logotypen [!DNL Experience Manager] och navigera till **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Cloud Services]**.
1. Leta upp den koppling du installerade under **[!UICONTROL Third Party Services]** på sidan **[!UICONTROL Cloud Services]**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. Klicka på länken **[!UICONTROL Configure now]** för att öppna dialogrutan **[!UICONTROL Create Configuration]**.

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Ange en titel och ett namn för kopplingen och klicka sedan på **[!UICONTROL Create]**. Den anpassade kopplingen finns i listan över kopplingar på fliken **[!UICONTROL Cloud Services]** som beskrivs i steg 5 i [Använda översättningstjänsterna](#applying-the-translation-services).
1. Kör ett översättningsarbetsflöde som beskrivs i [Skapa översättningsprojekt](translation-projects.md) när du har använt den anpassade kopplingen. Kontrollera informationen om kopplingen i rutan **[!UICONTROL Translation Summary]** för översättningsprojektets på konsolen **[!UICONTROL Projects]**.

   ![chlimage_1-220](assets/chlimage_1-220.png)
