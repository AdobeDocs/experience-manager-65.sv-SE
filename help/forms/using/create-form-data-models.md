---
title: Skapa formulärdatamodell
seo-title: Skapa formulärdatamodell
description: Lär dig hur du skapar formulärdatamodeller med eller utan konfigurerade datakällor.
seo-description: Lär dig hur du skapar formulärdatamodeller med eller utan konfigurerade datakällor.
uuid: 5a94f733-0c08-41bb-983f-e7d34816d8fb
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: 7c392909-ff84-4411-b44f-16f99dffac54
docset: aem65
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 0%

---


# Skapa formulärdatamodell{#create-form-data-model}

![](do-not-localize/data-integeration.png)

AEM Forms dataintegrering ger ett intuitivt användargränssnitt för att skapa och arbeta med formulärdatamodeller. En formulärdatamodell bygger på datakällor för datautbyte. Du kan dock skapa en formulärdatamodell med eller utan en datakälla. Det finns två sätt att skapa en utifrån datamodell beroende på om du har konfigurerat datakällor:

* **Använda förkonfigurerade datakällor**: Om du har konfigurerat datakällor enligt beskrivningen i  [Konfigurera datakällor](../../forms/using/configure-data-sources.md) kan du välja dem när du skapar en formulärdatamodell. Den hämtar alla datamodellsobjekt, egenskaper och tjänster från de valda datakällorna som är tillgängliga för användning i formulärdatamodellen.

* **Utan datakällor**: Om du inte har konfigurerat datakällor för formulärdatamodellen kan du fortfarande skapa den utan datakällor. Du kan använda formulärdatamodellen för att skapa adaptiva formulär och interaktiv kommunikation och testa dem med exempeldata. När datakällor är tillgängliga kan du binda formulärdatamodellen till datakällor, som automatiskt återspeglas i de tillhörande adaptiva formulären och interaktiva kommunikationerna.

>[!NOTE]
>
>Du måste vara medlem i båda grupperna **fdm-author** och **forms-user** för att kunna skapa och arbeta med formulärdatamodellen. Kontakta AEM om du vill bli medlem i grupperna.

## Skapa formulärdatamodell {#data-sources}

Kontrollera att du har konfigurerat de datakällor som du vill använda i formulärdatamodellen enligt beskrivningen i [Konfigurera datakällor](../../forms/using/configure-data-sources.md). Så här skapar du en formulärdatamodell som baseras på konfigurerade datakällor:

1. I AEM författarinstans går du till **[!UICONTROL Forms > Data Integrations]**.
1. Tryck på **[!UICONTROL Create > Form Data Model]**.
1. I dialogrutan Skapa formulärdatamodell:

   * Ange ett namn för formulärdatamodellen.
   * (**Valfritt**) Ange rubrik, beskrivning och taggar för formulärdatamodellen.
   * (**Valfritt och endast tillämpligt om datakällor har konfigurerats**) Tryck på bockikonen bredvid fältet **[!UICONTROL Data Source Configuration]** och välj konfigurationsnoden där molntjänster för de datakällor som du vill använda finns. Den begränsar listan med datakällor som är tillgängliga för val på nästa sida till de som är tillgängliga i den valda konfigurationsnoden. Alla JDBC-databaser och AEM datakällor för användarprofiler listas som standard. Om du inte väljer en konfigurationsnod visas datakällor från alla konfigurationsnoder.

   Tryck på **[!UICONTROL Next]**.

1. (**Gäller endast om datakällor har konfigurerats**) Skärmen **[!UICONTROL Select Datasource]** visar tillgängliga datakällor, om det finns några. Välj datakällor som du vill använda i formulärdatamodellen.
1. Tryck på **[!UICONTROL Create]** och tryck på **[!UICONTROL Open]** i bekräftelsedialogrutan för att öppna formulärdatamodellredigeraren.

Låt oss granska de olika komponenterna i användargränssnittet för formulärdatamodellsredigeraren.

![En formulärdatamodell med tre datakällor - en RESTful-tjänst, AEM användarprofil och ett RDBMS](assets/fdm-ui.png)

**S. DatakällorVisar** datakällor i en formulärdatamodell. Expandera en datakälla om du vill visa dess datamodellsobjekt och -tjänster.

**B. Uppdatera** definitioner för datakällaHämtar alla ändringar i definitioner för datakällor från konfigurerade datakällor och uppdaterar dem på fliken Datakällor i formulärdatamodellens redigerare.

**C.** Modellinnehållsområdet där datamodellsobjekt som lagts till visas.

**D. TjänsterInnehållsområde** där tillagda datakällåtgärder eller -tjänster visas.

**E.** VerktygsfältVerktyg för att arbeta med formulärdatamodell. I verktygsfältet visas fler alternativ beroende på vilket objekt som är markerat i formulärdatamodellen.

**F. Lägg till** markeradeLägger till markerade datamodellsobjekt och tjänster i formulärdatamodellen.

Mer information om redigerare för formulärdatamodell och hur du kan arbeta med den för att redigera och konfigurera formulärdatamodell finns i [Arbeta med formulärdatamodell](../../forms/using/work-with-form-data-model.md).

## Uppdatera datakällor {#update}

Gör följande för att lägga till eller uppdatera datakällor till en befintlig formulärdatamodell.

1. Gå till **[!UICONTROL Forms > Data Integrations]**, välj den formulärdatamodell i vilken du vill lägga till eller uppdatera datakällor och tryck på **[!UICONTROL Properties]**.
1. Gå till fliken **[!UICONTROL Update Source]** i egenskaperna för formulärdatamodellen.

   På fliken Uppdateringskälla:

   * Tryck på bläddringsikonen i fältet **[!UICONTROL Context-Aware Configuration]** och välj en konfigurationsnod där molnkonfigurationen för den datakälla som du vill lägga till finns. Om du inte väljer en nod visas molnkonfigurationer som bara finns i `global`-noden när du trycker på **[!UICONTROL Add Sources]**.

   * Om du vill lägga till en ny datakälla trycker du på **[!UICONTROL Add Sources]** och väljer de datakällor som ska läggas till i formulärdatamodellen. Alla datakällor som konfigurerats i `global` och den valda konfigurationsnoden (om det finns någon) visas.

   * Om du vill ersätta en befintlig datakälla med en annan datakälla av samma typ trycker du på ikonen **[!UICONTROL Edit]** för datakällan och väljer i listan över tillgängliga datakällor.
   * Om du vill ta bort en befintlig datakälla trycker du på ikonen **[!UICONTROL Delete]** för datakällan. Ikonen Ta bort är inaktiverad om ett datamodellsobjekt i datakällan läggs till i formulärdatamodellen.

   ![fdm-properties](assets/fdm-properties.png)

1. Tryck på **[!UICONTROL Save & Close]** för att spara uppdateringarna.

>[!NOTE]
>
>När du lägger till nya datakällor eller uppdaterar befintliga datakällor i en formulärdatamodell måste du uppdatera bindningsreferenserna, beroende på vad som är lämpligt, i anpassningsbara formulär och interaktiv kommunikation som använder den uppdaterade formulärdatamodellen.

## Nästa steg {#next-steps}

Nu har du en formulärdatamodell med nya datakällor. Därefter kan du redigera formulärdatamodellen för att lägga till och konfigurera datamodellsobjekt och -tjänster, lägga till associationer mellan datamodellsobjekt, redigera egenskaper, lägga till anpassade datamodellsobjekt och egenskaper, generera exempeldata osv.

Mer information finns i [Arbeta med formulärdatamodell](../../forms/using/work-with-form-data-model.md).
