---
title: Använd layoutläget för att ändra storlek på komponenter för interaktiv kommunikation
description: Definiera placeringen av komponenterna med det responsiva stödrastret som finns i layoutläget
feature: Interactive Communication
exl-id: 9534fcb2-4260-4dd0-9f7e-779b10fd3a22
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%

---

# Använd layoutläget för att ändra storlek på komponenter {#use-layout-mode-to-resize-components}

Med gränssnittet Interactive Communication Web Channel kan du ändra storlek på komponenter i layoutläget. Dra och släpp blå punkter i kolumner för att definiera start- och slutpunkterna för placering av komponenter. De blå punkterna visas när du har tryckt på komponenten i det responsiva rutnätet. Det responsiva rutnätet består av 12 lika stora kolumner. Den vita och blå färgskuggningen i alternativa kolumner skiljer den ena kolumnen från den andra.

Du kan använda layoutläget för att ändra storlek på komponenter för alla enhetstyper, som stationära datorer, surfplattor, telefoner och andra mindre enheter. Tabletten hämtar automatiskt layoutkonfigurationen från skrivbordsversionen och de mindre enheterna hämtar layoutkonfigurationen från telefonen. Du kan dock åsidosätta de automatiskt härledda konfigurationerna för att definiera olika konfigurationer för varje enhetstyp.

>[!NOTE]
>
>Om du skapar webbkanalen med [Skriva ut kanal som master](../../forms/using/create-interactive-communication.md) för interaktiv kommunikation omfattar de komponenter som är tillgängliga för storleksändring även de delformulär och fält som genereras automatiskt i webbkanalen med hjälp av utskriftskanalen. Webbkanalen behåller layouten för Print channel-elementen i layoutläge.

## Åtkomst till layoutläge {#access-layout-mode}

Välj **Layout** från listrutan som visas högst upp i redigeringsgränssnittet för interaktiv kommunikation bredvid **Förhandsgranska** alternativ. Formuläret visas i layoutläget.

1. Logga in på AEM författarinstans och navigera till **Adobe Experience Manager** > **Forms** > **Forms och dokument**.
1. Skapa en [Interaktiv kommunikation](../../forms/using/create-interactive-communication.md) eller öppna en befintlig.
1. Välj **Layout** från listrutan som visas högst upp bredvid **Förhandsgranska** alternativ. Formuläret visas i layoutläget.

   ![Layoutläge för interaktiv kommunikation](assets/layout_mode_ic_new.png)

## Ändra storlek på komponenter {#resize-components}

1. Tryck på komponenten för att ändra storlek i layoutläget. De blå punkterna visas i början och slutet av det responsiva rutnätet.
1. Dra och släpp de blå punkterna för att definiera placeringen av komponenten i det responsiva rutnätet.

   ![Ändra storlek i layoutläget](assets/layout_mode_resize_new_updated.png)

   Verktygsfältet som visas när du har tryckt på komponenter består av följande alternativ:

   * **Överordnad:** Markera den överordnade komponenten för en komponent.
   * **Flyt till ny rad:** Flytta komponenten till nästa rad om det finns flera komponenter på samma rad.

   Du kan ångra alla storleksändringar och använda standardlayout på panelen som innehåller storleksändrade komponenter med **[!UICONTROL Revert breakpoint layout]** ( ![Återställ brytpunkt](assets/reverttopreviouslypublishedversion.png)). Tryck på den överordnade för den storleksändrade komponenten för att visa alternativet.

   >[!NOTE]
   >
   >Du kan inte ändra storlek på tabellkolumn, verktygsfält, verktygsfältsknapp och målområdeskomponenter i layoutläget. Använd stilläget om du vill ändra storlek på de här komponenterna.

### Exempel {#example}

**Mål:** Du vill infoga en tabellkomponent och en bildkomponent och placera dem parallellt med varandra i en interaktiv kommunikation.

1. Infoga tabell- och bildkomponenterna i redigeringsläget i webbkanalen i en interaktiv kommunikation. Bildkomponenten visas efter tabellkomponenten.
1. Växla till layoutläget och tryck på tabellkomponenten. De blå punkter som komponentvisningen ska ändra storlek på i kolumnerna 1 och 12.
1. Dra och släpp den blå punkten i kolumn 12 till kolumn 6 i det responsiva rutnätet.

   ![Definiera tabellens slutpunkt](assets/layout_mode_end_point_table_new.png)

1. Markera på samma sätt bildkomponenten och dra och släpp den blå punkten i kolumn 1 till kolumn 7 i det responsiva rutnätet. Tabellen och bildkomponenterna visas parallellt med varandra.

   ![Tabell och bilden parallellt i layoutläge](assets/table_image_parallel_new.png)

   Du kan välja komponenten Bild och trycka på **Flyt till ny rad** som finns i verktygsfältet för att flytta bildkomponenten till nästa rad.

## Ändra storlek på paneler {#resize-panels-layout-mode}

Utför följande steg om du vill ändra storlek på hela panelen i stället för enskilda komponenter:

1. Tryck på någon av komponenterna i panelen som du vill ändra storlek på, välj ![Markera överordnad](assets/select_parent_icon.svg)och välj det första alternativet i listrutan, om panelen är komponentens omedelbara överordnade objekt.

   De blå punkterna visas i början och slutet av det responsiva rutnätet.

1. Dra och släpp de blå punkterna för att definiera panelens position i det responsiva rutnätet.
Du kan upprepa steg 1 och 2 och välja ![Markera överordnad](assets/float_to_new_line_icon.svg) om du vill ändra den storleksändrade panelen till nästa rad.

## Definiera layout med flera kolumner för en panel

Utför följande steg för att definiera antalet kolumner för en panel:

1. I **[!UICONTROL Edit]** läge, tryck på panelen, välj ![Konfigurera](assets/configure_icon.png)och markera **[!UICONTROL Responsive - everything on the page without navigation]** från **[!UICONTROL Panel Layout]** listruta.

1. Tryck ![Spara](assets/save_icon.svg) för att spara egenskaperna.

1. I **[!UICONTROL Layout]** läge, tryck på någon av komponenterna i panelen, välj ![Markera överordnad](assets/select_parent_icon.svg)och markerar panelen.

1. Tryck ![flera kolumner](assets/multi-column.svg) och välj antalet kolumner i listrutan. Antalet kolumner kan vara mellan 1 och 12. Panelen delas upp i en layout med flera kolumner.

![flera kolumner i layoutläge](assets/multi-column-layout.png)

## Inaktivera layoutläget för formulär med gammal responsiv layout {#disable-layout-mode-for-forms-with-old-responsive-layout}

Du kan inaktivera layoutläget för formulär med äldre responsiv layout genom att redigera egenskaperna för mallen som används i formuläret.

Utför följande steg för att inaktivera layoutläget:

1. Välj **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Templates]** och öppna mallen som används i formuläret i **[!UICONTROL Edit]** läge.
1. Markera dokumentbehållaren i den vänstra rutan och tryck på **[!UICONTROL Policy.]**

   ![Inaktivera layoutläget](assets/policy_disable_layout_mode.png)

1. Tryck på **[!UICONTROL Layout Settings]** och markera **[!UICONTROL Disable Layout Mode]**.
1. Tryck ![Spara ändringar](assets/save_icon.png) om du vill spara mallegenskaperna.
