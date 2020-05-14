---
title: 'Metadata-scheman för att definiera layouten för metadataegenskapssidan i [!DNL Adobe Experience Manager Assets]. '
description: Metadata-schemat definierar layouten för egenskapssidan och de metadataegenskaper som visas för resurser. Lär dig hur du skapar anpassade metadatamatcheman, redigerar metadatamatchema och hur du använder metadatamatchema på resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 2366abc3be015fa637621f235edb8e8d79e51372
workflow-type: tm+mt
source-wordcount: '2591'
ht-degree: 7%

---


# Metadata schemas {#metadata-schemas}

Organisationer har en metadatamodell som förbättrar tillgångsidentifiering, användning, interoperabilitet och så vidare. Korrekt metadataanvändning är till stor hjälp för att underhålla metadatadrivna arbetsflöden och processer. Om du vill följa en metadatastrategi och standarder för hela organisationen kan du använda metadatamodeller som hjälper DAM-användare att anpassa sig. Med Adobe Experience Manager kan ni enkelt och flexibelt skapa, underhålla och använda metadatamatchningar.

I [!DNL Adobe Experience Manager Assets]innehåller scheman specifika fält för specifik information som ska fyllas i. Den innehåller även layoutinformation för att visa metadatafält på ett användarvänligt sätt. Metadataegenskaperna innehåller titel, beskrivning, MIME-typer, taggar med mera. Du kan använda redigeraren för att ändra befintliga scheman eller lägga till anpassade metadatamatcheman [!UICONTROL Metadata Schema Forms] .

Så här visar och redigerar du egenskapssidan för en resurs:

1. Klicka på eller tryck på **[!UICONTROL View Properties]** ikonen från Snabbåtgärder på resurspanelen i kortvyn.

   ![Snabbåtgärder på resurspanelen](assets/chlimage_1-170.png)

   Du kan också markera en resurs och sedan klicka på eller trycka på [!UICONTROL Properties] ikonen i verktygsfältet.

1. Du kan redigera de olika redigerbara metadataegenskaperna under de tillgängliga flikarna. Du kan dock inte ändra resursen [!UICONTROL Type] på egenskapsfliken [!UICONTROL Basic] .

   ![Fliken Grundläggande i resursegenskaper, där resurstypen inte kan ändras](assets/asset-properties-basic-tab.png)

*Bild: Fliken Grundläggande för resurs[!UICONTROL Properties].*

Om du vill ändra MIME-typen för en resurs använder du ett anpassat metadatamatchschema eller ändrar ett befintligt formulär. Mer information finns i [Redigera metadata-schemaformulär](/help/assets/metadata-schemas.md#edit-metadata-schema-forms) . Om du ändrar metadataschemat för en viss MIME-typ ändras egenskapssidlayouten för resurser med den aktuella MIME-typen och alla resursundertyper. Om du till exempel ändrar ett jpeg-schema under `default/image` endast ändras metadatalayouten (resursegenskaper) för resurser med MIME-typ `image/jpeg`. Om du redigerar standardschemat ändrar du metadatalayouten för alla typer av resurser.

## Metadata Schema Forms {#default-metadata-schema-forms}

Om du vill visa en lista med formulär/mallar går du till [!DNL Experience Manager] > **[!UICONTROL Tools]** > **[!UICONTROL Assets]** i **[!UICONTROL Metadata Schemas]** gränssnittet.

[!DNL Experience Manager] innehåller följande formulärmallar för metadataschema:

| Mallar |  | Beskrivning |
|---|---|---|
| [!UICONTROL default] |  | Basmetadataschemaformuläret för resurser. |
|  | Följande underordnade formulär ärver egenskaperna för [!UICONTROL default] formuläret: |  |
|  | <ul><li> [!UICONTROL image]</li></ul> | Schemaformulär för resurser med MIME-typen &quot;image&quot;, till exempel image/jpeg, image/png o.s.v. <br> Formuläret har [!UICONTROL image] följande underordnade formulärmallar: <ul><li> [!UICONTROL jpeg]: Schemaformulär för resurser med undertyp [!UICONTROL jpeg].</li> <li>[!UICONTROL tiff]: Schemaformulär för resurser med undertyp [!UICONTROL tiff].</li></ul> |
|  | <ul><li> [!UICONTROL application]</li></ul> | Schemaformulär för resurser med MIME-typen &quot;application&quot;, till exempel application/pdf, application/zip och så vidare. <br>[!UICONTROL pdf]: Schemaformulär för resurser med undertyp pdf. |
|  | <ul><li>[!UICONTROL video]</li></ul> | Schemaformulär för resurser med MIME-typen &quot;video&quot;, till exempel video/avi, video/mp4 och så vidare. |
| [!UICONTROL collection] |  | Schemaformulär för samlingar. |
| [!UICONTROL contentfragment] |  | Schemaformulär för innehållsfragment. |
| [!UICONTROL forms] |  | Det här schemaformuläret gäller [Adobe Experience Manager Forms](/help/forms/home.md). |

>[!NOTE]
>
>Om du vill visa de underordnade formulären för ett schemaformulär klickar du på schemaformulärets namn.

## Lägg till ett metadatamatchformulär {#add-a-metadata-schema-form}

1. Om du vill lägga till en anpassad mall i listan klickar du på **[!UICONTROL Create]** i verktygsfältet.

   >[!NOTE]
   >
   >Oredigerade mallar har en låsikon. Om du anpassar någon av mallarna försvinner låsikonen från före mallen.

1. Ange schemaformulärets rubrik i dialogrutan och klicka **[!UICONTROL Create]** för att slutföra formulärskapandet.

## Redigera metadata-schemaformulär {#edit-metadata-schema-forms}

Du kan redigera ett nyligen tillagt eller befintligt metadatchemaformulär. Metadatchemaformuläret innehåller flikar och formulärobjekt på flikar. Du kan mappa/konfigurera dessa formulärobjekt till ett fält i en metadatanod i CRX-databasen. Du kan lägga till nya flikar eller formulärobjekt i metadatchemaformuläret. Flikarna och formulärobjekten som härleds från det överordnade objektet är låsta. Du kan inte ändra dem på underordnad nivå.

1. In the Schema Forms page, select the check box before a form and then click **[!UICONTROL Edit]** on the toolbar.

1. På sidan **[!UICONTROL Metadata Schema Editor]** anpassar du egenskapssidan för resursen genom att dra en eller flera komponenter från listan med komponenttyper på fliken **[!UICONTROL Build Form]** till fliken **[!UICONTROL Basic]**.

   ![Redigerare för metadatamodell för att anpassa sidan Egenskaper för resurser](assets/metadata-schema-editor.png)

   *Bild:[!UICONTROL Basic]-fliken i[!UICONTROL Metadata Schema]redigeraren.*

1. Om du vill konfigurera en komponent markerar du den och ändrar dess egenskaper på **[!UICONTROL Settings]** fliken.

### Komponenter på fliken Skapa formulär {#components-within-the-build-form-tab}

På **[!UICONTROL Build Form]** fliken visas formulärobjekt som du använder i schemaformuläret. På fliken **[!UICONTROL Settings]** finns attributen för varje objekt som du markerar på **[!UICONTROL Build Form]** fliken. I följande tabell visas de formulärobjekt som är tillgängliga på **[!UICONTROL Build Form]** fliken:

| Komponentnamn | Beskrivning |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| [!UICONTROL Section Header] | Lägg till en avsnittsrubrik för en lista med gemensamma komponenter. |
| [!UICONTROL Single Line Text] | Lägg till en textegenskap för en rad. Den lagras som en sträng. |
| [!UICONTROL Multi Value Text] | Lägg till en textegenskap med flera värden. Den lagras som en strängarray. |
| [!UICONTROL Number] | Lägg till en sifferkomponent. |
| [!UICONTROL Date] | Lägg till en datumkomponent. |
| [!UICONTROL Dropdown] | Lägg till en listruta. |
| [!UICONTROL Standard Tags] | Lägg till en tagg. |
| [!UICONTROL Smart Tags] | Förbättra sökfunktionerna genom att automatiskt lägga till metadatataggar. |
| [!UICONTROL Hidden Field] | Lägg till ett dolt fält. Den skickas som en POST-parameter när resursen sparas. |
| [!UICONTROL Asset Referenced By] | Lägg till den här komponenten för att visa en lista över resurser som resursen refererar till. |
| [!UICONTROL Asset Referencing] | Lägg till om du vill visa en lista med resurser som refererar till resursen. |
| [!UICONTROL Products References] | Lägg till om du vill visa listan över produkter som är länkade till resursen. |
| [!UICONTROL Asset Rating] | Lägg till för att visa alternativ för att klassificera resursen. |
| [!UICONTROL Contextual Metadata] | Lägg till för att styra visningen av andra metadataflikar på egenskapssidan för resurser. |

<!-- TBD: Check against 6.5.4.0 if the list of components is complete.
-->

#### Redigera metadatakomponenten {#edit-the-metadata-component}

Om du vill redigera egenskaperna för en metadatakomponent i formuläret klickar du på komponenten och redigerar alla eller en delmängd av följande egenskaper på **[!UICONTROL Settings]** fliken.

**Fältetikett**: Namnet på metadataegenskapen som visas på egenskapssidan för resursen.

**Mappa till egenskap**: This property specifies the relative path/name to the asset node where it is saved in the CRX database. Det börjar med `./` att ange att sökvägen finns under objektets nod.

Följande är giltiga värden för den här egenskapen:

* `./jcr:content/metadata/dc:title`: Lagrar värdet vid resursens metadatanod som egenskapen `dc:title`.

* `./jcr:created`: Visar JCR-egenskapen vid objektets nod. Om du konfigurerar de här egenskaperna för visning bör du markera dem som Inaktivera redigering, eftersom de är skyddade. Annars [!UICONTROL Asset(s) failed to modify] uppstår felet när du sparar resursens egenskaper.

För att komponenten ska visas korrekt i metadataschemaformuläret bör egenskapssökvägen inte innehålla några blanksteg.

* **Platshållare**: Använd den här egenskapen för att ange relevant platshållartext för metadataegenskapen.
* **Obligatoriskt**: Använd den här egenskapen för att markera en metadataegenskap som obligatorisk på egenskapssidan.
* **Inaktivera redigering**: Använd den här egenskapen för att göra en metadataegenskap icke-redigerbar på egenskapssidan.
* **Visa tomt fält i skrivskyddat**: Markera den här egenskapen om du vill visa en metadataegenskap på egenskapssidan även om den inte har något värde. Om en metadataegenskap inte har något värde visas den inte som standard på egenskapssidan.
* **Visa sorterad** lista: Använd den här egenskapen för att visa en ordnad lista med alternativ
* **Alternativ**: Använd den här egenskapen för att ange alternativ i en lista
* **Beskrivning** : Använd den här egenskapen om du vill lägga till en kort beskrivning för metadatakomponenten.
* **Klass**: Den objektklass som egenskapen är associerad med.
* **Ta bort**: Klicka [!UICONTROL Delete] för att ta bort en komponent från schemaformuläret.

>[!NOTE]
>
>Komponenten [!UICONTROL Hidden Field] innehåller inte dessa attribut. I stället innehåller den egenskaper som till exempel attributnamn, värde, fältetikett och Beskrivning. Värdena för komponenten Dolt fält skickas som en POST-parameter när resursen sparas. Den sparas inte som metadata för resursen.

Om du väljer alternativet **[!UICONTROL Required]** kan du söka efter resurser som saknar obligatoriska metadata. På panelen **[!UICONTROL Filters]** expanderar du predikatet **[!UICONTROL Metadata Validation]** och väljer alternativet **[!UICONTROL Invalid]**. Sökresultatet visar resurser som saknar obligatoriska metadata som du har konfigurerat via schemaformuläret.

![Ett ogiltigt alternativ har valts i metadataverifieringspredikatet på panelen Filter ](assets/chlimage_1-178.png)

Om du lägger till komponenten Sammanhangsbaserade metadata på en flik i ett schemaformulär, visas komponenten som en lista på egenskapssidan med resurser som det aktuella schemat används på. Listan innehåller alla andra flikar förutom den flik som du tillämpade på komponenten Sammanhangsberoende metadata på. För närvarande innehåller den här funktionen grundläggande funktioner för att styra visningen av metadata baserat på sammanhanget.

![Sammanhangsberoende metadatakomponentflikar för resursegenskaper](assets/chlimage_1-179.png)

Om du vill visa en flik på egenskapssidan förutom fliken där komponenten Sammanhangsberoende metadata används, väljer du fliken i listan. Fliken läggs till på egenskapssidan.

![Fliken som valts i listan Sammanhangsberoende metadata visas på sidan med resursegenskaper](assets/contextual-metadata-asset-properties.png)

*Bild: Sammanhangsbaserade metadata på egenskapssidan för resurser.*

### Ange egenskaper i JSON-filen {#specify-properties-in-json-file}

I stället för att ange egenskaper för alternativen på fliken **[!UICONTROL Settings]** kan du definiera alternativen i en JSON-fil genom att ange motsvarande nyckelvärdespar. Ange sökvägen till JSON-filen i fältet **[!UICONTROL JSON Path]**.

#### Lägga till eller ta bort en flik i schemaformuläret {#adding-deleting-a-tab-in-the-schema-form}

Med schemaredigeraren kan du lägga till eller ta bort en flik. The default schema form includes the **[!UICONTROL Basic]**, **[!UICONTROL Advanced]** , **[!UICONTROL IPTC]**, and **[!UICONTROL IPTC Extension]** tabs.

![Standardflikar i formuläret för metadataschema](assets/chlimage_1-181.png)

Klicka `+` för att lägga till en ny flik i ett schemaformulär. Som standard har den nya fliken namnet `Unnamed-1`. Du kan ändra namnet på **[!UICONTROL Settings]** fliken.

Klicka `X` för att ta bort en flik.

![Lägga till eller ta bort en flik med metadatamodigeraren](assets/chlimage_1-182.png)

## Ta bort metadata-schemaformulär {#delete-metadata-schema-forms}

[!DNL Experience Manager] I kan du bara ta bort anpassade schemaformulär. Du kan inte ta bort standardschemaformulär/-mallar. Du kan dock ta bort anpassade ändringar i dessa formulär.

Om du vill ta bort ett formulär markerar du det och klickar på Ta bort.

>[!NOTE]
>
>* När du har tagit bort anpassade ändringar i ett standardformulär, visas låsikonen igen före den i gränssnittet för metadatamatchning för att ange att formuläret har återställts till standardläget.
>* Det går inte att ta bort metadata som inte finns i rutan för schemaformulär i Resurser.


## Schemaformulär för MIME-typer {#schema-forms-for-mime-types}

Resurser innehåller standardformulär för olika MIME-typer. Du kan dock lägga till anpassade formulär för resurser av olika MIME-typer.

### Lägg till nya formulär för MIME-typer {#add-new-forms-for-mime-types}

Skapa ett nytt formulär med lämplig formulärtyp. Om du till exempel vill lägga till en ny mall för undertypen `image/png` skapar du formuläret som ett bildformulär. Schemaformulärets titel är undertypsnamnet. In this case, the title is `png`.

#### Använd en befintlig schemamall för olika MIME-typer {#use-an-existing-schema-template-for-various-mime-types}

Du kan använda en befintlig mall för en annan MIME-typ. Använd till exempel `image/jpeg` formuläret för resurser av MIME-typ `image/png`.

I det här fallet skapar du en ny nod på `/etc/dam/metadataeditor/mimetypemappings` CRX-databasen. Ange ett namn för noden och definiera följande egenskaper:

| Namn | Beskrivning | Typ | Värde |
|------|-------------|------|-------|
| `exposedmimetype` | Namnet på det befintliga formulär som ska mappas | `String` | `image/jpeg` |
| `mimetypes` | Lista över MIME-typer som använder formuläret som definierats i `exposedmimetype` attributet | `String` | `image/png` |

Resurser mappar följande MIME-typer och schemaformulär:

| Schemaformulär | MIME-typer |
| --------------------------- | --------------------------------------------------- |
| image/jpeg | image/pjpeg |
| bild/tiff | image/x-tiff |
| application/pdf | application/postscript |
| application/x-ImageSet | Multipart/Related. type=application/x-ImageSet |
| application/x-SpinSet | Multipart/Related. type=application/x-SpinSet |
| application/x-MixedMediaSet | Multipart/Related. type=application/x-MixedMediaSet |
| video/quicktime | video/x-quicktime |
| video/mpeg4 | video/mp4 |
| video/avi | video/avi, video/msvideo, video/x-msvideo |
| video/wmv | video/x-ms-wmv |
| video/flv | video/x-flv |

## Bevilja åtkomst till metadatamappningar {#grant-access-to-metadata-schemas}

Funktionen Metadata Schema är bara tillgänglig för administratörer. Administratörer kan dock ge åtkomst till icke-administratörer genom att ändra vissa behörigheter. Den som inte är administratör bör ha behörighet att skapa, ändra och ta bort i `/conf` mappen.

## Använd mappspecifika metadata {#apply-folder-specific-metadata}

Med Resurser kan du definiera en variant av ett metadataram och använda det på en viss mapp.

Du kan t.ex. definiera en variant av standardmetadataschemat och använda det på en mapp. När du använder det ändrade schemat åsidosätter det det ursprungliga standardmetadatarammet som används för resurser i mappen.

Endast resurser som har överförts till den mapp som det här schemat används på följer de ändrade metadata som har definierats i variantmetadataschemat. Resurser i andra mappar där det ursprungliga schemat används fortsätter att överensstämma med metadata som definierats i det ursprungliga schemat.

Metadataarv av resurser baseras på det schema som tillämpas på mappen på första nivån i hierarkin. Om en mapp inte innehåller undermappar ärver resurserna i mappen metadata från det schema som används i mappen.

Om mappen har en undermapp ärver resurserna i undermappen metadata från det schema som används på undermappsnivå om ett annat schema används på undermappsnivå. Om inget schema eller samma schema används på undermappsnivå ärver undermappsresurserna metadata från det schema som används på den överordnade mappnivån.

1. Navigera [!DNL Experience Manager] till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]**. Sidan **[!UICONTROL Metadata Schema Forms]** visas.
1. Markera kryssrutan före ett formulär, till exempel standardformuläret för metadata, och klicka på **[!UICONTROL Copy]** och spara det som ett anpassat formulär. Ange ett eget namn för formuläret, till exempel `my_default`. Du kan också skapa ett eget formulär.

1. Markera **[!UICONTROL Metadata Schema Forms]** formuläret på `my_default` sidan och klicka sedan på **[!UICONTROL Edit]**.

1. Lägg till ett textfält i schemaformuläret på **[!UICONTROL Metadata Schema Editor]** sidan. Lägg till exempel till ett fält med etiketten **[!UICONTROL Category]**.

   ![Textfält har lagts till i Formulärredigeraren för metadataschema](assets/text-field-metadata-schema-editor.png)

   *Bild: Textfält har lagts till i formulärredigeraren för metadata.*

1. Klicka på **[!UICONTROL Save]**. Det ändrade formuläret visas på **[!UICONTROL Metadata Schema Forms]** sidan.
1. Klicka **[!UICONTROL Apply to Folder(s)]** i verktygsfältet för att använda anpassade metadata i en mapp.

1. Markera mappen som det ändrade schemat ska tillämpas på och klicka sedan på **[!UICONTROL Apply]**.

   ![Välj en mapp för metadataschemat](assets/chlimage_1-188.png)

1. Om det andra metadataschemat används i mappen visas ett varningsmeddelande om att du håller på att skriva över det befintliga metadataschemat. Klicka på **Skriv över**.
1. Klicka på **OK** för att stänga meddelandet.
1. Navigera till mappen som du tillämpade det ändrade metadataschemat på.

## Definiera obligatoriska metadata {#define-mandatory-metadata}

Du kan definiera obligatoriska fält på mappnivå, vilket tillämpas på resurser som överförs till mappen. Om du överför resurser som saknar metadata för de obligatoriska fält som definierats tidigare visas en visuell indikation på saknade metadata för resurserna i kortvyn.

>[!NOTE]
>
>Ett metadatafält kan definieras som obligatoriskt baserat på värdet i ett annat fält. I kortvyn visas [!DNL Experience Manager] inte varningsmeddelandet om saknade metadata för sådana obligatoriska metadatafält.

1. Navigera [!DNL Experience Manager] till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]**. Sidan **[!UICONTROL Metadata Schema Forms]** visas.
1. Spara standardformuläret för metadata som ett anpassat formulär. Du kan till exempel spara den som `my_default`.

1. Redigera det anpassade formuläret. Lägg till ett obligatoriskt fält. Lägg till exempel till ett **[!UICONTROL Category]** fält och gör fältet obligatoriskt.

   ![Lägg till ett obligatoriskt fält i metadataformuläret genom att välja Obligatoriskt på fliken Regler i Formulärredigeraren för metadataschema](assets/mandatory-field-metadata-schema-editor.png)

   *Bild: Obligatoriskt fält i formulärredigeraren för metadata.*

1. Klicka på **[!UICONTROL Save]**. Det ändrade formuläret visas på **[!UICONTROL Metadata Schema Forms]** sidan. Markera formuläret och klicka sedan på **[!UICONTROL Apply to Folder(s)]** i verktygsfältet för att använda anpassade metadata i en mapp.

1. Navigera till mappen och överför vissa resurser med saknade metadata för det obligatoriska fältet som du lade till i det anpassade formuläret. Ett meddelande om saknade metadata för det obligatoriska fältet visas i kortvyn för resursen.

   ![Meddelande om att obligatoriska metadata saknas i resurskortsvyn vid överföring av resurser i mapp](assets/chlimage_1-192.png)

1. (Valfritt) Åtkomst `https://[aem_server]:[port]/system/console/components/`. Konfigurera och aktivera `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` komponenter som är inaktiverade som standard. Ange en frekvens som ska användas för att [!DNL Experience Manager] kontrollera om metadata för resurserna är giltiga. Den här konfigurationen lägger till en egenskap `hasValidMetadata` till `jcr:content` resurser. Om du använder den här egenskapen [!DNL Experience Manager] kan ogiltiga filterresultat förekomma i en sökning. Om du lägger till en resurs efter en kontroll flaggas resursen inte med `hasValidMetadata` förrän vid nästa schemalagda kontroll. Resurserna visas därför inte i sökfiltren för ogiltiga metadata förrän efter nästa schemalagda kontroll.

   >[!CAUTION]
   >
   >Valideringskontrollerna av metadata är resurskrävande och kan påverka systemets prestanda. Schemalägg kontrollerna därefter. Om servern inte kan hantera inläsningen provar du med att inaktivera det här jobbet.

<!-- TBD: Add this method to find invalid metadata in the metadata article later.
-->
