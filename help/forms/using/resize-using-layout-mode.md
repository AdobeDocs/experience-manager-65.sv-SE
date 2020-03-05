---
title: Använd layoutläget för att ändra storlek på komponenter
seo-title: Använd layoutläget för att ändra storlek på komponenter
description: 'Definiera placeringen av komponenterna med det responsiva stödrastret som finns i layoutläget '
seo-description: 'Definiera placeringen av komponenterna med det responsiva stödrastret som finns i layoutläget '
uuid: 6b077ebe-caea-4ae3-b17a-be2dca94eeb3
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9e9aaf36-bb86-4954-83cc-fa6b3e80ae4b
docset: aem65
translation-type: tm+mt
source-git-commit: 8ebe1a2c23ec5e3e16807072ac17ec13a6df9701

---


# Använd layoutläget för att ändra storlek på komponenter{#use-layout-mode-to-resize-components}

Med det adaptiva formuläret och redigeringsgränssnittet för webbkanalen för interaktiv kommunikation kan du ändra storlek på komponenter i layoutläget. Dra och släpp blå punkter i kolumner för att definiera start- och slutpunkterna för placering av komponenter. De blå punkterna visas när du har tryckt på komponenten i det responsiva rutnätet. Det responsiva rutnätet består av 12 lika stora kolumner. Den vita och blå färgskuggningen i alternativa kolumner skiljer den ena kolumnen från den andra.

Du kan använda layoutläget för att ändra storlek på komponenter för alla enhetstyper, som stationära datorer, surfplattor, telefoner och andra mindre enheter. Tabletten hämtar automatiskt layoutkonfigurationen från skrivbordsversionen och de mindre enheterna hämtar layoutkonfigurationen från telefonen. Du kan dock åsidosätta de automatiskt härledda konfigurationerna för att definiera olika konfigurationer för varje enhetstyp.

Om du skapar webbkanalen med [Utskriftskanalen som master](../../forms/using/create-interactive-communication.md) för en interaktiv kommunikation, inkluderar de komponenter som är tillgängliga för storleksändring även de delformulär och fält som genereras automatiskt i webbkanalen med hjälp av Print-kanalen. Webbkanalen behåller layouten för Print channel-elementen i layoutläge.

## Åtkomst till layoutläge {#access-layout-mode}

Välj **Layout** i listrutan som visas högst upp i det adaptiva formuläret och redigeringsgränssnittet för interaktiv kommunikation bredvid alternativet **Förhandsgranska** . Formuläret visas i layoutläget.

1. Logga in på AEM-författarinstansen och gå till **Adobe Experience Manager** > **Formulär** > **Formulär och dokument**.
1. [Skapa ett nytt](../../forms/using/create-interactive-communication.md) eller öppna ett befintligt adaptivt formulär eller en interaktiv kommunikation.
1. Välj **Layout** i listrutan som visas högst upp bredvid alternativet **Förhandsgranska** . Formuläret visas i layoutläget.

   ![Layoutläge för interaktiv kommunikation](assets/layout_mode_ic_new.png)

## Ändra storlek på komponenter {#resize-components}

1. Tryck på komponenten för att ändra storlek i layoutläget. De blå punkterna visas i början och slutet av det responsiva rutnätet.
1. Dra och släpp de blå punkterna för att definiera placeringen av komponenten i det responsiva rutnätet.

   ![Ändra storlek i layoutläget](assets/layout_mode_resize_new_updated.png)

   Verktygsfältet som visas när du har tryckt på komponenter består av följande alternativ:

   * **Överordnad:** Markera den överordnade komponenten för en komponent.
   * **Flyt till ny rad:** Flytta komponenten till nästa rad om det finns flera komponenter på samma rad.
   Du kan ångra alla storleksändringar och använda standardlayout på panelen som innehåller storleksändrade komponenter med alternativet **[!UICONTROL Återställ brytpunktslayout]** ( ![Återställ brytpunkt](assets/reverttopreviouslypublishedversion.png)). Tryck på den överordnade för den storleksändrade komponenten för att visa alternativet.

   >[!NOTE]
   >
   >Du kan inte ändra storlek på tabellkolumn, verktygsfält, verktygsfältsknapp och målområdeskomponenter i layoutläget. Använd stilläget om du vill ändra storlek på komponenterna.

### Exempel {#example}

**Mål:** Du vill infoga en tabellkomponent och en bildkomponent och placera dem parallellt med varandra i en interaktiv kommunikation.

1. Infoga tabell- och bildkomponenterna i redigeringsläget i webbkanalen. Bildkomponenten visas efter tabellkomponenten.
1. Växla till layoutläget och tryck på tabellkomponenten. De blå punkter som komponentvisningen ska ändra storlek på i kolumnerna 1 och 12.
1. Dra och släpp den blå punkten i kolumn 12 till kolumn 6 i det responsiva rutnätet.

   ![Definiera tabellens slutpunkt](assets/layout_mode_end_point_table_new.png)

1. Markera på samma sätt bildkomponenten och dra och släpp den blå punkten i kolumn 1 till kolumn 7 i det responsiva rutnätet. Tabellen och bildkomponenterna visas parallellt med varandra.

   ![Tabell och bilden parallellt i layoutläge](assets/table_image_parallel_new.png)

   Du kan markera bildkomponenten och trycka på alternativet **Flyt till ny rad** i verktygsfältet för att flytta bildkomponenten till nästa rad.

## Ändra storlek på paneler {#resize-panels-layout-mode}

Utför följande steg om du vill ändra storlek på hela panelen i stället för enskilda komponenter:

1. Tryck på någon av komponenterna i panelen som du vill ändra storlek på, välj ![Markera överordnad](assets/select_parent_icon.svg)och markera det första alternativet i listrutan, om panelen är komponentens omedelbara överordnade.

   De blå punkterna visas i början och slutet av det responsiva rutnätet.

1. Dra och släpp de blå punkterna för att definiera panelens position i det responsiva rutnätet.
Du kan upprepa steg 1 och 2 och välja ![Markera överordnad](assets/float_to_new_line_icon.svg) för att flytta den storleksändrade panelen till nästa rad.

## Definiera layout med flera kolumner för en panel

Utför följande steg för att definiera antalet kolumner för en panel:

1. I **[!UICONTROL redigeringsläget]** trycker du på panelen, väljer ![Konfigurera](assets/configure_icon.png)och väljer **[!UICONTROL Responsiv - allt på sidan utan navigeringsalternativ]** .

1. Tryck på ![Spara](assets/save_icon.svg) för att spara egenskaperna.

1. I **[!UICONTROL layoutläget]** trycker du på någon av komponenterna i panelen som du vill ändra storlek på, väljer ![Markera överordnad](assets/select_parent_icon.svg)och väljer det första alternativet i listrutan om panelen är komponentens omedelbara överordnade.

1. Tryck på ![flera kolumner](assets/multi-column.svg) och välj antalet kolumner i listrutan. Antalet kolumner kan vara mellan 1 och 12. Panelen delas upp i en layout med flera kolumner.

![flera kolumner i layoutläge](assets/multi-column-layout.png)

## Aktivera det nya responsiva rutnätet för äldre responsiva layouter {#enableresponsivegrid}

Aktivera det nya responsiva stödrastret för formulär som du skapar med AEM Forms 6.4 eller senare för att ändra storlek på komponenter.

>[!NOTE]
>
>När du växlar till det nya responsiva rutnätet tas de layoutegenskaper som redan har definierats bort för komponenter som används i formuläret.

Gör så här för att aktivera det nya responsiva rutnätet:

1. Välj **Layout** i listrutan som visas högst upp bredvid alternativet **Förhandsgranska** . En bekräftelse som aktiverar layoutläget visas.
1. Tryck på **Ja** för att aktivera **layoutläget** för formuläret.

### Bädda in ett gammalt fragment i en adaptiv form med ny responsiv layout {#embed-an-old-fragment-in-an-adaptive-form-with-new-responsive-layout}

Med den nya responsiva layouten för adaptiva formulär kan du lägga till ett adaptivt formulärfragment med den gamla responsiva layouten i formuläret. Den nya layouten tar dock bort de layoutegenskaper som redan har definierats för komponenter som används i fragmentet. Du kan växla till layoutläget för att definiera layoutegenskaperna för komponenter som används i fragmentet.

### Bädda in ett fragment med ny responsiv layout i ett gammalt anpassat formulär {#embed-a-fragment-with-new-responsive-layout-in-an-old-adaptive-form}

Om du bäddar in ett fragment med den nya responsiva layouten i ett adaptivt formulär med en gammal responsiv layout uppmanas du att aktivera layoutläget för formuläret och bädda in fragmentet igen.

Om du vill aktivera layoutläget väljer du **Layout** i listrutan som visas högst upp bredvid alternativet **Förhandsgranska** och trycker på **Ja** för att bekräfta. Välj **redigeringsläget** om du vill bädda in fragmentet igen.

## Inaktivera layoutläget för formulär med gammal responsiv layout {#disable-layout-mode-for-forms-with-old-responsive-layout}

Du kan inaktivera layoutläget för formulär med äldre responsiv layout genom att redigera egenskaperna för mallen som används i formuläret.

Utför följande steg för att inaktivera layoutläget:

1. Välj **[!UICONTROL Verktyg]** > **[!UICONTROL Allmänt]** > **[!UICONTROL Mallar]** och öppna mallen som används i formuläret i läget **[!UICONTROL Redigera]** .
1. Välj dokumentbehållaren i den vänstra rutan och tryck på **[!UICONTROL Policy.]**

   ![Inaktivera layoutläget](assets/policy_disable_layout_mode.png)

1. Tryck på fliken **[!UICONTROL Layoutinställningar]** och välj **[!UICONTROL Inaktivera layoutläge]**.
1. Tryck på ![Spara ändringar](assets/save_icon.png) för att spara mallegenskaperna.

