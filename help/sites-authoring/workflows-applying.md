---
title: Tillämpa arbetsflöden på innehållssidor
description: När du redigerar kan du anropa arbetsflöden för att göra något på sidorna; det går även att använda mer än ett arbetsflöde.
uuid: 652d9a23-907d-43ad-9eef-7ab1d07918cd
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 6472dc94-96e0-4286-8f86-d85726cc843c
docset: aem65
exl-id: e00da2b3-046a-4d93-aed0-07dd8c66899f
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 11%

---

# Använda arbetsflöden på sidor{#applying-workflows-to-pages}

När du redigerar kan du anropa arbetsflöden för att göra något på sidorna; det går även att använda mer än ett arbetsflöde.

När du använder arbetsflödet anger du följande information:

* Det arbetsflöde som ska användas.
Du kan använda vilket arbetsflöde som helst (som du fått tillgång till av AEM-administratören).
* Alternativt kan du använda en titel som hjälper till att identifiera arbetsflödesinstansen i en användares inkorg.
* Arbetsflödets nyttolast. detta kan vara en eller flera sidor.

Arbetsflöden kan startas från:

* [Sites-konsolen](#starting-a-workflow-from-the-sites-console).
* [när du redigerar en sida, från Sidinformation](#starting-a-workflow-from-the-page-editor).

>[!NOTE]
>
>Se även:
>
>* [Tillämpa arbetsflöden på DAM-resurser](/help/assets/assets-workflow.md).
>* [Arbeta med projektarbetsflöden](/help/sites-authoring/projects-with-workflows.md).
>


>[!NOTE]
>
>AEM administratörer kan [starta arbetsflöden med flera andra metoder](/help/sites-administering/workflows-starting.md).

## Starta ett arbetsflöde från platskonsolen {#starting-a-workflow-from-the-sites-console}

Du kan starta ett arbetsflöde från:

* [alternativet Skapa i verktygsfältet Platser](#starting-a-workflow-from-the-sites-toolbar).
* [tidslinjespår i webbplatskonsolen](#starting-a-workflow-from-the-timeline).

I båda fallen måste du:

* [Ange arbetsflödesinformation i guiden Skapa arbetsflöde](#specifying-workflow-details-in-the-create-workflow-wizard).

### Starta ett arbetsflöde från verktygsfältet Platser {#starting-a-workflow-from-the-sites-toolbar}

Du kan starta ett arbetsflöde från verktygsfältet i **Webbplatser** konsol:

1. Navigera till och markera önskad sida.

1. Från **Skapa** i verktygsfältet kan du nu välja **Arbetsflöde**.

   ![screen_shot_2019-03-06at121237pm](assets/screen_shot_2019-03-06at121237pm.png)

1. The **Skapa arbetsflöde** guiden hjälper dig [ange arbetsflödesinformation](#specifying-workflow-details-in-the-create-workflow-wizard).

### Starta ett arbetsflöde från tidslinjen {#starting-a-workflow-from-the-timeline}

Från **Tidslinje** du kan starta ett arbetsflöde som ska användas för den valda resursen.

1. [Välj resurs](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources) och öppna [Tidslinje](/help/sites-authoring/basic-handling.md#timeline) (eller öppna tidslinjen och välj sedan resursen).
1. Pilen i kommentarfältet kan användas för att visa **Starta arbetsflöde**:

   ![screen-shot_2019-03-05at120026](assets/screen-shot_2019-03-05at120026.png)

1. The **Skapa arbetsflöde** guiden hjälper dig [ange arbetsflödesinformation](#specifying-workflow-details-in-the-create-workflow-wizard).

### Ange arbetsflödesinformation i guiden Skapa arbetsflöde {#specifying-workflow-details-in-the-create-workflow-wizard}

The **Skapa arbetsflöde** hjälper dig att välja arbetsflöde och ange nödvändig information.

När du har öppnat **Skapa arbetsflöde** guide från antingen

* [alternativet Skapa i verktygsfältet Platser](#starting-a-workflow-from-the-sites-toolbar).
* [tidslinjespår i webbplatskonsolen](#starting-a-workflow-from-the-timeline).

Du kan ange information:

1. I **Egenskaper** de grundläggande alternativen för arbetsflödet definieras:

   * **Arbetsflödesmodell**
   * **Arbetsflödets titel**

      * Du kan ange en titel för den här instansen så att du lättare kan identifiera den i ett senare skede.

   Beroende på arbetsflödesmodellen är följande alternativ också tillgängliga. Dessa gör att det paket som skapas som nyttolast kan behållas när arbetsflödet har slutförts.

   * **Behåll arbetsflödespaket**
   * **Pakettitel**

      * Du kan ange en rubrik för paketet för att underlätta identifieringen.
   >[!NOTE]
   >
   >Alternativet **Behåll arbetsflödespaket** är tillgängligt när arbetsflödet har konfigurerats med stöd för flera resurser och flera resurser har valts.[](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support)

   När det är klart, använd **Nästa** för att fortsätta.

   ![wf-52](assets/wf-52.png)

1. I **Omfång** steg du kan välja:

   * **Lägg till innehåll** för att öppna [sökvägsläsare](/help/sites-authoring/author-environment-tools.md#path-browser) och välja ut ytterligare resurser, i webbläsaren klickar/trycker du **Välj** för att lägga till innehållet i arbetsflödesinstansen.

   * En befintlig resurs som visar ytterligare åtgärder:

      * **Inkludera underordnade** för att ange att underordnade resurser ska inkluderas i arbetsflödet.
En dialogruta öppnas där du kan förfina markeringen enligt:

         * Inkludera endast omedelbara barn.
         * Inkludera endast ändrade sidor.
         * Inkludera endast redan publicerade sidor.

         Alla underordnade objekt läggs till i listan över resurser som arbetsflödet gäller för.

      * **Ta bort markering** för att ta bort resursen från arbetsflödet.

   ![wf-53](assets/wf-53.png)

   >[!NOTE]
   >
   >Om du lägger till ytterligare resurser kan du använda **Bakåt** för att justera inställningen för **Behåll arbetsflödespaket** i steget **Egenskaper**.

1. Använd **Skapa** för att stänga guiden och skapa arbetsflödesinstansen. Ett meddelande visas i webbplatskonsolen.

## Starta ett arbetsflöde från sidredigeraren {#starting-a-workflow-from-the-page-editor}

När du redigerar en sida kan du markera **Sidinformation** i verktygsfältet. Listrutan har ett alternativ **Starta i arbetsflöde**. Då öppnas en dialogruta där du kan ange önskat arbetsflöde, tillsammans med en titel om det behövs:

![wf-54](assets/wf-54.png)
