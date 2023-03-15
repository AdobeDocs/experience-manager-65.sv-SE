---
title: Konfigurera synkroniseringsplaneraren
seo-title: Configuring the synchronization scheduler
description: Lär dig hur du migrerar och synkroniserar resurser, konfigurerar schemaläggaren för synkronisering och använder mappar för att ordna resurser.
seo-description: Learn how to migrate and sync assets, configure sync scheduler, and use folders to arrange assets.
uuid: b2c89feb-2947-418a-b343-4c01e453602b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8c8b1998-eab4-4230-b24f-5e96883ba599
docset: aem65
role: Admin
exl-id: 34db1f76-ee40-4612-85da-22041e7560fb
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Konfigurera synkroniseringsplaneraren {#configuring-the-synchronization-scheduler}

Som standard körs synkroniseringsschemaläggaren efter var tredje minut för att synkronisera alla resurser som ändrats och uppdaterats i databasen via LiveCycle Workbench 11. Program som innehåller formulär och resurser visas i AEM Forms användargränssnitt när synkroniseringsprocessen är klar.

## Ändra intervall för synkroniseringsschemaläggaren {#change-interval-of-the-synchronization-scheduler}

Utför följande steg för att ändra intervallet för synkroniseringsplaneraren:

1. Logga in AEM Configuration Manager. URL:en för Configuration Manager är `https://'[server]:[port]'/lc/system/console/configMgr`

1. Leta reda på och öppna **FormsManagerConfiguration** paket.

1. Ange ett nytt värde för **Frekvens för synkroniseringsschemaläggare** alternativ.

   Frekvensenheten är minuter. Om du till exempel vill konfigurera schemaläggaren att köras efter var 60:e minut anger du 60.

## Synkronisera resurser {#synchronizing-assets}

Du kan använda **Synkronisera resurser från databas** om du vill synkronisera resurserna manuellt. Så här synkroniserar du resurserna manuellt:

1. Logga in på AEM Forms. Standardwebbadressen är `https://'[server]:[port]'/lc/aem/forms/`.

   ![AEM Forms användargränssnitt](assets/aem_forms_ui.png)

   **Bild:** *AEM Forms användargränssnitt*

1. Klicka på ![aem6forms_sync](assets/aem6forms_sync.png) i verktygsfältet. Om du inte har några resurser på den senast konfigurerade sökvägen visas dialogrutan enligt nedan. Klicka **Starta** för att initiera synkroniseringen.

   ![Synkroniseringsdialogruta](assets/migrate-and-syncronize.png)

   **Bild:** *Synkroniseringsdialogruta*

## Felsökning av synkroniseringsfel {#troubleshooting-synchronization-error}

Du kan skapa nya program i arbetsflödesdesignern (LiveCycle Workbench).

Om det nyligen skapade programmet och en mapp på /content/dam/formsanddocuments har samma namn visas ett felmeddelande &quot;*Det finns redan en resurs med samma namn som det här programmet på rotnivå.*&quot; är loggad.

Lös konflikten genom att byta namn på programmet och manuellt synkronisera resurserna.

![Konflikter i dialogrutan för resurssynkronisering](assets/sync-conflict.png)

**Bild:** *Konflikter i dialogrutan för resurssynkronisering*
