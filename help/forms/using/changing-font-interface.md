---
title: Ändra teckensnitt i gränssnittet
seo-title: Ändra teckensnitt i gränssnittet
description: Så här ändrar du teckensnitt i användargränssnittet selektivt.
seo-description: Så här ändrar du teckensnitt i användargränssnittet selektivt.
uuid: 421fdd24-441a-4092-8c52-f3ed3d5d5671
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 9fcb80b4-cbc2-48a5-afd1-4f3bc50bc503
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Ändra teckensnitt i gränssnittet{#changing-the-font-on-the-interface}

Du kan ändra teckensnittet som visas på arbetsytan i AEM Forms. Teckensnitt som används i ett visst avsnitt i användargränssnittet definieras i motsvarande avsnitt i formatmallen. Du kan ändra teckensnitten i användargränssnittet selektivt.

Följ de [allmänna stegen för anpassning](../../forms/using/generic-steps-html-workspace-customization.md) av arbetsytan i AEM Forms och följ stegen för anpassning av CSS, HTML eller båda, beroende på dina behov.

1. Ändra eller lägg till teckensnittsfamiljen i en befintlig stil.
1. Ändra eller lägg till infogad teckensnittsfamilj för HTML-elementet.
1. Lägg till ett format och använd det för HTML-elementet.

Om du till exempel vill ändra teckensnittet för den översta navigeringsfältets ankartext till Courier New följer du de här stegen:

1. Logga in på CRXDE Lite med åtkomst `https://[server]:[port]/lc/crx/de/index.jsp`.
1. Gör något av följande:

   1. Om du vill ändra font-family i en befintlig stil lägger du till följande i filen newStyle.css på /apps/ws/css.

      ```css
      #topnav a {
         font-family: "Courier New";
      }
      ```

   1. Om du vill lägga till teckensnittsfamiljen för HTML-elementet kopierar du filen till `/libs/ws/js/runtime/templates/appnavigation.html` `/apps/ws/js/runtime/templates/appnavigation.html`.

      Uppdatera /apps/ws/js/runtime/templates/appnavigation.html så här:

      ```
      <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
      <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.todo.name')%></a></li>
      <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
      <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
      ```

      Öppna /apps/ws/js/registry.js för redigering och ersättning `text!/lc/libs/ws/js/runtime/templates/appnavigation.html` med `text!/lc/apps/ws/js/runtime/templates/appnavigation.html`.

   1. Om du vill lägga till en stil som definierar teckensnittsfamiljen lägger du till följande i filen newStyle.css på /apps/ws/css.

      ```css
      .myNewFontStyle a {
         font-family: "Courier New";
      }
      ```

      Lägg till följande i filen appnavigation.html på /apps/ws/js/runtime/templates om du vill lägga till teckensnittsfamiljen för HTML-elementet.

      ```css
      <div id="topnav" class="myNewFontStyle">
          <ul>
              <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
              <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>"><%= $.t('index.header.topnav.todo.name')%></a></li>
              <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
              <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
          </ul>
      </div>
      ```

1. Starta om arbetsytan och rensa webbläsarcachen så att ändringarna syns.

![change_font_before](assets/change_font_before.png)

Övre navigeringsfält före teckensnittsanpassning

![change_font_after](assets/change_font_after.png)

Det övre navigeringsfältet efter teckensnittsanpassning på den första fliken

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
