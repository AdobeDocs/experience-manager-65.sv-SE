---
title: Lägg till vattenstämpel i dina digitala resurser
description: Lär dig hur du använder funktionen Vattenstämpel för att lägga till en digital vattenstämpel till resurser.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
hide: true
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 1%

---

# Vattenstämpla era digitala resurser {#watermarking}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/watermark-assets.html?lang=en) |
| AEM 6.5 | Den här artikeln |

[!DNL Adobe Experience Manager Assets] Med kan du lägga till en digital vattenstämpel till resurser som hjälper användarna att verifiera autenticiteten och upphovsrättsinnehållet i resurserna. [!DNL Experience Manager Assets] stöder text som ska användas som vattenstämpel i PNG- och JPEG-filer.

Om du vill kunna använda vattenstämpel på resurser lägger du till vattenstämpelsteget i [!UICONTROL DAM Update Asset] arbetsflöde.

1. Öppna [!DNL Experience Manager] användargränssnitt och gå till **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. Från **[!UICONTROL Workflow Models]** väljer du **[!UICONTROL DAM Update Asset]** och klicka **[!UICONTROL Edit]**.

1. Dra från sidopanelen **[!UICONTROL Add Watermark]** till [!UICONTROL DAM Update Asset] arbetsflöde.

   ![Dra [!UICONTROL Add Watermark] steg och lägga till [!UICONTROL DAM Update Asset] arbetsflöde](assets/add_watermark_step_aem_assets.png)

   *Bild: Dra [!UICONTROL Add Watermark] steg och lägga till [!UICONTROL DAM Update Asset] arbetsflöde.*

   >[!NOTE]
   >
   >Placera [!UICONTROL Add Watermark] var som helst före [!UICONTROL Process Thumbnail] steg.

1. Öppna **[!UICONTROL Add Watermark]** för att visa dess egenskaper.
1. I **[!UICONTROL Arguments]** anger du giltiga värden i de olika fälten, inklusive text, teckensnittstyp, storlek, färg, position, orientering och så vidare. Bekräfta ändringarna genom att klicka **[!UICONTROL Done]**.

   ![Ange argumenten i steget Lägg till vattenstämpel i [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *Bild: Ange argumenten i steget Lägg till vattenstämpel i [!DNL Assets].*

1. Spara **[!UICONTROL DAM Update Asset]** arbetsflöde med vattenstämpelsteget.
1. Från [!DNL Assets] -användargränssnittet, överföra en exempelresurs. Vattenstämpeln visas med teckensnittsstorlek, färg o.s.v. på den plats som du konfigurerade i ovanstående steg.

Om du vill lägga till en vattenstämpel i PDF-dokument med programkod eller med dynamisk information bör du överväga att använda [Experience Manager dokumenttjänster](/help/forms/using/overview-aem-document-services.md) erbjuder.

## Tips och begränsningar {#tips-limitations}

* Endast textbaserade vattenstämplar stöds. Bilder används inte som vattenstämplar, även om du kan överföra bilder när du skapar [!UICONTROL Add Watermark Process].
* Endast PNG- och JPEG-filer kan ha vattenstämplar. Andra resursformat har ingen vattenstämpel.
