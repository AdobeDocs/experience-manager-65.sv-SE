---
title: Redigera Launches
description: När en startsida har skapats för en sida (eller en uppsättning sidor) kan du redigera innehållet i startkopian av sidorna.
uuid: 3a310eeb-553d-4d2b-98b5-c5bc523b2aca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 666b967a-e94b-4f94-a676-00adf150580f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 21776f42-cd81-459d-b4b9-1d92e0aec164
source-git-commit: 71b3f7c6ad2c7712762a29518de6cf0639081cb7
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 2%

---

# Redigera Launches{#editing-launches}

## Redigera startsidor {#editing-launch-pages}

När en startsida har skapats för en sida (eller en uppsättning sidor) kan du redigera innehållet i startkopian av sidorna.

1. Öppna sidan för redigering.
1. I Sidekick väljer du **Versioner** och sedan expandera **Startar** grupp. Titeln på den programstart som redigeras använder ett fetstilt teckensnitt.

   ![chlimage_1-13](assets/chlimage_1-13.jpeg)

1. Välj den start du vill arbeta med och klicka sedan på **Byt**.
1. Börja redigera.

   >[!NOTE]
   >
   >Du kan använda **Sida** flik för att utföra åtgärder som **Skapa underordnad sida**, bland annat.

## Redigera en startkonfiguration {#editing-a-launch-configuration}

När du har skapat en programstart kan du ändra startnamnet och startdatumet. Du kan också ange en bild som ska associeras med starten.

1. Öppna administrationssidan för starter ([http://localhost:4502/libs/launches/content/admin.html](http://localhost:4502/libs/launches/content/admin.html)).

1. Välj önskad start och klicka på **Redigera** för att öppna dialogrutan:

   * I **Allmänt** kan du redigera:

      * **Titel**
      * **Live-datum**: detta motsvarar startdatumet
      * **Produktionsklar**

     Se [Startar - ordningen för händelser](/help/sites-authoring/launches.md#launches-the-order-of-events) för information om syftet med och interaktionen med dessa fält.

   * I **Bild** kan du överföra en bildfil.

1. Klicka **Spara**.

## Identifiera startstatus för en sida {#discovering-the-launch-status-of-a-page}

När du redigerar en startsida visas information om startsidan längst ned i **Versioner** Sidekick:

* Startnamnet.
* Tiden sedan den senaste ändringen.
* Den användare som utförde den senaste ändringen.
* Status för **Produktionsklar** flag (orange=not set; green=set).

![chlimage_1-186](assets/chlimage_1-186.png)
