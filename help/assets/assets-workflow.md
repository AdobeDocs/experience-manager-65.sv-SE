---
title: Bearbeta resurser med arbetsflöden
description: Resursbearbetning för att konvertera format, skapa renderingar, hantera resurser, validera resurser och köra arbetsflöden.
contentOwner: AG
feature: Workflow, Renditions
role: User, Admin
exl-id: e7c84385-efb3-4997-83ff-7a7f31582469
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 2%

---

# Bearbeta digitala resurser {#process-assets}

[!DNL Adobe Experience Manager Assets] gör att du kan arbeta med dina digitala resurser på många olika sätt för att få en robust materialbearbetning. Du kan använda standardmetoderna eller anpassade bearbetningsmetoder för att säkerställa att hela processen slutförs, att alla granskningar och att de efterlevs, att identifieringen och distributionen samt att de digitala resurserna är rena. Du kan utföra resurshanteringsuppgifterna samtidigt som du uppnår önskad skala och anpassning.

## Förstå arbetsflöden {#understand-workflows}

För bearbetning av tillgångar [!DNL Experience Manager] använder arbetsflöden. Arbetsflöden hjälper till att automatisera affärslogiken eller -aktiviteterna. Detaljerade steg för att utföra specifika uppgifter anges som standard och utvecklare kan skapa egna anpassade steg. Dessa steg kan kombineras i en logisk ordning för att skapa arbetsflöden. Ett arbetsflöde kan till exempel lägga till en vattenstämpel på överförda bilder baserat på ett visst villkor, till exempel den mapp som det överförs till, upplösning för bilden och så vidare. Ett annat exempel är ett arbetsflöde som är konfigurerat för vattenstämplar och som lägger till metadata, skapar renderingar, lägger till smarta taggar och publicerar i ett datalager.

## Standardarbetsflöden som är tillgängliga i [!DNL Experience Manager] {#default-workflows}

Som standard bearbetas alla överförda resurser med [!UICONTROL DAM Update Asset] arbetsflöde. Arbetsflödet körs för varje överförd resurs och utför grundläggande resurshanteringsåtgärder som återgivningsgenerering, tillbakaskrivning av metadata, sidextrahering, medieextrahering och omkodning.

Information om de olika arbetsflödesmodellerna som är tillgängliga som standard finns i **[!UICONTROL Tools > Workflow > Models]** in [!DNL Experience Manager].

![En del av standardarbetsflödet](assets/aem-default-workflows.png)

*Bild: Vissa av standardarbetsflödena i [!DNL Experience Manager].*

## Använda arbetsflöden för att bearbeta resurser {#applying-workflows-to-assets}

Att använda arbetsflöden på digitala resurser är detsamma som för webbsidor. En fullständig guide om hur du skapar och använder arbetsflöden finns på [starta arbetsflöden](/help/sites-authoring/workflows-participating.md).

Använd arbetsflöden i digitala resurser för att aktivera resursen eller skapa vattenstämplar. Många av arbetsflödena för resurser aktiveras automatiskt. Arbetsflödet som automatiskt skapar en återgivning efter att en bild har redigerats aktiveras automatiskt.

>[!NOTE]
>
>Om ett arbetsflöde som är tillgängligt i det klassiska användargränssnittet inte är tillgängligt i det användargränssnitt som är aktiverat för pekskärm, till exempel [!UICONTROL Request to Activate] och [!UICONTROL Request to Deactivate], se [skapa arbetsflödesmodeller](/help/sites-developing/workflows-models.md#classic2touchui).

## Tillämpa ett arbetsflöde på en resurs {#apply-a-workflow-to-an-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->
Så här använder du ett arbetsflöde för en resurs:

1. Navigera till platsen för resursen som du vill starta ett arbetsflöde för och klicka på resursen för att öppna resurssidan. Välj **[!UICONTROL Timeline]** på menyn för att visa tidslinjen.

   ![tidslinje-1](assets/timeline.png)

1. Klicka **[!UICONTROL Actions]** längst ned för att öppna en lista med tillgängliga åtgärder för resursen.

1. Klicka **[!UICONTROL Start Workflow]** från listan.

1. I **[!UICONTROL Start Workflow]** väljer du en arbetsflödesmodell i listan.

1. (Valfritt) Ange en rubrik för arbetsflödet som kan användas för att referera till arbetsflödets instans.

   ![välj arbetsflöde, ange en titel och klicka på början](assets/start-workflow.png)

1. Klicka **[!UICONTROL Start]** och sedan klicka **[!UICONTROL Proceed]**. Varje steg i arbetsflödet visas på tidslinjen som en händelse.

   ![chlimage_1-256](assets/chlimage_1-52.png)

## Tillämpa ett arbetsflöde på flera resurser {#applying-a-workflow-to-multiple-assets}

1. Från [!DNL Assets] navigera till platsen för de resurser som du vill starta ett arbetsflöde för och markera resurserna. Välj **[!UICONTROL Timeline]** på menyn för att visa tidslinjen.

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. Klicka **[!UICONTROL Actions]** ![uppåt](assets/do-not-localize/chevron-up-icon.png) längst ned.
1. Klicka på **[!UICONTROL Start Workflow]**. I **[!UICONTROL Start Workflow]** väljer du en arbetsflödesmodell i listan.

   ![starta arbetsflöde](assets/start-workflow.png)

1. (Valfritt) Ange en rubrik för arbetsflödet som kan användas som referens för arbetsflödesinstansen.
1. Klicka på **[!UICONTROL Start]** och sedan på **[!UICONTROL Confirm]** i dialogrutan. Arbetsflödet körs på alla resurser som du har valt.

## Tillämpa ett arbetsflöde på flera mappar {#applying-a-workflow-to-multiple-folders}

Hur du tillämpar ett arbetsflöde på flera mappar liknar hur du tillämpar ett arbetsflöde på flera resurser. Markera mapparna i [!DNL Assets] -gränssnittet och utför steg 2-7 i proceduren [använda ett arbetsflöde på flera resurser](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets).

## Tillämpa ett arbetsflöde på en samling {#applying-a-workflow-to-a-collection}

Se [använda ett arbetsflöde i en samling](/help/assets/manage-collections.md#running-a-workflow-on-a-collection).

## Starta ett arbetsflöde automatiskt för att bearbeta resurser {#auto-execute-workflow-on-some-assets}

Administratörer kan konfigurera arbetsflödet så att resurser automatiskt körs och bearbetas baserat på fördefinierade villkor. Funktionen är användbar för användare och marknadsförare inom olika branscher, till exempel för att skapa anpassade arbetsflöden för specifika mappar. Anta att alla resurser från en reklambyrås foton kan vara vattenstämplade eller att alla resurser som överförts av en frilansare kan bearbetas för att skapa specifika renderingar.

För en arbetsflödesmodell kan användare skapa en startfil för arbetsflödet som kör den. En arbetsflödesstartsfunktion övervakar ändringar i innehållsdatabasen och kör arbetsflödet när de fördefinierade villkoren är uppfyllda. Administratörer kan ge marknadsförarna åtkomst för att skapa arbetsflödena och konfigurera startprogrammet. Användare kan ändra standardinställningen [!UICONTROL DAM Update Asset] arbetsflöde för att lägga till de extra steg som krävs för att bearbeta specifika resurser. Arbetsflödet körs på alla nyligen överförda resurser. Använd någon av följande metoder för att begränsa utförandet av de extra stegen för specifika resurser:

* Skapa en kopia av [!UICONTROL DAM Update Asset] arbetsflöde och ändra det så att det körs i en viss mapphierarki. Den här metoden är användbar för ett fåtal mappar.
* De extra bearbetningsstegen kan läggas till med en [ELLER dela](/help/sites-developing/workflows-step-ref.md#or-split) enligt villkor som gäller för så många mappar som behövs.

## Bästa praxis och begränsningar {#best-practices-limitations-tips}

* Tänk på dina behov av alla typer av återgivningar när du utformar arbetsflöden. Om du inte förutser att en återgivning behövs i framtiden tar du bort steget när du skapar den från arbetsflödet. Återgivningar kan inte tas bort gruppvis efteråt. Oönskade återgivningar kan ta upp lagringsutrymmet efter långvarig användning av [!DNL Experience Manager]. För enskilda resurser kan du ta bort återgivningar manuellt från användargränssnittet. För flera resurser kan du antingen anpassa [!DNL Experience Manager] om du vill ta bort specifika återgivningar eller ta bort resurserna och överföra dem igen.
* Som standard [!UICONTROL DAM Update Asset] arbetsflödet innehåller några steg för att skapa miniatyrbilder och webbåtergivningar. Om någon standardåtergivning tas bort från arbetsflödet används användargränssnittet i [!DNL Assets] återger inte korrekt.

>[!MORELIKETHIS]
>
>* [Använda och delta i arbetsflöden](/help/sites-authoring/workflows.md)
>* [Skapa arbetsflödesmodeller och utöka arbetsflödesfunktioner](/help/sites-developing/workflows.md)
>* [Metoder som kör arbetsflöden](/help/sites-administering/workflows-starting.md)
>* [Bästa praxis för arbetsflöden](/help/sites-developing/workflows-best-practices.md)
