---
title: Resursinsikter
description: Lär dig hur funktionen Assets Insights gör att du kan spåra användarbetyg och användningsstatistik för bilder som används på tredjepartswebbplatser, marknadsföringskampanjer och Adobe kreativa lösningar.
contentOwner: AG
role: Business Practitioner, Administrator
feature: Resursinsikter,Resursrapporter
exl-id: 0130ac40-a72b-4caf-a10f-3c7d76eaa1e6
source-git-commit: 68c36d4e3a14567a4d115ee64a4474bcaf9aa386
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 2%

---

# Resursinsikter {#asset-insights}

Med funktionen Assets Insights kan ni spåra användarbetyg och användningsstatistik för bilder som används på tredjepartswebbplatser, marknadsföringskampanjer och Adobe kreativa lösningar. Det hjälper till att få insikter om deras prestanda och popularitet.

[!DNL Assets] Insikter fångar upp användaraktivitetsinformation, t.ex. hur många gånger en bild klassificeras, klickas och hur många gånger bilden läses in på webbplatsen. Det tilldelar poäng till bilder baserat på denna statistik. Du kan använda resultat och prestandastatistik för att välja populära bilder som ska ingå i kataloger, marknadsföringskampanjer och så vidare. Man kan till och med utforma arkiverings- och licensförnyelseregler baserat på denna statistik.

För att [!DNL Assets]-insikter ska kunna samla in användningsstatistik för bilder från en webbplats måste du inkludera bildens inbäddningskod i webbplatskoden.

Om du vill att Assets Insights ska visa användningsstatistik för resurser måste du först konfigurera funktionen så att rapporteringsdata hämtas från Adobe Analytics. Mer information finns i [Konfigurera resursinsikter](/help/assets/configure-asset-insights.md). Om du vill använda den här funktionen i en lokal installation måste du köpa [!DNL Adobe Analytics]-licensen separat. Kunder på [!DNL Managed Services] får [!DNL Analytics] licens som paketerats med [!DNL Experience Manager]. Se [Managed Services produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>Insikter stöds endast och tillhandahålls för bilder.

## Visa statistik för en bild {#viewing-statistics-for-an-image}

Du kan visa bakgrundsmusik för resursinsikter från metadatasidan.

1. I användargränssnittet för [!DNL Assets] markerar du bilden och klickar sedan på **[!UICONTROL Properties]** i verktygsfältet.
1. Klicka på fliken **[!UICONTROL Insights]** på sidan Egenskaper.
1. Granska användningsinformationen för resursen på fliken **[!UICONTROL Insights]**. Avsnittet **[!UICONTROL Score]** beskriver den totala resursanvändningen och prestandan för en tillgång.

   Användningspoäng beskriver hur många gånger resursen används i olika lösningar.

   **[!UICONTROL Impressions]**-poängen är antalet gånger som resursen läses in på webbplatsen. Siffran som visas under **[!UICONTROL Clicks]** är antalet gånger som användaren klickar på resursen.

1. Gå igenom **[!UICONTROL Usage Statistics]**-avsnittet för att ta reda på vilka enheter resursen var en del av och vilka kreativa lösningar som nyligen har använt den. Ju högre användning, desto större chans att resursen är populär bland användarna. Användningsdata visas under följande rubriker:

   * **Resurs**: Antalet gånger som tillgången var en del av en samling eller sammansatt tillgång
   * **Webb och mobil**: Antalet gånger som resursen ingick i webbplatser och appar
   * **Socialt**: Antalet gånger som resursen användes i lösningar som Adobe Social och Adobe Campaign
   * **E-post**: Antalet gånger som resursen användes i e-postkampanjer

   ![användningsstatistik](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Eftersom funktionen Assets Insights (Resursinsikter) vanligtvis hämtar data från Adobe Analytics från lösningar med jämna mellanrum, kanske inte avsnittet Lösningar visar de senaste data. Den tidsperiod som data visas för beror på schemat för hämtningsåtgärden som Assets Insights kör för att hämta Analytics-data.

1. Om du vill visa prestandastatistik för resursen grafiskt över en tidsperiod väljer du period i **[!UICONTROL Performance Statistics]**-avsnittet. Detaljer, inklusive klick och visningar, visas som trendlinjer i ett diagram.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >Till skillnad från data i avsnittet Lösningar visar avsnittet Prestandastatistik de senaste data.

1. Om du vill hämta inbäddningskoden för resursen som du inkluderar på webbplatser för att få prestandadata klickar du **[!UICONTROL Get Embed Code]** under miniatyrbilden för resursen. Mer information om hur du inkluderar din inbäddade kod i tredjepartswebbsidor finns i [Använda sidspåraren och bädda in kod i webbsidor](/help/assets/use-page-tracker.md).

   ![chlimage_1-98](assets/chlimage_1-303.png)

## Visa sammanställningsstatistik för bilder {#viewing-aggregate-statistics-for-images}

Du kan visa bakgrundsmusik för alla resurser i en mapp samtidigt med **[!UICONTROL Insights View]**.

1. I [!DNL Assets]-användargränssnittet navigerar du till mappen som innehåller de resurser som du vill visa insikter för.
1. Klicka på Layout i verktygsfältet och välj sedan **[!UICONTROL Insights View]**.
1. På sidan visas användningsresultat för resurserna. Jämför omdömen om de olika tillgångarna och få insikter.

## Schemalägg bakgrundsjobb {#scheduling-background-job}

Assets Insights hämtar användningsdata för resurser från Adobe Analytics rapportsviter regelbundet. Som standard kör Assets Insights ett bakgrundsjobb var 24:e timme kl. 2:00 för att hämta data. Du kan dock ändra både frekvens och tid genom att konfigurera tjänsten **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** från webbkonsolen.

1. Klicka på logotypen [!DNL Experience Manager] och gå till **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Öppna tjänstkonfigurationen för **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]**.

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. Ange önskad schemaläggningsfrekvens och starttid för jobbet i egenskapsschemaläggaruttrycket. Spara ändringarna.
