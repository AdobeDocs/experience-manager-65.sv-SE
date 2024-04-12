---
title: Anpassa Adobe Analytics Framework
description: Lär dig hur du anpassar Adobe Analytics ramverk för Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: ab0d4f2e-f761-4510-ba51-4a2dcea49601
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Developer
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 0%

---

# Anpassa Adobe Analytics Framework{#customizing-the-adobe-analytics-framework}

Adobe Analytics-ramverket avgör vilken information som spåras med Adobe Analytics. Om du vill anpassa standardramverket använder du JavaScript för att lägga till anpassad spårning, integrera Adobe Analytics-plugin-program och ändra allmänna inställningar i det ramverk som används för spårning.

## Om genererad JavaScript för ramverk {#about-the-generated-javascript-for-frameworks}

När en sida är kopplad till ett Adobe Analytics-ramverk och sidan innehåller [referenser till analysmodulen](/help/sites-administering/adobeanalytics.md)skapas en analytics.sitecatalyst.js-fil automatiskt för sidan.

JavaScript-koden på sidan skapar en `s_gi`objekt (som definieras av Adobe Analytics-biblioteket s_code.js) och tilldelar värden till dess egenskaper. Namnet på objektinstansen är `s`. De kodexempel som presenteras i det här avsnittet innehåller flera referenser till det här `s` variabel.

Följande exempelkod liknar koden i en analytics.sitecatalyst.js-fil:

```
var s_account = "my_sitecatalyst_account";
var s = s_gi(s_account);
s.fpCookieDomainPeriods = "3";
s.currencyCode= 'USD';
s.trackInlineStats= true;
s.linkTrackVars= 'None';
s.charSet= 'UTF-8';
s.linkLeaveQueryString= false;
s.linkExternalFilters= '';
s.linkTrackEvents= 'None';
s.trackExternalLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.trackDownloadLinks= true;

s.visitorNamespace = "mynamespace";
s.trackingServer = "xxxxxxx.net";
s.trackingServerSecure = "xxxxxxx.net";

/* Plugin Config */
/*
s.usePlugins=false;
function s_doPlugins(s) {
    //add your custom plugin code here
}
s.doPlugins=s_doPlugins;
*/
```

När du använder anpassad JavaScript-kod för att anpassa ramverket ändrar du innehållet i den här filen.

## Konfigurera Adobe Analytics-egenskaper {#configuring-adobe-analytics-properties}

Det finns flera fördefinierade variabler i Adobe Analytics som kan konfigureras i ett ramverk. The **charset**, **cookieLifetime**, **currencyCode** och **trackInlineStats** variabler tas med i **Allmänna analysinställningar** som standard.

![aa-22](assets/aa-22.png)

Du kan lägga till variabelnamn och värden i listan. Dessa fördefinierade variabler och eventuella variabler som du lägger till används för att konfigurera egenskaperna för `s` i filen analytics.sitecatalyst.js. I följande exempel visas hur den tillagda `prop10` värdeegenskap `CONSTANT` representeras i JavaScript-koden:

```
var s_account = "my_sitecatalyst_account";
var s = s_gi(s_account);
s.fpCookieDomainPeriods = "3";
s.currencyCode= 'USD';
s.trackInlineStats= true;
s.linkTrackVars= 'None';
s.charSet= 'UTF-8';
s.linkLeaveQueryString= false;
s.linkExternalFilters= '';
s.linkTrackEvents= 'None';
s.trackExternalLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
s.prop10= 'CONSTANT';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.trackDownloadLinks= true;

s.visitorNamespace = "mynamespace";
s.trackingServer = "xxxxxxx.net";
s.trackingServerSecure = "xxxxxxx.net";
```

Använd följande procedur för att lägga till variabler i listan:

1. På din Adobe Analytics-ramverkssida kan du **Allmänna analysinställningar** område.
1. Under variabellistan klickar du på Lägg till objekt för att lägga till en ny variabel i listan.
1. I den vänstra cellen anger du ett namn för variabeln, till exempel: `prop10`.

1. I den högra kolumnen anger du ett värde för variabeln, till exempel: `CONSTANT`.

1. Om du vill ta bort en variabel klickar du på knappen (-) bredvid variabeln.

>[!NOTE]
>
>När du anger variabler och värden måste du se till att de är korrekt formaterade och stavade, eller **samtal skickas inte** med rätt värde/variabelpar. Felstavade variabler och värden kan till och med förhindra anrop.
>
>Kontakta din Adobe Analytics-representant för att kontrollera att dessa variabler är rätt inställda.

>[!CAUTION]
>
>Vissa variabler i den här listan är **obligatoriskt** för att Adobe Analytics-anrop ska fungera korrekt (till exempel **currencyCode**, **charSet**).
>
>Så även om de tas bort från själva ramverket kommer de fortfarande att få ett standardvärde när Adobe Analytics-anropet görs.

### Lägga till anpassad JavaScript i en Adobe Analytics Framework {#adding-custom-javascript-to-an-adobe-analytics-framework}

Den kostnadsfria JavaScript-rutan i **Allmänna analysinställningar** kan du lägga till anpassad kod i ett Adobe Analytics-ramverk.

![aa-21](assets/aa-21.png)

Koden som du lägger till läggs till i filen analytics.sitecatalyst.js. Därför kan du komma åt `s` variabel, som är en instans av `s_gi` JavaScript-objekt som definieras i `s_code.js`. Att lägga till följande kod motsvarar till exempel att lägga till en variabel med namnet `prop10` värde `CONSTANT`, som är exemplet i föregående avsnitt:

`s.prop10= 'CONSTANT';`

Koden i [analytics.sitecatalyst.js](/help/sites-developing/extending-analytics-components.md) som innehåller Adobe Analytics `s-code.js` -filen) innehåller följande kod:

`if (s.usePlugins) s.doPlugins(s)`

Följande procedur visar hur du använder JavaScript-rutan för att anpassa Adobe Analytics-spårning. Om ditt JavaScript behöver använda Adobe Analytics-plugin-program, [integrera dem](/help/sites-administering/adobeanalytics.md) till AEM.

1. Lägg till följande JavaScript-kod i rutan så att `s.doPlugins` körs:

   ```
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom code here
   }
   s.doPlugins=s_doPlugins;
   ```

   >[!CAUTION]
   >
   >Den här koden är nödvändig om du vill skicka variabler i ett Adobe Analytics-anrop som har anpassats på något sätt som inte går att göra via dra och släpp-gränssnittet ELLER via infogad JavaScript i Adobe Analytics View.
   >
   >Om de anpassade variablerna ligger utanför s_doPlugins-funktionen skickas de som *undefined *i Adobe Analytics-anropet

1. Lägg till din JavaScript-kod i **s_doPlugins** funktion.

I följande exempel sammanfogas de data som samlats in på en sida i hierarkisk ordning med hjälp av en gemensam avgränsare (|).

Ett Adobe Analytics-ramverk har följande konfigurationer:

* The `prop2` Adobe Analytics-variabeln mappas till `pagedata.sitesection` site-egenskap.

* The `prop3` Adobe Analytics-variabeln mappas till `pagedata.subsection` site-egenskap.

* Följande kod läggs till i den kostnadsfria JavaScript-rutan:

  ```
  s.usePlugins=true;
   function s_doPlugins(s) {
   s.prop1 = s.prop2+'|'+s.prop3;
   }
   s.doPlugins=s_doPlugins;
  ```

* När webbsidan som använder ramverket besöktes (eller, i redigeringsläge, sidan läses in igen eller förhandsgranskas), anropas Adobe Analytics.

Följande värden genereras till exempel i Adobe Analytics:

![aa-20](assets/aa-20.png)

### Lägga till global anpassad kod för alla Adobe Analytics-ramverk {#adding-global-custom-code-for-all-adobe-analytics-frameworks}

Skapa anpassad JavaScript-kod som är integrerad i alla Adobe Analytics ramverk. När en sidas Adobe Analytics-ramverk inte innehåller någon anpassad [JavaScript utan extra kostnad](/help/sites-administering/adobeanalytics.md), läggs det JavaScript som genereras av /libs/cq/analytics/components/sitecatalyst/config.js.jsp-skriptet till i [analytics.sitecatalyst.js](/help/sites-administering/adobeanalytics.md) -fil. Skriptet har som standard ingen effekt eftersom det kommenteras ut. Koden ställer också in `s.usePlugins` till `false`:

```
/* Plugin Config */
/*
s.usePlugins=false;
function s_doPlugins(s) {
    //add your custom plugin code here
}
s.doPlugins=s_doPlugins;
*/
```

Koden i filen analytics.sitecatalyst.js (som innehåller innehållet i Adobe Analytics-filen s_code.js) innehåller följande kod:

if (s.usePlugins) s.doPlugins(s)

Därför bör ditt JavaScript anges `s.usePlugins` till `true` så att all kod i `s_doPlugins` funktionen körs. Om du vill anpassa koden lägger du över config.js.jsp-filen med en som använder ditt eget JavaScript. Om ditt JavaScript behöver använda Adobe Analytics-plugin-program, [integrera dem](/help/sites-administering/adobeanalytics.md) till AEM.

>[!NOTE]
>
>Redigera inte filen /libs/cq/analytics/components/sitecatalyst/config.js.jsp. Vissa AEM uppgraderings- eller underhållsåtgärder kan installera om originalfilen och ta bort ändringarna.

1. I CRXDE Lite skapar du mappstrukturen /apps/cq/analytics/components:

   1. Högerklicka på mappen /apps och klicka på Create > Create Folder.
   1. Ange `cq` som mappnamn och klicka på OK.
   1. På samma sätt skapar du `analytics` och `components` mappar.

1. Högerklicka på `components` som du skapade och klickar på Skapa > Skapa komponent. Ange följande egenskapsvärden:

   * Etikett: `sitecatalyst`
   * Titel: `sitecatalyst`
   * Supertyp: `/libs/cq/analytics/components/sitecatalyst`
   * Grupp: `hidden`

1. Klicka på Nästa upprepade gånger tills knappen OK är aktiverad och klicka sedan på OK.

   Komponenten sitecatalyst innehåller den automatiskt skapade filen sitecatalyst.jsp.

1. Högerklicka på filen sitecatalyst.jsp och klicka på Ta bort.

1. Högerklicka på sitecatalyst-komponenten och klicka på Skapa > Skapa fil. Ange namnet `config.js.jsp` och klicka sedan på OK.

   config.js.jsp-filen öppnas automatiskt för redigering.

1. Lägg till följande text i filen och klicka sedan på Spara alla:

   ```java
   <%@page session="true"%>
   /* Plugin Config */
   s.usePlugins=true;
   function s_doPlugins(s) {
       //add your custom plugin code here
   }
   s.doPlugins=s_doPlugins;
   ```

   JavaScript-koden som genereras av /apps/cq/analytics/components/sitecatalyst/config.js.jsp-skriptet infogas nu i filen analytics.sitecatalyst.js för alla sidor som använder ett Adobe Analytics-ramverk.

1. Lägg till den JavaScript-kod som du vill köra i `s_doPlugins` och klicka sedan på Spara alla.

>[!CAUTION]
>
>Om det finns text i JavaScript-koden med valfri form i en sidas ramverk (även om bara tomt utrymme), ignoreras config.js.jsp.

### Använda Adobe Analytics Plugins i AEM {#using-adobe-analytics-plugins-in-aem}

Hämta JavaScript-koden för Adobe Analytics-plugin-program och integrera dem i ditt Adobe Analytics-ramverk i AEM. Lägg till koden i en biblioteksmapp i kategorin `sitecatalyst.plugins` så att de är tillgängliga för din anpassade JavaScript-kod.

Om du till exempel integrerar `getQueryParams` plugin-programmet kan du anropa plugin-programmet från `s_doPlugins` funktionen i det anpassade JavaScript-skriptet. Följande exempelkod skickar frågesträngen i **&quot;pid&quot;** från referentens URL som **eVar1**, när ett Adobe Analytics-samtal utlöses.

```
s.usePlugins=true;
function s_doPlugins(s) {
   // take the query string from the referrer
   s.eVar1=s.getQueryParam('pid','',document.referrer);
}
s.doPlugins=s_doPlugins;
```

AEM installerar följande Adobe Analytics-plugin-program så att de är tillgängliga som standard:

* getQueryParam()
* getPreviousValue()
* split()

Klientbiblioteksmappen /libs/cq/analytics/clientlibs/sitecatalyst/plugins innehåller dessa plugin-program i kategorin sitecatalyst.plugins.

>[!NOTE]
>
>Skapa en biblioteksmapp för dina plugin-program. Lägg inte till plugin-program i `/libs/cq/analytics/clientlibs/sitecatalyst/plugins` mapp. Detta säkerställer att du bidrar till `sitecatalyst.plugins` -kategorin skrivs inte över under AEM ominstallationer eller uppgraderingar.

Använd följande procedur för att skapa klientbiblioteksmappen för dina plugin-program. Du behöver bara utföra den här proceduren en gång. Om du vill lägga till ett plugin-program i klientbiblioteksmappen gör du följande.

1. Öppna CRXDE Lite i en webbläsare. ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))

1. Högerklicka på mappen /apps/my-app/clientlibs och klicka på Skapa > Skapa nod. Ange följande egenskapsvärden och klicka sedan på OK:

   * Namn: Ett namn på klientbiblioteksmappen, till exempel mina plugin-program

   * Typ: cq:ClientLibraryFolder

1. Markera klientbiblioteksmappen som du skapade och använd egenskapsfältet längst ned till höger för att lägga till följande egenskap:

   * Namn: kategorier
   * Typ: String
   * Värde: sitecatalyst.plugins
   * Flera: markerade

   Klicka på OK i redigeringsfönstret för att bekräfta egenskapsvärdet.

1. Högerklicka på klientbiblioteksmappen som du skapade och klicka på Skapa > Skapa fil. För filnamnstypen js.txt och klicka sedan på OK.

1. Klicka på Spara alla.

Använd följande procedur för att hämta plugin-programkoden, lagra koden i AEM och lägga till koden i klientbiblioteksmappen.

1. Logga in på [sc.omniture.com](https://sc.omniture.com/login/) med ditt Adobe Analytics-konto.
1. På landningssidan går du till Hjälp > Hjälp hemsida.
1. Klicka på Implementeringsplugin-program i innehållsförteckningen till vänster.
1. Klicka på länken till det plugin-program som du vill lägga till, och när sidan öppnas, leta reda på JavaScript-källkoden för plugin-programmet, markera koden och kopiera den.

1. Högerklicka på klientbiblioteksmappen och klicka på Skapa > Skapa fil. För filnamnet skriver du namnet på det plugin-program som du integrerar följt av .js och klickar sedan på OK. Om du till exempel integrerar plugin-programmet getQueryParam ger du filen namnet getQueryParam.js.

   När du skapar filen öppnas den för redigering.

1. Klistra in JavaScript-koden för plugin-programmet i filen, klicka på Spara alla och stäng sedan filen.

1. Öppna filen js.txt från klientbiblioteksmappen.

1. På en ny rad lägger du till namnet på filen som innehåller plugin-programmet, till exempel getQueryParam.js. Klicka sedan på Spara alla och stäng filen.

>[!NOTE]
>
>När du använder plugin-program måste du även integrera eventuella plugin-program som stöds, annars känner JavaScript-pluginprogrammet inte igen de anrop som görs till funktionerna i det plugin-program som stöds. Plugin-programmet getPreviousValue() kräver till exempel att plugin-programmet split() fungerar korrekt.
>
>Namnet på plugin-programmet måste läggas till i **js.txt** också.
