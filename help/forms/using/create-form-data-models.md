---
title: Skapa formulärdatamodell
seo-title: Create form data model
description: Lär dig hur du skapar formulärdatamodeller med eller utan konfigurerade datakällor.
seo-description: Learn how to create form data models with or without configured data sources.
uuid: 5a94f733-0c08-41bb-983f-e7d34816d8fb
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: 7c392909-ff84-4411-b44f-16f99dffac54
docset: aem65
feature: Form Data Model
exl-id: 7f5978c3-6c9f-4ce4-b0fb-660ac1d49244
source-git-commit: e9f64722ba7df0a7f43aaf1005161483e04142f5
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 0%

---

# Skapa formulärdatamodell{#create-form-data-model}

![hero-image](do-not-localize/data-integration.png)

AEM Forms dataintegrering ger ett intuitivt användargränssnitt för att skapa och arbeta med formulärdatamodeller. En formulärdatamodell bygger på datakällor för datautbyte. Du kan dock skapa en formulärdatamodell med eller utan en datakälla. Det finns två sätt att skapa en utifrån datamodell beroende på om du har konfigurerat datakällor:

* **Använda förkonfigurerade datakällor**: Om du har konfigurerat datakällor enligt beskrivningen i [Konfigurera datakällor](../../forms/using/configure-data-sources.md)kan du markera dem när du skapar en formulärdatamodell. Den hämtar alla datamodellsobjekt, egenskaper och tjänster från de valda datakällorna som är tillgängliga för användning i formulärdatamodellen.

* **Utan datakällor**: Om du inte har konfigurerat datakällor för formulärdatamodellen kan du fortfarande skapa den utan datakällor. Du kan använda formulärdatamodellen för att skapa adaptiva formulär och interaktiv kommunikation och testa dem med exempeldata. När datakällor är tillgängliga kan du binda formulärdatamodellen till datakällor, som automatiskt återspeglas i de tillhörande adaptiva formulären och interaktiva kommunikationerna.

>[!NOTE]
>
>Du måste vara medlem i båda **fdm-author** och **formuläranvändare** grupper för att kunna skapa och arbeta med formulärdatamodell. Kontakta AEM om du vill bli medlem i grupperna.

## Skapa formulärdatamodell {#data-sources}

Kontrollera att du har konfigurerat de datakällor som du vill använda i formulärdatamodellen enligt beskrivningen i [Konfigurera datakällor](../../forms/using/configure-data-sources.md). Så här skapar du en formulärdatamodell som baseras på konfigurerade datakällor:

1. I AEM författarinstans går du till **[!UICONTROL Forms > Data Integrations]**.
1. Tryck på **[!UICONTROL Create > Form Data Model]**.
1. I dialogrutan Skapa formulärdatamodell:

   * Ange ett namn för formulärdatamodellen.
   * (**Valfritt**) Ange rubrik, beskrivning och taggar för formulärdatamodellen.
   * (**Valfritt och endast tillämpligt om datakällor har konfigurerats**) Tryck på bockikonen bredvid **[!UICONTROL Data Source Configuration]** och välj konfigurationsnoden där molntjänster för de datakällor som du vill använda finns. Den begränsar listan med datakällor som är tillgängliga för val på nästa sida till de som är tillgängliga i den valda konfigurationsnoden. Alla JDBC-databaser och AEM datakällor för användarprofiler listas som standard. Om du inte väljer en konfigurationsnod visas datakällor från alla konfigurationsnoder.

   Tryck på **[!UICONTROL Next]**.

1. (**Gäller endast om datakällor har konfigurerats**) **[!UICONTROL Select Datasource]** visas tillgängliga datakällor, om det finns några. Välj datakällor som du vill använda i formulärdatamodellen.
1. Tryck **[!UICONTROL Create]** och i bekräftelsedialogrutan trycker du på **[!UICONTROL Open]** för att öppna formulärdatamodellens redigerare.

Låt oss granska de olika komponenterna i användargränssnittet för formulärdatamodellsredigeraren.

![En formulärdatamodell med tre datakällor - en RESTful-tjänst, AEM användarprofil och ett RDBMS](assets/fdm-ui.png)

**S. Datakällor** Visar datakällor i en formulärdatamodell. Expandera en datakälla för att visa dess datamodellsobjekt och tjänster.

**B. Uppdatera definitioner för datakällor** Hämtar alla ändringar i datakälldefinitioner från konfigurerade datakällor och uppdaterar dem på fliken Datakällor i formulärdatamodellens redigerare.

**C. Modell** Innehållsområde där tillagda datamodellsobjekt visas.

**D. Tjänster** Innehållsområde där tillagda datakällåtgärder eller -tjänster visas.

**E. Verktygsfält** Verktyg för att arbeta med formulärdatamodell. I verktygsfältet visas fler alternativ beroende på vilket objekt som är markerat i formulärdatamodellen.

**F. Lägg till markerade** Lägger till markerade datamodellsobjekt och tjänster i formulärdatamodellen.

Mer information om formulärdatamodellredigerare och hur du kan arbeta med den för att redigera och konfigurera formulärdatamodellen finns i [Arbeta med formulärdatamodell](../../forms/using/work-with-form-data-model.md).

## Uppdatera datakällor {#update}

Gör följande för att lägga till eller uppdatera datakällor till en befintlig formulärdatamodell.

1. Gå till **[!UICONTROL Forms > Data Integrations]**, välj den formulärdatamodell i vilken du vill lägga till eller uppdatera datakällor och tryck **[!UICONTROL Properties]**.
1. I egenskaperna för formulärdatamodellen går du till **[!UICONTROL Update Source]** -fliken.

   På fliken Uppdateringskälla:

   * Tryck på bläddringsikonen i dialogrutan **[!UICONTROL Context-Aware Configuration]** och välj en konfigurationsnod där molnkonfigurationen för den datakälla som du vill lägga till finns. Om du inte väljer en nod finns molnkonfigurationer endast i `global` visas när du trycker **[!UICONTROL Add Sources]**.

   * Om du vill lägga till en ny datakälla trycker du **[!UICONTROL Add Sources]** och välj de datakällor som ska läggas till i formulärdatamodellen. Alla datakällor konfigurerade i `global` och den valda konfigurationsnoden (om sådan finns) visas.

   * Om du vill ersätta en befintlig datakälla med en annan datakälla av samma typ trycker du på **[!UICONTROL Edit]** -ikonen för datakällan och välj i listan över tillgängliga datakällor.
   * Om du vill ta bort en befintlig datakälla trycker du på **[!UICONTROL Delete]** -ikon för datakällan. Ikonen Ta bort är inaktiverad om ett datamodellsobjekt i datakällan läggs till i formulärdatamodellen.

   ![fdm-properties](assets/fdm-properties.png)

1. Tryck **[!UICONTROL Save & Close]** för att spara uppdateringarna.

>[!NOTE]
>
>När du lägger till nya datakällor eller uppdaterar befintliga datakällor i en formulärdatamodell måste du uppdatera bindningsreferenserna, beroende på vad som är lämpligt, i anpassningsbara formulär och interaktiv kommunikation som använder den uppdaterade formulärdatamodellen.

## Nästa steg {#next-steps}

Nu har du en formulärdatamodell med nya datakällor. Därefter kan du redigera formulärdatamodellen för att lägga till och konfigurera datamodellsobjekt och -tjänster, lägga till associationer mellan datamodellsobjekt, redigera egenskaper, lägga till anpassade datamodellsobjekt och egenskaper, generera exempeldata osv.

Mer information finns i [Arbeta med formulärdatamodell](../../forms/using/work-with-form-data-model.md).
