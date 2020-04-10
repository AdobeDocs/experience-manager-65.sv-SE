---
title: Bearbeta material för att genomföra affärsprocesser, utföra revisioner, uppfylla regelkrav och upprätthålla en grundläggande smidighet
description: Resursbearbetning för att konvertera format, skapa renderingar, hantera resurser, validera resurser och köra arbetsflöden.
contentOwner: AG
translation-type: tm+mt
source-git-commit: bf291206a8c0e435053fbdba493ad949619ee5b3

---


# Bearbeta digitala resurser {#process-assets}

[!DNL Adobe Experience Manager Assets] gör att du kan arbeta med dina digitala resurser på många olika sätt för att möjliggöra robust materialbearbetning. Du kan använda de tillgängliga processmetoderna eller utöka metoderna för att säkerställa att hela processen slutförs med hjälp av, granskning och regelefterlevnad av, identifiering och distribution av samt grundläggande trygghet i era digitala resurser. Du kan göra allt detta samtidigt som du får önskad skala och anpassning.

## Förstå arbetsflöden {#understand-workflows}

För bearbetning av resurser [!DNL Experience Manager] används arbetsflöden. Arbetsflöden hjälper till att automatisera affärslogiken eller -aktiviteterna. Detaljerade steg för att utföra specifika uppgifter anges som standard och utvecklare kan skapa egna anpassade steg. Dessa steg kan kombineras i en logisk ordning för att skapa arbetsflöden. Ett arbetsflöde kan t.ex. automatiskt lägga till vattenstämpel i överförda bilder baserat på ett visst villkor, t.ex. metadata inbäddade i en bild, mapp som den överförs till, upplösning för bilden osv. Ett annat exempel är ett arbetsflöde som är konfigurerat för vattenstämpelbilder på ett sådant sätt och som samtidigt hanterar flera resurshanteringsbehov, som att lägga till metadata, skapa återgivningar, lägga till smarta taggar för tillgångsidentifiering, publicera i ett datalager, ange behörigheter för användaråtkomst och så vidare.

## Standardarbetsflöden som är tillgängliga i Experience Manager {#default-workflows}

Som standard bearbetas alla överförda resurser med hjälp av arbetsflödet [!UICONTROL DAM-uppdatering] . Arbetsflödet körs för varje överförd resurs och utför grundläggande resurshanteringsåtgärder som återgivningsgenerering, tillbakaskrivning av metadata, sidextrahering, medieextrahering och omkodning.

Information om de olika arbetsflödesmodellerna som är tillgängliga som standard finns i [!UICONTROL Verktyg > Arbetsflöde > Modeller] i [!DNL Experience Manager].

![En del av standardarbetsflödet](assets/aem-default-workflows.png)

*Bild: Vissa standardarbetsflöden finns i[!DNL Experience Manager]*

## Använda arbetsflöden för att bearbeta resurser {#applying-workflows-to-assets}

Att använda arbetsflöden på digitala resurser är detsamma som för webbsidor. En fullständig guide om hur du skapar och använder arbetsflöden finns i [Starta arbetsflöden](/help/sites-authoring/workflows-participating.md).

Använd arbetsflöden i digitala resurser för att aktivera resursen eller skapa vattenstämplar. Många av arbetsflödena för resurser aktiveras automatiskt. Arbetsflödet som automatiskt skapar en återgivning efter att en bild har redigerats aktiveras till exempel automatiskt.

>[!NOTE]
>
>Om ett arbetsflöde som är tillgängligt i det klassiska användargränssnittet inte är tillgängligt i det Touch-aktiverade användargränssnittet, som [!UICONTROL Begäran att aktivera] och [!UICONTROL Begär att inaktivera], ska du läsa [skapa arbetsflödesmodeller](/help/sites-developing/workflows-models.md#classic2touchui).

## Tillämpa ett arbetsflöde på en resurs {#apply-a-workflow-to-an-asset}

Så här använder du ett arbetsflöde för en resurs:

1. Navigera till platsen för resursen som du vill starta ett arbetsflöde för och klicka på resursen för att öppna resurssidan. Välj **[!UICONTROL Tidslinje]** på menyn för att visa tidslinjen.

   ![tidslinje-1](assets/timeline.png)

1. Klicka på **[!UICONTROL Åtgärder]** längst ned för att öppna en lista med tillgängliga åtgärder för resursen.

   ![chlimage_1-252](assets/chlimage_1-45.png)

1. Klicka på **[!UICONTROL Starta arbetsflöde]** i listan.

   ![chlimage_1-253](assets/chlimage_1-49.png)

1. In the **[!UICONTROL Start Workflow]** dialog, select a workflow model from the list.

   ![chlimage_1-254](assets/chlimage_1-50.png)

1. (Valfritt) Ange en rubrik för arbetsflödet som kan användas för att referera till arbetsflödets instans.

   ![chlimage_1-255](assets/chlimage_1-51.png)

1. Klicka på **[!UICONTROL Start]** och sedan på **[!UICONTROL Fortsätt]**. Varje steg i arbetsflödet visas på tidslinjen som en händelse.

   ![chlimage_1-256](assets/chlimage_1-52.png)

## Tillämpa ett arbetsflöde på flera resurser {#applying-a-workflow-to-multiple-assets}

1. I resurskonsolen navigerar du till platsen för de resurser som du vill starta ett arbetsflöde för och väljer resurser. Välj **[!UICONTROL Tidslinje]** på menyn för att visa tidslinjen.

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. Klicka på **[!UICONTROL Åtgärder]** längst ned.

   ![chlimage_1-30](assets/chlimage_1-137.png)

1. Klicka på **[!UICONTROL Starta arbetsflöde]**. In the **[!UICONTROL Start Workflow]** dialog, select a workflow model from the list.

   ![chlimage_1-31](assets/chlimage_1-138.png)

1. (Valfritt) Ange en rubrik för arbetsflödet som kan användas som referens för arbetsflödesinstansen.
1. Click **[!UICONTROL Start]** and then click **[!UICONTROL Confirm]** in the dialog. Arbetsflödet körs på alla resurser som du har valt.

## Tillämpa ett arbetsflöde på flera mappar {#applying-a-workflow-to-multiple-folders}

Hur du tillämpar ett arbetsflöde på flera mappar liknar hur du tillämpar ett arbetsflöde på flera resurser. Markera mapparna i resurskonsolen och utför steg 2-7 i proceduren för att [tillämpa ett arbetsflöde på flera resurser](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets).

## Tillämpa ett arbetsflöde på en samling {#applying-a-workflow-to-a-collection}

Se [Använda ett arbetsflöde i en samling](/help/assets/managing-collections-touch-ui.md#running-a-workflow-on-a-collection).

## Starta ett arbetsflöde automatiskt för att bearbeta resurser {#auto-execute-workflow-on-some-assets}

Administratörer kan konfigurera arbetsflödet så att resurser automatiskt körs och bearbetas baserat på fördefinierade villkor. Funktionen är användbar för företagsanvändare och marknadsförare, till exempel för att skapa anpassade arbetsflöden för specifika mappar. Anta att alla resurser från en reklambyrås foton kan vara vattenstämplade eller att alla resurser som överförts av en frilansare kan bearbetas för att skapa specifika renderingar.

För en arbetsflödesmodell kan användare skapa en startfunktion för arbetsflödet som startar den. Administratörer kan ge marknadsförarna åtkomst för att skapa arbetsflödena och konfigurera startprogrammet. Användarna kan ändra standardarbetsflödet för [!UICONTROL DAM-uppdatering av resurser] och lägga till de extra steg som krävs för att bearbeta specifika resurser. Arbetsflödet körs på alla nyligen överförda resurser, så använd en av följande metoder för att begränsa körningen av de extra stegen för specifika resurser:

* Gör en kopia av arbetsflödet för [!UICONTROL DAM-uppdatering av resurser] och ändra det så att det körs i en viss mapphierarki. Den här metoden är användbar för ett fåtal mappar.
* De extra bearbetningsstegen kan läggas till med hjälp av en [OR-delning](/help/sites-developing/workflows-step-ref.md#or-split) enligt villkor som gäller för så många mappar som behövs.

>[!MORELIKETHIS]
>
>* [Använda och delta i arbetsflöden](/help/sites-authoring/workflows.md)
>* [Skapa arbetsflödesmodeller och utöka arbetsflödesfunktioner](/help/sites-developing/workflows.md)
>* [Bästa arbetsflöden](/help/sites-developing/workflows-best-practices.md)
>* [Community-artikel om att ändra resurs med hjälp av arbetsflöde](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)

