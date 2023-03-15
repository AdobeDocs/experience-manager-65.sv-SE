---
title: Skapa en ny inloggningsskärm
seo-title: Creating a new login screen
description: Så här ändrar du inloggningssidan för moduler i LiveCycle, till exempel AEM Forms Workspace eller Forms Manager.
seo-description: How-to modify the login page of LiveCycle modules, for example of AEM Forms workspace or Forms Manager.
uuid: 2d4a72f4-cc9a-412d-856d-0fca75f1272b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 35497785-263d-44b1-9ee4-85921997295b
docset: aem65
exl-id: 5cb906b6-6a3c-498c-94f5-27a9071ea934
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 4%

---

# Skapa en ny inloggningsskärm{#creating-a-new-login-screen}

Du kan ändra inloggningsskärmen för alla AEM Forms-moduler som använder inloggningsskärmen för AEM Forms. Ändringarna påverkar till exempel inloggningsskärmen för både Forms Manager och AEM Forms.

## Förutsättning {#prerequisite}

1. Logga in på `/lc/crx/de` med administratörsbehörighet.
1. Utför följande åtgärder:

   1. Replikera den hierarkiska strukturen: av `/libs/livecycle/core/content` på `/apps/livecycle/core/content`.

      Behåll samma egenskaper (nod/mapp) och åtkomstkontroll.

   1. Kopiera innehållsmappen:

      från: `/libs/livecycle/core`

      till: `/apps/livecycle/core`.

   1. Ta bort innehållet i `/apps/livecycle/core` mapp.

1. Utför följande åtgärder:

   1. Replikera den hierarkiska strukturen: av `/libs/livecycle/core/components/login` på `/apps/livecycle/core/components/login`. Behåll samma egenskaper (nod/mapp) och åtkomstkontroll.

   1. Kopiera komponentmappen: från `/libs/livecycle/core` till `/apps/livecycle/core`.

   1. Ta bort innehållet i mappen: `/apps/livecycle/core/components/login`.

### Lägga till en ny språkinställning {#adding-a-new-locale}

1. Kopiera `i18n` mapp:

   * från `/libs/livecycle/core/components/login`
   * till `/apps/livecycle/core/components/login`

1. Ta bort alla mappar i `i18n` förutom en, säg `en`.

1. I mappen `en`utför du följande åtgärder:

   1. Byt namn på mappen till det språknamn som du vill ha stöd för. Till exempel, `ar`.

   1. Ändra egenskapen `jcr:language` värde till `ar`(för `ar` mapp).
   >[!NOTE]
   >
   >Om språkinställningen är en kombination av språkkoder, till exempel `ar-DZ`ändrar du sedan mappnamnet och egenskapsvärdet till `ar-DZ`.

1. Kopiera `login.jsp`:

   * från `/libs/livecycle/core/components/login`
   * till `/apps/livecycle/core/components/login`

1. Ändra följande kodfragment för `/apps/livecycle/core/components/login/login.jsp`:

***Språkinställningen är språkkod***

```jsp
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
```

Till

```jsp
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

```jsp
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
```

Till

```jsp
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

```jsp
   String browserLocale = "en";
   for(int i=0; i<locales.length; i++)

   To

   String browserLocale = "ar";
   for(int i=0; i<locales.length; i++)
```

### Lägga till ny text eller ändra befintlig text {#adding-new-text-or-modifying-existing-text}

1. Kopiera `i18n` mapp:

   * från `/libs/livecycle/core/components/login`
   * till `/apps/livecycle/core/components/login`

1. Ändra nu värdet för egenskapen `sling:message` för noden (under den önskade språkkodsmappen) som du vill ändra texten för. Översättningen görs via nyckeln som anges i värdet av `sling:key` -egenskap för noden.

1. Utför följande åtgärder om du vill lägga till ett nytt nyckelvärdepar. Markera ett exempel i skärmbilden som följer.

   1. Skapa en nod av typen `sling:MessageEntry`, eller kopiera en befintlig nod och ändra namn på den, under alla språkmappar.
   1. Kopiera `login.jsp` :

      * från `/libs/livecycle/core/components/login`

      * till `/apps/livecycle/core/components/login`
   1. Ändra `/apps/livecycle/core/components/login/login.jsp` för att lägga till den nya texten.

   ![Lägg till nytt nyckelvärdepar](assets/capture_new.png)

   ```jsp
   div class="loginContent">
   
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

   Till

   ```jsp
   div class="loginContent">
   
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("My Welcome Message") %></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

### Lägga till ett nytt format eller ändra ett befintligt format {#adding-new-style-or-modifying-existing-style}

1. Kopiera `login` nod:

   * från `/libs/livecycle/core/content`
   * till `/apps/livecycle/core/content`

1. Ta bort filer `login.js` och `jquery-1.8.0.min.js`från noden `/apps/livecycle/core/content/login.`
1. Ändra formaten i CSS-filen.
1. Så här lägger du till nya format:

   1. Lägg till nya format i `/apps/livecycle/core/content/login/login.css`
   1. Kopiera `login.jsp`

      * från `/libs/livecycle/core/components/login`

      * till `/apps/livecycle/core/components/login`
   1. Ändra `/apps/livecycle/core/components/login/login.jsp` om du vill använda de nya formaten.



Till exempel:

* Lägg till följande i `/apps/livecycle/core/content/login/login.css`.

```
css.newLoginContentArea {
    width: 700px;
    padding: 100px 0px 0px 100px;
   }
```

* Ändra följande i `/apps/livecycle/core/components/login.jsp`.


   ```jsp
   <div class="loginContentArea">
   ```

   Till

   ```jsp
   <div class="newLoginContentArea">
   ```

>[!NOTE]
>
>Om de befintliga bilderna i `/apps/livecycle/core/content/login` (kopierad från `/libs/livecycle/core/content/login`) tas bort och därefter tas motsvarande referenser bort i CSS.

### Lägg till nya bilder {#add-new-images}

1. Följ stegen i Lägga till ett nytt format eller ändra ett befintligt format (dokumenteras ovan).
1. Lägg till nya bilder i `/apps/livecycle/core/content/login`. Så här lägger du till bild:

   1. Installera WebDAV-klienten.
   1. Navigera till `/apps/livecycle/core/content/login` mapp med hjälp av webDAV-klienten. Mer information finns i: [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

   1. Lägg till nya bilder.

1. Lägg till nya format i `/apps/livecycle/core/content/login/login.css,` motsvarar nya bilder som lagts till i `/apps/livecycle/core/content/login`.
1. Använd de nya formaten i `login.jsp` på `/apps/livecycle/core/components`.

Exempel:


```css
.newLoginContainerBkg {

 background-image: url(my_Bg.gif);
 background-repeat: no-repeat;
 background-position: left top;
 width: 727px;
}
```


    * Ändra följande i /apps/livecycle/core/components/login.jsp.

```jsp
<div class="loginContainerBkg">
```

Till

```jsp
<div class="newLginContainerBkg">
```
