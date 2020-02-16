---
title: Skapa en ny inloggningsskärm
seo-title: Skapa en ny inloggningsskärm
description: Hur man ändrar inloggningssidan för LiveCycle-moduler, till exempel arbetsytan i AEM Forms eller Forms Manager.
seo-description: Hur man ändrar inloggningssidan för LiveCycle-moduler, till exempel arbetsytan i AEM Forms eller Forms Manager.
uuid: 2d4a72f4-cc9a-412d-856d-0fca75f1272b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 35497785-263d-44b1-9ee4-85921997295b
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Skapa en ny inloggningsskärm{#creating-a-new-login-screen}

Du kan ändra inloggningsskärmen för alla AEM Forms-moduler som använder inloggningsskärmen i AEM Forms. Ändringarna påverkar till exempel inloggningsskärmen för både Forms Manager och AEM Forms.

## Förutsättning {#prerequisite}

1. Logga in `/lc/crx/de` med administratörsbehörighet.
1. Utför följande åtgärder:

   1. Replikera den hierarkiska strukturen: på `/libs/livecycle/core/content` kl `/apps/livecycle/core/content`. Behåll samma egenskaper (nod/mapp) och åtkomstkontroll.

   1. Kopiera innehållsmappen: från `/libs/livecycle/core` till `/apps/livecycle/core`.

   1. Ta bort innehållet i `/apps/livecycle/core` mappen.

1. Utför följande åtgärder:

   1. Replikera den hierarkiska strukturen: på `/libs/livecycle/core/components/login` kl `/apps/livecycle/core/components/login`. Behåll samma egenskaper (nod/mapp) och åtkomstkontroll.

   1. Kopiera komponentmappen: från `/libs/livecycle/core` till `/apps/livecycle/core`.

   1. Ta bort innehållet i mappen: `/apps/livecycle/core/components/login`.

### Lägga till en ny språkinställning {#adding-a-new-locale}

1. Kopiera `i18n` mappen:

   * from `/libs/livecycle/core/components/login`
   * to `/apps/livecycle/core/components/login`

1. Ta bort alla mappar inuti `i18n` utom en, till exempel `en`.
1. Utför följande åtgärder i mappen `en`:

   1. Byt namn på mappen till det språknamn som du vill ha stöd för. Exempel, `ar`.
   1. Ändra egenskapsvärdet `jcr:language` till `ar`(för `ar` mappen).
   >[!NOTE]
   >
   >Om språkinställningen är en kombination av språk och land, till exempel `ar-DZ`ändrar du mappnamnet och egenskapsvärdet till `ar-DZ`.

1. Kopiera `login.jsp`:

   * from `/libs/livecycle/core/components/login`
   * to `/apps/livecycle/core/components/login`

1. Ändra följande kodfragment för `/apps/livecycle/core/components/login/login.jsp`:

   ***Språkinställningen är språkkod***

   ```
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   
   To
   
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().startsWith("ar")) {
               browserLocale = "ar";
               break;
           }
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   ```

   ***Språkkoden är***

   ```
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   
   To
   
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().equalsIgnoreCase("ar-DZ")) {
               browserLocale = "ar-DZ";
               break;
           }
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   ```

   ***Ändra standardspråk***

   ```
   String browserLocale = "en";
   for(int i=0; i<locales.length; i++)
   
   To
   
   String browserLocale = "ar";
   for(int i=0; i<locales.length; i++)
   ```

### Lägga till ny text eller ändra befintlig text {#adding-new-text-or-modifying-existing-text}

1. Kopiera `i18n` mapp:

   * from `/libs/livecycle/core/components/login`
   * to `/apps/livecycle/core/components/login`

1. Ändra nu värdet på egenskapen för noden ( `sling:message` under den önskade språkkodsmappen) som du vill ändra texten för. Översättningen görs via den nyckel som anges i värdet för nodens `sling:key` egenskap.
1. Utför följande åtgärder om du vill lägga till ett nytt nyckelvärdepar. Markera ett exempel i skärmbilden som följer.

   1. Skapa en nod av typen `sling:MessageEntry`, eller kopiera en befintlig nod och byt namn på den, under alla språkmappar.
   1. Kopiera `login.jsp` :

      * from `/libs/livecycle/core/components/login`

      * to `/apps/livecycle/core/components/login`
   1. Ändra `/apps/livecycle/core/components/login/login.jsp` så att den nya texten läggs till.
   ![Lägg till nytt nyckelvärdepar](assets/capture_new.png)

   ```
   div class="loginContent">
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   
   To
   
   div class="loginContent">
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("My Welcome Message") %></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

### Lägga till ett nytt format eller ändra ett befintligt format {#adding-new-style-or-modifying-existing-style}

1. Kopiera `login` nod:

   * from `/libs/livecycle/core/content`
   * to `/apps/livecycle/core/content`

1. Ta bort filer `login.js` och `jquery-1.8.0.min.js`från noden `/apps/livecycle/core/content/login.`
1. Ändra formaten i CSS-filen.
1. Så här lägger du till nya format:

   1. Lägg till nya format i `/apps/livecycle/core/content/login/login.css`
   1. Kopiera `login.jsp`

      * from `/libs/livecycle/core/components/login`

      * to `/apps/livecycle/core/components/login`
   1. Ändra om du `/apps/livecycle/core/components/login/login.jsp` vill använda de nya formaten.


1. Exempel:

   * Lägg till följande i `/apps/livecycle/core/content/login/login.css`.

   ```css
   .newLoginContentArea {
    width: 700px;
    padding: 100px 0px 0px 100px;
   }
   ```

   * Ändra följande i /apps/livecycle/core/components/login.jsp.

   ```
   <div class="loginContentArea">
   
   To
   
   <div class="newLoginContentArea">
   ```

>[!NOTE]
>
>Om de befintliga bilderna i `/apps/livecycle/core/content/login` (kopieras från `/libs/livecycle/core/content/login`) tas bort, tar du bort motsvarande referenser i CSS.

### Lägg till nya bilder {#add-new-images}

1. Följ stegen i Lägga till nytt format eller ändra befintligt format (dokumenteras ovan).
1. Lägg till nya bilder i `/apps/livecycle/core/content/login`. Så här lägger du till bild:

   1. Installera WebDAV-klienten.
   1. Navigera till `/apps/livecycle/core/content/login` mapp med hjälp av webDAV-klienten. Mer information finns i: [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

   1. Lägg till nya bilder.

1. Lägg till nya format i `/apps/livecycle/core/content/login/login.css,` som motsvarar nya bilder som lagts till i `/apps/livecycle/core/content/login`.
1. Använd de nya formaten i `login.jsp``/apps/livecycle/core/components`.
1. Exempel:

   * Lägg till följande i `/apps/livecycle/core/content/login/login.css`

   ```css
   .newLoginContainerBkg {
    background-image: url(my_Bg.gif);
    background-repeat: no-repeat;
    background-position: left top;
    width: 727px;
   }
   ```

   * Ändra följande i /apps/livecycle/core/components/login.jsp.

   ```
   <div class="loginContainerBkg">
   
   To
   
   <div class="newLginContainerBkg">
   ```

[Kontakta supporten](https://www.adobe.com/account/sign-in.supportportal.html)
