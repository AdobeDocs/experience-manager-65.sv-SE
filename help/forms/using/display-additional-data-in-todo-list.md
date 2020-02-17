---
title: Visa ytterligare data i ToDo-listan
seo-title: Visa ytterligare data i ToDo-listan
description: Anpassa visningen av Att göra-listan på arbetsytan i LiveCycle AEM Forms så att mer information visas utöver standardinställningen.
seo-description: Anpassa visningen av Att göra-listan på arbetsytan i LiveCycle AEM Forms så att mer information visas utöver standardinställningen.
uuid: 9467c655-dce2-43ce-8e8f-54542fe81279
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: fed3b562-bcc2-4fb7-8fd2-35b1ac621e16
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Visa ytterligare data i ToDo-listan{#displaying-additional-data-in-todo-list}

Som standard visas aktivitetens visningsnamn och beskrivning i listan Att göra på arbetsytan i AEM Forms. Du kan dock lägga till annan information, t.ex. skapandedatum och deadlinedatum. Du kan också lägga till ikoner och ändra visningsformatet.

![En titt på fliken Att göra-uppgifter i HTML-arbetsytan som visar standardkonfigurationen](assets/html-todo-list.png)

I den här artikeln beskrivs stegen för hur du lägger till information för varje uppgift i Att göra-listan.

## Vad kan läggas till {#what-can-be-added}

Du kan lägga till den information som finns i `task.json` som skickas av servern. Informationen kan läggas till som oformaterad text eller formateras med hjälp av format.

Mer information om JSON-objektbeskrivningen finns i [den här](/help/forms/using/html-workspace-json-object-description.md) artikeln.

## Visa information om en uppgift {#displaying-information-on-a-task}

1. Följ de [allmänna stegen för anpassning](../../forms/using/generic-steps-html-workspace-customization.md)av arbetsytan i AEM Forms.
1. Om du vill visa ytterligare information för en uppgift måste motsvarande nyckelvärdepar läggas till i åtgärdsblocket för `translation.json`.

   Ändra t.ex. `/apps/ws/locales/en-US/translation.json` för engelska:

   ```
   "task" : {
           "reminder" : {
               "value" : "Reminder",
               "tooltip" : "This is reminder __reminderCount__, for this task."
           },
           "deadlined" : {
               "value" : "Deadlined",
               "tooltip" : "This task has deadlined"
           },
           "save" : {
               "message" : "Task has been saved successfully"
           },
           "status" : {
               "deadlined" : "Deadlined",
               "created" : "Created",
               "assignedsaved" : "Draft from assigned task",
               "terminated" : "Terminated",
               "assigned" : "Assigned",
               "unknown" : "Unknown",
               "createdsaved" : "Draft from created task",
               "completed" : "Completed"
           },
           "draft" : {
               "value" : "Saved",
               "tooltip" : "This task is marked as a draft"
           },
           "escalated" : {
               "value" : "Escalated",
               "tooltip" : "This task has been escalated"
           },
           "forward" : {
               "value" : "Forwarded",
               "tooltip" : "This task was forwarded"
           },
           "priority" : {
               "highest" : "Highest priority",
               "normal" : "Normal priority",
               "high" : "High priority",
               "low" : "Low priority",
               "lowest" : "Lowest priority"
           },
           "claimed" : {
               "value" : "Claimed",
               "tooltip" : "This task has been claimed"
           },
           "locked" : {
               "value" : "Locked",
               "tooltip" : "This task is locked"
           },
           "consulted" : {
               "value" : "Consulted",
               "tooltip" : "This task has been consulted"
           },
           "returned" : {
               "value" : "Returned",
               "tooltip" : "This task was returned back"
           },
           "multiplesubmitbuttons" : {
               "message" : "The form associated with this task has multiple submit buttons so the Workspace Complete button will be disabled. Click the appropriate button on the form to submit it."
           },
           "nosubmitbutton" : {
               "message" : "The form associated with this task does not appear to have submit buttons. You may need to upgrade your Adobe Reader version to 9.1 or greater and enable the Reader Submit option in your process."
           },
           "icon" : {
               "tooltip" : "open the task __taskName__"
           }
       }
   ```

   >[!NOTE]
   >
   >Lägg till motsvarande nyckelvärdepar för alla språk som stöds.

1. Lägg till exempel till information i åtgärdsblocket:

   ```
   "stepname" : {
               "value" : "Step Name",
               "tooltip" : "This task belongs to __stepName__ step"
   }
   ```

## Definiera CSS för den nya egenskapen {#defining-css-for-the-new-property}

1. Du kan använda format på informationen (egenskapen) som läggs till i en uppgift. För att göra detta måste du lägga till formatinformation för den nya egenskapen som lagts till i `/apps/ws/css/newStyle.css`.

   Lägg till exempel till:

   ```css
   .task .taskProperties .stepname{
       width: 25px;
       background: url(../images/stepname.png) no-repeat; /*-------- Or just reuse background image / image-sprite defined .task .taskProperties span of style.css---------------------*/
       background-position: 0px 0px; /*-------- Dummy values, need to be configured as per user background image / image-sprite ---------------------*/
   }
   ```

## Lägga till post i HTML-mallen {#adding-entry-in-the-html-template}

Slutligen måste du ta med en post i dev-paketet för varje egenskap som du vill lägga till i uppgiften. Om du vill skapa en hänvisar du till Skapa AEM Forms-arbetsytekod.

1. Kopiera `task.html`:

   * from: `/libs/ws/js/runtime/templates/`
   * to: `/apps/ws/js/runtime/templates/`

1. Lägg till den nya informationen i `/apps/ws/js/runtime/templates/task.html`.

   Lägg till under `div class="taskProperties"`:

   ```
   <span class="stepname" alt="<%= $.t('task.stepname.value')%>" title = '<%= $.t("task.stepname.tooltip",{stepName:stepName})%>'/>
   ```

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
