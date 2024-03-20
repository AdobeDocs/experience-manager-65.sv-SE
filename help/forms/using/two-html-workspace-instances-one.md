---
title: Köra två AEM Forms-arbetsyteinstanser på en server
description: Hur LC-administratörer kan anpassa HTML WS för att ha två instanser på en enda server som kan nås via olika URL:er.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 32a546fc-e33f-46f9-ac3b-45eca0e12239
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 1%

---

# Köra två AEM Forms-arbetsyteinstanser på en server {#hosting-two-aem-forms-workspace-instances-on-one-server}

Standardinstallationen och standardinställningarna för AEM Forms tillåter endast att en AEM Forms-arbetsyta är tillgänglig på servern. Du kan dock behöva placera två olika instanser av AEM Forms-arbetsytan på en enda AEM Forms-server. De två instanserna är tillgängliga med olika URL:er.

AEM Forms-administratörer anpassar arbetsytan för att skapa två olika URL:er och gör två arbetsytor tillgängliga på samma server. I den här anpassningsartikeln kan du anta att de två arbetsytorna är tillgängliga på `https://'[server]:[port]'/lc/ws` och `https://'[server]:[port]':/lc/ws2`.

Följ de här stegen för att konfigurera arbetsytan i AEM Forms.

1. Installera Dev-paketet för AEM Forms-arbetsytan på servern. Se [dev-paket](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p), för instruktioner om hur du skapar den.
1. Logga in på CRXDE Lite som administratör via `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Kopiera nod på /content och klistra in på /content. Byt namn på noden till ws2. Klicka på **[!UICONTROL Save all]**. Ändra värdet för `sling:resourceType` till ws2. Klicka på **[!UICONTROL Save all]**.

1. Kopiera mapp från /libs och klistra in på /apps. Byt namn på mappen till ws2. Klicka på **[!UICONTROL Save all]**.
1. I `GET.jsp` på `/apps/ws2`gör du följande kodändringar. Ersätt följande

   ```html
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

   ```html
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. I `registry.js` på `/apps/ws2/js`, ändra sökvägen till mallar för att hänvisa till mallar på `/apps/ws2/js/runtime/templates`. Ersätt följande kod

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

1. I `userinfo.js` på `/apps/ws2/js/runtime/models` och `/apps/ws2/js/runtime/views`, ändringssträng `/lc/content/ws` till `lc/content/ws2`.

1. I `/apps/ws2/js/runtime/services/service.js`, ändra banan i `getLocalizationData` function to point to `/lc/apps/ws2/Locale.html`.

1. Att referera till `pdf.html` för den nya arbetsytan, ändra sökvägen för `pdf.html` in `/apps/ws2/js/runtime/views/forms/pdftaskform.js`.

1. Att referera till `pdf.html` för den nya arbetsytan, ändra sökvägar för `pdf.html` och `WsNextAdapter.swf` in `startprocess.html`, `taskdetails.html`och `processinstancehistory.html` på `/apps/ws2/js/runtime/templates`.

1. Kopiera `/etc/map/ws` mapp och klistra in på `/etc/map`. Byt namn på den nya mappen till ws2. Klicka på Spara alla.

1. I egenskaper för `ws2`, ändra värdet för `sling:redirect` till `content/ws2`.

1. Ändra värdet för `sling:match` till `^[^/\||]/[^/\||]/ws2$`.
