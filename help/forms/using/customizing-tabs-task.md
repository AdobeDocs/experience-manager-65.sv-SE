---
title: Anpassa flikar för en uppgift
description: Anpassa namnen på flikarna för dina uppgifter i arbetsytan i LiveCycle AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# Anpassa flikar för en uppgift {#customizing-tabs-for-a-task}

Du kan anpassa tabbnamn för `Start Process` -komponenten i `Start Process` Användarvy och `Task Details` -komponenten i `ToDo` Uber-vy.

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
