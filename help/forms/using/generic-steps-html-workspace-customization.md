---
title: Allmänna steg för anpassning av AEM Forms arbetsyta
seo-title: Allmänna steg för anpassning av AEM Forms arbetsyta
description: Hur man kommer igång med att anpassa användargränssnittet i AEM Forms arbetsyta.
seo-description: Hur man kommer igång med att anpassa användargränssnittet i AEM Forms arbetsyta.
uuid: da6310b4-1c58-468d-85c6-975fd2c141f9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: dd3218c4-2bb2-40fc-9141-5823b0ea4224
docset: aem65
translation-type: tm+mt
source-git-commit: e863089a4328b7222b60429c82ca3df2b8e1dd05
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 2%

---


# Allmänna steg för anpassning av arbetsytan i AEM Forms {#generic-steps-for-aem-forms-workspace-customization}

De allmänna stegen för att utföra anpassningar är:

1. Logga in på CRXDE Lite med `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Skapa en `sling:Folder`-mapp med namnet `ws` på `/apps`, om den inte finns. Om du vill skapa en `sling:Folder`-mapp högerklickar du på mappen `apps` och väljer **[!UICONTROL Create]** > **[!UICONTROL Create Node]**. Ange namnet som `ws`, välj typen `sling:Folder` och klicka på **[!UICONTROL OK]**. Klicka på **[!UICONTROL Save All]**.
1. Bläddra till `/apps/ws` och navigera till fliken **[!UICONTROL Access Control]**.
1. Välj alternativet **[!UICONTROL Repository]**. Klicka på **[!UICONTROL +]** i listan **[!UICONTROL Access Control]** för att lägga till en ny post. Klicka på **[!UICONTROL +]** igen.
1. Sök efter och välj **PERM_WORKSPACE_USER** Principal.

   ![Välj PERM_WORKSPACE_USER som en del av de allmänna stegen för att anpassa HTML-arbetsytan](assets/perm_workspace_user.png)

1. Ge `jcr:read` privilegium till huvudmannen.
1. Klicka på **[!UICONTROL Save All]**.
1. Kopiera filerna `GET.jsp`, `index` och `html.jsp` från mappen `/libs/ws` till mappen `/apps/ws`.
1. Kopiera mappen `/libs/ws/locales` i mappen `/apps/ws`. Klicka på **[!UICONTROL Save All]**.
1. Uppdatera referenserna och de relativa sökvägarna i `GET.jsp`-filen enligt nedan och klicka på **[!UICONTROL Save all]**.

   ```javascript
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. Gör följande för CSS-anpassningar:

   1. Navigera till mappen `/apps/ws` och skapa en ny mapp med namnet `css`.

   1. Skapa en ny fil med namnet `newStyle.css` i mappen `css`.

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

   1. Kopiera mappen `/libs/ws/js/libs/jqueryui` till `/apps/ws/js/libs`. Klicka på **[!UICONTROL Save All]**.

1. Gör följande för HTML-anpassningar:

   1. Skapa en mapp med namnet `runtime` under `/apps/ws/js`. Klicka på **[!UICONTROL Save All]**.

   1. Skapa en mapp med namnet `templates` under `/apps/ws/js/runtime`. Klicka på **[!UICONTROL Save All]**.

   1. Kopiera `/libs/ws/js/main.js` till `/apps/ws/js/main.js`.

   1. Kopiera /libs/ws/js/registry.js till `/apps/ws/js/registry.js`.

1. Klicka på **[!UICONTROL Save All]**, rensa cache och uppdatera AEM Forms-arbetsytan.

   Gå till URL:en `https://'[server]:[port]'/lc/ws` och logga in med autentiseringsuppgifter för administratör/lösenord. Webbläsaren omdirigeras till `https://'[server]:[port]'/lc/apps/ws/index.html`.
