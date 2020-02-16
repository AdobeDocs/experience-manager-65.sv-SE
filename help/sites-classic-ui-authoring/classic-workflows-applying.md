---
title: Använda arbetsflöden på sidor
seo-title: Använda arbetsflöden på sidor
description: Arbetsflödena kan startas antingen från webbplatskonsolen eller från Sidekick när du redigerar en sida.
seo-description: Arbetsflödena kan startas antingen från webbplatskonsolen eller från Sidekick när du redigerar en sida.
uuid: 55f6f1d7-da54-4732-b9ff-b7479622db51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 22712b73-90f2-4329-b32f-dbb7ce802d1d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Använda arbetsflöden på sidor{#applying-workflows-to-pages}

När du använder arbetsflödet anger du följande information:

* Arbetsflödet som ska användas.

   Du kan tillämpa vilket arbetsflöde som helst (som du har tillgång till, enligt din AEM-administratörs anvisningar).
* Valfritt:

   * En kommentar som ger information om varför du startade arbetsflödet.
   * En titel som hjälper till att identifiera arbetsflödesinstansen i en användares inkorg.

>[!NOTE]
>
>AEM-administratörer kan starta arbetsflöden med [flera andra metoder](/help/sites-administering/workflows-starting.md).

## Använda arbetsflöden {#applying-workflows}

Arbetsflödena kan startas antingen från webbplatskonsolen eller från Sidekick när du redigerar en sida.

Kolumnen **Status** i konsolen **Webbplatser** anger om ett arbetsflöde har tillämpats på en sida:

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
1. Utöka dialogrutan **Arbetsflöde** så att du kan välja **Arbetsflöde** och eventuellt ange **arbetsflödets titel** och **kommentar**.

   ![arbetsflödenstartsidespark](assets/workflowstartsidekick.png)

1. Klicka på **Starta arbetsflöde** för att starta en ny arbetsflödesinstans med de egenskaper som du har konfigurerat och den aktuella sidan som nyttolast. Nu körs arbetsflödet.

