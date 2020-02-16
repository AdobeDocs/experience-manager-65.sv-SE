---
title: Hantera flera resurser och samlingar
description: Lär dig hur du redigerar metadata för flera resurser och samlingar samtidigt för att snabbt sprida vanliga metadataändringar.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Hantera resurser och samlingar {#managing-multiple-assets-and-collections}

Med Adobe Enterprise Manager (AEM) Assets kan du redigera metadata för flera resurser samtidigt så att du snabbt kan sprida vanliga metadataändringar till resurser samtidigt. Du kan också redigera metadata för flera samlingar samtidigt.

Använd egenskapssidan för att utföra metadataändringar på flera resurser eller samlingar:

* Ändra metadataegenskaper till ett gemensamt värde
* Lägga till eller ändra taggar

Om du vill anpassa sidan med metadataegenskaper, inklusive lägga till, ändra eller ta bort metadataegenskaper, använder du schemaredigeraren.

>[!NOTE]
>
>Massredigeringsmetoderna fungerar för resurser som är tillgängliga i en mapp eller en samling. För resurser som är tillgängliga i olika mappar eller som matchar ett gemensamt villkor är det möjligt att [uppdatera metadata satsvis efter sökning](search-assets.md#metadataupdates).

## Redigera metadataegenskaper för flera resurser {#editing-metadata-properties-of-multiple-assets}

1. Navigera till platsen för de resurser som du vill redigera i användargränssnittet Resurser.
1. Markera de resurser som du vill redigera gemensamma egenskaper för.
1. Tryck/klicka på ikonen **[!UICONTROL Egenskaper]** i verktygsfältet för att öppna egenskapssidan för de valda resurserna.

   >[!NOTE]
   >
   >När du väljer flera resurser markeras det lägsta gemensamma överordnade formuläret för resurserna. Egenskapssidan visar alltså bara metadatafält som är gemensamma för egenskapssidorna för alla enskilda resurser.

1. Ändra metadataegenskaperna för markerade resurser på de olika flikarna.
1. Om du vill visa metadataredigeraren för en viss resurs avmarkerar du återstående resurser i listan. Metadataredigeringsfälten fylls i med metadata för den aktuella resursen.

   >[!NOTE]
   >
   >* På egenskapssidan kan du ta bort resurser från resurslistan genom att avmarkera dem. Resurslistan har alla resurser markerade som standard. Metadata för resurser som du tar bort från listan uppdateras inte.
   >* Överst i resurslistan markerar du kryssrutan nära **[!UICONTROL Titel]** för att växla mellan att markera resurserna och rensa listan.


1. Om du vill välja ett annat metadataram för resurserna trycker/klickar du på **[!UICONTROL inställningsikonen]** i verktygsfältet och väljer önskat schema.
1. Spara ändringarna.
1. Om du vill lägga till nya metadata med befintliga metadata i fält som innehåller flera värden väljer du **[!UICONTROL Lägg till läge]**. Om du inte markerar det här alternativet ersätter de nya metadata som finns i fälten. Tryck/klicka på **[!UICONTROL Skicka]**.

   >[!CAUTION]
   >
   >För fält med ett värde läggs de nya metadata inte till det befintliga värdet i fältet, även om du väljer **[!UICONTROL Lägg till läge]**.

## Redigera metadataegenskaper för flera samlingar {#editing-metadata-properties-of-multiple-collections}

1. Välj de samlingar du vill redigera i konsolen Samlingar.
1. Tryck/klicka på **[!UICONTROL Egenskaper]** i verktygsfältet för att öppna egenskapssidan för de valda samlingarna.
1. Ändra metadataegenskaperna för markerade samlingar under de olika flikarna.

   >[!NOTE]
   >
   >De metadata som du lägger till för de valda samlingarna skriver över tidigare metadata för dessa samlingar, med undantag för taggar. Alla taggar som du lägger till i fältet **[!UICONTROL Taggar]** läggs till i den befintliga listan med taggar i metadata.

1. Om du vill visa metadataegenskaperna för en viss samling avmarkerar du de återstående samlingarna i samlingslistan. Metadataredigeringsfälten fylls i med metadata för den aktuella samlingen.

   >[!NOTE]
   >
   >* På sidan med samlingsegenskaper kan du ta bort samlingar från listan med samlingar genom att avmarkera dem. I samlingslistan är alla samlingar markerade som standard. Metadata för samlingar som du tar bort uppdateras inte.
   >* Överst i listan markerar du kryssrutan vid **[!UICONTROL Titel]** för att växla mellan att markera samlingarna och rensa listan.


1. Spara ändringarna.

## Konfigurera gräns för uppdatering av massmetadata {#configlimit}

För att förhindra DOS-liknande situationer begränsar AEM antalet parametrar som stöds i en Sling-begäran. När du uppdaterar metadata för många resurser på en gång kan du nå gränsen och metadata uppdateras inte för fler resurser. AEM genererar följande varning i loggarna:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

Om du vill ändra gränsen öppnar du Webbkonsol ( **[!UICONTROL Verktyg]** > **[!UICONTROL Åtgärder]** > **[!UICONTROL Webbkonsol]**) och ändrar värdet för **[!UICONTROL maximalt antal POST-parametrar]** i konfigurationen för **[!UICONTROL APache Sling Request Parameter Handling]** OSGi.
