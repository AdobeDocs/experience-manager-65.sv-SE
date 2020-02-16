---
title: Hjälpmedel för SCF-handtag
seo-title: Hjälpmedel för SCF-handtag
description: Hanteringsfält Hjälpmetoder som underlättar arbete med SCF
seo-description: Hanteringsfält Hjälpmetoder som underlättar arbete med SCF
uuid: 9c514199-871e-4b68-8147-2052d2eeda15
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8b6c1697-d693-41f4-8337-f41658465107
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Hjälpmedel för SCF-handtag {#scf-handlebars-helpers}

| **[⇐ - funktioner](essentials.md)** | **[Anpassning på serversidan](server-customize.md)** |
|---|---|
|  | **[Anpassning på klientsidan](client-customize.md)** |

Handlister Hjälpprogram är metoder som kan anropas från Handlebars-skript för att underlätta arbetet med SCF-komponenter.

Implementeringen innehåller en definition på klientsidan och en serversida. Det är också möjligt för utvecklare att skapa anpassade hjälpprogram.

De anpassade SCF-hjälprarna som levereras med AEM Communities definieras i [klientbiblioteket](../../help/sites-developing/clientlibs.md):

* /etc/clientlibs/social/commons/scf/helpers.js

>[!NOTE]
>
>Installera det [senaste funktionspaketet](deploy-communities.md#latestfeaturepack)för communityn.

## Förkortning {#abbreviate}

En hjälp som returnerar en förkortad sträng som uppfyller egenskaperna maxWords och maxLength.

Strängen som ska förkortas anges som kontext. Om inget sammanhang anges returneras en tom sträng.

Först trimmas kontexten till maxLength och sedan delas kontexten upp i ord och reduceras till maxWords.

Om safeString är true är den returnerade strängen SafeString.

### Parametrar {#parameters}

* **kontext**:Sträng

   (valfritt) Standard är den tomma strängen

* **maxLength**: Nummer

   (valfritt) Standard är längden på kontexten.

* **maxWords**: Nummer

   (valfritt) Standard är antalet ord i den trimmade strängen.

* **safeString**:Boolean

   (valfritt) Returnerar en Handlebars.SafeString() om true. Standardvärdet är false.

### Exempel {#examples}

```
{{abbreviate subject maxWords=2}}

/*
If subject =
    "AEM Communities - Site Creation Wizard"

Then abbreviate would return
    "AEM Communities".
*/
```

```
{{{abbreviate message safeString=true maxLength=30}}}

/*
If message =
    "The goal of AEM Communities is to quickly create a community engagement site."

Then abbreviate would return
    "The goal of AEM Communities is"
*/
```

## Content-loadMore {#content-loadmore}

Ett hjälpmedel för att lägga till två intervall under en div, ett för den fullständiga texten och det andra för den mindre texten, med möjlighet att växla mellan de två vyerna.

### Parametrar {#parameters-1}

* **kontext**:Sträng

   (valfritt) Default är den tomma strängen.

* **numChars**: Nummer

   (valfritt) Det antal tecken som ska visas när den fullständiga texten inte visas. Standardvärdet är 100.

* **moreText**:Sträng

   (valfritt) Texten som ska visas anger att det finns mer text att visa. Standardvärdet är &quot;more&quot;.

* **ellipsesText**:Sträng

   (valfritt) Den text som ska visas som indikation på dold text. Standardvärdet är &quot;..&quot;.

* **safeString**:Boolean

   (valfritt) Ett booleskt värde som anger om Handlebars.SafeString() ska användas eller inte innan resultatet returneras. Standardvärdet är false.

### Exempel {#example}

```
{{content-loadmore  context numChars=32  moreText="go on"  ellipsesText="..." }}

/*
If context =
    "Here is the initial less content and this is more content."

Then content-loadmore would return
    "Here is the initial less content<span class="moreelipses">...</span> <span class="scf-morecontent"><span>and this is more content.</span>  <a href="" class="scf-morelink" evt="click=toggleContent">go on</a></span>"
*/
```

## DateUtil {#dateutil}

En hjälp som returnerar en formaterad datumsträng.

### Parametrar {#parameters-2}

* **kontext**: Nummer

   (valfritt) en millisekundförskjutning från 1 januari 1970 (epok). Standard är aktuellt datum.

* **format**:Sträng

   (valfritt) Datumformatet som ska användas. Standardvärdet är &quot;YYY-MM-DDTHH:mm:ss.sssZ&quot; och resultatet visas som &quot;2015-03-18T18:17:13-07:00&quot;

### Exempel {#examples-1}

```
{{dateUtil this.memberSince format="dd MMM yyyy, hh:mm"}}

// returns "18 Mar 2015, 18:17"
```

```
{{dateUtil this.birthday format="MM-DD-YYYY"}}

// returns "03-18-2015"
```

## Lika med {#equals}

En hjälpfunktion som returnerar innehåll beroende på ett likhetsvillkor.

### Parametrar {#parameters-3}

* **lvalue**:Sträng

   Det vänstra värdet som ska jämföras

* **värde**:Sträng

   Högervärdet som ska jämföras

### Exempel {#example-1}

```
{{#equals  value "some-value"}}
  <div>They are EQUAL!</div>
{{else}}
  <div>They are NOT equal!</div>
{{/equals}}
```

## If-wcm-mode {#if-wcm-mode}

En blockhjälp som testar det aktuella värdet för [WCM-läget](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) mot en strängavgränsad lista med lägen.

### Parametrar {#parameters-4}

* **kontext**:Sträng

   (valfritt) Den sträng som ska översättas. Obligatoriskt om inget standardvärde har angetts.

* **läge**:Sträng

   (valfritt) En kommaseparerad lista med [WCM-lägen](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) som ska testas om de anges.

### Exempel {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{{else}}
 ...
{{/if-wcm-mode}}
```

## i18n {#i-n}

Den här hjälpen åsidosätter Handlebars help &#39;i18n&#39;.

Se även [Internationalisering av strängar i JavaScript-kod](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code).

### Parametrar {#parameters-5}

* **kontext**:Sträng

   (valfritt) Den sträng som ska översättas. Obligatoriskt om inget standardvärde har angetts.

* **standard**:Sträng

   (valfritt) Standardsträngen som ska översättas. Obligatoriskt om ingen kontext har angetts.

* **kommentar**:Sträng

   (valfritt) Ett översättningstips

### Exempel {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## Inkludera {#include}

En hjälp som du kan använda för att inkludera en komponent som en icke-befintlig resurs i en mall.

Detta gör att resursen kan anpassas programmatiskt enklare än vad som är möjligt för en resurs som lagts till som en JCR-nod. Se [Lägga till eller inkludera en webbgruppskomponent](scf.md#add-or-include-a-communities-component).

Endast ett urval av webbgruppskomponenter kan inkluderas. För AEM 6.1 är de som ingår [kommentarer](essentials-comments.md), [omdömen](rating-basics.md), [granskningar](reviews-basics.md)och [omröstningar](essentials-voting.md).

Den här hjälpen, som bara är lämplig på serversidan, innehåller funktioner som liknar [cq:include](../../help/sites-developing/taglib.md) för JSP-skript.

### Parametrar {#parameters-6}

* **kontext**: Sträng eller objekt

   (valfritt, såvida det inte finns en relativ sökväg)

   använd `this`för att skicka aktuell kontext

   använd `this.id` för att hämta resursen vid `id` återgivning av begärd resourceType

* **resourceType**:Sträng

   (valfritt) resurstypen blir standard för resurstypen från kontext

* **mall**:Sträng

   sökväg till komponentskript

* **sökväg**:Sträng

   (obligatoriskt) Sökvägen till resursen. Om sökvägen är relativ måste en kontext anges, annars returneras den tomma strängen.

* **authoringDisabled**:Boolean

   (valfritt) Standardvärdet är false. Endast för internt bruk.

### Exempel {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

Det här kommer att innehålla en ny kommentarkomponent på `this.id` + /comments

## IncludeClientLib {#includeclientlib}

En handledare som innehåller ett AEM html-klientbibliotek, som kan vara ett js, en css eller ett temabibliotek. För flera inkluderingar av olika typer, till exempel js och css, måste den här taggen användas flera gånger i Handlebars-skriptet.

Den här hjälpen, som bara är lämplig på serversidan, innehåller funktioner som liknar [ui:includeClientLib](../../help/sites-developing/taglib.md) för JSP-skript.

### Parametrar {#parameters-7}

* **kategorier**:Sträng

   (valfritt) En lista med kommaavgränsade klientbibliotekskategorier. Detta inkluderar alla JavaScript- och CSS-bibliotek för de angivna kategorierna. Temanamnet extraheras från begäran.

* **tema**:Sträng

   (valfritt) En lista med kommaavgränsade klientbibliotekskategorier. Detta inkluderar alla temarelaterade bibliotek (både CSS och JS) för de angivna kategorierna. Temanamnet extraheras från begäran.

* **js**:Sträng

   (valfritt) En lista med kommaavgränsade klientbibliotekskategorier. Detta inkluderar alla JavaScript-bibliotek för de angivna kategorierna.

* **css**:Sträng

   (valfritt) En lista med kommaavgränsade klientbibliotekskategorier. Detta inkluderar alla CSS-bibliotek för de angivna kategorierna.

### Exempel {#examples-2}

```
// all: js + theme (theme-js + css)
{{includeClientLib categories="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/socialgraph.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/socialgraph.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// only js libs
{{includeClientLib js="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/socialgraph.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// theme only (theme-js + css)
{{includeClientLib theme="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// css only
{{includeClientLib css="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/socialgraph.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
```

## Vackert {#pretty-time}

En hjälpfunktion som visar hur mycket tid som har gått upp till en brytpunkt, efter vilken ett vanligt datumformat visas.

Exempel:

* För 12 timmar sedan
* 7 dagar sedan

### Parametrar {#parameters-8}

* **kontext**: Nummer

   Tidigare kunde man jämföra med&quot;now&quot;. Tiden uttrycks som en millisekundförskjutning från 1 januari 1970 (epok).

* **daysCutoff**: Nummer

   Antalet dagar sedan innan du växlar till ett faktiskt datum. Standardvärdet är 60.

### Exempel {#example-5}

```
{{pretty-time this.published daysCutoff=7}}

/*
Depending on how long in the past, may return

  "3 minutes ago"

  "3 hours ago"

  "3 days ago"
*/
```

## Xss-html {#xss-html}

En handledare som kodar en källsträng för HTML-elementinnehåll för att skydda mot XSS.

OBS! det här är inte en validerare och ska inte användas för att skriva attributvärden.

### Parametrar {#parameters-9}

* **kontext**: object

   den HTML som ska kodas

### Exempel {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

En handledare som kodar en källsträng för skrivning till ett HTML-attributvärde för att skydda mot XSS.

OBS! det här är inte en validerare och ska inte användas för att skriva åtgärdbara attribut (href, src, händelsehanterare).

### Parametrar {#parameters-10}

* **kontext**: Objekt

   Den HTML som ska kodas

### Exempel {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

En hjälp som kodar en källsträng för skrivning till JavaScript-stränginnehåll för att skydda mot XSS.

OBS! detta är inte en validerare och ska inte användas för att skriva till godtycklig JavaScript.

### Parametrar {#parameters-11}

* **kontext**: Objekt

   Den HTML som ska kodas

### Exempel {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

En hjälpare som sanerar en URL för att skriva som ett HTML-href- eller srce-attributvärde för att skydda mot XSS.

OBS! detta kan returnera en tom sträng

### Parametrar {#parameters-12}

* **kontext**: Objekt

   Den URL som ska saneras

### Exempel {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Handlebars.js Basic Overview {#handlebars-js-basic-overview}

En snabb översikt över hjälpfunktioner i [Handlebars.js-dokumentationen](https://handlebarsjs.com/expressions.html):

* Ett Handlebars-anrop är en enkel identifierare (hjälpens *namn *) följt av noll eller flera blankstegsavgränsade parametrar.
* Parametrar kan vara ett enkelt String-, number-, boolean- eller JSON-objekt, samt en valfri sekvens av nyckelvärdepar (hash-argument) som den sista parametern/de sista.
* Nycklarna i hash-argumenten måste vara enkla identifierare.
* Värdena i hash-argument är Handlebars-uttryck: enkla identifierare, sökvägar eller strängar.
* Den aktuella kontexten, `this`, är alltid tillgänglig för HandleBar-hjälpredor.
* Kontexten kan vara ett String-, number-, boolean- eller JSON-dataobjekt.
* Det går att skicka ett objekt som är kapslat i det aktuella sammanhanget som kontext, till exempel `this.url` eller `this.id` (se exempel på enkla och blockerade hjälpprogram).

* Blockhjälpredor är funktioner som kan anropas var som helst i mallen. De kan anropa ett mallblock noll eller flera gånger med olika kontext varje gång. De innehåller en kontext mellan {{#*name*}} och {{/*name*}}.

* Handtag ger en slutgiltig parameter för hjälpredor med namnet&quot;options&quot;. Alternativobjektet innehåller

   * Valfria privata data (options.data)
   * Valfria nyckelvärdegenskaper från anropet (options.hash)
   * Möjlighet att anropa sig själv (options.fn())
   * Möjlighet att anropa den inverterade av sig själv (options.inverse())

* Vi rekommenderar att det HTML-stränginnehåll som returneras från en hjälpreda är en SafeString.

### Ett exempel på en enkel hjälp från Handlebars.js-dokumentationen: {#an-example-of-a-simple-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link_to', function(title, options) {
    return new Handlebars.SafeString('<a href="/posts' + this.url + '">' + title + "!</a>");
});

var context = {posts: [
    {url: "/hello-world",
      body: "Hello World!"}
  ] };

// when link_to is called, posts is the current context
var source = '<ul>{{#posts}}<li>{{{link_to "Post"}}}</li>{{/posts}}</ul>'

var template = Handlebars.compile(source);

template(context);
```

Återger:

&lt;ul>&lt;li>&lt;a href=&quot;/post/hello-world&quot;>Post!&lt;/a>&lt;/li>&lt;/ul>

### Ett exempel på en blockhjälp från Handlebars.js-dokumentationen: {#an-example-of-a-block-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link', function(options) {
    return new Handlebars.SafeString('<a href="/people/' + this.id + '">' + options.fn(this) + '</a>');
});

var data = { "people": [
  { "name": "Alan", "id": 1 },
  { "name": "Yehuda", "id": 2 }
]};

// when link is called, people is the current context
var source = "<ul>{{#people}}<li>{{#link}}{{name}}{{/link}}</li>{{/people}}</ul>";

var template = Handlebars.compile(source);

template(data);
```

Återger:
&lt;ul>&lt;li>&lt;a href=&quot;/people/1&quot;>Alan&lt;/a>&lt;/li>&lt;li>&lt;a href=&quot;/people/2&quot;>Yehuda&lt;/a>&lt;/li>&lt;/ul>

## Anpassade SCF-hjälpredor {#custom-scf-helpers}

Anpassade hjälpprogram måste implementeras både på serversidan och på klientsidan, särskilt när data skickas. För SCF kompileras och återges de flesta mallar på serversidan när servern genererar HTML-koden för en viss komponent när sidan begärs.

### Anpassade hjälpmedel på serversidan {#server-side-custom-helpers}

För att implementera och registrera en anpassad SCF-hjälp på serversidan behöver du bara implementera Java-gränssnittet [TemplateHelper](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html), göra det till en [OSGi-tjänst](../../help/sites-developing/the-basics.md#osgi) och installera den som en del av ett OSGi-paket.

Exempel:

### FooTextHelper.java {#footexthelper-java}

```java
/** Custom Handlebars Helper */

package com.my.helpers;

import java.io.IOException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

import com.adobe.cq.social.handlebars.api.TemplateHelper;
import com.github.jknack.handlebars.Options;

@Service
@Component
public class FooTextHelper implements TemplateHelper<String>{

    @Override
    public CharSequence apply(String context, Options options) throws IOException {
        return "foo-" + context;
    }

    @Override
    public String getHelperName() {
        return "foo-text";
    }

    @Override
    public Class<String> getContextType() {
        return String.class;
    }
}
```

>[!NOTE]
>
>En hjälp som skapats för serversidan måste också skapas för klientsidan.
>
>Komponenten återges på nytt på klientsidan för den inloggade användaren, och om hjälpen på klientsidan inte hittas försvinner komponenten.

### Anpassade hjälpmedel på klientsidan {#client-side-custom-helpers}

Hjälpprogram på klientsidan är Handlebars-skript som registreras genom anrop `Handlebars.registerHelper()`.
Exempel:

### custom-helpers.js {#custom-helpers-js}

```
function(Handlebars, SCF, $CQ) {

    Handlebars.registerHelper('foo-text', function(context, options) {
        if (!context) {
            return "";
        }
        return "foo-" + context;
    });

})(Handlebars, SCF, $CQ);
```

De anpassade hjälpfilerna på klientsidan måste läggas till i ett anpassat klientbibliotek.
Klientlib måste:

* Inkludera ett beroende på `cq.social.scf`
* Läs in efter att handtag har lästs in
* Bli [inkluderad](clientlibs.md)

Obs! SCF-hjälprarna definieras i `/etc/clientlibs/social/commons/scf/helpers.js`.

| **[⇐ - funktioner](essentials.md)** | **[Anpassning på serversidan](server-customize.md)** |
|---|---|
|  | **[Anpassning på klientsidan](client-customize.md)** |

