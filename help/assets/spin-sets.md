---
title: Snurrande uppsättningar
description: Lär dig hur du arbetar med snurruppsättningar i Dynamic Media
uuid: 379a20a3-6a17-499a-b0f1-3a835b97aa7b
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 8e9b3815-2893-4e6b-ac41-77720b42d56b
docset: aem65
feature: Spin Sets,Asset Management
role: User, Admin
exl-id: 758ad754-15de-4e72-9b7d-ab49c51d7d4f
source-git-commit: d83a647d8ac5466ba09230c584d5d501aab55274
workflow-type: tm+mt
source-wordcount: '1888'
ht-degree: 8%

---

# Snurrande uppsättningar{#spin-sets}

Med en snurra uppsättning kan du simulera hur det ser ut när du vrider ett objekt för att undersöka det. Med snurra uppsättningar kan du visa objekt från vilken vinkel som helst och få fram de viktigaste visuella detaljerna från vilken vinkel som helst.

En snurra uppsättning simulerar en 360-gradig visningsupplevelse. Dynamic Media erbjuder snurra uppsättningar med en axel där tittarna kan rotera ett objekt. Dessutom kan man zooma och panorera med några enkla musklick. På så sätt kan användare undersöka ett objekt närmare från en viss betraktningsvinkel.

Snurra uppsättningar anges av en banderoll med ordet **[!UICONTROL SPINSET]**. Om rotationsuppsättningen dessutom är publicerad är det publiceringsdatum som anges av **[!UICONTROL World]** ikonen finns på banderollen tillsammans med det senaste ändringsdatumet, vilket anges av **[!UICONTROL Pencil]** visas.

![chlimage_1-](assets/chlimage_1-380.png)

>[!NOTE]
>
>Mer information om gränssnittet Resurser finns i [Hantera resurser](/help/assets/manage-assets.md).

När du skapar en snurrsuppsättning rekommenderar Adobe följande bästa praxis och tillämpar följande gräns:

| Begränsningstyp | Bästa praxis | Begränsning har införts |
| --- | --- | --- |
| Maximalt antal rader/kolumner per 2D-uppsättning | 12-18 bilder per uppsättning | 1000 |

Se även [Dynamic Media begränsningar](/help/assets/limitations.md).

## Snabbstart: Snurra uppsättningar {#quick-start-spin-sets}

Så här kommer du igång snabbt med Spin Sets:

1. [Överför dina bilder för flera vyer](#uploading-assets-for-spin-sets).

   Du behöver minst 8-12 tagningar av ett objekt för en endimensionell snurra och 16-24 för en tvådimensionell snurra uppsättning. Fotografierna måste tas med jämna mellanrum för att ge intryck av att objektet roteras och vändas. Om en endimensionell snurra t.ex. innehåller 12 tagningar roterar du objektet 30° (360/12) för varje tagning.

   Se [Dynamic Media - Rasterbildformat som stöds](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) om du vill visa en lista över format som kan användas i snurruppsättningar.

1. [Skapa en snurruppsättning](#creating-spin-sets).

   Om du vill skapa en snurruppsättning väljer du **[!UICONTROL Create > Spin Set]** och namnge uppsättningen, välja resurser och välj i vilken ordning bilderna ska visas.

   Se [Arbeta med väljare](/help/assets/working-with-selectors.md).

   >[!NOTE]
   >
   >Du kan också skapa rotationsuppsättningar automatiskt med hjälp av [förinställningar för gruppuppsättningar](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets). **Viktigt:** Batchuppsättningar skapas av IPS (Image Production System) som en del av tillgångsintag och är endast tillgängliga i Dynamic Media-Scene7-läge.

1. Konfigurera [Snurra inställningar för visningsprogram](/help/assets/managing-viewer-presets.md), efter behov.

   Administratörer kan skapa eller ändra visningsförinställningar för rotationsuppsättningar. Om du vill visa rotationsuppsättningen med en visningsförinställning markerar du rotationsuppsättningen och väljer **Visningsprogram** i listrutan till vänster.

   Se **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Viewer Presets]** om du vill skapa eller redigera visningsförinställningar.

   Se [Lägga till och redigera visningsprogramförinställningar](/help/assets/managing-viewer-presets.md).

1. [Visa en snurruppsättning](#viewing-spin-sets).

   Du kan visa och komma åt uppsättningar som skapats med hjälp av gruppuppsättningsförinställningar på tre olika sätt. (Uppsättningar som skapats med gruppuppsättningsförinställningar, gör *not* visas i användargränssnittet.)

1. [Förhandsgranska en snurra uppsättning](/help/assets/previewing-assets.md).

   Markera rotationsuppsättningen så kan du förhandsgranska den. Rotera snurrsuppsättningen. Du kan välja olika visningsprogram från **[!UICONTROL Viewers]** som finns på den vänstra menyn.

1. [Publicera en snurruppsättning](/help/assets/publishing-dynamicmedia-assets.md).

   När du publicerar en snurruppsättning aktiveras URL-adressen och strängen Embed. Dessutom måste du [publicera visningsförinställningen](/help/assets/managing-viewer-presets.md).

1. [Länka URL:er till ditt webbprogram](/help/assets/linking-urls-to-yourwebapplication.md) eller [Bädda in video- eller bildvisningsprogrammet](/help/assets/embed-code.md).

   Adobe Experience Manager Assets skapar URL-anrop för Spin Sets och aktiverar dem när du har publicerat snurruppsättningarna. Du kan kopiera dessa URL:er när du förhandsgranskar resurser. Du kan även bädda in dem på din webbplats.

   Markera rotationsuppsättningen och välj sedan **[!UICONTROL Viewers]** i listrutan till vänster.

   Se [Länka en snurruppsättning till en webbsida](/help/assets/linking-urls-to-yourwebapplication.md) och [Bädda in video- eller bildvisningsprogrammet](/help/assets/embed-code.md).

Om det behövs kan du [redigera en snurruppsättning](#editing-spin-sets). Dessutom kan du visa och ändra [Snurra uppsättningsegenskaper](/help/assets/manage-assets.md#editing-properties).

## Överför resurser för en snurruppsättning {#uploading-assets-for-spin-sets}

Du behöver minst 8-12 tagningar av ett objekt för en endimensionell snurra och 16-24 för en tvådimensionell snurra uppsättning. Fotografierna måste tas med jämna mellanrum för att ge intryck av att objektet roteras och vändas. Om en endimensionell snurra t.ex. innehåller 12 tagningar roterar du objektet 30° (360/12) för varje tagning.

Du kan överföra bilder för snurra uppsättningar på samma sätt som du gör [ladda upp alla andra resurser i Experience Manager Assets](/help/assets/manage-assets.md).

Se [Dynamic Media - Rasterbildformat som stöds](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) om du vill visa en lista över format som kan användas i snurruppsättningar.

### Riktlinjer för hämtning av bilder för din snurruppsättning {#guidelines-for-shooting-spin-set-images}

Nedan följer några tips om hur du använder snurra uppsättningsbilder. Ju fler bilder du har i en snurrfunktion, desto bättre blir effekten av att snurra. Om du inkluderar många bilder i uppsättningen ökar dock tiden det tar för bilderna att läsas in. Experience Manager rekommenderar följande riktlinjer för att ta bilder för användning i snurra uppsättningar:

* Använd minst 8-12 bilder i en endimensionell snurra och 16-24 bilder i en tvådimensionell snurra. Minst 8 bilder krävs för att kunna vridas 360°. Endimensionella snurruppsättningar är vanligare eftersom det är arbetsintensivt att skapa tvådimensionella snurruppsättningar.
* Använd ett förlustfritt format, TIFF och PNG rekommenderas.
* Maskera alla bilder så att objektet visas på en helt vit eller annan bakgrund med hög kontrast. Du kan också lägga till skuggor.
* Se till att produktinformationen är väl belyst och i fokus.
* Ta snurra bilder till modekläder med mannequin eller modell. Ofta är mannequin antingen maskerat (med hjälp av en glasmannequin) eller en stiliserad mannequin/form visas i bilden. Du kan skapa en omformningsrotation genom att definiera antalet vinklar. Markera varje vinkel med band på golvet så att du kan vägleda modellen till steg och titta i riktningen för varje tagning.

## Skapa en snurruppsättning {#creating-spin-sets}

I det här avsnittet beskrivs hur du skapar en snurra uppsättning i Experience Manager.

>[!NOTE]
>
>Du kan också skapa rotationsuppsättningar automatiskt med hjälp av [förinställningar för gruppuppsättningar](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets). **Viktigt:** Batchuppsättningar skapas av IPS (Image Production System) som en del av tillgångsintag och är endast tillgängliga i Dynamic Media-Scene7-läge.
>
>Se&quot;Skapa gruppuppsättningsförinställningar för automatisk generering av bilduppsättningar och snurruppsättningar&quot; i [Konfigurera Dynamic Media - Scene7-läge](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets).

>[!NOTE]
>
>Den ordning i vilken bilderna visas i en snurrfunktion. Se till att ordna dem så att snurret blir en mjuk 360-gradersvy.

När du skapar en snurrsuppsättning rekommenderar Adobe följande bästa praxis och tillämpar följande gräns:

| Begränsningstyp | Bästa praxis | Begränsad |
| --- | --- | --- |
| Maximalt antal rader/kolumner per 2D-uppsättning | 12-18 bilder per uppsättning | 1000 |

Se även [Dynamic Media begränsningar](/help/assets/limitations.md).

**Så här skapar du en snurra:**

1. I Resurser navigerar du till den plats där du vill skapa en snurruppsättning och väljer **[!UICONTROL Create]** och markera **[!UICONTROL Spin Set]**. Du kan också skapa uppsättningen inifrån en mapp som innehåller resurserna. Redigeraren för rotationsuppsättningar visas.

   ![6_5_spinset-createpulldownmenu](assets/6_5_spinset-createpulldownmenu.png)

1. I sned uppsättningsredigeraren, i **[!UICONTROL Title]** anger du ett namn för rotationsrutan. Namnet visas i banderollen över snurruppsättningen. Du kan också ange en beskrivning.

   ![6_5_spinset-spinseteditortitle](assets/6_5_spinset-spinseteditortitle.png)

   >[!NOTE]
   >
   >När du skapar rotationsuppsättningen kan du ändra miniatyrbilden för rotationsuppsättningen eller låta Experience Manager välja miniatyrbilden automatiskt baserat på resurserna i rotationsuppsättningen. Om du vill välja en miniatyrbild väljer du **[!UICONTROL Change thumbnail]** och markera en bild (du kan navigera till andra mappar för att hitta bilder också). Om du har markerat en miniatyrbild och sedan vill att Experience Manager ska generera en miniatyrbild från rotationsuppsättningen väljer du **[!UICONTROL Switch to Automatic thumbnail]**.

1. Gör något av följande:

   * I närheten av det övre vänstra hörnet på sidan för redigeraren för sned uppsättning väljer du **[!UICONTROL Add Asset]**.

   * I mitten av sidan för redigeraren för sned uppsättning väljer du **[!UICONTROL Tap to open Asset Selector]**.
   Tryck för att välja resurser som du vill inkludera i din snurruppsättning. De markerade resurserna visas med en bock. När du är klar väljer du **[!UICONTROL Select]**.

   Med resursväljaren kan du söka efter resurser genom att skriva ett nyckelord och trycka på **[!UICONTROL Return]**. Du kan också använda filter för att förfina sökresultatet. Du kan filtrera efter sökväg, samling, filtyp och tagg. Markera filtret och välj sedan **[!UICONTROL Filter]** -ikonen i verktygsfältet. Ändra vyn genom att trycka på ikonen Visa och sedan välja **[!UICONTROL Column View]**, **[!UICONTROL Card View]** eller **[!UICONTROL List View]**.

   Se [Arbeta med väljare](/help/assets/working-with-selectors.md).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. När du lägger till resurser i uppsättningen läggs de automatiskt till i alfanumerisk ordning. Du kan ändra ordning på eller sortera resurser manuellt när du har lagt till dem.

   Om det behövs kan du dra en resurs sorteringsikon till höger om resursens filnamn för att ordna om bilderna uppåt eller nedåt i uppsättningslistan.

   ![Ändra ordning på bildruta 11 i rotationsrutan genom att dra den till en ny plats](assets/6_5_spinset-reorderassets.png).

   Ändra ordning på bildruta 11 i rotationsrutan genom att dra den till en ny plats.

1. (Valfritt) Gör något av följande:

   * Om du vill ta bort en bild markerar du bilden och väljer **[!UICONTROL Delete Asset]**.

   * Om du vill använda en förinställning väljer du **[!UICONTROL Preset]** väljer du sedan en förinställning som ska användas på alla resurser samtidigt.

1. Välj **[!UICONTROL Save]**. Den nyligen skapade rotationsuppsättningen visas i den mapp du skapade den i.

## Visa en snurruppsättning {#viewing-spin-sets}

Du kan skapa snurruppsättningar antingen i användargränssnittet eller automatiskt med [gruppuppsättningsförinställningar](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets). Men uppsättningar som skapats med gruppuppsättningsförinställningar gör *not* visas i användargränssnittet. Du kan få åtkomst till uppsättningar som skapats med gruppuppsättningsförinställningar på tre olika sätt. (Dessa metoder är tillgängliga även om du har skapat rotationsuppsättningarna i användargränssnittet).

>[!NOTE]
>
>Du kan också visa uppsättningar via användargränssnittet enligt beskrivningen i [Redigera snurruppsättningar](#editing-spin-sets).

**Så här visar du en snurruppsättning:**

1. När egenskaperna för en enskild resurs öppnas. Egenskaperna anger vad som ställer in den valda resursen som medlem av (under **[!UICONTROL Member of Sets]**). Markera namnet på uppsättningen så att du kan se hela uppsättningen.

   ![chlimage_1-156](assets/chlimage_1-384.png)

1. Från en medlemsbild i en uppsättning. Välj **[!UICONTROL Sets]** för att visa de uppsättningar som resursen är medlem i.

   ![chlimage_1-157](assets/chlimage_1-385.png)

1. I sökningen kan du välja **[!UICONTROL Filters]** och sedan expandera **[!UICONTROL Dynamic Media]** och markera **[!UICONTROL Sets]**.

   Sökningen returnerar matchande uppsättningar som skapats manuellt i användargränssnittet eller automatiskt skapats med gruppuppsättningsförinställningar. För automatiska uppsättningar utförs sökfrågan med `Starts with` sökvillkor som skiljer sig från sökningen i Experience Manager som baseras på att använda `Contains` sökvillkor. Ange att filtret ska **[!UICONTROL Sets]** är det enda sättet att söka i automatiska uppsättningar.

   ![chlimage_1-158](assets/chlimage_1-386.png)

## Redigera en snurra uppsättning {#editing-spin-sets}

Du kan utföra olika redigeringsåtgärder på snurra uppsättningar, till exempel:

* Lägg till bilder i rotationsrutan.
* Ändra ordning på bilderna i rotationsrutan.
* Ta bort resurser i rotationsuppsättningen.
* Använd förinställningar för visningsprogram.
* Ta bort rotationsrutan.

**Så här redigerar du en snurra:**

1. Gör något av följande:

   * Håll pekaren över en resurs i en sned uppsättning och välj sedan **[!UICONTROL Edit]** (pennikon).
   * Håll pekaren över en resurs i en snurra uppsättning, välj **[!UICONTROL Select]** (bockmarkeringsikon) och sedan välja **[!UICONTROL Edit]** i verktygsfältet.

   * Välj en resurs i en snurra uppsättning och välj sedan **[!UICONTROL Edit]** (pennikon) i verktygsfältet.

1. Gör något av följande om du vill redigera rotationsuppsättningen:

   * Om du vill ändra ordning på bilderna drar du en bild till en ny plats (markera ikonen för att ändra ordning för att flytta objekt).
   * Om du vill sortera objekt i stigande eller fallande ordning markerar du kolumnrubriken.
   * Om du vill lägga till en resurs eller uppdatera en befintlig resurs väljer du **[!UICONTROL Add Asset]**. Navigera till en resurs, markera den och välj **[!UICONTROL Select]** nära det övre högra hörnet.
Om du tar bort den bild som Experience Manager använder som miniatyrbild genom att ersätta den med en annan bild, visas fortfarande originalresursen.
   * Om du vill ta bort en resurs markerar du den och väljer **[!UICONTROL Delete Asset]**.
   * Om du vill använda en förinställning väljer du förinställningsikonen och väljer en förinställning.
   * Om du vill ta bort en hel snurruppsättning går du till snurra-uppsättningen, markerar den och markerar den **[!UICONTROL Delete]**

   >[!NOTE]
   >
   >Du kan redigera bilderna i en snurruppsättning genom att navigera till uppsättningen och välja **[!UICONTROL Set Members]** i den vänstra listen och välj sedan pennikonen på en enskild resurs för att öppna redigeringsfönstret.

1. Välj **[!UICONTROL Save]** när redigeringen är klar.

## Förhandsgranska en snurra uppsättning {#previewing-spin-sets}

Se [Förhandsgranska resurser](/help/assets/previewing-assets.md).

## Publicera en snurruppsättning {#publishing-spin-sets}

Se [Publicera resurser](/help/assets/publishing-dynamicmedia-assets.md).
