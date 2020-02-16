---
title: Anpassa flikar för en uppgift
seo-title: Anpassa flikar för en uppgift
description: Anpassa flikarnas namn för dina uppgifter på arbetsytan i LiveCycle AEM Forms.
seo-description: Anpassa flikarnas namn för dina uppgifter på arbetsytan i LiveCycle AEM Forms.
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Anpassa flikar för en uppgift {#customizing-tabs-for-a-task}

Du kan anpassa fliknamn för `Start Process` komponenten i `Start Process` användarvyn och för `Task Details` komponenten i `ToDo` användarvyn.

1. Följ de [allmänna stegen för anpassning](/help/forms/using/generic-steps-html-workspace-customization.md)av arbetsytan i AEM Forms.
1. Ändra värdet för `tabname`i `translation.json` filen.

   Ändra till exempel `/apps/ws/locales/en-US/translation.json` för engelska till följande.

   * Använd följande utdrag från blocket för uppgifter som initieras i startprocessen `"startprocess" : {}` .

   ```
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * För uppgifter i Att göra använder du följande kodutdrag från `"todo" : {}` blocket.

   ```
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

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
