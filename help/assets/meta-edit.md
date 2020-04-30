---
title: Redigera eller lägga till metadata
description: Läs om metadata för resurser i [!DNL Adobe Experience Manager Assets] och olika sätt att redigera metadata för resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# Redigera eller lägga till metadata {#how-to-edit-or-add-metadata}

Metadata är ytterligare information om resursen som kan sökas igenom. Den extraheras automatiskt när du överför en bild. Du kan redigera befintliga metadata eller lägga till nya metadataegenskaper i befintliga fält (till exempel när ett metadatafält är tomt).

Eftersom organisationer behöver kontrollerade och tillförlitliga metadata-ordlistor går det inte att lägga till nya metadataegenskaper [!DNL Experience Manager Assets] för hand. Även om författare inte kan lägga till nya metadatafält för resurser kan utvecklare göra det. Se [Skapa ny metadataegenskap för resurser](meta-edit.md#editing-metadata-schema).

## Redigera metadata för en resurs {#editing-metadata-for-an-asset}

Så här redigerar du metadata:

1. Gör något av följande:

   * I [!DNL Assets] gränssnittet markerar du resursen och klickar på **[!UICONTROL Visa egenskaper]** i verktygsfältet.
   * Välj snabbåtgärden **[!UICONTROL Visa egenskaper]** i miniatyrbilden av resursen.
   * Klicka på **[!UICONTROL Visa egenskaper]** ![chlimage_1-168](assets/chlimage_1-168.png) i verktygsfältet på resurssidan.
   Resurssidan visar alla metadata för resursen. Metadata extraheras när resursen överförs (hämtas) till Experience Manager.

   ![välj resursegenskaper för att visa metadata](assets/asset-metadata.png)

   *Bild: Redigera eller lägga till metadata på sidan Egenskaper för resurser.*

1. Make edits to the metadata under the various tabs, as required, and when completed, click **[!UICONTROL Save]** from the toolbar to save your changes. Click **[!UICONTROL Close]** to return to the Assets web interface.

   >[!NOTE]
   >
   >Om ett textfält är tomt finns det ingen befintlig metadatauppsättning. Du kan ange ett värde i fältet och spara det för att lägga till metadataegenskapen.

Alla ändringar av metadata för en resurs skrivs tillbaka till den ursprungliga binärfilen som en del av dess XMP-data. Detta görs via Experience Managers arbetsflöde för återskrivning av metadata. Ändringar som görs i befintliga egenskaper (t.ex. `dc:title`) skrivs över och nya egenskaper (inklusive anpassade egenskaper som `cq:tags`) läggs ihop med schemat.

XMP-återskrivning stöds och är aktiverat för de plattformar och filformat som beskrivs i de [tekniska kraven.](/help/sites-deploying/technical-requirements.md)

## Redigera metadatamatchema {#editing-metadata-schema}

Mer information om hur du redigerar metadatamatchema finns i [Redigera metadatamatchformulär](metadata-schemas.md#edit-metadata-schema-forms).

## Registrera ett anpassat namnutrymme i Experience Manager {#registering-a-custom-namespace-within-aem}

Du kan lägga till egna namnutrymmen i Experience Manager. Precis som det finns fördefinierade namnutrymmen som cq, jcr och sling kan du ha ett namnutrymme för databasens metadata och XML-bearbetning.

1. Gå till administrationssidan för nodtypen `https:[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Klicka på **[!UICONTROL Namnutrymmen]** högst upp på sidan. Namnutrymmesadministrationssidan visas i ett fönster.

1. Om du vill lägga till ett namnutrymme klickar du på **[!UICONTROL Nytt]** längst ned.
1. Ange ett anpassat namnutrymme i XML-namnutrymmeskonventionen (ange id:t i form av en URI och ett associerat prefix för id:t) och klicka på **[!UICONTROL Spara]**.
