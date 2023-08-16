---
title: Utöka resursredigeraren
description: Lär dig hur du utökar funktionerna i Resursredigeraren med anpassade komponenter.
contentOwner: AG
role: User, Admin
feature: Developer Tools
exl-id: de1c63c1-a0e5-470b-8d83-b594513a5dbd
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 13%

---

# Utöka resursredigeraren {#extending-asset-editor}

Resursredigeraren är den sida som öppnas när användaren klickar på en resurs som hittas via Resursresurs, så att användaren kan redigera sådana aspekter av resursen som metadata, miniatyrbilder, rubrik och taggar.

Konfiguration av redigeraren med de fördefinierade redigeringskomponenterna beskrivs i [Skapa och konfigurera en resursredigeringssida](assets-finder-editor.md#creating-and-configuring-an-asset-editor-page).

Förutom att använda befintliga redigeringskomponenter [!DNL Adobe Experience Manager] utvecklare kan också skapa egna komponenter.

## Skapa en resursredigeringsmall {#creating-an-asset-editor-template}

Följande exempelsidor finns i Geometrixx:

* Exempelsida för Geometrixx: `/content/geometrixx/en/press/asseteditor.html`
* Exempelmall: `/apps/geometrixx/templates/asseteditor`
* Exempel på sidkomponent: `/apps/geometrixx/components/asseteditor`

### Konfigurera Clientlib {#configuring-clientlib}

[!DNL Assets] -komponenter använder ett tillägg till WCM-klienten för redigering. Klientlibs läses vanligtvis in i `init.jsp`.

Jämfört med standardinläsning av klientlib (i kärnan) `init.jsp`), [!DNL Assets] -mallen måste ha följande:

* Mallen måste innehålla `cq.dam.edit` clientlib (i stället för `cq.wcm.edit`).

* Clientlib måste också inkluderas i inaktiverat WCM-läge (t.ex. läsas in vid **publicering**) för att kunna återge predikat, åtgärder och linser.

I de flesta fall kopieras det befintliga exemplet `init.jsp` (`/apps/geometrixx/components/asseteditor/init.jsp`) ska tillgodose dessa behov.

### Konfigurera JS-åtgärder {#configuring-js-actions}

Vissa av [!DNL Assets] komponenter kräver JS-funktioner definierade i `component.js`. Kopiera den här filen till komponentkatalogen och länka den.

```javascript
<script type="text/javascript" src="<%= component.getPath() %>/component.js"></script>
```

Exemplet läser in den här JavaScript-källan i `head.jsp`(`/apps/geometrixx/components/asseteditor/head.jsp`).

### Ytterligare formatmallar {#additional-style-sheets}

Vissa av [!DNL Assets] -komponenter använder widgetbiblioteket. För att kunna återges korrekt i innehållskontexten måste ytterligare en formatmall läsas in. Kodåtgärdskomponenten kräver en till.

```css
<link href="/etc/designs/geometrixx/ui.widgets.css" rel="stylesheet" type="text/css">
```

### Geometrixx formatmall {#geometrixx-style-sheet}

Komponenterna för exempelsidorna kräver att alla väljare börjar med `.asseteditor` av `static.css` (`/etc/designs/geometrixx/static.css`). God praxis: Kopiera alla `.asseteditor` väljare till formatmallen och justera reglerna efter behov.

### FormChooser: Justeringar för resurser som eventuellt lästs in {#formchooser-adjustments-for-eventually-loaded-resources}

Resursredigeraren använder formulärväljaren, som gör att du kan redigera resurser - i det här fallet resurser - på samma formulärsida genom att lägga till en formulärväljare och formulärsökvägen till resursens URL.

Till exempel:

* Oformaterad formulärsida: [http://localhost:4502/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/geometrixx/en/press/asseteditor.html)
* Resursen har lästs in på formulärsidan: [http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html)

Exempelhandtagen i `head.jsp` (`/apps/geometrixx/components/asseteditor/head.jsp`) gör följande:

* De identifierar om en resurs har lästs in eller om det rena formuläret måste visas.
* Om en resurs läses in kan de inaktivera WCM-läget som parsys bara redigeras på en vanlig formulärsida.
* Om en resurs läses in använder de dess titel i stället för den på formulärsidan.

```javascript
 List<Resource> resources = FormsHelper.getFormEditResources(slingRequest);
    if (resources != null) {
        if (resources.size() == 1) {
            // single resource
            FormsHelper.setFormLoadResource(slingRequest, resources.get(0));
        } else if (resources.size() > 1) {
            // multiple resources
            // not supported by CQ 5.3
        }
    }
    Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
    String title;
    if (loadResource != null) {
        // an asset is loaded: disable WCM
        WCMMode.DISABLED.toRequest(request);

        String path = loadResource.getPath();
        Asset asset = loadResource.adaptTo(Asset.class);
        try {
            // it might happen that the adobe xmp lib creates an array
            Object titleObj = asset.getMetadata("dc:title");
            if (titleObj instanceof Object[]) {
                Object[] titleArray = (Object[]) titleObj;
                title = (titleArray.length > 0) ? titleArray[0].toString() : "";
            } else {
                title = titleObj.toString();
            }
        }
        catch (NullPointerException e) {
            title = path.substring(path.lastIndexOf("/") + 1);
        }
    }
    else {
        title = currentPage.getTitle() == null ? currentPage.getName() : currentPage.getTitle();
    }
```

Använd den föregående titeluppsättningen (antingen resurs eller sidrubrik) i HTML-delen:

```html
<title><%= title %></title>
```

## Skapa en enkel formulärfältskomponent {#creating-a-simple-form-field-component}

I det här exemplet beskrivs hur du skapar en komponent som visar och visar metadata för en inläst resurs.

1. Skapa en komponentmapp i projektkatalogen, till exempel `/apps/geometrixx/components/samplemeta`.
1. Lägg till `content.xml` med följande kodutdrag:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Dimension"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Asset Editor"/>
   ```

1. Lägg till `samplemeta.jsp` med följande kodutdrag:

   ```javascript
   <%--
   
     Sample metadata field component
   
   --%><%@ page import="com.day.cq.dam.api.Asset,
                    java.security.AccessControlException" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       String value = "";
       String name = "dam:sampleMetadata";
       boolean readOnly = false;
   
       // If the form page is requested for an asset loadResource will be the asset.
       Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
   
       if (loadResource != null) {
   
           // Determine if the loaded asset is read only.
           Session session = slingRequest.getResourceResolver().adaptTo(Session.class);
           try {
               session.checkPermission(loadResource.getPath(), "set_property");
               readOnly = false;
           }
           catch (AccessControlException ace) {
               // checkPermission throws exception if asset is read only
               readOnly = true;
           }
           catch (RepositoryException re) {}
   
           // Get the value of the metadata.
           Asset asset = loadResource.adaptTo(Asset.class);
           try {
               value = asset.getMetadata(name).toString();
           }
           catch (NullPointerException npe) {
               // no metadata dc:description available
           }
       }
   %>
   <div class="form_row">
       <div class="form_leftcol">
           <div class="form_leftcollabel">Sample Metadata</div>
       </div>
       <div class="form_rightcol">
           <%
           if (readOnly) {
               %><c:out value="<%= value %>"/><%
           }
           else {
               %><input class="text" type="text" name="./jcr:content/metadata/<%= name %>" value="<c:out value="<%= value %>" />"><%
           }%>
       </div>
   </div>
   ```

1. Om du vill göra komponenten tillgänglig måste du kunna redigera den. Gör en komponent redigerbar genom att lägga till en nod i CRXDE Lite `cq:editConfig` av primär typ `cq:EditConfig`. Du kan ta bort stycken genom att lägga till en egenskap med flera värden `cq:actions` med ett enda värde på `DELETE`.

1. Navigera till webbläsaren och till exempelsidan (till exempel `asseteditor.html`) växla till designläge och aktivera den nya komponenten för styckesystemet.

1. I **redigeringsläget** är den nya komponenten (till exempel **Exempelmetadata**) nu tillgänglig i assistenten (finns i gruppen **Resursredigeraren**). Infoga komponenten. För att metadata ska kunna lagras måste de läggas till i metadataformuläret.

## Ändra metadataalternativ {#modifying-metadata-options}

Du kan ändra de namnutrymmen som finns i dialogrutan [metadata-formulär](assets-finder-editor.md#metadata-form-and-text-field-configuring-the-view-metadata-component).

Tillgängliga metadata definieras i `/libs/dam/options/metadata`:

* Den första nivån i den här katalogen innehåller namnutrymmena.
* Objekten i varje namnutrymme representerar metadata, till exempel resultat i ett lokalt delsobjekt.
* Metadatainnehållet innehåller information om typen och alternativen för flera värden.

Alternativen kan skrivas över i `/apps/dam/options/metadata`:

1. Kopiera katalogen från `/libs` till `/apps`.

1. Ta bort, ändra eller lägga till objekt.

>[!NOTE]
>
>Om du lägger till nya namnutrymmen måste de registreras i din databas/CRX. Om du inte skickar metadataformuläret uppstår ett fel.
