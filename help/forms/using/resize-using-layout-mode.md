---
title: Använd layoutläget för att ändra storlek på komponenter för anpassningsbara formulär
description: 'Definiera placeringen av komponenterna med det responsiva stödrastret som finns i layoutläget '
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 0%

---


# Använd layoutläget för att ändra storlek på komponenter {#use-layout-mode-to-resize-components}

Med det adaptiva gränssnittet för formulärutveckling kan du ändra storlek på komponenter i layoutläget. Dra och släpp blå punkter i kolumner för att definiera start- och slutpunkterna för placering av komponenter. De blå punkterna visas när du har tryckt på komponenten i det responsiva rutnätet. Det responsiva rutnätet består av 12 lika stora kolumner. Den vita och blå färgskuggningen i alternativa kolumner skiljer den ena kolumnen från den andra.

Du kan använda layoutläget för att ändra storlek på komponenter för alla enhetstyper, som stationära datorer, surfplattor, telefoner och andra mindre enheter. Tabletten hämtar automatiskt layoutkonfigurationen från skrivbordsversionen och de mindre enheterna hämtar layoutkonfigurationen från telefonen. Du kan dock åsidosätta de automatiskt härledda konfigurationerna för att definiera olika konfigurationer för varje enhetstyp.

## Åtkomst till layoutläget {#access-layout-mode}

Välj **Layout** i listrutan som visas högst upp i redigeringsgränssnittet för adaptiva formulär bredvid alternativet **Förhandsgranska**. Formuläret visas i layoutläget.

1. Logga in på AEM författarinstans och navigera till **Adobe Experience Manager** > **Forms** > **Forms &amp; Documents**.
1. Skapa ett nytt eller öppna ett befintligt [adaptivt formulär](../../forms/using/creating-adaptive-form.md).
1. Välj **Layout** i listrutan som visas högst upp bredvid alternativet **Förhandsgranska**. Formuläret visas i layoutläget.

   ![Layoutläge](assets/layout_mode_ic_new.png)

## Ändra storlek på komponenter {#resize-components}

1. Tryck på komponenten för att ändra storlek i layoutläget. De blå punkterna visas i början och slutet av det responsiva rutnätet.
1. Dra och släpp de blå punkterna för att definiera placeringen av komponenten i det responsiva rutnätet.

   ![Ändra storlek i layoutläget](assets/layout_mode_resize_new_updated1.png)

   Verktygsfältet som visas när du har tryckt på komponenter består av följande alternativ:

   * **[!UICONTROL Parent]**: Markera den överordnade komponenten för en komponent.
   * **[!UICONTROL Revert breakpoint layout]**: Ångra alla storleksändringar och använd standardlayout på komponenten.
   * **[!UICONTROL Float to new line]**: Flytta komponenten till nästa rad om det finns flera komponenter på samma rad.

   Du kan också använda alternativet **[!UICONTROL Revert breakpoint layout]** ( ![Återställ brytpunkt](assets/reverttopreviouslypublishedversion.png)) på panelnivå om du vill ångra alla storleksändringar.

   >[!NOTE]
   >
   >Du kan inte ändra storlek på tabellkolumn, verktygsfält, verktygsfältsknapp och målområdeskomponenter i layoutläget. Använd stilläget om du vill ändra storlek på komponenterna.

### Exempel {#example}

**Mål:** Du vill infoga en tabellkomponent och en bildkomponent och placera dem parallellt med varandra i en adaptiv form.

1. Infoga tabell- och bildkomponenterna i redigeringsläget i det adaptiva formuläret. Bildkomponenten visas efter tabellkomponenten.
1. Växla till layoutläget och tryck på tabellkomponenten. De blå punkter som komponentvisningen ska ändra storlek på i kolumnerna 1 och 12.
1. Dra och släpp den blå punkten i kolumn 12 till kolumn 6 i det responsiva rutnätet.

   ![Definiera tabellens slutpunkt](assets/layout_mode_end_point_table_new.png)

1. Markera på samma sätt bildkomponenten och dra och släpp den blå punkten i kolumn 1 till kolumn 7 i det responsiva rutnätet. Tabellen och bildkomponenterna visas parallellt med varandra.

   ![Tabell och bilden parallellt i layoutläge](assets/table_image_parallel_new.png)

   Du kan markera bildkomponenten och trycka på alternativet **Flyt till ny rad** i verktygsfältet för att flytta bildkomponenten till nästa rad.

## Ändra storlek på paneler {#resize-panels-layout-mode}

Utför följande steg om du vill ändra storlek på hela panelen i stället för enskilda komponenter:

1. Tryck på någon av komponenterna i panelen som du vill ändra storlek på, välj ![Markera överordnad](assets/select_parent_icon.svg) och välj det första alternativet i listrutan, om panelen är komponentens omedelbara överordnade.

   De blå punkterna visas i början och slutet av det responsiva rutnätet.

1. Dra och släpp de blå punkterna för att definiera panelens position i det responsiva rutnätet.
Du kan upprepa steg 1 och 2 och välja ![Välj överordnad](assets/float_to_new_line_icon.svg) för att flytta den storleksändrade panelen till nästa rad.

## Definiera layout med flera kolumner för en panel

Utför följande steg för att definiera antalet kolumner för en panel:

1. I **[!UICONTROL Edit]**-läget trycker du på panelen, väljer ![Konfigurera](assets/configure_icon.png) och väljer **[!UICONTROL Responsive - everything on the page without navigation]** i listrutan **[!UICONTROL Panel Layout]**.

1. Tryck på ![Spara](assets/save_icon.svg) för att spara egenskaperna.

1. I läget **[!UICONTROL Layout]** trycker du på någon av komponenterna i panelen, väljer ![Välj överordnad](assets/select_parent_icon.svg) och väljer panelen.

1. Tryck på ![multi-column](assets/multi-column.svg) och välj antalet kolumner i listrutan. Antalet kolumner kan vara mellan 1 och 12. Panelen delas upp i en layout med flera kolumner.

![flera kolumner i layoutläge](assets/multi-column-layout.png)

## Aktivera det nya responsiva rutnätet för äldre responsiva layouter {#enableresponsivegrid}

Aktivera det nya responsiva rutnätet för formulär som du skapar med AEM Forms 6.4 eller tidigare för att ändra storlek på komponenter.

>[!NOTE]
>
>När du växlar till det nya responsiva rutnätet tas de layoutegenskaper som redan har definierats bort för komponenter som används i formuläret.

Gör så här för att aktivera det nya responsiva rutnätet:

1. Välj **Layout** i listrutan som visas högst upp bredvid alternativet **Förhandsgranska**. En bekräftelse som aktiverar layoutläget visas.
1. Tryck på **Yes** för att aktivera **layoutläget** för formuläret.

### Bädda in ett gammalt fragment i ett adaptivt formulär med ny responsiv layout {#embed-an-old-fragment-in-an-adaptive-form-with-new-responsive-layout}

Med den nya responsiva layouten för adaptiva formulär kan du lägga till ett adaptivt formulärfragment med den gamla responsiva layouten i formuläret. Den nya layouten tar dock bort de layoutegenskaper som redan har definierats för komponenter som används i fragmentet. Du kan växla till layoutläget för att definiera layoutegenskaperna för komponenter som används i fragmentet.

### Bädda in ett fragment med ny responsiv layout i en gammal adaptiv form {#embed-a-fragment-with-new-responsive-layout-in-an-old-adaptive-form}

Om du bäddar in ett fragment med den nya responsiva layouten i ett adaptivt formulär med en gammal responsiv layout uppmanas du att aktivera layoutläget för formuläret och bädda in fragmentet igen.

Om du vill aktivera layoutläget väljer du **Layout** i listrutan som visas högst upp bredvid alternativet **Förhandsgranska** och bekräftar genom att trycka på **Ja**. Välj **Redigera**-läge om du vill bädda in fragmentet igen.

## Inaktivera layoutläget för formulär med gammal responsiv layout {#disable-layout-mode-for-forms-with-old-responsive-layout}

Du kan inaktivera layoutläget för formulär med äldre responsiv layout genom att redigera egenskaperna för mallen som används i formuläret.

Utför följande steg för att inaktivera layoutläget:

1. Välj **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Templates]** och öppna mallen som används i formuläret i **[!UICONTROL Edit]**-läge.
1. Markera dokumentbehållaren i den vänstra rutan och tryck på **[!UICONTROL Policy.]**

   ![Inaktivera layoutläget](assets/policy_disable_layout_mode.png)

1. Tryck på fliken **[!UICONTROL Layout Settings]** och välj **[!UICONTROL Disable Layout Mode]**.
1. Tryck på ![Spara ändringar](assets/save_icon.png) för att spara mallegenskaperna.

