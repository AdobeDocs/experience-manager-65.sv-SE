---
title: Använd översättningsmolntjänster på mappar
description: Använd översättningsmolntjänster på mappar
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 42%

---


# Använd översättningsmolntjänster på mappar {#applying-translation-cloud-services-to-folders}

Med Adobe Experience Manager (AEM) kan ni använda molnbaserade översättningstjänster från den översättningsleverantör ni väljer för att se till att era resurser översätts utifrån era behov.

Du kan använda översättningsmolntjänsten direkt i resursmappen så att den kan användas under översättningsarbetsflöden.

## Använda översättningstjänster {#applying-the-translation-services}

Genom att använda översättningsmolntjänster direkt i resursmappen behöver du inte konfigurera översättningstjänster när du skapar eller uppdaterar översättningsarbetsflöden.

1. I Assets-användargränssnittet väljer du den mapp som du vill använda översättningstjänster på.
1. From the toolbar, click the **[!UICONTROL Properties]** icon to display the **[!UICONTROL Folder Properties]** page.

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. Navigera till fliken **[!UICONTROL Cloud Services]**.
1. Välj önskad översättningsleverantör i listan Cloud-tjänstkonfigurationer. Om du till exempel vill använda översättningstjänster från Microsoft väljer du **[!UICONTROL Microsoft Translator]**.

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. Välj koppling för översättningsprovidern.

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. From the toolbar, click **[!UICONTROL Save]**, and then click **[!UICONTROL OK]** to close the dialog.The translation service is applied to the folder.

## Använd anpassad översättningskoppling  {#applying-custom-translation-connector}

Du kan använda en anpassad koppling för de översättningstjänster som du vill använda i översättningsarbetsflöden. Om du vill använda en anpassad koppling måste du först installera kopplingen från pakethanteraren. Konfigurera sedan kopplingen från Cloud Services-konsolen. När du har konfigurerat kopplingen är den tillgänglig i listan över kopplingar på fliken Cloud Services som beskrivs i [Använda översättningstjänsterna](transition-cloud-services.md#applying-the-translation-services). När du har använt den anpassade kopplingen och kört översättningsarbetsflödena visas kopplingsinformationen under rubrikerna **[!UICONTROL Provider]** och **[!UICONTROL Method]** i rutan **[!UICONTROL Translation Summary]** för översättningsprojektet.

1. Installera kopplingen från Package Manager.
1. Click the AEM logo, and navigate to **[!UICONTROL Tools > Deployment > Cloud Services]**.
1. Leta upp den koppling du installerade under **[!UICONTROL Third Party Services]** på sidan **[!UICONTROL Cloud Services]**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. Klicka på **[!UICONTROL Configure now]** länken för att öppna **[!UICONTROL Create Configuration]** dialogrutan.

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Specify a title and a name for the connector, and then click **[!UICONTROL Create]**. Den anpassade kopplingen finns i listan över kopplingar på fliken **[!UICONTROL Cloud Services]** som beskrivs i steg 5 i [Använda översättningstjänsterna](#applying-the-translation-services).
1. Kör ett översättningsarbetsflöde som beskrivs i [Skapa översättningsprojekt](translation-projects.md) när du har använt den anpassade kopplingen. Kontrollera informationen om kopplingen i rutan **[!UICONTROL Translation Summary]** för översättningsprojektets på konsolen **[!UICONTROL Projects]**.

   ![chlimage_1-220](assets/chlimage_1-220.png)
