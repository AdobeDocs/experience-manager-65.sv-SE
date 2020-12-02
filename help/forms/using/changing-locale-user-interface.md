---
title: Ändra språkområdet för användargränssnittet i AEM Forms arbetsyta
seo-title: Ändra språkområdet för användargränssnittet i AEM Forms arbetsyta
description: Så här ändrar du arbetsytan i AEM Forms för att lokalisera text, komprimerade kategorier, köer och processer samt datumväljaren i gränssnittet.
seo-description: Så här ändrar du arbetsytan i AEM Forms för att lokalisera text, komprimerade kategorier, köer och processer samt datumväljaren i gränssnittet.
uuid: c89ff150-a36e-45cc-99a6-8768dbe58eab
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 89f9d666-28e2-4201-8467-ae90693ca5d2
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---


# Ändra språkinställningen för användargränssnittet för arbetsytan i AEM Forms{#changing-the-locale-of-aem-forms-workspace-user-interface}

AEM Forms arbetsyta har stöd för engelska, franska, tyska och japanska. Det gör det även möjligt att lokalisera användargränssnittet för AEM Forms-arbetsytan till andra språk.

Så här lokaliserar du användargränssnittet för AEM Forms-arbetsytan till det språk du vill:

* Lokalisera texten på arbetsytan i AEM Forms.
* Lokalisera dolda kategorier, köer och processer.
* Lokalisera datumväljare

Innan du utför ovanstående steg måste du följa de steg som anges i [Allmänna steg för anpassning av AEM Forms-arbetsytan](../../forms/using/generic-steps-html-workspace-customization.md).

>[!NOTE]
>
>Information om hur du ändrar språk för inloggningsskärmen i AEM Forms finns i [Skapa en ny inloggningsskärm](../../forms/using/creating-new-login-screen.md).

## Lokaliserar text {#localizing-text}

Utför följande steg för att lägga till stöd för språket *Nytt* och webbläsarens språkkod *nw*.

1. Logga in på CRXDE Lite.
Standardwebbadressen för CRXDE Lite är `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Navigera till platsen `apps/ws/locales` och skapa en ny mapp `nw.`
1. Kopiera filen `translation.json`från platsen `/apps/ws/locales/en-US` till platsen `/apps/ws/locales/nw`.
1. Navigera till `/apps/ws/locales/nw` och öppna `translation.json` för redigering. Gör språkspecifika ändringar i filen translation.json.

   Följande exempel innehåller filen translation.json för engelska och franska i AEM Forms arbetsyta.

   ![translation_json_in_](assets/translation_json_in_en.png) ![entranslation_json_in_fr](assets/translation_json_in_fr.png)

## Lokalisera komprimerade kategorier, köer och processer {#localizing-collapsed-categories-queues-and-processes}

På arbetsytan i AEM Forms används bilder för att visa rubriker för kategorier, köer och processer. Du behöver ett utvecklingspaket för att lokalisera dessa rubriker. Mer information om hur du skapar utvecklingspaket finns i [Skapa AEM Forms-arbetsytekod.](introduction-customizing-html-workspace.md#building-html-workspace-code).

I följande steg antas de nya lokaliserade bildfilerna vara *Categories_nw.png*, *Queue_nw.png* och *Processes_nw.png*. Bildernas rekommenderade bredd är 19px.

>[!NOTE]
>
>För att hitta språkkoden för webbläsaren. Öppna `https://'[server]:[port]'/lc/libs/ws/Locale.html`.

![collapsing_panels_image](assets/collapsing_panels_image.png)

Utför följande steg för att lokalisera bilderna:

1. Placera bildfilerna i mappen */apps/ws/images* med en WebDAV-klient.
1. Navigera till */apps/ws/css*. Öppna *newStyle.css* för att redigera och lägga till följande poster:

   ```css
   #categoryListBar .content.nw {
        background: #3e3e3e url(../images/Categories_nw.png) no-repeat 10px 10px;
    }
   
   #filterListBar .content.nw {
       background: #3e3e3e url(../images/Queues_nw.png) no-repeat 10px 10px;
   }
   
   #processNameListBar .content.nw {
       background: #3e3e3e url(../images/Processes_nw.png) no-repeat 10px 10px;
   }
   ```

1. Utför alla semantiska ändringar som listas i artikeln [Anpassa arbetsytan](../../forms/using/introduction-customizing-html-workspace.md).
1. Navigera till mappen *js/runtime/utility* och öppna filen *usersession.js* för redigering.
1. Leta reda på koden i det ursprungliga kodblocket och lägg till villkoret *lang !== &#39;nw&#39;* till if-satsen:

   ```javascript
   // Orignal code
   setLocale = function () {
           var lang = $.trim(i18n.lng());
           if (lang === null || lang === '' || (lang !== 'fr-FR' && lang !== 'de-DE' && lang !== 'ja-JP')) {
               window.lcWorkspace.locale = 'en-US';
           } else {
               window.lcWorkspace.locale = lang;
           }
       }
   ```

   ```javascript
   //new code
    setLocale = function () {
           var lang = $.trim(i18n.lng());
           if (lang === null || lang === '' || (lang !== 'fr-FR' && lang !== 'de-DE' && lang !== 'ja-JP' && lang !== 'nw')) {
               window.lcWorkspace.locale = 'en-US';
           } else {
               window.lcWorkspace.locale = lang;
           }
       }
   ```

## Lokaliserar datumväljaren {#localizing-date-picker}

Du behöver ett utvecklingspaket för att lokalisera API:t *datepicker*. Mer information om hur du skapar utvecklingspaket finns i [Bygga AEM Forms-arbetsytekod](introduction-customizing-html-workspace.md#building-html-workspace-code).

1. Hämta och extrahera [jQuery-gränssnittspaketet](https://jqueryui.com/download/all/), navigera till *&lt;extraherat jQuery-gränssnittspaket>*\jquery-ui-1.10.2.zip\jquery-ui-1.10.2\ui\i18n.
1. Kopiera filen jquery.ui.datepicker-nw.js för språkkod nu till apps/ws/js/libs/jqueryui och gör språkspecifika ändringar i filen.
1. Navigera till `apps/ws/js` och öppna `jquery.ui.datepicker-nw.js`-filen för redigering.
1. I filen main.js skapar du ett alias för `jquery.ui.datepicker-nw.js.` Koden som skapar ett alias för filen `jquery.ui.datepicker-nw.js` är:

   ```javascript
   jqueryuidatepickernw : pathprefix + 'libs/jqueryui/jquery.ui.datepicker-nw'
   ```

1. Använd aliaset `jqueryuidatepickernw` om du vill ta med filen `jquery.ui.datepicker-nw.js` i alla filer som använder datumväljaren. Datepicker används i följande filer:

   * `js/runtime/views/outofoffice.js`
   * `js/runtime/views/searchtemplatedetails.js`

   I exempelkoden nedan visas hur du lägger till posten för jquery.ui.datepicker-nw.js:

   ```json
   //Original Code
   define([
       'jquery',
       'underscore',
       'backbone',
       'jqueryui',
       'jqueryuidatepickerja',
       'jqueryuidatepickerde',
       'jqueryuidatepickerfr',
       'slimscroll',
       'usersearchview',
       'logmanagerutil',
       'loggerutil'
   ], function ($, _, Backbone, jQueryUI, jQueryUIDatePickerJA, jQueryUIDatePickerDE, jQueryUIDatePickerFR, slimScroll, UserSearch, LogManager, Logger) {
   ```

   ```json
   // Code with Date Picker alias for new language
   define([
       'jquery',
       'underscore',
       'backbone',
       'jqueryui',
       'jqueryuidatepickerja',
       'jqueryuidatepickerde',
       'jqueryuidatepickerfr',
       'jqueryuidatepickernw', // Date Picker alias
       'slimscroll',
       'usersearchview',
       'logmanagerutil',
       'loggerutil'
   ], function ($, _, Backbone, jQueryUI, jQueryUIDatePickerJA, jQueryUIDatePickerDE, jQueryUIDatePickerFR, jQueryUIDatePickerNW, slimScroll, UserSearch, LogManager, Logger) {
   ```

1. I alla filer som använder API:t för datumväljaren ändrar du standardinställningarna för API:t för datumväljaren. API:t för datumväljaren används i följande filer:

   * apps\ws\js\runtime\views\searchtemplatedetails.js
   * apps\ws\js\runtime\views\outofoffice.js

   Ändra följande kod för att lägga till den nya språkinställningen:

   ```javascript
   if (locale === 'ja-JP') {
      $.datepicker.setDefaults($.datepicker.regional.ja);
   } else if (locale === 'de-DE') {
      $.datepicker.setDefaults($.datepicker.regional.de);
   } else if (locale === 'fr-FR') {
      $.datepicker.setDefaults($.datepicker.regional.fr);
   } else {
      $.datepicker.setDefaults($.datepicker.regional['']);
   }
   ```

   ```javascript
   if (locale === 'ja-JP') {
       $.datepicker.setDefaults($.datepicker.regional.ja);
   } else if (locale === 'de-DE') {
       $.datepicker.setDefaults($.datepicker.regional.de);
   } else if (locale === 'fr-FR') {
       $.datepicker.setDefaults($.datepicker.regional.fr);
   } else if (locale === 'nw') {
       $.datepicker.setDefaults($.datepicker.regional.nw);
   } else {
       $.datepicker.setDefaults($.datepicker.regional['']);
   }
   ```
