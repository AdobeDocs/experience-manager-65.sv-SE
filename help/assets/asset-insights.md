---
title: Resursinsikter
description: Lär dig hur funktionen Assets Insights gör att du kan spåra användarbetyg och användningsstatistik för bilder som används på tredjepartswebbplatser, marknadsföringskampanjer och Adobe kreativa lösningar.
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 0130ac40-a72b-4caf-a10f-3c7d76eaa1e6
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 3%

---

# Resursinsikter {#asset-insights}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/assets-insights.html?lang=en) |
| AEM 6.5 | Den här artikeln |
| AEM 6.4 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/touch-ui-configuring-asset-insights.html?lang=en) |

Med funktionen Assets Insights kan ni spåra användarbetyg och användningsstatistik för bilder som används på tredjepartswebbplatser, marknadsföringskampanjer och Adobe kreativa lösningar. Det hjälper till att få insikter om deras prestanda och popularitet.

[!DNL Assets] Insikter fångar upp användaraktivitetsinformation, t.ex. hur många gånger en bild klassificeras, klickas och hur många gånger bilden läses in på webbplatsen. Det tilldelar poäng till bilder baserat på denna statistik. Du kan använda resultat och prestandastatistik för att välja populära bilder som ska ingå i kataloger, marknadsföringskampanjer och så vidare. Man kan till och med utforma arkiverings- och licensförnyelseregler baserat på denna statistik.

För [!DNL Assets] Insikter för att hämta användningsstatistik för bilder från en webbplats måste du inkludera inbäddningskoden för bilden i webbplatskoden.

Om du vill att Assets Insights ska visa användningsstatistik för resurser måste du först konfigurera funktionen så att rapporteringsdata hämtas från Adobe Analytics. Mer information finns i [Konfigurera resursinsikter](/help/assets/configure-asset-insights.md). Om du vill använda den här funktionen i en lokal installation ska du köpa [!DNL Adobe Analytics] separat. Kunder på [!DNL Managed Services] ta [!DNL Analytics] licens som medföljer [!DNL Experience Manager]. Se [Managed Services produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>Insikter stöds endast och tillhandahålls för bilder.

## Visa statistik för en bild {#viewing-statistics-for-an-image}

Du kan visa bakgrundsmusik för resursinsikter från metadatasidan.

1. Från [!DNL Assets] användargränssnitt, markera bilden och klicka sedan på **[!UICONTROL Properties]** i verktygsfältet.
1. På sidan Egenskaper klickar du på **[!UICONTROL Insights]** -fliken.
1. Granska användningsinformationen för resursen i **[!UICONTROL Insights]** -fliken. The **[!UICONTROL Score]** I avsnittet beskrivs den totala användningen av tillgångar och prestandan för en tillgång.

   Användningspoäng beskriver hur många gånger resursen används i olika lösningar.

   The **[!UICONTROL Impressions]** poäng är antalet gånger som resursen läses in på webbplatsen. Numret som visas under **[!UICONTROL Clicks]** är antalet gånger som användaren klickar på resursen.

1. Granska **[!UICONTROL Usage Statistics]** för att ta reda på vilka enheter resursen ingick i och vilka kreativa lösningar som nyligen använde den. Ju högre användning, desto större chans att resursen är populär bland användarna. Användningsdata visas under följande rubriker:

   * **Tillgång**: Antalet gånger som tillgången var en del av en samling eller sammansatt tillgång
   * **Webb och mobil**: Antalet gånger som resursen ingick i webbplatser och appar
   * **Social**: Antalet gånger som resursen användes i lösningar som Adobe Social och Adobe Campaign
   * **E-post**: Antalet gånger som resursen användes i e-postkampanjer

   ![användningsstatistik](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Eftersom funktionen Assets Insights (Resursinsikter) vanligtvis hämtar data från Adobe Analytics från lösningar med jämna mellanrum, kanske inte avsnittet Lösningar visar de senaste data. Den tidsperiod som data visas för beror på schemat för hämtningsåtgärden som Assets Insights kör för att hämta Analytics-data.

1. Om du vill visa prestandastatistik för resursen grafiskt över en tidsperiod väljer du period i **[!UICONTROL Performance Statistics]** -avsnitt. Detaljer, inklusive klick och visningar, visas som trendlinjer i ett diagram.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >Till skillnad från data i avsnittet Lösningar visar avsnittet Prestandastatistik de senaste data.

1. Om du vill hämta inbäddningskoden för resursen som du inkluderar på webbplatser för att få prestandadata klickar du på **[!UICONTROL Get Embed Code]** under miniatyrbilden av resursen. Mer information om hur du inkluderar din inbäddningskod på webbsidor från tredje part finns i [Använda sidspåraren och bädda in kod på webbsidor](/help/assets/use-page-tracker.md).

   ![chlimage_1-98](assets/chlimage_1-303.png)

## Visa sammanställd statistik för bilder {#viewing-aggregate-statistics-for-images}

Du kan visa bakgrundsmusik för alla resurser i en mapp samtidigt med **[!UICONTROL Insights View]**.

1. I [!DNL Assets] -användargränssnittet, navigera till den mapp som innehåller de resurser som du vill visa insikter för.
1. Klicka på Layout i verktygsfältet och välj sedan **[!UICONTROL Insights View]**.
1. På sidan visas användningsresultat för resurserna. Jämför omdömen om de olika tillgångarna och få insikter.

## Schemalägg bakgrundsjobb {#scheduling-background-job}

Assets Insights hämtar användningsdata för resurser från Adobe Analytics rapportsviter regelbundet. Som standard kör Assets Insights ett bakgrundsjobb var 24:e timme kl. 2:00 för att hämta data. Du kan dock ändra både frekvens och tid genom att konfigurera **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** från webbkonsolen.

1. Klicka på [!DNL Experience Manager] logotyp och gå till **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Öppna **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** tjänstkonfiguration.

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. Ange önskad schemaläggningsfrekvens och starttid för jobbet i egenskapsschemaläggaruttrycket. Spara ändringarna.
