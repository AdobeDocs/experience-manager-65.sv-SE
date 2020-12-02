---
title: Lägg till vattenstämpel i dina digitala resurser
description: Lär dig hur du använder funktionen Vattenstämpel för att lägga till en digital vattenstämpel till resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# Vattenstämpla dina digitala resurser {#watermarking}

[!DNL Adobe Experience Manager Assets] gör att du kan lägga till en digital vattenstämpel till resurser som hjälper användarna att verifiera autenticiteten och upphovsrätten till resurserna. [!DNL Experience Manager Assets] stöder text som ska användas som vattenstämpel i PNG- och JPEG-filer.

Om du vill kunna använda vattenstämpel på resurser lägger du till vattenstämpelsteget i [!UICONTROL DAM Update Asset]-arbetsflödet.

1. Gå till [!DNL Experience Manager]-användargränssnittet och gå till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. På sidan **[!UICONTROL Workflow Models]** väljer du arbetsflödet för **[!UICONTROL DAM Update Asset]** och klickar på **[!UICONTROL Edit]**.

1. Dra **[!UICONTROL Add Watermark]**-steget från sidopanelen till [!UICONTROL DAM Update Asset]-arbetsflödet.

   ![Dra  [!UICONTROL Add Watermark] steget och lägg till det i  [!UICONTROL DAM Update Asset] arbetsflödet](assets/add_watermark_step_aem_assets.png)
2
   *Bild: Dra  [!UICONTROL Add Watermark] steget och lägg till det i  [!UICONTROL DAM Update Asset] arbetsflödet.*

   >[!NOTE]
   >
   >Placera [!UICONTROL Add Watermark]-steget var som helst före [!UICONTROL Process Thumbnail]-steget.

1. Öppna **[!UICONTROL Add Watermark]**-steget för att visa dess egenskaper.
1. På fliken **[!UICONTROL Arguments]** anger du giltiga värden i de olika fälten, inklusive text, teckensnittstyp, storlek, färg, position, orientering och så vidare. Bekräfta ändringarna genom att klicka på **[!UICONTROL Done]**.

   ![Ange argumenten i steget Lägg till vattenstämpel i Resurser](assets/arguments_add_watermark_aem_assets.png)

   *Bild: Ange argumenten i steget Lägg till vattenstämpel i  [!DNL Assets].*

1. Spara arbetsflödet **[!UICONTROL DAM Update Asset]** med vattenstämpelsteget.
1. Ladda upp en exempelresurs från [!DNL Assets]-användargränssnittet. Vattenstämpeln visas med teckensnittsstorlek, färg o.s.v. på den plats som du konfigurerade i ovanstående steg.

Om du vill lägga till en vattenstämpel i PDF-dokument med programkod eller med dynamisk information kan du överväga att använda erbjudandet [Experience Manager Document Services](/help/forms/using/overview-aem-document-services.md).
