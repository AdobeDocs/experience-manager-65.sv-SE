---
title: Allmänna steg för anpassning av arbetsytan i AEM Forms
seo-title: Allmänna steg för anpassning av arbetsytan i AEM Forms
description: Hur man kommer igång med att anpassa användargränssnittet för arbetsytan i AEM Forms.
seo-description: Hur man kommer igång med att anpassa användargränssnittet för arbetsytan i AEM Forms.
uuid: da6310b4-1c58-468d-85c6-975fd2c141f9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: dd3218c4-2bb2-40fc-9141-5823b0ea4224
docset: aem65
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 3%

---


# Allmänna steg för anpassning av arbetsytan i AEM Forms{#generic-steps-for-aem-forms-workspace-customization}

De allmänna stegen för att utföra anpassningar är:

1. Logga in på CRXDE Lite med åtkomst `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Skapa en mapp med namnet `ws`at `/apps`om den inte finns. Klicka på **[!UICONTROL Save All]**.
1. Bläddra till `/apps/ws`och navigera till **[!UICONTROL Access Control]** fliken.
1. Klicka i **[!UICONTROL Access Control]** listan för **[!UICONTROL +]** att lägga till en ny post. Klicka **[!UICONTROL +]** igen.
1. Sök efter och markera **PERM_WORKSPACE_USER** Principal.

   ![Välj PERM_WORKSPACE_USER som en del av de allmänna stegen för att anpassa HTML-arbetsytan](assets/perm_workspace_user.png)

1. Ge huvudmannen `jcr:read` privilegium.
1. Klicka på **[!UICONTROL Save All]**.
1. Kopiera `GET.jsp` och `html.jsp`filer från `/libs/ws`mappen till `/apps/ws` mappen.
1. Kopiera `/libs/ws/locales` mappen i `/apps/ws` mappen. Klicka på **[!UICONTROL Save All]**.
1. Uppdatera referenserna och de relativa sökvägarna i `GET.jsp` filen, så som visas nedan, och klicka på **[!UICONTROL Save all]**.

   ```javascript
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. Gör följande för CSS-anpassningar:

   1. Navigera till `/apps/ws` mappen och skapa en ny mapp med namnet `css`.

   1. Skapa en ny fil med namnet `css`i `newStyle.css`mappen.

   1. Öppna `/apps/ws/html`.jsp och ändra från

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/jquery-ui.css"/>
   ```

   till

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/newStyle.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/jquery-ui.css"/>
   ```

   >[!NOTE]
   >
   >Placera den användardefinierade CSS-filen efter posten newStyle.css, som visas ovan.

1. I /apps/ws/html.jsp

   ```jsp
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   till

   ```jsp
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. Gör följande:

   1. Skapa en mapp med namnet `js`at `/apps/ws`. Klicka på **[!UICONTROL Save All]**.

   1. Skapa en mapp med namnet `libs`at `/apps/ws/js`. Klicka på **[!UICONTROL Save All]**.

   1. Skapa en mapp med namnet `jqueryui`at `/apps/ws/js/libs`. Klicka på **[!UICONTROL Save All]**.

   1. Kopiera `/libs/ws/js/libs/jqueryui/jquery.ui.datepicker-ja.js` till `/apps/ws/js/libs/jqueryui`. Klicka på **[!UICONTROL Save All]**.

1. Gör följande för HTML-anpassningar:

   1. Under `/apps/ws/js`skapar du en mapp med namnet `runtime`. Klicka på **[!UICONTROL Save All]**.

   1. Under `/apps/ws/js/runtime`skapar du en mapp med namnet `templates`. Klicka på **[!UICONTROL Save All]**.

   1. Kopiera `/libs/ws/js/main.js` till `/apps/ws/js/main.js`.

   1. Kopiera /libs/ws/js/registry.js till `/apps/ws/js/registry.js`.

1. Klicka **[!UICONTROL Save All]** på, rensa cache och uppdatera arbetsytan i AEM Forms.

   Gå till URL:en `https://'[server]:[port]'/lc/ws` och logga in med administratörs-/lösenordsinformation. Webbläsaren dirigeras om till `https://'[server]:[port]'/lc/apps/ws/index.html`.
