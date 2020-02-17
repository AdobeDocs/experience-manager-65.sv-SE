---
title: Använda arbetsflöden på resurser
description: Lär dig hur du använder arbetsflöden på resurser, mappar och samlingar i AEM Resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Använda arbetsflöden för att bearbeta resurser {#applying-workflows-to-assets}

Att använda arbetsflöden på digitala resurser är detsamma som för webbsidor. En fullständig guide om hur du skapar och använder arbetsflöden i AEM finns i [Starta arbetsflöden](/help/sites-authoring/workflows-participating.md).

Använd arbetsflöden i digitala resurser för att aktivera resursen eller skapa vattenstämplar. Många av arbetsflödena för resurser aktiveras automatiskt. Arbetsflödet som automatiskt skapar en återgivning efter att en bild har redigerats aktiveras till exempel automatiskt.

Om ett arbetsflöde som är tillgängligt i det klassiska användargränssnittet inte är tillgängligt i det beröringsaktiverade användargränssnittet, som begäran om aktivering och begäran om inaktivering, ska du läsa [skapa arbetsflödesmodeller](/help/sites-developing/workflows-models.md#classic2touchui).

## Tillämpa ett arbetsflöde på en AEM-resurs {#applying-a-workflow-to-an-aem-asset}

Mer information om hur du tillämpar ett arbetsflöde på en AEM-resurs finns i [Starta ett arbetsflöde för en resurs](/help/assets/managing-assets-touch-ui.md#starting-a-workflow-on-an-asset).

## Tillämpa ett arbetsflöde på flera resurser {#applying-a-workflow-to-multiple-assets}

1. I resurskonsolen navigerar du till platsen för de resurser som du vill starta ett arbetsflöde för och väljer resurser.
1. Klicka på/tryck på Experience Manager-logotypen och välj **[!UICONTROL Tidslinje]** på menyn för att visa tidslinjen.

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. Klicka/tryck på **[!UICONTROL Åtgärder]** längst ned.

   ![chlimage_1-30](assets/chlimage_1-137.png)

1. Tryck på **[!UICONTROL Starta arbetsflöde]**.
1. Välj en arbetsflödesmodell i listan i dialogrutan **[!UICONTROL Starta arbetsflöde]** .

   ![chlimage_1-31](assets/chlimage_1-138.png)

1. (Valfritt) Ange en rubrik för arbetsflödet som kan användas som referens för arbetsflödesinstansen.
1. Tryck på **[!UICONTROL Start]** och sedan på **[!UICONTROL Bekräfta]** i dialogrutan. Arbetsflödet körs på alla resurser som du har valt.

## Tillämpa ett arbetsflöde på flera mappar {#applying-a-workflow-to-multiple-folders}

Hur du tillämpar ett arbetsflöde på flera mappar liknar hur du tillämpar ett arbetsflöde på flera resurser. Markera mapparna i resurskonsolen och utför steg 2-7 i proceduren för att [tillämpa ett arbetsflöde på flera resurser](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets).

## Tillämpa ett arbetsflöde på en samling {#applying-a-workflow-to-a-collection}

Se [Använda ett arbetsflöde i en samling](/help/assets/managing-collections-touch-ui.md#running-a-workflow-on-a-collection).
