---
title: Redigeringsövningar
seo-title: Redigeringsövningar
description: När en startsida har skapats för en sida (eller en uppsättning sidor) kan du redigera innehållet i startkopian av sidorna.
seo-description: När en startsida har skapats för en sida (eller en uppsättning sidor) kan du redigera innehållet i startkopian av sidorna.
uuid: 3a310eeb-553d-4d2b-98b5-c5bc523b2aca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 666b967a-e94b-4f94-a676-00adf150580f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Redigeringsövningar{#editing-launches}

## Redigera startsidor {#editing-launch-pages}

När en startsida har skapats för en sida (eller en uppsättning sidor) kan du redigera innehållet i startkopian av sidorna.

1. Öppna sidan för redigering.
1. I Sidekick väljer du fliken **Versionshantering** och expanderar sedan gruppen **Launches** . Titeln på den programstart som redigeras använder ett fet teckensnitt.

   ![chlimage_1-13](assets/chlimage_1-13.jpeg)

1. Välj den start du vill arbeta med och klicka sedan på **Byt**.
1. Börja redigera.

   >[!NOTE]
   >
   >Du kan använda fliken **Sida** i sidokicka för att utföra åtgärder som **Skapa underordnad sida**, bland annat.

## Redigera en startkonfiguration {#editing-a-launch-configuration}

När du har skapat en programstart kan du ändra startnamnet och startdatumet. Du kan också ange en bild som ska associeras med starten.

1. Öppna administrationssidan för starter ([http://localhost:4502/libs/launches/content/admin.html](http://localhost:4502/libs/launches/content/admin.html)).

1. Välj önskad start och klicka på **Redigera** för att öppna dialogrutan:

   * På fliken **Allmänt** kan du redigera:

      * **Titel**
      * **Live-datum**: detta motsvarar startdatumet
      * **Produktionsklar**
      Se [Startar - Ordning för händelser](/help/sites-authoring/launches.md#launches-the-order-of-events) för information om syftet med och interaktionen med dessa fält.

   * På fliken **Bild** kan du överföra en bildfil.


1. Click **Save**.

## Identifiera startstatus för en sida {#discovering-the-launch-status-of-a-page}

När du redigerar en start av en sida visas information om starten längst ned på fliken **Versionshantering** i Sidekick:

* Startnamnet.
* Tiden sedan den senaste ändringen.
* Den användare som utförde den senaste ändringen.
* Status för flaggan **Production Ready** (orange=ej inställd); green=set).

![chlimage_1-186](assets/chlimage_1-186.png)

