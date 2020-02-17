---
title: Utöka sökfunktionerna i AEM Assets
description: Utöka sökfunktionerna i AEM Assets utöver standardvärdena.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Utöka resurssökning {#extending-assets-search}

Du kan utöka sökfunktionerna i Adobe Experience Manager (AEM) Assets. När allt är klart söker AEM Resurser efter resurser efter strängar.

Sökningen görs via gränssnittet i QueryBuilder så att sökningen kan anpassas med flera predikat. Du kan täcka över standarduppsättningen med predikat i följande katalog: `/apps/dam/content/search/searchpanel/facets`.

Du kan även lägga till ytterligare flikar på AEM Resurser-administratörspanelen.

>[!CAUTION]
>
>Från och med AEM 6.4 är det klassiska användargränssnittet föråldrat. Information finns i [Borttagna och borttagna funktioner](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/deprecated-removed-features.html). Du rekommenderas att använda användargränssnittet med pekskärmsfunktioner. Mer information om anpassning finns i [Sök efter ansikten](/help/assets/search-facets.md).

## Övertäckning {#overlaying}

Om du vill täcka över de förkonfigurerade predikaten kopierar du `facets` noden från `/libs/dam/content/search/searchpanel` till `/apps/dam/content/search/searchpanel/` eller anger en annan `facetURL` egenskap i `searchpanel` konfigurationen (standardvärdet är `/libs/dam/content/search/searchpanel/facets.overlay.infinity.json`).

![screen_shot_2012-06-05at113619am](assets/screen_shot_2012-06-05at113619am.png)

>[!NOTE]
>
>Som standard finns inte katalogstrukturen under/ `apps` och måste skapas. Kontrollera att nodtyperna matchar dem under / `libs`.


## Lägg till tabbar {#adding-tabs}

Du kan lägga till fler sökflikar genom att konfigurera dem i AEM Resurser Admin. Så här skapar du ytterligare flikar:

1. Skapa mappstrukturen `/apps/wcm/core/content/damadmin/tabs,`om den inte redan finns, och kopiera `tabs` noden från `/libs/wcm/core/content/damadmin` och klistra in den.
1. Skapa och konfigurera den andra fliken efter behov.

   >[!NOTE]
   >
   >När du skapar en andra `siteadminsearchpanel`ska du se till att ange en `id` egenskap för att förhindra formulärkonflikter.

## Skapa anpassade predikat {#creating-custom-predicates}

AEM Resurser innehåller en uppsättning fördefinierade predikat som kan användas för att anpassa en resursdelssida. Att anpassa en resurs på det här sättet beskrivs i [Skapa och konfigurera en resursdelssida](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page).

Förutom att använda befintliga predikat kan AEM-utvecklare även skapa egna predikat med [Query Builder API](/help/sites-developing/querybuilder-api.md).

Det krävs grundläggande kunskaper om [widgetramverket](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)för att kunna skapa anpassade predikat.

Det bästa sättet är att kopiera ett befintligt predikat och justera det. Exempelpredikaten finns i **/libs/cq/search/components/predikates**.

### Exempel: Skapa ett enkelt egenskapspredikat {#example-build-a-simple-property-predicate}

Så här skapar du ett egenskapspredikat:

1. Skapa en komponentmapp i projektkatalogen, till exempel **/apps/geometrixx/components/titlepreate**.
1. Lägg till **content.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Title Predicate"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. Lägg till `titlepredicate.jsp`.

   ```xml
   <%--
   
     Sample title predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Title</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:title";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // createId adds a counter to the predicate name - useful in case this predicate
           // is inserted multiple times on the same page.
           var id = qb.createId(predicateName);
   
           // Hidden field that defines the property to search for; in our case this
           // is the "dc:title" metadata. The name "property" (or "1_property", "2_property" etc.)
           // indicates the server to use the property predicate
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id,
               "value": propertyName
           });
   
           // The visible text field. The name has to be like the one of the hidden field above
           // plus the ".value" suffix.
           qb.addField({
               "xtype": "textfield",
               "renderTo": elemId,
               "name": id + ".value"
           });
   
           // Depending on the predicate additional parameters allow to configure the
           // predicate. Here we add an operation parameter to create a "like" query.
           // Again note the name set to the id and a suffix.
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id + ".operation",
               "value": "like"
           });
       });
   </script>
   ```

1. Om du vill göra komponenten tillgänglig måste du kunna redigera den. Om du vill göra en komponent redigerbar lägger du i CRXDE till en nod **cq:editConfig** av den primära typen **cq:EditConfig**. Du kan ta bort stycken genom att lägga till en egenskap med flera värden **cq:actions** med ett enda värde på **DELETE**.
1. Navigera till webbläsaren och på exempelsidan (till exempel **press.html**) växla till designläge och aktivera den nya komponenten för det prediktiva styckesystemet (till exempel **vänster**).

1. I **redigeringsläget** är den nya komponenten nu tillgänglig i sidosparken (finns i **sökgruppen** ). Infoga komponenten i kolumnen **Predikatorer** och skriv ett sökord, till exempel **Diamant** , och klicka på förstoringsglaset för att starta sökningen.

   >[!NOTE]
   >
   >När du söker måste du skriva in ordet exakt, inklusive rätt skiftläge.

### Exempel: Skapa ett enkelt grupppredikat {#example-build-a-simple-group-predicate}

Så här skapar du ett grupppredikat:

1. Skapa en komponentmapp i projektkatalogen, till exempel **/apps/geometrixx/components/picspredicate.**
1. Lägg till **content.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Formats"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. Lägg till **titlepreate.jsp**:

   ```xml
   <%--
   
     Sample group predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page.
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Image Formats</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:format";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // Create a unique group ID; will return e.g. "1_group".
           var groupId = qb.createGroupId();
   
           // Hidden field that defines the property to search for  - in our case "dc:format" -
           // and declares the group of predicates. "property" in the name ("1_group.property")
           // indicates to the server to use the "property predicate"
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": "<%= elemId %>",
               "name": groupId + "." + predicateName, // 1_group.property
               "value": propertyName
           });
   
           // Declare to combine the multiple values using OR.
           qb.add(new CQ.Ext.form.Hidden({
               "name": groupId + ".p.or",  // 1_group.p.or
               "value": "true"
           }));
   
           // The options
           var options = [
               { "label":"JPEG", "value":"image/jpeg"},
               { "label":"PNG",  "value":"image/png" },
               { "label":"GIF",  "value":"image/gif" }
           ];
   
           // Build a checkbox for each option.
           for (var i = 0; i < options.length; i++) {
               qb.addField({
                   "xtype": "checkbox",
                   "renderTo": "<%= elemId %>",
                   // 1_group.property.0_value, 1_group.property.1_value etc.
                   "name": groupId + "." +  predicateName + "." + i + "_value",
                   "inputValue": options[i].value,
                   "boxLabel": options[i].label,
                   "listeners": {
                       "check": function() {
                           // Submit the search form when checking/unchecking a checkbox.
                           qb.submit();
                       }
                   }
               });
           }
       });
   ```

1. Om du vill göra komponenten tillgänglig måste du kunna redigera den. Om du vill göra en komponent redigerbar lägger du i CRXDE till en nod **cq:editConfig** av den primära typen **cq:EditConfig**. Du kan ta bort stycken genom att lägga till en egenskap med flera värden **cq:actions** med ett enda värde på **DELETE**.
1. Navigera till webbläsaren och på exempelsidan (till exempel **press.html**) växla till designläge och aktivera den nya komponenten för det prediktiva styckesystemet (till exempel **vänster**).
1. I **redigeringsläget** är den nya komponenten nu tillgänglig i sidosparken (finns i **sökgruppen** ). Infoga komponenten i kolumnen **Predicates** .

## Installerade prediktiva widgetar {#installed-predicate-widgets}

Följande predikat är tillgängliga som förkonfigurerade ExtJS-widgetar.

### FulltextPredicate {#fulltextpredicate}

| Egenskap | Typ | Beskrivning |
|---|---|---|
| predikateName | Sträng | Predikatets namn. Standardvärdet är `fulltext` |
| searchCallback | Funktion | Återanrop för att utlösa sökning vid händelse `keyup`. Standardvärdet är `CQ.wcm.SiteAdmin.doSearch` |

### PropertyPredicate {#propertypredicate}

| Egenskap | Typ | Beskrivning |
|---|---|---|
| predikateName | Sträng | Predikatets namn. Standardvärdet är `property` |
| propertyName | Sträng | Namn på JCR-egenskapen. Standardvärdet är `jcr:title` |
| defaultValue | Sträng | Förfyllt standardvärde. |

### PathPredicate {#pathpredicate}

| Egenskap | Typ | Beskrivning |
|---|---|---|
| predikateName | Sträng | Predikatets namn. Standardvärdet är `path` |
| rootPath | Sträng | Predikatets rotsökväg. Standardvärdet är `/content/dam` |
| pathFieldPredicateName | Sträng | Standardvärdet är `folder` |
| showFlatOption | Boolesk | Flagga som visar kryssrutan `search in subfolders`. Standardvärdet är true. |

### DatePredicate {#datepredicate}

| Egenskap | Typ | Beskrivning |
|---|---|---|
| predikateName | Sträng | Predikatets namn. Standardvärdet är `daterange` |
| egenskapsnamn | Sträng | Namn på JCR-egenskapen. Standardvärdet är `jcr:content/jcr:lastModified` |
| defaultValue | Sträng | Förfyllt standardvärde |

### OptionsPredicate {#optionspredicate}

| Egenskap | Typ | Beskrivning |
|---|---|---|
| title | Sträng | Lägger till ytterligare en rubrik |
| predikateName | Sträng | Predikatets namn. Standardvärdet är `daterange` |
| egenskapsnamn | Sträng | Namn på JCR-egenskapen. Standardvärdet är `jcr:content/metadata/cq:tags` |
| komprimera | Sträng | Komprimera nivå. Standardvärdet är `level1` |
| triggerSearch | Boolesk | Flagga för att utlösa sökning vid kontroll. Standardvärdet är false |
| searchCallback | Funktion | Återanrop för att utlösa sökning. Standardvärdet är `CQ.wcm.SiteAdmin.doSearch` |
| searchTimeoutTime |  Nummer | Timeout innan searchCallback aktiveras. Standardvärdet är 800 ms |

## Anpassa sökresultat {#customizing-search-results}

Presentationen av sökresultaten på en resursdelningssida styrs av det valda objektivet. AEM Assets innehåller en uppsättning fördefinierade objektiv som kan användas för att anpassa en resursdelssida. Att anpassa en resurs på det här sättet beskrivs i [Skapa och konfigurera en resursdelssida](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page).

Förutom att använda befintliga linser kan AEM-utvecklare även skapa egna linser.
