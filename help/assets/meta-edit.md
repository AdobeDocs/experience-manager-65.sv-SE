---
title: Redigera eller lägga till metadata
description: Lär dig mer om metadata för resurser [!DNL Adobe Experience Manager Assets] på olika sätt där du kan redigera metadata för resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 4748eed3ce484e8446b641ccbc7b5d76cb66f428
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 1%

---


# Redigera eller lägga till metadata {#how-to-edit-or-add-metadata}

Metadata är ytterligare information om resursen som kan sökas igenom. Den extraheras automatiskt när du överför en bild. Du kan redigera befintliga metadata eller lägga till nya metadataegenskaper i befintliga fält, till exempel när ett metadatafält är tomt.

Organisationer behöver kontrollerade och tillförlitliga metadata-språk. Det går alltså [!DNL Experience Manager Assets] inte att lägga till nya metadataegenskaper på begäran. Utvecklare och inte författare kan lägga till nya metadatafält för resurser. Se [Skapa metadataegenskap för resurser](meta-edit.md#editing-metadata-schema).

## Redigera metadata för en resurs {#editing-metadata-for-an-asset}

Så här redigerar du metadata:

1. Gör något av följande:

   * I [!DNL Assets] gränssnittet markerar du resursen och klickar på **[!UICONTROL View Properties]** i verktygsfältet.
   * Välj snabbåtgärden från miniatyrbilden av resursen **[!UICONTROL View Properties]** .
   * På sidan Resurser klickar du på ikonen **[!UICONTROL View Properties]** ![](assets/do-not-localize/info-circle-icon.png) Resurser i verktygsfältet.

   Resurssidan visar alla metadata för resursen. Metadata extraheras när resursen överförs (hämtas) till [!DNL Experience Manager].

   ![Välj Egenskaper för en resurs för att visa dess metadata](assets/asset-metadata.png)

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

1. Gå till administrationssidan för nodtypen `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Du öppnar sidan för namnutrymmesadministration genom att klicka på **[!UICONTROL Namespaces]** överst på sidan.
1. Om du vill lägga till ett namnutrymme klickar du **[!UICONTROL New]** längst ned på sidan.
1. Ange ett anpassat namnutrymme i XML-namnutrymmeskonventionen. Ange ID:t i form av en URI och ett associerat prefix för ID:t. Klicka på **[!UICONTROL Save]**.

>[!MORELIKETHIS]
>
>* [Om metadata och dess behov i Assets](metadata.md)
>* [XMP-metadata](xmp.md)
>* [Referens för metadatamappningar](meta-ref.md)

