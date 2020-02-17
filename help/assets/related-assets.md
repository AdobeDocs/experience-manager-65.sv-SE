---
title: Relaterade tillgångar
description: Lär dig hur du relaterar resurser som delar vissa gemensamma attribut. Du kan också använda funktionen för att skapa käll-/härledda relationer mellan resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Relaterade tillgångar {#related-assets}

Med Adobe Experience Manager Assets (AEM) kan ni manuellt relatera resurser baserat på organisationens behov med hjälp av funktionen för relaterade resurser. Du kan till exempel relatera en licensfil till en resurs eller en bild/video på ett liknande ämne. Du kan relatera resurser som delar vissa gemensamma attribut. Du kan också använda funktionen för att skapa käll-/härledda relationer mellan resurser. Om du till exempel har en PDF-fil som genereras från en INDD-fil kan du koppla PDF-filen till dess INDD-källfil.

Med den här funktionen kan du dela en lågupplöst PDF- eller JPG-fil med leverantörer eller myndigheter och göra den högupplösta INDD-filen tillgänglig endast på begäran.

## Relatera resurser {#relating-assets}

1. I AEM-gränssnittet öppnar du sidan [!UICONTROL Egenskaper] för en resurs som du vill relatera.

   ![chlimage_1-272](assets/chlimage_1-272.png)

   Du kan också välja resursen i listvyn.

   ![chlimage_1-273](assets/chlimage_1-273.png)

   Du kan också välja resursen från en samling.

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. Om du vill koppla en annan resurs till den valda resursen klickar/trycker du på ikonen **[!UICONTROL Relatera]** i verktygsfältet.

   ![chlimage_1-275](assets/chlimage_1-275.png)

1. Gör något av följande:

   * Om du vill relatera källfilen för resursen väljer du **[!UICONTROL Källa]** i listan.
   * Om du vill relatera en härledd fil väljer du **[!UICONTROL Härledd]** i listan.
   * Om du vill skapa en dubbelriktad relation mellan resurserna väljer du **[!UICONTROL Övriga]** i listan.
   ![chlimage_1-276](assets/chlimage_1-276.png)

1. På skärmen **[!UICONTROL Välj resurs]** navigerar du till platsen för den resurs du vill relatera till och markerar den.

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. Klicka på/tryck på ikonen **[!UICONTROL Bekräfta]** .
1. Klicka/tryck på **[!UICONTROL OK]** för att stänga dialogrutan. Beroende på ditt val av relation i steg 3 listas den relaterade resursen under en lämplig kategori i **[!UICONTROL relaterat]** avsnitt. Om den resurs du har relaterat är källfilen för den aktuella resursen visas den under **[!UICONTROL Källa]**.

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. Om du vill ta bort kopplingen för en resurs klickar/trycker du på **[!UICONTROL Ta bort relation]** i verktygsfältet.

   ![chlimage_1-279](assets/chlimage_1-279.png)

1. Välj de mediefiler som du vill ta bort kopplingen för i dialogrutan **[!UICONTROL Ta bort relationer]** och klicka/tryck på **[!UICONTROL Ta bort relation]**.

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. Klicka/tryck på **[!UICONTROL OK]** för att stänga dialogrutan. Resurserna som du har tagit bort relationer för tas bort från listan över relaterade resurser under avsnittet **[!UICONTROL Relaterade]** .

## Översätter relaterade resurser {#translating-related-assets}

Det är också praktiskt att skapa käll-/härledda relationer mellan resurser med hjälp av funktionen Relaterade resurser i översättningsarbetsflöden. När du kör ett översättningsarbetsflöde på en härledd resurs hämtar AEM Resurser automatiskt alla resurser som källfilen refererar till och inkluderar dem för översättning. På så sätt översätts den resurs som källresursen refererar till tillsammans med källresursen och de härledda resurserna. Tänk dig till exempel ett scenario där den engelska språkkopian innehåller en härledd resurs och dess källfil som visas.

![chlimage_1-281](assets/chlimage_1-281.png)

Om källfilen är relaterad till en annan resurs hämtar AEM Resurser den refererade resursen och inkluderar den för översättning.

![chlimage_1-282](assets/chlimage_1-282.png)

1. Översätt resurserna i källmappen till ett målspråk genom att följa stegen i [Skapa ett nytt översättningsprojekt](translation-projects.md#create-a-new-translation-project). I det här fallet kan du till exempel översätta dina resurser till franska.
1. Öppna översättningsmappen på sidan [!UICONTROL Projekt] .

   ![chlimage_1-283](assets/chlimage_1-283.png)

1. Klicka/tryck på projektpanelen för att öppna informationssidan.

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. Klicka på/tryck på ellipserna under översättningsjobbkortet för att visa översättningsstatusen.

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. Markera resursen och klicka/tryck sedan på **[!UICONTROL Visa i resurser]** i verktygsfältet för att visa översättningsstatusen för resursen.

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. Om du vill kontrollera om de resurser som är relaterade till källan har översatts klickar/trycker du på källresursen.

   ![chlimage_1-287](assets/chlimage_1-287.png)

1. Välj den resurs som är relaterad till källan och klicka/tryck sedan på **[!UICONTROL Visa i Resurser]**. Den översatta relaterade resursen visas.

   ![chlimage_1-288](assets/chlimage_1-288.png)
