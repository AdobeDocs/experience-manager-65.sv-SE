---
title: Blandade medieuppsättningar
description: Lär dig hur du arbetar med blandade medieuppsättningar i Dynamic Media
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
feature: Mixed Media Sets,Asset Management
role: User, Admin
exl-id: 70a72fb9-a289-4eda-abcc-300edf9f1961
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1426'
ht-degree: 14%

---

# Blandade medieuppsättningar{#mixed-media-sets}

Med blandade medieuppsättningar kan du kombinera bilder, bilduppsättningar, snurruppsättningar och videoklipp i en presentation.

Blandade medieuppsättningar definieras av en banderoll med ordet **[!UICONTROL MixedMediaSet]**. Om uppsättningen med blandade medier publiceras visas dessutom det publiceringsdatum som anges av ikonen **[!UICONTROL World]** på banderollen tillsammans med det senaste ändringsdatumet, som anges av ikonen **[!UICONTROL Pencil]**.

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>Mer information om gränssnittet Resurser finns i [Hantera resurser](/help/assets/manage-assets.md).

## Snabbstart: Blandade medieuppsättningar {#quick-start-mixed-media-sets}

Följ de här stegen för att komma igång snabbt med blandade medieuppsättningar:

1. [Överför dina resurser](#uploading-assets).

   Börja med att ladda upp bilder och videoklipp för uppsättningarna med blandade medier. Om det behövs kan du skapa [bilduppsättningar](/help/assets/image-sets.md) och [rotationsuppsättningar](/help/assets/spin-sets.md). Eftersom användarna kan zooma in på bilder i visningsprogrammet för den blandade medieuppsättningen bör du vara noggrann när du väljer bilder. Se till att bilderna har minst 2 000 pixlar i den största dimensionen.

   Se [Dynamic Media - Rasterbildformat som stöds](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) för en lista över format som stöds av blandade medieuppsättningar.

1. [Skapa blandade medieuppsättningar](#creating-mixed-media-sets).

   Om du vill skapa en blandad medieuppsättning väljer du **[!UICONTROL Create]** > **[!UICONTROL Mixed Media Set]** och namnge uppsättningen, välj resurser och välj i vilken ordning bilderna ska visas.

   Se [Arbeta med väljare](/help/assets/working-with-selectors.md).

1. Konfigurera [Förinställningar för blandad Media Viewer](/help/assets/managing-viewer-presets.md), efter behov.

   Administratörer kan skapa eller ändra visningsförinställningar för blandade medieuppsättningar. Om du vill visa de blandade medierna med en visningsförinställning väljer du uppsättningen med blandade medier och väljer sedan **[!UICONTROL Viewers]** i listrutan till vänster.

   Information om hur du skapar eller redigerar förinställningar för visningsprogram finns i **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Viewer Presets]**.

   Se [Lägga till och redigera visningsprogramförinställningar](/help/assets/managing-viewer-presets.md).

1. [Förhandsgranska blandade medieuppsättningar](#previewing-mixed-media-sets).

   Markera den blandade medieuppsättningen och du kan förhandsgranska den. Markera miniatyrbildikonerna så att du kan undersöka den blandade medieuppsättningen i det valda visningsprogrammet. Du kan välja olika visningsprogram från **[!UICONTROL Viewers]** som finns på den vänstra menyn.

1. [Publicera blandade medieuppsättningar](#publishing-mixed-media-sets).

   När du publicerar en blandad medieuppsättning aktiveras URL-adressen och strängen Embed. Dessutom måste du [publicera visningsförinställningen](/help/assets/managing-viewer-presets.md#publishing-viewer-presets).

1. [Länka URL:er till ditt webbprogram](/help/assets/linking-urls-to-yourwebapplication.md) eller [Bädda in video- eller bildvisningsprogrammet](/help/assets/embed-code.md).

   Adobe Experience Manager Assets skapar URL-anrop för blandade medieuppsättningar och aktiverar dem när du har publicerat de blandade medieuppsättningarna. Du kan kopiera dessa URL:er när du förhandsgranskar resurser. Du kan även bädda in dem på din webbplats.

   Välj den blandade medieuppsättningen och välj sedan i listrutan till vänster **[!UICONTROL Viewers]**.

   Se [Länka en blandad medieuppsättning till en webbsida](/help/assets/linking-urls-to-yourwebapplication.md) och [Bädda in video- eller bildvisningsprogrammet](/help/assets/embed-code.md).

Du kan redigera vid behov [Blandade medieuppsättningar](#editing-mixed-media-sets). Dessutom kan du visa och ändra [Egenskaper för uppsättning med blandade media](/help/assets/manage-assets.md#editing-properties).

>[!NOTE]
>
>Om du har problem med att skapa uppsättningar finns mer information i [Felsöka Dynamic Media - Scene7-läge](/help/assets/troubleshoot-dms7.md).

## Överför resurser {#uploading-assets}

Börja med att ladda upp bilder och videoklipp för uppsättningarna med blandade medier. Eftersom användarna kan zooma in på bilder i visningsprogrammet för den blandade medieuppsättningen bör du vara noggrann när du väljer bilder. Se till att bilderna har minst 2 000 pixlar i den största dimensionen.

Om du dessutom vill lägga till snurrsuppsättningar eller bilduppsättningar i den blandade medieuppsättningen skapar du också dessa uppsättningar.

Se [Dynamic Media - Rasterbildformat som stöds](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) för en lista över format som stöds av blandade medieuppsättningar.

## Skapa en blandad medieuppsättning {#creating-mixed-media-sets}

Du kan lägga till bilder, bilduppsättningar, snurruppsättningar och videoklipp i din uppsättning med blandade media. Se till att dina filer, bilduppsättningar och snurruppsättningar är klara att publiceras innan du lägger till dem i den blandade medieuppsättningen.

När du lägger till resurser i uppsättningen läggs de automatiskt till i alfanumerisk ordning. Du kan ändra ordning på eller sortera resurser manuellt när de har lagts till.

**Så här skapar du en blandad medieuppsättning:**

1. Navigera till den plats där du vill skapa en blandad medieuppsättning i Resurser och välj **[!UICONTROL Create]** och markera **[!UICONTROL Mixed Media Set]**. Du kan också skapa uppsättningen inifrån en mapp som innehåller resurserna. Redigeraren för uppsättningar med blandade medier visas.

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. I redigeraren för den blandade medieuppsättningen **[!UICONTROL Title]** anger du ett namn för den blandade medieuppsättningen. Namnet visas i banderollen över den blandade medieuppsättningen. Du kan också ange en beskrivning.

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >När du skapar den blandade medieuppsättningen kan du ändra miniatyrbilden för den blandade medieuppsättningen eller låta Experience Manager välja miniatyrbilden automatiskt baserat på resurserna i den blandade medieuppsättningen. Om du vill välja en miniatyrbild väljer du **[!UICONTROL Change thumbnail]** och markera en bild (du kan navigera till andra mappar för att hitta bilder också). Om du har valt en miniatyrbild och sedan bestämmer dig för att Experience Manager ska generera en från den blandade medieuppsättningen, markerar du **[!UICONTROL Switch to Automatic thumbnail]**.

1. Markera resursväljaren så att du kan välja resurser som du vill inkludera i den blandade medieuppsättningen. Markera dem och välj sedan **[!UICONTROL Select]**.

   Med resursväljaren kan du söka efter resurser genom att skriva ett nyckelord och trycka på **[!UICONTROL Return]**. Du kan också använda filter för att förfina sökresultatet. Du kan filtrera efter sökväg, samling, filtyp och tagg. Markera filtret och välj sedan **[!UICONTROL Filter]** -ikonen i verktygsfältet. Ändra vyn genom att markera ikonen **[!UICONTROL View]** och markera **[!UICONTROL List View]**, **[!UICONTROL Column View]** eller **[!UICONTROL Card View]**.

   Se [Arbeta med väljare](/help/assets/working-with-selectors.md).

   ![chlimage_1-140](assets/chlimage_1-383.png)

1. Ändra ordning på resurserna genom att dra dem uppåt eller nedåt i listan (måste välja **[!UICONTROL Reorder]** -ikon), om det behövs.

   ![chlimage_1-141](assets/chlimage_1-352.png)

   Om du vill lägga till miniatyrbilder väljer du **+** **[!UICONTROL thumbnail]** -ikonen bredvid bilden och navigera till miniatyrbilden som du vill använda. När du är klar markerar du alla miniatyrbilder **[!UICONTROL Save]**.

   >[!NOTE]
   >
   >Om du vill lägga till resurser väljer du **[!UICONTROL Add Asset]**.

1. Om du vill ta bort en resurs markerar du motsvarande kryssruta och väljer **[!UICONTROL Delete Asset]**.
1. Om du vill använda en förinställning väljer du **[!UICONTROL Preset]** i det övre högra hörnet och välj en förinställning som ska användas för resurserna.
1. Välj **[!UICONTROL Save]**. Den nya blandade medieuppsättningen visas i den mapp som du skapade den i.

## Redigera en blandad medieuppsättning {#editing-mixed-media-sets}

Du kan utföra olika redigeringsåtgärder för resurser i blandade medieuppsättningar direkt i användargränssnittet [på samma sätt som andra resurser i Assets](/help/assets/manage-assets.md). Du kan även utföra följande åtgärder i Blandade medieuppsättningar:

* Lägg till resurser i den blandade medieuppsättningen.
* Ändra ordning på resurser i den blandade medieuppsättningen.
* Ta bort resurser i den blandade medieuppsättningen.
* Använd förinställningar för visningsprogram.
* Ändra standardminiatyrbilden.

**Så här redigerar du en blandad medieuppsättning:**

1. Gör något av följande:

   * Håll pekaren över en resurs i en blandad medieuppsättning och välj sedan **[!UICONTROL Edit]** (pennikon).
   * Hovra över en resurs i en blandad medieuppsättning, välj **[!UICONTROL Select]** (bockmarkeringsikon) och sedan välja **[!UICONTROL Edit]** i verktygsfältet.

   * Välj en resurs för en blandad medieuppsättning och välj sedan **[!UICONTROL Edit]** (pennikon) i verktygsfältet.

1. Gör något av följande i redigeraren för den blandade medieuppsättningen:

   * Om du vill ändra ordning på resurser väljer du **[!UICONTROL Assets]** (bildikon) drar du en resurs till en ny plats.
   * Om du vill lägga till resurser väljer du **[!UICONTROL Add Asset]**. Navigera till resurserna. För varje resurs som du vill lägga till håller du pekaren över resursens bild (inte resursens namn) och väljer sedan bockmarkeringsikonen. I det övre högra hörnet väljer du **[!UICONTROL Select]**.

   * Om du vill ta bort en resurs väljer du **[!UICONTROL Assets]** (bildikon) och välj sedan resursen. I verktygsfältet väljer du **[!UICONTROL Delete Asset]**.

   * Om du vill sortera resurser efter namn i stigande eller fallande ordning väljer du **[!UICONTROL Assets]** (bildikon). Till höger om **[!UICONTROL Assets]** välj ikonerna för cirkumflex uppåt eller nedåt.

     >[!NOTE]
     >
     >* Om du vill ta bort en hel uppsättning med blandade media från valfritt visningsläge (till exempel **[!UICONTROL Card View]** eller **[!UICONTROL Column View]**) navigera till den blandade medieuppsättningen. Håll markören över resursen och markera bockmarkeringsikonen så att du markerar den. Tryck **[!UICONTROL Backspace]** på tangentbordet eller välj **[!UICONTROL More]** (tre punkter) i verktygsfältet och välj sedan **[!UICONTROL Delete]**.
     >
     >* Du kan redigera resurser i en uppsättning med blandade media genom att navigera till uppsättningen och klicka på **[!UICONTROL Set Members]** till vänster. Välj **[!UICONTROL Pencil]** på en enskild resurs så att du kan öppna den i redigeringsfönstret.

1. Välj **[!UICONTROL Save]** när du är klar med redigeringen.

   >[!NOTE]
   >
   >* Om du vill redigera resurserna i en uppsättning med blandade media navigerar du till den blandade medieuppsättningen. Markera (markera inte) uppsättningen så att den öppnas på sidan Förhandsvisa Experience Manager. Markera nedåtpilen i den vänstra listen för att öppna listrutan och välj sedan **[!UICONTROL Set Members]**. Håll markören över en resurs på sidan Ange medlemmar och välj sedan **[!UICONTROL Edit]** (pennikon) för att öppna redigeringssidan.
   >
   >* Om du vill ta bort en hel uppsättning med blandade media - I valfritt visningsläge (som kortvyn eller kolumnvyn) går du till den blandade medieuppsättningen. Hovra på scenen och välj sedan **Välj** (bockmarkeringsikon). Tryck **[!UICONTROL Backspace]** på tangentbordet, eller välj **[!UICONTROL More]** (rad om tre punkter), markera sedan **[!UICONTROL Delete]**.

## Förhandsgranska en uppsättning med blandade media {#previewing-mixed-media-sets}

Se [Förhandsgranska resurser](/help/assets/previewing-assets.md) om du vill ha mer information om hur du förhandsvisar blandade medieuppsättningar.

## Publicera en blandad medieuppsättning {#publishing-mixed-media-sets}

Se [Publicera resurser](/help/assets/publishing-dynamicmedia-assets.md) om du vill ha mer information om hur du publicerar blandade medieuppsättningar.

>[!NOTE]
>
>Om den blandade medieuppsättningen inte hamnar helt i leveranstjänsten första gången du publicerar den publicerar du den blandade medieuppsättningen en andra gång.
