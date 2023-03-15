---
title: Anpassa flikar för en uppgift
seo-title: Customizing tabs for a task
description: Anpassa namnen på flikarna för dina uppgifter på arbetsytan i LiveCycle AEM Forms.
seo-description: How-to customize the names of the tabs for your tasks, in LiveCycle AEM Forms workspace.
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# Anpassa flikar för en uppgift {#customizing-tabs-for-a-task}

Du kan anpassa tabbnamn för `Start Process` i `Start Process` Användarvy och `Task Details` i `ToDo` Användarvy.

1. Följ [Allmänna steg för anpassning av AEM Forms arbetsyta](/help/forms/using/generic-steps-html-workspace-customization.md).
1. Ändra värdet för `tabname`i `translation.json` -fil.

   Ändra till exempel `/apps/ws/locales/en-US/translation.json` för engelska till följande:

   * Använd följande utdrag från `"startprocess" : {}` -block.

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * Använd följande kodutdrag från `"todo" : {}` -block.

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
