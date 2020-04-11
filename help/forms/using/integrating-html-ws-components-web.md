---
title: Integrera AEM Forms-arbetsytekomponenter i webbprogram
seo-title: Integrera AEM Forms-arbetsytekomponenter i webbprogram
description: Hur du återanvänder AEM Forms-arbetsytekomponenter i dina egna webbprogram för att utnyttja funktionaliteten och få en nära integrering.
seo-description: Hur du återanvänder AEM Forms-arbetsytekomponenter i dina egna webbprogram för att utnyttja funktionaliteten och få en nära integrering.
uuid: bb9b8aa0-3f41-4f44-8eb7-944e778ee8a6
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6be87939-007e-42c7-8a41-e34ac2b8bed4
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Integrera AEM Forms-arbetsytekomponenter i webbprogram {#integrating-aem-forms-workspace-components-in-web-applications}

Du kan använda [komponenter](/help/forms/using/description-reusable-components.md) på arbetsytan för AEM Forms i ditt eget webbprogram. The following sample implementation uses components from an AEM Forms workspace dev package installed on a CRX™ instance to create a web application. Anpassa lösningen nedan efter dina specifika behov. Exempelimplementeringen återanvänder `UserInfo`, `FilterList`och `TaskList`komponenter i en webbportal.

1. Logga in i CRXDE Lite-miljön på `https://'[server]:[port]'/lc/crx/de/`. Kontrollera att du har ett AEM Forms-arbetsytedev-paket installerat.
1. Skapa en bana `/apps/sampleApplication/wscomponents`.
1. Kopiera css, bilder, js/libs, js/runtime och js/registry.js

   * from `/libs/ws`
   * to `/apps/sampleApplication/wscomponents`.

1. Skapa en demomain.js-fil i mappen /apps/sampleApplication/wscomponents/js. Kopiera kod från /libs/ws/js/main.js till demomain.js.
1. I demomain.js tar du bort koden för att initiera Router och lägger till följande kod:

   ```
   require(['initializer','runtime/util/usersession'],
       function(initializer, UserSession) {
           UserSession.initialize(
               function() {
                   // Render all the global components
                   initializer.initGlobal();
               });
       });
   ```

1. Skapa en nod under /content efter namn `sampleApplication` och typ `nt:unstructured`. I egenskaperna för den här noden lägger du till `sling:resourceType` typen String och value `sampleApplication`. I åtkomstkontrollistan för den här noden lägger du till en post för `PERM_WORKSPACE_USER` att tillåta jcr:läsbehörighet. I åtkomstkontrollistan lägger du även till en post för `/apps/sampleApplication` att `PERM_WORKSPACE_USER` tillåta jcr:läsbehörighet.
1. I `/apps/sampleApplication/wscomponents/js/registry.js` Uppdatera sökvägar från `/lc/libs/ws/` till `/lc/apps/sampleApplication/wscomponents/` för mallvärden.
1. I JSP-filen på portalstartsidan `/apps/sampleApplication/GET.jsp`lägger du till följande kod för att inkludera de nödvändiga komponenterna i portalen.

   ```as3
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   Inkludera även de CSS-filer som krävs för AEM Forms-arbetsytekomponenter.

   >[!NOTE]
   >
   >Each component is added to the component tag (having class gcomponent) while rendering. Kontrollera att din hemsida innehåller dessa taggar. Mer information om de här grundläggande kontrolltaggarna finns i filen för `html.jsp` arbetsytan i AEM Forms.

1. Om du vill anpassa komponenterna kan du utöka de befintliga vyerna för den önskade komponenten enligt följande:

   ```as3
   define([
       ‘jquery’,
       ‘underscore’,
       ‘backbone’,
       ‘runtime/views/userinfo'],
       function($, _, Backbone, UserInfo){
           var demoUserInfo = UserInfo.extend({
               //override the functions to customize the functionality
               render: function() {
                   UserInfo.prototype.render.call(this); // call the render function of the super class
                   …
                   //other tasks
                   …
               }
           });
           return demoUserInfo;
   });
   ```

1. Ändra portalens CSS för att konfigurera layout, placering och format för de nödvändiga komponenterna på portalen. Du vill till exempel behålla bakgrundsfärgen som svart för den här portalen för att kunna visa userInfo-komponenten på ett bra sätt. Du kan göra detta genom att ändra bakgrundsfärgen i `/apps/sampleApplication/wscomponents/css/style.css` följande:

   ```as3
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
