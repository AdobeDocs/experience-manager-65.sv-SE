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

---


# Skapa formulärdatamodell{#create-form-data-model}

![](do-not-localize/data-integeration.png)

AEM Forms dataintegrering ger ett intuitivt användargränssnitt för att skapa och arbeta med formulärdatamodeller. En formulärdatamodell bygger på datakällor för datautbyte. Du kan dock skapa en formulärdatamodell med eller utan en datakälla. Det finns två sätt att skapa en utifrån datamodell beroende på om du har konfigurerat datakällor:

* **Använda förkonfigurerade datakällor**: Om du har konfigurerat datakällor enligt beskrivningen i [Konfigurera datakällor](../../forms/using/configure-data-sources.md)kan du välja dem när du skapar en formulärdatamodell. Den hämtar alla datamodellsobjekt, egenskaper och tjänster från de valda datakällorna som är tillgängliga för användning i formulärdatamodellen.

* **Utan datakällor**: Om du inte har konfigurerat datakällor för formulärdatamodellen kan du fortfarande skapa den utan datakällor. Du kan använda formulärdatamodellen för att skapa adaptiva formulär och interaktiv kommunikation och testa dem med exempeldata. När datakällor är tillgängliga kan du binda formulärdatamodellen till datakällor, som automatiskt återspeglas i de tillhörande adaptiva formulären och interaktiva kommunikationerna.

>[!NOTE]
>
>Du måste vara medlem i både **fdm-author** - och **forms-user** -grupper för att kunna skapa och arbeta med formulärdatamodellen. Kontakta din AEM-administratör om du vill bli medlem i grupperna.

## Skapa formulärdatamodell {#data-sources}

Kontrollera att du har konfigurerat de datakällor som du vill använda i formulärdatamodellen enligt beskrivningen i [Konfigurera datakällor](../../forms/using/configure-data-sources.md). Så här skapar du en formulärdatamodell som baseras på konfigurerade datakällor:

1. I AEM-författarinstansen går du till **[!UICONTROL Formulär > Dataintegreringar]**.
1. Tryck på **[!UICONTROL Skapa > Formulärdatamodell]**.
1. I dialogrutan Skapa formulärdatamodell:

   * Ange ett namn för formulärdatamodellen.
   * (**Valfritt**) Ange rubrik, beskrivning och taggar för formulärdatamodellen.
   * (**Valfritt och endast tillämpligt om datakällor har konfigurerats**) Tryck på bockikonen bredvid fältet **[!UICONTROL Datakällkonfiguration]** och välj den konfigurationsnod där molntjänster för de datakällor som du vill använda finns. Den begränsar listan med datakällor som är tillgängliga för val på nästa sida till de som är tillgängliga i den valda konfigurationsnoden. Alla datakällor i JDBC-databaser och AEM-användarprofiler listas som standard. Om du inte väljer en konfigurationsnod visas datakällor från alla konfigurationsnoder.
   Tryck på **[!UICONTROL Nästa]**.

1. (**Gäller endast om datakällor har konfigurerats**) Skärmen **[!UICONTROL Välj datakälla]** visar tillgängliga datakällor, om det finns några. Välj datakällor som du vill använda i formulärdatamodellen.
1. Tryck på **[!UICONTROL Skapa]** och tryck på **[!UICONTROL Öppna]** i bekräftelsedialogrutan för att öppna formulärdatamodellens redigerare.

Låt oss granska de olika komponenterna i användargränssnittet för formulärdatamodellsredigeraren.

![En formulärdatamodell med tre datakällor - en RESTful-tjänst, en AEM-användarprofil och ett RDBMS](assets/fdm-ui.png)

**S. Datakällor** Visar datakällor i en formulärdatamodell. Expandera en datakälla om du vill visa dess datamodellsobjekt och -tjänster.

**B. Uppdatera definitioner** för datakälla Hämtar alla ändringar i datakälldefinitioner från konfigurerade datakällor och uppdaterar dem på fliken Datakällor i formulärdatamodellens redigerare.

**C. Modellinnehållsområde** där tillagda datamodellsobjekt visas.

**D. Området Services** Content där tillagda datakällåtgärder eller -tjänster visas.

**E. Verktyg i verktygsfältet** för att arbeta med formulärdatamodell. I verktygsfältet visas fler alternativ beroende på vilket objekt som är markerat i formulärdatamodellen.

**F. Lägg till markerade** Lägger till markerade datamodellsobjekt och tjänster i formulärdatamodellen.

Mer information om formulärdatamodellredigerare och hur du kan arbeta med den för att redigera och konfigurera formulärdatamodellen finns i [Arbeta med formulärdatamodell](../../forms/using/work-with-form-data-model.md).

## Uppdatera datakällor {#update}

Gör följande för att lägga till eller uppdatera datakällor till en befintlig formulärdatamodell.

1. Gå till **[!UICONTROL Formulär > Dataintegrering]**, välj den formulärdatamodell i vilken du vill lägga till eller uppdatera datakällor och tryck sedan på **[!UICONTROL Egenskaper]**.
1. Gå till fliken **[!UICONTROL Uppdatera källa]** i egenskaperna för formulärdatamodellen.

   På fliken Uppdateringskälla:

   * Tryck på bläddringsikonen i fältet **[!UICONTROL Kontextmedveten konfiguration]** och välj en konfigurationsnod där molnkonfigurationen för den datakälla som du vill lägga till finns. Om du inte väljer en nod visas molnkonfigurationer som bara finns i `global` noden när du trycker på **[!UICONTROL Lägg till källor]**.

   * Om du vill lägga till en ny datakälla trycker du på **[!UICONTROL Lägg till källor]** och väljer de datakällor som ska läggas till i formulärdatamodellen. Alla datakällor som är konfigurerade i `global` och den valda konfigurationsnoden (om det finns någon) visas.

   * Om du vill ersätta en befintlig datakälla med en annan datakälla av samma typ trycker du på ikonen **[!UICONTROL Redigera]** för datakällan och väljer i listan över tillgängliga datakällor.
   * Om du vill ta bort en befintlig datakälla trycker du på ikonen **[!UICONTROL Ta bort]** för datakällan. Ikonen Ta bort är inaktiverad om ett datamodellsobjekt i datakällan läggs till i formulärdatamodellen.
   ![fdm-properties](assets/fdm-properties.png)

1. Tryck på **[!UICONTROL Spara och stäng]** för att spara uppdateringarna.

>[!NOTE]
>
>När du lägger till nya datakällor eller uppdaterar befintliga datakällor i en formulärdatamodell måste du uppdatera bindningsreferenserna, beroende på vad som är lämpligt, i anpassningsbara formulär och interaktiv kommunikation som använder den uppdaterade formulärdatamodellen.

## Nästa steg {#next-steps}

Nu har du en formulärdatamodell med nya datakällor. Därefter kan du redigera formulärdatamodellen för att lägga till och konfigurera datamodellsobjekt och -tjänster, lägga till associationer mellan datamodellsobjekt, redigera egenskaper, lägga till anpassade datamodellsobjekt och egenskaper, generera exempeldata osv.

Mer information finns i [Arbeta med formulärdatamodell](../../forms/using/work-with-form-data-model.md).
