---
title: Skapa en anpassad verktygsfältsåtgärd
seo-title: Skapa en anpassad verktygsfältsåtgärd
description: Formulärutvecklare kan skapa anpassade verktygsfältsåtgärder för anpassningsbara formulär i AEM Forms. Med anpassade åtgärder kan formulärförfattare tillhandahålla fler arbetsflöden och alternativ till sina slutanvändare.
seo-description: Formulärutvecklare kan skapa anpassade verktygsfältsåtgärder för anpassningsbara formulär i AEM Forms. Med anpassade åtgärder kan formulärförfattare tillhandahålla fler arbetsflöden och alternativ till sina slutanvändare.
uuid: cd785cfb-e1bb-4158-be9b-d99e04eccc02
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 4beca23f-dbb0-4e56-8047-93e4f1775418
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---


# Skapa en anpassad verktygsfältåtgärd{#creating-a-custom-toolbar-action}

## Förutsättningar {#prerequisite}

Innan du skapar en anpassad verktygsfältåtgärd bör du känna till [Använda bibliotek på klientsidan](/help/sites-developing/clientlibs.md) och [Utveckla med CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

## Vad är en åtgärd {#what-is-an-action-br}?

Ett adaptivt formulär har ett verktygsfält där formulärförfattaren kan konfigurera en uppsättning alternativ. Dessa alternativ definieras som åtgärder för det adaptiva formuläret. Klicka på knappen Redigera i verktygsfältet för panelen för att ange vilka åtgärder som kan användas i adaptiva formulär.

![Standardåtgärder i verktygsfältet](assets/default_toolbar_actions.png)

Förutom den uppsättning åtgärder som finns som standard kan du skapa anpassade åtgärder i verktygsfältet. Du kan till exempel lägga till en åtgärd som gör att användaren kan granska alla anpassningsbara formulärfält innan ett formulär skickas.

## Steg för att skapa en anpassad åtgärd i anpassade formulär {#steps}

Följande steg visar hur du skapar en anpassad verktygsfältåtgärd och hur du skapar en knapp där slutanvändare kan granska alla anpassningsbara formulärfält innan de skickar in ett ifyllt formulär.

1. Alla standardåtgärder som stöds av adaptiva formulär finns i mappen `/libs/fd/af/components/actions`. I CRXDE kopierar du noden `fileattachmentlisting` från `/libs/fd/af/components/actions/fileattachmentlisting` till `/apps/customaction`.

1. När du har kopierat noden till mappen `apps/customaction` byter du namn på noden till `reviewbeforesubmit`. Ändra även egenskaperna `jcr:title` och `jcr:description` för noden.

   Egenskapen `jcr:title` innehåller namnet på åtgärden som visas i verktygsfältsdialogrutan. Egenskapen `jcr:description` innehåller mer information som visas när en användare håller pekaren över åtgärden.

   ![Hierarki med noder för anpassning av verktygsfältet](assets/action3.png)

1. Välj noden `cq:template` i noden `reviewbeforesubmit`. Kontrollera att värdet för egenskapen `guideNodeClass` är `guideButton` och ändra egenskapen `jcr:title` därefter.
1. Ändra type-egenskapen i noden `cq:Template`. I det aktuella exemplet ändrar du type-egenskapen till button.

   Typvärdet läggs till som en CSS-klass i den genererade HTML-koden för komponenten. Användare kan använda den CSS-klassen för att formatera sina åtgärder. Standardformatet för både mobila och stationära enheter finns för knappar, skicka, återställa och spara typvärden.

1. Välj den anpassade åtgärden i verktygsfältet för redigering av anpassningsbara formulär. En granskningsknapp visas i panelens verktygsfält.

   ![Anpassad åtgärd är tillgänglig i ](assets/custom_action_available_in_toolbar.png) ![verktygsfältetVisa den anpassade verktygsfältsåtgärden](assets/action7.png)

1. Om du vill lägga till funktioner till knappen Granska lägger du till JavaScript- och CSS-kod och kod på serversidan i filen init.jsp, som finns i noden `reviewbeforesubmit`.

   Lägg till följande kod i `init.jsp`.

   ```jsp
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <guide:initializeBean name="guideField" className="com.adobe.aemds.guide.common.GuideButton"/>
   
   <c:if test="${not isEditMode}">
           <cq:includeClientLib categories="reviewsubmitclientlibruntime" />
   </c:if>
   
   <%--- BootStrap Modal Dialog  --------------%>
   <div class="modal fade" id="reviewSubmit" tabindex="-1">
       <div class="modal-dialog">
           <div class="modal-content">
               <div class="modal-header">
                   <h3>Review the Form Fields</h3>
               </div>
               <div class="modal-body">
                   <div class="modal-list">
                       <table class="table table-bordered">
                           <tr class="name">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Name is: </label>
                               </td>
                           </tr>
                           <tr class="pan">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Pan Number is: </label>
                               </td>
                           </tr>
                           <tr class="dob">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Date Of Birth is: </label>
                               </td>
                           </tr>
                           <tr class="80cdeclaration">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Total 80C Declaration Amount is: </label>
                               </td>
                           </tr>
                           <tr class="rentpaid">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Total HRA Amount is: </label>
                               </td>
                           </tr>
                       </table>
                   </div>
               </div><!-- /.modal-body -->
               <div class="modal-footer">
                   <div class="fileAttachmentListingCloseButton col-md-2 col-xs-2 col-sm-2">
                       <button data-dismiss="modal">Close</button>
                   </div>
               </div>
           </div><!-- /.modal-content -->
       </div><!-- /.modal-dialog -->
   </div><!-- /.modal -->
   ```

   Lägg till följande kod i `ReviewBeforeSubmit.js`-filen.

   ```javascript
   /*anonymous function to handle show of review before submit view */
   $(function () {
       if($("div.reviewbeforesubmit button[id*=reviewbeforesubmit]").length > 0) {
           $("div.reviewbeforesubmit button[id*=reviewbeforesubmit]").click(function(){
               // Create the options object to be passed to the getElementProperty API
               var options = {},
                   result = [];
               options.somExpressions = [];
               options.propertyName = "value";
               guideBridge.visit(function(model){
                   if(model.name === "name" || model.name === "pan" || model.name === "dateofbirth" || model.name === "total" || model.name === "totalmonthlyrent"){
                           options.somExpressions.push(model.somExpression);
                   }
               }, this);
               result = guideBridge.getElementProperty(options);
   
               $('#reviewSubmit .reviewlabel').each(function(index, item){
                   var data = ((result.data[index] == null) ? "No Data Filled" : result.data[index]);
                   if($(this).next().hasClass("reviewlabelvalue")){
                       $(this).next().html(data);
                   } else {
                       $(this).after($("<td></td>").addClass("reviewlabelvalue col-md-6 active").html(data));
                   }
               });
               // added because in mobile devices it was causing problem of backdrop
               $("#reviewSubmit").appendTo('body');
               $("#reviewSubmit").modal("show");
           });
       }
   });
   ```

   Lägg till följande kod i filen `ReviewBeforeSubmit.css`.

   ```css
   .modal-list .reviewlabel {
       white-space: normal;
       text-align: right;
       padding:2px;
   }
   
   .modal-list .reviewlabelvalue {
       border: #cde0ec 1px solid;
       padding:2px;
   }
   
   /* Adding icon for this action in mobile devices */
   /* This is the glyphicon provided by bootstrap eye-open */
   /* .<type> .iconButton-icon */
   .reviewbeforesubmit .iconButton-icon {
       position: relative;
       top: -8px;
       font-family: 'Glyphicons Halflings';
       font-style: normal;
   }
   
   .reviewbeforesubmit .iconButton-icon:before {
       content: "\e105"
   }
   ```

1. Om du vill kontrollera funktionaliteten för den anpassade åtgärden öppnar du det adaptiva formuläret i förhandsgranskningsläget och klickar på Granska i verktygsfältet.

   >[!NOTE]
   >
   >Biblioteket `GuideBridge` har inte lästs in i redigeringsläge. Den här anpassade åtgärden fungerar därför inte i redigeringsläget.

   ![Demonstration av åtgärden för knappen för anpassad granskning](assets/action9.png)

## Exempel {#samples}

Följande arkiv innehåller ett innehållspaket. Paketet innehåller ett anpassat formulär relaterat till demonstrationen ovan av en anpassad verktygsfältåtgärd.

[Hämta fil](assets/customtoolbaractiondemo.zip)
