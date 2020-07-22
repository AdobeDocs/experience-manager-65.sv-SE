---
title: Sidexporteraren
description: Lär dig hur du använder AEM Page Exporter.
translation-type: tm+mt
source-git-commit: b0126894dec33648a24c0308972aa5b47d7e4b84
workflow-type: tm+mt
source-wordcount: '1052'
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

I följande steg beskrivs hur du exporterar en sida och förutsätter att det finns en exportmall för platsen. En exportmall definierar hur en sida exporteras och är specifik för din plats. Om du vill skapa en exportmall läser du avsnittet [Skapa en sidexportkonfiguration för platsen](#creating-a-page-exporter-configuration-for-your-site) .

Så här exporterar du en sida:

1. Navigera till önskad sida i **webbplatskonsolen** .

1. Markera sidan och öppna sedan dialogrutan **Egenskaper** .

1. Välj fliken **Avancerat** .

1. Expandera fältet **Exportera** för att välja en exportmall.
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

Sidexporteraren baseras på ramverket för [innehållssynkronisering](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html). De konfigurationer som är tillgängliga i dialogrutan **Sidegenskaper** är exportmallar som definierar nödvändiga beroenden för en sida.

När en sidexport aktiveras refereras exportmallen och både sidsökvägen och designsökvägen tillämpas dynamiskt. ZIP-filen skapas sedan med standardfunktionen för innehållssynkronisering.

En körklar AEM-installation innehåller en standardmall under `/etc/contentsync/templates/default`.

* Den här mallen är en reservmall när ingen exportmall hittas i databasen.

* I mallen `default` visas hur en sidexport kan konfigureras så att den kan fungera som bas för en ny exportmall.

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

2. Under mallnoden, som anropas här, `mysite`skapar du en nodstruktur med hjälp av konfigurationsnoderna som beskrivs nedan.

## Aktivera en sidexportmall för dina sidor {#activating-a-page-exporter-configuration-for-your-pages}

När mallen har konfigurerats måste du göra den tillgänglig:

1. I CRXDE navigerar du till önskad sida i `/content` grenen.

1. Skapa egenskapen på sidans nod `jcr:content` :
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value`: Sökväg till mallen. till exempel: `/etc/contentsync/templates/mysite`

### Konfigurationsnoder för sidexport {#page-exporter-configuration-nodes}

Mallen består av en nodstruktur som använder ramverket för [innehållssynkronisering](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html).  Varje nod har en `type` egenskap som definierar en specifik åtgärd när zip-filen skapas.

<!-- For more details about the type property, refer to the Overview of configuration types section in the Content Sync framework page.
-->

Följande noder kan användas för att skapa en exportmall:

* `page`
Sidnoden används för att kopiera sidans HTML-kod till zip-filen. Den har följande egenskaper:

   * Är en obligatorisk nod.
   * Finns nedan `/etc/contentsync/templates/<mysite>`.
   * Definieras med egenskapen `Name`inställd på `page`.
   * Nodtypen är `nt:unstructured`

   Noden har `page` följande egenskaper:

   * En `type` egenskapsuppsättning med värdet `pages`.

   * Den har ingen `path` egenskap eftersom den aktuella sidsökvägen kopieras dynamiskt till konfigurationen.

   <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
Noden rewrite definierar hur länkarna skrivs om på den exporterade sidan. De omskrivna länkarna kan antingen peka på filerna som finns i ZIP-filen eller på resurserna på servern.
   <!-- Please refer to the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
Designnoden används för att kopiera designen som används för den exporterade sidan. Den har följande egenskaper:

   * Är valfritt.
   * Finns nedan `/etc/contentsync/templates/<mysite>`.
   * Definieras med egenskapen `Name` inställd på `design`.
   * Nodtypen är `nt:unstructured`.

   Noden har `design` följande egenskaper:

   * En `type` egenskap som är inställd på värdet `copy`.

   * Den har ingen `path` egenskap eftersom den aktuella sidsökvägen kopieras dynamiskt till konfigurationen.


* `generic`
En allmän nod används för att kopiera resurser som clientlibs 
`.js` eller `.css` filer till zip-filen. Den har följande egenskaper:

   * Är valfritt.
   * Finns nedan `/etc/contentsync/templates/<mysite>`.
   * Har inget specifikt namn.
   * Nodtypen är `nt:unstructured`.
   * Har en `type` egenskap och `type` relaterade egenskaper. <!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

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
As you may have noticed in the node structure, the **Geometrixx** page export template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

För att uppfylla vissa specifika krav kan du behöva implementera en [anpassad uppdateringshanterare](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/handler/package-summary.html).

<!-- To meet some specific requirements, you may need to implement a custom `type` property: to do so, refer to the Implementing a custom update handler section in the Content Sync page.
-->

## Programmatisk export av en sida {#programmatically-exporting-a-page}

Om du vill exportera en sida programmatiskt kan du använda tjänsten [PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI. Med den här tjänsten kan du:

* Exportera en sida och skriv till HTTP-serverns svar.
* Exportera en sida och spara zip-filen på en viss plats.

Servern som är bunden till `export` väljaren och `zip` tillägget använder tjänsten PageExporter.

## Felsökning {#troubleshooting}

Om du får problem med nedladdningen av zip-filen kan du ta bort noden i databasen och skicka exportbegäran igen. `/var/contentsync`
