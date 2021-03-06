---
title: Konfigurerar cookie-användning
seo-title: Konfigurerar cookie-användning
description: AEM tillhandahåller en tjänst som gör att du kan konfigurera och styra hur cookies används på dina webbsidor
seo-description: AEM tillhandahåller en tjänst som gör att du kan konfigurera och styra hur cookies används på dina webbsidor
uuid: 10d95176-0a56-41f1-9d36-01dbdac757d4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 5773ec1a-f15b-462d-8f9f-54ee1d7ead44
translation-type: tm+mt
source-git-commit: f64eb57a69f2124523bd6eaed3e2f58a54c1ea8e
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 2%

---


# Konfigurerar cookie-användning{#configuring-cookie-usage}

AEM tillhandahåller en tjänst som gör att du kan konfigurera och styra hur cookies används med dina webbsidor:

* En konfigurerbar tjänst på serversidan upprätthåller en lista över cookies som kan användas.
* Med ett javascript-API kan din javascript-kod verifiera att en cookie kan användas.

Använd den här funktionen för att kontrollera att sidorna uppfyller användarnas samtycke när det gäller användningen av cookies.

## Konfigurerar tillåtna cookies {#configuring-allowed-cookies}

Konfigurera avanmälningstjänsten för Adobe Granite för att ange hur cookies ska användas på dina webbsidor. I följande tabell beskrivs de egenskaper som du kan konfigurera.

Om du vill konfigurera tjänsten kan du använda [webbkonsolen](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) eller [lägga till en OSGi-konfiguration i databasen](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository). I följande tabell beskrivs de egenskaper som du behöver för någon av metoderna. Tjänstens-PID är `com.adobe.granite.optout` för en OSGi-konfiguration.

| Egenskapsnamn (webbkonsol) | OSGi-egenskapsnamn | Beskrivning |
|---|---|---|
| Cookies för avanmälan | optout.cookies | Namnen på cookies som anger, när de finns på användarens enhet, att användaren inte har godkänt att använda cookies. |
| Avanmäl HTTP-huvuden | optout.headers | Namnen på HTTP-rubriker som anger, i förekommande fall, att användaren inte har samtyckt till att använda cookies. |
| Cookies i vitlista | optout.whitelist.cookies | En lista över cookies som är viktiga för att webbplatsen ska fungera och som kan användas utan användarens samtycke. |

## Verifierar cookie-användning {#validating-cookie-usage}

Använd javascript på klientsidan för att anropa tjänsten Adobe Granite Opt-Out för att verifiera att du kan använda en cookie. Använd Granite.OptOutUtil javascript-objektet om du vill utföra någon av följande åtgärder:

* Hämta en lista med cookie-namn som anger att användaren inte godkänner att cookies används i spårningssyfte.
* Hämta en lista med cookies som kan användas.
* Avgör om webbläsaren innehåller en cookie som anger att användaren inte godkänner användningen av cookies för spårning.
* Avgör om en viss cookie kan användas.

Granite.utils [klientbiblioteksmappen](/help/sites-developing/clientlibs.md#referencing-client-side-libraries) innehåller objektet Granite.OptOutUtil. Lägg till följande kod i sidhuvud-JSP för att inkludera en länk till javascript-biblioteket:

`<ui:includeClientLib categories="granite.utils" />`

Följande javascript-funktion avgör till exempel om cookien COOKIE_NAME får användas innan den skrivs till den:

```
function writeCookie(value){
   if (!Granite.OptOutUtil.maySetCookie("COOKIE_NAME"))
      return;
   if (value) {
      value = encodeURIComponent(value);
      document.cookie = "COOKIE_NAME=" + value;
   }
}
```

## Granite.OptOutUtil JavaScript-objektet {#the-granite-optoututil-javascript-object}

Med Granite.OptOutUtil kan du avgöra om cookie-användning är tillåten.

### funktionen getCookieNames() {#getcookienames-function}

Returnerar namnen på de cookies som, i förekommande fall, anger att användaren inte har gett sitt samtycke till användningen av cookies.

**Parametrar**

Inget.

**Returnerar**

En array med cookie-namn.

#### funktionen getWhitelistCookieNames() {#getwhitelistcookienames-function}

Returnerar namnen på cookies som kan användas oavsett användarens samtycke.

**Parametrar**

Inget.

**Returnerar**

En array med cookie-namn.

#### isOptedOut(), funktion {#isoptedout-function}

Avgör om användarens webbläsare innehåller cookies som anger att samtycke inte har getts för att använda cookies.

**Parametrar**

Inget.

**Returnerar**

Ett booleskt värde på `true` om det finns en cookie som inte anger något samtycke, och värdet `false` om ingen cookie anger att den inte medgett.

### Funktionen maySetCookie(cookieName) {#maysetcookie-cookiename-function}

Avgör om en viss cookie kan användas i användarens webbläsare. Den här funktionen motsvarar att använda funktionen `isOptedOut` när du avgör om den angivna cookien finns med i listan som funktionen `getWhitelistCookieNames` returnerar.

**Parametrar**

* cookieName: Sträng. Namnet på kakan.

**Returnerar**

Ett booleskt värde på `true` om `cookieName` kan användas, eller ett värde på `false` om `cookieName` inte kan användas.
