---
title: Sidexporteraren
description: Lär dig hur du använder AEM Page Exporter.
translation-type: tm+mt
source-git-commit: 000666e0c3f05635a9469d3571a10c67b3b21613
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 0%

---


# Sidexporteraren{#the-page-exporter}

Med AEM kan du exportera en sida som en komplett webbsida, inklusive bilder `.js` och `.css` filer.

När konfigurationen är klar begär du en sidexport från webbläsaren genom att ersätta `html` med `export.zip` i URL:en. Detta genererar en arkivfil (ZIP) som innehåller den återgivna sidan i html-format, tillsammans med de refererade resurserna. Alla sökvägar på sidan (till exempel sökvägar till bilder) skrivs om så att de pekar på antingen filerna som finns i arkivet eller på resurserna på servern. Arkivfilen (ZIP) kan sedan laddas ned från webbläsaren.

>!![NOTE]
Beroende på vilken webbläsare du använder och vilka inställningar du har blir hämtningen antingen:
* en arkivfil (`<page-name>.export.zip`)
* en mapp (`<page-name>`); arkivfilen har redan utökats


## Exportera en sida {#exporting-a-page}

I följande steg beskrivs hur du exporterar en sida och förutsätter att det finns en exportkonfigurationsmall för platsen. En konfigurationsmall definierar hur en sida exporteras och är specifik för din plats. Om du vill skapa en konfigurationsmall läser du avsnittet [Skapa en sidexportkonfiguration för platsen](#creating-a-page-exporter-configuration-for-your-site) .

Så här exporterar du en sida:

1. Navigera till önskad sida, markera sidan och öppna sedan dialogrutan **Egenskaper** .

1. Välj fliken **Avancerat** .

1. Expandera fältet **Exportera** för att välja en konfigurationsmall.
Välj önskad mall för platsen och bekräfta med **OK**.

1. Välj **Spara och stäng** för att stänga dialogrutan för sidegenskaper.

1. Begär att sidan ska exporteras och ersätt suffixet `html` med `export.zip` i URL:en.

   Till exempel:
   * localhost:4502/content/we-retail/language-masters/en.html

   Används via:
   * localhost:4502/content/we-retail/language-masters/en.export.zip


1. Hämta arkivfilen till filsystemet.

1. Zippa upp filen i filsystemet om det behövs. När den är utökad finns det en mapp med samma namn som den markerade sidan. Mappen innehåller:

   * undermappen `content`, som är roten till en serie undermappar som återspeglar sökvägen till sidan i databasen

   * i den här strukturen finns HTML-filen för den valda sidan (`<page-name>.html`)

   * andra resurser (`.js` filer, `.css` filer, bilder etc.) är placerade enligt inställningarna i exportmallen

1. Öppna HTML-sidfilen (`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`) i webbläsaren för att kontrollera återgivningen.

## Skapa en sidexportkonfiguration för platsen {#creating-a-page-exporter-configuration-for-your-site}

Sidexporteraren baseras på ramverket för innehållssynkronisering. De konfigurationer som är tillgängliga i dialogrutan **Sidegenskaper** är exportmallar som definierar nödvändiga beroenden för en sida.

När en sidexport aktiveras refereras exportmallen och både sidsökvägen och designsökvägen tillämpas dynamiskt. ZIP-filen skapas sedan med standardfunktionen för innehållssynkronisering.

AEM bäddar in en standardmall under `/etc/contentsync/templates/default`.

* Den här mallen är reservmallen när ingen konfigurationsmall hittas i databasen.

* I mallen `default` visas hur en sidexport kan konfigureras så att den kan fungera som bas för en ny konfigurationsmall.

* Om du vill visa nodstrukturen för mallen i webbläsaren som JSON-format begär du följande URL:
   `http://localhost:4502/etc/contentsync/templates/default.json`

Det enklaste sättet att skapa en ny sidexportmall är att:

* kopiera `default` mallen,

* tilldela ett nytt namn som passar din webbplats,

* gör sedan nödvändiga uppdateringar.

Så här skapar du en helt ny mall:

1. Skapa en nod nedan i **CRXDE Lite**`/etc/contentsync/templates`:

   * `Name`: ett namn som passar er plats, till exempel `<mysite>`. Namnet visas i dialogrutan för sidegenskaper när du väljer sidexportmall.

   * `Type`: `nt:unstructured`

1. Under mallnoden, som anropas här, `mysite`skapar du en nodstruktur med hjälp av konfigurationsnoderna som beskrivs nedan.

## Aktivera en sidexportmall för dina sidor {#activating-a-page-exporter-configuration-for-your-pages}

När mallen har konfigurerats måste du göra den tillgänglig:

1. Gå till önskad sida i CRXDE.

1. Skapa egenskapen på `jcr:content` noden:
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value`: Sökväg till mallen. till exempel: `/etc/contentsync/templates/mysite`

### Konfigurationsnoder för sidexport {#page-exporter-configuration-nodes}

Mallen består av en nodstruktur. Varje nod har en `type` egenskap som definierar en specifik åtgärd när zip-filen skapas. Mer information om type-egenskapen finns i avsnittet Översikt över konfigurationstyper på ramverkssidan för innehållssynkronisering.

Följande noder kan användas för att skapa en exportkonfigurationsmall:

* `page`
Sidnoden används för att kopiera sidans HTML-kod till zip-filen. Den har följande egenskaper:

   * Är en obligatorisk nod.
   * Finns nedan `/etc/contentsync/templates/<sitename>`.
   * Det heter `page`.
   * Dess nodtyp är `nt:unstructured`

   Noden har `page` följande egenskaper:

   * En `type` egenskapsuppsättning med värdet `pages`.

   * Den har ingen `path` egenskap eftersom den aktuella sidsökvägen kopieras dynamiskt till konfigurationen.

   * De andra egenskaperna beskrivs i avsnittet Översikt över konfigurationstyper i ramverket för innehållssynkronisering.


* `rewrite`
Noden rewrite definierar hur länkarna skrivs om på den exporterade sidan. De omskrivna länkarna kan antingen peka på filerna som finns i ZIP-filen eller på resurserna på servern.

   En fullständig beskrivning av `rewrite` noden finns på sidan Innehållssynkronisering.

* `design`
Designnoden används för att kopiera designen som används för den exporterade sidan. Den har följande egenskaper:

   * Är valfritt.
   * Finns nedan `/etc/contentsync/templates/<sitename>`.
   * Det heter `design`.
   * Dess nodtyp är `nt:unstructured`.

   Noden har `design` följande egenskaper:

   * En `type` egenskap som är inställd på värdet `copy`.

   * Den har ingen `path` egenskap eftersom den aktuella sidsökvägen kopieras dynamiskt till konfigurationen.


* `generic`
En allmän nod används för att kopiera resurser som .js- eller .css-filer med klienten till zip-filen. Den har följande egenskaper:

   * Är valfritt.

   * Finns nedan `/etc/contentsync/templates/<sitename>`.

   * Har inget specifikt namn.

   * Dess nodtyp är `nt:unstructured`.

   * Har en `type` egenskap och alla `type` relaterade egenskaper enligt definitionen i avsnittet Översikt över konfigurationstyper i ramverket för innehållssynkronisering.

   Följande konfigurationsnod kopierar till exempel `mysite.clientlibs.js` filerna till zip-filen:

   ```xml
   "mysite.clientlibs.js": {
       "extension": "js",
       "type": "clientlib",
       "path": "/etc/designs/mysite/clientlibs",
       "jcr:primaryType": "nt:unstructured"
   }
   ```

**Implementera en anpassad konfiguration**

Anpassade konfigurationer är också möjliga.

<!--
As you may have noticed in the node structure, the **Geometrixx** page export configuration template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

För att uppfylla vissa specifika krav kan du behöva implementera en anpassad `type` egenskap: Mer information finns i avsnittet Implementera en anpassad uppdateringshanterare på sidan Innehållssynkronisering.

## Programmatisk export av en sida {#programmatically-exporting-a-page}

Om du vill exportera en sida programmatiskt kan du använda tjänsten [PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI. Med den här tjänsten kan du:

* Exportera en sida och skriv till HTTP-serverns svar.
* Exportera en sida och spara zip-filen på en viss plats.

Servern som är bunden till `export` väljaren och `zip` tillägget använder tjänsten PageExporter.

## Felsökning {#troubleshooting}

Om du får problem med nedladdningen av zip-filen kan du ta bort noden i databasen och skicka exportbegäran igen. `/var/contentsync`

