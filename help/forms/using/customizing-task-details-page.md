---
title: Anpassa sidan med uppgiftsinformation
seo-title: Anpassa sidan med uppgiftsinformation
description: Anpassa uppgiftsinformationssidan på arbetsytan i AEM Forms för att ändra standardinformationen som visas för en uppgift.
seo-description: Anpassa uppgiftsinformationssidan på arbetsytan i AEM Forms för att ändra standardinformationen som visas för en uppgift.
uuid: d85fae55-8e66-4595-8560-5485622b6841
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 16e57cf6-aaa1-406d-a6ad-71ec60b15386
translation-type: tm+mt
source-git-commit: 21623c615ebe69226cfaf84baf4cfb1717b449f4

---


# Anpassa sidan med uppgiftsinformation {#customizing-the-task-details-page}

Sidan med uppgiftsinformation innehåller information om en uppgift och dess processer. Du kan dock anpassa informationssidan för att lägga till eller ta bort information.

Du kan lägga till följande information på informationssidan:

* Information som är tillgänglig i JSON-objektet för en uppgift (aktivitetsavsnittet i JSON-objektbeskrivningen [för](/help/forms/using/html-workspace-json-object-description.md)AEM Forms-arbetsytan)
* Information tillgänglig i JSON-objektet för en processinstans (Processinstansavsnitt i JSON-objektbeskrivning [för](/help/forms/using/html-workspace-json-object-description.md)AEM Forms-arbetsytan)

Så här anpassar du informationssidan:

1. Följ [allmänna steg för anpassning av arbetsytan i AEM Forms.](/help/forms/using/generic-steps-html-workspace-customization.md)
1. Om du vill visa ytterligare information lägger du till motsvarande nyckelvärdepar i `translation.json` filen vid `todo`block > `details`block > `app`block > [ block `required`].

   Det här [`required`blocket] refererar till tillgängliga block, t.ex. uppgiftsblocket, processblock för processinformation och det aktuella väntande uppgiftsblocket för information om väntande uppgifter.

   Om du till exempel vill lägga till information om val av väg krävs på sidan med uppgiftsinformation kan du lägga till följande nyckelvärdepar i åtgärdsblocket:

   ```
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

   Lägg till den nya informationen i `/apps/ws/js/runtime/templates/taskdetails.html`. Exempel:

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
>Om du vill anpassa uppgiftsinformationssidan med uppgifter som skapats på fliken **Starta process** på arbetsytan i AEM Forms lägger du till den nya informationen `/apps/ws/js/runtime/templates/startprocess.html`.
>
>Om du vill lägga till nya format för informationen som läggs till på informationssidan, ändrar du CSS-filen med hjälp av ändringsavsnittet *för* användargränssnittet i [Anpassa](/help/forms/using/changing-locale-user-interface.md#main-pars-header-3)arbetsytan.

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
