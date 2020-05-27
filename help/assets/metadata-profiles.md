---
title: Metadataprofiler för att anpassa metadatakrav för resurser
description: Lär dig mer om metadataprofiler för resurser. Lär dig hur du skapar en metadataprofil och använder den på mappresurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '1310'
ht-degree: 16%

---


# Metadataprofiler {#metadata-profiles}

Med en metadataprofil kan du använda standardmetadata för resurser i en mapp. Skapa en metadataprofil och tillämpa den på en mapp. Alla resurser som du sedan överför till mappen ärver de standardmetadata som du konfigurerade i metadataprofilen.

## Lägg till en metadataprofil {#adding-a-metadata-profile}

1. Navigera till **[!UICONTROL Tools > Assets > Metadata Profiles]** och klicka **[!UICONTROL Create]**.
1. Ange en rubrik för metadataprofilen, till exempel Exempelmetadata, och klicka på **[!UICONTROL Create]**. Metadataprofilens [!UICONTROL Edit Form] namn visas.

   ![chlimage_1-197](assets/chlimage_1-480.png)

1. Klicka på en komponent och konfigurera dess egenskaper på **[!UICONTROL Settings]** fliken. Klicka till exempel på **[!UICONTROL Description]** komponenten och redigera dess egenskaper.

   ![chlimage_1-198](assets/chlimage_1-481.png)

   Redigera följande egenskaper för **[!UICONTROL Description]** komponenten:

   * **[!UICONTROL Field Label]**: Visningsnamnet för metadataegenskapen. Det är bara till för användarreferensen.

   * **[!UICONTROL Map to Property]**: Värdet för den här egenskapen anger den relativa sökvägen/namnet till resursnoden där den sparas i databasen. Värdet ska alltid börja med `./` eftersom det anger att sökvägen finns under objektets nod.
   ![chlimage_1-199](assets/chlimage_1-482.png)

   The value you specify for **[!UICONTROL Map to property]** is stored as a property under the asset&#39;s metadata node. Om du till exempel anger . `/jcr:content/metadata/dc:desc` som namn på **[!UICONTROL Map to property]** lagrar Resurser värdet `dc:desc` på objektets metadatanod.

   * **[!UICONTROL Default Value]**: Använd den här egenskapen om du vill lägga till ett standardvärde för metadatakomponenten. Om du till exempel anger &quot;Min beskrivning&quot; tilldelas det här värdet till egenskapen `dc:desc` vid objektets metadatanod.
   ![chlimage_1-200](assets/chlimage_1-483.png)

   >[!NOTE]
   >
   >Lägga till ett standardvärde i en ny metadataegenskap (som inte finns redan i . `/jcr:content/metadata` nod) visar inte egenskapen och dess värde på objektets egenskapssida som standard. Om du vill visa den nya egenskapen på resursens [!UICONTROL Properties] sida ändrar du motsvarande schemaformulär.

1. (Valfritt) Lägg till fler komponenter i Redigera formulär på fliken **[!UICONTROL Build Form]** och konfigurera deras egenskaper på fliken **[!UICONTROL Settings]**. Följande egenskaper är tillgängliga på fliken **[!UICONTROL Build Form]**:

| Komponent | Egenskaper |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL Section Header] | Fältetikett, <br> beskrivning |
| [!UICONTROL Single Line Text] | Fältetikett, <br> Koppla till egenskap, <br> standardvärde |
| [!UICONTROL Multi Value Text] | Fältetikett, <br> Koppla till egenskap, <br> standardvärde |
| [!UICONTROL Number] | Fältetikett, <br> Koppla till egenskap, <br> standardvärde |
| [!UICONTROL Date] | Fältetikett, <br> Koppla till egenskap, <br> standardvärde |
| [!UICONTROL Standard Tags] | Fältetikett, <br> Koppla till egenskap, <br> Standardvärde, <br> Beskrivning |

![chlimage_1-201](assets/chlimage_1-484.png)

1. Klicka på **[!UICONTROL Done]**. Metadataprofilen läggs till i listan med profiler på **[!UICONTROL Metadata Profiles]** sidan.<br>

   ![Metadataprofil har lagts till på sidan Metadataprofiler](assets/MetadataProfiles-page.png)

## Kopiera en metadataprofil {#copying-a-metadata-profile}

1. Välj en metadataprofil på **[!UICONTROL Metadata Profiles]** sidan för att skapa en kopia av den.

   ![chlimage_1-203](assets/chlimage_1-486.png)

1. Klicka **[!UICONTROL Copy]** i verktygsfältet.
1. I **[!UICONTROL Copy Metadata Profile]** dialogrutan anger du en rubrik för den nya kopian av metadataprofilen.
1. Klicka på **[!UICONTROL Copy]**. Kopian av metadataprofilen visas i listan med profiler på sidan **[!UICONTROL Metadata Profiles]**.

   ![En kopia av metadataprofilen som lagts till på sidan Metadataprofiler](assets/copy-metadata-profile.png)

## Ta bort en metadataprofil {#deleting-a-metadata-profile}

1. På **[!UICONTROL Metadata Profiles]** sidan väljer du en profil att ta bort.

   ![chlimage_1-205](assets/chlimage_1-488.png)

1. Ta[] **[!UICONTROL Delete Metadata Profiles]** in the toolbar.
1. Klicka på **[!UICONTROL Delete]** för att bekräfta borttagningen i dialogrutan. Metadataprofilen tas bort från listan.

## Använda en metadataprofil för mappar {#applying-a-metadata-profile-to-folders}

När du tilldelar en metadataprofil till en mapp ärver alla undermappar automatiskt profilen från den överordnade mappen. Det innebär att du bara kan tilldela en metadataprofil till en mapp. Fundera därför noga över mappstrukturen för var du överför, lagrar, använder och arkiverar resurser.

Om du har tilldelat en annan metadataprofil till en mapp åsidosätter den nya profilen den tidigare profilen. De tidigare befintliga mappresurserna ändras inte. Den nya profilen används för resurser som läggs till i mappen senare.

Mappar som har tilldelats en profil visas i användargränssnittet med namnet på profilen som visas i kortnamnet.

![chlimage_1-206](assets/chlimage_1-489.png)

Du kan tillämpa metadataprofiler på specifika mappar eller globalt på alla resurser.

Du kan bearbeta resurser i en mapp som redan har en befintlig metadataprofil som du senare ändrade. Se [Bearbeta resurser i en mapp när du har redigerat dess bearbetningsprofil](processing-profiles.md#reprocessing-assets).

### Använda metadataprofiler på specifika mappar {#applying-metadata-profiles-to-specific-folders}

Du kan använda en metadataprofil på en mapp från menyn **[!UICONTROL Tools]** eller, om du är i mappen, från **[!UICONTROL Properties]**. I det här avsnittet beskrivs hur du använder metadataprofiler på mappar på båda sätten.

För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

Du kan bearbeta resurser i en mapp som redan har en befintlig videoprofil som du senare ändrade. Se [Bearbeta resurser i en mapp när du har redigerat dess bearbetningsprofil](processing-profiles.md#reprocessing-assets).

#### Använda metadataprofiler på mappar från användargränssnittet för profiler {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

Så här använder du metadataprofilen:

1. Klicka på Experience Manager-logotypen och navigera till **[!UICONTROL Tools > Assets > Metadata Profiles]**.
1. Välj den metadataprofil som du vill använda för en eller flera mappar.

   ![chlimage_1-207](assets/chlimage_1-490.png)

1. Click **[!UICONTROL Apply Metadata Profile to Folder(s)]** and select the folder or multiple folders you want use to receive the newly uploaded assets and click **[!UICONTROL Done]**. För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

#### Använd metadataprofiler på mappar från Egenskaper {#applying-metadata-profiles-to-folders-from-properties}

1. Klicka på den vänstra listen **[!UICONTROL Assets]** och navigera sedan till mappen där du vill använda en metadataprofil.
1. Markera mappen genom att klicka på bockmarkeringen och klicka sedan på **[!UICONTROL Properties]**.

1. Välj fliken **[!UICONTROL Metadata Profiles]**, välj profilen i listrutan och klicka sedan på **[!UICONTROL Save]**.

   ![chlimage_1-208](assets/chlimage_1-491.png)

   För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

### Använd en metadataprofil globalt {#applying-a-metadata-profile-globally}

Förutom att tillämpa en profil på en mapp kan du även tillämpa en profil globalt så att allt innehåll som överförs till Experience Manager-resurser i en mapp har den valda profilen.

Du kan bearbeta resurser i en mapp som redan har en befintlig metadataprofil som du senare ändrade. Se [Bearbeta resurser i en mapp när du har redigerat dess bearbetningsprofil](processing-profiles.md#reprocessing-assets).

Så här använder du en metadataprofil globalt:

* Navigera till `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` och använd rätt profil och klicka på **[!UICONTROL Save]**.

   ![chlimage_1-209](assets/chlimage_1-492.png)

* Navigera till följande nod i CRXDE Lite: `/content/dam/jcr:content`. Lägg till egenskapen `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` och klicka på **[!UICONTROL Save All]**.

   ![chlimage_1-210](assets/chlimage_1-493.png)

## Ta bort en metadataprofil från mappar {#removing-a-metadata-profile-from-folders}

När du tar bort en metadataprofil från en mapp ärver alla undermappar automatiskt borttagningen av profilen från den överordnade mappen. All bearbetning av filer som har inträffat i mapparna förblir dock oförändrad.

You can remove a metadata profile from a folder from within the **[!UICONTROL Tools]** menu or if you are in the folder, from the **[!UICONTROL Properties]**. I det här avsnittet beskrivs hur du tar bort metadataprofiler från mappar på båda sätten.

### Ta bort metadataprofiler från mappar via användargränssnittet Profiler {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Klicka på Experience Manager-logotypen och navigera till **[!UICONTROL Tools > Assets > Metadata Profiles]**.
1. Markera den metadataprofil som du vill ta bort från en eller flera mappar.
1. Click **[!UICONTROL Remove Metadata Profile from Folder(s)]** and select the folder or multiple folders you want use to remove a profile from and click **[!UICONTROL Done]**.

   Du kan bekräfta att metadataprofilen inte längre används för en mapp eftersom namnet inte längre visas under mappnamnet.

### Ta bort metadataprofiler från mappar via Egenskaper {#removing-metadata-profiles-from-folders-via-properties}

1. Klicka på Experience Manager-logotypen och navigera **[!UICONTROL Assets]** sedan till mappen som du vill ta bort en metadataprofil från.
1. Markera mappen genom att klicka på bockmarkeringen och klicka sedan på **[!UICONTROL Properties]**.
1. Välj fliken **[!UICONTROL Metadata Profiles]**, välj **[!UICONTROL None]** i listrutan och klicka på **[!UICONTROL Save]**. För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

## Begränsningar och bästa metoder {#limitations-best-practices-tips}

* Det kan finnas befintliga metadataprofiler sedan du uppgraderade till [!DNL Experience Manager] 6.5. Om du tillämpar en sådan profil i mappen [!UICONTROL Properties] på [!UICONTROL Metadata Profiles] fliken efter uppgraderingen visas inte metadatafälten. Om du däremot använder en ny metadataprofil visas formulärfälten, men de är inte tillgängliga som förväntat. Funktionsbortfall är inte kvar, men om du vill se (ej tillgängliga) formulärfält redigerar du och sparar de befintliga metadataprofilerna.

>[!MORELIKETHIS]
>
>* [Profiler för att bearbeta metadata, bilder och videoklipp](processing-profiles.md)
>* [De bästa sätten att ordna digitala resurser så att de kan använda bearbetningsprofiler](/help/assets/organize-assets.md)

