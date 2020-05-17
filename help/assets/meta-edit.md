---
title: Redigera eller lägga till metadata
description: Läs om metadata för resurser i [!DNL Adobe Experience Manager Assets] och olika sätt att redigera metadata för resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5d66bf75a6751e41170e6297d26116ad33c2df44
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 1%

---


# Redigera eller lägga till metadata {#how-to-edit-or-add-metadata}

Metadata är ytterligare information om resursen som kan sökas igenom. Den extraheras automatiskt när du överför en bild. Du kan redigera befintliga metadata eller lägga till nya metadataegenskaper i befintliga fält (till exempel när ett metadatafält är tomt).

Eftersom organisationer behöver styrda och tillförlitliga metadata-ordlistor går det inte att lägga till nya metadataegenskaper på begäran [!DNL Experience Manager Assets] . Även om författare inte kan lägga till nya metadatafält för resurser kan utvecklare göra det. Se [Skapa metadataegenskap för resurser](meta-edit.md#editing-metadata-schema).

## Redigera metadata för en resurs {#editing-metadata-for-an-asset}

Så här redigerar du metadata:

1. Gör något av följande:

   * I [!DNL Assets] gränssnittet markerar du resursen och klickar på **[!UICONTROL View Properties]** i verktygsfältet.
   * Välj snabbåtgärden från miniatyrbilden av resursen **[!UICONTROL View Properties]** .
   * Klicka på **[!UICONTROL View Properties]** chlimage_1-168 ![](assets/chlimage_1-168.png) i verktygsfältet på resurssidan.
   Resurssidan visar alla metadata för resursen. Metadata extraheras när resursen överförs (hämtas) till [!DNL Experience Manager].

   ![välj resursegenskaper för att visa metadata](assets/asset-metadata.png)

   *Bild: Redigera eller lägga till metadata på[!UICONTROL Properties]resurssidan.*

1. Make edits to the metadata under the various tabs, as required, and when completed, click **[!UICONTROL Save]** from the toolbar to save your changes. Click **[!UICONTROL Close]** to return to the [!DNL Assets] web interface.

   >[!NOTE]
   >
   >Om ett textfält är tomt finns det ingen befintlig metadatauppsättning. Du kan ange ett värde i fältet och spara det för att lägga till metadataegenskapen.

Alla ändringar av metadata för en resurs skrivs tillbaka till den ursprungliga binärfilen som en del av dess XMP-data. Metadataåterskrivningsarbetsflödet lägger till metadata i den ursprungliga binärfilen. Ändringar som görs i befintliga egenskaper (till exempel `dc:title`) skrivs över och nya egenskaper (inklusive anpassade egenskaper som `cq:tags`) läggs till i schemat.

XMP-återskrivning stöds och är aktiverat för de plattformar och filformat som beskrivs i de [tekniska kraven.](/help/sites-deploying/technical-requirements.md)

## Redigera metadatamatchema {#editing-metadata-schema}

Mer information finns i [Redigera schemaformulär](metadata-schemas.md#edit-metadata-schema-forms)för metadata.

## Registrera ett anpassat namnutrymme i [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

Du kan lägga till egna namnutrymmen i [!DNL Experience Manager]. Precis som det finns fördefinierade namnutrymmen som `cq`, `jcr`och `sling`kan du ha ett namnutrymme för databasens metadata och XML-bearbetning.

1. Gå till administrationssidan för nodtypen `https:[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Klicka **[!UICONTROL Namespaces]** överst på sidan. Namnutrymmesadministrationssidan visas i ett fönster.

1. Klicka **[!UICONTROL New]** längst ned om du vill lägga till ett namnutrymme.
1. Ange ett anpassat namnutrymme i XML-namnutrymmeskonventionen. Ange ID:t i form av en URI och ett associerat prefix för id:t. Klicka på **[!UICONTROL Save]**.
