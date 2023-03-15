---
title: Använda arbetsflöden på sidor
seo-title: Applying Workflows to Pages
description: Arbetsflödena kan startas antingen från webbplatskonsolen eller från Sidekick när du redigerar en sida.
seo-description: Workflows can be started from either the Websites console or, when editing a page, from Sidekick.
uuid: 55f6f1d7-da54-4732-b9ff-b7479622db51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 22712b73-90f2-4329-b32f-dbb7ce802d1d
exl-id: d8b604c5-a6da-47c4-9422-b519e224c7ca
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 11%

---

# Använda arbetsflöden på sidor{#applying-workflows-to-pages}

När du använder arbetsflödet anger du följande information:

* Det arbetsflöde som ska användas.

   Du kan använda vilket arbetsflöde som helst (som du fått tillgång till av AEM-administratören).
* Valfritt:

   * En kommentar som ger information om varför du startade arbetsflödet.
   * En titel som hjälper till att identifiera arbetsflödesinstansen i en användares inkorg.

>[!NOTE]
>
>AEM kan starta arbetsflöden med [flera andra metoder](/help/sites-administering/workflows-starting.md).

## Använda arbetsflöden {#applying-workflows}

Arbetsflödena kan startas antingen från webbplatskonsolen eller från Sidekick när du redigerar en sida.

The **Status** kolumn i **Webbplatser** konsolen anger om ett arbetsflöde har tillämpats på en sida:

![arbetsflödesstatus](assets/workflowstatus.png)

### Starta ett arbetsflöde från webbplatskonsolen {#starting-a-workflow-from-the-websites-console}

1. Öppna webbplatskonsolen. ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin))
1. I trädet Webbplatser väljer du den överordnade sidan till sidan som du vill använda arbetsflödet på.
1. Markera sidan i sidlistan och klicka sedan på Arbetsflöde.
1. Välj arbetsflödet som ska användas i dialogrutan Starta arbetsflöde. Du kan även ange en kommentar och en titel. Klicka sedan på Start.

### Starta ett arbetsflöde med Sidespark {#starting-a-workflow-using-sidekick}

1. Öppna webbplatskonsolen.
1. Öppna önskad sida.
1. Välj fliken Arbetsflöde i Spark.
1. Expandera **Arbetsflöde** dialogruta där du kan välja **Arbetsflöde** och ange **Titel för arbetsflöde** och **Kommentar**.

   ![arbetsflödenstartsidespark](assets/workflowstartsidekick.png)

1. Klicka **Starta arbetsflöde** om du vill starta en ny arbetsflödesinstans med de egenskaper som du har konfigurerat och den aktuella sidan som nyttolast. Nu körs arbetsflödet.
