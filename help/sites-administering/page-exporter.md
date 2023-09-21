---
title: Sidexporteraren
description: Lär dig hur du använder Adobe Experience Manager (AEM) Page Exporter.
exl-id: 15d08758-cf75-43c0-9818-98a579d64183
source-git-commit: 6799f1d371734b69c547f3c0c68e1e633aa63229
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 0%

---

# Sidexporteraren{#the-page-exporter}

Med Adobe Experience Manager (AEM) kan du exportera en sida som en komplett webbsida med bilder, `.js`och `.css` filer.

När konfigurationen är konfigurerad begär du en sidexport från webbläsaren genom att ersätta `html` med `export.zip` i webbadressen. Detta genererar en arkivfil (ZIP) som innehåller den återgivna sidan i html-format, tillsammans med de refererade resurserna. Alla sökvägar på sidan (till exempel sökvägar till bilder) skrivs om så att de pekar på antingen filerna som finns i arkivet eller på resurserna på servern. Arkivfilen (ZIP) kan sedan laddas ned från webbläsaren.

>[!NOTE]
>
>Beroende på webbläsaren och inställningarna är hämtningen antingen:
>
>* en arkivfil (`<page-name>.export.zip`)
>* en mapp (`<page-name>`); arkivfilen är i själva verket redan utökad

## Exportera en sida {#exporting-a-page}

I följande steg beskrivs hur du exporterar en sida och förutsätter att det finns en exportmall för platsen. En exportmall definierar hur en sida exporteras och är specifik för din plats. Information om hur du skapar en exportmall finns i [Skapa en sidexportkonfiguration för platsen](#creating-a-page-exporter-configuration-for-your-site).

Exportera en sida:

1. Navigera till önskad sida i **Webbplatser** konsol.

1. Markera sidan och öppna sedan **Egenskaper** -dialogrutan.

1. Välj **Avancerat** -fliken.

1. Expandera **Exportera** om du vill välja en exportmall.
Välj önskad mall för platsen och bekräfta sedan med **OK**.

1. Välj **Spara och stäng** för att stänga dialogrutan för sidegenskaper.

1. Begär att sidan ska exporteras och ersätta suffixet `html` med `export.zip` i webbadressen.

   Till exempel:
   * localhost:4502/content/we-retail/language-masters/en.html

   Åtkomst via:
   * localhost:4502/content/we-retail/language-masters/en.export.zip

1. Hämta arkivfilen till filsystemet.

1. Zippa upp filen i filsystemet om det behövs. När den är expanderad finns det en mapp med samma namn som den markerade sidan. Mappen innehåller:

   * undermappen `content`, som är roten i en serie undermappar som återspeglar sökvägen till sidan i databasen

      * i den här strukturen finns HTML-filen för den valda sidan (`<page-name>.html`)

   * övriga resurser (`.js` filer, `.css` filer, bilder och så vidare) är placerade enligt inställningarna i exportmallen

1. Öppna HTML-filen för sidan (`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`) i webbläsaren så att du kan kontrollera återgivningen.

## Skapa en sidexportkonfiguration för platsen {#creating-a-page-exporter-configuration-for-your-site}

Sidexporteraren baseras på [Innehållssynkroniseringsramverk](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/package-summary.html). De konfigurationer som är tillgängliga i **Sidegenskaper** -dialogrutor är exportmallar som definierar nödvändiga beroenden för en sida.

När en sidexport aktiveras refereras exportmallen. Både sidbanan och designbanan tillämpas dynamiskt. ZIP-filen skapas sedan med standardfunktionen för innehållssynkronisering.

En körklar AEM innehåller en standardmall under `/etc/contentsync/templates/default`.

* Den här mallen är en reservmall när ingen exportmall hittas i databasen.

* The `default` -mallen visar hur en sidexport kan konfigureras så att den kan fungera som en bas för en ny exportmall.

* Om du vill visa nodstrukturen för mallen i webbläsaren som JSON-format begär du följande URL:
  `http://localhost:4502/etc/contentsync/templates/default.json`

Det enklaste sättet att skapa en sidexportmall är att:

* kopiera `default` mall,

* tilldela ett nytt namn som passar din webbplats,

* gör sedan nödvändiga uppdateringar.

Så här skapar du en helt ny mall:

1. I **CRXDE Lite**, skapa en nod nedan `/etc/contentsync/templates`:

   * `Name`: ett namn som passar din plats, till exempel `<mysite>`. Namnet visas i dialogrutan för sidegenskaper när du väljer sidexportmall.

   * `Type`: `nt:unstructured`

2. Under mallnoden som anropas här `mysite`skapar du en nodstruktur med hjälp av konfigurationsnoderna som beskrivs nedan.

## Aktivera en sidexportmall för dina sidor {#activating-a-page-exporter-configuration-for-your-pages}

Gör mallen tillgänglig när du har konfigurerat den:

1. I CRXDE navigerar du till önskad sida i dialogrutan `/content` gren. Det kan vara en enskild sida eller en rotsida i ett underträd.

1. På `jcr:content` på sidans nod, skapa egenskapen:
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value`: sökväg till mallen, till exempel: `/etc/contentsync/templates/mysite`

### Konfigurationsnoder för sidexport {#page-exporter-configuration-nodes}

Mallen består av en nodstruktur som använder [Innehållssynkroniseringsramverk](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/package-summary.html). Varje nod har en `type` -egenskap som definierar en viss åtgärd när zip-filen skapas.

<!-- For more details about the type property, refer to the Overview of configuration types section in the Content Sync framework page.
-->

Följande noder kan användas för att skapa en exportmall:

* `page`
Sidnoden används för att kopiera sidans HTML-kod till zip-filen. Den har följande egenskaper:

   * En obligatorisk nod.
   * Finns nedan `/etc/contentsync/templates/<mysite>`.
   * Definieras med egenskapen `Name`ange till `page`.
   * Nodtypen är `nt:unstructured`

  The `page` noden har följande egenskaper:

   * A `type` egenskap som anges med värdet `pages`.

   * Den har inte en `path` egenskapen när den aktuella sidsökvägen kopieras dynamiskt till konfigurationen.
  <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
Noden rewrite definierar hur länkarna skrivs om på den exporterade sidan. De omskrivna länkarna kan antingen peka på filerna som finns i ZIP-filen eller på resurserna på servern.
  <!-- Please refer to the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
Designnoden används för att kopiera designen som används för den exporterade sidan. Den har följande egenskaper:

   * Valfritt.
   * Finns nedan `/etc/contentsync/templates/<mysite>`.
   * Definieras med egenskapen `Name` ange till `design`.
   * Nodtypen är `nt:unstructured`.

  The `design` noden har följande egenskaper:

   * A `type` egenskapen inställd på värdet `copy`.

   * Den har inte en `path` -egenskapen när den aktuella sidsökvägen kopieras dynamiskt till konfigurationen.

* `generic`
En allmän nod används för att kopiera resurser som clientlibs `.js` eller `.css` till zip-filen. Den har följande egenskaper:

   * Valfritt.
   * Finns nedan `/etc/contentsync/templates/<mysite>`.
   * Inget specifikt namn.
   * Nodtypen är `nt:unstructured`.
   * Har en `type` egenskap och `type` relaterade egenskaper. <!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

  Följande konfigurationsnod kopierar till exempel `mysite.clientlibs.js` filer till zip-filen:

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

Implementera en [anpassad uppdateringshanterare](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/handler/package-summary.html).

<!-- To meet some specific requirements, you may need to implement a custom `type` property: to do so, refer to the Implementing a custom update handler section in the Content Sync page.
-->

## Programmatisk export av en sida {#programmatically-exporting-a-page}

Om du vill exportera en sida programmatiskt kan du använda [PageExporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI-tjänster. Med den här tjänsten kan du:

* Exportera en sida och skriv till HTTP-serverns svar.
* Exportera en sida och spara zip-filen på en viss plats.

Servern som är bunden till `export` väljaren och `zip` i används tjänsten PageExporter.

## Felsökning {#troubleshooting}

Om du får problem med nedladdningen av ZIP-filen kan du ta bort `/var/contentsync` i databasen och skicka exportbegäran igen.
