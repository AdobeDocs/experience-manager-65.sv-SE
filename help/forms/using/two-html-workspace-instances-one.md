---
title: Två AEM Forms-instanser finns på en server
seo-title: Två AEM Forms-instanser finns på en server
description: Så här kan LC-administratörer anpassa HTML WS för att ha två instanser på en enda server som kan nås via olika URL:er.
seo-description: Så här kan LC-administratörer anpassa HTML WS för att ha två instanser på en enda server som kan nås via olika URL:er.
uuid: 0584f512-6b92-4418-b71c-93605cfa1927
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 1254a7c2-2c67-4661-803e-afd53e817916
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Två AEM Forms-instanser finns på en server {#hosting-two-aem-forms-workspace-instances-on-one-server}

Standardinstallationen och inställningarna för AEM Forms tillåter endast att en AEM Forms-arbetsyta är tillgänglig på servern. Du kan dock behöva placera två olika instanser av arbetsytan i AEM Forms på en enda AEM Forms-server. De två instanserna är tillgängliga via olika URL:er.

AEM Forms-administratörer anpassar arbetsytan för att skapa två olika URL:er och gör två arbetsytor tillgängliga på samma server. I den här artikeln antar vi att de två arbetsytorna är tillgängliga både `https://'[server]:[port]'/lc/ws` och `https://'[server]:[port]':/lc/ws2`.

Följ de här stegen för att konfigurera arbetsytan i AEM Forms.

1. Installera utvecklarpaketet för AEM Forms-arbetsytan på servern. Se [dev-paketet](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)för instruktioner om hur du skapar det.
1. Logga in på CRXDE Lite som administratör via `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Kopiera nod på /content och klistra in på /content. Byt namn på noden till ws2. Klicka på **[!UICONTROL Spara alla]**. Ändra värdet på `sling:resourceType` till ws2 i den här nodens egenskaper. Klicka på **[!UICONTROL Spara alla]**.

1. Kopiera mapp från /libs och klistra in på /apps. Byt namn på mappen till ws2. Klicka på **[!UICONTROL Spara alla]**.
1. Gör följande kodändringar i `GET.jsp``/apps/ws2`på. Ersätt följande

   ```
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" /><html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" />
   ```

   med följande kod

   ```
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. I `registry.js` finns `/apps/ws2/js`mallarna som du kan ändra till att referera till mallarna i `/apps/ws2/js/runtime/templates`. Ersätt följande kod

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/libs/ws/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

   med följande kod

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/apps/ws2/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

1. I `userinfo.js` at `/apps/ws2/js/runtime/models` och `/apps/ws2/js/runtime/views`ändrar du strängen `/lc/content/ws` till `lc/content/ws2`.

1. I `/apps/ws2/js/runtime/services/service.js`ändrar du banan i `getLocalizationData` funktionen till peka `/lc/apps/ws2/Locale.html`.

1. Om du vill referera till `pdf.html` den nya arbetsytan ändrar du sökvägen för `pdf.html` i `/apps/ws2/js/runtime/views/forms/pdftaskform.js`.

1. Om du vill referera till `pdf.html` den nya arbetsytan ändrar du sökvägar för `pdf.html` och `WsNextAdapter.swf` i `startprocess.html`, `taskdetails.html`och `processinstancehistory.html` på `/apps/ws2/js/runtime/templates`.

1. Kopiera `/etc/map/ws` mapp och klistra in på `/etc/map`. Byt namn på den nya mappen till ws2. Klicka på Spara alla.

1. I egenskaperna för `ws2`ändrar du värdet för `sling:redirect` till `content/ws2`.

1. Ändra värdet för `sling:match` till `^[^/\||]/[^/\||]/ws2$`.

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
