---
title: Importera och exportera resursmetadata i grupp.
description: Importera och exportera metadata från digitalt material i grupp.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 42532bfe73c44ad04b67afa973eef526f47588cf
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 5%

---


# Importera och exportera metadata för resurser i grupp {#import-and-export-asset-metadata-in-bulk}

[!DNL Adobe Experience Manager Assets] I kan du importera resursmetadata gruppvis med hjälp av en CSV-fil. Du kan göra satsvisa uppdateringar för de nyligen överförda resurserna eller för befintliga resurser genom att importera en CSV-fil. Du kan också importera resursmetadata i grupp från tredjepartssystem i CSV-format.

## Importera metadata {#import-metadata}

Import av metadata är asynkron och påverkar inte systemets prestanda. Samtidig uppdatering av metadata för flera resurser kan vara resurskrävande på grund av XMP-återskrivningsaktivitet om arbetsflödesflaggan är markerad. Planera en sådan import under begränsad serveranvändning så att prestanda för andra användare inte påverkas.

>[!NOTE]
>
>Om du vill importera metadata för anpassade namnutrymmen måste du först registrera namnutrymmena.

1. Navigera till [!DNL Assets] användargränssnittet och klicka **[!UICONTROL Create]** i verktygsfältet.
1. Välj **[!UICONTROL Metadata]** i menyn.
1. In the **[!UICONTROL Metadata Import]** page, click **[!UICONTROL Select File]**. Markera CSV-filen med metadata.
1. Ange följande parametrar. Se ett exempel på en CSV-fil på [metadata-import-sample-file.csv](assets/metadata-import-sample-file.csv).

   | Parametrar för metadataimport | Beskrivning |
   |:---|:---|
   | [!UICONTROL Batch Size] | Antal resurser i en grupp som metadata ska importeras för. Standardvärdet är 50. Maxvärdet är 100. |
   | [!UICONTROL Field Separator] | Standardvärdet är `,` (komma). Du kan ange andra tecken. |
   | [!UICONTROL Multi Value Delimiter] | Avgränsare för metadatavärden. Standardvärdet är `|`. |
   | [!UICONTROL Launch Workflows] | Falskt som standard. När det är inställt på `true` och standardinställningarna för startprogrammet används för [!UICONTROL DAM Metadata WriteBack] arbetsflödet (som skriver metadata till binära XMP-data). Om du aktiverar startarbetsflöden blir systemet långsammare. |
   | [!UICONTROL Asset Path Column Name] | Definierar kolumnnamnet för CSV-filen med resurser. |

1. Tap/click **[!UICONTROL Import]** from the toolbar. När metadata har importerats visas ett meddelande i [!UICONTROL Notification] inkorgen.

1. Om du vill verifiera korrekt import navigerar du till en tillgångs [!UICONTROL Properties] sida och kontrollerar värdena i fälten.

Om du vill lägga till datum och tidsstämpel när du importerar metadata använder du `YYYY-MM-DDThh:mm:ss.fff-00:00` formatet för datum och tid. Datum och tid avgränsas med `T`, `hh` är timmar i 24-timmarsformat, `fff` är nanosekunder och `-00:00` är tidszonsförskjutning. Exempel: `2020-03-26T11:26:00.000-07:00` är 26 mars 2020 kl. 11:26:00.000 PST.

>[!CAUTION]
>
>Om datumformatet inte matchar `YYYY-MM-DDThh:mm:ss.fff-00:00`ställs datumvärdena inte in. Datumformaten för den exporterade CSV-metadatafilen har formatet `YYYY-MM-DDThh:mm:ss-00:00`. Om du vill importera den konverterar du den till ett godkänt format genom att lägga till värdet för nanosekunder som anges av `fff`.

## Exportera metadata {#export-metadata}

Du kan exportera metadata för flera resurser i ett CSV-format. Metadata exporteras asynkront och påverkar inte systemets prestanda. Om du vill exportera metadata går du igenom egenskaperna för objektnoden [!DNL Experience Manager] `jcr:content/metadata` och dess underordnade noder och exporterar metadataegenskaperna i en CSV-fil.

Några exempel på användningsområden för att exportera flera metadata samtidigt är:

* Importera metadata i ett tredjepartssystem när du migrerar resurser.
* Dela metadata med ett större projektteam.
* Testa eller granska metadata för att se om de är kompatibla.
* Gör metadata externt och lokalisera dem separat.

1. Välj den resursmapp som innehåller resurser som du vill exportera metadata för. Välj **[!UICONTROL Export metadata]** i verktygsfältet.

1. In the [!UICONTROL Metadata Export] dialog, specify a name for the CSV file. Om du vill exportera metadata för resurser i undermappar väljer du **[!UICONTROL Include assets in subfolders]**.

   ![Gränssnitt och alternativ för att exportera metadata för alla resurser i en](assets/export_metadata_page.png "mappGränssnitt och alternativ för att exportera metadata för alla resurser i en mapp")

1. Välj önskade alternativ. Ange ett filnamn och vid behov ett datum.

1. Ange i **[!UICONTROL Properties to be exported]** fältet om du vill exportera alla eller specifika egenskaper. Om du väljer Selektiva egenskaper som ska exporteras lägger du till de önskade egenskaperna.

1. Klicka på **[!UICONTROL Export]** i verktygsfältet. Ett meddelande bekräftar att metadata exporteras. Stäng meddelandet.

1. Öppna inkorgsmeddelandet för exportjobbet. Markera jobbet och klicka på **[!UICONTROL Open]** i verktygsfältet. To download the CSV file with the metadata, click **[!UICONTROL CSV Download]** from the toolbar. Klicka på **[!UICONTROL Close]**.

   ![Dialogruta för att hämta CSV-filen som innehåller metadata som exporterats i grupp](assets/csv_download.png)

   *Bild: Dialogruta för att hämta CSV-filen som innehåller metadata som exporterats i grupp.*

## Bästa praxis, begränsningar och tips {#best-practices-limitations-tips}

* CSV-filen för import av metadata för resurser har ett mycket specifikt format. För att spara arbete och tid och undvika oavsiktliga fel kan du börja skapa CSV-filen med formatet för en exporterad CSV-fil.
* När du importerar metadata med hjälp av en CSV-fil är datumformatet `YYYY-MM-DDThh:mm:ss.fff-00:00`obligatoriskt. Om något annat format används ställs datumvärdena inte in. Datumformaten för den exporterade CSV-metadatafilen har formatet `YYYY-MM-DDThh:mm:ss-00:00`. Om du vill importera den konverterar du den till ett godkänt format genom att lägga till värdet för nanosekunder som anges av `fff`.
* Om du vill importera metadata för anpassade namnutrymmen måste du först registrera namnutrymmena.

>[!MORELIKETHIS]
>
>* [Import och export av metadata i Experience Manager Assets](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html)

