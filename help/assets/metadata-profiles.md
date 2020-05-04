---
title: Metadataprofiler för att anpassa metadatakrav för resurser
description: Lär dig mer om metadataprofiler för resurser. Lär dig hur du skapar en metadataprofil och använder den på mappresurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 95ac9d4c8b171c01b9adc056f5dc3a9d776c0465

---


# Metadataprofiler {#metadata-profiles}

Med en metadataprofil kan du använda standardmetadata för resurser i en mapp. Skapa en metadataprofil och tillämpa den på en mapp. Alla resurser som du sedan överför till mappen ärver de standardmetadata som du konfigurerade i metadataprofilen.

## Lägg till en metadataprofil {#adding-a-metadata-profile}

1. Navigera till **[!UICONTROL Verktyg > Resurser > Metadataprofiler]** och tryck på **[!UICONTROL Skapa]**.
1. Ange en rubrik för metadataprofilen, till exempel Exempelmetadata, och tryck på **[!UICONTROL Skapa]**. Metadataprofilens [!UICONTROL redigeringsformulär] visas.

   ![chlimage_1-197](assets/chlimage_1-480.png)

1. Klicka på en komponent och konfigurera dess egenskaper på fliken **[!UICONTROL Inställningar]** . Klicka till exempel på komponenten **[!UICONTROL Beskrivning]** och redigera dess egenskaper.

   ![chlimage_1-198](assets/chlimage_1-481.png)

   Redigera följande egenskaper för komponenten **[!UICONTROL Description]** :

   * **[!UICONTROL Fältetikett]**: Visningsnamnet för metadataegenskapen. Det är bara till för användarreferensen.

   * **[!UICONTROL Mappa till egenskap]**: Värdet för den här egenskapen anger den relativa sökvägen/namnet till resursnoden där den sparas i databasen. Värdet ska alltid börja med `./` eftersom det anger att sökvägen finns under objektets nod.
   ![chlimage_1-199](assets/chlimage_1-482.png)

   The value you specify for **[!UICONTROL Map to property]** is stored as a property under the asset&#39;s metadata node. Om du till exempel anger . `/jcr:content/metadata/dc:desc` som namnet på **[!UICONTROL Mappa till egenskap]** lagrar AEM Resurser värdet `dc:desc` i objektets metadatanod.

   * **[!UICONTROL Standardvärde]**: Använd den här egenskapen om du vill lägga till ett standardvärde för metadatakomponenten. Om du till exempel anger &quot;Min beskrivning&quot; tilldelas det här värdet till egenskapen `dc:desc` vid objektets metadatanod.
   ![chlimage_1-200](assets/chlimage_1-483.png)

   >[!NOTE]
   >
   >Lägga till ett standardvärde i en ny metadataegenskap (som inte finns redan i . `/jcr:content/metadata` nod) visar inte egenskapen och dess värde på objektets egenskapssida som standard. Om du vill visa den nya egenskapen på [!UICONTROL egenskapssidan] för resurserna ändrar du motsvarande schemaformulär.

1. (Optional) Add more components to the Edit Form from the **[!UICONTROL Build Form]** tab, and configure their properties in the **[!UICONTROL Settings]** tab. The following properties are available from the **[!UICONTROL Build Form]** tab:

| Komponent | Egenskaper |
|---|---|
| [!UICONTROL Avsnittshuvud] | Fältetikett, <br> beskrivning |
| [!UICONTROL Enkelradstext] | Fältetikett, <br> Koppla till egenskap, <br> standardvärde |
| [!UICONTROL Flervärdestext] | Fältetikett, <br> Koppla till egenskap, <br> standardvärde |
| [!UICONTROL Siffra] | Fältetikett, <br> Koppla till egenskap, <br> standardvärde |
| [!UICONTROL Date] | Fältetikett, <br> Koppla till egenskap, <br> standardvärde |
| [!UICONTROL Standardtaggar] | Fältetikett, <br> Koppla till egenskap, <br> Standardvärde, <br> Beskrivning |

![chlimage_1-201](assets/chlimage_1-484.png)

1. Tryck/klicka på **[!UICONTROL Klar]**. Metadataprofilen läggs till i listan över profiler på sidan **[!UICONTROL Metadataprofiler]** .<br>

   ![Metadataprofil har lagts till på sidan Metadataprofiler](assets/MetadataProfiles-page.png)

## Kopiera en metadataprofil {#copying-a-metadata-profile}

1. Välj en metadataprofil på sidan **[!UICONTROL Metadataprofiler]** och gör en kopia av den.

   ![chlimage_1-203](assets/chlimage_1-486.png)

1. Tryck på **[!UICONTROL Kopiera]** i verktygsfältet.
1. I dialogrutan **[!UICONTROL Kopiera metadataprofil]** anger du en rubrik för den nya kopian av metadataprofilen.
1. Tryck på **[!UICONTROL Kopiera]**. The copy of the Metadata Profile appears in the list of profiles in the **[!UICONTROL Metadata Profiles]** page.

   ![En kopia av metadataprofilen som lagts till på sidan Metadataprofiler](assets/copy-metadata-profile.png)

## Ta bort en metadataprofil {#deleting-a-metadata-profile}

1. På sidan **[!UICONTROL Metadataprofiler]** väljer du en profil som ska tas bort.

   ![chlimage_1-205](assets/chlimage_1-488.png)

1. Ta[] **[!UICONTROL bort metadataprofiler]** i verktygsfältet.
1. Klicka på **[!UICONTROL Ta bort]** i dialogrutan för att bekräfta borttagningen. Metadataprofilen tas bort från listan.

## Använda en metadataprofil för mappar {#applying-a-metadata-profile-to-folders}

När du tilldelar en metadataprofil till en mapp ärver alla undermappar automatiskt profilen från den överordnade mappen. Det innebär att du bara kan tilldela en metadataprofil till en mapp. Fundera därför noga över mappstrukturen för var du överför, lagrar, använder och arkiverar resurser.

Om du har tilldelat en annan metadataprofil till en mapp åsidosätter den nya profilen den tidigare profilen. De tidigare befintliga mappresurserna ändras inte. Den nya profilen används för resurser som läggs till i mappen senare.

Mappar som har tilldelats en profil visas i användargränssnittet med namnet på profilen som visas i kortnamnet.

![chlimage_1-206](assets/chlimage_1-489.png)

Du kan tillämpa metadataprofiler på specifika mappar eller globalt på alla resurser.

Du kan bearbeta resurser i en mapp som redan har en befintlig metadataprofil som du senare ändrade. Se [Bearbeta resurser i en mapp när du har redigerat dess bearbetningsprofil](processing-profiles.md#reprocessing-assets).

### Använda metadataprofiler på specifika mappar {#applying-metadata-profiles-to-specific-folders}

You can apply a metadata profile to a folder from within the **[!UICONTROL Tools]** menu or if you are in the folder, from **[!UICONTROL Properties]**. I det här avsnittet beskrivs hur du använder metadataprofiler på mappar på båda sätten.

För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

Du kan bearbeta resurser i en mapp som redan har en befintlig videoprofil som du senare ändrade. Se [Bearbeta resurser i en mapp när du har redigerat dess bearbetningsprofil](processing-profiles.md#reprocessing-assets).

#### Använda metadataprofiler på mappar från användargränssnittet för profiler {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

Så här använder du metadataprofilen:

1. Tryck på AEM-logotypen och navigera till **[!UICONTROL Verktyg > Resurser > Metadataprofiler]**.
1. Välj den metadataprofil som du vill använda för en eller flera mappar.

   ![chlimage_1-207](assets/chlimage_1-490.png)

1. Tryck på **[!UICONTROL Använd metadataprofil för mappar]** och markera den eller de mappar som du vill använda för att ta emot de nyligen överförda resurserna. Tryck sedan på **[!UICONTROL Klar]**. För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

#### Använd metadataprofiler på mappar från Egenskaper {#applying-metadata-profiles-to-folders-from-properties}

1. I den vänstra listen trycker du på **[!UICONTROL Resurser]** och navigerar sedan till mappen som du vill använda en metadataprofil på.
1. På mappen: tryck eller klicka på bockmarkeringen för att markera den och tryck eller klicka sedan på **[!UICONTROL Egenskaper]**.

1. Select the **[!UICONTROL Metadata Profiles]** tab and select the profile from the drop-down menu and tap **[!UICONTROL Save]**.

   ![chlimage_1-208](assets/chlimage_1-491.png)

   För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

### Använd en metadataprofil globalt {#applying-a-metadata-profile-globally}

Förutom att tillämpa en profil på en mapp kan du även tillämpa en profil globalt så att allt innehåll som överförs till AEM-resurser i en mapp har den valda profilen.

Du kan bearbeta resurser i en mapp som redan har en befintlig metadataprofil som du senare ändrade. Se [Bearbeta resurser i en mapp när du har redigerat dess bearbetningsprofil](processing-profiles.md#reprocessing-assets).

Så här använder du en metadataprofil globalt:

* Navigera till `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` och använd rätt profil och tryck på **[!UICONTROL Spara]**.

   ![chlimage_1-209](assets/chlimage_1-492.png)

* Navigera till följande nod i CRXDE Lite: `/content/dam/jcr:content`. Lägg till egenskapen `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` och klicka på **[!UICONTROL Spara alla]**.

   ![chlimage_1-210](assets/chlimage_1-493.png)

## Ta bort en metadataprofil från mappar {#removing-a-metadata-profile-from-folders}

När du tar bort en metadataprofil från en mapp ärver alla undermappar automatiskt borttagningen av profilen från den överordnade mappen. All bearbetning av filer som har inträffat i mapparna förblir dock oförändrad.

Du kan ta bort en metadataprofil från en mapp från menyn **[!UICONTROL Verktyg]** eller, om du är i mappen, från **[!UICONTROL Egenskaper]**. I det här avsnittet beskrivs hur du tar bort metadataprofiler från mappar på båda sätten.

### Ta bort metadataprofiler från mappar via användargränssnittet Profiler {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Tryck eller klicka på AEM-logotypen och navigera till **[!UICONTROL Verktyg > Resurser > Metadataprofiler]**.
1. Markera den metadataprofil som du vill ta bort från en eller flera mappar.
1. Tryck på **[!UICONTROL Ta bort metadataprofil från]** mapp(ar) och markera den eller de mappar du vill ta bort en profil från och tryck sedan på **[!UICONTROL Klar]**.

   Du kan bekräfta att metadataprofilen inte längre används för en mapp eftersom namnet inte längre visas under mappnamnet.

### Ta bort metadataprofiler från mappar via Egenskaper {#removing-metadata-profiles-from-folders-via-properties}

1. Tryck på AEM-logotypen, navigera till **[!UICONTROL Resurser]** och sedan till den mapp som du vill ta bort en metadataprofil från.
1. Markera mappen genom att trycka på bockmarkeringen och sedan på **[!UICONTROL Egenskaper]**.
1. Välj fliken **[!UICONTROL Metadataprofiler]** och välj **[!UICONTROL Ingen]** i listrutan och klicka på **[!UICONTROL Spara]**. För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

## Begränsningar och bästa metoder {#limitations-best-practices-tips}

* Det kan finnas befintliga metadataprofiler sedan du uppgraderade till [!DNL Experience Manager] 6.5. Om du efter uppgraderingen använder en sådan profil i mappegenskaper  på fliken [!UICONTROL Metadataprofiler] visas inte metadatafälten. Om du däremot använder en ny metadataprofil visas formulärfälten, men de är inte tillgängliga som förväntat. Funktionsbortfall är inte kvar, men om du vill se (ej tillgängliga) formulärfält redigerar du och sparar de befintliga metadataprofilerna.

>[!MORELIKETHIS]
>
>* [Profiler för att bearbeta metadata, bilder och videoklipp](processing-profiles.md)
>* [De bästa sätten att ordna digitala resurser så att de kan använda bearbetningsprofiler](/help/assets/organize-assets.md)

