---
title: Anpassa bilder som används i flödesåtgärder
seo-title: Anpassa bilder som används i flödesåtgärder
description: Hur man anpassar bilderna som används i vägåtgärder på arbetsytan i LiveCycle AEM Forms.
seo-description: Hur man anpassar bilderna som används i vägåtgärder på arbetsytan i LiveCycle AEM Forms.
uuid: 42608376-587e-4b57-a9d5-8f9ebd981426
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 10158c13-47b4-43e3-ac47-690f3cbab158
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Anpassa bilder som används i flödesåtgärder {#customize-images-used-in-route-actions}

Om du vill anpassa bilderna som används i vägåtgärder utför du stegen som beskrivs i [Allmänna steg för anpassning](/help/forms/using/generic-steps-html-workspace-customization.md) , följt av stegen som beskrivs i den här artikeln.

## Bilder för vägåtgärder {#images-for-route-actions}

1. Lägg till formaten som definierar bilder i CSS på följande plats för de nya vägåtgärderna:

   `/apps/ws/css/newStyle.css`

   Till exempel: Lägg till ett nytt format `myStyle1`som kallas nedan och överför bildfilen `myStyleIcon1.png` till mappen `/apps/ws/image`s med en WebDAV-klient.

   >[!NOTE]
   >
   >Mer information om WebDAV-åtkomst finns på [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

   >[!NOTE]
   >
   >Använd formatnamnet som namn på flödesåtgärden.

   ```css
   .myStyle1{
   
           background-image: url('../images/myStyleIcon1.png');
   
       }
   ```

## Åtgärdspopup för uppgiftslisteåtgärd {#task-list-task-action-popup}

1. Skapa ett åtgärdsfönster för uppgiftslistan, se [Skapa kod](/help/forms/using/introduction-customizing-html-workspace.md#main-pars-heading-3)för arbetsytan i AEM Forms. Dev-paketet måste användas.

1. Kopiera `/libs/ws/js/runtime/templates/task.html` till `/apps/ws/js/runtime/templates/task.html`.

1. Om namnet på CSS-formatet är detsamma som namnet på vägåtgärden som kommer från servern ändrar du följande kod i `/apps/ws/js/runtime/templates/task.html`:

   ```
   <%if(routeList == null){%>
               <li>
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li>
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
               </li>
               <%}%>
               <%}%>
   
   To
   
   <%if(routeList == null){%>
               <li class="<%= availableCommands.directCommands[0]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li class="<%= availableCommands.directCommands[i]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
               </li>
               <%}%>
               <%}%>
   ```

1. Om namnet på CSS-formatet skiljer sig från namnet på vägåtgärden som kommer från servern ändrar du följande kod i `/apps/ws/js/runtime/templates/task.html`. Den lägger till en hög med serverletsvillkoren för att mappa formatet med flödesåtgärdens namn. `if-else`

```
<%if(routeList == null){%>
            <li>
                <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
            </li>
            <%}else{%>
            <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
            <li>
                <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
            </li>
            <%}%>
            <%}%>

To

<%if(routeList == null){%>
            <li class="<%= availableCommands.directCommands[0]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0]+'.value')%>">
                <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
            </li>
            <%}else{%>
            <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
                <%if(availableCommands.directCommands[i].equals("myAction1")){%>
                     <li class="myStyle1" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                         <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                     </li>
                <%}else if(availableCommands.directCommands[i].equals("myAction2")){%>
                     <li class="myStyle2" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                         <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                     </li>
                <%}%>
            <%}%>
            <%}%>
```

## Åtgärdsfönster för aktivitetsåtgärd för aktivitetsinformation {#task-details-task-action-popup}

1. Kopiera `/libs/ws/js/runtime/templates/taskdetails.html` till `/apps/ws/js/runtime/templates/taskdetails.html`.

1. Om namnet på CSS-formatet är detsamma som namnet på vägåtgärden som kommer från servern ändrar du följande kod i `/apps/ws/js/runtime/templates/taskdetails.html`:

   ```
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                           </li>
                       <%}%>
   
   To
   
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                       <%}%>
   ```

1. Om namnet på CSS-formatet skiljer sig från namnet på vägåtgärden som kommer från servern ändrar du följande kod i `/apps/ws/js/runtime/templates/taskdetails.html`. Den lägger till en hög med `if-else` serverletvillkor för att mappa formatet med vägåtgärdens namn.

   ```
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                           </li>
                       <%}%>
   
   To
   
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                   <%if(availableCommands.directCommands[i].equals("myAction1")){%>
                       <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="myStyle1" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                   <%}else if(availableCommands.directCommands[i].equals("myAction2")){%>
                       <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="myStyle2" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                   <%}%>
               <%}%>
   ```

1. Öppna `/apps/ws/js/registry.js` för redigering och sök efter följande text:
   `"text!/lc/libs/ws/js/runtime/templates/taskdetails.html"`

1. Ersätt texten med följande:
   `"text!/lc/apps/ws/js/runtime/templates/taskdetails.html"`

**[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)**
