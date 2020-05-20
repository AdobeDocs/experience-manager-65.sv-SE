---
title: XMP-tillbakaskrivning till återgivningar
description: Lär dig hur XMP-återskrivningsfunktionen sprider metadataändringar för en resurs till alla eller vissa återgivningar av resursen.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 8%

---


# XMP-tillbakaskrivning till återgivningar {#xmp-writeback-to-renditions}

Funktionen för XMP-tillbakaskrivning i [!DNL Adobe Experience Manager Assets] replikerar ändringar i resursens metadata. När du ändrar metadata för en resurs inifrån [!DNL Experience Manager Assets] eller när du överför resursen, lagras ändringarna först i resursnoden i CRXDe. Funktionen för XMP-tillbakaskrivning sprider metadataändringarna till alla eller specifika återgivningar av resursen.

Tänk dig ett scenario där du ändrar egenskapen [!UICONTROL Title] för resursen som har namnet `Classic Leather` på `Nylon`.

![metadata](assets/metadata.png)

I det här fallet [!DNL Experience Manager Assets] sparas ändringarna av **[!UICONTROL Title]** egenskapen i `dc:title` parametern för resursens metadata som lagras i resurshierarkin.

![metadata_stored](assets/metadata_stored.png)

Inga metadataändringar sprids dock automatiskt till återgivningarna av en resurs. [!DNL Experience Manager Assets]

Med funktionen XMP-återställning kan du sprida metadataändringarna till alla eller specifika återgivningar av resursen. Ändringarna lagras dock inte under metadatanoden i resurshierarkin. I stället bäddar den här funktionen in ändringarna i de binära filerna för återgivningarna.

## Aktivera XMP-tillbakaskrivning {#enabling-xmp-writeback}

Om du vill att metadataändringarna ska kunna spridas till återgivningarna av resursen när du överför den ändrar du **[!UICONTROL Adobe CQ DAM Rendition Maker]** konfigurationen i Configuration Manager.

1. Öppna Configuration Manager genom att gå till `https://[aem_server]:[port]/system/console/configMgr`.
1. Öppna **[!UICONTROL Adobe CQ DAM Rendition Maker]** konfigurationen.
1. Välj alternativet **[!UICONTROL Sprid XMP[!UICONTROL ** och spara sedan ändringarna.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## Aktivera XMP-tillbakaskrivning för specifika återgivningar {#enabling-xmp-writeback-for-specific-renditions}

Om du vill att XMP-återskrivningsfunktionen ska kunna sprida metadataändringar för att välja återgivningar, anger du dessa återgivningar i arbetsflödessteget för XMP-återskrivningsprocessen i [!UICONTROL DAM Metadata WriteBack] arbetsflödet. Som standard konfigureras det här steget med den ursprungliga återgivningen.

Utför dessa steg för XMP-återskrivningsfunktionen som sprider metadata till återgivningsminiatyrerna 140.100.png och 319.319.png.

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]** i Experience Manager-gränssnittet.
1. Öppna arbetsflödesmodellen på sidan **[!UICONTROL DAM Metadata Writeback]** Modeller.
1. På egenskapssidan för **[!UICONTROL DAM Metadata Writeback]** öppnar du steget **[!UICONTROL XMP Writeback Process]**.
1. In the [!UICONTROL Step Properties] dialog box, click the **[!UICONTROL Process]** tab.
1. Lägg till **i rutan** Argument `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`och klicka sedan på **OK**.

   ![step_properties](assets/step_properties.png)

1. Spara ändringarna.
1. To regenerate the pyramid TIFF renditions for [!DNL Dynamic Media] images with the new attributes, add the **[!UICONTROL Dynamic Media Process Image Assets]** step to the [!UICONTROL DAM Metadata Writeback] workflow.

   PTIFF-återgivningar skapas och lagras bara lokalt i en Dynamic Media-hybridimplementering.

1. Spara arbetsflödet.

Metadataändringarna sprids till miniatyrbilden för återgivningarna.140.100.png och miniatyrbilden.319.319.png för resursen, inte till de andra.

>[!NOTE]
>
>Information om XMP-återskrivningsproblem i 64-bitars Linux finns i [Så här aktiverar du XMP-återskrivningsproblem i 64-bitars RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>Mer information om vilka plattformar som stöds finns i [XMP-metadatavillkor](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## Filtrera XMP-metadata {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] har stöd för både svartlistsfiltrering och vitlistsfiltrering av egenskaper/noder för XMP-metadata som läses från resurbinärfiler och lagras i JCR när resurser hämtas.

Med svartlistsfiltrering kan du importera alla XMP-metadataegenskaper utom de egenskaper som anges för uteslutning. För resurstyper som INDD-filer som har stora mängder XMP-metadata (till exempel 1 000 noder med 10 000 egenskaper) är namnen på de noder som ska filtreras inte alltid kända i förväg. Om svartlistsfiltrering tillåter ett stort antal resurser med flera XMP-metadata att importeras, kan Experience Manager-distributionen stöta på stabilitetsproblem, till exempel övervakningsköer som stoppats.

Vitlistsfiltrering av XMP-metadata löser problemet genom att du kan definiera de XMP-egenskaper som ska importeras. På så sätt ignoreras andra/okända XMP-egenskaper. Du kan lägga till några av dessa egenskaper i svartlistningsfiltret för bakåtkompatibilitet.

>[!NOTE]
>
>Filtrering fungerar bara för egenskaper som härletts från XMP-källor i objektbinärfiler. För egenskaper som härleds från andra källor än XMP, t.ex. EXIF- och IPTC-format, fungerar inte filtreringen. Datumet då resursen skapades sparas till exempel i egenskapen EXIF TIFF `CreateDate` . Det här värdet lagras i ett metadatafält med namnet `exif:DateTimeOriginal`. Eftersom källan inte är en XMP-källa fungerar inte filtrering på den här egenskapen.

1. Öppna Configuration Manager genom att gå till `https://[aem_server]:[port]/system/console/configMgr`.
1. Öppna **[!UICONTROL Adobe CQ DAM XmpFilter]** konfigurationen.
1. Om du vill använda vitlistefiltrering markerar du **[!UICONTROL Apply Whitelist to XMP Properties]** och anger de egenskaper som ska importeras i rutan **[!UICONTROL Whitelisted XML Names for XMP filtering]**.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. Om du vill filtrera bort svartlistade XMP-egenskaper efter att ha använt vitlistefiltrering anger du dem i rutan **[!UICONTROL Blacklisted XML Names for XMP filtering]**.

   >[!NOTE]
   >
   >The **[!UICONTROL Apply Blacklist to XMP Properties]** option is selected by default. Svartlistsfiltrering är alltså aktiverat som standard. Om du vill inaktivera filtrering av svarta listor avmarkerar du **[!UICONTROL Apply Blacklist to XMP Properties]** alternativet.

1. Spara ändringarna.
