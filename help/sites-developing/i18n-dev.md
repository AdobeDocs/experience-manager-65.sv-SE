---
title: Internationaliserar gränssnittssträngar
seo-title: Internationalizing UI Strings
description: Med Java- och JavaScript-API:er kan du internationalisera strängar
seo-description: Java and JavaScript APIs enable you to internationalize strings
uuid: 1cfa409f-9b1e-466f-8b03-5628db42bc57
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 9da8823c-13a4-4244-bfab-a910a4fd44e7
exl-id: bc5b1cb7-a011-42fe-8759-3c7ee3068aad
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1100'
ht-degree: 0%

---

# Internationaliserar gränssnittssträngar {#internationalizing-ui-strings}

Med Java- och JavaScript-API:er kan du internationalisera strängar i följande typer av resurser:

* Java-källfiler.
* JSP-skript.
* JavaScript i klientbibliotek eller i sidkällan.
* Egenskapsvärden för JCR-nod som används i dialogrutor och komponentkonfigurationsegenskaper.

En översikt över internationalisering och lokalisering finns på [Internationalisering av komponenter](/help/sites-developing/i18n.md).

## Internationalisering av strängar i Java- och JSP-kod {#internationalizing-strings-in-java-and-jsp-code}

The `com.day.cq.i18n` Med Java-paketet kan du visa lokaliserade strängar i användargränssnittet. The `I18n` klassen innehåller `get` som hämtar lokaliserade strängar från AEM. Den enda obligatoriska parametern i `get` är stränglitteralen på engelska. Engelska är standardspråk för användargränssnittet. I följande exempel lokaliseras ordet `Search`:

`i18n.get("Search");`

Att identifiera strängen på det engelska språket skiljer sig från vanliga internationaliseringsramverk där ett ID identifierar en sträng och används för att referera till strängen vid körning. Att använda den engelska stränglitteralen ger följande fördelar:

* Kod är lätt att förstå.
* Strängen i standardspråket är alltid tillgänglig.

### Bestämma användarens språk {#determining-the-user-s-language}

Det finns två sätt att avgöra vilket språk användaren föredrar:

* För autentiserade användare anger du språket i inställningarna för användarkontot.
* Språkinställningen för den begärda sidan.

Användarkontots language-egenskap är den metod som rekommenderas eftersom den är mer tillförlitlig. Användaren måste dock vara inloggad för att kunna använda den här metoden.

#### Skapa Java-objektet I18n {#creating-the-i-n-java-object}

I18n-klassen innehåller två konstruktorer. Hur du avgör vilket språk användaren föredrar avgör vilken konstruktor som ska användas.

Om du vill visa strängen på det språk som anges i användarkontot använder du följande konstruktor (efter import `com.day.cq.i18n.I18n)`:

```java
I18n i18n = new I18n(slingRequest);
```

Konstruktorn använder `SlingHTTPRequest` för att hämta användarens språkinställning.

Om du vill använda sidans språkområde för att fastställa språket måste du först hämta ResourceBundle för den begärda sidans språk:

```java
Locale pageLang = currentPage.getLanguage(false);
ResourceBundle resourceBundle = slingRequest.getResourceBundle(pageLang);
I18n i18n = new I18n(resourceBundle);
```

#### Internationalisering av en sträng {#internationalizing-a-string}

Använd `get` metoden `I18n` objekt för att internationalisera en sträng. Den enda obligatoriska parametern i `get` -metoden är strängen som ska internationaliseras. Strängen motsvarar en sträng i en Translator-ordlista. get-metoden söker upp strängen i ordlistan och returnerar översättningen för det aktuella språket.

Det första argumentet i `get` Metoden måste följa följande regler:

* Värdet måste vara en stränglitteral. En variabel av typen `String` är inte acceptabelt.
* Stränglitteralen måste vara uttryck på en enda rad.
* Strängen är skiftlägeskänslig.

```xml
i18n.get("Enter a search keyword");
```

#### Använda översättningstips {#using-translation-hints}

Ange [översättningstips](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings) av den internationaliserade strängen för att skilja mellan dubblettsträngar i ordlistan. Använd den andra valfria parametern för `get` metod för att tillhandahålla översättningstips. Översättningstipset måste exakt matcha kommentaregenskapen för objektet i ordlistan.

Ordlistan innehåller till exempel strängen `Request` två gånger: en gång som ett verb och en gång som ett substantiv. I följande kod inkluderas översättningstipset som ett argument i `get` metod:

```java
i18n.get("Request","A noun, as in a request for a web page");
```

#### Inkludera variabler i lokaliserade meningar {#including-variables-in-localized-sentences}

Inkludera variabler i den lokaliserade strängen för att skapa sammanhangsbaserad betydelse i en mening. När du har loggat in i ett webbprogram visas till exempel meddelandet &quot;Welcome back Administrator&quot; på startsidan. Du har två meddelanden i din inkorg.&quot; Sidkontexten bestämmer användarnamnet och antalet meddelanden.

[I ordlistan](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings), representeras variablerna i strängar som index inom hakparenteser. Ange värdena för variablerna som argument för `get` -metod. Argumenten placeras efter översättningstipset och indexen motsvarar argumentens ordning:

```xml
i18n.get("Welcome back {0}. You have {1} messages.", "user name, number of messages", user.getDisplayName(), numItems);
```

Den internationaliserade strängen och översättningstipset måste exakt matcha strängen och kommentaren i ordlistan. Du kan utelämna lokaliseringstipset genom att ange en `null` som det andra argumentet.

#### Använda metoden Statisk hämtning {#using-the-static-get-method}

The `I18N` klassen definierar en statisk `get` -metod som är användbar när du behöver lokalisera ett litet antal strängar. Förutom parametrarna för ett objekts `get` -metoden kräver den statiska metoden `SlingHttpRequest` eller `ResourceBundle` som du använder, beroende på hur du avgör vilket språk som användaren föredrar:

* Använd användarens språkinställning: Ange SlingHttpRequest som den första parametern.

  `I18n.get(slingHttpRequest, "Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`
* Använd sidspråket: Ange ResourceBundle som den första parametern.

  `I18n.get(resourceBundle,"Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`

### Internationalisering av strängar i JavaScript-kod {#internationalizing-strings-in-javascript-code}

Med JavaScript API kan du lokalisera strängar på klienten. Som med [Java och JSP](#internationalizing-strings-in-java-and-jsp-code) JavaScript API gör att du kan identifiera strängar för att lokalisera, ge lokaliseringstips och ta med variabler i de lokaliserade strängarna.

The `granite.utils` [biblioteksmapp för klient](/help/sites-developing/clientlibs.md) innehåller JavaScript-API:t. Om du vill använda API:t inkluderar du den här klientbiblioteksmappen på sidan. Lokaliseringsfunktionerna använder `Granite.I18n` namnutrymme.

Innan du presenterar lokaliserade strängar måste du ange språkområdet med `Granite.I18n.setLocale` funktion. Funktionen kräver språkkoden för språkområdet som ett argument:

```
Granite.I18n.setLocale("fr");
```

Om du vill presentera en lokaliserad sträng använder du `Granite.I18n.get` funktion:

```
Granite.I18n.get("string to localize");
```

I följande exempel internationaliseras strängen &quot;Welcome back&quot;:

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("string to localize", [variables], "localization hint");
```

Funktionsparametrarna skiljer sig från Java I18n.get-metoden:

* Den första parametern är stränglitteralen som ska lokaliseras.
* Den andra parametern är en array med värden som ska matas in i stränglitteralen.
* Den tredje parametern är lokaliseringstipset.

I följande exempel används JavaScript för att lokalisera administratören för välkomstsidan. Du har två meddelanden i din inkorg.&quot; mening:

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("Welcome back {0}. You have {1} new messages in your inbox.", [username, numMsg], "user name, number of messages");
```

### Internationalisering av strängar från JCR-noder {#internationalizing-strings-from-jcr-nodes}

Gränssnittssträngar baseras ofta på egenskaper för JCR-noder. Till exempel `jcr:title` egenskapen för en sida används vanligtvis som innehållet i `h1` -element i sidkoden. The `I18n` klassen innehåller `getVar` metod för lokalisering av strängarna.

Följande exempel på JSP-skript hämtar `jcr:title` från databasen och visar den lokaliserade strängen på sidan:

```java
<% title = properties.get("jcr:title", String.class);%>
<h1><%=i18n.getVar(title) %></h1>
```

#### Ange översättningstips för JCR-noder {#specifying-translation-hints-for-jcr-nodes}

Liknar [översättningstips i Java API](#using-translation-hints)kan du ange översättningstips för att skilja på duplicerade strängar i ordlistan. Ange översättningstipset som en egenskap för noden som innehåller den internationaliserade egenskapen. Namnet på tipsegenskapen består av namnet på den internationaliserade egenskapen med namnet `_commentI18n` suffix:

`${prop}_commentI18n`

Till exempel en `cq:page` noden innehåller egenskapen jcr:title som lokaliseras. Tipset anges som värdet för egenskapen jcr:title_commentI18n.

### Testa täckningen för internationalisering {#testing-internationalization-coverage}

Testa om du har internationaliserat alla strängar i användargränssnittet. Om du vill se vilka strängar som täcks anger du användarspråket till zz_ZZ och öppnar användargränssnittet i webbläsaren. De internationaliserade strängarna visas med en stub-översättning i följande format:

`USR_*Default-String*_尠`

I följande bild visas stub-förflyttningen för AEM hemsida:

![chlimage_1](assets/chlimage_1a.jpeg)

Konfigurera språkegenskapen för inställningsnoden för användarkontot för att ställa in språket för användaren.

Noden preferences för en användare har en sökväg som den här:

`/home/users/<letter>/<hash>/preferences`

![chlimage_1-1](assets/chlimage_1-1a.jpeg)
