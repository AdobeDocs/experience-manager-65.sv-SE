---
title: Konfiguration och administration av metadatafunktioner.
description: Konfiguration och administration av [!DNL Experience Manager Assets] funktioner för att lägga till och hantera metadata.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 56c92b7f-e687-4ab5-a376-afa58bdb6ee0
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '1855'
ht-degree: 3%

---

# Konfiguration och administration av metadatafunktioner i [!DNL Assets] {#config-metadata}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/metadata-profiles.html?lang=en) |
| AEM 6.5 | Den här artikeln |
| AEM 6.4 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/metadata-profiles.html?lang=en) |

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] sparar metadata för varje resurs. Det gör det enklare att kategorisera och ordna resurser och det hjälper personer som letar efter en viss resurs. Med möjligheten att behålla och hantera metadata med dina resurser kan du automatiskt ordna och bearbeta resurser baserat på deras metadata. [!DNL Adobe Experience Manager Assets] gör att administratörer kan konfigurera och anpassa metadatafunktioner för att ändra standarderbjudandet för Adobe.

## Redigera metadatamatchema {#metadata-schema}

Mer information finns i [redigera metadata-schemaformulär](metadata-schemas.md#edit-metadata-schema-forms).

## Registrera ett anpassat namnutrymme i [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

Du kan lägga till egna namnutrymmen i [!DNL Experience Manager]. Precis som det finns fördefinierade namnutrymmen som `cq`, `jcr`och `sling`kan du ha ett namnutrymme för databasens metadata och XML-bearbetning.

1. Åtkomst till administrationssidan för nodtypen `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Klicka på **[!UICONTROL Namespaces]** överst på sidan.
1. Om du vill lägga till ett namnutrymme klickar du på **[!UICONTROL New]** längst ned på sidan.
1. Ange ett anpassat namnutrymme i XML-namnutrymmeskonventionen. Ange ID:t i form av en URI och ett associerat prefix för ID:t. Klicka på **[!UICONTROL Save]**.

## Konfigurera gränser för massmetadatauppdatering {#bulk-metadata-update-limit}

För att förhindra att DOS-liknande situationer uppstår [!DNL Enterprise Manager] begränsar antalet parametrar som stöds i en Sling-begäran. När du uppdaterar metadata för många resurser på en gång kan du nå gränsen och metadata uppdateras inte för fler resurser. Enterprise Manager genererar följande varning i loggarna:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

Om du vill ändra gränsen måste du ha åtkomst **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** och ändra värdet för **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi-konfiguration.

## Metadataprofiler {#metadata-profiles}

Med en metadataprofil kan du använda standardmetadata för resurser i en mapp. Skapa en metadataprofil och tillämpa den på en mapp. Alla resurser som du senare överför till mappen ärver de standardmetadata som du konfigurerade i metadataprofilen.

### Lägg till en metadataprofil {#adding-a-metadata-profile}

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]** och klicka **[!UICONTROL Create]**.
1. Ange en rubrik för profilen, till exempel `Sample Metadata`och klicka **[!UICONTROL Create]**. The [!UICONTROL Edit Form] för metadataprofilen visas.

   ![Redigera ett metadataformulär](assets/metadata-edit-form.png)

1. Klicka på en komponent och konfigurera dess egenskaper i **[!UICONTROL Settings]** -fliken. Klicka till exempel på **[!UICONTROL Description]** och redigera dess egenskaper.

   ![Inställning av en komponent i metadataprofil](assets/metadata-profile-component-setting.png)

   Redigera följande egenskaper för **[!UICONTROL Description]** komponent:

   * **[!UICONTROL Field Label]**: Visningsnamnet för metadataegenskapen. Det är bara till för användarreferensen.

   * **[!UICONTROL Map to Property]**: Värdet för den här egenskapen anger den relativa sökvägen eller namnet till resursnoden där den sparas i databasen. Värdet ska alltid börja med `./` eftersom det anger att sökvägen finns under objektets nod.

   ![Mappa till egenskapsinställning i metadataprofil](assets/metadata-profile-setting-map-property.png)

   Värdet som du anger för **[!UICONTROL Map to property]** lagras som en egenskap under objektets metadatanod. Om du till exempel anger `./jcr:content/metadata/dc:desc` som namnet på **[!UICONTROL Map to property]**, [!DNL Assets] lagrar värdet `dc:desc` på resursens metadatanod. Adobe rekommenderar att du endast mappar ett fält till en viss egenskap i metadatarammet. I annat fall hämtas det senast tillagda fältet som är mappat till egenskapen av systemet.

   * **[!UICONTROL Default Value]**: Använd den här egenskapen om du vill lägga till ett standardvärde för metadatakomponenten. Om du till exempel anger &quot;Min beskrivning&quot; tilldelas det här värdet till egenskapen `dc:desc` på resursens metadatanod.

   ![Ange standardbeskrivning i metadataprofil](assets/metadata-profile-setting-default-value.png)

   >[!NOTE]
   >
   >Lägga till ett standardvärde i en ny metadataegenskap (som inte finns vid `/jcr:content/metadata` nod) visar inte egenskapen och dess värde på resursens [!UICONTROL Properties] sida som standard. Så här visar du den nya egenskapen för resurserna [!UICONTROL Properties] ändrar du motsvarande schemaformulär.

1. (Valfritt) I dialogrutan **[!UICONTROL Build Form]** flik, lägga till fler komponenter i [!UICONTROL Edit Form]och konfigurera deras egenskaper i **[!UICONTROL Settings]** -fliken. Följande egenskaper är tillgängliga i **[!UICONTROL Build Form]** tab:

| Komponent | Egenskaper |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL Section Header] | Fältetikett, <br> Beskrivning |
| [!UICONTROL Single-Line Text] | Fältetikett, <br> Mappa till egenskap, <br> Standardvärde |
| [!UICONTROL Multi Value Text] | Fältetikett, <br> Mappa till egenskap, <br> Standardvärde |
| [!UICONTROL Number] | Fältetikett, <br> Mappa till egenskap, <br> Standardvärde |
| [!UICONTROL Date] | Fältetikett, <br> Mappa till egenskap, <br> Standardvärde |
| [!UICONTROL Standard Tags] | Fältetikett, <br> Mappa till egenskap, <br> Standardvärde, <br> Beskrivning |

1. Klicka på **[!UICONTROL Done]**. Metadataprofilen läggs till i listan över profiler i **[!UICONTROL Metadata Profiles]** sida.<br>

   ![Metadataprofil har lagts till på sidan Metadataprofiler](assets/MetadataProfiles-page.png)

### Kopiera en metadataprofil {#copying-a-metadata-profile}

1. Från **[!UICONTROL Metadata Profiles]** väljer du en metadataprofil för att göra en kopia av den.

   ![Kopiera en metadataprofil](assets/metadata-profile-edit-copy-option.png)

1. Klicka på **[!UICONTROL Copy]** i verktygsfältet.
1. I **[!UICONTROL Copy Metadata Profile]** anger du en rubrik för den nya kopian av metadataprofilen.
1. Klicka på **[!UICONTROL Copy]**. Kopian av metadataprofilen visas i listan med profiler på sidan **[!UICONTROL Metadata Profiles]**.

   ![En kopia av metadataprofilen som lagts till på sidan Metadataprofiler](assets/copy-metadata-profile.png)

### Ta bort en metadataprofil {#deleting-a-metadata-profile}

1. Från **[!UICONTROL Metadata Profiles]** väljer du en profil att ta bort.

1. Klicka **[!UICONTROL Delete Metadata Profiles]** i verktygsfältet.
1. Klicka på **[!UICONTROL Delete]** för att bekräfta borttagningsåtgärden. Metadataprofilen tas bort från listan.

<!-- TBD: Revisit to find out the correct config. and update these steps. When fixed, also o
These steps have been carried forward from old AEM versions. See https://helpx.adobe.com/experience-manager/6-2/assets/using/metadata-profiles.html#ApplyingaMetadataProfiletoFolders

### Configuration to apply a metadata profile globally {#apply-a-metadata-profile-globally}

In addition to applying a profile to a folder, you can also apply one globally so that any content uploaded into [!DNL Experience Manager] assets in any folder has the selected profile applied.

You can reprocess assets in a folder that already has an existing metadata profile that you later changed. See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets).

To apply a metadata profile globally, follow these steps:

* Navigate to `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` and apply the appropriate profile and click **[!UICONTROL Save]**.

  ![Apply metadata profile to a folder globally](assets/metadata-profile-folder-setting.png)

* In CRXDE Lite, navigate to the following node: `/content/dam/jcr:content`. Add the property `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` and click **[!UICONTROL Save All]**.

  ![See applied metadata profile to a folder in the JCR in CRXDE](assets/metadata-profile-folder-setting2.png)
-->

## Metadata-schema för en mapp {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] Med kan du skapa metadatascheman för resursmappar, som definierar layouten och metadata som visas på mappegenskapssidor.

### Lägga till ett schemaformulär för mappmetadata {#add-a-folder-metadata-schema-form}

Använd schemaredigeraren för mappmetadata i Forms för att skapa och redigera metadatascheman för mappar.

1. I [!DNL Experience Manager] gränssnitt, gå till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Folder Metadata Schemas]**.
1. På sidan [!UICONTROL Folder Metadata Schema Forms] klickar du på **[!UICONTROL Create]**.
1. Ange ett namn för formuläret och klicka på **[!UICONTROL Create]**. Det nya schemaformuläret visas i listan i [!UICONTROL Schema Forms] sida.

### Redigera schemaformulär för mappmetadata {#edit-folder-metadata-schema-forms}

Du kan redigera ett nyligen tillagt eller befintligt metadatchemaformulär, som innehåller följande:

* Tabbar
* Formulärobjekt på flikar.

Du kan mappa/konfigurera dessa formulärobjekt till ett fält i en metadatanod i CRX-databasen. Du kan lägga till nya flikar eller formulärobjekt i metadatchemaformuläret.

1. På Forms-sidan Schema väljer du det formulär du skapade och väljer sedan **[!UICONTROL Edit]** i verktygsfältet.
1. Klicka på knappen Schemaredigeraren för mappmetadata `+` om du vill lägga till en flik i formuläret. Om du vill byta namn på fliken klickar du på standardnamnet och anger det nya namnet under **[!UICONTROL Settings]**.

   ![custom_tab](assets/custom_tab.png)

   Om du vill lägga till fler flikar klickar du på `+`. Om du vill ta bort klickar du på `X` på en flik.

1. Lägg till en eller flera komponenter från fliken Aktiv **[!UICONTROL Build Form]** -fliken.

   ![adding_components](assets/adding_components.png)

   Om du skapar flera flikar klickar du på en viss flik för att lägga till komponenter.

1. Om du vill konfigurera en komponent markerar du den och ändrar dess egenskaper i **[!UICONTROL Settings]** -fliken.

   Ta bort en komponent från **[!UICONTROL Settings]** -fliken.

   ![configure_properties](assets/configure_properties.png)

1. Spara ändringarna genom att välja **[!UICONTROL Save]** i verktygsfältet.

#### Komponenter för att skapa formulär {#components-to-build-forms}

The **[!UICONTROL Build Form]** På fliken visas formulärobjekt som du använder i schemaformuläret för mappmetadata. The **[!UICONTROL Settings]** på -fliken visas attributen för varje objekt som du väljer i **[!UICONTROL Build Form]** -fliken. Här är en lista över de tillgängliga formulärobjekten i **[!UICONTROL Build Form]** tab:

| Komponentnamn | Beskrivning |
|---|---|
| [!UICONTROL Section Header] | Lägg till en avsnittsrubrik för en lista med gemensamma komponenter. |
| [!UICONTROL Single Line Text] | Lägg till en enkelradig textegenskap. Den lagras som en sträng. |
| [!UICONTROL Multi Value Text] | Lägg till en textegenskap med flera värden. Den lagras som en strängarray. |
| [!UICONTROL Number] | Lägg till en sifferkomponent. |
| [!UICONTROL Date] | Lägg till en datumkomponent. |
| [!UICONTROL Dropdown] | Lägg till en nedrullningsbar lista. |
| [!UICONTROL Standard Tags] | Lägg till en tagg. |
| [!UICONTROL Hidden Field] | Lägg till ett dolt fält. Den skickas som en POST-parameter när resursen sparas. |

#### Redigera formulärobjekt {#editing-form-items}

Om du vill redigera egenskaperna för formulärobjekt klickar du på komponenten och redigerar alla eller en delmängd av följande egenskaper i dialogrutan **[!UICONTROL Settings]** -fliken.

**[!UICONTROL Field Label]**: Namnet på metadataegenskapen som visas på egenskapssidan för mappen.

**[!UICONTROL Map to Property]**: This property specifies the relative path of the folder node in the CRX database where it is saved. Det börjar med &quot;**./**&quot;, vilket anger att sökvägen finns under mappens nod.

Följande är giltiga värden för den här egenskapen:

* `./jcr:content/metadata/dc:title`: Lagrar värdet i mappens metadatanod som egenskapen `dc:title`.

* `./jcr:created`: Visar JCR-egenskapen vid mappens nod. Om du konfigurerar de här egenskaperna i CRXDE rekommenderar Adobe att du markerar dem som Inaktivera redigering eftersom de är skyddade. Annars returneras felet `Asset(s) failed to modify`&#39; inträffar när du sparar resursens egenskaper.

För att komponenten ska visas på rätt sätt i schemaformuläret för metadata ska du inte ta med något utrymme i egenskapssökvägen.

**[!UICONTROL JSON Path]**: Använd den för att ange sökvägen till JSON-filen där du anger nyckelvärdepar för alternativ.

**[!UICONTROL Placeholder]**: Använd den här egenskapen för att ange relevant platshållartext för metadataegenskapen.

**[!UICONTROL Choices]**: Använd den här egenskapen för att ange alternativ i en lista.

**[!UICONTROL Description]**: Använd den här egenskapen om du vill lägga till en kort beskrivning för metadatakomponenten.

**[!UICONTROL Class]**: Den objektklass som egenskapen är associerad med.

### Ta bort schemaformulär för mappmetadata {#delete-folder-metadata-schema-forms}

Du kan ta bort schemaformulär för mappmetadata från Forms-sidan för mappmetadataschema. Om du vill ta bort ett formulär markerar du det och klickar på borttagningsalternativet i verktygsfältet.

![delete_form](assets/delete_form.png)

### Tilldela ett mappmetadatchema {#assign-a-folder-metadata-schema}

Du kan tilldela ett mappmetadatchema till en mapp från Forms-sidan för mappmetadataschema eller när du skapar en mapp.

Om du konfigurerar ett metadataschema för en mapp lagras sökvägen till schemaformuläret i `folderMetadataSchema` egenskap för mappnoden under `./jcr:content`.

#### Tilldela till ett schema från sidan Mappmetadatamatchema {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. I [!DNL Experience Manager] gränssnitt, gå till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Folder Metadata Schemas]**.
1. På Forms-sidan för mappmetadataschema väljer du det schemaformulär som du vill tillämpa på en mapp.
1. Klicka på **[!UICONTROL Apply to Folder(s)]** i verktygsfältet.

1. Välj den mapp som schemat ska tillämpas på och klicka sedan på **[!UICONTROL Apply]**. Om ett metadatamatchema redan används för mappen visas ett varningsmeddelande om att du håller på att skriva över det befintliga metadatamodemet. Klicka på **[!UICONTROL Overwrite]**.
1. Öppna metadataegenskaperna för den mapp som du tillämpade metadataschemat på.

   ![folder_properties](assets/folder_properties.png)

   Om du vill visa metadatafälten för mappen klickar du på **[!UICONTROL Folder Metadata]** -fliken.

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

#### Tilldela ett schema när du skapar en mapp {#assign-a-schema-when-creating-a-folder}

Du kan tilldela ett mappmetadatchema när du skapar en mapp. Om det finns minst ett mappmetadatchema i systemet visas en extra lista i **[!UICONTROL Create Folder]** -dialogrutan. Du kan välja önskat schema. Som standard är inget schema valt.

1. Från [!DNL Experience Manager Assets] användargränssnitt, klicka **[!UICONTROL Create]** i verktygsfältet.
1. Ange en rubrik och ett namn för mappen.
1. Välj önskat schema i listan Mappmetadatamatchema. Klicka sedan på **[!UICONTROL Create]**.

   ![select_schema](assets/select_schema.png)

1. Öppna metadataegenskaperna för den mapp som du tillämpade metadataschemat på.
1. Om du vill visa metadatafälten för mappen klickar du på **[!UICONTROL Folder Metadata]** -fliken.

### Använd mappens metadatamatchema {#use-the-folder-metadata-schema}

Öppna egenskaperna för en mapp som har konfigurerats med ett schema för mappmetadata. A **[!UICONTROL Folder Metadata]** -fliken visas i mappen [!UICONTROL Properties] sida. Om du vill visa formuläret för schemat med mappmetadata väljer du den här fliken.

Ange metadatavärden i de olika fälten och klicka på **[!UICONTROL Save]** för att lagra värdena. De värden du anger lagras i mappnoden i CRX-databasen.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## Tips och begränsningar {#best-practices-limitations}

* Om du vill importera metadata för anpassade namnutrymmen måste du först registrera namnutrymmena.
* Egenskapsväljaren visar egenskaper som används i schemaredigerare och sökformulär. Egenskapsväljaren väljer inte metadataegenskaper för en resurs.
* Det kan finnas befintliga metadataprofiler sedan du uppgraderade till [!DNL Experience Manager] 6.5. Om du har tillämpat en sådan profil i mappen efter uppgraderingen [!UICONTROL Properties] in [!UICONTROL Metadata Profiles] visas inte metadatafälten. Om du däremot använder en ny metadataprofil visas formulärfälten, men de är inte tillgängliga som förväntat. Funktionsbortfall är inte kvar, men om du vill se (ej tillgängliga) formulärfält redigerar du och sparar de befintliga metadataprofilerna.

>[!MORELIKETHIS]
>
>* [Metadatabegrepp och -förståelse](metadata-concepts.md).
>* [Redigera metadataegenskaper för flera samlingar](manage-collections.md#editing-collection-metadata-in-bulk).
>* [Import och export av metadata i Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-export.html).
>* [Profiler för att bearbeta metadata, bilder och videoklipp](processing-profiles.md).
>* [De bästa sätten att ordna digitala resurser så att de kan använda bearbetningsprofiler](/help/assets/organize-assets.md).
>* [XMP](/help/assets/xmp-writeback.md).

