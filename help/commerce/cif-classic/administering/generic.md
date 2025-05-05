---
title: Administrera generisk e-handel
description: Den AEM generiska lösningen innehåller metoder för att hantera den handelsinformation som finns i databasen.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: c29f6213-1df6-45af-91c8-14b255276d82
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '2907'
ht-degree: 0%

---

# Administrera generisk e-handel {#administering-generic-ecommerce}

Den generiska Adobe Experience Manager-lösningen (AEM) innehåller metoder för att hantera den handelsinformation som finns i databasen (till skillnad från en extern e-handelsmotor). Detta omfattar följande:

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
>Detta är avsett för demonstrationssyften, eller som en grundläggande grund för en anpassad implementering enligt dina krav.

## Produkter och produktvariationer {#products-and-product-variations}

>[!NOTE]
>
>Följande procedurer gäller för både Produkter och Produktvariationer.

Definiera en [schafold](/help/sites-authoring/scaffolding.md) innan du skapar produkter. Här anges fälten som du måste definiera, produkterna och hur de redigeras.

Det behövs ett ställningar för varje enskild produkttyp. Den lämpliga strukturen är kopplad till produkterna antingen genom att

* bana
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
>Du kan skapa en produktdefinition var som helst under den utan ytterligare inställningar.

### Importerar produkter {#importing-products}

#### Importera produkter - Touchoptimerat användargränssnitt {#importing-products-touch-optimized-ui}

1. Navigera till konsolen **Produkter** via **Commerce**.
1. Använd konsolen **Produkter** för att navigera till önskad plats.
1. Använd ikonen **Importera produkter** för att öppna guiden.

   ![Ikonen Importera produkter](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. Ange:

   * **Importör**

     Importören för den specifika [e-handelsprovidern](/help/commerce/cif-classic/administering/concepts.md#commerce-providers), som standard `Geometrixx`.

   * **Source**

     Den fil som du vill importera. Du kan använda webbläsaren för att välja en fil.

   * **Inkrementell import**

     Ange om detta är en stegvis import (i motsats till fullständig).

   >[!NOTE]
   >
   >Den stegvisa importen (av importexemplaret geometrixx-outdoor) sker på produktnivå.
   >
   >En anpassad importör kan definieras för att fungera som det ska.

1. Välj **Nästa** om du vill importera produkterna, så visas en logg över de åtgärder som har vidtagits.

   >[!NOTE]
   >
   >Produkterna importeras till, eller i förhållande till, den aktuella platsen.

   >[!NOTE]
   >
   >Om du använder **Nästa** och **Bakåt** flera gånger importeras produktdefinitionerna. Eftersom de har samma SKU:er skrivs den befintliga informationen i databasen över.

1. Välj **Klar** för att stänga guiden.

#### Importerar produkter - klassiskt användargränssnitt {#importing-products-classic-ui}

1. Öppna mappen **Commerce** med konsolen **Verktyg**.
1. Dubbelklicka för att öppna **produktimporteraren**:

   ![Produktimporterarkonsolen](/help/sites-administering/assets/chlimage_1-22.jpeg)

1. Ange:

   * **Butiksnamn**

     Produkterna importeras till:

     `/etc/commerce/products/<*store name*>/`

   * **Commerce Provider**

     Importören för din [e-handelsleverantör](/help/commerce/cif-classic/administering/concepts.md#commerce-providers), som standard, Geometrixx.

   * **Source-fil**

     Platsen i databasen för filen som du vill importera.

   * **Inkrementell import**

     Ange om detta är en stegvis import (i motsats till fullständig).

1. Klicka på **Importera produkter**.

### Skapar produktinformation {#creating-product-information}

>[!NOTE]
>
>Standardprodukthanteringen är grundläggande eftersom produktuppsättningen för Geometrixx-utomhusbruk har hållits grundläggande. Komplexiteten baseras på produktens [ställningar](/help/sites-authoring/scaffolding.md), så med din egen produktavkodning är det möjligt att få en mer avancerad redigering.

#### Skapa produktinformation - Touchoptimerat gränssnitt {#creating-product-information-touch-optimized-ui}

1. Använd **Products**-konsolen (via **Commerce**) och navigera till önskad plats.
1. Använd ikonen **Skapa** för att välja antingen (beroende på struktur och plats):

   * **Skapa produkt**
   * **Skapa produktvariation**

   ![Plustyrd ikon för att skapa](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. Guiden öppnas. Använd **Grundläggande** och **Produktflikar** för att ange [produktattributen](/help/commerce/cif-classic/administering/concepts.md#product-attributes) för den nya produkten eller produktvarianten.

   >[!NOTE]
   >
   >**Titel** och **SKU** är det minsta som krävs för att skapa en produkt eller variant.

1. Välj **Skapa** om du vill spara informationen.

>[!NOTE]
>
>Många produkter finns i en rad olika färger och/eller storlekar. Information om basprodukten och relaterade produktvarianter kan båda hanteras från **Products**-konsolen.
>
>Produkterna och deras varianter lagras som en trädstruktur, produktinformationen är högst upp, med varianterna under (den här strukturen används av användargränssnittet).

### Redigera produktinformation {#editing-product-information}

>[!NOTE]
>
>Produktbilder i geometrixx-utomhusbruk kan fås från:
>
>`/etc/commerce/products/...`
>
>Det innebär att de som standard blockeras av [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=sv-SE), så konfigurera som det behövs.

#### Redigera produktinformation - Touchoptimerat gränssnitt {#editing-product-information-touch-optimized-ui}

1. Gå till produktinformationen med **Products**-konsolen (via **Commerce**).
1. Använda antingen:

   * [snabbåtgärder](/help/sites-authoring/basic-handling.md#quick-actions)
   * [markeringsläge](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Välj ikonen **Visa produktdata**:

   ![visa produktdataikon - informationsikon](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. [produktattributen](/help/commerce/cif-classic/administering/concepts.md#product-attributes) visas. Använd **Redigera** och **Klar** om du vill göra några ändringar.

### Visar produktreferenser {#showing-product-references}

#### Visar produktreferenser - Touchoptimerat användargränssnitt {#showing-product-references-touch-optimized-ui}

1. Gå till produktinformationen med **Products**-konsolen (via **Commerce**).
1. Öppna den sekundära listen för referenser med ikonen:

   ![dubbelpil, ikon](/help/sites-administering/do-not-localize/chlimage_1-16.png)

1. Välj önskad produkt - uppdateringarna på den sekundära listen visar vilka referenstyper som är tillgängliga:

   ![produktkonsolen med öppna referenser](/help/sites-administering/assets/chlimage_1-88.png)

1. Klicka på referenstypen (till exempel Produktsidor) för att utöka listan.
1. Välj en specifik referens så att du kan visa alternativen:

   * Navigera till produktsidan
   * Redigera produktsida

   ![Referenspanelen för produktkonsolen](/help/sites-administering/assets/chlimage_1-89.png)

### Sök efter produkter {#search-for-products}

1. Navigera till konsolen **Produkter** via **Commerce**.
1. Öppna den andra listen för sökning med ikonen:

   ![förstoringsglasikon](/help/sites-administering/do-not-localize/chlimage_1-17.png)

1. Du kan söka efter produkter på flera olika sätt. Du kan bara använda en eller flera aspekter för en sökning. De produkter som hittas visas:

   ![Produktdata i produktkonsolen](/help/sites-administering/assets/chlimage_1-90.png)

1. Om du klickar/trycker på en produkt öppnas den. Du kan också publicera den eller visa produktdata.

#### Utöka sökning {#extending-search}

Du kan ändra en befintlig aspekt eller lägga till nya, med CRXDE Lite:

1. Navigera till:

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. Du kan till exempel redigera de storlekar som visas på produktsöksidan. Klicka på noden `sizegroup`.
1. Klicka på noden `items` och sedan på noden `propertypredicate`.
1. Du kan redigera `propertyValues`. Du kan till exempel lägga till XS eller XXL, eller ta bort en storlek.
1. Klicka på **Spara alla** och navigera till produktsöksidan. Ändringarna bör visas.

### Flera Assets {#multiple-assets}

Du kan lägga till flera resurser i produktkomponenten och sedan ange den resurs som du vill ska visas på produktsidan.

>[!NOTE]
>
>Allt som rör flera resurser görs med det pekoptimerade användargränssnittet.

#### Lägga till flera Assets {#adding-multiple-assets}

1. Navigera till konsolen **Produkter** via **Commerce**.
1. Navigera till önskad produkt med **Products**-konsolen.

   >[!NOTE]
   >
   >Du måste vara på produktnivå, inte på variantnivå.

1. Välj ikonen **Visa produktdata** med markeringsläge eller snabbåtgärder.
1. Välj ikonen Redigera.
1. Bläddra till **Lägg till**.

   ![Lägger till skärmbild för produktdata](/help/sites-administering/assets/chlimage_1-91.png)

1. Välj **Lägg till**. En ny platshållare för resursen visas.
1. Om du väljer **Ändra** öppnas en dialogruta där du kan välja en resurs.
1. Välj den resurs som du vill lägga till.

   >[!NOTE]
   >
   >De resurser du kan välja är från [Assets](/help/assets/assets.md).

1. Klicka på ikonen Klar.

Två resurser lagras nu i din produktkomponent. Du kan konfigurera vilken som ska visas på produktsidan. Detta fungerar med ett kategorisystem. Först måste du lägga till en kategori till de enskilda resurserna:

1. Välj **Visa produktdata**.
1. Ange en **tillgångskategori** under resurserna, till exempel `cat1` och `cat2`.

   >[!NOTE]
   >
   >Du kan också använda taggar för kategorier.

1. Klicka på ikonen Klar. Du måste nu [utrulla](#rolling-out-a-catalog) dina ändringar.

Nu har resurserna i produktkomponenten en kategori. Du kan konfigurera vilken kategori som ska visas på tre olika nivåer:

* [Produktsida](#product-page)
* [Katalog](#catalog)
* [Products Console](#products-console)

>[!NOTE]
>
>Om du inte anger kategorier visas den första resursen på produktsidan.

Mekanismen för att välja den bild som ska visas är följande:

1. Kontrollera om en kategori har angetts för produktsidan.
1. Om inte, kontrollerar du om en kategori har angetts för katalogen.
1. Om inte, kontrollerar du om en kategori har angetts för produktkonsolen.

>[!NOTE]
>
>För både katalognivå och produktkonsolnivå måste du implementera ändringarna och se skillnaden på produktsidan.

#### Produktsida {#product-page}

1. Gå till din produktsida.
1. **Redigera** produktkomponenten.
1. Skriv den **bildkategori** som du valde ( `cat1` till exempel).
1. Välj **Klar**. Sidan uppdateras och rätt resurs ska visas.

#### Katalog  {#catalog}

1. Navigera till katalogen.
1. Välj **Visa egenskaper**.
1. Välj **Redigera**.
1. Klicka på fliken **Assets**.
1. Ange den nödvändiga **produktresurskategorin**.
1. Välj **Klar**.
1. [Utlöses](#rolling-out-a-catalog) dina ändringar.

#### Products Console {#products-console}

1. Navigera till önskad produkt med **Products**-konsolen.
1. Välj **Visa produktdata**.
1. Välj **Redigera**.
1. Ange **standardresurskategori**.
1. Välj **Klar**.
1. [Utlöses](#rolling-out-a-catalog) dina ändringar.

### Publicera/avpublicera produktinformation {#publishing-unpublishing-product-information}

#### Publicera/avpublicera produktinformation - Touchoptimerat gränssnitt {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>Produktinformationen publiceras ofta via de sidor som refererar till den. När du publicerar sidan X som refererar till produkten Y, frågar AEM om du även vill publicera produkten Y.
>
>I särskilda fall kan AEM även publicera direkt från produktinformationen.

1. Gå till produktinformationen med **Products**-konsolen (via **Commerce**).
1. Använda antingen:

   * [snabbåtgärder](/help/sites-authoring/basic-handling.md#quick-actions)
   * [markeringsläge](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Välj ikonen **Publish** eller **Avpublicera** efter behov:

   ![världsikon](/help/sites-administering/do-not-localize/chlimage_1-18.png) ![världsikon med ett kors - inget tecken](/help/sites-administering/do-not-localize/chlimage_1-19.png)

   Produktinformationen publiceras eller avpubliceras, beroende på vad som är lämpligt.

<!-- Search&Promote is end of life as of September 1, 2022 ### Product Feed {#product-feed} -->

<!-- Search&Promote is end of life as of September 1, 2022 The Search&Promote integration lets you: -->

<!-- Search&Promote is end of life as of September 1, 2022 * use the eCommerce API, independently of the underlying repository structure and commerce platform. -->
<!-- Search&Promote is end of life as of September 1, 2022 * use the Index Connector feature of Search&Promote to provide a product feed in XML format. -->
<!-- Search&Promote is end of life as of September 1, 2022 * use the Remote Control feature of Search&Promote to perform on-demand or scheduled requests of the product feed -->
<!-- Search&Promote is end of life as of September 1, 2022 * feed generation for different Search&Promote accounts, configured as cloud services configurations. -->

<!-- Search&Promote is end of life as of September 1, 2022 For more information, read [Product Feed](/help/sites-administering/product-feed.md). -->

### Händelsehanterare för produktuppdateringar {#event-handler-for-product-updates}

Det finns en händelsehanterare som loggar en händelse när en produkt läggs till, redigeras eller tas bort och när en produktsida läggs till, redigeras eller tas bort. Det finns följande OSGi-händelser:

* `com/adobe/cq/commerce/pim/PRODUCT_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_DELETED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_DELETED`

För `PRODUCT_*`-händelserna pekar sökvägen till basprodukten i `/etc/commerce/products`. För händelserna `PRODUCT_PAGE_*` pekar sökvägen till noden `cq:Page`.

Du kan titta på dem i webbkonsolen i OSGI-händelser ( `/system/console/events`), till exempel:

![Exempel på OSGI-händelser](/help/sites-administering/do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>Läs även [Händelsehantering i AEM](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/).

### Bild med Lägg till i kundvagnslänkar {#image-with-add-to-cart-links}

Med komponenten Bild med Lägg till i kundvagnslänkar kan du snabbt lägga till en produkt i kundvagnen genom att skapa en aktiveringspunkt länkad till en produkt i en bild.

När du klickar på aktiveringspunkten öppnas en dialogruta där du kan välja storlek och kvantitet för produkten.

1. Navigera till sidan där du vill lägga till komponenten.
1. Dra och släpp komponenten på sidan.
1. Dra och släpp en bild i komponenten från [resursläsaren](/help/sites-authoring/author-environment-tools.md#assets-browser).
1. Du kan antingen:

   * klicka på komponenten och sedan på ikonen Redigera
   * dubbelklicka långsamt

1. Klicka på helskärmsikonen.

   ![helskärmsikon](/help/sites-administering/assets/chlimage_1-92.png)

1. Klicka på ikonen Starta karta.

   ![startmappningsikon](/help/sites-administering/assets/chlimage_1-93.png)

1. Klicka på en av formikonerna.

   ![formikoner](/help/sites-administering/do-not-localize/chlimage_1-21.png)

1. Ändra och flytta formen efter behov.
1. Klicka på formen.
1. Om du klickar på bläddringsikonen öppnas [Resursväljaren](/help/assets/search-assets.md#assetpicker).

   >[!NOTE]
   >
   >Du kan också skriva produktsökvägen som måste finnas på produktnivå, inte på variantnivå, direkt.

   ![textbana](/help/sites-administering/assets/chlimage_1-94.png)

1. Klicka på bekräftelseikonen två gånger och sedan på Avsluta helskärm.
1. Klicka någonstans på sidan bredvid komponenten. Sidan bör uppdateras och följande symbol bör visas på bilden:

   ![plustecken](/help/sites-administering/do-not-localize/chlimage_1-22.png)

1. Växla till [förhandsgranskningsläget](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui).
1. Klicka på hotspot-området +. En dialogruta öppnas där du kan välja storlek och kvantitet för den produkt du angav i **Sökväg**.

   ![produktexempel: poncho](/help/sites-administering/assets/chlimage_1-95.png)

1. Ange en storlek och en kvantitet.
1. Klicka på knappen Lägg till i kundvagnen. Dialogrutan stängs.
1. Gå till kundvagnen. Produkten ska vara här.

#### Konfigurationsalternativ {#configuration-options}

Du kan konfigurera hur dialogrutan ser ut när du klickar på hotspot-området:

1. Klicka på komponenten och klicka på konfigurationsikonen.

   ![konfigurera ikon](/help/sites-administering/assets/chlimage_1-96.png)

1. Rulla ned. Det finns en **ADD TO CART**-flik.

   ![lägg till i kundvagnsfliken](/help/sites-administering/assets/chlimage_1-97.png)

1. Klicka på **LÄGG TILL I KORT**. Det finns tre konfigurationsalternativ som du kan använda.

   ![konfigurationsalternativ](/help/sites-administering/assets/chlimage_1-98.png)

1. Klicka på ikonen Klar.

## Kataloger {#catalogs}

### Skapa en katalog {#generating-a-catalog}

#### Generera en katalog - Touchoptimerat användargränssnitt {#generating-a-catalog-touch-optimized-ui}

>[!NOTE]
>
>Katalogen refererar till dina produktdata.

Så här skapar du en katalog:

1. Öppna webbplatskonsolen (till exempel [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)).
1. Navigera till den plats där du vill skapa sidan.
1. Använd ikonen **Skapa** för att öppna alternativlistan:

   ![create-icon](/help/sites-administering/do-not-localize/chlimage_1-23.png)

1. Välj **Skapa katalog** i listan. Guiden Skapa katalog öppnas.

   ![guiden Skapa katalog](/help/sites-administering/assets/chlimage_1-99.png)

1. Navigera till önskad katalogutkast.
1. Välj knappen **Markera** och klicka på önskad katalogutkast.
1. Välj **Nästa**.

   Guiden ![katalogegenskaper](/help/sites-administering/assets/chlimage_1-100.png)

1. Skriv en **titel** och ett **namn**.
1. Klicka på knappen **Skapa**. Katalogen skapas och en dialogruta öppnas.

   Dialogrutan ![som skapades av katalogen](/help/sites-administering/assets/chlimage_1-101.png)

1. Om du väljer knappen **Klar** återgår du till webbplatskonsolen där du kan se katalogen.

   Om du trycker/klickar på knappen **Öppna katalog** öppnas katalogen (till exempel `http://localhost:4502/editor.html/content/test-catalog.html`).

#### Generera en katalog - Classic UI {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>Katalogen refererar till dina [produktdata](#products-and-product-variants).

1. Använd konsolen **Webbplatser** för att navigera till din **katalogutkast** och sedan till baskatalogen.

   Till exempel:

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. Skapa en sida med mallen **Avsnittsutkast**.

   Exempel: `Swimwear`.

1. Öppna den nya `Swimwear`-sidan och klicka sedan på **Redigera utkast**. Dialogrutan **Egenskaper** öppnas så att du kan ställa in valet **Produkter**.

   Öppna till exempel fältet **Taggar/nyckelord** för att välja Aktivitet och sedan Simma i avsnittet Geometrixx-utomhus.

1. Klicka på **OK** så att dina egenskaper sparas. Exempelprodukter visas under **Produkturvalskriterier** på sidan med utkast.
1. Klicka på **Utrullningsändringar..**, välj **Utrullningssida och alla undersidor** och klicka sedan på **Nästa** och sedan **Utrullning**. När utrullningen är klar visas indikatorn **Status** som grön.
1. Nu kan du klicka på **Stäng** och kontrollera den nya katalogsektionen, till exempel på och under:

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. Klicka på **Redigera utkast** på sidan med utkast och öppna fliken **Genererad sida** i dialogrutan **Egenskaper**. Välj den bild som du vill visa i listfältet Banner, till exempel `summer.jpg`
1. Klicka på **OK** så att dina egenskaper sparas. Banderollinformation visas under **Produkturvalskriterierna** på sidan för utkast.
1. Utför de här nya ändringarna.

### Stänger ut en katalog {#rolling-out-a-catalog}

#### Skapa en katalog - Touchoptimerat användargränssnitt {#rolling-out-a-catalog-touch-optimized-ui}

Så här distribuerar du en katalog:

1. Navigera till konsolen **Kataloger** via **Commerce**.
1. Navigera till den katalog som du vill lansera.
1. Använda antingen:

   * [snabbåtgärder](/help/sites-authoring/basic-handling.md#quick-actions)
   * [markeringsläge](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Markera ikonen **Utrullningsändringar** :

   ![utrullning](/help/sites-administering/do-not-localize/chlimage_1-24.png)

1. I guiden ställer du in utrullningen efter behov och klickar sedan på **Överrullningsändringar**.
1. En dialogruta öppnas. Välj **Klar** när processen är klar.

#### Öppnar en katalog - Classic UI {#rolling-out-a-catalog-classic-ui}

Så här distribuerar du en katalog:

1. Navigera till den katalog som du vill lansera. Till exempel:

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. Klicka på **Utrullningsändringar..**
1. Ställ in utrullningen efter behov.
1. Klicka på **Rollout**.

### Blueprint Importer {#blueprint-importer}

#### Blueprint Importer - pekoptimerat användargränssnitt {#blueprint-importer-touch-optimized-ui}

1. Navigera till konsolen **Kataloger** via **Commerce**.
1. Navigera till den plats där du vill importera katalogdesignen.
1. Välj ikonen **Importera utkast** .

   ![Importera utkast-ikon](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. I guiden väljer du Source efter behov och klickar på **Nästa**.

   ![guide för utkast](/help/sites-administering/assets/chlimage_1-102.png)

1. Välj **Klar** när importen är klar.

#### Blueprint Importer - Classic UI {#blueprint-importer-classic-ui}

1. Navigera till **Commerce** med **verktygskonsolen**.

   Till exempel:

   `http://localhost:4502/miscadmin#/etc/commerce`

1. Öppna **Katalogvisningsimporteraren**.
1. Ställ in importen efter behov.
1. Klicka på **Importera katalogutkast**.

## Erbjudanden {#promotions}

### Skapa en kampanj {#creating-a-promotion}

#### Skapa en kampanj - klassiskt användargränssnitt {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>I följande exempel behandlas en kampanj som hålls direkt i en [kampanj](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md). Den används för verifikationer.
>
>En kampanj kan också finnas i en [upplevelse](/help/sites-authoring/personalization.md) i en kampanj.
>
>Mer information finns i [Kampanjer och kuponger](#promotions-and-vouchers).

1. Öppna konsolen **Webbplatser** för din författarinstans.
1. Välj önskad **kampanj** i den vänstra rutan.
1. Klicka på **Nytt**, välj mallen **Erbjudande** och ange sedan en **titel** (och **namn** om det behövs) för din nya voucher.
1. Klicka på **Skapa**. Den nya kampanjsidan visas i den högra rutan.

1. Redigera **egenskaperna** genom att antingen:

   * öppnar sidan och klickar sedan på knappen Redigera för att öppna dialogrutan Egenskaper
   * markera sidan i webbplatskonsolen och sedan använda snabbmenyn (oftast högerknappen) för att välja **Egenskaper...** och öppna dialogrutan Egenskaper.

   Ange **erbjudandetyp**, **rabatttyp**, **rabattvärde** och eventuella andra fält efter behov.

1. Klicka på **OK** för att spara.

1. Nu kan ni aktivera kampanjen så att kunderna ser den i publiceringsinstansen.

## Vouchers {#vouchers}

### Skapa en voucher {#creating-a-voucher}

#### Skapa en kupong - klassiskt användargränssnitt {#creating-a-voucher-classic-ui}

1. Öppna konsolen **Webbplatser** för din författarinstans.
1. Välj önskad **kampanj** i den vänstra rutan.
1. Klicka på **Nytt**, markera mallen **Voucher** och ange sedan en **titel** (och **namn** om det behövs) för den nya verifikationen.
1. Klicka på **Skapa**. Den nya verifikationssidan visas i den högra rutan.

1. Öppna din nya verifikationssida med ett dubbelklick, klicka sedan på **Redigera** och konfigurera informationen efter behov.
1. Klicka på **OK** för att spara.

1. Nu kan du aktivera din voucher så att kunderna kan använda den i sina kundvagnar i publiceringsinstansen.

### Tar bort Vouchers {#removing-vouchers}

#### Tar bort Vouchers - klassiskt användargränssnitt {#removing-vouchers-classic-ui}

Om du vill att en voucher inte ska vara tillgänglig för kunderna kan du antingen:

* Inaktivera vouchern - den är fortfarande tillgänglig i författarmiljön så att du kan återaktivera den senare.
* Ta bort den helt.

Båda åtgärderna kan utföras från konsolen **Webbplatser**.

### Ändra verifikationer {#modifying-vouchers}

#### Ändra Vouchers - klassiskt användargränssnitt {#modifying-vouchers-classic-ui}

Om du vill ändra egenskaperna för en voucher eller befordran kan du dubbelklicka på den i konsolen **Webbplatser** och klicka på **Redigera**. När du har sparat den bör du aktivera den så att ändringarna överförs till publiceringsinstanserna.

### Lägga till verifikationer i en kundvagn {#adding-vouchers-to-a-cart}

Om du vill tillåta användare att lägga till vouchers i sina kundvagnar kan du använda den inbyggda **Vouchers** -komponenten (Commerce-kategori). Lägg till detta på samma sida som där kundvagnen visas (men detta är inte obligatoriskt). Verifikationskomponenten är bara ett formulär där användaren kan ange en verifikationskod, det är kundvagnskomponenten som faktiskt visar listan över använda verifikationer och deras rabatt.

På demowebbplatsen (Geometrixx Outdoors - engelska) kan du se kupongformuläret på kundvagnssidan, under den faktiska kundvagnen.

## Beställningar {#orders}

>[!NOTE]
>
>Det bör noteras att färdiga AEM inte har åtgärder som krävs för standardfunktioner som rör order, som att returnera varor, uppdatera orderstatus, utföra leveranser och generera följesedlar. Den är främst avsedd som en förhandstitt på teknik.
>
>Det generiska Order Management i AEM har hållits grundläggande. Vilka fält som är tillgängliga i guiden beror på strukturen:
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

1. Använd konsolen **Beställningar** för att navigera till önskad plats.
1. Använd ikonen **Skapa** för att välja **Skapa ordning**.

   ![Plustyrd ikon för att skapa](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. Guiden öppnas. Använd flikarna **Grundläggande**, **Innehåll**, **Betalning** och **Uppfyllelse** för att ange [information om den nya ordern](/help/commerce/cif-classic/administering/concepts.md#order-information).

1. Välj **Skapa** om du vill spara informationen.

### Redigera orderinformation {#editing-order-information}

#### Redigera beställningsinformation - Touchoptimerat gränssnitt {#editing-order-information-touch-optimized-ui}

1. Använd konsolen **Beställningar** för att navigera till ordningen.
1. Använda antingen:

   * [snabbåtgärder](/help/sites-authoring/basic-handling.md#quick-actions)
   * [markeringsläge](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Välj ikonen **Visa orderdata** :

   ![informationsikon](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. [orderinformationen](/help/commerce/cif-classic/administering/concepts.md#order-information) visas. Använd **Redigera** och **Klar** om du vill göra några ändringar.

