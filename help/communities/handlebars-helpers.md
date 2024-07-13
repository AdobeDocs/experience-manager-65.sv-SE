---
title: Hjälpmedel för SCF-handtag
description: Hanteringsfält Hjälpmetoder som underlättar arbete med SCF
topic-tags: developing
content-type: reference
exl-id: bfb95cae-4b0f-4521-a113-042dc4005a63
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 1%

---

# Hjälpmedel för SCF-handtag {#scf-handlebars-helpers}

| **[⇐ Feature Essentials](essentials.md)** | **[Anpassning på serversidan¥](server-customize.md)** |
|---|---|
|   | **[Anpassning på klientsidan¥](client-customize.md)** |

Handlister Hjälpprogram är metoder som kan anropas från Handlebars-skript för att underlätta arbetet med SCF-komponenter.

Implementeringen innehåller en definition på klientsidan och en definition på serversidan. Det är också möjligt för utvecklare att skapa anpassade hjälpprogram.

De anpassade SCF-hjälpen som levereras med AEM Communities definieras i [klientbiblioteket](../../help/sites-developing/clientlibs.md):

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>Installera det [senaste funktionsmakropaketet för communityn](deploy-communities.md#latestfeaturepack).

## Förkortning {#abbreviate}

En hjälp som returnerar en förkortad sträng som uppfyller egenskaperna maxWords och maxLength.

Strängen som ska förkortas anges som kontext. Om ingen kontext anges returneras en tom sträng.

Först trimmas kontexten till maxLength och sedan delas kontexten upp i ord och reduceras till maxWords.

Om safeString är true är den returnerade strängen SafeString.

### Parametrar {#parameters}

* **context**: String

  (Valfritt) Standard är den tomma strängen

* **maxLength**: Number

  (Valfritt) Standard är längden på kontexten.

* **maxWords**: Number

  (Valfritt) Standard är antalet ord i den trimmade strängen.

* **safeString**: Boolean

  (Valfritt) Returnerar en Handlebars.SafeString() om true. Standardvärdet är false.

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

* **context**: String

  (Valfritt) Standard är den tomma strängen.

* **numChars**: Number

  (Valfritt) Det antal tecken som ska visas när inte den fullständiga texten visas. Standardvärdet är 100.

* **moreText**: String

  (Valfritt) Den text som ska visas anger att det finns mer text att visa. Standardvärdet är &quot;more&quot;.

* **ellipsesText**: String

  (Valfritt) Den text som ska visas anger att det finns dold text. Standardvärdet är &quot;..&quot;.

* **safeString**: Boolean

  (Valfritt) Ett booleskt värde som anger om Handlebars.SafeString() ska användas innan resultatet returneras. Standardvärdet är false.

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

* **context**: Number

  (Valfritt) en millisekundförskjutning från 1 januari 1970 (epok). Standard är aktuellt datum.

* **format**: Sträng

  (Valfritt) Datumformatet som ska användas. Standardvärdet är `YYYY-MM-DDTHH:mm:ss.sssZ` och resultatet visas som `2015-03-18T18:17:13-07:00`

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

* **lvalue**: String

  Det vänstra värdet som ska jämföras.

* **värde**: Sträng

  Högervärdet som ska jämföras.

### Exempel {#example-1}

```
{{#equals  value "some-value"}}
  <div>They are EQUAL!</div>
`{{else}}`
  <div>They are NOT equal!</div>
{{/equals}}
```

## If-wcm-mode {#if-wcm-mode}

En blockhjälp som testar det aktuella värdet för [WCM-läge](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) mot en strängavgränsad lista med lägen.

### Parametrar {#parameters-4}

* **context**: String

  (Valfritt) Den sträng som ska översättas. Obligatoriskt om inget standardvärde har angetts.

* **mode**: Sträng

  (Valfritt) En kommaavgränsad lista med [WCM-lägen](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) som ska testas om de anges.

### Exempel {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{else}}
 ...
`{{/if-wcm-mode}}`
```

## i18n {#i-n}

Den här hjälpen åsidosätter Handlebars help &#39;i18n&#39;.

Se även [Internationalisering av strängar i JavaScript Code](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code).

### Parametrar {#parameters-5}

* **context**: String

  (Valfritt) Den sträng som ska översättas. Obligatoriskt om inget standardvärde har angetts.

* **standard**: Sträng

  (Valfritt) Standardsträngen som ska översättas. Obligatoriskt om ingen kontext har angetts.

* **kommentar**: Sträng

  (Valfritt) Ett översättningstips

### Exempel {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## Inkludera {#include}

En hjälp som du kan använda för att inkludera en komponent som en icke-befintlig resurs i en mall.

Med den här metoden kan resursen anpassas programmatiskt enklare än vad som är möjligt för en resurs som lagts till som en JCR-nod. Se [Lägg till eller inkludera en webbgruppskomponent](scf.md#add-or-include-a-communities-component).

Det finns bara ett urval av webbgruppskomponenter att ta med. <!-- OBSOLETE/OLD  NEED TO UPDATE FOR 6.5  For AEM 6.1, those that are includable are [comments](essentials-comments.md), [rating](rating-basics.md), [reviews](reviews-basics.md), and [voting](essentials-voting.md). -->

Den här hjälpen, som bara är lämplig på serversidan, innehåller funktioner som liknar [cq:include](../../help/sites-developing/taglib.md) för JSP-skript.

### Parametrar {#parameters-6}

* **context**: Sträng eller objekt

  (Valfritt, såvida du inte anger en relativ sökväg)

  Använd `this` för att skicka den aktuella kontexten.

  Använd `this.id` för att hämta resursen på `id` för återgivning av begärd resourceType.

* **resourceType**: String

  (Valfritt) Resurstypen är som standard resurstyp från kontext.

* **template**: String

  Sökväg till komponentskript.

* **sökväg**: Sträng

  (Obligatoriskt) Sökvägen till resursen. Om sökvägen är relativ måste en kontext anges, annars returneras den tomma strängen.

* **authoringDisabled**: Boolean

  (Valfritt) Standardvärdet är false. Endast för internt bruk.

### Exempel {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

Innehåller en ny kommentarskomponent på `this.id` + /comments.

## IncludeClientLib {#includeclientlib}

En handledare som innehåller ett AEM HTML-klientbibliotek, som kan vara ett js, en css eller ett temabibliotek. Om flera inkluderingar av olika typer, till exempel js och css, ska den här taggen användas flera gånger i Handlebars-skriptet.

Den här hjälpen, som bara är lämplig på serversidan, innehåller funktioner som liknar [ui:includeClientLib](../../help/sites-developing/taglib.md) för JSP-skript.

### Parametrar {#parameters-7}

* **categories**: String

  (Valfritt) En lista med kommaavgränsade klientbibliotekskategorier. Inkludera alla JavaScript- och CSS-bibliotek för de angivna kategorierna. Temanamnet extraheras från begäran.

* **tema**: Sträng

  (Valfritt) En lista med kommaavgränsade klientbibliotekskategorier. Inkludera alla temarelaterade bibliotek (både CSS och JS) för de angivna kategorierna. Temanamnet extraheras från begäran.

* **js**: Sträng

  (Valfritt) En lista med kommaavgränsade klientbibliotekskategorier. Inkluderar alla JavaScript-bibliotek för de angivna kategorierna.

* **css**: Sträng

  (Valfritt) En lista med kommaavgränsade klientbibliotekskategorier. Inkluderar alla CSS-bibliotek för de angivna kategorierna.

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

Till exempel:

* För 12 timmar sedan
* 7 dagar sedan

### Parametrar {#parameters-8}

* **context**: Number

  Tidigare kunde man jämföra med&quot;now&quot;. Tiden uttrycks som en millisekundförskjutning från 1 januari 1970 (epok).

* **daysCutoff**: Number

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

En hjälp som kodar en källsträng för HTML-elementinnehåll för att skydda mot XSS.

OBS! Den här hjälpen är inte en validerare och ska inte användas för att skriva attributvärden.

### Parametrar {#parameters-9}

* **kontext**: objekt

  HTML som ska kodas.

### Exempel {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

En hjälpskrivare som kodar en källsträng för skrivning till ett HTML-attributvärde för att skydda mot XSS.

OBS! Den här hjälpen är inte en validerare och ska inte användas för att skriva åtgärdbara attribut (href, src, händelsehanterare).

### Parametrar {#parameters-10}

* **kontext**: Objekt

  HTML som ska kodas.

### Exempel {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

En hjälpare som kodar en källsträng för skrivning till JavaScript-stränginnehåll för att skydda mot XSS.

OBS! Den här hjälpen är inte en validerare och ska inte användas för att skriva till godtycklig JavaScript.

### Parametrar {#parameters-11}

* **kontext**: Objekt

  HTML som ska kodas.

### Exempel {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

En hjälp som sanerar en URL som kan skrivas som ett HTML href- eller srce-attributvärde för att skydda mot XSS.

OBS! Den här hjälpen kan returnera en tom sträng.

### Parametrar {#parameters-12}

* **kontext**: Objekt

  Den URL som ska saneras.

### Exempel {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Handlebars.js Basic Overview {#handlebars-js-basic-overview}

* Ett hjälpanrop till en handledare är en enkel identifierare (hjälpens *namn*) följt av noll eller flera mellanrumsavgränsade parametrar.
* Parametrar kan vara ett enkelt String-, number-, boolean- eller JSON-objekt och en valfri sekvens av nyckelvärdepar (hash-argument) som de sista parametrarna.
* Nycklarna i hash-argumenten måste vara enkla identifierare.
* Värdena i hash-argument är Handlebars-uttryck: enkla identifierare, sökvägar eller strängar.
* Den aktuella kontexten `this` är alltid tillgänglig för Handlebars-hjälpredor.
* Kontexten kan vara ett String-, number-, boolean- eller JSON-dataobjekt.
* Det går att skicka ett objekt som är kapslat i den aktuella kontexten som kontext, till exempel `this.url` eller `this.id` (se följande exempel på enkla och blockerade hjälpprogram).

* Blockhjälpredor är funktioner som kan anropas var som helst i mallen. De kan anropa ett mallblock noll eller flera gånger med olika kontext varje gång. De innehåller en kontext mellan `{{#*name*}}` och `{{/*name*}}`.

* Handtag ger en slutgiltig parameter till hjälpredor som heter &quot;options&quot;. Alternativobjektet innehåller

   * Valfria privata data (options.data)
   * Valfria nyckelvärdegenskaper från anropet (options.hash)
   * Möjlighet att anropa sig själv (options.fn())
   * Möjlighet att anropa den inverterade av sig själv (options.inverse())

* Vi rekommenderar att HTML String-innehåll som returneras från en hjälpfunktion är en SafeString.

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
var source = '<ul>`{{#posts}}`<li>{{{link_to "Post"}}}</li>`{{/posts}}`</ul>'

var template = Handlebars.compile(source);

template(context);
```

Återger:

&lt;ul>
&lt;li>&lt;a href=&quot;/post/hello-world&quot;>Post!&lt;/a>&lt;/li>
&lt;/ul>

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
var source = "<ul>`{{#people}}`<li>`{{#link}}``{{name}}``{{/link}}`</li>`{{/people}}`</ul>";

var template = Handlebars.compile(source);

template(data);
```

Återger:
&lt;ul>
&lt;li>&lt;a href=&quot;/people/1&quot;>Alan&lt;/a>&lt;/li>
&lt;li>&lt;a href=&quot;/people/2&quot;>Yehuda&lt;/a>&lt;/li>
&lt;/ul>

## Anpassade SCF-hjälpredor {#custom-scf-helpers}

Anpassade hjälpprogram måste implementeras på serversidan och klientsidan, särskilt när data skickas. För SCF kompileras och återges de flesta mallar på serversidan när servern genererar HTML för en viss komponent när sidan begärs.

### Anpassade hjälpmedel på serversidan {#server-side-custom-helpers}

Om du vill implementera och registrera en anpassad SCF-hjälp på serversidan implementerar du bara Java™-gränssnittet [TemplateHelper](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html), gör det till en [OSGi-tjänst](../../help/sites-developing/the-basics.md#osgi) och installerar det som en del av ett OSGi-paket.

Till exempel:

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

Hjälpprogrammen på klientsidan är Handlebars-skript som har registrerats genom att anropa `Handlebars.registerHelper()`.
Till exempel:

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

* Ta med ett beroende av `cq.social.scf`.
* Läs in när Hanterarfält har lästs in.
* Bli [inkluderad](clientlibs.md).

Obs! Hjälpprogrammen för SCF definieras i `/etc/clientlibs/social/commons/scf/helpers.js`.

| **[⇐ Feature Essentials](essentials.md)** | **[Anpassning på serversidan¥](server-customize.md)** |
|---|---|
|   | **[Anpassning på klientsidan¥](client-customize.md)** |
