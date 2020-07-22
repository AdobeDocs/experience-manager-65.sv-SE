---
title: Relaterade tillgångar
description: Lär dig hur du relaterar digitala resurser som delar vissa gemensamma attribut. Skapa också källbaserade relationer mellan digitala resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 91caca39b0b6c5c0c98b58be02f518901a3d90e3
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 3%

---


# Relaterade tillgångar {#related-assets}

[!DNL Adobe Experience Manager Assets] I kan du manuellt relatera resurser baserat på organisationens behov med hjälp av funktionen för relaterade resurser. Du kan till exempel relatera en licensfil till en resurs eller en bild/video på ett liknande ämne. Du kan relatera resurser som delar vissa gemensamma attribut. Du kan också använda funktionen för att skapa käll-/härledda relationer mellan resurser. Om du till exempel har en PDF-fil som genereras från en INDD-fil kan du koppla PDF-filen till dess INDD-källfil.

Med den här funktionen kan du dela en lågupplöst PDF- eller JPG-fil med leverantörer eller myndigheter och göra den högupplösta INDD-filen tillgänglig endast på begäran.

>[!NOTE]
>
>Endast användare med redigeringsbehörighet för resurser kan relatera och ta bort kopplingen för resurserna.

## Relatera resurser {#relating-assets}

1. I gränssnittet Experience Manager öppnar du **[!UICONTROL Properties]** sidan för en resurs som du vill relatera.

   ![öppna en tillgångs egenskapssida för att relatera resursen](assets/asset-properties-relate-assets.png)

   *Bild:[!DNL Assets][!UICONTROL Properties]sida för att relatera tillgångar.*

   Du kan också välja resursen i listvyn.

   ![chlimage_1-273](assets/chlimage_1-273.png)

   Du kan också välja resursen från en samling.

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. Om du vill koppla en annan resurs till den valda resursen klickar du på **[!UICONTROL Relate]** Relatera ![resurser](assets/do-not-localize/link-relate.png) i verktygsfältet.
1. Gör något av följande:

   * Om du vill relatera källfilen för resursen väljer du **[!UICONTROL Source]** i listan.
   * Om du vill relatera en härledd fil väljer du **[!UICONTROL Derived]** i listan.
   * Om du vill skapa en dubbelriktad relation mellan resurserna väljer du **[!UICONTROL Others]** i listan.

   ![chlimage_1-276](assets/chlimage_1-276.png)

1. Navigera från **[!UICONTROL Select Asset]** skärmen till platsen för resursen som du vill relatera och markera den.

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. Klicka på **[!UICONTROL Confirm]**.
1. Klicka **[!UICONTROL OK]** för att stänga dialogrutan. Beroende på ditt val av relation i steg 3 listas den relaterade resursen under en lämplig kategori i **[!UICONTROL Related]** avsnittet. Om den resurs du har relaterat är källfilen för den aktuella resursen visas den under **[!UICONTROL Source]**.

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. Om du vill ta bort kopplingen för en resurs klickar du på **[!UICONTROL Unrelate]** i verktygsfältet.

   ![ej hänförliga tillgångar](assets/do-not-localize/link-unrelate-icon.png)

1. Markera de resurser som du vill ta bort kopplingen för i **[!UICONTROL Remove Relations]** dialogrutan och klicka på **[!UICONTROL Unrelate]**.

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. Klicka **[!UICONTROL OK]** för att stänga dialogrutan. Resurserna som du har tagit bort relationer för tas bort från listan över relaterade resurser under **[!UICONTROL Related]** avsnittet.

## Översätter relaterade resurser {#translating-related-assets}

Det är också praktiskt att skapa käll-/härledda relationer mellan resurser med hjälp av funktionen Relaterade resurser i översättningsarbetsflöden. När du kör ett översättningsarbetsflöde på en härledd resurs hämtar automatiskt alla resurser som källfilen refererar till och inkluderar dem för översättning. [!DNL Experience Manager Assets] På så sätt översätts den resurs som källresursen refererar till tillsammans med källresursen och de härledda resurserna. Tänk dig till exempel ett scenario där den engelska språkkopian innehåller en härledd resurs och dess källfil som visas.

![chlimage_1-281](assets/chlimage_1-281.png)

Om källfilen är relaterad till en annan resurs hämtar [!DNL Experience Manager Assets] den refererade resursen och inkluderar den för översättning.

![sidan med resursegenskaper visar den relaterade resursens källfil som ska inkluderas för översättning](assets/asset-properties-source-asset.png)

*Bild: Källtillgång för relaterade tillgångar som ska inkluderas för översättning.*

1. Översätt resurserna i källmappen till ett målspråk genom att följa stegen i [Skapa ett nytt översättningsprojekt](translation-projects.md#create-a-new-translation-project). I det här fallet kan du till exempel översätta dina resurser till franska.

1. Öppna översättningsmappen från [!UICONTROL Projects] sidan.

   ![chlimage_1-283](assets/chlimage_1-283.png)

1. Klicka på projektpanelen för att öppna informationssidan.

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. Klicka på ellipserna under översättningsjobbkortet för att visa översättningsstatusen.

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. Markera resursen och klicka sedan på **[!UICONTROL Reveal in Assets]** i verktygsfältet för att visa översättningsstatusen för resursen.

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. Om du vill kontrollera om de resurser som är relaterade till källan har översatts klickar du på källresursen.

   ![chlimage_1-287](assets/chlimage_1-287.png)

1. Markera resursen som är relaterad till källan och klicka sedan på **[!UICONTROL Reveal in Assets]**. Den översatta relaterade resursen visas.

   ![chlimage_1-288](assets/chlimage_1-288.png)
