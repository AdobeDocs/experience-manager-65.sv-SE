---
title: XMP till återgivning
description: Lär dig hur XMP återskrivningsfunktionen sprider metadataändringar för en resurs till alla eller vissa återgivningar av resursen.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 82148ae5-37e9-4fc5-ada9-db3d91b29c33
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 4%

---

# XMP till återgivning {#xmp-writeback-to-renditions}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/xmp-metadata.html?lang=en) |
| AEM 6.5 | Den här artikeln |
| AEM 6.4 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/xmp-writeback.html?lang=en) |

Den här XMP återskrivningsfunktionen i [!DNL Adobe Experience Manager Assets] återger metadataändringarna i återgivningarna av den ursprungliga resursen. När du ändrar metadata för en resurs i Resurser eller när du överför resursen, lagras ändringarna först i metadatanoden i resurshierarkin.

Med funktionen XMP kan du sprida metadataändringarna till alla eller vissa återgivningar av resursen. Funktionen skriver bara tillbaka de metadataegenskaper som använder `jcr` namespace, d.v.s. en egenskap med namnet `dc:title` skrivs tillbaka men egenskapen heter `mytitle` inte.

Tänk dig ett scenario där du ändrar [!UICONTROL Title] egenskap för tillgången i namnet `Classic Leather` till `Nylon`.

![metadata](assets/metadata.png)

I det här fallet [!DNL Experience Manager Assets] sparar ändringarna i **[!UICONTROL Title]** -egenskapen i `dc:title` parameter för resursens metadata som lagras i resurshierarkin.

![metadata_stored](assets/metadata_stored.png)

Men [!DNL Experience Manager Assets] sprider inte automatiskt metadataändringar till återgivningar av en resurs. Se [aktivera XMP-tillbakaskrivning](#enable-xmp-writeback).

## Aktivera XMP {#enable-xmp-writeback}

Om du vill att metadataändringarna ska kunna spridas till återgivningarna av resursen när du överför den ändrar du **[!UICONTROL Adobe CQ DAM Rendition Maker]** konfiguration i Configuration Manager.

1. Öppna Configuration Manager genom att öppna `https://[aem_server]:[port]/system/console/configMgr`.
1. Öppna **[!UICONTROL Adobe CQ DAM Rendition Maker]** konfiguration.
1. Välj **[!UICONTROL Propagate XMP]** och spara sedan ändringarna.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## Aktivera XMP återskrivning för specifika återgivningar {#enabling-xmp-writeback-for-specific-renditions}

Om du vill att XMP återskrivningsfunktion ska kunna sprida metadataändringar för att välja återgivningar, anger du dessa återgivningar i arbetsflödet för XMP återskrivningsprocess i [!UICONTROL DAM Metadata WriteBack] arbetsflöde. Som standard konfigureras det här steget med den ursprungliga återgivningen.

Utför följande steg för XMP återskrivningsfunktion som sprider metadata till återgivningsminiatyrerna 140.100.png och 319.319.png.

1. Navigera till Experience Manager i gränssnittet **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. Öppna sidan Modeller **[!UICONTROL DAM Metadata Writeback]** arbetsflödesmodell.
1. På egenskapssidan för **[!UICONTROL DAM Metadata Writeback]** öppnar du steget **[!UICONTROL XMP Writeback Process]**.
1. I [!UICONTROL Step Properties] klickar du på **[!UICONTROL Process]** -fliken.
1. I **Argument** ruta, lägga till `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`och klicka **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Spara ändringarna.
1. Generera om pyramidens TIFF-renderingar för [!DNL Dynamic Media] bilder med nya attribut, lägg till **[!UICONTROL Dynamic Media Process Image Assets]** till [!UICONTROL DAM Metadata Writeback] arbetsflöde.

   PTIFF-återgivningar skapas och lagras bara lokalt i en Dynamic Media-hybridimplementering.

1. Spara arbetsflödet.

Metadataändringarna sprids till miniatyrbilden för återgivningarna.140.100.png och miniatyrbilden.319.319.png för resursen, inte till de andra.

>[!NOTE]
>
>Information om XMP återskrivningsproblem i 64-bitars Linux finns i [Aktivera XMP för 64-bitars RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>Information om vilka plattformar som stöds finns i [XMP för metadataåterskrivning](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## Filtrera XMP metadata {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] har stöd för både blockeringslista och tillåtelselista-filtrering av egenskaper/noder för XMP metadata som läses från objektbinärfiler och lagras i JCR när resurser hämtas.

Om du filtrerar med hjälp av blockeringslista kan du importera alla XMP metadataegenskaper utom de egenskaper som anges för undantag. För resurstyper som INDD-filer som har stora mängder XMP metadata (till exempel 1 000 noder med 10 000 egenskaper) är namnen på de noder som ska filtreras inte alltid kända i förväg. Om du filtrerar med blockeringslista kan ett stort antal resurser med många XMP metadata importeras, [!DNL Experience Manager] driftsättning kan stöta på stabilitetsproblem, till exempel övervakningsköer som har fastnat.

Filtrering av XMP metadata via tillåtelselista löser problemet genom att du kan definiera de XMP egenskaper som ska importeras. På så sätt ignoreras alla andra eller okända XMP. För bakåtkompatibilitet kan du lägga till några av dessa egenskaper i filtret som använder blockeringslista.

>[!NOTE]
>
>Filtrering fungerar bara för egenskaper som härletts från XMP källor i objektbinärfiler. För egenskaper som härleds från andra källor än XMP, som EXIF- och IPTC-format, fungerar inte filtreringen. Datumet då en resurs skapas sparas till exempel i egenskapen med namnet `CreateDate` i EXIF TIFF. Experience Manager lagrar det här värdet i ett metadatafält med namnet `exif:DateTimeOriginal`. Eftersom källan inte är en XMP källa fungerar inte filtrering på den här egenskapen.

1. Öppna Configuration Manager genom att öppna `https://[aem_server]:[port]/system/console/configMgr`.
1. Öppna **[!UICONTROL Adobe CQ DAM XmpFilter]** konfiguration.
1. Om du vill använda filtrering via tillåtelselista väljer du **[!UICONTROL Apply Allowlist to XMP Properties]** och ange de egenskaper som ska importeras i **[!UICONTROL Allowed XML Names for XMP filtering]** box.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. Om du vill filtrera bort blockerade XMP efter att ha använt filtrering via tillåtelselista anger du egenskaperna i dialogrutan **[!UICONTROL Blocked XML Names for XMP filtering]** box.

   >[!NOTE]
   >
   >The **[!UICONTROL Apply Blocklist to XMP Properties]** är markerat som standard. Filtrering med blockeringslista är alltså aktiverat som standard. Om du vill inaktivera en sådan filtrering avbryter du valet av **[!UICONTROL Apply Blocklist to XMP Properties]** alternativ.

1. Spara ändringarna.
