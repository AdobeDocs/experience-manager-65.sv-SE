---
title: Anpassa uppgiftsåtgärder
seo-title: Anpassa uppgiftsåtgärder
description: Du kan anpassa utseendet på uppgiftsåtgärderna, endast använda bilder för åtgärder och anpassa bilderna som används i flödesåtgärder.
seo-description: Du kan anpassa utseendet på uppgiftsåtgärderna, endast använda bilder för åtgärder och anpassa bilderna som används i flödesåtgärder.
uuid: f6aebcd5-beac-41bf-95bf-2c07d36afa8b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ca3f6025-7e17-4173-8267-e24a338ea4a1
translation-type: tm+mt
source-git-commit: 21623c615ebe69226cfaf84baf4cfb1717b449f4

---


# Anpassa uppgiftsåtgärder {#customizing-task-actions}

Med arbetsytan i AEM Forms kan användarna anpassa uppgiftsåtgärderna. Innan du anpassar uppgiftsåtgärderna måste du följa de steg som beskrivs i [Allmänna steg för anpassning](/help/forms/using/generic-steps-html-workspace-customization.md)av arbetsytan i AEM Forms.

## Anpassa textstil {#customizing-text-style}

Om du vill anpassa textformatet lägger du till följande kodfragment i `/apps/ws/css/newStyle.css` filen:

```css
/*-------- For Task Actions visible in task list task action popup ----------------------------------------------------*/
#taskarea .taskActionsPopUp{
    position:absolute;
    right: 78px;
    top: 16px;
    display: none;
}

#taskarea .taskActionsPopUp ul{
    list-style-type: none;
    padding: 0px;
    margin: 0px;
    border: 1px solid #B2B2B2;
    background: #1D1D1D;
    box-shadow: inset 0px 0px 11px 2px #1C1C1C;
    height:34px;
}

#taskarea .taskActionsPopUp li{
    width: auto;
    height: 34px;
    float: left;
    border-right: 1px solid #B2B2B2;
}

#taskarea .taskActionsPopUp li i{
    height: 34px;
    width: 20px;
    float: left;
    cursor: pointer;
}

#taskarea .taskActionsPopUp li a{
    color: white;
    text-decoration: none;
    display: inline-block;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    text-align: left;
    max-width: 150px;
    margin: 8px 10px 0px 4px;
}

/*-------- For Task Actions visible in task Details task action popup ----------------------------------------------------*/
.task .taskActionsPopUp {
    position: absolute;
    border: 1px solid #1D1D1D;
    z-index: 110;
    right: 5px;
    top : 35px;
    background: #2f2f2f;
    display:none;
}

.task .taskActionsPopUp ul{
    list-style: none outside none;
    font-size: 13px;
    width: 160px;
}

.task .taskActionsPopUp li{
    height: 33px;
    border-bottom: 1px solid #474747;
    width: 20px
}

.task .taskActionsPopUp ul a{
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    color: white;
    text-decoration: none;
    height: 26px;
    width: 133px;
    padding: 7px 0px 0px 27px;
    display: block;
    text-align: left;
    cursor: pointer;
    border-bottom: 1px solid #474747;
}
```

## Anpassa bilder {#customizing-images}

Om du vill anpassa bilderna lägger du till följande kodfragment i `/apps/ws/css/newStyle.css` filen. Följande kodfragment anpassar bilden för *låsåtgärden* :

```css
#taskarea .taskActionsPopUp .lock, .task .taskActionsPopUp .lock{
    background: url(../images/icons.png) no-repeat -265px -6px;
}
```

>[!NOTE]
>
>Lägg till separata format om du vill visa olika bilder eller bilder med olika upplösning för åtgärderna Uppgiftslista och Uppgiftsinformation. Om du till exempel vill ändra åtgärden &#39;lock&#39;:

```css
#taskarea .taskActionsPopUp .lock{
    background: url(../images/icons1.png) no-repeat -265px -6px;
}
.task .taskActionsPopUp .lock{
    background: url(../images/icons2.png) no-repeat -265px -6px;
}
```

## Visa endast bilder för åtgärder {#showing-only-images-for-actions}

Om du bara vill visa bilder för åtgärder anpassar du bilderna som används i flödesåtgärder. Mer information finns i [Bilder för flödesåtgärder](/help/forms/using/images-route-actions.md).

### Åtgärdssnabbmeny för uppgiftslistans åtgärd {#task-list-task-action-nbsp-pop-up-menu}

1. Du behöver ett utvecklingspaket för att kunna anpassa objekt på aktivitetsmenyn på arbetsytan i AEM Forms. Mer information om hur du skapar utvecklingspaket finns i [Skapa kod för arbetsytan i AEM Forms.](/help/forms/using/introduction-customizing-html-workspace.md#main-pars-heading-3)

1. Kopiera /libs/ws/js/runtime/templates/task.html för att `/apps/ws/js/runtime/templates/task.html`ersätta följande kodfragment:

   ```
   // Orignal code
   <div class="taskActionsPopUp">
           <!--START_TASKACTIONS-->
           <ul>
               <li class="arrow"></li>
               <%if(!isMustOpenToComplete && window.lcWorkspace != undefined && window.lcWorkspace.currentUser != undefined && window.lcWorkspace.currentUser.properties != undefined && window.lcWorkspace.currentUser.properties['/client/routes/formViewOnly'] == 'false'){%>
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
               <%}%>
               <%for(var i = 0; i<availableCommands.taskACLCommands.length; i++){%>
               <li class="<%= availableCommands.taskACLCommands[i]%>" alt="<%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.tooltip')%>" value="<%= availableCommands.taskACLCommands[i]%>" data-action="taskACL"><%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.value')%></a>
               </li>
               <%}%>
               <%for(var i = 0; i<availableCommands.otherCommands.length; i++){%>
               <li class="<%= availableCommands.otherCommands[i]%>" alt="<%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.tooltip')%>" value="<%= availableCommands.otherCommands[i]%>" data-action="other"><%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.value')%></a>
               </li>
               <%}%>
           </ul>
           <!--END_TASKACTIONS-->
           <%}%>
       </div>
   ```

   ```
   //New code
   
   <div class="taskActionsPopUp">
           <!--START_TASKACTIONS-->
           <ul>
               <li class="arrow"></li>
               <%if(!isMustOpenToComplete && window.lcWorkspace != undefined && window.lcWorkspace.currentUser != undefined && window.lcWorkspace.currentUser.properties != undefined && window.lcWorkspace.currentUser.properties['/client/routes/formViewOnly'] == 'false'){%>
               <%if(routeList == null){%>
               <li>
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li>
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"></a>
               </li>
               <%}%>
               <%}%>
               <%}%>
               <%for(var i = 0; i<availableCommands.taskACLCommands.length; i++){%>
               <li class="<%= availableCommands.taskACLCommands[i]%>" alt="<%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.tooltip')%>" value="<%= availableCommands.taskACLCommands[i]%>" data-action="taskACL"></a>
               </li>
               <%}%>
               <%for(var i = 0; i<availableCommands.otherCommands.length; i++){%>
               <li class="<%= availableCommands.otherCommands[i]%>" alt="<%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.tooltip')%>" value="<%= availableCommands.otherCommands[i]%>" data-action="other"></a>
               </li>
               <%}%>
           </ul>
           <!--END_TASKACTIONS-->
           <%}%>
       </div>
   ```

1. Ta bort den fasta bredden som tilldelats en ankartagg från `/apps/ws/css/newStyle.css` filen:

   ```css
   .task .taskActionsPopUp ul{
       list-style: none outside none;
       font-size: 13px;
       width: 160px;
   }
   
   To
   .task .taskActionsPopUp ul{
       list-style: none outside none;
       font-size: 13px;
   }
   
   AND
   
   .task .taskActionsPopUp ul a{
       white-space: nowrap;
       overflow: hidden;
       text-overflow: ellipsis;
       color: white;
       text-decoration: none;
       height: 26px;
       width: 133px;
       padding: 7px 0px 0px 27px;
       display: block;
       text-align: left;
       cursor: pointer;
       border-bottom: 1px solid #474747;
   }
   
   To
   
   .task .taskActionsPopUp ul a{
       white-space: nowrap;
       overflow: hidden;
       text-overflow: ellipsis;
       color: white;
       text-decoration: none;
       height: 26px;
       width: 0px;
       padding: 7px 0px 0px 27px;
       display: block;
       text-align: left;
       cursor: pointer;
       border-bottom: 1px solid #474747;
   }
   ```

### Åtgärdssnabbmenyn Åtgärd för uppgiftsinformation {#task-details-task-action-pop-up-menu}

Utför följande steg för att anpassa snabbmenyn Detaljåtgärdsåtgärder:

* Kopiera /libs/ws/js/runtime/templates/taskdetails.html till `/apps/ws/js/runtime/templates/` mappen:
* Kapsla in ikontaggen inuti ankartaggen i stället för text. Den *nya koden* nedan kapslar till exempel in ikontaggen inuti ankartaggen:

```
// Original code
<div class="taskActionsPopUp">
        <!--START_ACTIONBUTTONGROUP-->
        <ul>
            <li class="leftArrow"><a href="javascript:void(0);"><</a></li>

            <% if (isOwner && showDirectActions) { %>
                <% if (routeList === null) {%>
                    <li class="routeAction">
                        <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
                    </li>
                <% } else { %>
                    <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                        <li class="routeAction">
                            <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                        </li>
                    <%}%>
                <%}%>
             <%}%>

            <% if (isOwner || (showACLActions && availableCommands.taskACLCommands !== null && availableCommands.taskACLCommands !== undefined && availableCommands.taskACLCommands.length > 0) ||  availableCommands.otherCommands.length > 2) { %>
                <%for (var i = 0; showACLActions && i < availableCommands.taskACLCommands.length; i++) {%>
                    <li title="<%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.tooltip')%>">
                        <i class="<%= availableCommands.taskACLCommands[i]%>" value="<%= availableCommands.taskACLCommands[i]%>" data-action="taskACL"/>
                        <a href="javascript:void(0);" value="<%= availableCommands.taskACLCommands[i]%>" data-action="taskACL"><%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.value')%></a>
                    </li>
                <%}%>

                <%for (var i = 0; i < availableCommands.otherCommands.length; i++) {%>
                    <li title="<%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.tooltip')%>">
                        <i class="<%= availableCommands.otherCommands[i]%>" value="<%= availableCommands.otherCommands[i]%>" data-action="other"/>
                        <a href="javascript:void(0);" value="<%= availableCommands.otherCommands[i]%>" data-action="other"><%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.value')%></a>
                    </li>
                <%}%>
            <%}%>

            <li class="rightArrow"><a href="javascript:void(0);">></a></li>
        </ul>
        <!--END_ACTIONBUTTONGROUP-->
    </div>
```

```
//New code

<div class="taskActionsPopUp">
        <!--START_ACTIONBUTTONGROUP-->
        <ul>
            <li class="leftArrow"><a href="javascript:void(0);"><</a></li>

            <% if (isOwner && showDirectActions) { %>
                <% if (routeList === null) {%>
                    <li class="routeAction">
                        <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
                    </li>
                <% } else { %>
                    <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                        <li class="routeAction">
                            <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                        </li>
                    <%}%>
                <%}%>
             <%}%>

            <% if (isOwner || (showACLActions && availableCommands.taskACLCommands !== null && availableCommands.taskACLCommands !== undefined && availableCommands.taskACLCommands.length > 0) ||  availableCommands.otherCommands.length > 2) { %>
                <%for (var i = 0; showACLActions && i < availableCommands.taskACLCommands.length; i++) {%>
                    <li title="<%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.tooltip')%>">
                        <a href="javascript:void(0);" value="<%= availableCommands.taskACLCommands[i]%>" data-action="taskACL">
                            <i class="<%= availableCommands.taskACLCommands[i]%>" value="<%= availableCommands.taskACLCommands[i]%>" data-action="taskACL"/>
                        </a>
                    </li>
                <%}%>

                <%for (var i = 0; i < availableCommands.otherCommands.length; i++) {%>
                    <li title="<%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.tooltip')%>">
                        <a href="javascript:void(0);" value="<%= availableCommands.otherCommands[i]%>" data-action="other">
                            <i class="<%= availableCommands.otherCommands[i]%>" value="<%= availableCommands.otherCommands[i]%>" data-action="other"/>
                        </a>
                    </li>
                <%}%>
            <%}%>

            <li class="rightArrow"><a href="javascript:void(0);">></a></li>
        </ul>
        <!--END_ACTIONBUTTONGROUP-->
    </div>
```

* Öppna /apps/ws/js/registry.js för redigering.
* Leta reda på följande text: `text!/lc/libs/ws/js/runtime/templates/taskdetails.html`
* Ersätt den placerade texten med följande text: `text!/lc/apps/ws/js/runtime/templates/taskdetails.html`

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
