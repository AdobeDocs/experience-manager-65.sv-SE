---
title: Rensa poster från Job Manager-databasen
seo-title: Rensa poster från Job Manager-databasen
description: Stora processdata kan ge lägre prestanda för AEM-formulär. Det är god praxis att rensa processdata när det inte längre behövs några poster.
seo-description: Stora processdata kan ge lägre prestanda för AEM-formulär. Det är god praxis att rensa processdata när det inte längre behövs några poster.
uuid: cf214498-36e9-4dcc-b4d4-e7c46f80dbab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 69a406f2-4fa8-40bb-b671-7b0f5b6a2c4c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Rensa poster från Job Manager-databasen {#purge-records-from-the-job-manager-database}

Processdata som genereras när en långvarig process anropas kan bli för stora, vilket ger lägre prestanda för AEM-formulär och kräver onödigt diskutrymme. Det är god praxis att rensa processdata när det inte längre behövs några poster.

Du kan använda administrationskonsolen för att rensa bort inaktuella poster en gång eller för att schemalägga regelbundna automatiska rensningar. Andra metoder för att rensa inaktuella poster beskrivs i [Rensa processdata](/help/forms/using/admin-help/purging-process-data.md#purging-process-data).

**Gå till sidan Schemaläggaren för jobbrensning**

1. Klicka på Hälsoövervakning i det övre högra hörnet på sidan i administrationskonsolen.
1. Klicka på fliken Schemaläggaren för jobbrensning.

Information om eventuella schemalagda rensningar visas i rutan Information om schemaläggaren för jobbtömning.

>[!NOTE]
>
>Om du klickar på Stoppa schemaläggare avbryts alla rensningar som är schemalagda i framtiden, men det går inte att stoppa ett rensningsjobb som redan pågår.

**Schemalägg en engångsrensning**

1. Välj Endast en gång.
1. I området Töm slutförda poster anger du antalet dagar eller veckor efter vilka en post anses föråldrad och klar för rensning.

   >[!NOTE]
   >
   >Poster som hör till processer som inte har slutförts rensas inte, även om de är äldre än den angivna åldern.

1. Ange när rensningen ska ske. Markera kryssrutan Använd aktuellt datum och tid eller avmarkera kryssrutan och klicka på ikonerna för kalender och klocka för att ange datum och tid då rensningen ska utföras.

   >[!NOTE]
   >
   >Om du anger ett tidigare startdatum och en tidigare starttid inträffar rensningen omedelbart när du klickar på Starta schemaläggare.

1. Klicka på Starta schemaläggare. Tidigare schemalagda schemaläggningsinställningar ersätts med de nya inställningarna.

**Konfigurera ett automatiskt rensningsschema**

1. Välj Återskapa varje och ange antalet dagar eller veckor mellan tömningar.
1. I området Töm slutförda poster anger du antalet dagar eller veckor efter vilka en post anses föråldrad och klar för rensning. Du kan inte ange värdet till `0`.

   >[!NOTE]
   >
   >Poster som hör till processer som inte har slutförts rensas inte, även om de är äldre än den angivna åldern.

1. Ange när tömningarna ska börja. Markera kryssrutan Använd aktuellt datum och tid eller avmarkera kryssrutan och klicka på ikonerna för kalender och klocka för att ange datum och tid då rensningen ska utföras.

   >[!NOTE]
   >
   >Om du anger ett tidigare startdatum och en tidigare starttid, beräknas det logiska nästa startdatumet baserat på det angivna datumet i AEM-formuläret. Om du till exempel schemalägger att jobbtömningen ska ske varje vecka från den 7 april och nu är den 9 april, sker den första tömningen den 14 april.

1. Klicka på Starta schemaläggare. Tidigare schemalagda schemaläggningsinställningar ersätts med de nya inställningarna.

