---
title: Anpassa sidan med uppgiftsinformation
seo-title: Anpassa sidan med uppgiftsinformation
description: Anpassa informationssidan i AEM Forms arbetsyta för att ändra standardinformationen som visas för en uppgift.
seo-description: Anpassa informationssidan i AEM Forms arbetsyta för att ändra standardinformationen som visas för en uppgift.
uuid: d85fae55-8e66-4595-8560-5485622b6841
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 16e57cf6-aaa1-406d-a6ad-71ec60b15386
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Anpassa informationssidan {#customizing-the-task-details-page}

Sidan med uppgiftsinformation innehåller information om en uppgift och dess processer. Du kan dock anpassa informationssidan för att lägga till eller ta bort information.

Du kan lägga till följande information på informationssidan:

* Information tillgänglig i JSON-objektet för en uppgift (aktivitetsavsnittet i [JSON-objektbeskrivning för AEM Forms-arbetsytan](/help/forms/using/html-workspace-json-object-description.md))
* Information tillgänglig i JSON-objektet för en processinstans (avsnittet Processinstans i [JSON-objektbeskrivning för AEM Forms-arbetsytan](/help/forms/using/html-workspace-json-object-description.md))

Så här anpassar du informationssidan:

1. Följ [Allmänna steg för anpassning av arbetsytan i AEM Forms.](/help/forms/using/generic-steps-html-workspace-customization.md)
1. Om du vill visa ytterligare information lägger du till motsvarande nyckelvärdepar i `translation.json`-filen på `todo`block > `details`block > `app`block > [ `required`block].

   [ `required`blocket] refererar till tillgängliga block, t.ex. aktivitetsblocket för aktivitetsinformation, processblock för processinformation och aktuellt väntande aktivitetsblock för information om väntande aktiviteter.

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

   Lägg till den nya informationen i `/apps/ws/js/runtime/templates/taskdetails.html`. Till exempel:

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

   Sök och ersätt `text!/lc/libs/ws/js/runtime/templates/taskdetails.html` med `text!/lc/apps/ws/js/runtime/templates/taskdetails.html`.

>[!NOTE]
>
>Om du vill anpassa uppgiftsinformationssidan med uppgifter som skapats på fliken **Starta process** på arbetsytan i AEM Forms lägger du till den nya informationen i `/apps/ws/js/runtime/templates/startprocess.html`.
>
>Om du vill lägga till nya format för informationen som läggs till på informationssidan ändrar du CSS-filen med *Ändringarna i användargränssnittet* i [Anpassa arbetsytan](changing-locale-user-interface.md).
