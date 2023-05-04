---
title: Hantera metadata för dina digitala resurser
description: Lär dig mer om metadatatyperna och hur du hanterar metadata för resurser för att enkelt ordna och bearbeta resurser.
contentOwner: AG
mini-toc-levels: 1
feature: Tagging, Metadata
role: Architect, Leader
exl-id: c630709a-7e8b-417c-83a4-35ca9be832a0
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '2258'
ht-degree: 10%

---

# Hantera metadata för dina digitala resurser {#managing-metadata-for-digital-assets}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-metadata.html?lang=en) |
| AEM 6.5 | Den här artikeln |

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] sparar metadata för varje resurs. Det gör det enklare att kategorisera och ordna resurser och det hjälper personer som letar efter en viss resurs. Med möjlighet att extrahera metadata från filer som överförts till [!DNL Experience Manager Assets], integreras metadatahanteringen med det kreativa arbetsflödet. Med möjligheten att behålla och hantera metadata med dina resurser kan du automatiskt ordna och bearbeta resurser baserat på deras metadata.

## Metadata och dess ursprung {#how-to-edit-or-add-metadata}

Metadata är ytterligare information om resursen som kan sökas igenom. Den läggs till i resurser och i [!DNL Experience Manager] bearbetas när du överför en resurs. Du kan redigera befintliga metadata och lägga till nya metadataegenskaper i befintliga fält. Organisationer behöver kontrollerade och tillförlitliga metadata-språk. Därför [!DNL Experience Manager Assets] tillåter inte att nya metadataegenskaper läggs till på begäran. Endast administratörer och utvecklare kan lägga till nya egenskaper eller fält som innehåller metadata. Användarna kan fylla i befintliga fält med metadata.

Följande metoder kan användas för att lägga till metadata i digitala resurser:

* Till att börja med lägger de program som skapar resurser till metadata i det. Till exempel: [Acrobat lägger till metadata](https://helpx.adobe.com/acrobat/using/pdf-properties-metadata.html) till PDF-filer eller en kamera lägger till vissa grundläggande metadata till fotona. När du genererar resurser kan du lägga till metadata i de ursprungliga programmen. Du kan till exempel [lägga till IPTC-metadata i Adobe Lightroom](https://helpx.adobe.com/lightroom-classic/help/metadata-basics-actions.html).

* Innan du överför en resurs till [!DNL Experience Manager]kan du redigera och ändra metadata antingen med det program som användes för att skapa en resurs eller med något annat metadataredigeringsprogram. När du överför en resurs till Experience Manager bearbetas metadata. Se till exempel hur du [arbeta med metadata i [!DNL Adobe Bridge]](https://helpx.adobe.com/bridge/user-guide.html/bridge/using/metadata-adobe-bridge.ug.html) och se [taggpanel för [!DNL Adobe Bridge]](https://exchange.adobe.com/creativecloud.details.20009.aem-tags-panel-for-bridge-cc.html) in [!DNL Adobe Exchange].

* I [!DNL Experience Manager Assets]kan du manuellt lägga till eller redigera metadata för resurser i [!UICONTROL Properties] sida.

* Du kan utnyttja [metadataprofiler](/help/assets/metadata-config.md#metadata-profiles) funktionaliteten i [!DNL Experience Manager Assets] för att automatiskt lägga till metadata när resurser överförs till DAM.

## Lägg till eller redigera metadata i [!DNL Experience Manager Assets] {#add-edit-metadata}

Redigera metadata för en resurs i [!DNL Assets] gör så här:

1. Gör något av följande:

   * Från [!DNL Assets] markerar du resursen och klickar på **[!UICONTROL View Properties]** i verktygsfältet.
   * Välj miniatyrbilden för resursen **[!UICONTROL View Properties]** snabbåtgärd.
   * På resurssidan klickar du på **[!UICONTROL View Properties]** ![Ikon för resursinformation](assets/do-not-localize/info-circle-icon.png) i verktygsfältet.

   Resurssidan visar alla metadata för resursen. Metadata extraheras när resursen överförs (hämtas) till [!DNL Experience Manager].

   ![Välj Egenskaper för en resurs för att visa dess metadata](assets/asset-metadata.png)

   *Bild: Redigera eller lägga till metadata för resurs [!UICONTROL Properties] sida.*

1. Redigera metadata under de olika flikarna efter behov och klicka när du är klar **[!UICONTROL Save]** i verktygsfältet för att spara ändringarna. Klicka **[!UICONTROL Close]** för att gå tillbaka till [!DNL Assets] webbgränssnitt.

   >[!NOTE]
   >
   >Om ett textfält är tomt finns det ingen befintlig metadatauppsättning. Du kan ange ett värde i fältet och spara det för att lägga till metadataegenskapen.

Alla ändringar av metadata för en resurs skrivs tillbaka till den ursprungliga binärfilen som en del av dess XMP data. Metadataåterskrivningsarbetsflödet lägger till metadata i den ursprungliga binärfilen. Ändringar som gjorts i befintliga egenskaper (t.ex. `dc:title`) skrivs över och nya egenskaper (inklusive anpassade egenskaper som `cq:tags`) läggs till med schemat.

XMP stöds och är aktiverat för de plattformar och filformat som beskrivs i [tekniska krav.](/help/sites-deploying/technical-requirements.md)

## Redigera metadataegenskaper för flera resurser {#editing-metadata-properties-of-multiple-assets}

[!DNL Adobe Enterprise Manager Assets] Med kan du redigera metadata för flera resurser samtidigt så att du snabbt kan sprida vanliga metadataändringar till resurser i grupp. Du kan också redigera metadata för flera samlingar samtidigt. Använd egenskapssidan för att utföra metadataändringar på flera resurser eller samlingar:

* Ändra metadataegenskaper till ett gemensamt värde
* Lägga till eller ändra taggar

Om du vill anpassa sidan med metadataegenskaper, inklusive lägga till, ändra eller ta bort metadataegenskaper, använder du [schemaredigerare](metadata-config.md#folder-metadata-schema).

>[!NOTE]
>
>Massredigeringsmetoderna fungerar för resurser som är tillgängliga i en mapp eller en samling. För resurser som är tillgängliga i olika mappar eller matchar ett gemensamt villkor är det möjligt att [massuppdatera metadata efter sökning](search-assets.md#metadataupdates).

1. I [!DNL Assets] navigera till platsen för de resurser som du vill redigera.
1. Markera de resurser som du vill redigera gemensamma egenskaper för.
1. I verktygsfältet klickar du på **[!UICONTROL Properties]** för att öppna egenskapssidan för de valda resurserna.
1. Ändra metadataegenskaperna för markerade resurser på de olika flikarna.
1. Om du vill visa metadata för en viss resurs avbryter du valet av återstående resurser i listan. Om du avbryter urvalet av några resurser på [!UICONTROL Properties] sidan uppdateras inte metadata för sådana resurser.
1. Om du vill välja ett annat metadatamatchschema för resurserna klickar du på **[!UICONTROL Settings]** i verktygsfältet och välj ett schema. Klicka på **[!UICONTROL Save & Close]**.
1. Om du vill lägga till nya metadata till befintliga metadata i fält som innehåller flera värden väljer du **[!UICONTROL Append mode]**. Om du inte markerar det här alternativet ersätter de nya metadata de data som finns i fälten. Klicka på **[!UICONTROL Submit]**.

![Massor av metadatamatcheman gäller för flera resurser](assets/metadata-schema-bulk-edit.gif)

>[!CAUTION]
>
>För fält med ett enda värde läggs de nya metadata inte till det befintliga värdet i fältet, även om du väljer **[!UICONTROL Append mode]**.

## Importera metadata {#import-metadata}

[!DNL Assets] I kan du importera resursmetadata gruppvis med hjälp av en CSV-fil. Du kan göra satsvisa uppdateringar för de nyligen överförda resurserna eller för befintliga resurser genom att importera en CSV-fil. Du kan också importera resursmetadata i grupp från tredjepartssystem i CSV-format.

Import av metadata är asynkron och påverkar inte systemets prestanda. Samtidig uppdatering av metadata för flera resurser kan vara resurskrävande på grund av XMP återskrivningsaktivitet om arbetsflödesflaggan är markerad. Planera en sådan import under begränsad serveranvändning så att prestanda för andra användare inte påverkas.

>[!NOTE]
>
>Om du vill importera metadata för anpassade namnutrymmen måste du först registrera namnutrymmena.

1. Navigera till [!DNL Assets] användargränssnittet och klicka **[!UICONTROL Create]** i verktygsfältet.
1. Välj **[!UICONTROL Metadata]** i menyn.
1. I **[!UICONTROL Metadata Import]** sida, klicka **[!UICONTROL Select File]**. Markera CSV-filen med metadata.
1. Ange följande parametrar. Se ett exempel på en CSV-fil på [metadata-import-sample-file.csv](/help/assets/assets/metadata-import-sample-file.csv).

   | Parametrar för metadataimport | Beskrivning |
   |:---|:---|
   | [!UICONTROL Batch Size] | Antal resurser i en grupp som metadata ska importeras för. Standardvärdet är 50. Maxvärdet är 100. |
   | [!UICONTROL Field Separator] | Standardvärdet är `,` (komma). Du kan ange andra tecken. |
   | [!UICONTROL Multi Value Delimiter] | Avgränsare för metadatavärden. Standardvärdet är `|`. |
   | [!UICONTROL Launch Workflows] | Falskt som standard. När inställt på `true` och standardinställningarna används för [!UICONTROL DAM Metadata WriteBack] arbetsflöde (som skriver metadata till binära XMP). Om du aktiverar arbetsflödena blir systemet långsammare. |
   | [!UICONTROL Asset Path Column Name] | Definierar kolumnnamnet för CSV-filen med resurser. |

1. Klicka på **[!UICONTROL Import]** i verktygsfältet. När metadata har importerats visas ett meddelande i [!UICONTROL Notification] inkorg.

1. Navigera till en resurs för att verifiera korrekt import [!UICONTROL Properties] och verifiera värdena i fälten.

Om du vill lägga till datum och tidsstämpel när du importerar metadata använder du `YYYY-MM-DDThh:mm:ss.fff-00:00` format för datum och tid. Datum och tid avgränsas med `T`, `hh` är timmar i 24-timmarsformat, `fff` är nanosekunder, och `-00:00` är tidszonsförskjutning. Till exempel: `2020-03-26T11:26:00.000-07:00` är 26 mars 2020 kl. 11:26:00 000 PST-tid.

>[!CAUTION]
>
>Om datumformatet inte matchar `YYYY-MM-DDThh:mm:ss.fff-00:00`, ställs datumvärdena inte in. Datumformaten för den exporterade CSV-metadatafilen har formatet `YYYY-MM-DDThh:mm:ss-00:00`. Om du vill importera den konverterar du den till ett godkänt format genom att lägga till värdet för nanosekunder som markeras med `fff`.

## Exportera metadata {#export-metadata}

Du kan exportera metadata för flera resurser i ett CSV-format. Metadata exporteras asynkront och påverkar inte systemets prestanda. Om du vill exportera metadata [!DNL Experience Manager] går igenom objektnodens egenskaper `jcr:content/metadata` och dess underordnade noder och exporterar metadataegenskaperna i en CSV-fil.

Några exempel på användningsområden för att exportera flera metadata samtidigt är:

* Importera metadata i ett tredjepartssystem när du migrerar resurser.
* Dela metadata med ett större projektteam.
* Testa eller granska metadata för att se om de är kompatibla.
* Gör metadata externt och lokalisera dem separat.

1. Välj den resursmapp som innehåller resurser som du vill exportera metadata för. Välj **[!UICONTROL Export metadata]** i verktygsfältet.

1. I [!UICONTROL Metadata Export] anger du ett namn för CSV-filen. Om du vill exportera metadata för resurser i undermappar väljer du **[!UICONTROL Include assets in subfolders]**.

   ![Gränssnitt och alternativ för att exportera metadata för alla resurser i en mapp](assets/export_metadata_page.png "Gränssnitt och alternativ för att exportera metadata för alla resurser i en mapp")

1. Välj önskade alternativ. Ange ett filnamn och vid behov ett datum.

1. I **[!UICONTROL Properties to be exported]** anger du om du vill exportera alla eller specifika egenskaper. Om du väljer Selektiva egenskaper som ska exporteras lägger du till de önskade egenskaperna.

1. Klicka på **[!UICONTROL Export]** i verktygsfältet. Ett meddelande bekräftar att metadata exporteras. Stäng meddelandet.

1. Öppna inkorgsmeddelandet för exportjobbet. Markera jobbet och klicka på **[!UICONTROL Open]** i verktygsfältet. Om du vill hämta CSV-filen med metadata klickar du på **[!UICONTROL CSV Download]** i verktygsfältet. Klicka på **[!UICONTROL Close]**.

   ![Dialogruta för att hämta CSV-filen som innehåller metadata som exporterats i grupp](assets/csv_download.png)

   *Bild: Dialogruta för att hämta CSV-filen som innehåller metadata som exporterats i grupp.*

## Redigera metadata för samlingar {#collections-metadata}

Mer information finns i [visa och redigera samlingsmetadata](/help/assets/manage-collections.md#view-edit-collection-metadata) och [redigera metadata för flera samlingar samtidigt](/help/assets/manage-collections.md#editing-collection-metadata-in-bulk).

## Använda en metadataprofil för mappar {#applying-a-metadata-profile-to-folders}

<!-- TBD: Review this overview.
-->

När du tilldelar en metadataprofil till en mapp ärver alla undermappar automatiskt profilen från den överordnade mappen. Det innebär att du bara kan tilldela en metadataprofil till en mapp. Fundera därför noga över mappstrukturen för var du överför, lagrar, använder och arkiverar resurser.

Om du har tilldelat en annan metadataprofil till en mapp åsidosätter den nya profilen den tidigare profilen. De tidigare befintliga mappresurserna ändras inte. Den nya profilen används för resurser som läggs till i mappen senare.

Mappar som har tilldelats en profil visas i användargränssnittet med namnet på profilen som visas i kortnamnet.

![I kortvyn visas den metadataprofil som används för en mapp](assets/metadata-profile-card-view-display.png)

Du kan tillämpa metadataprofiler på specifika mappar eller globalt på alla resurser.

Du kan bearbeta resurser i en mapp som redan har en befintlig metadataprofil som du senare ändrade. Se [Bearbeta resurser i en mapp efter att du har redigerat dess bearbetningsprofil](processing-profiles.md#reprocessing-assets).

Du kan använda en metadataprofil på en mapp från menyn **[!UICONTROL Tools]** eller, om du är i mappen, från **[!UICONTROL Properties]**. I det här avsnittet beskrivs hur du använder metadataprofiler på mappar på båda sätten.

För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

Du kan bearbeta resurser i en mapp som redan har en befintlig videoprofil som du senare ändrade. Se [Bearbeta resurser i en mapp efter att du har redigerat dess bearbetningsprofil](processing-profiles.md#reprocessing-assets).

### Använd metadataprofiler på mappar från [!UICONTROL Profiles] användargränssnitt {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

Så här använder du metadataprofilen:

1. Klicka på [!DNL Experience Manager] logotyp och navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]**.
1. Välj den metadataprofil som du vill använda för en eller flera mappar.
1. Klicka **[!UICONTROL Apply Metadata Profile to Folder(s)]** och markera den eller de mappar som du vill använda för att ta emot de nyligen överförda resurserna och klicka på **[!UICONTROL Done]**. För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

### Använd metadataprofiler på mappar från [!UICONTROL Properties] {#applying-metadata-profiles-to-folders-from-properties}

1. Klicka på **[!UICONTROL Assets]** navigera sedan till den mapp som du vill använda en metadataprofil på.
1. Markera mappen genom att klicka på bockmarkeringen och klicka sedan på **[!UICONTROL Properties]**.

1. Välj **[!UICONTROL Metadata Profiles]** och välj profilen på popup-menyn och klicka på **[!UICONTROL Save]**.

För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

<!-- TBD: Commenting as the topic in metadata-config.md is incomplete.

### Apply metadata profile globally {#metadata-profile-global}

For details, see [configuration to apply metadata profile globally](/help/assets/metadata-config.md#apply-a-metadata-profile-globally). -->

### Ta bort en metadataprofil från mappar {#removing-a-metadata-profile-from-folders}

När du tar bort en metadataprofil från en mapp ärver alla undermappar automatiskt borttagningen av profilen från den överordnade mappen. All bearbetning av filer som har inträffat i mapparna förblir dock oförändrad.

Du kan ta bort en metadataprofil från en mapp i **[!UICONTROL Tools]** eller från **[!UICONTROL Properties]** i mappen.

#### Ta bort metadataprofiler från mappar via användargränssnittet Profiler {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Klicka på [!DNL Experience Manager] logotyp och navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]**.
1. Markera den metadataprofil som du vill ta bort från en eller flera mappar.
1. Klicka **[!UICONTROL Remove Metadata Profile from Folder(s)]** och markera den eller de mappar som du vill ta bort en profil från och klicka på **[!UICONTROL Done]**.

   Du kan bekräfta att metadataprofilen inte längre används för en mapp eftersom namnet inte längre visas under mappnamnet.

#### Ta bort metadataprofiler från mappar via Egenskaper {#removing-metadata-profiles-from-folders-via-properties}

1. Klicka på [!DNL Experience Manager] logotyp och navigera **[!UICONTROL Assets]** och sedan till mappen som du vill ta bort en metadataprofil från.
1. Markera mappen genom att klicka på bockmarkeringen och klicka sedan på **[!UICONTROL Properties]**.
1. Välj fliken **[!UICONTROL Metadata Profiles]**, välj **[!UICONTROL None]** i listrutan och klicka på **[!UICONTROL Save]**. För mappar som redan har tilldelats en profil visas profilens namn direkt under mappnamnet.

## Tips och begränsningar {#best-practices-limitations}

* Metadatauppdateringar via användargränssnittet ändrar metadataegenskaperna i `dc` namnutrymme. Alla uppdateringar som görs via HTTP API ändrar metadataegenskaperna i `jcr` namnutrymme. Se [uppdatera metadata med HTTP API](/help/assets/mac-api-assets.md#update-asset-metadata).

* CSV-filen för import av metadata för resurser har ett mycket specifikt format. För att spara arbete och tid och undvika oavsiktliga fel kan du börja skapa CSV-filen med formatet för en exporterad CSV-fil.

* När du importerar metadata med hjälp av en CSV-fil är datumformatet obligatoriskt `YYYY-MM-DDThh:mm:ss.fff-00:00`. Om något annat format används ställs datumvärdena inte in. Datumformaten för den exporterade CSV-metadatafilen har formatet `YYYY-MM-DDThh:mm:ss-00:00`. Om du vill importera den konverterar du den till ett godkänt format genom att lägga till värdet för nanosekunder som markeras med `fff`.

>[!MORELIKETHIS]
>
>* [Metadatabegrepp och -förståelse](metadata-concepts.md).
>* [Redigera metadataegenskaper för flera samlingar](manage-collections.md#editing-collection-metadata-in-bulk)
>* [Import och export av metadata i Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html)


<!-- TBD: Try filling the available information in these topics to the extent possible. As and when complete, publish the sections live.

## Where to find metadata of an asset or folder {#find-metadata}

What all methods to access asset Properties. More Details option in column view. Select asset and click Properties. Keyboard shortcut `p`. What else?

## Understand metadata handling in Experience Manager {#metadata-possibilities-with-aem}

Describe the journey of an assets' metadata. What all happens to metadata when an asset is added to Experience Manager.

## Add metadata to your digital assets {#add-metadata}

* To begin with, assets come with some metadata. The applications that create digital assets add some metadata to the assets created. Before uploading an asset to Experience Manager, you can edit and modify metadata using either the native application used to create an asset or using some other metadata editing application. When you upload an asset to Experience Manager, the metadata is processed.

* Link to PS, ID, AI, PDF, etc. metadata-related help articles.

* Link to XMP writeback.

* Manually add (or edit) metadata in AEM in Properties page.

* Metadata profiles

* Any workflows related to metadata?

* Advanced topic: Add, edit, modify, process and writeback metadata of subassets.

## Metadata of assets, folders, and collections {#metadata-of-assets-folders-collections}

Similarities and differences between metadata of asset and folder. 

Link to metadata handling of collections.

## Modify metadata of an asset, folder, or collection {#modify-metadata}

* While creating assets: Native application.

* Before ingesting assets: Metadata editors

* After ingesting assets: Properties of an asset, folder, collection, etc.

* Any supported programmatic method to bulk edit metadata directly in JCR?

## Modify metadata in bulk {#modify-metadata-in-bulk}

[!DNL Adobe Enterprise Manager Assets] lets you edit the metadata of multiple assets simultaneously so you can quickly propagate common metadata changes to assets in bulk. You can also edit the metadata for multiple collections in bulk.

Use the properties page to perform metadata changes on multiple assets or collections:

* Change metadata properties to a common value

* Add or modify tags

To customize the metadata properties page, including adding, modifying, deleting metadata properties, use the schema editor.

>[!NOTE]
>
>The bulk editing methods work for assets available in a folder or a collection. For the assets that are available across folders or match a common criteria, it is possible to [bulk update the metadata after searching](search-assets.md#metadataupdates).

1. In the [!DNL Assets] user interface, navigate to the location of the assets you want to edit.
1. Select the assets for which you want to edit common properties.
1. From the toolbar, click **[!UICONTROL Properties]** to open the properties page for the selected assets.

   >[!NOTE]
   >
   >When you select multiple assets, the lowest common parent form is selected for the assets. In other words, the properties page only displays metadata fields that are common across the properties pages of all the individual assets.

1. Modify the metadata properties for selected assets under the various tabs.
1. To view the metadata editor for a specific asset, deselect the remaining assets in the list. The metadata editor fields are populated with the metadata for the particular asset.

   >[!NOTE]
   >
   >* In the Properties page, you can remove assets from the asset list by deselecting them. The asset list has all the assets selected by default. The metadata for assets that you remove from the list is not updated.
   >
   >* At the top of assets list, select the check box near **[!UICONTROL Title]** to toggle between selecting the assets and clearing the list.

1. To select a different metadata schema for the assets, click **[!UICONTROL Settings]** from the toolbar, and select the desired schema.
1. Save the changes.
1. To append the new metadata with the existing metadata in fields that contain multiple values, select **[!UICONTROL Append mode]**. If you do not select this option, the new metadata replaces the existing metadata in the fields. click **[!UICONTROL Submit]**.

   >[!CAUTION]
   >
   >For single-value fields, the new metadata is not appended to the existing value in the field even if you select **[!UICONTROL Append mode]**.

-->
