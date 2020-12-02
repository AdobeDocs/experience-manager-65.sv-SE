---
title: Anpassa flikar för en uppgift
seo-title: Anpassa flikar för en uppgift
description: Anpassa namnen på flikarna för dina uppgifter på arbetsytan i LiveCycle AEM Forms.
seo-description: Anpassa namnen på flikarna för dina uppgifter på arbetsytan i LiveCycle AEM Forms.
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Anpassa flikar för en uppgift {#customizing-tabs-for-a-task}

Du kan anpassa fliknamn för komponenten `Start Process` i vyn `Start Process` Uber och för komponenten `Task Details` i vyn `ToDo` Uber.

1. Följ de allmänna [stegen för anpassning av arbetsytan i AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md).
1. Ändra värdet för `tabname`i `translation.json`-filen.

   Ändra till exempel `/apps/ws/locales/en-US/translation.json` för engelska till följande.

   * Använd följande utdrag från `"startprocess" : {}`-blocket för uppgifter som initieras i startprocessen.

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * Använd följande kodutdrag från `"todo" : {}`-blocket för uppgifter i Att göra.

   ```json
   "tabname" : {
               "summary" : "Bird's-eye view",
               "history" : "Past",
               "form" : "Form",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Notes"
   }
   ```

   >[!NOTE]
   >
   >Lägg till motsvarande nyckelvärdepar för alla språk som stöds.
