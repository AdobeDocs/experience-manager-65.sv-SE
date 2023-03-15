---
title: Integrera AEM Forms-arbetsytekomponenter i webbprogram
seo-title: Integrating AEM Forms workspace components in web applications
description: Hur du återanvänder AEM Forms arbetsytekomponenter i dina egna webbprogram för att utnyttja funktionaliteten och få en nära integrering.
seo-description: How to reuse AEM Forms workspace components in your own webapps to leverage functionality and provide tight integration.
uuid: bb9b8aa0-3f41-4f44-8eb7-944e778ee8a6
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6be87939-007e-42c7-8a41-e34ac2b8bed4
exl-id: bb4a500d-c34f-4586-83f0-ad7ef69b4fb1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# Integrera AEM Forms-arbetsytekomponenter i webbprogram {#integrating-aem-forms-workspace-components-in-web-applications}

Du kan använda arbetsytan i AEM Forms [komponenter](/help/forms/using/description-reusable-components.md) i ditt eget webbprogram. I följande exempelimplementering används komponenter från ett dev-paket för AEM Forms-arbetsytan som är installerat på en CRX™-instans för att skapa ett webbprogram. Anpassa lösningen nedan efter dina specifika behov. Exempelimplementeringen återanvänds `UserInfo`, `FilterList`och `TaskList`-komponenter i en webbportal.

1. Logga in i CRXDE Lite-miljön på `https://'[server]:[port]'/lc/crx/de/`. Kontrollera att du har ett AEM Forms Workspace-dev-paket installerat.
1. Skapa en bana `/apps/sampleApplication/wscomponents`.
1. Kopiera css, bilder, js/libs, js/runtime och js/registry.js

   * från `/libs/ws`
   * till `/apps/sampleApplication/wscomponents`.

1. Skapa en demomain.js-fil i mappen /apps/sampleApplication/wscomponents/js. Kopiera kod från /libs/ws/js/main.js till demomain.js.
1. I demomain.js tar du bort koden för att initiera Router och lägger till följande kod:

   ```javascript
   require(['initializer','runtime/util/usersession'],
       function(initializer, UserSession) {
           UserSession.initialize(
               function() {
                   // Render all the global components
                   initializer.initGlobal();
               });
       });
   ```

1. Skapa en nod under /content efter namn `sampleApplication` och text `nt:unstructured`. Lägg till `sling:resourceType` av typen String och value `sampleApplication`. Lägg till en post för i åtkomstkontrollistan för den här noden `PERM_WORKSPACE_USER` tillåt jcr:läsbehörighet. I åtkomstkontrollistan för `/apps/sampleApplication` lägg till en post för `PERM_WORKSPACE_USER` tillåt jcr:läsbehörighet.
1. I `/apps/sampleApplication/wscomponents/js/registry.js` uppdatera sökvägar från `/lc/libs/ws/` till `/lc/apps/sampleApplication/wscomponents/` för mallvärden.
1. På portalstartsidan finns JSP-filen på `/apps/sampleApplication/GET.jsp`lägger du till följande kod för att inkludera de nödvändiga komponenterna i portalen.

   ```jsp
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   Inkludera även de CSS-filer som krävs för AEM Forms arbetsytekomponenter.

   >[!NOTE]
   >
   >Varje komponent läggs till i komponenttaggen (med klasskomponent) vid återgivningen. Kontrollera att din hemsida innehåller dessa taggar. Se `html.jsp` fil med AEM Forms arbetsyta för att få mer information om dessa grundläggande kontrolltaggar.

1. Om du vill anpassa komponenterna kan du utöka de befintliga vyerna för den önskade komponenten enligt följande:

   ```javascript
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

1. Ändra portalens CSS för att konfigurera layout, placering och format för de nödvändiga komponenterna på portalen. Du vill till exempel behålla bakgrundsfärgen som svart för den här portalen för att kunna visa userInfo-komponenten på ett bra sätt. Du kan göra detta genom att ändra bakgrundsfärgen i `/apps/sampleApplication/wscomponents/css/style.css` enligt följande:

   ```css
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
