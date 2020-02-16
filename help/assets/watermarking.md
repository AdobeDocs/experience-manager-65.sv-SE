---
title: Lägg till vattenstämpel i era digitala resurser.
description: Lär dig hur du använder funktionen Vattenstämpel för att lägga till en digital vattenstämpel till resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Vattenstämpla era digitala resurser {#watermarking}

Med Adobe Experience Manager Assets (AEM) kan ni lägga till en digital vattenstämpel i mediefiler som hjälper användarna att verifiera autenticiteten och upphovsrättsinnehållet i mediefilerna. AEM Resurser stöder text som ska användas som vattenstämpel i PNG- och JPEG-filer.

Om du vill kunna använda vattenstämpel på resurser lägger du till vattenstämpelsteget i arbetsflödet för [!UICONTROL DAM-uppdatering av resurser] .

1. Gå till AEM-användargränssnittet och gå till **[!UICONTROL Verktyg]** > **[!UICONTROL Arbetsflöde]** > **[!UICONTROL Modeller]**.
1. På sidan **[!UICONTROL Arbetsflödesmodeller]** väljer du arbetsflödet **[!UICONTROL DAM-uppdatering av resurs]** och klickar på **[!UICONTROL Redigera]**.

1. Dra steget **[!UICONTROL Lägg till vattenstämpel]** från sidopanelen till arbetsflödet för [!UICONTROL DAM-uppdatering av resurser] .

   ![Dra steget Lägg till vattenstämpel och lägg till i arbetsflödet för DAM-uppdateringsresurser](assets/add_watermark_step_aem_assets.png)

   >[!NOTE]
   >
   >Placera steget [!UICONTROL Lägg till vattenstämpel] var som helst före steget [!UICONTROL Bearbeta miniatyrbild] .

1. Öppna steget **[!UICONTROL Lägg till vattenstämpel]** för att visa dess egenskaper.
1. På fliken **[!UICONTROL Argument]** anger du giltiga värden i de olika fälten, inklusive text, teckensnittstyp, storlek, färg, position, orientering och så vidare. Bekräfta ändringarna genom att trycka/klicka på ikonen Klar.

   ![Ange argumenten i steget Lägg till vattenstämpel i Resurser](assets/arguments_add_watermark_aem_assets.png)

1. Spara arbetsflödet för **[!UICONTROL DAM-uppdatering av resurser]** med vattenstämpelsteget.
1. Ladda upp en exempelresurs från Assets-användargränssnittet. Vattenstämpeln visas med teckensnittsstorlek, färg o.s.v. på den plats som du konfigurerade i ovanstående steg.
