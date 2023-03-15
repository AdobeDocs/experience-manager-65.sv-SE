---
title: Allmänna steg för anpassning av AEM Forms arbetsyta
seo-title: Generic steps for AEM Forms workspace customization
description: Hur man kommer igång med att anpassa användargränssnittet i AEM Forms arbetsyta.
seo-description: How to get started customizing AEM Forms workspace user interface.
uuid: da6310b4-1c58-468d-85c6-975fd2c141f9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: dd3218c4-2bb2-40fc-9141-5823b0ea4224
docset: aem65
exl-id: 45e50b47-1b36-4937-9e1a-cc7bfb953861
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 2%

---

# Allmänna steg för anpassning av AEM Forms arbetsyta {#generic-steps-for-aem-forms-workspace-customization}

De allmänna stegen för att utföra anpassningar är:

1. Logga in på CRXDE Lite med åtkomst `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Skapa en `sling:Folder` mapp namngiven `ws` på `/apps`, om den inte finns. Skapa en `sling:Folder` mapp, högerklicka på `apps` mapp och markera **[!UICONTROL Create]** > **[!UICONTROL Create Node]**. Ange namnet som `ws`, välj text som `sling:Folder` och klicka **[!UICONTROL OK]**. Klicka på **[!UICONTROL Save All]**.
1. Bläddra till `/apps/ws`och navigera till **[!UICONTROL Access Control]** -fliken.
1. Välj **[!UICONTROL Repository]** alternativ. I **[!UICONTROL Access Control]** lista, klicka på **[!UICONTROL +]** för att lägga till en ny post. Klicka **[!UICONTROL +]** igen.
1. Sök och välj **PERM_WORKSPACE_USER** Huvudman.

   ![Välj PERM_WORKSPACE_USER som en del av de allmänna stegen för att anpassa arbetsytan i HTML](assets/perm_workspace_user.png)

1. Ge `jcr:read` Privilegium till rektorn.
1. Klicka på **[!UICONTROL Save All]**.
1. Kopiera `GET.jsp`, `index`och `html.jsp` filer från `/libs/ws` mapp till `/apps/ws` mapp.
1. Kopiera `/libs/ws/locales` i `/apps/ws` mapp. Klicka på **[!UICONTROL Save All]**.
1. Uppdatera referenserna och de relativa sökvägarna i `GET.jsp` som visas nedan och klicka på **[!UICONTROL Save all]**.

   ```javascript
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. Gör följande för CSS-anpassningar:

   1. Navigera till `/apps/ws` och skapa en ny mapp med namnet `css`.

   1. I `css` mapp, skapa en ny fil med namnet `newStyle.css`.

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
   >Placera posten för den användardefinierade CSS-filen efter posten för style.css, som visas ovan.

1. I /apps/ws/html.jsp

   ```jsp
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   till

   ```jsp
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. Gör följande:

   1. Skapa en mapp med namnet `js` på `/apps/ws`. Klicka på **[!UICONTROL Save All]**.

   1. Skapa en mapp med namnet `libs` på `/apps/ws/js`. Klicka på **[!UICONTROL Save All]**.

   1. Kopiera `/libs/ws/js/libs/jqueryui` mapp till `/apps/ws/js/libs`. Klicka på **[!UICONTROL Save All]**.

1. Gör följande för anpassning av HTML:

   1. Under `/apps/ws/js`, skapa en mapp med namnet `runtime`. Klicka på **[!UICONTROL Save All]**.

   1. Under `/apps/ws/js/runtime`, skapa en mapp med namnet `templates`. Klicka på **[!UICONTROL Save All]**.

   1. Kopiera `/libs/ws/js/main.js` till `/apps/ws/js/main.js`.

   1. Kopiera /libs/ws/js/registry.js till `/apps/ws/js/registry.js`.

1. Klicka **[!UICONTROL Save All]**, rensa cacheminne och uppdatera AEM Forms arbetsyta.

   Öppna URL:en `https://'[server]:[port]'/lc/ws` och logga in med inloggningsuppgifter för administratör/lösenord. Webbläsaren omdirigeras till `https://'[server]:[port]'/lc/apps/ws/index.html`.
