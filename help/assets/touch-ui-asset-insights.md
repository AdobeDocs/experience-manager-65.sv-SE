---
title: 'Asset Insights '
description: Lär dig hur funktionen för tillgångsinsikter gör att du kan spåra användarbetyg och användningsstatistik för bilder som används på tredjepartswebbplatser, marknadsföringskampanjer och Adobes kreativa lösningar.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b59f7471ab9f3c5e6eb3365122262b592c8e6244
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 3%

---


# Asset Insights {#asset-insights}

Med funktionen för tillgångsinsikter kan du spåra användarbetyg och användningsstatistik för bilder som används på tredjepartswebbplatser, marknadsföringskampanjer och Adobes kreativa lösningar. Det hjälper till att få insikter om deras prestanda och popularitet.

Assets Insights samlar in information om användaraktivitet, t.ex. hur många gånger en bild klassificeras, klickas och hur många gånger bilden läses in på webbplatsen. Det tilldelar poäng till bilder baserat på denna statistik. Du kan använda resultat och prestandastatistik för att välja populära bilder som ska ingå i kataloger, marknadsföringskampanjer och så vidare. Man kan till och med utforma arkiverings- och licensförnyelseregler baserat på denna statistik.

För att Assets Insights ska kunna samla in användningsstatistik för bilder från en webbplats måste du inkludera inbäddningskoden för bilden i webbplatskoden.

Om du vill att tillgångsinsikter ska visa användningsstatistik för resurser måste du först konfigurera funktionen för att hämta rapportdata från Adobe Analytics. Mer information finns i [Konfigurera tillgångsinsikter](/help/assets/touch-ui-configuring-asset-insights.md).

>[!NOTE]
>
>Insikter stöds endast och tillhandahålls för bilder.

## Visa statistik för en bild {#viewing-statistics-for-an-image}

Du kan visa poängen för resursinsikter från metadatasidan.

1. Välj bilden i användargränssnittet Resurser och klicka sedan på **[!UICONTROL Properties]** i verktygsfältet.
1. Klicka på fliken på sidan Egenskaper **[!UICONTROL Insights]** .
1. Granska användningsinformationen för resursen på **[!UICONTROL Insights]** fliken. I avsnittet **[!UICONTROL Score]** beskrivs den totala resursanvändningen och prestandan för en tillgång.

   Användningspoäng beskriver hur många gånger resursen används i olika lösningar.

   Poängen **[!UICONTROL Impressions]** är antalet gånger som resursen läses in på webbplatsen. Siffran som visas under **[!UICONTROL Clicks]** är antalet gånger som användaren klickar på resursen.

1. Läs igenom **[!UICONTROL Usage Statistics]** avsnittet för att ta reda på vilka enheter resursen ingick i och vilka kreativa lösningar som nyligen använt den. Ju högre användning, desto större chans att resursen är populär bland användarna. Användningsdata visas under följande rubriker:

   * **Resurs**: Antalet gånger som tillgången var en del av en samling eller sammansatt tillgång
   * **Webb och mobil**: Antalet gånger som resursen ingick i webbplatser och appar
   * **Socialt**: Antalet gånger som resursen användes i lösningar som Adobe Social och Adobe Campaign
   * **E-post**: Antalet gånger som resursen användes i e-postkampanjer
   ![användningsstatistik](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Eftersom funktionen för tillgångsinsikter vanligtvis hämtar data från Adobe Analytics i lösningar regelbundet, kanske inte avsnittet Lösningar visar de senaste data. Den tidsperiod som data visas för beror på schemat för hämtningsåtgärden som resursinsikter körs för att hämta Analytics-data.

1. To view performance statistics for the asset graphically over a period of time, select period in the **[!UICONTROL Performance Statistics]** section. Detaljer, inklusive klick och visningar, visas som trendlinjer i ett diagram.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >Till skillnad från data i avsnittet Lösningar visar avsnittet Prestandastatistik de senaste data.

1. Om du vill hämta inbäddningskoden för resursen som du inkluderar på webbplatser för att få prestandadata klickar du på **[!UICONTROL Get Embed Code]** nedanför miniatyrbilden för resursen. Mer information om hur du inkluderar din inbäddningskod på webbsidor från tredje part finns i [Använda sidspåraren och bädda in kod på webbsidor](/help/assets/touch-ui-using-page-tracker.md).

   ![chlimage_1-98](assets/chlimage_1-303.png)

## Visa sammanställd statistik för bilder {#viewing-aggregate-statistics-for-images}

You can view scores of all assets within a folder simultaneously using **[!UICONTROL Insights View]**.

1. I Assets-användargränssnittet navigerar du till den mapp som innehåller de resurser som du vill visa insikter för.
1. Klicka på Layout i verktygsfältet och välj sedan **[!UICONTROL Insights View]**.
1. På sidan visas användningsresultat för resurserna. Jämför omdömen om de olika tillgångarna och få insikter.

## Schemalägg bakgrundsjobb {#scheduling-background-job}

Resursinsikter hämtar användningsdata för resurser från Adobe Analytics rapporteringsprogram regelbundet. Som standard körs ett bakgrundsjobb var 24:e timme i resursinsikter för att hämta data. Du kan dock ändra både frekvens och tid genom att konfigurera **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** tjänsten från webbkonsolen.

1. Klicka på Experience Manager-logotypen och gå till **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Öppna **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** tjänstkonfigurationen.

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. Ange önskad schemaläggningsfrekvens och starttid för jobbet i egenskapsschemaläggaruttrycket. Spara ändringarna.
