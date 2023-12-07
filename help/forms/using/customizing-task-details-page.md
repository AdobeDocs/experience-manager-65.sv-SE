---
title: Anpassa sidan med uppgiftsinformation
description: Anpassa uppgiftsinformationssidan i AEM Forms arbetsyta för att ändra standardinformationen som visas för en uppgift.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 48c24442-22d2-4d1a-9462-0aba78340281
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Anpassa sidan med uppgiftsinformation {#customizing-the-task-details-page}

Sidan med uppgiftsinformation innehåller information om en uppgift och dess processer. Du kan dock anpassa informationssidan för att lägga till eller ta bort information.

Du kan lägga till följande information på informationssidan:

* Information som är tillgänglig i JSON-objektet för en uppgift (Uppgiftsavsnitt i [JSON-objektbeskrivning för arbetsytan i AEM Forms](/help/forms/using/html-workspace-json-object-description.md))
* Information tillgänglig i JSON-objektet för en processinstans (processinstansavsnitt i [JSON-objektbeskrivning för arbetsytan i AEM Forms](/help/forms/using/html-workspace-json-object-description.md))

Så här anpassar du informationssidan:

1. Följ [Allmänna steg för anpassning av AEM Forms arbetsyta.](/help/forms/using/generic-steps-html-workspace-customization.md)
1. Om du vill visa ytterligare information lägger du till motsvarande nyckelvärdepar i `translation.json` fil på `todo`block > `details`block > `app`block > [`required`block].

   The [`required`block] refererar till tillgängliga block, t.ex. uppgiftsblocket för uppgiftsinformation, processblock för processinformation och aktuellt väntande uppgiftsblock för information om väntande uppgifter.

   Om du till exempel vill lägga till information om val av väg krävs på sidan med uppgiftsinformation kan du lägga till följande nyckelvärdepar i åtgärdsblocket:

   ```json
   "todo" : {
       .
       .
       .
       "details" : {
           .
           .
           "task" : {
               .
               .
               "RouteSelectionRequired" : "Route Selection Required"
           }
       }
   }
   ```

   >[!NOTE]
   >
   >Lägg till motsvarande nyckelvärdepar för alla språk som stöds.

1. Kopiera `/libs/ws/js/runtime/templates/taskdetails.html` till `/apps/ws/js/runtime/templates/taskdetails.html`.

   Lägg till ny information i `/apps/ws/js/runtime/templates/taskdetails.html`. Till exempel:

   ```css
   <div class="detailsContainer">
       .
       .
       <ul>
           .
           .
           <li>
               <label for="routeSelectionRequired" title="<%= $.t('todo.details.task.RouteSelectionRequired')%>"><%= $.t('todo.details.task.RouteSelectionRequired')%></label>
               <div>
                   <span id="routeSelectionRequired"><%= isRouteSelectionRequired != null ? isRouteSelectionRequired : ''%></span>
               </div>
           </li>
           .
           .
       </ul>
   </div>
   ```

1. Öppna /apps/ws/js/registry.js för redigering.

   Söka och ersätta `text!/lc/libs/ws/js/runtime/templates/taskdetails.html` med `text!/lc/apps/ws/js/runtime/templates/taskdetails.html`.

>[!NOTE]
>
>Anpassa uppgiftsinformationssidan med uppgifter som skapats i **Starta process** på AEM Forms arbetsyta lägger du till den nya informationen i `/apps/ws/js/runtime/templates/startprocess.html`.
>
>Om du vill lägga till nya format för informationen som lagts till på informationssidan ändrar du CSS-filen med hjälp av *Ändringar i användargränssnittet* avsnitt i [Anpassa arbetsytan](changing-locale-user-interface.md).
