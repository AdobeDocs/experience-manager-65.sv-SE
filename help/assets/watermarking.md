---
title: Lägg till vattenstämpel i era digitala resurser.
description: Lär dig hur du använder funktionen Vattenstämpel för att lägga till en digital vattenstämpel till resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5035d3457187f4d5fe5c2af255a1a886df7291b4
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# Vattenstämpla era digitala resurser {#watermarking}

[!DNL Adobe Experience Manager Assets] gör att du kan lägga till en digital vattenstämpel till resurser som hjälper användarna att verifiera autenticiteten och upphovsrätten till resurserna. [!DNL Experience Manager Assets] stöder text som ska användas som vattenstämpel i PNG- och JPEG-filer.

Om du vill kunna använda vattenstämpel på resurser lägger du till vattenstämpelsteget i [!UICONTROL DAM Update Asset] arbetsflödet.

1. Gå till [!DNL Experience Manager] användargränssnittet och gå till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. Markera arbetsflödet på **[!UICONTROL Workflow Models]** sidan och klicka sedan på **[!UICONTROL DAM Update Asset]****[!UICONTROL Edit]**.

1. Dra **[!UICONTROL Add Watermark]** steget från sidopanelen till [!UICONTROL DAM Update Asset] arbetsflödet.

   ![Dra [!UICONTROL Add Watermark] steget och lägg till det i [!UICONTROL DAM Update Asset] arbetsflödet](assets/add_watermark_step_aem_assets.png)2
   *Bild: Dra[!UICONTROL Add Watermark]steget och lägg till det i[!UICONTROL DAM Update Asset]arbetsflödet.*

   >[!NOTE]
   >
   >Placera [!UICONTROL Add Watermark] steget var som helst före [!UICONTROL Process Thumbnail] steget.

1. Öppna **[!UICONTROL Add Watermark]** steget för att visa dess egenskaper.
1. Ange giltiga värden i de olika fälten på **[!UICONTROL Arguments]** fliken, inklusive text, teckensnittstyp, storlek, färg, position, orientering och så vidare. Bekräfta ändringarna genom att klicka på **[!UICONTROL Done]**.

   ![Ange argumenten i steget Lägg till vattenstämpel i Resurser](assets/arguments_add_watermark_aem_assets.png)

   *Bild: Ange argumenten i steget Lägg till vattenstämpel i[!DNL Assets].*

1. Save the **[!UICONTROL DAM Update Asset]** workflow with the watermark step.
1. Ladda upp en exempelresurs från [!DNL Assets] användargränssnittet. Vattenstämpeln visas med teckensnittsstorlek, färg o.s.v. på den plats som du konfigurerade i ovanstående steg.

Om du vill skapa vattenstämplar i PDF-dokument med programkod eller med dynamisk information bör du överväga att använda [AEM Document Services](/help/forms/using/overview-aem-document-services.md) .
