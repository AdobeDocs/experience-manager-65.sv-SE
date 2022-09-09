---
title: Administrera generisk e-handel
seo-title: Administering generic eCommerce
description: Den AEM generiska lösningen innehåller metoder för att hantera den handelsinformation som finns i databasen.
seo-description: The AEM generic solution provides methods of managing the commerce information held within the repository.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: c29f6213-1df6-45af-91c8-14b255276d82
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '2910'
ht-degree: 1%

---

# Administrera generisk e-handel {#administering-generic-ecommerce}

Den AEM generiska lösningen innehåller metoder för att hantera den handelsinformation som finns i databasen (till skillnad från att använda en extern e-handelsmotor). Detta omfattar följande:

* [Produkter](/help/commerce/cif-classic/administering/concepts.md#products)
* [Produktvarianter](/help/commerce/cif-classic/administering/concepts.md#product-variants)
* [Kataloger](/help/commerce/cif-classic/administering/concepts.md#catalogs)
* [Erbjudanden](/help/commerce/cif-classic/administering/concepts.md#promotions)
* [Vouchers](/help/commerce/cif-classic/administering/concepts.md#vouchers)
* [Beställningar](/help/commerce/cif-classic/administering/concepts.md#shopping-cart-and-orders)
* [Proxysidor](/help/commerce/cif-classic/administering/concepts.md#proxy-pages)

>[!NOTE]
>
>Standardinstallationen AEM innehåller den allmänna AEM (JCR)-implementeringen av e-handel.
>
>Detta är för närvarande avsett för demonstrationssyften, eller som en grundläggande grund för en anpassad implementering enligt dina krav.

## Produkter och produktvariationer {#products-and-product-variations}

>[!NOTE]
>
>Följande procedurer gäller för både Produkter och Produktvariationer.

Innan du skapar produkter måste du definiera en [ställningar](/help/sites-authoring/scaffolding.md). Här anges vilka fält du behöver för att definiera produkterna och hur de ska redigeras.

Det behövs ett ställningar för varje enskild produkttyp. Den lämpliga strukturen är kopplad till produkterna antingen genom att

* path
* produkten kan referera till skalet

>[!NOTE]
>
>I Geometrixx-utomhusbutiken finns en enda produkttyp (och därmed ett enda schafet):
>
>`/etc/scaffolding/geometrixx-outdoors`
>
>Produkttypen Geometrixx-Outdoor är aktiv på:
>
>`/etc/commerce/products/geometrixx-outdoors`
>
>Du kan skapa en ny produktdefinition var som helst under den utan ytterligare inställningar.

### Importerar produkter {#importing-products}

#### Importera produkter - Touchoptimerat användargränssnitt {#importing-products-touch-optimized-ui}

1. Navigera till **Produkter** konsol, via **Handel**.
1. Använda **Produkter** konsolen navigerar till önskad plats.
1. Använd **Importera produkter** -ikonen för att öppna guiden.

   ![chlimage_1-1](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. Ange:

   * **Importör**

      Importören för den specifika [e-handelsleverantör](/help/commerce/cif-classic/administering/concepts.md#commerce-providers), som standard `Geometrixx`.

   * **Källa**

      Den fil du vill importera; du kan använda webbläsaren för att välja en fil.

   * **Inkrementell import**

      Ange om detta är en stegvis import (i motsats till fullständig).
   >[!NOTE]
   >
   >Den stegvisa importen (av importexemplaret geometrixx-outdoor) sker på produktnivå.
   >
   >En anpassad importör kan definieras för att fungera som det ska.

1. Välj **Nästa** Om du vill importera produkterna visas en logg över de åtgärder som vidtagits.

   >[!NOTE]
   >
   >Produkterna importeras till, eller i förhållande till, den aktuella platsen.

   >[!NOTE]
   >
   >Använda flera gånger **Nästa** och **Bakåt** kommer att importera produktdefinitionerna upprepade gånger. Eftersom de har samma SKU:er skrivs den information som finns i databasen över.

1. Välj **Klar** för att stänga guiden.

#### Importerar produkter - klassiskt användargränssnitt {#importing-products-classic-ui}

1. Använda **verktyg** konsolen öppnar **Handel** mapp.
1. Dubbelklicka för att öppna **Produktimporterare**:

   ![chlimage_1-22](/help/sites-administering/assets/chlimage_1-22.jpeg)

1. Ange:

   * **Butiksnamn**

      Produkterna importeras till:

      `/etc/commerce/products/<*store name*>/`

   * **Commerce Provider**

      Importören för din [e-handelsleverantör](/help/commerce/cif-classic/administering/concepts.md#commerce-providers); som standard Geometrixx.

   * **Källfil**

      Platsen i databasen för filen som du vill importera.

   * **Inkrementell import**

      Ange om detta är en stegvis import (i motsats till fullständig).

1. Klicka **Importera produkter**.

### Skapar produktinformation {#creating-product-information}

>[!NOTE]
>
>Standardprodukthanteringen är grundläggande eftersom produktuppsättningen för Geometrixx-utomhusbruk har hållits grundläggande. Komplexiteten bygger på produkten [ställningar](/help/sites-authoring/scaffolding.md)så att du med din egen produktanpassning kan göra mer avancerad redigering.

#### Skapa produktinformation - Touchoptimerat gränssnitt {#creating-product-information-touch-optimized-ui}

1. Använda **Produkter** konsol (via **Handel**) navigera till önskad plats.
1. Använd **Skapa** -ikonen för att välja antingen (beroende på struktur och plats):

   * **Skapa produkt**
   * **Skapa produktvariation**

   ![chlimage_1-14](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. Guiden öppnas. Använd **Grundläggande** och **Flikar** för att ange [produktattribut](/help/commerce/cif-classic/administering/concepts.md#product-attributes) för den nya produkten eller produktvarianten.

   >[!NOTE]
   >
   >**Titel** och **SKU** är det minsta som krävs för att skapa en produkt eller variant.

1. Välj **Skapa** för att spara informationen.

>[!NOTE]
>
>Många produkter finns i en rad olika färger och/eller storlekar. Information om basprodukten och relaterade produktvarianter kan båda hanteras från **Produkter** konsol.
>
>Produkterna och deras varianter lagras som en trädstruktur, produktinformationen är högst upp, med varianterna under (den här strukturen används av användargränssnittet).

### Redigera produktinformation {#editing-product-information}

>[!NOTE]
>
>Produktbilder i geometrixx-utomhusbruk kan fås från:
>
>`/etc/commerce/products/...`
>
>Det innebär att de som standard blockeras av [avsändare](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html)så konfigurera efter behov.

#### Redigera produktinformation - Touchoptimerat gränssnitt {#editing-product-information-touch-optimized-ui}

1. Använda **Produkter** konsol (via **Handel**) navigera till produktinformationen.
1. Använd antingen:

   * [snabbåtgärder](/help/sites-authoring/basic-handling.md#quick-actions)
   * [markeringsläge](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Välj **Visa produktdata** ikon:

   ![chlimage_1-3](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. The [produktattribut](/help/commerce/cif-classic/administering/concepts.md#product-attributes) visas. Använd **Redigera** och **Klar** för att göra ändringar.

### Visar produktreferenser {#showing-product-references}

#### Visar produktreferenser - Touchoptimerat användargränssnitt {#showing-product-references-touch-optimized-ui}

1. Använda **Produkter** konsol (via **Handel**) navigera till produktinformationen.
1. Öppna den sekundära listen för referenser med ikonen:

   ![chlimage_1-4](/help/sites-administering/do-not-localize/chlimage_1-16.png)

1. Välj önskad produkt - den sekundära rälen uppdateras för att visa tillgängliga referenstyper:

   ![chlimage_1-88](/help/sites-administering/assets/chlimage_1-88.png)

1. Klicka/tryck på referenstypen (t.ex. produktsidor) för att utöka listan.
1. Välj en specifik referens för att visa alternativen:

   * Navigera till produktsidan
   * Redigera produktsida

   ![chlimage_1-89](/help/sites-administering/assets/chlimage_1-89.png)

### Sök efter produkter {#search-for-products}

1. Navigera till **Produkter** konsol, via **Handel**.
1. Öppna den andra listen för sökning med ikonen:

   ![](/help/sites-administering/do-not-localize/chlimage_1-17.png)

1. Du kan söka efter produkter på flera olika sätt. Du kan bara använda en eller flera aspekter för en sökning. De produkter som hittas visas:

   ![chlimage_1-90](/help/sites-administering/assets/chlimage_1-90.png)

1. Om du klickar/trycker på en produkt öppnas den. Du kan också publicera den eller visa produktdata.

#### Utöka sökning {#extending-search}

Du kan ändra en befintlig aspekt eller lägga till nya, med CRXDE Lite:

1. Navigera till:

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. Du kan till exempel ändra de storlekar som ska visas på produktsöksidan. Klicka på `sizegroup` nod.
1. Klicka `items` nod, klicka sedan på `propertypredicate` nod.
1. Du kan ändra `propertyValues`. Du kan till exempel lägga till XS, eller XXL, eller ta bort en storlek.
1. Klicka **Spara alla** och navigera till produktsöksidan. Ändringarna bör visas.

### Flera resurser {#multiple-assets}

Du kan lägga till flera resurser i produktkomponenten och sedan ange vilken resurs som ska visas på produktsidan.

>[!NOTE]
>
>Allt som rör flera resurser görs med det pekoptimerade användargränssnittet.

#### Lägga till flera resurser {#adding-multiple-assets}

1. Navigera till **Produkter** konsol, via **Handel**.
1. Använda **Produkter** navigera till önskad produkt.

   >[!NOTE]
   >
   >Du måste vara på produktnivå, inte på variantnivå.

1. Tryck/klicka **Visa produktdata** med markeringsläge eller snabbåtgärder.
1. Tryck/klicka på ikonen Redigera.
1. Bläddra till **Lägg till**.

   ![chlimage_1-91](/help/sites-administering/assets/chlimage_1-91.png)

1. Tryck/klicka **Lägg till**. En ny platshållare för resursen visas.
1. Om du trycker/klickar på **Ändra **öppnas en dialogruta där du kan välja en resurs.
1. Välj den resurs som du vill lägga till.

   >[!NOTE]
   >
   >De resurser du kan välja är från [Resurser](/help/assets/assets.md).

1. Tryck/klicka på ikonen Klar.

Två resurser lagras nu i produktkomponenten. Du kan konfigurera vilken som ska visas på produktsidan. Detta fungerar med ett kategorisystem. Först måste du lägga till en kategori till de enskilda resurserna:

1. Tryck/klicka **Visa produktdata**.
1. Skriv en **Tillgångskategori** under tillgångarna, till exempel `cat1` och `cat2`.

   >[!NOTE]
   >
   >Du kan också använda taggar för kategorier.

1. Tryck/klicka på ikonen Klar. Nu måste du [utrullning](#rolling-out-a-catalog) dina ändringar.

Nu har resurserna i produktkomponenten en kategori. Du kan konfigurera vilken kategori som ska visas på tre olika nivåer:

* [Produktsida](#product-page)
* [Katalog](#catalog)
* [Products Console](#products-console)

>[!NOTE]
>
>Om du inte anger kategorier visas den första resursen på produktsidan.

Mekanismen för att välja den bild som ska visas är följande:

1. Verifiera om en kategori har angetts för produktsidan.
1. Annars kontrollerar du om en kategori har angetts för katalogen.
1. Om inte, kontrollerar du om en kategori har angetts för produktkonsolen.

>[!NOTE]
>
>För både katalognivå och produktkonsolnivå måste du implementera ändringarna och se skillnaden på produktsidan.

#### Produktsida {#product-page}

1. Gå till din produktsida.
1. **Redigera** produktkomponenten.
1. Skriv **Bildkategori** du valde ( `cat1` till exempel).
1. Tryck/klicka **Klar**. Sidan uppdateras och rätt resurs ska visas.

#### Katalog  {#catalog}

1. Navigera till katalogen.
1. Tryck/klicka **Visa egenskaper**.
1. Tryck/klicka **Redigera**.
1. Tryck/klicka på **Resurser** -fliken.
1. Ange den obligatoriska **Produkttillgångskategori**.
1. Tryck/klicka **Klar**.
1. [Utrullning](#rolling-out-a-catalog) dina ändringar.

#### Products Console {#products-console}

1. Använda **Produkter** navigera till önskad produkt.
1. Tryck/klicka **Visa produktdata**.
1. Tryck/klicka **Redigera**.
1. Skriv a **Standardtillgångskategori**.
1. Tryck/klicka **Klar**.
1. [Utrullning](#rolling-out-a-catalog) dina ändringar.

### Publicera/avpublicera produktinformation {#publishing-unpublishing-product-information}

#### Publicera/avpublicera produktinformation - Touchoptimerat gränssnitt {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>Produktinformationen publiceras ofta via de sidor som refererar till den. Om du till exempel publicerar sidan X som refererar till produkten Y, frågar AEM om du även vill publicera produkten Y.
>
>I särskilda fall kan AEM även publicera direkt från produktinformationen.

1. Använda **Produkter** konsol (via **Handel**) navigera till produktinformationen.
1. Använd antingen:

   * [snabbåtgärder](/help/sites-authoring/basic-handling.md#quick-actions)
   * [markeringsläge](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Välj **Publicera** eller **Avpublicera** ikon efter behov:

   ![chlimage_1-6](/help/sites-administering/do-not-localize/chlimage_1-18.png) ![chlimage_1-7](/help/sites-administering/do-not-localize/chlimage_1-19.png)

   Produktinformationen kommer att publiceras eller avpubliceras efter behov.

<!-- Search&Promote is end of life as of September 1, 2022 ### Product Feed {#product-feed} -->

<!-- Search&Promote is end of life as of September 1, 2022 The Search&Promote integration allows you to: -->

<!-- Search&Promote is end of life as of September 1, 2022 * use the eCommerce API, independently of the underlying repository structure and commerce platform. -->
<!-- Search&Promote is end of life as of September 1, 2022 * leverage the Index Connector feature of Search&Promote to provide a product feed in XML format. -->
<!-- Search&Promote is end of life as of September 1, 2022 * leverage the Remote Control feature of Search&Promote to perform on-demand or scheduled requests of the product feed -->
<!-- Search&Promote is end of life as of September 1, 2022 * feed generation for different Search&Promote accounts, configured as cloud services configurations. -->

<!-- Search&Promote is end of life as of September 1, 2022 For more information, read [Product Feed](/help/sites-administering/product-feed.md). -->

### Händelsehanterare för produktuppdateringar {#event-handler-for-product-updates}

Det finns en händelsehanterare som loggar en händelse när en produkt läggs till, ändras eller tas bort och när en produktsida läggs till, ändras eller tas bort. Det finns följande OSGi-händelser:

* `com/adobe/cq/commerce/pim/PRODUCT_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_DELETED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_DELETED`

För `PRODUCT_*` -händelser pekar sökvägen till basprodukten i `/etc/commerce/products`. För `PRODUCT_PAGE_*` händelser, banan pekar på `cq:Page` nod.

Du kan titta på dem i webbkonsolen i OSGI-händelser ( `/system/console/events`), till exempel:

![](/help/sites-administering/do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>Läs även [Händelsehantering i AEM](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/).

### Bild med Lägg till i kundvagnslänkar {#image-with-add-to-cart-links}

Med komponenten Bild med Lägg i kundvagnslänkar kan du snabbt lägga till en produkt i kundvagnen genom att skapa en aktiveringspunkt länkad till en produkt i en bild.

När du klickar på aktiveringspunkten öppnas en dialogruta där du kan välja storlek och kvantitet för produkten.

1. Navigera till sidan där du vill lägga till komponenten.
1. Dra och släpp komponenten på sidan.
1. Dra och släpp en bild i komponenten från [resurshanterare](/help/sites-authoring/author-environment-tools.md#assets-browser).
1. Du kan antingen:

   * klicka på komponenten och sedan på ikonen Redigera
   * dubbelklicka långsamt

1. Klicka på helskärmsikonen.

   ![chlimage_1-92](/help/sites-administering/assets/chlimage_1-92.png)

1. Klicka på ikonen Starta karta.

   ![chlimage_1-93](/help/sites-administering/assets/chlimage_1-93.png)

1. Klicka på en av formikonerna.

   ![chlimage_1-21](/help/sites-administering/do-not-localize/chlimage_1-21.png)

1. Ändra och flytta formen efter behov.
1. Klicka på formen.
1. När du klickar på bläddringsikonen öppnas [Resursväljaren](/help/assets/search-assets.md#assetpicker).

   >[!NOTE]
   >
   >Du kan också skriva produktsökvägen som måste finnas på produktnivå, inte på variantnivå, direkt.

   ![chlimage_1-94](/help/sites-administering/assets/chlimage_1-94.png)

1. Klicka på bekräftelseikonen två gånger och sedan på Avsluta helskärm.
1. Klicka någonstans på sidan bredvid komponenten. Sidan bör uppdateras och följande symbol bör visas på bilden:

   ![](/help/sites-administering/do-not-localize/chlimage_1-22.png)

1. Växla till [förhandsgranska](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui) läge.
1. Klicka på hotspot-området +. En dialogruta öppnas där du kan välja storlek och kvantitet för den produkt du angav i **Bana**.

   ![chlimage_1-95](/help/sites-administering/assets/chlimage_1-95.png)

1. Ange en storlek och en kvantitet.
1. Klicka på knappen Lägg till i kundvagnen. Dialogrutan stängs.
1. Gå till kundvagnen. Produkten ska vara här.

#### Konfigurationsalternativ {#configuration-options}

Du kan konfigurera hur dialogrutan ser ut när du klickar på hotspot-området:

1. Klicka på komponenten och klicka på konfigurationsikonen.

   ![chlimage_1-96](/help/sites-administering/assets/chlimage_1-96.png)

1. Bläddra nedåt. Det finns en **LÄGG TILL I KARTONG** -fliken.

   ![chlimage_1-97](/help/sites-administering/assets/chlimage_1-97.png)

1. Klicka **LÄGG TILL I KARTONG**. Det finns tre konfigurationsalternativ som du kan använda.

   ![chlimage_1-98](/help/sites-administering/assets/chlimage_1-98.png)

1. Klicka på ikonen Klar.

## Kataloger {#catalogs}

### Skapa en katalog {#generating-a-catalog}

#### Generera en katalog - Touchoptimerat användargränssnitt {#generating-a-catalog-touch-optimized-ui}

>[!NOTE]
>
>Katalogen kommer att referera till dina produktdata.

Så här skapar du en katalog:

1. Öppna Sites-konsolen (till exempel [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)).
1. Navigera till den plats där du vill skapa den nya sidan.
1. Om du vill öppna alternativlistan använder du **Skapa** ikon:

   ![create-icon](/help/sites-administering/do-not-localize/chlimage_1-23.png)

1. Välj **Skapa katalog**&#x200B;öppnas guiden Skapa katalog.

   ![chlimage_1-99](/help/sites-administering/assets/chlimage_1-99.png)

1. Navigera till önskad katalogutkast.
1. Tryck/klicka **Välj** och tryck/klicka på den önskade katalogdesignen.
1. Tryck/klicka **Nästa**.

   ![chlimage_1-100](/help/sites-administering/assets/chlimage_1-100.png)

1. Skriv a **Titel** och **Namn**.
1. Tryck/klicka på **Skapa** -knappen. Katalogen skapas och en dialogruta öppnas.

   ![chlimage_1-101](/help/sites-administering/assets/chlimage_1-101.png)

1. Tryck/klicka **Klar** Med knappen kommer du tillbaka till webbplatskonsolen där du kan se katalogen.

   Tryck/klicka **Öppna katalog** knappen öppnar katalogen (till exempel `http://localhost:4502/editor.html/content/test-catalog.html`).

#### Generera en katalog - Classic UI {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>Katalogen refererar till din [Produktdata](#products-and-product-variants).

1. Använda **Webbplatser** konsol, navigera till **Katalogutkast** och sedan baskatalogen.

   Till exempel:

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. Skapa en ny sida med **Avsnittsutkast** mall.

   Till exempel, `Swimwear`.

1. Öppna den nya `Swimwear` sida och klicka sedan på **Redigera utkast** för att öppna **Egenskaper** där du kan ställa in **Produkter** markering.

   Öppna till exempel **Taggar/nyckelord** för att välja Activity (Aktivitet) och sedan simma från sektionen Geometrixx-Outdoor.

1. Klicka **OK** för att spara dina egenskaper, exempelprodukter visas under **Kriterier för produkturval** på planeringsidan.
1. Klicka på **Ändringar i utrullning...**, markera **Startsida och alla undersidor** och sedan klicka **Nästa** sedan **Utrullning**. När utrullningen är klar **Status** indikator visas som grön.
1. Nu kan du klicka **Stäng** och kontrollera den nya katalogdelen, till exempel på och under:

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. Återigen från sidan med utkast klickar du på **Redigera utkast** och i **Egenskaper** öppnar dialogrutan **Genererad sida** -fliken. I fältet Banderolllista väljer du den bild som du vill visa; till exempel `summer.jpg`
1. Klicka **OK** för att spara dina egenskaper, banderollinformation visas under **Kriterier för produkturval** på planeringsidan.
1. Utför de här nya ändringarna.

### Stänger ut en katalog {#rolling-out-a-catalog}

#### Skapa en katalog - Touchoptimerat användargränssnitt {#rolling-out-a-catalog-touch-optimized-ui}

Så här distribuerar du en katalog:

1. Navigera till **Kataloger** konsol, via **Handel**.
1. Navigera till den katalog som du vill lansera.
1. Använd antingen:

   * [snabbåtgärder](/help/sites-authoring/basic-handling.md#quick-actions)
   * [markeringsläge](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Välj **Ändringar av utrullning** ikon:

   ![utrullning](/help/sites-administering/do-not-localize/chlimage_1-24.png)

1. I guiden ställer du in utrullningen efter behov och trycker/klickar sedan **Ändringar av utrullning**.
1. En dialogruta öppnas. Tryck/klicka **Klar** när processen är klar.

#### Öppnar en katalog - Classic UI {#rolling-out-a-catalog-classic-ui}

Så här distribuerar du en katalog:

1. Navigera till den katalog som du vill lansera. Till exempel:

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. Klicka **Ändringar i utrullning...**
1. Ställ in utrullningen efter behov.
1. Klicka **Utrullning**.

### Blueprint Importer {#blueprint-importer}

#### Blueprint Importer - pekoptimerat användargränssnitt {#blueprint-importer-touch-optimized-ui}

1. Navigera till **Kataloger** konsol, via **Handel**.
1. Navigera till den plats där du vill importera katalogplanen.
1. Tryck/klicka på **Importera utkast** ikon.

   ![](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. Välj källa i guiden efter behov och tryck/klicka **Nästa**.

   ![chlimage_1-340](/help/sites-administering/assets/chlimage_1-102.png)

1. Tryck/klicka **Klar** när importen är klar.

#### Blueprint Importer - Classic UI {#blueprint-importer-classic-ui}

1. Använda **verktyg** konsol, navigera till **Handel**.

   Till exempel:

   `http://localhost:4502/miscadmin#/etc/commerce`

1. Öppna **Katalogvisare**.
1. Ställ in importen efter behov.
1. Klicka **Importera katalogutkast**.

## Erbjudanden {#promotions}

### Skapa en kampanj {#creating-a-promotion}

#### Skapa en kampanj - klassiskt användargränssnitt {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>I följande exempel behandlas en kampanj som hålls direkt i en [kampanj](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)används den för verifikationer.
>
>En kampanj kan även finnas i en [upplevelse](/help/sites-authoring/personalization.md) inom en kampanj.
>
>Mer information finns i [Kampanjer och kuponger](#promotions-and-vouchers).

1. Öppna **Webbplatser** konsolen för din författarinstans.
1. Välj önskat alternativ i den vänstra rutan **Campaign**.
1. Klicka på **Nytt** väljer du **Kampanj** mall och ange sedan en **Titel** (och **Namn** om det behövs) för din nya voucher.
1. Klicka **Skapa**. Den nya kampanjsidan visas i den högra rutan.

1. Redigera **Egenskaper** antingen

   * öppnar sidan och klickar sedan på knappen Redigera för att öppna dialogrutan Egenskaper
   * markera sidan i webbplatskonsolen och sedan använda snabbmenyn (vanligtvis höger musknapp) för att välja **Egenskaper...** och öppna egenskapsdialogrutan

   Ange **Erbjudandetyp**, **Rabattyp**, **Rabattvärde** och andra fält efter behov.

1. Klicka **OK** att spara.

1. Nu kan ni aktivera kampanjen så att kunderna ser den i publiceringsinstansen.

## Vouchers {#vouchers}

### Skapa en voucher {#creating-a-voucher}

#### Skapa en kupong - klassiskt användargränssnitt {#creating-a-voucher-classic-ui}

1. Öppna **Webbplatser** konsolen för din författarinstans.
1. Välj önskat alternativ i den vänstra rutan **Campaign**.
1. Klicka på **Nytt** väljer du **Voucher** mall och ange sedan en **Titel** (och **Namn** om det behövs) för din nya voucher.
1. Klicka **Skapa**. Den nya verifikationssidan visas i den högra rutan.

1. Öppna din nya kupongsida med ett dubbelklick och klicka sedan på **Redigera** för att konfigurera informationen efter behov.
1. Klicka **OK** att spara.

1. Nu kan du aktivera din voucher så att kunderna kan använda den i sina kundvagnar i publiceringsinstansen.

### Tar bort verifikationer {#removing-vouchers}

#### Tar bort Vouchers - klassiskt gränssnitt {#removing-vouchers-classic-ui}

För att göra en voucher otillgänglig för kunderna kan du antingen:

* Inaktivera vouchern - den är fortfarande tillgänglig i författarmiljön så att du kan återaktivera den vid ett senare tillfälle.
* Ta bort den helt.

Båda åtgärderna kan utföras från **Webbplatser** konsol.

### Ändra verifikationer {#modifying-vouchers}

#### Ändra Vouchers - klassiskt användargränssnitt {#modifying-vouchers-classic-ui}

Om du vill ändra egenskaperna för en voucher eller befordran kan du dubbelklicka på den på **Webbplatser** konsol och klicka **Redigera**. När du har sparat den bör du aktivera den så att ändringarna överförs till publiceringsinstansen.

### Lägga till verifikationer i en kundvagn {#adding-vouchers-to-a-cart}

Om du vill att användare ska kunna lägga till vouchers i sina kundvagnar kan du använda den inbyggda **Vouchers** -komponent (handelskategori). Du måste lägga till det här på samma sida som kundvagnen visas på (men är inte obligatoriskt). Verifikationskomponenten är bara ett formulär där användaren kan ange en verifikationskod, det är kundvagnskomponenten som faktiskt visar listan över använda verifikationer och deras rabatt.

På demowebbplatsen (Geometrixx Outdoors - engelska) kan du se kupongformuläret på kundvagnssidan, under den faktiska kundvagnen.

## Beställningar {#orders}

>[!NOTE]
>
>Det bör noteras att färdiga AEM inte har åtgärder som krävs för standardfunktioner som rör order, som att returnera varor, uppdatera orderstatus, utföra leveranser och generera följesedlar. Den är främst avsedd som en förhandstitt på teknik.
>
>Den allmänna orderhanteringen i AEM har hållits grundläggande. Vilka fält som är tillgängliga i guiden beror på skalan:
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`
>
>Om du skapar ett anpassat ställningar kan du lagra mer orderinformation.

>[!NOTE]
>
>Orderkonsolen visar information om leverantörsorder, som aldrig publiceras.
>
>Kundorderinformationen finns i deras hemkataloger och visas i orderhistoriken för deras konto. Denna information publiceras tillsammans med resten av deras hemkatalog.

### Skapar orderinformation {#creating-order-information}

#### Skapa beställningsinformation - Touchoptimerat gränssnitt {#creating-order-information-touch-optimized-ui}

1. Använda **Beställningar** konsolen navigerar till önskad plats.
1. Använd **Skapa** ikon som du vill markera **Skapa order**.

   ![](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. Guiden öppnas. Använd **Grundläggande**, **Innehåll**, **Betalning** och **Uppfyllelse** -tabbar för att ange [information om den nya ordern](/help/commerce/cif-classic/administering/concepts.md#order-information).

1. Välj **Skapa** för att spara informationen.

### Redigera orderinformation {#editing-order-information}

#### Redigera beställningsinformation - Touchoptimerat gränssnitt {#editing-order-information-touch-optimized-ui}

1. Använda **Beställningar** konsolen navigerar till ordningen.
1. Använd antingen:

   * [snabbåtgärder](/help/sites-authoring/basic-handling.md#quick-actions)
   * [markeringsläge](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Välj **Visa orderdata** ikon:

   ![](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. The [orderinformation](/help/commerce/cif-classic/administering/concepts.md#order-information) visas. Använd **Redigera** och **Klar** för att göra ändringar.

