---
title: Anpassa listan över processinstanser
seo-title: Anpassa listan över processinstanser
description: Anpassa egenskaperna som visas i processinstansen i AEM Forms arbetsyta.
seo-description: Anpassa egenskaperna som visas i processinstansen i AEM Forms arbetsyta.
uuid: 3b55d9b9-7f73-46dd-9eb6-42be218440a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 40d7d43f-ee0a-4e34-ae93-20c9c940f76b
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---


# Anpassa listan över processinstanser {#customizing-the-listing-of-process-instances}

Processinstanslistan visas på fliken Spåra i AEM Forms arbetsyta.

I processinstanslistan visar AEM Forms-arbetsytan några egenskaper för den instansen för varje processinstans. Följande egenskaper är tillgängliga för varje processinstans. Dessa egenskaper lagras som attribut i processinstansens komponentmodell och är tillgängliga för användning i dess vy och mall.

<table>
 <tbody>
  <tr>
   <td><strong>Egenskap</strong></td>
   <td><strong>Kommentarer</strong></td>
  </tr>
  <tr>
   <td>description</td>
   <td>Beskrivning av processinstansen.</td>
  </tr>
  <tr>
   <td>initiator</td>
   <td>Namnet på processinstansens initierare.</td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>ID för initieraren för processinstansen.</td>
  </tr>
  <tr>
   <td>processCompleteTime</td>
   <td>Tidsstämpel när processen har slutförts.</td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>ID för processinstansen.</td>
  </tr>
  <tr>
   <td>processInstanceStatus</td>
   <td>0 = Initierad<br /> 1 = Körning<br /> 2 = Fullständig<br /> 3 = Slutför<br /> 4 = Avbruten<br /> 5 = Avsluta<br /> 6 = Upphävd<br /> 7 = Upphävande<br /> 8 = Upphävande</td>
  </tr>
  <tr>
   <td>processName</td>
   <td>Processens namn.</td>
  </tr>
  <tr>
   <td>processStartTime</td>
   <td>Tidsstämpel när processen startades.</td>
  </tr>
  <tr>
   <td>processVariables</td>
   <td>Array med objekt av processvariabler. Varje processvariabelobjekt innehåller <strong>namn</strong> (namnet på processvariabeln), <strong>värde</strong> (värdet på processvariabeln) och<strong> typ</strong> (typen av processvariabel).</td>
  </tr>
 </tbody>
</table>

**Exempel:**

Utför följande steg för att visa egenskapen `description` för processinstansen i processinstanskortet.

1. Följ de allmänna [stegen för anpassning av arbetsytan i AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md).
1. Gör följande:

   1. Kopiera /libs/ws/js/runtime/templates/processinstance.html till/apps/ws/js/runtime/templates/, om den inte finns. Klicka på **Spara alla**.
   1. Lägg till processbeskrivning div med klass = &#39;processDescription&#39; inprocessinstance.html.

   ```jsp
   <div class="processDescription" title="<%= description%>"><%= description%></div>
   ```

1. Gör följande:

   1. Öppna /apps/ws/js/registry.js för redigering.
   1. Sök och ersätt `text!/lc/libs/ws/js/runtime/templates/processinstance.html`med `text!/lc/`**program**/ws/js/runtime/templates/processinstance.html.

1. Ovanstående ändringar kan kräva en uppdatering av CSS-filen genom att lägga till en post i formatmallen /apps/ws/css/newStyle.css på följande sätt:

   ```css
   .processinstance .processDescription {
    <!--Dummy values, need to be configured by user as per requirement as well as user can add or delete any property depending upon requirement-->
       width : 250px;
       font-size : 11pt;
       padding : 2px;
   }
   ```
